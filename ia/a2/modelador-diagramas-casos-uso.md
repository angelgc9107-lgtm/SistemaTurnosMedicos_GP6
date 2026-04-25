# Copilot Agent Mode - Modelador de Diagramas de Casos de Uso
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de casos de uso.

## Prompt utilizado
```
 - 1 Prompt: Leer el archivo anexo/introduccion.md para tener como contexto
 - 2 Prompt: Generar un código de PlantUML para cada caso de uso
 - 3 Necesito minimo 5 diagramas que tengan lo siguiente: Actores principales, Casos de uso con relaciones adecuadas (inclusiones o extensiones)
 - 4 el cu1 los actores serian la secretaria y el paciente
 - 5 el paciente solicita el turno, debe tener una interacción con agendar el turno
 - Necesito que analices el archivo introducción.md el caso 6. cancelar turno y hagas con lenguaje Plantuml un archivo puml de ese caso de uso en la carpeta 02-casos-de-uso llamado "02-cancelar-turno-06.puml"
 ```

## Archivos utilizados como contexto
- anexos/introduccion.md

## Ajustes realizados
- CU1  Actores: Agregar al Paciente como actor (antes solo estaba la Secretaria y Sistema WhatsApp)

- CU1  Relaciones de actores: Reorganizar las interacciones:
La Secretaria inicia Agendar Turno y Agendar como sobreturno (todas las acciones de gestión quedan de su lado)
El Paciente solicita el turno con una interacción directa hacia Agendar Turno (con etiqueta "solicita turno")
El Sistema WhatsApp envía la notificación al Paciente (WA --> PAC)
- CU6 Se agrego el CU6 el puml y el archivo png.

## Interacciones

### Iteración 1: Creación de Diagramas de casos de uso
- **Prompt usado:**
```
Leer el archivo anexo/introduccion.md para tener como contexto
En base a ese contexto generar 5 archivos puml con cada caso de uso registrado.
```
**Respuesta:** Genero los 5 diagramas de casos de uso.

### Iteración 2: Corrección a diagrama CU1
- **Prompt usado:**
```
el cu1 los actores serian la secretaria y el paciente
```
**Respuesta:** Genero el archivo con la corrección solicitada.

### Iteración 3: Corrección a diagrama CU1 — 2
- **Prompt usado:**
```
El Paciente solicita el turno con una interacción directa hacia Agendar Turno (con etiqueta "solicita turno")
El Sistema WhatsApp envía la notificación al Paciente (WA --> PAC)
```
**Respuesta:** Genero el archivo con las correcciones solicitada.

### Iteración 6: Generación de archivo puml CU6
- **Prompt usado:**
```
Leer en el archivo anexo/introduccion.md el caso de uso "6. Cancelar turno" para tomar como contexto, en base a eso generar un archivo puml con el nombre "02-cancelar-turno-06"
```
**Respuesta:** Generó el caso de uso N° 6.

