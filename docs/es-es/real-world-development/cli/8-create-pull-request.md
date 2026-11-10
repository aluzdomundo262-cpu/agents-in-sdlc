---
title: "Lección 8: Crear y combinar la solicitud de incorporación de cambios de la funcionalidad"
description: "Revisa el filtrado, las instrucciones, la habilidad, el perfil de control de calidad (QA) y las pruebas; después crea una solicitud de incorporación de cambios y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las instrucciones, la actualización de la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Ahora revisarás los cambios en conjunto y abrirás una solicitud de incorporación de cambios (PR). La PR de las valoraciones por estrellas la combinaste manualmente; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> En condiciones normales, separarías la funcionalidad, las instrucciones, la actualización de la habilidad y el agente de QA en varias PR. Para agilizar el taller, has mantenido todo el flujo del filtrado y de calidad en una conversación y una rama.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- inspeccionarás todos los cambios de la funcionalidad y las pruebas de verificación.
- crearás la PR del filtrado.
- habilitarás Agent Merge solo después de revisar los cambios y confirmarás que la PR se ha combinado.

## Escenario

Durante el flujo del filtrado has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la PR, pero mantener bajo el control del desarrollador la autorización para combinarla.

## Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de incorporación de cambios. Cuando lo habilitas, Copilot resuelve los bloqueos de la PR —como las comprobaciones de integración continua (CI) fallidas, los comentarios de revisión y las reorganizaciones de la rama— y, si el repositorio lo permite, habilita la combinación automática de GitHub.

Hasta ahora has seleccionado **Merge pull request** manualmente. Agent Merge puede encargarse de ese proceso, pero debes revisar el trabajo y confirmar que está listo antes de habilitarlo.

## Utiliza Agent Merge para gestionar la PR

Revisa el código, crea la PR y permite que Agent Merge se ocupe del resto.

1. Vuelve al Codespace.
2. Abre el diálogo de agentes con `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR con `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la PR y la combinará cuando se completen correctamente todas las comprobaciones.
7. Confirma que Copilot muestra un mensaje similar a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si el proceso se bloquea, revisa el motivo indicado y completa manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y pasos siguientes

Has automatizado partes del desarrollo, desde la generación y validación del código hasta el proceso de PR. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- has inspeccionado todos los cambios de la funcionalidad y las pruebas de verificación.
- has creado la PR del filtrado.
- has habilitado Agent Merge después de revisar los cambios y confirmado que la PR se ha combinado.

A continuación, [explorarás más comandos de barra de Copilot CLI][next-lesson] para gestionar el contexto, los modelos, el uso compartido y la delegación opcional en la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
