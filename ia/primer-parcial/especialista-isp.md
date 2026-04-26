# Especialista ISP

## Prompt utilizado
Analizá el sistema de turnos médicos utilizando como contexto los archivos `anexos/introduccion.md`, `diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw` y `herramientas-agile/tarjetas-crc/`. Actuá como Especialista en Segregación de Interfaces (ISP) y aplicá el principio ISP al diseño actual del sistema.

## Archivos de contexto referenciados
- anexos/introduccion.md
- diagramas/01-diagrama-clases/01-boceto-inicial.excalidraw
- herramientas-agile/tarjetas-crc/00-tarjeta-crc-persona.md
- herramientas-agile/tarjetas-crc/01-tarjeta-crc-paciente.md
- herramientas-agile/tarjetas-crc/02-tarjeta-crc-medico.md
- herramientas-agile/tarjetas-crc/03-tarjeta-crc-turno.md
- herramientas-agile/tarjetas-crc/04-tarjeta-crc-agenda.md
- herramientas-agile/tarjetas-crc/05-tarjeta-crc-secretaria.md
- herramientas-agile/tarjetas-crc/06-tarjeta-crc-llegada-paciente.md

## Output obtenido
Se generaron los siguientes entregables completos:
- `anexos/principios-solid/04-isp.md`: análisis del principio ISP aplicado al sistema de turnos médicos, con motivación, explicación de interfaces, estructura de clases, diagrama referenciado e imágenes.
- `diagramas/01-diagrama-clases/01-solid-04-isp.puml`: diagrama PlantUML que modela las interfaces ISP y las clases del sistema.
- `diagramas/01-diagrama-clases/01-solid-04-isp.png`: imagen del diagrama ISP.
- `ia/primer-parcial/especialista-isp.md`: registro del prompt, contexto utilizado, resultados obtenidos y ajustes realizados.

## Ajustes realizados
- Definí cuatro interfaces del dominio orientadas a ISP:
  - `IRegistroDeTurnos`
  - `IConsultaDeDisponibilidad`
  - `IAutorizacionDeSobreturno`
  - `IRegistroDeAsistencia`
- Identifiqué que `Secretaria` debe implementar los contratos de gestión de turnos, consulta de disponibilidad y registro de asistencia.
- Identifiqué que `Medico` debe implementar solo el contrato de autorización de sobreturnos.
- Asigné a `Agenda` el contrato de consulta de disponibilidad, evitando que implemente métodos de registro de turnos o gestión de llegada.
- Descarté interfaces amplias como `IGestionTurno` y `IUsuarioSistema` porque no son semánticas del dominio y violan ISP al mezclar comportamientos distintos.
- Añadí la referencia de diagrama UML y la imagen embebida en `anexos/principios-solid/04-isp.md`.

## Observaciones finales
- Las interfaces propuestas son específicas del dominio médico y no son genéricas.
- El diseño evita que las clases queden obligadas a implementar métodos no utilizados.
- Se priorizó claridad de roles: administrativo (Secretaria), médico (Medico), consulta (Agenda) y asistencia (LlegadaPaciente).
