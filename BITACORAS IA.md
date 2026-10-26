
# BITACORAS IA

## 25 de Octubre de 2026
- **Herramienta:** ChatGPT – GPT-6.

- **Objetivo:** Resolver la actividad del foro sobre el uso de Git y comprobar si las respuestas de la IA son correctas.

- **Prompt:** "Hola, tengo que hacer una actividad para la universidad sobre Git, es de una clase que el profe nos dió el viernes y me tocó elegir una de tres situaciones. Quiero trabajar con la opción B, que trata sobre un compañero que subió por error un archivo .env con un token de acceso y después lo borró e hizo otro commit. Ayúdame a redactar mi respuesta con palabras sencillas, como estudiante de Ingeniería en Ciencias de la Computación, incluyendo los comandos que usaría y cómo evitaría que vuelva a pasar. También necesito una respuesta de IA para el punto 2 y una verificación para el punto 3, comparando la información con la documentación oficial de Git. La respuesta debe cumplir con las indicaciones del foro y no sonar demasiado técnica."

- **Respuesta de la IA:** Se explicó que borrar el archivo en un commit posterior no garantiza que el token haya dejado de estar expuesto. Se recomendó revocar el token, generar uno nuevo, agregar `.env` al `.gitignore` y utilizar `git rm --cached .env` si el archivo todavía está siendo rastreado.

- **Qué usamos y decidimos:** Utilizamos la explicación sobre la exposición de credenciales y las medidas para prevenir que vuelva a ocurrir. Se decidió proponer un archivo `.env.example` sin credenciales reales.

- **Qué descartamos y por qué:** Descartamos la idea de que borrar el archivo y hacer otro commit fuera suficiente, porque el secreto podría permanecer en el historial de Git.

- **Verificación:** La documentación oficial confirma que `.gitignore` no afecta a los archivos que ya están siendo rastreados y que `git rm --cached` permite dejar de rastrearlos sin borrar la copia local.

- **Fuentes:**
  - https://git-scm.com/docs/gitignore
  - https://git-scm.com/docs/git-rm

- **Conclusión:** La IA facilitó la elaboración de la respuesta, pero fue necesario contrastar las recomendaciones con la documentación oficial para comprobar que fueran correctas.
