# CU-05: Visualizar agenda (Diaria/Semanal)

## 1. Descripción y trazabilidad con requisitos funcionales de A1
El caso de uso CU-05 permite que la secretaria y el médico consulten la agenda de turnos en una vista diaria o semanal. El sistema debe mostrar los estados de cada turno, los horarios bloqueados con su motivo y permitir la navegación entre fechas sin modificar los datos.

### Trazabilidad con requisitos de A1
- **RF1**: La agenda debe presentar un calendario semanal con opción de vista diaria.
- **RF4**: El acceso está restringido a usuarios autenticados con rol Secretaria o Médico.
- **RF6**: La vista respeta los horarios habilitados del consultorio y muestra los bloques de cada día.
- **RF8**: El sistema muestra el estado de los turnos, incluyendo "Pendiente" y "Presente".
- **RNF5**: La agenda actúa como el único componente centralizado para controlar la visualización de los turnos.

## 2. Diagrama de casos de uso de A2
![Diagrama de casos de uso CU-05](../../diagramas/02-casos-de-uso/02-visualizar-agenda-05.png)

El diagrama de casos de uso muestra a Secretaria y Médico accediendo a la agenda, seleccionando vista diaria o semanal, navegando fechas y observando horarios bloqueados y estados de turnos.

## 3. Diagrama de actividades de A3
![Diagrama de actividades CU-05](../../diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.png)

El diagrama de actividades describe la validación de autenticación, la carga de la vista diaria por defecto, la obtención de turnos y bloqueos, y la renderización del calendario con los estados y motivos.

## 4. Diagrama de secuencia de A3
![Diagrama de secuencia CU-05](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png)

El diagrama de secuencia muestra la interacción de Usuario, Sistema, Agenda y Turno al acceder a la agenda, cargar la vista diaria y navegar entre fechas.

## 5. Diagrama de clases específico

![Diagrama de clases CU-05](../../diagramas/01-diagrama-clases/05-clases-visualizar-agenda.png)

El diagrama muestra que `Agenda` es el componente central para recuperar turnos y bloqueos. `VistaCalendario` es responsable de presentar la información en modo diario o semanal, mientras que `Usuario` determina el acceso autorizado.

## 6. Coherencia con tarjetas CRC

### Clases involucradas

| Clase | Responsabilidad (según tarjeta CRC) | Tarjeta CRC |
|---------|--------------------------------------|-------------|
| Secretaria | Gestionar agenda y consultar disponibilidad | `05-tarjeta-crc-secretaria.md` |
| Medico | Gestionar disponibilidad y consultar agenda médica | `02-tarjeta-crc-medico.md` |
| Agenda | Gestionar disponibilidad y presentar información de turnos | `04-tarjeta-crc-agenda.md` |
| Turno | Mantener la información de fecha, hora y estado de los turnos | `03-tarjeta-crc-turno.md` |
| ControlSistema | Coordinar las operaciones entre usuarios y componentes del sistema | `08-tarjeta-crc-control-sistema.md` |
| VistaCalendario | Mostrar información de agenda, turnos y bloqueos | `10-tarjeta-crc-vista-calendario.md` |

### Relaciones UML

| Relación | Clases | Justificación |
|-----------|---------|--------------|
| Generalización | Secretaria → Usuario | La Secretaria hereda de Usuario los atributos y operaciones comunes de autenticación y acceso a la agenda. |
| Generalización | Medico → Usuario | El Médico hereda de Usuario los atributos y operaciones comunes del sistema. |
| Asociación | Usuario → ControlSistema | El Usuario interactúa con el sistema a través de ControlSistema para acceder a la agenda y solicitar distintas vistas. |
| Asociación | ControlSistema → Agenda | ControlSistema consulta la Agenda para recuperar la información necesaria para construir la vista solicitada. |
| Asociación | Agenda → Turno | Agenda obtiene los turnos correspondientes a una fecha o rango de fechas para su visualización. |
| Asociación | Agenda → GestorBloqueos | Agenda utiliza GestorBloqueos para recuperar los bloqueos registrados que deben mostrarse en la vista. |
| Asociación | GestorBloqueos → Bloqueo | GestorBloqueos administra una colección de bloqueos que representan períodos no disponibles. |
| Asociación | Agenda → VistaCalendario | Agenda suministra la información de turnos y bloqueos que será presentada en la interfaz. |
| Dependencia | ControlSistema → VistaCalendario | ControlSistema solicita la renderización de la vista diaria o semanal. |
| Dependencia | ControlSistema → Resultado | Las operaciones realizadas retornan objetos Resultado indicando éxito o error. |
| Dependencia | Usuario → Resultado | Las operaciones iniciadas por el Usuario retornan un objeto Resultado. |

## 7. Pseudocódigo orientado a objetos
```pseudo
class Usuario {
    autenticar(): boolean
    accederAgenda(tipoVista, fechaActual): Resultado {
        if not self.autenticar() then
            return Resultado.error("Acceso denegado")
        // Delegación a través de ControlSistema, como muestra el diagrama
        return ControlSistema.instancia().cargarVista(tipoVista, fechaActual)
    }
}

class ControlSistema {
    cargarVista(tipoVista, fechaActual): Resultado {
        return Agenda.instancia().mostrarAgenda(tipoVista, fechaActual)
    }
}

class Agenda {
    mostrarAgenda(tipoVista, fechaActual): Resultado {
        turnos = self.obtenerTurnosPorFecha(fechaActual)
        bloqueos = self.getGestorBloqueos().obtenerBloqueosPorFecha(fechaActual)
        if tipoVista == "diaria" then
            VistaCalendario.instancia().mostrarVistaDiaria(turnos, bloqueos)
        else
            calendario = self.calcularRangoSemanal(fechaActual)
            rango = new RangoFechaHora(calendario.fechaInicio, calendario.fechaFin)
            turnos = self.obtenerTurnosPorRango(rango)
            bloqueos = self.getGestorBloqueos().obtenerBloqueosPorRango(rango)
            VistaCalendario.instancia().mostrarVistaSemanal(turnos, bloqueos)
        return Resultado.ok("Agenda mostrada")
    }
}

class VistaCalendario {
    mostrarVistaDiaria(turnos, bloqueos): void {
        renderizarBloques(turnos)
        renderizarBloqueos(bloqueos)
    }
    mostrarVistaSemanal(turnos, bloqueos): void {
        renderizarBloques(turnos)
        renderizarBloqueos(bloqueos)
    }
}

class GestorBloqueos {
    obtenerBloqueosPorFecha(fecha): List<Bloqueo> {
        return bloqueos.filtrar(b => b.contiene(fecha, null)) // null = todas las horas
    }
}
```
El pseudocódigo muestra cómo un Usuario autenticado delega la solicitud de visualización en ControlSistema, que actúa como mediador hacia Agenda. Luego Agenda reúne los turnos y bloqueos correspondientes y VistaCalendario presenta la información en la vista solicitada.