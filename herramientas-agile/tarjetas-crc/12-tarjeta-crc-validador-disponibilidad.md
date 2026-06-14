|  |  |  |  |
|---|---|---|---|
| **Nombre de la Clase:** | ValidadorDisponibilidad | | |
| **Superclase:** | | | |
| **Subclase:** | | | |
| **Responsabilidades** | **Colaboradores** | **Pensamiento del objeto** | **Propiedad** |
| Validar que el rango de fechas y horarios tenga una estructura coherente (inicio anterior a fin) | RangoFechaHora | Sé reconocer un rango de fechas/horarios mal formado | |
| Validar que el rango solicitado esté dentro de los horarios habilitados del consultorio | Agenda, RangoFechaHora | Sé qué días y horarios están habilitados para el consultorio | horariosHabilitados |
| Informar si un rango es apto para ser bloqueado | Agenda | Sé responder si un rango puede aplicarse o no antes de modificar la agenda | |