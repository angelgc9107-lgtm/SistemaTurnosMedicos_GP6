# Uso de Copilot Agent Mode - Documentador y Coodinador

## Prompt utilizado
```
Actúa como un Senior Software Engineer realizando una code review profesional de la Pull Request.

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código

• Enumera los hallazgos (1, 2, 3...)

• Cada hallazgo debe ser independiente

• Sé claro, técnico y concreto

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests

PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:

════════════════════════════════════════════════════════════ HALLAZGO #<número>

Archivo: Línea:

Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro)

Severidad: (baja | media | alta | crítica)

Explicación técnica: Por qué esto es un problema real.

Sugerencia de mejora: Cambio concreto recomendado.

Ejemplo de código corregido (si aplica):

DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia

Justificación del revisor humano: (Completar manualmente si se rechaza)

════════════════════════════════════════════════════════════

Al final agrega:

RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos.

DECISIÓN FINAL SUGERIDA POR IA:

APPROVE

REQUEST CHANGES

COMMENT ONLY

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
```
## Archivos utilizados como contexto
- Pull requests

## Ajustes realizados
- Sistema de "Checklist" para el Revisor
- Se notifico mas en profundo los errores a los colaboradores
