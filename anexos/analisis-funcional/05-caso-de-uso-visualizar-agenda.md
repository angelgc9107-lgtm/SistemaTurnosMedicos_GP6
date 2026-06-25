## 1. Descripción y trazabilidad con requisitos funcionales de A1

### CU-05: Visualizar agenda (Diaria/Semanal)

**Actor/es:** Secretaria (principal), Médico (principal)

**Objetivo:** Permitir a la secretaria y al médico consultar la agenda de turnos de forma organizada en un calendario con vistas diaria o semanal, visualizando los estados de cada turno y los horarios bloqueados con su motivo.

**Flujo principal:**

1. El usuario ingresa a la sección "Agenda" desde el menú principal.
2. El sistema presenta por defecto la vista diaria del día actual.
3. El usuario elige entre la vista "Día" o "Semana" según su necesidad.
4. El sistema muestra el calendario con los bloques horarios correspondientes.
5. Los bloques con turno asignado muestran los datos del paciente y el estado del turno.
6. Los bloques bloqueados muestran el motivo del bloqueo.
7. El usuario navega entre fechas para consultar otros días o semanas.

**Flujos alternativos:**

No se definen flujos alternativos en el escenario de este caso de uso.

### Requisitos funcionales que satisface:

| ID | Requisito Funcional (texto exacto de introduccion.md) | Cómo lo satisface este caso de uso |
|---|---|---|
| RF1 | Gestión de Agenda: El sistema debe generar turnos en un calendario semanal con opción de vista diaria | El sistema presenta la agenda con vista diaria por defecto y permite cambiar a vista semanal. |
| RF4 | Roles y Privilegios: Definir perfiles para Secretaria (gestión), Paciente (consulta/cancelación) y Médico (autorización de sobreturnos y agenda) | El acceso a la agenda está restringido a usuarios autenticados con rol Secretaria o Médico. El médico tiene acceso de solo consulta desde esta vista. |
| RF6 | Horarios Definidos: Lunes a viernes de 9-13 y 15-19 (excepto jueves tarde), y sábados ocasionales según defina el médico | La vista respeta los horarios habilitados del consultorio y muestra únicamente los bloques definidos para cada día. |
| RF8 | Registro de Presencia: Incorporar un estado de "check-in" para marcar la llegada del paciente a la sala de espera | El calendario muestra el estado de cada turno (Pendiente o Presente en sala) de forma diferenciada. |
| RNF5 | Control Centralizado: La agenda debe ser el único componente que controle la gestión de los turnos | La Agenda actúa como único componente centralizado para recuperar y presentar la información de turnos y bloqueos. |

## 2. Diagrama de casos de uso de A2
![Diagrama de casos de uso CU-05](../../diagramas/02-casos-de-uso/02-visualizar-agenda-05.png)

**Actores y relaciones:**

- Secretaria → Es actor principal. Accede a la agenda desde el menú, selecciona el tipo de vista, navega entre fechas y consulta el estado de los turnos y los bloqueos registrados.
- Médico → Es actor principal. Accede a la agenda con las mismas capacidades de visualización que la Secretaria, pero con acceso de solo consulta: no puede modificar turnos ni bloqueos desde esta vista.

**Include/Extend:**

- Ambos actores comparten el mismo flujo de visualización porque el caso de uso no diferencia operaciones entre ellos: los dos acceden, eligen vista y navegan. La distinción de rol solo determina el acceso, no el comportamiento dentro del caso de uso.
- No se modelaron extends porque el escenario no define flujos alternativos disparados por condiciones opcionales.

## 3. Diagrama de actividades de A3
![Diagrama de actividades CU-05](../../diagramas/04-diagramas-actividades/04-actividad-visualizar-agenda-05.png)

**Swimlanes:**

- Usuario (Secretaria / Médico) → Representa al actor que inicia el proceso. Ingresa a la agenda, selecciona el tipo de vista y navega entre fechas. No modifica ningún dato durante la consulta.
- Sistema → Representa los componentes internos que procesan la solicitud: valida la autenticación, recupera los turnos y bloqueos correspondientes a la fecha solicitada y renderiza el calendario con los estados y motivos visibles.

**Decisiones clave del flujo:**

- ¿El usuario está autenticado con rol válido? → Si el usuario no tiene rol Secretaria o Médico, el sistema no habilita el acceso a la agenda.
- ¿Qué tipo de vista seleccionó el usuario? → Si eligió vista diaria, el sistema carga los turnos y bloqueos del día actual. Si eligió vista semanal, construye la grilla con la información de los siete días a partir de la fecha seleccionada.

## 4. Diagrama de secuencia de A3
![Diagrama de secuencia CU-05](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png)

**Participantes:**

- Usuario → actor que inicia el flujo (Secretaria o Médico)
- :ControlSistema → objeto coordinador que recibe la solicitud y delega a Agenda y VistaCalendario
- :Agenda → objeto central que recupera turnos y bloqueos para construir la vista
- :GestorBloqueos → objeto consultado por Agenda para obtener los bloqueos registrados por fecha
- :VistaCalendario → objeto que presenta el calendario con turnos y bloqueos al usuario

**Mensajes clave:**

- `accederAgenda(dni, rol)` → ControlSistema valida que el usuario tenga rol Secretaria o Médico y habilita el acceso a la agenda
- `cargarVistaDiaria(fecha)` → ControlSistema solicita a Agenda la información del día y luego le indica a VistaCalendario que renderice la vista diaria
- `obtenerVistaDiaria(fecha)` → Agenda recupera los turnos del día y consulta a GestorBloqueos los bloqueos registrados para esa fecha
- `obtenerBloquesPorFecha(fecha)` → GestorBloqueos devuelve los bloqueos correspondientes a la fecha indicada con su motivo
- `mostrarVistaDiaria(turnos, bloqueos)` → VistaCalendario presenta los turnos con su estado y las franjas bloqueadas con su motivo
- `navegarFecha(direccion)` → VistaCalendario calcula la nueva fecha y ControlSistema recarga la vista correspondiente sin modificar datos

**Objetos temporales destruidos:**

- `Resultado` → se crea en cada operación para comunicar éxito o error al componente solicitante, pero no persiste una vez procesado el mensaje
- `Calendario` → se construye con los turnos y bloqueos recuperados para transferir la información a VistaCalendario, pero no se almacena una vez que la vista fue renderizada

## 5. Diagrama de clases específico

![Diagrama de clases CU-05](../../diagramas/01-diagrama-clases/05-clases-visualizar-agenda.png)

El diagrama muestra que `Agenda` es el componente central para recuperar turnos y bloqueos. `VistaCalendario` es responsable de presentar la información en modo diario o semanal, mientras que `Usuario` determina el acceso autorizado.

## 6. Coherencia con tarjetas CRC

### Clases involucradas

| Clase | Responsabilidad (según tarjeta CRC) | Tarjeta CRC |
|---------|--------------------------------------|-------------|
| Secretaria | Gestionar agenda y consultar disponibilidad | [05-tarjeta-crc-secretaria.md](../../herramientas-agile/tarjetas-crc/05-tarjeta-crc-secretaria.md)|
| Medico | Gestionar disponibilidad y consultar agenda médica | [02-tarjeta-crc-medico.md](../../herramientas-agile/tarjetas-crc/02-tarjeta-crc-medico.md) |
| Agenda | Gestionar disponibilidad y presentar información de turnos | [04-tarjeta-crc-agenda.md](../../herramientas-agile/tarjetas-crc/04-tarjeta-crc-agenda.md) |
| Turno | Mantener la información de fecha, hora y estado de los turnos | [03-tarjeta-crc-turno.md](../../herramientas-agile/tarjetas-crc/03-tarjeta-crc-turno.md)|
| ControlSistema | Coordinar las operaciones entre usuarios y componentes del sistema | [08-tarjeta-crc-control-sistema.md](../../herramientas-agile/tarjetas-crc/08-tarjeta-crc-control-sistemas.md) |
| VistaCalendario | Mostrar información de agenda, turnos y bloqueos | [10-tarjeta-crc-vista-calendario.md](../../herramientas-agile/tarjetas-crc/10-tarjeta-crc-vista-calendario.md) |
| GestorBloqueos | Almacenar y administrar la colección de bloqueos registrados en la agenda | [11-tarjeta-crc-gestor-bloqueos.md](../../herramientas-agile/tarjetas-crc/11-tarjeta-crc-gestor-bloqueos.md) |
| Bloqueo | Representar un período inhabilitado con su rango de fechas y el motivo asociado | [13-tarjeta-crc-bloqueo.md](../../herramientas-agile/tarjetas-crc/13-tarjeta-crc-bloqueo.md) |
| Resultado | Encapsular el resultado de una operación indicando éxito o error con su mensaje | [14-tarjeta-crc-resultado.md](../../herramientas-agile/tarjetas-crc/14-tarjeta-crc-resultado.md) |

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
``` 
INICIO CU-05 Visualizar Agenda

// La secretaria o el médico solicitan acceder a la agenda
// para consultar los turnos programados y los períodos
// que se encuentran bloqueados.

Usuario.accederAgenda(tipoVista, fechaActual)

    // El sistema verifica que el usuario posea
    // credenciales válidas para acceder a la agenda.

    Usuario.autenticar()

    // Una vez autenticado, ControlSistema valida
    // que el rol corresponda a Secretaría o Médico.

    ControlSistema.accederAgenda(dni, rol)


// El sistema habilita el acceso a la agenda.

mostrar "Vista habilitada" a Usuario


// Inicialmente se carga la información correspondiente
// a la fecha actual.

Calendario calendario =
    ControlSistema.cargarVistaDiaria(fechaActual)

    // Agenda recupera todos los turnos registrados
    // para la fecha solicitada.

    List<Turno> turnos =
        Agenda.obtenerTurnosPorFecha(fechaActual)

        // De cada turno se consulta su estado para
        // informar correctamente la situación de la agenda.

        Turno.getEstado()


    // Agenda recupera también los períodos bloqueados
    // registrados para esa fecha.

    GestorBloqueos gestor =
        Agenda.getGestorBloqueos()

    List<Bloqueo> bloqueos =
        gestor.obtenerBloqueosPorFecha(fechaActual)


    // Para cada bloqueo se recupera el motivo
    // que justifica la indisponibilidad.

    gestor.obtenerMotivo(fechaActual, hora)


    // Agenda construye la vista diaria con toda
    // la información disponible.

    Agenda.obtenerVistaDiaria(fechaActual)


// El sistema presenta la agenda diaria mostrando
// turnos y bloqueos.

VistaCalendario.mostrarVistaDiaria(turnos, bloqueos)


// El usuario puede solicitar otra vista del calendario,
// por ejemplo una vista semanal.

ControlSistema.cargarVista(tipoVista, fechaActual)

    // Agenda obtiene la información necesaria
    // para construir la vista solicitada.

    Agenda.obtenerVistaSemanal(fechaActual)


// El sistema presenta la información en la vista elegida.

VistaCalendario.mostrarVistaSemanal(turnos, bloqueos)


// El usuario puede desplazarse entre fechas para
// consultar períodos anteriores o futuros.

ControlSistema.navegarFecha(direccion)

    VistaCalendario.navegarFecha(direccion)


// La agenda se actualiza para reflejar la nueva fecha.

mostrar "Calendario actualizado" a Usuario


// Cuando finaliza la consulta, el usuario cierra la agenda.

ControlSistema.cerrarVista()


// Estado final del sistema:
//
// - El usuario accedió a la agenda con permisos válidos.
// - Se visualizaron los turnos registrados.
// - Se visualizaron los períodos bloqueados y sus motivos.
// - Fue posible alternar entre vistas de calendario.
// - Fue posible navegar entre fechas.
// - No se modificó información de turnos ni bloqueos.
// - La Agenda centralizó la consulta de información (RNF5).

Retornar "Visualización finalizada"

FIN CU-05
``` 
El pseudocódigo muestra cómo un Usuario autenticado delega la solicitud de visualización en ControlSistema, que actúa como mediador hacia Agenda. Luego Agenda reúne los turnos y bloqueos correspondientes y VistaCalendario presenta la información en la vista solicitada.