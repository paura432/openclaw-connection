---
name: 4geeks-projects
description: Obtiene los proyectos de 4Geeks Academy del usuario autenticado y muestra su estado.
---

# 4Geeks Projects

## Cuándo usar

Usa esta skill cuando el usuario quiera ver sus proyectos de 4Geeks Academy, su estado y entregas.

## Secreto requerido

- `FOURGEEKS_TOKEN` — Token de autenticación para la API de BreatheCode/4Geeks.

## Endpoint

- **URL base:** `https://breathecode.herokuapp.com`
- **Ruta:** `GET /v1/assignment/user/me/task?task_type=PROJECT`
- **Autenticación:** `Authorization: Token <token>`

## Procedimiento

1. Obtén el token del secreto `FOURGEEKS_TOKEN`. **No muestres, loguees ni hardcodees el valor del token.**

2. Realiza una petición HTTP GET a `https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT` con el header:
   ```
   Authorization: Token <token>
   ```
   Usa `exec` con `curl`, pasando el token por variable de entorno para no exponerlo.

3. Interpreta la respuesta:
   - **HTTP 200** — Lista de proyectos obtenida correctamente.
   - **HTTP 401** — Token inválido o no proporcionado.
   - **HTTP 403** — Token válido pero sin permisos suficientes.
   - **Error de red / otro código** — Informar del error y sugerir reintentar.

4. Para cada proyecto en la respuesta, extrae:
   - `title` — nombre del proyecto.
   - `task_status` — estado actual de la tarea.
   - `revision_status` — estado de revisión/corrección.
   - `task_type` — tipo (debe ser `PROJECT`).
   - `associated_slug` — slug del proyecto.
   - `url` — enlace al proyecto si existe.
   - Cualquier campo adicional relevante que contenga información de estado o entrega.

5. Clasifica cada proyecto según los datos reales:

   | Señal en los datos | Interpretación |
   |---|---|
   | `task_status: "PENDING"` | ⏳ Pendiente — no entregado |
   | `task_status: "DONE"` y `revision_status: null` o ausente | ✅ Entregado, pendiente de corrección |
   | `task_status: "DONE"` y `revision_status: "APPROVED"` | ✅ Aprobado / corregido |
   | `task_status: "DONE"` y `revision_status: "PENDING"` | ✅ Entregado, esperando revisión |
   | `task_status: "DONE"` y `revision_status: "REJECTED"` | ❌ Rechazado — necesita cambios |
   | Otros valores | Mostrar el valor literal sin inventar significado |

   No inventes estados. Si un campo no existe, no lo asumas.

6. Responde al usuario con una tabla o lista clara con todos los proyectos y su estado.

## Output esperado

La skill no modifica archivos. Solo informa al usuario el listado de proyectos con su estado real.