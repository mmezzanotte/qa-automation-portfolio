# HU-Login — Historia de Usuario

> Fuente: definición del curso / backlog del proyecto portfolio  
> Playground: https://playground.calidadsinhumo.com/login

---

## Historia de usuario

**Como** usuario registrado,  
**quiero** poder iniciar sesión con mi email y contraseña,  
**para** acceder a las funciones del sistema de manera segura.

---

## Criterios de aceptación

### CA-L01 — Login exitoso

**Dado** que el usuario tiene credenciales válidas  
**Cuando** ingresa su email y contraseña correctos y hace clic en "Iniciar sesión"  
**Entonces** el sistema redirige al dashboard y muestra un mensaje de bienvenida

### CA-L02 — Credenciales inválidas

**Dado** que el usuario ingresa credenciales incorrectas  
**Cuando** hace clic en "Iniciar sesión"  
**Entonces** el sistema muestra un mensaje de error y permanece en la página de login

### CA-L03 — Campos requeridos

**Dado** que el usuario no completa algún campo requerido  
**Cuando** hace clic en "Iniciar sesión"  
**Entonces** el sistema muestra mensajes de validación para los campos vacíos

### CA-L04 — Formato de email

**Dado** que el usuario ingresa un email con formato inválido  
**Cuando** hace clic en "Iniciar sesión"  
**Entonces** el sistema muestra un mensaje de validación de formato

---

## Elementos de la pantalla

| Elemento | Tipo | Locator preferido |
|---|---|---|
| Campo Email | Input tipo email | `getByLabel('Email')` |
| Campo Contraseña | Input tipo password | `getByLabel('Contraseña')` |
| Botón Iniciar sesión | Button | `getByRole('button', { name: 'Iniciar sesión' })` |
| Mensaje de error | Texto | `getByText(...)` o por clase |
| Enlace a Registro | Link | `getByRole('link', { name: 'Regístrate' })` |

---

## Casos de prueba derivados

Ver `docs/casos-login.md` para la lista completa de casos de prueba con sus pasos
y criterios de aceptación observables.

---

## Notas de implementación

- URL del playground: `https://playground.calidadsinhumo.com/login`
- No incluir credenciales reales en ningún archivo del repositorio
- Los locators se comprueban en DevTools antes de usarlos en tests (ver `docs/mapa-selectores.md`)

---

## Estado

| CA | Descripción | Caso de prueba | Automatizado |
|---|---|---|---|
| CA-L01 | Login exitoso | CP-L01 | ❌ |
| CA-L02 | Credenciales inválidas | CP-L02, CP-L03 | ❌ |
| CA-L03 | Campos requeridos | CP-L04 | ❌ |
| CA-L04 | Formato de email | CP-L05 | ❌ |
