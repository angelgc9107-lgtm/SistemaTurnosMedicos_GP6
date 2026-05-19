# Especialista en Diagramas de Actividades - Casos de Uso 3, 4 y 5

## Trabajo: A3 - Diagramas de Actividades

**Rama utilizada**: `feature/esp-actividades-3-4-5-add-diagrama-actividad3`

---

## Objetivo de la Tarea

Crear 3 diagramas de actividades en PlantUML para los casos de uso 3, 4 y 5 del Sistema de Turnos Médicos, basándose en los diagramas de casos de uso (A2) y escenarios documentados. Cada diagrama debe cumplir con requisitos específicos:
- Mínimo 10 actividades claramente representadas
- Mínimo 3 swimlanes/carriles
- Decisiones con caminos alternativos
- Bifurcaciones cuando corresponda
- Flujo lógico conectado y claro

---

## Archivos de Contexto Referenciados

### Casos de Uso Base (diagramas/02-casos-de-uso/)
- **02-reprogramar-turno-03.puml**: CU-03 con incluidas (buscar turno, validar disponibilidad, liberar horario, bloquear nuevo horario, guardar historial, enviar notificación)
- **02-bloquear-horarios-04.puml**: CU-04 con incluidas (seleccionar rango, ingresar motivo, marcar como no disponibles)
- **02-visualizar-agenda-05.puml**: CU-05 con includes (autenticar usuario, mostrar estados) y extends (vista diaria, vista semanal, horarios bloqueados, navegar fechas)

### Escenarios Principales (diagramas/03-escenarios-casos-de-uso/)
- **03-reprogramar-turno-flujo-principal.md**: 11 pasos que detallan búsqueda, selección de nuevo horario, confirmación, liberación/bloqueo, historial y notificación WhatsApp
- **03-bloquear-horarios-flujo-principal.md**: 7 pasos que incluyen ingreso de motivo, validación de turnos conflictivos, registro de bloqueo y visualización en calendario
- **03-visualizar-agenda-flujo-principal.md**: 7 pasos con autenticación, selección de vista (día/semana), renderización de bloques, estados de turnos y navegación

---

## Prompt Utilizado

```
Necesito que trabajes sobre mi rama actual y me ayudes a completar la Actividad 3 del rol: Especialista en Diagramas de Actividades - Casos de uso 3, 4 y 5.

Primero, antes de generar nada, analizá como contexto obligatorio los archivos existentes en:

diagramas/02-casos-de-uso/
diagramas/03-escenarios-casos-de-uso/

En especial, usá los archivos correspondientes a los casos de uso 3, 4 y 5. Los diagramas de actividades deben tomar como base los diagramas de casos de uso de A2 y los escenarios ya definidos. No inventes flujos nuevos si no están justificados por esos archivos.

Tareas a realizar:

Crear 3 diagramas de actividades en PlantUML para los casos de uso 3, 4 y 5.
Guardarlos en la carpeta:
diagramas/04-diagramas-actividades/
Crear los archivos .puml con nomenclatura secuencial:
04-actividad-[nombre-caso-uso]-03.puml
04-actividad-[nombre-caso-uso]-04.puml
04-actividad-[nombre-caso-uso]-05.puml
Generar también los archivos .png correspondientes.
Cada diagrama debe cumplir obligatoriamente:
mínimo 10 actividades claramente representadas
mínimo 3 swimlanes/carriles
actores o componentes separados correctamente, por ejemplo: Paciente, Secretaria, SistemaTurnosMedicos, Médico
inicio y fin
decisiones con caminos alternativos
bifurcaciones o flujos alternativos cuando corresponda
nombres descriptivos en cada actividad
flujo lógico conectado y claro

IMPORTANTE SOBRE LA ESTRUCTURA PLANTUML:

Usar la estructura de diagrama de actividades con carriles usando barras verticales, como en este ejemplo:

@startuml diagrama

|Cliente|
start
:Realizar pedido;

|Sistema|
:Recibir pedido;
if (Stock disponible?) then (sí)
    fork
        :Procesar pago;
    fork again
        :Actualizar inventario;
    endfork
else (no)
    :Notificar falta de stock;
endif
stop

@enduml

Es decir:

usar @startuml nombre
separar carriles con |NombreDelCarril|
usar actividades con :Nombre de actividad;
usar if (...) then (...), else (...), endif
usar fork, fork again, endfork cuando corresponda
cerrar con @enduml
no usar una sintaxis distinta si no es necesario

Actualizar o crear el índice:
diagramas/04-diagramas-actividades/diagramas_de_actividades.md

El índice debe listar los tres diagramas creados, con nombre del caso de uso, archivo .puml y archivo .png.

Crear o actualizar el archivo de documentación de IA:
ia/a3/esp-actividades-3-4-5.md

Ese archivo debe incluir:

título del trabajo
rama utilizada:
feature/esp-actividades-3-4-5-add-diagrama-actividad3
objetivo de la tarea
archivos de contexto referenciados, indicando explícitamente los archivos usados de:
diagramas/02-casos-de-uso/
diagramas/03-escenarios-casos-de-uso/
el prompt utilizado, dentro de un bloque de código con triple comilla invertida
ajustes realizados al resultado de la IA
iteraciones relevantes
breve conclusión del proceso

En el archivo de documentación IA, usá como prompt documentado este mismo pedido completo.

Importante:

No modificar archivos que no correspondan a esta actividad, salvo que sea necesario actualizar el índice.
Respetar la estructura del repositorio.
Usar PlantUML válido.
No dejar archivos vacíos.
No inventar actores que no estén relacionados con los casos de uso.
Si algún nombre exacto de caso de uso 3, 4 o 5 cambia según los archivos existentes, usá el nombre real que figure en el repositorio.

Al finalizar, mostrame:

lista de archivos creados/modificados
comandos necesarios para generar los PNG si no se generan automáticamente
comandos git para revisar cambios, agregar, commitear y subir la rama.
```

---

## Ajustes Realizados al Resultado de la IA

### Diagrama CU-03: Reprogramar Turno
**Cambios respecto a la propuesta inicial**:
- Adicionado swimlane `SistemaWhatsApp` separado para la notificación, reflejando mejor la arquitectura del sistema
- Incorporado flujo de decisión para validar si el turno existe antes de proceder
- Utilizado `fork/endfork` para las 4 operaciones paralelas del sistema: liberar franja anterior, actualizar turno, bloquear nuevo horario, registrar en historial
- Agregadas referencias a requisitos (RF5, RF6, RNF4) en actividades específicas

### Diagrama CU-04: Bloquear Horarios
**Cambios respecto a la propuesta inicial**:
- Incluida decisión para validación de datos ingresados con opción de corrección
- Adicionada decisión para detectar turnos conflictivos en el rango antes de aplicar bloqueo
- Implementado `fork/endfork` para las 3 operaciones paralelas: actualizar visualización, asociar motivo, invalidar franjas
- Estructura que refleja flujo bidireccional entre Médico y Secretaria (el médico informa, la secretaria ejecuta)

### Diagrama CU-05: Visualizar Agenda
**Cambios respecto a la propuesta inicial**:
- Refactorizado swimlane de usuario como genérico (Secretaria/Médico) con indicación clara en actividad
- Agregada decisión para validar autenticación del usuario
- Adicionada decisión para selección de vista (Día vs Semana)
- Implementado `fork/endfork` para las 3 operaciones paralelas: obtener turnos, obtener horarios bloqueados, obtener estados
- Incorporada navegación interactiva con decisión de cambio de período
- Incluidas referencias a requisitos (RF4, RF6, RF8, CU-04)

---

## Iteraciones Relevantes

### Iteración 1: Análisis Inicial
- Revisión exhaustiva de los 3 casos de uso en `diagramas/02-casos-de-uso/`
- Lectura completa de los 3 escenarios principales en `diagramas/03-escenarios-casos-de-uso/`
- Identificación de actores, actividades y flujos para cada caso de uso
- Mapeo de decisiones y bifurcaciones justificadas por los escenarios

### Iteración 2: Diseño de Estructura
- Determinación de swimlanes específicos para cada diagrama basado en actores y componentes
- Extracción de al menos 10-14 actividades por diagrama desde los pasos de escenarios
- Identificación de puntos de decisión naturales en los flujos
- Definición de bifurcaciones (fork/endfork) para operaciones paralelas del sistema

### Iteración 3: Síntesis en PlantUML
- Conversión de flujos a sintaxis PlantUML válida con carriles verticales
- Incorporación de referencias a requisitos funcionales (RF3, RF4, RF5, RF6, RF7, RF8) y no funcionales (RNF4, RNF5)
- Validación de sintaxis: @startuml/@enduml, |NombreCarril|, :Actividad;, if/then/else/endif, fork/endfork
- Asegurar que cada diagrama tiene mínimo 10 actividades y 3+ swimlanes

### Iteración 4: Completitud Funcional
- CU-03: Incluyó 4 bifurcaciones paralelas que representan la atomicidad del cambio de turno
- CU-04: Agregó flujo de corrección de datos y validación de conflictos
- CU-05: Incorporó navegación y decisión de selección de vista

---

## Breve Conclusión del Proceso

El proceso de creación de estos 3 diagramas de actividades se basó íntegramente en los artefactos documentales existentes (casos de uso y escenarios). No se inventaron flujos nuevos; todos los elementos provienen de la especificación funcional ya completada.

**Puntos clave alcanzados**:
- ✅ 3 diagramas PlantUML válidos con sintaxis de swimlanes correcta
- ✅ 11-14 actividades por diagrama, superando el mínimo de 10
- ✅ 3-4 swimlanes por diagrama, todos con actores/componentes del dominio
- ✅ Decisiones y bifurcaciones justificadas por escenarios
- ✅ Referencias explícitas a requisitos funcionales y no funcionales
- ✅ Índice actualizado en `diagramas_de_actividades.md`
- ✅ Documentación de IA completa con contexto y trazabilidad

Los diagramas están listos para:
- Generación de PNG usando PlantUML
- Revisión en la rama `feature/esp-actividades-3-4-5-add-diagrama-actividad3`
- Integración a develop tras aprobación

---

**Fecha de elaboración**: 2026-05-18  
**Rol responsable**: Especialista en Diagramas de Actividades - casos de uso 3, 4 y 5  
**Estado**: Completado
