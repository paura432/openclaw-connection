# TOOLS.md - Connected Services

Documenta únicamente herramientas realmente disponibles para el agente.

## Google Docs

### Create Document From Text

**Cuándo usarla**
- Cuando el usuario pide crear un documento.
- Cuando una skill necesita guardar contenido estructurado.

**Datos mínimos**
- Título.
- Contenido del documento.

**Si faltan datos**
- Si falta el título y puede inferirse de forma segura, usar uno descriptivo.
- Si falta contenido esencial, preguntar antes de crear el documento.

**Reglas**
- No inventar información ausente.
- Confirmar qué documento se ha creado.
- No exponer datos sensibles innecesarios.

---

## Google Calendar

### Create Event

**Cuándo usarla**
- Cuando el usuario pide crear o calendarizar un evento.
- Cuando una skill necesita reservar tiempo explícitamente.

**Datos mínimos**
- Título.
- Fecha.
- Hora.
- Duración o hora de finalización.

**Si faltan datos**
- Preguntar únicamente por los datos imprescindibles que impidan crear correctamente el evento.

**Reglas**
- No crear eventos si el usuario solo pidió una propuesta de planificación.
- Confirmar fecha, hora y duración del evento creado.
- No inventar asistentes, ubicaciones o recordatorios.

---

## Telegram

**Cuándo usarlo**
- Para recibir solicitudes del usuario.
- Para responder y confirmar resultados desde el canal conectado.

**Reglas**
- No enviar mensajes no solicitados salvo que una automatización configurada lo requiera.
- No incluir tokens, API keys ni credenciales en mensajes.
- Confirmar de forma breve el resultado de acciones ejecutadas.

---

## General Tool Rules

- Usar únicamente herramientas realmente disponibles.
- No afirmar que una acción se completó si la herramienta no confirmó éxito.
- Pedir confirmación antes de acciones irreversibles o sensibles.
- Minimizar el acceso a datos y herramientas al estrictamente necesario.
