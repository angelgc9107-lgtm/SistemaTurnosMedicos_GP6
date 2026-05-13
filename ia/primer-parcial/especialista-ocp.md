# Uso de Copilot Agent Mode - Especialista en Principios de Extensión

- **Prompt usado:**

```
Actúa como Senior Software Engineer especializado en Open/Closed Principle (OCP).

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
- Conclusiones verificables sobre escalabilidad.
```

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- herramientas-agile/tarjetas-crc

## Ajustes Realizados

**Ajuste 1:** Identificación de condicionales por tipo de turno en la clase `Turno`

- La IA identificó que la clase `Turno` concentraba la lógica de `calcularDuracion()` con condicionales `if/switch` según el tipo de turno (`PRIMERA_VEZ`, `CONTROL`, `CONSULTA`).
- Esto viola OCP: agregar un nuevo tipo de turno requería modificar la clase existente.
- Decisión tomada: extraer subclases `TurnoConsulta`, `TurnoPrimeraVez` y `TurnoControl`, cada una con su propia implementación de `calcularDuracion()`, permitiendo extensión sin modificar `Turno`.

**Ajuste 2:** Identificación del sistema de notificaciones cerrado a extensión

- La IA detectó que el sistema notificaba solo por un canal fijo, sin abstracción.
- Decisión tomada: proponer una interfaz `Notificador` con implementaciones independientes por canal, que `Turno` reciba por inyección de dependencias.

## Iteraciones

### Iteración 1: Identificación de Oportunidades Perdidas

**Prompt enviado a Copilot:**

"Analiza las tarjetas CRC y el boceto inicial. Para CADA clase, identifica:
1. ¿Usa condicionales (if/switch) para diferenciar comportamiento según tipo?
2. Si agregar un nuevo tipo de turno requiere modificar esa clase, márcala como VIOLACIÓN OCP.
3. Lista extensiones futuras probables (nuevos tipos de turno, nuevos notificadores) y verifica si el diseño actual las soporta sin modificar código existente."

**Salida obtenida de Copilot:**

```
VIOLACIÓN OCP — Clase: Turno
→ calcularDuracion() diferencia por tipo con condicional implícito
→ Agregar TurnoEmergencia requeriría modificar Turno
→ Punto de fragilidad: lógica de duración acoplada al tipo

OPORTUNIDAD PERDIDA — Notificaciones
→ No hay abstracción de canal de notificación
→ Cambiar de WhatsApp a Email requeriría modificar la clase que notifica
→ Solución: interfaz Notificador con implementaciones por canal

CLASES SIN VIOLACIÓN OCP en diseño actual:
→ Paciente, Medico, Secretaria, Agenda: no presentan condicionales por tipo
```

**Decisión tomada:** Se aceptó la propuesta de subclases para `Turno`. Se descartó implementar `Notificador` en este parcial por estar fuera del alcance del diagrama de clases entregado.

### Iteración 2: Propuesta de Arquitectura Extensible

**Prompt enviado a Copilot:**

"Para la violación OCP identificada en Turno, propone la arquitectura extensible:
1. Define la clase abstracta con el método abstracto
2. Define las subclases con sus implementaciones concretas
3. Muestra cómo agregar TurnoEmergencia sin modificar código existente"

**Salida obtenida de Copilot:**

```
abstract class Turno {
  - fecha, hora, estado
  + abstract calcularDuracion(): int
}

class TurnoConsulta extends Turno {
  + calcularDuracion(): 30  // minutos
}
class TurnoPrimeraVez extends Turno {
  + calcularDuracion(): 30
}
class TurnoControl extends Turno {
  + calcularDuracion(): 15
}

// EXTENSIÓN FUTURA — sin modificar Turno:
class TurnoEmergencia extends Turno {
  + calcularDuracion(): 60
}
```

**Decisión tomada:** Se adoptó este diseño directamente en el diagrama de clases OCP del proyecto.
