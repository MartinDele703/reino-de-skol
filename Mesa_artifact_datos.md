# Mesa en el artifact · Formato de los datos

Referencia para el DM. El artifact (frontend del repo `ChelabsWeb/mesa-dnd`) muestra en vivo lo que haya en su base. El DM la escribe con la herramienta `ArtifactData`; los jugadores solo miran.

- **Link:** https://claude.ai/artifact/JV38YxDJSoLib7CJqLrzRJ
- **Todo lo que se escribe acá lo leen todos los jugadores.** Solo va lo que los personajes saben. Nunca: PG de enemigos, notas del DM, secretos de PNJ, lo que viene después.
- Antes de escribir un documento que ya existe hay que leerlo (la escritura va atada a su versión). Si cambió sin que lo haya escrito el DM, avisar antes de pisarlo.
- Cuando hay más de dos escrituras juntas, van en un solo `batch`.

## `campaign/state` · un solo documento

```json
{
  "titulo": "Reino de SKOL",
  "capitulo": "Sesión 1 · [nombre del capítulo]",
  "escena": {
    "titulo": "Título corto de la escena",
    "lugar": "Dónde están",
    "ambiente": "taberna",
    "texto": "Lo que ven y pasa. Párrafos separados por salto de línea.",
    "objetivo": "Qué pueden hacer ahora (las opciones, en una frase)."
  },
  "combate": {
    "activo": true,
    "ronda": 1,
    "turno": 0,
    "orden": [ { "nombre": "Nombre", "ini": 17 } ]
  },
  "mapa": {
    "nombre": "Nombre de la región",
    "semilla": "texto-fijo",
    "lugares": [ { "nombre": "Lugar", "x": 0.4, "y": 0.6, "tipo": "pueblo" } ],
    "aqui": "Lugar"
  }
}
```

- `ambiente`: uno de `taberna`, `mazmorra`, `bosque`, `camino`, `montana`, `mar`, `ciudad`, `cueva`, `ruinas`.
- `combate.turno`: posición (desde 0) en `orden` de quien juega. `orden` ya va ordenado por iniciativa. Los enemigos van con nombre genérico ("Goblin 1"), sin PG. Fuera de combate: `activo: false`.
- `mapa.semilla`: no cambiarla una vez elegida, porque redibuja la costa y las montañas. `x`, `y` de 0 a 1. `tipo`: `pueblo`, `fuerte` o `castillo`. `aqui` es el nombre del lugar donde está el grupo.

## `characters/<id>` · un documento por personaje

`<id>`: el nombre en minúsculas, sin tildes, con guiones (`thorin-barba-roja`).

```json
{
  "nombre": "Nombre", "jugador": "Jugador", "raza": "Enano", "clase": "Clérigo",
  "nivel": 1, "orden": 1,
  "stats": { "fue": 14, "des": 10, "con": 15, "int": 8, "sab": 16, "car": 12 },
  "pg": 10, "pgMax": 10, "ca": 18, "velocidad": "7,5 m",
  "salvaciones": ["sab", "car"],
  "competencias": ["medicina", "religion"],
  "estados": [],
  "ataques": [ { "nombre": "Maza", "bono": 4, "dano": "1d6+2", "nota": "Contundente." } ],
  "aptitud": "sab",
  "espacios": { "1": { "max": 2, "usados": 0 } },
  "conjuros": [ { "nivel": 0, "nombre": "Llama sagrada", "desc": "Una línea.", "concentracion": false } ],
  "rasgos": [ { "nombre": "Rasgo", "desc": "Qué hace y cuántas veces." } ],
  "inventario": ["Cota de escamas", "Escudo", "15 monedas de oro"]
}
```

- `orden`: 1, 2, 3… Define el asiento en la mesa (máximo 5 personajes sentados).
- `clase`: el color y el escudo salen del nombre en español (Guerrero, Bárbaro, Paladín, Mago, Hechicero, Brujo, Clérigo, Druida, Explorador, Pícaro, Bardo, Monje).
- `competencias`, con estas claves: `acrobacias`, `arcanos`, `atletismo`, `engano`, `historia`, `interpretacion`, `intimidacion`, `investigacion`, `juego-de-manos`, `medicina`, `naturaleza`, `percepcion`, `perspicacia`, `persuasion`, `religion`, `sigilo`, `supervivencia`, `trato-con-animales`.
- El artifact calcula solo: bonificador de competencia, modificadores, salvaciones, pericias, percepción pasiva, CD y ataque de conjuros. `ca`, `pgMax` y el `bono` de cada ataque van ya calculados.
- `aptitud`, `espacios` y `conjuros`: solo si lanza conjuros. `nivel: 0` son trucos.
- `estados`: lista de textos cortos ("Envenenado", "Furia").
- `inventario`: lista de textos. El dinero va como un ítem más ("15 monedas de oro").
- Lo que no entra en estos campos (personalidad, historia, ganchos) queda solo en `fichas/`.

## `log/<id>` · el diario

```json
{ "orden": 12, "tipo": "combate", "titulo": "Emboscada en el puente", "texto": "Una o dos frases." }
```

- `orden`: creciente; el más alto aparece arriba. Se muestran los últimos 80.
- `tipo`: `combate`, `botin`, `descubrimiento` o `historia`.
- `<id>`: `s<sesión>-<orden>` (por ejemplo `s1-012`).
