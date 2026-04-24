| **Nombre del escenario:** | Flujo principal - Reprogramacion de turno exitosa | | |
|---|---|---|---|
| **Nombre del caso de uso:** | Reprogramar turno | **ID Unica:** | CU-03 |
| **Area:** | Sistema de Gestion de Turnos Medicos - Modificacion de Turnos | | |
| **Actor(es):** | Secretaria (principal), Sistema de Notificaciones WhatsApp | | |
| **Descripcion:** | Permite a la secretaria reasignar un turno existente a un nuevo dia y horario disponible. El sistema libera la franja anterior, bloquea la nueva, guarda el historial del cambio y notifica al paciente por WhatsApp con los nuevos datos del turno (RF3, RNF4). | | |
| **Activar Evento:** | El paciente solicita reprogramar su turno asignado. | | |
| **Tipo de senal:** | [x] Externa | [ ] Temporal | [ ] |

| **Pasos desempenados (ruta principal)** | **Informacion para los pasos** |
|---|---|
| 1. El paciente solicita reprogramar su turno. | Solicitud presencial en recepcion. |
| 2. La secretaria busca el turno en la agenda con los datos del paciente. | Busqueda por apellido, nombre o DNI del paciente. |
| 3. La secretaria selecciona el turno que el paciente desea reprogramar. | Turno en estado "Pendiente" o "Presente". |
| 4. La secretaria elige la opcion "Reprogramar". | Accion habilitada para rol Secretaria (RF4). |
| 5. El sistema presenta el calendario con dias y horarios disponibles. | Disponibilidad respetando horarios habilitados (RF6) y restricciones vigentes (RF5). |
| 6. La secretaria selecciona el nuevo dia y horario para el turno. | Nueva franja que debe estar disponible y cumplir restricciones (RF5, RF6). |
| 7. La secretaria confirma la reprogramacion. | Confirmacion explicita de la operacion. |
| 8. El sistema libera la franja horaria anterior en la agenda. | Horario previo vuelve a estar disponible para nuevos turnos (RF3). |
| 9. El sistema actualiza el turno con la nueva fecha y horario y bloquea la nueva franja. | Cambio persistido con historial de modificacion registrado (RNF4). |
| 10. El sistema envia notificacion por WhatsApp al paciente con el nuevo dia y horario. | Aviso de cambio con datos actualizados del turno (RF7). |
| 11. El sistema confirma la reprogramacion exitosa en pantalla. | Cierre del flujo principal. |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El turno debe estar registrado en el calendario. Debe existir al menos un dia y horario disponible para reprogramar. La secretaria debe estar validada en el sistema. |
| **Poscondiciones:** | El calendario muestra el nuevo dia y horario del turno reprogramado. La franja horaria anterior queda liberada y disponible. El paciente recibe notificacion por WhatsApp con los nuevos datos. El historial del cambio queda registrado obligatoriamente en el sistema (RNF4). |
| **Suposiciones:** | Existe disponibilidad en la agenda para la nueva fecha solicitada. El paciente cuenta con WhatsApp para recibir la notificacion. |
| **Reunir requerimientos:** | RF3 (validacion de conflictos y bloqueo de horarios), RF6 (horarios habilitados), RF5 (restricciones por dia y tipo), RF7 (notificacion al paciente), RNF4 (historial obligatorio de cambios). |
| **Aspectos sobresalientes:** | El historial de cambios es un requisito obligatorio del sistema (RNF4). Se aplican las mismas restricciones horarias que en el alta de turno (RF5, RF6). La operacion debe ser atomica: si falla la persistencia, no se debe liberar la franja anterior ni enviar la notificacion. |
| **Prioridad:** | Alta |
| **Riesgo:** | Alto - Tiempo (Alto) - Coste (Medio) |
