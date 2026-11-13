---
title: "Lección 2: añade valoraciones por estrellas, una mejora rápida"
description: "Usa Copilot CLI para hacer un pequeño cambio en las tarjetas de juegos, revisarlo en un navegador de Codespaces y fusionarlo en tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ahora que has instalado Copilot CLI y has probado una conversación, es el momento de hacer tu primer cambio en el proyecto. Será pequeño: los datos de los juegos ya incluyen una valoración por estrellas, pero las tarjetas de la página principal aún no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo fusionarás como tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una conversación de Copilot centrada en una rama de funcionalidad.
- pedirás al agente que haga un pequeño cambio en el proyecto.
- revisarás el cambio con `/diff`.
- ejecutarás la aplicación para comprobarlo en un navegador de Codespaces.
- abrirás y fusionarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración por estrellas, que ya aparece en la página de detalles. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, el editor y la descripción. Como ejercicio inicial, pedirás al agente que muestre la valoración existente en cada tarjeta: un cambio pequeño e independiente, perfecto para tu primera sesión.

## Anatomía de una conversación

Una **conversación** es el espacio donde trabajas con Copilot CLI en una tarea. A diferencia de la aplicación de Copilot, una conversación normal de la CLI usa el repositorio y la rama de Git que tienes actualmente seleccionados en el terminal, en lugar de crear un worktree dedicado. Las conversaciones guardadas te permiten volver a la misma conversación más tarde, mientras los archivos y la rama siguen siendo el estado normal de Git en el disco.

En una conversación verás tres cosas: tus mensajes y las respuestas del agente, la actividad de las herramientas mientras el agente explora y edita archivos, y los cambios que puedes inspeccionar con `/diff`.

## Inicia una conversación y solicita el cambio

Vamos a iniciar una conversación nueva para empezar a implementar la funcionalidad.

1. Vuelve a tu Codespace.
2. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Si Copilot aún no está abierto, inicia la CLI con este comando:

   ```bash
   copilot --yolo
   ```

4. Inicia una sesión nueva con el comando de barra `/new` y pulsa <kbd>Enter</kbd>.
5. Usa este mensaje para solicitar el cambio:

   ```plaintext
   Muestra la propiedad starRating de cada juego sobre 5 en las tarjetas de la página de listado. Si la valoración es null, muestra "No rating yet". Mantén el diseño actual de las tarjetas, añade pruebas y ejecuta las comprobaciones pertinentes.
   ```

Copilot explorará el proyecto, localizará los archivos que se usan para mostrar los detalles de los juegos y creará el código necesario. ¡Ya has añadido una funcionalidad con Copilot CLI!

## Revisa las diferencias

Debes revisar todos los cambios generados por IA antes de fusionarlos, aunque sean pequeños. Vamos a inspeccionarlos en Copilot CLI.

1. Escribe `/diff` e inspecciona todos los archivos modificados.
2. Confirma que la tarjeta muestra la valoración numérica cuando existe y `No rating yet` cuando `starRating` es `null`.
3. Confirma que las pruebas cubren ambos casos.
4. Revisa los resultados de las comprobaciones que ha ejecutado Copilot y pídele que corrija los errores.
5. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.

> [!NOTE]
> Como Copilot, al igual que todas las herramientas de IA generativa, es probabilístico y no determinista, el código concreto puede variar. Revisa su comportamiento en lugar de esperar una implementación exacta.

## Comprueba los cambios

No basta con leer el código y dar por hecho que funciona. Vamos a pedir a Copilot que inicie el sitio para examinar la interfaz actualizada en el navegador abierto desde Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Inicia la aplicación para que pueda comprobar en el navegador el cambio de la valoración por estrellas. Dime la URL y deja el servidor en ejecución.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Confirma que las tarjetas de juegos muestran las valoraciones sobre cinco.
4. Vuelve a Copilot y pídele que detenga el servidor que ha iniciado:

   ```plaintext
   Detén el servidor de desarrollo que has iniciado.
   ```

## Abre y fusiona tu primera solicitud de incorporación de cambios

¡Ya has creado la funcionalidad! Ahora crearás una solicitud de incorporación de cambios (PR) para incorporarla al proyecto.

1. Pide al agente predeterminado que confirme el cambio:

   ```plaintext
   Crea un commit con los cambios revisados de la valoración por estrellas y usa un mensaje apropiado.
   ```

2. Escribe `/pr create`. Copilot CLI subirá el commit existente al crear la solicitud y mostrará la URL.
3. Abre la solicitud manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando la URL que muestra Copilot CLI.
4. Revisa los archivos modificados y las comprobaciones.
5. Cuando esté todo listo, selecciona **Merge pull request** y confirma la fusión.
6. Vuelve a tu Codespace y sal de Copilot CLI con `/exit`.
7. Actualiza tu rama local `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumen y siguientes pasos

¡Enhorabuena! Has publicado tu primer cambio con GitHub Copilot CLI. En concreto:

- has iniciado una conversación de Copilot centrada en una rama de funcionalidad.
- has pedido al agente que haga un pequeño cambio en las tarjetas de juegos.
- has revisado el cambio con `/diff`.
- has ejecutado la aplicación para comprobar la valoración por estrellas en un navegador de Codespaces.
- has abierto y fusionado tu primera solicitud de incorporación de cambios.

A continuación, [partirás de la incidencia de filtrado y usarás los modos Plan y Autopilot][next-lesson] para crear una funcionalidad más amplia.

## Recursos

- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
