---
title: "Lección 6: Validar la funcionalidad con Playwright MCP"
description: "Inspecciona o configura Playwright MCP en Copilot CLI y utilízalo para probar la funcionalidad de filtrado en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos indicado, programar no consiste únicamente en escribir código. Tenemos que trabajar con datos y servicios externos, e incluso proporcionar a Copilot más automatizaciones. Para eso sirven los servidores MCP: permiten que Copilot vaya más allá de las funciones integradas en la CLI y le proporcionan más herramientas y servicios.

En esta lección:

- comprenderás qué es el Protocolo de contexto de modelo (MCP) y cómo lo utiliza Copilot CLI;
- añadirás el servidor MCP de Playwright si todavía no está disponible;
- pedirás al agente que controle un navegador y explore la funcionalidad de filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar las actualizaciones de la interfaz de usuario hay que interactuar con ella. Quieres que Copilot pueda utilizar el sitio web como lo haría una persona y automatizar aún más el proceso de cambios, para tener mayor confianza en que las actualizaciones funcionan como se espera.

## ¿Qué es el Protocolo de contexto de modelo (MCP)?

El [Protocolo de contexto de modelo (MCP)][mcp-blog-post] permite a los agentes de IA comunicarse con herramientas y servicios externos. Gracias a MCP, los agentes de IA pueden comunicarse con herramientas y servicios externos en tiempo real. Esto les permite acceder a información actualizada y realizar acciones en tu nombre.

Se accede a estas herramientas y recursos a través de un servidor MCP, que actúa como puente entre el agente de IA y las herramientas y los servicios externos. Cada servidor MCP representa un conjunto distinto de herramientas y recursos a los que puede acceder el agente de IA.

Algunos servidores MCP existentes y populares son:

- **[Servidor MCP de GitHub][github-mcp]**: proporciona acceso a las API para gestionar repositorios de GitHub, incidencias y solicitudes de incorporación de cambios.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: proporciona funciones de automatización del navegador mediante Playwright.

Hay muchos otros servidores MCP disponibles. GitHub aloja un [registro de MCP][mcp-registry] para facilitar la búsqueda y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, verifica quién lo publica y considera las implicaciones de seguridad.

## Añade el servidor MCP de Playwright

Si el servidor MCP de Playwright todavía no está disponible, añádelo para que Copilot pueda interactuar con el sitio web como lo haría una persona.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos de configuración y continúa con la sección siguiente.

1. Vuelve a tu Codespace.
2. En Copilot CLI, abre el cuadro de diálogo para añadir un servidor MCP escribiendo el comando siguiente:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** pulsando <kbd>Enter</kbd> y, a continuación, pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el cuadro de diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor MCP nuevo.
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de diálogo MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Antes has confirmado manualmente que la funcionalidad se comporta como esperas. Ahora utilizaremos el servidor MCP de Playwright disponible en Copilot para hacer lo mismo.

1. Envía esta instrucción a Copilot para pedirle que utilice el servidor MCP de Playwright y valide la funcionalidad:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> No es necesario pedir expresamente a Copilot que utilice el servidor MCP, ya que normalmente lo averiguará por su cuenta. Sin embargo, como sabes qué herramienta debería utilizar, nunca está de más indicárselo. Así aumentará la coherencia de los resultados y se utilizarán menos tokens.

2. Observa cómo Copilot enumera los pasos que va realizando en el navegador para comprobar que la funcionalidad funciona.
3. Lee el informe y asegúrate de que todo se comporta como se esperaba.

Copilot iniciará el servidor, utilizará Playwright para interactuar con el sitio web, detendrá el servidor y te entregará un informe.

## Resumen y próximos pasos

¡Enhorabuena! Has utilizado el servidor MCP de Playwright para explorar la funcionalidad en un navegador real desde Copilot CLI. En resumen:

- has aprendido qué es el Protocolo de contexto de modelo (MCP) y cómo lo utiliza Copilot CLI;
- has añadido el servidor MCP de Playwright si todavía no estaba disponible;
- has pedido al agente que controle un navegador y explore la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de QA][next-lesson] que combinará la aptitud y las herramientas del navegador en un rol especializado.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de ello?][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
