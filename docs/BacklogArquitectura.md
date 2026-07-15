# BA-001 — Biblioteca Musical como concepto independiente del Catálogo

## Estado

Pendiente de evaluación.

## Origen

Glosario.md — Conceptos Fundamentales.

## Descripción

Durante la definición del concepto de Catálogo se identificó la posible necesidad de distinguir entre los conceptos de Biblioteca Musical y Catálogo.

Actualmente GeminiFy gestiona un único Catálogo, por lo que ambos conceptos pueden considerarse equivalentes. Sin embargo, en futuras versiones podría resultar conveniente separar ambos niveles de abstracción.

## Hipótesis

La Biblioteca Musical representaría el conjunto completo de canciones conocidas o disponibles para el sistema.

El Catálogo representaría un subconjunto de la Biblioteca Musical, gestionado con un propósito específico.

Esto permitiría que una misma Biblioteca Musical pudiera dar soporte a múltiples Catálogos independientes.

## Posibles casos de uso

- Catálogo Running.
- Catálogo Ciclismo.
- Catálogo Gimnasio.
- Catálogo Relax.
- Catálogo Concentración.

Todos ellos podrían compartir canciones procedentes de una única Biblioteca Musical.

## Beneficios potenciales

- Mayor reutilización de información.
- Eliminación de duplicidades.
- Escalabilidad del modelo de dominio.
- Posibilidad de gestionar múltiples catálogos especializados.

## Riesgos

- Incremento de la complejidad del modelo de dominio.
- Necesidad de definir nuevas relaciones entre entidades.

## Próxima revisión

Durante el diseño de ModeloDominio.md.

# BA-002 — Sustitución del concepto "Último Combate"

## Estado

Pendiente de evaluación.

## Origen

Auditoría del archivo Excel origen.

## Descripción

Durante la revisión del modelo heredado se identificó el atributo **Último Combate**, cuyo nombre deja de ser coherente tras la sustitución del concepto *Batalla* por *Participación*.

Se propone revisar este concepto y adoptar una terminología alineada con el lenguaje oficial de GeminiFy.

## Propuesta

Sustituir el atributo **Último Combate** por **Última Participación**.

La nueva denominación representa de forma precisa la última aparición registrada de una Canción dentro de una Lista consolidada.

## Motivación

- Mantener la coherencia terminológica del proyecto.
- Eliminar referencias heredadas del modelo Excel.
- Alinear el lenguaje con los ADR aprobados.
- Facilitar la comprensión del modelo de dominio.

## Impacto potencial

La modificación afectará a:

- Modelo de Dominio.
- Reglas de Negocio.
- Migración desde Excel.
- Exportación de datos.
- Interfaz de usuario.

## Próxima revisión

Durante la elaboración de `ModeloDominio.md`.

# BA-003 — Definición del flujo del proceso de Consolidación

## Estado

Pendiente de evaluación.

## Origen

Redacción de `Glosario.md` — Sección 3. Procesos.

## Descripción

Durante la definición del proceso de Consolidación se identificó la necesidad de documentar detalladamente las fases que lo componen.

Aunque el Glosario únicamente define el concepto de Consolidación, será necesario diseñar posteriormente el flujo completo del proceso dentro de la Arquitectura del sistema.

## Hipótesis

Una Consolidación podría estar compuesta, entre otras, por las siguientes fases:

1. Validación de la Lista.
2. Identificación de Canciones existentes.
3. Registro de nuevas Canciones.
4. Generación de Participaciones.
5. Recalculo de estadísticas.
6. Aplicación de Reglas de Negocio.
7. Actualización de Estados y Flags.
8. Registro de Auditoría.
9. Generación del informe de Consolidación.

El orden, contenido y alcance de estas fases deberán definirse durante el diseño de la Arquitectura.

## Beneficios potenciales

- Estandarizar el principal proceso de negocio de GeminiFy.
- Facilitar la implementación del sistema.
- Garantizar la trazabilidad de todas las operaciones.
- Permitir la incorporación de nuevas fases en futuras versiones.

## Próxima revisión

Durante la elaboración de `Arquitectura.md`.

# BA-004 — Clasificación de los procesos de GeminiFy

## Estado

Pendiente de evaluación.

## Origen

Redacción de `Glosario.md` — Sección 3. Procesos.

## Descripción

Durante la definición de los procesos de GeminiFy se identificó una posible clasificación funcional basada en el propósito de cada proceso dentro del sistema.

Esta clasificación podría servir como base para la organización de la Arquitectura y facilitar la comprensión del flujo general de funcionamiento de GeminiFy.

## Hipótesis

Los procesos de GeminiFy podrían agruparse en dos grandes categorías:

### Procesos de Aprendizaje

Procesos cuya finalidad es incorporar, organizar y mantener el conocimiento del Catálogo.

Ejemplos:

- Importación.
- Consolidación.

### Procesos de Explotación del Conocimiento

Procesos que utilizan el conocimiento acumulado para generar valor al usuario.

Ejemplos:

- Propuesta de Lista.
- Exportación.

## Beneficios potenciales

- Simplificar la comprensión de la arquitectura.
- Separar claramente la adquisición de conocimiento de su utilización.
- Facilitar la evolución del sistema.
- Mejorar la organización de la documentación y del código.

## Riesgos

La clasificación propuesta podría resultar insuficiente si en futuras versiones aparecen nuevos tipos de procesos.

## Próxima revisión

Durante la elaboración de `Arquitectura.md`.
