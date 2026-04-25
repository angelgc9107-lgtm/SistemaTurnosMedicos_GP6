# Copilot Agent Mode - Modelador de Diagramas de Casos de Uso
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de casos de uso.

## Prompt utilizado
```
 - 1 Prompt: Leer el archivo anexo/introduccion.md para tener como contexto
 - 2 Prompt: Generar un código de PlantUML para cada caso de uso
 - 3 Necesito minimo 5 diagramas que tengan lo siguiente: Actores principales, Casos de uso con relaciones adecuadas (inclusiones o extensiones)
 - 4 el cu1 los actores serian la secretaria y el paciente
 - 5 el paciente solicita el turno, debe tener una interacción con agendar el turno
 - 6 Necesito que analices el archivo introducción.md el caso 6. cancelar turno y hagas con lenguaje Plantuml un archivo puml de ese caso de uso en la carpeta 02-casos-de-uso llamado "02-cancelar-turno-06.puml"
 - 7 El CU2 agregar al actor Médico.
 - 8 Agregarle una realación entre el actor Médico con "Visualizar paciente en sala de espera".
 - 9 en el archivo 02-reprogramar-turno-03.puml necesito que hagas que system sea el que le informa a paciente.
 - 10 En el CU4 Se debe quitar los exted de bloquear días y horarios por el motivo que estos no son un derivado sino un motivo del bloqueo.
 - 11 En el CU5 agregar "extend" a "ver horarios bloqueados" por ser un derivado de visualizar agenda.


 ```

## Archivos utilizados como contexto
- anexos/introduccion.md

## Ajustes realizados
- CU1  Actores: Agregar al Paciente como actor (antes solo estaba la Secretaria y Sistema WhatsApp)

- CU1  Relaciones de actores: Reorganizar las interacciones:
La Secretaria inicia Agendar Turno y Agendar como sobreturno (todas las acciones de gestión quedan de su lado)
El Paciente solicita el turno con una interacción directa hacia Agendar Turno (con etiqueta "solicita turno")
El Sistema WhatsApp envía la notificación al Paciente (WA --> PAC)
- CU6 Se agrego el CU6 el puml y el archivo png.
- CU2 El CU2 se agrego al actor Médico, incluir una relación entre el actor Médico y visualizar paciente en sala de espera.
- CU3 Se agrego una linea para representar que la notificación al paciente se le es enviada por whatsApp
- CU4 Se removio los "extend" por no ser un derivado del caso "Bloquear horarios y días" sino motivmos del mismo.
- CU5 Agregar al actor "Médico" que interactue con "Visualizar Agenda"

## Interacciones

### Iteración 1: Creación de Diagramas de casos de uso
- **Prompt usado:**
```
Leer el archivo anexo/introduccion.md para tener como contexto
En base a ese contexto generar 5 archivos puml con cada caso de uso registrado.
```
**Respuesta:** Genero los 5 diagramas de casos de uso.

### Iteración 2: Corrección a diagrama CU1
- **Prompt usado:**
```
el cu1 los actores serian la secretaria y el paciente
```
**Respuesta:** Genero el archivo con la corrección solicitada.

### Iteración 3: Corrección a diagrama CU1 — 2
- **Prompt usado:**
```
El Paciente solicita el turno con una interacción directa hacia Agendar Turno (con etiqueta "solicita turno")
El Sistema WhatsApp envía la notificación al Paciente (WA --> PAC)
```
**Respuesta:** Genero el archivo con las correcciones solicitada.

### Iteración 4: Agregar actor en el CU2
- **Prompt usado:**
```
El CU2 se agrego al actor Médico, incluir una relación entre el actor Médico y visualizar paciente en sala de espera.
```
**Respuesta:** Se realizo la modificación solicitada.

### Iteración 5: Agregar una linea entre la notificación y el paciente
- **Prompt usado:**
```
en el archivo 02-reprogramar-turno-03.puml necesito que hagas que system sea el que le informa a paciente
```
**Respuesta:** Agregué WA --> PAC.

### Iteración 6: Generación de archivo puml CU6
- **Prompt usado:**
```
Remover los tres extend de horarios en calendarios del CU4.
```
**Respuesta:** Listo. Eliminé los tres use cases de extensión (CU4_EXT1/2/3) y sus relaciones <<extend>>.
### Iteración 7: Generación de archivo puml CU6
- **Prompt usado:**
```
En el archivo CU5 agregar el actor Médico, debe interactuar con "Visualizar paciente en sala"
```
**Respuesta:** Se agrego el actor con la relación solicitada.

### Iteración 8: Generación de archivo puml CU6
- **Prompt usado:**
```
Leer en el archivo anexo/introduccion.md el caso de uso "6. Cancelar turno" para tomar como contexto, en base a eso generar un archivo puml con el nombre "02-cancelar-turno-06"
```
**Respuesta:** Generó el caso de uso N° 6.

