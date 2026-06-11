# Análisis Funcional del Caso de Uso 1: Agendar Turno
## Especialista: Analista Funcional

### Prompt utilizado

```
Actúa como Analista Funcional del Caso de Uso 1 (Agendar Turno) y Coordinador de Repositorio del proyecto SistemaTurnosMedicos_GP6.

CONTEXTO OBLIGATORIO:
1. Diagrama de casos de uso: diagramas/02-casos-de-uso/02-agendar-turno-01.puml
2. Escenario: diagramas/03-escenarios-casos-de-uso/03-agendar-turno-flujo-principal.md
3. Diagrama de actividades: diagramas/04-diagramas-actividades/04-actividad-agendar-turno-01.puml
4. Diagrama de secuencia: diagramas/05-diagramas-secuencia/05-secuencia-cu-agendar-turno-agendar-turno-flujo-principal-01.puml
5. Tarjetas CRC: todas las de herramientas-agile/tarjetas-crc/
6. Requisitos funcionales: anexos/introduccion.md

TAREAS:
1. Diseñar diagrama de clases específico para CU1 (diagramas/01-diagrama-clases/01-clases-agendar-turno-01.puml)
2. Generar PNG (diagramas/01-diagrama-clases/01-clases-agendar-turno-01.png)
3. Crear anexo: anexos/analisis-funcional/01-caso-de-uso-agendar-turno.md
4. Actualizar índices

RESTRICCIONES:
- No inventar requisitos, actores, clases ni métodos
- Todo debe surgir de los artefactos existentes
- Trazabilidad completa entre diagrama de secuencia, CRC y clase
- Nombres exactos según repositorio
```

### Archivos utilizados como contexto

1. **Artefactos de CU1:**
   - `diagramas/02-casos-de-uso/02-agendar-turno-01.puml` (actores: Secretaria, Paciente, sistema WhatsApp)
   - `diagramas/03-escenarios-casos-de-uso/03-agendar-turno-flujo-principal.md` (flujo con 12 pasos)
   - `diagramas/04-diagramas-actividades/04-actividad-agendar-turno-01.puml` (swimlanes: Paciente, Secretaria, Sistema)
   - `diagramas/05-diagramas-secuencia/05-secuencia-cu-agendar-turno-agendar-turno-flujo-principal-01.puml` (participantes: Secretaria, Sistema, Agenda, Turno, ServicioNotificacion)

2. **Tarjetas CRC:**
   - `00-tarjeta-crc-persona.md` (superclase abstracta)
   - `01-tarjeta-crc-paciente.md` (hereda de Persona)
   - `02-tarjeta-crc-medico.md` (hereda de Persona)
   - `05-tarjeta-crc-secretaria.md` (hereda de Persona)
   - `03-tarjeta-crc-turno.md` (entidad core)
   - `04-tarjeta-crc-agenda.md` (entidad core)
   - `08-tarjeta-crc-servicio-notificacion.md` (servicio)

3. **Requisitos:**
   - `anexos/introduccion.md` (RF1-RF8, casos de uso CU1-CU6)

### Ajustes realizados sobre propuesta inicial

**Decisión 1: Inclusión de Turno como clase con identidad**
- Propuesta inicial: Turno solo como agregación de Agenda
- Ajuste: Turno es entidad con identidad propia (idTurno: UUID) y atributos de estado
- Justificación: Diagrama de secuencia muestra `<<create>> new Turno(...)` → Turno es clase que se instancia

**Decisión 2: Métodos de Agenda**
- Fuente: Diagrama de secuencia enumera: consultarDisponibilidad, obtenerHorariosDelDia, filtrarHorariosDisponibles, verificarDisponibilidad, registrarTurno, validarHorario, validarRestricciones, bloquearFranjaHoraria
- Aplicado: Todos incluidos en clase Agenda con firmas de método tipadas

**Decisión 3: Métodos de Turno**
- Fuente: Escenario paso 9 "registra turno en estado Pendiente"; Secuencia "establecerEstado('Pendiente'); bloquearFranja()"
- Aplicado: establecerEstado(String), bloquearFranja(Integer), obtenerDuracion(), validarRestricciones()

**Decisión 4: Relaciones UML**
- Agregación vs Composición: Agenda *-- Turno (agregación con propietario fuerte)
- Dependencia: Agenda ..> ServicioNotificacion (no es tenencia, es delegación temporal)
- Asociaciones bidireccionales: Secretaria → Agenda, Medico → Agenda (ambas gestionan)

**Decisión 5: Atributos de Turno**
- Fuente: Escenario pasos 2-9: tipoConsulta, estado, fecha, hora, paciente, medico
- Agregado: fechaRegistro para auditoría (RNF4: "mantener historial de cambios")

### Iteraciones relevantes

**Iteración 1: Análisis de Diagrama de Secuencia**
- Identificadas 5 clases participantes: Secretaria, Sistema, Agenda, Turno, ServicioNotificacion
- Mapeadas operaciones de cada clase al diagrama de secuencia

**Iteración 2: Trazabilidad CRC→Métodos**
- Paciente.solicitar() → CRC: "Solicitar un turno médico"
- Médico.autorizarSobreturno() → CRC: "Solo yo decido si se agrega un turno extra"
- Secretaria.registrarTurno() → CRC: "Registrar turnos"
- Agenda.consultarDisponibilidad() → CRC: "Mostrar turnos disponibles"
- ServicioNotificacion.enviarConfirmacion() → CRC: "Enviar confirmación de turno"

**Iteración 3: Restricciones RF5**
- Escenario línea 20: "Debe cumplir restricciones: sin procedimientos los lunes; sin Primera vez viernes tarde"
- Aplicado: método validarRestricciones(tipoConsulta, fecha, hora) en Agenda
- Aplicado: método validarRestricciones() en Turno para self-validation

**Iteración 4: Horarios habilitados RF6**
- Escenario línea 18: "Horarios habilitados: Lun-Vie 9-13 y 15-19"
- Aplicado: atributo horariosHabilitados: String = "Lun-Vie 9-13, 15-19" en Agenda

### Justificación de cambios

1. **Herencia de Persona**: Respeta modelo OO definido en introducción.md + CRC cards
2. **Agregación Agenda-Turno**: Agenda es propietaria, mantiene colección, responsabilidad central (RF1)
3. **Dependencia Agenda→ServicioNotificacion**: No es propiedad, es delegación temporal (patrón Dependency Injection)
4. **Métodos tipados**: Aumentan claridad y trazabilidad vs diagrama de secuencia
5. **idTurno: UUID**: Permite identificación única, coherente con bases de datos relacionales
6. **Estados explícitos en Turno**: Facilita validación y auditoría

### Coherencia con artefactos

| Artefacto | Mapeo | Trazabilidad |
|-----------|-------|-------------|
| Diagrama Secuencia | Secretaria.registrarTurno() | Secuencia línea 72: `confirmarTurno()` |
| Diagrama Secuencia | Agenda.consultarDisponibilidad() | Secuencia línea 42: `consultarDisponibilidad(matricula, semana)` |
| Diagrama Secuencia | Turno.establecerEstado() | Secuencia línea 82: `establecerEstado("Pendiente")` |
| Diagrama Actividades | Secretaria.validarRestricciones() | Actividad línea 52: decision "¿Horario cumple restricciones?" |
| Escenario CU1 | Agenda.horariosDisponibles | Escenario paso 5: "horarios disponibles del dia" |
| Requisito RF2 | Turno.tipoConsulta | RF2: "30 min / 15 min" |
| Requisito RF5 | Agenda.validarRestricciones() | RF5: restricciones específicas |
| Requisito RF7 | ServicioNotificacion.enviarConfirmacion() | RF7: "Envío de recordatorios por WhatsApp" |
