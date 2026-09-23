# recursos-s8 — lo que C8 pone en tu repositorio

## Resultado de hoy

Cosechas tus reglas en `.agents/rules/criterio-qa.md`, **auditas capa por capa** cómo la IA produce los
casos del login —la docente los corre en pantalla, el gate de cada capa lo haces tú— y recibes ese
procedimiento **empaquetado y terminado** como la segunda skill del repositorio:
`.agents/skills/derivar-casos-de-hu/SKILL.md`. En clase se recorre entera —de qué gate salió cada uno
de sus nueve límites— y la ves correr sobre una historia que nunca vio. La registras en
`.agents/agents.md`.

> **Lo tuyo está en la tarea.** El programa promete para C8 *«empaquetás tu segunda skill sin ayuda»*.
> En clase la recibes hecha; el fin de semana le agregas **por lo menos un límite tuyo** y **la corres
> tú**, por primera vez. Está en `Tarea-S9-Consigna.md`, parte 2.

## Qué trae

```text
recursos-s8/
├── HU-login.md                    la historia de hoy · se copia a docs/
├── HU-registro.md                 la historia con que se prueba la skill · se copia a docs/
├── casos-login.md                 los casos del login resueltos y auditados en clase · se copia a docs/
├── derivar-casos-de-hu.SKILL.md   la segunda skill, terminada · se copia como .agents/skills/derivar-casos-de-hu/SKILL.md
└── recuperacion-c7/               semillas de C7 · solo si te faltan
    ├── agents.md
    ├── criterio-qa.md

```

**La skill viaja como archivo suelto, no dentro de una carpeta `.agents/`.** Por eso se llama
`derivar-casos-de-hu.SKILL.md` y se copia con nombre nuevo: si viniera adentro de un `.agents/`, el
`cp -R` te pisaría el `agents.md` y el `criterio-qa.md`.

**Este paquete no tiene carpeta `.agents/`, a propósito.** Todo se copia **archivo por archivo**, y
solo si el archivo no existe. Si viniera una carpeta `.agents` para copiar entera, el `cp -R` te
pisaría el `agents.md` y el `criterio-qa.md` que vienes escribiendo.

## Cómo se copia

Desde la raíz de `qa-automation-portfolio`, con `recursos-s8/` descomprimido ahí. Son tres bloques y
en clase se ejecutan en tres momentos distintos.

`[ -f archivo ]` pregunta si el archivo existe; `||` ejecuta lo que sigue solo si la respuesta es no.
Si ya tienes el archivo, la línea no hace nada.

### 1 · Reglas (slide 4)

```bash
mkdir -p .agents/rules
[ -f .agents/agents.md ] || cp recursos-s8/recuperacion-c7/agents.md .agents/
[ -f .agents/rules/criterio-qa.md ] || cp recursos-s8/recuperacion-c7/criterio-qa.md .agents/rules/
ls -a .agents .agents/rules
```

### 2 · La historia (slide 6, al empezar el bloque 4)

```bash
mkdir -p docs
[ -f docs/HU-login.md ] || cp recursos-s8/HU-login.md docs/
```

### 2b · Los casos resueltos (slide 11, al **cerrar** el bloque 4)

Se copia al final a propósito: si lo tienes abierto desde el principio, el gate se vuelve copiar la
respuesta.

```bash
[ -f docs/casos-login.md ] || cp recursos-s8/casos-login.md docs/
```

### 3 · La skill y la historia de prueba (slide 13)

```bash
mkdir -p .agents/skills/derivar-casos-de-hu
[ -f .agents/skills/derivar-casos-de-hu/SKILL.md ] || cp recursos-s8/derivar-casos-de-hu.SKILL.md .agents/skills/derivar-casos-de-hu/SKILL.md
[ -f docs/HU-registro.md ] || cp recursos-s8/HU-registro.md docs/
```

La historia de registro se copia hoy pero **la necesitas el fin de semana**: en clase la corrida la
hace la docente en su pantalla.

**Nunca** `cp -R recursos-s7/.agents .` ni copies `recuperacion-c7/` entera sobre `.agents/`. Si un
`cp` te pisó un archivo: `git checkout HEAD -- <ruta>` lo vuelve a la última versión commiteada.

## Qué haces con cada archivo

| Archivo | Qué haces |
|---|---|
| `docs/HU-login.md` | lo lees. No se edita: es la fuente |
| `docs/casos-login.md` | **llega hecho**: las cinco capas, ya corregidas en el gate de cada una. Lo que pones tú: fecha, nombre y **tu P6**, la pregunta que la IA no podía hacer |
| `.agents/skills/derivar-casos-de-hu/SKILL.md` | **llega terminado.** En clase se recorre entero: sus pasos son los cinco pedidos de `Materiales-S8.md` y sus nueve límites salen de los gates del bloque 4 (ocho) y de una corrida de prueba (el noveno). Lo que pones tú, en la tarea: **al menos un límite propio** en la sección 4, y una bitácora de tu primera corrida |
| `docs/HU-registro.md` | la historia sobre la que corres la skill **en la tarea**. En clase la corre la docente. No se edita |
| `.agents/rules/criterio-qa.md` | agregas la sección 5 (el texto está en `Materiales-S8.md`) |
| `.agents/agents.md` | pegas el registro de la skill en la sección 3 y actualizas tres filas (`Materiales-S8.md`) |

## Si faltaste

1. Ejecuta los tres bloques de arriba.
2. Sigue `Materiales-S8.md` en orden. Copia `docs/casos-login.md` y **aplica tú el gate de cada capa**,
   que viene escrito adentro del archivo: empieza por buscar tres fragmentos de la sección 5 en la
   historia. Eso es lo que en clase se hizo en grupo, y es lo que el lunes te va a hacer falta.
3. Corre tú los cinco pedidos de la sección *El encuadre y los cinco pedidos*, uno por vez, en una
   conversación nueva, y compara con el archivo. Es lo mejor que puedes hacer si faltaste.
4. Abre el `SKILL.md` que copiaste y **lee la sección 4 con la tabla de `Materiales-S8.md` al lado**
   (*La sección 4, línea por línea*): dice de dónde salió cada uno de los nueve límites. Eso es lo que se hizo en pantalla y es lo que no se recupera solo leyendo el archivo.
5. Haz la tarea de `Tarea-S9-Consigna.md`. La parte 2 es la que más te falta: ahí corres tú y le
   agregas tu propio límite.

## Orden de recuperación, si faltaste a varias clases

De menor a mayor: `recursos-s7` → `recursos-s8` → `recursos-s9` → … Siempre con los bloques con guarda.
Así ninguna semilla vieja queda encima de algo que ya escribiste.

## Guardar

```bash
git add docs/HU-login.md docs/HU-registro.md docs/casos-login.md .agents
git commit -m "feat: derivar casos del login con fuente y empaquetar derivar-casos-de-hu"
git push
```
