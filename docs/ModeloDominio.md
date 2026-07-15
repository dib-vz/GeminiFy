# GeminiFy

# Modelo de Dominio

**Versión:** 1.0  
**Estado:** Activo  
**Última actualización:** 16/07/2026

---

# Introducción

El Modelo de Dominio describe la estructura conceptual de GeminiFy desde la perspectiva del negocio.

Su finalidad es identificar y definir las entidades, relaciones, restricciones y principios que conforman el núcleo funcional del sistema, proporcionando una representación independiente de cualquier decisión tecnológica o de implementación.

Este documento constituye la referencia principal para comprender cómo se organiza el conocimiento gestionado por GeminiFy y sirve de base para el diseño de la arquitectura, la base de datos, las reglas de negocio y el desarrollo de la aplicación.

---

# Objetivo

Establecer un modelo de dominio único, coherente y extensible que describa con precisión los conceptos fundamentales de GeminiFy y las relaciones existentes entre ellos.

El Modelo de Dominio debe garantizar que todas las decisiones funcionales y técnicas del proyecto se apoyen sobre una representación consistente del negocio.

---

# Alcance

Este documento incluye:

- Los principios que rigen el modelo de dominio.
- La definición de las entidades principales.
- La información asociada a cada entidad.
- Las relaciones existentes entre los diferentes conceptos.
- Las restricciones del dominio.
- La información derivada utilizada por GeminiFy.

Quedan fuera del alcance de este documento:

- La implementación técnica.
- El diseño físico de la base de datos.
- La definición de las reglas de negocio.
- La arquitectura software.
- Los detalles de la interfaz de usuario.

---

# Documentación relacionada

Este documento se complementa con la siguiente documentación oficial del proyecto:

- ADR
- Glosario
- Arquitectura
- Reglas de Negocio
- Diccionario de Datos
- Visión
- Roadmap

---

# Criterios

Para la elaboración de este documento se aplican los siguientes principios:

- El modelo representa el dominio del negocio, no la implementación técnica.
- La Canción constituye la entidad central del sistema (ADR-014).
- El modelo se organiza alrededor de la Canción (ADR-015).
- Cada concepto debe tener una única responsabilidad claramente definida.
- Se evitarán duplicidades entre documentos.
- Las relaciones deberán reflejar el funcionamiento real del dominio.
- La evolución del modelo deberá preservar la compatibilidad conceptual con las versiones anteriores siempre que sea posible.

---

# Índice

## 1. Principios del Modelo

### 1.1 Principios generales

### 1.2 La Canción como entidad central (ADR-014)

### 1.3 Organización del modelo (ADR-015)

---

## 2. Entidad Central

### 2.1 Canción

- Descripción
- Responsabilidad
- Identidad
- Relaciones
- Atributos
- Restricciones
- Información derivada

---

## 3. Información Asociada

### 3.1 Artista

- Descripción
- Responsabilidad
- Identidad
- Relaciones
- Atributos
- Restricciones

### 3.2 Lista

- Descripción
- Responsabilidad
- Identidad
- Relaciones
- Atributos
- Restricciones

### 3.3 Participación

- Descripción
- Responsabilidad
- Identidad
- Relaciones
- Atributos
- Restricciones

---

## 4. Clasificación

### 4.1 Estado

### 4.2 Flag

### 4.3 Tag

---

## 5. Información Estadística

### 5.1 Puntuación

### 5.2 Nota Media

### 5.3 Indicadores

---

## 6. Relaciones del Modelo

---

## 7. Restricciones del Modelo

---

## 8. Información Derivada
