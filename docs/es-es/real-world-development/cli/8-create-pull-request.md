---
title: "Lección 8: Crear y combinar la PR de la funcionalidad"
description: "Revisa en conjunto el filtrado, las instrucciones, la actualización de la aptitud, el perfil de QA y las pruebas; después crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de instrucciones, la actualización de la aptitud, el perfil de control de calidad (QA) y las pruebas están guardados en una misma rama. Es el momento de revisarlos en conjunto y abrir una solicitud de incorporación de cambios. Combinaste manualmente la PR de valoración por estrellas; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente separaríamos la funcionalidad, las actualizaciones de instrucciones, la actualización de la aptitud y el agente de QA en varias PR. Para agilizar el taller, has mantenido todo el flujo de trabajo de filtrado y calidad en una conversación y una rama, y todo ese trabajo se incluirá en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una PR;
- inspeccionarás todos los cambios de la funcionalidad y las pruebas de verificación;
- crearás la PR de filtrado;
- activarás Agent Merge únicamente después de revisar los cambios y confirmarás que la PR se ha combinado.

## Escenario

Durante el flujo de trabajo de filtrado, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere ahora automatizar el trabajo restante de la PR, pero mantener bajo el control del desarrollador la autorización para combinarla.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante necesario para integrar una solicitud de incorporación de cambios. Cuando lo activas, Copilot resuelve los impedimentos que haya para combinarla: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y vuelve a realizar la combinación con la rama base cuando sea necesario. Después, activa la combinación automática de GitHub si el repositorio lo permite.

Hasta ahora has seleccionado manualmente **Merge pull request**. Agent Merge puede encargarse de esa responsabilidad. Revisa el trabajo y asegúrate de que está listo antes de activarlo.

## Utiliza Agent Merge para gestionar la PR

Ya está todo el código. Revisémoslo en conjunto, creemos la PR y dejemos que Agent Merge gestione el resto del proceso.

1. Vuelve a tu Codespace.
2. Abre el cuadro de diálogo de agentes escribiendo `/agent`.
3. Selecciona **Default** en la lista de opciones y pulsa <kbd>Enter</kbd>.
4. Crea una PR con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la PR. Cuando todas las comprobaciones hayan terminado correctamente, la combinará.
7. Comprueba que Copilot muestra un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, lee el motivo indicado y completa manualmente la combinación revisada cuando la configuración del repositorio lo permita.

## Resumen y próximos pasos

Has automatizado varias partes del proceso de desarrollo: generar código, probarlo y validarlo, y ahora gestionar el proceso de la solicitud de incorporación de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una PR;
- has inspeccionado todos los cambios de la funcionalidad y las pruebas de verificación;
- has creado la PR de filtrado;
- has activado Agent Merge únicamente después de revisar los cambios y has confirmado que la PR se ha combinado.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente al agente en la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
