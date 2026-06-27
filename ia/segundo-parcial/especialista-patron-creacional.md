# Uso de Copilot Agent Mode - Especialista en Patrón de Diseño Creacional

- **Prompt usado:**

```
Actúa como Senior Software Engineer especializado en patrones de diseño GoF y diseño orientado a objetos.

Analizá los siguientes archivos de contexto del Sistema de Turnos Médicos (STM):
- diagramas/01-diagrama-clases/06-clases-diagrama-final.puml
- diagramas/01-diagrama-clases/01-solid-01-srp.puml
- diagramas/01-diagrama-clases/01-solid-02-ocp.puml
- diagramas/01-diagrama-clases/01-solid-03-lsp.puml
- diagramas/01-diagrama-clases/01-solid-04-isp.puml
- diagramas/01-diagrama-clases/01-solid-05-dip.puml

Tu tarea es aplicar un patrón de diseño CREACIONAL al STM:

1. IDENTIFICAR el problema concreto de instanciación en el sistema actual.
   → ¿Qué clase crea objetos de forma acoplada? ¿Qué viola esto en SOLID?

2. SELECCIONAR el patrón creacional GoF más apropiado (Singleton, Factory Method,
   Abstract Factory, Builder, Prototype) y justificar por qué.

3. DISEÑAR el diagrama de clases UML en PlantUML con:
   - Solo las clases involucradas en el patrón (no el sistema completo)
   - Producto abstracto, productos concretos, creador abstracto, creadores concretos
   - Relaciones correctas: herencia, dependencia de creación (<<crea>>)
   - Notas explicativas sobre el rol de cada elemento
   - skinparam paleta azul coherente con el diagrama final del proyecto
   - Nomenclatura: 01-patron-creacional-factory-method.puml

4. DOCUMENTAR en patron-de-diseno-creacional.md con las secciones:
   - Patrones creacionales y su relación con SOLID
   - Propósito y tipo del patrón
   - Motivación detallada (problema original, solución, clases nuevas)
   - Estructura de clases con imagen incrustada y enlace al PUML
   - Justificación técnica de cada clase y del flujo de creación
```

## Archivos utilizados como contexto

- `diagramas/01-diagrama-clases/06-clases-diagrama-final.puml`
- `diagramas/01-diagrama-clases/01-solid-01-srp.puml`
- `diagramas/01-diagrama-clases/01-solid-02-ocp.puml`
- `diagramas/01-diagrama-clases/01-solid-03-lsp.puml`
- `diagramas/01-diagrama-clases/01-solid-04-isp.puml`
- `diagramas/01-diagrama-clases/01-solid-05-dip.puml`

---

## Ajustes Realizados

**Ajuste 1 — Elección del patrón: Factory Method sobre Abstract Factory**

- Copilot propuso inicialmente Abstract Factory, argumentando que el sistema podría necesitar familias de productos relacionados.
- Se rechazó porque en el STM el problema concreto es la creación de un único tipo de objeto (Turno)
con variantes, no la creación de familias de objetos relacionados. Abstract Factory introduce complejidad innecesaria para este caso específico. Factory Method es más directo y proporcional.
- Decisión tomada: se procedió con Factory Method.
Esto mejora la cohesión textual sin cambiar el contenido técnico.

**Ajuste 2 — Producto abstracto: de clase concreta a clase abstracta**

- Copilot generó inicialmente `Turno` como clase concreta con `calcularDuracion()` implementado.
- Se rechazó porque si `Turno` implementa `calcularDuracion()`, las subclases no están obligadas a sobreescribirla, perdiendo el contrato del patrón.
- Decisión tomada: declarar `Turno` como clase abstracta con `calcularDuracion()` y `getTipoConsulta()` abstractos, coherente con el diagrama OCP (01-solid-02-ocp.puml) del proyecto.

**Ajuste 3 — Integración de Agenda como cliente del Factory**

- Copilot modeló inicialmente `Agenda` con una dependencia directa a los tres creadores concretos.
- Se rechazó porque eso no resuelve el problema de OCP: `Agenda` seguiría conociendo los tipos concretos.
- Decisión tomada: `Agenda` depende únicamente de `CreadorTurno` (abstracción) recibido por inyección mediante `setCreadorTurno()`. El creador concreto lo determina `ControlSistema` según la selección de la secretaria.

**Ajuste 4 — Nota explicativa en CreadorTurno**

- El diagrama inicial no tenía notas que explicaran la distinción entre el Factory Method (`crearTurno()`) y el método plantilla (`registrarEnAgenda()`).
- Se solicitó agregar una nota que documente el rol de cada método para que el diagrama sea autoexplicativo al ser revisado por el docente.
- Decisión tomada: se aceptó la nota propuesta por Copilot con ajuste de redacción para incluir la referencia a OCP explícita.

---

## Iteraciones

### Iteración 1: Identificación del problema de instanciación en el STM

**Prompt enviado a Copilot:**

```
Analizando el archivo diagramas/01-diagrama-clases/06-clases-diagrama-final.puml,
identificá qué clase del STM tiene el problema de instanciación acoplada.
¿Qué método concreto concentra la lógica de creación de objetos?
¿Qué principios SOLID viola este diseño actual?
Explicá por qué el Factory Method es más apropiado que el Abstract Factory
para este caso específico.
```

**Respuesta de Copilot:**

Identificó que `Agenda.registrarTurno(datos: Map)` concentra la lógica de creación de turnos. Señaló violación de OCP (agregar tipo de turno requiere modificar `Agenda`) y SRP (`Agenda` mezcla gestión con fabricación). Recomendó Factory Method por ser un problema de una sola familia de productos.

**Decisión:** Se aceptó el análisis. Se descartó Abstract Factory. Se procedió con Factory Method.

---

### Iteración 2: Diseño del diagrama de clases UML

**Prompt enviado a Copilot:**

```
Diseñá el diagrama PlantUML del Factory Method para el STM con:
- Turno como clase abstracta con calcularDuracion() y getTipoConsulta() abstractos
- TurnoConsulta (30 min), TurnoPrimeraVez (30 min), TurnoControl (15 min) como concretos
- CreadorTurno abstracto con crearTurno() (Factory Method) y registrarEnAgenda() (método plantilla)
- CreadorTurnoConsulta, CreadorTurnoPrimeraVez, CreadorTurnoControl como concretos
- Agenda recibe CreadorTurno por inyección (setCreadorTurno)
- Notas que expliquen el rol del método plantilla vs el Factory Method
- skinparam paleta azul coherente con 06-clases-diagrama-final.puml
```

**Respuesta de Copilot:**

Generó el diagrama con la estructura correcta. `Turno` quedó como clase concreta en la primera versión. Se solicitó cambiarla a abstracta. También las notas no referenciaban OCP explícitamente. Se ajustó la redacción de las notas.

**Decisión:** Se aceptó el diagrama con los dos ajustes solicitados. El resultado cumple con la estructura del Factory Method según GoF.

---

### Iteración 3: Redacción del documento patron-de-diseno-creacional.md

**Prompt enviado a Copilot:**

```
Redactá el documento patron-de-diseno-creacional.md con las siguientes secciones:
1. Introducción a patrones creacionales y su relación con SRP, OCP y DIP
2. Propósito y tipo: Factory Method, problema concreto en STM y solución
3. Motivación: problema original (if/switch en Agenda), limitaciones, clases nuevas
   introducidas y su rol, cómo el patrón reorganiza la arquitectura
4. Estructura de clases: imagen incrustada con ruta relativa correcta desde
   anexos/patrones-diseno/ hacia diagramas/01-diagrama-clases/, enlace al PUML
5. Justificación técnica: descripción de cada clase (responsabilidad, relación,
   necesidad) y flujo de creación paso a paso
```

**Respuesta de Copilot:**

Generó el documento con todas las secciones. La sección de motivación inicialmente describía el problema en términos genéricos sin referenciar clases específicas del STM (Agenda, ControlSistema, Secretaria). Se solicitó reformular usando los nombres exactos del diagrama final.

**Decisión:** Se aceptó el documento con la reformulación de la sección de motivación usando nomenclatura exacta del sistema.

---

### Iteración 4: Verificación de coherencia con el diagrama final

**Prompt enviado a Copilot:**

```
Verificá que el diagrama de Factory Method sea coherente con
06-clases-diagrama-final.puml:
1. ¿Los atributos y métodos de Turno en el diagrama del patrón
   son un subconjunto coherente de los definidos en el diagrama final?
2. ¿La relación Agenda - Turno (composición 1 a *) se mantiene?
3. ¿Hay alguna contradicción entre el patrón aplicado y el diseño SOLID
   del proyecto (01-solid-02-ocp.puml)?
```

**Respuesta de Copilot:**

Confirmó coherencia en atributos y métodos de `Turno`. Señaló que la composición `Agenda "1" *-- "*" Turno` se mantiene en el diagrama del patrón. Verificó que el diagrama OCP del proyecto ya anticipaba la jerarquía `Turno → TurnoConsulta / TurnoPrimeraVez / TurnoControl`, lo que confirma que el Factory Method es la formalización creacional de lo que OCP planteaba a nivel estructural.

**Decisión:** Sin cambios adicionales. El diagrama y la documentación son coherentes con los artefactos previos del proyecto.
