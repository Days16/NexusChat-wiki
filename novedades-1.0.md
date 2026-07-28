---
title: Novedades 1.0
nav_order: 1.5
---

# Novedades de la 1.0
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .note }
> Esta página resume lo añadido en NexusChat 1.0 (release), de cara a quien ya
> conocía versiones anteriores del mod (1.0 beta). Se irá actualizando según
> avance el desarrollo — si algo de aquí no coincide con lo que ves en el
> juego, confía en el comportamiento real y avisa para corregir la página.

## Pantalla "Novedades" al actualizar

- Desde la 1.1, la primera vez que abres `/nexuschat` (o pulsas **N**) tras
  actualizar el mod, se muestra una pantalla de solo lectura
  ("🎉 Novedades — v...") con el resumen de cambios de esa versión, en vez de
  la pantalla de configuración normal. Se genera desde un fichero interno del
  mod (`whatsnew.json`) — no requiere conexión a internet. Pulsa
  **Continuar** o Esc para cerrarla y pasar a la configuración; no vuelve a
  aparecer hasta la siguiente actualización con novedades nuevas.

## Overlay y chat en directo

- **Encuestas y predicciones de Twitch en el overlay**: cuando hay una
  encuesta o predicción activa en tu canal, aparece una barra con las
  opciones y porcentajes directamente sobre el HUD, con un breve fade al
  cerrarse. Sondeo automático cada 30s (`TwitchPollPoller`).
- **Posición, ancho y escala de la encuesta/predicción configurables**: ya no
  queda fija pegada encima del chat ni comparte el tamaño del chat — tiene su
  propia posición, ancho y escala (`pollX`/`pollY`/`pollWidth`/`pollScale`)
  que se ajustan desde una pantalla dedicada (buscador de `/nexuschat`,
  palabra clave "poll"/"encuesta"). Ver
  [Configuración → sección `overlay`](configuracion.html#sección-overlay).
- **Comando `/nexuschat poll dismiss`**: quita manualmente del overlay la
  encuesta o predicción visible en ese momento. Si sigue activa en Twitch, no
  reaparece hasta que cambie de título (empiece una encuesta nueva). Ver
  [Comandos y Keybinds](comandos.html#comandos-de-cliente).
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

## Panel de Widgets

- **Pantalla "Widgets" centralizada**: lista Chat, Encuesta y Música en un
  solo lugar, cada uno con un toggle ON/OFF y un botón "Mover posición" que
  abre su pantalla de arrastre correspondiente. Accesible desde el botón
  junto a la sección OVERLAY de la config principal, o desde el buscador de
  `/nexuschat` (palabra clave "widgets").

## Widget de música "now playing"

- **Nuevo widget que muestra qué estás escuchando**: portada, título,
  artista(s) y barra de progreso, compatible con **Spotify de escritorio**,
  **YouTube en cualquier navegador** (Chrome/Edge/Firefox) y **YouTube
  Music** — todo con un solo mecanismo (lee la sesión de medios activa de
  Windows vía System Media Transport Controls), sin necesitar cuentas ni
  API keys de ningún servicio para el uso básico.
- **Dos estilos**: barra compacta horizontal, o tarjeta expandida con
  "waveform" decorativo (puramente visual, no reactivo al audio real) +
  tiempo transcurrido/total. Ambos con **ancho**, **tamaño (escala)** y
  **tema de color** configurables (varios presets, incluye uno estilo
  Spotify y uno de blanco y negro). Se elige y se posiciona desde la
  pantalla dedicada del widget (panel **Widgets** → Música →
  "Mover posición"). Si los colores configurados quedaran sin contraste por
  algún motivo, el widget cae automáticamente a blanco sobre negro en vez de
  verse ilegible.
- **Más rápido y estable**: el sondeo de Windows ahora usa un proceso
  persistente en vez de reiniciar PowerShell en cada consulta, por lo que
  refleja cambios de canción mucho más rápido; y ya no desaparece de golpe
  si una lectura puntual falla (espera unos segundos antes de ocultarse).
- **Todos los artistas de la canción**: el estilo expandido ahora envuelve
  el nombre del/los artista(s) en hasta 2 líneas en vez de recortarlo a uno
  solo.
- **Conexión opcional con Spotify** (botón "🎵 Conectar Spotify" dentro de
  la pantalla de posición del widget, o buscador → "Spotify"): si conectás
  tu cuenta, el widget usa la API oficial de Spotify —lista completa de
  artistas y portada en mejor calidad— mientras Spotify sea la app activa.
  Requiere registrar tu propia app en
  [developer.spotify.com](https://developer.spotify.com/) con el Redirect
  URI que te muestra la pantalla de conexión. Sin esto, el widget sigue
  funcionando igual solo con los datos que da Windows.
- **Detección mejorada de la sesión activa**: Windows a veces se queda
  "pegado" a la última app con la que interactuaste (por ejemplo Spotify en
  pausa) en vez de mostrar lo que realmente suena en el navegador; ahora se
  revisan todas las sesiones de medios activas y se prioriza la que esté de
  verdad en reproducción.
- **Solo Windows**: en macOS/Linux el widget simplemente no se activa (no
  hay error ni crash), ya que la API que lee "qué se está reproduciendo" es
  exclusiva de Windows.

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
  [Comandos y Keybinds](comandos.html#simulación-y-perfiles).

## Internacionalización

- Trabajo en curso de traducción (`es_es` / `en_us`) para toda la interfaz;
  la pantalla principal de configuración ya está completamente traducida.

## Soporte y reportes

- **Comando `/nexuschat report <mensaje>`**: envía un reporte de bug directo
  al Discord del autor del mod. Incluye tu mensaje, versión del mod/Minecraft/
  Fabric, sistema operativo, perfil de overlay activo, plataformas
  conectadas, y el `mod.log` completo adjunto como archivo (no solo un
  extracto). Cooldown de 60s entre envíos para evitar spam. Ver
  [Comandos y Keybinds](comandos.html#comandos-de-cliente).
- **Botón "🐞" en la pantalla principal**: abre una ventanita para escribir y
  enviar un reporte sin tener que escribir el comando a mano.
