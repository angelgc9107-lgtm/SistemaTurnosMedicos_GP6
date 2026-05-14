# Diagramas de Actividades

Índice de diagramas de actividades del Sistema de Turnos Médicos (STM).
Generados con PlantUML para los casos de uso 1 y 2.

---

## Diagramas disponibles

| N° | Caso de Uso | Archivo PUML | Archivo PNG | Swimlanes | Actividades |
|----|-------------|--------------|-------------|-----------|-------------|
| 01 | CU1 - Agendar Turno | [04-actividad-agendar-turno-01.puml](./04-actividad-agendar-turno-01.puml) | [04-actividad-agendar-turno-01.png](./04-actividad-agendar-turno-01.png) | Paciente, Secretaria, Sistema | 12+ |
| 02 | CU2 - Registrar Check-in | [04-actividad-registrar-checkin-02.puml](./04-actividad-registrar-checkin-02.puml) | [04-actividad-registrar-checkin-02.png](./04-actividad-registrar-checkin-02.png) | Paciente, Secretaria, Sistema, Médico | 11+ |

---

## Descripción de cada diagrama

### CU1 — Agendar Turno

**Actores representados:** Paciente, Secretaria, Sistema

**Flujo principal documentado:**
- Inicio en solicitud del paciente en recepción
- Ingreso de datos y selección de tipo de consulta y médico
- Presentación del calendario semanal y selección de horario
- Validación de restricciones (RF5): sin "Primera vez" los viernes tarde, sin procedimientos los lunes
- Detección de conflictos de horario con posibilidad de sobreturno
- Registro del turno en estado "Pendiente" y bloqueo de franja horaria (RF2, RF3)
- Envío de confirmación inmediata por WhatsApp (RF7)
- Programación de recordatorios automáticos (24 hs antes y 8:00 AM del día — RF7)

**Requisitos cubiertos:** RF1, RF2, RF3, RF5, RF6, RF7

---

### CU2 — Registrar Check-in (Llegada del Paciente)

**Actores representados:** Paciente, Secretaria, Sistema, Médico

**Flujo principal documentado:**
- Inicio con la presentación física del paciente en recepción
- Búsqueda del turno por nombre, apellido o DNI (RF4)
- Manejo de turno no encontrado y verificación de datos
- Validación de que el turno esté en estado "Pendiente"
- Ejecución de la acción de check-in por la secretaria
- Registro del timestamp real de llegada (RF8)
- Cambio de estado: "Pendiente" → "Presente / En sala de espera" (RF8)
- Actualización en tiempo real de la vista del médico (RF4)
- Llamado al siguiente paciente por el médico

**Requisitos cubiertos:** RF4, RF8

---

## Convención de nomenclatura

```
04-actividad-[nombre-caso-uso]-[número-secuencial].puml
04-actividad-[nombre-caso-uso]-[número-secuencial].png
```

Ejemplos:
- `04-actividad-agendar-turno-01.puml`
- `04-actividad-registrar-checkin-02.puml`
