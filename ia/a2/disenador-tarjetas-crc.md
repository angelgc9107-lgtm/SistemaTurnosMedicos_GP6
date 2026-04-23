# Uso de Copilot Agent Mode - Diseñador de Tarjetas CRC

## Prompt utilizado
```
Se solicitó a Copilot analizar los archivos anexos/introduccion.md y el diagrama de clases en Excalidraw para identificar las clases principales del sistema y generar tarjetas CRC incluyendo nombre, superclase, responsabilidades, colaboraciones, pensamiento del objeto y propiedades.
```

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw

## Ajustes realizados
- Se corrigieron responsabilidades de la clase Turno para alinearlas con los requisitos funcionales (cancelar, reprogramar, registrar).
- Se reemplazó la clase Notificación por Recepcionista para representar correctamente al actor administrativo del sistema.
- Se ajustaron las colaboraciones entre Paciente, Médico y Agenda.
- Se agregaron propiedades relevantes a cada clase.
- Se adaptó el formato de salida a la plantilla de tarjetas CRC en markdown requerida.

## Iteraciones

### Iteración 1: Generación inicial de tarjetas CRC
- **Prompt usado:**
  ```
  Analiza los archivos introduccion.md y el diagrama Excalidraw para identificar clases principales y generar tarjetas CRC con nombre, superclase, responsabilidades, colaboraciones, pensamiento del objeto y propiedades.
  ```
- **Respuesta de Copilot:** Generó tarjetas básicas para Paciente, Médico, Turno, Agenda y Notificación.
- **Observaciones:** Las tarjetas iniciales no cubrían completamente los requisitos funcionales, especialmente en Turno.

### Iteración 2: Corrección de responsabilidades y reemplazo de clase
- **Prompt usado:**
  ```
  Corrige las responsabilidades de la clase Turno para incluir cancelar, reprogramar y registrar. Reemplaza la clase Notificación por Recepcionista para representar al actor administrativo.
  ```
- **Respuesta de Copilot:** Actualizó las responsabilidades de Turno y cambió Notificación por Recepcionista.
- **Observaciones:** Mejoró la alineación con los casos de uso del sistema.

### Iteración 3: Ajustes finales de colaboraciones, propiedades y formato
- **Prompt usado:**
  ```
  Ajusta las colaboraciones entre Paciente, Médico y Agenda. Agrega propiedades relevantes a cada clase y adapta el formato a markdown.
  ```
- **Respuesta de Copilot:** Refinó colaboraciones, agregó propiedades como fecha, hora y estado, y formateó en markdown.
- **Observaciones:** El resultado final cumple con la plantilla requerida y los requisitos del proyecto.