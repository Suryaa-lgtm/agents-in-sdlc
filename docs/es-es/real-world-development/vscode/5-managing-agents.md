---
title: "Ejercicio 5: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

Cuando utilizas el modo agente de GitHub Copilot, este trabaja de forma autónoma: explora la base de código, propone cambios, edita archivos y ejecuta comandos. Como el trabajo se realiza en tiempo real en tu equipo, Copilot Chat en VS Code te muestra en todo momento las llamadas a herramientas y las ediciones de archivos. Puedes revisar cada diferencia en línea, aceptar o rechazar cambios concretos y orientar la conversación con instrucciones de seguimiento para perfeccionar o ampliar el trabajo sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad;
- revisarás y aceptarás las ediciones de archivos propuestas;
- orientarás al agente durante la sesión para añadir un botón de alternancia del modo claro además del modo de alto contraste.

## Escenario

El agente personalizado de accesibilidad que utilizaste en el [ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño ha hecho una petición adicional: también quiere un botón de alternancia del modo claro para quienes consideran que el tema predeterminado es demasiado oscuro. En lugar de empezar una conversación nueva desde cero, orientarás la sesión existente para ampliar el trabajo.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Cada modificación de archivo aparece en línea en el chat con sus diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para observar cada llamada a herramienta. Verás lecturas de archivos, ediciones de archivos y los comandos de terminal que te pida ejecutar.
3. Cuando el agente proponga una edición, las diferencias aparecerán en línea:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertirlo y permitir que el agente vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed**, situado en la parte superior del chat, para ver todos los archivos modificados por el agente durante esta sesión.

> [!NOTE]
> Si una llamada a herramienta solicita permiso (por ejemplo, para ejecutar un comando de terminal), el agente se detendrá y mostrará una solicitud **Allow**. Aprueba únicamente los comandos con los que estés de acuerdo.

5. Espera a que el agente termine de implementar el modo de alto contraste. Deberías ver un mensaje final que resuma los cambios realizados.

## Orienta al agente para añadir el modo claro

Ahora que ya está implementado el modo de alto contraste, ampliarás la misma conversación para añadir un botón de alternancia del modo claro. Como continuarás en la misma sesión de chat, el agente conservará todo el contexto del trabajo anterior, incluidos los componentes que modificó, el enfoque de estilo que utilizó y el patrón de almacenamiento local que configuró.

1. En el campo de entrada de Copilot Chat, envía la siguiente instrucción de seguimiento:

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. El agente continuará desde donde lo dejó, explorará los cambios realizados y propondrá modificaciones para añadir el modo claro.
3. Revisa cada modificación nueva cuando aparezca, como hiciste con el modo de alto contraste. Utiliza **Keep** o **Undo** para cada diferencia.
4. Si el agente avanza en una dirección que no quieres —por ejemplo, si intenta reorganizar la interfaz de alternancia de una forma que no te gusta—, puedes detenerlo con el botón **Stop** junto al campo de entrada del chat y enviar una instrucción de seguimiento para aclarar lo que necesitas.

> [!TIP]
> Orientar una sesión en curso es más rápido que empezar de nuevo. Utiliza instrucciones de seguimiento para pedir ajustes («simplifica el CSS: utiliza variables CSS en lugar de duplicar selectores»), corregir el rumbo («no añadas un tercer botón de alternancia; integra el modo claro en el panel de configuración existente») o ampliar el alcance («añade también métodos abreviados de teclado para los dos botones de alternancia»).

## Revisa el conjunto de trabajo

Antes de confirmar el trabajo, revisa rápidamente todo lo que ha modificado el agente.

1. Abre la vista **Source Control** en VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver actualizaciones de los componentes Astro, los estilos y las pruebas relacionadas.
3. Abre algunos archivos modificados y revisa sus diferencias. Confirma que se aplican los patrones de accesibilidad del agente personalizado: atributos ARIA, navegación con el teclado, HTML semántico y persistencia mediante almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel Source Control. Los publicarás en [la siguiente lección][next-lesson].

## Resumen y próximos pasos

Has utilizado el modo agente de Copilot Chat para supervisar y orientar una sesión en curso: has revisado cada edición de archivo a medida que aparecía, aceptado o rechazado cambios y enviado instrucciones de seguimiento para ampliar el trabajo sin perder el contexto.

En esta lección has explorado estos conceptos:

- supervisar el trabajo de un agente en tiempo real;
- aceptar y rechazar ediciones de archivos individuales;
- orientar una sesión en curso mediante instrucciones de seguimiento.

En la [siguiente lección][next-lesson] publicarás el trabajo de accesibilidad en una solicitud de incorporación de cambios y revisarás las modificaciones generadas por el agente personalizado local durante este laboratorio.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
