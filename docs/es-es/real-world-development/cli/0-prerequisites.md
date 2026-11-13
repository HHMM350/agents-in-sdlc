---
title: "Lección 0: requisitos previos"
description: "Crea una copia propia de Tailspin Toys y prepara un GitHub Codespace para el taller de Copilot CLI."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Antes de empezar las lecciones de Copilot CLI, prepara todo lo necesario. Crearás una copia propia del repositorio de Tailspin Toys y pondrás en marcha un [codespace][codespaces]. En el siguiente ejercicio usarás su terminal integrado para instalar y ejecutar Copilot CLI.

En esta lección:

- crearás una copia propia del proyecto Tailspin Toys a partir de la plantilla.
- crearás un codespace y confirmarás que el proyecto está listo.

## Configura el repositorio del laboratorio

Trabajarás con una copia propia del proyecto Tailspin Toys. Créala ahora a partir de la [plantilla del repositorio][tailspin-template]. El nuevo repositorio incluye todos los archivos necesarios para el laboratorio.

1. Abre una ventana nueva del navegador y visita la [plantilla de Tailspin Toys][tailspin-template].
2. Crea una copia propia del repositorio seleccionando **Use this template** y, después, **Create a new repository**.
3. Si participas en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. De lo contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.
4. Anota la ruta del repositorio que has creado (`organization-or-user-name/repository-name`), ya que la necesitarás más adelante en el taller.

> [!NOTE]
> Al crear el repositorio a partir de la plantilla, se generará automáticamente una lista de incidencias de GitHub. Trabajarás con ellas durante todo el taller; no tienes que crear ninguna.

Usa una copia nueva de la plantilla del taller. Incluye instrucciones del repositorio, código de la aplicación, pruebas, una skill `quality-checks` y las incidencias pendientes que usarás. Si usas una copia antigua, confirma con la persona que imparte el taller que contiene los archivos necesarios.

## Crea un codespace

A continuación, usarás un codespace para completar el taller.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que permite escribir, ejecutar y depurar código directamente en el navegador. Proporciona un editor completo con compatibilidad con varios lenguajes de programación, extensiones y herramientas.

1. Ve al repositorio que acabas de crear.
2. Selecciona **Code**.
3. Selecciona la pestaña **Codespaces** y, después, **Create codespace on main**.
4. Espera a que termine la configuración del codespace. La plantilla instalará las dependencias del proyecto, Playwright Chromium y la base de datos local.
5. Si aparece el mensaje **Do you trust the authors of the files in this folder?**, selecciona **Trust Folder & Continue**.
6. Abre un terminal en la raíz del repositorio e inicia la aplicación:

   ```bash
   npm run dev
   ```

7. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser** y confirma que se carga el sitio de Tailspin Toys.
8. Vuelve al terminal y detén el servidor de desarrollo con <kbd>Ctrl</kbd>+<kbd>C</kbd>.

## Resumen y siguientes pasos

Ya tienes el entorno preparado. En esta lección:

- has creado una copia propia del proyecto Tailspin Toys a partir de la plantilla.
- has creado un codespace y confirmado que el proyecto estaba listo.

A continuación, [instalarás GitHub Copilot CLI][next-lesson] en el codespace e iniciarás sesión con tu cuenta de GitHub.

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
