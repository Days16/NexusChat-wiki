---
title: Text-to-Speech
nav_order: 6
---

# Text-to-Speech (TTS)
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

NexusChat puede leer el chat en voz alta usando las voces instaladas en tu
sistema (SAPI5 en Windows). Se configura desde `/nexuschat` → **Text-to-Speech**.

## Voz y sonido

| Opción | Descripción |
|---|---|
| Voz | Selector cíclico entre las voces detectadas en el sistema. "Predeterminada" usa la voz del sistema. |
| Volumen | 0–100%. |
| Velocidad | -10 (más lento) a 10 (más rápido), 0 = normal. |
| Tono | -10 (más grave) a 10 (más agudo), 0 = normal. |
| Espera | Pausa en segundos tras cada frase antes de leer la siguiente, 0 = sin pausa. |

## Opciones

- **Menciones**: lee automáticamente en voz alta los mensajes que te
  mencionan a ti o al streamer.
- **Cmd !tts**: habilita el comando `!tts <mensaje>` en el chat para que
  cualquier usuario autorizado pida que se lea su mensaje.
- **Autor**: antepone "Usuario dice:" antes del texto leído.
- **Plataformas TTS** (Twitch, YouTube, Kick, TikTok): cada una cicla entre 4
  modos independientes:
  1. `OFF` — nunca lee esa plataforma.
  2. `Solo !tts` — solo lee cuando alguien usa el comando.
  3. `Menciones + !tts` — además lee menciones automáticas.
  4. `Todo el chat` — lee absolutamente todos los mensajes de esa plataforma.

## Permisos de `!tts`

Controla quién puede usar el comando `!tts` en el chat:

| Permiso | Descripción |
|---|---|
| Todos | Cualquier usuario del chat. |
| Mod | Solo moderadores y el broadcaster. |
| VIP | Solo usuarios VIP. |
| Sub | Solo suscriptores. |
| Nicks adicionales | Lista de usuarios concretos (separados por coma) que siempre pueden usarlo, independientemente de su rol. |

Estos permisos son acumulativos: puedes activar varios a la vez (p. ej. Mod +
VIP + una lista de nicks de confianza).

## Probar la configuración

La pantalla incluye tres botones de prueba:

- **▶ Probar voz**: reproduce una frase de ejemplo con la configuración actual.
- **▶ !tts**: simula cómo sonaría un comando `!tts` real del chat.
- **⏹ Detener**: para la lectura en curso y vacía la cola de TTS pendiente.

{: .note }
> Cambiar de voz reinicia el proceso de síntesis (`TtsUtil.resetProcess()`) y
> reproduce automáticamente una frase de confirmación con la nueva voz.
