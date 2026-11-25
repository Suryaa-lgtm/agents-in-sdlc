---
title: "Ejercicio 2: Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Es probable que haya muy pocas organizaciones —si es que hay alguna— que no tengan problemas con la deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidades que llevan mucho tiempo en la lista de tareas pendientes porque nunca ha habido tiempo para implementarlas. El agente en la nube de GitHub Copilot está diseñado para realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Cuando termina el trabajo, genera un borrador de solicitud de incorporación de cambios (PR) para que lo revise una persona. Así puedes delegar tareas tediosas, acelerar el proceso de desarrollo y liberar tiempo para que los desarrolladores se centren en cuestiones de mayor alcance.

Con el agente en la nube de Copilot explorarás los siguientes aspectos:

- personalizar el entorno para generar código;
- asegurarte de que las operaciones se realicen de forma segura;
- comprender la importancia de delimitar claramente las incidencias;
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica que quiere resolver. Los contratistas que crearon la primera versión del sitio dejaron la documentación en un estado poco ideal: como verás, no hay documentación. Como primer paso, quieren añadir comentarios de documentación TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño está listo para mejorar la forma de descubrir juegos. Quieren que la página de detalles de cada juego muestre juegos relacionados —otros títulos de la misma categoría— para que las personas puedan seguir explorando. Por ahora no necesitan una implementación pulida; solo algo que puedan utilizar para probar la experiencia de usuario y realizar pruebas de aceptación. Esta tarea es actualmente un impedimento, pero hay otras incidencias que tienen más prioridad en este momento.

Ambos son ejemplos de tareas que pueden acabar relegadas y que resulta muy conveniente asignar al agente en la nube de Copilot. El agente puede trabajar en ellas de forma asincrónica mientras el desarrollador se centra en otras tareas, y después volver para revisar el trabajo de Copilot y asegurarse de que todo está como se esperaba.

## Presentación del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma muy parecida a un desarrollador. Y, al igual que con una persona, puedes asignarle trabajo de distintas maneras, por ejemplo, [asignándole una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Una vez asignada, Copilot creará una solicitud de incorporación de cambios en borrador para hacer un seguimiento del progreso, configurará un entorno y empezará a trabajar en la tarea. Puedes consultar la sesión de Copilot mientras sigue en curso o una vez completada. Cuando la solución propuesta esté lista para que la revises, Copilot te mencionará en la solicitud de incorporación de cambios.

## La importancia de unas instrucciones bien delimitadas

GitHub Copilot no hace magia: no puedes saltarte el trabajo de análisis. Incluso las operaciones que parecen sencillas pueden ser complejas cuando se examinan en detalle; por eso, [delimita con cuidado las tareas que asignas al agente en la nube de Copilot][cloud-agent-best-practices]. Trátalo como a un programador colaborador con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque sobre la marcha. Los fundamentos del desarrollo de software no cambian por incorporar IA generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has conocido las instrucciones personalizadas y cómo orientan a Copilot. Si ya has completado un ejercicio práctico sobre instrucciones personalizadas, habrás visto cómo funciona `.github/copilot-instructions.md`; si no, este es un buen momento para echarle un vistazo rápido. Antes de asignar trabajo al agente en la nube de Copilot, lee los archivos de instrucciones que ya incluye este repositorio sin modificarlos para poder observar su efecto más adelante.

Abre los siguientes archivos en la interfaz web de GitHub de tu repositorio o en un codespace, si ya tienes uno en marcha:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, en especial las expectativas sobre las convenciones de TypeScript y los comentarios de documentación TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en el frontmatter `applyTo`, que aplica estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes la incidencia `Code lacks documentation` al agente en la nube en la sección siguiente, observa si la solicitud de incorporación de cambios resultante incluye comentarios TSDoc, convenciones de TypeScript y encabezados de comentarios. Estas características provienen de los archivos de instrucciones. Volveremos a mencionarlas al revisar las solicitudes de incorporación de cambios en un ejercicio posterior.

## Configura el entorno de desarrollo del agente en la nube de Copilot

Crear código, independientemente de quién lo haga, suele requerir un entorno específico y algunos scripts de configuración para garantizar que todo esté en buen estado. Esto también se aplica al asignar tareas a Copilot, que trabaja de forma similar a un ingeniero de software.

El agente en la nube utiliza [GitHub Actions][github-actions] como entorno de trabajo. Puedes personalizarlo creando un [flujo de trabajo de configuración especial][setup-workflow], definido en el archivo `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece a trabajar. Así puede acceder a las herramientas de desarrollo y dependencias necesarias. Este flujo ya está configurado para facilitar el taller y permitirte aprender cómo funciona. Garantiza que Copilot tenga acceso a Node.js, las dependencias del proyecto, los binarios del navegador para las pruebas de extremo a extremo y la base de datos SQLite migrada y con datos iniciales para la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos en el nivel mínimo necesario para *tus pasos*. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de los pasos de configuración (por ejemplo, para instalar dependencias), necesitarás el permiso `contents: read`. Si no clonas el repositorio durante la configuración, Copilot lo hará automáticamente cuando terminen los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración del frontend y la aplicación: Node.js (ahora toda la aplicación utiliza Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga los datos iniciales de la base de datos SQLite local para que las compilaciones y las pruebas dispongan de datos.
      - name: Set up the database
        run: npm run db:setup
```

Se parece a cualquier otro archivo de flujo de trabajo de GitHub, pero tiene algunos aspectos importantes:

- Contiene un único trabajo llamado `copilot-setup-steps`. Este trabajo se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la solicitud de incorporación de cambios.
- Observa el activador `workflow_dispatch`, que permite ejecutar el flujo de trabajo manualmente desde la pestaña **Actions** del repositorio. Resulta útil para comprobar que el flujo se ejecuta correctamente, sin esperar a que Copilot lo ejecute.

## Añade documentación

Aunque todo el mundo reconoce la importancia de la documentación, la mayoría de los proyectos tienen información obsoleta o carecen de ella. Esta deuda técnica suele quedar desatendida, lo que reduce la productividad y dificulta mantener la base de código o incorporar a nuevos miembros al equipo. Por suerte, Copilot destaca a la hora de crear documentación, así que esta incidencia es ideal para asignársela al agente en la nube. Trabajará en segundo plano para generar la documentación necesaria. En un ejercicio futuro volverás para revisar el trabajo.

1. Abre tu repositorio en github.com en una nueva pestaña del navegador.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para crear la incidencia.
5. Escribe `Code lacks documentation` en **Title**.
6. Escribe lo siguiente en **Description**:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

  ![Detalles de asignación de Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecciona la pestaña **Pull Requests**.
11. Abre la solicitud de incorporación de cambios (PR) que se acaba de generar. Tendrá un título parecido a `[WIP]: Code lacks documentation`. Si no aparece una solicitud nueva en la lista, espera uno o dos minutos y actualiza la ventana del navegador.
12. Al cabo de unos minutos, Copilot debería haber creado una lista de tareas.

> [!NOTE]
> Es posible que la lista de tareas de Copilot tarde varios minutos en aparecer en la solicitud de incorporación de cambios. Copilot está creando su entorno (ejecutando el flujo de trabajo que se ha descrito antes), analizando el proyecto y determinando el mejor enfoque para resolver el problema.

13. Revisa la lista y las tareas que va a completar.
14. Desplázate por la cronología de la solicitud de incorporación de cambios. Deberías ver una actualización que indica que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona el botón **View session**.

  ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Es posible que tengas que actualizar la ventana para ver el indicador actualizado.

16. Observa que puedes desplazarte por la sesión en directo y ver cómo Copilot resuelve el problema. Esto incluye explorar el código y comprender su estado, detenerse a pensar para decidir el plan adecuado y crear código.

Es probable que esto tarde varios minutos. Uno de los objetivos principales del agente en la nube de Copilot es permitir que trabaje de forma asincrónica y así liberar tiempo para otras tareas. Aprovecharemos esa misma función: asignaremos otra tarea al agente en la nube de Copilot y, mientras tanto, nos centraremos en escribir código para añadir funcionalidades a la aplicación.

## Añade una sección de juegos relacionados a la página de detalles del juego

Como ya hemos indicado, una de las grandes ventajas del agente en la nube de GitHub Copilot es que permite repartir el trabajo: tú puedes centrarte en un conjunto de tareas mientras él se ocupa de otro. Añadir una sección de juegos relacionados para el equipo de diseño quizá no lleve mucho tiempo, pero ese tiempo se podría dedicar a otras tareas. ¡Vamos a asignársela al agente en la nube de Copilot!

1. Vuelve a tu repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue** para utilizar la plantilla en blanco.
5. Escribe `Show related games on the game details page` en **Title**.
6. Escribe lo siguiente en **Description**:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Al poco tiempo, verás una serie de 👀 en el primer comentario de la incidencia, lo que indica que Copilot ya está trabajando.

![Copilot utiliza el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

¡Copilot ya está trabajando diligentemente en tu segunda solicitud! Como el agente en la nube de Copilot trabaja de forma similar a un ingeniero de software, no tienes que supervisarlo constantemente; basta con revisar el resultado cuando termine. Ahora pasaremos a crear y utilizar agentes personalizados.

## Resumen y próximos pasos

En esta lección has explorado el [agente en la nube de GitHub Copilot][copilot-agents]. Puedes asignar incidencias a este agente para que las resuelva de forma asincrónica. Copilot puede ayudarte con la deuda técnica, crear funcionalidades nuevas o migrar código de un marco de trabajo a otro.

Has explorado estos conceptos:

- personalizar el entorno para generar código;
- asegurarte de que las operaciones se realicen de forma segura;
- comprender la importancia de delimitar claramente las incidencias;
- asignar incidencias a Copilot.

Mientras el agente en la nube trabaja, puedes pasar a crear y utilizar agentes personalizados. El [agente en la nube de Copilot también puede utilizar servidores MCP][cloud-agent-mcp], y dispone de instrucciones personalizadas que hemos explorado en módulos anteriores.

## Recursos

- [Información sobre el agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de trabajo de configuración del agente en la nube de Copilot][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
