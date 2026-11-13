---
title: "Lección 1: instala GitHub Copilot CLI"
description: "Instala y autentica Copilot CLI en tu codespace, conoce el entorno y localiza la incidencia de filtrado inicial."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] es un potente asistente de programación con agentes que se ejecuta en el terminal y permite explorar bases de código, generar código, ejecutar comandos e interactuar con herramientas externas desde la línea de comandos. Te permite delegar tareas, solicitar cambios y mantener la concentración. El primer paso es instalar la herramienta; por suerte, puedes hacerlo con herramientas que ya conoces.

En esta lección:

- instalarás GitHub Copilot CLI con npm.
- iniciarás sesión con tu cuenta de GitHub.
- confiarás en el repositorio del taller y probarás una conversación rápida.
- localizarás la incidencia de filtrado con el servidor GitHub MCP integrado.

## Escenario

Tu equipo está empezando a usar agentes de IA para abordar una lista creciente de tareas pendientes. Copilot CLI lleva esa capacidad al terminal, donde ya trabajan muchos desarrolladores. En esta lección instalarás y autenticarás la herramienta, y la dejarás lista para el resto del taller.

## Instala Copilot CLI

Puedes instalar Copilot CLI con [npm][install-cli], WinGet o Homebrew. Como GitHub Codespaces incluye Node.js, usarás npm.

1. Vuelve a tu codespace y abre un terminal.
2. Comprueba que Node.js esté instalado y cumpla el requisito de versión:

   ```bash
   node --version
   ```

   Debe aparecer la versión 24 o posterior.

3. Instala Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Comprueba la instalación:

   ```bash
   copilot --version
   ```

   Debería aparecer el número de versión.

## Inicia sesión con GitHub

La primera vez que se inicia Copilot CLI, solicita que te autentiques con tu cuenta de GitHub.

1. Inicia Copilot CLI:

   ```bash
   copilot
   ```

2. Si se te solicita, sigue las instrucciones del código de dispositivo para autenticarte y autorizar Copilot CLI.
3. Copilot CLI mostrará este mensaje:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Confirma que la ruta corresponde al repositorio de Tailspin Toys y selecciona **Yes, and remember this folder for future sessions**.

> [!NOTE]
> En un codespace, puede que ya hayas iniciado sesión mediante tu sesión de GitHub. Si Copilot CLI se inicia sin pedirte que te autentiques, ya está listo.

## Familiarízate con el entorno

Los comandos escritos en el prompt habitual del shell se ejecutan directamente en el codespace. Después de iniciar Copilot CLI, los mensajes en lenguaje natural se envían al agente y los comandos de barra controlan la conversación.

1. Escribe `/model`, usa las teclas de flecha para seleccionar **Auto**, pulsa <kbd>Enter</kbd> y vuelve a pulsar <kbd>Enter</kbd> para confirmar.
2. Escribe `/help` para ver los comandos de la versión instalada y pulsa <kbd>Esc</kbd> para cerrar la ayuda.
3. Haz una pregunta sencilla para comprobar que todo funciona:

   ```plaintext
   ¿Cuáles son los archivos principales de este proyecto?
   ```

4. Lee la respuesta y observa cómo Copilot explora el repositorio antes de responder.
5. Escribe `/mcp list` y confirma que está disponible el servidor GitHub MCP integrado.
6. Pide a Copilot que encuentre la incidencia de filtrado:

   ```plaintext
   Usa GitHub MCP para buscar en este repositorio la incidencia titulada "Allow users to filter games by category and publisher". Dame su URL y un breve resumen. No hagas cambios.
   ```

7. Abre la URL y lee la incidencia. La usarás después de completar un primer cambio rápido.

> [!TIP]
> Una sesión normal de Copilot CLI trabaja en la rama que esté seleccionada en el terminal; no crea un worktree automáticamente. Crearás una rama de funcionalidad antes de cada cambio.

## Usa el atajo del taller

Normalmente, Copilot CLI pide permiso antes de usar herramientas fuera de los permisos establecidos. En este taller, la iniciarás con `--yolo`, un atajo aprobado por ti que elimina esas solicitudes dentro del codespace para que puedas centrarte en los ejercicios.

> [!CAUTION]
> `--yolo` habilita los permisos automáticos completos (`--allow-all-tools`, `--allow-all-paths` y `--allow-all-urls`). Úsalo solo en un entorno aislado, como un codespace o una máquina virtual; nunca lo configures como opción predeterminada para el desarrollo diario. Consulta [Permitir y denegar el uso de herramientas][allow-all-warning] para obtener más información.

En este taller, `--enable-all-github-mcp-tools` habilita las herramientas de lectura y escritura de GitHub MCP que usarás en lecciones posteriores para trabajar con incidencias y solicitudes de incorporación de cambios. El codespace limita el acceso a tu equipo local, pero los recursos de GitHub autenticados siguen siendo reales. Revisa los cambios antes de publicarlos o fusionarlos.

1. Sal de Copilot CLI con `/exit`.
2. Vuelve a iniciarlo desde la raíz del repositorio:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Haz otra pregunta rápida sobre el proyecto para confirmar que la conversación funciona y, después, sal con `/exit`.

Copilot guarda las conversaciones automáticamente. Más adelante, cuando cambies las instrucciones o añadas un agente, volverás a la misma conversación y rama con `copilot --resume`.

## Resumen y siguientes pasos

Enhorabuena. En esta lección:

- has instalado GitHub Copilot CLI con npm.
- has iniciado sesión con tu cuenta de GitHub.
- has confiado en el repositorio del taller y probado una conversación rápida.
- has localizado la incidencia de filtrado con el servidor GitHub MCP integrado.

A continuación, [empezarás tu primer cambio concreto][next-lesson] y usarás Copilot CLI para mostrar una valoración por estrellas en las tarjetas de juegos.

## Recursos

- [Instalar GitHub Copilot CLI][install-cli]
- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
