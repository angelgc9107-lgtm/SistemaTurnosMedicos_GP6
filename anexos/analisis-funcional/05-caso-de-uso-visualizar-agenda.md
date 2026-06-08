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
El diagrama de clases específico para CU-05 se diseñó en PlantUML y está disponible en `diagramas/01-diagrama-clases/05-clase-visualizar-agenda.puml`.

```plantuml
@startuml CU05-Clases-Visualizar-Agenda
skinparam classAttributeIconSize 0
skinparam class {
    BackgroundColor #E0F2FE
    BorderColor #2563EB
    ArrowColor #1D4ED8
}

title CU-05 - Diagrama de Clases Específico

class Usuario {
    - dni: String
    - rol: String
    + autenticar(): boolean
    + accederAgenda(): Resultado
}

class Secretaria {
    + accederAgenda(): Resultado
}

class Medico {
    + accederAgenda(): Resultado
}

class Agenda {
    - listaTurnos: List<Turno>
    - gestorBloqueos: GestorBloqueos
    + obtenerVistaDiaria(fecha: Date): Calendario
    + obtenerVistaSemanal(fechaInicio: Date): Calendario
    + obtenerTurnosPorFecha(fecha: Date): List<Turno>
    + obtenerBloqueosPorFecha(fecha: Date): List<Bloqueo>
}

class VistaCalendario {
    + mostrarVistaDiaria(turnos: List<Turno>, bloqueos: List<Bloqueo>): void
    + mostrarVistaSemanal(turnos: List<Turno>, bloqueos: List<Bloqueo>): void
    + navegarFecha(direccion: String): Date
}

class Turno {
    - fecha: Date
    - hora: Time
    - paciente: Paciente
    - medico: Medico
    - estado: String
    + getEstado(): String
    + getFechaHora(): DateTime
}

class GestorBloqueos {
    - bloqueos: List<Bloqueo>
    + obtenerBloqueosPorFecha(fecha: Date): List<Bloqueo>
    + obtenerMotivo(fecha: Date, hora: Time): String
}

class Bloqueo {
    - fechaInicio: Date
    - fechaFin: Date
    - motivo: String
    + contiene(fecha: Date, hora: Time): boolean
}

Usuario <|-- Secretaria
Usuario <|-- Medico
Agenda --> Turno : consulta >
Agenda --> GestorBloqueos : usa >
Agenda --> VistaCalendario : presenta >
GestorBloqueos --> Bloqueo : administra >
@enduml
```

El diagrama muestra que `Agenda` es el componente central para recuperar turnos y bloqueos. `VistaCalendario` es responsable de presentar la información en modo diario o semanal, mientras que `Usuario` determina el acceso autorizado.

## 6. Coherencia con tarjetas CRC
- La tarjeta CRC de `Secretaria` define su responsabilidad de "Consultar disponibilidad" y "Gestionar agenda", lo cual valida su rol en CU-05.
- La tarjeta CRC de `Agenda` describe su capacidad de "Mostrar turnos disponibles" y "Gestionar disponibilidad", lo que coincide con la recuperación de turnos y bloqueos para la vista.
- La tarjeta CRC de `Turno` refuerza que cada turno aporta un estado visible y una fecha/hora, necesario para la visualización correcta de la agenda.

## 7. Pseudocódigo orientado a objetos
```pseudo
class Usuario {
    autenticar(): boolean
    accederAgenda(tipoVista, fechaActual): Resultado {
        if not self.autenticar() then
            return Resultado.error("Acceso denegado")
        return Agenda.instancia().mostrarAgenda(tipoVista, fechaActual)
    }
}

class Agenda {
    mostrarAgenda(tipoVista, fechaActual): Resultado {
        turnos = self.obtenerTurnosPorFecha(fechaActual)
        bloqueos = self.gestorBloqueos.obtenerBloqueosPorFecha(fechaActual)
        if tipoVista == "diaria" then
            VistaCalendario.instancia().mostrarVistaDiaria(turnos, bloqueos)
        else
            calendario = self.calcularRangoSemanal(fechaActual)
            turnos = self.obtenerTurnosPorRango(calendario.fechaInicio, calendario.fechaFin)
            bloqueos = self.gestorBloqueos.obtenerBloqueosPorRango(calendario.fechaInicio, calendario.fechaFin)
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
        return bloqueos.filtrar(b => b.contiene(fecha, cualquierHora))
    }
}
```

El pseudocódigo muestra cómo un `Usuario` autenticado solicita la visualización de la agenda, cómo `Agenda` reúne los turnos y bloqueos correspondientes y cómo `VistaCalendario` presenta la información en la vista solicitada.
