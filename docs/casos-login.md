# Casos de prueba — Login

> Fuente: HU-login.md  
> Playground: https://playground.calidadsinhumo.com/login  
> **QA:** Maria  
> **Fecha:** 2026-09-23  
> **Herramienta usada:** skill `derivar-casos-de-hu` + revisión manual

## P6 — La pregunta que la IA no podía hacer

> Esta pregunta sale del contexto del equipo o del producto, no de la historia sola.

**¿Qué pasa si un usuario ya tiene sesión activa e intenta hacer login nuevamente desde otra pestaña?**  
La historia no lo dice. Depende de si el sistema permite sesiones múltiples o si invalida la anterior.
Sin esa definición, el caso no entra al backlog: se registra como incógnita en `docs/contrato-api.md` sección 5.

---

## Contexto

Estos casos derivan de la Historia de Usuario de Login y cubren los flujos principales
que se espera automatizar en sesiones posteriores. Cada caso tiene fuente trazable,
criterio de aceptación observable y estado de automatización.

---

## CP-L01 — Login exitoso con credenciales válidas

| Campo | Detalle |
|---|---|
| **ID** | CP-L01 |
| **HU** | HU-login |
| **Precondición** | Usuario registrado en el sistema |
| **Datos de entrada** | Email: usuario@ejemplo.com · Contraseña: correcta |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar email · 3. Ingresar contraseña · 4. Clic en "Iniciar sesión" |
| **Resultado esperado** | Redirige al dashboard; el mensaje de bienvenida es visible |
| **Criterio observable** | URL cambia; elemento de bienvenida aparece en pantalla |
| **Prioridad** | Alta |
| **Estado automatización** | Pendiente |

---

## CP-L02 — Login con contraseña incorrecta

| Campo | Detalle |
|---|---|
| **ID** | CP-L02 |
| **HU** | HU-login |
| **Precondición** | Usuario registrado en el sistema |
| **Datos de entrada** | Email: usuario@ejemplo.com · Contraseña: incorrecta |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar email · 3. Ingresar contraseña incorrecta · 4. Clic en "Iniciar sesión" |
| **Resultado esperado** | Permanece en `/login`; mensaje de error visible |
| **Criterio observable** | Mensaje de error con texto sobre credenciales inválidas |
| **Prioridad** | Alta |
| **Estado automatización** | Pendiente |

---

## CP-L03 — Login con email no registrado

| Campo | Detalle |
|---|---|
| **ID** | CP-L03 |
| **HU** | HU-login |
| **Precondición** | Email no existe en la base de datos |
| **Datos de entrada** | Email: noexiste@ejemplo.com · Contraseña: cualquiera |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar email inexistente · 3. Ingresar contraseña · 4. Clic en "Iniciar sesión" |
| **Resultado esperado** | Permanece en `/login`; mensaje de error visible |
| **Criterio observable** | Mensaje de error observable; no se accede al dashboard |
| **Prioridad** | Media |
| **Estado automatización** | Pendiente |

---

## CP-L04 — Login con campos vacíos

| Campo | Detalle |
|---|---|
| **ID** | CP-L04 |
| **HU** | HU-login |
| **Precondición** | Ninguna |
| **Datos de entrada** | Email: vacío · Contraseña: vacía |
| **Pasos** | 1. Abrir `/login` · 2. No ingresar datos · 3. Clic en "Iniciar sesión" |
| **Resultado esperado** | El formulario no se envía; mensajes de validación visibles |
| **Criterio observable** | Campos marcados como requeridos o mensaje de error en pantalla |
| **Prioridad** | Media |
| **Estado automatización** | Pendiente |

---

## CP-L05 — Login con email en formato inválido

| Campo | Detalle |
|---|---|
| **ID** | CP-L05 |
| **HU** | HU-login |
| **Precondición** | Ninguna |
| **Datos de entrada** | Email: texto-sin-arroba · Contraseña: cualquiera |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar email con formato incorrecto · 3. Clic en "Iniciar sesión" |
| **Resultado esperado** | El formulario muestra validación de formato de email |
| **Criterio observable** | Mensaje de validación de email visible |
| **Prioridad** | Baja |
| **Estado automatización** | Pendiente |

---

## CP-L06 — Login con solo email (sin contraseña)

| Campo | Detalle |
|---|---|
| **ID** | CP-L06 |
| **HU** | HU-login · CA-L03 |
| **Fuente** | «El formulario no se envía; mensajes de validación visibles» — CA-L03 |
| **Técnica** | Valor límite: campo contraseña vacío |
| **Precondición** | Ninguna |
| **Datos de entrada** | Email: usuario@ejemplo.com · Contraseña: vacía |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar email · 3. Dejar contraseña vacía · 4. Clic en "Iniciar sesión" |
| **Resultado esperado** | El formulario muestra validación en el campo contraseña |
| **Criterio observable** | Campo contraseña marcado como requerido; sin acceso al dashboard |
| **Prioridad** | Media |
| **Estado automatización** | Pendiente |

---

## CP-L07 — Login con solo contraseña (sin email)

| Campo | Detalle |
|---|---|
| **ID** | CP-L07 |
| **HU** | HU-login · CA-L03 |
| **Fuente** | «El formulario no se envía; mensajes de validación visibles» — CA-L03 |
| **Técnica** | Valor límite: campo email vacío |
| **Precondición** | Ninguna |
| **Datos de entrada** | Email: vacío · Contraseña: cualquiera |
| **Pasos** | 1. Abrir `/login` · 2. Dejar email vacío · 3. Ingresar contraseña · 4. Clic en "Iniciar sesión" |
| **Resultado esperado** | El formulario muestra validación en el campo email |
| **Criterio observable** | Campo email marcado como requerido; sin acceso al dashboard |
| **Prioridad** | Media |
| **Estado automatización** | Pendiente |

---

## CP-L08 — Verificar mensaje de bienvenida con nombre del usuario tras login exitoso

| Campo | Detalle |
|---|---|
| **ID** | CP-L08 |
| **HU** | HU-login · CA-L01 |
| **Fuente** | REQ-L04: «Tras un login exitoso, el sistema muestra un mensaje de bienvenida con el nombre del usuario» |
| **Técnica** | Partición de equivalencia: login válido con nombre conocido |
| **Precondición** | Usuario registrado con nombre conocido |
| **Datos de entrada** | Email: usuario@ejemplo.com · Contraseña: correcta |
| **Pasos** | 1. Abrir `/login` · 2. Ingresar credenciales válidas · 3. Clic en "Iniciar sesión" · 4. Verificar mensaje de bienvenida |
| **Resultado esperado** | El mensaje de bienvenida contiene el nombre del usuario registrado |
| **Criterio observable** | Texto visible con el nombre del usuario en el dashboard |
| **Prioridad** | Alta |
| **Estado automatización** | Pendiente |

---

## Estado general

| ID | Descripción | CA | Técnica | Prioridad | Automatizado |
|---|---|---|---|---|---|
| CP-L01 | Login exitoso | CA-L01 | Partición de equivalencia | Alta | ❌ |
| CP-L02 | Contraseña incorrecta | CA-L02 | Partición de equivalencia | Alta | ❌ |
| CP-L03 | Email no registrado | CA-L02 | Partición de equivalencia | Media | ❌ |
| CP-L04 | Campos vacíos (ambos) | CA-L03 | Valor límite | Media | ❌ |
| CP-L05 | Formato de email inválido | CA-L04 | Valor límite | Baja | ❌ |
| CP-L06 | Solo email, sin contraseña | CA-L03 | Valor límite | Media | ❌ |
| CP-L07 | Solo contraseña, sin email | CA-L03 | Valor límite | Media | ❌ |
| CP-L08 | Mensaje de bienvenida con nombre | CA-L01 · REQ-L04 | Partición de equivalencia | Alta | ❌ |

> Actualizar esta tabla cuando un caso pase a automatizado y tenga evidencia de ejecución.
