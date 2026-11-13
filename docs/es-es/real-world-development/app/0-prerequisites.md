---
title: "Lección 0: requisitos previos"
description: "Prepara el entorno para las lecciones de la aplicación de GitHub Copilot: instala Node.js para Tailspin Toys y crea una copia propia del repositorio a partir de la plantilla."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La aplicación de GitHub Copilot es una aplicación de escritorio que sirve de centro para Copilot y GitHub. Proporciona acceso rápido a incidencias y solicitudes de incorporación de cambios y permite desarrollar con GitHub Copilot. Durante este taller trabajarás localmente con la aplicación de Tailspin Toys, creada con Astro, mediante la aplicación de GitHub Copilot. Antes de empezar, comprueba que Node.js esté instalado localmente y, después, instala la aplicación Copilot.

En esta lección:

- instalarás Node.js para poder ejecutar las pruebas del proyecto en tu equipo.
- crearás una copia propia del proyecto Tailspin Toys a partir de la plantilla.

## Instala Node.js

En varias lecciones pedirás a un agente que implemente funciones y ejecute las pruebas de Tailspin Toys localmente. Para ello necesitas **[Node.js][nodejs]**, el único entorno de ejecución que requiere el proyecto. Instala la versión **LTS** actual.

La opción más sencilla en cualquier plataforma es el instalador oficial:

1. Abre un terminal en tu sistema operativo, como Windows Terminal, Terminal de macOS o el que uses habitualmente.
2. Ejecuta estos comandos para comprobar las versiones instaladas de Node.js y npm:

   ```shell
   node --version
   npm --version
   ```

3. Si ambos comandos funcionan y Node.js cumple los requisitos del README y de `package.json` del proyecto, puedes pasar a la sección siguiente.

> [!TIP]
> Solo tienes que completar estos pasos si no tienes Node instalado o necesitas actualizarlo.

4. Abre la [página de descargas de Node.js][node-download].
5. Descarga la versión **LTS** para tu sistema operativo.
6. Ejecuta el instalador y acepta las opciones predeterminadas. En Windows, deja seleccionada la opción **Add to PATH**.
7. Después de la instalación, abre un terminal nuevo.
8. Confirma la instalación en el nuevo terminal:

   ```bash
   node --version
   npm --version
   ```

9. Deberían aparecer las versiones instaladas de Node.js y npm.

> [!IMPORTANT]
> El agente de la aplicación Copilot también debe poder ejecutar `node --version` y `npm --version`. Que funcionen en el terminal habitual no garantiza que estén disponibles en la aplicación. Cierra completamente la aplicación y vuelve a abrirla después de instalar Node.js o cambiar `PATH`. Si alguno de los comandos sigue fallando en una sesión, sigue los [pasos para solucionar problemas del entorno de sesión][session-environment] antes de continuar.

> [!IMPORTANT]
> Cada worktree también necesita las dependencias del proyecto y Playwright Chromium para las comprobaciones E2E. Sigue el README del repositorio de Tailspin Toys al preparar un worktree y revisa cualquier solicitud de instalación antes de aprobarla.

## Configura el repositorio del laboratorio

Trabajarás con una copia propia del proyecto Tailspin Toys. Créala ahora a partir del [repositorio de plantilla][template-repository]. El nuevo repositorio incluye todos los archivos del laboratorio y lo conectarás al instalar la aplicación.

1. Abre una ventana nueva del navegador y visita el repositorio de GitHub del laboratorio: `https://github.com/github-samples/tailspin-toys`.
2. Crea una copia propia del repositorio seleccionando **Use this template** en la página del repositorio del laboratorio. Después, selecciona **Create a new repository**.

   ![Botón Use this template con Create a new repository seleccionado en el menú desplegable](../../../_images/app-0-use-template.png)

3. Si participas en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. De lo contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.

   ![Formulario Create a new repository con github-samples/tailspin-toys como plantilla y el nombre del repositorio cumplimentado](../../../_images/app-0-create-repository.png)

4. Anota la ruta del repositorio que has creado (**organization-or-user-name/repository-name**), ya que la necesitarás más adelante en el laboratorio.

> [!NOTE]
> Al crear el repositorio a partir de la plantilla, se generará automáticamente una lista de incidencias de GitHub. Trabajarás con ellas durante todo el taller; no tienes que crear ninguna.

Usa una copia nueva de la plantilla del taller. Incluye instrucciones del repositorio, código de la aplicación, pruebas, una skill `quality-checks` y una extensión de Canvas existente. Durante el taller personalizarás la skill y crearás un agente de QA. Si usas una copia antigua, confirma con la persona que imparte el taller que contiene los archivos necesarios.

## Resumen y siguientes pasos

Ya tienes el entorno preparado. En esta lección:

- has instalado Node.js para poder compilar y probar el proyecto en tu equipo.
- has creado una copia propia del repositorio de Tailspin Toys a partir de la plantilla.

A continuación, [instalarás la aplicación de GitHub Copilot][next-lesson], conectarás el repositorio que acabas de crear y conocerás el espacio de trabajo.

## Recursos

- [Descargar Node.js][node-download]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Acerca de la aplicación de GitHub Copilot][about-copilot-app]

[next-lesson]: ../1-install-copilot-app/
[nodejs]: https://nodejs.org/
[node-download]: https://nodejs.org/en/download
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[session-environment]: ../3-agent-modes/#inicia-una-sesión-desde-la-incidencia
