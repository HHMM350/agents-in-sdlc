---
title: "Ejercicio 3: agentes personalizados"
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

Con los agentes personalizados explorarás:

- cómo se definen los agentes personalizados.
- cómo asignar una tarea a un agente personalizado.

## Escenario

Tailspin Toys se compromete a que todas las personas puedan usar su plataforma de financiación colectiva, independientemente de sus capacidades o preferencias visuales. Los comentarios recientes indican que algunas personas tienen dificultades para leer el tema oscuro actual debido al poco contraste entre el texto y el fondo. Para solucionar este problema de accesibilidad, el equipo de diseño ha solicitado un modo de contraste alto que se pueda activar y desactivar.

Como la accesibilidad es fundamental, quieres implementar esta función cuanto antes. Para ello, usarás un agente personalizado.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado de accesibilidad para ti. Vamos a revisar su contenido para entender cómo guiará a Copilot.

Vuelve a tu codespace y revisa el archivo del agente personalizado de accesibilidad:

1. Abre `.github/agents/accessibility.md`.
2. Fíjate en los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios en los agentes personalizados.

3. Revisa las secciones siguientes, que describen:
   - las responsabilidades principales al generar código para un sitio web accesible.
   - las prácticas recomendadas de accesibilidad.
   - ejemplos de código HTML, CSS y JavaScript.
   - problemas y errores habituales.

## Crea y asigna una incidencia

El panel de agentes es el centro de control para trabajar con todos los agentes de tu entorno. Permite asignar tareas a Copilot cloud agent, supervisarlas y reorientarlas, y proporcionar directrices adicionales. Vamos a pedir a Copilot que cree el modo de contraste alto.

1. Ve a tu repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el formulario de una incidencia nueva.
4. Selecciona **Blank issue**.
5. Escribe `Add high contrast mode to website` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   Necesitamos un modo de contraste alto para el sitio. Debe haber un conmutador para activarlo, y la selección del usuario debe guardarse en el almacenamiento local del navegador.
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el diálogo de asignación.
9. Selecciona **Accessibility agent** en la lista de agentes personalizados.

   ![Captura del diálogo de asignación de cloud agent, con el agente personalizado y Accessibility resaltados](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.
11. ¡Copilot empezará a trabajar en segundo plano!

## Resumen y siguientes pasos

En esta lección has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes de IA especializados para tareas y áreas concretas. Con ellos, puedes convertir los conocimientos y estándares del equipo en agentes reutilizables que ayuden a Copilot a realizar determinados tipos de trabajo con mayor eficacia.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados.
- cómo asignar una tarea a un agente personalizado.

Mientras Copilot implementa el modo de contraste alto, puedes [supervisar y dirigir la sesión del agente][next-lesson] desde el panel de agentes.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparación para usar agentes personalizados en tu organización][org-custom-agents]
- [Preparación para usar agentes personalizados en tu empresa][enterprise-custom-agents]

---

| [← Lección anterior: GitHub Copilot cloud agent][previous-lesson] | [Siguiente lección: supervisar y administrar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
