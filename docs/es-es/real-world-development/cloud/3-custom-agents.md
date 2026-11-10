---
title: "Lección 3: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de inteligencia artificial (IA) especializados en tareas o ámbitos concretos del desarrollo. Puedes definirlos en archivos Markdown de `.github/agents` e incluir instrucciones, prácticas recomendadas, patrones de codificación y conocimientos específicos. Así, los equipos pueden reutilizar su experiencia mediante agentes, por ejemplo, uno de accesibilidad que aplique las [pautas de accesibilidad para el contenido web (WCAG)][wcag], uno de seguridad o uno que mantenga patrones de pruebas coherentes.

Los agentes personalizados se definen en archivos Markdown de `.github/agents` dentro del proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML que incluye al menos `name` y `description`, seguido de un prompt en Markdown que define el comportamiento, la experiencia y las instrucciones del agente.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] comparten algunos aspectos: ambos se definen principalmente mediante archivos Markdown y explican a la IA cómo realizar tareas. Una forma sencilla de distinguirlos es que el **agente personalizado** es quien realiza el trabajo y las **habilidades** son las herramientas que puede utilizar.

Los agentes personalizados tienen su propia ventana de contexto y pueden coordinar habilidades e incluso otros agentes. En este taller, el agente personalizado de accesibilidad revisará y actualizará el sitio según las directrices de accesibilidad y podría utilizar habilidades para crear solicitudes de incorporación de cambios o ejecutar pruebas.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Como con cualquier herramienta de IA, prueba distintas opciones e itera para encontrar la que mejor funcione en tu entorno y escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En esta lección explorarás:

- cómo se definen los agentes personalizados.
- cómo asignar una tarea a un agente personalizado.

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas, independientemente de sus capacidades o preferencias visuales. Algunos usuarios han indicado que el tema oscuro actual es difícil de leer porque el contraste entre el texto y el fondo es insuficiente. El equipo de diseño ha solicitado un modo de alto contraste que se pueda activar y desactivar.

La accesibilidad es importante, así que utilizarás un agente personalizado para implementar esta funcionalidad rápidamente.

## Revisa el agente personalizado de accesibilidad

Ya hay un agente personalizado de accesibilidad. Revísalo para saber qué instrucciones proporcionará a Copilot.

1. Vuelve al Codespace y abre `.github/agents/accessibility.md`.
2. Revisa el frontmatter YAML y los campos `name` y `description`.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios para los agentes personalizados.

3. Revisa las secciones siguientes, que describen las responsabilidades principales, las prácticas recomendadas de accesibilidad, ejemplos de lenguaje de marcado de hipertexto (HTML), hojas de estilo en cascada (CSS) y JavaScript, y errores habituales.

## Crea y asigna una incidencia

Mission control es el centro para gestionar agentes del entorno. Desde allí puedes asignar tareas al agente en la nube, supervisarlas y proporcionar indicaciones adicionales. Asignarás una tarea para implementar el modo de alto contraste.

1. Abre el repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Add high contrast mode to website` en **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. Selecciona **Create** para crear la incidencia.
8. En el panel derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.
9. En la lista de agentes personalizados, selecciona **Accessibility agent**.

   ![Cuadro de asignación del agente en la nube con el agente personalizado Accessibility seleccionado](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.

Copilot empezará a trabajar en la tarea en segundo plano.

## Resumen y pasos siguientes

Has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes especializados en tareas y ámbitos concretos. Permiten codificar la experiencia y los estándares del equipo en agentes reutilizables.

En esta lección:

- has revisado cómo se definen los agentes personalizados.
- has asignado una tarea al agente personalizado.

Mientras Copilot implementa el modo de alto contraste, [supervisarás y dirigirás la sesión del agente][next-lesson] desde Mission control.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para utilizar agentes personalizados][org-custom-agents]
- [Preparar la empresa para utilizar agentes personalizados][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisar y administrar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
