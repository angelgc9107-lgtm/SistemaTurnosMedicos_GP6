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
|---|---|---|
| Secretaria | Gestionar agenda y operaciones administrativas relacionadas con los turnos | [05-tarjeta-crc-secretaria.md](../../herramientas-agile/tarjetas-crc/05-tarjeta-crc-secretaria.md) |
| Medico | Definir disponibilidad y restricciones para la atención médica | [02-tarjeta-crc-medico.md](../../herramientas-agile/tarjetas-crc/02-tarjeta-crc-medico.md) |
| Agenda | Gestionar disponibilidad, turnos y bloqueos de horarios | [04-tarjeta-crc-agenda.md](../../herramientas-agile/tarjetas-crc/04-tarjeta-crc-agenda.md) |
| Turno | Mantener la información correspondiente a fecha, hora y estado del turno | [03-tarjeta-crc-turno.md](../../herramientas-agile/tarjetas-crc/03-tarjeta-crc-turno.md) |
| ControlSistema | Coordinar las operaciones entre los usuarios y los componentes del sistema | [08-tarjeta-crc-control-sistemas.md](../../herramientas-agile/tarjetas-crc/08-tarjeta-crc-control-sistemas.md) |
| VistaCalendario | Presentar la información de agenda, disponibilidad y bloqueos | [10-tarjeta-crc-vista-calendario.md](../../herramientas-agile/tarjetas-crc/10-tarjeta-crc-vista-calendario.md) |
| GestorBloqueos | Almacenar y administrar la colección de bloqueos registrados en la agenda | [11-tarjeta-crc-gestor-bloqueos.md](../../herramientas-agile/tarjetas-crc/11-tarjeta-crc-gestor-bloqueos.md) |
| ValidadorDisponibilidad | Verificar que el rango solicitado se encuentre dentro de los horarios habilitados del consultorio | [12-tarjeta-crc-validador-disponibilidad.md](../../herramientas-agile/tarjetas-crc/12-tarjeta-crc-validador-disponibilidad.md) |
| Bloqueo | Representar un período inhabilitado con su rango de fechas y el motivo asociado | [13-tarjeta-crc-bloqueo.md](../../herramientas-agile/tarjetas-crc/13-tarjeta-crc-bloqueo.md) |
| Resultado | Encapsular el resultado de una operación indicando éxito o error con su mensaje | [14-tarjeta-crc-resultado.md](../../herramientas-agile/tarjetas-crc/14-tarjeta-crc-resultado.md) |
| RangoFechaHora | Encapsular el intervalo de fechas y horarios que define el período a bloquear | [15-tarjeta-crc-rango-fecha-hora.md](../../herramientas-agile/tarjetas-crc/15-tarjeta-crc-rango-fecha-hora.md)|

### Relaciones UML:

| Relación | Clases | Justificación |
|---|---|---|
| Asociación | Medico → Secretaria | El Médico informa a la Secretaria el intervalo no disponible que debe bloquearse en la agenda. |
| Asociación | Secretaria → ControlSistema | La Secretaria delega la solicitud de bloqueo a ControlSistema, que coordina la operación con los componentes del dominio. |
| Asociación | ControlSistema → Agenda | ControlSistema delega a Agenda la ejecución del bloqueo y la consulta de turnos existentes en el rango. |
| Asociación | Agenda → GestorBloqueos | Agenda posee su propio GestorBloqueos como atributo y lo utiliza para registrar y recuperar los períodos bloqueados. |
| Asociación | Agenda → Turno | Agenda consulta los turnos registrados para detectar conflictos dentro del rango a bloquear. |
| Dependencia | Agenda → ValidadorDisponibilidad | Agenda usa ValidadorDisponibilidad para verificar que el rango solicitado esté dentro de los horarios habilitados del consultorio. |
| Dependencia | Agenda → VistaCalendario | Agenda provee la información actualizada de bloqueos a VistaCalendario para su presentación en pantalla. |
| Dependencia | Agenda → Resultado | Las operaciones de Agenda retornan objetos Resultado para indicar éxito o error al componente solicitante. |
| Asociación | GestorBloqueos → Bloqueo | GestorBloqueos administra una colección de objetos Bloqueo que representan los períodos inhabilitados registrados. |
| Dependencia | ControlSistema → VistaCalendario | ControlSistema invoca operaciones de VistaCalendario para presentar el estado actualizado del calendario. |
| Dependencia | ControlSistema → Resultado | Las operaciones ejecutadas por ControlSistema retornan objetos Resultado indicando el estado de la operación. |
| Dependencia | Secretaria → RangoFechaHora | La Secretaria utiliza RangoFechaHora como parámetro para encapsular el intervalo de fechas y horarios del bloqueo. |

## 7. Pseudocódigo orientado a objetos
```pseudo
class Secretaria

    solicitarBloqueo(rango, motivo)

        // La secretaria carga en el sistema el rango de fechas y horarios
        // que el médico indicó como no disponibles, junto con el motivo
        // del bloqueo (vacaciones, feriado u otra actividad del médico).

        resultado = ControlSistema.confirmarBloqueo(rango.fechaInicio, rango.fechaFin, motivo)

        if resultado.exito = false then
            return resultado
        end if

        // El sistema actualiza el calendario mostrando las franjas
        // inhabilitadas con el motivo asociado, para que la secretaria
        // pueda verificar que el bloqueo quedó registrado correctamente.

        ControlSistema.mostrarBloqueoEnCalendario()

        return Resultado.ok("Bloqueo registrado correctamente")


class ControlSistema

    confirmarBloqueo(fechaInicio, fechaFin, motivo)

        // ControlSistema delega a la Agenda la validación y el registro
        // del bloqueo solicitado.

        resultado = Agenda.bloquearRango(fechaInicio, fechaFin, motivo)

        return resultado


    mostrarBloqueoEnCalendario()

        // Se recuperan los bloqueos registrados en la agenda
        // para presentarlos actualizados en el calendario.

        bloqueos = Agenda.obtenerBloqueosPorRango(rango)

        VistaCalendario.mostrarBloqueos(bloqueos)


class Agenda

    bloquearRango(fechaInicio, fechaFin, motivo)

        // El consultorio solo opera en franjas definidas
        // (Lun-Vie 9-13 y 15-19, sábados ocasionales).
        // Se verifica que el período solicitado caiga dentro
        // de esos horarios habilitados.

        rangoValido = ValidadorDisponibilidad.validarRango(rango)

        if rangoValido = false then
            return Resultado.error("Rango fuera de los horarios habilitados del consultorio")
        end if

        // Antes de bloquear, se verifica si algún paciente tiene
        // un turno confirmado dentro del período solicitado.
        // Si los hay, el bloqueo no puede realizarse y esos turnos
        // deben resolverse primero.

        turnosEnRango = obtenerTurnosPorRango(rango)

        if turnosEnRango no está vacío then
            return Resultado.error("Existen turnos asignados en el rango indicado")
        end if

        // Sin conflictos, la Agenda delega a GestorBloqueos
        // la creación y almacenamiento del nuevo bloqueo.

        gestorBloqueos.bloquearRango(rango, motivo)

        return Resultado.ok("Bloqueo registrado")


    obtenerTurnosPorRango(rango)

        // Se recorre la lista de turnos para detectar
        // si alguno se encuentra dentro del rango indicado.

        turnosEnRango = []

        for turno in listaTurnos do
            if turno.estaEnRango(rango) then
                turnosEnRango.agregar(turno)
            end if
        end for

        return turnosEnRango


    obtenerBloqueosPorRango(rango)

        // Se recuperan los bloqueos registrados dentro
        // del rango indicado para actualizar la vista.

        return gestorBloqueos.obtenerMotivo(rango.fechaInicio, rango.fechaFin)


class GestorBloqueos

    bloquearRango(rango, motivo)

        // Se crea el bloqueo con el rango de fechas y el motivo
        // y se incorpora a la colección de franjas inhabilitadas.

        bloqueo = nuevo Bloqueo(rango.fechaInicio, rango.fechaFin, motivo)
        bloqueos.agregar(bloqueo)


class ValidadorDisponibilidad

    validarRango(rango)

        // Se verifica que el rango solicitado se encuentre
        // dentro de los horarios habilitados del consultorio.

        return rango.estaEnHorariosHabilitados()


class VistaCalendario

    mostrarBloqueos(bloqueos)

        // Se presenta en el calendario cada franja bloqueada
        // con su motivo, permitiendo identificar visualmente
        // los períodos no disponibles para nuevos turnos.

        for bloqueo in bloqueos do
            renderizarFranjaBloqueada(bloqueo)
        end for
```
El pseudocódigo define la responsabilidad de cada objeto: la `Secretaria` inicia el bloqueo delegando a `ControlSistema`, el `ControlSistema` coordina la operación con `Agenda`, `Agenda` valida la disponibilidad a través de `ValidadorDisponibilidad` y delega el registro a `GestorBloqueos`, mientras que `VistaCalendario` actualiza la presentación con las franjas bloqueadas. Se han incluido las clases de soporte `Resultado` y `ValidadorDisponibilidad` para completar la coherencia entre diagrama y especificación.