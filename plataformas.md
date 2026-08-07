---
title: Plataformas
nav_order: 5
---

# Plataformas soportadas
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Asistente de conexión web

Para las 4 plataformas, la forma recomendada de conectar es el comando
`/conectar <plataforma>`: NexusChat levanta un pequeño servidor web local y
abre tu navegador en un panel guiado, en vez de tener que editar el JSON de
configuración a mano. También puedes configurar cada plataforma directamente
desde las pantallas de `/nexuschat <plataforma>`.

---

## Twitch

- **Transporte**: IRC (`irc.chat.twitch.tv:6667`), anónimo o autenticado con
  token OAuth.
- **Funciones**:
  - Chat normal, subs (`USERNOTICE`), bits/donaciones, recompensas de canal.
  - **Follows en el chat** (vía EventSub — ver más abajo, requiere reconectar
    con el token nuevo).
  - Badges globales y de canal.
  - Emotes nativos de Twitch + 7TV/BTTV/FFZ.
  - Colores de nombre de usuario.
  - Con token: [menú de moderación](moderacion.html) (timeout, ban, borrar
    mensaje, VIP, mod) y envío de mensajes.
- **Autenticación**: sin token configurado, la conexión es de solo lectura —
  ves el chat pero no podés moderar, enviar mensajes, ni ver el nº de
  espectadores en el [contador de vistas](novedades-1.0.html#widget-contador-de-vistas).
  Hay dos formas de conseguir el token, ambas desde la pantalla **Twitch**
  (buscador de `/nexuschat`, o `/conectar twitch`):
  - **Botón "OAuth" (recomendado)**: un solo clic. Usa el Device Code Flow —
    sin necesidad de servidor local ni redirect URI. Te muestra un código
    corto en pantalla y abre `twitch.tv/activate` en el navegador; pegás el
    código ahí, autorizás la app, y el token se guarda solo en cuanto Twitch
    confirma (verás "✓ Autenticado. Reconectando..." en la pantalla).
  - **Botón "❓ Cómo conseguir token"**: abre un panel web local
    (`localhost:7654/connect/twitch`, vía el flujo Authorization Code + PKCE)
    con instrucciones paso a paso — alternativa si el botón OAuth no te
    funciona por algún motivo. Una vez que tengas un token (`oauth:...`),
    también podés pegarlo directamente en el campo **Token** de la pantalla
    y presionar **"Validar token"**.

{: .note }
> **Follows en el chat**: Twitch dejó de exponerlos por el chat/PubSub
> normal hace años — NexusChat los recupera vía **EventSub**, que necesita
> el scope `moderator:read:followers`. Si conectaste tu cuenta antes de esta
> función, reconectá con el botón **OAuth** una vez más para que el token
> incluya el permiso nuevo; todo lo demás (chat, moderación, envío de
> mensajes) sigue funcionando igual sin reconectar.

### Multi-canal por plataforma

Además del canal principal (`twitch.channelName`), puedes seguir canales de
Twitch adicionales listando sus nombres en `twitch.extraChannelNames`
(editable desde la pantalla **Twitch** de la config, campo de texto separado
por comas). Los mensajes de esos canales extra se muestran con un prefijo
`[canal]` en el overlay y quedan marcados como **restringidos** en el
[menú de moderación](moderacion.html) (algunas acciones solo aplican al canal
principal). Útil para raids/colabs donde quieres ver varios chats a la vez
sin cambiar de canal.

## Kick

- **Transporte**: WebSocket Pusher (`ws-us2.pusher.com`).
- **Funciones**: chat, subs, regalos de subs, follows, bans; emotes de Kick +
  7TV sobre Kick.
- **Hosts**: se muestran con el mismo estilo visual que un raid (espectadores
  redirigidos desde otro canal), en vez de mezclarse con las donaciones.
- **Autenticación**: no requiere login para leer el chat público.

## YouTube

- **Transporte**: polling REST sobre InnerTube (API interna de YouTube, cada
  N segundos).
- **Funciones**: chat en directo, Super Chat (con color y monto), Super
  Sticker, notificaciones de miembros/suscripciones, regalos de membresía
  (compra y recepción).
- **Autenticación**: ninguna — usa InnerTube de forma anónima, **no
  necesitas una API Key de Google**.

## TikTok

TikTok no ofrece una API pública de chat en directo, así que NexusChat se
apoya en **[EulerStream](https://eulerstream.com)**, un servicio de terceros
que firma y retransmite el chat en vivo de TikTok.

- **Requisito obligatorio**: una **API Key gratuita de EulerStream** (incluye
  1000 peticiones/mes sin coste). Sin ella, TikTok no se puede activar.
- **Opcional**: cookies `sessionid` y `tt-target-idc` de tiktok.com (F12 →
  Application → Cookies), solo necesarias si la conexión sin sesión falla.

### Cómo conseguir la API Key

1. Ve a [eulerstream.com](https://eulerstream.com) y crea una cuenta
   gratuita.
2. Entra al Dashboard → sección **API Keys**.
3. Pulsa **Create API Key** y cópiala.
4. Pégala en `/nexuschat tiktok` → campo **API Key** → Guardar.

{: .tip }
> Dentro del juego, la pantalla de configuración de TikTok tiene un botón
> **"¿Cómo obtener mi API Key?"** que abre esta misma guía paso a paso sin
> salir de Minecraft.

## OBS (integración, no una plataforma de chat)

NexusChat también puede conectarse a **OBS Studio** vía OBS-WebSocket para
disparar cambios de escena desde el chat (p. ej. escribiendo `!escena nombre`
en Twitch). Ver [OBS](obs.html).

---

## Resumen de autenticación por plataforma

| Plataforma | ¿Requiere login? | Qué necesitas |
|---|---|---|
| Twitch | Opcional (recomendado para moderar/enviar/ver follows) | Token OAuth (incluye `moderator:read:followers` para follows) |
| Kick | No | Solo el nombre de canal |
| YouTube | No | Solo el handle (`@canal`) |
| TikTok | Sí (servicio externo) | API Key de EulerStream (gratuita) |
