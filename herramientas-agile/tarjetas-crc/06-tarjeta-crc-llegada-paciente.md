|  |  |  |  |
|---|---|---|---|
| **Nombre de la Clase:** | LlegadaPaciente | | |
| **Superclase:**| — (Entidad de dominio independiente) | | |  
| **Subclase:** | | | |  
| **Responsabilidades** | **Colaboradores** | **Pensamiento del objeto** | **Propiedad** |
| Registrar hora real de llegada | Turno, Secretaria | Existo solo si el paciente llega, sé cuándo llegó realmente | horaLlegada |
| Indicar presencia del paciente | Turno, Agenda | Sé si el paciente está presente o ausente | presente |
| Notificar al médico | Médico, Secretaria | Informe cuando el paciente ya está en la sala | estadoPresencia |
| Herencia: | NO (Entidad de dominio independiente) |
| Notas: | LlegadaPaciente es un objeto de dominio que NO hereda de Persona.
              | Representa un acto de llegada, no una identidad de usuario. |
