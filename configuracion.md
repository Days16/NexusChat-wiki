---
title: Configuración
nav_order: 3
---

# Configuración
{: .no_toc }

Toda la configuración vive en un único archivo JSON:

```
<carpeta-de-minecraft>/config/nexuschat/config.json
```

Se crea automáticamente la primera vez que arrancas el cliente con el mod.
Puedes editarlo con el juego abierto — NexusChat detecta los cambios
(`WatchService` con debounce de 500 ms) y recarga en caliente sin reiniciar.
También puedes editar casi todo desde dentro del juego con **N** / `/nexuschat`.

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Configuración rápida (primera vez)

1. Arranca Minecraft con el mod — se genera `config.json` con los valores por defecto.
2. Entra a un mundo y abre la config con **N** (o `/nexuschat`).
3. Activa las plataformas que quieras (ver [Plataformas](plataformas.html) para el detalle de cada una):
   - **Twitch**: `/conectar twitch` → introduce tu canal. Opcionalmente añade un token OAuth para poder moderar/enviar mensajes.
   - **Kick**: `/conectar kick` → introduce tu canal. No requiere autenticación para leer.
   - **YouTube**: `/conectar youtube` → introduce tu handle (`@tucanal`).
   - **TikTok**: `/conectar tiktok` → requiere una API Key gratuita de EulerStream.
4. Pulsa **M** para mostrar/ocultar el overlay.

---

## Estructura del archivo

```jsonc
{
  "overlay":            { /* aspecto y comportamiento del HUD */ },
  "twitch":              { /* credenciales / canal Twitch */ },
  "youtube":             { /* config YouTube */ },
  "kick":                { /* config Kick */ },
  "tiktok":              { /* config TikTok / EulerStream */ },
  "obs":                 { /* integración OBS-WebSocket */ },
  "streamlabs":          { /* puente de alertas Streamlabs */ },
  "streamElements":      { /* puente de alertas StreamElements */ },
  "specialUsers":        [ /* usuarios destacados */ ],
  "wantedUsers":         [ /* usuarios con alerta especial */ ],
  "teamUsers":           [ /* "Solo mi equipo": usuarios de confianza */ ],
  "zeresGroup":          { /* etiqueta/badge del grupo de specialUsers */ },
  "wantedGroup":         { /* etiqueta/badge del grupo de wantedUsers */ },
  "blockedWords":        [ /* palabras filtradas */ ],
  "blockedUsers":        [ /* usuarios filtrados */ ],
  "overlayProfiles":     { /* perfiles alternativos del overlay */ },
  "activeProfile":       "default",
  "platformOverrides":   { /* overrides de OverlayConfig por plataforma */ },
  "usernameColorOverrides": { /* color custom por usuario */ },
  "textureCacheTtlDays": 7,
  "historyMultiplier":   10,
  "debugLogging":        false,
  "enableHistory":       false,
  "streamerMode":        false
}
```

---

## Sección `overlay`

Controla **cómo** se ve y se comporta el chat en pantalla.

| Campo | Tipo | Default | Descripción |
|---|---|---|---|
| `x`, `y` | `float` | `10.0`, `200.0` | Posición del overlay en píxeles. |
| `width` | `int` | `320` | Anchura del panel. |
| `opacity` | `float` | `0.65` | Opacidad del fondo `[0.0, 1.0]`. |
| `maxMessages` | `int` | `6` | Nº máximo de mensajes visibles a la vez. |
| `visible` | `bool` | `true` | Toggle master (también con `M`). |
| `scale` | `float` | `1.0` | Escala global `[0.5, 3.0]`. |
| `showTwitch` / `showYoutube` / `showKick` / `showTiktok` | `bool` | `true` | Mostrar mensajes de cada plataforma en el overlay (independiente de si está *conectada*). |
| `messageLifetimeMs` | `int` | `0` | ms antes de desvanecer cada mensaje. `0` = infinito. |
| `messageFadeMs` | `int` | `0` | Duración del fade-out al final de la vida. |
| `messageSlideIn` | `bool` | `true` | Animación deslizante al entrar. |
| `backgroundEnabled` | `bool` | `true` | Pinta fondo tras cada mensaje. |
| `backgroundColor` | `int` (RGB) | `0x000000` | Color de fondo cuando `theme=CUSTOM`. |
| `displayMode` | enum | `FULL` | `FULL` / `COMPACT` / `MINIMAL`. |
| `textScale` | `float` | `1.0` | Escala del texto (independiente de la escala global). |
| `theme` | enum | `DEFAULT` | Ver [temas](#temas-y-colores). |
| `highlightMentions` | `bool` | `true` | Resalta mensajes que te mencionan a ti o al streamer. |
| `notifySubscriptions` / `notifyDonations` | `bool` | `true` | Popup al recibir una sub / donación. |
| `duplicateThresholdSec` | `int` | `5` | Ventana de colapso de duplicados (`x3`, `x7`...). `0` = desactivado. |
| `duplicateMaxVisible` | `int` | `3` | A partir de este nº de repeticiones, el duplicado deja de re-mostrarse (solo sube el contador). `0` = desactivado. |
| `userThrottleMax` / `userThrottleWindowSec` | `int` | `0` / `10` | Si un usuario supera `userThrottleMax` mensajes en la ventana, se descartan los siguientes. `0` = desactivado. |
| `mentionSound` | `bool` | `true` | Sonido al ser mencionado. |
| `mentionVolume` | `float` | `0.6` | Volumen del sonido de mención `[0.0, 1.0]`. |
| `mentionSoundId` / `subSoundId` / `donationSoundId` | `String` | ver catálogo | ID de sonido de Minecraft (editable desde la pantalla *Notificaciones*). |
| `subSound` / `donationSound` | `bool` | `true` | Activa el sonido de sub / donación. |
| `enableBttv` / `enableFfz` | `bool` | `true` | Activa los proveedores de emotes BTTV / FFZ. |
| `highlightRoles` | `bool` | `true` | Tinta el fondo del mensaje según el rol más alto del autor. |
| `roleColorBroadcaster` / `roleColorModerator` / `roleColorVip` / `roleColorSubscriber` | `int` (RGB) | naranja / verde / rosa / morado | Colores de tinte por rol (editables en *Colores de rol*). |
| `roleEnabledBroadcaster` / `...Moderator` / `...Vip` / `...Subscriber` | `bool` | `true` | Activa/desactiva el tinte por rol individualmente. |
| `reduceMotion` | `bool` | `false` | Desactiva animaciones (slide-in, spinner) para sensibilidad vestibular o equipos modestos. |
| `onlyMentions` | `bool` | `false` | Solo muestra mensajes que sean menciones (a ti o al streamer). |
| `onlyTeam` | `bool` | `false` | Solo muestra mensajes de usuarios en `teamUsers` ("Solo mi equipo"). |
| `hypeThresholdPerMin` | `int` | `0` | Mensajes por minuto a partir de los cuales se dispara el indicador de hype/raid. `0` = desactivado. |
| `ttsBlockedWords` | `List<String>` | `[]` | Palabras que, si aparecen en un mensaje, hacen que el TTS no lo lea (independiente de la lista negra general). |
| `showStreamPreview` / `streamPreviewWidth` | `bool` / `int` | `false` / `160` | Miniatura del stream en directo sobre el overlay (refresco cada 10s). |
| `continuousExport` | `bool` | `false` | Añade cada mensaje recibido a `live.jsonl` en la carpeta de transcripciones, en tiempo real. |
| `ttsEnabled`, `ttsCommandEnabled`, `ttsReadAuthor`, `ttsAllowAll/Mod/Vip/Sub`, `ttsAllowedUsers`, `ttsVolume`, `ttsPitch`, `ttsRate`, `ttsVoice`, `ttsGapSeconds`, `ttsMode<Plataforma>` | — | — | Ver [Text-to-Speech](tts.html). |

### Modos de display

| Modo | Incluye |
|---|---|
| `FULL` | Header + avatar + icono de plataforma + badges + usuario + mensaje, con ajuste de línea inteligente (vuelve al margen izquierdo). |
| `COMPACT` | Icono de plataforma reducido + solo badges de prioridad 0 + mensaje. |
| `MINIMAL` | Solo nombre y mensaje, sin iconos. |

---

## Sección `twitch`

| Campo | Descripción |
|---|---|
| `enabled` | `true` para conectar al arrancar. |
| `channelName` | Canal a leer (sin `#`). |
| `oauthToken` | Token OAuth de chat (`chat:read chat:edit`). Opcional — sin él, conexión anónima de solo lectura y sin moderación. |
| `username` | Tu nombre de usuario de Twitch (requerido si hay token). |
| `twitchClientId` | Client ID OAuth propio de [dev.twitch.tv/console/apps](https://dev.twitch.tv/console/apps) (Redirect URI `http://localhost:7654/callback`). Opcional — si lo dejas vacío, NexusChat usa un Client ID embebido propio. |

Sin token, el chat se lee pero no puedes enviar mensajes ni usar el
[menú de moderación](moderacion.html).

## Sección `youtube`

| Campo | Descripción |
|---|---|
| `enabled` | `true` para conectar. |
| `channelHandle` | Handle del canal (`@nombre`, con o sin `@`). |

YouTube usa InnerTube anónimo — no hace falta API Key de Google.

## Sección `kick`

| Campo | Descripción |
|---|---|
| `enabled` | `true` para conectar. |
| `channelName` | Nombre del canal de Kick. |
| `pusherAppKey` | Clave pública del Pusher de Kick (preset, normalmente no hace falta tocarla). |
| `pusherCluster` | Cluster geográfico del WebSocket (`us2` por defecto). |
| `chatroomId` | ID numérico de la sala — se resuelve automáticamente al conectar. |
| `manualChatroomId` | Override manual si la resolución automática falla. |

## Sección `tiktok`

| Campo | Descripción |
|---|---|
| `enabled` | `true` para conectar. |
| `channelName` | Usuario de TikTok (sin `@`). |
| `apiKey` | **Requerida.** API Key gratuita de [EulerStream](https://eulerstream.com) (1000 peticiones/mes gratis). |
| `sessionId` | Cookie `sessionid` de tiktok.com (F12 → Application → Cookies). Opcional, solo si la conexión sin sesión falla. |
| `ttTargetIdc` | Cookie `tt-target-idc` de tiktok.com. Opcional, se usa junto a `sessionId`. |

Ver [Plataformas → TikTok](plataformas.html#tiktok) para la guía completa de
cómo conseguir la API Key.

## Sección `obs`

| Campo | Descripción |
|---|---|
| `enabled` | `true` para conectar con OBS-WebSocket. |
| `host` | Host de OBS (`localhost` por defecto). |
| `port` | Puerto de OBS-WebSocket (`4455` por defecto). |
| `password` | Contraseña configurada en OBS → Herramientas → WebSocket Server Settings. |
| `sceneCommand` | Prefijo de chat que dispara un cambio de escena (por defecto `!escena`). |

Ver [OBS](obs.html) para más detalle.

## Secciones `streamlabs` / `streamElements`

| Campo | Descripción |
|---|---|
| `streamlabs.enabled` | `true` para conectar con Streamlabs al arrancar. |
| `streamlabs.token` | Socket API Token de Streamlabs (Settings → API Tokens). Se cifra en disco. |
| `streamElements.enabled` | `true` para conectar con StreamElements al arrancar. |
| `streamElements.jwtToken` | JWT Token de StreamElements (Account → Show secrets). Se cifra en disco. |

Ver [Alertas Streamlabs/StreamElements](alertas.html) para más detalle.

---

## `specialUsers` / `wantedUsers`

Cada uno es un array de objetos `SpecialUser`:

```jsonc
{
  "platform":    "TWITCH",        // TWITCH | YOUTUBE | KICK | TIKTOK
  "username":    "forsen",
  "displayName": "Forsen",        // opcional; para mostrar
  "color":       "#9146FF",       // opcional
  "note":        "Streamer favorito"
}
```

- **`specialUsers`**: resaltados con un color/badge distintivo en el overlay (etiqueta configurable en `zeresGroup`).
- **`wantedUsers`**: disparan una notificación al aparecer (etiqueta configurable en `wantedGroup`).

Se gestionan desde la pantalla **Usuarios especiales** dentro de la config
del mod, sin necesidad de editar el JSON a mano.

## `teamUsers` ("Solo mi equipo")

Mismo formato `SpecialUser` que `specialUsers`/`wantedUsers`, pero usado
solo cuando `overlay.onlyTeam=true`: en ese modo, el overlay oculta cualquier
mensaje de un autor que no esté en esta lista. Se gestiona desde la pantalla
**Equipo** dentro de la config del mod.

## Listas negras

```jsonc
{
  "blockedWords": ["spam", "phishing.com"],
  "blockedUsers": ["bottedaccount123"]
}
```

Comparación case-insensitive, por substring. Un mensaje que coincida con
cualquiera de las dos listas **no** entra en la cola del overlay.

## Perfiles de overlay

Permiten alternar configuraciones de aspecto rápidamente. Los tokens de
autenticación son **globales** — no cambian entre perfiles, solo el aspecto
(`OverlayConfig`).

```jsonc
{
  "overlayProfiles": {
    "stream": { "x": 400, "y": 100, "scale": 1.5, "theme": "PREMIUM_GLASS" },
    "chill":  { "x": 10,  "y": 400, "scale": 1.0, "theme": "MINIMAL_WHITE",
                "messageLifetimeMs": 15000, "messageFadeMs": 2000 }
  },
  "activeProfile": "stream"
}
```

Cambio vía `/nexuschat profile <nombre>` o desde la pantalla **Perfiles**.

## Overrides por plataforma

`platformOverrides` permite sobreescribir campos concretos de `OverlayConfig`
según la plataforma de origen del mensaje (p. ej. mostrar más mensajes de
Twitch que de TikTok). Se gestiona internamente por clave (`twitch`,
`youtube`, `kick`, `tiktok`).

## Temas y colores

| Tema | Fondo | Texto | Acento |
|---|---|---|---|
| `DEFAULT` | `#000000` | `#FFFFFF` | `#FFFFFF` |
| `DARK_GLASS` | `#0A0A0A` | `#E0E0E0` | `#88AABB` |
| `PREMIUM_GLASS` | `#000000` | `#FFFFFF` | `#55AAFF` (con efecto cristal) |
| `QSMP` | `#1A0A2E` | `#FFD700` | `#9146FF` |
| `MINIMAL_WHITE` | `#FFFFFF` | `#000000` | `#888888` |
| `HIGH_CONTRAST` | `#000000` | `#FFFFFF` | `#FFFF00` (accesibilidad) |
| `CUSTOM` | `backgroundColor` | `#FFFFFF` | `#FFFFFF` |

El color del nombre de cada usuario se ajusta automáticamente para mantener
contraste contra el fondo. También puedes fijar un color fijo por usuario en
`usernameColorOverrides`.

## Otros ajustes globales

| Campo | Default | Descripción |
|---|---|---|
| `textureCacheTtlDays` | `7` | Días que se conserva una textura en la caché de disco antes de re-descargarla. |
| `historyMultiplier` | `10` | La capacidad del historial es `max(100, maxMessages * historyMultiplier)`. |
| `debugLogging` | `false` | Logging detallado de texturas/plataformas (silencioso en producción por defecto). |
| `enableHistory` | `false` | Activa el buffer de historial navegable (pantalla **Historial**). |
| `streamerMode` | `false` | Oculta tokens, cookies y nombres de canal en todas las pantallas de auth — actívalo antes de compartir pantalla. |

## Keybinds

Se editan en *Opciones → Controles → NexusChat*, no se guardan en
`config.json` sino en la configuración estándar de Minecraft. Ver el listado
completo en [Comandos y Keybinds](comandos.html#keybinds).

## Preguntas frecuentes

**¿Los tokens se envían a algún servidor mío?** No. Solo se usan localmente
para autenticarte contra la plataforma correspondiente (Twitch IRC, Kick
Pusher, EulerStream para TikTok).

**¿Puedo usar NexusChat en servidores multijugador?** Sí, es un mod
client-side; el servidor no necesita tenerlo instalado.

**¿Funciona en Forge/NeoForge?** No, solo Fabric.

**¿Dónde está la caché de emotes/texturas?** En
`run/nexuschat/tex-cache/`. Puedes borrarla con seguridad, se regenera sola.

**¿Cómo exporto el chat?** `/nexuschat export 500` genera un `.txt` en
`run/nexuschat/transcripts/`. Con `continuousExport` activo también se
escribe en vivo en `live.jsonl`.
