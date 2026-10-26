### IA-01 · 25/10/2026 · S3 – Foro sobre trabajo colaborativo con Git (Opción C)

- **Herramienta:** ChatGPT – GPT-6.

- **Objetivo:** Consultar si es recomendable trabajar con ramas individuales y Pull Requests en lugar de realizar cambios directamente en `main`.

- **Prompt:** "En Git, nuestro equipo no está trabajando directo en main, sino que usa ramas por cada integrante del equipo, por sus nombres, con Pull Request. Defiende una de las dos opciones para la etapa actual del proyecto (documentación del DAS) o si preferirías cambiar de opinión cuando empiece el desarrollo del código".

- **Respuesta:** La IA recomendó mantener el trabajo mediante ramas independientes y Pull Requests. También sugirió que, cuando comience la programación, sería conveniente utilizar ramas por funcionalidades, realizar revisiones de código y ejecutar pruebas antes de integrar los cambios.

- **Qué usamos:** La recomendación de continuar trabajando con ramas y Pull Requests, manteniendo `main` para las versiones finales y `develop` para integrar los avances. También consideramos utilizar ramas por funcionalidades cuando empecemos a programar.

- **Qué descartamos y por qué:** No consideramos necesario cambiar inmediatamente las ramas personales por ramas de funcionalidades, porque actualmente cada integrante tiene su propia rama y estamos aprendiendo a utilizar Git.

- **Verificación:** Se contrastó la respuesta con la documentación oficial de Git, específicamente `git-merge`. Se comprobó que trabajar con ramas permite separar los cambios, pero pueden aparecer conflictos cuando dos integrantes modifican la misma parte de un archivo.
Fuente: https://git-scm.com/docs/git-merge

- **¿Error de la IA?:** Omisión. La IA mencionó la resolución de conflictos, pero no explicó cómo resolverlos ni aclaró suficientemente que trabajar con ramas no evita todos los conflictos.


 
### IA-02 · 26/10/2026 · S3 – Actores y casos de uso

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Identificar los actores y organizar los casos de uso principales de Visión Integral 360.

- **Prompt:** (Resumen de la consulta) Solicité orientación para desarrollar los casos de uso de Visión Integral 360 tomando como referencia el ejercicio CampusEats. Posteriormente pedí mantener la información de la primera versión del DAS, diferenciando los actores  de los sistemas externos.

- **Respuesta (resumen):** La IA identificó usuarios que consultarían el dashboard y sistemas externos como Redmine y Excel online. También propuso un catálogo de 11 casos de uso relacionados con proyectos, indicadores, alertas y sincronización de información.

- **Qué usamos:** La identificación de los actores, la organización del catálogo de 11 casos de uso y la asignación de prioridades según su importancia para el reto.

- **Qué descartamos y por qué:** Se eliminaron etiquetas innecesarias en los nombres de los actores y se mantuvieron Redmine y Excel online como fuentes principales. No añadimos integraciones directas con GitLab y SonarQube porque ese funcionamiento no está confirmado.

- **Verificación:** Contrasté los actores y las funcionalidades propuestas con el documento inicial del DAS, la información obtenida en la entrevista y las instrucciones del docente sobre la identificación de actores y casos de uso.

- **¿Error de la IA?:** Omisión. La propuesta inicial necesitó ajustes para conservar completamente la información y los requisitos definidos en la primera versión del DAS.

- **Decisión del grupo:** Conservar actores identificados y el catálogo de 11 casos de uso, manteniendo coherencia con los requisitos existentes.

---

### IA-03 · 26/10/2026 · S3 – Diagrama de casos de uso UML

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Comprender cómo representar correctamente los actores, casos de uso y relaciones UML mediante PlantUML.

- **Prompt:** (Resumen de la consulta) Consulté cómo organizar el diagrama de casos de uso en PlantUML, colocar los actores fuera de la frontera del sistema y utilizar las relaciones `«include»` y `«extend»` de acuerdo con el comportamiento de Visión Integral 360.

- **Respuesta (resumen):** La IA proporcionó código PlantUML con los actores y los 11 casos de uso. Explicó la frontera del sistema, las asociaciones y las relaciones entre funcionalidades.

- **Qué usamos:** La estructura del diagrama en PlantUML, los actores y casos de uso previamente definidos y la relación `«include»` entre CU-01 y CU-04.


- **Qué descartamos y por qué:** Se descartó la relación   «extend» propuesta inicialmente entre CU-10 y CU-09,  porque en nuestra especificación establecimos que toda
  sincronización completada con información válida debe   ejecutar la evaluación de alertas. Por eso utilizamos
  «include», aunque la evaluación no siempre genere  alertas nuevas.

- **Verificación:** Comparamos las relaciones del diagrama   PlantUML con el catálogo de casos de uso y las  especificaciones de CU-09 y CU-10. Corregimos la
  relación para que el diagrama represente el mismo   comportamiento descrito en el DAS.

- **¿Error de la IA?:** Omisión. La IA no mantuvo   inicialmente la coherencia entre la relación UML
  propuesta y el comportamiento definido posteriormente   en las especificaciones.

- **Decisión del grupo:** Utilizar «include» entre CU-09 y CU-10, manteniendo la evaluación de alertas como parte del resultado de una sincronización válida.
---

### IA-04 · 26/10/2026 · S3 – Revisión de especificaciones

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Revisar la estructura de las especificaciones de casos de uso, especialmente los flujos alternativos y las excepciones.

- **Prompt:** (Resumen de la consulta) Consulté cómo redactar las precondiciones, postcondiciones, flujos y excepciones de los casos de uso de Visión Integral 360. Pedí revisar las excepciones siguiendo el formato del documento CampusEats y comprobar su relación con los actores y el diagrama UML.

- **Respuesta (resumen):** La IA revisó las especificaciones de CU-01, CU-09 y CU-10. Propuso ajustar los pasos de los flujos principales, identificar el punto donde empiezan los flujos alternativos y describir las excepciones indicando el error y la respuesta del sistema.

- **Qué usamos:** La estructura de las tres especificaciones, el formato `E-01 (Paso X)` para las excepciones y los requisitos especiales medibles.

- **Qué descartamos y por qué:** Se descartó sustituir CU-10 por CU-05 entre los tres casos prioritarios, porque CU-10 ya formaba parte de la selección y estaba relacionado con la sincronización de fuentes. También se corrigió una excepción que señalaba dos pasos en vez de uno concreto.

- **Verificación:** Comparé las especificaciones con mi actividad de CampusEats y con los requisitos del Taller 2: precondiciones como estados, flujos de entre 5 y 10 pasos, al menos dos flujos alternativos, manejo de fallos externos y requisitos con valores medibles.

- **¿Error de la IA?:** Omisión. Algunas versiones iniciales de los flujos y excepciones no cumplían completamente la estructura solicitada o no mantenían la correspondencia con las secciones anteriores.

- **Decisión del grupo:** Mantener CU-01, CU-09 y CU-10 como casos prioritarios, con las excepciones corregidas y los requisitos especiales definidos como metas iniciales.

---

### IA-05 · 26/10/2026 · S3 – Matriz de trazabilidad

- **Integrante:** Diana Bermeo.
- **Herramienta:** ChatGPT – GPT-6.
- **Objetivo:** Comprobar la relación entre los objetivos específicos del proyecto y los casos de uso definidos.

- **Prompt:** (Resumen de la consulta) Consulté cómo relacionar los casos de uso con los objetivos específicos de Visión Integral 360, conservando los cinco objetivos de la primera versión del DAS. También pedí verificar la diferencia entre los objetivos de arquitectura y las funcionalidades del sistema.

- **Respuesta (resumen):** La IA propuso una matriz que vincula los cinco objetivos específicos con los casos de uso correspondientes y una tabla complementaria con los requisitos funcionales RF-01 a RF-08.

- **Qué usamos:** La organización de la matriz, las justificaciones de relación entre objetivos y casos de uso, y la correspondencia con los ocho requisitos funcionales originales.

- **Qué descartamos y por qué:** No se incorporaron objetivos nuevos. También se evitó interpretar la identificación de stakeholders o la construcción de las vistas 4+1 como funciones que debe realizar el usuario dentro del dashboard.

- **Verificación:** Comparé los cinco objetivos utilizados en la matriz con los establecidos en la sección 3.2 de la primera versión del DAS. También revisé que todos los objetivos tuvieran al menos un caso de uso relacionado.

- **¿Error de la IA?:** Omisión. Fue necesario aclarar que algunos objetivos se cumplen mediante actividades de diseño arquitectónico y no solamente mediante las funcionalidades del sistema.

- **Decisión del grupo:** Mantener los cinco objetivos originales y utilizar la matriz para demostrar cómo contribuyen los casos de uso, diferenciando las funciones del sistema de las actividades propias del DAS.

  
- **Decisión:** Mantener la organización actual con ramas individuales y Pull Requests. Cuando comience el desarrollo del código, considerar el uso de ramas por funcionalidades y revisar los cambios antes de integrarlos.
