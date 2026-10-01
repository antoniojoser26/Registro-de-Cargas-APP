# Funcionamiento interno

Cómo está construida **Registro de Cargas**, qué guarda y, sobre todo, **qué campos modifican a qué otros campos**. Está pensado para quien quiera entender la app a fondo, adaptarla o llevar sus datos a otra aplicación.

## 1. Arquitectura

- **Un único archivo**, `index.html`, con HTML, CSS y JavaScript sin frameworks.
- **Única dependencia externa**: [JSZip](https://stuk.github.io/jszip/), cargada desde cdnjs, para leer el ZIP de Samsung Health y crear el ZIP de exportación.
- **Dos modos de funcionamiento**, que la app detecta sola al arrancar:

| | Dentro de Claude (artifact) | Independiente (GitHub Pages / local) |
|---|---|---|
| Almacenamiento | Base de datos privada del artifact | `localStorage` del navegador (clave `rc.db`) |
| Entrenador IA | Claude, con la cuenta del usuario | API de Anthropic con la clave del usuario |
| Vídeos | Enlace, Google Drive o archivo subido | Solo enlace |
| Exportar registros | A una carpeta de Google Drive | ZIP descargado |
| Calendario de turnos | Google Calendar + ajustes manuales | Solo ajustes manuales |
| Copia de seguridad | Importar | Exportar e importar |

En modo independiente, la capa de almacenamiento imita la misma interfaz (`collection`, `doc`, `set`, `onSnapshot`…). El resto del código es idéntico en los dos modos.

## 2. Modelo de datos

Los datos son documentos JSON organizados por colecciones:

| Ruta | Contenido |
|---|---|
| `profile/main` | Perfil: `name`, `height` (cm), `goal` (fase), `gym`, `trainer`, `equipment`, `macros[]`, `notes[]`, `reminders[]`, `rest[]` (tabla de descansos, opcional), `tower[]` (torre de pesos, opcional), `shifts` → `{list: [{code, start, end}], teleDefault}`, `goals` → `{weight, fat, muscle, date, source}` |
| `plan/gym`, `plan/home` | Rutinas: `title`, `subtitle`, `days[]` → `{name, ex[]}` → `{n, t, last, note, tip, prog}` |
| `logs/<id>` | Una sesión: `date`, `place` (`gym`/`home`), `day`, `energy` (1-5), `note`, `createdAt`, `entries[]` |
| `body/<id>` | Una medición: `date`, `weight`, `fat`, `muscle`, `source`, `note` |
| `daily/<AAAA-MM-DD>` | Un día de nutrición y actividad: `steps`, `kcal`, `protein`, `fat`, `carbs`, `source` |
| `videos/<lugar>--<nombre-normalizado>` | Vídeos de un ejercicio en un lugar (`gym` o `home`): `n`, `items[]` → `{id, kind, label, url, fileId, asset, title, addedAt}` |
| `chat/main` | Últimos 40 mensajes del entrenador |
| `calendar/main` | Última sincronización con Google Calendar: `syncedAt`, `calendars[]`, `calNames`, `from`, `to`, `days` → `{AAAA-MM-DD: {shift: "M"/"T"/"N"/null, code: "M1"…/null, tele, off, weigh, titles[]}}` |
| `calendar/gcal` | Eventos creados por la app en Google Calendar: `days` → `{AAAA-MM-DD: idDelEvento}`. Solo esos se borran o sustituyen al cambiar un ajuste. |
| `calendar/overrides` | Ajustes manuales por día: `days` → `{AAAA-MM-DD: {shift, tele, off}}`. Se conservan los de los últimos 60 días en adelante. |

**Campos de un ejercicio del plan:**

| Campo | Significado |
|---|---|
| `n` | Nombre del ejercicio |
| `t` | Objetivo, por ejemplo `3 series (12-10-8)` |
| `last` | Último peso registrado, por ejemplo `27,5kg / 25kg por lado` |
| `note` | Notas del plan |
| `tip` | Indicaciones de técnica |
| `prog` | Progresión: `Mantener`, `Sí, subir` o `N/A` |

**Entrada de una sesión (`entries[]`):**

- **Fuerza**: `{n, sets: [{kg, reps, tgt}], feel, note}`. `tgt` son las reps objetivo de esa serie.
- **Cardio**: `{n, cardio: true, min, detail, feel, note}`.

## 3. Mapa de dependencias: qué modifica a qué

### 3.1 Al guardar una sesión

| Lo que haces | Lo que cambia automáticamente |
|---|---|
| Guardar sesión | Se crea un documento en `logs`. |
| … con pesos en un ejercicio | El campo **Último peso** (`last`) de ese ejercicio en el plan pasa a ser los pesos distintos de la sesión, unidos con « / » y con el sufijo «por lado» o «total» que tuviera antes. |
| … completando todas las series ≥ reps objetivo **y** con sensación Fácil o Bien | **Progresión** (`prog`) pasa a «Sí, subir». |
| … en cualquier otro caso | **Progresión** pasa a «Mantener». |
| … en un ejercicio con progresión «N/A» | La progresión no se toca nunca. |
| … en cualquier caso | La sesión aparece en **Progreso** (gráficas por ejercicio e historial), sirve para rellenar la próxima sesión y la ve el entrenador. |

### 3.2 Al rellenar una sesión (lectura)

| Dato propuesto | De dónde sale |
|---|---|
| Día marcado «toca hoy» | El día de la semana de hoy: lunes = 1.º día del plan … viernes = 5.º. Sábado y domingo no marcan ninguno. |
| Número de series y reps objetivo | Campo **Objetivo** del plan: el número antes de «series» y los números entre paréntesis separados por guiones. Si no hay paréntesis, se proponen 3 series sin reps. |
| Peso de cada serie | 1) Las series de la **última sesión del mismo ejercicio en el mismo lugar**. 2) Si no hay, los números seguidos de «kg» del campo **Último peso**. |
| Unidad mostrada (kg, kg por lado, kg total) | El texto del campo **Último peso**. |
| Modo cardio (minutos en vez de series) | El nombre del ejercicio contiene «Cardio». |
| Minutos de cardio por defecto | El número del campo **Objetivo** (por ejemplo `30min`). |

### 3.3 El nombre del ejercicio es la clave

| Usa el nombre exacto | Efecto si lo renombras |
|---|---|
| Historial y gráficas de Progreso | Las sesiones antiguas quedan con el nombre viejo, en una gráfica aparte. |
| Peso propuesto al registrar | Se pierde la referencia a la última sesión hasta que registres una con el nombre nuevo. |
| Vídeos (nombre sin tildes ni mayúsculas) | Los vídeos se quedan con el nombre viejo. |

El **nombre del día** se copia en cada sesión al guardarla. Renombrar un día no cambia las sesiones ya guardadas.

### 3.4 Perfil

| Campo | Lo usan |
|---|---|
| Altura | El IMC de todas las mediciones, tanto en las cifras como en las exportaciones. |
| Fase | La cabecera del Perfil y del Entrenador, y el enfoque del entrenador. Al cambiarla se abre la edición de objetivos. |
| Objetivos de nutrición | Las barras de **Nutrición y actividad**, el cálculo de g/kg de proteína, las sugerencias y el contexto del entrenador. |
| Notas y recordatorios | El contexto del entrenador. |
| Gimnasio, entrenador y material | El contexto del entrenador. |

**Cómo se leen los objetivos de nutrición.** Se extraen los números del texto, ignorando los puntos de miles. Si hay dos números (un rango, como `1.700 - 1.800 kcal`), la barra se mide contra el **mayor**. Se busca cada macro por su nombre: «calor», «prote», «grasa» e «hidrat».

### 3.5 Progreso

| Cifra | Cálculo |
|---|---|
| IMC | peso ÷ (altura en m)² |
| Diferencias de composición | Última medición − primera medición, de todas las fuentes. Verde si bajan peso, grasa o IMC, o si sube el músculo. |
| Filtro de fuente | Solo afecta a la gráfica. |
| Carga máx. | Mayor kg de la sesión en ese ejercicio. |
| 1RM estimado | Fórmula de Epley sobre la mejor serie: kg × (1 + reps ÷ 30). |
| Volumen | Suma de kg × reps de todas las series. |
| Medias de nutrición | Media de los días con dato dentro de los últimos 7 días; los días sin dato no cuentan. |
| Objetivos: progreso | (actual − primera medición) ÷ (objetivo − primera medición), entre 0 y 100 %. Solo con mediciones de la fuente elegida, si hay una. |
| Objetivos: ritmo | Pendiente de una regresión lineal sobre las mediciones de los últimos 120 días (al menos 2 mediciones separadas 7 días o más), expresada por mes (× 30). |
| Objetivos: fecha estimada | Hoy + (objetivo − actual) ÷ ritmo diario, solo si el ritmo va en la dirección del objetivo. |
| Objetivos: «En ritmo» | Con fecha objetivo: el ritmo actual es al menos el 90 % del ritmo necesario (objetivo − actual) ÷ días que faltan. |
| Masa magra | peso × (1 − % grasa ÷ 100). Peso equivalente a un % de grasa: masa magra ÷ (1 − % ÷ 100). |

### 3.6 Importación de Samsung Health

- **Archivos leídos**:
    - `*step_daily_trend*.csv`, o `*pedometer_day_summary*.csv` si no hay el anterior: pasos.
    - `*health.nutrition*.csv`: comidas.
- **Formato**: se salta la primera línea de metadatos y los nombres de columna se leen sin el prefijo `com.samsung…`.
- **Pasos**: el máximo registrado ese día (`count` o `step_count`).
- **Nutrición**: suma de las comidas del día (`calorie`, `protein`, `total_fat`, `carbohydrate`), redondeada.
- **Rango**: solo los últimos 120 días.
- **Días repetidos**: un día ya existente se actualiza. Los campos importados sustituyen a los anteriores y los demás se conservan.

### 3.7 Entrenador

En cada pregunta se envía:

1. Las instrucciones del entrenador.
2. Un resumen con: fecha y día que toca, perfil, objetivos, descansos, notas, recordatorios, mediciones, las dos rutinas completas, las **últimas 15 sesiones**, el **horario de trabajo** de 3 días atrás a 13 días adelante y los **últimos 14 días** de nutrición.
3. Los **últimos 20 mensajes** de la conversación.

El entrenador no tiene más memoria que esa. Se guardan los últimos 40 mensajes.

### 3.8 Calendario de turnos

| Paso | Regla |
|---|---|
| Pesajes | Título con «pesaje», «EVOLT», «báscula» o «composición corporal» → **pesaje** (`weigh`). Un evento de pesaje no cambia el turno de ese día. |
| Qué eventos cuentan | Título con «tarde» → turno **T**; «mañana» → turno **M**; «noche» → turno **N**. Un código como `M1`, `T1` o `N2` (letra seguida de un número) se guarda como `code`; si no hay palabra, la letra del código da el turno, y si el código contradice la palabra, se ignora. «teletrabajo», «remoto», «home office» o «desde casa» → **teletrabajo**. «vacaciones», «día libre», «libranza», «festivo» o «baja» → **libre**. Los demás eventos se ignoran. |
| Turno por defecto en teletrabajo | Si un día es de teletrabajo y no tiene código, se le asigna `shifts.teleDefault` (si coincide con el tipo de turno, cuando lo hay). |
| Horario de cada turno | `shifts.list` asigna a cada código su hora de entrada y salida. Se muestra en Hoy, en la Agenda y se envía al entrenador. |
| Qué días cubre un evento | De día completo: del inicio al día anterior a su fin. Con hora: del día de inicio al día en que termina, salvo que termine a las 00:00. |
| Calendarios leídos | Los elegidos en «Elegir calendarios» (por defecto, el principal). |
| Ajuste manual | Sustituye por completo al dato de Google Calendar en ese día. «Automático» lo quita. |
| Efecto en **Hoy** | Si hoy es teletrabajo, el lugar propuesto es **Casa**; si no, **Gimnasio**. Elegir el lugar a mano manda sobre la propuesta. |
| Efecto en el entrenador | Recibe la lista de turnos con su horario, el turno y el lugar sugerido de cada día con datos (de 3 días atrás a 13 adelante) y la fecha del próximo pesaje. |
| Rango leído | De 14 días atrás a 60 días adelante. |
| Día de rutina | No cambia: sigue dependiendo del día de la semana (lunes = día 1…). El calendario solo decide gimnasio o casa. |

## 4. Formatos de exportación

La exportación genera estos archivos. CSV con coma como separador, punto decimal, UTF-8 y fechas `AAAA-MM-DD`.

| Archivo | Columnas |
|---|---|
| `series.csv` | fecha, lugar, dia, ejercicio, serie, kg, reps, reps_objetivo, sensacion, nota_ejercicio, energia_sesion, nota_sesion, id_sesion |
| `cardio.csv` | fecha, lugar, dia, ejercicio, minutos, detalle, sensacion, nota, id_sesion |
| `composicion_corporal.csv` | fecha, peso_kg, grasa_pct, musculo_kg, imc, fuente, nota |
| `nutricion_y_pasos.csv` | fecha, pasos, kcal, proteina_g, grasa_g, hidratos_g, fuente |
| `rutinas.csv` | rutina, dia, orden, ejercicio, objetivo, ultimo_peso, notas, tecnica, progresion |
| `copia_completa.json` | Copia de seguridad completa (ver abajo) |

`series.csv` tiene **una fila por serie**. Agrupando por `id_sesion` se reconstruye cada sesión.

### Copia de seguridad (JSON)

```json
{
  "app": "registro-de-cargas",
  "version": 1,
  "exportedAt": "2026-10-01T12:00:00.000Z",
  "docs": {
    "profile/main": { "...": "..." },
    "plan/gym": { "...": "..." },
    "logs/abc123": { "...": "..." }
  }
}
```

Cada clave de `docs` es la ruta del documento, y su valor es el documento tal cual. Al importar, cada documento sustituye al que tenga la misma ruta; los demás se conservan. Los vídeos subidos como archivo no se incluyen, solo los enlaces.

En `ejemplos/copia-ejemplo.json` hay una copia de ejemplo con una rutina genérica, para probar la app sin escribir nada.

## 5. Privacidad

- **Modo independiente**: nada sale del navegador, salvo las preguntas al entrenador, que van a `api.anthropic.com` con la clave del usuario.
- **Clave de la API**: se guarda en `localStorage` (`rc.apikey`) y nunca se incluye en las exportaciones.
- **Dentro de Claude**: los datos viven en la base de datos privada del artifact, que solo ve su propietario mientras no lo comparta.
