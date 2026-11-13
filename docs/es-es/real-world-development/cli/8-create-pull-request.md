---
title: "Lección 8: crea y fusiona la solicitud de incorporación de cambios"
description: "Revisa juntos el filtrado, las instrucciones, la actualización de la skill, el perfil de QA y las pruebas; después, crea una solicitud de incorporación de cambios y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las instrucciones, la actualización de la skill, el perfil de control de calidad (QA) y las pruebas están guardados en una misma rama. Es el momento de revisarlos juntos y abrir una solicitud de incorporación de cambios. Fusionaste tú la solicitud de incorporación de cambios (PR) de la valoración por estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo normal sería dividir la funcionalidad, las actualizaciones de instrucciones, la actualización de la skill y el agente de QA en varias solicitudes de incorporación de cambios. Para agilizar el taller, has mantenido todo el flujo de filtrado y calidad en una conversación y una rama, y lo incluirás en esta solicitud.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud de incorporación de cambios.
- inspeccionarás todos los cambios de la funcionalidad y las pruebas que los respaldan.
- crearás la solicitud de incorporación de cambios del filtrado.
- activarás Agent Merge solo después de revisar los cambios y confirmarás que la solicitud se ha fusionado.

## Escenario

Durante el flujo de trabajo de filtrado, has usado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere ahora automatizar el trabajo restante de la solicitud, pero mantener bajo el control del desarrollador la autorización para fusionarla.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de incorporación de cambios. Al activarlo, Copilot resuelve los bloqueos de la solicitud: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y vuelve a basar los cambios cuando es necesario. Después, habilita la fusión automática de GitHub si la configuración del repositorio lo permite.

Hasta ahora has seleccionado tú **Merge pull request**. Agent Merge puede encargarse de esa responsabilidad. Revisa el trabajo y decide si está listo antes de activarlo.

## Usa Agent Merge para gestionar la solicitud

Ya has creado todo el código. Vamos a revisarlo, crear la solicitud y dejar que Agent Merge gestione el resto del proceso.

1. Vuelve a tu Codespace.
2. Abre el diálogo de agentes con `/agent`.
3. Selecciona **Default** en la lista de opciones y pulsa <kbd>Enter</kbd>.
4. Crea una solicitud con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la solicitud. Cuando todo se complete correctamente, la fusionará.
7. Comprueba que Copilot muestra un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no elude las aprobaciones obligatorias, la protección de ramas, las colas de fusión, la configuración del repositorio ni los permisos que falten. Si se bloquea, lee el motivo y completa manualmente la fusión revisada cuando el repositorio lo permita.

## Resumen y siguientes pasos

Has automatizado varias partes del proceso de desarrollo: la generación de código, las pruebas y la validación, y ahora el proceso de solicitud de incorporación de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud.
- has inspeccionado todos los cambios de la funcionalidad y las pruebas que los respaldan.
- has creado la solicitud de incorporación de cambios del filtrado.
- has activado Agent Merge solo después de revisar los cambios y has confirmado que la solicitud se ha fusionado.

A continuación, [explorarás otros comandos de barra de Copilot CLI][next-lesson] para gestionar el contexto y los modelos, compartir sesiones y delegar tareas opcionalmente en la nube.

## Recursos

- [Administrar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
