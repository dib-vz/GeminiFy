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
- ADR-013 — Clasificación de los Componentes del Sistema
- ADR-014 — La Canción como entidad central del modelo de dominio

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

# ADR-003 — Modelo de Canción

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy establece la entidad **Canción** como el núcleo principal del modelo de negocio.

Una Canción representa una obra musical única dentro del catálogo del sistema y existe independientemente de sus participaciones.

La identidad de una Canción nunca dependerá de los resultados obtenidos, de su estado, de sus flags o de cualquier otro atributo derivado.

## Contexto

El modelo basado en Excel asociaba gran parte de la información de una canción a las filas de distintas hojas.

Durante el rediseño de GeminiFy se decidió separar completamente la identidad de una Canción de cualquier información histórica o calculada.

## Motivación

Los principales objetivos de esta decisión son:

- Normalizar el modelo de datos.
- Evitar duplicidades.
- Mantener una única representación de cada canción.
- Facilitar la reutilización de información.
- Separar datos permanentes de datos históricos.

## Definición

Una Canción representa una obra musical única dentro del catálogo de GeminiFy.

Una Canción puede existir aunque nunca haya participado en ninguna Lista.

Las Participaciones representan hechos históricos asociados a una Canción, pero nunca forman parte de su identidad.

## Atributos permanentes

Entre otros, una Canción podrá disponer de los siguientes atributos:

- Identificador GEM.
- Título.
- Artista.
- Duración.
- BPM.
- Género.
- Subgénero.
- Álbum.
- Año.
- Idioma.
- Fecha de alta.
- Estado del ciclo de vida.

La lista de atributos podrá ampliarse en futuras versiones sin alterar la identidad de la entidad.

## Atributos derivados

Los siguientes valores no forman parte de la información permanente de una Canción:

- Nota media.
- Número de participaciones.
- Mejor nota.
- Peor nota.
- Ranking.
- Tendencia.
- Índices estadísticos.

Estos valores serán calculados automáticamente por GeminiFy.

## Relaciones

Una Canción:

- pertenece al Catálogo;
- puede tener cero o muchas Participaciones;
- posee un único Estado;
- puede tener cero, uno o muchos Flags;
- puede tener cero, uno o muchos Tags.

## Alternativas consideradas

### Mantener el modelo heredado del Excel

Descartada por mezclar información permanente con información histórica.

## Consecuencias

Esta decisión convierte la entidad Canción en el eje central del modelo de negocio de GeminiFy.

Toda la información histórica, estadística o derivada se almacenará o calculará mediante entidades específicas.

## Impacto

Esta decisión afecta al modelo de datos completo y condiciona el diseño de todas las entidades relacionadas.

# ADR-004 — Regla de Oro del Modelo de Datos

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy no almacenará ningún atributo cuyo valor pueda obtenerse de forma determinista a partir de otros datos persistidos.

Únicamente se almacenarán los datos originales del negocio y aquellos necesarios para garantizar la integridad, la trazabilidad y el rendimiento del sistema.

## Contexto

En el modelo original basado en Excel existían numerosos valores calculados que se almacenaban junto con la información principal.

Este enfoque incrementa el riesgo de inconsistencias, dificulta el mantenimiento y obliga a sincronizar continuamente datos derivados.

Durante el diseño de GeminiFy se decide separar claramente los datos persistentes de los datos calculados.

## Motivación

Los principales objetivos de esta decisión son:

- Evitar la duplicidad de información.
- Garantizar la consistencia del modelo de datos.
- Reducir el riesgo de errores por desincronización.
- Simplificar la evolución del sistema.
- Facilitar la auditoría y la reconstrucción completa de la información.

## Definición

Se consideran **datos persistentes** aquellos que representan hechos del negocio y que no pueden reconstruirse automáticamente.

Se consideran **datos derivados** aquellos cuyo valor puede calcularse de forma determinista a partir de los datos persistentes.

GeminiFy almacenará únicamente los datos persistentes.

Los datos derivados serán calculados cuando sean necesarios o durante procesos específicos de actualización.

## Ejemplos

### Datos persistentes

- Canción.
- Artista.
- Participación.
- Lista.
- Fecha.
- Nota.
- Duración.
- BPM.
- Flags.
- Tags.
- Estado.

### Datos derivados

- Nota media.
- Número de participaciones.
- Ranking.
- Tendencia.
- Mejor nota.
- Peor nota.
- Tiempo en cada estado.
- Índices estadísticos.
- Posiciones históricas.

## Excepciones

Cuando el rendimiento del sistema lo requiera, GeminiFy podrá mantener información precalculada.

Estos datos deberán poder regenerarse completamente a partir de la información persistente y nunca constituirán la fuente oficial de información.

## Alternativas consideradas

### Almacenar todos los valores calculados

Descartada por incrementar la complejidad del sistema y aumentar el riesgo de inconsistencias.

## Consecuencias

La arquitectura de GeminiFy distinguirá claramente entre información persistente e información derivada.

Todo cálculo deberá poder reconstruirse utilizando únicamente los datos almacenados.

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Motor de estadísticas.
- Motor de reglas.
- Exportación.
- Auditoría.
- Rendimiento.
- Diseño de consultas.

# ADR-005 — Identificador Universal de Entidades

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

Todas las entidades persistentes de GeminiFy dispondrán de un identificador único con formato:

GEM-XXXXXX

Ejemplos:

- GEM-000001
- GEM-000002
- GEM-000003

Este identificador constituirá la identidad oficial de la entidad durante todo su ciclo de vida.

## Contexto

Durante el diseño del modelo de datos se evaluaron diferentes alternativas para identificar las entidades del sistema.

Se descartó utilizar identificadores dependientes de la tecnología (por ejemplo, claves enteras autoincrementales) como referencia funcional, ya que dificultan la auditoría, las migraciones y la interoperabilidad entre componentes.

## Motivación

Los principales objetivos son:

- Disponer de un identificador único, estable y permanente.
- Independizar la identidad de la implementación técnica.
- Facilitar la trazabilidad completa del sistema.
- Simplificar auditorías e importaciones.
- Evitar referencias basadas en posiciones físicas dentro de la base de datos.

## Definición

El identificador GEM:

- será único en todo el sistema;
- nunca cambiará;
- nunca será reutilizado;
- no contendrá información de negocio;
- será generado automáticamente por GeminiFy.

Los usuarios no podrán modificarlo.

## Alcance

El identificador GEM podrá utilizarse en cualquier entidad persistente del sistema.

Entre ellas:

- Canción.
- Artista.
- Lista.
- Participación.
- Tag.
- Flag.
- Regla.
- Acción.
- Evento.

## Alternativas consideradas

### Identificadores numéricos autoincrementales

Descartada por depender de la implementación física de la base de datos.

### Identificadores con prefijos por entidad

Ejemplos:

- SON-000001
- PAR-000001
- ART-000001

Descartada por aumentar la complejidad sin aportar ventajas funcionales relevantes.

## Consecuencias

Todo el sistema utilizará el identificador GEM como referencia oficial entre entidades.

Los identificadores internos de SQLite podrán existir por motivos técnicos, pero nunca formarán parte del modelo funcional ni serán visibles para el usuario.

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Relaciones entre entidades.
- Auditoría.
- Exportaciones.
- API.
- Interfaces de usuario.

# ADR-006 — Sistema de Flags

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy adopta un sistema de Flags como mecanismo estándar para modificar el comportamiento de las entidades sin alterar su identidad ni su ciclo de vida.

Los Flags constituyen marcas funcionales independientes del Estado de una entidad y podrán ser asignados o eliminados tanto por acciones del usuario como por reglas del sistema.

## Contexto

Inicialmente se planteó incorporar atributos específicos como VIP o VETO dentro de la entidad Canción.

Durante el diseño del modelo de negocio se concluyó que esta solución dificultaría la evolución del sistema, ya que cada nuevo comportamiento obligaría a modificar la estructura del modelo de datos.

## Motivación

Los objetivos principales son:

- Permitir la incorporación de nuevos comportamientos sin modificar la arquitectura.
- Separar el comportamiento de la identidad de las entidades.
- Facilitar la automatización mediante reglas.
- Permitir la intervención manual del usuario.
- Mejorar la escalabilidad del sistema.

## Definición

Un Flag representa una característica funcional que modifica el comportamiento de una entidad.

Un Flag:

- puede existir o no sobre una entidad;
- puede ser añadido o eliminado;
- puede ser gestionado por reglas o por el usuario;
- no modifica la identidad de la entidad;
- no modifica el Estado de la entidad.

Una entidad podrá tener simultáneamente cero, uno o múltiples Flags.

## Ejemplos

- VIP
- VETO
- FAVORITA
- DESCUBRIMIENTO
- PENDIENTE
- CLÁSICO

La lista de Flags podrá ampliarse sin modificar el modelo de datos.

## Alternativas consideradas

### Atributos específicos (VIP, VETO...)

Descartada por limitar la extensibilidad del sistema.

## Consecuencias

Los Flags pasan a formar parte del modelo funcional de GeminiFy.

Toda modificación de un Flag deberá realizarse mediante una Acción y quedará registrada en la Auditoría.

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Motor de reglas.
- Auditoría.
- Acciones.
- Interfaz de usuario.

# ADR-007 — Sistema de Tags

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy adopta un sistema de Tags para clasificar las entidades sin modificar su comportamiento funcional.

Los Tags constituyen un mecanismo de organización y búsqueda completamente independiente del sistema de Flags.

## Contexto

Durante el diseño del modelo de negocio se identificó la necesidad de diferenciar claramente entre las características que afectan al funcionamiento del sistema y aquellas cuyo único objetivo es clasificar o agrupar información.

## Motivación

Los objetivos principales son:

- Organizar el catálogo.
- Facilitar búsquedas y filtros.
- Agrupar entidades según criterios definidos por el usuario.
- Evitar utilizar Flags con fines exclusivamente organizativos.

## Definición

Un Tag representa una etiqueta descriptiva.

Los Tags:

- no modifican el comportamiento del sistema;
- no modifican el Estado;
- pueden ser creados por el usuario;
- pueden asignarse a múltiples entidades;
- una entidad puede disponer de cero, uno o muchos Tags.

## Ejemplos

- Running
- Rock Alternativo
- Energía Alta
- Favoritas 2026
- Verano
- Top 100

## Alternativas consideradas

### Utilizar únicamente Flags

Descartada por mezclar clasificación con comportamiento.

## Consecuencias

GeminiFy mantiene separados los conceptos de comportamiento (Flags) y clasificación (Tags).

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Motor de búsqueda.
- Filtros.
- Interfaz de usuario.

# ADR-008 — Ciclo de Vida de una Canción

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

Toda Canción perteneciente al Catálogo deberá encontrarse exactamente en un único Estado de su ciclo de vida.

Los Estados son mutuamente excluyentes y representan la situación funcional actual de la Canción dentro de GeminiFy.

## Contexto

El modelo heredado de Excel utilizaba distintas hojas (Cuartel, Legiones y Cementerio) para representar situaciones funcionales de las canciones.

Durante el diseño de GeminiFy se decidió sustituir este enfoque por un modelo basado en un único Estado asociado a cada Canción.

## Estados definidos

### INICIAL

Canción incorporada al catálogo que todavía no dispone de Participaciones.

### ACTIVA

Canción con una o más Participaciones y disponible para continuar participando.

### OBSERVACIÓN

Canción sometida a seguimiento especial por decisión del usuario o como consecuencia de las reglas del sistema.

### INACTIVA

Canción retirada del catálogo activo.

Podrá ser recuperada mediante las Acciones autorizadas por GeminiFy.

## Reglas de compatibilidad

- Una Canción solo puede tener un Estado.
- Una Canción sin Participaciones nunca podrá encontrarse en estado ACTIVA u OBSERVACIÓN.
- Una Canción con Participaciones no podrá permanecer en estado INICIAL.
- Las transiciones de Estado deberán respetar las reglas de negocio definidas por GeminiFy.
- Toda transición quedará registrada en la Auditoría.

## Motivación

Los principales objetivos son:

- Simplificar el modelo funcional.
- Eliminar la dependencia de la estructura del Excel.
- Representar correctamente el ciclo de vida de una Canción.
- Facilitar la aplicación automática de reglas.

## Alternativas consideradas

### Mantener las hojas del Excel como entidades independientes

Descartada por duplicar información y dificultar la evolución del sistema.

## Consecuencias

GeminiFy utilizará un único Estado para representar el ciclo de vida de cada Canción.

Las antiguas hojas del Excel pasarán a considerarse representaciones derivadas del Estado.

## Impacto

Esta decisión afecta a:

- Modelo de datos.
- Motor de reglas.
- Auditoría.
- Estadísticas.
- Exportación.
- Interfaz de usuario.

# ADR-009 — Modelo Conceptual del Dominio

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy adopta un modelo de dominio centrado en la entidad Canción, sobre la que se estructuran el resto de entidades y relaciones del sistema.

El modelo conceptual será independiente de cualquier implementación técnica y representará exclusivamente los conceptos del negocio.

## Contexto

El modelo heredado del Excel estaba condicionado por la organización física de las hojas de cálculo.

Durante el rediseño de GeminiFy se decidió construir un modelo basado en conceptos del negocio en lugar de estructuras de almacenamiento.

## Modelo conceptual

El núcleo del sistema estará formado por las siguientes entidades:

- Catálogo
- Canción
- Artista
- Lista
- Participación
- Estado
- Flag
- Tag

Estas entidades podrán complementarse con otras en futuras versiones sin alterar la estructura fundamental del modelo.

## Relaciones

- Un Catálogo contiene muchas Canciones.
- Una Canción pertenece a un único Catálogo.
- Una Canción pertenece a un único Artista.
- Una Canción puede tener cero o muchas Participaciones.
- Una Lista contiene una o muchas Participaciones.
- Una Canción posee un único Estado.
- Una Canción puede disponer de múltiples Flags.
- Una Canción puede disponer de múltiples Tags.

## Motivación

Los principales objetivos son:

- Modelar el negocio y no la tecnología.
- Eliminar dependencias del Excel.
- Facilitar la evolución del sistema.
- Simplificar el mantenimiento.
- Mejorar la comprensión del dominio.

## Consecuencias

Toda la arquitectura de GeminiFy se desarrollará sobre este modelo conceptual.

Las estructuras técnicas (SQLite, API, interfaces, etc.) serán una implementación de este modelo y nunca al contrario.

## Impacto

Esta decisión afecta a toda la arquitectura del sistema.

# ADR-010 — Arquitectura basada en Acciones

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

Toda modificación del sistema deberá realizarse exclusivamente mediante una Acción.

Ningún componente podrá modificar directamente la información persistente.

## Contexto

GeminiFy incorpora distintos componentes capaces de solicitar cambios sobre el sistema:

- Usuario.
- Motor de reglas.
- Procesos de importación.
- API.
- Automatizaciones futuras.

Todos ellos utilizarán un mecanismo único de ejecución.

## Definición

Una Acción representa una operación de negocio capaz de modificar el estado del sistema.

Toda Acción deberá:

- Validar la operación.
- Ejecutar el cambio.
- Registrar la auditoría.
- Generar los eventos correspondientes.
- Devolver el resultado de la operación.

## Ejemplos

- CrearCancion
- ActualizarCancion
- ConsolidarLista
- CrearParticipacion
- CambiarEstadoCancion
- AñadirFlag
- QuitarFlag
- AñadirTag
- RecalcularEstadisticas

## Motivación

- Centralizar toda modificación.
- Garantizar la trazabilidad.
- Simplificar las pruebas.
- Evitar modificaciones inconsistentes.
- Unificar el comportamiento del sistema.

## Consecuencias

Toda modificación pasará por una Acción.

Las Reglas nunca modificarán directamente la información.

## Impacto

Esta decisión afecta a:

- Motor de reglas.
- API.
- Importaciones.
- Interfaz de usuario.
- Auditoría.

# ADR-011 — Arquitectura basada en Eventos

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

Toda Acción ejecutada por GeminiFy generará uno o varios Eventos que describan los hechos producidos durante su ejecución.

## Contexto

Una Acción representa una intención.

Los Eventos representan los hechos realmente ocurridos como consecuencia de esa Acción.

## Definición

Los Eventos constituyen el registro funcional del sistema.

Ejemplos:

- CancionCreada
- ParticipacionCreada
- EstadoCambiado
- FlagAñadido
- TagAñadido
- EstadisticasRecalculadas
- ListaImportada

## Motivación

Los principales objetivos son:

- Mejorar la trazabilidad.
- Facilitar la auditoría.
- Permitir futuras integraciones.
- Generar estadísticas.
- Registrar el comportamiento real del sistema.

## Consecuencias

Una Acción podrá generar cero, uno o múltiples Eventos.

Los Eventos nunca modificarán el sistema.

Representarán únicamente hechos ya ocurridos.

## Impacto

Esta decisión afecta a:

- Auditoría.
- Estadísticas.
- Integraciones.
- Registro histórico.

# ADR-012 — Arquitectura basada en Funciones

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy separará el conocimiento del negocio de la toma de decisiones mediante un sistema de Funciones reutilizables.

Las Funciones serán responsables de realizar cálculos, evaluaciones y comprobaciones, sin modificar el estado del sistema.

## Contexto

Durante el diseño del motor de reglas se identificó la necesidad de evitar reglas complejas y difíciles de mantener.

Para ello se adopta una arquitectura donde las reglas delegan la lógica de negocio en Funciones especializadas.

## Definición

Una Función representa un proceso reutilizable que responde a una pregunta o realiza un cálculo.

Las Funciones:

- no modifican información;
- no generan eventos;
- no ejecutan acciones;
- devuelven un resultado objetivo.

## Ejemplos

- EsCandidataAObservacion()
- CalcularNotaMedia()
- CalcularRanking()
- TieneFlag()
- ObtenerEstado()
- CalcularTendencia()
- ValidarTransicionEstado()

## Motivación

Los principales objetivos son:

- Reutilizar lógica de negocio.
- Simplificar las reglas.
- Facilitar las pruebas.
- Reducir la duplicidad de código.
- Mejorar el mantenimiento.

## Consecuencias

Las Reglas pasarán a limitarse a decidir cuándo debe ejecutarse una Acción.

Las Funciones concentrarán toda la lógica de cálculo y validación.

## Impacto

Esta decisión afecta a:

- Motor de reglas.
- Acciones.
- Estadísticas.
- Validaciones.
- Arquitectura general del sistema.

# ADR-013 — Clasificación de los Componentes del Sistema

## Estado

🟢 Aprobado

## Fecha

15/07/2026

## Decisión

GeminiFy clasificará todos los componentes del sistema en categorías funcionales claramente diferenciadas.

Cada componente pertenecerá a una única categoría principal, que determinará su responsabilidad dentro de la arquitectura.

Esta clasificación constituye la organización oficial del dominio y servirá como referencia para el diseño de la documentación, la base de datos y el código fuente.

## Contexto

Durante la definición de la arquitectura se identificó la necesidad de disponer de una estructura común que permitiera clasificar todos los elementos del sistema de forma coherente.

Esta clasificación facilitará el mantenimiento, la evolución del proyecto y la comprensión de la arquitectura.

## Clasificación

### 1. Entidades del Dominio

Representan los conceptos principales del negocio.

Ejemplos:

- Catálogo
- Canción
- Artista
- Lista
- Participación

Son la base del modelo de datos y contienen la información persistente del negocio.

---

### 2. Componentes de Organización

Permiten organizar y clasificar las entidades del dominio.

Ejemplos:

- Estado
- Flag
- Tag

No representan entidades independientes del negocio, sino mecanismos de clasificación y organización.

---

### 3. Componentes de Comportamiento

Definen el funcionamiento interno del sistema.

Ejemplos:

- Función
- Regla
- Acción

Estos componentes implementan la lógica de negocio y coordinan el comportamiento de GeminiFy.

---

### 4. Componentes de Registro

Representan los hechos ocurridos durante la ejecución del sistema.

Ejemplos:

- Evento
- Auditoría

Su finalidad es garantizar la trazabilidad completa de todas las operaciones.

---

### 5. Componentes de Configuración

Permiten adaptar el comportamiento de GeminiFy sin modificar el código.

Ejemplos:

- Parámetros
- Preferencias
- Catálogos auxiliares
- Configuración del sistema

## Motivación

Los principales objetivos de esta decisión son:

- Establecer una arquitectura uniforme.
- Separar claramente las responsabilidades de cada componente.
- Facilitar la comprensión del sistema.
- Simplificar la evolución futura de GeminiFy.
- Servir como guía para el diseño de la documentación, el modelo de datos y el código.

## Consecuencias

Toda nueva funcionalidad deberá clasificarse dentro de una de las categorías definidas en este ADR.

Si un nuevo componente no pudiera clasificarse, será necesario revisar la arquitectura antes de incorporarlo al sistema.

Esta clasificación será utilizada como referencia para organizar:

- la documentación;
- el modelo de datos;
- la estructura del código;
- las pruebas;
- la auditoría.

## Impacto

Esta decisión afecta a toda la arquitectura de GeminiFy y constituye el modelo de organización oficial del proyecto.

# ADR-014 — La Canción como entidad central del modelo de dominio

## Estado

Aprobado.

## Fecha

16/07/2026

## Contexto

Durante el diseño del Modelo de Dominio se analizó la naturaleza de las principales entidades de GeminiFy.

Se concluyó que el objetivo del sistema no es gestionar listas de reproducción, sino construir y mantener el conocimiento asociado a las Canciones para generar propuestas musicales fundamentadas.

Las Listas, Participaciones, Estados, Flags, Tags, Estadísticas y demás elementos del dominio existen únicamente en relación con una Canción.

## Decisión

Se establece que la **Canción constituye la entidad central del modelo de dominio de GeminiFy**.

El resto de entidades, procesos y componentes deberán diseñarse tomando la Canción como núcleo del sistema.

Las Listas representan agrupaciones de Canciones.

Las Participaciones representan hechos históricos asociados a una Canción dentro de una Lista.

Los Estados, Flags, Tags y Estadísticas describen o caracterizan una Canción, pero no forman parte de su identidad.

## Consecuencias

- El Modelo de Dominio se diseñará con la Canción como entidad principal.
- Las relaciones entre entidades se definirán tomando la Canción como eje del modelo.
- Los procesos de Consolidación y Propuesta de Lista operarán principalmente sobre las Canciones del Catálogo.
- La Base de Datos, la API y la interfaz de usuario deberán respetar este principio de diseño.
- Las futuras ampliaciones del sistema deberán preservar la centralidad de la Canción dentro del dominio.

## Justificación

Este enfoque representa con mayor fidelidad el propósito de GeminiFy: construir un catálogo musical vivo cuyo conocimiento evoluciona a partir de las Participaciones registradas y sirve como base para la generación de nuevas propuestas de listas.
