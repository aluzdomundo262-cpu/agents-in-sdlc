---
title: "Lección 2: Añadir valoraciones por estrellas, una mejora rápida"
description: "Haz un cambio pequeño con Copilot CLI, revisa el resultado en el navegador reenviado y combina tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ya has instalado Copilot CLI y probado una conversación. Ahora harás tu primer cambio en el proyecto: los datos de los juegos ya incluyen una valoración por estrellas, pero las tarjetas de la página principal todavía no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo combinarás como tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una conversación específica de Copilot en una rama de funcionalidad.
- pedirás al agente que realice un cambio pequeño en el proyecto.
- revisarás el cambio con `/diff`.
- ejecutarás la aplicación y comprobarás el cambio en un navegador reenviado.
- abrirás y combinarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración por estrellas, que ya aparece en la página de detalles. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, la editorial y la descripción. Como primer ejercicio, pedirás al agente que muestre en cada tarjeta la valoración existente. Es un cambio pequeño y autónomo, adecuado para la primera sesión.

## Cómo funciona una conversación

Una **conversación** es el espacio donde trabajas con Copilot CLI en una tarea. A diferencia de la aplicación Copilot, una conversación normal de CLI utiliza el repositorio y la rama de Git seleccionados en el terminal, en lugar de crear un worktree dedicado. Las conversaciones guardadas permiten volver al mismo intercambio; los archivos y la rama siguen siendo el estado habitual de Git en el disco.

En una conversación verás tus prompts y las respuestas del agente, la actividad de las herramientas mientras explora y edita archivos, y los cambios que puedes inspeccionar con `/diff`.

## Inicia una conversación y solicita el cambio

Inicia una conversación nueva para comenzar a implementar la funcionalidad.

1. Vuelve a tu Codespace.
2. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Si Copilot CLI aún no está abierto, ejecuta este comando:

   ```bash
   copilot --yolo
   ```

4. Inicia una sesión nueva con `/new` y pulsa <kbd>Enter</kbd>.
5. Usa este prompt para solicitar el cambio:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot explora el proyecto, localiza los archivos que muestran los detalles de los juegos y crea el código necesario.

## Revisa el diff

Revisa todos los cambios generados por IA antes de combinarlos, aunque sean pequeños.

1. Escribe `/diff` e inspecciona todos los archivos modificados.
2. Confirma que la tarjeta muestra la valoración numérica cuando existe y `No rating yet` cuando `starRating` es `null`.
3. Confirma que las pruebas cubren ambos casos.
4. Revisa los resultados de las comprobaciones y pide a Copilot que corrija los fallos.
5. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la vista del diff.

> [!NOTE]
> Copilot, como todas las herramientas de IA generativa, es probabilístico, no determinista. El código puede variar; revisa el comportamiento en lugar de esperar una implementación idéntica.

## Comprueba los cambios

Ejecuta el sitio y examina la interfaz de usuario (UI) actualizada en el navegador que reenvía Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Confirma que las tarjetas de juegos muestran la valoración sobre cinco.
4. Vuelve a Copilot y pídele que detenga el servidor que inició:

   ```plaintext
   Stop the development server you started.
   ```

## Abre y combina tu primera solicitud de incorporación de cambios

Has implementado la funcionalidad. Ahora crea una solicitud de incorporación de cambios (PR) para integrarla en el proyecto.

1. Pide al agente predeterminado que confirme el cambio:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Escribe `/pr create`. Copilot CLI publica la confirmación existente al crear la PR y muestra su URL.
3. Abre la PR manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando la URL que muestra Copilot CLI.
4. Revisa los archivos modificados y las comprobaciones.
5. Cuando esté todo listo, selecciona **Merge pull request** y confirma la combinación.
6. Vuelve al Codespace y sal de Copilot CLI con `/exit`.
7. Actualiza tu rama local `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumen y pasos siguientes

En esta lección:

- has iniciado una conversación específica de Copilot en una rama de funcionalidad.
- has pedido al agente que realice un cambio pequeño en las tarjetas de juegos.
- has revisado el cambio con `/diff`.
- has ejecutado la aplicación y comprobado la valoración por estrellas en el navegador reenviado.
- has abierto y combinado tu primera PR.

A continuación, [partirás de la incidencia de filtrado y utilizarás los modos Plan y Autopilot][next-lesson] para implementar una funcionalidad más amplia.

## Recursos

- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
