---
title: "Lección 8 - Completar el ciclo de revisión de Copilot"
description: "Crea una solicitud de incorporación de cambios, solicita una revisión de Copilot, atiende los comentarios pertinentes y deja que Agent Merge mantenga la solicitud en buen estado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-05
---

La incidencia implementada pasa a una solicitud de incorporación de cambios (PR), que se somete a una revisión de Copilot y se actualiza con los comentarios pertinentes antes de fusionarla.

En esta lección:

- inspeccionarás los cambios de la sesión por última vez.
- crearás una solicitud de incorporación de cambios desde la sesión del agente.
- solicitarás una revisión de código de Copilot.
- revisarás y aplicarás los comentarios que requieran cambios.
- activarás Agent Merge para mantener la solicitud de incorporación de cambios en buen estado hasta que se fusione.

## Crea y revisa la solicitud de incorporación de cambios

La revisión empieza por inspeccionar los cambios de la sesión y termina al resolver los comentarios pertinentes:

> [!IMPORTANT]
> Copilot Free no incluye la revisión de código de Copilot para solicitudes de incorporación de cambios. Copilot Student y algunos planes de pago de Copilot sí la incluyen. Una organización también puede habilitar la revisión de código de pago en GitHub.com para miembros sin una licencia de Copilot. La [disponibilidad de la revisión de código de Copilot][code-review] detalla estas opciones.
>
> Si no tienes acceso:
>
> 1. Utiliza Copilot Student o un plan de pago de Copilot que incluya la revisión de código. Una organización también puede habilitar la revisión de código de pago en GitHub.com para miembros sin una licencia de Copilot.
> 2. Si sigues sin tener acceso, completa los pasos 1-4, revisa las diferencias tú mismo o pide a un compañero que las revise y omite los pasos 5-9, que dependen de los comentarios de revisión de Copilot.
> 3. Atiende los comentarios de los revisores humanos y vuelve a probar la funcionalidad antes de continuar con la sección de fusión.

1. Abre el panel desplegable de la derecha y selecciona la pestaña **Changes** para inspeccionar los archivos modificados en la sesión.
2. Selecciona **Create PR** en la barra de herramientas de la sesión.
3. Revisa el título y la descripción generados y crea la solicitud de incorporación de cambios.
4. Abre la solicitud de incorporación de cambios en GitHub.
5. Desde el menú **Reviewers**, solicita una revisión de **Copilot**.
6. Abre la pestaña **Files changed** y lee todos los comentarios de revisión.
7. Para cada comentario que requiera un cambio, utiliza la acción **Fix** de Copilot en la aplicación o realiza el cambio tú mismo.
8. Revisa cada cambio y vuelve a probar la funcionalidad.
9. Responde con una descripción concisa de lo que ha cambiado y resuelve la conversación.

> [!NOTE]
> Si una sugerencia no es aplicable o queda fuera del alcance de la solicitud de incorporación de cambios:
>
> 1. Responde con el motivo en lugar de realizar un cambio innecesario.
> 2. Resuelve todas las conversaciones de revisión antes de fusionar.

## Fusiona con Agent Merge

Agent Merge puede mantener la PR en buen estado hasta que se fusione; también puedes completar la fusión manualmente. Elige una de estas opciones:

1. Activa **Agent Merge** para la PR. El agente atenderá los comentarios de revisión, corregirá las comprobaciones que fallen y resolverá los conflictos a medida que aparezcan; después, fusionará la solicitud cuando todo pase.
2. Si prefieres fusionarla tú mismo, revisa las diferencias finales, comprueba la funcionalidad y fusiónala cuando pasen todas las comprobaciones.

## Resumen y pasos siguientes

- Has inspeccionado por última vez los cambios de la sesión.
- Has creado una PR desde la sesión del agente.
- Has solicitado una revisión de código de Copilot.
- Has revisado y aplicado los comentarios pertinentes.
- Has activado Agent Merge para mantener la PR en buen estado hasta que se fusione.

Continúa con la [lección 9: Automatizar la clasificación de incidencias][next-lesson].

[code-review]: https://docs.github.com/copilot/concepts/agents/code-review
[next-lesson]: ../9-automations/
