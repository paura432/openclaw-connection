---
name: weekly-planner
description: Convierte objetivos y compromisos semanales en un plan priorizado, lo guarda en Google Docs y, si el usuario lo pide, crea bloques en Google Calendar.
---

# Weekly Planner

## Cuándo usar

Usa esta skill cuando el usuario quiera organizar, planificar o calendarizar su semana.

## Input

Extrae del mensaje, si existen:

- objetivos;
- compromisos fijos;
- prioridades;
- restricciones horarias;
- fechas;
- duraciones.

Usa Europe/Madrid como zona horaria salvo que el usuario indique otra.

## Procedimiento

1. Ordena los objetivos por prioridad.
2. Distribuye las tareas de forma realista por días.
3. No inventes fechas, compromisos ni duraciones.
4. Crea un Google Doc con:
   - Objetivos
   - Prioridades
   - Plan por días
   - Tareas clave
   - Riesgos o bloqueos
   - Próximos pasos
5. Usa las herramientas de Google Docs disponibles vía Zapier.
6. Crea eventos en Google Calendar solo si el usuario lo pide o confirma explícitamente.
7. Si para Calendar falta fecha, hora o duración imprescindible, pregunta únicamente por ese dato.
8. Verifica el resultado de cada herramienta antes de afirmar que se completó.

## Output

Responde de forma breve indicando:

- documento creado;
- eventos creados, si aplica;
- cualquier dato pendiente o error real.

No repitas todo el contenido del documento en el chat.

## Calendar reliability

- For calendar events, prefer structured event creation over natural-language or quick-add creation.
- Resolve relative weekdays into explicit calendar dates before calling the tool.
- Always provide explicit start time and end time or duration.
- Use the user's timezone from USER.md.
- Never report an event as created unless the calendar tool confirms success.
- If one event fails, continue with the remaining valid events and report exactly which one failed.

## Calendar reliability

- Prefer structured event creation over natural-language or quick-add creation.
- Resolve relative weekdays into explicit calendar dates before calling the tool.
- Always provide explicit start time and end time or duration.
- Use the user's timezone from USER.md.
- Never report an event as created unless the calendar tool confirms success.
- If one event fails, continue with the remaining valid events and report exactly which one failed.
