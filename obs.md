---
title: OBS
nav_order: 8
---

# Integración con OBS
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

NexusChat puede conectarse a **OBS Studio** mediante el protocolo
**OBS-WebSocket** (incluido de serie en OBS 28+) para reaccionar a comandos
del chat, como cambiar de escena.

## Configurar OBS

1. En OBS, ve a **Herramientas → WebSocket Server Settings**.
2. Activa el servidor WebSocket y anota el **puerto** (por defecto `4455`) y
   la **contraseña**.
3. En Minecraft, abre `/nexuschat` → **OBS** y rellena:

| Campo | Descripción |
|---|---|
| `enabled` | Activa la conexión. |
| `host` | Normalmente `localhost` (si Minecraft y OBS están en el mismo PC). |
| `port` | Puerto del WebSocket de OBS (`4455` por defecto). |
| `password` | La contraseña que configuraste en OBS. |
| `sceneCommand` | Prefijo de comando de chat que dispara el cambio de escena (por defecto `!escena`). |

## Uso

Con la integración activa, cualquier mensaje de chat con el prefijo
configurado cambia la escena activa en OBS, por ejemplo:

```
!escena Just Chatting
```

cambiaría OBS a la escena llamada exactamente `Just Chatting`.

{: .note }
> El nombre de la escena debe coincidir exactamente (sensible a mayúsculas)
> con el nombre configurado en OBS.

{: .warning }
> Si tienes streamers o moderadores de confianza, ten en cuenta que
> **cualquiera** que conozca el comando puede cambiar tu escena mientras
> `sceneCommand` esté activo — considera restringir quién puede escribir en
> el chat si te preocupa el uso indebido.
