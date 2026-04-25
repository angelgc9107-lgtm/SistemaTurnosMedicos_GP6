# Principio de Inversión de Dependencias (DIP)

El Principio de Inversión de Dependencias (DIP) establece que los sistemas más flexibles son aquellos en los que las dependencias del código fuente se refieren únicamente a abstracciones y no a concreciones.

### Este principio se desglosa en dos reglas fundamentales:

- **Independencia de niveles:** Los módulos de alto nivel (la lógica de negocio o "qué" hace el sistema) no deben depender de los módulos de bajo nivel (los detalles de implementación o "cómo" se hace); ambos deben depender de abstracciones (interfaces o clases abstractas).

- **Abstracción sobre el detalle:** Las abstracciones no deben depender de los detalles técnicos; por el contrario, son los detalles los que deben depender de las abstracciones.

## Motivación

**Problema detectado:** Específicamente, la clase Agenda (o GestorTurnos), que contiene la política de alto nivel sobre cómo organizar las citas, dependía directamente de una implementación concreta y volátil: NotificadorWhatsApp [User interaction, 100]. En el diseño original, la Agenda era la responsable de instanciar y conocer el funcionamiento interno de WhatsApp para enviar recordatorios.

**Solución mediante DIP:** Al aplicar el DIP, invertimos esta relación introduciendo una abstracción (la interfaz INotificador) que define el contrato de lo que significa "notificar", sin decir "cómo" se hace. Ahora, la Agenda ya no conoce a WhatsApp; solo conoce la interfaz.

## Abstracciones en el Diseño Orientado a Objetos
En el marco del Principio de Inversión de Dependencias (DIP), la clave para reducir el acoplamiento consiste en dejar de depender de "concreciones" (clases que implementan lógica específica) para pasar a depender de abstracciones. Estas abstracciones se materializan principalmente a través de dos mecanismos:

### La Interfaz (Interface)

Una interfaz se define como un conjunto de operaciones que especifica un aspecto determinado de la funcionalidad de una clase, funcionando como un "contrato" de servicios que una clase presenta a las demás.

- **Características principales:** Una interfaz pura carece de implementación, es decir, solo contiene las firmas o declaraciones de los métodos, pero no sus cuerpos ni campos de datos.

- **Rol en el DIP:** Actúan como una capa de abstracción que separa la política de alto nivel de los detalles de bajo nivel. Al hacer que el módulo de alto nivel dependa de la interfaz, el sistema se vuelve flexible, permitiendo intercambiar las implementaciones concretas (detalles) sin afectar la lógica central.

### La Clase Abstracta (Abstract Class)

Una clase abstracta es una clase general diseñada específicamente para no tener instancias directas.

- **Características principales:** Se utiliza en relaciones de generalización para agrupar atributos y métodos comunes que serán heredados por subclases especializadas o "clases concretas". A diferencia de las interfaces, las clases abstractas pueden incluir alguna realización o implementación parcial de sus métodos.

- **Representación en UML:** Se distingue visualmente porque su nombre debe escribirse obligatoriamente en letra cursiva.

### Inversión y Abstracción

La aplicación conjunta de estos conceptos permite que las dependencias del código fuente dejen de ser paralelas al flujo de ejecución. Mientras que en el tiempo de ejecución una clase de alto nivel llama a una de bajo nivel, en el diseño del código fuente ambas "apuntan" hacia la interfaz o clase abstracta.
Este desacoplamiento se termina de concretar mediante la Inyección de Dependencias, técnica por la cual un objeto recibe sus colaboradores desde el exterior (generalmente a través del constructor) en lugar de crearlos internamente, logrando así que el control sobre "qué objeto usar" sea delegado a un tercero.

## Diagrama Solid
![Diagrama DIP](../../diagramas/01-diagrama-clases/01-solid-05-dip.png)