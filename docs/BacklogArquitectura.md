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

# BA-005 — Incorporación del concepto "Indicador"

## Estado

Pendiente de evaluación.

## Origen

Redacción de `Glosario.md` — Sección 5. Estadísticas.

## Descripción

Durante la definición de los conceptos estadísticos se identificó la posible necesidad de incorporar el concepto **Indicador** como elemento diferenciador entre los datos registrados y la información calculada por GeminiFy.

## Hipótesis

Un Indicador representaría una medida calculada a partir de uno o varios datos del sistema con el objetivo de facilitar el análisis y la toma de decisiones.

Bajo esta clasificación podrían considerarse Indicadores, entre otros:

- Nota Media.
- Ranking.
- Tendencia.
- Otros indicadores que puedan incorporarse en futuras versiones.

La Puntuación, al representar un valor registrado en una Participación, no tendría la consideración de Indicador.

## Beneficios potenciales

- Mejorar la precisión del lenguaje del dominio.
- Diferenciar claramente entre datos e información calculada.
- Facilitar la evolución del modelo estadístico.
- Proporcionar una base conceptual para futuros análisis avanzados.

## Riesgos

La incorporación de este concepto podría requerir una reorganización de la sección de Estadísticas del Glosario y del Modelo de Dominio.

## Próxima revisión

Durante la elaboración de `ModeloDominio.md`.

# BA-006 — Separación entre Componentes del Dominio y Componentes Técnicos

## Estado

Pendiente de evaluación.

## Origen

Redacción de `Glosario.md`.

## Descripción

Durante la elaboración del Glosario se identificó la conveniencia de diferenciar claramente los conceptos propios del dominio funcional de GeminiFy de los componentes técnicos utilizados para su implementación.

## Hipótesis

La documentación podría organizarse distinguiendo dos niveles conceptuales:

### Dominio

Conceptos propios del negocio.

Ejemplos:

- Canción
- Participación
- Estado
- Flag
- Lista
- Catálogo

### Sistema

Componentes técnicos responsables de la implementación.

Ejemplos:

- Base de Datos
- Motor de Reglas
- Motor de Estadísticas

## Beneficios potenciales

- Mejor separación de responsabilidades.
- Mayor claridad documental.
- Facilitar la evolución de la arquitectura.
- Reducir el acoplamiento entre negocio e implementación.

## Próxima revisión

Durante la elaboración de `Arquitectura.md`.

# BA-007 — Revisión del concepto "Historial"

## Estado

Pendiente de evaluación.

## Origen

Redacción de `Glosario.md` — Sección 5. Estadísticas.

## Descripción

Durante la definición del concepto Historial se observó que podría no pertenecer realmente al ámbito de las Estadísticas.

## Hipótesis

El Historial podría constituir un concepto transversal del dominio, al representar la evolución completa de una Canción a lo largo de su ciclo de vida.

En ese caso, dejaría de considerarse un concepto estadístico y pasaría a formar parte del modelo principal del dominio.

## Beneficios potenciales

- Mejor organización conceptual del Glosario.
- Mayor coherencia con el Modelo de Dominio.
- Separación clara entre información histórica e indicadores estadísticos.

## Riesgos

La reclasificación podría requerir reorganizar la estructura del Glosario.

## Próxima revisión

Durante la elaboración de `ModeloDominio.md`.

# BA-008 — Revisión del documento Visión

## Estado

Pendiente de evaluación.

## Origen

Evolución del Modelo de Dominio y aprobación de los ADR-014 y ADR-015.

## Descripción

Durante la definición del Modelo de Dominio se constató una evolución significativa en la comprensión del propósito y alcance de GeminiFy.

El proyecto ha evolucionado desde una solución orientada a la elaboración de listas musicales para entrenamientos de running hacia una plataforma de gestión inteligente del conocimiento musical, donde la Canción constituye el núcleo del dominio y el conocimiento acumulado se utiliza para generar propuestas de listas adaptadas a distintos objetivos.

Se considera necesario revisar el documento `Vision.md` para comprobar que refleja adecuadamente esta evolución conceptual.

## Aspectos a revisar

- Propósito principal de GeminiFy.
- Alcance funcional del sistema.
- Definición del problema que resuelve.
- Relación entre aprendizaje y generación de propuestas.
- Papel del running como primer caso de uso, sin limitar la evolución futura del sistema.
- Coherencia con los ADR-014 y ADR-015.

## Beneficios potenciales

- Mantener alineada la documentación estratégica con el Modelo de Dominio.
- Reflejar con mayor precisión la filosofía del proyecto.
- Evitar contradicciones entre la visión y las decisiones arquitectónicas.
- Facilitar la evolución futura de GeminiFy hacia nuevos escenarios de uso.

## Riesgos

Una revisión prematura podría provocar nuevas modificaciones mientras el Modelo de Dominio y la Arquitectura aún están en evolución.

## Próxima revisión

Una vez finalizados `ModeloDominio.md` y `Arquitectura.md`, antes de declarar estable la versión 1.0 de la documentación funcional.

# BA-009 — Definición de la Política de Canonización

## Estado

Pendiente.

## Descripción

Revisar y ampliar las reglas de canonización del catálogo para contemplar todos los escenarios posibles.

Entre otros:

- Versiones acústicas.
- Versiones sinfónicas.
- Versiones electrónicas.
- Mashups.
- Medleys.
- Regrabaciones oficiales.
- Versiones censuradas.
- Versiones internacionales.
- Versiones en otros idiomas.
- Reinterpretaciones del propio artista.

## Objetivo

Disponer de una política completa que permita resolver automáticamente cualquier proceso de consolidación futura.

# BA-010 — Incorporación del concepto "Canonización" al Glosario

## Estado

Pendiente.

## Origen

Definición del proceso de canonización del catálogo durante el diseño del Modelo de Dominio y aprobación del ADR-017.

## Descripción

Se ha identificado el concepto "Canonización" como un término propio del dominio de GeminiFy.

Una vez estabilizado el Modelo de Dominio y las reglas de consolidación, deberá incorporarse al Glosario con una definición formal que describa el proceso mediante el cual GeminiFy selecciona la representación canónica de una Canción cuando existen varias alternativas.

## Objetivo

Mantener el Glosario alineado con la evolución del Modelo de Dominio, incorporando únicamente conceptos cuya definición haya alcanzado un grado suficiente de estabilidad.

## Dependencias

- ADR-017 — Canonización del Catálogo Musical.
- ModeloDominio.md.
- ReglasNegocio.md.

## Próxima revisión

Al finalizar la primera versión del Modelo de Dominio.

