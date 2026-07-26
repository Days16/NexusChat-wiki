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
  - Badges globales y de canal.
  - Emotes nativos de Twitch + 7TV/BTTV/FFZ.
  - Colores de nombre de usuario.
  - Con token: [menú de moderación](moderacion.html) (timeout, ban, borrar
    mensaje, VIP, mod) y envío de mensajes.
- **Autenticación**: dos flujos disponibles —
  - **Device Code Flow** (`TwitchDeviceCodeFlow`): sin redirect URI, ideal
    para no tener que abrir un servidor local.
  - **Authorization Code + PKCE** (`TwitchOAuthFlow`): abre un servidor local
    en `127.0.0.1:7654` y tu navegador para autorizar la app.
  - Sin token configurado, la conexión es de solo lectura.

## Kick

- **Transporte**: WebSocket Pusher (`ws-us2.pusher.com`).
- **Funciones**: chat, subs, hosts, bans, regalos; emotes de Kick + 7TV sobre
  Kick.
- **Autenticación**: no requiere login para leer el chat público.

## YouTube

- **Transporte**: polling REST sobre InnerTube (API interna de YouTube, cada
  N segundos).
- **Funciones**: chat en directo, Super Chat (con color y monto), Super
  Sticker, notificaciones de miembros/suscripciones.
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
| Twitch | Opcional (recomendado para moderar/enviar) | Token OAuth con scopes `chat:read chat:edit` |
| Kick | No | Solo el nombre de canal |
| YouTube | No | Solo el handle (`@canal`) |
| TikTok | Sí (servicio externo) | API Key de EulerStream (gratuita) |
