# Abstracción
---

La abstracción en Diseño Orientado a Objetos consiste en enfocarse en lo esencial de un concepto y ocultar los detalles secundarios. En el sistema de turnos médicos, esto significa representar la gestión de citas y horarios por lo que hacen, no por cómo guardan internamente sus datos.

En nuestro proyecto, `Agenda` es una abstracción que ofrece servicios como reservar un turno, consultar disponibilidad y registrar el check-in. Los demás componentes no necesitan conocer si esa agenda usa listas, tablas de horarios o validadores complejos; solo usan la interfaz pública.

La abstracción es útil porque permite cambiar la implementación interna sin afectar a las clases que dependen de ella. Por ejemplo, se puede mejorar la validación de solapamientos o el algoritmo de bloqueo de horarios sin cambiar el código de `Secretaria`, `Medico` o `Notificador`.

También se conecta con varios principios SOLID. En particular, ayuda a mantener el principio de Responsabilidad Única (SRP), porque `Agenda` concentra la lógica de gestión de turnos y evita que otras clases deban conocer todos los detalles de esa responsabilidad. Además, favorece el principio de Abierto/Cerrado (OCP), ya que permite modificar o ampliar la implementación interna de la agenda sin afectar a las clases que dependen de su interfaz pública.

---

## Ejemplo en el proyecto

La clase `Agenda` es el punto de acceso para las operaciones principales del flujo de turnos. Así, `Secretaria` y `ControlSistema` dependen de la abstracción de `Agenda` y no de su implementación interna.

![Abstracción — Ejemplo 1: Agenda](../../diagramas/01-diagrama-clases/capturas-pilares/poo-abstraccion-ejemplo-1.png)

> Ver diagrama completo en: [abstraccion-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-abstraccion-ejemplo-1.png)

**Descripción del diagrama:** Se muestra a `Agenda` como la clase que expone los métodos públicos necesarios para el sistema. Sus detalles internos, como `gestorBloqueos`, `validadores` y listas de turnos, quedan ocultos detrás de esa interfaz.

**Justificación técnica:** `Agenda` cumple el principio de abstracción porque separa lo que ofrece (reservar turnos, buscar disponibilidad, registrar check-in) de cómo lo hace internamente. Las otras clases interactúan con el contrato de `Agenda` y no dependen de su implementación concreta.

---

## Ejemplo de código

El siguiente fragmento ilustra cómo `Secretaria` utiliza la abstracción de `Agenda` sin conocer la lógica interna:

```java
public class Secretaria {

    private Agenda agenda;

    public Secretaria(Agenda agenda) {
        this.agenda = agenda;
    }

    public void agendarTurno(Paciente paciente, Medico medico, LocalDateTime fechaHora) {
        Turno turno = agenda.reservarTurno(paciente, medico, fechaHora);
        turno.confirmar();
    }
}

public class Agenda {

    public Turno reservarTurno(Paciente paciente, Medico medico, LocalDateTime fechaHora) {
        // Validaciones internas de disponibilidad y reglas de negocio
        return new Turno(paciente, medico, fechaHora);
    }

    public void registrarCheckIn(UUID idTurno) {
        // Actualiza el estado del turno sin exponer la búsqueda ni la estructura de datos
    }
}
```

**Justificación técnica del código:** La clase `Secretaria` usa solo la interfaz pública de `Agenda`. No necesita saber si la agenda guarda los turnos en una lista, si valida con un `ValidadorDisponibilidad` o si usa un componente de `Notificador` para avisos.

---