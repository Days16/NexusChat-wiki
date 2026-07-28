---
title: Troubleshooting
nav_order: 10
---

# Troubleshooting
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## El overlay no aparece

- Pulsa **M** — puede estar oculto (`overlay.visible=false`).
- Ejecuta `/nexuschat test` para inyectar 5 mensajes de prueba; si tampoco
  aparecen, el problema es de render, no de conexión.
- Revisa que al menos una plataforma tenga `enabled=true` y `showX=true` en
  la sección `overlay` de la configuración.

## Una plataforma no conecta

- **Twitch**: comprueba `channelName`. Si usas token, confirma que tiene el
  scope `chat:read` (y `chat:edit` si quieres enviar mensajes).
- **Kick**: revisa `channelName`; si `chatroomId` no se resuelve solo, prueba
  a rellenar `manualChatroomId` manualmente.
- **YouTube**: confirma el `channelHandle` (con o sin `@`) y que el canal
  esté realmente en directo — sin stream activo no hay chat que leer.
- **TikTok**: revisa que la **API Key de EulerStream** esté rellena — sin
  ella la conexión ni siquiera se intenta. Si sigue sin conectar, prueba a
  rellenar `sessionId` y `ttTargetIdc`.

## Los emotes no se animan

1. Activa `debugLogging=true` y busca en el log:
   ```
   [Texture] GIF animado (WxH, N frames en C cols) para ...
   ```
   Si solo ves `GIF estático`, el CDN devolvió un GIF de un solo frame (no es
   un bug del mod).
2. Si ves `[Texture] GIF decode fallo ... usando proxy fallback`, el
   decodificador nativo falló — abre un issue con el ID del emote.
3. Borra `run/nexuschat/tex-cache/` para forzar la re-descarga.

## Crash relacionado con `GL_MAX_TEXTURE_SIZE`

Ya está cubierto por el empaquetado 2D de emotes animados (límite de
4096px). Si aún así ocurre en una GPU muy antigua, abre un issue adjuntando
el log completo.

## Uso alto de RAM / VRAM

- Baja `maxMessages` en la configuración del overlay.
- Reduce `textureCacheTtlDays` o borra manualmente
  `run/nexuschat/tex-cache/`.
- El LRU de 500 entradas ya destruye texturas desalojadas automáticamente;
  si el uso sigue creciendo sin límite, es un bug — repórtalo.

## El menú de moderación no muestra botones de acción

Solo Twitch tiene acciones de moderación implementadas, y requieren un
**token OAuth** configurado (ver
[Configuración → Twitch](configuracion.html#sección-twitch)). Sin token, el
popup solo muestra un aviso y un acceso directo a la pantalla de conexión.

## El TTS no lee nada

- Revisa el modo TTS de la plataforma correspondiente (`OFF` por defecto en
  algunos casos) en la pantalla **Text-to-Speech**.
- Si esperas que lea *todo* el chat, asegúrate de que el modo esté en
  `Todo el chat`, no en `Solo !tts`.
- Prueba primero con el botón **▶ Probar voz** para descartar problemas de
  voces SAPI5 del sistema operativo.

## El TTS se corta a mitad de un mensaje largo

Corregido: el proceso de síntesis de voz (PowerShell/SAPI5 en Windows)
esperaba una confirmación con un tiempo límite fijo demasiado corto para
frases largas, y las cortaba a media lectura interpretando la síntesis en
curso como un proceso colgado. El tiempo de espera ahora escala con la
longitud del texto. Si lo sigues viendo, [reporta el bug](#reportar-un-bug)
con el mensaje exacto que causó el corte.

## Errores de instalador de Windows (2503/2502) al instalar herramientas relacionadas

Si usas un build de Windows no oficial ("AIO"/modificado), el subsistema de
Windows Installer puede estar dañado o con la versión del SO falseada, lo que
provoca errores `2503`/`2502` al instalar cualquier `.msi` — no solo
relacionado con NexusChat. La alternativa más fiable es usar versiones
portables (`.zip`) de las herramientas que necesites en vez del instalador
MSI.

## Reportar un bug

La forma más rápida es el comando `/nexuschat report <mensaje>` (ver
[Comandos y Keybinds](comandos.html#comandos-de-cliente)): envía tu mensaje
directo al Discord del autor del mod, adjuntando automáticamente el
`mod.log` completo y datos de diagnóstico (versión del mod/Minecraft/Fabric,
SO, perfil de overlay activo, plataformas conectadas). Cooldown de 60s entre
envíos.

Si prefieres abrir un issue manualmente en su lugar, incluye siempre:

1. Versión del mod, de Fabric Loader y de Fabric API.
2. El log completo (`logs/latest.log`) con `debugLogging=true` activado.
3. Pasos exactos para reproducir el problema.
