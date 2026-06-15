# Los Cuatro Pilares del Paradigma Orientado a Objetos

---

## 1. Encapsulamiento

**Definición:** El encapsulamiento agrupa datos y comportamiento dentro de una clase, ocultando los detalles internos y exponiendo solo lo necesario mediante una interfaz pública controlada.

**Ejemplo 1 — Turno:**

La clase `Turno` encapsula sus atributos internos (`fecha`, `hora`, `estado`, `tipoConsulta`, `fechaRegistro`) con visibilidad privada. Ninguna clase externa puede modificar el estado del turno directamente: debe invocar `establecerEstado(nuevoEstado)` o `cambiarEstado(nuevoEstado)`, que son los únicos puntos de acceso controlados. Esto garantiza que el estado solo pueda transitar por valores válidos (Pendiente, Presente, Cancelado, Reprogramado) y que la duración de la franja sea siempre consistente con el tipo de consulta. Un turno mal modificado desde afuera rompería la integridad del historial y los registros de llegada.

![Encapsulamiento - Ejemplo 1](./capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

**Ejemplo 2 — GestorBloqueos:**

`GestorBloqueos` encapsula la colección interna de bloqueos (`bloqueos: List<Bloqueo>`) y las reglas horarias (`reglasHorario`) como atributos privados. Las clases que necesitan saber si una franja está bloqueada (como `Agenda` o `ValidadorDisponibilidad`) solo invocan `estaBloqueado(fecha, hora)` u `obtenerMotivo(fecha, hora)`, sin acceder nunca a la lista interna. Esto permite modificar la estructura de almacenamiento de bloqueos sin impactar a las clases colaboradoras, lo que es crítico en el dominio porque las reglas de bloqueo pueden cambiar (vacaciones, feriados, licencias) sin afectar la lógica de la agenda.

![Encapsulamiento - Ejemplo 2](./capturas-pilares/poo-encapsulamiento-ejemplo-2.png)

---

## 2. Herencia

**Definición:** La herencia permite que una clase derive de otra, reutilizando atributos y métodos de la superclase y especializando su comportamiento según el rol concreto que representa en el dominio.

**Ejemplo 1 — Persona → Medico:**

`Medico` hereda de `Persona` los atributos de identidad y contacto (`nombre`, `apellido`, `dni`, `telefono`, `email`, `rol`, `estadoActivo`) y los métodos `getDatos()`, `getContacto()` y `notificar()`. Sobre esa base, agrega sus propios atributos (`matricula`, `especialidad`) y métodos específicos de su rol: `definirDisponibilidad()`, `autorizarSobreturno()` y `obtenerAgenda()`. La relación tiene sentido en el dominio porque un médico es ante todo una persona del sistema con datos personales compartidos, pero además tiene responsabilidades que ningún otro rol comparte: solo él puede autorizar sobreturnos y es identificado por su matrícula profesional.

![Herencia - Ejemplo 1](./capturas-pilares/poo-herencia-ejemplo-1.png)

**Ejemplo 2 — Persona → Secretaria:**

`Secretaria` hereda de `Persona` los mismos datos de identidad y agrega `legajo` como propiedad propia y métodos de gestión de turnos: `registrarTurno()`, `cancelarTurno()`, `reprogramarTurno()`, `consultarDisponibilidad()`, `registrarPresencia()` y `accederAgenda()`. La relación tiene sentido porque la secretaria opera el sistema con su propia identidad laboral (legajo), pero comparte con todos los demás roles la necesidad de estar identificada en el sistema (nombre, DNI, teléfono). Su especialización expande el contrato de Persona sin contradecirlo.

![Herencia - Ejemplo 2](./capturas-pilares/poo-herencia-ejemplo-2.png)

---

## 3. Polimorfismo

**Definición:** El polimorfismo permite que distintas clases respondan al mismo mensaje de forma diferente según su implementación, permitiendo tratar objetos de distintos tipos de manera uniforme.

**Ejemplo 1 — notificar(mensaje) en Paciente vs Medico:**

El método `notificar(mensaje: String)` está definido en `Persona` y sobreescrito en `Paciente` y `Medico` con comportamiento diferente. En `Paciente`, `notificar()` envía un SMS al número del paciente. En `Medico`, envía una notificación al panel médico del sistema. Esto permite que `LlegadaPaciente`, al ejecutar `notificarMedico()`, invoque `medico.notificar()` sin conocer el canal concreto. Agregar un nuevo canal de notificación por rol no requiere modificar la lógica de negocio que invoca la notificación.

![Polimorfismo - Ejemplo 1](./capturas-pilares/poo-polimorfismo-ejemplo-1.png)

**Ejemplo 2 — notificar(mensaje) en Secretaria vs Paciente:**

En `Secretaria`, `notificar()` envía una alerta al sistema de gestión administrativo, mientras que en `Paciente` envía un SMS personal. El `ServicioNotificacion` puede invocar `persona.notificar()` de forma uniforme sobre cualquier subclase y cada una resolverá el canal correcto. Esto respeta el principio LSP documentado en el proyecto: todas las subclases cumplen la postcondición de que el destinatario recibe el mensaje, sin importar el canal específico de cada una.

![Polimorfismo - Ejemplo 2](./capturas-pilares/poo-polimorfismo-ejemplo-2.png)

---

## 4. Abstracción

**Definición:** La abstracción consiste en representar solo los aspectos relevantes de un concepto del dominio, ocultando la complejidad de implementación y exponiendo una interfaz simplificada que otras clases pueden usar sin conocer los detalles internos.

**Ejemplo 1 — Agenda:**

`Agenda` abstrae toda la complejidad de la gestión de disponibilidad horaria. Las clases que necesitan consultar, registrar o bloquear turnos solo invocan métodos como `consultarDisponibilidad()`, `registrarTurno()` o `bloquearRango()`. Detrás, `Agenda` coordina internamente la colección de turnos, el `GestorBloqueos`, el `ValidadorDisponibilidad` y la `VistaCalendario`. Las clases colaboradoras no necesitan conocer esa complejidad: solo piden una operación de negocio y `Agenda` la resuelve de forma centralizada, respetando RNF5 (único componente que controla la gestión de turnos).

![Abstracción - Ejemplo 1](./capturas-pilares/poo-abstraccion-ejemplo-1.png)

**Ejemplo 2 — ControlSistema:**

`ControlSistema` abstrae la coordinación de los flujos de negocio del sistema. Cuando `Secretaria` necesita registrar un check-in, solo invoca `controlSistema.registrarPresencia(turno)`. Detrás, `ControlSistema` delega en `Agenda`, que a su vez crea `LlegadaPaciente`, actualiza el estado del `Turno` y cancela recordatorios pendientes. La `Secretaria` no conoce esa cadena de colaboraciones: interactúa con una interfaz simple que oculta la complejidad del flujo interno, respetando el principio de separación de responsabilidades entre la presentación y la lógica de dominio.

![Abstracción - Ejemplo 2](./capturas-pilares/poo-abstraccion-ejemplo-2.png)
