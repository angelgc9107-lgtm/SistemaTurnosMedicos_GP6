# Uso de GitHub Copilot Agent Mode — Especialista DIP

## Archivos de contexto
* `anexos/introduccion.md`
* `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw`
* `herramientas-agile/tarjetas-crc/`

## Prompts utilizados
Actuá como un Especialista en Inversión de Dependencias y aplica los principios de DIP: Debes identificar dependecias, proponer abstracciones, aplicar inyección de dependencias, hacer una revisión del diseño y lograr un resultado estructurado. Primero, leé y usá como contexto los siguientes archivos del proyecto:
* `anexos/introduccion.md`
* `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw`
* `herramientas-agile/tarjetas-crc/`

## Resultado obtenido
- Copilot identificó a la Agenda como módulo de alto nivel con dependencia directa hacia una clase concreta de notificación, y propuso introducir una interfaz INotificador para desacoplar esa relación. 
**Dependencias detectadas:**
La clase Agenda instancia directamente a NotificadorWhatsApp, generando
un acoplamiento concreto que dificulta el cambio de canal de notificación y
la realización de pruebas unitarias en aislamiento.
**Abstracción propuesta:**
Introducir la interfaz INotificador con el método enviarRecordatorio(Turno turno). Agenda dependerá de esta interfaz, y NotificadorWhatsApp la implementará.
- Y también generó un borrador inicial del archivo 05-dip.md con las secciones requeridas por la rúbrica, incluyendo motivación, justificación técnica y estructura de clases. 

## Ajustes manuales realizados
- Se ajustó el nombre de la clase concreta de notificación para
que fuera coherente con el vocabulario real del sistema (tarjetas CRC y boceto
inicial), ya que Copilot había utilizado un nombre genérico que no correspondía. 
- Se amplió la explicación sobre el impacto del DIP
en la testabilidad del sistema. 
- Se ajustó la imagen referenciada para que apuntara
al diagrama correcto. 
- Se reescribió la sección `## Justificación Técnica` incorporando distinción explicita entre interface y clase abstracta en el contexto DIP. 
-

## Observaciones finales
- Copilot generaliza el dominio cuando el contexto no es suficientemente explicito. Copilot propuso nombres de clases genéricos que no coincidian con el vocabulario real del STM, por lo que requirió intervención manual para mantener coherencia.
- Se amplio la explicación sobre el impacto del DIP en la testabilidad del
sistema, dado que la versión generada era demasiado breve y no mencionaba
ejemplos concretos.
- Se identifico correctamente que `Agenda` dependia de una clase concreta de Notificación. 
