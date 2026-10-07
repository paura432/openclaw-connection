---
name: 4geeks-recent-activity
description: Muestra la actividad reciente de 4Geeks Academy del usuario autenticado.
---

# 4Geeks Recent Activity

## Cuándo usar

Usa esta skill cuando el usuario quiera ver su actividad reciente en 4Geeks Academy: tareas creadas, proyectos entregados, ejercicios abiertos o cualquier cambio en sus asignaciones.

## Secreto requerido

- `FOURGEEKS_TOKEN` — Token de autenticación para la API de BreatheCode/4Geeks.

## Endpoint primario

- **URL base:** `https://breathecode.herokuapp.com`
- **Ruta:** `GET /v1/activity/me`
- **Autenticación:** `Authorization: Token <token>`
- **Header requerido:** `Academy: <numeric_academy_id>` (ID numérico de la academia, ej. `6` para 4Geeks Madrid)

> ⚠️ **Nota:** Este endpoint requiere el permiso `read_activity`, que no todos los usuarios tienen. Si devuelve `403`, usa el endpoint de tareas como fallback (ver sección Fallback).

## Fallback

Cuando el endpoint primario no está disponible:

- **Ruta:** `GET /v1/assignment/user/me/task`
- **Autenticación:** `Authorization: Token <token>`
- **Sin header Academy requerido**

La respuesta incluye un array de tareas con campos de timestamp que permiten determinar la actividad reciente.

## Procedimiento

1. Obtén el token del secreto `FOURGEEKS_TOKEN` usando `secrets(action="list")` para verificar que existe. **No muestres, loguees ni hardcodees el valor del token.**

2. **Intenta el endpoint primario:** Realiza una petición HTTP GET a `https://breathecode.herokuapp.com/v1/activity/me` con los headers:
   ```
   Authorization: Token <token>
   Academy: <academy_id_numérico>
   ```
   Usa `exec` con `curl`, pasando el token por variable de entorno para no exponerlo.

3. Interpreta el resultado del endpoint primario:
   - **200** — Datos de actividad obtenidos. Procesa el array de actividades.
   - **403 con `don't have this capability: read_activity`** — Cambia al fallback (paso 4).
   - **401** — Token inválido. Indica al usuario.
   - **Otro / error de red** — Informa del error.

4. **Fallback:** Consulta `https://breathecode.herokuapp.com/v1/assignment/user/me/task` (sin filtro de `task_type` para obtener todas las tareas: PROJECT, EXERCISE, LESSON, QUIZ, etc.).

   La respuesta es un objeto con:
   ```json
   {
     "count": <número_total>,
     "results": [ ... ]
   }
   ```

5. De cada elemento del array (`results`), extrae los campos relevantes para actividad:
   - `title` — Nombre de la tarea/actividad.
   - `task_type` — Tipo (`PROJECT`, `EXERCISE`, `LESSON`, `QUIZ`, etc.).
   - `task_status` — Estado actual (`PENDING`, `DONE`, etc.).
   - `revision_status` — Estado de revisión (`APPROVED`, `REJECTED`, `PENDING`, o `null`).
   - `created_at` — Fecha de creación.
   - `updated_at` — Fecha de última actualización.
   - `associated_slug` — Slug identificador.

6. **Ordena** todas las tareas por `updated_at` descendente (más reciente primero). Si `updated_at` no existe, usa `created_at`.

7. **Limita a 10** las más recientes.

8. Para cada actividad, muestra:
   - Fecha y hora de la última actualización.
   - Tipo (PROJECT, EXERCISE, etc.).
   - Título.
   - Estado actual y estado de revisión.
   - Cualquier otro campo real presente que aporte contexto.

9. Si no hay tareas (array vacío), indica claramente que no hay actividad registrada.

10. **No inventes campos ni interpretes valores no contemplados.** Si aparece un valor desconocido, muéstrarlo literalmente.

## Interpretación de actividad

Usa las señales en los datos para describir la actividad:

| Señal | Significado |
|---|---|
| `task_type: "PROJECT"` | Proyecto |
| `task_type: "EXERCISE"` | Ejercicio |
| `task_type: "LESSON"` | Lección |
| `task_type: "QUIZ"` | Cuestionario |
| `task_status: "DONE"` + `revision_status: "APPROVED"` | ✅ Completado y aprobado |
| `task_status: "DONE"` + `revision_status: "REJECTED"` | ❌ Entregado pero rechazado |
| `task_status: "DONE"` + (`revision_status: null` o `"PENDING"`) | ✅ Entregado, esperando revisión |
| `task_status: "PENDING"` | ⏳ Pendiente (no entregado / por hacer) |
| Otros valores | Mostrar literalmente |

## Output esperado

La skill no modifica archivos. Solo informa al usuario las 10 actividades más recientes con fecha, tipo, título y estado.