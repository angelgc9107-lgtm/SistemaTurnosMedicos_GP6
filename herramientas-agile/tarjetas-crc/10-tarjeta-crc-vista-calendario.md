|  |  |  |  |
|---|---|---|---|
| **Nombre de la Clase:** | VistaCalendario | | |
| **Superclase:** | | | |
| **Subclase:** | | | |
| **Responsabilidades** | **Colaboradores** | **Pensamiento del objeto** | **Propiedad** |
| Mostrar vista diaria | Agenda, Turno, GestorBloqueos | Sé cómo presentar la agenda del día | periodoActual |
| Mostrar vista semanal | Agenda, Turno, GestorBloqueos | Sé cómo agrupar turnos y bloqueos por semana | tipoVista |
| Renderizar turnos con estados | Turno, Usuario | Sé distinguir estados Pendiente/Presente | |
| Mostrar horarios bloqueados con motivo | GestorBloqueos, Agenda | Sé mostrar franjas no disponibles en el calendario | |
| Actualizar la vista al cambiar período | Usuario, Agenda | Sé presentar la agenda sin modificar datos | |
| Respetar horarios habilitados del consultorio | Agenda, GestorBloqueos | Sé qué horarios pueden mostrarse y cuáles no | |
