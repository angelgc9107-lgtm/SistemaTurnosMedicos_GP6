|                                              |                   |                                                              |               |
| -------------------------------------------- | ----------------- | ------------------------------------------------------------ | ------------- |
| **Nombre de la Clase:**                      | HistorialTurno    |                                                              |               |
| **Superclase:**                              |                   |                                                              |               |
| **Subclase:**                                |                   |                                                              |               |
| **Responsabilidades**                        | **Colaboradores** | **Pensamiento del objeto**                                   | **Propiedad** |
| Registrar cambios realizados sobre un turno  | Turno, Agenda     | Guardo cada modificación importante realizada sobre un turno | fechaCambio   |
| Guardar los datos anteriores del turno       | Turno             | Conozco cómo estaba programado el turno antes del cambio     | fechaAnterior |
| Guardar los datos nuevos del turno           | Turno             | Conozco cómo quedó programado el turno después del cambio    | horaAnterior  |
| Mantener trazabilidad de reprogramaciones    | Secretaria        | Permito conocer cuándo y por qué se modificó un turno        | fechaNueva    |
| Permitir consultar modificaciones realizadas | Agenda            | Ayudo a reconstruir el historial de cambios de un turno      | horaNueva     |
|                                              |                   |                                                              | Secretaria        |
