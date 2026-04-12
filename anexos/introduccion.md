
# Introducción al Diseño Orientado a Objetos

## Descripción del paradigma orientado a objetos
El paradigma orientado a objetos (POO) es un modelo de programación que organiza el software en objetos, los cuales combinan datos (atributos) y comportamiento (métodos). Es importante porque permite modelar problemas del mundo real de forma natural, facilita la reutilización de código y hace que los sistemas sean más fáciles de mantener y escalar.

## Los cuatro fundamentos de POO

### 1. Encapsulamiento
Se trata de no mostrar todo lo que pasa por dentro, sino solo lo necesario.
En nuestro sistema, el Turno funciona de manera cerrada, es decir que no se puede modificar 
directamente, sino que solo se puede cambiar usando opciones claras como confirmar o cancelar.

### 2. Herencia
Permite que una clase herede atributos y métodos de otra. En nuestro 
sistema, podríamos tener una clase base Persona de la cual heredan 
Paciente y Medico, compartiendo atributos como nombre y telefono.

### 3. Polimorfismo
Permite que objetos de distintas clases respondan al mismo mensaje 
de formas diferentes. Por ejemplo, tanto el Paciente como 
el Médico pueden tener una forma de ser notificados, pero 
cada uno recibe esa notificación de una manera diferente.

### 4. Abstracción
Consiste en modelar solo las características relevantes de un objeto. 
En nuestro sistema, la clase Turno abstrae la complejidad de una 
cita médica mostrando solo fecha, hora, paciente y tipo de consulta.


## Requisitos iniciales del sistema
[Notebook LM - Material de ayuda para revisar los casos de uso y los diseños de clase](https://notebooklm.google.com/notebook/ae349fb5-874b-428f-9bb0-5822e5c8be15?authuser=1&pageId=none)

### Requisitos funcionales

- RF1: Gestión de Agenda: El sistema debe generar turnos en un calendario semanal con opción de vista diaria

- RF2: Tipos de Turno: Se deben diferenciar turnos de "Primera vez" (30 min) y "Control" (15 min), con posibilidad de extensión

- RF3: Validación de Conflictos: Bloquear horarios ya asignados para evitar solapamientos, permitiendo excepciones solo como sobreturnos autorizados

- RF4: Roles y Privilegios: Definir perfiles para Secretaria (gestión), Paciente (consulta/cancelación) y Médico (autorización de sobreturnos y agenda)

- RF5: Restricciones Específicas: No permitir procedimientos los lunes ni turnos de "Primera vez" los viernes por la tarde

- RF6: Horarios Definidos: Lunes a viernes de 9-13 y 15-19 (excepto jueves tarde), y sábados ocasionales según defina el médico

- RF7: Notificaciones: Envío de recordatorios por WhatsApp 24 horas antes y a las 8:00 AM del día del turno

- RF8: Registro de Presencia: Incorporar un estado de "check-in" para marcar la llegada del paciente a la sala de espera

### Requisitos No Funcionales 

- RNF1: Usabilidad: El personal administrativo debe poder operar el sistema tras una breve capacitación

- RNF2: Escalabilidad: Capacidad para soportar un incremento del 50% en la base de usuarios

- RNF3: Disponibilidad del MVP: El sistema debe estar funcional para entregarse a principios de julio

- RNF4: Integridad de Datos: Es obligatorio mantener un historial de todos los cambios realizados en los turnos

- RNF5: Control Centralizado: La agenda debe ser el único componente que controle la gestión de los turnos

## Casos de uso

##  1. Agendar Turno
Actor: Secretaria (Principal)

Descripción: El sistema debe permitir a la recepcionista agendar un turno a un paciente con un Médico, validando que el horario esté disponible y respetando las restricciones impuestas en el sistema (Horarios bloqueados a pedido del Médico, duración del tipo de turno asignado).

#### Flujo de eventos:
- La recepcionista selecciona la opción Nuevo turno en la agenda que controla el calendario.
- Ingresar los datos del paciente que solicita el turno (Apellido & Nombre - Sexo - Edad - DNI)
- Se selecciona el tipo de consulta y el Médico (En un principio solo tendrán un usuario tipo Médico)
- El sistema mostrará el calendario semanal
- La recepcionista deberá seleccionar un día para mostrar los horarios disponibles para ese día, bloqueando los horarios que no estén disponibles (Disponibilidad del Médico - Horarios con turnos ya asignados)
- La recepcionista elegirá un horario disponible y seleccionará el tipo de turno que se agenda.
- La recepcionista confirmará el turno.
- Una vez que se confirme el turno, el calendario bloqueará en la fecha elegida el horario que consumirá el turno (varía por tipo de turno) pasando a no estar disponible ese horario, evitando superposiciones de turnos.
- El sistema confirmará que el turno se agendó de forma correcta y enviará una notificación al paciente por WhatsApp informando el día y horario del turno.

## Precondiciones:

- El usuario de la recepcionista debe estar validado para poder agendar los turnos en el calendario.
- El Usuario de Médico debe estar registrado en el sistema.
- Los horarios deben estar bien definidos para generar los turnos.

## Postcondiciones:
- El turno se guardará en la base relacionado al usuario Médico seleccionado.
- El turno asignado tendrá el estado de "Pendiente".
- En la agenda el horario de los turnos agendados se bloqueará para no estar disponible para otro turnos.
- Al momento en que se genere el turno se informará el día y horario del turno creado al paciente vía WhatsApp.
- Se generará una tarea para enviar un recordatorio al paciente vía WhatsApp en dos ocasiones, una vez 24 horas antes del turno y otra vez a las 8:00 A.M. del mismo día en que tienen el turno asignado.

## 2. Registrar Check-in (Llegada del Paciente)
Actores: Secretaria, Médico.

Descripción: Cuando el paciente llega físicamente, la secretaria lo busca en la agenda y marca su estado como "Presente" o "En sala de espera" para informar al Médico que el paciente se encuentra esperando en la sala de espera. El sistema registra el horario real en que el turno pasó del estado pendiente a presente o en sala.

### Flujo de eventos:

- El paciente se presenta en la recepción del consultorio.
- La recepcionista busca el turno del paciente en la agenda.
- La recepcionista selecciona el turno y lo marca para pasarlo al estado de "Presente" o "En sala de espera".
- En el sistema se guarda el horario real en que se presentó el paciente en recepción.
- El sistema cambia el estado del turno.
- El Médico puede ver que el paciente ya se encuentra en la sala esperando por la interfaz del calendario.

## Precondiciones:

- El turno debe estar asignado en el calendario en la fecha y horario correcto.
- La recepcionista debe estar validada en el sistema para poder visualizar el calendario semanal o diario.
- El Médico debe estar validado en el sistema para poder visualizar el calendario semanal o diario.

## Postcondiciones:

- La agenda debe cambiar el estado del turno de "Pendiente" a "presente o en sala de espera"

## 3. Reprogramar Turno
Actor: Secretaria

Descripción: La recepcionista selecciona un turno existente para reprogramarlo a otro horario disponible, el sistema debe guardar el historial de estos cambios y enviar una notificación por WhatsApp al paciente para informarle de la modificación.

### Flujo de eventos:
 
 - El paciente solicita que reprogramen un turno cargado en la agenda.
 - La recepcionista busca en la agenda el turno con los datos del paciente.
 - La recepcionista selecciona el turno que el paciente desea reprogramar.
 - La recepcionista elije la opción "Reprogramar".
 - La recepcionista tiene que elegir en el calendario un día y horario que estén disponibles para reprogramar un turno.
 - La recepcionista confirma la reprogramación del turno.
 - En la agenda se libera el horario que ocupaba el turno antes de la reprogramación y pasa a estar disponible nuevamente. El horario donde se reprograma el turno pasa a estar bloqueado.
 - El sistema envía una notificación vía WhatsApp al paciente con los nuevos horarios del turno.

 ## Precondiciones:

- El turno debe estar asignado en el calendario.
- El día y horario deben estar disponibles para poder reprogramar un turno.
- La recepcionista debe estar validada en el sistema para poder reprogramar el turno.


## Postcondiciones:

- En el calendario se tiene que visualizar el nuevo horario y día que ocupa el turno reprogramado.
- En el calendario se tiene que liberar el día y horario que tenía el turno antes de reprogramarlo.
- El sistema debe notificar el nuevo día y horario al paciente vía WhatssApp.

## 4. Bloquear días y horarios en calendario
Actores: Secretaria, Médico

Descripción: Recepcionista marca rangos de fechas (vacaciones, feriados o días de guardia del doctor) como no disponibles, En el calendario reflejará estos cambios impidiendo la asignación de turnos en esos bloques.

### Flujo de eventos:
 
 - El médico indicará a la recepcionista los horarios y fechas que debe seleccionar como no disponible, indicando el motivo (vacaciones, feriado, horarios no disponibles por diferente actividad)
 - El usuario recepcionista ingresa al calendario y selecciona un rango de fechas y horarios.
 - La recepcionista ingresa un motivo u observación.
 - La recepcionista marcará ese rango de días y horarios como no disponible.
 - En el calendario se reflejará esos horarios como no disponibles para asignar un turno.

 ## Precondiciones:

- La recepcionista debe estar validada para agregar fechas y horarios como no disponible por vacaciones, feriado, otras actividades.
- El médico debe estar validado en el sistema.


## Postcondiciones:

- En el calendario se tiene que bloquear las fechas y horarios que la recepcionista marcó como no disponible.
- En el calendario tiene que verse el motivo por el cual esos horarios no están disponibles.


## 5. Visualizar Agenda (Diaria/Semanal)
Actores: Secretaria, Médico.

Descripción: La agenda permite ver los turnos de forma clara y organizada en un calendario que puede visualizarse por día o semana.

### Flujo de eventos:
 
 - El usuario recepcionista o médico ingresa a la sección "Agenda" desde el menú principal.

 - El sistema presenta por defecto la vista diaria correspondiente al día actual.

 - El usuario puede elegir entre las vistas "Día", "Semana" según lo requiera.
 - Según lo seleccionado el calendario muestra el horario en los bloques, se tiene que ver si el horario está asignado un turno con los datos del paciente y en caso de que esté bloqueado el horario por otro motivo tiene que mostrarlo.
 - Se utilizan estados para representar los turnos (pendiente- presente en sala)
 - El usuario puede retroceder para elegir otro día o ver el calendario de forma semanal.

 ## Precondiciones:

 - El usuario recepcionista o médico debe estar validado en el sistema para poder visualizar la agenda.
 - Las fechas y horarios deben estar bien definidos para que se pueda visualizar.


## Postcondiciones:

- El usuario puede visualizar los turnos asignados en el calendario.

## Boceto inicial del diseño de clases
![Boceto inicial](/diagramas/01-diagrama-clases/01-boceto-inicial.png)
