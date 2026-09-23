# HU-Registro — Historia de Usuario

> Fuente: definición del curso / backlog del proyecto portfolio  
> Playground: https://playground.calidadsinhumo.com/registro

---

## Historia de usuario

**Como** visitante sin cuenta,  
**quiero** poder crear una cuenta nueva con mi email y una contraseña,  
**para** acceder a las funciones del sistema como usuario registrado.

---

## Criterios de aceptación

### CA-R01 — Registro exitoso

**Dado** que el visitante completa todos los campos con datos válidos  
**Cuando** hace clic en "Registrarse"  
**Entonces** el sistema crea la cuenta y redirige al login o al dashboard con mensaje de confirmación

### CA-R02 — Email ya registrado

**Dado** que el visitante usa un email que ya existe en el sistema  
**Cuando** hace clic en "Registrarse"  
**Entonces** el sistema muestra un mensaje de error indicando que el email ya está en uso

### CA-R03 — Campos requeridos

**Dado** que el visitante no completa algún campo requerido  
**Cuando** hace clic en "Registrarse"  
**Entonces** el sistema muestra mensajes de validación para los campos vacíos

### CA-R04 — Formato de email

**Dado** que el visitante ingresa un email con formato inválido  
**Cuando** hace clic en "Registrarse"  
**Entonces** el sistema muestra un mensaje de validación de formato de email

### CA-R05 — Contraseña mínima

**Dado** que el visitante ingresa una contraseña que no cumple los requisitos mínimos  
**Cuando** hace clic en "Registrarse"  
**Entonces** el sistema muestra un mensaje indicando los requisitos de contraseña

---

## Elementos de la pantalla

| Elemento | Tipo | Locator preferido |
|---|---|---|
| Campo Nombre | Input tipo text | `getByLabel('Nombre')` |
| Campo Email | Input tipo email | `getByLabel('Email')` |
| Campo Contraseña | Input tipo password | `getByLabel('Contraseña')` |
| Botón Registrarse | Button | `getByRole('button', { name: 'Registrarse' })` |
| Mensaje de error | Texto | `getByText(...)` o por clase |
| Enlace a Login | Link | `getByRole('link', { name: 'Inicia sesión' })` |

---

## Relación con otras HU

| HU relacionada | Relación |
|---|---|
| HU-login | El usuario registrado aquí puede iniciar sesión en HU-login |

---

## Casos de prueba a derivar

> Esta sección se completa cuando se creen los casos formales en `docs/casos-registro.md`

| CA | Descripción | Caso de prueba | Automatizado |
|---|---|---|---|
| CA-R01 | Registro exitoso | CP-R01 (pendiente) | ❌ |
| CA-R02 | Email ya registrado | CP-R02 (pendiente) | ❌ |
| CA-R03 | Campos requeridos | CP-R03 (pendiente) | ❌ |
| CA-R04 | Formato de email | CP-R04 (pendiente) | ❌ |
| CA-R05 | Contraseña mínima | CP-R05 (pendiente) | ❌ |

---

## Notas de implementación

- URL del playground: `https://playground.calidadsinhumo.com/registro`
- No incluir credenciales reales en ningún archivo del repositorio
- Verificar los locators en DevTools antes de usarlos en tests
- El flujo de registro es previo al flujo de login; se puede usar como precondición en tests E2E
