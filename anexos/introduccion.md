# Introducción al Diseño Orientado a Objetos

## Descripción del paradigma orientado a objetos
El paradigma orientado a objetos (POO) es un modelo de programación que organiza el software en objetos, los cuales combinan datos (atributos) y comportamiento (métodos). Es importante porque permite modelar problemas del mundo real de forma natural, facilita la reutilización de código y hace que los sistemas sean más fáciles de mantener y escalar.

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

RF1: El sistema debe permitir registrar nuevos turnos médicos.

RF2: El sistema debe mostrar los turnos disponibles según el horario configurado.

RF3: El sistema debe permitir cancelar o reprogramar turnos existentes.

RF4: El sistema debe enviar notificaciones automáticas al paciente por WhatsApp.

RF5: El sistema debe permitir bloquear la agenda por vacaciones o ausencias.

### Requisitos no funcionales

RNF1: Un usuario administrativo sin experiencia previa debe poder agendar el turno después de tener una breve capacitación.

RNF2: El sistema debe tener la capacidad para soportar el aumento de usuarios en un 50 %.

RNF3: El sistema debe ser funcional y estar disponible para entregar el MVP a principios de julio

RNF4: El sistema debe permitir que solo la agenda tenga un control de los turnos.

RNF5: El sistema debe guardar el historial de los cambios realizados a los turnos.

## Casos de uso


## Boceto inicial del diseño de clases

![Boceto inicial](/diagramas/01-diagrama-clases/01-boceto-inicial.png)
