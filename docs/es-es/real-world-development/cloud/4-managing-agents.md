---
title: "Ejercicio 4: supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los dos ejercicios anteriores has pedido a Copilot cloud agent que se ocupe de tres tareas independientes para mejorar la experiencia de usuario y añadir funcionalidades. Aunque cloud agent está diseñado para trabajar de forma asíncrona y autónoma, también es importante poder supervisar esas tareas.

Hay varias herramientas para administrar las tareas asignadas a cloud agent, incluida la [página de agentes][agents-page] de GitHub.com. Desde este centro de control puedes ver todas las tareas de los agentes que tienen solicitudes de incorporación de cambios abiertas. Puedes consultar las operaciones realizadas e incluso orientar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas de cloud agent.
- orientarás una sesión en curso para solicitar una funcionalidad adicional.

## Escenario

Después de asignar al agente la creación de un modo de contraste alto, el equipo se dio cuenta de que también sería buen momento para añadir un modo claro. Como ya se iban a actualizar los estilos del sitio y a añadir una función de cambio de modo, parecía razonable incluirlo. Quieres orientar el trabajo del agente para que añada tanto el modo claro como el modo de contraste alto.

## Revisa las tareas de Copilot cloud agent

Vamos a consultar el estado de todas las tareas asignadas a Copilot cloud agent.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Fíjate en la lista de tareas del panel principal y del panel izquierdo. Deberías ver las tareas que has asignado a Copilot, entre ellas:
   - actualizar la documentación del código.
   - generar API para modificar juegos.
   - añadir un modo de contraste alto al sitio web.
3. Selecciona una de las tareas en curso y revisa las operaciones que ha realizado Copilot. Pueden incluir:
   - obtener el código del repositorio.
   - crear el entorno de trabajo de Copilot.
   - configurar servidores MCP.
   - realizar varios pasos para completar la tarea asignada.

> [!NOTE]
> Los pasos concretos varían en función del estado del trabajo de Copilot y del enfoque que haya seguido.

4. Fíjate también en el panel de solicitudes de incorporación de cambios (PR) de la derecha. Desde ahí puedes consultar la solicitud y los archivos modificados para seguir el trabajo.

## Orienta el trabajo del agente en la nube

Ya has visto las tareas activas. Ahora pediremos a Copilot que añada la opción de modo claro mientras trabaja en el modo de contraste alto.

1. Selecciona la sesión relacionada con el modo de contraste alto. El título exacto dependerá del nombre que le haya puesto Copilot y del estado del trabajo.

   ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Observa la sesión durante unos minutos, hasta que indique que ha terminado la configuración y ha empezado a trabajar. Lo sabrás cuando empiecen a aparecer mensajes parecidos a los siguientes.
3. En el diálogo **Steer active session while Copilot is working**, escribe este mensaje:

   ```plaintext
   Ya que estamos trabajando en un modo de contraste alto, vamos a añadir también un modo claro. Debe haber un conmutador para este modo, de forma que los usuarios puedan seleccionar el modo de visualización que prefieran.
   ```

   ![Captura de la tarea de cloud agent en la página de agentes, con el diálogo para orientar la sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el mensaje.
5. Observa cómo Copilot confirma que lo ha recibido y lo incorpora a su flujo de trabajo.

## Deja que Copilot trabaje

Como antes, Copilot empezará a trabajar en la tarea actualizada. Incorporará la solicitud nueva al flujo cuando termine el paso que estaba ejecutando al recibir el mensaje.

El proceso tardará varios minutos. Es un buen momento para hacer una pausa y repasar todo lo que has aprendido y explorado hasta ahora.

## Resumen y siguientes pasos

En esta lección has explorado la página de agentes de Copilot, el centro de control para supervisar y orientar las tareas de GitHub Copilot cloud agent. Desde ahí puedes seguir las tareas activas y completadas, revisar el trabajo y reorientar tareas en curso para ajustar su alcance o añadir directrices.

Has explorado estos conceptos:

- has usado el centro de control y la página de agentes para supervisar las tareas de cloud agent.
- has reorientado una sesión en curso para solicitar una funcionalidad adicional.

Mientras Copilot termina de trabajar en las funciones de accesibilidad, puedes [iterar sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: agentes personalizados][previous-lesson] | [Siguiente lección: iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
