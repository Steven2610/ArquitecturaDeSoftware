**UNIVERSIDAD TÉCNICA PARTICULAR DE LOJA**

Carrera de Ingeniería en Ciencias de la Computación

**ARQUITECTURA DE SOFTWARE**

**VISIÓN INTEGRAL 360**

Documento de Arquitectura de Software (DAS)

**Versión 1 corregida · Sección 2**

Casos de uso (vista de escenarios)

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

# 2. Casos de uso (vista de escenarios)

Continuidad de la propuesta de solución del Grupo B y de los requisitos funcionales RF-01 a RF-14 (sección 1.6). La primera versión estableció como fuentes Redmine y el Excel online; ambas manejan proyectos, iniciativas y requerimientos, pero todavía no se sabe si usan identificadores equivalentes. El reto consiste en consolidar la información para mostrar avances, indicadores y alertas, evitando relaciones incorrectas.

## 2.1 Actores

| **Actor**                                       | **Tipo**                 | **Objetivo principal**                                                      | **Estado**                                                                  |
|-------------------------------------------------|--------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Jefa del Departamento de Desarrollo de Software | Persona                  | Consultar la situación global de los proyectos, indicadores y alertas.      | Identificada durante la entrevista.                                         |
| Alta dirección                                  | Persona                  | Conocer avances y riesgos para tomar decisiones.                            | Actor previsto en el TDR.                                                   |
| Responsable de proyecto                         | Persona                  | Revisar proyectos, iniciativas, requerimientos, hitos y alertas.            | Actor previsto en el TDR.                                                   |
| Administrador de la plataforma                  | Persona                  | Solicitar sincronizaciones y revisar problemas de integración.              | Rol propuesto; pendiente de validación.                                     |
| Temporizador                                    | Sistema externo (tiempo) | Iniciar la sincronización programada y la evaluación automática de alertas. | Actor técnico propuesto para iniciar procesos automáticos.                  |
| Redmine                                         | Sistema externo          | Suministrar registros de proyectos, iniciativas y requerimientos.           | Sistema real identificado en la entrevista; acceso pendiente de validación. |
| Excel online                                    | Sistema externo          | Suministrar información complementaria registrada semanalmente.             | Fuente real identificada en la entrevista; acceso pendiente de validación.  |
| Servidor de correo (SMTP)                       | Sistema externo          | Entregar al responsable la notificación de las alertas nuevas.              | Nuevo. Canal complementario; disponibilidad pendiente (SUP-08).             |

## 2.2 Decisiones de consolidación del catálogo

Al revisar el catálogo original con las demás vistas se tomaron cuatro decisiones. Cada una se aplica en todo el DAS (vocabulario de la sección 1.9).

| **Decisión**                                                                     | **Motivo**                                                                                                                                                                                                                        | **Efecto**                                                                                                                                                              |
|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fusionar CU-03, CU-06 y CU-07 en CU-02                                           | Son consultas del mismo actor sobre el mismo proyecto, sin lógica propia distinta; separarlas dejaba tres casos casi idénticos sin especificación.                                                                                | Quedan 8 casos activos. Los IDs 03, 06 y 07 se retiran y no se reutilizan. La funcionalidad se conserva como variantes de CU-02 y se respalda con RF-09, RF-10 y RF-11. |
| CU-10 «extend» CU-09 (antes «include»)                                           | CU-10 también se ejecuta solo, por su propia programación, y solo se activa tras una sincronización si hay datos nuevos válidos y la versión no fue evaluada. Una inclusión es incondicional; una extensión modela esa condición. | Punto de extensión «información válida consolidada» en CU-09. Se corrigen el UML, las especificaciones y, en las vistas siguientes, secuencias, paquetes y despliegue.  |
| CU-10 notifica por correo (RF-14)                                                | El responsable debe enterarse de un retraso sin entrar al dashboard. El dashboard sigue siendo el canal principal y el correo es complementario.                                                                                  | Nuevo actor Servidor de correo (SMTP), nueva clase Notificacion y un paso adicional en CU-10 con su flujo de falla.                                                     |
| Registrar la evaluación (RegistroEvaluacion) y las incidencias de sincronización | Sin evidencia no se puede garantizar «no evaluar dos veces la misma versión» (CU-10) ni revisar rechazos y fuentes caídas (CU-11).                                                                                                | Nuevas clases RegistroEvaluacion e IncidenciaSincronizacion en la vista lógica; deben aparecer en la vista de procesos.                                                 |

## 2.3 Catálogo priorizado

| **ID** | **Caso de uso**                     | **Actor principal**                           | **Prioridad** | **Justificación**                                                                                                   |
|--------|-------------------------------------|-----------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------|
| CU-01  | Consultar panorama de proyectos     | Jefa de Desarrollo / Alta dirección           | Alta          | Ofrece una visión general para la toma de decisiones.                                                               |
| CU-02  | Consultar detalle de proyecto       | Responsable de proyecto                       | Alta          | Reúne en un solo caso el detalle, las iniciativas y requerimientos, los hitos y el seguimiento semanal (variantes). |
| CU-04  | Consultar indicadores de avance     | Jefa de Desarrollo / Alta dirección           | Alta          | Resume información mediante indicadores automáticos.                                                                |
| CU-05  | Revisar alertas de retrasos         | Responsable de proyecto / Jefa de Desarrollo  | Alta          | Permite conocer situaciones que necesitan atención.                                                                 |
| CU-08  | Comparar estado de proyectos        | Jefa de Desarrollo / Alta dirección           | Media         | Facilita comparar diferentes proyectos en un mismo período.                                                         |
| CU-09  | Sincronizar fuentes de información  | Temporizador / Administrador de la plataforma | Alta          | Integra la información de Redmine y Excel.                                                                          |
| CU-10  | Generar alertas por desviaciones    | Temporizador                                  | Alta          | Detecta automáticamente posibles retrasos o incumplimientos y notifica.                                             |
| CU-11  | Revisar problemas de sincronización | Administrador de la plataforma                | Media         | Permite identificar fuentes sin actualizar o registros rechazados.                                                  |

**Variantes de consulta de CU-02.** El responsable elige qué revisar dentro del detalle de un proyecto:

| **Variante**                 | **Qué muestra**                                                                 | **Requisito** | **Antes** |
|------------------------------|---------------------------------------------------------------------------------|---------------|-----------|
| Resumen del proyecto         | Estado, responsable, avance y fechas de actualización con su origen.            | RF-04, RF-08  | CU-02     |
| Iniciativas y requerimientos | Registros vinculados al proyecto y los de correspondencia ambigua, sin asociar. | RF-09, RF-03  | CU-03     |
| Hitos y plazos               | Hitos con fecha de compromiso, estado y cumplimiento.                           | RF-10         | CU-06     |
| Seguimiento semanal          | Aportes de reuniones del Excel online con su fecha de corte.                    | RF-11, RF-02  | CU-07     |

## 2.4 Diagrama UML de casos de uso

Archivo fuente en el repositorio: diagramas/vision360-casos-de-uso.puml (el gráfico de este documento se generó con Graphviz a partir de casos.dot; ambos describen el mismo modelo).

![Figura 2. Diagrama de casos de uso de Visión Integral 360.](imagenes/01_figura_image2.png)

*Figura 2. Diagrama de casos de uso de Visión Integral 360.*

- **CU-01 «include» CU-04:** consultar un panorama siempre incluye sus indicadores de avance.

- **CU-10 «extend» CU-09:** al alcanzar el punto de extensión «información válida consolidada», CU-10 se ejecuta solo si la evaluación está habilitada y la versión de los datos no fue evaluada con las mismas reglas. Evaluar las reglas no significa que siempre se genere una alerta. Si ambas fuentes fallan, el punto de extensión no se habilita. CU-10 también lo inicia el Temporizador de forma independiente.

- **CU-02** agrupa las antiguas consultas de iniciativas y requerimientos, hitos y plazos, y seguimiento semanal (sección 2.3).

## 2.5 Especificaciones de casos de uso

Se especifican CU-01, CU-09 y CU-10 por ser tres de los casos de mayor prioridad y cubrir las funciones centrales: consultar el panorama, consolidar Redmine y Excel online, y generar alertas.

### CU-01 – Consultar panorama de proyectos

| **Campo**               | **Descripción**                                                                                                        |
|-------------------------|------------------------------------------------------------------------------------------------------------------------|
| ID                      | CU-01                                                                                                                  |
| Actor principal         | Jefa del Departamento de Desarrollo de Software / Alta dirección                                                       |
| Otros actores           | Ninguno                                                                                                                |
| Objetivo                | Consultar una vista general de los proyectos para conocer sus estados, indicadores, alertas y fechas de actualización. |
| Relación UML            | Incluye CU-04 – Consultar indicadores de avance.                                                                       |
| Requisitos relacionados | RF-04, RF-05, RF-07 y RF-08                                                                                            |

**Precondiciones**

1.  El usuario tiene una sesión activa en Visión Integral 360.

2.  El usuario cuenta con un perfil con permisos para consultar el panorama de proyectos.

3.  El sistema dispone de información consolidada o tiene registrado que todavía no existen datos disponibles.

**Postcondiciones**

Si termina bien: se presenta la información general de los proyectos que el usuario está autorizado a consultar; se muestran los indicadores disponibles y la fecha de última actualización; los datos consultados permanecen sin modificaciones.

Si falla: el sistema informa que no fue posible completar la consulta; no se muestra información restringida ni se alteran los registros existentes.

**Flujo principal**

| **Paso** | **Acción**                                                                                                                                       |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | Usuario: Solicita consultar el panorama general de proyectos.                                                                                    |
| 2        | Sistema: Verifica los permisos del perfil y presenta los períodos disponibles para consulta.                                                     |
| 3        | Usuario: Selecciona el período de seguimiento que desea revisar.                                                                                 |
| 4        | Sistema: Recupera los proyectos correspondientes al período seleccionado y presenta su estado general.                                           |
| 5        | Usuario: Revisa el estado general de los proyectos del período seleccionado.                                                                     |
| 6        | Sistema: Ejecuta CU-04 y presenta los indicadores de avance, las alertas disponibles, el origen de los datos y la fecha de última actualización. |
| 7        | Usuario: Selecciona un criterio para filtrar los proyectos, como estado o responsable.                                                           |
| 8        | Sistema: Actualiza el panorama y presenta los proyectos correspondientes al filtro seleccionado.                                                 |

**Flujos alternativos**

- **FA-01 (paso 4).** No existen proyectos correspondientes al período seleccionado. El sistema informa que no se encontraron resultados y permite regresar al paso 3.

- **FA-02 (paso 6).** La información de alguna fuente no está actualizada. El sistema presenta los indicadores disponibles e informa la fecha real de última actualización. La consulta continúa en el paso 7.

- **FA-03 (paso 8).** No existen proyectos que coincidan con el filtro. El sistema informa que no hay resultados y permite regresar al paso 7.

**Excepciones**

- **E-01 (paso 4).** El sistema no puede recuperar la información consolidada por una falla del servicio. Informa al usuario que no es posible completar la consulta y termina el caso de uso.

**Requisitos especiales**

1.  **Rendimiento:** con 100 proyectos y 10 consultas concurrentes, al menos el 95 % responde en menos de 3 segundos.

2.  **Seguridad:** solo se muestran los proyectos autorizados para el perfil del usuario.

3.  **Trazabilidad:** se identifica la fecha de última actualización de la información presentada.

4.  **Usabilidad:** el estado general y los indicadores principales de un proyecto se alcanzan con un máximo de tres acciones de navegación.

**Observación:** si no existen datos suficientes para calcular un indicador, el sistema mostrará «No disponible» en lugar de presentar un valor sin sustento.

### CU-09 – Sincronizar fuentes de información

| **Campo**                      | **Descripción**                                                                                                                                  |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| ID                             | CU-09                                                                                                                                            |
| Actor principal                | Temporizador                                                                                                                                     |
| Actor iniciador alternativo    | Administrador de la plataforma (sincronización manual)                                                                                           |
| Actores externos participantes | Redmine y Excel online                                                                                                                           |
| Objetivo                       | Obtener y consolidar los registros de Redmine y Excel online, relacionando proyectos, iniciativas y requerimientos mediante reglas verificables. |
| Relación UML                   | Es extendido por CU-10 – Generar alertas por desviaciones, en el punto de extensión «información válida consolidada».                            |
| Requisitos relacionados        | RF-01, RF-02, RF-03, RF-08 y RF-13                                                                                                               |

**Precondiciones**

1.  El sistema cuenta con mecanismos de acceso configurados para Redmine y Excel online.

2.  Existen reglas iniciales para validar y relacionar proyectos, iniciativas y requerimientos.

3.  El servicio de sincronización está habilitado y no existe otra ejecución incompatible en curso.

**Postcondiciones**

Si termina bien: la información válida queda consolidada y disponible para consulta; los registros conservan la referencia de su fuente; se registra la sincronización con fecha, hora, resultado por fuente e incidencias; si se cumple la condición del punto de extensión, se activa CU-10.

Si falla: se conserva la última versión válida de los datos; se registra el problema y se identifica la fuente afectada; no se crean relaciones entre registros cuya correspondencia no pueda confirmarse; si no se obtiene información de ninguna fuente, no se habilita el punto de extensión de CU-10.

**Flujo principal**

| **Paso** | **Acción**                                                                                                                                                                     |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | Temporizador: Solicita iniciar la sincronización programada de información.                                                                                                    |
| 2        | Sistema: Solicita a Redmine los registros disponibles de proyectos, iniciativas y requerimientos.                                                                              |
| 3        | Redmine: Entrega la información solicitada.                                                                                                                                    |
| 4        | Sistema: Solicita a Excel online los registros complementarios del seguimiento semanal.                                                                                        |
| 5        | Excel online: Entrega la información registrada en el archivo compartido.                                                                                                      |
| 6        | Sistema: Valida los registros, relaciona la información confiable, guarda los resultados y registra la sincronización con su resultado por fuente.                             |
| 7        | Sistema: En el punto de extensión «información válida consolidada», activa CU-10 si la evaluación está habilitada y la versión de datos no fue evaluada con las mismas reglas. |

**Flujos alternativos**

- **FA-01 (paso 3).** Redmine no responde. El sistema registra la incidencia, conserva la última información válida de esa fuente y continúa en el paso 4. Si Excel online responde, la sincronización se registra como parcial.

- **FA-02 (paso 5).** Excel online no responde. El sistema registra la incidencia, conserva la última información válida de Excel y continúa en el paso 6 con los datos de Redmine. La sincronización se registra como parcial.

- **FA-03 (paso 6).** Hay registros con coincidencias ambiguas entre Redmine y Excel online. El sistema no los relaciona, registra la observación como incidencia y continúa con los demás registros válidos.

- **FA-04 (paso 1).** El administrador solicita una sincronización manual. El sistema comprueba su autorización y que no haya otra ejecución en curso; registra la solicitud, responde de inmediato «sincronización en curso» y la ejecución continúa en segundo plano desde el paso 2. El administrador consulta el resultado después (CU-11). Si ya hay una ejecución en curso, rechaza la solicitud e informa.

- **FA-05 (paso 5).** Excel online responde, pero su estructura es incompatible (faltan columnas obligatorias). El sistema registra los registros incompatibles como incidencias, conserva la versión válida anterior del Excel y continúa en el paso 6; la sincronización se registra como parcial.

**Excepciones**

- **E-01 (paso 5).** Redmine no respondió y Excel online tampoco está disponible. El sistema registra el fallo de ambas fuentes, conserva la última información válida y termina la sincronización como fallida, sin actualizar los registros y sin habilitar el punto de extensión de CU-10.

**Requisitos especiales**

1.  **Interoperabilidad:** con 200 registros, el sistema procesa la información válida en menos de 5 minutos.

2.  **Integridad:** en un conjunto de prueba con correspondencias conocidas, no genera asociaciones falsas entre proyectos, iniciativas y requerimientos.

3.  **Fiabilidad:** cada sincronización queda registrada con fecha, hora, resultado y fuentes afectadas, indicando si fue exitosa, parcial o fallida.

4.  **Seguridad:** el acceso a Redmine y Excel online se realiza con mecanismos autorizados y sin exponer credenciales.

**Observación:** las fuentes principales son Redmine y Excel online. GitLab y SonarQube forman parte del contexto descrito en la entrevista, pero no se incorporan como fuentes directas en esta etapa.

### CU-10 – Generar alertas por desviaciones

| **Campo**               | **Descripción**                                                                                                                              |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| ID                      | CU-10                                                                                                                                        |
| Actor principal         | Temporizador                                                                                                                                 |
| Inicio adicional        | Extensión de CU-09 tras consolidar información válida (punto de extensión «información válida consolidada»).                                 |
| Otros actores           | Servidor de correo (SMTP), para la notificación de alertas nuevas                                                                            |
| Objetivo                | Evaluar la información de proyectos e hitos para identificar retrasos o desviaciones, registrar las alertas correspondientes y notificarlas. |
| Relación UML            | Extiende CU-09; también se ejecuta mediante programación automática.                                                                         |
| Requisitos relacionados | RF-06, RF-08 y RF-14. El cálculo de KPI (RF-05) pertenece a CU-04; CU-10 solo usa información ya consolidada.                                |

**Precondiciones**

1.  El sistema dispone de información consolidada válida sobre al menos un proyecto.

2.  Se encuentran definidas las reglas de alerta vigentes.

3.  El proceso de evaluación de alertas se encuentra habilitado.

**Postcondiciones**

Si termina bien: las condiciones que cumplen las reglas quedan registradas como alertas consultables; se registra la evaluación (fecha, versión de datos evaluada, reglas aplicadas y resultado); no se crean alertas duplicadas para un mismo proyecto y una misma condición activa; las alertas nuevas se notifican por correo; si no hay desviaciones, la evaluación finaliza sin generar alertas.

Si falla: no se generan alertas con información insuficiente o no verificable; se registra la causa; las alertas válidas anteriores se conservan; una falla del correo no revierte ni oculta las alertas registradas.

**Flujo principal**

| **Paso** | **Acción**                                                                                                                                            |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | Temporizador: Solicita iniciar la evaluación programada de posibles desviaciones.                                                                     |
| 2        | Sistema: Recupera los proyectos e hitos de la última información consolidada válida y las reglas de alerta vigentes.                                  |
| 3        | Sistema: Comprueba, con el registro de evaluaciones, que esa versión de datos no haya sido evaluada con las mismas reglas.                            |
| 4        | Sistema: Verifica que los registros contengan fechas, estados y datos suficientes para su evaluación.                                                 |
| 5        | Sistema: Aplica las reglas para identificar retrasos o desviaciones.                                                                                  |
| 6        | Sistema: Identifica las condiciones de alerta y comprueba si ya existen alertas activas para esos proyectos.                                          |
| 7        | Sistema: Registra las alertas nuevas sin duplicar las existentes, guarda el registro de la evaluación y deja la información disponible para consulta. |
| 8        | Sistema: Envía al responsable de cada proyecto la notificación por correo de sus alertas nuevas y registra el resultado del envío.                    |

**Flujos alternativos**

- **FA-01 (paso 1).** La evaluación se activa por la extensión de CU-09 tras consolidar información válida. El sistema comienza en el paso 2 con la información recién actualizada.

- **FA-02 (paso 3).** La versión de datos ya fue evaluada con las mismas reglas. El sistema registra que la evaluación se omitió y termina sin crear alertas.

- **FA-03 (paso 4).** Un proyecto no tiene datos suficientes. El sistema registra que no puede evaluarse y continúa con los demás en el paso 5.

- **FA-04 (paso 6).** Ningún proyecto presenta condiciones de alerta. El sistema registra la evaluación sin nuevas desviaciones y continúa en el paso 7; no hay notificaciones que enviar.

- **FA-05 (paso 6).** Una condición detectada ya tiene una alerta activa. El sistema conserva esa alerta, no genera otra igual ni la vuelve a notificar, y continúa en el paso 7.

- **FA-06 (paso 8).** El servidor de correo no está disponible o rechaza el envío. El sistema registra la notificación como fallida; la alerta permanece activa y visible en el dashboard.

**Excepciones**

- **E-01 (paso 2).** El sistema no puede recuperar la información consolidada necesaria. Registra el problema y termina sin generar nuevas alertas.

**Requisitos especiales**

1.  **Rendimiento:** con 100 proyectos, completa la evaluación en menos de 60 segundos.

2.  **Exactitud:** en 20 situaciones previamente clasificadas, identifica correctamente las 20 condiciones según las reglas establecidas.

3.  **Fiabilidad:** no existen dos alertas activas para el mismo proyecto y la misma condición.

4.  **Trazabilidad:** cada alerta indica el proyecto relacionado, la condición detectada y la fecha de generación.

**Observación:** las fórmulas de avance, los umbrales de retraso y las condiciones exactas de alerta deben validarse con los responsables de la cooperativa.

## 2.6 Matriz de trazabilidad

La matriz relaciona los objetivos específicos de Visión Integral 360 con los casos de uso vigentes y comprueba la coherencia con los requisitos de la sección 1.6.

**Objetivos específicos y casos de uso**

| **Código** | **Objetivo específico**                                                                 | **Casos de uso**                                | **Justificación**                                                                                                                                                                |
|------------|-----------------------------------------------------------------------------------------|-------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OE-01      | Identificar y documentar a los interesados (ISO/IEC/IEEE 42010).                        | CU-01, CU-02, CU-05, CU-09, CU-11               | Reflejan las necesidades de la jefa de Desarrollo, la alta dirección, los responsables de proyecto y el administrador.                                                           |
| OE-02      | Definir mecanismos de obtención, normalización y correspondencia entre Redmine y Excel. | CU-02, CU-09, CU-11                             | CU-09 obtiene y consolida; CU-02 permite consultar la información relacionada (incluidos los registros sin asociar); CU-11 revela problemas de sincronización o correspondencia. |
| OE-03      | Describir la solución con las vistas 4+1 con trazabilidad.                              | CU-01, CU-02, CU-09, CU-10                      | Representan las interacciones principales y sirven de referencia para las demás vistas.                                                                                          |
| OE-04      | Priorizar atributos de calidad verificables.                                            | CU-01, CU-09, CU-10, CU-11                      | CU-01 controla el acceso; CU-09 aborda interoperabilidad y fallos de fuente; CU-10 evita alertas incorrectas o duplicadas; CU-11 permite revisar problemas.                      |
| OE-05      | Construir un prototipo mínimo con dos fuentes, información consolidada, KPI y alertas.  | CU-01, CU-02, CU-04, CU-05, CU-08, CU-09, CU-10 | CU-09 consolida; CU-01, CU-02 y CU-08 consultan y comparan; CU-04 presenta indicadores; CU-10 genera alertas y CU-05 las revisa.                                                 |

**Requisitos funcionales y casos de uso**

| **Requisito** | **Descripción abreviada**                                            | **Casos de uso**           |
|---------------|----------------------------------------------------------------------|----------------------------|
| RF-01         | Consultar proyectos, iniciativas y requerimientos desde Redmine.     | CU-02, CU-09               |
| RF-02         | Obtener los datos complementarios del Excel online.                  | CU-02, CU-09               |
| RF-03         | Normalizar y relacionar registros comunes, registrando los ambiguos. | CU-02, CU-09, CU-11        |
| RF-04         | Vista consolidada de cada proyecto, hitos, avances y responsables.   | CU-01, CU-02               |
| RF-05         | Calcular indicadores a partir de fórmulas documentadas.              | CU-01, CU-04               |
| RF-06         | Señalar retrasos y desviaciones mediante reglas de alerta.           | CU-05, CU-10               |
| RF-07         | Vistas y consultas por perfil.                                       | CU-01, CU-02, CU-08        |
| RF-08         | Mostrar origen y última fecha de actualización.                      | CU-01, CU-02, CU-09, CU-11 |
| RF-09         | Consultar iniciativas y requerimientos de un proyecto.               | CU-02                      |
| RF-10         | Consultar hitos y plazos de un proyecto.                             | CU-02                      |
| RF-11         | Consultar el seguimiento semanal de un proyecto.                     | CU-02                      |
| RF-12         | Comparar el estado de proyectos en un período.                       | CU-08                      |
| RF-13         | Registrar sincronizaciones, resultado por fuente e incidencias.      | CU-09, CU-11               |
| RF-14         | Notificar por correo las alertas nuevas.                             | CU-10                      |

**Verificación de la trazabilidad.** La matriz permite comprobar que:

1.  Los cinco objetivos específicos se relacionan con al menos un caso de uso.

2.  Los ocho casos de uso vigentes participan en la cobertura de los objetivos (CU-03, CU-06 y CU-07 se fusionaron en CU-02).

3.  Los catorce requisitos funcionales se relacionan con al menos un caso de uso.

4.  Los tres casos especificados (CU-01, CU-09 y CU-10) representan funciones prioritarias de consulta, integración y generación de alertas.

Los objetivos OE-01 y OE-03 no se cumplen únicamente con funcionalidades del sistema: también requieren documentar los interesados y elaborar las vistas del DAS. OE-04 necesita además escenarios y pruebas que verifiquen los atributos de calidad.
