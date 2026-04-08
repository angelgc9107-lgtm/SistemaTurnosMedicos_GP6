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

## Boceto inicial del diseño de clases
