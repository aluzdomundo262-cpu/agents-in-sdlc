---
title: "Lección 5 - Publicar el proyecto"
description: "Convierte el experimento local de Space Quiz en un repositorio público de GitHub."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-05
---

La publicación del Space Quiz permite gestionar incidencias, utilizar worktrees aislados y completar un flujo de trabajo de solicitudes de incorporación de cambios.

En esta lección:

- inicializarás la carpeta como repositorio de Git.
- crearás un repositorio público de GitHub y enviarás los cambios.
- vincularás el proyecto a GitHub en la aplicación Copilot.

## Publica el repositorio

> [!WARNING]
> Según la configuración de aprobación, el agente puede pedir confirmación antes de crear un repositorio o enviar código, o esas acciones pueden aprobarse automáticamente. Con **Approve all**, no esperes una solicitud de confirmación adicional. Antes de enviar el prompt de publicación, es importante revisar la configuración, la acción solicitada y el destino.

Estos pasos inicializan el repositorio, lo publican en GitHub y vinculan el proyecto a la aplicación:

1. Antes de enviar el prompt, revisa la configuración, la acción solicitada y el destino.
2. Envía el siguiente prompt:

   ```plaintext
   Initialize this folder as a Git repository, create an initial commit, and create a new public GitHub repository named space-quiz in my account. Push the current branch and set it as the default branch. Refresh the project within this app so the GitHub project is linked.
   ```

3. Cuando el agente termine, abre el nuevo repositorio en GitHub.
4. Confirma que `index.html` está presente.
5. Vuelve a la aplicación Copilot y confirma que el proyecto está vinculado al repositorio.

## Resumen y pasos siguientes

- Has inicializado la carpeta como repositorio de Git.
- Has creado un repositorio público de GitHub, enviado la rama actual y la has establecido como rama predeterminada.
- Has vinculado el proyecto a GitHub en la aplicación Copilot.

Continúa con la [lección 6: Trabajar con incidencias y sesiones][next-lesson].

[next-lesson]: ../6-issues-and-sessions/
