---
title: Novedades 1.0 beta
nav_order: 1.5
---

# Novedades de la 1.0 beta
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .note }
> Esta página resume lo añadido en la beta actual de NexusChat 1.0, de cara a
> quien ya conocía versiones anteriores del mod. Se irá actualizando según
> avance la beta — si algo de aquí no coincide con lo que ves en el juego,
> confía en el comportamiento real y avisa para corregir la página.

## Overlay y chat en directo

- **Encuestas y predicciones de Twitch en el overlay**: cuando hay una
  encuesta o predicción activa en tu canal, aparece una barra con las
  opciones y porcentajes directamente sobre el HUD, con un breve fade al
  cerrarse. Sondeo automático cada 30s (`TwitchPollPoller`).
- **Modo "Solo mi equipo"**: filtra el overlay para mostrar únicamente
  mensajes de una lista de confianza (pantalla **Equipo**, separada de los
  grupos de usuarios especiales existentes). Toggle rápido desde
  `MainConfigScreen`.
- **Umbral de hype/raid**: si el ritmo de mensajes por minuto supera un
  umbral configurable, aparece un indicador visual de "hype" en el overlay.
  El umbral se ajusta desde la pantalla **Estadísticas**.
- **Marcador de "mensajes nuevos"**: si dejas de mirar el overlay (ventana
  sin foco) y llegan mensajes mientras tanto, aparece un separador al volver
  indicando desde dónde son nuevos.
- **Multi-canal por plataforma (Twitch)**: puedes añadir canales de Twitch
  adicionales a seguir además del principal (`extraChannelNames`); sus
  mensajes se etiquetan con `[canal]` en el overlay y quedan marcados como
  "restringidos" en el menú de moderación (algunas acciones solo aplican al
  canal principal). Ver [Plataformas → Twitch](plataformas.html#twitch).

## Reconexión y estabilidad

- **Reintentos con backoff visibles**: si una plataforma se desconecta, el
  overlay muestra un indicador con el número de intento y los segundos
  restantes hasta el siguiente reintento, en vez de fallar en silencio.

## Herramientas de escritura y moderación

- **Vista previa de emotes**: al escribir un mensaje desde
  `ChatSendScreen`, los nombres de emote se autocompletan y se renderiza una
  vista previa en vivo antes de enviar.
- **Confirmación antes de banear**: el botón *Ban* del
  [menú de moderación](moderacion.html) requiere doble clic (se "arma" y
  expira solo si no confirmas), para evitar bans accidentales por un clic de
  más.
- **Botón "Ignorar" en el menú de moderación**: añade al usuario directamente
  a la lista de bloqueo (`blockedUsers`) sin salir del overlay.
- **Buscador de ajustes**: la pantalla principal de configuración
  (`/nexuschat`) tiene un buscador en la parte superior que filtra todas las
  subpantallas por nombre o palabra clave.

## Estadísticas

- **Gráfico de actividad** y **exportación a CSV** en la pantalla
  **Estadísticas**, además del umbral de hype configurable desde ahí mismo.

## Seguridad

- **Cifrado de credenciales sensibles**: tokens OAuth, contraseñas (OBS) y
  ahora también los tokens de Streamlabs/StreamElements se cifran en disco
  (AES/GCM, clave derivada de la máquina) dentro de `config.json`. Se
  descifran solo en memoria al cargar — sigues pudiendo editar el JSON en
  caliente con el juego abierto.

## Integraciones nuevas

- **Puente de alertas Streamlabs/StreamElements**: reenvía donaciones/tips
  que no tienen equivalente nativo en el chat (PayPal, tips directos) como
  mensajes de tipo donación en el overlay. Ver
  [Alertas Streamlabs/StreamElements](alertas.html).

## Simulación / pruebas

- `/nexuschat simulate` y la pantalla **Sesión de Prueba** ahora también
  cubren encuesta, predicción, hype/raid y un mensaje de canal extra, además
  de los ya existentes (chat, sub, donación, recompensa). Ver
  [Comandos y Keybinds](comandos.html#comandos-de-servidor-debug).

## Internacionalización

- Trabajo en curso de traducción (`es_es` / `en_us`) para toda la interfaz;
  la pantalla principal de configuración ya está completamente traducida.
