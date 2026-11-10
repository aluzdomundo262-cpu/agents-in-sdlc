---
title: "Lección 8 - Revisar y fusionar"
description: "Crea una solicitud de incorporación de cambios desde Source Control, solicita una revisión de código de Copilot, resuelve los comentarios con las herramientas de GitHub y fusiónala."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-05
---

Inspecciona, revisa y fusiona los cambios nuevos con las herramientas de GitHub en Visual Studio Code (VS Code).

En esta lección:

- crearás un commit con el nuevo trabajo y una solicitud de incorporación de cambios desde **Source Control**.
- solicitarás una revisión de código de Copilot.
- resolverás los comentarios y las comprobaciones que fallen con el servidor de Model Context Protocol (MCP) de GitHub.
- fusionarás la solicitud de incorporación de cambios.

## Inspecciona, revisa y fusiona

> [!IMPORTANT]
> Copilot Free no incluye la revisión de código de Copilot para solicitudes de incorporación de cambios. Utiliza Copilot Student o un plan de pago de Copilot que incluya la revisión de código. Una organización también puede habilitar la revisión de código de pago en GitHub.com para miembros sin una licencia de Copilot, pero esto no concede acceso a la revisión de código en los entornos de desarrollo integrados (IDE). Consulta la [disponibilidad de la revisión de código de Copilot][code-review].
>
> Si no tienes acceso, omite la solicitud de revisión de Copilot del paso 4. Revisa las diferencias tú mismo o pide a un compañero que las revise y continúa con los pasos restantes, resolviendo los comentarios de los revisores humanos y volviendo a probar antes de fusionar.

1. Abre **Source Control** para inspeccionar los archivos modificados y las diferencias antes de crear nada.
2. Crea un commit con el nuevo trabajo y vuelve a utilizar el botón con destellos para redactar el mensaje.
3. Selecciona el botón **Create Pull Request** que aparece en **Source Control**. Copilot redacta el título y la descripción a partir de tus commits, así que obtienes una solicitud de incorporación de cambios mejor que si la pides desde cero.
4. Solicita una **revisión de código de Copilot** mientras creas la solicitud de incorporación de cambios, desde la vista **GitHub** de VS Code o en GitHub.
5. Pide a Copilot, con GitHub MCP, que inspeccione la solicitud de incorporación de cambios, resuelva los conflictos de fusión, responda a los comentarios de revisión e investigue las comprobaciones de integración continua (CI) que fallen.
6. Vuelve a probar en el navegador integrado, revisa cada cambio propuesto y actualiza la rama.
7. Cuando las comprobaciones y la revisión hayan terminado, pide al agente que fusione la solicitud o fusiónala desde la integración de GitHub.

> [!NOTE]
> Siempre puedes pedir a Copilot que haga esto desde el chat. Merece la pena aprender primero la vía de **Source Control**, porque redacta por ti el texto del commit y de la solicitud de incorporación de cambios a partir de lo que ha cambiado realmente.

## Resumen y pasos siguientes

Has revisado y fusionado una solicitud de incorporación de cambios sin salir de VS Code. Continúa con la [lección 9: Entregar la siguiente idea a una sesión en la nube][next-lesson].

[code-review]: https://docs.github.com/copilot/concepts/agents/code-review
[next-lesson]: ../9-cloud-session/
