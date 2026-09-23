# Estrategia de automatización — QA Portfolio

> Documento vivo. Se actualiza al cerrar cada sesión de trabajo.  
> Fuente de verdad para decidir qué automatizar y por qué.

---

## 1. Objetivo

Definir los criterios, alcance y límites de la automatización de pruebas en este
portfolio, de manera que cualquier decisión de "qué automatizar" tenga una razón
trazable y no sea arbitraria.

---

## 2. Criterios de selección

Un caso de prueba entra al backlog de automatización si cumple al menos tres de estos cuatro criterios:

| Criterio | Descripción | Peso |
|---|---|---|
| **Frecuencia** | Se ejecuta en cada ciclo de regresión | Alto |
| **Estabilidad** | El flujo no cambia con frecuencia | Alto |
| **Riesgo** | Un fallo tiene impacto crítico en producción | Alto |
| **Mantenimiento** | El test no requiere esfuerzo excesivo de mantenimiento | Medio |

> Ver `docs/` → skill `priorizar-automatizacion` para el procedimiento de scoring.

---

## 3. Alcance actual

### Incluido

- Flujos de autenticación: login y registro
- Validaciones de formularios críticos
- Flujos E2E de alta frecuencia

### Excluido (por ahora)

- Pruebas exploratorias
- Pruebas de usabilidad
- Pruebas de carga y performance
- Casos de baja frecuencia o bajo riesgo

---

## 4. Stack tecnológico

| Herramienta | Rol |
|---|---|
| **Playwright** | Framework de automatización E2E |
| **TypeScript** | Lenguaje de los tests |
| **Node.js** | Runtime |
| **Git** | Control de versiones y evidencia |

---

## 5. Estructura de tests

```
tests/
├── e2e/          → Tests de flujo completo (usuario final)
├── api/          → Tests de capa de API (HTTP)
├── primer-ciclo.spec.ts       → Validación del setup inicial
├── comprobar-locators.spec.ts → Verificación de selectores
├── comprobar-propuesta-ia.spec.ts → Gate de propuestas de IA
└── orden-ejecucion.spec.ts    → Comprensión de async/await
```

---

## 6. Convenciones

- **Nombres de archivos:** `kebab-case.spec.ts`
- **Nombres de tests:** describen el comportamiento observable, no la implementación
- **Locators:** se prefiere `getByLabel`, `getByRole`, `getByText` antes que CSS puro
- **Datos de prueba:** no incluir credenciales reales en ningún archivo

---

## 7. Flujo de trabajo

```
1. Identificar candidato (HU, bug report, criterio de negocio)
2. Puntuar con skill priorizar-automatizacion
3. Escribir el caso de prueba en docs/
4. Implementar el test en tests/
5. Ejecutar y guardar evidencia en evidence/
6. Hacer commit con mensaje descriptivo
```

---

## 8. Definition of Done para un test automatizado

- [ ] El test tiene fuente trazable (HU, bug o caso documentado en `docs/`)
- [ ] El test pasa de manera estable en al menos dos ejecuciones consecutivas
- [ ] La evidencia está guardada en `evidence/`
- [ ] El commit tiene mensaje que identifica la sesión y el cambio
- [ ] No hay datos privados ni credenciales reales en el código

---

## 9. Casos del login — priorizados con skill priorizar-automatizacion

> Corrida ejecutada el 2026-09-23 sobre los 8 casos de `docs/casos-login.md`.
> Skill usada: `priorizar-automatizacion` · Firmado por: Maria

### Backlog priorizado

| ID | Candidato | Frecuencia | Estabilidad | Riesgo | Mantenimiento | Score | Zona | Decisión | Razón |
|---|---|---|---|---|---|---|---|---|---|
| CP-L01 | Login exitoso con credenciales válidas | 3 | 3 | 3 | 3 | **12** | 🟢 VERDE | Automatizar | Flujo crítico de alta frecuencia, locators estables, impacto directo en acceso al sistema |
| CP-L08 | Mensaje de bienvenida con nombre — REQ-L04 | 3 | 3 | 3 | 2 | **11** | 🟢 VERDE | Automatizar | Verifica comportamiento post-login que depende del backend; alta frecuencia, riesgo de regresión alto |
| CP-L02 | Login con contraseña incorrecta | 3 | 3 | 2 | 3 | **11** | 🟢 VERDE | Automatizar | Cubre REQ-L02 directamente; frecuente en regresión, locators del mismo formulario |
| CP-L03 | Login con email no registrado | 2 | 3 | 2 | 3 | **10** | 🟢 VERDE | Automatizar | Variante del flujo de error; mismo formulario, bajo costo de mantenimiento |
| CP-L04 | Campos vacíos (ambos) | 2 | 3 | 2 | 3 | **10** | 🟢 VERDE | Automatizar | Validación de HTML nativo o JS; estable y de bajo mantenimiento |
| CP-L06 | Solo email, sin contraseña | 2 | 3 | 1 | 3 | **9** | 🟡 AMARILLO | Automatizar | Valor límite de CA-L03; comparte setup con CP-L04, bajo costo incremental |
| CP-L07 | Solo contraseña, sin email | 2 | 3 | 1 | 3 | **9** | 🟡 AMARILLO | Automatizar | Ídem CP-L06; separados por mi límite propio de la skill |
| CP-L05 | Formato de email inválido | 1 | 3 | 1 | 3 | **8** | 🟡 AMARILLO | No automatizar por ahora | Validación de formato delegable al browser (HTML5); frecuencia baja y riesgo bajo; revisar en C10 |

### ¿Alguno de los ocho no vale la pena automatizar?

**CP-L05** — Formato de email inválido. La validación de formato de email es manejada por el atributo `type="email"` del navegador en la mayoría de los casos. El riesgo es bajo (no da acceso indebido al sistema) y la frecuencia de fallo es baja. Se puede verificar manualmente en cada ciclo de regresión hasta que haya evidencia de que falla con frecuencia.

---

## 10. Historial de decisiones

| Sesión | Decisión | Razón |
|---|---|---|
| S1 | Usar Playwright + TypeScript | Stack estándar del curso; soporte activo |
| S2 | Empezar por login antes que registro | Mayor frecuencia y riesgo |
| S3 | Preferir locators de Playwright sobre CSS puro | Más legibles y menos frágiles |
| S4 | Documentar candidatos antes de automatizar | Evita automatizar lo incorrecto |
