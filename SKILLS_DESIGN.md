# SKILLS_DESIGN.md

## Skill 1: weekly-planner

### 1. ¿Qué hace esta skill?

Convierte los objetivos y compromisos de una semana en un plan priorizado, genera un Google Doc estructurado y, cuando el usuario lo solicita o confirma, crea los bloques importantes en Google Calendar.

### 2. ¿Qué input necesita?

El usuario proporciona:

- Objetivos de la semana.
- Compromisos fijos conocidos.
- Restricciones horarias opcionales.
- Prioridades opcionales.
- Fechas o duraciones cuando sean relevantes.

El agente ya conoce por sus archivos de configuración:

- El idioma preferido.
- La zona horaria.
- El estilo de respuesta.
- Las reglas de seguridad y confirmación.

Si falta información imprescindible para crear eventos de Calendar, debe preguntar únicamente por esos datos.

### 3. ¿Cómo es un buen output?

Un buen resultado incluye un Google Doc con:

- Objetivos de la semana.
- Prioridades.
- Plan organizado por días.
- Tareas clave.
- Riesgos o bloqueos.
- Próximos pasos.

Si el usuario ha solicitado calendarizar el plan, también incluye los eventos correspondientes en Google Calendar.

La respuesta final resume qué documento y qué eventos se han creado.

### Herramientas

- Google Docs.
- Google Calendar.

### Cuándo preguntar

Preguntar si falta alguno de estos datos necesarios para Calendar:

- Fecha.
- Hora.
- Duración.

No preguntar por información que pueda omitirse sin afectar al resultado.

### Criterios de éxito

- El plan está priorizado y es accionable.
- El Google Doc se crea correctamente.
- Los eventos solo se crean si el usuario los solicita o confirma.
- Las fechas y duraciones coinciden con la petición.
- No se inventan compromisos.

### Casos de error

- Si Google Docs falla, informar del fallo y no afirmar que el documento existe.
- Si Calendar falla, mantener el plan en el documento e informar de qué eventos no pudieron crearse.
- Si faltan datos imprescindibles, pedirlos antes de ejecutar la acción.


---

## Skill 2: meeting-notes

### 1. ¿Qué hace esta skill?

Convierte notas en bruto de una reunión en un documento estructurado con resumen, decisiones, acciones, preguntas abiertas y próximos pasos.

### 2. ¿Qué input necesita?

El usuario proporciona:

- Notas o texto de la reunión.
- Título opcional.
- Fecha opcional.

El agente utiliza su configuración existente para mantener el idioma y estilo de salida.

No necesita ninguna integración nueva.

### 3. ¿Cómo es un buen output?

Un Google Doc estructurado con:

- Título.
- Resumen.
- Decisiones.
- Acciones.
- Responsable, solo si aparece explícitamente en las notas.
- Preguntas abiertas.
- Próximos pasos.

La respuesta final confirma que el documento se creó y resume brevemente su contenido.

### Herramientas

- Google Docs.

### Cuándo preguntar

Preguntar únicamente si falta información que impida cumplir la petición.

El título puede generarse de forma descriptiva si el usuario no especifica uno.

### Criterios de éxito

- El contenido está organizado y es fácil de revisar.
- Las decisiones se distinguen de las acciones.
- No se inventan responsables.
- No se inventan fechas.
- No se inventan decisiones.
- El documento se crea correctamente.

### Casos de error

- Si Google Docs falla, informar claramente del fallo.
- Si las notas son demasiado ambiguas, estructurar únicamente la información explícita.
- Nunca completar huecos con información inventada.
