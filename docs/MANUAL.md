# Manual de uso

Guía completa de **Registro de Cargas**, pantalla por pantalla.

La app tiene seis pestañas, en la barra inferior: **Registrar**, **Rutinas**, **Vídeos**, **Progreso**, **Entrenador** y **Perfil**.

## 1. Primeros pasos

1. Abre la app. Si es la primera vez, la pestaña **Perfil** te pide crear tu perfil: nombre, altura, fase y gimnasio (opcional).
2. Ve a **Rutinas** y crea tus días con **+ Añadir día**. El orden importa: el día 1 es el lunes, el 2 el martes… y el 5 el viernes.
3. Dentro de cada día, añade ejercicios con **+ Añadir ejercicio** y rellena:
    - **Objetivo**: con el formato `3 series (12-10-8)`. La app saca de aquí cuántas series y cuántas repeticiones esperas en cada una.
    - **Último peso**: por ejemplo `40kg / 35kg por lado`. Se usa para rellenar la primera sesión.
    - **Notas del plan** e **Indicaciones de técnica**: aparecen al registrar.
4. En **Perfil**, rellena tus **objetivos de nutrición**.
5. Si usas la versión independiente (GitHub), pega tu clave de la API de Anthropic en **Perfil → Entrenador IA** para usar el entrenador.

## 2. Registrar una sesión

1. Elige **Gimnasio** o **Casa** arriba a la derecha.
2. La app marca con **toca hoy** el día que corresponde a hoy y lo deja seleccionado. En fin de semana no marca ninguno; elige el día a mano si entrenas.
3. Cada ejercicio aparece rellenado:
    - **Series y repeticiones**: las del objetivo del plan. El número gris dentro de la casilla de reps es el objetivo de esa serie.
    - **Peso**: el que usaste la última vez en ese ejercicio y en ese lugar. Si es la primera vez, el del campo «Último peso» del plan.
4. Ajusta con **−** y **+**. El peso cambia de 2,5 en 2,5 kg y las repeticiones de 1 en 1. También puedes escribir directamente; se admite coma decimal.
5. **+ Añadir serie** añade una serie más, copiando el peso de la anterior.
6. Marca la **sensación** de cada ejercicio (Fácil, Bien, Duro, Al fallo) y añade notas si quieres: molestias, agarre, técnica…
7. En **Cómo te has sentido hoy**, marca la energía del 1 al 5, la fecha y las sensaciones generales.
8. Pulsa **Guardar sesión**.

Más detalles:

- **Cardio.** Cualquier ejercicio cuyo nombre contenga «Cardio» se registra con minutos (pasos de 5) y un campo de velocidad o inclinación, en lugar de series.
- **Borrador.** Lo que vas apuntando se guarda en tu dispositivo aunque cierres la app. **Reiniciar** lo descarta. Cambiar de día también empieza un borrador nuevo.
- **Qué se guarda.** Los ejercicios que dejes sin ningún dato no se guardan.

## 3. Rutinas

- **Editar** un ejercicio permite cambiar todos sus campos o quitarlo.
- **¿Subir peso la próxima semana?** puede valer:
    - **Mantener** o **Sí, subir**: la app lo actualiza sola al guardar sesiones (ver «Funcionamiento interno»).
    - **N/A**: la app no lo toca nunca. Úsalo para cardio, abdominales y ejercicios con peso corporal.
- **Renombrar** cambia el nombre de un día. **Quitar día** lo elimina junto con sus ejercicios; las sesiones ya guardadas no se borran.
- **Cuidado al renombrar un ejercicio.** El nombre es lo que une el ejercicio con su historial, sus gráficas y sus vídeos. Si lo cambias, las sesiones antiguas siguen con el nombre viejo.

## 4. Vídeos

Cada ejercicio (salvo el cardio) puede tener uno o varios vídeos. Al añadirlos eliges el tipo: **Mi técnica**, **Referencia del entrenador** o **Corrección**.

Formas de añadir un vídeo:

- **Pegar enlace**: un enlace compartido de Google Fotos, Google Drive, YouTube u otro sitio. Se abre en otra pestaña.
- **Desde Drive** (solo dentro de Claude): busca los vídeos de tu carpeta de Drive y eliges cuál corresponde al ejercicio.
- **Subir archivo** (solo dentro de Claude): MP4 o WebM de hasta 20 MB. Se reproduce dentro de la app.

Los vídeos aparecen también en **Registrar**, bajo cada ejercicio, para consultarlos mientras entrenas.

Si el gimnasio y la casa tienen un ejercicio con el mismo nombre, comparten vídeos.

## 5. Progreso

### Composición corporal

- **Las cuatro cifras de arriba** (peso, % grasa, músculo, IMC) son las de la última medición. Debajo de cada una aparece la diferencia con la primera: en verde si va en la buena dirección y en rojo si no.
- **Gráfica**: elige la métrica. Los chips de fuente filtran por báscula o reloj, porque cada aparato mide distinto. Compara tendencias dentro de una misma fuente.
- **Añadir medición**: fecha, peso, % de grasa, masa muscular, fuente y notas. El IMC se calcula solo con tu altura del Perfil.

### Nutrición y actividad

- **Barras**: media de los últimos 7 días de calorías, proteína, grasas e hidratos frente a tus objetivos del Perfil. La barra se vuelve naranja si la media supera el objetivo en más de un 5 %.
- **Gráfica**: calorías, proteína o pasos de los últimos 45 días.
- **Importar desde Samsung Health**:
    1. En Samsung Health: menú ⋮ → **Ajustes** → **Descargar datos personales**.
    2. Comprime la carpeta que se crea en **Mis archivos → Descargas → Samsung Health**.
    3. Elige el ZIP en la app. También puedes elegir solo los CSV `step_daily_trend` y `health.nutrition`.
- **Apuntar un día a mano**: para días sueltos o si usas otra app de nutrición.

### Cargas por ejercicio

- Elige un ejercicio y una métrica:
    - **Carga máx.**: el mayor peso de la sesión.
    - **1RM est.**: la estimación de tu máximo a una repetición.
    - **Volumen**: kg × reps de todas las series.
- Debajo aparecen las últimas 8 sesiones de ese ejercicio.

### Sesiones

Muestra el historial completo. Toca una sesión para ver el detalle o borrarla.

## 6. Entrenador

- Escribe una pregunta o usa una de las sugerencias.
- El entrenador recibe en cada pregunta tus datos actuales: perfil, fase, objetivos, notas, rutinas, últimas sesiones, mediciones y nutrición.
- **Parar** corta una respuesta larga.
- **Nueva conversación** borra el historial del chat. Tus datos no se tocan.
- No sustituye a un profesional sanitario. Ante dolor o síntomas, para y consulta.

## 7. Perfil

- **Editar datos y fase**: nombre, altura, fase (recomposición, definición, mantenimiento, volumen), gimnasio, entrenador y material de casa. Al cambiar de fase se abren los objetivos de nutrición para que los revises.
- **Objetivos de nutrición**:
    - Escribe cada objetivo como texto, por ejemplo `1.700 - 1.800 kcal`, `140 g` o `~170 g`.
    - **Pedir propuesta al entrenador** le pide unas cifras para tu fase.
    - Debajo verás cuántos g/kg de proteína supone tu objetivo con tu último peso.
- **Notas generales**:
    - Toca el estado para alternar entre Pendiente y Resuelto.
    - **Quitar** borra una nota y **Quitar resueltas** borra todas las resueltas.
- **Recordatorios**: **Completado · quitar** los elimina.
- **Exportar registros**: CSV de todo tu historial. Dentro de Claude va a tu carpeta de Drive; en la versión independiente se descarga un ZIP.
- **Copia de seguridad** (JSON): exportar e importar todos los datos.

## 8. Instalar en el móvil

- **Dentro de Claude**: abre la app desde la app de Claude o desde claude.ai en el navegador del móvil.
- **Versión de GitHub**: abre la dirección de GitHub Pages en el navegador del móvil y elige **Añadir a pantalla de inicio**.

## 9. Preguntas frecuentes

**No me marca el día que toca.** Comprueba que tu rutina tiene al menos tantos días como el día de la semana actual. Un jueves necesita un día 4.

**El peso propuesto no es el de la última vez.** Pasa si cambiaste el nombre del ejercicio o si la última vez lo hiciste en el otro lugar (gimnasio o casa).

**No aparece «Subir peso».** Necesitas completar todas las series con al menos las repeticiones objetivo y marcar la sensación como Fácil o Bien.

**He perdido los datos (versión independiente).** Los datos viven en el navegador. Si borraste los datos de navegación, solo se recuperan importando una copia de seguridad.
