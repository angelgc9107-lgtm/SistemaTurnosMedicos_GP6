# Uso de Copilot Agent Mode - Diseñador de Tarjetas CRC

## Prompt utilizado
Se solicitó a Copilot analizar los archivos anexos/introduccion.md y el diagrama de clases en Excalidraw para identificar las clases principales del sistema y generar tarjetas CRC incluyendo nombre, superclase, responsabilidades, colaboraciones, pensamiento del objeto y propiedades.

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw

## Ajustes realizados
- Se corrigieron responsabilidades de la clase Turno para alinearlas con los requisitos funcionales (cancelar, reprogramar, registrar).
- Se reemplazó la clase Notificación por Recepcionista para representar correctamente al actor administrativo del sistema.
- Se ajustaron las colaboraciones entre Paciente, Médico y Agenda.
- Se agregaron propiedades relevantes a cada clase.
- Se adaptó el formato de salida a la plantilla de tarjetas CRC en markdown requerida.