# Criterio QA — reglas estables de este repositorio

> **Copia de recuperación entregada en C8.** Es la versión con la que cierra C7, con **la sección 4 ya
> llena con una lista de ejemplo**, para que nadie se quede sin material con qué trabajar. Solo se
> copia si tu repositorio no tiene `.agents/rules/criterio-qa.md`; el comando de clase lo comprueba
> antes de copiar.
>
> **Aviso de C8:** la sección 4 dice que tu segunda skill sale de la segunda lista. En C8 cambió: la
> segunda skill empaqueta el procedimiento que se ejecuta en clase —derivar casos de una historia,
> capa por capa, auditando cada salida—. La segunda lista queda como lista de espera.

> ## Este archivo llega dado, y llega a medio hacer. A propósito.
>
> **Qué es:** las reglas que ya venías repitiendo en cada pedido, escritas **una sola vez**. No se
> invocan: están siempre activas. Cualquier capacidad de este repositorio —la skill de hoy y las que
> vengan— trabaja debajo de estas reglas.
>
> **Por qué está incompleto:** acá abajo hay **cuatro** reglas, y son las cuatro que la skill de hoy
> necesita para funcionar. Entre C1 y C7 apareció bastante más que eso: cómo se pide un diagnóstico,
> qué locators se usan, cómo se explica código, qué se hace con una discrepancia. **Eso se cosecha en
> C8**, que es la clase donde este repositorio se convierte en un sistema de trabajo completo.
>
> **Qué NO va en este archivo:** el contexto del producto (eso vive en `docs/`) y los procedimientos
> con pasos (eso vive en `.agents/skills/`).

---

## 1. Honestidad sobre la fuente

Estas tres reglas son la misma idea con tres nombres, uno por artefacto. La idea es: **cuando falta
un dato, se escribe que falta.**

| Regla | Cuándo aplica | Nació en |
|---|---|---|
| Si un dato no está en lo que te entregué, escribe `SIN FUENTE` en esa celda y sigue. No lo completes con lo probable. | cualquier tabla o documento | C1 · C6 |
| Si un puntaje depende de información que no te di, escribe `SIN CONTEXTO` y di en una línea qué dato necesitas. No lo adivines. | priorización | C7 |
| **No inventes** endpoints, pantallas, requerimientos, campos ni comportamientos. La superficie real del sistema bajo prueba está en `docs/contrato-api.md` y en `docs/mapa-selectores.md`. Si algo no está ahí, no existe hasta que alguien lo verifique. | siempre | C6 · C7 |

---

## 2. Quién decide

| Regla | Nació en |
|---|---|
| No completes las columnas «decisión» ni «razón» de ningún documento. **Esas dos las firmo yo.** | C7 |

---

## 3. Cómo crece este archivo

Una regla entra acá cuando cumple las tres condiciones:

1. **Ya la escribiste al menos dos veces** en pedidos distintos.
2. **Vale para más de un artefacto.** Si solo aplica a un procedimiento, va dentro de esa skill, no acá.
3. **No es contexto del producto.** *"El curso `api-testing` no tiene cupo"* no es una regla: es un
   dato, y los datos viven en `docs/`.

Si una regla deja de cumplirse en la práctica, se borra. Un archivo de reglas que nadie respeta
enseña justo lo contrario de lo que dice.

---

## 4. Para cosechar en C8

> **Esta sección llega con una lista de ejemplo**, escrita sin ordenar y sin clasificar, como la
> escribiría cualquiera al terminar C7. Está a propósito mezclada: hay reglas, hay un dato del
> producto, hay una línea de contexto del repositorio y hay procedimientos. Separarlos es el trabajo
> de C8.
>
> **Si trajiste tu lista de la tarea, reemplaza estas líneas por las tuyas.** Si no la trajiste,
> trabaja sobre estas y quédate solo con las que reconozcas como propias: algo que de verdad le
> pediste a la IA dos veces o más.

### Reglas mías que deberían estar siempre encendidas

> Cosas que le repetiste a la IA más de una vez entre C1 y C7, en pedidos de temas distintos.

- le pedí que me dijera qué dato le faltaba en vez de suponerlo (C1, C6)
- le pedí que no inventara selectores que no estaban en el HTML que le pasé (C3, C4)
- le pedí que citara de qué parte del contrato sacaba cada afirmación (C6)
- le dije que no tocara el código, que solo me explicara qué pasaba (C2, C5)
- el login se bloquea después de cinco intentos fallidos
- le pedí que me explicara el test en el orden en que se ejecuta (C5)
- le repetí que la verdad de la API está en `docs/contrato-api.md` (C6, C7)

### Cosas que hice más de una vez y que todavía no son skill

> Procedimientos que repetiste. Esta lista es la **lista de espera**: cada línea se empaqueta el día
> que la vuelvas a ejecutar con criterio.

- pedirle casos de prueba a la IA a partir de una historia o un requerimiento (C1)
- comparar la respuesta real de la API contra el contrato (C6)
- revisar los selectores que propone la IA contra el DOM real (C3, C4)

---

*Semilla entregada en C7 con cuatro reglas · se cosecha entero en C8.*
