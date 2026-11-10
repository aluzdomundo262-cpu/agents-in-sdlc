---
title: "Lección 2: Añadir funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso los cambios más sencillos suelen afectar a varios archivos y requieren ejecutar pruebas. Como desarrollador, tienes que localizar los archivos pertinentes, hacer los cambios, ejecutar las pruebas, depurar los fallos y volver a revisar el trabajo. El modo de agente de Copilot puede explorar el proyecto, actualizar varios archivos, ejecutar tareas como las pruebas y corregir los errores que encuentre. En esta lección lo utilizarás para añadir una funcionalidad al sitio.

> [!NOTE]
> Aunque sus nombres se parecen, el modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el entorno de desarrollo integrado (IDE) y permite iterar rápidamente. El agente en la nube trabaja de forma asíncrona con incidencias y solicitudes de incorporación de cambios.

En esta lección:

- utilizarás el modo de agente de Copilot para explorar el proyecto, identificar los archivos pertinentes y coordinar cambios.
- implementarás una funcionalidad que afecta a la interfaz de usuario (UI) y a la capa de datos.
- revisarás los cambios y las pruebas generados por Copilot antes de combinarlos.

## Escenario

A medida que crece la lista de juegos, quieres que los usuarios puedan filtrarla por categoría y editorial. En la lección anterior añadiste un método auxiliar para las editoriales. Ahora completarás el trabajo de la capa de datos, la interfaz y las pruebas con el modo de agente.

## Ejecuta el sitio de Tailspin Toys

Antes de hacer cambios, explora el sitio para conocer su funcionalidad actual.

Tailspin Toys es una plataforma de financiación colectiva para juegos de mesa con una temática para desarrolladores. Permite mostrar juegos y consultar sus detalles. El sitio es una única aplicación Astro que genera páginas estáticas de lenguaje de marcado de hipertexto (HTML) durante la compilación. Las páginas consultan una base de datos SQLite local mediante Drizzle ORM desde su frontmatter; no hay una interfaz de programación de aplicaciones (API) de backend independiente ni un framework de interfaz de cliente. Los métodos auxiliares reutilizables para acceder a los datos están en `src/lib/`, y la interactividad se implementa con scripts `<script>` de Astro acotados que utilizan las interfaces de programación de aplicaciones (API) estándar del modelo de objetos del documento (Document Object Model, DOM).

### Inicia el sitio

El proyecto incluye la tarea `npm run dev`, que inicia el servidor de desarrollo de Astro.

1. Vuelve al Codespace. Al terminar el ejercicio anterior, deberías estar en `main`.
2. Abre un terminal en el Codespace con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, debería mostrar un mensaje con la URL:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo para abrir `http://localhost:4321` en un navegador, ciérralo seleccionando **x**.

5. Mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona la dirección del servidor Astro `http://localhost:4321` en el terminal.

> [!NOTE]
> En un Codespace, al seleccionar el enlace `localhost` desde el terminal se abrirá `https://<your-codespace-name>-4321.app.github.dev/`, un túnel privado al servidor del Codespace.

### Explora el sitio

Cuando el sitio esté en marcha, explora sus funciones principales:

- **Home Page**: muestra juegos de mesa con el título, las imágenes y las descripciones.
- **Game Details Page**: muestra información adicional sobre un juego, incluido el título, la descripción, la editorial y la categoría.

## Explora el backlog con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al Codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; se indican en cada paso cuando importa.

La primera versión del sitio funciona, pero quieres añadir funciones. El repositorio de plantilla incluye un backlog de incidencias. Pide a GitHub Copilot que te lo muestre.

1. En el menú de agentes de Chat, selecciona **Agent**. El agente explora y modifica varios archivos, ejecuta comandos de terminal y utiliza herramientas.

   ![Selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores del taller no recomiendan un modelo en particular. Se utilizó Claude Sonnet 4.5 para que las sugerencias fueran relativamente coherentes, pero los modelos de lenguaje de gran tamaño no son deterministas. Es normal que las sugerencias difieran de los ejemplos.

> [!NOTE]
> Por su naturaleza probabilística, Copilot puede utilizar un comando de Model Context Protocol (MCP) diferente, pero debería completar la tarea.

3. Envía este prompt para consultar las incidencias del backlog:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para permitir que el comando muestre todas las incidencias.
5. Revisa la lista generada.

Copilot también puede priorizar las incidencias según el valor que considere que aportan a los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere código, revisa el archivo de instrucciones que le proporcionará contexto. El archivo [de instrucciones para la interfaz de usuario][ui-instructions] describe cómo añadir funcionalidades al sitio.

1. En el Codespace, abre `.github/instructions/ui.instructions.md`.
2. Revisa las directrices generales, que incluyen:
   - una descripción de la arquitectura.
   - principios de diseño de componentes, capacidad de prueba y accesibilidad.
   - enlaces a instrucciones específicas para Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas al archivo que contiene el enlace. Esto permite reutilizar instrucciones, dividirlas en partes más pequeñas y proporcionar ejemplos y plantillas.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md

## Implementa el filtrado

Para completar el filtrado, tendrás que actualizar la lógica de la capa de datos en `src/lib/`, añadir o modificar pruebas y actualizar la página de lista de juegos con los controles de filtrado. También tendrás que ejecutar y superar las pruebas antes de combinar los cambios. El modo de agente de Copilot puede ayudarte con estas tareas.

1. Continúa la conversación actual o selecciona **New Chat** para iniciar otra.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Ejemplo de selección del archivo de instrucciones UI](../../../_images/ex3-select-instructions-file.png)

3. Comprueba que **Agent** sigue seleccionado en el menú de agentes de Chat.

   ![Selector de agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Comprueba que sigue seleccionado el modelo **Claude Sonnet 4.5**.
5. Pide a Copilot que implemente la funcionalidad de la incidencia relacionada:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos de la capa de datos, la interfaz y las pruebas. Después, modifica los archivos y ejecuta las pruebas.

   ![Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot puede explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar varios minutos. Es posible que aparezcan los botones **Keep** y **Undo** en el editor; espera a que termine antes de aceptar o deshacer todos los cambios.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Cuadro de diálogo de Copilot Chat que solicita permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede que haya pausas o que fallen algunas pruebas durante el proceso. Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea y dejar de detectar errores.

   ![Sesión completa de Copilot Chat en modo de agente](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Revisa el código generado para detectar posibles problemas.

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador donde se está ejecutando el sitio y prueba el filtrado.
11. Cuando hayas revisado el código y confirmado que funciona, selecciona **Keep** en Copilot Chat.

## Resumen y pasos siguientes

Has utilizado el modo de agente de GitHub Copilot para añadir funcionalidades al sitio de Tailspin Toys. En esta lección:

- has utilizado el modo de agente para explorar el proyecto, localizar archivos pertinentes y coordinar cambios.
- has implementado una funcionalidad que afecta a la interfaz y a la capa de datos.
- has revisado los cambios y las pruebas generados por Copilot antes de combinarlos.

A continuación, [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y crearás una solicitud de incorporación de cambios.

### Ejercicio adicional: implementa la paginación

A medida que crezca la lista de juegos, puede que necesites paginarla. Utiliza lo aprendido para pedir a Copilot que implemente la paginación y ten en cuenta estas recomendaciones:

- Sigue las prácticas recomendadas existentes y utiliza los archivos de instrucciones.
- Decide si los usuarios podrán elegir el tamaño de página o si este será fijo.
- Incluye en el prompt las directrices necesarias para implementar la paginación como quieres.
- Itera con GitHub Copilot, solicita cambios y proporciona más contexto cuando haga falta.

## Recursos

- [Modos Ask, Edit y Agent de Copilot: qué hacen y cuándo se utilizan][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
