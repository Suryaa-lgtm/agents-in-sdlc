---
title: "Ejercicio 1: Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo agente →][next-lesson]

El contexto es clave cuando se trabaja con IA generativa. Si una tarea debe realizarse de una forma concreta —o Copilot necesita conocer información de contexto—, asegúrate de que tenga acceso a ella. Hay varias formas de compartir contexto específico con Copilot. Una de las principales son los [archivos de instrucciones][instruction-files], que permiten orientar la generación de código.

En este ejercicio:

- explorarás cómo el contexto específico del proyecto, las directrices de programación y los estándares de documentación llegan a Copilot mediante las instrucciones personalizadas del repositorio y los archivos de instrucciones asociados a rutas;
- generarás la primera parte de la capa de datos para el filtrado (una función auxiliar para obtener editores) con las instrucciones *actuales*;
- añadirás un nuevo estándar para todo el repositorio en `.github/copilot-instructions.md`;
- volverás a ejecutar la misma instrucción y observarás cómo el código generado adopta el nuevo estándar;
- confirmarás en `main` la actualización de instrucciones y la parte de filtrado para que Copilot pueda utilizar las nuevas directrices en el próximo ejercicio.

> [!CAUTION]
> Es posible que el código generado no cumpla algunos de los estándares que hayas establecido. Copilot no es determinista. El objetivo de este ejercicio es observar la *tendencia* de cambio en el comportamiento después de actualizar las instrucciones, no obtener exactamente el mismo resultado carácter por carácter.

## Archivos de instrucciones

### Escenario

Como cualquier empresa de desarrollo competente, Tailspin Toys tiene un conjunto de directrices y requisitos para sus prácticas de desarrollo. Entre ellos se encuentran:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz de usuario debe utilizar el modo oscuro y tener un aspecto moderno.
- Se debe añadir documentación al código en forma de comentarios de documentación TSDoc.
- Al principio de cada archivo se debe añadir un bloque de comentarios que describa su contenido.

Mediante archivos de instrucciones, te asegurarás de que Copilot disponga de la información adecuada para realizar tareas de acuerdo con las prácticas indicadas.

### Instrucciones personalizadas

Las instrucciones personalizadas permiten proporcionar contexto y preferencias a Copilot para que comprenda mejor tu estilo de programación y tus requisitos. Esta función te ayuda a orientar a Copilot para que ofrezca sugerencias y fragmentos de código más pertinentes. Puedes especificar las convenciones de programación y bibliotecas preferidas, e incluso los tipos de comentarios que quieres incluir en el código. Puedes crear instrucciones para todo el repositorio o para tipos concretos de archivos y proporcionar así contexto específico para las tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo de instrucciones que se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información a nivel de proyecto, pertinente para la mayoría de las solicitudes de chat o CLI que se envíen a Copilot. Puede describir la pila tecnológica, resumir lo que se está desarrollando e incluir prácticas recomendadas y otras directrices globales.
- Los archivos `.github/instructions/*.instructions.md` se pueden crear para tareas o tipos de archivos específicos. Puedes utilizarlos para proporcionar directrices para determinados lenguajes, como TypeScript o Astro, o para tareas como crear un componente de interfaz de usuario o un conjunto de pruebas unitarias.

> [!NOTE]
> Al trabajar en el IDE, los archivos de instrucciones solo se utilizan para generar código en Copilot Chat, no para las finalizaciones de código ni las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` (con la propiedad `applyTo` en el frontmatter) al generar código.
>
> Además, Copilot [admite archivos de instrucciones basados en otros estándares][custom-instructions-support], incluidos AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

Hablar en profundidad sobre la creación de archivos de instrucciones queda fuera del alcance de este taller. Sin embargo, los ejemplos del proyecto muestran un enfoque representativo. En líneas generales:

- Mantén las instrucciones de `copilot-instructions.md` centradas en directrices a nivel de proyecto, como una descripción de lo que se está desarrollando, la estructura del proyecto y los estándares globales de programación.
- Utiliza archivos `*.instructions.md` para proporcionar instrucciones específicas sobre tipos de archivos (pruebas unitarias, componentes Astro o capa de datos) o tareas concretas.
- Escribe en lenguaje natural. Procura que las directrices sean claras e incluye ejemplos de cómo debería y cómo no debería ser el código.

No hay una única forma correcta de crear archivos de instrucciones, del mismo modo que no hay una única forma de utilizar la IA. La experimentación te permitirá descubrir qué funciona mejor para tu proyecto.

> [!TIP]
> Todos los proyectos que utilizan GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. Al explorar los archivos de este proyecto, puede que observes que hay instrucciones para muchos tipos de tareas, incluidas las [actualizaciones de la interfaz de usuario][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada entorno ofrece esta opción de una forma diferente (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI); la lección correspondiente al entorno que estés utilizando la explicará cuando sea pertinente.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizados de este proyecto

Dedica un momento a leer los archivos de instrucciones incluidos en este repositorio: hay un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Explora el archivo y fíjate en la breve descripción del proyecto y en secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. Dentro de **Code standards**, presta atención a las directrices anidadas sobre **GitHub Actions Workflows**. Estas se aplican a cualquier interacción que tengas con Copilot.
3. Abre la carpeta `.github/instructions` y echa un vistazo. Verás instrucciones para archivos Astro, la capa de datos Drizzle, pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. Fíjate en el campo `applyTo` de la parte superior: define un patrón glob (relativo a la raíz del repositorio) que determina a qué archivos se aplican las instrucciones. En este caso, coincide con cualquier archivo de pruebas TypeScript (por ejemplo, uno que coincida con `**/*.test.ts`).
5. Observa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Fíjate en los enlaces a otros archivos de instrucciones (como `unit-tests.instructions.md`) y a archivos existentes del proyecto. Así puedes dividir conjuntos de instrucciones grandes en archivos más pequeños y reutilizables, y señalar a Copilot ejemplos que debe seguir al generar código. Las rutas indicadas son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero todavía no exige documentación dentro del código. En los pasos siguientes añadirás reglas para los comentarios de documentación TSDoc y los encabezados de comentarios de archivo.

## Crea una rama para los cambios

Sigamos algunas prácticas recomendadas y creemos una rama para los cambios.

1. Vuelve al codespace del ejercicio anterior.
2. Abre un terminal nuevo pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama nueva y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Utiliza Copilot Chat *antes* de actualizar las instrucciones

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los ejercicios siguientes, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y la selección del modelo varían según el ejercicio; cada paso lo indicará cuando sea pertinente.

Para observar el efecto de las instrucciones personalizadas, empieza enviando una instrucción con el archivo de instrucciones actual. Más adelante, lo actualizarás y volverás a enviar la misma instrucción para ver la diferencia.

1. Cierra las pestañas de editor que sigan abiertas de ejercicios anteriores para que Copilot solo utilice el contexto que necesitas.
2. Abre `src/lib/publishers.ts` para indicar a Copilot dónde debe ubicarse la función auxiliar.
3. En el menú desplegable de agentes de la vista Chat, selecciona **Agent** para que Copilot pueda aplicar cambios a los archivos.

   ![Captura de pantalla del selector de agentes en la vista Chat.](../../../_images/shared-chat-mode-selector.png)

4. Envía esta instrucción:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot explorará el proyecto y aplicará actualizaciones al código, a menudo tanto al archivo de la función auxiliar como a sus pruebas.
6. Fíjate en que la función auxiliar propuesta es una función tipada que recibe un cliente `db` como primer argumento y devuelve una matriz tipada de editores. Esto se debe a las convenciones de la capa de datos en `.github/instructions/drizzle.instructions.md` (que se aplica a `src/lib/*.ts`).
7. Observa que al código propuesto **le faltan** comentarios de documentación TSDoc y un encabezado de comentarios a nivel de archivo.

> [!CAUTION]
> Como Copilot es probabilístico, existe la posibilidad de que añada comentarios de documentación aunque no se lo pidas. No pasa nada: el objetivo es observar la mejora de la *coherencia* después de actualizar las instrucciones.

## Añade un nuevo estándar para el repositorio

Como se indicó antes, `.github/copilot-instructions.md` está pensado para proporcionar a Copilot información a nivel de proyecto. Documentemos los estándares de programación del repositorio para mejorar las sugerencias de código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Observa cómo documenta los estándares de programación del proyecto, pero todavía no incluye reglas para la documentación en el código; por eso la función auxiliar generada no tenía comentarios de documentación.
3. Añade las siguientes líneas de Markdown justo después de los estándares existentes para indicar a Copilot que añada encabezados de comentarios de archivo y comentarios de documentación TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como has visto en la lección anterior, los archivos de instrucciones se pueden crear a nivel de repositorio (`.github/copilot-instructions.md`) para ofrecer directrices globales, o como archivos `*.instructions.md` para lenguajes, tipos de archivos o tareas concretos. El archivo a nivel de repositorio es el lugar adecuado para estándares globales, como la regla sobre los comentarios de documentación que acabas de añadir.

## Vuelve a ejecutar la instrucción y observa el cambio

1. Vuelve a Copilot Chat y selecciona **New Chat** para borrar el contenido de la conversación.
2. Vuelve a seleccionar `src/lib/publishers.ts` para que Copilot se centre en el archivo adecuado.
3. Envía la **misma instrucción** que antes:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Observa que el archivo propuesto ahora empieza con un bloque de comentarios parecido a este:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Observa que la función propuesta ahora incluye un comentario TSDoc parecido a este:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Acabas de orientar a Copilot para que siga un nuevo estándar del proyecto y lo aplique al código real sobre el que se trabajará en el siguiente ejercicio.

## Confirma las instrucciones y publica la rama

Los archivos de instrucciones son recursos del repositorio y se gestionan con el mismo sistema de control de versiones que cualquier otro archivo. Vamos a confirmar los cambios y publicar la rama en el repositorio.

1. Abre una ventana de terminal nueva pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. En el terminal, ejecuta el siguiente comando para comprobar que la actualización de instrucciones y los cambios de la función auxiliar estén presentes:

   ```bash
   git status
   ```

3. En el terminal, prepara y confirma la actualización de instrucciones y todos los archivos modificados por Copilot para crear la función auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra actualizaciones de archivos complementarios (por ejemplo, pruebas), añade también esos archivos.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Desde el terminal, publica la rama en el repositorio:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Después de publicar la rama, debemos crear una solicitud de incorporación de cambios y asociarla con la incidencia sobre los estándares de documentación de la lista de pendientes. Podríamos hacerlo manualmente, pero Copilot puede encargarse de ello utilizando las herramientas de GitHub ya conectadas al proyecto. Pidamos a Copilot que encuentre la incidencia, cree una PR para cerrarla y, después, la combine.

> [!NOTE]
> Este es el primer ejercicio en el que Copilot actúa en GitHub en tu nombre. La plantilla del proyecto ya conecta las herramientas de GitHub con tu espacio de trabajo, así que no hay nada que configurar. La primera vez que Copilot utilice una herramienta, VS Code podría pedirte que inicies sesión en GitHub. Sigue las instrucciones para permitirlo. En un ejercicio posterior aprenderás cómo funciona esta conexión (Model Context Protocol).

1. Abre Copilot Chat en el codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista Copilot Chat y comprueba que **Agent** esté seleccionado en el selector de agentes.
3. Pide a Copilot que encuentre la incidencia relacionada con la actualización de los archivos de instrucciones y que cree una PR desde la rama actual. Indícale que describa tanto la actualización de instrucciones como la nueva base de la función auxiliar para editores:

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot empezará a buscar la incidencia y a crear la PR.
5. Si Copilot te pide **Allow** para realizar acciones de GitHub en tu nombre, revisa el comando y selecciona **Allow** cuando corresponda.
6. Cuando se haya creado la PR, pide a Copilot que la combine y que vuelva a `main`:

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Si Copilot te pide **Allow** para realizar acciones de GitHub y ejecutar comandos de shell en tu nombre, revisa el comando y selecciona **Allow** cuando corresponda.

¡Ya has creado y combinado una solicitud de incorporación de cambios con ayuda de GitHub Copilot!

## Resumen y próximos pasos

Has explorado cómo Copilot utiliza el contexto de los archivos de instrucciones de este proyecto y has usado Copilot Chat en VS Code para:

- enviar una instrucción de generación de código y observar lo que produce Copilot con las instrucciones *existentes*;
- añadir un nuevo estándar para todo el repositorio en `.github/copilot-instructions.md`;
- volver a ejecutar la misma instrucción y observar cómo el código propuesto adopta el nuevo estándar;
- confirmar la actualización de instrucciones y la base de la función auxiliar en `main` para que el siguiente ejercicio pueda continuar el trabajo.

A continuación, pondrás estas instrucciones en práctica en el [modo agente][next-lesson], mientras Copilot añade una nueva funcionalidad en toda la base de código.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personalizadas personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
