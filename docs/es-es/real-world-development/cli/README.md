---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Crea, verifica y entrega dos cambios en Tailspin Toys mientras aprendes los modos, las personalizaciones, las herramientas MCP y la automatización de solicitudes de incorporación de cambios de Copilot CLI."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** incorpora GitHub Copilot al terminal como asistente de programación con agentes. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas, todo desde la línea de comandos, para que puedas mantener el flujo sin cambiar a un editor gráfico.

El taller sigue un flujo de trabajo continuo en Tailspin Toys:

1. Prepara el proyecto en GitHub Codespaces, instala Copilot CLI y familiarízate con el entorno.
2. Haz un cambio específico en la valoración por estrellas, revísalo en el navegador y fusiona manualmente tu primera solicitud de incorporación de cambios (PR).
3. Parte de la incidencia de filtrado, define el enfoque en modo Plan, impleméntalo en modo Autopilot y revísalo en modo Interactive.
4. Actualiza las instrucciones del repositorio y aplícalas al trabajo de filtrado.
5. Personaliza la skill `quality-checks` existente y úsala para ejecutar las comprobaciones del proyecto.
6. Añade el servidor Model Context Protocol (MCP) de Playwright y úsalo para explorar el filtrado en un navegador.
7. Crea un agente personalizado de control de calidad (QA) y úsalo para revisar requisitos, cobertura y pruebas de verificación.
8. Revisa todo el cambio de filtrado y usa Agent Merge para la solicitud correspondiente.
9. Explora comandos de barra útiles para gestionar el contexto y los modelos, compartir sesiones y delegar tareas opcionalmente en la nube.

Para centrar el taller, crearás dos solicitudes: una para las valoraciones por estrellas y otra para el filtrado, con las actualizaciones de instrucciones y de la skill, el perfil de QA y las pruebas. El flujo de filtrado y calidad comparte una conversación y una rama para que puedas aprovechar el trabajo al explorar cada herramienta.

## Lecciones

| Lección | Tema | Descripción |
| ------ | ----- | ----------- |
| [0. Requisitos previos][ex0] | Configuración | Crea el repositorio y el codespace |
| [1. Instalar Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI y familiarízate con el entorno |
| [2. Añadir valoraciones por estrellas: una mejora rápida][ex2] | Primer cambio | Muestra las valoraciones y el estado sin valoración y, después, fusiona la primera solicitud |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica la función desde su incidencia, impleméntala con Autopilot y revísala en Interactive |
| [4. Guiar a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones y aplícalas al filtrado |
| [5. Personalizar y usar una skill quality-checks][ex5] | Comprobaciones repetibles | Explora la skill existente, cambia el formato del informe y ejecútala |
| [6. Validar la funcionalidad con Playwright MCP][ex6] | Observación en el navegador | Configura MCP en la CLI y examina el comportamiento del filtrado |
| [7. Crear y usar un agente de QA][ex7] | Requisitos y cobertura | Crea y selecciona un perfil especializado y reúne las pruebas de verificación finales |
| [8. Crear y fusionar la solicitud de la función][ex8] | Revisión y fusión | Revisa todo el cambio, crea la solicitud y usa Agent Merge |
| [9. Comandos de barra de GitHub Copilot CLI][ex9] | Funciones de CLI | Explora el contexto, los modelos, el uso compartido y la delegación opcional a cloud agent |
| [10. Resumen y siguientes pasos][ex10] | Resumen | Repasa el flujo, las personalizaciones reutilizables y otros recursos |
| [Opcional: incorporar Foundry][foundry] | Agentes hospedados | Prepara un modelo, implementa un agente basado en el catálogo y conéctalo al sitio |

## Requisitos previos

Antes de participar en este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Permiso para crear un repositorio y un codespace
- [ ] Conocimientos básicos del terminal o de la línea de comandos

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][student-plan]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que se usan en este taller.

> [!NOTE]
> Si usas Copilot Business o Copilot Enterprise, confirma con el administrador que Copilot CLI esté habilitado.

## Primeros pasos

**[Empieza por los requisitos previos →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
