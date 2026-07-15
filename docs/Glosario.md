# GeminiFy

# Glosario

**Versión:** 1.0  
**Estado:** Activo  
**Última actualización:** 15/07/2026

---

# Introducción

El Glosario recoge las definiciones oficiales de los conceptos utilizados en GeminiFy.

Su finalidad es establecer un lenguaje común para toda la documentación, la arquitectura, el desarrollo y la interfaz de usuario, garantizando que cada término tenga un único significado dentro del proyecto.

Las definiciones incluidas en este documento constituyen la referencia oficial del vocabulario de GeminiFy.

---

# Objetivos

- Establecer un lenguaje común para todo el proyecto.
- Definir el significado oficial de cada concepto del dominio.
- Evitar ambigüedades terminológicas.
- Facilitar la comprensión de la documentación.
- Servir de referencia para el Modelo de Dominio, las Reglas de Negocio, la Arquitectura y el desarrollo del software.

---

# Criterios del documento

1. Cada término se definirá una única vez.
2. Las definiciones deberán ser breves, claras y precisas.
3. Cada definición responderá únicamente a la pregunta **"¿Qué es...?"**.
4. El Glosario describirá conceptos, no reglas de negocio.
5. El Glosario no describirá atributos de las entidades.
6. El Glosario no incluirá decisiones de arquitectura.
7. Las definiciones podrán referenciar otros términos definidos en este mismo documento.
8. Los términos se organizarán por áreas funcionales y no por orden alfabético.
9. Toda la documentación de GeminiFy utilizará la terminología definida en este documento.
10. Este documento constituye la referencia oficial del vocabulario del proyecto.

---

# Índice

## 1. Conceptos Fundamentales

- Catálogo
- Canción
- Artista
- Lista
- Participación

## 2. Organización

- Estado
- Flag
- Tag

## 3. Procesos

- Consolidación
- Importación
- Exportación

## 4. Automatización

- Función
- Regla
- Acción
- Evento
- Auditoría

## 5. Estadísticas

- Puntuación
- Nota Media
- Ranking
- Tendencia
- Historial

## 6. Sistema

- Base de Datos
- Motor de Reglas
- Motor de Estadísticas

# 1. Conceptos Fundamentales

Los conceptos fundamentales constituyen el núcleo del modelo de negocio de GeminiFy.

Representan las entidades principales sobre las que se construye el resto del sistema y definen el lenguaje básico utilizado en toda la documentación del proyecto.

---

## GeminiFy

GeminiFy es un sistema de gestión inteligente de un catálogo musical diseñado para construir, mantener y evolucionar listas de reproducción adaptadas a objetivos específicos.

El proyecto nace de la necesidad de crear listas de reproducción optimizadas para entrenamientos de running, donde las características de las canciones deben ajustarse a las exigencias de cada sesión y a las preferencias del usuario.

GeminiFy transforma un proceso inicialmente manual, basado en hojas de cálculo y asistido por inteligencia artificial, en un sistema capaz de organizar el catálogo musical, conservar el historial de participaciones, aplicar reglas de negocio, automatizar procesos y ofrecer propuestas fundamentadas para la creación de nuevas listas de reproducción.

Aunque su origen está ligado al running, su arquitectura está diseñada para evolucionar hacia un sistema flexible, extensible e independiente del caso de uso inicial.

---

## Catálogo

Conjunto de todas las Canciones registradas y gestionadas por GeminiFy.

El Catálogo constituye el universo musical del sistema y representa la colección completa de canciones conocidas, independientemente de su estado, historial o clasificación.

---

## Canción

Obra musical única registrada en el Catálogo.

La Canción constituye la entidad principal del modelo de negocio y mantiene su identidad durante todo su ciclo de vida, independientemente de sus Participaciones, Estado, Flags o Tags.

---

## Artista

Persona, grupo musical o formación artística responsable de la interpretación principal de una Canción.

Un Artista puede estar asociado a una o varias Canciones del Catálogo.

---

## Lista

Colección ordenada de Canciones utilizada como entrada para un proceso de Consolidación.

Una Lista representa una selección musical correspondiente a un momento determinado y constituye el origen de las futuras Participaciones.

---

## Participación

Registro histórico generado por GeminiFy como resultado de la Consolidación de una Lista.

Cada Participación representa la presencia de una Canción en una Lista concreta y constituye la unidad básica del historial musical del sistema.

# 2. Organización

Los conceptos de organización permiten clasificar, identificar y gestionar las Canciones dentro del Catálogo.

Estos conceptos no modifican la identidad de una Canción, sino que facilitan su organización, seguimiento y administración durante su ciclo de vida.

---

## Estado

Condición que refleja la situación funcional de una Canción dentro del Catálogo en un momento determinado.

Toda Canción debe encontrarse en un único Estado, el cual determina su posición dentro de su ciclo de vida.

Los Estados son mutuamente excluyentes.

---

## Flag

Marca o indicador utilizado para identificar características, condiciones o situaciones específicas de una Canción.

Una Canción puede tener ninguna, una o varias Flags simultáneamente.

Las Flags son independientes del Estado y pueden asignarse o retirarse sin modificar el ciclo de vida de la Canción.

---

## Tag

Etiqueta utilizada para clasificar y agrupar Canciones según criterios definidos por el usuario o por el sistema.

Una Canción puede estar asociada a ninguno, uno o varios Tags de forma simultánea.

Los Tags tienen una finalidad organizativa y no afectan al comportamiento funcional de la Canción.

# 3. Procesos

Los procesos representan el conjunto de operaciones mediante las cuales GeminiFy incorpora, transforma, actualiza o utiliza el conocimiento almacenado en el Catálogo.

Cada proceso persigue un objetivo específico y puede implicar la creación, modificación, análisis o explotación de la información gestionada por el sistema.

---

## Propuesta de Lista

Proceso mediante el cual GeminiFy analiza el Catálogo y genera una propuesta de Lista adaptada a los criterios, objetivos y restricciones definidos por el usuario.

La propuesta se construye aplicando el conocimiento acumulado del sistema, las Reglas de Negocio, las estadísticas disponibles y las preferencias configuradas, con el objetivo de ofrecer una selección musical coherente con el propósito solicitado.

---

## Consolidación

Proceso mediante el cual GeminiFy incorpora al Catálogo la información procedente de una Lista.

Como resultado de una Consolidación, el sistema genera las Participaciones correspondientes, actualiza el conocimiento asociado a las Canciones y ejecuta las Reglas de Negocio que sean aplicables.

---

## Importación

Proceso mediante el cual GeminiFy incorpora información procedente de fuentes externas.

La Importación permite integrar datos en el sistema garantizando su compatibilidad con el modelo de dominio y preservando la integridad del Catálogo.

---

## Exportación

Proceso mediante el cual GeminiFy genera información del Catálogo para su utilización por sistemas externos o por el propio usuario.

La Exportación puede realizarse en diferentes formatos, respetando siempre la estructura y consistencia de la información generada.

# 4. Automatización

Los conceptos de automatización definen el comportamiento de GeminiFy y permiten que el sistema responda de forma inteligente ante los distintos eventos que se producen durante su funcionamiento.

La automatización se basa en la aplicación de Reglas de Negocio que desencadenan Acciones mediante la ejecución de Funciones específicas.

---

## Evento

Suceso producido dentro o fuera de GeminiFy que puede desencadenar uno o varios procesos automáticos.

Un Evento representa el punto de inicio de la automatización y puede ser originado por una acción del usuario, por otro proceso del sistema o por una fuente externa.

---

## Regla

Condición lógica que determina el comportamiento de GeminiFy ante uno o varios Eventos.

Una Regla evalúa una situación concreta y establece qué Acciones deben ejecutarse cuando se cumplen las condiciones definidas.

---

## Acción

Operación ejecutada por GeminiFy como consecuencia de la aplicación de una Regla.

Una Acción representa un cambio, actualización o actuación concreta realizada por el sistema sobre el modelo de dominio.

---

## Función

Componente reutilizable que implementa una operación específica dentro de GeminiFy.

Las Funciones constituyen los bloques básicos de ejecución utilizados por las Acciones y pueden ser invocadas desde distintos procesos del sistema.

---

## Auditoría

Mecanismo mediante el cual GeminiFy registra y conserva la trazabilidad de las operaciones realizadas por el sistema.

La Auditoría permite conocer qué ocurrió, cuándo ocurrió, cómo ocurrió y cuál fue su resultado.




