# Principio de Inversión de Dependencias (DIP)

## Propósito y Tipo del Principio SOLID

El Principio de Inversión de Dependencias (DIP) establece que las clases de alto nivel no deben depender de clases de bajo nivel, sino de abstracciones.

Esto permite reducir el acoplamiento y mejorar la flexibilidad del sistema.

---

## Motivación

En el diseño original, la clase `Agenda` dependía directamente de `NotificadorWhatsApp`.

Esto genera un problema:
- No se puede cambiar fácilmente el tipo de notificación
- El sistema queda acoplado a una implementación concreta

---

## Explicación de Clases Abstractas e Interfaces

Una interfaz define un contrato que diferentes clases pueden implementar.

Una clase abstracta puede contener implementación parcial.

En DIP:
- Se utilizan interfaces como abstracciones
- Las clases concretas dependen de estas abstracciones

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