---
title: "Lección 7: Crear y utilizar un agente de QA"
description: "Crea un agente personalizado de QA que combine los requisitos de las incidencias, la habilidad de agente quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has utilizado la habilidad de agente `quality-checks` para ejecutar comprobaciones automatizadas y Playwright MCP para observar la experiencia de filtrado en un navegador. Ahora reunirás estas funciones en un agente personalizado con un proceso de QA claramente definido.

En esta lección:

- explorarás cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP;
- crearás y revisarás un perfil de control de calidad reutilizable;
- seleccionarás el agente de QA y revisarás sus conclusiones respecto a la incidencia de filtrado.

## Escenario

Tailspin Toys quiere que, antes de abrir una solicitud de incorporación de cambios (PR), se revisen de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador. Un agente personalizado puede coordinar el proceso de QA y proporcionar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot que se define mediante un perfil Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles para el agente. En este taller, definirás un rol de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Las personalizaciones que has utilizado tienen funciones distintas. Las instrucciones del repositorio describen los estándares del equipo. La habilidad `quality-checks` agrupa comprobaciones repetibles. Playwright MCP proporciona herramientas de navegador. El perfil de QA indica a Copilot cómo utilizar estas funciones para evaluar los requisitos e informar de los resultados. No las sustituye ni requiere iniciar otra conversación.

## Crea el perfil de QA

Antes de abrir la PR de la funcionalidad, pedirás a Copilot que cree un perfil de QA reutilizable. El perfil definirá tanto las comprobaciones que realiza QA como los límites que debe respetar.

1. Vuelve a tu Codespace y comprueba que la conversación de filtrado está en el modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Inspecciona el perfil

Antes de utilizar el agente nuevo, revisa su perfil para comprobar que Copilot ha incorporado el proceso de QA y los límites previstos. Así evitarás que un perfil incompleto o demasiado amplio modifique la funcionalidad cuando solo quieres que se verifique.

1. Escribe `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. `description` es obligatorio; `name` es opcional, pero incluirlo da al agente un nombre claro en la interfaz.
3. Lee las instrucciones del perfil y comprueba que QA empieza por los requisitos, sigue las instrucciones del repositorio, ejecuta la habilidad `quality-checks` y utiliza Playwright MCP.
4. Comprueba que QA comunica las pruebas que respaldan sus conclusiones, solicita permiso antes de cambiar el código de implementación y no crea confirmaciones ni abre solicitudes de incorporación de cambios.
5. Si al perfil generado le falta alguna de estas responsabilidades o límites, pide al agente predeterminado que lo revise antes de continuar.

## Ejecuta QA con la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Después de crear el perfil, reanuda la misma conversación de filtrado y selecciona QA para que pueda utilizar la incidencia y las decisiones de planificación que ya forman parte del contexto.

1. Activa el agente con esta instrucción:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, quizá no aparezca en la lista de agentes disponibles. Aun así, existe y el comando anterior lo activará.

2. Envía esta instrucción para pedir al agente de QA que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. ¡El agente de QA se pondrá a trabajar!
4. Cuando termine, lee el informe que te proporcione.

## Resumen y próximos pasos

Has añadido al flujo de trabajo un rol especializado reutilizable y has revisado su trabajo. En esta lección:

- has explorado cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP;
- has creado y revisado un perfil de control de calidad reutilizable;
- has seleccionado el agente de QA y revisado sus conclusiones respecto a la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y el informe de verificación listos para revisión. A continuación, [los reunirás en una PR de funcionalidad y utilizarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
