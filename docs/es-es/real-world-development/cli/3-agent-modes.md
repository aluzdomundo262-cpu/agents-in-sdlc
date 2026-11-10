---
title: "Lección 3: Modos de agente: Plan y Autopilot"
description: "Define un enfoque con Plan, implementa el filtrado desde una incidencia con Autopilot y revisa el resultado en modo Interactive."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Empezaste añadiendo una funcionalidad pequeña al proyecto. Los cambios más amplios requieren un proceso más sólido. En esta lección seguirás un flujo de desarrollo con agentes: partirás de una incidencia para planificar e implementar una funcionalidad, comprobarás el código y validarás el comportamiento.

> [!NOTE]
> Utilizarás la misma conversación y rama durante el flujo de trabajo de esta funcionalidad. En un proyecto habitual, probablemente separarías los cambios en varias ramas o solicitudes de incorporación de cambios. En este taller los mantendrás juntos para centrarte en los conceptos principales.

En esta lección:

- iniciarás una conversación de Copilot desde una incidencia de GitHub.
- definirás los requisitos en modo Plan.
- implementarás la funcionalidad en modo Autopilot.
- revisarás el código.
- validarás manualmente la funcionalidad en un navegador reenviado.

Al continuar con esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad `quality-checks`, añadirás validación mediante MCP, crearás un agente de QA y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar los juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero es necesario acordar detalles como la combinación de categorías antes de escribir código. Utilizarás el modo Plan para decidir esos detalles y, después, autorizarás una implementación acotada con Autopilot.

## Introducción

Los agentes de programación con inteligencia artificial (IA) no cambian los principios básicos del desarrollo. Un flujo de trabajo habitual suele incluir estos pasos:

1. Partir de una incidencia que describa el trabajo.
2. Planificar lo que hay que desarrollar.
3. Implementar y revisar el código.
4. Ejecutar pruebas para validar el código.
5. Validar manualmente la funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Combinar el código después de que se revise y se completen correctamente las comprobaciones de integración continua (CI).

> [!NOTE]
> Los detalles varían según el equipo y la organización, pero la mayoría de los procesos siguen un patrón parecido.

Seguir este enfoque ayuda a comprobar que el código generado por IA cumple los requisitos y pasa por las mismas revisiones que el código escrito manualmente.

## Modos de conversación

El **modo de conversación** controla el grado de autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo:

- **Interactive**: colaboras con el agente. Propone cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente prepara primero un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma, escribe código, ejecuta pruebas e itera hasta considerar que la tarea está terminada.

Empieza en modo Plan, revisa el plan y, después, usa Autopilot para implementarlo.

## Parte de la incidencia

Antes de empezar a trabajar en el filtrado, vuelve al Codespace y comprueba que el repositorio y el terminal están preparados.

1. Vuelve al Codespace. Si está detenido, reinícialo.
2. Confirma que la PR de valoraciones por estrellas está combinada.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Usa las teclas de dirección para resaltar **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al prompt y volver a la pestaña **Session**.

El prompt debería empezar por `#7` (o un número similar). El prefijo `#` permite añadir al contexto una incidencia o PR de GitHub.

## Planifica la funcionalidad de filtrado

La planificación permite acordar cómo implementar una funcionalidad o realizar una tarea antes de delegarla a Copilot. Para los trabajos complejos, conviene dedicar tiempo a planificar.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Plan. Confirma que el indicador debajo del prompt muestra **Plan**.
2. Después de la referencia a la incidencia que añadiste en el paso anterior, escribe:

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot explorará el proyecto y determinará el enfoque. Puede preguntarte cómo deben funcionar los filtros. Responde según tus preferencias; no hay una única respuesta correcta.

3. Cuando termine el plan, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandirlo.
4. Revisa el plan y pide a Copilot que modifique cualquier parte que no refleje tus decisiones.

## Autoriza Autopilot

Una vez redactado y revisado el plan, puedes pedir a Copilot que lo implemente.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente de tu versión.
2. Confirma que el indicador debajo del prompt muestra **Autopilot**.
3. Observa cómo Copilot sigue el plan, genera código y ejecuta pruebas.

> [!NOTE]
> Al aprobarlo, la implementación puede empezar de inmediato, así que revisa primero el plan. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar por completas las comprobaciones.

## Revisa y comprueba la implementación

Revisa el código generado antes de combinarlo, como harías con cualquier otro cambio.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar en modo Interactive. Comprueba que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Escribe `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones de planificación.
4. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la vista del diff.
5. Revisa los resultados de las comprobaciones del proyecto y pide a Copilot que corrija los fallos.

## Explora la funcionalidad

Inicia la aplicación y abre el sitio a través del puerto reenviado por Codespaces para comprobar que funciona.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros de categoría y editorial, así como las combinaciones que acordaste en el plan.
4. Comprueba que el restablecimiento y los resultados vacíos coinciden con la incidencia y tus decisiones.
5. Vuelve al Codespace y pide a Copilot que detenga el servidor de desarrollo que inició.

## Resumen y pasos siguientes

En esta lección:

- has iniciado una conversación nueva de Copilot desde una incidencia de GitHub.
- has definido los requisitos en modo Plan.
- has implementado la funcionalidad en modo Autopilot.
- has revisado el código.
- has validado manualmente la funcionalidad en un navegador reenviado.

A continuación, [explorarás cómo se genera el código mediante instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
