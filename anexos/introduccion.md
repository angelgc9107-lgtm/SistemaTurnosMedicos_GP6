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

### Requisitos Funcionales
- RF1: El sistema debe permitir registrar nuevos turnos médicos.
- RF2: El sistema debe mostrar los turnos disponibles según el horario configurado.
- RF3: El sistema debe permitir cancelar o reprogramar turnos existentes.
- RF4: El sistema debe enviar notificaciones automáticas al paciente por WhatsApp.
- RF5: El sistema debe permitir bloquear la agenda por vacaciones o ausencias.

### Requisitos No Funcionales
- RNF1: El sistema debe ser accesible desde cualquier navegador web.
- RNF2: El sistema debe responder en menos de 3 segundos.
- RNF3: El sistema debe estar disponible al menos el 99% del tiempo.
- RNF4: Los datos de los pacientes deben estar protegidos.
- RNF5: El sistema debe ser fácil de usar para personal sin conocimientos técnicos.

## Casos de uso

Completar por el Modelador de Casos de Uso

## Boceto inicial del diseño de clases

Completar por el Diseñador de Clases Iniciales
