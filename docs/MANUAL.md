# Manual de uso

Guía completa de **Registro de Cargas**, pantalla por pantalla.

La app tiene siete pestañas, en la barra inferior: **Hoy** (registrar la sesión), **Rutinas**, **Vídeos**, **Agenda** (calendario de turnos), **Progreso**, **Coach** (el entrenador) y **Perfil**.

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

1. Elige **Gimnasio** o **Casa** arriba a la derecha. Si en la **Agenda** hoy es día de teletrabajo, la app ya propone **Casa**; debajo verás tu turno de hoy.
2. La app marca con **toca hoy** el día que corresponde a hoy y lo deja seleccionado. En fin de semana no marca ninguno; elige el día a mano si entrenas.
   Los días que ya has registrado esta semana (de lunes a domingo) aparecen en **verde** con «✓ hecho», da igual si los hiciste en el gimnasio o en casa. Cada lunes vuelven a quedar en blanco.
3. Debajo de los días aparece **La última vez**: lo que hiciste en la sesión anterior de ese mismo día de rutina (gimnasio o casa), con cada ejercicio, sus series (kg × reps), la sensación, las notas y la energía. Tócalo para plegarlo o desplegarlo; la app recuerda tu elección.
4. Cada ejercicio aparece rellenado:
    - **Series y repeticiones**: las del objetivo del plan. El número gris dentro de la casilla de reps es el objetivo de esa serie.
    - **Peso**: el que usaste la última vez en ese ejercicio y en ese lugar. Si es la primera vez, el del campo «Último peso» del plan.
    - **Antes**: a la izquierda de cada serie, lo que hiciste en esa serie la vez anterior. Se pone en **verde** cuando la superas (más peso, o el mismo peso con más repeticiones), con borde gris si la igualas y en amarillo si estás por debajo.
5. Ajusta con **−** y **+**. El peso cambia de 2,5 en 2,5 kg y las repeticiones de 1 en 1. También puedes escribir directamente; se admite coma decimal.
6. **+ Añadir serie** añade una serie más, copiando el peso de la anterior.
7. Marca la **sensación** de cada ejercicio (Fácil, Bien, Duro, Al fallo) y añade notas si quieres: molestias, agarre, técnica…
8. En **Cómo te has sentido hoy**, marca la energía del 1 al 5, la fecha y las sensaciones generales.
9. Pulsa **Guardar sesión**.

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

### Cambiar el nombre de un ejercicio

Cada ejercicio y cada día tienen un código interno fijo; el nombre es solo una etiqueta. Al editar un ejercicio en **Rutinas** y cambiarle el nombre, elige:

- **Es el mismo ejercicio con otro nombre**: conserva su historial, sus vídeos y sus gráficas.
- **Es otro ejercicio distinto**: empieza de cero (sin «Antes» ni peso de referencia).

Los días también se pueden renombrar sin perder «La última vez». Gimnasio y casa tienen ejercicios separados aunque se llamen igual.

### Calentamiento y estiramientos

Al final de **Rutinas** puedes crear bloques (por ejemplo «Torso» y «Pierna») con su calentamiento y sus estiramientos, cada uno con su cantidad (12 reps, 30 s por lado…), y elegir en qué días de gimnasio y de casa se hacen. Pulsa **Editar** para añadir, quitar o cambiar ejercicios. En **Hoy** aparecen como listas para marcar: el calentamiento antes de los ejercicios y los estiramientos al final. Al guardar la sesión queda registrado cuántos hiciste y el entrenador lo tiene en cuenta.

## 4. Vídeos

Cada ejercicio (salvo el cardio) puede tener uno o varios vídeos. Al añadirlos eliges el tipo: **Mi técnica**, **Referencia del entrenador** o **Corrección**.

Formas de añadir un vídeo:

- **Pegar enlace**: un enlace compartido de Google Fotos, Google Drive, YouTube u otro sitio. Se abre en otra pestaña.
- **Desde Drive** (solo dentro de Claude): busca los vídeos de tu carpeta de Drive y eliges cuál corresponde al ejercicio.
- **Subir archivo** (solo dentro de Claude): MP4 o WebM de hasta 20 MB. Se reproduce dentro de la app.

Los vídeos aparecen también en **Hoy**, bajo cada ejercicio, para consultarlos mientras entrenas.

Los vídeos de **Gimnasio** y de **Casa** van por separado, aunque el ejercicio se llame igual: cambia de apartado arriba a la derecha.

## 5. Calendario (Agenda)

La pestaña **Agenda** muestra el mes completo, de lunes a domingo, con tu turno de trabajo, los días de teletrabajo, las vacaciones, los pesajes y el día de rutina que toca. Con **‹** y **›** pasas de mes para planificar con antelación; **Hoy** vuelve al mes actual. Al cambiar de mes, la app lee de Google Calendar los días que aún no tenía.

- **Leyenda**:
    - **M1, M2…** (azul): turno de mañana. **T1…** (naranja): turno de tarde. Si el evento no lleva código, aparece solo **M** o **T**.
    - **Casa**: teletrabajo. Ese día la app propone entrenar en casa con la rutina de casa.
    - **Vac.** (morado): vacaciones. **L**: día libre.
    - **Pes.**: pesaje (revisión de composición corporal).
    - **D1, D2…**: día de rutina que toca. **✓**: ya registraste una sesión ese día.
- **Sincronizar con Google Calendar** (solo dentro de Claude):
    - La app lee los eventos de tu calendario cuyo título incluye «mañana», «tarde», un código de turno como **M1** o **T1**, «teletrabajo», «vacaciones», «día libre» o «festivo».
    - También lee los **pesajes**: eventos cuyo título incluye «pesaje», «EVOLT», «báscula» o «composición corporal». Ese día, **Hoy** te recuerda apuntar la medición, y **Progreso** muestra cuántos días faltan para el próximo.
    - Sirven eventos de día completo y eventos con hora que abarcan varios días, como «Semana de tarde» de lunes a viernes.
    - **Elegir calendarios** permite leer también otros calendarios tuyos.
    - Se sincroniza sola al abrir la app (si ya diste permiso y han pasado más de 6 horas) y al abrir la Agenda (si han pasado más de 3).
- **Corregir un día**: toca el día, elige el turno correcto y pulsa **Guardar día**. **Aplicar de lunes a viernes** lo aplica a toda esa semana. Vuelve a **Automático** para quitar el ajuste.
- **Aplicar a un rango de fechas**: elige «Desde», «Hasta» y qué marcar (un turno, teletrabajo, **Vacaciones** o libre). Con «Solo de lunes a viernes» se saltan los fines de semana. Sirve para meter de una vez tus vacaciones o varias semanas del mismo turno (hasta dos meses por vez).
- **Añadir también a Google Calendar** (solo dentro de Claude): con esta casilla marcada, al guardar un día o una semana la app crea en tu calendario principal un evento por día con el horario del turno (por ejemplo «Turno de mañana M1», de 08:00 a 17:00; «Teletrabajo · Turno de mañana M2»; «Día libre»). Si después cambias o quitas ese ajuste, la app borra el evento que creó ella y, si toca, crea el nuevo. Nunca borra eventos que hayas creado tú.
- **Tus turnos** (al final de la Agenda): define cada código con su horario, por ejemplo **M1** de 08:00 a 17:00. Con eso la app y el entrenador saben a qué hora trabajas cada día. **Turno por defecto en teletrabajo** se aplica cuando un día de teletrabajo no lleva código.
- **Versión de GitHub**: no se conecta a Google Calendar. Marca los turnos a mano con **Corregir este día** y **Aplicar de lunes a viernes**.

## 6. Progreso

### Objetivos

- **Editar** permite fijar un objetivo de **peso**, de **% de grasa** y de **masa muscular**, una **fecha objetivo** opcional y la **fuente** con la que medir (por ejemplo, solo la báscula del gimnasio).
- Al editar, la app calcula tu **masa magra** (peso sin grasa) y qué pesarías con distintos % de grasa si la mantienes. Sirve para fijar un peso objetivo coherente con el % de grasa.
- Cada objetivo muestra:
    - el valor actual, el objetivo y lo que falta;
    - una barra con el % del camino recorrido desde tu primera medición;
    - el **ritmo** de los últimos 120 días (por mes) y la **fecha estimada** a la que llegarías a ese ritmo;
    - con fecha objetivo, el ritmo que necesitas y si vas **En ritmo** o **Por detrás**.
- **Pedir propuesta al entrenador** le pide objetivos realistas con plazo a partir de tus mediciones.

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
    4. **Desde el móvil, dentro de Claude** (recomendado): comparte con Google Drive los dos CSV (`step_daily_trend` y `health.nutrition`; el ZIP completo suele pasar de 10 MB, el máximo que se puede descargar desde Drive) y guárdalos en la carpeta de importaciones de la app. Después pulsa **Buscar en Drive**, marca los archivos y pulsa **Importar seleccionados**. Así no dependes del selector de archivos del móvil.
- **Apuntar un día a mano**: para días sueltos o si usas otra app de nutrición.

### Cargas por ejercicio

- Elige un ejercicio y una métrica:
    - **Carga máx.**: el mayor peso de la sesión.
    - **1RM est.**: la estimación de tu máximo a una repetición.
    - **Volumen**: kg × reps de todas las series.
- Debajo aparecen las últimas 8 sesiones de ese ejercicio.

### Pulso de la sesión

Después de entrenar, en **Progreso** aparece «¿Añades el pulso de tu sesión?» (y en cada sesión, «Añadir pulso del reloj»). Sube la captura de la gráfica de pulso de tu reloj y escribe en la nota qué tramo fue pesas y cuál cardio (por ejemplo «del minuto 0 al 55 pesas, del 55 al 80 cinta»). La app calcula pulso medio y máximo, tiempo en zonas, intensidad de las pesas y del cardio, y una valoración. Si no hay entrenador IA, puedes poner los números a mano. El entrenador lo usa para valorar la intensidad y la recuperación, y el Excel de la copia tiene una hoja «Pulso».

### Sesiones

Muestra el historial completo. Toca una sesión para ver el detalle o borrarla.

## 6 bis. EVOLT

Tu hoja de resultados de la báscula EVOLT 360, explicada:

- **Arriba**: puntuación BWI (8-8,9 óptimo, 9-10 atlético), edad biológica y las cuatro cifras clave (peso, % de grasa, músculo esquelético y nivel de grasa visceral) con el cambio desde el escaneo anterior.
- **En resumen**: cuántos valores están en rango, qué ha cambiado y qué zonas se salen del rango.
- **Músculo y Grasa**: cada dato con una explicación de una línea y una barra que marca tu rango óptimo (verde) y dónde estás tú.
- **Por zonas**: músculo y grasa de brazos, tronco y piernas, y si estás equilibrado entre lado izquierdo y derecho.
- **Agua, Energía y comida, Cintura**: agua dentro y fuera de las células, gasto en reposo y total, y lo que EVOLT te recomienda comer frente a tus objetivos del Perfil.

**Importar**: guarda el PDF en tu carpeta de Google Drive y pulsa «Buscar en Drive», o usa «Importar PDF» desde el dispositivo. Cada escaneo también añade una medición a **Progreso** (fuente EVOLT). Pulsa «Pregunta al entrenador por este escaneo» para que te lo comente.

## 7. Entrenador

- Escribe una pregunta o usa una de las sugerencias.
- El entrenador recibe en cada pregunta tus datos actuales: perfil, fase, objetivos de nutrición y de composición corporal, notas, rutinas, últimas sesiones, mediciones, nutrición, tu horario de trabajo de las próximas dos semanas (con el horario de cada turno) y la fecha del próximo pesaje.
- **Qué recuerda**:
    - **Notas generales del Perfil**: siempre, hasta que las quites. Es el sitio para lo que debe tener en cuenta a largo plazo (una lesión, una época de mucho trabajo).
    - **Sensaciones y energía de cada sesión**: mientras esa sesión esté entre las 15 últimas.
    - **Lo que le dices en el chat**: solo mientras siga entre los últimos 20 mensajes, y se borra con **Nueva conversación**.
- El botón de la **bombilla** abre una lista de preguntas sugeridas; al tocar una, se envía.
- El botón de la **imagen** adjunta capturas o fotos (por ejemplo, el registro de agua o de comidas de Samsung Health, o una foto de tu plato). El entrenador lee los datos que aparezcan y los valora frente a tus objetivos; en fotos de comida, estima raciones y macros. También puedes pegar una captura directamente en el cuadro de texto. Las imágenes no se guardan: solo queda la nota de que adjuntaste una.
- **Parar** corta una respuesta larga.
- **Nueva conversación** borra el historial del chat. Tus datos no se tocan.
- No sustituye a un profesional sanitario. Ante dolor o síntomas, para y consulta.

## 8. Perfil

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

## 9. Instalar en el móvil

### Versión de GitHub (se instala como una app)

1. En el móvil Android, abre la dirección de GitHub Pages en **Chrome**.
2. Toca el menú **⋮** y elige **Instalar aplicación** (en algunos móviles aparece como **Añadir a pantalla de inicio → Instalar**).
3. La app aparece en el cajón de aplicaciones y en la pantalla de inicio con su propio icono. Se abre a pantalla completa, sin barra del navegador, y funciona sin conexión salvo el entrenador.

En iPhone: abre la dirección en Safari, toca **Compartir** y elige **Añadir a pantalla de inicio**.

### Dentro de Claude (con tus datos de Claude)

Abre la app desde la app de Claude, o abre su enlace en Chrome con tu cuenta de claude.ai iniciada y usa **⋮ → Añadir a pantalla de inicio**. Este acceso directo abre la app en Chrome; no es una app instalada.

Las dos versiones guardan sus datos por separado. Para pasar tus datos de una a otra, usa la copia de seguridad (JSON).

## 10. Preguntas frecuentes

**No me marca el día que toca.** Comprueba que tu rutina tiene al menos tantos días como el día de la semana actual. Un jueves necesita un día 4.

**El peso propuesto no es el de la última vez.** Pasa si cambiaste el nombre del ejercicio o si la última vez lo hiciste en el otro lugar (gimnasio o casa).

**No aparece «Subir peso».** Necesitas completar todas las series con al menos las repeticiones objetivo y marcar la sensación como Fácil o Bien.

**He perdido los datos (versión independiente).** Los datos viven en el navegador. Si borraste los datos de navegación, solo se recuperan importando una copia de seguridad.
