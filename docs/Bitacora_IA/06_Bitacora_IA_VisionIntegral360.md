# BITÁCORA DE USO DE IA · Visión Integral 360

**Grupo B:** Diana Bermeo · Camilo Fierro · Steven Vega · Lady Robalino
**Docente:** Mgtr. Jackson Masache · **Entrega final del DAS:** 27/11/2026

Formato de cada entrada (TDR): fecha, herramienta/modelo, objetivo, prompt, resumen de la respuesta, qué usamos, qué descartamos y por qué, verificación y error de la IA.

> **Nota para el equipo:** las entradas se armaron con lo que quedó registrado en el DAS y en la bitácora anterior. Los campos marcados con **[Equipo: completar]** no aparecen en ningún documento: hay que llenarlos con el historial real del chat antes de subir la bitácora. El profe dijo que una plantilla sin llenar no cuenta.

---

### IA-00 · 20/10/2026 · S2 – Propuesta de solución (sección 1 del DAS)

- **Integrante:** [Equipo: completar]
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Estructurar la propuesta de solución e identificar a los interesados del reto.
- **Prompt (resumen):** Contexto de la reunión con la jefa del Departamento de Desarrollo de Software de la cooperativa Padre Julián Lorente. Redmine recoge datos de GitLab y SonarQube, y un Excel compartido comparte con Redmine tres campos: proyectos, iniciativas y requerimientos. Se pidió ayuda para crear una página que consuma Redmine y el Excel online e identificar otros stakeholders.
- **Respuesta (resumen):** Una propuesta en Word con stakeholders y roles, alcance, fuentes, requisitos funcionales y no funcionales, supuestos, visión y plan semanal.
- **Qué usamos:** La estructura de la propuesta, los stakeholders y la organización en RF/RNF.
- **Qué descartamos y por qué:** Las integraciones directas con GitLab y SonarQube. Solo llegan a Redmine y ese funcionamiento no está confirmado (sección 1.5).
- **Verificación:** Se contrastó con el TDR (Anexo B, Grupo B) y con el relato de la reunión con la cooperativa.
- **¿Error de la IA?:** [Equipo: completar]
- **Decisión del grupo:** Aceptado con correcciones.

---

### IA-01 · 25/10/2026 · S3 – Foro sobre trabajo colaborativo con Git (Opción C)

- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Saber si conviene trabajar con ramas individuales y Pull Requests en lugar de hacer cambios directamente en `main`.
- **Prompt:** "En Git, nuestro equipo no está trabajando directo en main, sino que usa ramas por cada integrante del equipo, por sus nombres, con Pull Request. Defiende una de las dos opciones para la etapa actual del proyecto (documentación del DAS) o si preferirías cambiar de opinión cuando empiece el desarrollo del código".
- **Respuesta:** Recomendó mantener ramas independientes y Pull Requests. Para cuando empiece la programación sugirió ramas por funcionalidad, revisiones de código y pruebas antes de integrar.
- **Qué usamos:** Seguir con ramas y Pull Requests, con `main` para las versiones finales y `develop` para integrar los avances.
- **Qué descartamos y por qué:** Cambiar ya a ramas por funcionalidad. Cada integrante tiene su rama y todavía estamos aprendiendo Git.
- **Verificación:** Se contrastó con la documentación oficial de Git (`git-merge`). Fuente: https://git-scm.com/docs/git-merge
- **¿Error de la IA?:** Omisión. No explicó cómo resolver conflictos ni aclaró que las ramas no los evitan todos.
- **Decisión del grupo:** Mantener ramas individuales y Pull Requests. Usar ramas por funcionalidad cuando empiece el desarrollo del código.

---

### IA-02 · 26/10/2026 · S3 – Actores y casos de uso

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Identificar los actores y organizar los casos de uso de Visión Integral 360.
- **Prompt (resumen):** Orientación para los casos de uso, tomando como referencia CampusEats, manteniendo la primera versión del DAS y separando a los actores de los sistemas externos.
- **Respuesta (resumen):** Identificó a los usuarios del dashboard y a los sistemas externos (Redmine, Excel online). Propuso un catálogo de 11 casos de uso.
- **Qué usamos:** Los actores, el catálogo de 11 casos de uso y sus prioridades.
- **Qué descartamos y por qué:** Etiquetas innecesarias en los nombres de los actores. Las integraciones directas con GitLab y SonarQube, porque no están confirmadas.
- **Verificación:** Se contrastó con el DAS inicial, la entrevista y las indicaciones del docente.
- **¿Error de la IA?:** Omisión. Hubo que ajustarla para conservar los requisitos de la primera versión.
- **Decisión del grupo:** Conservar los actores y el catálogo de 11 casos de uso.

---

### IA-03 · 26/10/2026 · S3 – Diagrama de casos de uso UML

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Representar los actores, los casos de uso y sus relaciones en PlantUML.
- **Prompt (resumen):** Cómo poner los actores fuera de la frontera y cómo usar «include» y «extend».
- **Respuesta (resumen):** Código PlantUML con los actores, los 11 casos de uso, la frontera y las relaciones.
- **Qué usamos:** La estructura del diagrama y el «include» de CU-01 a CU-04.
- **Qué descartamos y por qué:** En ese momento se descartó el «extend» entre CU-10 y CU-09 y se usó «include».
- **Verificación:** Se compararon las relaciones con el catálogo y con las especificaciones de CU-09 y CU-10.
- **¿Error de la IA?:** Omisión de coherencia entre la relación y la especificación.
- **Decisión del grupo:** «include» entre CU-09 y CU-10. **Corregido después (ver IA-08):** la versión final del DAS usa **CU-10 «extend» CU-09** (sección 2.2 y decisión P-2 de la vista de procesos), porque CU-10 solo se ejecuta si la evaluación está habilitada y esa versión de los datos no fue evaluada.

---

### IA-04 · 26/10/2026 · S3 – Revisión de especificaciones

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Revisar las especificaciones, sobre todo los flujos alternativos y las excepciones.
- **Prompt (resumen):** Cómo redactar precondiciones, postcondiciones, flujos y excepciones con el formato de CampusEats.
- **Respuesta (resumen):** Revisó CU-01, CU-09 y CU-10 y propuso ajustar los pasos, los puntos de inicio de los flujos alternativos y las excepciones.
- **Qué usamos:** La estructura de las tres especificaciones, el formato `E-01 (Paso X)` y los requisitos especiales medibles.
- **Qué descartamos y por qué:** Cambiar CU-10 por CU-05 entre los casos prioritarios. Se corrigió además una excepción que señalaba dos pasos.
- **Verificación:** Se comparó con CampusEats y con el Taller 2: flujos de 5 a 10 pasos, al menos dos flujos alternativos y requisitos medibles.
- **¿Error de la IA?:** Omisión. Algunos flujos no cumplían la estructura pedida.
- **Decisión del grupo:** Mantener CU-01, CU-09 y CU-10 como casos prioritarios.

---

### IA-05 · 26/10/2026 · S3 – Matriz de trazabilidad

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Relacionar los objetivos específicos con los casos de uso.
- **Prompt (resumen):** Relacionar los casos de uso con los cinco objetivos de la primera versión y distinguir los objetivos de arquitectura de las funciones del sistema.
- **Respuesta (resumen):** Una matriz de objetivos y casos de uso, más una tabla con RF-01 a RF-08.
- **Qué usamos:** La matriz, sus justificaciones y la correspondencia con los RF.
- **Qué descartamos y por qué:** Objetivos nuevos. También se evitó tratar las actividades del DAS (stakeholders, vistas 4+1) como funciones del dashboard.
- **Verificación:** Se comparó con los objetivos de la primera versión y se revisó que cada objetivo tuviera al menos un caso de uso.
- **¿Error de la IA?:** Omisión. Algunos objetivos se cumplen con trabajo de arquitectura y no con funciones del sistema.
- **Decisión del grupo:** Mantener los cinco objetivos originales.

---

### IA-06 · 26/10/2026 · S3 – Preparación del PDF de entrega

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Dar al documento de casos de uso el formato de entrega.
- **Prompt (resumen):** Pasar el Markdown del DAS a PDF con portada, diagrama UML, tablas y especificaciones.
- **Respuesta (resumen):** Estructuró el PDF con portada y los cinco apartados de la sección 2.
- **Qué usamos:** La organización, la portada y la presentación de las tablas.
- **Qué descartamos y por qué:** La primera versión del PDF, porque no incluía la imagen del diagrama UML.
- **Verificación:** Se revisó contra el Taller 2 que estuvieran la portada, los cinco apartados y el diagrama.
- **¿Error de la IA?:** Omisión. Faltaba el diagrama en la primera conversión.
- **Decisión del grupo:** Usar el PDF corregido, después de la revisión del equipo.

---

### IA-07 · [Equipo: completar fecha] · S4 – Vista lógica del dominio (sección 3)

- **Integrante:** [Equipo: completar]
- **Herramienta:** [Equipo: completar]
- **Objetivo:** Construir el modelo de dominio a partir de escenarios con datos concretos.
- **Prompt (resumen):** [Equipo: completar desde el historial]
- **Respuesta (resumen):** Según el DAS, el resultado fue: cuatro escenarios con datos concretos (E-01 a E-04 con P-001, I-003, R-015, H-01), tabla de candidatos con las cinco preguntas, diagrama de 17 clases con multiplicidades, diccionario de clases y trazabilidad.
- **Qué usamos:**
  - Las cinco preguntas para decidir si un candidato es clase.
  - Los tipos del negocio en lugar de String.
  - La clase escondida ResultadoFuente.
  - La restricción **{xor}** de ReferenciaOrigen.
  - Las cuatro clases nuevas de la versión corregida: RegistroEvaluacion, Notificacion, IncidenciaSincronizacion y PerfilUsuario.
- **Qué descartamos y por qué:**
  - Como clases: los actores, los sistemas externos (Redmine, Excel, SMTP) y las vistas, porque fallan la pregunta P5.
  - "Registro de errores", "tabla de base de datos" y "GitLab/SonarQube".
- **Verificación:** [Equipo: completar] (por ejemplo, revisar que cada clase pase las cinco preguntas y que las multiplicidades estén en ambos extremos).
- **¿Error de la IA?:** [Equipo: completar]
- **Decisión del grupo:** 17 clases de dominio. Pendientes con la cooperativa: la fórmula de avance, los umbrales de retraso y las claves comunes entre Redmine y Excel (3.5).

---

### IA-08 · [Equipo: completar fecha] · S5 – Vista de procesos (sección 4)

- **Integrante:** [Equipo: completar]
- **Herramienta:** [Equipo: completar]
- **Objetivo:** Hacer los diagramas de robustez y de secuencia de los ocho casos vigentes y corregir lo que observó el docente.
- **Prompt (resumen):** [Equipo: completar desde el historial]
- **Respuesta (resumen):** Según el DAS, el resultado fue: robustez y secuencia de CU-01, 02, 04, 05, 08, 09, 10 y 11 (figuras 6 a 23), diagrama de clases solo con entidades (figura 24) y la tabla caso de uso → secuencia → operaciones por entidad (4.11).
- **Qué usamos (decisiones P-1 a P-7):**
  - El Temporizador entra por el borde **Planificador**.
  - **CU-10 «extend» CU-09**.
  - **Mensaje asíncrono** `encolarSincronizacion` en la sincronización manual (FA-04).
  - El correo sale por **AdaptadorCorreo**.
  - El diagrama de clases lleva solo entidades.
- **Qué corregimos por la retroalimentación del docente:**
  - El Temporizador hablaba directo con el control.
  - Faltaba el mensaje asíncrono.
  - Faltaba la tabla de trazabilidad.
  - El diagrama de clases incluía pantallas, controles y adaptadores.
- **Verificación:** El DAS registra que todas las operaciones de la figura 24 aparecen en alguna secuencia y viceversa (4.11). [Equipo: añadir cómo lo comprobaron.]
- **¿Error de la IA?:** [Equipo: completar]
- **Decisión del grupo:** Aceptada con las correcciones. Quedan pendientes las especificaciones de CU-02, 04, 05, 08 y 11 en la sección 2.5.

---

### IA-09 · 16/11/2026 · S6 – Vista de desarrollo (sección 5)

- **Integrante:** Lady Robalino.
- **Herramienta:** Claude (chat).
- **Objetivo:** Revisar la vista de desarrollo: paquetes con estereotipo, dependencias justificadas, tabla de plataformas, chequeo con los controles y adaptadores, y carpetas del repositorio.
- **Prompt (resumen):** Se compartieron el DAS, los diagramas de casos de uso, de robustez y de secuencia de CU-01, CU-09 y CU-10, el diagrama de clases y la estructura del repositorio.
- **Respuesta (resumen):** Nueve paquetes con estereotipo, once dependencias justificadas, una tabla de plataformas provisional, el chequeo de controles y adaptadores, y carpetas por paquete.
- **Qué usamos:**
  - Paquetes agrupados por función.
  - La regla de dirección: los dominios dependen de utilitarios y plataformas, nunca al revés.
  - Los adaptadores en integración.
  - Un control por caso de uso.
  - Carpetas por paquete y no por tipo técnico.
- **Qué descartamos y por qué:**
  - Un solo paquete de dominio, porque formaba un ciclo entre Seguimiento y Alertas.
  - La flecha del Temporizador a integración, que quedó como nota.
  - Las carpetas por tipo técnico.
  - Los servidores, que corresponden a la semana 7.
- **Verificación:** Se recorrieron las dependencias a mano buscando ciclos y se cruzó cada control y adaptador con su paquete.
- **¿Error de la IA?:** Dos. La numeración de la sección estaba mal, y la primera propuesta de dependencias tenía un ciclo.
- **Corrección posterior (retroalimentación del docente):**
  - Se pasó de 9 a **13 paquetes** (11 de código y 2 plataformas).
  - Paquetes en notación UML, sin flechas «include».
  - Persistencia y Tareas programadas pasaron a **«utilitario»**, porque tienen código propio.
  - ControlIntegracion pasó al paquete de dominio Consolidación.
  - La plataforma se unificó en **Node.js 22 + BullMQ**: se descartaron Django y Celery, que contradecían la vista de despliegue.
- **Decisión del grupo:** Aprobada con las correcciones. [Equipo: confirmar quién verificó la versión final.]

---

### IA-10 · 23/11/2026 y 26/11/2026 · S7 – Vista de despliegue (sección 6)

- **Integrante:** [Equipo: completar]
- **Herramienta:** Claude (Anthropic).
- **Objetivo:** Proponer la vista de despliegue y después adaptarla al DAS corregido (secciones 1 a 5) y a la retroalimentación del docente.
- **Prompt (resumen):**
  - Taller 7: el enunciado y el PDF con las vistas lógica y de procesos y el DAS hasta la sección 5. El equipo indicó Node.js, Microsoft Graph y alertas por dashboard y correo SMTP.
  - Corrección: el DAS corregido y las observaciones del docente sobre la legibilidad del diagrama, la bitácora y la presentación.
- **Respuesta (resumen):** Cuatro componentes, tres nodos propios, comunicaciones con protocolo y puerto, tres decisiones con su alternativa descartada, supuestos, trazabilidad y el código PlantUML del diagrama.
- **Qué usamos:** La estructura 6.1 a 6.8, los componentes, las tres decisiones (sincronización en el worker, el dashboard habla con la API, el Excel se lee por Microsoft Graph), la tabla de comunicaciones y el recorrido de AdaptadorExcel.
- **Qué corregimos y por qué:**
  - Se pasó de nueve paquetes a los 13 de la sección 5, porque Avance, RegistroSincronizacion y Registro de errores no existen en el vocabulario 1.9.
  - Persistencia y Tareas programadas pasaron a «utilitario».
  - Se cambió a CU-10 «extend» CU-09.
  - El dashboard pasó a "React compilado".
  - Se borraron restos de otro ejercicio ("ReservaSalas").
  - El diagrama quedó con orientación de arriba abajo, fondo claro y una etiqueta con protocolo y puerto por línea (observación del docente).
- **Qué descartamos y por qué:** [Equipo: indicar si se descartó alguna propuesta. Si no, escribirlo.]
- **Verificación:**
  - Se comparó la lista de 6.8 con la tabla 5.3: aparecen los 13 paquetes.
  - Se revisaron las 9 conexiones del archivo `.puml` y todas llevan protocolo y puerto.
  - [Equipo: anotar si el `.puml` generó el diagrama sin errores.]
- **¿Error de la IA?:** Usó nombres que no existían en el vocabulario y dejó restos de otro ejercicio. Se corrigieron.
- **Decisión del grupo:** Aceptada con correcciones.

---

### IA-11 · 27/11/2026 · S8 – Preparación de la presentación final

- **Integrante:** Lady Robalino.
- **Herramienta:** Claude (chat).
- **Objetivo:** Estudiar el DAS completo y preparar la exposición de la vista de despliegue (diapositivas 10 a 12 sobre CU-02).
- **Prompt (resumen):** Se compartieron las indicaciones del docente para la semana 8, las secciones 1 a 6 del DAS, las diapositivas y los archivos `.puml` de componentes y despliegue. Se pidió una guía para entender y exponer la parte asignada y para responder preguntas sobre cualquier vista.
- **Respuesta (resumen):** Una guía con los conceptos de despliegue, un guion por diapositiva, la explicación de las 9 líneas del diagrama, las tres decisiones y preguntas probables con su respuesta.
- **Qué usamos:** El guion y la tabla de comunicaciones para practicar. También la respuesta sobre redundancia: no hay redundancia (una instancia por nodo), pero sí aislamiento de fallas entre api y worker.
- **Qué descartamos y por qué:** [Equipo: completar]
- **Verificación:** Los datos de la guía se contrastaron con las tablas 6.3 y 6.4 y con los `.puml`. La IA detectó que una captura de la trazabilidad de CU-09 usaba nombres viejos ("DisparadorSincronizacion", "Orquestación de integración"). Se confirmó en el DAS que los vigentes son **Planificador**, **Consolidación** e **Integración de fuentes**.
- **¿Error de la IA?:** [Equipo: completar]
- **Decisión del grupo:** Usar los nombres del vocabulario 1.9 en toda la exposición.
