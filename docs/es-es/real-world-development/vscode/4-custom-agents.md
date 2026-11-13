---
title: "Ejercicio 4: agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o áreas concretas del flujo de trabajo de desarrollo. Al definirlos en archivos Markdown en la carpeta `.github/agents` del repositorio, puedes proporcionar a Copilot instrucciones, prácticas recomendadas, patrones de programación y conocimientos específicos para que realice determinados tipos de trabajo con mayor eficacia. Los equipos pueden convertir sus conocimientos en agentes reutilizables; por ejemplo, un agente de accesibilidad que aplique las pautas de [WCAG][wcag], uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones coherentes.

Los agentes personalizados se definen en archivos Markdown de la carpeta `.github/agents` del proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, como mínimo, `name` y `description`, seguido de una instrucción Markdown que define el comportamiento, la experiencia y las directrices del agente.

### Agentes personalizados y skills de agente

Hay cierto solapamiento entre los agentes personalizados y las [skills de agente][agent-skills-concept]. Ambos se definen principalmente mediante archivos Markdown e indican a una IA cómo realizar operaciones. La forma más sencilla de distinguirlos es que un **agente personalizado** es quien realiza el trabajo y las **skills** son las herramientas.

Los agentes personalizados tienen su propia ventana de contexto y están diseñados para coordinar skills e incluso otros agentes. En este laboratorio, el agente personalizado de accesibilidad revisará el sitio y lo actualizará de acuerdo con las pautas de accesibilidad; para hacerlo, podría llamar a skills como una skill de flujo de solicitudes de incorporación de cambios o una que ejecute y administre pruebas.

> [!NOTE]
> No hay una única manera correcta de crear un agente personalizado. Como ocurre con cualquier tecnología de IA, prueba distintas opciones e itera para encontrar la que mejor se adapte a tu entorno y a tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys se compromete a que todas las personas puedan usar su plataforma de financiación colectiva, independientemente de sus capacidades o preferencias visuales. Los comentarios recientes indican que algunas personas tienen dificultades para leer el tema oscuro actual debido al poco contraste entre el texto y el fondo. Para solucionar este problema de accesibilidad, el equipo de diseño ha solicitado un modo de contraste alto que se pueda activar y desactivar.

Como la accesibilidad es fundamental, quieres implementar esta función cuanto antes. Para ello, usarás un agente personalizado.

En este ejercicio:

- revisarás un agente personalizado de accesibilidad existente.
- usarás el agente de accesibilidad en Copilot Chat para implementar un modo de contraste alto.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado de accesibilidad para ti. Vamos a revisar su contenido para entender cómo guiará a Copilot.

Vuelve a tu codespace y abre un terminal. Crea una rama nueva desde `main` para el trabajo de accesibilidad; así mantendrás separada la solicitud de filtrado del ejercicio 3:

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. Abre `.github/agents/accessibility.md`.
2. Fíjate en los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios en los agentes personalizados.

3. Revisa las secciones siguientes, que describen:
   - las responsabilidades principales al generar código para un sitio web accesible.
   - las prácticas recomendadas de accesibilidad.
   - ejemplos de código HTML, CSS y JavaScript.
   - problemas y errores habituales.

## Usa el agente personalizado en Copilot Chat

VS Code muestra todos los agentes personalizados definidos en `.github/agents` en el menú desplegable de agentes de la parte inferior de la vista Copilot Chat. Puedes seleccionar un agente personalizado para aplicar sus instrucciones y herramientas a la sesión.

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los siguientes ejercicios, vuelve al codespace, abre el panel de Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso los indica cuando corresponde.

1. Si no está seleccionado, elige **Agent** en el menú desplegable de agentes de la vista Chat.

   ![Captura del selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Abre el menú desplegable de agentes en la parte inferior de la vista Chat. Muestra el agente activo; de forma predeterminada, es **default**.
3. Selecciona **Accessibility agent** en la lista de agentes.
4. Envía este mensaje al agente de accesibilidad:

   ```plaintext
   Añade al sitio un modo de contraste alto. Debe haber un conmutador para activarlo, y la selección del usuario debe guardarse en el almacenamiento local del navegador para que se conserve al volver a cargar la página.
   ```

5. Copilot Chat explorará el código, propondrá cambios y editará los archivos del proyecto. Cada edición aparecerá en el chat junto con la ruta del archivo y las diferencias para que puedas revisarla.
6. A medida que se apliquen los cambios, se actualizará el indicador **Files changed** para mostrar los archivos modificados por el agente.

> [!NOTE]
> El proceso puede tardar varios minutos. Copilot modificará archivos reales del repositorio, como componentes Astro, CSS y pruebas relacionadas.

Revisarás y orientarás este trabajo en curso en el siguiente ejercicio.

## Resumen y siguientes pasos

En esta lección has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes de IA especializados para tareas y áreas concretas. Con ellos, puedes convertir los conocimientos y estándares del equipo en agentes reutilizables que ayuden a Copilot a realizar determinados tipos de trabajo con mayor eficacia.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados.
- cómo usar un agente personalizado en el modo de agente de Copilot Chat.

A continuación, [supervisarás y orientarás el trabajo del agente][next-lesson], revisarás los cambios a medida que se produzcan y añadirás un conmutador para el modo claro en la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados de awesome-copilot][awesome-copilot-agents]

---

| [← Lección anterior: prueba la funcionalidad con el servidor Playwright MCP][previous-lesson] | [Siguiente lección: supervisar y administrar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
