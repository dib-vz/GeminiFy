
# GeminiFy

# Glosario

**Versión:** 1.0  
**Estado:** Activo  
**Última actualización:** 15/07/2026

---

# Introducción

Este documento recoge las definiciones oficiales de todos los conceptos utilizados en GeminiFy.

Su objetivo es establecer un lenguaje común para la documentación, la arquitectura, el desarrollo y la interfaz de usuario, evitando ambigüedades y garantizando que cada término tenga un único significado dentro del proyecto.

Las definiciones incluidas en este documento constituyen la referencia oficial del dominio funcional de GeminiFy.

---

# Objetivos

- Definir el significado oficial de cada concepto del negocio.
- Establecer un lenguaje común para todo el proyecto.
- Evitar ambigüedades terminológicas.
- Facilitar la comprensión de la arquitectura y del modelo de dominio.
- Servir como documento de referencia para el resto de la documentación.

---

# Reglas del documento

1. Cada término se definirá una única vez.
2. Las definiciones deberán ser breves, claras y precisas.
3. Un término podrá referenciar a otros términos definidos en este mismo documento.
4. Las reglas de negocio no se incluirán en el Glosario.
5. Los atributos de las entidades se documentarán en **ModeloDominio.md**.
6. Las decisiones de arquitectura se documentarán exclusivamente en **ADR.md**.
7. Este documento constituye la referencia oficial del vocabulario de GeminiFy.

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

## 3. Automatización

- Función
- Regla
- Acción
- Evento
- Auditoría

## 4. Estadísticas

- Puntuación
- Nota Media
- Ranking
- Tendencia
- Historial
- Consolidación

## 5. Sistema

- Importación
- Exportación
- Catálogo Musical
- Base de Datos
- Motor de Reglas
- Motor de Estadísticas

# 1. Conceptos Fundamentales

## Catálogo

Conjunto de todas las Canciones gestionadas por GeminiFy.

El Catálogo constituye el universo musical del sistema y representa la colección completa de canciones conocidas por la aplicación, independientemente de su estado, número de participaciones o clasificación.

Una Canción pertenece siempre a un único Catálogo.

---

## Canción

Entidad principal del modelo de negocio que representa una obra musical única dentro del Catálogo.

Una Canción posee identidad propia y permanente durante todo su ciclo de vida.

Una Canción puede existir aunque nunca haya participado en ninguna Lista.

---

## Artista

Persona, grupo musical o formación artística responsable de la interpretación principal de una Canción.

Un Artista puede estar asociado a una o varias Canciones.

---

## Lista

Conjunto ordenado de Canciones proporcionado como entrada al sistema para su proceso de consolidación.

Una Lista representa una fotografía del catálogo musical en un instante determinado y constituye el origen de las futuras Participaciones.

Por sí misma, una Lista no modifica el estado del sistema.

---

## Participación

Registro histórico generado por GeminiFy como resultado del proceso de consolidación de una Lista.

Una Participación representa la presencia de una Canción en una Lista concreta y almacena toda la información correspondiente a esa aparición, incluyendo la Puntuación obtenida y cualquier otro dato asociado a dicha participación.

Una Canción puede tener cero, una o muchas Participaciones.


