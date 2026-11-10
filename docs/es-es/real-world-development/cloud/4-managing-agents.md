---
title: "Lección 4: Supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En las últimas lecciones has asignado tres tareas distintas al agente en la nube de Copilot para mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente trabaja de forma asíncrona y autónoma, es importante supervisar las tareas.

Puedes administrar las tareas desde la [página de agentes][agents-page] de GitHub.com, que funciona como Mission control. Allí verás las tareas con solicitudes de incorporación de cambios (PR) abiertas, las operaciones realizadas y las sesiones en curso, a las que puedes proporcionar más indicaciones.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube.
- dirigirás una sesión en curso para solicitar una funcionalidad adicional.

## Escenario

Después de asignar al agente la implementación del modo de alto contraste, el equipo decide añadir también un modo claro. Como ya se están actualizando los estilos del sitio y añadiendo controles de modo, pedirás al agente que incluya el modo claro además del modo de alto contraste.

## Revisa las tareas del agente en la nube

Consulta el estado de las tareas que tiene asignadas el agente en la nube de Copilot.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa las tareas del panel principal y del panel izquierdo. Deberías ver las tareas que has asignado a Copilot, entre ellas:
   - actualizar la documentación del código.
   - generar interfaces de programación de aplicaciones (API) para modificar juegos.
   - añadir un modo de alto contraste al sitio.
3. Selecciona una tarea en curso y revisa las operaciones que ha realizado Copilot, como obtener el código del repositorio, preparar el entorno, configurar servidores de Model Context Protocol (MCP) y completar la tarea.

> [!NOTE]
> Los pasos concretos varían según el estado de la tarea y el enfoque utilizado por Copilot.

4. Revisa también el panel de PR, que aparece a la derecha y muestra la PR y los archivos modificados.

## Dirige al agente en la nube

Ahora que has visto las tareas activas, pide a Copilot que añada el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto depende del nombre que le haya dado Copilot y del estado del trabajo.

   ![Sesión de accesibilidad en Mission control](../../../_images/ex6-accessibility-session.png)

2. Espera unos minutos a que termine la configuración y empiece el trabajo. Lo sabrás cuando aparezcan mensajes que indiquen que ha comenzado la implementación.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Tarea del agente en la nube con el cuadro de diálogo Steer active session while Copilot is working resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Comprueba que Copilot reconoce la indicación y la incorpora al flujo de trabajo.

## Deja que Copilot trabaje

Copilot incorporará la nueva solicitud al completar el paso en curso. El proceso puede tardar varios minutos; mientras tanto, puedes repasar lo aprendido.

## Resumen y pasos siguientes

Has explorado la página de agentes de Copilot, el centro para supervisar y dirigir las tareas del agente en la nube. Puedes realizar el seguimiento de las tareas activas y completadas, revisar el trabajo y cambiar el alcance o proporcionar indicaciones adicionales a una sesión en curso.

En esta lección:

- has explorado Mission control y la página de agentes para supervisar las tareas.
- has dirigido una sesión en curso para pedir una funcionalidad adicional.

Mientras Copilot termina los cambios de accesibilidad, [revisarás e iterarás sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
