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

---

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

---

## 1.9 Resolución de ambigüedades

El Modelo de Dominio de GeminiFy asume que la información procedente de fuentes externas puede presentar ambigüedades, inconsistencias o duplicidades.

Por este motivo, los atributos descriptivos de una entidad no constituyen por sí mismos un mecanismo fiable de identificación.

Toda entidad dispondrá de una identidad técnica única y permanente, mientras que la resolución de posibles ambigüedades entre entidades se realizará mediante los procesos de consolidación definidos por las Reglas de Negocio.

La consolidación será responsable de detectar posibles coincidencias, proponer alternativas y garantizar la integridad del Catálogo sin comprometer la estabilidad de las identidades internas del sistema.

# 2. Entidad Central

## 2.1 Canción

### Descripción

La Canción constituye la entidad central del Modelo de Dominio de GeminiFy y representa la unidad fundamental de conocimiento gestionada por el sistema.

Cada Canción identifica una interpretación musical única dentro del Catálogo y constituye el elemento sobre el que GeminiFy registra, organiza, analiza y mantiene toda la información necesaria para generar propuestas musicales adaptadas a los objetivos del usuario.

Una Canción puede participar en múltiples Listas a lo largo de su ciclo de vida, acumulando información histórica, estadística y de clasificación que permite al sistema incrementar progresivamente su conocimiento sobre ella.

La identidad de una Canción permanece invariable durante toda su existencia, con independencia de la evolución de sus atributos, clasificaciones, participaciones o indicadores estadísticos.

---

### Responsabilidad

La responsabilidad de la Canción consiste en representar una interpretación musical única dentro del Catálogo y actuar como núcleo sobre el que se organiza todo el conocimiento gestionado por GeminiFy.

La Canción concentra la información descriptiva, las relaciones con el resto de entidades, el historial de Participaciones, las clasificaciones, las estadísticas y cualquier otro dato necesario para apoyar los procesos de aprendizaje, consolidación y generación de propuestas de listas.

---

### Identidad

Cada Canción dispone de dos mecanismos de identificación:

#### Identidad técnica

Cada Canción posee un identificador interno único, permanente e inmutable con el formato:

`GEM-xxxxxx`

Este identificador constituye la identidad persistente de la entidad y será utilizado por todos los componentes internos del sistema.

#### Identidad de negocio

La identidad funcional de una Canción viene determinada por la combinación de:

- Título.
- Artista o conjunto de artistas que constituyen la interpretación original de la Canción.

Una interpretación realizada por un artista diferente constituye una Canción distinta.

Las colaboraciones únicamente generarán una nueva Canción cuando den lugar a una obra inédita.

Las colaboraciones realizadas sobre una Canción previamente existente no generarán una nueva identidad, salvo decisión expresa del usuario.

La selección de la versión definitiva que formará parte del Catálogo se rige por las reglas de canonización definidas en el ADR-017.

---

### Relaciones

La Canción constituye el núcleo del Modelo de Dominio y mantiene relaciones con los siguientes conceptos:

- Artista.
- Lista.
- Participación.
- Estado.
- Flags.
- Tags.
- Estadísticas.

Todas las relaciones del dominio se establecen tomando la Canción como punto de referencia.

---

### Atributos

La Canción almacena la información descriptiva necesaria para identificarla, clasificarla y utilizarla dentro de GeminiFy.

Los atributos concretos se definirán en el Diccionario de Datos.

De forma conceptual, podrán clasificarse en:

- Identificación.
- Información musical.
- Clasificación.
- Metadatos.
- Estadísticas.
- Auditoría.

---

### Restricciones

La entidad Canción deberá cumplir las siguientes restricciones generales:

- Toda Canción deberá poseer un identificador técnico único.
- Toda Canción deberá disponer de una identidad de negocio válida.
- No podrán coexistir dos Canciones con la misma identidad de negocio.
- Una Canción únicamente podrá encontrarse en un Estado cada vez.
- Las Flags son independientes del Estado y podrán coexistir entre sí.
- Las reglas de canonización determinarán la representación definitiva de cada Canción dentro del Catálogo.

---

### Información derivada

A partir de la información registrada sobre una Canción, GeminiFy podrá calcular información derivada, entre ella:

- Nota media.
- Tendencia.
- Número de participaciones.
- Historial de rendimiento.
- Indicadores de estabilidad.
- Indicadores de uso.
- Cualquier otro indicador definido por las Reglas de Negocio.

La información derivada no forma parte de la identidad de la Canción y podrá recalcularse en cualquier momento.

## 2.2 Artista

### Descripción

El Artista representa a la persona, grupo musical o entidad responsable de la interpretación de una o varias Canciones dentro del Catálogo de GeminiFy.

Su finalidad es identificar de forma única a los intérpretes de las Canciones, permitiendo establecer relaciones consistentes entre todas las interpretaciones registradas en el sistema.

Un Artista puede participar como intérprete principal o como colaborador en una o varias Canciones.

El nombre artístico constituye únicamente una característica descriptiva del intérprete y no determina su identidad dentro del sistema.

---

### Responsabilidad

La responsabilidad del Artista consiste en representar de forma única a cada intérprete del Catálogo y actuar como punto común de relación entre todas las Canciones en las que participa.

El Artista concentra exclusivamente la información propia del intérprete y no almacena información específica de las Canciones, la cual pertenece a la entidad Canción.

Asimismo, proporciona un punto estable de referencia para mantener la integridad de las relaciones entre Canciones e intérpretes a lo largo del tiempo.

---

### Identidad

Cada Artista dispone de una identidad técnica única y permanente.

#### Identidad técnica

Cada Artista posee un identificador interno único, permanente e inmutable con el formato:

`ART-xxxxxx`

Este identificador constituye la identidad persistente de la entidad y será utilizado por todos los componentes internos del sistema.

#### Identificación funcional

El nombre artístico constituye un atributo descriptivo del Artista y no garantiza por sí mismo su unicidad dentro del sistema.

Podrán existir diferentes Artistas con el mismo nombre artístico, así como un mismo Artista podrá modificar su nombre a lo largo de su trayectoria sin perder su identidad dentro de GeminiFy.

La detección y resolución de posibles ambigüedades o duplicidades entre Artistas se realizará mediante los procesos de consolidación definidos por las Reglas de Negocio.

La identidad técnica del Artista permanecerá invariable durante todo su ciclo de vida.

---

### Relaciones

El Artista mantiene relaciones con las siguientes entidades del dominio:

- Canción.

Un Artista puede interpretar ninguna, una o múltiples Canciones.

Toda Canción deberá estar asociada, al menos, a un Artista.

Las colaboraciones entre varios Artistas se representarán mediante la asociación de una misma Canción con todos los intérpretes participantes.

La forma definitiva de modelar esta relación podrá evolucionar en futuras versiones del sistema sin modificar el Modelo de Dominio.

---

### Atributos

El Artista almacena exclusivamente información propia del intérprete.

Conceptualmente, sus atributos podrán clasificarse en las siguientes categorías:

- Identificación.
- Información descriptiva.
- Clasificación.
- Metadatos.
- Auditoría.

La definición detallada de cada atributo se realizará en el Diccionario de Datos.

---

### Restricciones

La entidad Artista deberá cumplir las siguientes restricciones generales:

- Todo Artista deberá disponer de un identificador técnico único.
- Todo Artista podrá participar en ninguna, una o múltiples Canciones.
- Toda Canción deberá estar asociada al menos a un Artista.
- El nombre artístico no constituye un criterio de unicidad.
- La identidad de un Artista nunca podrá modificarse una vez creada.
- La eliminación de un Artista no podrá comprometer la integridad referencial del Catálogo.

---

### Información derivada

A partir de la información registrada sobre un Artista, GeminiFy podrá calcular información derivada, entre ella:

- Número de Canciones interpretadas.
- Número de Participaciones acumuladas.
- Puntuación media de sus Canciones.
- Distribución por géneros musicales.
- Distribución por décadas.
- Indicadores de utilización.
- Indicadores de rendimiento dentro del Catálogo.
- Cualquier otro indicador definido por las Reglas de Negocio.

La información derivada no forma parte de la identidad del Artista y podrá recalcularse en cualquier momento.
