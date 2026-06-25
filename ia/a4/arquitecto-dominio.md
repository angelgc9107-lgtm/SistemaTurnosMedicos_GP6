# Uso de Copilot Agent Mode - Arquitecto de Dominio

- **Prompt usado:**

```
Actúa como Senior Software Architect especializado en diseño orientado a objetos y modelado UML.

Tenés acceso al repositorio completo del Sistema de Turnos Médicos (STM) con todos los aportes
de los roles mergeados a develop. Tu tarea es construir la versión final de los tres artefactos
del Arquitecto de Dominio:

1. DIAGRAMA DE CLASES FINAL UNIFICADO (06-clases-diagrama-final.puml)
   → Integrar las clases de los 5 diagramas parciales por CU
   → Detectar y documentar inconsistencias entre diagramas parciales
   → Mantener coherencia exacta con las 12 tarjetas CRC del proyecto
   → Organizar en paquetes: Jerarquía de Personas, Gestión de Turnos,
     Control y Presentación, Servicios
   → Relaciones: herencia, composición, asociación, dependencia según CRC

2. ANEXO DE LOS CUATRO PILARES POO (anexos/pilares-poo.md)
   → Exactamente 2 ejemplos por pilar desde clases del diagrama final
   → Capturas recortadas en capturas-pilares/ con nomenclatura poo-[pilar]-ejemplo-[N].png

3. PSEUDOCÓDIGO DEL HAPPY PATH GLOBAL (anexos/happy-path-global.md)
   → Escenario que atraviese CU1 + CU2 + CU3 + CU5 (mayor cobertura de clases)
   → Nombres exactos del diagrama final
   → Tabla de trazabilidad con CU y diagrama de secuencia de referencia
```

## Archivos utilizados como contexto

- `diagramas/01-diagrama-clases/01-clases-agendar-turno-01.puml`
- `diagramas/01-diagrama-clases/02-clase-registrar-checkin.puml`
- `diagramas/01-diagrama-clases/03-clase-reprogramar-turno.puml`
- `diagramas/01-diagrama-clases/04-clase-bloquear-horarios.puml`
- `diagramas/01-diagrama-clases/05-clase-visualizar-agenda.puml`
- `herramientas-agile/tarjetas-crc/00-tarjeta-crc-persona.md` hasta `12-tarjeta-crc-validador-disponibilidad.md`
- `diagramas/05-diagramas-secuencia/*.puml` (los 5 diagramas de secuencia)

---

## Ajustes Realizados

**Ajuste 1 — Eliminación de clase Usuario del diagrama final**

- CU5 introducía una clase `Usuario` como superclase de Secretaria y Medico.
- El sistema ya tiene `Persona` como superclase común de todos los roles.
- Decisión tomada: eliminar `Usuario` del diagrama final y agregar `accederAgenda()` como método propio de Secretaria y Medico, evitando una segunda jerarquía de herencia inconsistente con el resto del modelo.

**Ajuste 2 — Resolución del duplicado de tarjeta CRC ControlSistema**

- El repositorio contiene dos archivos para ControlSistema: `08-tarjeta-crc-control-sistema.md` y `08-tarjeta-crc-control-sistemas.md`, ambos con contenido idéntico.
- Decisión tomada: usar una única clase `ControlSistema` en el diagrama final. El duplicado es un error de nombre de archivo sin impacto en el diseño.

**Ajuste 3 — Consolidación de métodos de Agenda**

- Cada diagrama parcial (CU1 a CU5) definía métodos de `Agenda` para su caso de uso específico, con algunos nombres solapados.
- Decisión tomada: consolidar todos los métodos en una única clase `Agenda` del diagrama final, eliminando duplicados y manteniendo el método con la firma más completa cuando había variaciones menores de nombre.

**Ajuste 4 — Happy path extendido a 4 CU**

- La primera versión del happy path cubría solo CU1 + CU2 + CU3.
- Al integrar los aportes de CU4 y CU5, se agregó el bloque de Visualizar Agenda para incorporar VistaCalendario, GestorBloqueos, Bloqueo y Resultado al pseudocódigo.
- Decisión tomada: extender el happy path a CU1 + CU2 + CU3 + CU5, cubriendo 13 de las 16 clases del sistema.

---

## Iteraciones

### Iteración 1: Integración de diagramas parciales CU1 a CU3

**Prompt enviado a Copilot:**

```
Usando los PUMLs de clases de CU1, CU2 y CU3 y las tarjetas CRC correspondientes,
generá el diagrama de clases unificado en PlantUML con paquetes.
Detectá inconsistencias entre los diagramas parciales y documentalas.
Usá visibilidad correcta (público +, privado -, protegido #) y
tipos de relación UML apropiados según las colaboraciones CRC.
```

**Respuesta de Copilot:**

Generó la estructura base con los paquetes y las clases de CU1 a CU3. Detectó que CU2 usaba `Secretaria` para operaciones de check-in no contempladas en su CRC. También propuso `LlegadaPaciente` con relación de composición con `Agenda`, que se ajustó a dependencia de creación (`..>`) según el diagrama de secuencia CU2.

**Decisión:** Se aceptó la estructura de paquetes. Se corrigió la relación de `LlegadaPaciente` y se documentó la inconsistencia de `Secretaria` en la sección de decisiones de integración.

---

### Iteración 2: Incorporación de CU4 y CU5 — clases de control y presentación

**Prompt enviado a Copilot:**

```
Incorporá al diagrama final las clases de CU4 (GestorBloqueos, ValidadorDisponibilidad,
Bloqueo, RangoFechaHora, Resultado) y CU5 (VistaCalendario).
Verificá que ControlSistema consolide los métodos de coordinación de todos los CU.
Detectá si Usuario de CU5 es coherente con Persona como superclase ya existente.
```

**Respuesta de Copilot:**

Incorporó las clases nuevas y detectó el conflicto de `Usuario` vs `Persona`. Propuso eliminar `Usuario` y agregar `accederAgenda()` como método de las subclases de `Persona`. También consolidó `ControlSistema` con los métodos de los 4 CU donde aparece.

**Decisión:** Se aceptó la propuesta de eliminar `Usuario`. Se verificó que `accederAgenda()` estuviera en `Secretaria` y `Medico` con la firma correcta del diagrama de secuencia CU5.

---

### Iteración 3: Generación de capturas para pilares POO

**Prompt enviado a Copilot:**

```
Para cada uno de los 8 ejemplos de los 4 pilares POO, generá un PUML independiente
mostrando solo las clases involucradas. Los atributos y métodos deben coincidir
exactamente con el diagrama final aprobado. Agregá notas en los ejemplos de
polimorfismo explicando el comportamiento específico de cada subclase en el STM.
```

**Respuesta de Copilot:**

Generó los 8 PUMLs. Las notas de polimorfismo inicialmente usaban lenguaje genérico. Se solicitó reemplazarlas con descripciones específicas del dominio del STM (SMS al paciente, panel médico, sistema de gestión administrativo).

**Decisión:** Se aceptaron los PUMLs con las notas reformuladas.

---

### Iteración 4: Verificación final de coherencia

**Prompt enviado a Copilot:**

```
Verificá que el diagrama final cumpla:
1. Todos los métodos de los 5 diagramas de secuencia están representados en el diagrama final
2. Todas las colaboraciones de las 12 tarjetas CRC se reflejan como relaciones
3. No hay clases en el diagrama final que no tengan tarjeta CRC
4. El pseudocódigo usa nombres exactos del diagrama final
Reportá cualquier discrepancia encontrada.
```

**Respuesta de Copilot:**

Reportó que `HistorialTurno` tenía el método `registrarCambio()` con firma diferente entre el diagrama de clases de CU3 y el diagrama de secuencia CU3. Se unificó la firma usando los 4 parámetros del diagrama de secuencia: `registrarCambio(fechaAnterior, horaAnterior, fechaNueva, horaNueva)`. Sin otras discrepancias.

**Decisión:** Se aceptó la corrección de firma. El diagrama final quedó coherente con todos los artefactos previos.
