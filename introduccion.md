1. Agendar Turno
Actores: Secretaria (Principal), Médico (Secundario para autorizaciones)
.
Descripción: Valeria selecciona fecha, hora y tipo de consulta (Control 15 min / Primera vez 30 min)
. El sistema valida que no haya superposiciones
 y aplica restricciones: lunes sin procedimientos, jueves tarde cerrado y viernes tarde sin "Primera vez"
.
Flujo Alternativo: Si el horario está ocupado, el médico puede autorizar manualmente un sobreturno (máximo 2 por día)
.
2. Registrar Check-in (Llegada del Paciente)
Actor: Secretaria
.
Descripción: Cuando el paciente llega físicamente, la secretaria lo busca en la agenda y marca su estado como "Presente" o "En sala de espera"
.
Resultado: El sistema registra la hora real de llegada para que el médico sepa quién está esperando
.
3. Cancelar o Reprogramar Turno
Actores: Secretaria, Paciente
.
Descripción: Se selecciona un turno existente para anularlo o moverlo a un nuevo hueco disponible
.
Regla Crítica: El sistema debe guardar obligatoriamente un historial de estos cambios y enviar una notificación por WhatsApp al paciente
.
4. Bloquear Agenda por Inactividad
Actor: Secretaria
.
Descripción: Valeria marca rangos de fechas (vacaciones, feriados o días de guardia del doctor) como no disponibles
.
Resultado: El sistema impide la asignación de turnos en esos bloques, reemplazando el calendario físico de pared
.
5. Visualizar Agenda (Diaria/Semanal)
Actores: Secretaria, Médico
.
Descripción: El sistema permite ver los turnos organizados por día o semana en una interfaz clara y sin "tachones"
.
Resultado: Facilita la organización del consultorio y permite al Dr. Molina consultar su carga de trabajo desde el sistema
.
