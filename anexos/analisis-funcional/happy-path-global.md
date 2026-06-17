# Pseudocódigo - Happy Path Global del Sistema

---

## 1. Escenario Elegido

**Escenario:** Un paciente llama al consultorio, la secretaria agenda el turno con validación de restricciones y notificación automática; el día de la consulta la secretaria registra la llegada del paciente vía check-in; posteriormente reprograma el turno de control a otro horario notificando el cambio; y el médico visualiza su agenda actualizada antes de comenzar a atender.

Este escenario fue elegido como happy path global porque atraviesa la mayor cantidad de clases del sistema y cubre el ciclo de vida completo de un turno médico: creación, ejecución, modificación y visualización.

**Casos de uso involucrados:** CU1 - Agendar Turno, CU2 - Registrar Check-in, CU3 - Reprogramar Turno, CU5 - Visualizar Agenda

**Clases participantes:**

- Paciente
- Medico
- Secretaria
- Turno
- Agenda
- LlegadaPaciente
- HistorialTurno
- ServicioNotificacion
- ControlSistema
- VistaCalendario
- GestorBloqueos
- ValidadorDisponibilidad
- Resultado

---

## 2. Pseudocódigo

```text
INICIO Sistema de Turnos Médicos - Happy Path Global

// ============================================================
// CU1 - Agendar Turno
// La secretaria registra el turno del paciente en el sistema
// ============================================================

// La secretaria ingresa los datos del paciente y selecciona médico
Secretaria secretaria = nuevo Secretaria(legajo)
Medico medico = nuevo Medico(matricula, "Clínica General")
Paciente paciente = nuevo Paciente(dni, nombre, apellido, telefono)

// El sistema consulta disponibilidad del médico para la semana
ControlSistema controlSistema = nuevo ControlSistema()
Resultado acceso = controlSistema.accederAgenda(secretaria.dni, secretaria.rol)

Agenda agenda = nuevo Agenda(medico)
List<Turno> horariosDisponibles = agenda.consultarDisponibilidad(medico.matricula, semanaActual)
List<String> horariosDelDia = agenda.obtenerHorariosDelDia(fecha, medico.matricula)

// El sistema valida restricciones de negocio (RF5)
Boolean horarioValido = agenda.validarRestricciones("PrimeraVez", fecha, hora)

// El sistema verifica disponibilidad de la franja horaria
ValidadorDisponibilidad validador = nuevo ValidadorDisponibilidad()
Boolean disponible = validador.estaDisponible(fecha, hora, "PrimeraVez")

// La secretaria confirma; el sistema registra el turno y bloquea la franja
Turno turno = agenda.registrarTurno(paciente, medico, fecha, hora, "PrimeraVez")
turno.establecerEstado("Pendiente")
agenda.bloquearFranjaHoraria(fecha, hora, turno.obtenerDuracion())  // 30 min

// El sistema notifica confirmación al paciente por WhatsApp (RF7)
ServicioNotificacion svcNotificacion = nuevo ServicioNotificacion(canalWhatsApp)
svcNotificacion.enviarConfirmacion(paciente.telefono, fecha, hora, medico.nombre)
svcNotificacion.programarRecordatorio24h(paciente.telefono, fecha)
svcNotificacion.programarRecordatorioManana(paciente.telefono, fecha)
// Turno registrado en estado "Pendiente"

// ============================================================
// CU2 - Registrar Check-in
// El día del turno, la secretaria registra la llegada del paciente
// ============================================================

// La secretaria busca el turno del paciente por apellido/DNI
Resultado busqueda = controlSistema.buscarTurnoPaciente(paciente.apellido, paciente.nombre, paciente.dni)
Turno turnoEncontrado = agenda.filtrarHorariosDisponibles(paciente.dni, fechaHoy)

// El sistema verifica que el turno esté en estado válido para check-in
// turnoEncontrado.getEstado() == "Pendiente" → habilitado

// La secretaria registra la presencia; el caller solo interactúa con ControlSistema
controlSistema.registrarPresencia(turnoEncontrado)
// ControlSistema delega internamente en Agenda (no se llama agenda.registrarPresencia()
// desde el flujo principal, manteniendo la capa de abstracción):
//   → LlegadaPaciente llegada = agenda.registrarPresencia(turnoEncontrado.idTurno)
//   → llegada.registrarHoraLlegada()                    // horaLlegada = DateTime.ahora()
//   → turnoEncontrado.cambiarEstado("Presente")
//   → llegada.actualizarPresencia(true, "En sala de espera")
//   → llegada.notificarMedico(medico)

// El sistema cancela los recordatorios automáticos ya no necesarios
agenda.cancelarRecordatoriosPendientes(turnoEncontrado.idTurno)
controlSistema.confirmarCheckIn()
// Turno en estado "Presente"; médico visualiza al paciente en agenda

// ============================================================
// CU3 - Reprogramar Turno
// La secretaria reprograma el turno de control a otro horario
// ============================================================

// La secretaria busca el turno y selecciona reprogramar
Resultado busquedaRep = controlSistema.buscarTurnoPaciente(paciente.apellido, paciente.nombre, paciente.dni)
controlSistema.seleccionarReprogramar(turnoEncontrado)

// El sistema consulta disponibilidad para la nueva fecha
List<Time> nuevosHorarios = agenda.obtenerHorariosDelDia(nuevaFecha, medico.matricula)
Boolean nuevoHorarioValido = controlSistema.validarRestricciones("Control", nuevaFecha, nuevaHora)

// La secretaria confirma; ControlSistema encapsula la atomicidad internamente
controlSistema.confirmarReprogramacion()
// confirmarReprogramacion() invoca una única operación atómica en Agenda:
//   → Resultado reprog = agenda.reprogramarTurno(turnoEncontrado, nuevaFecha, nuevaHora)
//   → Internamente: liberarFranjaAnterior + actualizarFechaHora + bloquearNuevaFranja
//   → Si cualquier paso falla, ninguno se aplica (operación todo-o-nada)

// El sistema registra el cambio en el historial (RNF4 - obligatorio)
HistorialTurno historial = nuevo HistorialTurno()
historial.registrarCambio(fecha, hora, nuevaFecha, nuevaHora)

// El sistema notifica al paciente el nuevo horario por WhatsApp (RF7)
// Se reutiliza la instancia svcNotificacion ya creada en CU1 (servicio sin estado propio)
svcNotificacion.enviarReprogramacion(paciente.telefono, nuevaFecha, nuevaHora, medico.nombre)
svcNotificacion.reprogramarRecordatorio(paciente.telefono, nuevaFecha, nuevaHora)
// Turno de control reprogramado en estado "Pendiente"

// ============================================================
// CU5 - Visualizar Agenda
// El médico accede a su agenda para ver los turnos del día
// ============================================================

// El médico accede al sistema con su rol
Resultado accesoMedico = controlSistema.accederAgenda(medico.dni, "Medico")

// El sistema carga la vista diaria; Agenda encapsula la obtención de turnos y bloqueos
Resultado vistaResult = controlSistema.cargarVista("Diaria", fechaActual)
VistaCalendario vista = agenda.obtenerVistaDiaria(fechaActual)
// obtenerVistaDiaria() obtiene internamente turnos (obtenerTurnosPorRango) y
// bloqueos (gestorBloqueos.obtenerBloqueosPorFecha) antes de retornar la vista poblada

// El sistema presenta el calendario ya cargado
vista.mostrarVistaDiaria()

// El médico navega entre fechas si lo necesita
Date nuevaVista = controlSistema.navegarFecha("siguiente")
controlSistema.cerrarVista()

Retornar vistaResult

FIN
```

---

## 3. Trazabilidad del Pseudocódigo

| Bloque | Caso de uso | Clases involucradas | Diagrama de secuencia de referencia |
|--------|-------------|---------------------|-------------------------------------|
| Agendar Turno | CU1 | Secretaria, Medico, Paciente, ControlSistema, Agenda, Turno, ValidadorDisponibilidad, ServicioNotificacion | [05-secuencia-cu-agendar-turno-agendar-turno-flujo-principal-01.png](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-agendar-turno-agendar-turno-flujo-principal-01.png) |
| Registrar Check-in | CU2 | Secretaria, ControlSistema, Agenda, Turno, LlegadaPaciente, Medico | [05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.png](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.png) |
| Reprogramar Turno | CU3 | Secretaria, ControlSistema, Agenda, Turno, HistorialTurno, ServicioNotificacion | [05-secuencia-cu-reprogramar-turno-reprogramar-turno-flujo-principal-03.png](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-reprogramar-turno-reprogramar-turno-flujo-principal-03.png) |
| Visualizar Agenda | CU5 | Medico, ControlSistema, Agenda, Turno, GestorBloqueos, Bloqueo, VistaCalendario, Resultado | [05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png](../../diagramas/05-diagramas-secuencia/05-secuencia-cu-visualizar-agenda-visualizar-agenda-flujo-principal-05.png) |
