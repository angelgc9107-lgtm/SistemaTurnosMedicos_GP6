# Uso de Copilot Agent Mode - Analista Funcional de Casos de Uso 4 y 5 

## Prompt utilizado

```
- Construir los anexos completos correspondientes a los casos de uso 4 y 5 del sistema, integrando trazabilidad, diagramas previos, diagrama de clases y pseudocódigo orientado a objetos.  
- Diseñar diagramas de clases específicos para cada caso de uso utilizando PlantUML.  
- Asegurar coherencia entre requisitos funcionales, escenarios, diagramas de actividades, diagramas de secuencia y tarjetas CRC previamente desarrolladas. 

Al generar cada diagrama de clases tomaras como contexto estos archivos: 
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- diagramas/02-casos-de-uso/02-bloquear-horarios-04.png
- diagramas/02-casos-de-uso/02-bloquear-horarios-04.puml
- diagramas/02-casos-de-uso/02-visualizar-agenda-05.png
- diagramas/02-casos-de-uso/02-visualizar-agenda-05.puml
- diagramas/03-escenarios-casos-de-uso/03-bloquear-horarios-flujo-principal.md
- diagramas/03-escenarios-casos-de-uso/02-visualizar-agenda-flujo-principal.md
- diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.png
- diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.puml
- diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.png
- diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.puml
- diagramas/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.png
- diagramas/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.puml
- diagramas/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png
- diagramas/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.puml
- herramientas-agile/tarjetas-crc/

Utilizar obligatoriamente la plantilla 
https://drive.google.com/file/d/1stT7qZHuwbZixM1HTtNI048ugE0su6wK/view. No se aceptarán anexos que no sigan la estructura definida en la plantilla. 

Debes crear los anexos en: 
anexos/analisis-funcional/04-caso-de-uso-nombre-del-caso-de-uso.md y 
anexos/analisis-funcional/05-caso-de-uso-nombre-del-caso-de-uso.md. 

Debes redactar los anexos markdown por caso de uso incluyendo: 
○ Descripción del caso de uso y trazabilidad con requisitos funcionales de 
A1, referenciando cada RF por su identificador 
○ Diagrama de casos de uso de A2 incrustado con breve explicación 
○ Diagrama de actividades de A3 incrustado con breve explicación 
○ Diagrama de secuencia de A3 incrustado con breve explicación 
○ Diagrama de clases incrustado con breve explicación 
○ Pseudocódigo del caso de uso 


```

## Ajustes realizados 


## Interacciones realizadas 

### Interacción 1: Generación de diagramas de clases, carpeta y de carpeta de anexos.
**Promp Usado:**
```
- Construir los anexos completos correspondientes a los casos de uso 4 y 5 del sistema, integrando trazabilidad, diagramas previos, diagrama de clases y pseudocódigo orientado a objetos.  
- Diseñar diagramas de clases específicos para cada caso de uso utilizando PlantUML.  
- Asegurar coherencia entre requisitos funcionales, escenarios, diagramas de actividades, diagramas de secuencia y tarjetas CRC previamente desarrolladas. 

Al generar cada diagrama de clases tomaras como contexto estos archivos: 
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- diagramas/02-casos-de-uso/02-bloquear-horarios-04.png
- diagramas/02-casos-de-uso/02-bloquear-horarios-04.puml
- diagramas/02-casos-de-uso/02-visualizar-agenda-05.png
- diagramas/02-casos-de-uso/02-visualizar-agenda-05.puml
- diagramas/03-escenarios-casos-de-uso/03-bloquear-horarios-flujo-principal.md
- diagramas/03-escenarios-casos-de-uso/02-visualizar-agenda-flujo-principal.md
- diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.png
- diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.puml
- diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.png
- diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.puml
- diagramas/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.png
- diagramas/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.puml
- diagramas/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png
- diagramas/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.puml
- herramientas-agile/tarjetas-crc/

Utilizar obligatoriamente la plantilla 
https://drive.google.com/file/d/1stT7qZHuwbZixM1HTtNI048ugE0su6wK/view. No se aceptarán anexos que no sigan la estructura definida en la plantilla. 

Debes crear los anexos en: 
anexos/analisis-funcional/04-caso-de-uso-nombre-del-caso-de-uso.md y 
anexos/analisis-funcional/05-caso-de-uso-nombre-del-caso-de-uso.md. 

Debes redactar los anexos markdown por caso de uso incluyendo: 
○ Descripción del caso de uso y trazabilidad con requisitos funcionales de 
A1, referenciando cada RF por su identificador 
○ Diagrama de casos de uso de A2 incrustado con breve explicación 
○ Diagrama de actividades de A3 incrustado con breve explicación 
○ Diagrama de secuencia de A3 incrustado con breve explicación 
○ Diagrama de clases incrustado con breve explicación 
○ Pseudocódigo del caso de uso 
```
**Respuesta:** Copilot generó: 
- anexos/analisis-funcional/04-caso-de-uso-bloquear-horarios.md
- anexos/analisis-funcional/05-caso-de-uso-visualizar-agenda.md
- diagramas/01-diagrama-clases/04-clase-bloquear-horarios.puml
- diagramas/01-diagrama-clases/04-clase-bloquear-horarios.png
- diagramas/01-diagrama-clases/04-clase-visualizar-agenda.puml
- diagramas/01-diagrama-clases/04-clase-visualizar-agenda.png


**Observación:** Copilot generó bien los archivos, solo tuvo un error en el formato de los anexos.

### Interacción 2: Ajuste de formato
**Promp usado:**
```
Se solicitó a copilot que reemplace el codigo de plantUML que aparecia en los anexos por los .png correspondientes.
```
**Respuesta:** Copilot cumplio con lo asignado.

**Observación:** Se debio escribir un prompt simple esta vez para que entienda la tarea que debia realizar.

### Interacción 3: Ajuste de diagrama UML 

**Promp usado:**
´´´
Necesito que solo agregues al diagrama de 05-clase-visualizar-agenda.puml la clase sistema mencionada en 05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.puml, manteniendo relaciones y coherencia tal cual como lo hiciste al crearlo
´´´ 
**Respuesta:** Copilot agregó al diagrama la clase sistema.

**Observación:** Copilot resolvio bien.

### Interacción 4: Ajuste de diagrama UML

**Promp usado:** 
´´´
Ahora debes hacer lo mismo con el diagrama 04-clase-bloquear-horarios.puml, la clase sistema se menciona en el archivo 05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.puml
´´´

**Respuesta:** Copilot agregó al diagrama la clase sistema.

**Observación:** Copilot resolvio bien.