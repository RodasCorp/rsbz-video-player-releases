# Manual de RSBZ Video Player

Reproductor de video sincronizado para FL Studio, de **DAZERIT**. Carga un video, lo reproduce pegado al transporte de FL Studio (play/stop/seek) y, opcionalmente, lo combina con el render de audio al exportar.

## Instalación

Ver [README](README.md) o la página de [Releases](../../releases). El instalador pide permisos de administrador e instala en `Program Files\Common Files\VST3`.

---

## Tutorial: primeros pasos

### 1. Insertar el plugin

En FL Studio, insertarlo como efecto en cualquier pista del mixer (Master o una pista dedicada — no importa cuál, el plugin no modifica el audio que pasa por él). Si no aparece en el listado, Plugin Manager → **Find Plugins**.

### 2. Cargar un video

Botón **LOAD VIDEO** → elegir el archivo. El panel de preview muestra "Cargando..." mientras decodifica el primer frame, y después el video en vivo.

### 3. Reproducción sincronizada

No hay botones de play/pausa propios: el video sigue **el transporte de FL Studio**. Al presionar play en FL Studio, el video arranca con el proyecto; al detenerlo, el video se congela en ese frame. El reloj de arriba (`00:00:00.000`) muestra el tiempo del transporte, y debajo indica **PLAYING** o **STOPPED**.

### 4. Offset

Campo **Offset (s)**: corrige si el video está adelantado o atrasado respecto al audio. Un valor positivo adelanta el video; uno negativo lo atrasa. Se escribe el número y se presiona Enter (o se hace clic afuera) para aplicarlo.

### 5. Pantalla completa

Botón **FULLSCREEN**: cubre toda la pantalla donde esté el plugin con el video, sin controles. Para salir: clic en cualquier parte o tecla **Esc**.

### 6. Exportar el video combinado

Esto **no es un botón de "exportar ahora"** — se activa automáticamente cuando FL Studio hace un render offline (Ctrl+R, no la reproducción normal):

1. Activar el toggle **"Exportar video"**.
2. Escribir un nombre en **"Nombre del video exportado"**.
3. Renderizar el proyecto en FL Studio como de costumbre (el audio, en el formato habitual).
4. El plugin captura ese audio en segundo plano y lo combina con el video cargado (video sin recodificar, audio a AAC) en cuanto termina el render.
5. El estado de la parte inferior va mostrando el progreso: "Capturando audio...", "Combinando video...", y al final "Video exportado: \<ruta\>" (en ámbar) o un error en rojo con el motivo.

El video exportado queda truncado a la duración del video original (si el audio renderizado es más largo, no se agrega pantalla negra de relleno).

---

## Formatos de archivo soportados

| Extensión | Soportado |
|---|---|
| `.mp4` | Sí |
| `.mov` | Sí |
| `.avi` | Sí |
| `.mkv` | Sí |
| `.wmv` | Sí |
| `.mpg` / `.mpeg` | **No** (ver limitaciones) |

El selector de archivos (LOAD VIDEO) solo permite elegir entre las primeras 5 extensiones. Dentro de cada contenedor, el códec real lo decodifica FFmpeg — la gran mayoría de códecs comunes (H.264, H.265, VP9, etc.) funcionan sin configuración adicional.

## Limitaciones conocidas

- **`.mpg` / `.mpeg` no soportados todavía.** El formato MPEG-PS suele traer un desfase interno (`start_time` distinto de cero) que el decoder aún no corrige, y el video se vería atrasado. Se recomienda convertir el archivo a `.mp4` antes de cargarlo.
- **Videos 4K muy pesados** pueden consumir bastante memoria (el límite de hilos de decodificación de FFmpeg no tiene techo todavía). Si el contenido es más de ~3.5x más pesado que tiempo real de decodificar, puede volver a notarse algo de tranco en la reproducción.
- **Exportar con offset distinto de 0, o renderizando solo una parte del timeline** (no desde el inicio): el código lo soporta pero no está probado a fondo todavía. Si el flujo de trabajo siempre exporta el timeline completo desde el offset 0 (lo más común), esto no afecta.
- **"Smart Disable" de FL Studio** (si está activado para este plugin durante silencios largos) podría desincronizar el video — sin confirmar todavía. Si se nota desincronización, se recomienda desactivar Smart Disable para este plugin.
- El plugin **no altera el audio** que pasa por la pista donde está insertado — es seguro insertarlo en el Master sin riesgo de que cambie el sonido.

## Problemas comunes

- **No aparece en Plugin Manager:** Plugin Manager → Find Plugins (rescan completo). Si se viene de una versión anterior con otro nombre, o ya estaba instalado antes, puede hacer falta reinsertar el plugin en el proyecto si cambió de identidad.
- **"No se combinó el video: ya existe un archivo con ese nombre":** el nombre de salida ya está ocupado — colocar otro nombre y volver a renderizar.
- **Se capturó audio pero no se generó video:** revisar que haya un video cargado y un nombre de salida escrito antes de renderizar.

---
© DAZERIT
