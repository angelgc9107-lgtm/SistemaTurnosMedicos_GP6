# CU-04: Bloquear días/horarios en calendario

## 1. Descripción y trazabilidad con requisitos funcionales de A1

### CU-04: Bloquear días/horarios en calendario

**Actor/es:** Secretaria (principal), Médico (indica los rangos a bloquear)

**Objetivo:** Permitir a la secretaria marcar rangos de fechas y horarios como no disponibles en el calendario, impidiendo la asignación de nuevos turnos en esas franjas y mostrando el motivo del bloqueo.

**Flujo principal:**

1. El médico informa a la secretaria los horarios y fechas a bloquear con el motivo correspondiente.
2. La secretaria ingresa al calendario del sistema.
3. La secretaria selecciona el rango de fechas y horarios indicado por el médico.
4. La secretaria ingresa el motivo u observación del bloqueo.
5. La secretaria confirma el bloqueo del rango seleccionado.
6. El sistema registra el bloqueo en la agenda y refleja las franjas como no disponibles.
7. El calendario muestra las fechas y horarios bloqueados con el motivo ingresado.

**Flujos alternativos:**

No se definen flujos alternativos en el escenario de este caso de uso.

### Requisitos funcionales que satisface:

| ID | Requisito Funcional (texto exacto de introduccion.md) | Cómo lo satisface este caso de uso |
|---|---|---|
| RF3 | Validación de Conflictos: Bloquear horarios ya asignados para evitar solapamientos, permitiendo excepciones solo como sobreturnos autorizados | El sistema bloquea las franjas seleccionadas impidiendo la asignación de nuevos turnos en ese rango. |
| RF4 | Roles y Privilegios: Definir perfiles para Secretaria (gestión), Paciente (consulta/cancelación) y Médico (autorización de sobreturnos y agenda) | Solo la Secretaria puede registrar el bloqueo; el Médico es quien informa y autoriza el período a bloquear. |
| RF5 | Restricciones Específicas: No permitir procedimientos los lunes ni turnos de "Primera vez" los viernes por la tarde | El sistema valida que el rango de bloqueo respete las restricciones de días y horarios definidos para el consultorio. |
| RF6 | Horarios Definidos: Lunes a viernes de 9-13 y 15-19 (excepto jueves tarde), y sábados ocasionales según defina el médico | El bloqueo se aplica únicamente dentro de los horarios habilitados definidos para la agenda. |
| RNF5 | Control Centralizado: La agenda debe ser el único componente que controle la gestión de los turnos | La agenda es el componente centralizado que registra y gestiona todos los bloqueos del sistema. |

### Trazabilidad con requisitos de A1
- **RF3**: El sistema bloquea horarios ya asignados o no disponibles y evita solapamientos al marcar las franjas como no disponibles.
- **RF4**: Solo un usuario con rol Secretaría puede gestionar el bloqueo; el médico autoriza y explica el intervalo a bloquear.
- **RF5**: El sistema debe conocer las restricciones específicas de días y horarios del consultorio cuando valida rangos de bloqueo.
- **RF6**: El bloqueo se aplica dentro de los horarios habilitados definidos para la agenda (Lun-Vie 9-13 y 15-19, sábados ocasionales).
- **RNF5**: La agenda es el componente centralizado que controla la gestión de los turnos y los bloqueos.

## 2. Diagrama de casos de uso de A2
![Diagrama de casos de uso CU-04](../../diagramas/02-casos-de-uso/02-bloquear-horarios-04.png)

**Actores y relaciones:**

- Secretaria → Es el actor principal. Ingresa al calendario, selecciona el rango de fechas y horarios, registra el motivo y confirma el bloqueo.
- Médico → Participa como actor secundario. No opera el sistema directamente: informa presencialmente a la secretaria el período de indisponibilidad y el motivo antes de que ella ejecute el bloqueo.

**Include/Extend:**

- El caso de uso incluye la selección del rango de fechas, el ingreso del motivo y la confirmación del bloqueo como pasos obligatorios del flujo principal. Se modelaron como parte del flujo y no como casos de uso separados porque ninguno tiene sentido de forma independiente: sin rango no hay motivo, y sin ambos no hay bloqueo posible.
- No se modelaron extends porque el escenario no define flujos alternativos disparados por condiciones opcionales.

## 3. Diagrama de actividades de A3
![Diagrama de actividades CU-04](../../diagramas/04-diagramas-actividades/04-actividad-bloquear-horarios-04.png)

**Swimlanes:**

- Médico → Representa al actor que inicia el proceso de forma externa. Comunica presencialmente el período de indisponibilidad y el motivo antes de que la secretaria opere el sistema.
- Secretaria → Representa al actor que ejecuta todas las acciones sobre el sistema: selecciona el rango, ingresa el motivo y confirma el bloqueo.
- Sistema → Representa los componentes internos que procesan la operación: valida el rango dentro de los horarios habilitados, verifica conflictos con turnos existentes, registra el bloqueo y actualiza la vista del calendario.

**Decisiones clave del flujo:**

- ¿El rango está dentro de los horarios habilitados del consultorio? → Si el rango ingresado cae fuera de los horarios definidos (Lun-Vie 9-13 y 15-19, sábados ocasionales), el sistema informa el error y no permite continuar.
- ¿Existen turnos asignados en el rango a bloquear? → Si hay turnos confirmados dentro del período, el bloqueo no puede registrarse hasta que esos turnos sean cancelados o reprogramados previamente.

## 4. Diagrama de secuencia de A3
![Diagrama de secuencia CU-04](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-bloquear-horarios-bloquear-horarios-flujo-principal-04.png)

**Participantes:**

- Secretaria → actor que inicia el flujo
- :ControlSistema → objeto coordinador que recibe la solicitud y delega a Agenda
- :Agenda → objeto central que valida, consulta turnos y delega el registro
- :ValidadorDisponibilidad → objeto que verifica que el rango esté dentro de los horarios habilitados
- :GestorBloqueos → objeto que crea y almacena el bloqueo registrado
- :Turno → objeto consultado para detectar conflictos en el rango
- :VistaCalendario → objeto que presenta el calendario actualizado con las franjas bloqueadas

**Mensajes clave:**

- `confirmarBloqueo(fechaInicio, fechaFin, motivo)` → ControlSistema delega a Agenda la validación y el registro del bloqueo
- `validarRango(rango)` → ValidadorDisponibilidad verifica que el rango solicitado caiga dentro de los horarios habilitados del consultorio (Lun-Vie 9-13 y 15-19, sábados ocasionales)
- `obtenerTurnosPorRango(rango)` → Agenda consulta los turnos existentes para detectar si alguno cae dentro del período a bloquear
- `bloquearRango(rango, motivo)` → GestorBloqueos crea el objeto Bloqueo y lo incorpora a la colección de franjas inhabilitadas
- `mostrarBloqueoEnCalendario()` → VistaCalendario actualiza la presentación mostrando las franjas bloqueadas con el motivo asociado

**Objetos temporales destruidos:**

- `Resultado` → se crea en cada operación para comunicar éxito o error al componente solicitante, pero no persiste una vez que el mensaje fue procesado
- `RangoFechaHora` → se usa como parámetro para encapsular el intervalo durante la operación, pero no se almacena de forma independiente una vez que el bloqueo queda registrado

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
``` 
INICIO CU-04 Bloquear días/horarios en calendario

// Evento externo:
// El médico informa presencialmente a la secretaria el período
// en el que no estará disponible y el motivo del bloqueo.

// La secretaria selecciona en el sistema el rango de fechas
// que deberá quedar bloqueado.

ControlSistema.seleccionarRango(fechaInicio, fechaFin)


// Agenda recibe el rango solicitado para preparar
// la operación de bloqueo.

Agenda.seleccionarRango(fechaInicio, fechaFin)

retornar rangoSeleccionado


// El sistema informa a la secretaria que el rango fue registrado.

mostrar rangoSeleccionado a Secretaria

// La secretaria ingresa el motivo asociado al bloqueo.

ControlSistema.ingresarMotivo(motivo)


// Agenda registra el motivo que quedará asociado
// a la indisponibilidad del médico.

Agenda.ingresarMotivo(motivo)

retornar motivoRegistrado


// El sistema confirma que el motivo fue incorporado.

mostrar motivoRegistrado a Secretaria

// La secretaria confirma la operación de bloqueo.

ControlSistema.confirmarBloqueo(fechaInicio, fechaFin, motivo)


// Agenda analiza los turnos existentes dentro
// del período para conocer qué reservas se encuentran
// afectadas por la indisponibilidad.

Agenda.obtenerTurnosEnRango(fechaInicio, fechaFin)

    // Por cada turno encontrado se consulta su estado.

    Turno.getEstado()

    // También se recupera la fecha y hora de cada turno
    // comprendido dentro del rango solicitado.

    Turno.getFechaHora()


// Una vez analizada la información existente,
// Agenda registra el período como bloqueado.

Agenda.registrarBloqueo(fechaInicio, fechaFin, motivo)


// La agenda marca el rango completo como no disponible
// para impedir nuevas asignaciones de turnos.

Agenda.marcarNoDisponible(fechaInicio, fechaFin)

retornar bloqueoRegistrado


// Agenda informa al sistema que el bloqueo fue registrado.

mostrar bloqueoRegistrado

// El sistema actualiza la vista para que la secretaria
// pueda visualizar la indisponibilidad registrada.

ControlSistema.mostrarBloqueoEnCalendario()

// Estado final del sistema:
//
// - El rango indicado quedó registrado como bloqueado.
// - El motivo quedó asociado al bloqueo.
// - Las franjas comprendidas en el período aparecen
//   como no disponibles.
// - No podrán asignarse nuevos turnos dentro del rango (RF3).
// - El bloqueo queda visible en el calendario.
// - La agenda mantiene centralizada la gestión de turnos
//   y bloqueos (RNF5).

Retornar "Bloqueo registrado exitosamente"

FIN CU-04
``` 
El pseudocódigo define la responsabilidad de cada objeto: la `Secretaria` inicia el bloqueo delegando a `ControlSistema`, el `ControlSistema` coordina la operación con `Agenda`, `Agenda` valida la disponibilidad a través de `ValidadorDisponibilidad` y delega el registro a `GestorBloqueos`, mientras que `VistaCalendario` actualiza la presentación con las franjas bloqueadas. Se han incluido las clases de soporte `Resultado` y `ValidadorDisponibilidad` para completar la coherencia entre diagrama y especificación.