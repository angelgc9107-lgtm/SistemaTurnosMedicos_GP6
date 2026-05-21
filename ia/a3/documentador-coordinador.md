# Uso de Copilot Agent Mode - Documentador y Coordinador
## Prompt utilizado
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request:

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
## Archivos utilizados como contexto
- Pull requests

## Interacciones realizadas

### Interacción 1:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: @angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/142

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot generó análisis detallado identificando 7 hallazgos reales, con énfasis en:
- LlegadaPaciente elevado a swimlane (viola niveles de abstracción)
- Inconsistencia Secretaria vs Recepcionista (no coincide con tarjetas CRC)
- Changelog truncado (no cumple estándar)
- Ciclos implícitos sin límite

**Observación:** Copilot se volvia muy repetitivo en algunos hallazgos.

### Interacción 2:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/146

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot generó 6 hallazgos, identificando como MÁS CRÍTICO el #1 (changelog truncado) pero después el #2 (ambigüedad en swimlanes CU-03) como lo que realmente afecta comprensión arquitectónica.

**Observación:** Se observó que el hallazgo #1 no era correcto ya que se usó el formato corrrecto en changelog.md

### Interacción 3:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/141

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot identificó #5 hallazgos relacionados con consistencia del modelo orientado a objetos, nomenclatura de mensajes UML, documentación y coherencia entre tarjetas CRC y diagramas de secuencia. Entre las observaciones detectadas se encontraron inconsistencias en la jerarquía de `Persona`, problemas semánticos en nombres de mensajes (`notificarPacienteEnSala`), ausencia de contexto en archivos índice y ambigüedad entre los roles `Secretaria` y `Recepcionista` dentro del modelo de dominio.

**Observación:** Copilot logró detectar inconsistencias reales de diseño OO y nomenclatura UML que afectaban la coherencia del modelo del sistema. Las sugerencias relacionadas con la jerarquía de clases, responsabilidades de actores y nombres de mensajes fueron aceptadas debido a que mejoraban la trazabilidad entre tarjetas CRC, diagramas de secuencia y documentación del dominio.

### Interacción 4:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/141

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot generó una CODE REVIEW con #5 hallazgos reales, y marcó como criticos los hallazgos #5, #1, #3, #4.

**Observación:** Durante la revisión de la PR se detectaron principalmente observaciones relacionadas con la coherencia del modelo OO y la documentación asociada a los diagramas de secuencia.

### Interacción 5:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: @angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/142

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot generó #6 hallazgos, mientras que se rechazaron las observaciones sobre el changelog y espaciado (hallazgos #2 y #3) por considerarse incorrectas.

**Observación:** Permitió identificar posibles mejoras de modelado, consistencia y legibilidad en los diagramas y documentación asociada a la PR [#142](https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/142). Sin embargo, la revisión humana fue necesaria para validar la pertinencia de cada hallazgo, ya que algunos comentarios generados por Copilot correspondían a interpretaciones incorrectas del formato esperado.

### Interacción 6:
**Promp Usado:**
```
Actúa como un Senior Software Engineer realizando una code review profesional de esta Pull Request: https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/146

INSTRUCCIONES IMPORTANTES:

• Identifica SOLO problemas reales del código 

• Enumera los hallazgos (1, 2, 3...) 

• Cada hallazgo debe ser independiente Sé claro, técnico y concreto 

• No inventes problemas hipotéticos sin evidencia en el código

• No incluyas sugerencias de tests 

• PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:
════════════════════════════════════════════════════════════ HALLAZGO #<número> Archivo: Línea: 

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

⚠️ Nota importante: Si seleccionas "COMMENT ONLY", no completes la sección "DECISIÓN DEL REVISOR HUMANO". Debes quedar vía para edición manual en el Pull Request en la sección correspondiente. Publica comentarios directamente en el código si lo consideras necesario. Primero en chat antes de publicar el comentario, tengo que aprobarlo yo Segundo tene en cuenta lo siguiente para hacer el analisis: Agregar al menos 1 review adicional con CHANGES_REQUESTED, comentarios inline en el diff, y análisis de diseño OO (LlegadaPaciente ausente, falta tarjeta Persona, Recepcionista vs Secretaria, changelog multi-línea).
```
**Respuesta:** Copilot detectó problemas de modelado UML y consistencia de diseño OO, recomendando REQUEST CHANGES. Tras la revisión humana, se rechazaron los hallazgos #1 y #2 por ser falsos positivos, y se aceptaron las demás observaciones técnicas.

**Observación:** Se observó que los hallazgos #1 y #2 correspondían a falsos positivos generados por Copilot. El formato utilizado en changelog.md era válido según el criterio del proyecto y no existían líneas duplicadas en diagramasUML.md, sino un reemplazo correcto de contenido.