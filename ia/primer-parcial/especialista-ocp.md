# Uso de Copilot Agent Mode - Especialista en Principios de Extensión

- **Prompt usado:**

"Actúa como un Arquitecto de Software experto en Programación Orientada a Objetos y Principios SOLID. Necesito que realices un análisis de diseño sobre un Sistema de Gestión de Turnos Médicos utilizando los siguientes archivos como contexto:

Introducción y Dominio: anexos/introduccion.md

Estructura Visual: diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw

Responsabilidades: Todas las tarjetas en herramientas-agile/tarjetas-crc/

**Tu misión es:**

Identificar Violaciones al SRP: Detecta qué clases tienen múltiples responsabilidades (por ejemplo, si una entidad de dominio como Paciente también gestiona la persistencia, validaciones complejas o lógica de visualización).

Diagnóstico de Mantenibilidad: Para cada caso identificado, explica qué problemas genera (ej: acoplamiento excesivo, dificultad para realizar pruebas unitarias o riesgo de efectos secundarios al modificar el código).

Propuesta de Descomposición: Propón una nueva estructura donde cada clase tenga una única razón para cambiar. Indica claramente qué métodos o atributos deberían moverse a nuevas clases o servicios (ej: clases de validación, repositorios para persistencia o gestores de agenda).

Control de Coherencia de Dominio: Asegurate de que la solución sea realista para el flujo de un centro médico, respetando la lógica entre Médicos, Especialidades, Turnos y Pacientes.

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- herramientas-agile/tarjetas-crc
