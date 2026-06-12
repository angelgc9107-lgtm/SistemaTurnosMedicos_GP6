|  |  |  |  |
|---|---|---|---|
| **Nombre de la Clase:** | GestorBloqueos | | |
| **Superclase:** | | | |
| **Subclase:** | | | |
| **Responsabilidades** | **Colaboradores** | **Pensamiento del objeto** | **Propiedad** |
| Registrar bloqueo de rango con motivo | Agenda, Secretaria, Medico | Sé cuándo una franja está bloqueada y por qué | listaBloqueos |
| Verificar solapamientos con turnos existentes | Turno, Agenda | Sé si un bloqueo afecta turnos ya asignados | |
| Consultar bloqueos por fecha o rango | Agenda, VistaCalendario | Sé qué bloqueos impactan la agenda seleccionada | |
| Asociar motivo y estado al bloqueo | Secretaria, Medico | Sé describir la indisponibilidad de la franja | |
| Informar disponibilidad al calendario | Agenda, VistaCalendario | Sé si una franja puede reservarse o está anulada | reglasHorario |
| Actualizar la agenda con franjas no disponibles | Agenda, VistaCalendario | Sé marcar bloques como inválidos para nuevos turnos | |
