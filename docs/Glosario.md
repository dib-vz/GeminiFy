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


