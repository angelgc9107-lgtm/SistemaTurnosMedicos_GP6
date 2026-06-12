# Uso de Copilot Agent Mode - Analista Funcional de Casos de Uso 2 y 3 
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de clases

## Prompt utilizado
```
Tienes el rol de un experto en diagramas de clases
Debes crear 2 diagramas de clases por cada uno de los casos de uso que analizas, los diagramas siempre deben tener los siguientes puntos en cuenta, los casos analizados son los casos de uso y diagramas de (registrar check in & reprogramar turnos)
- Diseñar diagramas de clases específicos para cada caso de uso utilizando PlantUML.  
- Asegurar coherencia entre requisitos funcionales, escenarios, diagramas de actividades, diagramas de secuencia y tarjetas CRC previamente desarrolladas. 

Al generar cada diagrama de clases tomaras como contexto estos archivos: 
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- introduccion.md
-02-registrar-checkin-02.puml
-02-registrar-checkin-02.png
-02-reprogramar-turno-03.png
-02-reprogramar-turno-03.puml
-03-registrar-checkin-flujo-principal.md
-03-reprogramar-turno-flujo-principal.md
-04-actividad-registrar-checkin-02.png
-04-actividad-registrar-checkin-02.puml
-04-actividad-reprogramar-turno-03.puml
-04-actividad-reprogramar-turno-03.png
-05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.puml
-05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.png
- herramientas-agile/tarjetas-crc/

Debes crear 2 diagramas de clases por cada uno de los casos de uso que analizas, los diagramas siempre deben tener los siguientes puntos en cuenta:

Desarrollar los diagramas de clases siguiendo los requisitos mínimos:
 ○ Nombre de clases 
○ Atributos con tipos de datos 
○ Métodos con parámetros y tipo de retorno
 ○ Relaciones UML correctas (asociación, agregación, composición, dependencia y herencia)
 ○ Coherencia con tarjetas CRC y diagramas de secuencia (nombres de métodos y atributos) 
● Crear archivos .puml con nomenclatura secuencial (04-clases-nombre-caso-uso-04.puml, etc.) en la carpeta diagramas/01-diagrama-clases/
```
```
Redactar un pseudocódigo que muestre cómo las clases diseñadas colaboran para los casos de uso registrar checkin & reprogramar turno
El pseudocódigo debe:
● Instanciar los objetos necesarios con sus parámetros
● Invocar los métodos relevantes en el orden correcto, indicando argumentos y
valores de retorno
● Reflejar el flujo principal del caso de uso tal como está modelado en el
diagrama de actividades y el diagrama de secuencia
● No usar sintaxis de ningún lenguaje de programación particular: debe ser
legible para cualquier persona con conocimientos básicos de programación
orientada a objetos
El objetivo del pseudocódigo es mostrar cómo el diagrama de clases cobra vida en la
resolución concreta del problema.
```

## Archivos utilizados como contexto
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- introduccion.md
- 02-registrar-checkin-02.puml
- 02-registrar-checkin-02.png
- 02-reprogramar-turno-03.png
- 02-reprogramar-turno-03.puml
- 03-registrar-checkin-flujo-principal.md
- 03-reprogramar-turno-flujo-principal.md
- 04-actividad-registrar-checkin-02.png
- 04-actividad-registrar-checkin-02.puml
- 04-actividad-reprogramar-turno-03.puml
- 04-actividad-reprogramar-turno-03.png
- 05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.puml
- 05-secuencia-cu-registrar-checkin-registrar-checkin-flujo-principal-02.png
- herramientas-agile/tarjetas-crc/

## Ajustes realizados
- En el diagrama de clases de caso de uso 3 eliminar "HistorialTurno.getHistorial()"
- En el diagrama de clases de caso de uso 2 se agrego al comentario al lado de "ControlSistema" una referencia a la RNF5
- Corrección a la cardinalidad en LlegadaPaciente en el diagrama de clases de uso 2
- Se realizo una modificación para que el pseudocódigo coincida con el template propuesto del caso de uso 2 & 3
- Se agrego la clase abstracta persona en el archivo del diagrama de clase del caso de uso Registrar checkin.
- Se agrego la clase abstracta persona en el archivo del diagrama de clase del caso de uso Reprogramar Turno.


### interaciones 1
**Prompt usado:**
```
Verificar si los diagramas creados respetan lo siguiente, en caso de encontrar errores ofrecer solución
Los nombres de clases, atributos y métodos deben coincidir con:
- Las tarjetas CRC de A2 (responsabilidades y colaboraciones)
- Los participantes y mensajes del diagrama de secuencia de A3
No podés introducir métodos o atributos que no se desprendan de los artefactos anteriores.
```
**Respuesta de Copilot:**
---
**Diagrama de clase caso de uso 2**
---
Diagrama 2 (cu02-registrar-checkin-01.puml) no requirió cambios — todos sus métodos y atributos se derivan directamente del diagrama de secuencia CU-02 y las tarjetas CRC correspondientes
---
**Diagrama de clase caso de uso 3**
---
| Elemento | Problema | Corrección |
| ---- | ---- | ---- |
|HistorialTurno.getHistorial()  | No aparece en el diagrama de secuencia CU-03 (solo se llama registrarCambio())  | Eliminar  |

### interaciones 2
**Prompt usado:**
```
En el diagrama de clase 04-clase-registrar-checkin.puml agregar al comentario al lado del controlsistemas una referencia al RNF5
```
**Respuesta de Copilot:**
 Ahora la nota refleja fielmente RNF5 — ControlSistema lo respeta delegando en Agenda, que es quien debe ser el único componente en controlar la gestión de turnos.

 ### interaciones 3
**Prompt usado:**
```
verificar si la cardinalidad esta correcta en el diagrama de clase 04-clase-registrar-checkin.puml
```
**Respuesta de Copilot:**
El problema es que LlegadaPaciente --> Turno: la cardinalidad "0..1" del lado de LlegadaPaciente es semánticamente crítica — expresa que un Turno solo tiene LlegadaPaciente si el paciente efectivamente se presentó. Lo corrijo:

### interaciones 4
**Prompt usado:**
```
Verificar la cardinalidad en el diagrama de clases 04-clase-reprogramar-turno.puml
```
**Respuesta de Copilot:**
ControlSistema "1" --> "1" Agenda — agregada cardinalidad. Un único ControlSistema delega en una única Agenda (coherente con RNF5).

ServicioNotificacion ..> Turno eliminada — en el diagrama de secuencia, svcNotificacion solo recibe parámetros primitivos (telefono, nuevaFecha, nuevaHora, nombreMedico). Nunca recibe ni referencia un objeto Turno, por lo que la relación no se desprende de ningún artefacto previo.

### interaciones 5
**Prompt usado:**
```
verificar si la relación entre ServicioNotificación y Agenda es correcta, en caso de encontrar un error dar sugerencias de como solucionarlo
```

**Respuesta de Copilot:**
La relación es correcta en tipo y dirección — Agenda crea y destruye ServicioNotificacion dentro de una sola operación, por lo que una dependencia ..> es la relación UML apropiada (no asociación ni agregación, ya que no hay referencia persistente).

El único problema es la etiqueta: <<crea y usa>> es informal. El diagrama de secuencia usa el estereotipo estándar UML <<create>>, que es la notación correcta para expresar que Agenda instancia

### interaciones 6
**Prompt usado:**
```
El pseudocódigo debe seguir el flujo principal de la sección 1 y los mensajes del diagrama de secuencia. No uses sintaxis de ningún lenguaje particular. Usá los mismos nombres de clases y métodos que aparecen en el diagrama de clases: nada inventado. Cada comentario debe explicar QUÉ está pasando en términos del dominio, no describir el código. El objetivo es que alguien pueda leer solo el pseudocódigo y entender cómo se resuelve el caso de uso. Si el flujo no se entiende sin ver el diagrama, agregá más comentarios
INICIO [Nombre del Caso de Uso]

// [Contexto: qué condición disparó este caso de uso y quién lo inicia]

[NombreClase] objeto1 = nuevo [NombreClase](parametro1, parametro2)
[NombreClase] objeto2 = nuevo [NombreClase](parametro1)

// [Qué está resolviendo este bloque en términos del dominio]
resultado = objeto1.metodo(argumento)

// [Qué decisión se toma y por qué]
SI resultado es válido
    objeto2.metodo(resultado)
    // [Qué produce esta acción en el sistema]
SINO
    // [Qué flujo alternativo se activa]
FIN SI

// [Estado final del sistema tras ejecutar el caso de uso]
Retornar [resultado final]

FIN

```
**Respuesta de Copilot:**
El pseudocódigo tiene buena lógica pero no sigue la estructura del template. Las diferencias son:

Variables no tienen tipo declarado — el template usa [NombreClase] variable = nuevo ...
SI NO en lugar de SINO — el template usa SINO
Falta Retornar [resultado final] al cierre de cada CU
Instanciaciones sin tipo (llegada = nuevo LlegadaPaciente(...) → LlegadaPaciente llegada = nuevo LlegadaPaciente(...))
Edited
pseudocodigo-cu02-cu03.md+30-21
Pseudocódigo actualizado para cumplir exactamente el template. Los cambios aplicados:

Aspecto	Antes	Después
Declaración de variables	turnoEncontrado = ...	Turno turnoEncontrado = ...
Listas tipadas	listaTurnos = ...	List<Turno> listaTurnos = ...
Booleanos tipados	disponible = ...	boolean disponible = ...
Tipos primitivos	horaLlegada = ...	Time horaLlegada = ...
Instanciaciones	llegada = nuevo LlegadaPaciente(...)	LlegadaPaciente llegada = nuevo LlegadaPaciente(...)
Rama negativa	SI NO condicion ... FIN SI	SI condicion ... SINO ... FIN SI
Cierre	sin Retornar	Retornar "..." antes de FIN

### interaciones 7
```
En el archivo 02-clase-registrar-checkin.puml debes agregar la superclase de secretaria.
```
**Respuesta de Copilot:**
Listo. Se agregó la clase abstracta Persona con sus atributos estándar (dni, nombre, apellido, telefono, email, rol, estadoActivo) y la relación de herencia Persona <|-- Secretaria, consistente con el resto de los diagramas del proyecto (como 01-clases-agendar-turno-01.puml).

### interaciones 8
```
En el archivo 03-clase-reprogramar-turno.puml debes agregar la superclase de secretaria.
```
**Respuesta de Copilot:**
Listo. Se agregó la clase abstracta Persona con sus atributos estándar y la relación Persona <|-- Secretaria, consistente con el resto de los diagramas del proyecto