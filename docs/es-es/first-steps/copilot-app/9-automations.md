---
title: "Lección 9 - Automatizar la clasificación de incidencias"
description: "Crea y ejecuta una automatización semanal que resuma las incidencias abiertas recientes."
authors:
  - jamesmontemagno
lastUpdated: 2026-09-28
---

Una automatización convierte la clasificación recurrente de incidencias en un flujo de trabajo programado del agente.

En esta lección:

- crearás una automatización semanal.
- conectarás la automatización al proyecto Space Quiz.
- ejecutarás la automatización de inmediato y revisarás el resultado.

## Crea la automatización

![Ilustración de la vista Automations de la aplicación Copilot con los filtros All, Local y Cloud, un cuadro de búsqueda, los botones Templates y New automation y dos tarjetas de automatización semanal para el proyecto space-quiz: Issue triage (clasificación de incidencias) y Accessibility audit (auditoría de accesibilidad).](../../../_images/first-steps-app-automations.svg)

Las automatizaciones ejecutan el mismo prompt según una programación, cada una en su propia sesión, así que ninguna altera tu trabajo. Puedes filtrar por **All**, **Local** o **Cloud** y ejecutar cualquier automatización cuando lo necesites.

1. Abre **Automations**.
2. Elige la plantilla para una nueva automatización semanal.
3. Introduce el siguiente prompt:

   ```plaintext
   Review the latest GitHub issues created and still open in the last week, and provide a summary table ranked by severity and priority.
   ```

4. Establece el modo de sesión en **Autopilot**.
5. Establece el modelo en **Auto**.
6. Selecciona el proyecto `space-quiz`.
7. Abre el menú desplegable **Create** y selecciona **Create and run**.
8. Revisa el resumen generado y confirma que hace referencia a las incidencias abiertas recientes del repositorio.

## Resumen y pasos siguientes

- Has creado una automatización semanal.
- Has conectado la automatización al proyecto Space Quiz.
- Has ejecutado la automatización de inmediato y revisado el resultado.

Continúa con la [lección 10: Continuar una sesión de forma remota][next-lesson].

[next-lesson]: ../10-remote/
