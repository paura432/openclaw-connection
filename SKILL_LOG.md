# SKILL_LOG.md

## 4geeks-auth-check — 2026-10-07

**Prompt:** Verificar si mi sesión de 4Geeks está activa.

**Endpoint probado:**
```
GET https://breathecode.herokuapp.com/v1/admissions/user/me
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200 — Sesión activa.

**Datos obtenidos:**
- Usuario: Pau Ramos (pauramosimo@gmail.com)
- Cohorte activa: `spain-aie-devs-pt-1` (kickoff 2026-09-21, ending 2027-02-10)
- Estado educacional: `ACTIVE`
- Estado financiero: `UP_TO_DATE`
- Role: `STUDENT`
- Academy: 4Geeks Madrid

---

## 4geeks-projects — 2026-10-07

**Prompt:** Mostrar mis proyectos de 4Geeks y su estado.

**Endpoint probado:**
```
GET https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200 — 9 proyectos obtenidos.

---

## 4geeks-pending-work — 2026-10-07

**Prompt:** Decirme exactamente qué proyectos de 4Geeks me quedan por hacer o corregir.

**Endpoint probado:**
```
GET https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200 — filtrado aplicado.

---

## 4geeks-progress-summary — 2026-10-07

**Prompt:** Resumir mi progreso en los proyectos de 4Geeks.

**Endpoint probado:**
```
GET https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200

**Procesamiento de datos reales (corregido):**

| Concepto | Cantidad |
|---|---|
| Proyectos totales | 9 |
| Entregados (`DONE`) | 7 |
| % entregados | 78% |
| Aprobados (`APPROVED`) | 4 |
| Esperando revisión (`PENDING`/`null`) | 2 |
| Requieren cambios (`REJECTED`) | 1 |
| Sin entregar (`PENDING`) | 2 |

**Decisión:** Skill corregida y verificada funcional.

---

## 4geeks-recent-activity — 2026-10-07

**Prompt:** Mostrar mi actividad reciente en 4Geeks.

**Endpoint primario probado:**
```
GET https://breathecode.herokuapp.com/v1/activity/me
Authorization: Token <FOURGEEKS_TOKEN>
Academy: 6
```

**Resultado:** ❌ HTTP 403 — `don't have this capability: read_activity for academy 6`

**Endpoint fallback probado:**
```
GET https://breathecode.herokuapp.com/v1/assignment/user/me/task
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200 — 40 tareas obtenidas.

**Top 10 actividades más recientes (ordenadas por updated_at):**

| # | Tipo | Título | Última actualización | Estado |
|---|------|--------|---------------------|--------|
| 1 | EXERCISE | Agent Skill Creation | 2026-10-07T20:36 | PENDING |
| 2 | PROJECT | Building context from an existing project - Financial dashboard | 2026-10-07T20:10 | DONE / PENDING |
| 3 | PROJECT | My 4Geeks Assistant — Teaching OpenClaw to Track Your Progress | 2026-10-07T16:44 | PENDING |
| 4 | EXERCISE | How to Make Your Agent Interact with a System | 2026-10-07T16:44 | PENDING |
| 5 | EXERCISE | Connecting OpenClaw with 4Geeks Academy | 2026-10-07T16:44 | PENDING |
| 6 | EXERCISE | Managing Secrets and Environment Variables in OpenClaw | 2026-10-07T16:44 | PENDING |
| 7 | PROJECT | Setting Up Your Personal AI Agent with OpenClaw | 2026-10-06T03:56 | DONE / APPROVED ✅ |
| 8 | PROJECT | Operations Backoffice – Inventory Manager | 2026-10-05T19:00 | DONE / PENDING |
| 9 | PROJECT | My Agent, My Way: Teaching Your Personal Assistant New Skills | 2026-10-05T18:34 | DONE / APPROVED ✅ |
| 10 | EXERCISE | OpenClaw Advanced Concepts for Beginners | 2026-10-05T17:09 | PENDING |

**Decisión:** Skill creada, probada con datos reales. El endpoint primario no está disponible (falta permiso `read_activity`), pero el fallback funciona correctamente.

---

## 4geeks-cohorts — 2026-10-07

**Prompt:** Mostrar mis cohortes/cursos de 4Geeks y su estado.

**Endpoint primario probado:**
```
GET https://breathecode.herokuapp.com/v1/admissions/academy/cohort/me
Authorization: Token <FOURGEEKS_TOKEN>
Academy: 6
```

**Resultado:** ✅ HTTP 200 — Array vacío `[]`

**Endpoint fallback probado:**
```
GET https://breathecode.herokuapp.com/v1/admissions/user/me
Authorization: Token <FOURGEEKS_TOKEN>
```

**Resultado:** ✅ HTTP 200 — 17 cohorts únicas vía `user/me.cohorts[]`

**Observación:** El endpoint específico de cohorts requiere header `Academy: <numeric_id>` y devuelve `[]` para academy 6 (4Geeks Madrid), a pesar de que el usuario pertenece a esa academia. El endpoint `/v1/admissions/user/me` incluye el campo `cohorts[]` con la misma información. La skill documenta ambos caminos.

**Datos obtenidos:** 17 cohortes únicas:

| # | Cohorte | educational_status | stage |
|---|---------|-------------------|-------|
| 1 | spain-aie-devs-pt-1 | ACTIVE | PREWORK 🚀 |
| 2 | Working with AI coding agents | ACTIVE | INACTIVE |
| 3 | Personal assistants with Openclaw | GRADUATED 🎓 | INACTIVE |
| 4 | Advanced personal assistants with Openclaw | ACTIVE | INACTIVE |
| 5 | Agentic Workflows | ACTIVE | INACTIVE |
| 6 | Container applications with Docker | ACTIVE | INACTIVE |
| 7 | Implementing Data Pipelines | ACTIVE | INACTIVE |
| 8 | Asynchronous processing and offloading | ACTIVE | INACTIVE |
| 9 | Models training & RAG | ACTIVE | INACTIVE |
| 10 | Agentic Engineering | ACTIVE | INACTIVE |
| 11 | Application telemetry | ACTIVE | INACTIVE |
| 12 | Coding Fundamentals with Typescript | ACTIVE | INACTIVE |
| 13 | Ai Engineering Project Delivery | ACTIVE | INACTIVE |
| 14 | Intro to 4Geeks Method | ACTIVE | INACTIVE |
| 15 | Real-Time Communication | ACTIVE | INACTIVE |
| 16 | Secure AI Applications | ACTIVE | INACTIVE |
| 17 | Architecture optimization | ACTIVE | INACTIVE |

**Duplicados:** Ninguno detectado (todos los slugs son únicos).

**Decisión:** Skill creada, probada con datos reales y verificada funcional.