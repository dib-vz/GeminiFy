# GeminiFy

# Architectural Decision Records (ADR)

**Versión:** 1.0  
**Estado:** Activo  
**Última actualización:** 15/07/2026

---

# Introducción

Este documento recoge todas las Decisiones de Arquitectura (Architectural Decision Records, ADR) adoptadas durante el diseño, desarrollo y evolución de GeminiFy.

Su finalidad es preservar el conocimiento del proyecto, documentar el razonamiento detrás de cada decisión y garantizar la coherencia de la arquitectura a lo largo del tiempo.

Los ADR constituyen la referencia oficial sobre la arquitectura del sistema y prevalecen sobre cualquier otra documentación cuando exista una discrepancia.

---

# Objetivos

- Documentar todas las decisiones de arquitectura.
- Justificar cada decisión adoptada.
- Mantener un historial completo de la evolución del sistema.
- Facilitar el mantenimiento y la evolución futura de GeminiFy.
- Servir como guía para cualquier desarrollador que participe en el proyecto.

---

# Reglas del documento

1. Cada ADR tendrá un identificador único y secuencial.
2. Un ADR aprobado nunca se elimina.
3. Si una decisión cambia, se creará un nuevo ADR que sustituirá al anterior.
4. Todo ADR deberá incluir su motivación y sus consecuencias.
5. Los ADR forman parte de la documentación oficial del proyecto.
6. Ningún cambio de arquitectura podrá implementarse sin su correspondiente ADR.

---

# Estados de un ADR

| Estado | Significado |
|---------|-------------|
| 🟡 Propuesto | Pendiente de revisión o aprobación. |
| 🟢 Aprobado | Forma parte oficial de la arquitectura de GeminiFy. |
| 🔵 Sustituido | Reemplazado por un ADR posterior. |
| ⚫ Obsoleto | Ya no resulta aplicable. |

---

# Índice

- ADR-000 — Convención de los ADR
- ADR-001 — Fuente única de datos
- ADR-002 — Participación
- ADR-003 — Modelo de Canción
- ADR-004 — Regla de Oro
- ADR-005 — Identificador Universal
- ADR-006 — Sistema de Flags
- ADR-007 — Flags y Tags
- ADR-008 — Ciclo de Vida
- ADR-009 — Modelo Conceptual
- ADR-010 — Arquitectura basada en Acciones
- ADR-011 — Arquitectura basada en Eventos
- ADR-012 — Arquitectura basada en Funciones

---

# ADR-000 — Convención de los ADR

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy adopta la metodología **Architectural Decision Records (ADR)** como mecanismo oficial para documentar todas las decisiones que afecten a la arquitectura del sistema.

## Motivación

La arquitectura de GeminiFy evolucionará con el tiempo. Mantener un registro estructurado de las decisiones permitirá comprender el contexto en el que fueron adoptadas, facilitará el mantenimiento y preservará el conocimiento del proyecto.

## Reglas

- Todos los ADR tendrán un identificador único y secuencial.
- Los ADR aprobados nunca se eliminarán.
- Si una decisión cambia, se generará un nuevo ADR que sustituirá al anterior.
- Cada ADR deberá indicar su estado.
- Cada ADR deberá incluir la motivación de la decisión.
- Cada ADR deberá describir las consecuencias de su adopción.
- Todo cambio arquitectónico relevante deberá quedar reflejado en este documento antes de su implementación.

## Consecuencias

Este documento pasa a ser la referencia oficial de todas las decisiones arquitectónicas de GeminiFy.

# ADR-001 — Fuente Única de Datos

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

SQLite se establece como la única fuente de verdad (*Single Source of Truth*) de GeminiFy.

Microsoft Excel deja de ser el repositorio principal de información y pasa a ser un formato de intercambio de datos mediante procesos de importación y exportación.

Toda la información persistente será almacenada y gestionada exclusivamente por la base de datos SQLite.

## Contexto

El proyecto GeminiFy nace como evolución de un sistema basado en Microsoft Excel.

Aunque dicho sistema ha demostrado ser funcional, presenta limitaciones inherentes relacionadas con la integridad de los datos, la trazabilidad, la escalabilidad y el mantenimiento.

Para superar estas limitaciones, se adopta una arquitectura donde el modelo de negocio queda completamente desacoplado del formato físico utilizado para intercambiar información.

## Motivación

Los principales motivos para adoptar esta decisión son:

- Disponer de una única fuente oficial de información.
- Evitar duplicidades e inconsistencias.
- Desacoplar el modelo de negocio del formato Excel.
- Facilitar la evolución futura del sistema.
- Mejorar el rendimiento y la escalabilidad.
- Permitir auditoría completa de todas las operaciones.
- Simplificar la implementación de reglas de negocio.

## Alternativas consideradas

### Mantener Excel como base de datos

Descartada por sus limitaciones en integridad, concurrencia, trazabilidad y automatización.

### Mantener Excel sincronizado con SQLite

Descartada por introducir duplicidad de información y riesgo de inconsistencias entre ambas fuentes.

## Consecuencias

Como consecuencia de esta decisión:

- SQLite pasa a ser la única fuente persistente de datos.
- Excel deja de contener información maestra.
- La Lista Maestra será generada automáticamente por GeminiFy.
- Todas las operaciones se realizarán sobre SQLite.
- Los procesos de importación leerán archivos Excel y listas de entrada para incorporarlos al sistema.
- Los procesos de exportación generarán automáticamente los archivos Excel compatibles con el formato oficial del proyecto.

## Impacto

Esta decisión afecta a toda la arquitectura de GeminiFy y constituye el principio fundamental sobre el que se construirá el resto del sistema.

# ADR-002 — Sustitución del concepto Batalla por Participación

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy elimina definitivamente el concepto **Batalla** heredado del modelo Excel y adopta el concepto **Participación** como entidad oficial del dominio.

Una Participación representa la aparición de una Canción dentro de una Lista determinada.

Una Participación constituye un hecho histórico y almacena toda la información correspondiente a esa aparición concreta.

## Contexto

El sistema original utilizaba el término "Batalla" para representar cada registro asociado a una canción dentro de una lista.

Durante el diseño de GeminiFy se concluyó que dicho término no representa correctamente la naturaleza del dato y dificulta la comprensión del modelo de negocio.

El objetivo es utilizar una terminología basada en el dominio funcional y no en la nomenclatura heredada del archivo Excel.

## Motivación

Los principales motivos para adoptar esta decisión son:

- Utilizar un lenguaje más natural y comprensible.
- Describir correctamente el significado de la entidad.
- Facilitar el mantenimiento del sistema.
- Reducir ambigüedades durante el desarrollo.
- Independizar la arquitectura del diseño histórico del Excel.

## Definición

Una Participación representa la relación existente entre una Canción y una Lista.

Cada Participación pertenece exactamente a:

- una Canción;
- una Lista.

Una Canción puede tener cero, una o muchas Participaciones.

Una Lista contiene una o muchas Participaciones.

## Responsabilidades

La entidad Participación almacenará exclusivamente información correspondiente a esa aparición concreta.

Entre otra:

- Nota obtenida.
- Posición.
- Fecha.
- Tipo de lista.
- Orden de reproducción.
- Datos específicos de esa participación.

Nunca almacenará información permanente de la Canción.

## Alternativas consideradas

### Mantener el término Batalla

Descartada por inducir a confusión y no representar correctamente el dominio del negocio.

### Utilizar Registro

Descartada por resultar demasiado genérico.

### Utilizar Resultado

Descartada porque una Participación contiene más información que un simple resultado.

## Consecuencias

Como consecuencia de esta decisión:

- El término Batalla desaparece completamente de GeminiFy.
- Toda la documentación utilizará exclusivamente el término Participación.
- Todo el código utilizará el concepto Participación.
- La arquitectura quedará alineada con el lenguaje del negocio.

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Arquitectura.
- Código.
- Documentación.
- Auditoría.
- Motor de reglas.
- Motor de estadísticas.
