# Introducción al Diseño Orientado a Objetos

## Descripción del paradigma orientado a objetos

El paradigma orientado a objetos (POO) es un modelo de programación 
que organiza el software en objetos, los cuales combinan datos 
(atributos) y comportamiento (métodos). Es importante porque permite 
modelar problemas del mundo real de forma natural, facilita la 
reutilización de código y hace que los sistemas sean más fáciles de 
mantener y escalar.

## Los cuatro fundamentos de POO

### 1. Encapsulamiento
Consiste en ocultar los datos internos de un objeto y exponer solo 
lo necesario. En nuestro sistema, el Turno oculta su lógica interna 
y solo permite modificarlo a través de métodos como confirmar() o 
cancelar().

### 2. Herencia
Permite que una clase herede atributos y métodos de otra. En nuestro 
sistema, podríamos tener una clase base Persona de la cual heredan 
Paciente y Medico, compartiendo atributos como nombre y telefono.

### 3. Polimorfismo
Permite que objetos de distintas clases respondan al mismo mensaje 
de formas diferentes. Por ejemplo, tanto Paciente como Medico 
podrían tener un método notificar() que funciona distinto para 
cada uno.

### 4. Abstracción
Consiste en modelar solo las características relevantes de un objeto. 
En nuestro sistema, la clase Turno abstrae la complejidad de una 
cita médica mostrando solo fecha, hora, paciente y tipo de consulta.

## Requisitos iniciales del sistema

# Requisitos iniciales de sistema
[Notebook LM - Material de ayuda para revisar los casos de uso y los diseños de clase](https://notebooklm.google.com/notebook/ae349fb5-874b-428f-9bb0-5822e5c8be15)

### Requisitos funcionales

RF1 El sistema Deberá generar turnos en un agenda que represente el calendario de forma semanal con la opción para seleccionar un día para ver todo el horario

RF2 Hay dos tipos de turnos, los cuales son turnos de "Primera vez" y de "Control"

RF3 Dependiendo del turno se debe consumir un tiempo determinado en la agenda, turnos de "Control" consumen 15 minutos y los turnos de "Primera vez" consumen 30 minutos del día en la agenda pero se puede extender por díez minutos cada sesión

RF4 Los horarios que ya tengan un turno asignado deben bloquearse para evitar solapamiento entre turnos

RF5 Hay tres tipos de rol en el sistema, según lo seleccionado tendrán diferentes privilegios. "Secretaria" puede generar-modificar turnos, "Paciente" puede ver o cancelar el turno que tiene asignado y "Medico" puede autorizar sobre turnos u horarios en la agenda

RF6 Los días Lunes no se podrán asignar turnos del para procedimientos y los días viernes a la tarde no se asignaran turnos del tipo "Primera vez"

RF7 Los horarios y días disponibles para asignar turnos serán los Lunes, Martes, Miercoles y viernes desde las 9:00 hasta las 13:00 y desde las 15:00 hasta las 19:00, el Jueves solo atiende en el turno mañana desde 9:00 hasta las 13:00 y el sabado en el turno mañana se puede atender de forma ocacional según lo indique el usuario "Medico"

RF8 El sistema deberá enviar un recordatorio en forma de notificación por "Whatsapp" a los "Pacientes" en dos ocaciones, una vez 24 horas antes del turno y otra vez a las 8:00 AM del día del turno asignado

RF9 El sistema debera permitir agregar un estado llamado "chek-in" cuando se anuncie en recepción antes de ingresar a la sala de espera

### Requisitos no funcionales

RNF1 Un usuario administrativo sin experiencia previa debe poder agendar el turno despues tener una breve capacitación.

RNF2 El sistema debe tener la capacidad para aguantar el aumento de usuarios en un 50%
## Casos de uso

Completar por el Modelador de Casos de Uso

## Boceto inicial del diseño de clases

Completar por el Diseñador de Clases Iniciales
