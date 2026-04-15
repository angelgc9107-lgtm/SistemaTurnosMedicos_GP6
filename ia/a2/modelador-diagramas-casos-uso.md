# Copilot Agent Mode - Modelador de Diagramas de Casos de Uso
Se utilizó Copilot para la creación y corrección de los archivos puml de los diagramas de casos de uso.

## Prompt utilizado
- 1 Prompt:Leer el archivo anexo/introduccion.md para tener como contexto
- 2 Prompt:Generar un código de PlantUML para cada caso de uso
- 3 Necesito minimo 5 diagramas que tengan lo siguiente:
○ Actores principales
○ Casos de uso con relaciones adecuadas (inclusiones o extensiones).
- 4 el cu1 los actores serian la secretaria y el paciente
- 5 el paciente solicita el turno, debe tener una interacción con agendar el turno

## Archivos utilizados como contexto
- anexos/introduccion.md

## Ajustes realizados
CU1 - Actores: Agregar al Paciente como actor (antes solo estaba la Secretaria y Sistema WhatsApp)

CU1 - Relaciones de actores: Reorganizar las interacciones:

La Secretaria inicia Agendar Turno y Agendar como sobreturno (todas las acciones de gestión quedan de su lado)
El Paciente solicita el turno con una interacción directa hacia Agendar Turno (con etiqueta "solicita turno")
El Sistema WhatsApp envía la notificación al Paciente (WA --> PAC)