---
title: Alertas (Streamlabs / StreamElements)
nav_order: 8.5
---

# Puente de alertas Streamlabs / StreamElements
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Algunos tipos de donación (PayPal a través de Streamlabs, tips directos vía
StreamElements) **nunca pasan por el chat de Twitch/Kick/YouTube/TikTok** —
solo llegan como eventos a la cuenta de Streamlabs/StreamElements del
streamer. Este puente escucha esos eventos y los inyecta en el overlay de
NexusChat como un mensaje de tipo donación más, con el mismo pipeline que
cualquier otro mensaje (throttle, sonido, historial, exportación...).

{: .note }
> Deliberadamente **solo reenvía donaciones/tips**. Subs, bits, follows, etc.
> se descartan si llegan por Streamlabs/StreamElements porque ya te llegan de
> forma nativa por el chat de la plataforma — reenviarlos también duplicaría
> la notificación.

## Configurar Streamlabs

1. Entra al [Dashboard de Streamlabs](https://streamlabs.com/dashboard) →
   **Settings → API Tokens**.
2. Copia tu **Socket API Token**.
3. En Minecraft, abre `/nexuschat` → icono **🔔** (junto al de la wiki) →
   pega el token en el campo **Streamlabs Token** → activa **Streamlabs ON**.

## Configurar StreamElements

1. Entra a tu [cuenta de StreamElements](https://streamelements.com/dashboard)
   → **Account → Show secrets → JWT Token**.
2. Copia el JWT.
3. En Minecraft, abre `/nexuschat` → **🔔** → pega el JWT en el campo
   **StreamElements JWT** → activa **StreamElements ON**.

## Campos de configuración

| Campo | Sección | Descripción |
|---|---|---|
| `streamlabs.enabled` | `streamlabs` | Activa la conexión con Streamlabs al arrancar el cliente. |
| `streamlabs.token` | `streamlabs` | Socket API Token de Streamlabs. Se cifra en disco igual que el resto de tokens. |
| `streamElements.enabled` | `streamElements` | Activa la conexión con StreamElements al arrancar el cliente. |
| `streamElements.jwtToken` | `streamElements` | JWT Token de StreamElements. Se cifra en disco igual que el resto de tokens. |

## Cómo funciona por dentro

- Transporte: **Socket.IO** (`io.socket:socket.io-client`), sin dependencia de
  Kotlin/OkHttp adicionales (reutiliza el OkHttp 4 ya vendorizado del mod).
- Streamlabs se autentica pasando el token como parámetro de la URL de
  conexión; StreamElements se conecta sin credenciales y emite un evento
  `authenticate` con el JWT justo después de conectar.
- Al llegar un evento, se filtra por tipo (`donation` en Streamlabs,
  `tip-latest` / `*:tip` en StreamElements) y se traduce a un
  `UnifiedChatMessage` de tipo `DONATION`, despachado por el mismo
  `ChatMessageDispatcher` que procesa el resto de plataformas.
- El icono de estado en la pantalla de alertas muestra **Conectado** /
  **Desconectado** en tiempo real.

{: .warning }
> Ni Streamlabs ni StreamElements garantizan siempre en qué plataforma
> (Twitch/YouTube/Kick) ocurrió la donación original en cada evento. Por
> simplicidad, estos mensajes se muestran actualmente con el icono/color de
> **Twitch** — es el caso de uso más común, pero puede no ser exacto en
> configuraciones multi-plataforma.

## Solución de problemas

- **No conecta**: revisa que el token/JWT esté bien pegado (sin espacios) y
  que la plataforma esté marcada como `enabled`. El log de Minecraft
  (`logs/latest.log`) muestra el motivo del fallo de conexión.
- **Conecta pero no aparecen donaciones**: activa `debugLogging` en
  `config.json` (o desde la config del mod) — cada evento recibido se
  registra en crudo en el log, útil para comprobar si el formato del payload
  cambió por parte de Streamlabs/StreamElements.
- **JWT de StreamElements rechazado**: el log mostrará
  `StreamElements: JWT rechazado por el servidor` — regenera el JWT desde el
  dashboard (puede haber expirado o sido regenerado desde otro sitio).
