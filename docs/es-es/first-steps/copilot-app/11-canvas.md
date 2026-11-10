---
title: "Lección 11 - Explorar un Canvas"
description: "Instala un Canvas de Repository Issues Kanban e inicia una sesión desde una tarjeta de incidencia."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Un **Canvas** es un espacio bidireccional compartido donde puedes actualizar con un agente el mismo plan, tablero, lista de comprobación o panel. El Canvas Kanban de esta lección convierte las incidencias del repositorio en un flujo de trabajo visual.

En esta lección:

- instalarás una extensión de Canvas.
- conectarás el Canvas al repositorio de Space Quiz.
- moverás una incidencia al trabajo activo.
- inspeccionarás la sesión creada a partir de la incidencia.

## Instala el Canvas de Repository Issues Kanban

La extensión debe estar instalada antes de conectarla al repositorio:

1. Explora la [galería de extensiones de Canvas][canvas-gallery].
2. Abre la [extensión Repository Issues Kanban][kanban-extension].
3. Selecciona **Install in GitHub Copilot app** y aprueba la instalación.
4. En la aplicación, abre **Customize** y después **Canvas**.
5. Confirma que la extensión está instalada.

## Empieza a trabajar desde el Canvas

El tablero permite iniciar una sesión centrada en una incidencia y comprobar qué contexto recibe:

1. Selecciona **New session** para el Canvas.
2. Elige el proyecto `space-quiz`.
3. Explora el tablero de incidencias.
4. Mueve una tarjeta de incidencia a la columna de trabajo activo.
5. Abre la sesión generada automáticamente.
6. Confirma que la incidencia seleccionada está disponible como contexto de la sesión.

![Ilustración del Canvas de Repository Issues Kanban con las columnas Backlog, Plan, Ready e Implement. La tarjeta de la incidencia 13, «Review screen» (pantalla de revisión), se arrastra de Backlog a Plan, mientras que la incidencia 12, «Per-question timer» (temporizador por pregunta), permanece en Backlog.](../../../_images/first-steps-app-canvas-kanban.svg)

Al colocar una tarjeta en una columna, el Canvas entrega esa incidencia a una nueva sesión con la incidencia ya cargada.

> [!NOTE]
> La extensión actual de Repository Issues Kanban mueve las tarjetas mediante arrastrar y soltar con un ratón u otro dispositivo señalador. Si no puedes utilizar esa interacción:
>
> 1. Anota el número de la incidencia en el tablero.
> 2. Abre la incidencia desde **Issues**.
> 3. Selecciona **New session**. Esto crea la misma sesión basada en la incidencia sin mover la tarjeta.

El Canvas ofrece una forma visual de seleccionar y comenzar el trabajo mientras mantiene al agente centrado en la incidencia.

## Resumen y pasos siguientes

- Has instalado una extensión de Canvas.
- Has conectado el Canvas al repositorio Space Quiz.
- Has movido una incidencia al trabajo activo.
- Has inspeccionado la sesión creada desde la incidencia.

Continúa con la [lección 12: Publicar el sitio con GitHub Pages][next-lesson].

[canvas-gallery]: https://awesome-copilot.github.com/extensions/
[kanban-extension]: https://awesome-copilot.github.com/extension/accessibility-kanban/
[next-lesson]: ../12-deploy-pages/
