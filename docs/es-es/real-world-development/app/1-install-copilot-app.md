---
title: "Lección 1: instala la aplicación de GitHub Copilot"
description: "Instala la aplicación de GitHub Copilot, conecta el repositorio creado a partir de la plantilla, conoce el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La **[aplicación de GitHub Copilot][about-copilot-app]** es una aplicación de escritorio para el desarrollo dirigido por agentes. Se basa en GitHub Copilot CLI y se integra de forma nativa con GitHub, así que los repositorios, las ramas y las canalizaciones de CI funcionan sin configuración adicional. Está pensada para flujos de trabajo en los que diriges varios agentes en paralelo, cada uno en su propio espacio de trabajo aislado, en lugar de hacerlo todo por tu cuenta; también permite automatizar tareas repetitivas. Con Node.js instalado y el proyecto preparado, el siguiente paso es instalar la aplicación y conectar el repositorio.

En esta lección:

- instalarás la aplicación de GitHub Copilot e iniciarás sesión.
- añadirás el proyecto a la aplicación desde su repositorio de GitHub.
- conocerás el espacio de trabajo y la lista de tareas pendientes inicial que incluye la plantilla.
- probarás un chat rápido para conocer mejor la aplicación.

## Escenario

Tu equipo está adoptando agentes de IA para abordar una lista creciente de tareas pendientes. La aplicación Copilot ofrece un único lugar desde el que dirigir ese trabajo: seleccionar incidencias, ejecutar agentes, revisar cambios y fusionar solicitudes de incorporación de cambios. En esta lección instalarás y conectarás la aplicación, y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Necesitas un plan de Copilot válido: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si usas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instala y configura la aplicación de GitHub Copilot

El primer paso para usar la aplicación de GitHub Copilot es instalarla. Hay versiones para Windows, macOS y Linux. Vamos a instalar la aplicación, autenticarnos y añadir el repositorio de Tailspin Toys.

1. Abre en el navegador la [página de la aplicación de GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación después de instalarla.
4. Selecciona **Sign in to GitHub** y sigue las indicaciones para autenticarte. Si usas GitHub Enterprise Cloud con residencia de datos, selecciona **Use GitHub Enterprise** e introduce el nombre de host `*.ghe.com` cuando se te solicite. GitHub Enterprise Server no es compatible.
5. Si el proceso inicial te pide seleccionar repositorios, selecciona el repositorio de Tailspin Toys que has creado a partir de la plantilla. También puedes omitir este paso y añadir el proyecto más adelante.
6. Cuando se te solicite, elige un tema y completa la configuración inicial.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no hace falta volver a añadirlo.
8. Si aún no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Usa el propietario y el nombre del repositorio que anotaste en los requisitos previos.
9. Confirma que el repositorio aparece en la barra lateral. En esta disposición, las carpetas de repositorio, como `tailspin-toys`, aparecen agrupadas en **Sessions**, y las sesiones individuales se muestran debajo de cada repositorio.

## Familiarízate con el espacio de trabajo

Con el proyecto conectado, dedica un momento a conocer el espacio de trabajo. La aplicación organiza sus funciones en varias áreas de la barra lateral:

- **New**: inicia una sesión de chat con Copilot.
- **Pull requests**: muestra las solicitudes de incorporación de cambios gracias a la integración nativa con GitHub. Desde aquí puedes explorarlas y filtrarlas, comprobar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues**: muestra las incidencias de la misma manera. Puedes explorarlas y filtrarlas, e iniciar una sesión a partir de una incidencia.
- **Automations**: tareas de agente guardadas que se ejecutan según una programación o bajo demanda. Sirven para administrar listas de tareas, realizar tareas periódicas de mantenimiento y delegar otras actividades repetitivas. El resumen las propone como paso siguiente, no como otro ejercicio del taller.
- **Customize**: añade funciones a la aplicación Copilot mediante servidores MCP, plugins, skills y otros componentes. La usarás para configurar Playwright MCP.
- **Chats**: conversaciones sencillas para preguntas y lluvias de ideas que no necesitan una rama ni un espacio de trabajo propios. Esta sección aparece después de iniciar el primer chat. Si no la ves, selecciona **+** junto a **Sessions** para iniciar un chat.
- **Sessions**: agrupa las carpetas de repositorio y sus sesiones de agente. Selecciona un repositorio, como `tailspin-toys`, para abrir su vista, o selecciona una sesión para volver a esa conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado, por lo que puedes ejecutar varias a la vez sin que sus cambios entren en conflicto. Iniciarás tu primera sesión al añadir valoraciones por estrellas.

Explorarás el espacio de trabajo durante el taller.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si es posible, puede ayudarte a orientarte.

### Localiza la lista de tareas pendientes inicial

Casi todos los proyectos tienen tareas pendientes, y Tailspin Toys no es una excepción. Vamos a explorar la lista que se generó al crear el repositorio a partir de la plantilla.

1. En **Sessions**, selecciona la carpeta del repositorio Tailspin Toys, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título, no por el número:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia para leer sus detalles. Cada incidencia también sirve como punto de partida para una sesión de agente. Empezarás por la incidencia de filtrado después de hacer un primer cambio rápido.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar solo elementos de los repositorios añadidos a la aplicación Copilot. Para ver elementos de otros repositorios, añádelos a la aplicación.

## Prueba un chat rápido

Una buena forma de familiarizarte con la aplicación es usarla para aprender sobre la propia aplicación. Un **chat rápido** es justo lo que necesitas: permite hacer una pregunta o plantear ideas sin crear una rama ni un worktree, por lo que resulta ideal para una consulta rápida y puntual que no requiere una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat. Si aún no aparece **Chats**, selecciona **+** junto a **Sessions** para iniciar tu primer chat; después aparecerá la sección.
2. Pregunta a la aplicación cómo funcionan sus sesiones:

   ```plaintext
   ¿Cómo utiliza worktrees la aplicación de GitHub Copilot?
   ```

3. Lee la respuesta en la vista de conversación. Verás que cada sesión se ejecuta en su propio worktree de Git aislado, lo que permite ejecutar varios agentes en paralelo sin que sus cambios entren en conflicto. Puedes continuar la conversación o iniciar otra en cualquier momento.

## Resumen y siguientes pasos

Has instalado la aplicación de GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub.
- añadir un proyecto desde su repositorio de GitHub.
- conocer el espacio de trabajo y localizar la lista inicial de tareas pendientes en **Issues**.
- usar un chat rápido para hacer una pregunta breve y puntual.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] y la usarás para mostrar las valoraciones por estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación de GitHub Copilot][about-copilot-app]
- [Primeros pasos con la aplicación de GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación de GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
