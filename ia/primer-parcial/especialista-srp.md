# Copilot Agent Mode - DOCUMENTADOR Y COORDINADOR DE REPOSITORIO + SRP
Se utilizó Copilot para identificar que clases tienen multiple responsabilidades en el diseño actual, después del analisis se pidio que genere 5 archivos de lenguaje UML

## Prompt utilizado
 ```
 - 1 Usa como contexto anexos/introduccion.md,
 diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw y
 las tarjetas CRC de herramientas-agile/tarjetas-crc/ como contexto.
 identifica las clases con múltiples responsabilidades en el diseño
 actual, explicando qué problemas de mantenibilidad genera cada caso, y quepropone cómo descomponerlas para que cada clase tenga una única razón para cambiar.
 - 2 Generar estos casos reconocidos como un conjunto por archivo, es decir que este la clase original con las nuevas clases en un archivo (ejemplo agenda en un archivo con las nuevas clases) en lenguaje plantUML dentro de la carpeta diagramas\01-diagrama-clases, el nombre del archivo tiene que ser 01-solid-01 y asi sucesivamente
 - 3 Se pidio que la vista del calendario sea una responsabilidad fuera de agenda.
 - 4 El bloqueo quedara encerrado dentro de gestor de bloqueos
 - 5 En el solid 02 (turnos) agregar una clase llamada gestor de turnos que se encargue de crear, confirmar, cancelar y reprogramar los turnos y que estado del turno sea una instancia dentro de turno no una clase separada
 - 6 consultar disponiblidad tiene consultar horarios, ver la disponiblidad de ese horario.
 - 7 gestor de turnos que tenga los mismas resposabilidad que en el solid 02
 - 8 Agregar el validador de disponiblidad como clase propia}
 - 9 Se verifico que consultar historial corresponda a Paciente.
 ```

## Archivos utilizados como contexto
- anexos/introduccion.md
- 01-boceto-inicial.excalidraw
- tarjetas-crc

## Ajustes realizados
Se modificaron las clases dentro de los 4 archivos seleccionados
En bloqueo se saca como clase individual y quedo incorporado en gestor de bloqueo.
Se agrego vista calendario como una clase aparte de agenda
Se dividieron responsabilidades en diferentes clases.
