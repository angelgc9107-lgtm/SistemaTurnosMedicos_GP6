# Uso de Copilot Agent Mode - Especialista en Principios de Extensión
- **Prompt usado:**

Actúa como Senior Software Engineer especializado en Principios SOLID.

Analiza los archivos proporcionados como contexto y realiza un análisis exhaustivo 
de las clases identificadas, enfocándote en:

1. VIOLACIONES DE SRP (Single Responsibility Principle)
   → Identifica clases con MÚLTIPLES RAZONES PARA CAMBIAR
   → Explica qué problema de mantenibilidad genera cada caso
   
2. VIOLACIONES DE LSP (Liskov Substitution Principle)
   → Verifica si subclases pueden sustituir superclases sin quebrar el programa
   → Identifica herencias incorrectas
   
3. PROPUESTAS DE DESCOMPOSICIÓN
   → Propón cómo separar responsabilidades
   → Valida coherencia con el dominio del Sistema de Turnos Médicos
   
4. IMPACTO EN MANTENIBILIDAD
   → Explica qué problemas causa cada violación
   → Estima esfuerzo de cambios futuros (antes vs. después refactoring)

FORMATO REQUERIDO:
- Estructura clara con secciones: PROBLEMA | IMPACTO | PROPUESTA
- Ejemplos de código concretos (pseudocódigo o Java)
- Diagramas UML (ASCII o descripción textual)
- Conclusiones verificables y medibles

## Archivos utilizados como contexto
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- herramientas-agile/tarjetas-crc


## AJUSTES REALIZADOS A SOLICITAR
Durante el análisis, Copilot debe:

**Ajuste 1:** Corregir responsabilidades ambiguas de la clase Turno

- Actual: Turno maneja: "Registrar turno", "Confirmar turno", "Cancelar turno", "Reprogramar turno"
- Problema: ¿Quién notifica al paciente? ¿Turno o servicio externo?
- Solicitud: Separar responsabilidad de notificación de Turno

**Ajuste 2:** Eliminar la relación de herencia INCORRECTA entre LlegadaPaciente y Turno

- Actual: LlegadaPaciente aparece como herencia de Turno
- Problema: LlegadaPaciente NO ES-UN Turno (violación LSP)
- Solicitud: Proponer composición en lugar de herencia

**Ajuste 3:** Aclarar colaboraciones de Paciente, Médico y Secretaria

- Actual: Las tarjetas muestran confusión en responsabilidades
- Problema: ¿Quién realmente "gestiona agenda"? ¿Paciente, Médico o Secretaria?
- Solicitud: Desambiguar según RF4 ("Roles y Privilegios")

**Ajuste 4:* Analizar clase Agenda según RNF5

- Actual: Agenda tiene 4 responsabilidades
- Requisito: RNF5 dice Agenda es "único componente que controla gestión de turnos"
- Problema: ¿Cómo puede ser "único" si está sobrecargada?
- Solicitud: Proponer arquitectura que respete RNF5 sin violar SRP

**Ajuste 5:** Validar coherencia de atributos en tarjetas CRC

- Actual: Algunas tarjetas tienen propiedades vacías o inconsistentes
- Problema: Tabla de Turno falta "propiedad" en última fila
- Solicitud: Completar y validar todas las propiedades

## iteraciones

### Iteración 1: Identificación Inicial
Salida esperada:

✅ Lista de clases analizadas
✅ Identificación de responsabilidades por clase (basado en tarjetas CRC)
✅ Detección de SRP violations (clases con 2+ razones para cambiar)
✅ Detección de LSP violations (herencias dudosas)

Prompt para Copilot:

"Analiza las tarjetas CRC. Para CADA clase:
1. Lista todas sus responsabilidades (de la columna Responsabilidades)
2. Identifica cuántas 'razones para cambiar' tiene
3. Si tiene 2+, marca como VIOLACIÓN SRP
4. Si hereda, verifica si LSP se cumple"

### Iteración 2: Análisis Profundo de Problemas
Salida esperada:

✅ Para cada violación: PROBLEMA detallado
✅ Para cada problema: Impacto en mantenibilidad (ejemplos concretos)
✅ Escenarios de cambio futuros que quebrarían el diseño
✅ Validación contra requisitos (RNF4, RNF5, etc.)

Prompt para Copilot:

"Para cada VIOLACIÓN SRP identificada:
1. Explicar ESPECÍFICAMENTE qué cambios causarían que la clase se modifique
2. Simular un cambio real (ej: 'Ahora notificamos por Email en lugar de WhatsApp')
3. Mostrar qué archivos/clases se verían afectadas
4. Estimar esfuerzo y riesgo de ese cambio"

### Iteración 3: Propuestas de Refactoring
Salida esperada:

✅ Para cada violación: Propuesta de descomposición
✅ Clases nuevas que se crearían
✅ Responsabilidades de cada nueva clase
✅ Cómo se reorganizarían las relaciones

Prompt para Copilot:

"Para la clase Agenda (más problemática):
1. Propón separación en 2-3 clases más pequeñas
2. Describe responsabilidad única de cada nueva clase
3. Muestra cómo quedaría el código (métodos que iría en cada clase)
4. Dibuja relaciones entre las nuevas clases
5. Verifica que RNF5 ('control centralizado') se mantenga"

### Iteración 4: Validación de Coherencia con Dominio
Salida esperada:

✅ Verificación de que propuestas respetan requisitos (RF1-RF8, RNF1-RNF5)
✅ Validación de que casos de uso siguen siendo posibles
✅ Verificación de que clases nuevas tienen sentido en contexto médico
✅ Matriz de trazabilidad: RF/RNF → Clase → Responsabilidad

Prompt para Copilot:

"Validación de Coherencia:
1. Revisa cada RF en introduccion.md
2. Para cada RF, identifica qué clase/responsabilidad lo implementa
3. Verifica que después del refactoring, CADA RF sigue siendo implementable
4. Verifica que RNF4 (Trazabilidad) y RNF5 (Control centralizado) se respetan"

