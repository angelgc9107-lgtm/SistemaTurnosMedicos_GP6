| **Nombre del escenario:** | Flujo principal - Bloqueo de dias y horarios exitoso | | |
|---|---|---|---|
| **Nombre del caso de uso:** | Bloquear dias/horarios en calendario | **ID Unica:** | CU-04 |
| **Area:** | Sistema de Gestion de Turnos Medicos - Configuracion de Disponibilidad | | |
| **Actor(es):** | Secretaria (principal), Medico (indica los rangos a bloquear) | | |
| **Descripcion:** | Permite a la secretaria marcar rangos de fechas y horarios como no disponibles en el calendario (por vacaciones, feriados u otras actividades del medico), impidiendo la asignacion de nuevos turnos en esas franjas y mostrando el motivo del bloqueo. | | |

| **Activar Evento:** | El médico informa a la secretaria un periodo de indisponibilidad (vacaciones, feriado, guardia u otra actividad). | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | [x] Externa | [x] Temporal |

| **Pasos desempenados (ruta principal)** | **Informacion para los pasos** |
|---|---|
| 1. El medico informa a la secretaria los horarios y fechas a bloquear con el motivo correspondiente. | Motivos posibles: vacaciones, feriado, horarios no disponibles por otra actividad. |
| 2. La secretaria ingresa al calendario del sistema. | Usuario autenticado con rol Secretaria (RF4). |
| 3. La secretaria selecciona el rango de fechas y horarios indicado por el medico. | Seleccion de rango en la vista del calendario. |
| 4. La secretaria ingresa el motivo u observacion del bloqueo. | Campo de texto libre para registrar la razon del bloqueo. |
| 5. La secretaria confirma el bloqueo del rango seleccionado. | Confirmacion explicita de la operacion. |
| 6. El sistema registra el bloqueo en la agenda y refleja las franjas como no disponibles. | Las franjas bloqueadas dejan de ofrecerse para agendar nuevos turnos (RF3). |
| 7. El calendario muestra las fechas y horarios bloqueados con el motivo ingresado. | Visualizacion diferenciada del bloqueo con descripcion del motivo. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | La secretaria debe estar validada para gestionar disponibilidad en el calendario. El medico debe estar validado en el sistema (RF4). El rango de fechas y motivo deben estar definidos previamente por el medico. |
| **Poscondiciones:** | Las fechas y horarios seleccionados quedan bloqueados en el calendario. El motivo del bloqueo es visible en la agenda. Los horarios bloqueados no estan disponibles para nuevos turnos. |
| **Suposiciones:** | El rango informado por el medico no contiene turnos ya asignados, o estos seran gestionados previamente. El medico comunica la informacion con suficiente anticipacion. |
| **Reunir requerimientos:** | RF3 (bloqueo de horarios para evitar solapamientos), RF4 (roles: secretaria gestiona, medico informa), RF5 (restricciones de dias especificos), RF6 (horarios habilitados del consultorio), RNF5 (la agenda es el unico componente que controla los turnos). |
| **Aspectos sobresalientes:** | El calendario debe mostrar el motivo del bloqueo para informar al usuario (vacaciones, feriado, etc.). Si hay turnos asignados en el rango a bloquear, deben reprogramarse o cancelarse antes de aplicar el bloqueo. Los sabados solo son habilitados ocasionalmente por el medico (RF6). |
| **Prioridad:** | Alta |
| **Riesgo:** | Medio - Tiempo (Medio) - Coste (Medio) |
