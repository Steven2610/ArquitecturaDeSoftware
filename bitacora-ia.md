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

- **Decisión:** Mantener la organización actual con ramas individuales y Pull Requests. Cuando comience el desarrollo del código, considerar el uso de ramas por funcionalidades y revisar los cambios antes de integrarlos.
