# Uso de Copilot Agent Mode - Especialista en Escenarios de Casos de Uso 

## Prompt utilizado

```
Se solicito a Copilot actuar como un Especialista En Escenarios de Casos de Uso.
Analizar los archivos anexos/introducción.md y la plantilla de escenarios.
Completar los campos de cada escenario:
- ID
- Área
- Actores
- Descripción
- Evento activador
- Tipo de señal (usando checkboxes [x]/[ ])
- Flujo principal en formato de tabla (acción + información)
- Precondiciones
- Poscondiciones
- Suposiciones
- Reunir requerimientos
- Aspectos sobresalientes
- Prioridad
- Riesgo

El resultado debe estar en formato de tablas Markdown según la plantilla oficial y cada paso debe referenciar los RF/RNF correspondientes.
```

## Ajustes realizados 
- Se migraron las listas con guiones a tablas Markdown (plantilla oficial). 
- Se actualizo de genérico a Sistema de Gestion de Turnos Medicos. 
- Se corrigieron y completaron los 5 subcampos: Precondiciones, Poscondiciones, Suposiciones, Reunir requerimientos y Aspectos sobresalientes. 
- Cada paso y cada condición referencia el RF/RNF correspondiente de introduccion.md. 

## Interacciones realizadas 

### Interacción 1: Generación inicial de Escenarios 
**Promp Usado:**
```
Analiza los archivos anexos/introducción.md y la plantilla de escenarios para crear los escenarios de casos de uso.
```
**Respuesta:** Generó los escenarios de casos de uso. 

**Observación:** Los escenarios eran genéricos, con información incompleta y sin respetar el formato de tablas requerido por la plantilla. 

### Interacción 2: Ajuste de formato y estructura 
**Promp usado:**
```
Generar los escenarios de casos de uso en formato de tablas Markdown según la plantilla oficial.
Cada escenario debe incluir todos los campos definidos en la plantilla.
```
**Respuesta:** Copilot generó los escenarios en formato de tablas Markdown. 

**Observación:** Se logró el formato correcto, pero algunos campos estaban incompletos y no se incluían referencias a los RF y RNF .

### Interacción 3: Refinamiento final con los RF y RNF. 
**Promp usado:**
```
Completar todos los campos de los escenarios de casos de uso e incluir referencias a los requerimientos funcionales (RF) y no funcionales (RNF) en cada paso y condición, tomando como base el archivo introduccion.md.
```

**Respuesta:** Coplitot generó escenarios completos, con todos los campos y referencias a RF y RNF. 

**Observacion:** El resultado final cumple con la estructura de la plantilla, el formato de tablas Markdown y la inclucion de referencias a requerimientos.