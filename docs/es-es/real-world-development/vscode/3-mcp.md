---
title: "Lección 3: Probar la funcionalidad con el servidor Model Context Protocol (MCP) de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo de agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Acabas de crear la funcionalidad de filtrado con el modo de agente. Antes de abrir una solicitud de incorporación de cambios, comprueba que funciona en el navegador. Configurarás el **servidor MCP de Playwright** para que Copilot controle un navegador real y pruebe la funcionalidad. Después, publicarás la rama y abrirás la PR.

En esta lección:

- aprenderás qué es Model Context Protocol (MCP) y cómo amplía Copilot con herramientas.
- añadirás el servidor MCP de Playwright al espacio de trabajo.
- pedirás a Copilot que lo utilice para probar manualmente el filtrado en un navegador.
- publicarás la rama y abrirás una solicitud de incorporación de cambios para el trabajo de filtrado.

## ¿Qué es Model Context Protocol?

El modo de agente resulta más útil cuando puede acceder a recursos externos al editor. Model Context Protocol (MCP) es un estándar que permite al agente comunicarse con herramientas y servicios externos.

![Diagrama del funcionamiento interno del modo de agente y su interacción con el contexto, el modelo de lenguaje y las herramientas, incluidas las aportadas por servidores MCP y extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de inteligencia artificial (IA) se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada mediante recursos y realizar acciones en tu nombre mediante herramientas.

Los agentes acceden a estas herramientas y recursos mediante un servidor MCP, que actúa como puente y gestiona la comunicación con servicios externos, como interfaces de programación de aplicaciones (API) existentes o herramientas locales distribuidas como paquetes de npm. Cada servidor ofrece un conjunto distinto de herramientas y recursos.

- **[Servidor MCP de GitHub][github-mcp-server]**: proporciona acceso a las API para administrar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: proporciona automatización del navegador con Playwright, por ejemplo, abrir páginas, rellenar formularios y seleccionar botones.

Hay muchos otros servidores MCP que proporcionan acceso a diferentes herramientas y recursos. GitHub aloja un [registro MCP][mcp-registry] para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad. Utiliza solo servidores de confianza y ten cuidado al conceder acceso a recursos o acciones sensibles.

## Revisa la configuración de MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en este espacio de trabajo.

1. Abre `.vscode/mcp.json` en el Codespace.
2. Comprueba que ya haya un servidor `github` configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

La plantilla incluye la entrada `github`. Por eso Copilot pudo leer el backlog de incidencias en la lección anterior. Utiliza el [servidor MCP remoto de GitHub][remote-github-mcp-server], así que no hay que instalarlo localmente. VS Code se conecta mediante el protocolo de transferencia de hipertexto (HTTP) y, la primera vez que Copilot utiliza una herramienta, te autenticas en GitHub.

## Añade el servidor MCP de Playwright

Añadirás un segundo servidor. El [servidor MCP de Playwright][playwright-mcp-server] proporciona a Copilot un navegador controlable para probar la funcionalidad.

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github` para que el archivo quede así:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

A diferencia del servidor remoto `github`, `playwright` se ejecuta localmente: VS Code lo inicia mediante `npx @playwright/mcp@latest`. La opción `--headless` ejecuta el navegador sin ventana visible, algo necesario en un Codespace, que no tiene escritorio gráfico.

> [!NOTE]
> Tailspin Toys ya utiliza Playwright para las pruebas de extremo a extremo (E2E), así que normalmente el navegador ya está instalado. Si Copilot indica que falta, pídele que ejecute `npx playwright install chromium` y vuelve a intentarlo.

## Inicia y autoriza el servidor

VS Code inicia los servidores MCP cuando se necesitan. La primera vez que Copilot requiere las herramientas, VS Code inicia el servidor y solicita que confirmes que confías en él.

1. En `.vscode/mcp.json`, selecciona **Start**, que aparece encima de la entrada `playwright`, para iniciar el servidor y confirmar que la configuración es correcta.
2. Si VS Code te pregunta si confías en el servidor, revisa la configuración y autorízalo para que pueda iniciarse.

Iniciarlo manualmente es opcional. Si omites estos pasos, VS Code iniciará el servidor y te pedirá que lo autorices cuando Copilot necesite sus herramientas.

## Prueba la funcionalidad de filtrado

El servidor MCP de Playwright proporciona un navegador real que Copilot puede controlar. El agente puede abrir una página, aplicar filtros, leer los resultados y resumirlos. Así puedes comprobar el comportamiento sin salir de la conversación.

El servidor trabaja con el [árbol de accesibilidad de la página][playwright-mcp-server], no con capturas de pantalla. El agente utiliza elementos estructurados y etiquetados —como botones, enlaces y elementos de lista— de una forma parecida a las tecnologías de asistencia. Por eso, una comprobación funcional también permite detectar algunos problemas básicos de accesibilidad.

Con el servidor conectado y la aplicación en marcha, pide a Copilot que pruebe el filtrado:

1. Envía este prompt:

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

Copilot abrirá un navegador mediante el servidor MCP de Playwright, seguirá los pasos y resumirá los resultados. Compara el informe con los criterios de aceptación de la incidencia. Si algo no funciona, pide más información o corrige el código antes de crear la PR.

> [!NOTE]
> La aplicación debe estar en ejecución en `http://localhost:4321`. Si has detenido el servidor de desarrollo, vuelve a iniciarlo antes de enviar el prompt. La primera vez que Copilot utilice Playwright MCP puede descargar un navegador; si indica que falta, pídele que ejecute `npx playwright install chromium` y vuelve a intentarlo.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publica la rama y crea una solicitud de incorporación de cambios

Después de confirmar que la funcionalidad funciona, publica la rama `filtering-vscode` para que el equipo pueda revisar los cambios.

1. Abre el panel **Source Control** del Codespace y revisa los cambios de Copilot.
2. Selecciona **+** para preparar los cambios.
3. Genera un mensaje de confirmación con el botón **Sparkle**.

   ![Panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

4. Selecciona **Publish** para enviar la rama al repositorio.

## Crea la solicitud de incorporación de cambios

Puedes crear una solicitud de incorporación de cambios (PR) desde github.com o mediante la interfaz de línea de comandos (CLI) de GitHub. También puedes pedir a Copilot que la cree y la vincule a la incidencia correcta.

1. Abre el panel Copilot Chat y selecciona **New Chat** para iniciar una sesión nueva.
2. Comprueba que está seleccionado **Agent** para que Copilot pueda utilizar las herramientas de GitHub.
3. Pide a Copilot que cree una PR:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Cuando sea necesario, selecciona **Continue** para permitir que Copilot busque la información y realice las operaciones. La primera vez que utilice una herramienta de GitHub, puede que tengas que iniciar sesión; sigue las indicaciones.
5. Comprueba que Copilot encuentra la incidencia correcta y crea la PR.
6. Selecciona el enlace para revisar la PR. **No la combines todavía.**

## Resumen y pasos siguientes

En esta lección:

- has aprendido qué es Model Context Protocol (MCP) y cómo amplía Copilot con herramientas.
- has añadido el servidor MCP de Playwright al espacio de trabajo.
- has utilizado el servidor para probar manualmente la funcionalidad de filtrado en un navegador.
- has publicado la rama y abierto una solicitud de incorporación de cambios.

Has utilizado un servidor MCP para probar una funcionalidad. A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas específicas, como las revisiones de accesibilidad.

## Recursos

- [Qué es MCP y por qué se habla tanto de ello][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro MCP de GitHub][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
