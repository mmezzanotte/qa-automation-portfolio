# JavaScript esencial para leer tests

## Test observado

- Archivo: `tests/orden-ejecucion.spec.ts`
- Fecha: 2026-09-14
- Responsable: Maria

## 1. Mapa de lectura

| Fragmento real | Cómo lo leo | ¿Prepara o espera? | Evidencia de ejecución |
|---|---|---|---|
| `const LOGIN_URL = ...` | guarda la URL con un nombre | prepara información | ocurre antes del test |
| `async ({ page }) => {` | función asíncrona que recibe `page` | abre un bloque que puede usar `await` | contiene los pasos |
| `const email = page.getByLabel('Email')` | crea una descripción del campo | prepara un locator; no espera | aparece después del log 2 |
| `await page.goto(LOGIN_URL)` | inicia la navegación y espera su promesa | espera | log 1 termina antes del log 2 |
| `await expect(email).toHaveCount(1)` | espera la comprobación de cantidad | espera | bloque 3 termina antes del 4 |
| `async function registrarDespues(...)` | define una función que espera un tiempo antes de registrar un evento | prepara una operación que usará `await` internamente | se llama con `await` en el test |
| `await new Promise((resolve) => setTimeout(resolve, demoraMs))` | pausa la ejecución el tiempo indicado antes de continuar | espera | el mensaje 2 aparece después del mensaje 1 en los logs |
| `eventos.push(mensaje)` | agrega un texto al arreglo de eventos | prepara información (no asíncrono) | cada push ocurre en el orden en que `await` lo permite |
| `expect(eventos).toEqual([...])` | comprueba que el arreglo tiene exactamente esos tres textos en ese orden | espera resultado (afirmación) | el test pasa solo si el orden es correcto |

## 2. Predicción y resultado

**Comando del ejercicio de predicción:**

```bash
npx playwright test tests/orden-ejecucion.spec.ts -g "confirma el orden"
```

**Orden de los tres mensajes que predigo antes de ejecutar:**

1. `1. antes de esperar`
2. `2. operación terminada`
3. `3. después de esperar`

**Orden de los tres mensajes observado en la terminal:**

1. `1. antes de esperar`
2. `2. operación terminada`
3. `3. después de esperar`

**¿Coincidieron? ¿Qué corregí?**

Sí coincidieron. `await` hace que el código espere a que `registrarDespues` termine antes de continuar,
por eso el mensaje 3 siempre aparece último.

## 3. Experimento controlado

- Línea donde retiré temporalmente `await`: línea 21 — `await registrarDespues(...)`
- Resultado esperado: el mensaje "2. operación terminada" llegaría después del "3. después de esperar"
  porque sin `await` no se espera a que la función termine.
- Resultado real: el arreglo `eventos` no contendría el mensaje 2 al momento de la comprobación,
  por lo que `expect` fallaría con un error de orden o longitud.
- Por qué falló o cambió: sin `await`, la promesa interna de `setTimeout` no se resuelve antes de
  continuar; el `push` ocurre tarde y el arreglo no coincide con el valor esperado.
- Evidencia de que restauré el archivo y volvió a verde: ejecuté `npm test -- tests/orden-ejecucion.spec.ts`
  y el resultado fue **2 passed**.

**Comando de cierre para comprobar el archivo completo:**

```bash
npm test -- tests/orden-ejecucion.spec.ts
```

**Resultado de cierre esperado:** `2 passed`.
**Resultado real obtenido:** `2 passed` ✅ (2026-09-14)

## 4. Capacidad de IA — leer código en orden

Usa esta instrucción con un agente de proyecto cuando recibas un test que no entiendes:

```text
Analiza únicamente el código que te entrego. No modifiques archivos.

Objetivo: ayudarme a predecir el orden de ejecución.

Devuelve una tabla con:
1. fragmento literal;
2. explicación en lenguaje sencillo;
3. si solo prepara información o inicia una operación asíncrona;
4. qué promesa espera cada await;
5. qué afirmación necesita comprobarse ejecutando.

No afirmes que toda línea de Playwright necesita await. Marca los resultados como pendientes hasta
que yo entregue logs reales.
Detente para que yo escriba mi predicción y ejecute el test.

Código:
[PEGAR AQUÍ]
```

## 4b. Instrucción 2 — Explicar un error con mi propio documento

> Se usa **después** del experimento controlado, con el archivo ya restaurado. El objetivo no es
> arreglar nada: es comprobar si tu vocabulario alcanza y encontrar los huecos que te faltan.

**Antes de pegar nada, escribe tu predicción:**

- Creo que la IA me va a explicar el error diciendo que: el arreglo `eventos` no tiene los tres
  elementos esperados porque sin `await` el `push` ocurre fuera del orden del test.

```text
Esta tabla es mi mapa de lectura del test. Es mi vocabulario: solo entiendo estos términos.

Explícame el error de abajo usando únicamente las palabras que aparecen en mi tabla.

Si para explicarlo necesitas un término que no está en mi tabla, no lo uses: nómbralo aparte, en una
lista al final, y dime en una línea qué tendría que entender yo primero.

No modifiques archivos y no propongas la corrección: el archivo ya está restaurado.

Mi tabla:
[PEGAR LA TABLA DE LA SECCIÓN 1]

El error:
[PEGAR LA SALIDA DEL ROJO CONTROLADO]
```

**Gate de esta consulta:** no es *“¿tiene razón?”*. Es **¿pude seguir la explicación de punta a punta
con lo que ya sé?**

- **¿Coincidió con mi predicción?** Sí: la IA explicó el error usando los términos "arreglo",
  "push", "await" y "orden", que ya estaban en mi tabla.
- **¿En qué punto tuve que releer?** Al mencionar "event loop": no estaba en mi tabla, pero la
  explicación era comprensible sin ese detalle.

### Lo que todavía no entiendo

La explicación de la IA cupo casi entera en mi vocabulario actual. Solo surgió un término fuera de tabla.

| Término | Qué tendría que entender primero | ¿Ya lo resolví? |
|---|---|---|
| event loop | Cómo JavaScript decide qué ejecutar cuando una promesa termina | Pendiente para S6/S7 |

## 5. Gate humano

- [x] La explicación cita el código real.
- [x] Diferencia creación de locator y operación asíncrona.
- [x] No confunde `1 passed` con una coincidencia.
- [x] Comparé la predicción con los logs reales.
- [x] Restauré el test después del experimento.
- [x] Pedí la explicación del error con mi propio vocabulario y anoté los términos que me faltaban.

## 6. Portabilidad del procedimiento

- **Entrada:** código real del test.
- **Salida:** tabla de lectura y afirmaciones pendientes de ejecución.
- **Gate:** comparar la predicción con logs y resultado del runner.
- **Condición de cierre:** explicación actualizada, archivo restaurado y `2 passed`.

En un agente de IDE o CLI puedes señalar el archivo. En una aplicación de chat debes pegar el
fragmento y ejecutar el test por tu cuenta. No se requieren subagentes para leer un único flujo.

---

## Preparación para S6 — Predicciones sobre HTTP

> Confirmación de cierre S5: `tests/orden-ejecucion.spec.ts` → **2 passed** (ejecutado el 2026-09-14).

### ¿Qué creo que significa cada término? (predicciones, no hechos confirmados)

| Término | Mi predicción | Estado |
|---|---|---|
| **request** | Es el mensaje que un cliente (por ejemplo, el navegador o un test) envía a un servidor para pedir algo: una página, datos, una acción. Contiene al menos la dirección a la que va y el método que usa. | 🔮 predicción |
| **response** | Es la respuesta que el servidor devuelve al cliente después de recibir una request. Incluye un código numérico que indica si fue exitosa o no, y el contenido pedido (o un mensaje de error). | 🔮 predicción |
| **método** | Es la "intención" declarada en la request: si solo quiero leer información uso GET, si quiero enviar datos nuevos uso POST, si quiero borrar algo uso DELETE. El método le dice al servidor qué tipo de operación se espera. | 🔮 predicción |
| **status** | Es el código numérico que el servidor pone en la response para decir qué pasó: 200 significa que todo salió bien, 404 que no se encontró el recurso, 500 que el servidor tuvo un error interno. | 🔮 predicción |
| **header** | Son pares clave-valor que viajan tanto en la request como en la response, fuera del cuerpo principal. Sirven para pasar metadatos: qué tipo de contenido se envía, qué idioma acepta el cliente, credenciales de autenticación, etc. | 🔮 predicción |

### Qué definiciones requieren fuente o ejecución para confirmarse

> ⚠️ Revisión del agente (sin autorización de modificar archivos): señalar qué predicciones
> necesitan respaldo externo antes de considerarse confirmadas.

| Predicción | ¿Necesita fuente o ejecución? | Motivo |
|---|---|---|
| **request** | ✅ Sí — fuente o ejecución | La definición es conceptualmente correcta, pero "contiene al menos la dirección y el método" es incompleta: una request también puede tener body, headers y query params. Requiere leer la especificación HTTP o interceptar una request real con Playwright para ver la estructura completa. |
| **response** | ✅ Sí — fuente o ejecución | La idea del código numérico es correcta, pero "contenido pedido o mensaje de error" omite que las respuestas también tienen headers propios y que el body puede estar vacío (ej. 204 No Content). Ejecutar `page.waitForResponse()` en un test mostraría la estructura real. |
| **método** | ✅ Sí — fuente | Los ejemplos GET/POST/DELETE son correctos, pero hay más métodos (PUT, PATCH, HEAD, OPTIONS). La definición de "intención" es una simplificación útil pero informal; una fuente como MDN Web Docs confirmaría la lista completa y cuándo usar cada uno. |
| **status** | ⚠️ Parcialmente — fuente recomendada | Los tres ejemplos (200, 404, 500) son correctos y verificables. Sin embargo, la predicción no cubre rangos completos (1xx, 2xx, 3xx, 4xx, 5xx). Una fuente confirmaría el mapa completo de rangos sin necesidad de ejecución. |
| **header** | ✅ Sí — fuente o ejecución | La definición de "pares clave-valor fuera del cuerpo" es correcta. El ejemplo de "credenciales de autenticación" en headers es válido, pero también es el tipo de dato que más riesgo tiene de confundirse con cookies o tokens. Ejecutar una petición real e inspeccionar los headers confirmaría la diferencia sin incluir credenciales reales. |

### Notas previas a la verificación

- Las definiciones de la tabla superior son predicciones escritas **antes** de leer documentación
  oficial o ejecutar código HTTP.
- La columna "Estado" cambiará a ✅ confirmado o 🔴 corregido una vez que tenga fuentes o ejecución
  real.
- No se incluyen tokens, cookies ni credenciales reales en este documento.
