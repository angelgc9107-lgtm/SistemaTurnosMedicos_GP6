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

En el diagrama, cada subclase extiende `Persona` manteniendo coherencia con su rol en el sistema.

El método `notificar(mensaje: String)` está definido en `Persona` y sobreescrito en cada subclase con una implementación acorde a su rol:

| Clase | Implementación de `notificar()` |
|---|---|
| `Paciente` | Envía SMS al número del paciente |
| `Medico` | Envía notificación al panel médico |
| `Secretaria` | Envía alerta al sistema de gestión |

**Verificación de pre/postcondiciones (LSP):**

- **Precondición:** `mensaje != null` — ninguna subclase endurece esta condición (no exigen parámetros adicionales).
- **Postcondición:** el destinatario recibe el mensaje — todas las subclases garantizan esta postcondición con su implementación específica.
- **Invariante:** el atributo `nombre`, `dni` y `telefono` permanece accesible en todas las subclases sin modificación.

Esto garantiza que cualquier subclase puede sustituir a `Persona` sin alterar el comportamiento esperado del sistema (STM): si el sistema llama a `persona.notificar(msg)`, el resultado es siempre una notificación entregada, independientemente de qué subtipo concreto recibe el mensaje.

La solución es correcta porque respeta el principio LSP: las jerarquías de herencia son válidas, no se agregan comportamientos que rompan el contrato de la superclase, y cada subclase puede utilizarse en lugar de la clase base sin generar errores lógicos.