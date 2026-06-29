# Anexo - Aplicacion de Patron de Diseno Estructural

## Adapter - Patrones de Diseno Estructurales y su relacion con SOLID

---

## Proposito y Tipo del Patron

### Patrones estructurales y su relacion con SOLID

Los patrones de diseno estructurales de GoF se ocupan de como se componen clases y objetos para formar estructuras mas grandes, sin perder flexibilidad ni claridad. Su objetivo no es describir algoritmos ni flujos de control, sino establecer la forma en que las piezas del sistema se conectan entre si.

Su relacion con los principios SOLID es directa:

| Principio | Como lo refuerzan los patrones estructurales |
|-----------|---------------------------------------------|
| SRP | Separan la logica de adaptacion o composicion en clases dedicadas, evitando que una clase acumule responsabilidades de traduccion ademas de las propias |
| OCP | Permiten extender el comportamiento del sistema (nuevos canales, componentes, decoradores) sin modificar las clases existentes |
| DIP | El cliente depende de una abstracción (interfaz target), no de implementaciones concretas |
| ISP | Las interfaces target son reducidas y especificas; cada adaptador implementa solo lo que corresponde |
| LSP | Cada adaptador respeta el contrato de `INotificadorCanal`, permitiendo que sean intercambiables sin que el cliente (`ServicioNotificacion`) se vea afectado |

### Proposito:

**Problema estructural:** `ServicioNotificacion` era una clase concreta que enviaba notificaciones unicamente a traves de WhatsApp. `Agenda` la creaba directamente (`<<crea>>`), acoplandose a una implementacion especifica. Para agregar notificaciones por email o SMS, era necesario modificar tanto `ServicioNotificacion` como `Agenda`, violando OCP y DIP. Adicionalmente, cada proveedor externo (WhatsApp Business API, SMTP, Twilio) expone una interfaz completamente distinta: metodos con nombres, parametros y tipos de retorno incompatibles entre si.

**Como lo resuelve el patron:** Se introduce la interfaz `INotificadorCanal` como *target*. Cada proveedor externo es envuelto por un *Adapter* (`AdaptadorWhatsApp`, `AdaptadorEmail`, `AdaptadorSMS`) que traduce `INotificadorCanal` a la API del proveedor correspondiente. `ServicioNotificacion` pasa a ser el *client*: solo conoce `INotificadorCanal` y delega en los canales registrados. `Agenda` ya no crea ni conoce ningun canal concreto; solo usa `ServicioNotificacion`.

### Tipo:

Patron estructural seleccionado: **Adapter**.

El patron **Adapter** (tambien llamado *Wrapper*) permite que dos clases con interfaces incompatibles trabajen juntas. Introduce una clase intermediaria, el *Adapter*, que traduce las llamadas de la interfaz que el cliente conoce (*target*) a las llamadas que requiere la clase existente (*adaptee*).

Se elige Adapter porque el problema principal del sistema es la incompatibilidad entre APIs externas de notificacion (WhatsApp, Email, SMS), y se necesita una interfaz uniforme para evitar acoplamiento y permitir extensibilidad.

---

## Motivacion

En esta seccion se describe en detalle:

- Como estaban estructuradas inicialmente las clases del sistema.
- Que problemas surgian debido a la rigidez de las relaciones entre clases (acoplamiento, complejidad, falta de extensibilidad).
- Que clases participaban en el problema original.
- Que nuevas clases incorpora el patron estructural y cual es el rol de cada una.
- Como el patron organiza la arquitectura para resolver el inconveniente detectado (desacoplamiento, simplificacion, encapsulamiento).

### Desarrollo del caso real

El sistema de turnos medicos contempla notificaciones como parte del flujo de negocio: confirmacion de turno (CU1), recordatorios automaticos, notificacion de reprogramacion (CU3) y cancelacion de recordatorios tras check-in (CU2). En el diagrama final (v4), `Agenda` era responsable de crear `ServicioNotificacion` y `ServicioNotificacion` concentraba toda la logica de envio para un unico canal, WhatsApp.

Este diseno presentaba tres problemas concretos:

1. **Dificultad para incorporar nuevos canales de notificacion**

El sistema estaba disenado para enviar notificaciones unicamente mediante WhatsApp. Si la clinica necesitaba incorporar un nuevo canal, como email o SMS, era necesario modificar `ServicioNotificacion` para agregar la logica correspondiente. Esto dificultaba extender el sistema con nuevas alternativas de comunicacion y hacia que cada incorporacion implicara cambios sobre codigo existente.

2. **Interfaces externas incompatibles**

Cada proveedor de notificaciones ofrece una API diferente. Mientras WhatsApp utiliza un metodo como `sendMessage(phoneNumber, messageText)`, un servicio de correo electronico requiere direccion, asunto y cuerpo del mensaje, y un proveedor de SMS puede devolver un tipo de dato distinto. Estas diferencias impiden utilizar todos los proveedores mediante una interfaz comun, obligando al sistema a adaptarse a cada API en particular.

3. **Dependencia directa de infraestructura**

La logica del sistema quedaba vinculada a clases concretas encargadas de comunicarse con proveedores externos de notificaciones. Como consecuencia, las clases del dominio terminaban dependiendo de implementaciones especificas de infraestructura en lugar de hacerlo de una abstraccion. Esto incrementaba el acoplamiento entre ambas capas y reducia la flexibilidad de la arquitectura ante cambios tecnologicos.

### Como el patron Adapter resuelve el problema

El patron introduce un nivel de indireccion mediante la interfaz *target* `INotificadorCanal`. El vocabulario del patron en este sistema es el siguiente:

| Rol GoF | Clase en el sistema | Descripcion |
|---------|--------------------|-------------------------------------------------|
| **Target** | `INotificadorCanal` | Interfaz uniforme que el client conoce. Define `enviarConfirmacion()`, `enviarCancelacion()`, `enviarReprogramacion()`, `enviarRecordatorio()` y `estaDisponible()` |
| **Client** | `ServicioNotificacion` | Usa `INotificadorCanal`. Mantiene una lista de adapters para traducir la misma operacion de negocio a APIs externas incompatibles, sin conocer proveedores concretos |
| **Adapter** | `AdaptadorWhatsApp` | Implementa `INotificadorCanal` y traduce las llamadas a `WhatsAppGateway.sendMessage()` |
| **Adapter** | `AdaptadorEmail` | Implementa `INotificadorCanal` y construye asunto + cuerpo HTML antes de llamar a `EmailGateway.sendEmail()` |
| **Adapter** | `AdaptadorSMS` | Implementa `INotificadorCanal`, trunca el mensaje a 160 caracteres y convierte el `DeliveryStatus` de retorno a `Boolean` antes de delegar en `SMSGateway.dispatch()` |
| **Adaptee** | `WhatsAppGateway` | API externa de WhatsApp Business. Interfaz propia, no modificable |
| **Adaptee** | `EmailGateway` | Cliente SMTP externo. Interfaz propia, no modificable |
| **Adaptee** | `SMSGateway` | Proveedor de SMS externo (ej. Twilio). Interfaz propia, no modificable |

### Clases implicadas: rol y responsabilidad

**`INotificadorCanal` (nueva - target):**
Define el contrato minimo para cualquier canal de notificacion del sistema. Es la unica cosa que `ServicioNotificacion` conoce de los canales. Su existencia permite cumplir DIP: el dominio depende de esta abstraccion, nunca de los proveedores concretos.

**`ServicioNotificacion` (modificada - client):**
Deja de ser un canal concreto y pasa a ser un *orquestador de adapters*. Mantiene una lista de `INotificadorCanal` porque cada elemento traduce el mismo contrato del dominio hacia una API externa incompatible. Al recibir una solicitud de notificacion, delega en los adapters disponibles sin conocer detalles del proveedor. Esta separacion hace explicito que la responsabilidad central es la adaptacion de interfaces y no la logica del canal externo.

**`AdaptadorWhatsApp`, `AdaptadorEmail`, `AdaptadorSMS` (nuevas - adapters):**
Cada uno conoce exactamente un adaptee. Su unica responsabilidad es traducir el vocabulario de `INotificadorCanal` al vocabulario de la API concreta. Por ejemplo, `AdaptadorSMS` sabe que `SMSGateway.dispatch()` devuelve `DeliveryStatus`, y lo convierte a `Boolean` para respetar el contrato del target. Cada adapter tambien implementa `estaDisponible()` consultando el estado del proveedor, lo que permite que `ServicioNotificacion` omita un canal si su proveedor esta caido.

**`WhatsAppGateway`, `EmailGateway`, `SMSGateway` (existentes o de terceros - adaptees):**
Son clases externas cuya interfaz no se controla ni se modifica. El patron Adapter es precisamente la herramienta para trabajar con APIs de terceros sin acoplar el dominio a ellas.

**`Agenda` (sin cambios en su interfaz):**
Sigue usando `ServicioNotificacion` para notificaciones. Con el patron aplicado, `Agenda` no necesita cambiar cuando se incorpora un nuevo canal: basta con crear un nuevo adapter e inyectarlo en `ServicioNotificacion`.

## Estructura de Clases

Solo se incluyen en el diagrama las clases directamente relacionadas con la aplicacion del patron, evitando sobrecargarlo con detalles irrelevantes. Esto permite visualizar claramente la estructura solucion-problema.

### Ver diagrama en tamano completo

![Patron Estructural - Adapter](../../diagramas/01-diagrama-clases/01-patron-estructural-adapter.png)

[Ver diagrama completo](../../diagramas/01-diagrama-clases/01-patron-estructural-adapter.png)

---

## Justificacion Tecnica de la Estructura de Clases

En esta seccion se proporciona una explicacion tecnica basada en el diagrama UML presentado anteriormente.

### Descripcion de cada clase incluida en el diagrama

**`INotificadorCanal` (nueva - target):**
Define el contrato minimo para cualquier canal de notificacion del sistema. Es la unica cosa que `ServicioNotificacion` conoce de los canales. Su existencia permite cumplir DIP: el dominio depende de esta abstraccion, nunca de los proveedores concretos.

**`ServicioNotificacion` (modificada - client):**
Deja de ser un canal concreto y pasa a ser un *orquestador de adapters*. Mantiene una lista de `INotificadorCanal` porque cada elemento traduce el mismo contrato del dominio hacia una API externa incompatible. Al recibir una solicitud de notificacion, delega en los adapters disponibles sin conocer detalles del proveedor.

**`AdaptadorWhatsApp`, `AdaptadorEmail`, `AdaptadorSMS` (nuevas - adapters):**
Cada uno conoce exactamente un adaptee. Su unica responsabilidad es traducir el vocabulario de `INotificadorCanal` al vocabulario de la API concreta.

**`WhatsAppGateway`, `EmailGateway`, `SMSGateway` (existentes o de terceros - adaptees):**
Son clases externas cuya interfaz no se controla ni se modifica. El patron Adapter es la herramienta para trabajar con APIs de terceros sin acoplar el dominio a ellas.

**`Agenda` (contexto de uso):**
Sigue usando `ServicioNotificacion` para notificaciones. Con el patron aplicado, `Agenda` no necesita cambiar cuando se incorpora un nuevo canal: basta con crear un nuevo adapter e inyectarlo en `ServicioNotificacion`.

### Explicacion del flujo estructural

`Agenda` delega en `ServicioNotificacion` las operaciones de notificacion. `ServicioNotificacion` no conoce proveedores concretos: itera sobre una lista de `INotificadorCanal` y ejecuta operaciones del contrato comun. Cada adapter traduce esa llamada a su API externa (adaptee), resolviendo la incompatibilidad de interfaces entre cliente de dominio y servicios de infraestructura.

## Relacion con los principios SOLID del proyecto

| Principio | Impacto del patron Adapter |
|-----------|---------------------------|
| **SRP** | Cada adapter tiene una unica responsabilidad: traducir un proveedor. `ServicioNotificacion` tiene una sola responsabilidad: orquestar canales. Ya no mezcla logica de WhatsApp con la de otros canales |
| **OCP** | Para agregar un canal nuevo (ej. notificacion push) basta con crear `AdaptadorPush` que implemente `INotificadorCanal` e inyectarlo. Ni `ServicioNotificacion` ni `Agenda` se modifican |
| **LSP** | Cualquier `INotificadorCanal` puede reemplazar a otro en `ServicioNotificacion` sin alterar el comportamiento esperado. El contrato del target se respeta en todos los adapters |
| **DIP** | `Agenda` depende de `ServicioNotificacion`; esta depende de `INotificadorCanal`, una abstraccion. Ninguna clase del dominio depende de `WhatsAppGateway`, `EmailGateway` ni `SMSGateway` |
