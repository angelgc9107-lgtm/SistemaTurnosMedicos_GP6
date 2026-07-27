# Encapsulamiento

---

El encapsulamiento en este proyecto cumple una función más amplia que simplemente "ocultar datos": permite que la lógica de negocio se mantenga ordenada, que las reglas de turno no se rompan desde fuera y que cada clase controle su propio estado sin depender de decisiones arbitrarias de otras clases.

En el sistema de turnos médicos, esto es especialmente importante porque una cita puede pasar por varios cambios de estado y cada transición tiene consecuencias reales: afecta la disponibilidad horaria, el historial del turno, la notificación al paciente y la visibilidad en la agenda. Por eso, la información sensible no debe estar expuesta directamente.

## ¿Qué se encapsula en este sistema?

En la solución propuesta, el encapsulamiento aparece principalmente en dos puntos del dominio:

- la clase `Agenda`, que administra los turnos, los bloqueos y la disponibilidad;
- la clase `Turno`, que controla su propio ciclo de vida y sus cambios de estado.

Estas clases mantienen internamente datos como la lista de turnos asignados, los rangos bloqueados, el estado del turno y los registros de auditoría. Sin embargo, esas estructuras no se exponen de forma libre. Solo se accede a ellas mediante operaciones específicas diseñadas para preservar la integridad del sistema.

![Encapsulamiento — Ejemplo 1: Agenda y Turno](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

> Ver diagrama completo en: [encapsulamiento-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

## Aplicación en la clase Agenda

La clase `Agenda` funciona como el punto central de control del sistema. En lugar de permitir que otras clases manipulen directamente la colección de turnos o los horarios ocupados, la agenda ofrece operaciones de alto nivel como reservar, reprogramar, cancelar o registrar la presencia del paciente.

Esto significa que las clases externas, como `Secretaria` o `ControlSistema`, no necesitan conocer cómo se valida la disponibilidad ni cómo se registran los conflictos. Solo invocan un método público y reciben el resultado esperado. Ese diseño evita que un error en otra clase altere de forma accidental la lógica interna de la agenda.

Por ejemplo, si una secretaria intenta agendar un turno en un horario ya ocupado, la agenda no deja que esa operación se complete sin pasar por la validación correspondiente. De esa manera, el encapsulamiento no solo protege datos, sino que también protege las reglas de negocio.

## Aplicación en la clase Turno

La clase `Turno` también encapsula su estado interno. Un turno no puede cambiar de forma arbitraria de "Pendiente" a "Presente" o a "Cancelado" sin pasar por una regla definida. En este sentido, el encapsulamiento ayuda a evitar estados inconsistentes, como un turno que aparezca como presente aunque nunca haya sido confirmado o que se marque como reprogramado sin dejar registro del cambio previo.

Esto es clave para cumplir requisitos como:

- mantener la integridad de los datos del turno;
- conservar un historial ordenado de cambios;
- evitar errores en la visualización de la agenda;
- garantizar que la información enviada al paciente o al médico sea coherente.

## Ejemplo de código

El siguiente fragmento muestra cómo la agenda encapsula la lógica de negocio y deja que las clases externas interactúen solo con su interfaz pública:

```java
public class Agenda {

    private final List<Turno> turnos = new ArrayList<>();
    private final GestorBloqueos gestorBloqueos = new GestorBloqueos();

    public Turno reservarTurno(Paciente paciente, Medico medico, LocalDateTime inicio) {
        validarDisponibilidad(inicio, medico);

        Turno turno = new Turno(paciente, medico, inicio);
        turnos.add(turno);
        return turno;
    }

    private void validarDisponibilidad(LocalDateTime inicio, Medico medico) {
        if (gestorBloqueos.estaBloqueado(inicio, medico)) {
            throw new IllegalStateException("El horario no está disponible");
        }
    }
}
```

Y, de forma similar, la clase `Turno` protege su propio estado:

```java
public class Turno {

    private String estado;
    private final LocalDateTime inicio;

    public Turno(Paciente paciente, Medico medico, LocalDateTime inicio) {
        this.estado = "Pendiente";
        this.inicio = inicio;
    }

    public void marcarPresente() {
        if (!"Pendiente".equals(this.estado)) {
            throw new IllegalStateException("El turno no puede pasar a presente");
        }
        this.estado = "Presente";
    }
}
```

Este ejemplo refleja el objetivo del encapsulamiento: las clases externas no alteran directamente los datos internos, sino que invocan métodos que controlan el comportamiento y mantienen la consistencia del objeto.

## Relación con la consigna del trabajo

El encapsulamiento aporta directamente al cumplimiento de la consigna porque ayuda a resolver dos problemas centrales del sistema:

- controla el acceso a los datos sensibles del turno y de la agenda;
- concentra las reglas de negocio en los objetos correctos, evitando que se repitan en varias clases.

Gracias a este enfoque, la agenda puede seguir siendo el único componente que centraliza la gestión de turnos, mientras que los demás actores del sistema interactúan con una interfaz clara y segura. Además, se fortalece la integridad de los datos, algo esencial para cumplir con la idea de un sistema confiable, mantenible y preparado para cambios futuros.
