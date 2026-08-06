---
title: Roadmap
nav_order: 11
---

# Roadmap
{: .no_toc }

Estado funcional a fecha de esta wiki, verificado directamente contra el
código fuente de `NexusChat-26.2` (no solo contra la documentación interna
del proyecto, que en algunos puntos había quedado desactualizada).

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## ✅ Implementado

- Chat unificado Twitch + Kick + YouTube + **TikTok** (vía EulerStream).
- Emotes 7TV (global + por canal + zero-width) y BTTV/FFZ opcionales.
- Atlas 2D para emotes animados, caché en disco con TTL configurable.
- Badges oficiales, avatares asíncronos, colores de nombre con contraste
  automático.
- Modos de vista `FULL` / `COMPACT` / `MINIMAL`, 7 temas de color (incluye
  `HIGH_CONTRAST` de accesibilidad).
- Menciones resaltadas + notificaciones de sub/donación con sonido
  configurable.
- Colapso de duplicados (`xN`) y throttle por usuario.
- Perfiles de overlay y overrides de configuración por plataforma.
- Hot-reload de `config.json`.
- Historial navegable, exportación de transcripción (puntual y continua).
- Envío de mensajes al chat desde dentro del juego (`ChatSendScreen`).
- **Text-to-Speech** completo: menciones automáticas, comando `!tts`,
  permisos por rol, modos por plataforma.
- **Menú de moderación** in-overlay (timeout / ban / borrar mensaje / VIP /
  mod) vía Twitch Helix API, con clic derecho sobre el nombre.
- **Integración con OBS-WebSocket** (cambio de escena desde el chat).
- **Puente de alertas Streamlabs/StreamElements** para donaciones sin
  equivalente nativo en el chat. Ver [Alertas](alertas.html).
- **Miniatura de stream en directo** sobre el overlay.
- Encuestas y predicciones de Twitch en el overlay (posición configurable,
  comando `/nexuschat poll dismiss` para quitarlas), indicador de hype/raid,
  modo "Solo mi equipo", multi-canal por plataforma, reintentos con backoff
  visibles, marcador de mensajes nuevos, vista previa de emote,
  confirmación antes de banear, cifrado de credenciales en disco. Ver
  [Novedades 1.2](novedades-1.0.html) para el detalle completo.
- Reporte de bugs (`/nexuschat report <mensaje>`) directo al Discord del
  autor, con `mod.log` completo adjunto y datos de diagnóstico automáticos.
- Pantalla **"🎉 Novedades"** automática al abrir `/nexuschat` tras
  actualizar, con el resumen de cambios de esa versión.
- **Panel de Widgets** centralizado (Chat/Encuesta/Música/Contador de
  vistas: toggle + mover posición), **widget de música "now playing"**
  (Spotify/YouTube/YouTube Music vía SMTC, solo Windows, dos estilos, con
  títulos largos deslizándose en vez de cortarse) y **widget contador de
  vistas** (suma espectadores de las plataformas elegidas). Ver
  [Novedades 1.2](novedades-1.0.html) para el detalle completo.
- Arreglos de conexión: TikTok (timeout de conexión), YouTube (avisos
  repetidos cuando no hay directo activo), TTS (modo "Todo el chat" que se
  reseteaba solo). Botón "💬" para unirte al Discord del mod desde la
  pantalla principal.
- OAuth de Twitch: Device Code Flow + Authorization Code con PKCE, Client ID
  embebido propio como fallback.
- Modo streamer (oculta tokens/cookies en las pantallas de configuración).
- Accesibilidad: `reduceMotion`, tema de alto contraste, "solo menciones".
- **Publicado en [Modrinth](https://modrinth.com/mod/nexuschat)**, con builds
  para Minecraft `26.1.2` y `26.2` (`1.21.11`).

## ⏳ Pendiente / en evaluación

- Acciones de moderación nativas para Kick, YouTube y TikTok (por ahora solo
  Twitch expone una API de moderación directa).
- Reconocimiento de voz / accesibilidad ampliada (lector de pantalla).
- Publicación en CurseForge.

{: .note }
> Este roadmap se genera comparando el código fuente real contra la
> documentación interna del proyecto (`docs/PLAN.md`), que listaba TTS y OBS
> como "pendientes" pese a estar ya implementados — si algo de esta página no
> cuadra con lo que ves en el juego, confía en el código antes que en este
> documento y abre un issue para corregirlo.
