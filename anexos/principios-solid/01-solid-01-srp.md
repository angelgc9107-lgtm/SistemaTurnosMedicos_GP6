# Principio de Responsabilidad Única — SRP
## Propósito y Tipo del Principio SOLID

El SRP (Single Responsibility Principle) indica que una clase debe tener una única responsabilidad y, por lo tanto, una sola razón para cambiar.

Esto significa que una clase no debería mezclar tareas diferentes, como guardar datos, validar reglas, mostrar información y ejecutar procesos del sistema al mismo tiempo.

## Motivación

En el diseño inicial, algunas clases concentraban demasiadas responsabilidades. Por ejemplo, la clase Agenda se encargaba de mostrar turnos disponibles, registrar turnos, bloquear fechas y gestionar disponibilidad.

Esto generaba un problema: si cambiaba la forma de mostrar la agenda, las reglas de disponibilidad o la manera de registrar turnos, había que modificar la misma clase.

Por eso se aplicó SRP, separando esas tareas en clases más específicas.

## Explicación de Responsabilidad Única

Una responsabilidad representa una función principal dentro del sistema.

Aplicar SRP implica identificar qué hace cada clase y separar aquellas tareas que no pertenecen al mismo objetivo.


- Agenda debe mantener la colección de turnos y bloqueos.
- Validardisponibilidad debe validar horarios disponibles.
- Vistacalendario debe mostrar la agenda.
- Gestorbloqueos debe representar horarios no disponibles.

Así, cada clase cambia solo cuando cambia su propia responsabilidad.

## Estructura de Clases
[Diagrama UML - SRP](diagramas/01-diagrama-clases/01-solid-01-srp.png)

## Justificación Técnica

Se aplicó SRP separando las responsabilidades que estaban concentradas en clases como Agenda, Turno y Secretaria.

La clase Agenda dejó de validar disponibilidad y mostrar el calendario, quedando enfocada en administrar turnos y bloqueos.

La clase Turno dejó de encargarse de crear, cancelar y reprogramar turnos, quedando como representación de la cita médica.

La clase Secretaria dejó de contener lógica de gestión, quedando como usuario administrativo del sistema.

Con esta refactorización, el sistema queda más mantenible, porque un cambio en una regla de disponibilidad, en una vista del calendario o en el proceso de cancelación no obliga a modificar clases que no corresponden