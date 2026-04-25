| **Nombre del escenario:** | Flujo principal - Visualizacion de agenda exitosa | | |
|---|---|---|---|
| **Nombre del caso de uso:** | Visualizar agenda (Diaria/Semanal) | **ID Unica:** | CU-05 |
| **Area:** | Sistema de Gestion de Turnos Medicos - Consulta Operativa | | |
| **Actor(es):** | Secretaria (principal), Medico (principal) | | |
| **Descripcion:** | Permite a la secretaria y al medico consultar la agenda de turnos de forma organizada en un calendario con vistas diaria o semanal, visualizando los estados de cada turno (Pendiente, Presente en sala) y los horarios bloqueados con su motivo. | | |

| **Activar Evento:** | El usuario (secretaria o médico) ingresa a la sección "Agenda" desde el menú principal del sistema. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | [x] Externa | [ ] Temporal |

| **Pasos desempenados (ruta principal)** | **Informacion para los pasos** |
|---|---|
| 1. El usuario ingresa a la seccion "Agenda" desde el menu principal. | Usuario autenticado como Secretaria o Medico (RF4). |
| 2. El sistema presenta por defecto la vista diaria del dia actual. | Vista inicial: dia en curso con todos los bloques horarios (RF1). |
| 3. El usuario elige entre la vista "Dia" o "Semana" segun su necesidad. | Opciones de visualizacion: diaria o semanal (RF1). |
| 4. El sistema muestra el calendario con los bloques horarios correspondientes. | Horarios habilitados: Lun-Vie 9-13 y 15-19 (excl. jueves tarde); sabados ocasionales (RF6). |
| 5. Los bloques con turno asignado muestran los datos del paciente y el estado del turno. | Estados visibles: "Pendiente" y "Presente o en sala de espera" (RF8). |
| 6. Los bloques bloqueados muestran el motivo del bloqueo. | Motivos: vacaciones, feriado, horario no disponible (CU-04). |
| 7. El usuario navega entre fechas para consultar otros dias o semanas. | Navegacion libre entre periodos del calendario. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El usuario (secretaria o medico) debe estar validado en el sistema (RF4). Las fechas y horarios habilitados deben estar configurados en la agenda (RF6). |
| **Poscondiciones:** | El usuario visualiza los turnos asignados y estados en el calendario. No se modifica ninguna informacion durante la consulta. |
| **Suposiciones:** | El usuario conoce la navegacion basica del calendario. Los datos de la agenda estan actualizados al momento de la consulta. |
| **Reunir requerimientos:** | RF1 (calendario semanal con vista diaria), RF4 (acceso por rol), RF6 (horarios habilitados del consultorio), RF8 (estados de turno visibles), RNF5 (la agenda es el control centralizado de turnos). |
| **Aspectos sobresalientes:** | La vista por defecto es la diaria del dia actual. Los estados deben ser diferenciados visualmente para facilitar la lectura rapida. Los horarios bloqueados deben mostrar el motivo. El medico tiene acceso de solo consulta; no puede modificar turnos desde esta vista (RF4). |
| **Prioridad:** | Media |
| **Riesgo:** | Medio - Tiempo (Medio) - Coste (Bajo) |
