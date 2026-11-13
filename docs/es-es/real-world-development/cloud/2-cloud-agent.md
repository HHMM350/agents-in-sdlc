---
title: "Ejercicio 2: GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: instrucciones personalizadas][previous-lesson] |
|:--|

Probablemente haya pocas organizaciones, si es que hay alguna, que no tengan problemas con la deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidad relegadas en la lista de tareas por falta de tiempo. GitHub Copilot cloud agent está diseñado para realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, genera un borrador de solicitud de incorporación de cambios para que lo revise una persona. Así puedes delegar tareas tediosas, acelerar el desarrollo y centrarte en cuestiones de mayor alcance.

Con Copilot cloud agent explorarás:

- cómo personalizar el entorno de generación de código.
- cómo garantizar que las operaciones se realicen de forma segura.
- la importancia de delimitar claramente las incidencias.
- cómo asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica que quiere resolver. Los contratistas que crearon la primera versión del sitio dejaron la documentación en mal estado: comprobarás que no hay documentación. El primer paso será añadir comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere mejorar el descubrimiento de juegos. Quiere mostrar juegos relacionados en la página de detalles de cada juego; es decir, otros títulos de la misma categoría, para que los visitantes puedan seguir explorando. No necesitan una implementación pulida: solo quieren algo con lo que probar y aceptar la experiencia de usuario. Aunque esta tarea bloquea otros trabajos, ahora hay incidencias de mayor prioridad.

Son ejemplos de tareas que pueden quedar relegadas y que resulta útil asignar a Copilot cloud agent. El agente puede trabajar en ellas de forma asíncrona mientras tú te ocupas de otras tareas, para que después revises su trabajo y confirmes que todo está como esperabas.

## Presentación de GitHub Copilot cloud agent

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma parecida a un desarrollador. Igual que con una persona, puedes asignarle trabajo de varias maneras, por ejemplo, [asignándole una incidencia de GitHub](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Cuando se la asignas, Copilot crea un borrador de solicitud de incorporación de cambios para registrar el progreso, configura un entorno y empieza a trabajar. Puedes consultar la sesión de Copilot mientras sigue en curso o una vez completada. Cuando la solución esté lista para que la revises, te mencionará en la solicitud.

## La importancia de acotar bien las instrucciones

GitHub Copilot no hace magia: no puedes saltarte el análisis. Incluso las operaciones que parecen sencillas pueden ser complejas si se examinan de cerca, así que [define cuidadosamente el alcance de las tareas para Copilot cloud agent][cloud-agent-best-practices]. Trátalo como a un asistente de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir IA generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has visto cómo las instrucciones personalizadas guían a Copilot. Si ya has completado el ejercicio sobre instrucciones personalizadas, habrás visto cómo funciona `.github/copilot-instructions.md`; si no, este es un buen momento para echarle un vistazo. Antes de asignar trabajo a Copilot cloud agent, inspecciona en modo de solo lectura los archivos de instrucciones que incluye el repositorio para poder observar después su efecto.

Abre estos archivos en la interfaz web de GitHub o en un codespace que ya tengas en ejecución:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, en especial las convenciones de TypeScript y los requisitos de comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en el frontmatter `applyTo`, que limita estas instrucciones a los archivos `**/*.test.ts`.

Cuando en la sección siguiente asignes a cloud agent la incidencia `Code lacks documentation`, fíjate en los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentario que aparecen en la solicitud resultante. Proceden de estos archivos de instrucciones. Volveremos a señalarlos cuando revises las solicitudes en un ejercicio posterior.

## Configura el entorno de desarrollo para Copilot cloud agent

La creación de código suele necesitar un entorno específico y algunos scripts de configuración, independientemente de quién realice el trabajo. Lo mismo ocurre cuando asignas tareas a Copilot, que trabaja de forma parecida a un ingeniero de software.

Cloud agent usa [GitHub Actions][github-actions] como entorno de trabajo. Puedes personalizarlo con un [flujo de configuración especial][setup-workflow], definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de empezar. Así podrá acceder a las herramientas y dependencias necesarias. Este flujo ya está configurado para agilizar el laboratorio y facilitar el ejercicio. Proporciona Node.js, las dependencias del proyecto, los navegadores para las pruebas de extremo a extremo y la base de datos SQLite migrada y precargada para la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Asigna a estos pasos solo los permisos mínimos necesarios. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si en los pasos de configuración clonas el repositorio, por ejemplo, para instalar dependencias, necesitas el permiso `contents: read`. Si no lo clonas, Copilot lo hará automáticamente cuando terminen los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de la interfaz y la aplicación: Node.js (ahora toda la aplicación usa Astro y Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y precarga la base de datos SQLite local para que las compilaciones y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier flujo de trabajo de GitHub, pero tiene algunos aspectos importantes:

- Incluye un único trabajo llamado `copilot-setup-steps`. Se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la solicitud de incorporación de cambios.
- El activador `workflow_dispatch` permite ejecutar manualmente el flujo de trabajo desde la pestaña **Actions** del repositorio. Esto sirve para comprobar que se ejecuta correctamente sin esperar a que Copilot lo inicie.

## Añade documentación

Aunque todos reconocen la importancia de la documentación, muchos proyectos tienen información obsoleta o carecen de ella. Esta deuda técnica suele quedar desatendida, lo que reduce la productividad y dificulta mantener el código o incorporar a nuevos desarrolladores. Copilot destaca en la generación de documentación, así que esta es una incidencia ideal para asignarle. Trabajará en segundo plano y generará la documentación necesaria. En un ejercicio futuro volverás para revisarla.

1. Abre una pestaña nueva del navegador y visita tu repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el formulario de una incidencia nueva.
4. Selecciona **Blank issue**.
5. Escribe `Code lacks documentation` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   Nuestra organización exige que las funciones y los métodos incluyan comentarios TSDoc cuando resulte útil. Por desgracia, las actualizaciones recientes no han seguido este estándar. Hay que actualizar el código existente y añadir comentarios de documentación cuando ayuden a aclarar el comportamiento.
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el diálogo de asignación.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la solicitud de incorporación de cambios (PR) que acaba de generarse, cuyo título será parecido a `[WIP]: Code lacks documentation`. Si aún no aparece en la lista, espera un momento y actualiza la ventana del navegador.
12. Al cabo de unos minutos, Copilot debería haber creado una lista de tareas.

> [!NOTE]
> La lista de tareas de Copilot puede tardar varios minutos en aparecer en la solicitud. Copilot está preparando su entorno (ejecuta el flujo de trabajo anterior), analiza el proyecto y determina la mejor forma de abordar el problema.

13. Revisa la lista y las tareas que va a completar.
14. Desplázate por la cronología de la solicitud y busca una actualización que indique que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona **View session**.

   ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la ventana para ver el indicador actualizado.

16. Observa la sesión en directo y cómo Copilot resuelve el problema: explora el código y comprende su estado, se detiene a analizar y decidir el plan adecuado, y crea código.

El proceso tardará varios minutos. Uno de los objetivos principales de Copilot cloud agent es realizar tareas de forma asíncrona para que puedas centrarte en otros asuntos. Aprovecharemos esa función asignándole otra tarea y, mientras tanto, nos ocuparemos de añadir funcionalidades a la aplicación.

## Añade una sección de juegos relacionados a la página de detalles

Una de las ventajas de GitHub Copilot cloud agent es que permite repartir el trabajo para que tú te ocupes de unas tareas mientras el agente hace otras. Añadir una sección de juegos relacionados para el equipo de diseño quizá no lleve mucho tiempo, pero podrías dedicar ese tiempo a otras tareas. Vamos a asignársela al agente.

1. Vuelve a tu repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el formulario de una incidencia nueva.
4. Selecciona **Blank issue** para usar la plantilla en blanco.
5. Escribe `Show related games on the game details page` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

   ```markdown
   Queremos ayudar a descubrir más juegos mostrando juegos relacionados en la página de detalles de cada juego. El equipo de diseño quiere explorar la experiencia de usuario y hacer pruebas de aceptación. Estos son los requisitos:

   - Añadir un método auxiliar de acceso a datos en `src/lib/` que devuelva otros juegos de la misma categoría que un juego determinado, sin incluir ese juego
   - Mostrar en la página de detalles una sección «Juegos relacionados» que use el método auxiliar
   - Gestionar el caso en que un juego no tenga juegos relacionados
   - Añadir pruebas unitarias para el nuevo método auxiliar
   - Antes de crear la solicitud de incorporación de cambios, confirmar que se superan todas las pruebas
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el diálogo de asignación.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Poco después, aparecerán varios 👀 en el primer comentario de la incidencia para indicar que Copilot ya está trabajando.

![Copilot usa el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot ya está trabajando en la segunda solicitud. Copilot cloud agent funciona de forma parecida a un ingeniero de software: no hace falta que lo supervises continuamente, puedes revisar el resultado cuando termine. Ahora veremos cómo crear y usar agentes personalizados.

## Resumen y siguientes pasos

En esta lección has explorado [GitHub Copilot cloud agent][copilot-agents]. Puedes asignar incidencias a cloud agent para que las resuelva de forma asíncrona. Copilot puede ayudarte con deuda técnica, nuevas funcionalidades o la migración de código entre marcos de trabajo.

Has explorado estos conceptos:

- cómo personalizar el entorno de generación de código.
- cómo garantizar que las operaciones se realicen de forma segura.
- la importancia de delimitar claramente las incidencias.
- cómo asignar incidencias a Copilot.

Mientras cloud agent trabaja en segundo plano, puedes empezar a crear y usar agentes personalizados. [Copilot cloud agent también puede usar servidores MCP][cloud-agent-mcp] y puede acceder a las instrucciones personalizadas que hemos visto en módulos anteriores.

## Recursos

- [Acerca de Copilot cloud agent][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración de Copilot cloud agent][cloud-agent-best-practices]

| [Siguiente lección: agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
