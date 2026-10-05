---
name: meeting-notes
description: Convierte notas en bruto de una reunión en un Google Doc estructurado con resumen, decisiones, acciones y próximos pasos.
---

# Meeting Notes

## Cuándo usar

Usa esta skill cuando el usuario proporcione apuntes, transcripción o notas de una reunión y quiera organizarlas o guardarlas.

## Input

Necesita:

- notas de la reunión;
- título opcional;
- fecha opcional.

Si no hay título, genera uno breve y descriptivo.

## Procedimiento

1. Analiza únicamente la información proporcionada.
2. No inventes decisiones, responsables, fechas ni compromisos.
3. Organiza el contenido en:
   - Resumen
   - Decisiones
   - Acciones
   - Responsables, solo si aparecen explícitamente
   - Preguntas abiertas
   - Próximos pasos
4. Crea el resultado con la herramienta disponible de Google Docs vía Zapier.
5. Verifica que la herramienta confirme la creación antes de declararla completada.
6. Si las notas son ambiguas, conserva la ambigüedad en vez de rellenar huecos.

## Output

Confirma brevemente:

- título del documento;
- creación correcta;
- número de decisiones y acciones detectadas, si es útil.

No reproduzcas todo el documento en el chat.
