|  |  |  |  |
| ----- | ----- | ----- | ----- |
| **Nombre de la Clase:**               |ControlSistemas |    |    |
| **Superclase:**                       |    |    |    |
| **Subclase:**                         |                                |                                                                        |               |
| **Responsabilidades**                 | **Colaboradores**              | **Pensamiento del objeto**                                             | **Propiedad** |
| Coordinar la búsqueda de turnos       | Agenda, Secretaria, Medico             | Recibo la solicitud de la secretaria y delego la búsqueda en la agenda |               |
| Coordinar el registro de check-in     | Agenda, Turno, LlegadaPaciente | Organizo el flujo para marcar la llegada del paciente                  |               |
| Coordinar la reprogramación de turnos | Agenda, Turno, HistorialTurno  | Gestiono la operación sin reemplazar el control central de la agenda   |               |
| Solicitar notificaciones de cambios   | ServicioNotificacion           | Pido que se informe al paciente cuando corresponde                     |               |