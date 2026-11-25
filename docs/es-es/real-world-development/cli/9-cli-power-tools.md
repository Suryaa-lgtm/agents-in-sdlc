---
title: "Lección 9: Comandos de barra de GitHub Copilot CLI"
description: "Explora los comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente al agente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier herramienta de CLI completa, GitHub Copilot CLI incluye muchos comandos de barra para interactuar con ella. Estos comandos permiten acceder a funciones avanzadas, consultar información interna y cambiar opciones de configuración. Ya has utilizado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Veamos algunos otros que pueden resultar útiles.

En esta lección:

- utilizarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación;
- utilizarás `/model` para explorar los modelos disponibles;
- aprenderás cómo `/share` puede exportar o compartir una sesión;
- explorarás comandos opcionales para trabajar en paralelo, utilizar árboles de trabajo y delegar al agente en la nube.

## Escenario

Has terminado el flujo principal de trabajo con CLI. Ahora veremos otras funciones: gestionar el contexto, cambiar de modelo, compartir sesiones y, de forma opcional, delegar trabajo al [agente en la nube de Copilot][about-cloud-agent].

## Explora el contexto de Copilot CLI

Al trabajar en tareas grandes o complejas, puede que alcances la ventana de contexto máxima del modelo. Copilot CLI compacta automáticamente la conversación cuando es necesario, y puedes inspeccionar o compactar el contexto tú mismo mediante comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio, si todavía no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y cómo se distribuye el contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio disponible.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Si la conversación ya es corta, puede que no haya cambiado mucho.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto a medida que se llena la ventana. Utiliza `/compact` si quieres decidir cuándo hacerlo. Utiliza `/clear` o `/new` cuando cambies a una tarea que no esté relacionada y quieras empezar una conversación nueva.

## Elige el modelo

Cada modelo tiene capacidades diferentes y cada desarrollador puede tener sus propias preferencias. Copilot CLI permite mostrar una lista de los modelos disponibles y seleccionar el que quieras utilizar.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información sobre su uso.
3. Conserva el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Colaborar en equipo y compartir lo aprendido ayuda a todo el mundo a mejorar el uso de las herramientas de IA. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartirla o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` de la versión instalada.
2. Si quieres compartir la sesión, elige el destino que mejor se adapte a tus necesidades, por ejemplo, `/share file` para exportar localmente un archivo Markdown.
3. Revisa el contenido exportado antes de enviárselo a alguien o publicarlo. Las exportaciones de sesiones pueden incluir instrucciones, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de la conversación que tu equipo no tenga previsto compartir.

## Opcional: amplía el trabajo o delega

El flujo principal del taller ha terminado. Copilot CLI también proporciona comandos para tareas más grandes:

- `/fleet` puede dividir una tarea en subtareas independientes, asignarlas a subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un árbol de trabajo de Git aislado para una tarea distinta.
- `/delegate` puede enviar una tarea al agente en la nube de Copilot, que trabaja de forma asincrónica y puede abrir una solicitud de incorporación de cambios.

Estos comandos son opcionales porque pueden crear otros árboles de trabajo o trabajo remoto. Antes de probarlos, inicia una tarea nueva y bien delimitada, y revisa el resultado con el flujo habitual. Si quieres profundizar en el trabajo asincrónico de los agentes, continúa con el [taller sobre el agente en la nube][cloud-workshop].

## Resumen y próximos pasos

Los comandos de barra de Copilot CLI permiten configurar la herramienta, compartir sesiones y consultar lo que ocurre entre bastidores. En esta lección:

- has utilizado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación;
- has utilizado `/model` para explorar los modelos disponibles;
- has aprendido cómo `/share` puede exportar o compartir una sesión;
- has explorado comandos opcionales para trabajar en paralelo, utilizar árboles de trabajo y delegar al agente en la nube.

Hay más comandos de barra y funciones de Copilot CLI por explorar. Para terminar el recorrido, [repasaremos lo aprendido][next-lesson] y los siguientes pasos para continuar aprendiendo.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Información sobre el agente en la nube de Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
