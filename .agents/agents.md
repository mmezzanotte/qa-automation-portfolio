# Agents — QA Automation Portfolio

Configuración y catálogo de agentes disponibles para este proyecto.

---

## Agentes configurados

### Agente de proyecto (IDE / CLI)

Rol principal en las sesiones de trabajo del portfolio.

**Permisos:**
- ✅ Leer archivos del repositorio
- ✅ Proponer cambios
- ✅ Ejecutar comandos de diagnóstico (lectura)
- ❌ Modificar archivos sin aprobación explícita
- ❌ Ejecutar comandos que alteren el estado del repositorio sin aprobación

**Instrucciones base:**
Ver `.agents/rules/qa-reglas.md`

---

## Skills disponibles

| Skill | Carpeta | Cuándo usarla |
|---|---|---|
| `priorizar-automatizacion` | `.agents/skills/priorizar-automatizacion/` | Cuando el humano entrega una lista de candidatos de prueba y quiere saber cuáles automatizar primero |

---

## Cómo activar una skill

El humano puede activar una skill con una instrucción como:

```text
Usa la skill priorizar-automatizacion con estos candidatos: [lista]
```

O el agente puede sugerirla cuando detecta que el contexto lo amerita, pero
**no la activa sin que el humano lo confirme**.

---

## Cómo agregar una skill nueva

1. Crear una carpeta en `.agents/skills/<nombre-skill>/`
2. Agregar un archivo `SKILL.md` con:
   - Frontmatter YAML: `name` y `description`
   - Cuándo se activa
   - Entradas esperadas
   - Pasos del procedimiento
   - Límites y salida esperada
3. Registrar la skill en este archivo (`agents.md`)

---

## Portabilidad

Este repositorio sigue el estándar de agentes portables:

- Las instrucciones del agente viven en el repositorio, no en la herramienta.
- Cualquier agente compatible con este estándar puede leer `.agents/` y operar
  con las mismas reglas.
- Si la herramienta no soporta `.agents/`, el humano pega las reglas manualmente
  al inicio de la conversación.

Ver `docs/guia-portabilidad-ia.md` para más detalles.
