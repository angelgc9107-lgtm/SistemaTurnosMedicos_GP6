Caso de Uso 1: Agendar Turno
Actores: Valeria (Secretaria - Actor principal), Dr. Molina (Médico - Actor secundario)
.
Precondiciones:
El sistema debe tener configurados los horarios de atención (Lunes a viernes de 09:00 a 13:00 y 15:00 a 19:00)
.
El horario seleccionado debe estar libre para evitar la superposición, que es el problema crítico a resolver
.
Flujo Principal:
El actor selecciona la fecha en la agenda digital
.
El actor elige el tipo de consulta: Control (15 min) o Primera vez (30 min)
.
El sistema muestra los huecos disponibles según la duración elegida
.
El actor ingresa los datos del paciente y confirma la reserva.
El sistema registra el turno y lo visualiza de forma clara sin tachones
.
Flujo Alternativo:
Gestión de Sobreturnos: Si el horario está ocupado pero el Dr. Molina lo autoriza manualmente (por insistencia del paciente o carga del día), el sistema debe permitir forzar la entrada del paciente como "sobreturno" sin ser una regla automática
.
Postcondiciones: El turno queda agendado y se dispara una notificación automática de confirmación al paciente (preferentemente vía WhatsApp)

