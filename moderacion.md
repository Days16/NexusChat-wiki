---
title: Moderación
nav_order: 7
---

# Menú de moderación
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

NexusChat incluye un menú contextual de moderación directamente sobre el
overlay del chat, sin tener que salir del juego ni abrir el panel web de la
plataforma.

## Cómo abrirlo

**Clic derecho** sobre el nombre de un autor en el overlay (o sobre un
mensaje en el chat vanilla de Minecraft con `T` abierto, gracias al mixin que
intercepta scroll/click). Se abre un popup pequeño junto al cursor, sin
pausar el juego ni oscurecer la pantalla — así puedes seguir viendo el chat
mientras moderas.

## Acciones disponibles (Twitch)

| Acción | Efecto |
|---|---|
| Timeout 60s / 10m / 1h | Silencia al usuario ese tiempo. |
| Ban | Banea permanentemente al usuario del canal. Requiere **doble clic**: el primer clic "arma" el botón (y se desarma solo si no confirmas enseguida), el segundo lo ejecuta — pensado para evitar bans accidentales. |
| Eliminar mensaje | Borra ese mensaje concreto del chat de Twitch. |
| VIP | Otorga el rol VIP al usuario. |
| Mod | Otorga el rol de moderador al usuario. |
| 🚫 Ignorar | Añade al usuario a `blockedUsers` (lista negra local) sin salir del overlay — no requiere Helix ni token. |

Todas las acciones vía Helix se ejecutan en un hilo de I/O
(`TwitchModActions`), y el popup muestra el resultado (✓ éxito / ✗ error) sin
bloquear el juego. **Ignorar** es puramente local y funciona siempre, incluso
sin token OAuth.

{: .note }
> Si sigues varios canales de Twitch a la vez (ver
> [multi-canal por plataforma](novedades-1.1.html#overlay-y-chat-en-directo)),
> los mensajes de canales adicionales aparecen como **restringidos** en este
> menú: algunas acciones de moderación solo tienen sentido sobre el canal
> principal configurado en `twitch.channelName`.

### Requisito: token OAuth

Las acciones de moderación **solo están disponibles en Twitch** y requieren
que tengas un token OAuth configurado (ver
[Configuración → Twitch](configuracion.html#sección-twitch)). Si no hay
token, el popup muestra un aviso y un botón directo a la pantalla de conexión
de Twitch en lugar de los botones de acción.

## Otras plataformas

Para Kick, YouTube y TikTok el menú todavía no tiene acciones de moderación
propias (esas plataformas no exponen una API de moderación tan directa como
Twitch Helix); el popup ofrece **"Copiar nombre"** para copiar el usuario al
portapapeles rápidamente.

## Cerrar el menú

Pulsa **Cerrar**, o simplemente haz clic fuera del popup — se cierra solo.
