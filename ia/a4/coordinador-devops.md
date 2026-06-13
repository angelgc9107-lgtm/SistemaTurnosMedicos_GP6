# Coordinador de Repositorio

## Review 1 - PR #171

**Autor:** angelgc9107-lgtm  
**Rama:** feature/analista-cu-2-3-add-anexo-cu2-cu3  
**Fecha:** Junio 2026

### Objetivo de la revisión

Verificar consistencia entre diagramas de clases, anexos funcionales, documentación de IA, tarjetas CRC y requisitos funcionales correspondientes a los Casos de Uso 2 y 3.

---

## Prompt utilizado

```text
Actúa como un Senior Software Engineer realizando una revisión de código profesional de esta Pull Request https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/171

INSTRUCCIONES IMPORTANTES:
Identifica SOLO problemas reales del código
Enumera los hallazgos (1, 2, 3...)
Cada hallazgo debe ser independiente claro
Sé técnico y concreto
No inventes problemas hipotéticos sin evidencia en el código
No incluyes sugerencias de pruebas

PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:

════════════════════════════════════
HALLAZGO #<número>

Archivo:
Línea:
Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro)
Severidad: (baja | media | alta | crítica)

Explicación técnica:
Por qué esto es un problema real.

Sugerencia de mejora:
Cambio concreto recomendado.

Ejemplo de código corregido (si aplica):

DECISIÓN DEL REVISOR HUMANO:
[ ] Aceptar sugerencia
[ ] Rechazar sugerencia

Justificación del revisor humano:
(Completar manualmente si se rechaza)

════════════════════════════════════

Al final agrega:

RESUMEN GENERAL DE LA PR:
Evaluación global y riesgos técnicos.

DECISIÓN FINAL SUGERIDA POR IA:
APROBAR
SOLICITUD CAMBIOS
SÓLO COMENTARIOS

Nota importante:
Si seleccionas "SÓLO COMENTARIOS", no completa la sección "DECISIÓN DEL REVISOR HUMANO".
Debes dejar vía para edición manual en el Pull Request en la sección correspondiente.
Publica comentarios directamente en el código si lo consideras necesario.
```

---

## Archivos revisados

- herramientas-agile/tarjetas-crc/tarjetas_crc.md
- herramientas-agile/tarjetas-crc/08-tarjeta-crc-control-sistemas.md
- anexos/analisis-funcional/02-caso-de-uso-registrar-checkin.md
- anexos/analisis-funcional/03-caso-de-uso-reprogramar-turno.md
- diagramas/01-diagrama-clases/02-clase-registrar-checkin.puml
- diagramas/01-diagrama-clases/03-clase-reprogramar-turno.puml
- ia/a4/analista-cu-2-3.md

---

## Hallazgos detectados por Copilot

### Hallazgo 1
Referencia incorrecta en el índice de tarjetas CRC debido a una inconsistencia entre el nombre del archivo y la referencia utilizada en la documentación.

### Hallazgo 2
Error tipográfico en el nombre del archivo relacionado con la clase ControlSistema, generando inconsistencias de nomenclatura.

### Hallazgo 3
Ambigüedad en la relación de dependencia entre Agenda y LlegadaPaciente dentro de la documentación funcional.

### Hallazgo 4
Documentación UML incompleta en la nota descriptiva asociada a la clase ControlSistema.

### Hallazgo 5
Ambigüedad funcional en la interpretación del requisito RF7 respecto a las notificaciones y la reprogramación de recordatorios.

### Hallazgo 6
Cardinalidad no explicitada en la relación entre Agenda y ServicioNotificacion.

### Hallazgo 7
Pequeñas inconsistencias entre la documentación del proceso de IA y los diagramas generados.

---

## Ajustes solicitados

- Corregir referencias rotas en índices y documentación.
- Unificar la nomenclatura utilizada en archivos, diagramas y tarjetas CRC.
- Mejorar la trazabilidad entre requisitos funcionales y diagramas UML.
- Completar la documentación de las notas UML.
- Clarificar el comportamiento asociado al requisito RF7.
- Mantener consistencia entre documentación técnica y artefactos generados.

---

## Resultado de la revisión

Se solicitaron cambios antes de aprobar la Pull Request debido a inconsistencias de documentación, nomenclatura y trazabilidad detectadas durante la revisión asistida con IA.

---

## Conclusión

La revisión permitió detectar problemas de consistencia entre artefactos antes de la integración en la rama develop. Las observaciones realizadas contribuyen a mantener la calidad, trazabilidad y coherencia del proyecto.

**Estado final de la revisión:** Solicitud de cambios.

---

## Review 2 - PR #164

**Pull Request revisada:** #164  
**Título:** Reportaje/analista cu 4 5 agregar anexo cu4 cu5  
**Rama:** feature/analista-cu-4-5-add-anexo-cu4-cu5  
**Tipo de revisión:** Code review asistido con Copilot Agent Mode  

### Objetivo de la revisión

Verificar la coherencia entre diagramas de clases, anexos funcionales, documentación de IA, tarjetas CRC e índices correspondientes a los Casos de Uso 4 y 5.

---

### Prompt utilizado

```text
Actúa como un Senior Software Engineer realizando una revisión de código profesional de esta Pull Request https://github.com/angelgc9107-lgtm/SistemaTurnosMedicos_GP6/pull/164

INSTRUCCIONES IMPORTANTES:
Identifica SOLO problemas reales del código
Enumera los hallazgos (1, 2, 3...)
Cada hallazgo debe ser independiente claro
Sé, técnico y concreto
No inventes problemas hipotéticos sin evidencia en el código
No incluyes sugerencias de pruebas

PARA CADA HALLAZGO USA EXACTAMENTE ESTA ESTRUCTURA:

══════════════════════════════
══════════════════════════════
HALLAZGO #<número>

Archivo:
Línea:
Tipo de problema: (bug | performance | seguridad | legibilidad | diseño | otro)
Severidad: (baja | media | alta | crítica)

Explicación técnica:
Por qué esto es un problema real.

Sugerencia de mejora:
Cambio concreto recomendado.

Ejemplo de código corregido (si aplica):

DECISIÓN DEL REVISOR HUMANO:
[ ] Aceptar sugerencia
[ ] Rechazar sugerencia

Justificación del revisor humano:
(Completar manualmente si se rechaza)

══════════════════════════════
══════════════════════════════

Al final agrega:

RESUMEN GENERAL DE LA PR:
Evaluación global y riesgos técnicos.

DECISIÓN FINAL SUGERIDA POR IA:
APROBAR
SOLICITUD CAMBIOS
SÓLO COMENTARIOS

⚠️ Nota importante:
Si seleccionas "SÓLO COMENTARIOS", no completa la sección "DECISIÓN DEL REVISOR HUMANO".
Debes quedar vía para edición manual en el Pull Request en la sección correspondiente.
Publica comentarios directamente en el código si lo consideras necesario.
```

---

### Archivos revisados

- diagramas/01-diagrama-clases/04-clase-bloquear-horarios.puml
- diagramas/01-diagrama-clases/05-clase-visualizar-agenda.puml
- anexos/analisis-funcional/04-caso-de-uso-bloquear-horarios.md
- anexos/analisis-funcional/05-caso-de-uso-visualizar-agenda.md
- herramientas-agile/tarjetas-crc/tarjetas_crc.md
- ia/a4/analista-cu-4-5.md

---

### Hallazgos detectados por Copilot

#### Hallazgo 1
Inconsistencia entre el diagrama de clases CU-04 y el pseudocódigo del anexo, porque aparece `ControlSistema` como mediador en el diagrama pero el pseudocódigo delega directamente en `Agenda`.

#### Hallazgo 2
Inconsistencia similar en CU-05: `ControlSistema` aparece en el diagrama de clases, pero el pseudocódigo no refleja esa mediación.

#### Hallazgo 3
El pseudocódigo de CU-04 invoca clases o métodos que no están modelados en el diagrama de clases, como `ValidadorDisponibilidad` y `Resultado`.

#### Hallazgo 4
Ambigüedad en la relación entre `Agenda` y `GestorBloqueos`, porque el diagrama sugiere composición, pero el pseudocódigo lo usa como singleton.

#### Hallazgo 5
Uso de un parámetro indefinido (`cualquierHora`) en el pseudocódigo del anexo CU-05.

#### Hallazgo 6
Inconsistencia de nomenclatura en el índice de tarjetas CRC por numeración del archivo `010-tarjeta-crc-vista-calendario.md`.

---

### Ajustes solicitados

- Alinear el pseudocódigo con los diagramas de clases.
- Definir si `ControlSistema` participa como mediador o si debe eliminarse de los diagramas.
- Agregar al diagrama las clases utilizadas por el pseudocódigo o simplificar el pseudocódigo para no usar clases inexistentes.
- Clarificar si `GestorBloques/GestorBloqueos` se accede por composición o como singleton.
- Corregir parámetros indefinidos en pseudocódigo.
- Normalizar la nomenclatura de archivos en tarjetas CRC.

---

### Resultado de la revisión

La revisión fue publicada como comentario técnico en la PR.  
La decisión sugerida por la IA fue **SÓLO COMENTARIOS**, ya que los hallazgos afectan la claridad y coherencia documental, pero no bloquean funcionalidad ejecutable.

---

### Conclusión

La PR presenta una estructura completa y cumple con la entrega documental de los Casos de Uso 4 y 5. Sin embargo, se detectaron inconsistencias de trazabilidad entre diagramas UML, pseudocódigo y documentación, por lo que se recomendaron ajustes antes de la integración final.

**Estado final de la revisión:** Sólo comentarios.