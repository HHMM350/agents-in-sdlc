---
title: "Ejercicio 2: añade funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas de una aplicación suelen requerir cambios en varios archivos y tareas como ejecutar pruebas. El flujo de trabajo de un desarrollador suele consistir en localizar todos los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo falta, volver a cambiarlo... Y así sucesivamente.

Para eso sirve el modo de agente de Copilot.

El modo de agente de Copilot puede trabajar de forma más autónoma en el IDE. Se comporta de manera parecida a un desarrollador: primero explora la estructura existente del proyecto, hace los cambios necesarios, ejecuta tareas como las pruebas y corrige automáticamente los errores que encuentra. Vamos a ver cómo puedes usar el modo de agente para añadir funcionalidades al sitio.

> [!NOTE]
> Aunque los nombres son parecidos, el modo de agente y cloud agent están pensados para experiencias distintas. El modo de agente trabaja en el IDE, por lo que permite interacciones y ciclos de comentarios rápidos. Cloud agent trabaja de forma asíncrona como una persona del equipo e interactúa contigo mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio aprenderás:

- cómo el modo de agente de Copilot puede explorar el proyecto, identificar los archivos pertinentes y hacer cambios coordinados.
- cómo puede implementar nuevas funcionalidades en la interfaz de usuario y la capa de datos.
- cómo revisar los cambios y las pruebas que genera antes de fusionarlos en el código.

## Escenario

A medida que crece la lista de juegos, quieres permitir que los usuarios filtren por categoría y editor. En el ejercicio anterior ya añadiste un método auxiliar para editores. Ahora completarás el trabajo de la capa de datos, la interfaz de usuario y las pruebas con el modo de agente de Copilot.

## Ejecuta el sitio web de Tailspin Toys

Antes de hacer cambios, vamos a explorar el sitio web de Tailspin Toys para conocer sus funciones actuales.

El sitio es una plataforma de financiación colectiva de juegos de mesa con una temática para desarrolladores. Permite mostrar los juegos y sus detalles. Es una única aplicación Astro que genera las páginas como HTML estático durante la compilación. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM en el frontmatter; no hay una API de backend independiente ni un marco de interfaz de cliente. Los métodos auxiliares reutilizables para acceder a los datos están en `src/lib/`, y la interactividad se implementa con scripts `<script>` pequeños y específicos de Astro que usan las API DOM estándar.

### Inicia el sitio

Para facilitar la ejecución del sitio, se incluye la tarea `npm run dev`, que inicia un único servidor de desarrollo de Astro. Puedes ejecutarla en GitHub Codespaces así:

1. Vuelve a tu codespace. Después del ejercicio anterior, deberías estar en `main`.
2. Abre una ventana de terminal nueva en el codespace pulsando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama para trabajar en el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio con este comando:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, aparecerá un mensaje con la URL, parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo para abrir un navegador con `http://localhost:4321`, ciérralo seleccionando **x**.

5. Abre el sitio manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando en el terminal la dirección del servidor Astro: `http://localhost:4321`.

> [!NOTE]
> En un codespace, al seleccionar el vínculo de localhost en el terminal, se te redirigirá automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Se trata de un túnel privado al codespace, que ahora aloja el servidor web.

### Explora el sitio

Cuando esté en ejecución, puedes explorar sus funciones principales:

- **Página de inicio:** muestra una lista de juegos de mesa con títulos, imágenes y descripciones.
- **Página de detalles del juego:** al seleccionar un juego, se abre una página con más información, como el título, la descripción, el editor y la categoría.

## Explora las incidencias pendientes con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los siguientes ejercicios, vuelve al codespace, abre el panel de Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso los indica cuando corresponde.

La implementación inicial del sitio funciona, pero queremos añadir otras funciones. Empezaremos por revisar las incidencias pendientes. Al crear el proyecto a partir de la plantilla, se generó automáticamente una lista de incidencias. Pide a GitHub Copilot que te las muestre.

1. Selecciona **Agent** en el menú desplegable de agentes de la vista Chat. El agente puede planificar e implementar cambios de forma autónoma en varios archivos, ejecutar comandos de terminal y usar herramientas.

   ![Captura del selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no prefieren un modelo sobre otro. Al crear el taller, usamos Claude Sonnet 4.5, por lo que lo indicamos aquí. Esperamos que las sugerencias de código sean relativamente coherentes y la experiencia sea buena. Sin embargo, como los modelos de lenguaje grandes (LLM) son probabilísticos, puede que las sugerencias no coincidan con las del taller. Es normal y previsible.

> [!NOTE]
> Como los LLM son probabilísticos, Copilot puede usar un comando MCP distinto y aun así completar la tarea.

3. Pide a Copilot que muestre las incidencias pendientes con este mensaje:

   ```plaintext
   Muéstrame las incidencias pendientes de mi repositorio de GitHub. Ayúdame a priorizarlas según su utilidad para los usuarios.
   ```

4. Selecciona **Continue** para ejecutar el comando que enumera las incidencias.
5. Revisa la lista generada.

Fíjate en que Copilot también ha priorizado las incidencias según la utilidad que cree que tienen para los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere el código, conviene revisar el archivo de instrucciones que proporciona contexto a Copilot. Usarás el archivo de [interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que explica cómo añadir funciones al sitio.

1. En tu codespace, abre `.github/instructions/ui.instructions.md`.
2. Fíjate en las directrices generales para añadir funciones, como:
   - una descripción de la arquitectura.
   - principios de diseño de componentes, capacidad de prueba y accesibilidad.
   - vínculos a instrucciones específicas para varios tipos de archivo, incluidos:
     - Astro.
     - Tailwind CSS.
     - Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden incluir vínculos a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas al archivo de instrucciones. Así se pueden reutilizar instrucciones, dividir conjuntos complejos en partes más manejables e incluir ejemplos y plantillas.

## Implementa el filtrado

Para completar el filtrado, tendrás que hacer al menos tres cambios independientes en la aplicación:

- añadir o ajustar la lógica restante de filtrado en la capa de datos (`src/lib/`).
- añadir o actualizar las pruebas del comportamiento del filtrado.
- actualizar la página con la lista de juegos para incluir la interfaz del filtrado.

Además, las pruebas deben ejecutarse correctamente antes de fusionar los cambios. El modo de agente de Copilot puede ocuparse de estas tareas. Vamos a añadir la funcionalidad.

1. Puedes continuar la conversación actual con Copilot o iniciar otra seleccionando **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Captura de cómo seleccionar el archivo de instrucciones de interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Comprueba que **Agent** siga seleccionado en el menú desplegable de agentes de la vista Chat.

   ![Captura del selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Comprueba que siga seleccionado **Claude Sonnet 4.5**.
5. Pide a Copilot que implemente la funcionalidad según la incidencia relacionada de la lista:

   ```plaintext
   Actualiza el sitio para que permita filtrar por editor y categoría de acuerdo con los requisitos de la incidencia relacionada de GitHub. Ya existe un método auxiliar para editores del ejercicio anterior; consérvalo y mejóralo si hace falta al completar la lógica restante de la capa de datos, la interfaz y las pruebas. Comprueba que todas las pruebas se superan antes de terminar. El servidor ya está en ejecución, así que no hace falta que lo inicies.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos relacionados con la funcionalidad: los métodos auxiliares de la capa de datos, la interfaz y las pruebas. Después modifica los archivos y ejecuta las pruebas.

   ![Captura de Copilot explorando los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. Según la complejidad de la tarea y del código, puede tardar varios minutos. Mientras trabaja, puede que aparezcan los botones **Keep** y **Undo** en el editor. Cuando termine, tendrás una opción **Keep** o **Undo** para cada cambio; no hace falta que la selecciones mientras el agente sigue trabajando.

7. Cuando Copilot te lo pida, selecciona **Continue** para ejecutar las pruebas.

   ![Captura del diálogo de Copilot Chat para confirmar que quieres ejecutar las pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede que haya pausas o que algunas pruebas fallen durante el proceso. No pasa nada: Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea y dejar de detectar errores.

   ![Captura de una sesión completa de Copilot Agent Mode](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explora el código generado para detectar posibles problemas.

> [!CAUTION]
> Recuerda que siempre es importante revisar el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador donde se está ejecutando el sitio y explora la nueva funcionalidad.
11. Cuando hayas confirmado que todo funciona y revisado el código, selecciona **Keep** en la ventana de Copilot Chat.

## Resumen y siguientes pasos

¡Enhorabuena! En este ejercicio has aprendido a usar el modo de agente de GitHub Copilot para añadir funciones al sitio de Tailspin Toys. Has visto cómo:

- el modo de agente implementa nuevas funciones en la interfaz y en la capa de datos.
- puede explorar el proyecto, identificar los archivos pertinentes y hacer cambios coordinados.
- puedes revisar los cambios y las pruebas que genera antes de fusionarlos.

Ahora, [probaremos la funcionalidad con el servidor Playwright MCP][next-lesson] y abriremos una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar la paginación

A medida que crece la lista de juegos, será necesario habilitar la paginación. Usa las habilidades aprendidas en este ejercicio y pide a Copilot que la implemente en el sitio. Al planificar el código:

- sigue las prácticas recomendadas existentes, incluidos los archivos de instrucciones.
- decide cómo quieres implementar la paginación: por ejemplo, si los usuarios podrán elegir el tamaño de página o si será fijo.
- incluye en el mensaje las directrices necesarias para que Copilot implemente lo que quieres.
- puede que tengas que iterar con GitHub Copilot y proporcionar cambios y contexto. Es lo normal al trabajar con Copilot.

## Recursos

- [Modos Ask, Edit y Agent de Copilot: qué hacen y cuándo usarlos][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
