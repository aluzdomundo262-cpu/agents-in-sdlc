---
title: "Lección 2: Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Instrucciones personalizadas][previous-lesson]

Muchas organizaciones tienen que gestionar deuda técnica: problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidades que llevan tiempo en el backlog. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, crea una solicitud de incorporación de cambios (PR) en borrador para que la revise un desarrollador. Así puedes delegar tareas rutinarias y centrarte en trabajos de mayor alcance.

En esta lección explorarás cómo utilizar el agente en la nube de Copilot para:

- personalizar el entorno de generación de código.
- asegurar que las operaciones se realicen de forma segura.
- comprender la importancia de delimitar bien las incidencias.
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys quiere abordar varios problemas de deuda técnica. La documentación que dejó el equipo contratado para crear la primera versión del sitio es insuficiente. Como primer paso, quieren añadir comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere mejorar el descubrimiento de juegos. Quiere mostrar en la página de detalles de cada juego otros títulos de la misma categoría para que los visitantes puedan seguir explorando. Por ahora, necesitan una implementación sencilla para probar la experiencia de usuario (UX); la funcionalidad es un bloqueo, aunque hay incidencias de mayor prioridad.

Estas tareas suelen aplazarse y son buenas candidatas para delegarlas al agente en la nube. El agente puede trabajar de forma asíncrona mientras tú te ocupas de otras tareas y, después, puedes revisar el resultado.

## Acerca del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot][copilot-agents] puede realizar tareas en segundo plano de forma parecida a un desarrollador. Por ejemplo, puedes [asignarle una incidencia de GitHub][assign-issue]. Cuando se la asignas, Copilot crea una PR en borrador para seguir el progreso, configura un entorno y empieza a trabajar. Puedes consultar la sesión mientras está activa o cuando haya terminado. Cuando la solución esté lista para revisarla, Copilot te mencionará en la PR.

## Delimita bien las instrucciones

GitHub Copilot no elimina la necesidad de analizar el trabajo. Incluso las tareas aparentemente sencillas pueden tener complejidades, así que sigue las [recomendaciones para delimitar el trabajo del agente en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian por incorporar IA generativa.

## Instrucciones personalizadas del repositorio

En lecciones anteriores has visto cómo las instrucciones personalizadas orientan a Copilot. Antes de asignar trabajo al agente, revisa los archivos de instrucciones que ya incluye el repositorio. Podrás reconocer su influencia más adelante.

1. Abre en la interfaz web de GitHub o en un Codespace estos archivos:
   - `.github/copilot-instructions.md`: revisa la sección **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
   - `.github/instructions/unit-tests.instructions.md`: fíjate en el frontmatter `applyTo`, que limita estas instrucciones a archivos `**/*.test.ts`.

Cuando asignes la incidencia **Code lacks documentation** al agente en la nube, revisa si la PR incluye comentarios TSDoc, convenciones de TypeScript y encabezados de comentario. Estas directrices proceden de los archivos de instrucciones. Volverás a revisarlas al evaluar las PR en una lección posterior.

## Configura el entorno de desarrollo del agente

El agente en la nube utiliza [GitHub Actions][github-actions] para configurar el entorno en el que trabaja. Puedes personalizarlo mediante el flujo de trabajo de configuración `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece. Este archivo ya está preparado para el taller y garantiza que el agente tenga Node.js, las dependencias del proyecto, los navegadores de pruebas de extremo a extremo y la base de datos SQLite migrada y con datos iniciales para la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio.
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Concede solo los permisos mínimos necesarios para estos pasos. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si los pasos de configuración clonan el repositorio, por ejemplo, para instalar dependencias, necesitan el permiso `contents: read`. Si no lo clonan, Copilot lo hará automáticamente cuando terminen los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de frontend y aplicación: Node.js (la aplicación ahora utiliza Astro, Drizzle y libSQL).
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y prepara la base de datos SQLite local para que las compilaciones y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier otro flujo de trabajo de GitHub, pero hay dos aspectos importantes:

- Incluye un único trabajo llamado `copilot-setup-steps`, que se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la solicitud de incorporación de cambios.
- El activador `workflow_dispatch` permite ejecutar manualmente el flujo de trabajo desde la pestaña **Actions** del repositorio. Así puedes probarlo sin esperar a que Copilot lo ejecute.

## Asigna una tarea de documentación

La documentación de muchos proyectos está desactualizada o falta por completo. Esta deuda técnica reduce la productividad y dificulta el mantenimiento y la incorporación de nuevos desarrolladores. El agente en la nube puede trabajar en la documentación en segundo plano; revisarás el resultado en una lección posterior.

1. En una nueva pestaña del navegador, abre el repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Code lacks documentation` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. Selecciona **Create** para crear la incidencia.
8. En el panel derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

   ![Detalles de la asignación a Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecciona la pestaña **Pull Requests**.
11. Abre la nueva PR, cuyo título será similar a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la página.
12. Espera unos minutos a que Copilot cree una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer. Copilot está preparando el entorno mediante el flujo de trabajo anterior, analizando el proyecto y definiendo un enfoque.

13. Revisa la lista y las tareas previstas.
14. Desplázate por la cronología de la PR y comprueba que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona **View session**.

   ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la página para ver el indicador actualizado.

16. Recorre la sesión en directo y observa cómo Copilot explora el código, analiza el estado, planifica e implementa cambios.

El trabajo puede tardar varios minutos. El agente en la nube está diseñado para trabajar de forma asíncrona; mientras tanto, le asignarás otra tarea y podrás ocuparte de desarrollar una funcionalidad.

## Asigna una sección de juegos relacionados

Una ventaja del agente en la nube es que puede trabajar en una tarea mientras tú te ocupas de otra. Ahora delegarás al agente la sección de juegos relacionados que necesita el equipo de diseño.

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Show related games on the game details page` en **Title**.
6. Escribe lo siguiente en **Description**:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecciona **Create** para crear la incidencia.
8. En el panel derecho, selecciona **Assign to Copilot**.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Al poco tiempo, verás el emoji 👀 en el primer comentario de la incidencia. Indica que Copilot está trabajando en ella.

![El emoji de ojos indica que Copilot está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

El agente ya trabaja en la segunda tarea. No es necesario supervisarlo continuamente; revisa el resultado cuando termine. A continuación, crearás y utilizarás agentes personalizados.

## Resumen y pasos siguientes

Has explorado el [agente en la nube de GitHub Copilot][copilot-agents], al que puedes asignar incidencias para que las resuelva de forma asíncrona. Puedes utilizarlo para abordar deuda técnica, crear funcionalidades o migrar código entre frameworks.

En esta lección:

- has personalizado el entorno de generación de código.
- has comprobado cómo asegurar las operaciones.
- has explorado la importancia de delimitar bien las incidencias.
- has asignado incidencias a Copilot.

Mientras el agente en la nube trabaja, puedes crear y utilizar agentes personalizados. El [agente en la nube también puede utilizar servidores MCP][cloud-agent-mcp] y las instrucciones personalizadas que exploraste en lecciones anteriores.

## Recursos

- [Acerca del agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
