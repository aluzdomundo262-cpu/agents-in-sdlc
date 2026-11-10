---
title: "Lección 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Administrar agentes][previous-lesson] |
|:--|

## Revisa el trabajo

Durante el taller has utilizado GitHub Copilot para mejorar la experiencia de usuario y añadir funcionalidades: documentar el código, crear una sección de juegos relacionados y desarrollar funciones de accesibilidad con modos de alto contraste y claro. Revisarás los cambios y, si hace falta, pedirás a Copilot que los mejore.

### Escenario

Los principios de diseño de software y DevOps no cambian al incorporar inteligencia artificial generativa. Revisa el código generado y sigue el proceso habitual del equipo. En esta lección evaluarás las PR de documentación, juegos relacionados y accesibilidad antes de habilitar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

El agente en la nube trabaja de forma asíncrona y sin supervisión directa, por lo que se aplican restricciones de seguridad:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utiliza para su trabajo.
- El agente se ejecuta en GitHub Actions, en un entorno temporal e independiente.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de que se ejecuten.
- [El acceso a recursos externos está limitado de forma predeterminada][agent-firewall], incluidos los servidores de Model Context Protocol (MCP).

## Revisa la documentación generada

Empieza por la primera solicitud de incorporación de cambios (PR) que generó el agente en la nube: la documentación del código. La revisarás desde la interfaz estándar de PR de GitHub.com.

> [!NOTE]
> Es posible que la PR muestre una advertencia de que el firewall ha bloqueado a GitHub Copilot. Es lo esperado: el acceso a recursos externos, incluidos los servidores MCP externos, está limitado de forma predeterminada. Si quieres, puedes [configurar o deshabilitar el firewall del agente en la nube][agent-firewall].

1. Vuelve al repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de PR.
3. Abre la PR titulada, por ejemplo, **Add missing documentation**.

> [!NOTE]
> Si Copilot todavía trabaja en la tarea, la PR tendrá la etiqueta **[WIP]**. Espera a que termine; puede tardar unos minutos.

4. Cuando la PR esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que ahora puede incluir comentarios TSDoc y otra documentación. Los cambios exactos varían. Comprueba los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentario; proceden de los archivos de instrucciones que revisaste al principio de la lección 2.
6. Cuando hayas revisado los cambios, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Comprueba si hay flujos de trabajo pendientes de aprobación.
8. Si los hay, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos de trabajo aparecen en la sección de comprobaciones de la PR. Si todo va bien, las comprobaciones del proyecto de la aplicación Astro se completarán correctamente. El proceso puede tardar unos minutos.

## Solicita cambios a GitHub Copilot

Puedes mencionar a Copilot en los comentarios de una PR o en los comentarios insertados en el código, igual que a otro miembro del equipo, para iniciar otra sesión que atienda tus solicitudes. Como los resultados no son deterministas, no hay un prompt único. Por ejemplo, puedes pedirle que:

- añada al principio de cada archivo de código un comentario breve que explique su propósito.
- añada comentarios TSDoc a los archivos TypeScript y Astro.
- cree un README que describa la estructura de la aplicación Astro.

1. Añade un comentario que solicite un cambio en la documentación generada y menciona a **@copilot**. Puedes utilizar una de las ideas anteriores o proponer otra mejora.
2. Selecciona **View Session** para observar cómo Copilot inicia otra sesión y aplica los cambios.
3. Selecciona **Back to pull request** para volver a la PR.

   ![Botón Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine, comprueba que la PR contiene una nueva confirmación.
5. Selecciona **Files changed** y revisa los cambios.

Puedes seguir iterando hasta que estés conforme. Después, convierte la PR de borrador en lista para revisión y combínala.

![Opción para convertir la PR en lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Vuelve a la PR que Copilot creó para mostrar juegos relacionados en la página de detalles.

1. Abre el repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la PR con un título similar a **Show related games on the game details page**.
4. Selecciona **Files changed** y revisa el código generado.
5. Cuando hayas terminado, vuelve a **Conversation** y desplázate hacia abajo.
6. Comprueba si hay flujos de trabajo pendientes de aprobación.
7. Si los hay, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. Comprueba que los flujos de trabajo se han añadido a las comprobaciones de la PR y que las comprobaciones del proyecto Astro se completan correctamente. Puede tardar unos minutos.
9. **Opcional:** cambia a la rama de la PR en el Codespace para probar manualmente la funcionalidad. En el terminal, sustituye `<branch-name>` por la rama creada por Copilot, por ejemplo, `copilot/fix-8`:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot ha creado la funcionalidad de juegos relacionados. Puedes pedirle cambios mediante un comentario en la pestaña **Conversation**. Por ejemplo, puedes ajustar la cantidad de juegos relacionados o pedir comentarios de archivo y TSDoc. Recuerda que esta incidencia se asignó antes de actualizar las instrucciones personalizadas.

## Revisa las funciones de accesibilidad

Por último, revisarás la funcionalidad de accesibilidad creada por el agente personalizado. La PR debería incluir el modo de alto contraste solicitado en la lección 3 y el modo claro solicitado desde Mission control en la lección 4.

1. Abre el repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la PR titulada, por ejemplo, **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot todavía trabaja en la tarea, la PR tendrá la etiqueta **[WIP]**. Espera a que termine; puede tardar unos minutos.

4. Selecciona **Files changed** y revisa el código generado.
5. Revisa la implementación y presta atención a:
   - los controles de interfaz para cambiar de modo.
   - el uso del almacenamiento local para guardar las preferencias.
   - los cambios de hojas de estilo en cascada (CSS) o de estilos para los modos de alto contraste y claro.
   - los atributos de accesibilidad, la navegación con teclado y las etiquetas de aplicaciones de Internet enriquecidas y accesibles (Accessible Rich Internet Applications, ARIA).
   - el código JavaScript o TypeScript que controla el cambio de modo.
6. Cuando hayas terminado, vuelve a **Conversation** y desplázate hacia abajo.
7. Comprueba si hay flujos de trabajo pendientes de aprobación.
8. Si los hay, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos de trabajo se han añadido a las comprobaciones de la PR y que las comprobaciones del proyecto Astro se completan correctamente.
10. **Opcional:** cambia a la rama de la PR en el Codespace para probar manualmente las funciones de accesibilidad:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   Inicia la aplicación y prueba los controles de alto contraste y de modo claro en el navegador. Confirma que funcionan y conservan la selección al volver a cargar la página.

El agente personalizado de accesibilidad ha orientado a Copilot para seguir buenas prácticas. Si detectas problemas o mejoras posibles, menciona a **@copilot** en un comentario y solicita los cambios.

## Ejercicio opcional: sigue delegando

El agente en la nube es útil para abordar elementos reales del backlog mientras te ocupas de otras tareas. Para practicar, crea más incidencias en el repositorio y asígnaselas a Copilot. Por ejemplo:

- crear un formulario de interés para patrocinadores en la página de detalles de un juego.
- implementar la paginación en la página de la lista de juegos.
- añadir validación de entradas y gestión de errores a los métodos de acceso a datos.

## Resumen

Has completado el entorno del agente en la nube. En estas lecciones:

- has revisado los archivos de instrucciones del repositorio y su efecto en el trabajo del agente.
- has asignado incidencias al agente en la nube y has observado cómo prepara el entorno, planifica y trabaja de forma asíncrona.
- has creado y utilizado un agente personalizado de accesibilidad para añadir los modos de alto contraste y claro.
- has utilizado la página de agentes de Copilot como Mission control para supervisar y dirigir una sesión en curso.
- has revisado e iterado sobre las PR del agente, has mencionado a `@copilot` para solicitar cambios y has aprobado los flujos de trabajo.

## Repaso y pasos siguientes

Has completado el entorno del agente en la nube. Para seguir explorando, puedes probar otros entornos:

- [Entorno de VS Code](../../vscode/): utiliza el modo de agente de Copilot Chat y la integración con MCP en el editor.
- [Entorno de interfaz de línea de comandos (CLI)](../../cli/): entrega dos cambios revisados desde el terminal con Plan, Autopilot, habilidades, un agente de QA, Playwright MCP, Agent Merge y el puente opcional `/delegate` con el agente en la nube.

En tu propio repositorio, también puedes:

- asignar al agente una incidencia de refactorización o cobertura de pruebas.
- crear un agente personalizado para otro ámbito.
- configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el firewall del agente en la nube][agent-firewall]

---

| [← Lección anterior: Administrar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
