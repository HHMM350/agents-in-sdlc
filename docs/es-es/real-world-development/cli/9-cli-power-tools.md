---
title: "Lección 9: comandos de barra de GitHub Copilot CLI"
description: "Explora los comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier buena herramienta de CLI, GitHub Copilot CLI incluye muchos comandos de barra para interactuar con ella. Estos comandos permiten acceder a funciones avanzadas, información interna y opciones de configuración adicionales. Ya has usado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Vamos a explorar otros que resultan útiles.

En esta lección:

- usarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- usarás `/model` para ver qué modelos tienes disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas en el agente en la nube.

## Escenario

Has completado el flujo de trabajo principal de la CLI. Ahora veremos otras funciones: gestionar el contexto, cambiar de modelo, compartir sesiones y delegar trabajo opcionalmente en [Copilot cloud agent][about-cloud-agent].

## Explora el contexto de Copilot CLI

Al trabajar en tareas grandes o complejas, puede que alcances la ventana de contexto máxima del modelo. Copilot CLI compacta la conversación automáticamente cuando lo necesita, y puedes inspeccionar o compactar el contexto tú mismo con comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Anota el modelo, el uso actual de tokens y cómo se reparte el contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Puede que no haya cambiado mucho si la conversación ya era corta.

> [!NOTE]
> Copilot CLI compacta el contexto automáticamente a medida que se llena la ventana. Usa `/compact` cuando quieras elegir el momento. Usa `/clear` o `/new` cuando cambies a una tarea distinta y quieras iniciar una conversación nueva.

## Elige el modelo

Los modelos tienen distintas fortalezas y cada desarrollador puede tener sus preferencias. Copilot CLI permite mostrar y seleccionar el modelo que quieras usar.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información sobre su uso.
3. Conserva el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Trabajar en equipo y compartir lo aprendido ayuda a todos a sacar más partido a las herramientas de IA. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un vínculo para compartirla o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` de la versión que tienes instalada.
2. Si quieres compartir esta sesión, elige el destino que mejor se adapte a tus necesidades, como `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviárselo a alguien o publicarlo. Las exportaciones de sesiones pueden incluir mensajes, respuestas y detalles del proyecto.

Publicar un vínculo o un gist es opcional. No publiques contenido del repositorio o de la conversación que el equipo no tenga previsto compartir.

## Opcional: amplía el trabajo o delégalo

Has completado el taller principal. Copilot CLI también ofrece comandos para tareas de mayor envergadura:

- `/fleet` puede repartir subtareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un worktree de Git aislado para una tarea aparte.
- `/delegate` puede enviar una tarea a Copilot cloud agent, que trabaja de forma asíncrona y puede abrir una solicitud de incorporación de cambios.

Estos comandos son opcionales porque pueden crear worktrees adicionales o enviar trabajo a un servicio remoto. Empieza con una tarea nueva y bien acotada antes de probarlos y revisa el resultado con tu flujo de trabajo habitual. Si quieres profundizar en el trabajo asíncrono con agentes, continúa con el [taller sobre cloud agent][cloud-workshop].

## Resumen y siguientes pasos

Los comandos de barra de Copilot CLI permiten configurarla, compartir sesiones y consultar lo que sucede internamente. En esta lección:

- has usado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- has usado `/model` para ver los modelos disponibles.
- has aprendido cómo `/share` puede exportar o compartir una sesión.
- has explorado comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas en el agente en la nube.

Copilot CLI ofrece muchos otros comandos de barra y funciones por descubrir. Para terminar el recorrido, [repasaremos lo aprendido][next-lesson] y veremos cómo seguir aprendiendo.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Administración del contexto en Copilot CLI][context-management]
- [Acerca de Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
