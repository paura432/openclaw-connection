---
name: 4geeks-cohorts
description: Muestra las cohortes/cursos de 4Geeks Academy del usuario autenticado y su estado.
---

# 4Geeks Cohorts

## Cuándo usar

Usa esta skill cuando el usuario quiera ver sus cohortes (cursos) de 4Geeks Academy, su estado educativo y si están activas, graduadas o inactivas.

## Secreto requerido

- `FOURGEEKS_TOKEN` — Token de autenticación para la API de BreatheCode/4Geeks.

## Endpoint

- **URL base:** `https://breathecode.herokuapp.com`
- **Ruta:** `GET /v1/admissions/academy/cohort/me`
- **Autenticación:** `Authorization: Token <token>`
- **Header requerido:** `Academy: <numeric_academy_id>` (el ID numérico de la academia, ej. `6` para 4Geeks Madrid)

> ⚠️ **Nota:** Este endpoint requiere el header `Academy` con el ID numérico de la academia. Si devuelve un array vacío, usa el endpoint `/v1/admissions/user/me` como fallback, que incluye el campo `cohorts[]` con la misma información.

## Procedimiento

1. Obtén el token del secreto `FOURGEEKS_TOKEN` usando `secrets(action="list")` para verificar que existe. **No muestres, loguees ni hardcodees el valor del token.**

2. Realiza una petición HTTP GET a `https://breathecode.herokuapp.com/v1/admissions/academy/cohort/me` con los headers:
   ```
   Authorization: Token <token>
   Academy: <academy_id_numérico>
   ```
   Usa `exec` con `curl`, pasando el token por variable de entorno para no exponerlo.

3. Interpreta el código HTTP:
   - **200** — Datos obtenidos.
   - **400** — Academy ID inválido (no numérico).
   - **401** — Token inválido o no proporcionado.
   - **403** — Sin permisos para esa academia.
   - **Otro / error de red** — Informa del error.

4. **Si el endpoint devuelve array vacío (`[]`):** Prueba con otras academias o haz fallback a `/v1/admissions/user/me` y extrae el campo `cohorts[]` (que es un array de objetos relación usuario-cohorte).

5. Cada objeto en el array representa la relación usuario-cohorte y contiene:
   - `cohort.name` — Nombre de la cohorte.
   - `cohort.slug` — Slug identificador.
   - `role` — Rol del usuario en la cohorte (`STUDENT`, etc.).
   - `educational_status` — Estado educativo (`ACTIVE`, `GRADUATED`, etc.).
   - `finantial_status` — Estado financiero (`UP_TO_DATE`, `FULLY_PAID`, etc.).

6. Además, desde `cohort` se puede extraer:
   - `cohort.kickoff_date` — Fecha de inicio.
   - `cohort.ending_date` — Fecha de fin (si aplica).
   - `cohort.stage` — Etapa del cohorte (`PREWORK`, `INACTIVE`, etc.).
   - `cohort.academy.name` — Academia (ej. "4Geeks Madrid").
   - `cohort.current_day` — Día actual del programa (si aplica).

7. **Elimina duplicados** basándote en `cohort.slug`. Si un slug aparece más de una vez, conserva solo una entrada.

8. Para cada cohorte único, muestra nombre, estado y un indicador visual:

   | Señal en los datos | Interpretación |
   |---|---|
   | `educational_status: "ACTIVE"` | ✅ Activa — curso en curso |
   | `educational_status: "GRADUATED"` | 🎓 Graduado — completado |
   | Otro valor en `educational_status` | Mostrar el valor literal sin inventar |
   | `cohort.stage: "INACTIVE"` | 💤 Inactiva — cohorte finalizado o no vigente |
   | `cohort.stage: "PREWORK"` | 🚀 Prelanzamiento — empieza pronto |

   No inventes significados para valores no contemplados.

9. Responde al usuario con una lista clara de cohortes únicas, mostrando:
   - Nombre de la cohorte
   - `educational_status`
   - Indicador visual si está activa, graduada o inactiva
   - Otros campos relevantes sin inventar datos

## Output esperado

La skill no modifica archivos. Solo informa al usuario el listado de cohortes y su estado.