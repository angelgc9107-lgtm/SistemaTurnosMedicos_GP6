# Uso de GitHub Copilot Agent Mode — Especialista DIP

## Archivos de contexto
* `anexos/introduccion.md`
* `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw`
* `herramientas-agile/tarjetas-crc/`

## Prompt utilizado
```
Actuá como un Especialista en Inversión de Dependencias y aplica los principios de DIP: Debes identificar dependecias, proponer abstracciones, aplicar inyección de dependencias, hacer una revisión del diseño y lograr un resultado estructurado. Primero, leé y usá como contexto los siguientes archivos del proyecto:
* `anexos/introduccion.md`
* `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw`
* `herramientas-agile/tarjetas-crc/`
```

## Resultado obtenido
1. Copilot identificó a la Agenda como módulo de alto nivel con dependencia directa hacia una clase concreta de notificación, y propuso introducir una interfaz `INotificador` para desacoplar esa relación. 
- **Dependencias detectadas:**
La clase Agenda instancia directamente a `Notificador`, generando
un acoplamiento concreto que dificulta el cambio de canal de notificación y
la realización de pruebas unitarias en aislamiento.
- **Abstracción propuesta:**
Introducir la interfaz `INotificador` con el método `enviarNotificacion`. `Agenda` dependerá de esta interfaz, y `Notificador` la implementará.
2. Y también generó un borrador inicial del archivo 05-dip.md con las secciones requeridas por la rúbrica, incluyendo motivación, justificación técnica y estructura de clases. 

## Ajustes manuales realizados
- El nombre de la clase concreta propuesto por Copilot no figuraba en las tarjetas CRC ni en el boceto inicial del STM. Se adoptó el nombre `Notificador` como nombre coherente. 
- Se amplió la explicación sobre el impacto del DIP en la testabilidad del sistema. Dado que la versión generada era demasiado breve y no mencionaba ejemplos concretos.
- Se ajustó la imagen referenciada para que apuntara al diagrama correcto. 
- Se reescribió la sección `## Justificación Técnica` incorporando distinción explicita entre interface y clase abstracta en el contexto DIP. 

## Iteraciones

### Iteración 1: Identificación de Dependencias

**Prompt enviado a copilot:**
```
Actuá como un Especialista en Inversión de Dependencias y aplica los principios de DIP: Debes identificar dependencias, proponer abstracciones, aplicar inyección de dependencias, hacer una revisión del diseño y lograr un resultado estructurado. Primero, leé y usá como contexto los siguientes archivos del proyecto: `anexos/introduccion.md`, `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw` y `herramientas-agile/tarjetas-crc/`
```
**Salida obtenida de Copilot:**
``` 
DEPENDENCIA DETECTADA — Clase: Agenda
→ Agenda instancia directamente a NotificadorWhatsApp dentro de su propia lógica
→ Esto genera acoplamiento concreto: cualquier cambio en NotificadorWhatsApp
  impacta directamente en Agenda
→ No es posible cambiar el canal de notificación sin modificar Agenda
→ Testear Agenda en aislamiento requiere que NotificadorWhatsApp funcione correctamente

ABSTRACCIÓN PROPUESTA — INotificador
→ Definir interfaz INotificador con método enviarRecordatorio(Turno turno)
→ Agenda dependerá de INotificador en lugar de NotificadorWhatsApp
→ NotificadorWhatsApp implementará INotificador
→ Se recomienda inyección por constructor para explicitar la dependencia

BENEFICIOS ESPERADOS
→ Agenda queda desacoplada de cualquier implementación concreta de notificación
→ Es posible agregar NotificadorEmail o NotificadorSMS sin modificar Agenda
→ Agenda puede testearse inyectando un mock de INotificador
```

**Decisión tomada:**

Se aceptó la propuesta de la interfaz INotificador. Se rechazó el nombre NotificadorWhatsApp por no figurar en las tarjetas CRC ni en el boceto inicial, adoptando Notificador como nombre coherente con el dominio del STM.

### Iteración 2: Refinamiento del Nombre de Clase

**Prompt enviado a copilot:**
```
El nombre NotificadorWhatsApp no figura en las tarjetas CRC ni en el boceto inicial del sistema. Proponé un nombre más coherente con el dominio del STM.
``` 

**Salida obtenida de Copilot:**
```
ANÁLISIS DE NAMING
→ NotificadorWhatsApp asume un canal específico que no está definido en el dominio
→ Las tarjetas CRC y el boceto inicial no definen ninguna clase de notificación
→ Un nombre genérico es más apropiado para respetar el dominio actual del sistema

SUGERENCIA
→ Notificador — nombre genérico y coherente con el dominio del STM
→ No asume canal de notificación específico
→ Permite futuras implementaciones (NotificadorEmail, NotificadorSMS)
  sin modificar el contrato definido por INotificador
```

**Decisión tomada:** 

Se adoptó Notificador como nombre de la clase concreta, ya que no figura ninguna clase de notificación específica en las tarjetas CRC ni en el boceto inicial del STM.

### Iteración 3: Ampliación de Justificación Técnica

**Prompt enviado a copilot:**
```
Ampliá la justificación técnica del DIP explicando el impacto en testabilidad y flexibilidad del sistema con ejemplos concretos del STM.
```
**Salida obtenida de Copilot:**
```
IMPACTO EN TESTABILIDAD
→ Antes de DIP: testear Agenda requería instanciar Notificador,
  generando dependencia de infraestructura en los tests
→ Después de DIP: se puede inyectar un mock de INotificador
  y testear Agenda en completo aislamiento

IMPACTO EN FLEXIBILIDAD
→ Antes de DIP: incorporar notificaciones por email requería modificar Agenda
→ Después de DIP: basta con crear una nueva clase que implemente INotificador
  sin tocar ninguna línea de Agenda

IMPACTO EN MANTENIBILIDAD
→ Un cambio en la lógica de notificación queda contenido en Notificador
→ La clase Agenda, núcleo del sistema de turnos, permanece estable
```

**Decisión tomada:** 

Se incorporó el análisis de testabilidad, flexibilidad y mantenibilidad en la sección ## Justificación Técnica del archivo 05-dip.md, ampliando la explicación con ejemplos concretos del STM.

## Observaciones finales
- Copilot generaliza el dominio cuando el contexto no es suficientemente explicito. Copilot propuso nombres de clases genéricos que no coincidian con el vocabulario real del STM, por lo que requirió intervención manual para mantener coherencia.
- Se amplio la explicación sobre el impacto del DIP en la testabilidad del
sistema, dado que la versión generada era demasiado breve y no mencionaba
ejemplos concretos.
- Se identifico correctamente que `Agenda` dependia de una clase concreta de Notificación. 