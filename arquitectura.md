---
title: Arquitectura
nav_order: 9
---

# Arquitectura
{: .no_toc }

Página pensada para quien quiera **contribuir código** al mod o entender su
funcionamiento interno.

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Estructura de paquetes

```
com.nexuschat
├── NexusChat              · ModInitializer (común, registra comandos de servidor)
├── NexusChatClient        · ClientModInitializer (HUD, keybinds, tick de cliente)
├── NexusChatConstants      · Client ID de Twitch embebido (ofuscado con XOR)
├── chat/                  · Dispatcher, cola de mensajes, filtros
├── command/               · Comandos de servidor y de cliente
├── config/                · POJOs de Gson + ConfigManager (hot-reload, perfiles)
├── keybind/                · Keybinds configurables
├── mixin/                  · ChatScreenScrollMixin (intercepta scroll/click/right-click del chat vanilla)
├── model/                  · Records inmutables (UnifiedChatMessage, MessageSegment, ...)
├── platform/                · Un cliente por plataforma
│   ├── twitch/              · IRC + OAuth (Device Code + PKCE) + acciones de moderación (Helix)
│   ├── kick/                 · WebSocket Pusher + resolución de chatroom
│   ├── youtube/              · Polling InnerTube
│   ├── tiktok/                · Adaptador EulerStream + parser + resolución de emotes
│   └── obs/                  · Cliente OBS-WebSocket
├── render/                  · ChatOverlayRenderer, MessageRenderer, EmoteRenderer, BadgeRenderer, ...
├── screen/                  · Pantallas de configuración (Screen de Minecraft)
├── texture/                 · TextureCache (LRU + liberación GL), TextureFetcher (HTTP + GIF/WebP), TextureDiskCache, RemoteTexture (atlas 2D)
├── util/                    · ColorUtil, EmojiPreprocessor, ThreadUtil, ChatNotifier, TtsUtil, ...
└── web/                     · Servidor local + asistente de conexión web (`/conectar`)
```

### Puntos de entrada

| Clase | Rol |
|---|---|
| `NexusChat` | `onInitialize` — carga la config, registra comandos de servidor. |
| `NexusChatClient` | `onInitializeClient` — keybinds, HUD, tick de cliente, conecta plataformas. |
| `PlatformManager` | Singleton que arranca/detiene cada `ChatPlatform`. |

### Hilos

- **Render thread** (Minecraft) — el único autorizado a tocar GL y `TextureManager`.
- **`ThreadUtil.IO_POOL`** — `FixedThreadPool(8)` para HTTP y decodificación de imágenes.
- **`ThreadUtil.SCHEDULER`** — `SingleThreadScheduledExecutor` para polling y reconexiones.

Todo flujo que toque texturas usa `ThreadUtil.onRenderThread(...)` o
`MinecraftClient.getInstance().execute(...)`.

---

## Ciclo de vida de un mensaje

1. **La plataforma parsea un evento** (IRC/WS/InnerTube/EulerStream) →
   `UnifiedChatMessage` con `segments`, `badges` y `MessageType`. Los
   emotes de 7TV/BTTV/FFZ ya llegan resueltos como `EmoteSegment`.
2. `ChatMessageDispatcher.dispatch(msg)`:
   - Filtros de lista negra.
   - Pre-carga de texturas de avatar y badges.
   - Throttle de duplicados (`duplicateThresholdSec`) → contador `xN`.
   - Detección de menciones: streamer (rojo) > jugador (amarillo) → marcador
     en `rawContent`.
   - Reproduce sonido de notificación (en el hilo de cliente vía `mc.execute`).
   - `queue.add(msg)`.
3. **Render** en `HudRenderCallback`, cada frame:
   - `ChatOverlayRenderer.render` → `drainWindowFiltered` → bucle de dibujo.
   - `MessageRenderer.calculateHeight` cacheada en `heightBuf[]`.
   - `ChatOverlayRenderer.renderBackground` (compatible 1.21.1) → fondo según
     tipo de mensaje / mención.
   - `MessageRenderer.render(...)` → `EmoteRenderer.render` (texto + emotes
     con ajuste de línea sin indentar).

## Subsistema de texturas

```
TextureCache (RAM, LRU 500 entradas)
    ↓ miss
TextureDiskCache (disco, TTL configurable)
    ↓ miss
HttpUtil.getBytes  (HttpURLConnection — ver nota más abajo)
    ↓
TextureFetcher
    ├─ GIF  → decodeGif() → atlas 2D (empaquetado en rejilla, respeta GL_MAX_TEXTURE_SIZE / 4096px)
    └─ estático → NativeImage.read (PNG/JPEG) → fallback ImageIO (WebP) → fallback proxy wsrv.nl
```

Al desalojar del LRU se llama a `textureManager.destroyTexture(id)` **en el
render thread** para no filtrar memoria de GPU.

## HTTP dentro del classloader de Minecraft

Minecraft usa un classloader personalizado que rompe ciertas librerías HTTP.
Esto es importante si vas a tocar código de red:

| Librería | Estado |
|---|---|
| `HttpURLConnection` | ✅ Segura — la usa el propio Minecraft. |
| `java.net.http.HttpClient` | ⚠️ Falla con SSL en peticiones normales (el WebSocket sí funciona). |
| OkHttp | ❌ Crashea (`NoClassDefFoundError: kotlin/jvm/internal/Intrinsics`, falta el runtime de Kotlin en Fabric) — **excepto** para el WebSocket de Kick, donde se incluye vendorizado. |

**Regla**: usa siempre `HttpURLConnection` para peticiones REST.
`java.net.http.HttpClient` solo para WebSocket.

## Contribuir

1. Clona el repositorio del mod y compílalo con `./gradlew.bat compileJava`
   para validar cambios rápido.
2. Sigue las convenciones de hilos descritas arriba — cualquier código que
   toque `TextureManager` o `SoundManager` fuera del render thread provoca
   crashes silenciosos o texturas corruptas.
3. Antes de abrir un PR, prueba manualmente con `/nexuschat simulate chat`,
   `sub`, `reward` (o la pantalla **Sesión de Prueba**) y verifica que no
   rompes el hot-reload de configuración.
