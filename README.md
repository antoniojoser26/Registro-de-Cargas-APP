# Registro de Cargas

Aplicación web para registrar entrenamientos de fuerza, seguir la composición corporal y la nutrición, y consultar a un entrenador personal con IA que conoce todos tus datos.

Es un único archivo HTML, sin servidor ni instalación. Funciona en el móvil y en el ordenador, y se puede añadir a la pantalla de inicio como si fuera una app.

**Pruébala:** https://antoniojoser26.github.io/Registro-de-Cargas-APP/ (si GitHub Pages está activado en este repositorio).

## Documentación

| Documento | Contenido |
|---|---|
| [Manual de uso](docs/MANUAL.md) | Cómo usar cada pantalla, paso a paso, y preguntas frecuentes |
| [Funcionamiento interno](docs/FUNCIONAMIENTO.md) | Arquitectura, modelo de datos, qué campos modifican a cuáles y formatos de exportación |
| [Copia de ejemplo](ejemplos/copia-ejemplo.json) | Rutina y datos genéricos para probar la app: **Perfil → Copia de seguridad → Importar** |

## Estructura del repositorio

```
index.html              La app completa
manifest.webmanifest    Datos para instalarla en el móvil
icon.svg, icon-*.png     Iconos
sw.js                   Service worker: instalación y uso sin conexión
docs/MANUAL.md          Manual de uso
docs/FUNCIONAMIENTO.md  Funcionamiento interno y modelo de datos
ejemplos/               Copia de seguridad de ejemplo
```

## Qué hace

- **Hoy (registrar).** Te propone el día de rutina que toca según el día de la semana (lunes = Día 1 … viernes = Día 5). Cada ejercicio viene rellenado con tus series, repeticiones y el peso de la última vez. Apuntas sensaciones por ejercicio (Fácil, Bien, Duro, Al fallo), la energía del día y notas.
- **Progresión automática.** Si completas todas las repeticiones objetivo con sensación Fácil o Bien, el ejercicio se marca como «Subir peso» (doble progresión).
- **Rutinas.** Dos planes, gimnasio y casa. Puedes crear días y ejercicios y editarlos.
- **Vídeos.** Cada ejercicio admite enlaces a tus vídeos de técnica (Google Fotos, Drive, YouTube…).
- **Agenda.** Calendario de turnos de trabajo (con código y horario de cada turno: M1, T1…), teletrabajo, días libres y pesajes. Los días de teletrabajo propone entrenar en casa, y el entrenador adapta sus consejos a tu turno. En la versión de GitHub los turnos se marcan a mano.
- **Progreso.**
  - Objetivos de peso, % de grasa y masa muscular, con progreso, ritmo mensual y fecha estimada.
  - Peso, % de grasa, masa muscular e IMC, con filtro por fuente de medición.
  - Gráficas por ejercicio: carga máxima, 1RM estimado (Epley) y volumen.
  - Historial de sesiones.
- **Nutrición y actividad.** Importa la exportación de Samsung Health (pasos, calorías y macros) o apunta días a mano. Compara la media de 7 días con tus objetivos.
- **Entrenador IA.** Chat con Claude que recibe tus rutinas, sesiones, mediciones, nutrición y notas, y te aconseja sobre cargas, fatiga y comidas.
- **Perfil.** Incluye:
  - Fase (recomposición, definición, mantenimiento, volumen) y objetivos de macros editables.
  - Notas y recordatorios.
  - Exportación de todos los registros a CSV (series, cardio, composición, nutrición y rutinas) en un ZIP.
  - Copia de seguridad en JSON.

## Uso

### Opción 1: GitHub Pages (recomendado, sirve también para el móvil)

1. Haz un fork de este repositorio o sube estos archivos a uno tuyo.
2. En **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`.
3. Abre `https://<tu-usuario>.github.io/<repositorio>/` en el móvil.
4. **Android (Chrome)**: menú ⋮ → **Instalar aplicación**. Queda en el cajón de aplicaciones con su icono, se abre a pantalla completa y funciona sin conexión (salvo el entrenador). **iPhone (Safari)**: Compartir → **Añadir a pantalla de inicio**.

### Opción 2: en local

Descarga `index.html` y ábrelo en el navegador.

## Dónde se guardan los datos

Todo se guarda **solo en tu navegador** (`localStorage`). No hay servidor ni cuentas, y nadie más ve tus datos.

- Cada navegador y cada dispositivo tiene sus propios datos.
- Para pasar los datos a otro dispositivo, usa **Perfil → Copia de seguridad**: exporta un `.json` en uno e impórtalo en el otro.
- Si borras los datos del navegador, se pierden. Exporta una copia de vez en cuando.

## Entrenador IA

El entrenador llama a la API de Anthropic con **tu propia clave**:

1. Crea una clave en [console.anthropic.com](https://console.anthropic.com).
2. Pégala en **Perfil → Entrenador IA**.

La clave se guarda solo en tu navegador y se envía únicamente a `api.anthropic.com`. Cada pregunta consume créditos de tu cuenta de la API.

El modelo por defecto es `claude-sonnet-5-5`. Puedes cambiarlo en el mismo apartado; consulta los modelos disponibles en [docs.claude.com](https://docs.claude.com).

> Usar una clave de API directamente en el navegador es adecuado para uso personal en tu propio dispositivo. No publiques una versión con tu clave dentro del código.

## Importar desde Samsung Health

1. En Samsung Health: menú ⋮ → **Ajustes** → **Descargar datos personales** → Descargar.
2. Los archivos se guardan en **Mis archivos → Descargas → Samsung Health**. Comprime la carpeta en ZIP, o elige solo los CSV que contienen `step_daily_trend` y `health.nutrition`.
3. En la app: **Progreso → Nutrición y actividad → Importar desde Samsung Health**.

Se importan los últimos 120 días. Puedes repetirlo cuando quieras; los días ya importados se actualizan.

## Calendario

La app asocia los días de la rutina a los días de la semana: Día 1 = lunes, Día 2 = martes… Día 5 = viernes. Sábado y domingo son de descanso, aunque puedes registrar cualquier día manualmente.

## Aviso

Esta app no sustituye el consejo de un profesional sanitario, de un nutricionista o de un entrenador titulado. Si notas dolor o cualquier síntoma, para y consulta con un profesional.

## Licencia

MIT. Consulta [LICENSE](LICENSE).
