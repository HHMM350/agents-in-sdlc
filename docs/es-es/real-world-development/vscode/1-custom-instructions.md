---
title: "Ejercicio 1: instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: requisitos previos][previous-lesson] · [Siguiente lección: modo de agente →][next-lesson]

El contexto es fundamental cuando trabajas con IA generativa. Si una tarea debe realizarse de una manera concreta, o Copilot necesita información adicional, debes asegurarte de que pueda acceder a ese contexto. Los [archivos de instrucciones][instruction-files] son una de las principales maneras de proporcionar directrices a Copilot sobre la generación de código.

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto específico del proyecto, las directrices de programación y los estándares de documentación mediante las instrucciones personalizadas del repositorio y los archivos de instrucciones específicos para ciertas rutas.
- generarás la primera parte de los datos para el filtrado (un método auxiliar para editores) con las instrucciones actuales.
- añadirás un estándar nuevo para todo el repositorio en `.github/copilot-instructions.md`.
- volverás a enviar el mismo mensaje y observarás cómo el código generado incorpora el estándar nuevo.
- confirmarás las instrucciones y los cambios de la funcionalidad en `main` para que Copilot pueda usar las directrices actualizadas en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede no seguir todos los estándares que hayas indicado, porque Copilot no es determinista. El objetivo del ejercicio es observar la *tendencia* de los cambios en el comportamiento después de actualizar las instrucciones, no obtener siempre un resultado idéntico.

## Archivos de instrucciones

### Escenario

Como cualquier buen equipo de desarrollo, Tailspin Toys tiene directrices y requisitos para sus prácticas de desarrollo. Entre ellos:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz de usuario debe usar un tema oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Al principio de cada archivo debe haber un bloque de comentarios que explique su contenido.

Con los archivos de instrucciones, te asegurarás de que Copilot disponga de la información adecuada para realizar las tareas siguiendo estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias para que entienda mejor tu estilo y tus requisitos de programación. Te permiten orientar sus sugerencias y fragmentos de código. Puedes especificar las convenciones de programación, las bibliotecas e incluso los comentarios que prefieres. Puedes crear instrucciones para todo el repositorio o para tipos concretos de archivo y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un único archivo que se envía a Copilot en **todas** las solicitudes relacionadas con el repositorio. Debe incluir información del proyecto útil para la mayoría de las solicitudes de chat o CLI, como la pila tecnológica, una descripción general de lo que se está desarrollando, las prácticas recomendadas y otras directrices generales.
- `.github/instructions/*.instructions.md`, archivos que puedes crear para tareas o tipos de archivo concretos. Permiten proporcionar directrices para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz o un conjunto de pruebas unitarias.

> [!NOTE]
> En el IDE, los archivos de instrucciones solo se usan para generar código con Copilot Chat, no para completar código ni para las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y Copilot cloud agent usan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que tienen frontmatter `applyTo`.
>
> Copilot [admite otros formatos de archivos de instrucciones][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para administrar archivos de instrucciones

Este taller no incluye una explicación exhaustiva sobre cómo crear archivos de instrucciones, pero los ejemplos del proyecto muestran un enfoque representativo. A grandes rasgos:

- Limita las instrucciones de `copilot-instructions.md` a directrices generales del proyecto, como su descripción, estructura y estándares globales de programación.
- Usa archivos `*.instructions.md` para dar instrucciones específicas a tipos de archivo (pruebas unitarias, componentes Astro o la capa de datos) o tareas concretas.
- Escribe en lenguaje natural. Procura que las directrices sean claras e incluye ejemplos de cómo debería y no debería ser el código.

No existe una única manera de crear archivos de instrucciones, igual que no hay una única manera de usar la IA. La experimentación te ayudará a encontrar el enfoque que funciona mejor para tu proyecto.

> [!TIP]
> Todos los proyectos que usan GitHub Copilot deberían tener una colección completa de archivos de instrucciones. Al explorar los archivos de este proyecto, puede que observes que abarcan muchos tipos de tareas, incluidas las [actualizaciones de la interfaz de usuario][ui-instructions] y el [código Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada entorno ofrece esta opción de forma distinta; por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI. El ejercicio de cada entorno indicará cuándo corresponde usarla.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas de este proyecto

Dedica un momento a leer los archivos de instrucciones que incluye este repositorio: hay un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Explora el archivo y fíjate en la breve descripción del proyecto y en secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, fíjate también en las directrices anidadas de **GitHub Actions Workflows**. Estas instrucciones se aplican a cualquier interacción con Copilot en el repositorio.
3. Abre la carpeta `.github/instructions` y explórala. Verás instrucciones para archivos Astro, la capa de datos de Drizzle, pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. Fíjate en el campo `applyTo` del principio: contiene un patrón glob, relativo a la raíz del repositorio, que determina a qué archivos se aplican las instrucciones. Coincidirá con cualquier archivo de pruebas TypeScript, por ejemplo, uno que se ajuste al patrón `**/*.test.ts`.
5. Fíjate en las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Fíjate en los vínculos a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Así puedes dividir conjuntos de instrucciones grandes en archivos más pequeños y reutilizables, y enlazar ejemplos para que Copilot los siga. Las rutas que aparecen ahí son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero aún no exige documentación dentro del código. En los pasos siguientes añadirás reglas para los comentarios TSDoc y los encabezados de comentario de los archivos.

## Crea una rama para los cambios

Vamos a seguir algunas prácticas recomendadas y crear una rama para estos cambios.

1. Vuelve al codespace del ejercicio anterior.
2. Abre un terminal nuevo pulsando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea una rama nueva y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Usa Copilot Chat *antes* de actualizar las instrucciones

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los siguientes ejercicios, vuelve al codespace, abre el panel de Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso los indica cuando corresponde.

Para observar el efecto de las instrucciones personalizadas, empieza enviando un mensaje con el archivo de instrucciones actual. Más adelante, lo actualizarás y volverás a enviar el mismo mensaje para comparar el resultado.

1. Cierra las pestañas abiertas del editor de los ejercicios anteriores para que Copilot use solo el contexto que necesitas.
2. Abre `src/lib/publishers.ts` para que Copilot sepa dónde debe estar el método auxiliar.
3. Selecciona **Agent** en el menú desplegable de agentes de la vista Chat para que Copilot pueda modificar archivos.

   ![Captura del selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este mensaje:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un método auxiliar de acceso a datos que devuelva una lista de todos los editores, con el nombre y el id de cada uno. Aplica los cambios a los archivos.
   ```

5. Copilot explorará el proyecto y aplicará cambios de código; a menudo modificará tanto el archivo del método auxiliar como sus pruebas.
6. Fíjate en que el método auxiliar propuesto es una función tipada que recibe un cliente `db` como primer argumento y devuelve una matriz tipada de editores. Esto se debe a las convenciones de la capa de datos definidas en `.github/instructions/drizzle.instructions.md`, que se aplican a `src/lib/*.ts`.
7. Fíjate en que al código propuesto **le faltan** los comentarios TSDoc y el encabezado de comentario a nivel de archivo.

> [!CAUTION]
> Como Copilot no es determinista, es posible que añada comentarios de documentación aunque no se lo pidas. No pasa nada; el objetivo es observar la mejora de coherencia después de actualizar las instrucciones.

## Añade un estándar para todo el repositorio

Como ya hemos indicado, `.github/copilot-instructions.md` proporciona información del proyecto a Copilot. Añadiremos los estándares de programación del repositorio para mejorar las sugerencias.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Fíjate en cómo documenta los estándares de programación del proyecto. Aún no incluye instrucciones para documentar el código, por lo que la función auxiliar generada no tenía comentarios de documentación.
3. Añade estas líneas Markdown debajo de los estándares existentes para pedir a Copilot que añada encabezados de comentario y comentarios TSDoc:

   ```markdown
   - Todas las funciones exportadas deben incluir un comentario TSDoc que describa su objetivo, sus parámetros y su valor devuelto.
   - Antes de las importaciones o de cualquier otro código, añade un bloque de comentarios que explique el objetivo del archivo.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como has visto en la lección anterior, los archivos de instrucciones pueden estar en el nivel del repositorio (`.github/copilot-instructions.md`) para proporcionar directrices generales, o ser archivos `*.instructions.md` para lenguajes, tipos de archivo o tareas concretas. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla de comentarios de documentación que acabas de añadir.

## Vuelve a enviar el mensaje y observa el cambio

1. Vuelve a Copilot Chat y selecciona **New Chat** para vaciar la conversación.
2. Vuelve a seleccionar `src/lib/publishers.ts` para que Copilot se centre en el archivo correcto.
3. Envía **el mismo mensaje** que antes:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un método auxiliar de acceso a datos que devuelva una lista de todos los editores, con el nombre y el id de cada uno. Aplica los cambios a los archivos.
   ```

4. Fíjate en que el archivo propuesto ahora empieza con un bloque de comentarios parecido a este:

   ```typescript
   /**
    * Métodos auxiliares de acceso a los datos de editores de la plataforma de financiación colectiva de Tailspin Toys.
    * Proporciona funciones para recuperar información de los editores de la base de datos.
    */
   ```

5. Fíjate en que la función propuesta ahora incluye un comentario TSDoc parecido a este:

   ```typescript
   /**
    * Devuelve una lista de todos los editores con su id y su nombre.
    *
    * @param db - Cliente de base de datos Drizzle.
    * @returns Una promesa que se resuelve en una matriz de objetos de editor.
    */
   ```

Has orientado a Copilot para que siga un estándar nuevo del proyecto y lo aplique al código real sobre el que se basa el siguiente ejercicio.

## Confirma las instrucciones y sube la rama

Los archivos de instrucciones son recursos del repositorio y se administran mediante el mismo control de versiones que otros archivos. Vamos a confirmar los cambios y subir la rama al repositorio.

1. Abre una ventana de terminal nueva pulsando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Comprueba en el terminal que estén presentes la actualización de instrucciones y los cambios del método auxiliar:

   ```bash
   git status
   ```

3. Prepara y confirma la actualización de instrucciones y todos los archivos modificados por Copilot para la base del método auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra otros cambios relacionados, como pruebas, añade también esos archivos.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Sube la rama al repositorio:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y fusiona una solicitud de incorporación de cambios

Ya has subido la rama y ahora debes crear una solicitud de incorporación de cambios vinculada a la incidencia sobre los estándares de documentación de la lista de tareas. Podrías hacerlo manualmente, pero Copilot puede encargarse con las herramientas de GitHub conectadas al proyecto. Le pediremos que busque la incidencia, cree una solicitud para cerrarla y la fusione.

> [!NOTE]
> Este es el primer ejercicio en el que Copilot actúa en GitHub en tu nombre. La plantilla del proyecto ya conecta las herramientas de GitHub al espacio de trabajo, así que no hay que configurar nada. La primera vez que use una herramienta de GitHub, puede que VS Code te pida que inicies sesión. Sigue las instrucciones para permitirlo. En un ejercicio posterior aprenderás cómo funciona esta conexión (Model Context Protocol).

1. Abre Copilot Chat en el codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista de Copilot Chat y comprueba que **Agent** está seleccionado en el selector de agentes.
3. Pide a Copilot que busque la incidencia sobre la actualización de los archivos de instrucciones y cree una solicitud desde la rama actual que describa las instrucciones actualizadas y la nueva base del método auxiliar de editores:

   ```plaintext
   Busca la incidencia relacionada con la actualización del archivo de instrucciones. Crea una solicitud de incorporación de cambios desde la rama actual, indica que cierra esa incidencia e incluye que también hemos añadido la base del método auxiliar de editores para el próximo trabajo de filtrado.
   ```

4. Copilot buscará la incidencia y creará la solicitud.
5. Cuando Copilot te pida permiso para realizar acciones de GitHub en tu nombre, revisa el comando y selecciona **Allow** si corresponde.
6. Cuando se cree la solicitud, pide a Copilot que la fusione y vuelva a `main`:

   ```plaintext
   Fusiona la solicitud en main. Después, vuelve localmente a main y descarga el código más reciente para actualizarlo.
   ```

7. Cuando Copilot te pida permiso para realizar acciones de GitHub y ejecutar comandos de shell en tu nombre, revisa el comando y selecciona **Allow** si corresponde.

¡Has creado y fusionado una solicitud de incorporación de cambios con ayuda de GitHub Copilot!

## Resumen y siguientes pasos

Has explorado cómo obtiene Copilot el contexto de los archivos de instrucciones de este proyecto y has usado Copilot Chat en VS Code para:

- enviar un mensaje de generación de código y observar el resultado con las instrucciones *existentes*.
- añadir un estándar nuevo para todo el repositorio en `.github/copilot-instructions.md`.
- volver a enviar el mismo mensaje y observar cómo el código propuesto incorpora el estándar.
- confirmar la actualización de instrucciones y la base del método auxiliar en `main` para que sirvan de base al siguiente ejercicio.

A continuación, aplicarás las instrucciones en [modo de agente][next-lesson] mientras Copilot añade una funcionalidad al código.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personalizadas personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
