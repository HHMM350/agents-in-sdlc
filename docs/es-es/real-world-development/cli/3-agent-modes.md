---
title: "Lección 3: modos de agente, Plan y Autopilot"
description: "Usa Plan para acordar un enfoque, Autopilot para crear el filtrado a partir de una incidencia e Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Empezamos por añadir una pequeña funcionalidad al proyecto, pero los cambios más amplios requieren un proceso más sólido. Por suerte, GitHub Copilot CLI está diseñado para adaptarse al flujo de trabajo de una organización y ayudarnos a crear lo adecuado de la manera correcta. Esta es la primera de varias lecciones en las que seguirás un proceso habitual de desarrollo con agentes: partirás de una incidencia para crear una funcionalidad, comprobarás que el código es válido y que funciona como se espera y, finalmente, la fusionarás en el proyecto.

> [!NOTE]
> Seguirás trabajando en la misma conversación y rama durante todo el flujo de la funcionalidad. Lo habitual sería usar ramas o solicitudes de incorporación de cambios distintas para diferentes tipos de archivo, pero haremos una excepción para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una conversación de Copilot desde una incidencia de GitHub.
- definirás los requisitos en modo Plan.
- implementarás la funcionalidad en modo Autopilot.
- revisarás el código.
- validarás la funcionalidad manualmente en un navegador de Codespaces.

Mientras sigues trabajando en esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la skill `quality-checks` existente, añadirás validación con MCP, crearás un agente de QA y abrirás una solicitud de incorporación de cambios.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar los juegos por categoría y editor. La incidencia del trabajo pendiente describe la funcionalidad, pero hay que acordar algunos detalles antes de programar, como la combinación de categorías. Usarás el modo Plan para resolver esas decisiones y después autorizarás una implementación acotada con Autopilot.

## Contexto

Incorporar agentes de programación con IA a tu flujo de desarrollo no cambia los fundamentos. ¡De hecho, los hace aún más importantes! La mayoría de los desarrolladores siguen un proceso parecido a este:

1. Parten de una incidencia registrada que describe el trabajo necesario.
2. Crean un plan de lo que hay que desarrollar.
3. Desarrollan y revisan el código.
4. Ejecutan pruebas para validar el código.
5. Validan manualmente la nueva funcionalidad.
6. Crean una solicitud de incorporación de cambios (PR).
7. Cuando se ha revisado el código y se ha completado correctamente la integración continua, fusionan el código.

> [!NOTE]
> Los detalles concretos dependen del equipo y de la organización, pero la mayoría de los flujos de trabajo siguen alguna variante del proceso anterior.

Seguir este enfoque habitual ayuda a garantizar que el código generado por IA cumpla los requisitos establecidos y pase por el mismo proceso de revisión que el código escrito manualmente.

## Modos de conversación

El **modo de conversación** controla la autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre los modos:

- **Interactive**: trabajas con el agente. Este sugiere cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan y no puede editar archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma: escribe código, ejecuta pruebas y repite el proceso hasta completar la tarea.

Empieza en modo Plan, revisa el plan y después usa Autopilot para implementarlo.

## Parte de la incidencia

Antes de empezar a trabajar en el filtrado, vuelve a tu Codespace y comprueba que el repositorio y el terminal estén preparados.

1. Vuelve a tu Codespace. Si está detenido, reinícialo antes de continuar.
2. Confirma que se ha fusionado la solicitud de incorporación de cambios de la valoración por estrellas.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para trabajar en el filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Usa las teclas de flecha para resaltar la incidencia titulada **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al mensaje y volver a la pestaña **Session**.

Observa que el mensaje ahora empieza por `#7` (o un número parecido). El carácter `#` permite añadir al contexto una incidencia o una solicitud de incorporación de cambios (PR) de GitHub.

## Planifica la funcionalidad de filtrado

La planificación te permite definir cómo implementar una funcionalidad o realizar una tarea antes de delegarla en Copilot. Para cualquier trabajo complejo, conviene dedicar un rato a planificar. Vamos a cambiar al modo Plan y pedir a Copilot que cree el plan.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Plan. Confirma que el indicador debajo del mensaje muestra **Plan**.
2. Después de la referencia a la incidencia que has añadido en el paso anterior, escribe este mensaje:

   ```plaintext
   Crea un plan para implementar esta funcionalidad.
   ```

Copilot empezará a preparar el plan. Primero explorará el proyecto y luego determinará el mejor enfoque.

3. Es posible que Copilot te pregunte cómo debería funcionar el filtrado. Responde según tus preferencias. ¡No hay respuestas incorrectas!
4. Cuando el plan esté listo, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para ampliarlo.
5. Desplázate por el plan para revisarlo.
6. Pide a Copilot que revise cualquier parte que no coincida con tus decisiones.

## Aprueba Autopilot

Una vez redactado y revisado el plan, ha llegado el momento de implementarlo. Deja que Copilot trabaje en la tarea con el modo Autopilot.

Autopilot permite que Copilot trabaje en el problema hasta que considere que lo ha resuelto.

1. Selecciona **Accept plan and build on autopilot (recommended)**, o la opción equivalente de tu versión.
2. Confirma que el indicador debajo del mensaje muestra **Autopilot**.
3. Observa cómo Copilot sigue el plan acordado, genera el código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación de inmediato, así que revisa primero el plan. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar por completas las comprobaciones.

## Revisa y verifica la implementación

Una vez generado el código, hay que revisarlo antes de fusionarlo, igual que cualquier otro código. Revisaremos el código y ejecutaremos el sitio para comprobar que todo funciona.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar en el modo Interactive. Confirma que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Escribe `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones que has tomado durante la planificación.
4. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa los resultados de las comprobaciones del proyecto y pide a Copilot que resuelva los errores.

## Explora la nueva funcionalidad

De acuerdo, el código parece correcto, pero ¿se ejecuta? Vamos a iniciar la aplicación como antes y abrir el sitio mediante el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Inicia la aplicación para que pueda probar en el navegador la funcionalidad de filtrado. Dime la URL y deja el servidor en ejecución.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros por categoría y editor, así como las combinaciones acordadas en el plan.
4. Confirma que las opciones para restablecer los filtros y los resultados vacíos coinciden con la incidencia y tus decisiones.
5. Vuelve a tu Codespace y pide a Copilot que detenga el servidor de desarrollo que ha iniciado.

## Resumen y siguientes pasos

Has usado distintos modos de conversación para crear y revisar una funcionalidad. En esta lección:

- has iniciado una conversación de Copilot desde una incidencia de GitHub.
- has definido los requisitos en modo Plan.
- has implementado la funcionalidad en modo Autopilot.
- has revisado el código.
- has validado la funcionalidad manualmente en un navegador de Codespaces.

A continuación, veremos con más detalle cómo generar código para que siga las prácticas documentadas mediante [instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
