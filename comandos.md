---
title: Comandos y Keybinds
nav_order: 4
---

# Comandos y Keybinds
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Comandos de cliente

Disponibles en cualquier partida (singleplayer o servidor), no requieren
permisos de operador.

| Comando | Descripción |
|---|---|
| `/conectar` | Muestra en el chat los enlaces de conexión a las 4 plataformas. |
| `/conectar twitch` | Abre en el navegador el asistente web de conexión a Twitch. |
| `/conectar youtube` | Ídem para YouTube. |
| `/conectar kick` | Ídem para Kick. |
| `/conectar tiktok` | Ídem para TikTok. |
| `/nexuschat` | Abre la pantalla principal de configuración (`MainConfigScreen`). |
| `/nexuschat twitch` / `youtube` / `kick` / `tiktok` | Abre directamente la pantalla de configuración de esa plataforma. |
| `/nexuschat test` | Inyecta 5 mensajes de prueba en el overlay. |
| `/nexuschat export` | Exporta los últimos 100 mensajes a `run/nexuschat/transcripts/`. |
| `/nexuschat export <n>` | Exporta los últimos `n` mensajes (1–100000). |

Los comandos `/conectar <plataforma>` abren un **asistente web local**: el
mod levanta un pequeño servidor en `localhost` y abre tu navegador en un
panel de conexión guiado, en vez de tener que rellenar el JSON a mano.

## Comandos de servidor (debug)

Registrados también del lado servidor (útil en singleplayer o si quieres
simular eventos sin depender de la plataforma real):

| Comando | Descripción |
|---|---|
| `/nexuschat simulate chat` | Inyecta un mensaje de chat de prueba con un emote. |
| `/nexuschat simulate reward` | Inyecta una recompensa de canal de prueba. |
| `/nexuschat simulate sub` | Inyecta una suscripción de prueba. |
| `/nexuschat profile list` | Lista los perfiles de overlay disponibles y cuál está activo. |
| `/nexuschat profile <nombre>` | Cambia al perfil de overlay indicado. |

{: .tip }
> También existe una pantalla **Sesión de Prueba** (`SimulationScreen`)
> dentro de la config del mod que hace lo mismo que `simulate` pero con
> botones, sin tener que escribir el comando.

---

## Keybinds

Se configuran en *Opciones → Controles → NexusChat*. No se guardan en
`config.json`, sino en la configuración estándar de teclas de Minecraft.

| Acción | Tecla por defecto | Descripción |
|---|---|---|
| Mostrar/ocultar overlay | `M` | Toggle master del overlay. |
| Abrir configuración | `N` | Abre `MainConfigScreen` (si no hay otra pantalla abierta). |
| Limpiar overlay | *(sin asignar)* | Vacía la cola de mensajes visibles y resetea el scroll. |
| Ciclar modo de vista | *(sin asignar)* | Alterna entre `FULL` → `COMPACT` → `MINIMAL`. |
| Scroll arriba / abajo | *(sin asignar)* | Navega hacia atrás/adelante en el chat sin tener que abrir el chat vanilla. |
| Abrir filtro | *(sin asignar)* | Abre `FilterInputScreen` para añadir una palabra o usuario a la lista negra rápidamente. |
| Enviar mensaje | *(sin asignar)* | Abre `ChatSendScreen` para escribir un mensaje hacia la plataforma conectada. |
| Solo menciones | *(sin asignar)* | Alterna el filtro "solo menciones" (`onlyMentions`) sin entrar a la config. |
| Abrir historial | *(sin asignar)* | Abre `HistoryScreen` (requiere `enableHistory=true`). |

## Interacción con el ratón

- **Clic izquierdo** sobre un emote/enlace en el overlay: comportamiento
  contextual (tooltip, apertura de enlace).
- **Clic derecho** sobre el nombre de un autor en el overlay: abre el
  [menú de moderación](moderacion.html) contextual junto al cursor.
- El scroll y clic sobre el chat vanilla de Minecraft (tecla `T`) también
  quedan interceptados por NexusChat para navegar el historial unificado.
