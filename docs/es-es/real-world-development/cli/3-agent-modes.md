---
title: "Lección 3: Modos de agente, Plan y Autopilot"
description: "Utiliza Plan para acordar un enfoque, Autopilot para crear el filtrado a partir de una incidencia e Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Hemos empezado por añadir una pequeña funcionalidad al proyecto. Sin embargo, los cambios más amplios necesitan un proceso más sólido. Por suerte, GitHub Copilot CLI está diseñado para adaptarse al flujo de trabajo existente de una organización y ayudarnos a crear lo adecuado de la forma correcta. Esta es la primera de varias lecciones en las que seguirás un proceso habitual de desarrollo dirigido por agentes: partirás de una incidencia para crear una funcionalidad, comprobarás que el código es válido y que la funcionalidad se comporta como esperas y, por último, la combinarás correctamente en el proyecto.

> [!NOTE]
> A medida que avances con esta funcionalidad, utilizarás la misma conversación y la misma rama. Normalmente se crearían ramas o solicitudes de incorporación de cambios distintas para diferentes tipos de archivos, pero en este taller simplificaremos el proceso para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una conversación nueva de Copilot a partir de una incidencia de GitHub;
- definirás los requisitos en el modo Plan;
- implementarás la funcionalidad con el modo Autopilot;
- revisarás el código;
- validarás la funcionalidad manualmente en un navegador reenviado.

A medida que avances con la funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la aptitud existente `quality-checks`, añadirás validación MCP, crearás un agente de QA y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys está creciendo y las personas visitantes necesitan filtrar los juegos por categoría y editor. La incidencia de la lista de tareas pendientes describe la funcionalidad, pero antes de programar hay que acordar algunos detalles, como la combinación de categorías. Utilizarás el modo Plan para resolver estas decisiones y, después, autorizarás una implementación de alcance limitado con Autopilot.

## Contexto

Incorporar agentes de programación con IA al flujo de desarrollo no cambia los fundamentos. ¡Si acaso, los hace aún más importantes! La mayoría de los desarrolladores siguen un flujo parecido a este:

1. Parten de una incidencia registrada que describe lo que hay que hacer.
2. Elaboran un plan de lo que se debe crear.
3. Desarrollan el código y lo revisan.
4. Ejecutan las pruebas para validar el código.
5. Validan manualmente la nueva funcionalidad.
6. Crean una solicitud de incorporación de cambios (PR).
7. Cuando se ha revisado el código y se ha completado correctamente el proceso de integración continua, combinan el código.

> [!NOTE]
> Los detalles concretos dependen del equipo y de la organización, pero la mayoría de los procesos siguen alguna variante del flujo anterior.

Si sigues este enfoque estándar, te aseguras de que el código generado por IA cumpla los requisitos establecidos y pase por el mismo proceso de validación que el código escrito manualmente.

## Modos de conversación

El **modo de conversación** controla el grado de autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre los modos:

- **Interactive**: tú y el agente trabajáis juntos. El agente sugiere cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma: escribe código, ejecuta pruebas e itera hasta completar la tarea.

Empieza en el modo Plan, revisa el plan y, a continuación, utiliza Autopilot para implementarlo.

## Empieza desde la incidencia

Antes de comenzar el trabajo de filtrado, vuelve al Codespace y comprueba que el repositorio y el terminal estén preparados.

1. Vuelve al Codespace. Si está detenido, reinícialo antes de continuar.
2. Confirma que la PR de valoración por estrellas se ha combinado.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para el trabajo de filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Utiliza las teclas de flecha para resaltar la incidencia **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia a la instrucción y volver a la pestaña **Session**.

Observa que ahora la instrucción empieza por `#7` (o por un número parecido). El carácter `#` permite incluir en el contexto una incidencia o una solicitud de incorporación de cambios (PR) de GitHub.

## Planifica la funcionalidad de filtrado

La planificación te permite definir cómo se implementará una funcionalidad o se realizará una tarea antes de encargársela a Copilot. Para cualquier trabajo complejo, siempre conviene dedicar un tiempo a planificar. Cambiemos al modo Plan y pidamos a Copilot que cree el plan.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Plan. Comprueba que el indicador debajo de la instrucción muestra **Plan**.
2. Después de la referencia a la incidencia añadida en el paso anterior, escribe esta instrucción:

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot empezará a elaborar el plan. Primero explorará el proyecto y, después, determinará el mejor enfoque.

3. Durante el proceso, Copilot podría hacer preguntas sobre el funcionamiento del filtrado. Respóndelas según tus preferencias. No hay respuestas incorrectas.
4. Cuando el plan esté completo, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para ampliar el plan.
5. Desplázate hacia arriba y hacia abajo para revisarlo.
6. Pide a Copilot que modifique cualquier parte del plan que no coincida con tus decisiones.

## Aprueba Autopilot

Una vez redactado y revisado el plan, es el momento de implementarlo. Dejemos que Copilot trabaje utilizando Autopilot.

Autopilot permite que Copilot itere sobre el problema hasta que considere que lo ha resuelto.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente que aparezca en la versión instalada.
2. Comprueba que el indicador debajo de la instrucción muestra **Autopilot**.
3. Observa cómo Copilot sigue el plan acordado, genera código y ejecuta pruebas.

> [!NOTE]
> Al aprobarlo, puede que la implementación empiece inmediatamente, así que revisa primero el plan. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar las comprobaciones por completadas.

## Revisa y comprueba la implementación

Una vez generado el código, debes revisarlo antes de combinarlo, como harías con cualquier otro código. Revisemos el código y ejecutemos el sitio para comprobar que todo funciona.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar en el modo Interactive. Comprueba que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Escribe `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y con las decisiones que tomaste durante la planificación.
4. Cuando termines la revisión del código, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa los resultados de las comprobaciones del proyecto y pide a Copilot que solucione los errores que haya.

## Explora la nueva funcionalidad

El código parece correcto, pero ¿se ejecuta? Iniciemos la aplicación como antes y abramos el sitio a través del puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros por categoría y editor, y las combinaciones que acordaste en el plan.
4. Comprueba que el comportamiento de restablecimiento y de resultados vacíos coincide con la incidencia y con tus decisiones.
5. Vuelve al Codespace y pide a Copilot que detenga el servidor de desarrollo que ha iniciado.

## Resumen y próximos pasos

Has utilizado distintos modos de conversación para crear y revisar una funcionalidad. En esta lección:

- has iniciado una conversación nueva de Copilot a partir de una incidencia de GitHub;
- has definido los requisitos en el modo Plan;
- has implementado la funcionalidad con el modo Autopilot;
- has revisado el código;
- has validado manualmente la funcionalidad en un navegador reenviado.

A continuación, profundizarás en cómo se genera el código y te asegurarás de que siga las prácticas documentadas mediante [instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
