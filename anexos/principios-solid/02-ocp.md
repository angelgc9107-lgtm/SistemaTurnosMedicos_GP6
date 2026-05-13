# Principio Abierto/Cerrado (OCP)

## Propósito y Tipo del Principio SOLID

El Principio Abierto/Cerrado (OCP) establece que las clases deben estar abiertas a extensión pero cerradas a modificación.

En el diseño original del sistema, la clase `Turno` utilizaba un atributo `tipo` para definir su comportamiento, lo que obligaba a modificar la lógica cada vez que se agregaba un nuevo tipo de turno.

OCP permite evitar este problema utilizando herencia y polimorfismo.

---

## Motivación

En el modelo inicial:

- Se utilizaba `tipo: String`
- Se requerían estructuras condicionales (`if` o `switch`)

Ejemplo del problema:
Si se agrega un nuevo tipo de turno, se debe modificar el código existente.

Esto genera:
- Código rígido
- Difícil mantenimiento
- Alto riesgo de errores

La solución consiste en reemplazar esta lógica por una jerarquía de clases.

---

## Explicación de Herencia

La herencia es un mecanismo de la programación orientada a objetos que permite que una clase derive de otra, reutilizando su estructura y comportamiento.

En este caso:
- `Turno` se define como clase abstracta
- Los distintos tipos de turnos extienden esta clase

Esto permite que cada tipo tenga su propio comportamiento sin modificar la clase base.

---

## Estructura de Clases

![Diagrama UML - OCP](/diagramas/01-diagrama-clases/01-solid-02-ocp.png)



## Justificación Técnica

En el diagrama se observa que la clase Turno define una abstracción general, mientras que las subclases implementan comportamientos específicos.

Esto permite:

Agregar nuevos tipos de turnos sin modificar código existente
Reducir la complejidad condicional
Mejorar la extensibilidad del sistema

La solución cumple OCP ya que el sistema puede evolucionar mediante extensión, sin alterar las clases existentes.