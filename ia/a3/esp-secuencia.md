# Copilot Agent Mode - Especialista en diagramas de secuencia
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de secuencia

## Prompt utilizado
```
tu rol es de un especialista en diagramas de secuencia
Toma como contexto todos los archivos de 03-escenarios-de-casos-de-uso y tarjetas-crc para crear 5 diagramas de secuencia, para cada diagramas debes tener un mínimo de cuatro participantes y tres mensajes.
Utiliza PlantUML para generar los diagramas para que estos sean profesionales.
Ten en cuenta de utilizar la correcta notación del lenguaje UML y el naming en camelCase para recibir los argumentos. Recuerda hacer el simbolo de "Final de vida"  de los objetos que dejan de existir en la interacción modelada
Estos diagramas los debes crear dentro de la carpeta "05-diagramas-secuencia"
```
## Archivos utilizados como contexto
- 03-escenarios-de-casos-de-uso/
- tarjetas-crc/

## Ajustes realizados
- 05-cu01-agendar-turno: Se agregó "sistema" dentro del diagrama 05-cu01-agendar-turno para interactuar directamente con secretaria
-05-cu02-registrar-checkin: Se quito una note dentro del diagrama 05-cu02-registrar-checkin y se agrego sistema para que interactue directamente con la secretaria
- 05-cu03-reprogramar-turno: Se agregó "sistema" dentro del diagrama 05-cu03-reprogramar-turno para interactuar directamente con secretaria
- 05-cu04-bloquear-horarios: Se elimino el actor médico que interactuaba directamente con el actor secretaria y se pidio agregar una note para indicar el mensaje externo que inicia la interacción de la secretaria con el sistema.
- 05-cu04-bloquear-horarios: Se pidio sacar el "alt" dentro del diagrama 05-cu04-bloquear-horarios, el diagrama es el modelado del caso de flujo exitoso.
- 05-cu05-visualizar-agenda: Se agrego "sistema" dentro del diagrama 05-cu05-visualizar-agenda para interactuar directamente con secretaria
- 05-cu05-visualizar-agenda: Se pidio quitar los objetos bloque horarios y turnos del diagrama 05-cu05-visualizar-agenda.
- Se verifico que los mensajes de los 5 diagramas de secuencia correspondan a las clases dentro de tarjeta-crc/
- Se agrego una tarjeta crc "servicio-notificacion" ya que estaba mencionada en el escenario de casos de uso y era necesario de representarlo en los diagramas de secuencia.


### interaciones 1
- **Prompt usado:**
```
Analiza el contexto que tenes y agrega a "sistema" que es el objeto que solicita los datos del paciente a secretaria, la agenda solo controla y administra los turnos guardados en el diagrama "05-cu01-agendar-turno.puml"
```
- **Respuesta de Copilot:**
Actualizado. El diagrama ahora tiene 5 participantes con responsabilidades bien separadas:

Objeto	Rol
:Secretaria	Actor humano que interactúa con la UI
:Sistema	Capa de presentación — solicita datos, muestra pantallas, recibe input
:Agenda	Dominio — verifica disponibilidad, valida restricciones, registra y bloquea turnos
:Turno	Entidad creada por Agenda, establece su estado
:ServicioNotificacion	Servicio transiente que envía WhatsApp y programa recordatorios, luego se destruye

### interacion 2:
- **Prompt usado:**
```
¿Los mensajes corresponden a los atributos de los actores?
Verificalo
 ```
- **Respuesta de Copilot:**
Análisis completo. Hay 3 tipos de inconsistencias entre los diagramas y las tarjetas CRC:

❌ Atributos incorrectos o inexistentes
Diagrama	Mensaje / Parámetro	Problema	CRC correcto
CU-01, CU-03	idMedico	Médico no tiene idMedico	matricula (CRC Medico)
CU-02	numeroTurno	Turno no tiene numeroTurno	Propiedades de Turno: fecha, hora, estado, tipoConsulta
CU-05	idUsuario	Persona no tiene idUsuario	dni (CRC Persona)
❌ Responsabilidad ejercida por el objeto incorrecto
Diagrama	Mensaje en diagrama	Problema	Según CRC
CU-02	agenda → medico: notificarPacienteEnSala(...)	Agenda no tiene responsabilidad de notificar al médico	CRC de LlegadaPaciente: "Notificar al médico" (colaboradores: Médico, Secretaria) → debe ser llegadaPaciente → medico
Además, los atributos presente y estadoPresencia de LlegadaPaciente existen en la CRC pero no aparecen en ningún mensaje del CU-02.

⚠️ Clases sin tarjeta CRC (creadas sin respaldo en el modelo)
Clase	Aparece en	Observación
HistorialCambio	CU-03	No tiene CRC; requerido por RNF4 pero no modelado en el dominio
ValidadorConflictos	CU-04	No tiene CRC; lógica que podría pertenecer a Agenda
BloqueHorario	CU-04, CU-05	No tiene CRC; podría ser manejado directamente por Agenda
VistaCalendario	CU-05	No tiene CRC; es un objeto de presentación
Querés que corrija los diagramas afectados? Los cambios concretos serían:

idMedico → matricula en CU-01 y CU-03
Mover notificarPacienteEnSala() de agenda a llegadaPaciente en CU-02, y usar presente/estadoPresencia
numeroTurno → eliminarlo en CU-02
idUsuario → dni en CU-05

### interacion 3
- **Prompt usado:**
```
Modifica los diagramas de secuencia para que correspondan con el contexto dado
 ```
- **Respuesta de Copilot:**
correcciones aplicadas. Resumen de lo cambiado en cada diagrama:

05-cu01-agendar-turno.puml
idMedico → matricula en 5 mensajes (consultarDisponibilidad, verificarDisponibilidad, obtenerHorariosDelDia, filtrarHorariosDisponibles, registrarTurno, new)
05-cu02-registrar-checkin.puml

llegadaPaciente ahora llama actualizarPresencia(presente, estadoPresencia) sobre sí mismo — usa los atributos presente y estadoPresencia de su CRC
llegadaPaciente → medico reemplaza a agenda → medico para notificarPacienteEnSala() — cumple la responsabilidad CRC "Notificar al médico"
nombre reemplaza a nombrePaciente, se elimina numeroTurno (no estaba en CRC de Turno)
llegadaPaciente se desactiva después de notificar al médico, no antes
05-cu03-reprogramar-turno.puml

idMedico → matricula en verificarDisponibilidad
05-cu05-visualizar-agenda.puml

idUsuario → dni y rolUsuario → rol (atributos de CRC Persona) en accederSeccionAgenda, verificarAccesoPorRol y new
idMedico → matricula en 4 mensajes de consulta a Turno y BloqueHorario

### interacion 4
- **Prompt usado:**
```
En el diagrama cu02-registrar-checkin quitar la note del paciente ya está presente, no es necesario mostrarlo.
 ```
- **Respuesta de Copilot:**
Listo. El note fue eliminado del 05-cu02-registrar-checkin.puml, el mensaje cancelarRecordatoriosPendientes(idTurno) queda igual.

### interacion 5
- **Prompt usado:**
```
En cu03-reprogramar-turno el mensaje sincronico de horarios disponibles para reprogramar el turno debe ser una interacción que inicia la secretaria con el sistema, es decir que primero lo inicia la secretaria
 ```
- **Respuesta de Copilot:**
Pequeño ajuste: añado el mensaje iniciador desde secretaria antes de que sistema consulte la disponibilidad.

### interacion 6
- **Prompt usado:**
```
En el cu04-bloquear-horarios se debe eliminar el actor medico y dejar una nota indicando de donde ingresa el mensaje
 ```
- **Respuesta de Copilot:**
Listo. Los dos cambios aplicados en 05-cu04-bloquear-horarios.puml:

Eliminado actor ":Medico" de los participantes
Eliminado el mensaje medico → secretaria
Agregada una note over secretaria que indica que el evento es externo al sistema (comunicación presencial del médico) antes del primer mensaje con el sistema

### interacion 7
- **Prompt usado:**
```
Quitar el objeto validador de conflictos y agregar sistemas, la secretaria interactua con sistemas
 ```
- **Respuesta de Copilot:**
Listo. Cambios aplicados en 05-cu04-bloquear-horarios.puml:

### interacion 8
- **Prompt usado:**
```
Eliminar el fragmento alt del diagrama de secuencia cu04-bloquear-horarios
 ```
- **Respuesta de Copilot:**
Hecho. Se eliminaron el fragmento alt/else/end, la verificación de conflictos y la rama alternativa. El diagrama ahora modela únicamente el flujo principal exitoso: la secretaria confirma → Agenda crea el BloqueHorario → el calendario lo refleja → confirmación a la secretaria

### interacion 9
- **Prompt usado:**
```
Agregar sistema dentro del diagrama cu05-visualizar-agenda
 ```
- **Respuesta de Copilot:**
Reescribo el diagrama completo añadiendo :Sistema con el patrón usuario ↔ sistema ↔ agenda en todos los pasos del escenario.

Edited
05-cu05-visualizar-agenda.puml+50-32
Listo. :Sistema agregado en 05-cu05-visualizar-agenda.puml.

### interacion 10
- **Prompt usado:**
```
En el diagrama cu05-visualizar-agenda, bloque horarios y turnos estan contenidos dentro de agenda. Son interacciones dentro de el mismo. En caso de ser así eliminarlo del diagrama.
 ```
- **Respuesta de Copilot:**
Correcto. Para CU-05 aplican dos razones para no mostrarlos:

Agenda ya los contiene: Agenda tiene - listaTurnos: List<Turno> y delega bloqueos a GestorBloqueos (donde Bloqueo es clase interna). Son datos que Agenda ya posee, no interacciones externas.

CU-05 es solo lectura: no se crean ni modifican Turno ni BloqueHorario. Agenda simplemente entrega sus colecciones ya existentes a VistaCalendario.

Mostrar agenda → turno : getEstado() implica que Agenda envía un mensaje a un objeto externo, cuando en realidad itera su propia lista interna. Quito ambos participantes y simplifico.

### interacion 11
- **Prompt usado:**
```
En usuario agregar una note indicando que puede ser Secretaria o Medico
 ```
- **Respuesta de Copilot:**
Listo. Se agregó la nota sobre :Usuario indicando que puede ser :Secretaria o :Medico (RF4).

### interacion 12
```
Necesito que tomes el rol de un experto en diagramas de secuencia.

Analises todos los diagramas puml que se encuentra dentro de la carpeta 05-diagramas-secuencia

Tenes que usar como contexto los archivos que se encuentran dentro de la carpetas tarjeta-crc y 03-escenarios-casos-de-uso

Decime si los diagramas de secuencia coinciden con el contexto de los archivos de escenearios de casos de uso y tarjetas crc
```
- **Respuesta de Copilot:**
3. Resumen de observaciones
#	Diagrama	Tipo	Descripción
1	CU-01	Datos faltantes	Falta sexo y edad en ingresarDatosPaciente()
2	CU-02	Estado incompleto	Estado destino debe ser "Presente o en sala de espera", no solo "Presente"
3	CU-03	Estado incompleto	No considera turno en estado "Presente" como válido para reprogramar
4	CU-03	Responsabilidad faltante	No hay mensaje explícito actualizando fecha/hora en el objeto Turno
5	CU-05	Flujo omitido	No se modela la vista diaria por defecto antes de seleccionar vista
6	Todos	CRC faltante	ServicioNotificacion, HistorialTurno, BloqueHorario, VistaCalendario no tienen tarjeta CRC

