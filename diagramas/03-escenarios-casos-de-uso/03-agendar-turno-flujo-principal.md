| **Nombre del escenario:** | Flujo principal - Agendar turno exitoso | | |
|---|---|---|---|
| **Nombre del caso de uso:** | Agendar turno | **ID Unica:** | CU-01 |
| **Area:** | Sistema de Gestion de Turnos Medicos - Agenda | | |
| **Actor(es):** | Secretaria (principal), Medico | | |
| **Descripcion:** | Permite a la secretaria registrar un turno para un paciente con un medico, validando disponibilidad segun horarios definidos (RF6), tipo de turno (RF2) y restricciones especificas (RF5), y notificando la confirmacion por WhatsApp (RF7). |

| **Activar Evento:** | El paciente solicita un turno presencialmente en la recepción del consultorio. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | [x] Externa | [ ] Temporal |

| **Pasos desempenados (ruta principal)** | **Informacion para los pasos** |
|---|---|
| 1. La secretaria selecciona la opcion "Nuevo turno" en la agenda. | Usuario autenticado como Secretaria con permisos de gestion (RF4). |
| 2. El sistema solicita los datos del paciente. | Campos requeridos: Apellido, Nombre, Sexo, Edad y DNI. |
| 3. La secretaria ingresa los datos del paciente y selecciona el tipo de consulta y el medico. | Tipos de consulta: "Primera vez" (30 min) o "Control" (15 min) (RF2). |
| 4. El sistema presenta el calendario semanal. | Vista semanal de la agenda del medico seleccionado (RF1). |
| 5. La secretaria selecciona un dia para ver los horarios disponibles. | Horarios habilitados: Lun-Vie 9-13 y 15-19 (excl. jueves tarde); sabados ocasionales segun el medico (RF6). |
| 6. El sistema muestra horarios disponibles del dia, ocultando los bloqueados. | Horarios ocupados por turnos previos o bloqueos manuales quedan inhabilitados (RF3). |
| 7. La secretaria elige un horario disponible. | Debe cumplir restricciones: sin procedimientos los lunes; sin "Primera vez" los viernes por la tarde (RF5). |
| 8. La secretaria confirma el turno. | Confirmacion explicita de la operacion. |
| 9. El sistema registra el turno en estado "Pendiente" y bloquea la franja horaria. | La duracion bloqueada depende del tipo: 30 min para "Primera vez", 15 min para "Control" (RF2, RF3). |
| 10. El sistema envia notificacion por WhatsApp al paciente con dia y horario del turno. | Notificacion inmediata de confirmacion (RF7). |
| 11. El sistema programa recordatorios automaticos para el paciente. | Recordatorio 24 horas antes y a las 8:00 AM del dia del turno (RF7). |
| 12. El sistema confirma el alta exitosa del turno. | Cierre del flujo principal. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | La secretaria debe estar validada en el sistema. El usuario Medico debe estar registrado. Los horarios habilitados deben estar configurados (RF6). |
| **Poscondiciones:** | Turno guardado en estado "Pendiente" asociado al medico seleccionado. Franja horaria bloqueada segun tipo de turno. Notificacion de confirmacion enviada al paciente. Recordatorios programados para 24 horas antes y 8:00 AM del dia del turno (RF7). |
| **Suposiciones:** | El paciente cuenta con numero de WhatsApp disponible para recibir notificaciones. El medico tiene al menos un horario habilitado en la semana seleccionada. |
| **Reunir requerimientos:** | RF1 (calendario semanal), RF2 (tipos y duracion de turno), RF3 (bloqueo de conflictos), RF5 (restricciones por dia y tipo), RF6 (horarios habilitados), RF7 (notificaciones). |
| **Aspectos sobresalientes:** | Turnos "Primera vez" no pueden agendarse viernes por la tarde (RF5). No se pueden agendar procedimientos los lunes (RF5). Los sabados solo son habilitados por indicacion del medico (RF6). La duracion del bloqueo en agenda varia segun el tipo de turno (RF2). |
| **Prioridad:** | Alta |
| **Riesgo:** | Alto - Tiempo (Alto) - Coste (Medio) |
