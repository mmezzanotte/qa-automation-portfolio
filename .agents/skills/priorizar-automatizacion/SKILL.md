---
name: priorizar-automatizacion
description: >-
  Analiza candidatos de prueba proporcionados por el usuario y produce una
  propuesta ordenada de priorización para automatización. Calcula un score
  basado en cuatro criterios (Frecuencia, Estabilidad, Riesgo, Mantenimiento),
  clasifica cada candidato en zona VERDE / AMARILLO / ROJO, e identifica
  información faltante, empates e inconsistencias. La Skill propone puntajes
  pero no toma decisiones finales, no firma el backlog ni decide prioridades
  de negocio: esas responsabilidades pertenecen al humano.
---

# Skill: priorizar-automatizacion

## 1. Cuándo se usa

Activar esta Skill cuando el usuario proporcione una lista de candidatos de
prueba y quiera saber cuáles conviene automatizar primero.

Requisitos mínimos para activarla:

- Al menos un candidato con nombre y fuente trazable.
- Algún contexto del equipo o del sistema bajo prueba (aunque sea parcial).

Si no hay candidatos con fuente, la Skill igual se ejecuta pero coloca todos
los candidatos en la lista de **"ideas sin fuente"** y no produce backlog
priorizado.

---

## 2. Entrada

La Skill espera que el usuario provea:

| Campo | Descripción |
|---|---|
| **Candidatos** | Lista de pruebas o flujos a evaluar |
| **Fuente** | Origen trazable de cada candidato (ticket, documento, bug report, etc.) |
| **Contexto del equipo** | Tamaño del equipo, capacidad de mantenimiento, stack, etc. |
| **Contexto del sistema** | Frecuencia de cambios, áreas críticas, historial de fallos |

Si alguno de estos campos está ausente o es parcial, la Skill continúa y
marca los valores afectados con `SIN CONTEXTO`.

---

## 3. Pasos

### Paso 1 — Validar candidatos

Para cada candidato, verificar:

- ¿Tiene nombre claro?
- ¿Tiene fuente trazable?
- ¿La información es consistente (no contradictoria)?
- ¿Es verificable con lo proporcionado?

Resultado:

- Candidatos **completos** → pasan al scoring.
- Candidatos **sin fuente** → van a lista separada de "ideas sin fuente", no
  se incluyen en el backlog priorizado.
- Candidatos **incompletos pero con fuente** → pasan al scoring; los campos
  sin datos se marcan `SIN CONTEXTO` con indicación de qué falta.

### Paso 2 — Puntuar cada candidato

Escala: **1 = bajo · 2 = medio · 3 = alto**
Los cuatro criterios apuntan en la misma dirección: **3 = mejor candidato**.

| Criterio | Qué mide | Cuándo es 3 |
|---|---|---|
| **Frecuencia** | Con qué frecuencia se ejecuta o se necesita verificar este flujo | Se ejecuta o verifica muy seguido |
| **Estabilidad** | Qué tan estable es el flujo para ser automatizado | El flujo cambia poco; la prueba no se romperá constantemente |
| **Riesgo** | Qué impacto tiene un fallo en producción | Fallo crítico: pérdida de datos, dinero, seguridad o reputación |
| **Mantenimiento** | Qué tan fácil es mantener la prueba automatizada | Poco acoplamiento, selectores estables, lógica simple |

Fórmula:

Score = Frecuencia + Estabilidad + Riesgo + Mantenimiento

Rango posible: 4 – 12.

Si un valor no puede justificarse con la información disponible:

- Escribir `SIN CONTEXTO` en esa celda.
- En la columna **Información faltante**, indicar exactamente qué dato se
  necesitaría para asignar el puntaje.
- No calcular Score parcial como si fuera total; indicar que el Score es
  **INCOMPLETO**.

### Paso 3 — Clasificar por zona

| Score | Zona |
|---|---|
| 10 – 12 | VERDE |
| 7 – 9 | AMARILLO |
| 4 – 6 | ROJO |
| INCOMPLETO | SIN CLASIFICAR |

### Paso 4 — Detectar situaciones especiales

Identificar y documentar en la columna **Observaciones**:

- **Empate**: dos o más candidatos con el mismo Score.
- **Información contradictoria**: datos que se contradicen entre sí.
- **Información no verificable**: afirmaciones que no pueden confirmarse con
  lo proporcionado.
- **Candidato incompleto**: faltan uno o más criterios.

### Paso 5 — Ordenar el backlog priorizado

Ordenar de mayor a menor Score. En caso de empate, listar en el orden en que
fueron proporcionados y marcarlo en Observaciones.

---

## 4. Límites

La Skill **NO debe**:

- Tomar la decisión final de qué automatizar.
- Escribir la razón de la decisión.
- Inventar candidatos, fuentes o puntajes.
- Asumir información que no fue proporcionada.
- Convertir una inferencia en un hecho.
- Decidir prioridades de negocio.
- Firmar el backlog.

Si algo no puede justificarse con la información disponible → `SIN CONTEXTO`.

---

## 5. Cuándo pide decisión humana

La Skill debe detenerse y pedir input humano cuando:

- **Empate en zona VERDE**: dos o más candidatos con Score 10–12 y el
  contexto no permite distinguirlos.
- **Contradicción crítica**: la información es tan contradictoria que asignar
  un puntaje sería engañoso.
- **Sin candidatos válidos**: todos los candidatos carecen de fuente o están
  tan incompletos que no hay backlog posible.
- **Ambigüedad de alcance**: no está claro si el candidato es un único caso
  de prueba o un conjunto de pruebas.

En esos casos, la Skill presenta lo que pudo calcular e indica claramente
qué pregunta necesita respuesta antes de continuar.

---

## 6. Salida y Definition of Done

### Sección A — Backlog priorizado

Tabla ordenada de mayor a menor Score con candidatos que tienen fuente
trazable:

| ID | Candidato | Fuente | Frecuencia | Estabilidad | Riesgo | Mantenimiento | Score | Zona | Información faltante | Observaciones |
|---|---|---|---|---|---|---|---|---|---|---|

**Columnas que NO se incluyen:**

- Decisión
- Razón
- Qué cambiaría mi decisión

Esos tres campos pertenecen al humano.

### Sección B — Ideas sin fuente

Lista simple de candidatos que no tienen fuente trazable y por eso no
entran al backlog:

  - [Nombre del candidato] — motivo de exclusión: sin fuente trazable

### Sección C — Alertas

Lista de situaciones especiales detectadas (empates, contradicciones,
información no verificable, preguntas que requieren decisión humana).

### Definition of Done

La Skill completó su trabajo cuando:

- [ ] Todos los candidatos con fuente tienen Score o marcación SIN CONTEXTO justificada.
- [ ] Los candidatos sin fuente están en Sección B.
- [ ] Las alertas están documentadas en Sección C.
- [ ] No se incluyeron los campos Decisión, Razón ni "Qué cambiaría mi decisión".
- [ ] Si hay empates en VERDE, se indicó en Sección C y se pidió input humano.
