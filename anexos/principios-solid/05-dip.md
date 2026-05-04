# Principio de Inversión de Dependencias (DIP)

## Propósito y Tipo del Principio SOLID
El Principio de Inversión de Dependencias (DIP) es un principio de
**desacoplamiento estructural**. Establece dos reglas fundamentales:

1. Las clases de alto nivel no deben depender de clases de bajo nivel, sino de abstracciones.
2. Las abstracciones no deben depender de los detalles. Son los detalles los que deben depender de las abstracciones.

Esto permite reducir el acoplamiento y mejorar la flexibilidad del sistema.

---

## Motivación

En el diseño original del Sistemas de Turnos Medicos, la clase `Agenda` dependía directamente de `NotificadorWhatsApp`.

Esto genera los siguientes problemas:
- **Rigidez:** Si la clinica decide incorporar notificaciones por email o SMS, hay que modificar `Agenda`, una clase que no deberia conocer el detalle de como se notifica.
- **Acoplamiento:** `Agenda` queda atada a `NotificadorWhatsApp`. Un cambio en la API de WhatsApp puede romper la lógica de gestión de turnos. 
- **Baja Testeabilidad:** para testear `Agenda` en aislamiento es necesario
  que `NotificadorWhatsApp` funcione.

---

## Explicación de Clases Abstractas e Interfaces

Una interfaz define un contrato que diferentes clases pueden implementar.

Una clase abstracta puede contener implementación parcial.

En DIP:
- Se utilizan interfaces como abstracciones.
- Las clases concretas dependen de estas abstracciones.
- En el STM, por ejemplo, en lugar de que
`Agenda` conozca a `NotificadorWhatsApp` directamente, depende de la
interfaz `INotificador`.
---

## Estructura de Clases

![Diagrama UML -DIP](/diagramas/01-diagrama-clases/01-solid-05-dip.png)


## Justificación Técnica

En el diagrama, la clase Agenda depende de la interfaz Notificador y no de una implementación concreta.

Esto permite:

Cambiar el tipo de notificación sin modificar Agenda
Reducir el acoplamiento
Mejorar la escalabilidad del sistema

La solución es correcta porque sigue el principio de depender de abstracciones, logrando un diseño flexible y mantenible.