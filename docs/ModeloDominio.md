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

# 1. Principios del Modelo

El Modelo de Dominio de GeminiFy representa el negocio desde una perspectiva conceptual, independiente de cualquier decisión tecnológica o de implementación.

Su finalidad es describir de forma precisa los conceptos fundamentales del sistema, las relaciones existentes entre ellos y las restricciones que gobiernan su comportamiento.

Todos los elementos del modelo deberán respetar los principios definidos en este apartado.

---

## 1.1 Independencia tecnológica

El Modelo de Dominio no estará condicionado por el diseño de la base de datos, el lenguaje de programación, la interfaz de usuario ni cualquier otra decisión técnica.

Las decisiones de implementación deberán adaptarse al Modelo de Dominio y nunca a la inversa.

---

## 1.2 La Canción como entidad central

De acuerdo con el ADR-014, la Canción constituye la entidad central de GeminiFy.

El resto de conceptos del dominio existen para describir, clasificar, relacionar, analizar o registrar información asociada a una Canción.

---

## 1.3 Organización del modelo

De acuerdo con el ADR-015, el Modelo de Dominio se estructura alrededor de la Canción.

Los diferentes conceptos del dominio se agrupan según la función que desempeñan respecto a ella, distinguiendo entre información asociada, clasificación, información estadística, relaciones, restricciones e información derivada.

---

## 1.4 Responsabilidad única

Cada concepto del dominio deberá representar una única responsabilidad claramente definida.

Un mismo concepto no deberá asumir funciones pertenecientes a otros elementos del modelo.

---

## 1.5 Identidad

Toda entidad del dominio deberá disponer de una identidad única y estable durante todo su ciclo de vida.

La identidad de una entidad será independiente de sus atributos y permanecerá inalterable aunque estos cambien.

---

## 1.6 Integridad

El Modelo de Dominio deberá garantizar la coherencia interna de la información.

No podrán existir relaciones, estados o atributos que contradigan las reglas definidas por el propio modelo o por las Reglas de Negocio.

---

## 1.7 Evolución

El Modelo de Dominio deberá diseñarse para facilitar la incorporación de nuevos conceptos sin comprometer la coherencia del sistema.

Las ampliaciones futuras deberán preservar los principios establecidos en este documento y mantener la compatibilidad conceptual siempre que sea posible.

---

## 1.8 Criterio de entidad

En GeminiFy, una entidad es un concepto del dominio que representa un elemento identificable sobre el que el sistema mantiene conocimiento a lo largo del tiempo.

Una entidad deberá cumplir las siguientes características:

- Disponer de una identidad única y estable.
- Representar un concepto con significado propio dentro del dominio.
- Mantener un ciclo de vida definido.
- Ser susceptible de almacenar o generar información relevante para el sistema.
- Poder establecer relaciones con otras entidades del dominio.

El hecho de que una entidad dependa de otras para su creación o existencia no impide que sea considerada una entidad.

La clasificación definitiva de cada concepto como entidad, objeto de valor, atributo o información derivada se realizará durante el desarrollo del Modelo de Dominio.
