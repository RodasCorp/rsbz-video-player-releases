# RSBZ Video Player — Descargas

Reproductor de video sincronizado para FL Studio (plugin VST3), desarrollado por **DAZERIT**.

Este repositorio solo contiene instaladores listos para descargar. El código fuente está en un repositorio privado.

## Instalación

1. Ir a [Releases](../../releases) y descargar el instalador más reciente (`RSBZ-Video-Player-Setup-X.X.X.exe`).
2. Ejecutarlo (pide permisos de administrador: instala en `Program Files\Common Files\VST3`).
3. Abrir FL Studio y buscar **"RSBZ Video Player"** en el listado de plugins VST3 (puede requerir un rescan: Plugin Manager → Find Plugins).

Para cómo usarlo, formatos soportados y limitaciones conocidas: ver el **[Manual](MANUAL.md)**.

### Windows SmartScreen

Windows va a mostrar un aviso azul **"Windows protegió su PC"** al ejecutar el instalador — es normal, pasa con cualquier instalador que no tenga un certificado de firma de código pago (ese certificado cuesta USD 100-500/año). No significa que el archivo esté dañado ni sea un virus.

Para continuar:
1. Clic en **"Más información"**.
2. Clic en **"Ejecutar de todas formas"**.

Si Chrome o Edge bloquean la descarga del `.exe` directamente, elegir **"Conservar"** / **"Mantener"** cuando pregunte.

## Requisitos

- Windows 64-bit.
- FL Studio con soporte VST3 (v20+), o cualquier host VST3 (Reaper, Ableton — no probado aún).

## Licencias de terceros

Este plugin usa [JUCE](https://juce.com) y [FFmpeg](https://ffmpeg.org) (LGPL), y las tipografías [IBM Plex Mono](https://github.com/IBM/plex) y [Barlow Condensed](https://tribby.com/fonts/barlow/) (ambas SIL Open Font License).

---
© DAZERIT
