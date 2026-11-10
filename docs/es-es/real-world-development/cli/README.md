---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli)** incorpora GitHub Copilot al terminal como asistente de programación con agentes. Explora repositorios, genera código, ejecuta comandos y se conecta al Model Context Protocol (MCP) y a otras herramientas externas desde la línea de comandos.

En este taller crearás una copia del proyecto Tailspin Toys y trabajarás en un codespace. Instalarás Copilot CLI, añadirás valoraciones por estrellas y, después, desarrollarás el filtrado de juegos a partir de una incidencia. Usarás los modos Plan y Autopilot, instrucciones personalizadas, una habilidad de comprobaciones, Playwright MCP y un agente de control de calidad (QA). A continuación, revisarás la funcionalidad y utilizarás Agent Merge para gestionar la solicitud de incorporación de cambios (PR). Por último, explorarás comandos de barra y una serie opcional de tres módulos con Foundry.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea una copia del repositorio Tailspin Toys y prepara un codespace |
| [1. Instalar GitHub Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI y encuentra la incidencia de filtrado |
| [2. Añadir valoraciones por estrellas: una mejora rápida][ex2] | Primer cambio | Actualiza las tarjetas de juegos y combina tu primera PR |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica e implementa el filtrado a partir de una incidencia |
| [4. Guiar a Copilot con instrucciones personalizadas][ex4] | Contexto | Actualiza las instrucciones del repositorio y aplícalas |
| [5. Personalizar la habilidad quality-checks][ex5] | Comprobaciones | Personaliza y ejecuta la habilidad de comprobaciones |
| [6. Validar la funcionalidad con Playwright MCP][ex6] | Herramientas externas | Usa Playwright MCP para explorar el filtrado en un navegador |
| [7. Crear y utilizar un agente de control de calidad][ex7] | Agentes | Crea un perfil de QA reutilizable y revisa sus hallazgos |
| [8. Crear y combinar la PR de la funcionalidad][ex8] | Revisión | Revisa la funcionalidad de filtrado y utiliza Agent Merge |
| [9. Comandos de barra de Copilot CLI][ex9] | Funciones de CLI | Explora el contexto, los modelos, el uso compartido y la delegación opcional |
| [10. Repaso y pasos siguientes][ex10] | Resumen | Repasa el flujo de trabajo de Copilot CLI |
| [Opcional: serie Foundry Backer Concierge][foundry] | Agentes hospedados | Prepara un modelo, crea y despliega un agente y conéctalo al sitio |

## Requisitos previos

Antes de empezar, asegúrate de disponer de:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Conocimientos básicos del terminal o la línea de comandos
- [ ] Git instalado y configurado

> [!TIP]
> Si no tienes un plan de pago, los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][education]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que se utilizan en este taller.

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, el administrador debe habilitar Copilot CLI.

## Comenzar

**[Empieza por el ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
[education]: https://github.com/education/students
