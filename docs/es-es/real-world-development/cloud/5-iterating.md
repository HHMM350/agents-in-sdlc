---
title: "Ejercicio 5: iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: administrar agentes][previous-lesson] |
|:--|

## Revisa el trabajo

Durante este laboratorio has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario y añadir funcionalidades. Le has pedido que añada documentación al código, cree una función de juegos relacionados para que el equipo de diseño pueda iterar y añada funciones de accesibilidad, como conmutadores para los modos de contraste alto y claro. Vamos a explorar los cambios y, si hace falta, proporcionar comentarios a Copilot para mejorar su trabajo.

### Escenario

Como ya hemos repetido varias veces, los fundamentos del diseño de software y DevOps no cambian al añadir IA generativa. Siempre hay que revisar el código generado y seguir el proceso habitual de DevOps. Con eso en mente, revisaremos las sugerencias de GitHub Copilot para crear la documentación, la función de juegos relacionados y las funciones de accesibilidad antes de habilitar la revisión para el resto del equipo.

## Seguridad y GitHub Copilot cloud agent

Como Copilot cloud agent trabaja de forma asíncrona y sin supervisión, se han establecido restricciones de seguridad para garantizar que todo se mantenga protegido. Entre ellas:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que usará para su código.
- Cloud agent se ejecuta en GitHub Actions y crea un entorno temporal e independiente para trabajar.
- Una persona debe aprobar cualquier flujo de trabajo de GitHub Actions antes de que pueda ejecutarse.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores MCP.

## Revisa la documentación generada

Empezaremos por la primera solicitud de incorporación de cambios (PR) que ha generado GitHub Copilot cloud agent: añadir documentación al código. Usarás la interfaz habitual de solicitudes de GitHub.com.

> [!NOTE]
> Al revisar la solicitud, puede que aparezca una advertencia que indica que el cortafuegos ha bloqueado GitHub Copilot. Es **normal**: Copilot tiene acceso limitado a recursos externos de forma predeterminada, incluidas las llamadas a servidores MCP externos. Si quieres, puedes [personalizar o deshabilitar el cortafuegos de Copilot cloud agent][agent-firewall].

1. Vuelve a tu repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes.
3. Abre la solicitud cuyo título sea parecido a **Add missing documentation**.

> [!NOTE]
> Si Copilot sigue trabajando, el título de la solicitud incluirá la etiqueta **[WIP]**. En ese caso, espera a que termine. Puede tardar unos minutos; puedes descansar o repasar lo aprendido hasta ahora.

4. Cuando la solicitud esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que incluirá los nuevos comentarios TSDoc y otra documentación. Los cambios concretos pueden variar.

   Al revisar los cambios, busca comentarios TSDoc, convenciones de TypeScript y encabezados de comentario. Proceden de los archivos de instrucciones personalizadas que revisaste al principio del ejercicio 2.

6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que avisa de que algunos flujos de trabajo esperan aprobación.
8. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto deberían superarse para la aplicación Astro. Puede tardar unos minutos.

## Pide cambios a GitHub Copilot

Trabajar con Copilot en una solicitud no es un proceso unidireccional. Puedes mencionarlo en comentarios de la solicitud, igual que harías con otra persona del equipo, o añadir comentarios en línea en el código. Copilot verá esos comentarios e iniciará otra sesión para resolverlos. Como los resultados no son deterministas, no podemos recomendar un texto exacto. Algunas ideas de cambios que puedes pedirle:

- Añadir encabezados de comentario al principio de cada archivo de código con una descripción breve de su contenido.
- Añadir comentarios TSDoc a archivos TypeScript y Astro.
- Crear un archivo README que describa la estructura de la aplicación Astro.

1. Añade un comentario para solicitar un cambio en la documentación generada y menciona a **@copilot**, como harías con cualquier persona. Usa alguna de las ideas anteriores u otra sugerencia para la documentación del código.
2. Selecciona **View Session** para observar cómo trabaja Copilot. Fíjate en que inicia una sesión nueva para realizar las actualizaciones.
3. Puedes seleccionar **Back to pull request** para volver a la solicitud.

   ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine los cambios, aparecerá un commit nuevo en la solicitud.
5. Selecciona la pestaña **Files changed** para revisar los cambios.

Sigue iterando hasta que estés conforme. Cuando lo estés, puedes marcar la solicitud como lista para revisión y fusionarla en la rama principal.

![Marca la solicitud como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la función de juegos relacionados

Volvamos a la solicitud que Copilot ha generado para resolver la incidencia sobre los juegos relacionados en la página de detalles.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud cuyo título sea parecido a **Show related games on the game details page**.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado los cambios y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Deberías ver un indicador que avisa de que algunos flujos de trabajo esperan aprobación.
7. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto deberían superarse para la aplicación Astro. Puede tardar unos minutos.
9. **Opcional:** también puedes cambiar a esta rama en tu Codespace para probar manualmente la función de juegos relacionados. Ve al Codespace, abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por el nombre de la rama que haya creado Copilot, por ejemplo, **copilot/fix-8**:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot ha creado la función de juegos relacionados. Al igual que antes, puedes trabajar de forma iterativa con Copilot cloud agent para solicitar cambios. Por ejemplo, puedes pedirle que modifique cuántos juegos relacionados se muestran o que añada encabezados de comentario y comentarios TSDoc. Recuerda que esta solicitud se asignó **antes** de actualizar las instrucciones personalizadas. Como en la solicitud anterior, puedes añadir estas peticiones como comentarios en la pestaña **Conversation**; Copilot las verá e iniciará una sesión nueva.

## Revisa las funciones de accesibilidad

Por último, revisaremos las funciones de accesibilidad implementadas con el agente personalizado de accesibilidad. Esta solicitud debería incluir el modo de contraste alto que asignaste en el ejercicio 3 y el modo claro que pediste desde el panel de agentes en el ejercicio 4.

1. Vuelve a tu repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la solicitud cuyo título sea parecido a **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot sigue trabajando, el título de la solicitud incluirá la etiqueta **[WIP]**. En ese caso, espera a que termine. Puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código que ha generado.
5. Revisa la implementación y presta atención a:
   - los componentes de interfaz para alternar entre modos.
   - el uso del almacenamiento local para guardar las preferencias.
   - los cambios de CSS o de estilos para los modos de contraste alto y claro.
   - los atributos de accesibilidad, como las etiquetas ARIA y la navegación con el teclado.
   - el código JavaScript/TypeScript que controla el cambio de modo.

6. Cuando hayas revisado las actualizaciones y todo parezca correcto, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que avisa de que algunos flujos de trabajo esperan aprobación.
8. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Los flujos de trabajo deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto deberían superarse para la aplicación Astro. Puede tardar unos minutos.
10. **Opcional:** puedes cambiar a esta rama en tu Codespace para probar manualmente las funciones de accesibilidad. Ve al Codespace, abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por el nombre de la rama que haya creado Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Después, inicia la aplicación y prueba los conmutadores de contraste alto y modo claro en el navegador. Confirma que funcionan como se espera y que las preferencias se conservan al volver a cargar la página.

Fíjate en cómo el agente personalizado de accesibilidad ha ayudado a Copilot a implementar estas funciones siguiendo las prácticas recomendadas de accesibilidad. Si detectas problemas o posibles mejoras, puedes mencionarlo en un comentario con **@copilot** y pedirle que actualice los cambios, como hiciste con las solicitudes anteriores.

## Ejercicio opcional: sigue delegando

Cloud agent resulta especialmente útil cuando puedes asignarle tareas reales de la lista de pendientes y ocuparte de otra cosa. Para practicarlo, crea algunas incidencias más en el repositorio y asígnaselas a Copilot. Algunas ideas:

- Crear un formulario para mostrar el interés de los patrocinadores en la página de detalles del juego.
- Implementar la paginación en la página con la lista de juegos.
- Añadir validación de entradas y gestión de errores a los métodos auxiliares de acceso a datos.

## Resumen

Has completado el ejercicio de cloud agent. En estas lecciones:

- **Has inspeccionado los archivos de instrucciones personalizadas del repositorio** para observar su efecto en los resultados del agente en la nube.
- **Has asignado incidencias a Copilot cloud agent** y has visto cómo configura el entorno, planifica y trabaja de forma asíncrona.
- **Has creado y usado un agente personalizado** de accesibilidad para añadir conmutadores de contraste alto y modo claro.
- **Has usado la página de agentes de Copilot como centro de control** para supervisar y orientar la sesión de accesibilidad mientras estaba en curso.
- **Has revisado e iterado sobre las solicitudes de cloud agent**, has mencionado a `@copilot` para pedir cambios y has aprobado flujos de trabajo.

## Repaso y siguientes pasos

Has completado el ejercicio de cloud agent. Si quieres seguir explorando, puedes complementar lo aprendido con estos otros ejercicios:

- 🖥️ **[Ejercicio de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración con MCP directamente desde el IDE.
- 💻 **[Ejercicio de CLI](../../cli/)**: publica dos cambios revisados desde el terminal con los modos Plan y Autopilot, skills de agente, un agente de QA personalizado, Playwright MCP, Agent Merge y un puente opcional de `/delegate` a cloud agent.

En tu propio repositorio, prueba estas ideas:

- Asignar a cloud agent una incidencia de refactorización o cobertura de pruebas.
- Crear un agente personalizado para otro ámbito.
- Configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración de Copilot cloud agent][cloud-agent-best-practices]
- [Configurar el cortafuegos de Copilot cloud agent][agent-firewall]

---

| [← Lección anterior: administrar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
