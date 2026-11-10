---
title: "Lección 10: Repaso y pasos siguientes"
description: "Repasa el flujo de trabajo con Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI durante un flujo de trabajo continuo en Tailspin Toys. En este taller:

- has preparado un Codespace, instalado Copilot CLI, explorado el proyecto y encontrado la incidencia de filtrado.
- has añadido las valoraciones por estrellas, revisado el resultado en un navegador reenviado y combinado manualmente tu primera solicitud de incorporación de cambios (PR).
- has partido de la incidencia de filtrado, definido el enfoque en modo Plan, implementado la funcionalidad en modo Autopilot y revisado el resultado en modo Interactive.
- has guiado al agente con instrucciones personalizadas, personalizado la habilidad `quality-checks` y utilizado la habilidad para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- has añadido el servidor Model Context Protocol (MCP) de Playwright y lo has utilizado para explorar el filtrado en un navegador real.
- has creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas del navegador.
- has revisado los cambios completos del filtrado y autorizado Agent Merge para combinar la PR correspondiente.
- has explorado comandos de barra para el contexto, los modelos, el uso compartido y la delegación opcional en la nube.

## Lo que has entregado

El taller incluye dos hitos de PR, cada uno en su propia rama creada a partir de `main` actualizado:

1. **Valoraciones por estrellas:** muestra `starRating` y un estado explícito cuando no hay una valoración en las tarjetas de juegos.
2. **Filtrado y flujo de calidad:** implementa el filtrado, actualiza las instrucciones y las aplica a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de QA e incluye las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su PR, has utilizado la misma conversación y rama. Para agilizar el taller, hemos agrupado ese trabajo en una sola PR.

## Diferentes tipos de validación

Has comprobado el código de varias maneras: con pruebas automatizadas, mediante tu propia revisión en el navegador y con la exploración del navegador de Copilot mediante MCP. La habilidad `quality-checks` ejecutó las pruebas unitarias, el lint y las comprobaciones de tipos e informó de los resultados con el nuevo formato. QA combinó esos resultados con una revisión de los requisitos y de la cobertura antes de la PR.

Las pruebas nuevas deben cubrir carencias reales; una ejecución de QA que no necesite pruebas adicionales también puede ser correcta. Revisa el código y las pruebas antes de autorizar la combinación, y actualiza la evidencia afectada después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas influyen en el trabajo de Copilot. En este taller has actualizado instrucciones, personalizado una habilidad, creado un perfil de control de calidad (QA) y configurado un servidor de Model Context Protocol (MCP). Reutiliza y adapta estas personalizaciones a las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados de las herramientas, no solo el resumen del agente.

Elige el **modo y el modelo** adecuados para cada tarea. Usa **Plan** para definir un enfoque antes de implementar, **Interactive** para colaborar en cambios acotados y **Autopilot** para tareas bien definidas. Elige un modelo más rápido para ediciones rutinarias y uno más capaz para tareas complejas.

El contexto sigue siendo tan importante como las herramientas. Describir con claridad *qué* hay que crear, *por qué* y *cómo* influye de forma importante en el resultado.

## Más funciones que explorar

Has completado el flujo principal. Estas son algunas funciones más de CLI que puedes probar:

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para explicar un problema y obtener otra perspectiva.
- `/fleet` para coordinar tareas independientes en paralelo.
- `/worktree` para aislar otra tarea.
- `/delegate` para enviar una tarea al agente en la nube de Copilot.

## Pasos siguientes

La mejor forma de mejorar con una herramienta es seguir utilizándola: en código de producción, en proyectos personales o para crear una aplicación que tengas pendiente desde hace tiempo. Comparte lo que aprendas con el equipo y sigue explorando la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la [serie opcional Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora los talleres de [VS Code][vscode], la [aplicación GitHub Copilot][app] o el [agente en la nube de Copilot][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
