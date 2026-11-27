**UNIVERSIDAD TÉCNICA PARTICULAR DE LOJA**

Carrera de Ingeniería en Ciencias de la Computación

**ARQUITECTURA DE SOFTWARE**

**VISIÓN INTEGRAL 360**

Documento de Arquitectura de Software (DAS)

**Versión 1 corregida · Sección 3**

Vista lógica del dominio

**Reto:** Dashboard de proyectos \| **Institución beneficiaria:** Cooperativa de Ahorro y Crédito Padre Julián Lorente

**Repositorio del Grupo B:** https://github.com/Steven2610/ArquitecturaDeSoftware.git

**GRUPO B · INTEGRANTES**

| Diana Bermeo  | IA              |
|---------------|-----------------|
| Camilo Fierro | revisor         |
| Steven Vega   | arquitecto      |
| Lady Robalino | El que falta XD |

| **Docente**           | **Entrega**             | **Período académico** |
|-----------------------|-------------------------|-----------------------|
| Mgtr. Jackson Masache | 27 de noviembre de 2026 | Oct. 2026 – Feb. 2027 |

# 3. Vista lógica del dominio

## 3.1 Escenarios de dominio y extracción de sustantivos

*Los escenarios usan datos ficticios de prueba; no implican fórmulas, umbrales ni códigos aprobados por la cooperativa.*

### E-01 – CU-01 · Consultar panorama de proyectos

El 30/10/2026, el rol de Jefatura de Desarrollo de Software solicita el panorama de proyectos del período octubre de 2026. El proyecto ficticio P-001, «Canal web institucional», aparece en estado «En ejecución», con un responsable identificado y un hito H-01 previsto para el 28/10/2026. El indicador «Avance del proyecto» tiene un valor de indicador de 60 % (dato de prueba). Se muestra la fuente de información Redmine y su fecha de actualización: 29/10/2026. El perfil de alta dirección consulta el detalle y la fecha de corte; el sistema conserva los datos sin modificarlos y solo presenta los proyectos que el perfil de usuario puede consultar.

**Trazabilidad:** CU-01, que incluye CU-04; RF-04, RF-05, RF-07 y RF-08; RNF-02, RNF-04 y RNF-06.

### E-02 – CU-09 · Sincronizar fuentes y tratar coincidencias ambiguas

El 30/10/2026 a las 08:00, el temporizador inicia una sincronización de las fuentes de información Redmine y Excel online. Redmine entrega el proyecto P-001, la iniciativa I-003 y el requerimiento R-015; Excel entrega un seguimiento semanal del 29/10/2026 relacionado con el mismo proyecto. Una referencia de origen del Excel coincide con P-001 bajo una regla de correspondencia asumida solo para la prueba; otra solo comparte un nombre parecido y resulta ambigua. El sistema conserva el origen y la fecha de los registros válidos, no relaciona la referencia ambigua y registra una incidencia de sincronización. El resultado por fuente indica que ambas respondieron; la sincronización termina como exitosa con observaciones.

Al alcanzar el punto de extensión «información válida consolidada», CU-10 extiende a CU-09 solo si la evaluación está habilitada y esa versión de datos no se evaluó con las mismas reglas; no se ejecuta de forma incondicional. Si una semana el Excel llega sin columnas obligatorias (FA-05), sus registros se observan, se conserva la versión válida anterior y la sincronización queda parcial.

**Trazabilidad:** CU-09; RF-01, RF-02, RF-03, RF-08 y RF-13; RNF-01, RNF-03 y RNF-05; FA-03 (correspondencia ambigua) y FA-05 (estructura incompatible de Excel).

### E-03 – CU-10 · Evaluar retrasos sin duplicar alertas y notificar

El 30/10/2026 a las 09:00 se evalúa el proyecto de prueba P-001, que conserva un hito H-01 con fecha de compromiso 28/10/2026 y estado «Pendiente». Se utiliza una regla de alerta de ejemplo: «si la fecha de compromiso ya pasó y el hito sigue pendiente, se identifica un retraso». La primera evaluación crea el registro de evaluación RE-001 sobre la sincronización del día, aplica esa regla y registra la alerta A-001 asociada a P-001, con fecha y estado «Activa». Se genera la notificación N-001 por correo al responsable del proyecto y queda en estado «Enviada».

En una segunda evaluación de prueba, el sistema encuentra la misma condición activa: no crea otra alerta ni vuelve a notificar. Si se repite exactamente la versión de datos con las mismas reglas, registra la evaluación como omitida y no evalúa de nuevo; si faltan datos verificables, tampoco crea alertas nuevas. Si el servidor de correo no responde, la notificación queda «Fallida» y A-001 sigue visible en el dashboard. CU-10 puede iniciarse por el temporizador o al cumplirse la extensión de CU-09.

**Trazabilidad:** CU-10; RF-06, RF-08 y RF-14; RNF-03. El cálculo de KPI de RF-05 pertenece a CU-04.

### E-04 – CU-02 · Consultar detalle de proyecto (casos fusionados)

El 30/10/2026, el responsable de proyecto selecciona el proyecto P-001 y consulta su detalle autorizado: estado, responsable asignado y fechas de actualización. A continuación revisa la iniciativa I-003 y el requerimiento R-015; después consulta el hito H-01 y el seguimiento semanal del 29/10/2026 procedente de Excel online. Cada registro conserva su referencia de origen; un elemento de correspondencia ambigua no se vincula automáticamente con P-001.

**Trazabilidad:** CU-02 vigente; RF-01, RF-02, RF-03, RF-04, RF-07, RF-08, RF-09, RF-10 y RF-11. Los antiguos CU-03, CU-06 y CU-07 son variantes de consulta de CU-02 y no son casos activos independientes.

## 3.2 Cinco preguntas y lista de candidatos

P1: ¿Es un concepto relevante para el negocio? P2: ¿Tiene identidad o seguimiento independiente? P3: ¿Tiene atributos o reglas propios? P4: ¿Participa en relaciones del dominio? P5: ¿Es distinto de un actor, sistema externo, vista o componente técnico?

| **Candidato (evidencia)**                 | **P1** | **P2** | **P3** | **P4** | **P5** | **Decisión y justificación**                                                                                               |
|-------------------------------------------|--------|--------|--------|--------|--------|----------------------------------------------------------------------------------------------------------------------------|
| Proyecto (E-01/E-02/TDR)                  | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: identidad, estado, hitos e indicadores propios.                                                                     |
| Iniciativa (E-02/DAS)                     | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: concepto seguido en ambas fuentes.                                                                                  |
| Requerimiento (E-02/DAS)                  | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: concepto seguido en ambas fuentes.                                                                                  |
| Hito (E-01/E-03/TDR)                      | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: compromiso con fecha, estado y relaciones.                                                                          |
| Seguimiento semanal (E-04/DAS)            | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: registro de reuniones con fecha y observación.                                                                      |
| Indicador (E-01/TDR)                      | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: definición de métrica con reglas propias.                                                                           |
| Valor de indicador (E-01)                 | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: medición con valor, período y fecha. Reemplaza a «Avance».                                                          |
| Regla de alerta (E-03/CU-10)              | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: condición reutilizable, no umbral definitivo.                                                                       |
| Alerta (E-03/TDR)                         | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: tiene identidad, estado y causa.                                                                                    |
| Notificación (E-03/RF-14)                 | Sí     | Sí     | Sí     | Sí     | Sí     | Clase nueva: envío de una alerta con destinatario, estado y fecha; no se confunde con el servidor de correo.               |
| Registro de evaluación (E-03/CU-10)       | Sí     | Sí     | Sí     | Sí     | Sí     | Clase nueva: evidencia de qué versión se evaluó, con qué reglas y con qué resultado.                                       |
| Fuente de información (E-01/E-02)         | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: concepto de procedencia; no es un conector técnico.                                                                 |
| Referencia de origen (E-02/RF-08)         | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: relaciona registro, fuente y estado de correspondencia.                                                             |
| Sincronización (E-02/CU-09)               | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: ejecución registrada con estado y fecha. También llamada «registro de sincronización» en vistas previas.            |
| Resultado por fuente (E-02/CU-09)         | Sí     | Sí     | Sí     | Sí     | Sí     | Clase: datos propios de la relación fuente-ejecución.                                                                      |
| Incidencia de sincronización (E-02/CU-11) | Sí     | Sí     | Sí     | Sí     | Sí     | Clase nueva: fuente sin respuesta, estructura incompatible, registro ambiguo o rechazado; alimenta CU-11.                  |
| Perfil de usuario (E-01/RF-07)            | Sí     | Sí     | Sí     | Sí     | Sí     | Clase nueva: perfil de consulta (jefatura, alta dirección, responsable, administrador) que determina qué proyectos se ven. |
| Jefa de Desarrollo (E-01/CU-01)           | Sí     | Sí     | Sí     | Sí     | No     | Actor: solicita consulta; no es entidad de este modelo.                                                                    |
| Temporizador (E-02/CU-09)                 | Sí     | Sí     | Sí     | Sí     | No     | Actor: inicia procesos automáticos.                                                                                        |
| Redmine · Excel online (E-02)             | Sí     | Sí     | Sí     | Sí     | No     | Sistemas externos: distintos de FuenteInformacion.                                                                         |
| Servidor de correo (E-03)                 | Sí     | Sí     | Sí     | Sí     | No     | Sistema externo: actor secundario de CU-10.                                                                                |
| Responsable de proyecto (TDR/CU-02)       | Sí     | Sí     | Sí     | Sí     | No     | Actor: rol humano ya identificado.                                                                                         |
| Estado de proyecto (E-01)                 | Sí     | No     | No     | Sí     | Sí     | Atributo del Proyecto.                                                                                                     |
| Fecha de compromiso (E-03)                | Sí     | No     | No     | Sí     | Sí     | Atributo del Hito.                                                                                                         |
| Fecha de actualización (E-01/E-02)        | Sí     | No     | No     | Sí     | Sí     | Atributo de ReferenciaOrigen o FuenteInformacion.                                                                          |
| Responsable asignado (E-01/RF-04)         | Sí     | No     | No     | Sí     | Sí     | Atributo del Proyecto; su interacción es la de un actor.                                                                   |
| Período de consulta (E-01/CU-01)          | Sí     | No     | No     | Sí     | Sí     | Criterio de consulta, no clase ni atributo obligatorio.                                                                    |
| Regla de correspondencia (E-02/RF-03)     | Sí     | No     | Sí     | Sí     | Sí     | Regla documentada, no clase por ahora: se verifica con criterios, sin entidad autónoma confirmada.                         |
| Panorama de proyectos · Dashboard         | No     | No     | No     | No     | No     | Descartar: vista de presentación.                                                                                          |
| Controlador de sincronización             | No     | No     | No     | No     | No     | Descartar: diseño fuera de la vista lógica (vistas de procesos y desarrollo).                                              |
| Registro de errores (log técnico)         | No     | No     | No     | No     | No     | Descartar: bitácora técnica; el dominio registra incidencias en IncidenciaSincronizacion y RegistroEvaluacion.             |
| Tabla de base de datos                    | No     | No     | No     | No     | No     | Descartar: persistencia técnica.                                                                                           |
| GitLab / SonarQube (contexto)             | No     | No     | No     | No     | No     | Descartar: no son fuentes directas en esta etapa.                                                                          |

## 3.3 Diagrama de clases del dominio

El diagrama emplea conceptos de negocio, tipos de datos de dominio, asociaciones y dos composiciones justificadas. Las multiplicidades están indicadas en ambos extremos. Contiene 17 clases: las 13 de la versión anterior más RegistroEvaluacion, Notificacion, IncidenciaSincronizacion y PerfilUsuario. Archivo editable: vision360-vista-logica.mmd (el gráfico se generó con Graphviz desde clases.dot).

<img width="3817" height="1838" alt="02_figura_3" src="https://github.com/user-attachments/assets/5748072f-5c9d-46df-93a5-a123af2cd2c7" />


*Figura 3. Modelo conceptual completo de 17 clases (vista general; se amplía en las figuras 4 y 5).*

<img width="2537" height="1234" alt="02_figura_4" src="https://github.com/user-attachments/assets/4a69ca49-0ada-407e-9bd5-275031c69d6f" />



*Figura 4. Detalle: proyecto, seguimiento, indicadores y correspondencia de origen. La restricción {xor} se explica en 3.3.1.*

<img width="1476" height="1548" alt="02_figura_5" src="https://github.com/user-attachments/assets/bc164650-3d60-466e-85a6-fab387c9ba3d" />


*Figura 5. Detalle: sincronización, alertas, evaluación y notificación.*

## 3.3.1 Justificación de relaciones y multiplicidades

**Restricción {xor} de ReferenciaOrigen.** Una ReferenciaOrigen se vincula con cero o un elemento entre Proyecto, Iniciativa y Requerimiento: si la correspondencia está confirmada, exactamente uno; si está pendiente o es ambigua, ninguno. No son tres relaciones simultáneas. En el diagrama las tres asociaciones «corresponde» llevan la marca {xor}.

- **Proyecto 0..1 – Iniciativa / Requerimiento / SeguimientoSemanal.** Se permite provisionalmente que no tengan un Proyecto confirmado para no forzar la correspondencia de datos ambiguos; la jerarquía institucional no ha sido validada.

- **ValorIndicador.** Pertenece a un proyecto y a un indicador; puede haber varias mediciones por período. No se presupone una fórmula aprobada.

- **Sincronizacion ◆ ResultadoFuente (composición).** Un resultado no existe sin su sincronización; el conjunto de resultados identifica fallos parciales o totales. La sincronización siempre tiene al menos un resultado (1..\*).

- **ResultadoFuente ◆ IncidenciaSincronizacion (composición).** Las incidencias solo tienen sentido dentro del resultado de una fuente en una ejecución.

- **Sincronizacion 1 – 0..\* RegistroEvaluacion.** Una versión consolidada puede evaluarse varias veces (por ejemplo, con conjuntos de reglas distintos o con una evaluación omitida). Cada evaluación pertenece exactamente a una sincronización.

- **RegistroEvaluacion 0..\* – 1..\* ReglaAlerta.** Una evaluación aplica al menos una regla vigente; una regla participa en muchas evaluaciones. Con esta asociación se comprueba «misma versión, mismas reglas».

- **RegistroEvaluacion 1 – 0..\* Alerta.** Cada alerta nace en una evaluación; las evaluaciones posteriores que encuentran la misma condición activa no crean otra alerta.

- **Alerta 1 – 1 Proyecto y 1 – 1 ReglaAlerta.** Una Alerta se asocia a un solo proyecto y una sola regla; el par proyecto-condición no puede tener dos alertas activas.

- **Alerta 1 – 0..\* Notificacion.** Una alerta nueva genera notificaciones (una por destinatario); una alerta puede no tener ninguna si el correo no está habilitado.

- **PerfilUsuario 0..\* – 0..\* Proyecto.** Un perfil con alcance «proyectos asignados» puede consultar un subconjunto de proyectos; un proyecto es visible para varios perfiles.

## 3.4 Diccionario de clases

### 3.4.1 Proyecto

**Descripción:** Unidad de seguimiento institucional cuyo avance, responsables, hitos y estado se consolidan.

| **Atributo**     | **Tipo de negocio** | **Descripción**                                                                                       |
|------------------|---------------------|-------------------------------------------------------------------------------------------------------|
| codigo           | CodigoProyecto      | Identificador de dominio usado dentro del modelo; equivalencia con claves de las fuentes por validar. |
| nombre           | NombreProyecto      | Denominación del proyecto.                                                                            |
| estado           | EstadoProyecto      | Situación conocida del proyecto.                                                                      |
| responsable      | ResponsableAsignado | Referente de seguimiento; permisos y estructura organizativa por confirmar.                           |
| fechaFinPrevista | FechaOpcional       | Fecha comprometida si se conoce; no se presume para todos los proyectos.                              |

**Reglas de negocio / restricciones:**

- Pueden existir varias referencias de origen para un mismo proyecto confirmado.

- El proyecto consultado debe respetar las autorizaciones del perfil del usuario (CU-01).

- No se presume que el código ilustrativo P-001 exista en la cooperativa.

### 3.4.2 Iniciativa

**Descripción:** Iniciativa registrada para seguimiento; su vinculación a un proyecto requiere correspondencia verificada.

| **Atributo** | **Tipo de negocio**  | **Descripción**                             |
|--------------|----------------------|---------------------------------------------|
| referencia   | ReferenciaIniciativa | Identificación conceptual de la iniciativa. |
| nombre       | NombreIniciativa     | Denominación de la iniciativa.              |
| estado       | EstadoIniciativa     | Situación reportada.                        |

**Reglas de negocio / restricciones:**

- Su asociación a un proyecto es opcional (0..1) hasta validar la estructura real.

- Puede proceder de Redmine o de Excel y tener referencias de origen.

### 3.4.3 Requerimiento

**Descripción:** Necesidad o solicitud registrada para seguimiento, con relación al proyecto solo cuando se confirma.

| **Atributo** | **Tipo de negocio**      | **Descripción**                                    |
|--------------|--------------------------|----------------------------------------------------|
| referencia   | ReferenciaRequerimiento  | Identificador conceptual del requerimiento.        |
| descripcion  | DescripcionRequerimiento | Necesidad registrada.                              |
| estado       | EstadoRequerimiento      | Situación del requerimiento.                       |
| prioridad    | Prioridad                | Nivel de importancia, si lo proporciona la fuente. |

**Reglas de negocio / restricciones:**

- Asociación opcional (0..1) a proyecto; la relación exacta entre proyecto, iniciativa y requerimiento necesita validación.

- No relacionar requerimientos ambiguos por coincidencia de texto.

### 3.4.4 Hito

**Descripción:** Compromiso de seguimiento con fecha y estado, considerado al revisar atrasos.

| **Atributo**      | **Tipo de negocio** | **Descripción**                            |
|-------------------|---------------------|--------------------------------------------|
| codigo            | CodigoHito          | Referencia del compromiso.                 |
| descripcion       | DescripcionHito     | Resultado o entrega comprometida.          |
| fechaCompromiso   | Fecha               | Fecha prevista.                            |
| fechaCumplimiento | FechaOpcional       | Fecha real de finalización, cuando exista. |
| estado            | EstadoHito          | Estado conocido del compromiso.            |

**Reglas de negocio / restricciones:**

- Para detectar retrasos se debe disponer de una fecha y un estado verificables.

- La regla ilustrativa de vencimiento requiere validación institucional.

### 3.4.5 SeguimientoSemanal

**Descripción:** Registro complementario de seguimiento procedente del Excel online compartido, que puede quedar sin proyecto confirmado.

| **Atributo**  | **Tipo de negocio** | **Descripción**                                |
|---------------|---------------------|------------------------------------------------|
| fechaCorte    | Fecha               | Fecha de referencia del seguimiento.           |
| observacion   | TextoSeguimiento    | Información relevante registrada en reuniones. |
| fechaRegistro | FechaHora           | Momento registrado para ese seguimiento.       |

**Reglas de negocio / restricciones:**

- Los aportes son semanales según el contexto del DAS; la frecuencia del dashboard no está aprobada.

- Debe identificarse la fuente y su fecha; no reemplazar sin control la última versión válida.

- Si la correspondencia con un proyecto es ambigua, se registra el caso sin asociarlo automáticamente (CU-09, FA-03).

### 3.4.6 Indicador

**Descripción:** Definición de una medida de seguimiento de proyectos. El avance de un proyecto es un Indicador («Avance del proyecto»), no una clase aparte.

| **Atributo**       | **Tipo de negocio**  | **Descripción**                                                               |
|--------------------|----------------------|-------------------------------------------------------------------------------|
| codigo             | CodigoIndicador      | Referencia de la medida.                                                      |
| nombre             | NombreIndicador      | Ejemplo: avance del proyecto.                                                 |
| definicion         | DefinicionIndicador  | Significado de la medición.                                                   |
| formulaDocumentada | ReglaCalculoOpcional | Fórmula de negocio cuando esté documentada y validada; puede estar pendiente. |
| unidad             | UnidadMedida         | Ejemplo: porcentaje o cantidad.                                               |

**Reglas de negocio / restricciones:**

- La fórmula debe documentarse antes de aplicarse.

- Si no existe información suficiente, el indicador se presenta como «No disponible» (CU-01).

### 3.4.7 ValorIndicador

**Descripción:** Medición calculada de un indicador para un proyecto y período.

| **Atributo**  | **Tipo de negocio** | **Descripción**                                                                       |
|---------------|---------------------|---------------------------------------------------------------------------------------|
| periodo       | PeriodoSeguimiento  | Intervalo de la medición.                                                             |
| valor         | ValorMedidaOpcional | Medición cuando existan datos verificables; ausente si no hay información suficiente. |
| fechaCalculo  | FechaHora           | Momento en el que se obtuvo.                                                          |
| estadoCalculo | EstadoCalculo       | Calculado o no disponible.                                                            |

**Reglas de negocio / restricciones:**

- Una medición pertenece a un proyecto y a una definición de indicador.

- Un valor no disponible no se sustituye por una cifra inventada.

### 3.4.8 ReglaAlerta

**Descripción:** Condición de negocio definida para evaluar posibles retrasos o desviaciones.

| **Atributo** | **Tipo de negocio** | **Descripción**                               |
|--------------|---------------------|-----------------------------------------------|
| codigo       | CodigoRegla         | Referencia de la regla.                       |
| descripcion  | DescripcionRegla    | Qué situación busca identificar.              |
| criterio     | CondicionNegocio    | Condición evaluable, pendiente de aprobación. |
| estado       | VigenciaRegla       | Vigente o no vigente.                         |

**Reglas de negocio / restricciones:**

- Los umbrales específicos requieren aprobación por la cooperativa.

- La evaluación de reglas puede terminar sin emitir una alerta (CU-10).

- Solo las reglas vigentes se aplican y quedan asociadas a cada RegistroEvaluacion.

### 3.4.9 Alerta

**Descripción:** Señal de una desviación verificada asociada a un proyecto y una regla.

| **Atributo**       | **Tipo de negocio**  | **Descripción**              |
|--------------------|----------------------|------------------------------|
| codigo             | CodigoAlerta         | Identificación de la alerta. |
| condicionDetectada | DescripcionCondicion | Motivo de la alerta.         |
| fechaGeneracion    | FechaHora            | Momento de detección.        |
| estado             | EstadoAlerta         | Activa o resuelta.           |

**Reglas de negocio / restricciones:**

- No se permite más de una alerta activa para el mismo proyecto y la misma condición (CU-10); se garantiza con una restricción única parcial en la base de datos.

- Si los datos son insuficientes no se genera una alerta nueva.

### 3.4.10 Notificacion (nueva)

**Descripción:** Aviso emitido al responsable de un proyecto cuando se registra una alerta nueva. **Para qué sirve:** permite que el responsable se entere sin abrir el dashboard (RF-14) y deja constancia de si el aviso llegó, de modo que una falla del correo no se confunda con la ausencia de la alerta.

| **Atributo** | **Tipo de negocio** | **Descripción**                                                                                                             |
|--------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------|
| canal        | CanalNotificacion   | Medio de envío; en el alcance actual, solo correo electrónico. El dashboard es el canal principal y no genera Notificacion. |
| destinatario | Destinatario        | Persona o correo del responsable a quien se avisa.                                                                          |
| fechaEnvio   | FechaHoraOpcional   | Momento del envío; ausente mientras esté pendiente.                                                                         |
| estadoEnvio  | EstadoEnvio         | Pendiente, enviada o fallida.                                                                                               |

**Reglas de negocio / restricciones:**

- Una alerta nueva genera como máximo una notificación por destinatario; una alerta que ya estaba activa no se vuelve a notificar.

- La falla del envío no modifica ni oculta la Alerta (CU-10, FA-06).

- Depende de la disponibilidad del servidor de correo (SUP-08).

### 3.4.11 RegistroEvaluacion (nueva)

**Descripción:** Evidencia de una ejecución de CU-10: qué versión consolidada se evaluó, con qué reglas y con qué resultado. **Para qué sirve:** (1) garantiza que la misma versión de datos no se evalúe dos veces con las mismas reglas; (2) conserva el historial de evaluaciones, incluidas las omitidas y las fallidas; (3) permite explicar por qué un proyecto no se evaluó.

| **Atributo**          | **Tipo de negocio** | **Descripción**                                      |
|-----------------------|---------------------|------------------------------------------------------|
| fechaEvaluacion       | FechaHora           | Momento de la evaluación.                            |
| resultado             | ResultadoEvaluacion | Completada, omitida (versión ya evaluada) o fallida. |
| cantidadEvaluados     | CantidadRegistros   | Proyectos evaluados con datos suficientes.           |
| cantidadNoEvaluables  | CantidadRegistros   | Proyectos sin datos suficientes (CU-10, FA-03).      |
| cantidadAlertasNuevas | CantidadRegistros   | Alertas creadas en esa evaluación.                   |
| observacion           | TextoOpcional       | Causa de una evaluación omitida o fallida.           |

**Reglas de negocio / restricciones:**

- Pertenece a una sola Sincronizacion (la versión evaluada) y aplica al menos una ReglaAlerta.

- No puede haber dos evaluaciones completadas para la misma sincronización con el mismo conjunto de reglas.

- Las alertas creadas en una evaluación quedan asociadas a ella.

### 3.4.12 FuenteInformacion

**Descripción:** Referencia de negocio al origen de datos que contribuye a la consolidación.

| **Atributo**                | **Tipo de negocio** | **Descripción**                              |
|-----------------------------|---------------------|----------------------------------------------|
| nombre                      | NombreFuente        | Redmine o Excel online en el alcance actual. |
| tipo                        | TipoFuente          | Categoría de origen, no mecanismo técnico.   |
| ultimaActualizacionConocida | FechaHoraOpcional   | Última actualización reportada o conocida.   |

**Reglas de negocio / restricciones:**

- Las fuentes principales actuales son Redmine y Excel online.

- Representa el concepto «origen de información»; no es una clase del software Redmine o Excel.

### 3.4.13 ReferenciaOrigen

**Descripción:** Referencia que permite conocer de qué fuente proviene un registro y si se confirmó su correspondencia.

| **Atributo**               | **Tipo de negocio**   | **Descripción**                                                |
|----------------------------|-----------------------|----------------------------------------------------------------|
| referenciaEnFuente         | ReferenciaExterna     | Código o referencia tal como llega desde la fuente.            |
| fechaActualizacionEnFuente | FechaHoraOpcional     | Marca temporal informada por la fuente cuando esté disponible. |
| estadoCorrespondencia      | EstadoCorrespondencia | Confirmada, pendiente o ambigua.                               |

**Reglas de negocio / restricciones:**

- Restricción {xor}: una referencia confirmada se vincula a exactamente un elemento entre Proyecto, Iniciativa y Requerimiento; nunca a varios.

- Una referencia ambigua o pendiente queda sin asociación hasta su revisión (CU-09, FA-03).

### 3.4.14 Sincronizacion

**Descripción:** Ejecución de obtención y consolidación de información cuyo resultado debe quedar registrado. Es la clase que otras vistas llamaban «RegistroSincronizacion».

| **Atributo** | **Tipo de negocio**     | **Descripción**                              |
|--------------|-------------------------|----------------------------------------------|
| fechaInicio  | FechaHora               | Inicio del proceso.                          |
| fechaFin     | FechaHoraOpcional       | Fin de la ejecución.                         |
| resultado    | ResultadoSincronizacion | Exitosa, parcial o fallida.                  |
| observacion  | TextoOpcional           | Resumen de incidencias o registros ambiguos. |

**Reglas de negocio / restricciones:**

- Si fallan ambas fuentes no se actualizan datos y no se habilita el punto de extensión de CU-10; si hay datos nuevos válidos, la evaluación puede extender CU-09 bajo la condición documentada.

- Si cambia la estructura del Excel y faltan columnas obligatorias, los registros incompatibles se observan y se conserva la versión válida anterior.

- Si una fuente falla, se conserva la última versión válida y se informa la actualización parcial.

### 3.4.15 ResultadoFuente

**Descripción:** Resultado de consultar una fuente determinada en una ejecución de sincronización.

| **Atributo**       | **Tipo de negocio**  | **Descripción**                    |
|--------------------|----------------------|------------------------------------|
| estadoConsulta     | EstadoConsultaFuente | Disponible o fallida.              |
| fechaConsulta      | FechaHora            | Momento de consulta.               |
| cantidadValidos    | CantidadRegistros    | Registros que pudieron procesarse. |
| cantidadObservados | CantidadRegistros    | Registros con observaciones.       |

**Reglas de negocio / restricciones:**

- Debe pertenecer a una y solo una sincronización y corresponder a una fuente.

- Permite identificar qué fuente respondió o falló (CU-09 y CU-11).

### 3.4.16 IncidenciaSincronizacion (nueva)

**Descripción:** Problema concreto detectado al consultar una fuente en una sincronización. **Para qué sirve:** da contenido a CU-11 (revisar fuentes sin actualizar y registros rechazados) y evita ocultar los detalles en un texto libre.

| **Atributo**  | **Tipo de negocio**   | **Descripción**                                                                       |
|---------------|-----------------------|---------------------------------------------------------------------------------------|
| tipo          | TipoIncidencia        | Fuente sin respuesta, estructura incompatible, registro ambiguo o registro rechazado. |
| descripcion   | DescripcionIncidencia | Detalle de lo ocurrido y, si aplica, la referencia afectada.                          |
| fechaRegistro | FechaHora             | Momento en que se registró.                                                           |

**Reglas de negocio / restricciones:**

- Pertenece a un solo ResultadoFuente (composición).

- Una incidencia no cambia la última versión válida de los datos.

### 3.4.17 PerfilUsuario (nueva)

**Descripción:** Perfil de consulta que determina qué información puede ver quien accede al dashboard. **Para qué sirve:** sustenta RF-07 y las reglas de seguridad de CU-01 (solo se muestran los proyectos autorizados).

| **Atributo** | **Tipo de negocio** | **Descripción**                                                                  |
|--------------|---------------------|----------------------------------------------------------------------------------|
| nombre       | NombrePerfil        | Jefatura de Desarrollo, alta dirección, responsable de proyecto o administrador. |
| alcance      | AlcanceConsulta     | Todos los proyectos o solo los asignados.                                        |

**Reglas de negocio / restricciones:**

- Un perfil con alcance «asignados» se relaciona con los proyectos que puede consultar.

- Las cuentas de usuario y su autenticación quedan pendientes de definir con TI (SUP-07); este modelo solo fija el perfil de consulta.

## 3.5 Trazabilidad y decisiones pendientes

| **Requisito / caso de uso**                                          | **Clases principales**                                                                                                                                  |
|----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| CU-01, CU-04; RF-04, RF-05, RF-07, RF-08                             | Proyecto, Hito, Indicador, ValorIndicador, Alerta, FuenteInformacion, ReferenciaOrigen, PerfilUsuario                                                   |
| CU-02; RF-01, RF-02, RF-03, RF-04, RF-07, RF-08, RF-09, RF-10, RF-11 | Proyecto, Iniciativa, Requerimiento, Hito, SeguimientoSemanal, FuenteInformacion, ReferenciaOrigen, PerfilUsuario                                       |
| CU-05; RF-06                                                         | Alerta, ReglaAlerta, Proyecto                                                                                                                           |
| CU-08; RF-12                                                         | Proyecto, Indicador, ValorIndicador, PerfilUsuario                                                                                                      |
| CU-09; RF-01, RF-02, RF-03, RF-08, RF-13                             | Proyecto, Iniciativa, Requerimiento, SeguimientoSemanal, FuenteInformacion, ReferenciaOrigen, Sincronizacion, ResultadoFuente, IncidenciaSincronizacion |
| CU-10; RF-06, RF-08, RF-14                                           | Proyecto, Hito, ReglaAlerta, Alerta, RegistroEvaluacion, Sincronizacion, Notificacion                                                                   |
| CU-11; RF-03, RF-08, RF-13                                           | Sincronizacion, ResultadoFuente, IncidenciaSincronizacion, ReferenciaOrigen                                                                             |

**Decisiones pendientes con la cooperativa:** fórmula institucional de avance, umbrales de retraso, jerarquía real entre proyecto, iniciativa y requerimiento, claves comunes entre Redmine y Excel, mecanismo de autenticación y disponibilidad del servidor de correo.

**Compromisos para las vistas siguientes** (para que no se pierdan):

| **Vista**  | **Qué debe incorporar o corregir**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Procesos   | Usar los nombres de la sección 1.9 (Sincronizacion, ValorIndicador, Temporizador). Añadir RegistroEvaluacion, Notificacion, IncidenciaSincronizacion y PerfilUsuario en robustez y secuencias. Entrar por un borde (Planificador) en lugar de enlazar el Temporizador con el control. Mostrar CU-10 como extensión de CU-09. Mensaje asíncrono en la sincronización manual (FA-04) con su explicación. Paso de notificación y su falla (FA-06). Diagrama de clases solo con entidades más la tabla CU → secuencia → operaciones por entidad. |
| Desarrollo | Mover ControlIntegracion a un paquete de dominio; dejar solo adaptadores en Integración de fuentes. Asignar las 17 clases a paquetes (incluidas SeguimientoSemanal, Indicador, ValorIndicador, ReferenciaOrigen, ResultadoFuente, Notificacion, IncidenciaSincronizacion). Paquetes en notación UML, sin flechas «include». Añadir el adaptador de correo.                                                                                                                                                                                   |
| Despliegue | Ya usa Node.js 22, BullMQ, nginx y SMTP: es la referencia. Actualizar la trazabilidad con los paquetes definitivos y completar la bitácora de IA.                                                                                                                                                                                                                                                                                                                                                                                            |
