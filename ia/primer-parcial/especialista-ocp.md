# Uso de Copilot Agent Mode - Especialista en Principios de Extensión

- **Prompt usado:**

"Actúa como Senior Software Engineer especializado en Open/Closed Principle (OCP).

Analiza los archivos proporcionados como contexto y realiza un análisis exhaustivo 
de las clases identificadas, enfocándote en:

1. VIOLACIONES DE OCP (Open/Closed Principle)
   → Identifica clases CERRADAS PARA EXTENSIÓN (no permiten nuevas comportamientos)
   → Identifica clases ABIERTAS A MODIFICACIÓN (requieren cambio en código existente)
   → Explica qué problema de escalabilidad genera cada caso
   
2. OPORTUNIDADES DE EXTENSIÓN SIN MODIFICACIÓN
   → Analiza requisitos futuros potenciales (nuevos tipos de turnos, notificadores, etc.)
   → Verifica si el diseño actual soportaría esos cambios sin modificar clases existentes
   
3. PROPUESTAS DE ARQUITECTURA EXTENSIBLE
   → Propón abstracciones (interfaces, clases abstractas) para permitir extensión
   → Diseña estrategia de inyección de dependencias
   → Sugiere patrones de diseño (Strategy, Factory, Template Method, etc.)
   
4. IMPACTO EN ESCALABILIDAD Y MANTENIMIENTO
   → Explica qué cambios futuros (más probables) requieren modificación en código actual
   → Estima esfuerzo de agregar nuevas funcionalidades
   → Identifica "puntos de fragilidad" donde el código es frágil a cambios

FORMATO REQUERIDO:
- Estructura clara con secciones: PROBLEMA | OPORTUNIDAD PERDIDA | PROPUESTA
- Ejemplos de código concretos (pseudocódigo o Java)
- Diagramas de abstracción (ASCII o descripción textual)
- Escenarios de extensión futura simulados
- Conclusiones verificables sobre escalabilidad"

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- herramientas-agile/tarjetas-crc

## Ajustes Realizados

Ajuste: Analizar condicionales en clase Turno

Problema potencial: ¿Turno usa if/switch para diferentes tipos de turno?
Violación OCP: Si agregar nuevo tipo de turno requiere modificar Turno
Solicitud: Identificar dónde habría condicionales por tipo de turno (PRIMERA_VEZ vs. CONTROL vs. ?)


## Iteraciones

Iteración 1: Identificación de Oportunidades Perdidas
Salida esperada:

✅ Lista de extensiones futuras probables (nuevos notificadores, tipos de turno, etc.)
✅ Identificación de clases que NO están preparadas para esas extensiones
✅ Puntos específicos donde código se vería "quebrado" al agregar funcionalidad
✅ Análisis de patrón: ¿hay condicionales (if/switch) que indican violación OCP?