# Principio de Segregación de Interfaces (ISP) en el sistema de turnos médicos
---

## Propósito y Tipo del Principio SOLID
El principio de Segregación de Interfaces (ISP) establece que "ningún cliente debe verse obligado a depender de métodos que no usa". En SOLID, ISP es un principio de diseño que busca dividir contratos grandes en interfaces más pequeñas y cohesivas, de modo que cada clase implemente solo las operaciones necesarias para su rol.

---

## Motivación con ejemplo del proyecto
En el sistema de turnos médicos actual, las entidades del dominio realizan actividades claramente diferenciadas:
- `Secretaria`: agenda, cancela/reprograma turnos, consulta disponibilidad y registra la llegada del paciente.
- `Medico`: define disponibilidad, autoriza sobreturnos y atiende pacientes.
- `Agenda`: controla la disponibilidad de horarios y los turnos existentes.

Una interfaz única que contenga todos estos métodos sería demasiado amplia y obligaría a clases como `Medico` y `Agenda` a depender de operaciones que no usan, generando acoplamientos innecesarios.

---

## Explicación de Interfaces
Para respetar ISP en este dominio, se proponen las siguientes interfaces específicas:

- `IRegistroDeTurnos`
  - `registrarTurno()`
  - `cancelarTurno()`
  - `reprogramarTurno()`
  - Justificación: agrupa el comportamiento de manejo del ciclo de vida del turno sin mezclarlo con la presentación de disponibilidad o la llegada del paciente.

- `IConsultaDeDisponibilidad`
  - `consultarDisponibilidad()`
  - `mostrarTurnosDisponibles()`
  - Justificación: separa la consulta y visualización de horarios de la lógica de modificación de turnos.

- `IAutorizacionDeSobreturno`
  - `autorizarSobreturno()`
  - Justificación: es un comportamiento médico específico que no le corresponde a la secretaria ni a la agenda.

- `IRegistroDeAsistencia`
  - `registrarHoraLlegada()`
  - `marcarPresencia()`
  - `notificarMedico()`
  - Justificación: representa el registro de check-in y notificación, un dominio concreto alineado con la llegada del paciente.

Estas interfaces son coherentes con el dominio del sistema y no son genéricas ni artificiales.

---

## Estructura de Clases con referencia al diagrama
El diagrama ISP muestra cómo se distribuyen las responsabilidades:

- `Persona` es la superclase abstracta de `Paciente`, `Medico` y `Secretaria`.
- `Secretaria` implementa:
  - `IRegistroDeTurnos`
  - `IConsultaDeDisponibilidad`
  - `IRegistroDeAsistencia`
- `Medico` implementa:
  - `IAutorizacionDeSobreturno`
- `Agenda` implementa:
  - `IConsultaDeDisponibilidad`

Otras relaciones relevantes:
- `Paciente` es cliente de `IRegistroDeTurnos` al solicitar y cancelar turnos.
- `Turno` referente al ciclo de vida de la cita y colabora con `Paciente`, `Medico`, `Agenda` y `LlegadaPaciente`.

---

## Estructura de Clases y Diagrama UML
A continuación se muestra cómo se han diseñado las interfaces segregadas y cómo las clases existentes implementan cada contrato en el dominio de turnos médicos.

[![Diagrama ISP](../../diagramas/01-diagrama-clases/01-solid-04-isp.png)](../../diagramas/01-diagrama-clases/01-solid-04-isp.puml)

- Archivo PlantUML: `diagramas/01-diagrama-clases/01-solid-04-isp.puml`
- Imagen del diagrama: `diagramas/01-diagrama-clases/01-solid-04-isp.png`

---

## Justificación Técnica
### 1. Interfaces semánticas y específicas del dominio
Se eligieron nombres que expresan tareas reales del sistema de turnos médicos: `IRegistroDeTurnos`, `IConsultaDeDisponibilidad`, `IAutorizacionDeSobreturno` e `IRegistroDeAsistencia`.

### 2. Detección de interfaces gordas
Una interfaz como `IGestionDeTurnos` con métodos de registro, consulta, autorización y asistencia sería demasiado amplia. Forzaría a `Medico` a implementar métodos relacionados con disponibilidad administrativa y a `Agenda` a implementar notificación de llegada, violando ISP.

### 3. Descarte de propuestas poco adecuadas
- `IGestionTurno`: demasiado genérica y mezcla responsabilidades administrativas y médicas.
- `IUsuarioSistema`: no aporta valor semántico ni clarifica el comportamiento de cada clase.
- `IRegistroGeneral`: demasiado amplia para la segregación de tareas.

### 4. Beneficios de segregar las interfaces
- Reduce el acoplamiento entre clases.
- Facilita la prueba de componentes específicos.
- Permite ampliar el sistema con nuevos roles sin obligar a clases existentes a implementar operaciones innecesarias.
- Mejora la legibilidad del diseño al vincular métodos concretos a responsabilidades de rol.

### 5. Justificación aplicada al modelo actual
Aunque el origen del comportamiento es `LlegadaPaciente`, es `Secretaria` quien ejecuta el check-in según el caso de uso CU2. Por eso implementa `IRegistroDeAsistencia`, y `LlegadaPaciente` actúa como entidad de dominio colaboradora.

---

### Resumen de la propuesta ISP para el sistema
- Interfaces pequeñas y de propósito único.
- Clases implementan solo los contratos que reflejan su rol.
- `Secretaria` administra turnos y registra asistencias.
- `Medico` autoriza sobreturnos sin tomar responsabilidades administrativas.
- `Agenda` se usa principalmente para consulta de disponibilidad.
- La segregación evita que una sola interfaz mezcle tareas administrativas, de presencia y de autorización.
