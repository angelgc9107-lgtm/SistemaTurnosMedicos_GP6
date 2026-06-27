# Copilot Agent Mode - COORDINADOR Y DEVOPS
Se utilizó Copilot para realizar las reviews a las PR.

## Prompt utilizado
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request 
---LINK DE PR--
INSTRUCCIONES IMPORTANTES: Identifica SOLO problemas reales del código Enumera los hallazgos (1, 2, 3...) Cada hallazgo debe ser independiente Sé claro, técnico y concreto No inventes problemas hipotéticos sin evidencia en el código No incluyas sugerencias de tests PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA: ════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro) Severidad: (baja | media | alta | crítica) Explicación técnica: Por qué esto es un problema real. Sugerencia de mejora: Cambio concreto recomendado. Ejemplo de código corregido (si aplica): DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia Justificación del revisor humano: (Completar manualmente si se rechaza) ════════════════════════════════════════════════════════════ Al final agrega: RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos. DECISIÓN FINAL SUGERIDA POR IA: APPROVE REQUEST CHANGES COMMENT ONLY ⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
``` 
## Archivos utilizados como contexto
- Pull requests

## Interacciones realizadas 

### Interacción 1: 
**Prompt utilizado**
``` 
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request 
@angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/211
INSTRUCCIONES IMPORTANTES: Identifica SOLO problemas reales del código Enumera los hallazgos (1, 2, 3...) Cada hallazgo debe ser independiente Sé claro, técnico y concreto No inventes problemas hipotéticos sin evidencia en el código No incluyas sugerencias de tests PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA: ════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro) Severidad: (baja | media | alta | crítica) Explicación técnica: Por qué esto es un problema real. Sugerencia de mejora: Cambio concreto recomendado. Ejemplo de código corregido (si aplica): DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia Justificación del revisor humano: (Completar manualmente si se rechaza) ════════════════════════════════════════════════════════════ Al final agrega: RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos. DECISIÓN FINAL SUGERIDA POR IA: APPROVE REQUEST CHANGES COMMENT ONLY ⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
```

**Respuesta:** Copilot generó la Review

**Observación:** Copilot trabajo correctamente.

### Interacción 2: 
**Prompt utilizado**
``` 
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request 
@angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/214
INSTRUCCIONES IMPORTANTES: Identifica SOLO problemas reales del código Enumera los hallazgos (1, 2, 3...) Cada hallazgo debe ser independiente Sé claro, técnico y concreto No inventes problemas hipotéticos sin evidencia en el código No incluyas sugerencias de tests PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA: ════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro) Severidad: (baja | media | alta | crítica) Explicación técnica: Por qué esto es un problema real. Sugerencia de mejora: Cambio concreto recomendado. Ejemplo de código corregido (si aplica): DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia Justificación del revisor humano: (Completar manualmente si se rechaza) ════════════════════════════════════════════════════════════ Al final agrega: RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos. DECISIÓN FINAL SUGERIDA POR IA: APPROVE REQUEST CHANGES COMMENT ONLY ⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
```

**Respuesta:** Copilot generó la Review

**Observación:** Copilot trabajo correctamente.

### Interacción 3: 
**Prompt utilizado**
``` 
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request 
@angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/211
INSTRUCCIONES IMPORTANTES: Identifica SOLO problemas reales del código Enumera los hallazgos (1, 2, 3...) Cada hallazgo debe ser independiente Sé claro, técnico y concreto No inventes problemas hipotéticos sin evidencia en el código No incluyas sugerencias de tests PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA: ════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro) Severidad: (baja | media | alta | crítica) Explicación técnica: Por qué esto es un problema real. Sugerencia de mejora: Cambio concreto recomendado. Ejemplo de código corregido (si aplica): DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia Justificación del revisor humano: (Completar manualmente si se rechaza) ════════════════════════════════════════════════════════════ Al final agrega: RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos. DECISIÓN FINAL SUGERIDA POR IA: APPROVE REQUEST CHANGES COMMENT ONLY ⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
``` 

**Respuesta:** Copilot generó la Review. 

**Observación:** Copilot se confundio con las lineas ya corregidas y las lineas eliminadas, tuve que aclararle que las rojas eran lineas eliminadas del archivo.

### Interacción 4: 
**Prompt utilizado**
``` 
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request 
@angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/214
INSTRUCCIONES IMPORTANTES: Identifica SOLO problemas reales del código Enumera los hallazgos (1, 2, 3...) Cada hallazgo debe ser independiente Sé claro, técnico y concreto No inventes problemas hipotéticos sin evidencia en el código No incluyas sugerencias de tests PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA: ════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro) Severidad: (baja | media | alta | crítica) Explicación técnica: Por qué esto es un problema real. Sugerencia de mejora: Cambio concreto recomendado. Ejemplo de código corregido (si aplica): DECISIÓN DEL REVISOR HUMANO: [ ] Aceptar sugerencia [ ] Rechazar sugerencia Justificación del revisor humano: (Completar manualmente si se rechaza) ════════════════════════════════════════════════════════════ Al final agrega: RESUMEN GENERAL DE LA PR: Evaluación global y riesgos técnicos. DECISIÓN FINAL SUGERIDA POR IA: APPROVE REQUEST CHANGES COMMENT ONLY ⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario.
```

**Respuesta:** Copilot generó la Review. 

**Observación:** Al tener esa aclaración en la corrección de la PR anterior, copilot respondió bien esta vez.