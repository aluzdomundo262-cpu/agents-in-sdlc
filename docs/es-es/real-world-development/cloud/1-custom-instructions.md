---
title: "Lección 1: Instrucciones personalizadas para el agente en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental al trabajar con inteligencia artificial (IA) generativa. Si una tarea debe realizarse de una forma concreta, o Copilot necesita información de fondo, ese contexto debe estar disponible. Los [archivos de instrucciones][instruction-files] proporcionan esa orientación para que Copilot entienda no solo *qué* debe hacer, sino también *cómo* hacerlo.

En esta lección:

- explorarás cómo llegan a Copilot el contexto específico del proyecto, las directrices de codificación y los estándares de documentación mediante las instrucciones del repositorio y las instrucciones específicas de rutas.
- añadirás un estándar para todo el repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los entornos de VS Code y CLI, aquí no compararás prompts antes y después. El agente en la nube de Copilot trabaja de forma asíncrona con incidencias de GitHub, por lo que es más difícil mostrar el efecto en tiempo real. Verás la influencia de las instrucciones más adelante, al revisar las solicitudes de incorporación de cambios (PR) que genere el agente.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices para las prácticas de desarrollo:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario (UI) debe utilizar un tema oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Al principio de cada archivo debe haber un bloque de comentarios que describa su función.

Utilizarás archivos de instrucciones para proporcionar a Copilot la información necesaria para seguir estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias para que comprenda mejor tu estilo y tus requisitos. Puedes especificar convenciones de codificación, bibliotecas y los comentarios que quieres incluir. Las instrucciones pueden aplicarse a todo el repositorio o a determinados tipos de archivos y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información general del proyecto que sea pertinente para la mayoría de las interacciones con Copilot.
- Los archivos `.github/instructions/*.instructions.md` proporcionan directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz de usuario o pruebas unitarias.

> [!NOTE]
> En un entorno de desarrollo integrado (IDE), los archivos de instrucciones se utilizan para generar código en Copilot Chat, pero no para completar código ni para sugerir la siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` con el frontmatter `applyTo`.
>
> Copilot también [admite otros formatos de archivos de instrucciones][custom-instructions-support], como `AGENTS.md` y `CLAUDE.md`.

### Prácticas recomendadas para administrar archivos de instrucciones

Los ejemplos del proyecto muestran un enfoque representativo para administrar estos archivos:

- Mantén `copilot-instructions.md` centrado en la orientación general del proyecto, como su descripción, estructura y estándares globales de codificación.
- Utiliza archivos `*.instructions.md` para instrucciones específicas de tipos de archivo —como pruebas unitarias, componentes de Astro o la capa de datos— o para tareas concretas.
- Escribe en lenguaje natural. Expresa las directrices con claridad e incluye ejemplos del código que se debe utilizar y del que se debe evitar.

No hay una única forma correcta de crear archivos de instrucciones ni de utilizar la IA. La experimentación te ayudará a encontrar el enfoque adecuado para el proyecto.

> [!TIP]
> Todos los proyectos que utilicen GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. Al explorar los archivos de este proyecto, encontrarás instrucciones para tareas como las [actualizaciones de interfaz de usuario][ui-instructions] y el desarrollo con [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. La forma de hacerlo varía según el entorno; por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI. Las lecciones correspondientes indican cuándo utilizar estas opciones.
>
> Para encontrar plantillas o un punto de partida, explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones del proyecto

Revisa los archivos de instrucciones que incluye el repositorio: el archivo principal `copilot-instructions.md` y los archivos `*.instructions.md` para distintas tareas. Puedes abrirlos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Revisa la descripción breve del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, observa las directrices anidadas de **GitHub Actions Workflows**. Estas instrucciones se aplican a las interacciones con Copilot.
3. Abre la carpeta `.github/instructions` y explora sus archivos, que incluyen instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros ámbitos.
4. Abre `.github/instructions/unit-tests.instructions.md` y revisa el campo `applyTo` de la parte superior. Este campo define un patrón glob relativo a la raíz del repositorio; por ejemplo, coincide con archivos de pruebas TypeScript como `**/*.test.ts`.
5. Revisa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Así puedes dividir las instrucciones extensas en archivos reutilizables más pequeños y ofrecer ejemplos a Copilot. Las rutas son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de codificación del proyecto, pero todavía no exige incluir documentación en el código. En los pasos siguientes añadirás reglas para los comentarios TSDoc y los encabezados de comentario de los archivos.

## Añade un estándar para todo el repositorio

Añadirás una norma general para que la documentación se incluya en el código mediante comentarios TSDoc y un encabezado de comentario a nivel de archivo. El agente en la nube aplicará esta norma a las incidencias que le asignes más adelante.

Antes de editar el archivo, crea una rama. El agente en la nube lee las instrucciones de la rama a la que se dirige la incidencia, pero guardarás los cambios en una confirmación aparte.

1. Desde el terminal del Codespace, crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Las instrucciones principales del repositorio proporcionan a Copilot información general del proyecto. Añadirás los estándares de codificación que faltan para mejorar las sugerencias.

2. Vuelve a abrir `.github/copilot-instructions.md`.
3. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Comprueba que todavía no incluye reglas para documentar el código.
4. Añade estas líneas de Markdown justo después de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. Guarda `copilot-instructions.md`.

> [!TIP]
> Las instrucciones pueden definirse para todo el repositorio en `.github/copilot-instructions.md` o para lenguajes, tipos de archivo y tareas concretos en archivos `*.instructions.md`. El archivo del repositorio es el lugar adecuado para un estándar general como la regla de comentarios que acabas de añadir.

## Confirma, publica y combina la actualización

El agente en la nube lee las instrucciones de la rama de destino de la incidencia. En el siguiente ejercicio, Copilot creará una rama desde `main`; por eso, los cambios deben llegar a `main` para que el agente pueda utilizarlos.

1. Prepara y confirma el archivo:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Publica la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una solicitud de incorporación de cambios de `custom-instructions-cloud` a `main` y combínala. El agente en la nube leerá estas instrucciones cuando trabaje en las incidencias que le asignes en la siguiente lección.

> [!TIP]
> Si prefieres trabajar directamente en `main` durante este taller, puedes omitir la rama y confirmar los cambios directamente en `main`. La rama permite practicar un flujo de trabajo habitual en proyectos reales.

## Resumen y pasos siguientes

Has explorado cómo obtiene Copilot el contexto de los archivos de instrucciones y has añadido un estándar para todo el repositorio en `.github/copilot-instructions.md`. Verás cómo se aplica en las PR que genere el agente en la nube durante el resto del taller.

A continuación, [asignarás tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
