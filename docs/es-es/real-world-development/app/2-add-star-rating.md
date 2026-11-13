---
title: "Lección 2: añade valoraciones por estrellas, una mejora rápida"
description: "Inicia tu primera sesión de agente en la aplicación de GitHub Copilot, haz un pequeño cambio en las tarjetas de juegos y fusiónalo en tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Ahora que has explorado el espacio de trabajo y probado un chat rápido, es el momento de iniciar una **sesión de agente** y hacer tu primer cambio en el proyecto. Será pequeño: los juegos ya incluyen una valoración por estrellas en sus datos, pero las tarjetas de la página principal aún no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo fusionarás como tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una sesión de agente y aprenderás cómo se estructura.
- pedirás al agente que haga un cambio pequeño y concreto en el proyecto.
- revisarás el cambio en la vista de diferencias del espacio de trabajo.
- ejecutarás la aplicación localmente para comprobar el cambio en el navegador.
- abrirás y fusionarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración por estrellas, que ya aparece en la página de detalles. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, el editor y la descripción. Como ejercicio inicial, pedirás al agente que muestre la valoración existente en cada tarjeta: un cambio pequeño e independiente, perfecto para tu primera sesión.

## Anatomía de una sesión

Una **sesión** es una conversación con un agente que se ejecuta en su propio espacio de trabajo aislado. Cada sesión tiene un **worktree y una rama de Git dedicados**, lo que permite ejecutar varias sesiones a la vez —por ejemplo, una para añadir una función y otra para corregir un error— sin que sus cambios entren en conflicto. Las sesiones aparecen en la barra lateral, agrupadas por repositorio; selecciona una para cambiar a ella.

En una sesión verás tres elementos: la **conversación** con el agente, la **actividad de las herramientas** mientras explora y edita archivos, y la lista de **archivos modificados** con sus diferencias.

## Inicia una sesión y solicita el cambio

Vamos a iniciar una sesión nueva para explorar el proyecto e implementar la funcionalidad. Durante la [configuración de la aplicación][prior-lesson], añadiste el proyecto desde su repositorio de GitHub. Ahora crearemos una sesión para ese repositorio y solicitaremos el cambio.

1. Vuelve a abrir la aplicación de GitHub Copilot.
2. Selecciona **+** en la parte superior de la barra lateral para iniciar una sesión.
3. Selecciona el repositorio `tailspin-toys`.
4. Elige un **new working tree** y el modo **Interactive** debajo del cuadro de mensaje. Usa este mensaje para solicitar el cambio:

   ```plaintext
   Muestra la propiedad starRating de cada juego sobre 5 en las tarjetas de la página de listado. Si la valoración es null, muestra "No rating yet". Mantén el diseño actual de las tarjetas, añade pruebas y ejecuta las comprobaciones pertinentes.
   ```

5. Pulsa <kbd>Enter</kbd> para enviar el mensaje a Copilot.

La aplicación de Copilot empezará creando un worktree nuevo, una copia aislada del proyecto. Después explorará el proyecto, localizará los archivos que debe actualizar para añadir la función y creará el código necesario. ¡Ya has añadido una función con la aplicación de Copilot!

## Revisa las diferencias

Debes revisar todos los cambios generados por IA antes de fusionarlos, aunque sean pequeños. Vamos a inspeccionarlos en la aplicación de Copilot.

1. En la esquina superior derecha de la aplicación, selecciona **Toggle review panel**. En el panel que se abre, selecciona **Changes** para ver los archivos modificados y sus diferencias.

   ![Barra de herramientas superior de la aplicación de GitHub Copilot con una flecha que señala el botón Toggle review panel, a la derecha de Create PR](../../../_images/app-2-review-panel.png)

2. Deberías ver código añadido a `GameCard.astro`, el archivo principal para mostrar los detalles de los juegos. Debería parecerse a este pequeño bloque, que muestra la valoración si existe y, si `starRating` es `null`, muestra «No rating yet»:

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como Copilot, al igual que todas las herramientas de IA generativa, es probabilístico y no determinista, el código exacto puede variar. No obstante, debería ser relativamente parecido.

## Comprueba los cambios

Revisa los resultados de las comprobaciones automatizadas del agente antes de abrir un navegador. Confirma que las pruebas cubren una valoración `starRating` numérica y el caso de `null`. Un requisito previo ausente o una comprobación omitida no cuentan como superados; revisa cualquier solicitud de instalación antes de aprobarla.

No basta con leer el código y dar por hecho que funciona. Vamos a pedir a Copilot que abra el sitio para examinar la interfaz actualizada. Le pediremos que lo inicie y lo abra en un lienzo de navegador.

> [!TIP]
> Un lienzo es un widget interactivo disponible dentro de la aplicación de Copilot. Más adelante explorarás lienzos personalizados e incluso crearás uno, pero por ahora usaremos el lienzo de navegador integrado.

1. Usa este mensaje para pedir a Copilot que inicie la aplicación y abra la página en el lienzo de navegador:

   ```plaintext
   Inicia la aplicación y ábrela en el lienzo de navegador.
   ```

2. En unos instantes, la aplicación se iniciará y se abrirá una ventana del navegador dentro de la aplicación de Copilot.
3. Confirma que las tarjetas de juegos valorados muestran su puntuación sobre cinco.
4. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión y cierre el lienzo de navegador:

   ```plaintext
   Detén el servidor de desarrollo y cierra el lienzo de navegador.
   ```

## Abre y fusiona tu primera solicitud de incorporación de cambios

¡Ya has creado la función! Ahora crearás una solicitud de incorporación de cambios (PR) para integrarla en el código existente.

1. Selecciona **Create PR** en la esquina superior derecha.
2. Si se te solicita, selecciona **Sign in with your browser** y sigue las instrucciones para autenticarte.
3. Si Copilot indica que la política del repositorio requiere una incidencia asociada antes de crear la solicitud, confirma que debe seguir ese proceso.
4. Copilot empezará a crear la solicitud.
5. Selecciona la burbuja **PR** justo encima del chat para abrir la solicitud en el panel de revisión. Desde ahí podrás revisarla.
6. Cuando esté lista, selecciona **Ready to merge**.
7. En el nuevo cuadro de diálogo, selecciona **Merge pull request** para fusionar la solicitud.

## Resumen y siguientes pasos

¡Enhorabuena! Has publicado tu primer cambio con la aplicación de GitHub Copilot. En concreto:

- has iniciado una sesión de agente y aprendido cómo se estructuran las sesiones.
- has pedido al agente que haga un cambio pequeño y concreto en las tarjetas de juegos.
- has revisado el cambio en la vista de diferencias del espacio de trabajo.
- has ejecutado la aplicación localmente para comprobar la valoración por estrellas en el navegador.
- has abierto la solicitud 1, revisado sus comprobaciones y la has fusionado explícitamente.

A continuación, [partirás de la incidencia de filtrado y usarás los modos Plan y Autopilot][next-lesson] para crear una función más amplia.

## Recursos

- [Trabajar con sesiones de agente en la aplicación de GitHub Copilot][agent-sessions]
- [Acerca de la aplicación de GitHub Copilot][about-copilot-app]
- [Administrar incidencias y solicitudes de incorporación de cambios con la aplicación de GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instala-y-configura-la-aplicación-de-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
