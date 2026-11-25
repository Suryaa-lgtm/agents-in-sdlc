---
title: "Ejercicio 2: Añadir funcionalidad con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas de una aplicación suelen requerir cambios en varios archivos y operaciones como ejecutar pruebas. Como desarrollador, normalmente tienes que localizar todos los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo te has dejado y realizar otra actualización... La lista continúa.

Para eso está el modo agente de Copilot.

El modo agente de Copilot está diseñado para trabajar de forma más autónoma en el IDE. Se comporta de forma parecida a un desarrollador: empieza explorando la estructura del proyecto, realiza las actualizaciones necesarias, ejecuta tareas como las pruebas y corrige automáticamente los errores que detecta. Veamos cómo puedes utilizar el modo agente para añadir funcionalidades al sitio.

> [!NOTE]
> Aunque los nombres se parecen, el modo agente y el agente en la nube están diseñados para ofrecer experiencias distintas. El modo agente realiza las tareas en el IDE, lo que permite obtener comentarios e interactuar con rapidez. El agente en la nube está diseñado para trabajar de forma asincrónica como un colaborador del equipo, interactuando contigo mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio aprenderás cómo:

- el modo agente de Copilot puede explorar el proyecto, identificar archivos pertinentes y coordinar cambios;
- el modo agente de GitHub Copilot puede implementar nuevas funcionalidades en la interfaz de usuario y la capa de datos;
- revisar los cambios y las pruebas generados por el modo agente de Copilot antes de combinarlos en la base de código.

## Escenario

A medida que crece la lista de juegos, quieres permitir que los usuarios filtren por categoría y editor. En el ejercicio anterior ya añadiste una función auxiliar para obtener editores; ahora terminarás con el modo agente de Copilot el resto del trabajo de la capa de datos, la interfaz de usuario y las pruebas.

## Ejecuta el sitio web de Tailspin Toys

Antes de hacer cambios, exploremos el sitio web de Tailspin Toys para conocer sus funciones actuales.

El sitio web es una plataforma de financiación colectiva de juegos de mesa con un tema de desarrollo. Permite mostrar juegos y consultar sus detalles. El sitio es una única aplicación Astro que genera las páginas como HTML estático durante la compilación. Las páginas consultan directamente una base de datos SQLite local desde su frontmatter mediante Drizzle ORM; no hay una API de backend independiente ni un marco de trabajo de interfaz del lado del cliente. Las funciones auxiliares reutilizables para acceder a los datos se encuentran en `src/lib/`, y cualquier interactividad se añade mediante un pequeño `<script>` de Astro con ámbito limitado y las API estándar del DOM.

### Inicia el sitio web

Para que resulte más fácil ejecutar el sitio web, se ha proporcionado la tarea `npm run dev`, que inicia el único servidor de desarrollo de Astro. Puedes ejecutarlo en tu GitHub Codespace siguiendo estos pasos:

1. Vuelve al codespace. Después del ejercicio anterior deberías estar en `main`.
2. Abre una ventana de terminal nueva en el codespace pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama nueva para este trabajo de filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Ejecuta este comando para iniciar el sitio web:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, verás un mensaje con la URL, parecido al siguiente:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo que te pide abrir una ventana del navegador para `http://localhost:4321`, ciérralo seleccionando **x**.

5. Abre el sitio web manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando en el terminal la dirección del servidor Astro `http://localhost:4321`.

> [!NOTE]
> Si utilizas un codespace, al seleccionar un enlace a la URL localhost en el terminal del codespace, se te redirigirá automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Se trata de un túnel privado al codespace, que ahora aloja el servidor web.

### Explora el sitio web

Cuando el sitio esté en marcha, puedes explorar sus funciones. Entre las principales se encuentran:

- **Página de inicio**: muestra una lista de juegos de mesa con sus títulos, imágenes y descripciones.
- **Página de detalles del juego**: al seleccionar un juego, accederás a una página de detalles con más información, como el título, la descripción, el editor y la categoría.

## Explora la lista de tareas pendientes con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los ejercicios siguientes, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y la selección del modelo varían según el ejercicio; cada paso lo indicará cuando sea pertinente.

La implementación inicial del sitio web funciona, pero queremos mejorarla y añadir nuevas funciones. Empecemos revisando la lista de tareas pendientes. Al configurar el proyecto a partir de la plantilla, se generó automáticamente una lista de incidencias; pide a GitHub Copilot que te muestre esos elementos.

1. En el menú desplegable de agentes de la vista Chat, selecciona **Agent**. El agente **Agent** planifica e implementa cambios de forma autónoma en varios archivos, ejecuta comandos de terminal y utiliza herramientas.

   ![Captura de pantalla del selector de agentes en la vista Chat.](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no expresan ninguna preferencia por un modelo concreto. Durante su desarrollo utilizamos Claude Sonnet 4.5, por lo que lo hemos incluido en las instrucciones. Esperamos así que las sugerencias de código sean relativamente coherentes y la experiencia resulte satisfactoria. Sin embargo, como los modelos de lenguaje grandes (LLM) son probabilísticos, es posible que las sugerencias que recibas difieran de las indicadas en el taller. Es completamente normal y esperable.

> [!NOTE]
> Debido al carácter probabilístico de los LLM, Copilot podría utilizar un comando MCP distinto, pero debería poder completar la tarea.

3. Pide a Copilot que te muestre la lista de incidencias pendientes enviándole esta instrucción:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para ejecutar el comando que enumera todas las incidencias.
5. Revisa la lista de incidencias generada.

Observa que Copilot incluso ha priorizado los elementos según cuáles considera más útiles para el usuario.

## Revisa los archivos de instrucciones

Antes de poner al agente a generar código, conviene revisar el archivo de instrucciones que utilizarás para proporcionar contexto a Copilot. Aprovecharás el archivo de [interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que contiene información sobre cómo abordar la incorporación de funcionalidades al sitio web.

1. En el codespace, abre `.github/instructions/ui.instructions.md`.
2. Fíjate en las directrices generales para abordar la incorporación de funcionalidades. Incluyen:
   - una descripción general de la arquitectura;
   - principios para el diseño de componentes, su capacidad de prueba y la accesibilidad;
   - enlaces a archivos de instrucciones específicos para varios tipos de archivos, incluidos:
     - Astro;
     - Tailwind CSS;
     - Drizzle.

> [!TIP]
> Los archivos de instrucciones permiten hacer referencia tanto a otros archivos de instrucciones como a archivos del proyecto. Las rutas son relativas a la ubicación del archivo de instrucciones. Así puedes reutilizar instrucciones, dividir conjuntos complejos en partes más pequeñas y manejables y proporcionar ejemplos y plantillas.

## Implementa la funcionalidad de filtrado

Para completar el filtrado, la aplicación necesitará al menos tres cambios independientes:

- añadir o mejorar la lógica de filtrado restante en la capa de datos (`src/lib/`);
- añadir o actualizar las pruebas del comportamiento del filtrado;
- actualizar la página de lista de juegos para incorporar la interfaz de filtrado.

Además, las pruebas deben ejecutarse y pasar antes de combinar los cambios en la base de código. ¡El modo agente de Copilot puede hacer estas tareas por ti! Vamos a añadir la funcionalidad.

1. Puedes continuar la conversación actual con Copilot o iniciar otra seleccionando **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui** como archivo de instrucciones.

   ![Captura de pantalla con un ejemplo de selección del archivo de instrucciones de interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Comprueba que **Agent** sigue seleccionado en el menú desplegable de agentes de la vista Chat.

   ![Captura de pantalla del selector de agentes en la vista Chat.](../../../_images/shared-chat-mode-selector.png)

4. Comprueba que **Claude Sonnet 4.5** siga seleccionado como modelo.
5. Pide a Copilot que implemente la funcionalidad según la incidencia relacionada de la lista de tareas pendientes, utilizando esta instrucción:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot empieza explorando el proyecto y localizando los archivos relacionados con la funcionalidad. Deberías ver que encuentra tanto las funciones auxiliares de la capa de datos como la interfaz y las pruebas. Después, comienza a modificar los archivos y a ejecutar las pruebas.

   ![Captura de pantalla de Copilot explorando los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Observarás que Copilot realiza varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. Según la complejidad de la tarea y de la base de código, puede tardar unos minutos. Durante el proceso, es posible que aparezcan los botones **Keep** y **Undo** en el editor de código. Cuando Copilot termine, tendrás la opción **Keep** o **Undo** para todos los cambios, así que no hace falta que los selecciones mientras el trabajo siga en curso.

7. Cuando Copilot te lo pida, selecciona **Continue** para ejecutar las pruebas.

   ![Captura de pantalla de un cuadro de diálogo en el panel Copilot Chat que pide al usuario confirmar que quiere ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Es posible que haya pausas e incluso que algunas pruebas fallen durante el proceso. No pasa nada. Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea y dejar de detectar errores.

   ![Captura de pantalla de una sesión completa con el modo agente de Copilot](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explora el código generado para detectar posibles problemas.

> [!CAUTION]
> Recuerda que siempre es importante revisar el código que genera Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador donde se está ejecutando el sitio web y explora la nueva funcionalidad.
11. Cuando hayas confirmado que todo funciona y revisado el código, selecciona **Keep** en la ventana de Copilot Chat.

## Resumen y próximos pasos

¡Enhorabuena! En este ejercicio has aprendido a utilizar el modo agente de GitHub Copilot para añadir funciones al sitio web de Tailspin Toys. Has aprendido cómo:

- el modo agente de GitHub Copilot puede implementar nuevas funcionalidades en la interfaz de usuario y la capa de datos;
- el modo agente de Copilot puede explorar el proyecto, identificar archivos pertinentes y coordinar cambios;
- revisar los cambios y las pruebas generados por el modo agente de Copilot antes de combinarlos en la base de código.

Ahora [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar la paginación

A medida que crezca la lista de juegos, será necesario habilitar la paginación. Utiliza lo aprendido en este ejercicio para pedir a Copilot que actualice el sitio e implemente la paginación. Algunas cuestiones que debes tener en cuenta:

- sigue las prácticas recomendadas existentes, incluido el uso de los archivos de instrucciones disponibles;
- decide cómo quieres implementar la paginación: por ejemplo, si permitirás que el usuario seleccione el tamaño de página o si se establecerá de forma fija;
- al redactar la instrucción, proporciona a Copilot las directrices necesarias para crear la implementación que quieres;
- quizá tengas que iterar con GitHub Copilot, solicitando cambios y proporcionando contexto. Este es el flujo habitual de trabajo con Copilot.

## Recursos

- [Copilot: modos Ask, Edit y Agent: qué hacen y cuándo utilizarlos][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
