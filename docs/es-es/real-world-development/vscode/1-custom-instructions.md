---
title: "Lección 1: Instrucciones personalizadas para VS Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo de agente →][next-lesson]

El contexto es fundamental al trabajar con inteligencia artificial generativa. Si una tarea debe realizarse de una forma concreta, o Copilot necesita información de fondo, ese contexto debe estar disponible. Los [archivos de instrucciones][instruction-files] proporcionan orientación para generar código.

En esta lección:

- explorarás cómo llegan a Copilot el contexto del proyecto, las directrices de codificación y los estándares de documentación mediante las instrucciones del repositorio y las instrucciones específicas de rutas.
- generarás la primera parte de los datos para el filtrado (un método auxiliar de editoriales) con las instrucciones actuales.
- añadirás un estándar para todo el repositorio a `.github/copilot-instructions.md`.
- volverás a enviar el mismo prompt y observarás cómo el código generado sigue el estándar nuevo.
- confirmarás los cambios de instrucciones y de la primera parte del filtrado en `main` para que Copilot utilice las directrices actualizadas en la siguiente lección.

> [!CAUTION]
> El código generado puede no seguir todos los estándares: Copilot no es determinista. El objetivo es observar la tendencia del cambio después de actualizar las instrucciones, no obtener siempre el mismo resultado exacto.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices para las prácticas de desarrollo:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario (UI) debe utilizar un tema oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Al principio de cada archivo debe haber un bloque de comentarios que describa su función.

Utilizarás archivos de instrucciones para proporcionar a Copilot el contexto necesario para seguir estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias para que comprenda mejor tu estilo y tus requisitos. Puedes especificar convenciones de codificación, bibliotecas y los comentarios que quieres incluir. Las instrucciones pueden aplicarse a todo el repositorio o a determinados tipos de archivos y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en **todas** las solicitudes del repositorio. Debe incluir información general del proyecto, como la pila tecnológica, una descripción de lo que se desarrolla, prácticas recomendadas y directrices globales.
- Los archivos `.github/instructions/*.instructions.md` proporcionan directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas unitarias.

> [!NOTE]
> En un entorno de desarrollo integrado (IDE), los archivos de instrucciones se utilizan para generar código en Copilot Chat, pero no para completar código ni para sugerir la siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` con el frontmatter `applyTo`.
>
> Copilot también [admite otros formatos de archivos de instrucciones][custom-instructions-support], como `AGENTS.md` y `CLAUDE.md`.

### Prácticas recomendadas para administrar archivos de instrucciones

Los ejemplos del proyecto muestran un enfoque representativo:

- Mantén `copilot-instructions.md` centrado en la orientación general del proyecto, como su descripción, estructura y estándares globales de codificación.
- Utiliza archivos `*.instructions.md` para instrucciones específicas de tipos de archivo —como pruebas unitarias, componentes de Astro o la capa de datos— o para tareas concretas.
- Escribe en lenguaje natural, con directrices claras y ejemplos del código que se debe utilizar y del que se debe evitar.

No hay una única forma correcta de crear archivos de instrucciones ni de utilizar la IA. La experimentación te ayudará a encontrar el enfoque adecuado para el proyecto.

> [!TIP]
> Los proyectos que utilizan GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. En este proyecto encontrarás archivos para varias tareas, como las [actualizaciones de interfaz de usuario][ui-instructions] y el desarrollo con [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. La forma de hacerlo varía según el entorno; por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI. Las lecciones correspondientes indican cuándo utilizar estas opciones.
>
> Para encontrar plantillas o un punto de partida, explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones del proyecto

Revisa los archivos de instrucciones que incluye el repositorio: el archivo principal `copilot-instructions.md` y los archivos `*.instructions.md` para distintas tareas. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Revisa la descripción breve del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, observa las directrices anidadas de **GitHub Actions Workflows**. Se aplican a las interacciones con Copilot.
3. Abre la carpeta `.github/instructions` y explora sus archivos, que incluyen instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros ámbitos.
4. Abre `.github/instructions/unit-tests.instructions.md` y revisa el campo `applyTo` de la parte superior. Este campo define un patrón glob relativo a la raíz del repositorio; por ejemplo, coincide con archivos de pruebas TypeScript como `**/*.test.ts`.
5. Revisa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Así puedes dividir las instrucciones extensas en archivos reutilizables más pequeños y ofrecer ejemplos a Copilot. Las rutas son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de codificación, pero todavía no exige incluir documentación en el código. En los pasos siguientes añadirás reglas para los comentarios TSDoc y los encabezados de comentario de los archivos.

## Crea una rama para los cambios

Utilizarás una rama independiente para los cambios de este ejercicio.

1. Vuelve al Codespace de la lección anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Envía un prompt antes de actualizar las instrucciones

Para observar el efecto de las instrucciones personalizadas, empieza enviando un prompt con el archivo de instrucciones actual. Más adelante actualizarás el archivo y volverás a enviar el mismo prompt para comparar el resultado.

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al Codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; se indican en cada paso cuando importa.

1. Cierra las pestañas abiertas de ejercicios anteriores para que Copilot reciba solo el contexto pertinente.
2. Abre `src/lib/publishers.ts` para indicar a Copilot dónde debe ubicarse el método auxiliar.
3. En el menú de agentes de Chat, selecciona **Agent** para que Copilot pueda editar archivos.

   ![Selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot explora el proyecto y aplica cambios, normalmente en el método auxiliar y sus pruebas.
6. Observa que el método propuesto tiene tipos, recibe un cliente `db` como primer argumento y devuelve una matriz tipada de editoriales. Sigue las convenciones de la capa de datos de `.github/instructions/drizzle.instructions.md`, que se aplican a `src/lib/*.ts`.
7. Observa si el código propuesto carece de comentarios TSDoc y de un encabezado de comentario a nivel de archivo.

> [!CAUTION]
> Como Copilot no es determinista, puede que añada comentarios aunque todavía no se lo hayas pedido. No pasa nada: el objetivo es observar si mejora la coherencia después de actualizar las instrucciones.

## Añade un estándar para todo el repositorio

El archivo `.github/copilot-instructions.md` proporciona información general del proyecto. Añadirás los estándares que faltan para mejorar las sugerencias de código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Comprueba que todavía no incluya reglas para documentar el código.
3. Añade estas líneas de Markdown justo después de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Las instrucciones pueden definirse para todo el repositorio en `.github/copilot-instructions.md` o para lenguajes, tipos de archivo y tareas concretos en archivos `*.instructions.md`. El archivo del repositorio es el lugar adecuado para un estándar general como la regla de comentarios que acabas de añadir.

## Vuelve a enviar el prompt y observa el cambio

Repite el mismo prompt para comprobar si Copilot aplica las instrucciones nuevas.

1. Vuelve a Copilot Chat y selecciona **New Chat** para iniciar una conversación limpia.
2. Selecciona de nuevo `src/lib/publishers.ts` para proporcionar a Copilot el contexto del archivo.
3. Envía el mismo prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Comprueba si el archivo empieza con un bloque de comentarios similar a este:

   ```typescript
   /**
    * Métodos auxiliares de acceso a los datos de editoriales de la plataforma
    * de financiación colectiva de Tailspin Toys.
    * Proporciona funciones para recuperar información de las editoriales de la base de datos.
    */
   ```

5. Comprueba si la función incluye un comentario TSDoc similar a este:

   ```typescript
   /**
    * Devuelve una lista de todas las editoriales con su identificador y nombre.
    *
    * @param db - Cliente de base de datos Drizzle.
    * @returns Una promesa que se resuelve en una matriz de objetos de editorial.
    */
   ```

Has orientado a Copilot para que aplique un estándar nuevo al código que ampliarás en la siguiente lección.

## Confirma las instrucciones y publica la rama

Los archivos de instrucciones, como los demás archivos del repositorio, se administran mediante el control de versiones. Confirma los cambios y publícalos.

1. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Comprueba que están presentes las instrucciones actualizadas y los cambios del método auxiliar:

   ```bash
   git status
   ```

3. Prepara y confirma las instrucciones y todos los archivos modificados por Copilot para el método auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra otros cambios necesarios, como pruebas, añádelos también.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Publica la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Con la rama publicada, crea una solicitud de incorporación de cambios y vincúlala a la incidencia del backlog sobre los estándares de documentación. Copilot puede buscar la incidencia, crear la solicitud y combinarla.

> [!NOTE]
> Es el primer ejercicio en el que Copilot actúa en GitHub. La plantilla ya configura las herramientas de GitHub para el espacio de trabajo; no tienes que instalar nada. La primera vez que Copilot utilice una herramienta, VS Code puede pedirte que inicies sesión en GitHub. Sigue las instrucciones para autorizarlo. En una lección posterior aprenderás cómo funciona esta conexión mediante Model Context Protocol (MCP).

1. Abre Copilot Chat en el Codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista Copilot Chat y comprueba que **Agent** está seleccionado en el selector de agentes.
3. Pide a Copilot que encuentre la incidencia sobre las instrucciones y cree una PR desde la rama actual que describa ambos cambios:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Espera a que Copilot busque la incidencia y cree la PR.
5. Cuando Copilot te pida permiso para realizar acciones en GitHub, revisa el comando y selecciona **Allow** si estás de acuerdo.
6. Cuando se cree la PR, pide a Copilot que la combine y vuelva a la rama principal:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Cuando Copilot te pida permiso para realizar acciones de GitHub y ejecutar comandos de shell, revisa el comando y selecciona **Allow** si estás de acuerdo.

Has creado y combinado una solicitud de incorporación de cambios con GitHub Copilot.

## Resumen y pasos siguientes

Has explorado cómo obtiene Copilot el contexto de los archivos de instrucciones. En esta lección:

- has enviado un prompt de generación de código y observado el resultado con las instrucciones existentes.
- has añadido un estándar para todo el repositorio a `.github/copilot-instructions.md`.
- has vuelto a enviar el mismo prompt y observado cómo el código propuesto sigue el estándar nuevo.
- has confirmado los cambios de instrucciones y del método auxiliar en `main` para que la siguiente lección pueda utilizarlos.

A continuación, aplicarás esas instrucciones en el [modo de agente][next-lesson] mientras Copilot añade una funcionalidad al proyecto.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
[awesome-copilot]: https://github.com/github/awesome-copilot
