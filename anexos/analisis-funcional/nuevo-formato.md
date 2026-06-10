## 1. Descripción y Trazabilidad con Requisitos Funcionales

<!-- 
Copiá la descripción del caso de uso exactamente como está en introduccion.md y en el escenario de
diagramas/03-escenarios-casos-de-uso/. No reformules ni resumas: es el mismo caso de uso aprobado.
Los actores deben coincidir con los del diagrama de casos de uso de A2.
El flujo principal debe coincidir paso a paso con el escenario de A2.
-->

**Actor/es:** [nombre/s exactos como aparecen en el escenario de A2]

**Objetivo:** [una sola oración explicando qué resuelve este caso de uso]

**Flujo principal:**

<!-- Copiá los pasos del escenario de diagramas/03-escenarios-casos-de-uso/. No los reescribas. -->

1. [paso 1]
2. [paso 2]
3. [paso 3]

**Flujos alternativos:**

<!-- Solo si están definidos en el escenario. Si no hay, eliminá esta subsección. -->

- [A1: descripción]
- [A2: descripción]

**Requisitos funcionales que satisface:**

<!-- 
Copiá el identificador y el texto literal de introduccion.md. No parafrasees.
En la tercera columna explicá brevemente cómo este caso de uso cumple ese requisito.
Solo listá los RF que este caso de uso resuelve directamente, no todos los del sistema.
-->

| ID | Requisito Funcional (texto exacto de introduccion.md) | Cómo lo satisface este caso de uso |
|----|------------------------------------------------------|-------------------------------------|
| RF[N] | [texto literal] | [explicación breve] |
| RF[N] | [texto literal] | [explicación breve] |

---

## 2. Diagrama de Casos de Uso

<!-- 
Incrustá la imagen que ya existe en diagramas/02-casos-de-uso/.
No generes un diagrama nuevo ni modifiques el existente.
El nombre del archivo debe coincidir exactamente con el que está en el repositorio.
-->

![Diagrama de Casos de Uso - [Nombre del CU]](../../diagramas/02-casos-de-uso/02-caso-uso-nombre-caso-de-uso-0N.png)

<!-- 
Explicá brevemente:
- Qué actores participan y qué rol cumple cada uno
- Qué relaciones UML se usaron (include, extend, asociación) y por qué
No repitas lo que ya es obvio viendo el diagrama. Solo lo que no se ve a simple vista.
-->

**Actores y relaciones:**
- [Actor] → [qué hace en este caso de uso]
- Include/Extend: [si aplica, explicá por qué se modeló así]

---

## 3. Diagrama de Actividades

<!-- 
Incrustá la imagen que ya existe en diagramas/04-diagramas-actividades/.
No generes un diagrama nuevo ni modifiques el existente.
-->

![Diagrama de Actividades - [Nombre del CU]](../../diagramas/04-diagramas-actividades/04-actividad-nombre-caso-uso-0N.png)

<!-- 
Explicá brevemente:
- Qué swimlanes se usaron y por qué esa distribución de responsabilidades
- Cuáles son los puntos de decisión más importantes del flujo
No describas cada actividad una por una: el diagrama ya lo muestra.
-->

**Swimlanes:** [listá los carriles y qué actor o componente representa cada uno]

**Decisiones clave del flujo:** [los puntos de bifurcación más relevantes y qué condición los dispara]

---

## 4. Diagrama de Secuencia

<!-- 
Incrustá la imagen que ya existe en diagramas/05-diagramas-secuencia/.
No generes un diagrama nuevo ni modifiques el existente.
-->

![Diagrama de Secuencia - [Nombre del CU]](../../diagramas/05-diagramas-secuencia/05-secuencia-nombre-caso-uso-nombre-escenario-0N.png)

<!-- 
Explicá brevemente:
- Qué objetos participan y qué notación UML se usó para cada uno (Clase, :objeto, Clase:objeto)
- Cuáles son los mensajes más relevantes y qué desencadenan
- Si hay objetos temporales que se destruyen, mencioná cuáles y por qué son temporales
Los nombres de los mensajes deben coincidir exactamente con los del diagrama.
-->

**Participantes:** [listá los objetos/actores con su notación UML]

**Mensajes clave:**
- [metodo(argumento)] → [qué produce]
- [metodo(argumento)] → [qué produce]

**Objetos temporales destruidos:** [si aplica, cuáles y por qué no persisten]

---

## 5. Diagrama de Clases del Caso de Uso

<!-- 
Este es el diagrama nuevo generado en A4 con Copilot Agent Mode.
Solo debe incluir las clases involucradas en ESTE caso de uso, no todo el sistema.
Cada clase debe tener su tarjeta CRC en herramientas-agile/tarjetas-crc/.
Si durante el diseño identificás una clase nueva que no tiene tarjeta CRC, debés crearla
y justificar la decisión antes de incluirla en el diagrama.
Los nombres de clases, atributos y métodos deben coincidir con:
- Las tarjetas CRC de A2 (responsabilidades y colaboraciones)
- Los participantes y mensajes del diagrama de secuencia de A3
No podés introducir métodos o atributos que no se desprendan de los artefactos anteriores.
-->

![Diagrama de Clases - [Nombre del CU]](../../diagramas/01-diagrama-clases/0N-clases-nombre-caso-uso-0N.png)

**Clases involucradas:**

<!-- 
Una fila por clase. En la columna de tarjeta CRC, enlazá el archivo correspondiente.
La responsabilidad debe coincidir con la definida en la tarjeta CRC, no inventar una nueva.
-->

| Clase | Responsabilidad (según tarjeta CRC) | Tarjeta CRC |
|-------|-------------------------------------|-------------|
| [NombreClase] | [responsabilidad exacta de la tarjeta] | [link al archivo .md] |
| [NombreClase] | [responsabilidad exacta de la tarjeta] | [link al archivo .md] |

**Relaciones UML:**

<!-- 
Por cada relación, explicá brevemente por qué existe esa relación y no otra.
Por ejemplo: por qué es composición y no agregación, o por qué es dependencia y no asociación.
-->

| Relación | Clases | Justificación |
|----------|--------|---------------|
| [tipo] | [ClaseA] → [ClaseB] | [por qué existe esta relación] |

---

## 6. Pseudocódigo

<!-- 
El pseudocódigo debe seguir el flujo principal de la sección 1 y los mensajes del diagrama de secuencia.
No uses sintaxis de ningún lenguaje particular.
Usá los mismos nombres de clases y métodos que aparecen en el diagrama de clases: nada inventado.
Cada comentario debe explicar QUÉ está pasando en términos del dominio, no describir el código.
El objetivo es que alguien pueda leer solo el pseudocódigo y entender cómo se resuelve el caso de uso.
Si el flujo no se entiende sin ver el diagrama, agregá más comentarios.
-->

```text
INICIO [Nombre del Caso de Uso]

// [Contexto: qué condición disparó este caso de uso y quién lo inicia]

[NombreClase] objeto1 = nuevo [NombreClase](parametro1, parametro2)
[NombreClase] objeto2 = nuevo [NombreClase](parametro1)

// [Qué está resolviendo este bloque en términos del dominio]
resultado = objeto1.metodo(argumento)

// [Qué decisión se toma y por qué]
SI resultado es válido
    objeto2.metodo(resultado)
    // [Qué produce esta acción en el sistema]
SINO
    // [Qué flujo alternativo se activa]
FIN SI

// [Estado final del sistema tras ejecutar el caso de uso]
Retornar [resultado final]

FIN
```