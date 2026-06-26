# Uso de Copilot Agent Mode - Especialista en Patrón de Diseño Estructural
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de clases

## Prompt utilizado
```
Necesito que tengas como contexto los archivos adjuntos y hagas lo siguiente.

Identificar un problema específico dentro de la gestión del sistema de turnos médicos.
Seleccionar un patrón de diseño estructural GoF que ayude a resolver ese problema. El patrón debe ser adecuado para el contexto del sistema.
Implementar el patrón seleccionado en un diagrama de clases UML usando PlantUML.
El diagrama debe incluir:
Las clases actuales implicadas en el problema.
Las nuevas clases o interfaces necesarias para aplicar el patrón.
Las relaciones entre clases.
La lógica general de cómo se comunican las clases.
Estereotipos o notas que ayuden a entender el patrón aplicado.
Crear o completar el archivo patron-de-diseno-estructural.md explicando:
Propósito y Tipo del Patrón
Qué son los patrones de diseño estructurales GoF.
Cómo se relacionan con los principios SOLID.
Qué problema específico existe en el sistema de turnos médicos.
Cómo el patrón seleccionado soluciona ese problema.
Motivación
Explicar con más detalle el problema que tenía el sistema.
Describir por qué ese problema afecta el diseño del sistema.
Explicar cómo el patrón elegido mejora la solución.
Detallar las clases que ya existían y estaban implicadas en el problema.
Detallar las nuevas clases o interfaces incorporadas por el patrón.
Explicar la función de cada clase dentro de la solución.

El resultado debe incluir:

El contenido completo para el archivo patron-de-diseno-estructural.md.
El código completo PlantUML del diagrama de clases.
Una explicación breve de por qué el patrón elegido es correcto para este caso.
```

## Archivos utilizados como contexto
- 06-clases-diagrama-final.puml
- 01-solid-01-srp-01.puml
- 01-solid-01-srp-02.puml
- 01-solid-01-srp-03.puml
- 01-solid-01-srp-04.puml
- 01-solid-04-isp.puml
- 01-solid-02-ocp.puml
- 01-solid-03-lsp.puml
- 01-solid-05-dip.puml

## Ajustes realizados
- Se modifico una los problemas encontrados del sistema del archivo patron-de-diseno-estructural.md
- Se modifico una explicación del patrón "Adapter" ambigua y podia generar incoherencias
- Modificación en el archivo 01-patron-estructural-adapter.puml para que coincida con las modificaciones realizadas en el archivo patron-de-diseno-estructural.md.
- Se modifico la ubicación de la nota en el archivo puml.


### interaciones 1
**Prompt usado:**
```
Verificar si lo propuesto en el archivo patron-diseño-estructural es un adapter o esta detallando otro patrón, ejemplo strategy.
```
**Respuesta de Copilot:**
Lo que describe el documento es Adapter. La confusión con Strategy es comprensible porque ambos patrones usan una interfaz con múltiples implementaciones.

### interaciones 2
**Prompt usado:**
```
Modificar esa parte para dejar explicito que el foco de esta en el patrón adapter.
```
**Respuesta de Copilot:**
Voy a hacer una edición puntual en esa sección para que quede explícito: la lista de canales existe para adaptar APIs incompatibles (Target/Adapter/Adaptee)

### interaciones 3
**Prompt usado:**
```
Verificar que el uml coincida con lo propuesto en el archivo patron-de-diseno-estructural
```
**Respuesta de Copilot:**
Sí, el UML coincide con lo propuesto en el documento, en términos generales.
En el texto se enfatiza “lista de adapters”; en el UML el atributo se llama “canales”. Es compatible conceptualmente, pero si quieres máxima alineación semántica puedes renombrar el atributo a algo como listaAdaptadores.

### interaciones 4
**Prompt usado:**
```
Modificarlo para que coincida con lo informado en el archivo patrones de estructura y no generar incoherencias.
```
**Respuesta de Copilot:**
Listo, ya lo modifiqué para que el UML coincida con el texto y mantenga el foco en Adapter.
Cambios aplicados en patron-adapter-notificacion.puml:
En ServicioNotificacion:
canales → adaptadores
agregarCanal(canal: INotificadorCanal) → agregarAdaptador(adaptador: INotificadorCanal)
En la nota del Client:
“lista de canales” → “lista de adaptadores”
“agregar un canal nuevo” → “agregar un adaptador nuevo”
En la relación:
ServicioNotificacion o-- INotificadorCanal : canales > → ... : adaptadores >
Con eso, el diagrama queda alineado semánticamente con lo documentado en patron-de-diseno-estructural.md.

### interaciones 5
**Prompt usado:**
```
Mover la posición de la nota note right of ServicioNotificacion para que se pueda visualizar mejor, quedo entre cortada
```
**Respuesta de Copilot:**
Listo. Se modifico la posición de la nota.
