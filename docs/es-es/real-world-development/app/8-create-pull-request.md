---
title: "Lección 8: crea y fusiona la solicitud de la funcionalidad"
description: "Revisa juntos el filtrado, las instrucciones, la actualización de la skill, el perfil de QA y las pruebas; después, crea una solicitud y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación del filtrado, las actualizaciones de instrucciones y de la skill, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Es el momento de revisarlos juntos y abrir una solicitud de incorporación de cambios. Fusionaste tú la solicitud de incorporación de cambios (PR) de la valoración por estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo normal sería separar la función, las actualizaciones de instrucciones y de la skill y el agente de QA en varias solicitudes. Para agilizar el taller, has mantenido todo el flujo de filtrado y calidad en una sesión y una rama, y lo incluirás en esta solicitud.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud.
- inspeccionarás toda la solicitud de la función y las pruebas de verificación.
- autorizarás Agent Merge solo después de revisar los cambios y confirmarás que la solicitud se ha fusionado.

## Escenario

Durante el flujo de trabajo de filtrado, has usado Copilot para planificar, implementar y verificar una función. Tailspin Toys quiere automatizar el trabajo restante de la solicitud, pero mantener bajo el control del desarrollador la autorización para fusionarla.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de incorporación de cambios mediante la aplicación de GitHub Copilot. Al activarlo, la sesión de la aplicación lee la solicitud y resuelve sus bloqueos: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y actualiza la base cuando hace falta. Después la fusiona en cuanto GitHub lo permite. Se ejecuta en segundo plano, continúa aunque se reinicie la aplicación y se desactiva cuando la solicitud se fusiona.

Hasta ahora has seleccionado tú **Merge pull request**. Agent Merge puede encargarse de esa responsabilidad, pero sigue necesitando tu autorización explícita para editar código y fusionarlo. Revisa las acciones permitidas y el trabajo antes de conceder permiso para fusionar.

## Usa Agent Merge para gestionar la solicitud

Ya has creado y revisado todo el código. Vamos a dejar que Agent Merge gestione el proceso de la solicitud.

1. Usa el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El botón cambiará a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Elegir la opción del menú desplegable no lo inicia por sí solo.

Agent Merge empezará a trabajar. Hará lo siguiente:

- Creará la solicitud de incorporación de cambios con un título y una descripción.
- Si la sesión se inició desde una incidencia, la mencionará en el cuerpo de la descripción.
- Actualizará la base o resolverá posibles conflictos con la rama de destino.
- Supervisará el proceso de CI para comprobar que se superen todas las verificaciones.
- Supervisará los comentarios de otros desarrolladores y de la revisión de código de Copilot, y hará cambios para resolverlos.
- De forma opcional, fusionará automáticamente la solicitud cuando todo se haya completado correctamente.

Vamos a dejar que Agent Merge fusione también la solicitud cuando se superen todas las comprobaciones.

5. Revisa las diferencias de la solicitud y las pruebas de verificación antes de conceder permiso para fusionar.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que esté marcada la opción **Merge pull request**.
8. Pide explícitamente al agente que fusione la solicitud:

   ```plaintext
   Fusiona la solicitud cuando se superen todas las comprobaciones y aprobaciones obligatorias. No eludas las protecciones del repositorio.
   ```

9. Supervisa el progreso y resuelve los bloqueos que indique. Antes de continuar, confirma que el estado de la solicitud sea **Merged**; tener habilitado el permiso de fusión o un agente en ejecución no confirma que se haya completado.

> [!IMPORTANT]
> Agent Merge no elude las protecciones del repositorio ni los permisos que falten. Resuelve esos bloqueos antes de continuar.

## Resumen y siguientes pasos

Has automatizado varias partes del proceso de desarrollo: la generación de código, las pruebas y la validación, y ahora el proceso de solicitud de incorporación de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud.
- has inspeccionado toda la solicitud de la función y las pruebas de verificación.
- has autorizado Agent Merge solo después de revisar los cambios y has confirmado que la solicitud se ha fusionado.

A continuación, [usarás un lienzo existente y crearás uno de clasificación][next-lesson] para explorar una forma más completa de examinar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Administrar incidencias y solicitudes de incorporación de cambios con la aplicación de GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación de GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
