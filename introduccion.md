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

Caso de Uso 2: Agendar Turno Médico
Actores: Valeria (Secretaria), Dr. Molina (Médico)
.
Precondiciones: El sistema debe tener configurados los horarios de atención (Lunes a viernes de 9 a 13 y de 15 a 19)
.
Flujo Principal:
Valeria selecciona el tipo de cita: Control (15 minutos de duración prevista) o Primera vez (30 minutos)
.
El sistema busca un espacio disponible en la agenda digital clara
.
Valeria ingresa los datos del paciente.
El sistema valida que no exista superposición con otro turno en el mismo horario
.
Se confirma la reserva.
Flujo Alternativo:
Sábados: Si el paciente requiere un sábado, Valeria verifica si el Dr. Molina habilitó ese sábado específico, ya que se define mes a mes
.
Tolerancia: Si un paciente llega tarde, el sistema debe contemplar un margen de 10 minutos antes de que el médico decida si lo atiende o lo reprograma
.
Postcondiciones: El turno queda registrado sin tachones y se dispara una notificación automática por WhatsApp al paciente

Caso de Uso 3: Gestión de Sobreturnos (Manual)
Actores: Dr. Molina (Actor principal), Valeria (Actor secundario)
.
Precondiciones: El horario solicitado ya se encuentra ocupado.
Flujo Principal:
Un paciente insiste en un turno o el doctor decide agregar a alguien extra al inicio del día
.
El Dr. Molina autoriza la entrada del paciente extra de forma manual
.
Valeria registra al paciente en el sistema como un "sobreturno"
.
Flujo Alternativo: El Dr. Molina decide no aceptar el sobreturno según la carga de trabajo que tenga ese día específico
.
Postcondiciones: El paciente queda registrado en la agenda del día, aunque el sistema no lo asigne automáticamente para evitar el caos

Caso de Uso 4: Bloqueo de Agenda por Inactividad
Actores: Valeria
.
Precondiciones: El Dr. Molina comunica sus periodos de ausencia.
Flujo Principal:
Valeria accede al módulo de calendario (que reemplaza al calendario físico de pared)
.
Selecciona el rango de fechas correspondientes a vacaciones, feriados o eventos generales
.
El sistema marca el periodo como no disponible para la toma de turnos.
Postcondiciones: Se previene que Valeria dé turnos por error en días donde el consultorio estará cerrado

Caso de Uso 5: Reprogramación o Cancelación de Cita
Actores: Valeria
.
Precondiciones: Debe existir una cita previamente agendada.
Flujo Principal:
Valeria identifica el turno en la agenda digital
.
Realiza el cambio de horario o la cancelación (eliminando la necesidad de tachar y escribir encima)
.
El sistema actualiza la disponibilidad de la página afectada
.
Postcondiciones: El sistema envía automáticamente un mensaje al paciente informando el cambio para evitar que se presente al consultorio sin aviso
