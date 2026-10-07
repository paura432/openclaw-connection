---
name: 4geeks-progress-summary
description: Resume el progreso en los proyectos de 4Geeks Academy: entregados, aprobados y pendientes.
---

# 4Geeks Progress Summary

## Cuándo usar

Usa esta skill cuando el usuario quiera una visión general de su progreso en los proyectos de 4Geeks, sin el listado detallado de cada uno.

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

4. Clasifica cada proyecto según los datos reales:

   | Campo `task_status` | Interpretación |
   |---|---|
   | `"PENDING"` | No entregado |
   | `"DONE"` | Entregado |

   Del subconjunto de entregados (`task_status: "DONE"`), clasifica por `revision_status`:

   | `revision_status` | Interpretación |
   |---|---|
   | `"APPROVED"` | Corregido y aprobado |
   | `"REJECTED"` | Corregido y rechazado — requiere cambios |
   | `"PENDING"` o `null` o ausente | Entregado, pendiente de corrección |

5. Calcula los totales:

   - **Total** de proyectos recibidos.
   - **Entregados** (`task_status: "DONE"`).
   - **Corregidos/aprobados** (`revision_status: "APPROVED"`).
   - **Porcentaje de entregados** = (entregados / total) × 100, redondeado a entero.
   - **Aprobados** = entregados con `revision_status: "APPROVED"`.
   - **Esperando revisión** = entregados con `revision_status: "PENDING"` o `null`.
   - **Requieren cambios** = entregados con `revision_status: "REJECTED"`.
   - **Sin entregar** = `task_status: "PENDING"`.

6. Responde con un resumen numérico claro. No incluyas la lista completa de proyectos. Ejemplo:
   ```
   Proyectos totales:        9
   Entregados:               7  (78%)
   Aprobados:                4
   Esperando revisión:       2
   Requieren cambios:        1
   Sin entregar:             2
   ```

## Output esperado

La skill no modifica archivos. Solo informa al usuario el resumen numérico de su progreso.