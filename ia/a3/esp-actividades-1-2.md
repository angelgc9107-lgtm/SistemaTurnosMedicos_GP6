# Uso de Copilot Agent Mode - Especialista en Diagramas de Actividades (CU1 y CU2)

- **Prompt usado:**

```
Actúa como Senior Software Engineer especializado en modelado UML con PlantUML.

Analiza los archivos proporcionados como contexto y diseña diagramas de actividades
para los casos de uso CU1 (Agendar Turno) y CU2 (Registrar Check-in) del Sistema
de Turnos Médicos (STM).

Para cada diagrama:

1. SWIMLANES (mínimo 3 por diagrama)
   → Identificar los actores y sistemas involucrados en el flujo
   → Asignar cada actividad al responsable correcto (Paciente, Secretaria, Sistema, Médico)

2. ACTIVIDADES (mínimo 10 por diagrama)
   → Representar cada paso del flujo principal definido en los escenarios
   → Incluir actividades de validación, decisión y confirmación

3. FLUJOS DE DECISIÓN
   → Modelar bifurcaciones para casos alternativos (conflictos de horario, turno no encontrado)
   → Incluir flujos de error y manejo de excepciones relevantes

4. NOTAS Y REQUISITOS
   → Referenciar los requisitos funcionales (RF1-RF8) en las notas del diagrama
   → Documentar restricciones de negocio relevantes (RF5: restricciones por día/tipo)

FORMATO REQUERIDO:
- Código PlantUML válido y ejecutable con @startuml / @enduml
- skinparam de estilo profesional con colores diferenciados por CU
- Nomenclatura: 04-actividad-[nombre]-0N.puml
- Comentarios en español alineados con el dominio del STM
```

## Archivos utilizados como contexto

- `diagramas/02-casos-de-uso/02-agendar-turno-01.puml`
- `diagramas/02-casos-de-uso/02-registrar-checkin-02.puml`
- `diagramas/03-escenarios-casos-de-uso/03-agendar-turno-flujo-principal.md`
- `diagramas/03-escenarios-casos-de-uso/03-registrar-checkin-flujo-principal.md`

---

## Ajustes Realizados

**Ajuste 1 — CU1: Incorporación de restricciones RF5 como nodo de decisión**

- La IA generó inicialmente el flujo sin modelar las restricciones del RF5 (sin "Primera vez" los viernes tarde, sin procedimientos los lunes).
- Se solicitó agregar un rombo de decisión explícito que evalúe `¿Horario cumple restricciones?` antes de permitir la confirmación.
- Decisión tomada: se aceptó la sugerencia y se incorporó el nodo de decisión con texto que referencia RF5 directamente.

**Ajuste 2 — CU1: Flujo de sobreturno como rama alternativa**

- El diagrama inicial omitía el caso de extensión `CU1_EXT` (sobreturno) definido en el diagrama de casos de uso.
- Se solicitó incorporarlo como bifurcación dentro del flujo de conflicto de horario.
- Decisión tomada: se aceptó e incorporó como subrama dentro de la decisión `¿Horario disponible?`.

**Ajuste 3 — CU2: Incorporación del actor Médico como cuarto swimlane**

- La IA generó el CU2 inicialmente con solo 3 swimlanes (Paciente, Secretaria, Sistema).
- El flujo principal define que el médico visualiza al paciente en espera y lo llama (paso 7 del escenario), lo cual es una actividad propia del actor Médico.
- Decisión tomada: se incorporó el swimlane `Médico` con las actividades de visualización y llamado al paciente.

**Ajuste 4 — CU2: Manejo de turno no encontrado y estado inválido**

- La IA no modeló los caminos alternativos para turno no encontrado ni turno en estado diferente a "Pendiente".
- Se solicitó agregar ambos nodos de decisión con sus ramas de error y criterios de salida.
- Decisión tomada: se aceptó y se incorporaron ambas decisiones con flujos de error que terminan en `stop` cuando corresponde.

**Ajuste 5 — Ambos diagramas: Alineación de colores por CU**

- Se diferenció visualmente cada diagrama: azul (#EFF6FF / #3B82F6) para CU1 y verde (#F0FDF4 / #16A34A) para CU2, siguiendo la paleta usada en los diagramas de casos de uso originales.
- Decisión tomada: se aceptó para mantener consistencia visual con los artefactos existentes del proyecto.

---

## Iteraciones

### Iteración 1: Generación del flujo principal de CU1 — Agendar Turno

**Prompt enviado a Copilot:**

```
Usando como contexto el archivo diagramas/02-casos-de-uso/02-agendar-turno-01.puml
y diagramas/03-escenarios-casos-de-uso/03-agendar-turno-flujo-principal.md,
genera un diagrama de actividades PlantUML para CU1.
Incluye swimlanes para Paciente, Secretaria y Sistema.
Modela los 12 pasos del flujo principal del escenario.
Usa skinparam con paleta azul y agrega notas con referencias a RF2 y RF7.
```

**Respuesta de Copilot:**

Generó el diagrama con los 12 pasos del flujo principal distribuidos en 3 swimlanes. Incluyó notas para RF2 (tipos de turno) y RF7 (notificaciones WhatsApp). No modeló restricciones RF5 ni el flujo de sobreturno definido en CU1_EXT.

**Decisión:** Se aceptó la base del diagrama y se solicitaron ajustes en la iteración 2.

---

### Iteración 2: Incorporación de decisiones y flujo alternativo en CU1

**Prompt enviado a Copilot:**

```
Agrega al diagrama de CU1 los siguientes elementos:
1. Un rombo de decisión "¿Horario cumple restricciones?" que evalúe RF5
   (sin Primera vez los viernes tarde, sin procedimientos los lunes).
   En caso NO: informar restricción y volver a selección de horario.
2. Un rombo de decisión "¿Horario disponible?" dentro del flujo principal.
   En caso NO: ofrecer opción de sobreturno como rama alternativa.
Mantener los 3 swimlanes existentes.
```

**Respuesta de Copilot:**

Incorporó ambos rombos de decisión con sus ramas. El texto de los nodos se ajustó manualmente para incluir referencias a RF5 explícitas en los labels de los rombos. Se aceptaron los flujos alternativos propuestos. El resultado cumple con el mínimo de 10 actividades y 3 swimlanes.

**Decisión:** Se aceptaron todos los cambios. El resultado cumple con el mínimo de 10 actividades y 3 swimlanes.

---

### Iteración 3: Generación del flujo principal de CU2 — Registrar Check-in

**Prompt enviado a Copilot:**

```
Usando como contexto el archivo diagramas/02-casos-de-uso/02-registrar-checkin-02.puml
y diagramas/03-escenarios-casos-de-uso/03-registrar-checkin-flujo-principal.md,
genera un diagrama de actividades PlantUML para CU2.
Incluye swimlanes para Paciente, Secretaria y Sistema.
Modela los 8 pasos del flujo principal del escenario.
Agrega un cuarto swimlane para Médico con las actividades de visualización
y llamado al paciente definidas en el paso 7.
Usa skinparam con paleta verde para diferenciarlo de CU1.
Referencia RF4 y RF8 en las notas del diagrama.
```

**Respuesta de Copilot:**

Generó el diagrama con 4 swimlanes y modeló los 8 pasos del flujo principal. Incluyó notas para RF4 (roles diferenciados) y RF8 (registro de timestamp). No modeló los caminos alternativos para turno no encontrado ni turno en estado diferente a "Pendiente".

**Decisión:** Se aceptó la base y se solicitaron los flujos alternativos en la iteración 4.

---

### Iteración 4: Incorporación de flujos alternativos en CU2

**Prompt enviado a Copilot:**

```
Agrega al diagrama de CU2 los siguientes flujos alternativos:
1. Después de la búsqueda: rombo "¿Turno encontrado?".
   En caso NO: mostrar mensaje de error, verificar datos del paciente,
   reintentar búsqueda o terminar flujo si los datos son incorrectos.
2. Después de seleccionar el turno: rombo "¿Turno en estado Pendiente?".
   En caso NO: informar estado inválido y terminar flujo.
Mantener los 4 swimlanes y las notas RF4 y RF8.
```

**Respuesta de Copilot:**

Incorporó ambas ramas alternativas con nodos de decisión anidados. Se ajustó el nivel de anidamiento del primer rombo para incluir la subdecisión de verificación de datos con posibilidad de reintento o terminación del flujo si los datos son incorrectos. Se aceptó la propuesta completa.

**Decisión:** Se aceptaron todos los cambios. El resultado cumple con el mínimo de 10 actividades y 3 swimlanes (se superó con 4 swimlanes).
