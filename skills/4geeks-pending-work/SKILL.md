---
name: 4geeks-pending-work
description: Muestra los proyectos de 4Geeks Academy pendientes de hacer o que requieren correcciones.
---

# 4Geeks Pending Work

## Cuándo usar

Usa esta skill cuando el usuario quiera saber qué proyectos de 4Geeks le quedan por hacer o necesita corregir, excluyendo los ya aprobados y los que están esperando revisión.

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

3. Interpreta el código HTTP:
   - **200** — Datos obtenidos. Procesa la lista.
   - **401** — Token inválido. Indica al usuario.
   - **403** — Sin permisos. Indica al usuario.
   - **Otro / error de red** — Informa del error.

4. Filtra los proyectos según estas reglas:

   | Condición | Acción |
   |---|---|
   | `task_status: "PENDING"` | ✅ Incluir — proyecto no entregado |
   | `revision_status: "REJECTED"` | ✅ Incluir — entregado pero requiere cambios |
   | `revision_status: "APPROVED"` | ❌ Excluir — ya aprobado |
   | `task_status: "DONE"` y `revision_status: "PENDING"` | ❌ Excluir — entregado, esperando revisión |
   | `task_status: "DONE"` y `revision_status: null` o ausente | ❌ Excluir — entregado sin revisión pendiente |
   | Otros valores | Mostrar el valor literal sin inventar significado |

   En resumen: solo muestra proyectos **pendientes de hacer** (`PENDING`) o **rechazados** (`REJECTED`).

5. Para cada proyecto incluido, extrae:
   - `title` — nombre del proyecto.
   - `task_status` — estado de la tarea.
   - `revision_status` — estado de revisión.
   - `associated_slug` — slug del proyecto.
   - `cohort.name` — nombre de la cohorte asociada.
   - `url` o `github_url` — enlace si existe.
   - `description` — feedback del revisor si existe (útil para proyectos rechazados).

6. Responde al usuario con una lista clara:
   - Separando **pendientes** de **rechazados**.
   - Incluyendo el feedback textual cuando `revision_status=REJECTED`.
   - Si no hay pendientes ni rechazados, indica que todo está al día.

## Output esperado

La skill no modifica archivos. Solo informa al usuario los proyectos pendientes y rechazados.