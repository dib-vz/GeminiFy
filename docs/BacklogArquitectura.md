## Observaciones pendientes

### OBS-001 — Consolidación como posible Entidad del Dominio

Durante la elaboración del Glosario se identificó que una Consolidación podría constituir una entidad propia del dominio, al disponer de identidad, atributos y trazabilidad.

Esta propuesta deberá evaluarse durante el diseño del Modelo de Dominio.

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
