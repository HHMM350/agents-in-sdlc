---
title: "Lección 3: modos de agente, Plan y Autopilot"
description: "Explora los modos de agente: usa Plan para acordar un enfoque, Autopilot para crear el filtrado a partir de una incidencia e Interactive para revisar y verificar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Empezamos por añadir una pequeña función al proyecto, pero los cambios más amplios requieren un proceso más sólido. Por suerte, la aplicación de GitHub Copilot está diseñada para adaptarse al flujo de trabajo de una organización y ayudarnos a crear lo adecuado de la manera correcta. Esta es la primera de varias lecciones en las que seguirás un proceso habitual de desarrollo con agentes: partirás de una incidencia para crear una función, comprobarás que el código es válido y que funciona como se espera y, finalmente, la fusionarás en el proyecto.

> [!NOTE]
> Seguirás trabajando en la misma sesión durante todo el flujo de la función. Normalmente se usarían sesiones o solicitudes distintas para tipos de archivo diferentes, pero tomaremos un atajo para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una sesión de agente desde una incidencia de GitHub.
- definirás los requisitos en modo **Plan**.
- implementarás la función en modo **Autopilot**.
- revisarás el código.
- validarás la función manualmente en un lienzo de navegador.

Mientras sigues trabajando en esta función, actualizarás las instrucciones del repositorio, personalizarás la skill `quality-checks` existente, añadirás validación con MCP, crearás un agente de QA y abrirás la solicitud de la función.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar los juegos por categoría y editor. La incidencia del trabajo pendiente describe la función, pero hay que acordar algunos detalles antes de programar, como la combinación de categorías. Usarás el modo Plan para resolver esas decisiones y después autorizarás una implementación acotada con Autopilot.

## Contexto

Incorporar agentes de programación con IA a tu flujo de desarrollo no cambia los fundamentos. ¡De hecho, los hace aún más importantes! La mayoría de los desarrolladores siguen un proceso parecido a este:

1. Abrir una incidencia registrada con los detalles del trabajo necesario.
2. Crear un plan de lo que hay que desarrollar.
3. Desarrollar y revisar el código.
4. Ejecutar pruebas para validar el código.
5. Validar manualmente la nueva función.
6. Crear una solicitud de incorporación de cambios (PR).
7. Cuando se haya revisado el código y se haya completado correctamente la integración continua, fusionarlo.

> [!NOTE]
> Los detalles concretos dependen del equipo y de la organización, pero la mayoría de los flujos de trabajo siguen alguna variante del proceso anterior.

Seguir este enfoque ayuda a garantizar que el código generado por IA cumpla los requisitos establecidos y pase por el mismo proceso de revisión que el código escrito manualmente.

## Modos de sesión

El **modo de sesión** controla la autonomía del agente. Puedes seleccionarlo en el menú desplegable que hay debajo del campo de mensaje y cambiarlo en cualquier momento:

- **Interactive**: trabajas con el agente. Sugiere cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan. Lo revisas y apruebas antes de que el agente lo ejecute.
- **Autopilot**: el agente trabaja de forma totalmente autónoma: escribe código, ejecuta pruebas e itera sin esperar indicaciones.

Empieza en modo Plan, revisa el plan y después usa Autopilot para implementarlo.

## Inicia una sesión desde la incidencia

Antes de empezar, confirma que se ha fusionado la solicitud de incorporación de cambios de la valoración por estrellas y que tu `main` local está actualizado.

1. En **Sessions**, selecciona la carpeta del repositorio Tailspin Toys y, después, **Issues** en la navegación superior del repositorio. Abre **Allow users to filter games by category and publisher**. Es una incidencia inicial que ya existe; no tienes que crear otra.
2. Selecciona **New session** y crea un **new working tree** basado en `main` actualizado.

   ![Vista de una incidencia en la aplicación de GitHub Copilot con una flecha que señala el botón New session](../../../_images/app-new-session-from-issue.png)

3. Confirma que la incidencia está adjunta a la sesión y selecciona **Plan** en el selector de modo.

> [!NOTE]
> Si no se encuentra Node.js o npm, pide al agente que ejecute `node --version` y `npm --version`. Si funcionan en el terminal, pero no en la sesión, comprueba la configuración de `PATH` o del administrador de versiones de la aplicación y ciérrala por completo antes de volver a abrirla. Repite la operación y las comprobaciones que hayan fallado; no reinstales npm solo porque el agente no lo encuentre.

## Planifica la función de filtrado

La planificación te permite revisar el enfoque antes de que Copilot escriba código. Como has iniciado la sesión desde la incidencia, Copilot ya tiene la solicitud como contexto. Envía:

```plaintext
Implementa esta función.
```

Responde a las preguntas de Copilot y compara el plan con los criterios de aceptación de la incidencia. Comprueba que incluye filtros por categoría y editor, controles accesibles, cambios en el acceso a los datos y pruebas. Aclara cualquier comportamiento poco definido, como cómo se combinan varias categorías o qué ocurre cuando no hay juegos que coincidan.

El plan debe incluir lint, pruebas unitarias, pruebas E2E y comprobaciones de tipos con las herramientas existentes del proyecto. Céntralo en implementar y probar el filtrado; crearás la solicitud después de completar el flujo de calidad. Pide cambios en el plan antes de aprobarlo y conserva la URL de la incidencia y las aclaraciones acordadas para validarlas más adelante.

## Aprueba Autopilot explícitamente

Cuando estés conforme con el plan, selecciona **Approve and implement this plan** o la opción equivalente de tu versión. Comprueba el modo activo en lugar de dar por hecho que la aprobación cambia de modo. Confirma que el indicador muestra **Autopilot**.

Copilot empezará a implementar la función. Verás cómo sigue el plan acordado, genera código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación de inmediato, así que revisa primero el plan. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar las comprobaciones por completas. Detén solo los servidores que hayas iniciado.

## Revisa y verifica la implementación

Una vez generado el código, hay que revisarlo antes de fusionarlo, igual que cualquier otro código. Vamos a revisar el código y ejecutar el sitio para comprobar que todo funciona.

1. Abre **Changes** e inspecciona la implementación del filtrado y las pruebas.
2. Compara el resultado con la incidencia y las aclaraciones aprobadas, incluidas las combinaciones de categorías y editores. Comprueba que los cambios siguen las instrucciones existentes del repositorio.
3. Revisa los resultados de lint, las pruebas unitarias, las pruebas E2E y las comprobaciones de tipos. Una comprobación omitida no cuenta como superada.
4. Resuelve los errores y vuelve a ejecutar las comprobaciones afectadas antes de aceptar la implementación. La configuración E2E de Playwright compila y sirve una vista previa, y puede reutilizar un servidor local. Asegúrate de que el servidor probado pertenece a este worktree, no a una lección anterior.

## Explora la nueva función

El código parece correcto, pero ¿se ejecuta? Vamos a iniciar la aplicación como antes y abrir el sitio en un lienzo de navegador.

1. Usa este mensaje para pedir a Copilot que inicie la aplicación y abra la página en el lienzo:

   ```plaintext
   Inicia la aplicación y ábrela en el lienzo de navegador.
   ```

2. En unos instantes, la aplicación se iniciará y se abrirá una ventana del navegador dentro de la aplicación de Copilot.
3. Selecciona una categoría y confirma que los resultados coinciden. Borra el filtro, selecciona un editor y comprueba que los resultados coinciden con él.
4. Combina los filtros de categoría y editor y compara los resultados con la incidencia y el plan aprobado. Si se admiten varias categorías, comprueba el comportamiento acordado.
5. Prueba una combinación sin resultados y comprueba el estado vacío. Borra o restablece los filtros y confirma que vuelve a aparecer toda la lista.
6. Cuando termines, pide a Copilot que detenga el servidor de desarrollo de esta sesión y cierre el lienzo:

   ```plaintext
   Detén el servidor de desarrollo y cierra el lienzo de navegador.
   ```

## Conserva esta sesión para las lecciones siguientes

Todavía no crees ni fusiones la solicitud de filtrado. Conserva esta sesión, este worktree y esta rama para las lecciones 4 a 8. En las siguientes aplicarás instrucciones personalizadas al código de filtrado y añadirás mejoras de skills y de QA antes de crear y fusionar la solicitud conjunta en la lección 8. Después de detener el servidor, puedes dejar la sesión inactiva y volver a ella para la próxima lección.

## Resumen y siguientes pasos

Has utilizado distintos modos de agente para crear y revisar una función. En esta lección:

- has iniciado una sesión de agente desde una incidencia de GitHub.
- has definido los requisitos en modo **Plan**.
- has implementado la función en modo **Autopilot**.
- has revisado el código.
- has validado la función manualmente en un lienzo de navegador.

A continuación, profundizarás en cómo se genera el código y te asegurarás de que siga las prácticas documentadas mediante [instrucciones personalizadas][next-lesson].

## Recursos

- [Trabajar con sesiones de agente en la aplicación de GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
