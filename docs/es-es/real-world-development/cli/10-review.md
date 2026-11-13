---
title: "Lección 10: resumen y siguientes pasos"
description: "Repasa el flujo de trabajo con Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has usado GitHub Copilot CLI a lo largo de un flujo de trabajo completo en Tailspin Toys. En este taller:

- has preparado un Codespace, instalado Copilot CLI, explorado el proyecto y encontrado la incidencia de filtrado inicial.
- has añadido las valoraciones por estrellas, revisado el resultado en un navegador de Codespaces y fusionado manualmente tu primera solicitud de incorporación de cambios (PR).
- has partido de la incidencia de filtrado, definido el enfoque en modo Plan, implementado la funcionalidad en modo Autopilot y revisado el resultado en modo Interactive.
- has guiado al agente con instrucciones personalizadas, adaptado la skill `quality-checks` existente y la has usado para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- has añadido el servidor Model Context Protocol (MCP) de Playwright y lo has usado para explorar el filtrado en un navegador real.
- has creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la skill y las pruebas del navegador.
- has revisado todos los cambios del filtrado y autorizado Agent Merge para esa solicitud.
- has explorado comandos de barra para gestionar el contexto y los modelos, compartir sesiones y delegar tareas opcionalmente en la nube.

## Lo que has publicado

El taller incluye dos hitos de solicitud de incorporación de cambios, cada uno en su propia rama basada en `main` actualizado:

1. **Valoraciones por estrellas:** mostrar el valor de `starRating` existente y un estado explícito para los juegos sin valorar en sus tarjetas.
2. **Filtrado y flujo de trabajo de calidad:** implementar el filtrado, actualizar las instrucciones y aplicarlas a la funcionalidad, adaptar el informe de `quality-checks`, crear un perfil de QA e incluir las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su solicitud, has usado la misma conversación y rama. Hemos agrupado el trabajo en una solicitud para agilizar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias formas: con pruebas automatizadas, inspeccionándolo en el navegador y pidiendo a Copilot que lo explorara con MCP. La skill `quality-checks` ha ejecutado pruebas unitarias, lint y comprobaciones de tipos, y ha generado un informe con el formato nuevo. QA ha reunido esos resultados con una revisión de los requisitos y de la cobertura antes de abrir la solicitud.

Las pruebas nuevas deben cubrir carencias reales; una ejecución de QA que no necesite pruebas nuevas también puede ser correcta. Revisa el código y las pruebas antes de autorizar la fusión, y actualiza las pruebas afectadas después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas a Copilot determinan su trabajo. En este taller, has actualizado instrucciones, adaptado una skill, creado un perfil de QA y configurado un servidor MCP. Reutiliza estas personalizaciones en distintas conversaciones y ajústalas a las necesidades del equipo. Las instrucciones establecen normas, las skills describen tareas repetibles, los agentes personalizados definen funciones especializadas y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Usa **Plan** para analizar el enfoque antes de implementar, **Interactive** para seguir de cerca cambios concretos y **Autopilot** para tareas bien acotadas. Elige un modelo más rápido para ediciones rutinarias y uno más capaz para tareas complejas.

El contexto sigue siendo tan importante como la infraestructura. Describir con claridad *qué* quieres crear, *por qué* y *cómo* influye mucho en el resultado.

## Más funciones para explorar

Ya has recorrido el flujo de trabajo principal. Estas funciones de la CLI también pueden resultarte útiles:

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para explicar un problema y obtener otra perspectiva.
- `/fleet` para coordinar subtareas independientes en paralelo.
- `/worktree` para aislar una tarea aparte.
- `/delegate` para enviar una tarea a Copilot cloud agent.

## Siguientes pasos

La mejor forma de mejorar con cualquier herramienta es seguir usándola. Úsala con código de producción, proyectos personales o esa pequeña aplicación que llevas años queriendo crear. Comparte lo que aprendas con el equipo y aprende de sus experiencias. Y, como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación de GitHub Copilot][app] o el [taller de Copilot cloud agent][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalización de Copilot CLI][customize-cli]
- [Administración de solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
