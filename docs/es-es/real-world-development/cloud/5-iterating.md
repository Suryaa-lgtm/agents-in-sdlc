---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Supervisar y gestionar agentes][previous-lesson] |
|:--|

## Revisar el trabajo

Durante este laboratorio has trabajado con GitHub Copilot en varias tareas centradas en mejorar la experiencia de usuario y añadir funcionalidades. Has pedido a Copilot que añada documentación al código, que desarrolle la funcionalidad de juegos relacionados para que el equipo de diseño pueda iterar sobre ella y que implemente funciones de accesibilidad, incluidos los botones de alternancia del modo de alto contraste y el modo claro. Vamos a explorar los cambios en el código y, si es necesario, proporcionar comentarios a Copilot para mejorar su trabajo.

### Escenario

Como hemos destacado en numerosas ocasiones, los fundamentos del diseño de software y DevOps no cambian al incorporar IA generativa. Siempre queremos revisar el código generado y seguir nuestro proceso habitual de DevOps. Con esto en mente, revisemos las sugerencias de GitHub Copilot para añadir documentación, crear la funcionalidad de juegos relacionados e implementar las funciones de accesibilidad antes de activar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

Como el agente en la nube de Copilot realiza tareas de forma asincrónica y sin supervisión, se han establecido ciertas restricciones de seguridad para garantizar que todo siga siendo seguro. Entre ellas:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utilizará para su código.
- El agente en la nube se ejecuta en GitHub Actions, donde crea un entorno independiente y efímero para trabajar.
- Una persona debe aprobar todos los flujos de trabajo de GitHub Actions antes de que puedan ejecutarse.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores MCP.

## Revisa la documentación generada

Empecemos por explorar la primera solicitud de incorporación de cambios (PR) que generó el agente en la nube de GitHub Copilot: la que añade documentación al código. Para ello, utilizarás la interfaz estándar de solicitudes de incorporación de cambios de GitHub.com.

> [!NOTE]
> Al explorar la solicitud de incorporación de cambios, puede que veas una advertencia que indica que el cortafuegos ha bloqueado a GitHub Copilot. Es **lo esperado**, porque Copilot tiene acceso limitado a recursos externos de forma predeterminada, incluidas las llamadas a servidores MCP externos. Si quieres, puedes [personalizar o deshabilitar el cortafuegos del agente en la nube de Copilot][agent-firewall].

1. Vuelve a tu repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes de incorporación de cambios.
3. Abre la solicitud cuyo título sea parecido a **Add missing documentation** o que tenga un título más detallado.

> [!NOTE]
> Si Copilot sigue trabajando en la tarea, la solicitud de incorporación de cambios tendrá la etiqueta **[WIP]**. En ese caso, espera a que Copilot termine. Puede tardar unos minutos; puedes tomarte un descanso o repasar lo que has aprendido hasta ahora.

4. Cuando la solicitud esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

    ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que incluye los nuevos comentarios de documentación TSDoc y otra documentación. Los cambios concretos pueden variar.

    Al revisar los cambios, busca comentarios de documentación TSDoc, convenciones de TypeScript y encabezados de comentarios. Estas modificaciones se deben a los archivos de instrucciones personalizadas que revisaste al principio del ejercicio 2.

6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que señala que algunos flujos de trabajo están pendientes de aprobación.
8. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. Deberías ver que los flujos de trabajo se ponen en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto deberían pasar para la aplicación Astro. La operación puede tardar varios minutos.

## Solicita cambios a GitHub Copilot

La colaboración con Copilot en una solicitud de incorporación de cambios no es un proceso unidireccional. También puedes mencionar a Copilot en los comentarios de la solicitud —igual que mencionarías a otras personas del equipo— o en comentarios en línea sobre el código. Copilot verá esos comentarios e iniciará otra sesión para resolverlos. Como los resultados no son deterministas, no podemos proporcionar un texto prescriptivo que debas utilizar. Algunas ideas de cambios que podrías pedirle a Copilot:

- Añadir encabezados de comentarios al principio de cada archivo de código con una breve descripción de su contenido.
- Añadir comentarios de documentación TSDoc a los archivos TypeScript y Astro.
- Crear un archivo README con una descripción de la estructura de la aplicación Astro.

1. Añade un comentario para solicitar un cambio en la documentación generada y menciona a **@copilot**, como harías con cualquier usuario. Puedes utilizar alguna de las ideas anteriores o sugerir otro cambio relacionado con la documentación que quieras incluir en la base de código.
2. Selecciona **View Session** para observar cómo trabaja Copilot. Fíjate en que empieza una nueva sesión para aplicar los cambios.
3. Puedes seleccionar **Back to pull request** para volver a la solicitud de incorporación de cambios.

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine los cambios, deberías ver una nueva confirmación en la solicitud de incorporación de cambios.
5. Selecciona la pestaña **Files changed** para revisar los cambios.

Puedes seguir iterando hasta que estés conforme. Cuando lo estés, puedes marcar la PR en borrador como lista para revisión y combinarla en la rama principal.

![Convert PR to ready](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Volvamos a la solicitud de incorporación de cambios que generó Copilot para resolver la incidencia sobre cómo mostrar juegos relacionados en la página de detalles de un juego.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud de incorporación de cambios cuyo título sea parecido a **Show related games on the game details page** o que tenga un título más detallado.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Deberías ver un indicador que señala que algunos flujos de trabajo están pendientes de aprobación.
7. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
8. Deberías ver que los flujos de trabajo se ponen en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto deberían pasar para la aplicación Astro. La operación puede tardar varios minutos.
9. **Opcional:** incluso puedes cambiar a esta rama en tu codespace para probar manualmente la funcionalidad de juegos relacionados. Abre el terminal del codespace y ejecuta los comandos siguientes (sustituye `<branch-name>` por el nombre de la rama que haya creado Copilot, por ejemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

¡Copilot ha creado la funcionalidad de juegos relacionados! Como antes, puedes trabajar de forma iterativa con el agente en la nube de Copilot para pedirle cambios. Por ejemplo, podrías pedirle que ajuste cuántos juegos relacionados se muestran o que añada encabezados de comentarios y comentarios de documentación TSDoc (recuerda que la incidencia se asignó **antes** de que actualizaras las instrucciones personalizadas). Como antes, puedes solicitar estos cambios añadiendo un comentario en la pestaña **Conversation**. Copilot lo verá e iniciará una nueva sesión.

## Revisa las funciones de accesibilidad

Por último, revisaremos las funciones de accesibilidad implementadas mediante el agente personalizado de accesibilidad. Esta solicitud de incorporación de cambios debería incluir tanto el modo de alto contraste que asignaste en el ejercicio 3 como el modo claro que solicitaste desde el centro de control en el ejercicio 4.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud de incorporación de cambios cuyo título sea parecido a **Add high contrast mode to website** o que tenga un título más detallado.

> [!NOTE]
> Si Copilot sigue trabajando en la tarea, la solicitud de incorporación de cambios tendrá la etiqueta **[WIP]**. En ese caso, espera a que termine. Puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Revisa la implementación y presta especial atención a:
   - los componentes de interfaz para alternar entre los modos;
   - el uso del almacenamiento local para conservar las preferencias del usuario;
   - los cambios de CSS o de estilos para los modos de alto contraste y claro;
   - los atributos de accesibilidad (etiquetas ARIA, navegación con el teclado, etc.);
   - cualquier código JavaScript/TypeScript que gestione el cambio de modo.

6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que señala que algunos flujos de trabajo están pendientes de aprobación.
8. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)
9. Deberías ver que los flujos de trabajo se ponen en cola en la sección de comprobaciones de la solicitud de incorporación de cambios. Si todo va bien, las comprobaciones del proyecto deberían pasar para la aplicación Astro. La operación puede tardar varios minutos.
10. **Opcional:** puedes cambiar a esta rama en tu codespace para probar manualmente las funciones de accesibilidad. Abre el terminal del codespace y ejecuta los comandos siguientes (sustituye `<branch-name>` por el nombre de la rama que haya creado Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    A continuación, inicia la aplicación y prueba los botones de alternancia del modo de alto contraste y del modo claro en el navegador para comprobar que funcionan como se esperaba y que las preferencias se conservan al volver a cargar la página.

Observa cómo el agente personalizado de accesibilidad ayudó a orientar a Copilot para que implementara estas funciones siguiendo las prácticas recomendadas de accesibilidad. Si detectas problemas de accesibilidad o mejoras posibles, puedes mencionar a **@copilot** en un comentario y solicitar cambios, igual que hiciste con las solicitudes de incorporación de cambios anteriores.

## Ejercicio opcional: sigue delegando

El agente en la nube funciona mejor cuando puedes asignarle tareas reales de la lista de pendientes y dedicarte a otras cosas. Para adquirir esa costumbre, crea algunas incidencias más en tu repositorio y asígnaselas a Copilot. Algunas ideas:

- Crear un formulario para mostrar interés por apoyar el juego en la página de detalles.
- Implementar la paginación en la página de lista de juegos.
- Añadir validación de entradas y gestión de errores a las funciones auxiliares de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. A lo largo de estas lecciones:

- **Has inspeccionado los archivos de instrucciones personalizadas incluidos en este repositorio** para observar más adelante su efecto en los resultados del agente en la nube.
- **Has asignado incidencias al agente en la nube de Copilot** y has visto cómo configuraba su entorno, planificaba y trabajaba de forma asincrónica.
- **Has creado y utilizado un agente personalizado** para accesibilidad y has añadido botones de alternancia para los modos de alto contraste y claro.
- **Has utilizado la página de agentes de Copilot como centro de control** para supervisar y orientar sobre la marcha la sesión de accesibilidad.
- **Has revisado las solicitudes de incorporación de cambios del agente en la nube y has iterado sobre ellas**, mencionando a `@copilot` para solicitar cambios y aprobando flujos de trabajo.

## Repaso y próximos pasos

Has completado el recorrido del agente en la nube. Si quieres seguir explorando, los otros recorridos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: explora el modo Agente de Copilot Chat y la integración de MCP directamente desde el IDE.
- 💻 **[Recorrido de CLI](../../cli/)**: entrega desde el terminal dos cambios revisados con los modos Plan y Autopilot, aptitudes de agente, un agente de QA personalizado, Playwright MCP, Agent Merge y un puente opcional `/delegate` al agente en la nube.

En tu propio repositorio, prueba estas ideas para continuar:

- Asigna al agente en la nube una incidencia de refactorización o de cobertura de pruebas.
- Crea un agente personalizado para otro ámbito.
- Configura `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Información sobre los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de trabajo de configuración del agente en la nube de Copilot][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube de Copilot][agent-firewall]

---

| [← Lección anterior: Supervisar y gestionar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
