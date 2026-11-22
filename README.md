# Reino de SKOL

Campaña de D&D 5e (reglas 2014 + Xanathar) con Claude Code como Dungeon Master.

> El reino se llama **SKOL**. Algunos archivos conservan "SKQL" en el nombre para no romper rutas.

## Qué hay acá

| Ruta | Qué es |
| --- | --- |
| `Reino_de_SKQL_Contexto.md` | La memoria de la campaña: grupo, lore, PNJ, resumen de sesiones y dónde arranca la próxima. |
| `fichas/` | Una ficha por personaje. |
| `CLAUDE.md` | Las instrucciones del DM (cómo jugamos, reglas de la casa, cierre de sesión). |
| `Sesion_0_Creacion_de_personajes.md` | Guía de la sesión 0. |
| `Plantilla_ficha_personaje.md` | Formato de las fichas. |
| `Mesa_artifact_datos.md` | Formato de los datos de la mesa. |
| `artifact/` | La mesa: el frontend que vemos mientras jugamos y una copia de sus datos. |

## Cómo jugar una sesión

1. Cloná el repo y abrí la carpeta con Claude Code.
2. Claude lee `CLAUDE.md` y el contexto, y hace de DM.
3. Al terminar la sesión, Claude actualiza el contexto y las fichas. Hacé commit y push para que el resto tenga lo último.

Antes de arrancar, hacé `git pull`: si dos personas juegan sobre versiones distintas, el contexto se pisa.

## La mesa (`artifact/`)

- `artifact/index.html` y `artifact/assets/mesa.gltf.json`: el frontend, copiado del repo `ChelabsWeb/mesa-dnd`.
- `artifact/datos/`: copia de la base de la mesa (escena y mapa en `campaign/`, personajes en `characters/`, diario en `log/`), tomada el 22/11/2026.

La mesa en uso está publicada en https://claude.ai/artifact/JV38YxDJSoLib7CJqLrzRJ. Es privada: se entra solo si el dueño la comparte desde el menú Share.

**Solo la cuenta que publicó ese artifact puede escribir su base desde Claude Code.** Si otro va a hacer de anfitrión, tiene que publicar su propia copia:

1. Pedile a Claude Code que publique `artifact/index.html` junto con `artifact/assets/mesa.gltf.json` como artifact, con las capacidades `db` y `user`.
2. Pedile que cargue los datos de `artifact/datos/` en la base del artifact nuevo.
3. Cambiá el link en `CLAUDE.md` y en `Mesa_artifact_datos.md` por el nuevo.

Si no coinciden, valen los `.md`; la mesa es solo la pantalla.
