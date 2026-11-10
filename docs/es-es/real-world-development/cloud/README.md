---
slug: es-es/real-world-development/cloud
title: "Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El **[agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** permite que GitHub Copilot trabaje de forma asíncrona en la nube. Asigna trabajo en GitHub y el agente en la nube lo realiza en segundo plano: explora el repositorio, hace cambios y abre una solicitud de incorporación de cambios mientras tú te ocupas de otras tareas.

En estos ejercicios añadirás instrucciones personalizadas para el agente y le asignarás una incidencia de GitHub. Revisarás y utilizarás agentes personalizados para orientar su trabajo, supervisarás y dirigirás las sesiones desde el panel de agentes y, por último, revisarás sus solicitudes de incorporación de cambios e iterarás sobre los resultados.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y un codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade instrucciones para el agente en la nube |
| [2. Agente en la nube][ex2] | Agente asíncrono | Asigna incidencias al agente en la nube de Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revisa y utiliza agentes personalizados |
| [4. Administrar agentes][ex4] | Supervisión | Supervisa y dirige las sesiones de agente |
| [5. Iterar][ex5] | Revisión | Revisa las solicitudes de incorporación de cambios (PR), itera sobre el trabajo de Copilot y decide los siguientes pasos |

## Requisitos previos

Antes de empezar, asegúrate de disponer de:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] El agente en la nube de Copilot habilitado para tu cuenta u organización

> [!TIP]
> Si no tienes un plan de pago, los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][education]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que se utilizan en este taller.

> [!NOTE]
> El agente en la nube está disponible en todos los planes indicados, excepto Copilot Free. En Copilot Business o Copilot Enterprise, el administrador debe habilitarlo para la organización.

> [!NOTE]
> Este entorno no incluye Model Context Protocol (MCP). Para aprender a utilizar servidores MCP con Copilot, consulta los talleres de [CLI][cli] o [VS Code][vscode].

## Comenzar

**[Empieza por el ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[education]: https://github.com/education/students
[cli]: ../cli/
[vscode]: ../vscode/
