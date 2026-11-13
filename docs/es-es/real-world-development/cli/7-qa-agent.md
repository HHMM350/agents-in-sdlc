---
title: "Lección 7: crea y usa un agente de QA"
description: "Crea un agente personalizado de QA que combine los requisitos de la incidencia, la skill quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has usado la skill `quality-checks` para ejecutar comprobaciones automatizadas y Playwright MCP para observar en el navegador la experiencia de filtrado. Ahora combinarás esas funciones en un agente personalizado con un proceso de QA bien definido.

En esta lección:

- explorarás cómo trabaja un agente personalizado con instrucciones, skills y herramientas MCP.
- crearás e inspeccionarás un perfil reutilizable de control de calidad.
- seleccionarás el agente de QA y revisarás sus conclusiones con respecto a la incidencia de filtrado.

## Escenario

Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador antes de abrir una solicitud de incorporación de cambios (PR). Un agente personalizado puede coordinar el proceso de QA y generar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe el objetivo, las instrucciones y las herramientas disponibles para el agente. En este taller, definirás una función de QA en `.github/agents/qa.agent.md` y la seleccionarás en Copilot CLI.

Las personalizaciones que has usado cumplen funciones distintas. Las instrucciones del repositorio describen las normas del equipo. La skill `quality-checks` reúne comprobaciones repetibles. Playwright MCP proporciona herramientas para el navegador. El perfil de QA indica a Copilot cómo usar esas capacidades para evaluar los requisitos e informar de los resultados. No sustituye a las otras personalizaciones ni requiere otra conversación.

## Crea el perfil de QA

Antes de abrir la solicitud de la funcionalidad, pedirás a Copilot que cree un perfil de QA reutilizable. El perfil especificará las comprobaciones de QA y los límites que debe respetar.

1. Vuelve a tu Codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Crea un agente personalizado llamado QA en .github/agents/qa.agent.md. Debe comprobar las funcionalidades con respecto a sus incidencias y a los requisitos acordados, seguir las instrucciones del repositorio, ejecutar la skill quality-checks, usar Playwright MCP para verificar el comportamiento y añadir pruebas si falta cobertura.

   Debe indicar cada requisito como superado, no superado o bloqueado, con pruebas que respalden el resultado. Debe pedir permiso antes de cambiar el código de implementación y no debe confirmar cambios ni abrir solicitudes de incorporación de cambios.

   Por ahora, crea solo el perfil para que pueda revisarlo.
   ```

## Inspecciona el perfil

Antes de usar el agente nuevo, revisa su perfil para confirmar que Copilot ha incluido el flujo de trabajo de QA y los límites previstos. Así evitarás que un agente incompleto o demasiado permisivo cambie la funcionalidad cuando solo quieres verificarla.

1. Escribe `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. `description` es obligatorio; `name` es opcional, pero incluirlo da al agente un nombre claro en la interfaz.
3. Lee las instrucciones del perfil y confirma que QA parte de los requisitos, sigue las instrucciones del repositorio, ejecuta la skill `quality-checks` y usa Playwright MCP.
4. Confirma que QA aporta pruebas que respaldan sus conclusiones, pide permiso antes de cambiar el código de implementación y no confirma cambios ni abre solicitudes de incorporación de cambios.
5. Si el perfil generado omite alguna de estas responsabilidades o restricciones, pide al agente predeterminado que lo revise antes de continuar.

## Ejecuta QA con respecto a la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Reanuda la misma conversación de filtrado después de crear el perfil y selecciona QA para que pueda usar la incidencia y las decisiones de planificación que ya tienes en el contexto.

1. Activa el agente con este mensaje:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, es posible que no aparezca en la lista de agentes disponibles. Aunque no aparezca, el comando anterior lo activará.

2. Usa este mensaje para pedir al agente de QA que revise la funcionalidad:

   ```plaintext
   Revisa la funcionalidad de filtrado con respecto a la incidencia y a las decisiones de nuestro plan. ¿Está lista para una solicitud de incorporación de cambios?
   ```

3. ¡El agente de QA empezará a trabajar!
4. Cuando termine, lee el informe.

## Resumen y siguientes pasos

Has añadido una función especializada reutilizable y has revisado su trabajo. En esta lección:

- has explorado cómo trabaja un agente personalizado con instrucciones, skills y herramientas MCP.
- has creado e inspeccionado un perfil reutilizable de control de calidad.
- has seleccionado el agente de QA y revisado sus conclusiones con respecto a la incidencia de filtrado.

Ya tienes la implementación, la actualización de la skill, el perfil de QA, las pruebas y el informe de verificación listos para revisar. A continuación, [los reunirás en una solicitud de incorporación de cambios y usarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
