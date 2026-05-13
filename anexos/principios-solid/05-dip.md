# Principio de Inversión de Dependencias (DIP)

## Propósito y Tipo del Principio SOLID
El Principio de Inversión de Dependencias (DIP) es un principio de
**desacoplamiento estructural**. Establece dos reglas fundamentales:

1. Las clases de alto nivel no deben depender de clases de bajo nivel, sino de abstracciones.
2. Las abstracciones no deben depender de los detalles. Son los detalles los que deben depender de las abstracciones.

Esto permite reducir el acoplamiento y mejorar la flexibilidad del sistema.

---

## Motivación

En el diseño original del Sistemas de Turnos Medicos, la clase `Agenda` dependía directamente de `Notificador`.

Esto genera los siguientes problemas:
- **Rigidez:** Si la clinica decide incorporar notificaciones por email o SMS, hay que modificar `Agenda`, una clase que no deberia conocer el detalle de como se notifica.
- **Acoplamiento:** `Agenda` queda atada a `Notificador`.
- **Baja Testeabilidad:** para testear `Agenda` en aislamiento es necesario que `Notificador` funcione.

---

## Explicación de Clases Abstractas e Interfaces

Una interfaz define un contrato que diferentes clases pueden implementar.

Una clase abstracta puede contener implementación parcial.

En DIP:
- Se utilizan interfaces como abstracciones.
- Las clases concretas dependen de estas abstracciones.
- En el STM, por ejemplo, en lugar de que
`Agenda` conozca a `Notificador` directamente, depende de la
interfaz `INotificador`.
---

## Estructura de Clases

![Diagrama UML -DIP](/diagramas/01-diagrama-clases/01-solid-05-dip.png)


## Justificación Técnica

- Diseño antes de aplicar DIP: `Agenda` dependía directamente de `Notificador`. La dependencia era concreta, instanciada dentro de la propia clase.

- Diseño después de aplicar DIP: Se introduce la interfaz `INotificador` como abstracción. Agenda pasa a depender del contrato, no de la implementación.

- Testabilidad: Ahora es posible testear `Agenda` sin depender de `Notificador`.

- Flexibilidad: Si la clínica incorpora un nuevo canal de notificación,
basta con crear una nueva clase que implemente `INotificador` sin tocar `Agenda`.

- Mantenibilidad: Un cambio en la logica de notificación solo afecta a
`Notificador`. La clase `Agenda`, que contiene la lógica central del
sistema de turnos, permanece intacta.

En el diagrama se puede observar que Agenda apunta hacia `INotificador` y `Notificador` implementa `INotificador`. Esto refleja correctamente la aplicación del DIP: ambos modulos dependen de la abstracción, no entre si.