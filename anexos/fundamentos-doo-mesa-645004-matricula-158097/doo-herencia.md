# Herencia

---

La herencia permite construir una jerarquía de clases donde una subclase reutiliza la estructura y el comportamiento de una clase base, pero además agrega características propias que la hacen distinta dentro del dominio. En el sistema de turnos médicos, esto resulta útil porque existen conceptos que comparten datos generales pero requieren comportamientos específicos según el tipo de turno o el rol del usuario.

En este proyecto, la herencia no se usa solamente para reutilizar código, sino para modelar reglas del negocio de forma más clara. Por ejemplo, no todos los turnos tienen la misma duración ni la misma lógica de validación; tampoco todos los actores del sistema interactúan con la agenda de la misma manera. La jerarquía ayuda a representar estas diferencias sin duplicar toda la estructura.

La herencia se relaciona con varios principios SOLID. En particular, refuerza el principio de Sustitución de Liskov (LSP), porque las subclases pueden utilizarse donde se espera la clase base sin alterar el comportamiento esperado. Asimismo, favorece el principio de Abierto/Cerrado (OCP), ya que permite introducir nuevos tipos de turno o nuevas especializaciones sin modificar la lógica general que ya funciona. 

## Ejemplo en el proyecto

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

**Justificación técnica del código:** En este ejemplo, la clase base `Turno` define la estructura común de todos los turnos del sistema, como los datos del paciente, el médico y la fecha/hora, mientras que las subclases `TurnoPrimeraVez` y `TurnoControl` agregan únicamente el comportamiento específico que diferencia a cada tipo. La herencia se evidencia en el código a través de la palabra clave `extends`: tanto `TurnoPrimeraVez` como `TurnoControl` heredan de `Turno` mediante `public class TurnoPrimeraVez extends Turno` y `public class TurnoControl extends Turno`. Además, ambas subclases invocan `super(paciente, medico, fechaHora)` en su constructor, lo que demuestra que reutilizan la inicialización definida en la clase base en lugar de duplicarla. Por último, el método `calcularDuracion()` está declarado como `abstract` en `Turno` y cada subclase lo sobrescribe usando `@Override`, lo que confirma que están extendiendo y especializando el comportamiento heredado en vez de definir uno completamente nuevo.