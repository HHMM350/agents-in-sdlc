---
title: "Lección 6: valida la funcionalidad con Playwright MCP"
description: "Inspecciona o configura Playwright MCP en Copilot CLI y úsalo para explorar en el navegador la funcionalidad de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos comentado, programar no consiste únicamente en escribir código. También hay que trabajar con datos y servicios externos, e incluso proporcionar a Copilot más automatizaciones. Para ello sirven los servidores MCP: permiten que Copilot vaya más allá de las funciones integradas en la CLI y acceda a otras herramientas y servicios.

En esta lección:

- aprenderás qué es Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- añadirás el servidor Playwright MCP si aún no está disponible.
- pedirás al agente que use un navegador para explorar la funcionalidad de filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar cambios en la interfaz hay que interactuar con ella. Quieres que Copilot pueda usar el sitio web como lo haría una persona y automatizar mejor los cambios, para tener más confianza en que funcionan como se espera.

## ¿Qué es Model Context Protocol (MCP)?

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos. Con MCP, los agentes pueden consultar en tiempo real información actualizada y realizar acciones en tu nombre.

Se accede a estas herramientas y recursos a través de un servidor MCP, que actúa como puente entre el agente de IA y las herramientas y los servicios externos. Cada servidor MCP representa un conjunto distinto de herramientas y recursos al que el agente puede acceder.

Algunos servidores MCP conocidos son:

- **[GitHub MCP Server][github-mcp]**: proporciona acceso a API para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: proporciona funciones de automatización del navegador con Playwright.

Hay muchos otros servidores MCP disponibles. GitHub aloja un [registro de MCP][mcp-registry] para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de usar uno, revisa su código fuente, comprueba quién lo publica y ten en cuenta las implicaciones de seguridad.

## Añade el servidor Playwright MCP

Si aún no está disponible el servidor Playwright MCP, añádelo para que Copilot pueda interactuar con el sitio como lo haría un usuario.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos y continúa con la sección siguiente.

1. Vuelve a tu Codespace.
2. Abre el diálogo para añadir un servidor MCP con el siguiente comando en Copilot CLI:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Comprueba que el tipo de servidor sea **STDIO** y pulsa <kbd>Enter</kbd>; después, pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor MCP.
7. Pulsa <kbd>Esc</kbd> para salir del diálogo de MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Antes confirmaste manualmente que la funcionalidad se comporta como esperabas. Ahora usaremos el servidor Playwright MCP disponible en Copilot para hacer lo mismo.

1. Usa este mensaje para pedir a Copilot que valide la funcionalidad con el servidor Playwright MCP:

   ```plaintext
   Inicia la aplicación y usa Playwright MCP para comprobar el filtrado con respecto a la incidencia y al plan. Dime qué funciona y qué no, sin hacer cambios. Detén el servidor que has iniciado cuando termines.
   ```

> [!NOTE]
> No es necesario pedir expresamente a Copilot que use el servidor MCP, ya que normalmente lo averiguará por su cuenta. Aun así, indicar la herramienta que debe utilizar ayuda a obtener resultados más coherentes y puede ahorrar algunos tokens.

2. Observa cómo Copilot enumera los pasos que ejecuta en el navegador para comprobar que la funcionalidad funciona.
3. Lee el informe y confirma que todo se comporta como se espera.

Copilot iniciará el servidor, usará Playwright para interactuar con el sitio, detendrá el servidor y te dará un informe.

## Resumen y siguientes pasos

¡Enhorabuena! Has usado el servidor Playwright MCP para explorar la funcionalidad en un navegador real desde Copilot CLI. En resumen:

- has aprendido qué es Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- has añadido el servidor Playwright MCP si aún no estaba disponible.
- has pedido al agente que use un navegador para explorar la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de QA][next-lesson] que combinará la skill y las herramientas del navegador en una función especializada.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de ello?][mcp-blog-post]
- [Servidor Playwright MCP de Microsoft][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
