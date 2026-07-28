# Abstracción

---

La **abstracción** es uno de los principios fundamentales de la programación orientada a objetos. Consiste en representar únicamente las características y comportamientos esenciales de una entidad, dejando de lado aquellos detalles que no son necesarios para cumplir su función dentro del sistema. De esta manera, cada clase modela los aspectos más importantes del dominio, permitiendo construir soluciones más simples, organizadas y fáciles de mantener. Este principio favorece la comprensión del software porque cada objeto expone únicamente las operaciones necesarias para interactuar con él.

En el Sistema de Turnos Médicos, la clase `Agenda` representa la administración de los turnos de un profesional. Las demás clases utilizan los servicios que ofrece la agenda sin conocer cómo se implementan internamente sus procesos.

---

## Ejemplo en el proyecto

La clase `Agenda` abstrae toda la gestión relacionada con los turnos médicos. Desde otras partes del sistema solamente se utilizan sus operaciones públicas, mientras que la lógica necesaria para consultar disponibilidad, registrar turnos o administrar bloqueos permanece dentro de la propia clase.

![Abstracción — Ejemplo 1: Agenda](../../diagramas/01-diagrama-clases/capturas-pilares/poo-abstraccion-ejemplo-1.png)

> Ver diagrama completo en: [abstraccion-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-abstraccion-ejemplo-1.png)

### Descripción del diagrama:

La clase `Agenda` concentra las operaciones relacionadas con la administración de la agenda de un profesional. Entre ellas se encuentran la consulta de disponibilidad y el registro de turnos. Otras clases interactúan únicamente mediante estos métodos, sin acceder a la implementación interna.

### Justificación técnica:

La abstracción permite que `Agenda` represente el concepto de agenda médica mediante una interfaz clara. Las demás clases conocen qué operaciones pueden realizar, pero no cómo están implementadas, reduciendo el acoplamiento y facilitando el mantenimiento del sistema.

---

## Ejemplo de Código

```java
public class Agenda {

    private List<Turno> listaTurnos;
    private GestorBloqueos gestorBloqueos;

    public List<Turno> consultarDisponibilidad(String matricula,
                                               Date semana) {

        // Lógica para obtener los turnos disponibles
        return new ArrayList<>();
    }

    public Turno registrarTurno(Map<String, Object> datos) {

        // Lógica para registrar un turno
        Turno turno = new Turno();
        listaTurnos.add(turno);

        return turno;
    }
}
```

### Justificación técnica del código:

El código representa la abstracción de la clase **Agenda** al incluir tanto sus atributos (`listaTurnos` y `gestorBloqueos`), que almacenan el estado de la clase, como los métodos `consultarDisponibilidad()` y `registrarTurno()`, que definen su comportamiento. De esta manera, la clase reúne la información y las operaciones necesarias para gestionar los turnos, ocultando la complejidad de su implementación y exponiendo únicamente las funcionalidades que necesitan utilizar otras clases del sistema.
