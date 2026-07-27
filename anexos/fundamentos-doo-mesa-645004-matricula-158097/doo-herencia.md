# Herencia

---

La herencia permite construir una jerarquía de clases donde una subclase reutiliza la estructura y el comportamiento de una clase base, pero además agrega características propias que la hacen distinta dentro del dominio. En el sistema de turnos médicos, esto resulta útil porque existen conceptos que comparten datos generales pero requieren comportamientos específicos según el tipo de turno o el rol del usuario.

En este proyecto, la herencia no se usa solamente para reutilizar código, sino para modelar reglas del negocio de forma más clara. Por ejemplo, no todos los turnos tienen la misma duración ni la misma lógica de validación; tampoco todos los actores del sistema interactúan con la agenda de la misma manera. La jerarquía ayuda a representar estas diferencias sin duplicar toda la estructura.

## Aplicación en el proyecto

Un ejemplo muy claro de herencia aparece en la relación entre los tipos de turno. En el sistema, todos los turnos comparten información básica como fecha, hora, paciente, médico y estado, pero cada tipo tiene un comportamiento particular. Un turno de primera vez, un control y un turno de consulta pueden ser tratados de manera uniforme desde la lógica general, mientras que cada uno define su propia duración o regla de negocio.

Esta idea se refleja en el diagrama del proyecto, donde `Turno` funciona como clase base y las clases especializadas heredan de ella para adaptar el comportamiento según el caso.

![Herencia — Ejemplo 1: Turno → TurnoPrimeraVez / TurnoControl](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

> Ver diagrama completo en: [herencia-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

## ¿Por qué esta herencia tiene sentido?

La relación entre `Turno` y sus subclases es válida porque todas representan la misma idea general: una cita médica. Sin embargo, cada subclase agrega un detalle concreto que modifica su comportamiento.

Por ejemplo:

- un turno de primera vez puede tener una duración mayor;
- un turno de control puede requerir menos tiempo;
- un turno de consulta puede tener una regla de negocio distinta según la especialidad del médico.

Gracias a la herencia, la lógica común se define una vez en la clase base y las clases hijas solo implementan lo que les corresponde. Esto evita duplicar código y facilita el mantenimiento en caso de que cambien las reglas del sistema.

## Ejemplo de código

El siguiente fragmento muestra cómo se puede representar esta jerarquía en Java:

```java
public abstract class Turno {

    protected LocalDateTime fechaHora;
    protected Paciente paciente;
    protected Medico medico;
    protected String estado;

    public Turno(Paciente paciente, Medico medico, LocalDateTime fechaHora) {
        this.paciente = paciente;
        this.medico = medico;
        this.fechaHora = fechaHora;
        this.estado = "Pendiente";
    }

    public abstract int calcularDuracion();
}

public class TurnoPrimeraVez extends Turno {

    public TurnoPrimeraVez(Paciente paciente, Medico medico, LocalDateTime fechaHora) {
        super(paciente, medico, fechaHora);
    }

    @Override
    public int calcularDuracion() {
        return 30;
    }
}

public class TurnoControl extends Turno {

    public TurnoControl(Paciente paciente, Medico medico, LocalDateTime fechaHora) {
        super(paciente, medico, fechaHora);
    }

    @Override
    public int calcularDuracion() {
        return 15;
    }
}
```

Este ejemplo refleja el propósito de la herencia en el sistema: la clase base contiene lo esencial del concepto de turno y cada subclase adapta ese comportamiento a una regla específica del negocio.

## Relación con la consigna del trabajo

La herencia aporta al trabajo porque permite representar de forma ordenada las diferencias entre tipos de turno sin perder la idea de que todos pertenecen al mismo concepto general. Esto ayuda a construir un diseño más flexible, reutilizable y fácil de extender.

Además, esta estructura favorece la organización del código y facilita futuras modificaciones, como agregar nuevos tipos de turno o incorporar nuevas reglas de duración o validación sin tener que reescribir toda la lógica existente.
