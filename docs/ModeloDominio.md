# GeminiFy

# Modelo de Dominio

**Versión:** 1.0
**Estado:** Activo  
**Última actualización:** 19/07/2026

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

# Visión Conceptual del Dominio (BA-015)

Antes de profundizar en la definición técnica y detallada de cada componente, es imprescindible comprender la topología del dominio de GeminiFy. La plataforma no está diseñada como un reproductor, sino como un **Motor de Aprendizaje Musical**.

El núcleo absoluto de nuestro ecosistema es la **Canción**. Una canción no vive aislada; está ligada intrínsecamente a un **Artista**. El sistema adquiere conocimiento mediante el procesamiento de **Listas** de entrenamiento. Cuando una Lista es consolidada, el sistema no guarda la lista como un bloque rígido, sino que la descompone en **Participaciones** atómicas e inmutables. 

Cada Participación asocia una Canción con una puntuación concreta recibida en ese evento. El conjunto acumulado de estas participaciones da forma al **Historial (o ciclo de vida)** de la canción, provocando que el **Catálogo** recalcule sus indicadores y actualice de forma dinámica el **Estado** de la canción (Activa en Legiones, en Observación en Cuartel, o Protegida/Retirada en Cementerio).

### Diagrama de Relaciones del Dominio

```mermaid
classDiagram
    direction LR
    class Artista {
        +String Nombre
    }
    class Canción {
        +GEM_ID id
        +String Titulo
        +SongStatus Estado
        +List~Tag~ Tags
        +List~Flag~ Flags
        +recalcularIndicadores()
        +obtenerUltimaParticipación() Participación
    }
    class Participación {
        +GEM_ID id_lista
        +Integer Orden
        +Decimal Puntuacion
        +DateTime Fecha
    }
    class Lista {
        +GEM_ID id
        +String Tipo
        +DateTime FechaConsolidacion
    }

    Artista "1" --> "0..*" Canción : Interpreta
    Canción "1" *-- "0..*" Participación : Posee en su Historial
    Lista "1" *-- "1..*" Participación : Contiene
    Canción ..> Participación : Consulta Última Participación

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

---

## 1. Principios del Modelo

### 1.1 Principios generales

### 1.2 La Canción como entidad central (ADR-014)

### 1.3 Organización del modelo (ADR-015)

### 1.4 Responsabilidad única

### 1.5 Identidad

### 1.6 Integridad

### 1.7 Evolución

### 1.8 Criterio de entidad

### 1.9 Resolución de ambigüedades

---

## 2. Entidad Central

### 2.1 Canción

### 2.2 Artista

### 2.3 Lista

### 2.4 Participación

---

## 3. Clasificación

### 3.1 Estado

### 3.2 Flag

### 3.3 Tag

---

## 4. Información Estadística

### 4.1 Puntuación

### 4.2 Nota Media

### 4.3 Indicadores

---

## 5. Relaciones del Modelo

---

## 6. Restricciones del Modelo

---

## 7. Información Derivada

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
- Interpretación canónica.

La interpretación canónica representa la versión de referencia seleccionada por GeminiFy para identificar una Canción dentro del Catálogo.

Su determinación se realiza mediante las reglas de canonización definidas por las Reglas de Negocio y el ADR-017.

Una interpretación realizada por un artista diferente constituye una Canción distinta.

Las colaboraciones únicamente generarán una nueva Canción cuando den lugar a una obra inédita.

Las colaboraciones realizadas sobre una Canción previamente existente no generarán una nueva identidad, salvo decisión expresa del usuario.

La selección de la versión definitiva que formará parte del Catálogo se rige por las reglas de canonización definidas en el ADR-017.

---

### Relaciones

La Canción constituye el núcleo del Modelo de Dominio y mantiene relaciones con los siguientes conceptos:

- Artista.
- Participación.
- Estado.
- Flags.
- Tags.
- Estadísticas.

La relación entre una Canción y una Lista se establece exclusivamente mediante la entidad Participación.

Todas las relaciones del dominio se definen tomando la Canción como punto de referencia.

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

---

### Nota de Evolución Conceptual — Relación con el Historial (BA-002)
- Se extingue definitivamente el término heredado del Excel "Último Combate".
- Se introduce el concepto de **Última Participación** como una relación dinámica y derivada de la entidad `Canción`. 
- **Definición funcional:** Representa la referencia directa a la instancia de `Participación` más reciente en la línea temporal del `Historial` de dicha canción. A nivel de lectura, permite a la canción conocer instantáneamente la fecha (`FechaConsolidacion`) y el identificador de la lista (`id_lista`) de su última aparición sin necesidad de recalcular todo el histórico en operaciones de consulta rápidas.

---

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

## 2.3 Lista

### Descripción

La Lista representa una selección ordenada de Canciones creada para acompañar una sesión de entrenamiento con un objetivo determinado.

Cada Lista constituye el registro histórico de una decisión de selección musical, donde las Canciones han sido elegidas y ordenadas conforme a criterios técnicos, musicales y subjetivos con el propósito de maximizar su utilidad como estímulo durante una sesión concreta de running.

La Lista no constituye únicamente una colección de Canciones, sino el contexto en el que GeminiFy registra su utilización, evalúa su comportamiento y genera nuevo conocimiento sobre el Catálogo.

Cada utilización de una Canción dentro de una Lista incrementa el conocimiento del sistema y contribuye al aprendizaje necesario para mejorar futuras propuestas de reproducción.

La Lista constituye el principal mecanismo de generación de conocimiento de GeminiFy.

---

### Responsabilidad

La responsabilidad de la Lista consiste en representar una propuesta musical diseñada para un objetivo concreto de entrenamiento y conservar el contexto completo en el que las Canciones han sido utilizadas.

La Lista mantiene el orden de reproducción, registra las condiciones bajo las que fue creada y constituye el origen de la mayor parte de la información estadística y del aprendizaje generado por GeminiFy.

La Lista no almacena conocimiento propio de las Canciones, sino el contexto de utilización que permitirá al sistema aprender de la experiencia acumulada.

---

### Identidad

Cada Lista dispone de una identidad técnica única y permanente.

#### Identidad técnica

Cada Lista posee un identificador interno único, permanente e inmutable con el formato:

`LST-xxxxxx`

Este identificador constituye la identidad persistente de la entidad y será utilizado por todos los componentes internos del sistema.

#### Identificación funcional

Cada Lista representa una selección única de Canciones realizada para un propósito concreto.

Su identidad funcional viene determinada por el conjunto de información que describe su creación y utilización, pudiendo coexistir distintas Listas aunque contengan total o parcialmente las mismas Canciones.

---

### Relaciones

La Lista mantiene relaciones con las siguientes entidades del dominio:

- Participación.

Una Lista estará formada por una o varias Participaciones.

Cada Participación asociará una Canción concreta con una posición determinada dentro de la Lista.

La Lista no mantiene una relación directa con las Canciones, sino a través de las Participaciones, permitiendo conservar toda la información histórica asociada a cada utilización.

---

### Atributos

La Lista almacena exclusivamente información relacionada con su creación, finalidad y utilización.

Conceptualmente, sus atributos podrán clasificarse en las siguientes categorías:

- Identificación.
- Objetivo del entrenamiento.
- Configuración de generación.
- Información descriptiva.
- Metadatos.
- Auditoría.

La definición detallada de cada atributo se realizará en el Diccionario de Datos.

---

### Restricciones

La entidad Lista deberá cumplir las siguientes restricciones generales:

- Toda Lista deberá disponer de un identificador técnico único.
- Toda Lista deberá contener al menos una Participación.
- El orden de las Participaciones deberá ser único dentro de una misma Lista.
- Una misma Canción podrá aparecer en diferentes Listas.
- La eliminación de una Lista no podrá comprometer la integridad histórica del Catálogo.

---

### Información derivada

A partir de la información registrada sobre una Lista, GeminiFy podrá calcular información derivada, entre ella:

- Duración total.
- BPM medio.
- Distribución por géneros.
- Distribución por décadas.
- Distribución por estados.
- Número de Canciones.
- Indicadores de reutilización.
- Indicadores de diversidad.
- Cualquier otro indicador definido por las Reglas de Negocio.

La información derivada podrá recalcularse en cualquier momento y no forma parte de la identidad de la Lista.

## 2.4 Participación

### Descripción

La Participación representa el hecho de que una Canción forma parte de una Lista determinada.

Cada Participación constituye el registro individual de utilización de una Canción dentro de un contexto concreto de reproducción.

Además de establecer la relación entre la Canción y la Lista, la Participación almacena toda la información específica generada durante dicha utilización y constituye la unidad básica sobre la que GeminiFy registra experiencia y genera conocimiento.

La Participación representa un evento histórico único e irrepetible dentro del sistema.

---

### Responsabilidad

La responsabilidad de la Participación consiste en registrar cada utilización de una Canción dentro de una Lista y conservar toda la información específica generada durante dicha utilización.

La Participación conecta el conocimiento permanente almacenado por la Canción con el contexto concreto representado por la Lista.

Constituye el origen de la mayor parte de la información utilizada posteriormente para calcular estadísticas, tendencias e indicadores del Catálogo.

---

### Identidad

Cada Participación dispone de una identidad técnica única y permanente.

#### Identidad técnica

Cada Participación posee un identificador interno único con el formato:

`PAR-xxxxxx`

Este identificador constituye la identidad persistente de la entidad.

#### Identificación funcional

Cada Participación representa una utilización concreta de una Canción dentro de una Lista determinada.

Una misma Canción podrá participar múltiples veces en diferentes Listas.

Incluso podrá participar varias veces en una misma Lista siempre que las Reglas de Negocio lo permitan.

Cada Participación constituye un hecho independiente.

---

### Relaciones

La Participación mantiene relaciones con las siguientes entidades:

- Canción.
- Lista.

Cada Participación estará asociada obligatoriamente a una única Canción y a una única Lista.

Una Canción podrá tener múltiples Participaciones.

Una Lista estará formada por una o varias Participaciones.

La Participación constituye la única relación existente entre Canción y Lista.

---

### Atributos

La Participación almacena exclusivamente información correspondiente a una utilización concreta de una Canción.

Conceptualmente, sus atributos podrán clasificarse en:

- Identificación.
- Orden de reproducción.
- Valoración.
- Observaciones.
- Resultados.
- Metadatos.
- Auditoría.

La definición detallada de cada atributo se realizará en el Diccionario de Datos.

---

### Restricciones

La Participación deberá cumplir las siguientes restricciones generales:

- Toda Participación deberá disponer de un identificador técnico único.
- Toda Participación deberá estar asociada exactamente a una Canción.
- Toda Participación deberá estar asociada exactamente a una Lista.
- El orden de reproducción deberá ser único dentro de cada Lista.
- La eliminación de una Participación no podrá comprometer la coherencia histórica del sistema.

---

### Información derivada

A partir de las Participaciones registradas, GeminiFy podrá calcular información derivada para Canciones, Listas y Artistas.

La Participación constituye la principal fuente de información utilizada para generar conocimiento dentro del sistema.

La información derivada no forma parte de la identidad de la Participación y podrá recalcularse en cualquier momento.

---

# 3. Clasificación

La Clasificación agrupa los conceptos utilizados para organizar, categorizar y gobernar el ciclo de vida de las Canciones dentro del Catálogo. Ninguno de estos elementos posee identidad propia independiente de la Canción a la que califican.

---

## 3.1 Estado

### Descripción

El Estado define la situación actual de una Canción dentro de su ciclo de vida en GeminiFy.

Representa una condición mutuamente excluyente que determina cómo el sistema interactúa con la Canción y si esta es elegible para futuras Listas. Los Estados sustituyen conceptualmente a las antiguas pestañas de gestión operativa.

---

### Restricciones

- Toda Canción deberá tener un único Estado asignado en cualquier momento.
- Los Estados principales definidos por el dominio son: Activa (antiguas Legiones), Inactiva (antiguo Cementerio) y Observación (antiguo Cuartel).
- Las transiciones de Estado estarán gobernadas estrictamente por el Motor de Reglas de Negocio.
- El Estado Activa indica que la Canción es elegible para la generación de Listas.
- El Estado Inactiva indica que la Canción ha sido retirada del ciclo de selección, conservando su historial intacto.

---

## 3.2 Flag

### Descripción

Las Flags son marcadores binarios o etiquetas de control operativo asignadas a una Canción para forzar o alterar su comportamiento estándar dentro del sistema.

---

### Restricciones

- Una Canción podrá tener cero, una o múltiples Flags simultáneamente.
- Las Flags son independientes del Estado de la Canción.
- Actúan como modificadores de máxima prioridad sobre las reglas estadísticas (por ejemplo, una Flag de VETO impide que una Canción entre en una Lista, independientemente de su Nota Media).

---

## 3.3 Tag

### Descripción

Los Tags son metadatos descriptivos que permiten agrupar y filtrar Canciones basándose en características musicales o contextuales (por ejemplo: Género, Década, Ritmo).

---

### Restricciones

- Los Tags no definen el ciclo de vida de la Canción, sino su taxonomía musical.
- Son acumulables (una Canción puede pertenecer a varios Tags simultáneamente).
- Constituyen variables fundamentales en la configuración y generación de las Listas.

---

# 4. Información Estadística

La información estadística representa el rendimiento empírico de las Canciones y el conocimiento acumulado por el sistema. Constituye siempre el resultado matemático del historial de Participaciones.

---

## 4.1 Puntuación

### Descripción

La Puntuación es la evaluación numérica otorgada a una Canción durante una Participación específica en una Lista.

---

### Restricciones

- Es un atributo exclusivo de la entidad Participación, no de la Canción.
- Una vez consolidada, la Puntuación es inmutable y representa el rendimiento exacto de la Canción en ese contexto espacio-temporal.
- Su formato es numérico decimal con precisión de dos decimales.

---

## 4.2 Nota Media

### Descripción

La Nota Media es el indicador principal de rendimiento histórico de una Canción dentro del Catálogo.

---

### Restricciones

- Es un valor estrictamente derivado.
- No se almacena como un atributo fijo editable, sino que se calcula dinámicamente promediando todas las Puntuaciones históricas vinculadas a la identidad de la Canción.
- Constituye el factor clave para las transiciones automáticas de Estado.

---

## 4.3 Indicadores

### Descripción

Los Indicadores son el conjunto de métricas secundarias derivadas de las interacciones históricas de la Canción con el sistema a lo largo del tiempo.

---

### Restricciones

- Incluyen el Contador de Participaciones (número total de Listas en las que ha aparecido).
- Incluyen la Última Reproducción (fecha de la Participación más reciente, crucial para evitar la fatiga y sobreexposición).
- Se recalculan tras cada proceso de consolidación de Listas.

---

# 5. Relaciones del Modelo

La red conceptual de GeminiFy se vertebra a través de las siguientes relaciones fundamentales:

- **Canción - Artista (N:M):** Una Canción deberá estar interpretada por al menos un Artista. Un Artista podrá estar vinculado a múltiples Canciones.
- **Canción - Estado (1:1):** Una Canción se encontrará exactamente en un único Estado en un momento dado.
- **Lista - Participación (1:N):** Una Lista estará compuesta por una o más Participaciones ordenadas de forma secuencial.
- **Canción - Participación (1:N):** Una Canción podrá registrar múltiples Participaciones a lo largo de su historia.
- **Participación como Nexo:** La Participación actúa como la entidad intermedia inmutable que asocia una Lista (el contexto) con una Canción (el elemento) en una posición (orden numérico) y con un resultado (puntuación) específicos.

---

# 6. Restricciones del Modelo

Para garantizar la integridad y coherencia del sistema, el dominio obedece a las siguientes reglas invariables:

- **Inmutabilidad del Histórico:** Una vez consolidada, una Participación (y su Puntuación) no podrá ser alterada ni eliminada. Constituye un hecho histórico.
- **Supremacía del Cálculo (Single Source of Truth):** Ningún atributo estadístico (Nota Media, Contador) podrá existir desacoplado de sus eventos de origen. Todo cálculo matemático provendrá directamente del sumatorio de las Participaciones.
- **Estabilidad de la Identidad:** La evolución musical, los cambios de nombre artístico o las recategorizaciones de género jamás alterarán la identidad técnica interna (`GEM-xxxxxx`, `ART-xxxxxx`).
- **Precedencia de Retiro:** Las Canciones en Estado Inactiva gozarán de protección. Sus indicadores estadísticos no forzarán promociones automáticas a Estado Activa si fueron retiradas previamente.
- **Aislamiento de la Lista:** La eliminación de una Lista no borrará el conocimiento (las Participaciones) generado por la misma, garantizando que la experiencia de la IA persista aunque se depuren registros organizativos.

---

# 7. Información Derivada

La Información Derivada conforma el conocimiento avanzado e inteligencia de GeminiFy. Son proyecciones abstractas que el sistema construye sumando metadatos (Tags, Flags), eventos empíricos (Participaciones, Listas) e Indicadores.

Incluye, entre otros:

- **Tendencia Musical:** Análisis de la evolución de la Nota Media en las últimas participaciones de una Canción para evaluar su rendimiento al alza o a la baja.
- **Afinidad de Listas:** Identificación de patrones empíricos sobre qué Tags (Géneros, BPMs) funcionan mejor bajo qué objetivos de entrenamiento.
- **Fatiga del Catálogo:** Detección automática de la sobreutilización de determinadas Canciones o Artistas basándose en la concentración temporal de sus últimas reproducciones.

La Información Derivada no se almacena permanentemente como entidad; se consulta, se computa a través del Motor de Estadísticas y se actualiza constantemente para asegurar que las decisiones del sistema utilicen siempre los datos más recientes y consolidados.

---

## Estructura Avanzada de Información (BA-005 y BA-007)

### El Historial como Concepto Transversal (BA-007)
El **Historial** deja de ser considerado un mero reporte estadístico secundario. Se define formalmente como un concepto transversal y estructural del Dominio de GeminiFy. Representa la traza cronológica completa e inmutable de la evolución de una `Canción` a lo largo de su ciclo de vida dentro del sistema. Se compone del conjunto indexado de todas sus `Participaciones`. Cualquier cálculo posterior del sistema (cambios de estado, notas o clasificaciones) se deriva obligatoriamente de la lectura de este historial.

### Separación entre Datos e Indicadores Calculados (BA-005)
Para garantizar la escalabilidad del sistema, se establece una distinción taxonómica estricta:
1. **Dato de Negocio (Puntuación):** Es la nota individual e inmutable registrada en una `Participación` específica dentro de una lista de entrada. No es un indicador, sino una muestra atómica de información.
2. **Indicadores (Información Calculada):** Son métricas complejas generadas mediante funciones puras a partir del procesamiento del `Historial`. Tienen como objetivo la toma de decisiones y la explotación del conocimiento. Los indicadores oficiales de la v1.0 son:
   - **Nota Media (AverageScore):** Media aritmética de las puntuaciones del historial.
   - **Ranking:** Posición relativa de la canción en el catálogo basada en su rendimiento.
   - **Tendencia:** Vector de evolución del rendimiento en las últimas participaciones.
