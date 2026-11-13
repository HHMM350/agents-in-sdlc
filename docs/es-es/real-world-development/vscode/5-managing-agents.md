---
title: "Ejercicio 5: supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: agentes personalizados][previous-lesson] |
|:--|

Cuando usas el modo de agente de GitHub Copilot, el agente trabaja de forma autónoma: explora el código, propone cambios, edita archivos y ejecuta comandos. Como trabaja en tu equipo y en tiempo real, Copilot Chat de VS Code muestra cada llamada a una herramienta y cada edición de archivo a medida que ocurren. Puedes revisar las diferencias en línea, aceptar o rechazar cambios concretos y orientar la conversación con mensajes de seguimiento para ajustar o ampliar el trabajo sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios de archivo propuestos.
- orientarás al agente durante la sesión para añadir un conmutador para el modo claro junto al de contraste alto.

## Escenario

El agente personalizado de accesibilidad que usaste en el [ejercicio 4][previous-lesson] está implementando el modo de contraste alto. Mientras trabaja, el equipo de diseño ha hecho una petición adicional: quiere que los usuarios también puedan activar un modo claro. En lugar de iniciar otra conversación desde cero, orientarás la sesión existente para ampliar el trabajo.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y los cambios que propone. Cada edición aparece en línea en el chat, con las diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver cada llamada a una herramienta. Verás lecturas y ediciones de archivos y los comandos de terminal que solicita ejecutar.
3. Cuando el agente proponga una edición, aparecerá una diferencia en línea:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertirlo y dejar que el agente vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed** de la parte superior del chat para ver todos los archivos modificados durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta solicita permiso (por ejemplo, para ejecutar un comando de terminal), el agente se detendrá y mostrará el mensaje **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que el agente termine de implementar el modo de contraste alto. Deberías ver un mensaje final que resuma los cambios realizados.

## Pide al agente que añada el modo claro

Ahora que ya está disponible el modo de contraste alto, ampliarás la misma conversación para añadir un conmutador para el modo claro. Como continuarás en la misma sesión, el agente conservará el contexto de su trabajo anterior, incluidos los componentes modificados, el enfoque de estilos y el patrón de almacenamiento local.

1. Envía este mensaje de seguimiento en Copilot Chat:

   ```plaintext
   ¡Buen trabajo! Ahora añade un conmutador para el modo claro junto al de contraste alto. El modo claro debe seguir el mismo patrón: guardar la preferencia en el almacenamiento local y estar disponible en la misma zona de la interfaz. El usuario debe poder activar de forma independiente el modo de contraste alto y el modo claro.
   ```

2. El agente continuará desde donde lo dejó, explorará los cambios realizados y propondrá los cambios necesarios para el modo claro.
3. Revisa cada cambio nuevo a medida que aparezca, como hiciste con el modo de contraste alto. Selecciona **Keep** o **Undo** en cada diferencia.
4. Si el agente sigue un enfoque que no quieres —por ejemplo, intenta reorganizar la interfaz de los conmutadores—, detenlo con el botón **Stop** junto al campo de mensaje y envíale una aclaración.

> [!TIP]
> Orientar una sesión en curso es más rápido que empezar de nuevo. Usa mensajes de seguimiento para pedir ajustes («simplifica el CSS y usa variables CSS en lugar de duplicar selectores»), corregir el enfoque («no añadas un tercer conmutador; integra el modo claro en el panel de configuración actual») o ampliar el alcance («añade también métodos abreviados de teclado para ambos conmutadores»).

## Revisa los cambios

Antes de confirmar el trabajo, revisa rápidamente todos los archivos que ha modificado el agente.

1. Abre la vista **Source Control** de VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en los componentes Astro, los estilos y las pruebas relacionadas.
3. Abre algunos archivos modificados y revisa las diferencias. Confirma que se aplican las pautas de accesibilidad del agente personalizado: atributos ARIA, navegación con el teclado, HTML semántico y persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios en el panel Source Control. Los publicarás en [la lección siguiente][next-lesson].

## Resumen y siguientes pasos

Has usado el modo de agente de Copilot Chat para supervisar y orientar una sesión en curso: has revisado cada edición al aparecer, aceptado o rechazado cambios y enviado mensajes de seguimiento para ampliar el trabajo sin perder el contexto.

En esta lección:

- has supervisado en tiempo real el trabajo de un agente.
- has aceptado o rechazado ediciones de archivos concretas.
- has orientado una sesión en curso con mensajes de seguimiento.

En la [lección siguiente][next-lesson] publicarás el trabajo de accesibilidad en una solicitud de incorporación de cambios y revisarás los cambios generados por el agente personalizado local durante el laboratorio.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Usar el modo de agente][agent-mode]

---

| [← Lección anterior: agentes personalizados][previous-lesson] | [Siguiente lección: iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
