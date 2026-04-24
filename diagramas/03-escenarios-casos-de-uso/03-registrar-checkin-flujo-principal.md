| **Nombre del escenario:** | Flujo principal - Registro de check-in exitoso | | |
|---|---|---|---|
| **Nombre del caso de uso:** | Registrar check-in | **ID Unica:** | CU-02 |
| **Area:** | Sistema de Gestion de Turnos Medicos - Recepcion y Sala de Espera | | |
| **Actor(es):** | Secretaria (principal), Medico | | |
| **Descripcion:** | Permite a la secretaria registrar la llegada fisica del paciente al consultorio, cambiando el estado del turno a "Presente" o "En sala de espera" y registrando el horario real de presentacion, de modo que el medico pueda visualizar quien se encuentra esperando. | | |
| **Activar Evento:** | El paciente se presenta fisicamente en la recepcion del consultorio. | | |
| **Tipo de senal:** | [x] Externa | [ ] Temporal | [ ] |

| **Pasos desempenados (ruta principal)** | **Informacion para los pasos** |
|---|---|
| 1. El paciente se presenta en recepcion. | Evento fisico que inicia el flujo. |
| 2. La secretaria busca el turno del paciente en la agenda. | Busqueda por nombre, apellido o DNI del paciente. |
| 3. La secretaria selecciona el turno correspondiente. | Turno en estado "Pendiente" para la fecha actual. |
| 4. La secretaria ejecuta la accion de marcar como "Presente" o "En sala de espera". | Opcion habilitada para usuarios con rol Secretaria (RF4). |
| 5. El sistema registra el horario real de presentacion del paciente. | Timestamp de llegada guardado en el turno (RF8). |
| 6. El sistema cambia el estado del turno de "Pendiente" a "Presente o en sala de espera". | Actualizacion de estado persistida en la agenda (RF8). |
| 7. El medico visualiza al paciente en espera desde su interfaz del calendario. | Vista del medico actualizada en tiempo real (RF4). |
| 8. El sistema confirma el cambio de estado en pantalla. | Mensaje de exito visible para la secretaria. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El turno debe estar asignado en el calendario para la fecha y horario correcto. La secretaria debe estar validada en el sistema. El medico debe estar validado en el sistema para ver la lista de espera (RF4). |
| **Poscondiciones:** | El turno cambia de estado "Pendiente" a "Presente o en sala de espera". El horario real de presentacion queda registrado en el turno (RF8). El medico puede ver al paciente en espera desde su vista del calendario. |
| **Suposiciones:** | El paciente tiene un turno asignado para la fecha actual. La secretaria puede identificar al paciente por sus datos personales. |
| **Reunir requerimientos:** | RF8 (estado de check-in), RF4 (roles y privilegios diferenciados para secretaria y medico). |
| **Aspectos sobresalientes:** | El registro del horario real de llegada permite analizar puntualidad y optimizar tiempos de espera. El medico debe ver la actualizacion sin necesidad de recargar manualmente su vista. Solo puede registrarse check-in sobre turnos en estado "Pendiente". |
| **Prioridad:** | Media |
| **Riesgo:** | Medio - Tiempo (Medio) - Coste (Bajo) |
