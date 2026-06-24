# CU-04: Bloquear días/horarios en calendario

## 1. Descripción y trazabilidad con requisitos funcionales de A1
El caso de uso CU-04 permite que la secretaria registre en el calendario médico un rango de fechas y horarios como no disponibles, junto con el motivo del bloqueo (vacaciones, feriado u otra actividad del médico). El objetivo es que esas franjas queden inhabilitadas para nuevos turnos y que el motivo quede visible en la agenda.

### Trazabilidad con requisitos de A1
- **RF3**: El sistema bloquea horarios ya asignados o no disponibles y evita solapamientos al marcar las franjas como no disponibles.
- **RF4**: Solo un usuario con rol Secretaría puede gestionar el bloqueo; el médico autoriza y explica el intervalo a bloquear.
- **RF5**: El sistema debe conocer las restricciones específicas de días y horarios del consultorio cuando valida rangos de bloqueo.
- **RF6**: El bloqueo se aplica dentro de los horarios habilitados definidos para la agenda (Lun-Vie 9-13 y 15-19, sábados ocasionales).
- **RNF5**: La agenda es el componente centralizado que controla la gestión de los turnos y los bloqueos.

## 2. Diagrama de casos de uso de A2
![Diagrama de casos de uso CU-04](../../diagramas/02-casos-de-uso/02-bloquear-horarios-04.png)

El diagrama muestra a la Secretaria y al Médico como actores del caso de uso. Incluye los subcasos de selección del rango de fechas, ingreso del motivo y marcado de horarios como no disponibles, garantizando que el motivo quede asociado a cada bloqueo.

## 3. Diagrama de actividades de A3
![Diagrama de actividades CU-04](../../diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.png)

El diagrama de actividades refleja el flujo principal con las swimlanes de Médico, Secretaria y Sistema. El proceso valida datos, verifica si existen turnos en el rango, registra el bloqueo con GestorBloqueos y actualiza la agenda con franjas no disponibles.

## 4. Diagrama de secuencia de A3
![Diagrama de secuencia CU-04](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.png)

El diagrama de secuencia describe la interacción entre Secretaria, Sistema, Agenda y Turno. Muestra la confirmación de bloqueo, la verificación de turnos existentes en el rango y la notificación al usuario de que la franja quedó bloqueada.

## 5. Diagrama de clases específico

![Diagrama de clases CU-04](../../diagramas/01-diagrama-clases/04-clases-bloquear-horarios.png)

Este diseño enfatiza que la `Agenda` centraliza la gestión de bloqueos y turnos, mientras que `GestorBloqueos` almacena los rangos bloqueados y `VistaCalendario` presenta el estado actualizado. La `Secretaria` interactúa con la `Agenda`; el `Médico` provee la información del bloqueo.

## 6. Coherencia con tarjetas CRC

### Clases involucradas:

| Clase | Responsabilidad (según tarjeta CRC) | Tarjeta CRC |
|---------|--------------------------------------|-------------|
| Secretaria | Gestionar agenda y operaciones administrativas relacionadas con los turnos | `05-tarjeta-crc-secretaria.md` |
| Medico | Definir disponibilidad y restricciones para la atención médica | `02-tarjeta-crc-medico.md` |
| Agenda | Gestionar disponibilidad, turnos y bloqueos de horarios | `04-tarjeta-crc-agenda.md` |
| Turno | Mantener la información correspondiente a fecha, hora y estado del turno | `03-tarjeta-crc-turno.md` |
| ControlSistema | Coordinar las operaciones entre los usuarios y los componentes del sistema | `08-tarjeta-crc-control-sistema.md` |
| VistaCalendario | Presentar la información de agenda, disponibilidad y bloqueos | `10-tarjeta-crc-vista-calendario.md` |

### Relaciones UML:

| Relación | Clases | Justificación |
|-----------|---------|--------------|
| Generalización | Secretaria → Usuario | La Secretaria hereda de Usuario los atributos y operaciones comunes de autenticación y acceso a la agenda. |
| Generalización | Medico → Usuario | El Médico hereda de Usuario los atributos y operaciones comunes del sistema. |
| Asociación | Usuario → ControlSistema | El Usuario interactúa con el sistema a través de ControlSistema para acceder a las funcionalidades de la agenda. |
| Asociación | ControlSistema → Agenda | ControlSistema consulta y obtiene información de Agenda para construir las vistas solicitadas por el usuario. |
| Asociación | Agenda → Turno | Agenda administra y consulta los turnos registrados para determinar disponibilidad y conflictos. |
| Asociación | Agenda → GestorBloqueos | Agenda utiliza GestorBloqueos para recuperar los períodos bloqueados de la agenda. |
| Asociación | GestorBloqueos → Bloqueo | GestorBloqueos mantiene y administra una colección de bloqueos registrados. |
| Asociación | Agenda → VistaCalendario | Agenda proporciona la información de turnos y bloqueos que será mostrada en VistaCalendario. |
| Dependencia | ControlSistema → VistaCalendario | ControlSistema invoca operaciones de VistaCalendario para presentar la información solicitada. |
| Dependencia | ControlSistema → Resultado | Las operaciones ejecutadas por ControlSistema devuelven objetos Resultado indicando éxito o error. |
| Dependencia | Usuario → Resultado | Las operaciones de acceso realizadas por el Usuario retornan un objeto Resultado. |


## 7. Pseudocódigo orientado a objetos
```pseudo
class Resultado {
    - exito: boolean
    - mensaje: String
    
    {static} error(msg: String): Resultado
    {static} ok(msg: String): Resultado
}

class ValidadorDisponibilidad {
    validarRango(rango: RangoFechaHora): boolean {
        // Valida que el rango esté dentro de los horarios habilitados
        // del consultorio (Lun-Vie 9-13 y 15-19, sábados ocasionales)
        return rango.estaEnHorariosHabilitados()
    }
}

class Secretaria {
    autenticar(): boolean
    solicitarBloqueo(rango, motivo): Resultado {
        if not self.autenticar() then
            return Resultado.error("Acceso denegado")
        // Delegación a través de ControlSistema
        return ControlSistema.instancia().confirmarBloqueo(rango, motivo)
    }
}

class ControlSistema {
    confirmarBloqueo(rango, motivo): Resultado {
        resultado = Agenda.instancia().bloquearRango(rango, motivo)
        if resultado.exito then
            VistaCalendario.instancia().mostrarBloqueos(
                Agenda.instancia().obtenerBloqueosPorRango(rango)
            )
        return resultado
    }
}

class Agenda {
    - listaTurnos: List<Turno>
    - gestorBloqueos: GestorBloqueos
    
    bloquearRango(rango, motivo): Resultado {
        if not ValidadorDisponibilidad.instancia().validarRango(rango) then
            return Resultado.error("Rango inválido")
        if self.existeTurnoEnRango(rango) then
            return Resultado.error("Existen turnos asignados en el rango")
        self.getGestorBloqueos().bloquearRango(rango, motivo)
        return Resultado.ok("Bloqueo registrado")
    }

    existeTurnoEnRango(rango): boolean {
        for turno in listaTurnos do
            if turno.estaEnRango(rango) then
                return true
        return false
    }
    
    obtenerTurnosPorRango(rango): List<Turno>
    obtenerBloqueosPorRango(rango): List<Bloqueo>
    getGestorBloqueos(): GestorBloqueos
}

class GestorBloqueos {
    - bloqueos: List<Bloqueo>
    
    bloquearRango(rango, motivo): void {
        bloqueo = new Bloqueo(rango.fechaInicio, rango.fechaFin, motivo)
        bloqueos.agregar(bloqueo)
    }
}

class Bloqueo {
    - fechaInicio: Date
    - fechaFin: Date
    - motivo: String
    
    contiene(fecha: Date, hora: Time): boolean
}

class VistaCalendario {
    mostrarBloqueos(bloqueos): void {
        for bloqueo in bloqueos do
            renderizarFranjaBloqueada(bloqueo)
    }
}
```
El pseudocódigo define la responsabilidad de cada objeto: la `Secretaria` inicia el bloqueo delegando a `ControlSistema`, el `ControlSistema` coordina la operación con `Agenda`, `Agenda` valida la disponibilidad a través de `ValidadorDisponibilidad` y delega el registro a `GestorBloqueos`, mientras que `VistaCalendario` actualiza la presentación con las franjas bloqueadas. Se han incluido las clases de soporte `Resultado` y `ValidadorDisponibilidad` para completar la coherencia entre diagrama y especificación.