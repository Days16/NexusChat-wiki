---
title: Instalación
nav_order: 2
---

# Instalación
{: .no_toc }

## Tabla de contenido
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Requisitos

| Componente | Versión mínima |
|---|---|
| Minecraft | 1.21.11 |
| Fabric Loader | 0.18.2 |
| Fabric API | 0.139.5+1.21.11 |
| Java | 21 |

NexusChat es **client-side**: solo hace falta instalarlo en tu launcher, no en
el servidor al que te conectas.

## Paso a paso

1. Instala **Fabric Loader** para tu versión de Minecraft (desde el
   instalador oficial de Fabric).
2. Descarga **Fabric API** y colócalo en tu carpeta `mods/`.
3. Copia el `.jar` de NexusChat (`nexuschat-<version>.jar`) en la misma
   carpeta `mods/`.
4. Arranca Minecraft con el perfil de Fabric. Al entrar a un mundo, NexusChat
   genera automáticamente `config/nexuschat/config.json` con los valores por
   defecto.

## Compilar desde el código fuente

Si prefieres compilar el `.jar` tú mismo:

```powershell
git clone <url-del-repo-del-mod>
cd NexusChat-26.2
./gradlew.bat build --console=plain
```

El `.jar` resultante queda en `build/libs/`. Para probarlo directamente sin
empaquetar:

```powershell
./gradlew.bat runClient --console=plain
```

{: .note }
> El mod incluye dependencias runtime empaquetadas (`okhttp`, `okio` para el
> WebSocket de Kick; `webp-imageio` opcional para WebP estático), así que no
> necesitas instalarlas por separado.

## Primeros pasos tras instalar

1. Pulsa **N** (o escribe `/nexuschat`) para abrir la pantalla de
   configuración.
2. Conecta al menos una plataforma — ver [Plataformas](plataformas.html) para
   el detalle de cada una (Twitch, Kick, YouTube, TikTok).
3. Pulsa **M** para mostrar/ocultar el overlay del chat.

Si algo no conecta o no aparece nada en pantalla, revisa
[Troubleshooting](troubleshooting.html) antes de nada.
