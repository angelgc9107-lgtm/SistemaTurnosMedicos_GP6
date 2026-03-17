# Requisitos iniciales de sistema
[Notebook LM - Material de ayuda](https://notebooklm.google.com/notebook/273191bd-0f6f-400f-ba99-9b9bd4cfc947?pli=1)

### Requisitos funcionales

RF1 El sistema Deberá generar turnos en un agenda que represente el calendario mensual

RF2 Hay dos tipos de turnos, los cuales son turnos de "Primera vez" y de "Control"

RF3 Dependiendo del turno se debe consumir un tiempo determinado en la agenda, turnos de "Control" consumen 25 minutos y los turnos de "Primera vez" consumen 40 minutos del día en la agenda

RF4 Los horarios que ya tengan un turno asignado deben bloquearse para evitar solapamiento entre turnos

RF5 Hay tres tipos de rol en el sistema, según lo seleccionado tendrán diferentes privilegios. "Secretaria" puede generar-modificar turnos, "Paciente" puede ver o cancelar el turno que tiene asignado y "Medico" puede autorizar sobre turnos u horarios en la agenda

RF6 Los días Lunes no se podrán asignar turnos del tipo "Control" y los días viernes no se asignaran turnos del tipo "Primera vez"

RF7 Los horarios y días disponibles para asignar turnos serán los Lunes, Martes, Miércoles, Viernes desde las 9:00 hasta las 13:00 y desde las 15:00 hasta las 19:00

RF8 El sistema deberá enviar un recordatorio en forma de notificación por "Whatsapp" a los "Pacientes" en dos ocaciones, una vez 24 horas antes del turno y otra vez a las 8:00 AM del día del turno asignado

### Requisitos no funcionales

RNF1 Un usuario administrativo sin experiencia previa debe poder agendar el turno en menos de 5 minutos después de una capacitación de 15 minutos.

RNF2 El sistema debe tener la capacidad para aguantar el aumento de usuarios en un 50%

RNF3 El sistema debe cumplir con la normativa HStan-03-2006-priv para garantizar la confidencialidad de los datos del paciente

RNF4 El sistema debe estar disponible los 7 días de la semana las 24 horas

RNF5 En caso de fallas el sistema debe reiniciarse y estar disponible en 2 minutos

RNF6 El sistema debe ser capaz de procesar un turno generado en 5 segundos