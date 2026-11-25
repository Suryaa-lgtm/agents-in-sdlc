---
title: "Ejercicio 4: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los dos ejercicios anteriores has pedido al agente en la nube de Copilot que se ocupe de tres tareas diferentes para mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente en la nube está diseñado para trabajar de forma autónoma y asincrónica, sigue siendo importante poder supervisar estas tareas.

Dispones de varias herramientas para gestionar las tareas asignadas al agente en la nube, incluida [la página de agentes][agents-page] de GitHub.com. Desde este centro de control puedes ver todas las tareas del agente que tienen solicitudes de incorporación de cambios (PR) abiertas. Puedes explorar las operaciones realizadas e incluso orientar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube;
- orientarás una sesión en curso para solicitar funcionalidad adicional.

## Escenario

Después de asignar al agente la tarea de crear un modo de alto contraste, el equipo se dio cuenta de que también sería un buen momento para añadir un modo claro. Como ya se estaba trabajando en actualizar el estilo del sitio y añadir la funcionalidad de alternancia, parecía lógico incluirlo. Quieres orientar el trabajo del agente para asegurarte de que añada el modo claro además del modo de alto contraste.

## Revisa las tareas del agente en la nube de Copilot

Veamos el estado actual de todas las tareas asignadas al agente en la nube de Copilot.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas tanto en el panel principal como en el panel de la izquierda. Deberías ver las tareas que has asignado a Copilot, entre ellas:
   - actualizar la documentación de tu base de código;
   - generar API para modificar juegos;
   - añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en curso. Revisa las tareas que ha realizado Copilot. Pueden incluir:
   - obtener el código del repositorio;
   - crear el entorno de trabajo de Copilot;
   - configurar servidores MCP;
   - realizar varios pasos para completar la tarea asignada.

> [!NOTE]
> Los pasos concretos que se muestren dependerán del estado del trabajo de Copilot y del enfoque que haya seguido.

4. Observa también el panel de solicitudes de incorporación de cambios (PR), que aparece en el lado derecho. Desde ahí puedes consultar la solicitud y los archivos modificados para seguir supervisando el trabajo.

## Orienta al agente en la nube

Ahora que has visto las tareas activas, pide a Copilot que incluya el botón de alternancia del modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con la incorporación del modo de alto contraste. El título exacto dependerá del nombre que utilice Copilot y del estado actual del trabajo.

   ![Sesión de accesibilidad en el centro de control](../../../_images/ex6-accessibility-session.png)

2. Observa la sesión durante unos minutos, hasta que indique que ha terminado la configuración y ha empezado a trabajar. Sabrás que esto ha ocurrido cuando empiecen a aparecer mensajes parecidos a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, añade esta instrucción:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Captura de pantalla de la tarea del agente en la nube en la página de agentes, con el cuadro de diálogo «Steer active session while Copilot is working» resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar la instrucción.
5. Observa cómo Copilot la confirma y la incorpora a su flujo de trabajo.

## Deja que Copilot trabaje

¡Como antes, Copilot se pondrá a trabajar en la tarea actualizada! Incorporará la nueva solicitud a su flujo de trabajo cuando termine el paso concreto que estaba realizando en el momento en que enviaste el mensaje.

Como antes, esto tardará varios minutos; puedes aprovechar para hacer una pausa y reflexionar sobre todo lo que has aprendido y explorado hasta ahora.

## Resumen y próximos pasos

En esta lección has explorado la página de agentes de Copilot, el centro desde el que supervisar y orientar las tareas del agente en la nube de GitHub Copilot. Desde este centro de control puedes seguir todas las tareas activas y completadas, revisar el trabajo que se está realizando e incluso redirigir las tareas en curso para ajustar su alcance o proporcionar instrucciones adicionales.

Has explorado estos conceptos:

- has explorado el centro de control y la página de agentes para supervisar las tareas del agente en la nube;
- has redirigido una sesión en curso para solicitar funcionalidad adicional.

Mientras Copilot termina de trabajar en las funciones de accesibilidad, puedes pasar a [iterar sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Información sobre los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
