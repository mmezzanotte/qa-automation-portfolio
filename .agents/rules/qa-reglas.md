# Reglas del agente — QA Automation Portfolio

Estas reglas definen cómo debe comportarse el agente de IA cuando trabaja en este
repositorio. Se aplican en todas las sesiones, salvo instrucción explícita del humano
que indique lo contrario.

---

## Regla 1 — No modificar archivos sin aprobación explícita

Antes de modificar cualquier archivo del repositorio, el agente debe:

1. Presentar el análisis del problema.
2. Proponer el cambio mínimo necesario.
3. Indicar el archivo y la línea afectados.
4. **Detenerse y esperar aprobación explícita del humano.**

Un "listo" o "parece correcto" del humano no es aprobación. La aprobación es una
instrucción que menciona el cambio propuesto.

---

## Regla 2 — No inventar información

El agente no debe:

- Inventar selectores, locators ni datos de prueba.
- Afirmar que un test pasó sin evidencia de ejecución.
- Asumir que un elemento existe en el DOM sin haberlo comprobado.
- Completar campos de tablas con valores no verificables.

Si la información no está disponible, el agente escribe `SIN CONTEXTO` y señala
qué dato faltaría para completarlo.

---

## Regla 3 — Diagnóstico antes que solución

Cuando un test falla, el agente sigue el flujo de `docs/flujo-ia-diagnostico-fallos.md`:

1. Identificar la causa más probable.
2. Citar la evidencia observable.
3. Señalar el archivo y la línea.
4. Proponer el cambio mínimo.
5. **Detenerse antes de aplicar cualquier cambio.**

---

## Regla 4 — Alcance mínimo

Cada cambio propuesto debe ser el mínimo necesario para resolver el problema
identificado. El agente no debe:

- Agregar esperas arbitrarias (`waitForTimeout`).
- Agregar dependencias no solicitadas.
- Crear archivos nuevos fuera del alcance pedido.
- Refactorizar código no relacionado con el problema.

---

## Regla 5 — Trazabilidad

Cada test o caso de prueba que el agente ayude a crear debe tener fuente trazable:
un número de HU, un bug report, un caso documentado en `docs/`, o una instrucción
explícita del humano con contexto suficiente.

Un test sin fuente no se registra como backlog priorizado.

---

## Regla 6 — No incluir datos privados

El agente no debe incluir en ningún archivo:

- Credenciales reales (emails, contraseñas, tokens).
- Datos personales identificables.
- Claves de API o variables de entorno con valores reales.

Si necesita datos de prueba, usa valores claramente ficticios (ej: `usuario@ejemplo.com`).

---

## Aplicación

Estas reglas se aplican a todos los agentes que trabajen en este repositorio,
incluyendo agentes de IDE, CLI y aplicaciones de chat. Si una herramienta no permite
configurar reglas directamente, el humano debe pegarlas al inicio de la conversación.
