---
title: "Lección 10: Repaso y próximos pasos"
description: "Repasa el flujo de trabajo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI a lo largo de un flujo de trabajo de Tailspin Toys. En este proceso:

- has preparado un Codespace, instalado Copilot CLI, explorado el proyecto y encontrado la incidencia de filtrado creada de antemano;
- has añadido las valoraciones por estrellas, revisado el resultado en un navegador reenviado y combinado manualmente tu primera solicitud de incorporación de cambios (PR);
- has partido de la incidencia de filtrado, definido el enfoque en el modo Plan, creado la funcionalidad en el modo Autopilot y revisado el resultado en el modo Interactive;
- has orientado al agente con instrucciones personalizadas, personalizado la habilidad existente `quality-checks` y utilizado esta para ejecutar pruebas unitarias, lint y comprobaciones de tipos;
- has añadido el servidor del Protocolo de contexto de modelo (MCP) de Playwright y lo has utilizado para probar el filtrado en un navegador real;
- has creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas en el navegador;
- has revisado todos los cambios de filtrado y autorizado Agent Merge para combinar la PR de filtrado;
- has explorado los comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente al agente en la nube.

## Qué has publicado

El taller tiene dos hitos de PR, cada uno en su propia rama creada a partir de `main` actualizada:

1. **Valoraciones por estrellas:** mostrar el valor existente de `starRating` y un estado explícito para los juegos sin valorar en las tarjetas.
2. **Filtrado y flujo de trabajo de calidad:** implementar el filtrado, actualizar las instrucciones y aplicarlas a la funcionalidad, personalizar el informe de `quality-checks`, crear un perfil de QA e incluir las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su PR, has utilizado la misma conversación y la misma rama. Para agilizar el taller, hemos incluido todo ese trabajo en una sola PR.

## Diferentes tipos de verificación

Has comprobado el código de varias formas: con pruebas automatizadas, con tu propia inspección en el navegador y con la exploración del navegador que Copilot ha realizado mediante MCP. La habilidad `quality-checks` ha ejecutado pruebas unitarias, lint y comprobaciones de tipos, y ha incluido los resultados en el nuevo formato. QA ha reunido esos resultados con la revisión de los requisitos y la cobertura de pruebas antes de la PR.

Las pruebas nuevas deben resolver carencias reales; si una ejecución de QA determina que no hacen falta pruebas, también puede ser correcto. Antes de autorizar la combinación, revisa el código y las pruebas que respaldan el resultado, y vuelve a generar las pruebas afectadas después de realizar cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas a Copilot dan forma a su trabajo. En este taller has actualizado las instrucciones, personalizado una habilidad, creado un perfil de QA y configurado un servidor MCP. Reutiliza estas personalizaciones en otras conversaciones y ajústalas a medida que cambien las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Utiliza **Plan** para definir un enfoque antes de empezar a desarrollar, **Interactive** para mantener el control de los cambios concretos y **Autopilot** para las tareas bien delimitadas. Elige un modelo más rápido para las modificaciones rutinarias y uno más avanzado para el trabajo complejo.

El contexto sigue siendo tan importante como la infraestructura. Describir con claridad *qué* quieres crear, *por qué* y *cómo* cambia de forma significativa el resultado.

## Más aspectos que explorar

Has completado el flujo de trabajo principal. Estas son algunas funciones más de CLI que puedes explorar:

- `/review` para pedir al agente de revisión de código que analice los cambios;
- `/rubber-duck` para hablar de un problema y obtener otra perspectiva;
- `/fleet` para coordinar subtareas independientes en paralelo;
- `/worktree` para aislar una tarea distinta;
- `/delegate` para enviar una tarea al agente en la nube de Copilot.

## Próximos pasos

La mejor forma de mejorar con cualquier herramienta es seguir utilizándola. Úsala para código de producción, para proyectos personales o para esa pequeña aplicación que tienes en mente desde hace años y nunca has llegado a crear. Comparte lo que aprendas con el equipo y aprende de sus experiencias. Y, como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller del agente en la nube de Copilot][cloud].

## Recursos

- [Información sobre GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
