# Uso de IA

## Objetivo

Analizar la arquitectura existente del Sistema de Turnos Medicos y proponer una evolucion natural mediante un patron GoF de comportamiento que resuelva un problema real de mantenibilidad, sin redisenar el dominio ni romper consistencia con UML, CRC y SOLID del primer parcial.

## Prompt utilizado

```
Actua como un Software Architect Senior especializado en Diseno Orientado a Objetos, UML, PlantUML, Patrones GoF y documentacion tecnica.

IMPORTANTE:
No quiero una solucion generica.
Debes trabajar EXCLUSIVAMENTE sobre el proyecto existente llamado "Sistema de Turnos Medicos", reutilizando la arquitectura ya desarrollada durante el primer parcial.
Toda la solucion debe mantener consistencia con los diagramas UML existentes, las tarjetas CRC, los principios SOLID previamente implementados y la documentacion del proyecto.
Nunca cambies nombres de clases existentes salvo que sea estrictamente necesario.
No inventes funcionalidades que no existan en el dominio.
Todo debe parecer una evolucion natural del sistema.

(Se incluyeron en el prompt original: contexto obligatorio de diagramas, rol de especialista en patron de comportamiento, objetivo, preguntas de analisis tecnico, archivos requeridos, restricciones y formato final de entrega.)
```

## Archivos utilizados como contexto

- diagramas/01-diagrama-clases/06-clases-diagrama-final.puml
- diagramas/01-diagrama-clases/01-solid-01-srp-01.puml
- diagramas/01-diagrama-clases/01-solid-01-srp-02.puml
- diagramas/01-diagrama-clases/01-solid-01-srp-03.puml
- diagramas/01-diagrama-clases/01-solid-01-srp-04.puml
- diagramas/01-diagrama-clases/01-solid-02-ocp.puml
- diagramas/01-diagrama-clases/01-solid-03-lsp.puml
- diagramas/01-diagrama-clases/01-solid-04-isp.puml
- diagramas/01-diagrama-clases/01-solid-05-dip.puml
- diagramas/01-diagrama-clases/05-clases-visualizar-agenda.puml
- anexos/patrones-diseno/patron-de-diseno-estructural.md

## Respuesta inicial generada por la IA

La IA detecto que la operacion de carga de agenda por `tipoVista` (diaria/semanal) es un punto con acoplamiento conductual y potencial proliferacion de condicionales en `ControlSistema`. Como primera propuesta, selecciono el patron **Strategy** para encapsular cada variante de carga en clases concretas intercambiables.

## Ajustes realizados manualmente

- Se adapto la propuesta para respetar nomenclatura ya existente (`ControlSistema`, `Agenda`, `VistaCalendario`, `Resultado`).
- Se evito modificar funcionalidades del dominio, limitando el alcance a reorganizacion conductual.
- Se incorporo `FabricaEstrategiaVista` para concentrar la seleccion por `tipoVista` y evitar dispersion de reglas.
- Se mantuvo estilo grafico de PlantUML alineado al repositorio (skinparams, colores y notas).

## Iteraciones realizadas

1. Relevamiento de diagramas finales y SOLID para ubicar puntos de extension reales.
2. Evaluacion comparativa de patrones candidatos (Observer, Strategy, Command, State, Template Method, Chain of Responsibility).
3. Seleccion de Strategy por presencia explicita de variantes de algoritmo de visualizacion.
4. Redaccion del UML parcial del patron y validacion de coherencia con el modelo existente.
5. Elaboracion del anexo tecnico centrado en problema real del sistema.

## Resultado final

Se genero un diseno conductual basado en **Strategy** para la carga de vistas de agenda:

- interfaz `IEstrategiaVistaAgenda`;
- clase abstracta `EstrategiaVistaAgendaBase`;
- estrategias concretas `EstrategiaVistaDiaria` y `EstrategiaVistaSemanal`;
- `ControlSistema` como contexto;
- `FabricaEstrategiaVista` para resolucion de estrategia.

Entregables creados:

- diagramas/01-diagrama-clases/01-patron-comportamiento-strategy.puml
- anexos/patrones-diseno/patron-de-diseno-de-comportamiento.md
- ia/segundo-parcial/especialista-patron-comportamiento.md

## Justificacion de la eleccion del patron

Se eligio **Strategy** porque el problema detectado es de algoritmos alternativos para un mismo objetivo de negocio (cargar vista de agenda). El sistema ya evidencia esta variacion mediante `tipoVista` y metodos diarios/semanales diferenciados. Strategy permite encapsular variantes sin modificar el contexto principal y mejora OCP/DIP de forma directa.

Patrones descartados:

- Observer: util para eventos y difusion de cambios, pero no resuelve la seleccion de algoritmo de visualizacion.
- Command: orientado a encapsular solicitudes y deshacer/encolar, no es el problema principal detectado.
- State: apropiado para cambios por estado interno de una entidad, distinto al caso de variacion por modo de vista.
- Template Method: exige jerarquia por herencia para fijar esqueleto; en este caso conviene composicion y reemplazo dinamico.
- Chain of Responsibility: ideal para procesamiento encadenado, no para variantes mutuamente excluyentes de un algoritmo.

## Reflexion tecnica

La IA aporto velocidad para detectar el punto de mayor valor arquitectonico y estructurar una solucion GoF consistente con el dominio. Las decisiones manuales fueron clave para asegurar trazabilidad con el UML existente, preservar nombres de clases, limitar alcance y mantener coherencia documental del repositorio.

En sintesis, la IA acelero el analisis y la redaccion tecnica, mientras que la definicion final de limites, impacto y consistencia con la arquitectura del proyecto se resolvio mediante criterio arquitectonico manual.
