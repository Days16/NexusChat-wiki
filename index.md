---
title: Inicio
nav_order: 1
description: "NexusChat — overlay de chat multi-plataforma para Minecraft"
permalink: /
---

# NexusChat
{: .fs-9 }

Overlay de chat multi-plataforma para Minecraft (Fabric) que unifica **Twitch, Kick, YouTube y TikTok** en un solo HUD dentro del juego.
{: .fs-6 .fw-300 }

[Descargar en Modrinth](https://modrinth.com/mod/nexuschat){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Instalación](instalacion.html){: .btn .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Configuración](configuracion.html){: .btn .fs-5 .mb-4 .mb-md-0 }
[Novedades 1.0](novedades-1.0.html){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## ¿Qué es NexusChat?

NexusChat es un mod **client-side** para Fabric que muestra el chat de tus
plataformas de streaming favoritas directamente sobre la pantalla del juego,
sin necesidad de una segunda pantalla ni ventana externa. No requiere que el
servidor al que te conectas tenga el mod instalado.

## Características principales

- **Chat unificado** de Twitch, Kick, YouTube y TikTok (vía EulerStream) en un solo overlay.
- **Emotes animados**: Twitch, 7TV (global y por canal, con *zero-width overlays*), BTTV, FFZ, y emojis Unicode vía Twemoji — todo empaquetado en un atlas 2D por textura GL para rendimiento.
- **Caché en disco** de texturas (TTL configurable) para no re-descargar en cada arranque.
- **Badges e insignias** oficiales de cada plataforma, avatares cargados de forma asíncrona.
- **Text-to-Speech**: lee menciones o todo el chat en voz alta, con comando `!tts` configurable por plataforma y por rol (mod/VIP/sub). Ver [Text-to-Speech](tts.html).
- **Menú de moderación**: clic derecho sobre un nombre en el overlay para hacer timeout, ban, borrar mensaje, VIP o mod (Twitch, vía Helix API). Ver [Moderación](moderacion.html).
- **Integración con OBS** vía OBS-WebSocket: cambia de escena desde el chat con un comando (`!escena`). Ver [OBS](obs.html).
- **Puente de alertas Streamlabs/StreamElements**: dona sin equivalente nativo en el chat (PayPal, tips directos) llegan al overlay igual que cualquier otra donación. Ver [Alertas](alertas.html).
- **Encuestas y predicciones de Twitch** en vivo sobre el overlay, y un indicador de **hype/raid** cuando el ritmo de mensajes se dispara.
- **Modo "Solo mi equipo"** y **multi-canal por plataforma** (sigue varios canales de Twitch a la vez). Ver [Novedades 1.0](novedades-1.0.html).
- **Modos de visualización**: `FULL`, `COMPACT`, `MINIMAL`.
- **7 temas de color** (incluye un tema de alto contraste para accesibilidad) y colores de fondo por rol (streamer, mod, VIP, sub).
- **Menciones resaltadas**, notificaciones de sub/donación con sonido configurable.
- **Listas negras** de palabras y usuarios, throttle por usuario, colapso de duplicados.
- **Perfiles de overlay** intercambiables y overrides de configuración por plataforma.
- **Historial y exportación** de chat a fichero de texto, con export continuo opcional.
- **Envío de mensajes** al chat de la plataforma desde dentro del juego.
- **Modo streamer**: oculta tokens y datos sensibles en las pantallas de configuración mientras compartes pantalla.
- **Hot-reload** de la configuración: edita el JSON con el juego abierto y los cambios se aplican al vuelo.
- **Panel de Widgets**: activa/desactiva y reposiciona Chat, Encuesta y Música desde un solo lugar. Ver [Novedades 1.0](novedades-1.0.html#panel-de-widgets).
- **Widget de música "now playing"**: portada, título, artista y progreso de Spotify/YouTube/YouTube Music (solo Windows), sin cuentas ni API keys. Ver [Novedades 1.0](novedades-1.0.html#widget-de-música-now-playing).
- **Reporte de bugs** in-game (`/nexuschat report`) directo al Discord del autor.

## Stack técnico

| | |
|---|---|
| Minecraft | `26.1.2` y `26.2` (`26.2` = `1.21.11`) |
| Fabric Loader | ≥ 0.18.2 |
| Fabric API | según versión — ver [Modrinth](https://modrinth.com/mod/nexuschat) para la matriz exacta |
| Java | 21 |

## Empezar

1. [Descarga el mod en Modrinth](https://modrinth.com/mod/nexuschat) o [instálalo desde código fuente](instalacion.html).
2. Conecta tus plataformas desde [Configuración](configuracion.html) o con `/conectar <plataforma>`.
3. Pulsa **M** en el juego para mostrar/ocultar el overlay.

¿Algo no funciona? Revisa [Troubleshooting](troubleshooting.html).

{: .tip }
> Dentro de la pantalla de configuración (`/nexuschat`) hay un botón **[W]**
> junto al de Modo Streamer, arriba a la derecha, que abre esta wiki
> directamente en tu navegador.

{: .note }
> Tras actualizar el mod, la primera vez que abras `/nexuschat` (o pulses
> **N**) verás una pantalla **"🎉 Novedades"** con un resumen de los cambios
> de esa versión en vez de la configuración normal. Pulsa **Continuar** (o
> Esc) para cerrarla — no vuelve a aparecer hasta la siguiente actualización.
