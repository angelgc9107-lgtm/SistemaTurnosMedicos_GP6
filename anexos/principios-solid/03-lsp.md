# Principio de Sustitución de Liskov (LSP)

## Propósito y Tipo del Principio SOLID

El Principio de Sustitución de Liskov (LSP) establece que una subclase debe poder reemplazar a su clase base sin alterar el comportamiento esperado del sistema.

Este principio garantiza que las jerarquías de herencia sean correctas y coherentes.

---

## Motivación

En el diseño original, la jerarquía `Persona → Paciente / Medico / Secretaria` no garantizaba que todas las subclases respetaran el mismo comportamiento.

Podían existir métodos que no aplicaban a todas las subclases, generando inconsistencias.

Por ejemplo:
- Una `Secretaria` no debería comportarse como un `Paciente`
- No debería tener métodos como `verTurno()`

Esto indica un problema en la definición de responsabilidades dentro de la jerarquía.

---

## Explicación de Herencia

La herencia permite definir una relación "es un" entre clases.

Para cumplir LSP:
- Las subclases deben respetar el contrato de la superclase
- No deben alterar el comportamiento esperado
- No deben implementar funcionalidades que no les correspondan

---

## Estructura de Clases

![Diagrama UML - LSP](/diagramas/01-diagrama-clases/01-solid-03-lsp.png)

## Justificación Técnica

En el diagrama, cada subclase extiende Persona manteniendo coherencia con su rol en el sistema.

No se agregan comportamientos que rompan el contrato de la superclase.

Esto garantiza que:

Las subclases puedan utilizarse en lugar de la clase base
No se generen errores lógicos
Se mantenga la consistencia del sistema

La solución es correcta porque respeta el principio LSP y asegura una jerarquía de herencia válida.