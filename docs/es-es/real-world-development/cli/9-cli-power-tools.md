---
title: "Lección 9: Comandos de barra de GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar tareas opcionalmente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

GitHub Copilot CLI incluye muchos comandos de barra para mostrar funciones avanzadas, información de la sesión y opciones de configuración. Ya has utilizado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora explorarás otros comandos útiles.

En esta lección:

- utilizarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- utilizarás `/model` para explorar los modelos disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar worktrees y delegar tareas en el agente en la nube.

## Escenario

Has completado el flujo principal de CLI. Ahora explorarás algunas funciones adicionales: administrar el contexto, cambiar de modelo, compartir sesiones y delegar tareas opcionalmente en el [agente en la nube de Copilot][about-cloud-agent].

## Explora el contexto de Copilot CLI

En tareas amplias o complejas, puede que alcances la ventana máxima de contexto del modelo. Copilot CLI compacta la conversación cuando es necesario; también puedes inspeccionarla y compactarla manualmente.

1. Vuelve al Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y la distribución del contexto entre instrucciones del sistema, herramientas, mensajes y espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Si la conversación ya es pequeña, puede que apenas cambie.

> [!NOTE]
> Copilot CLI compacta el contexto automáticamente cuando la ventana se llena. Utiliza `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` para empezar una conversación nueva al cambiar a una tarea no relacionada.

## Elige un modelo

Los modelos tienen distintas capacidades y cada desarrollador puede tener preferencias diferentes. Copilot CLI permite mostrar los modelos disponibles y seleccionar uno.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información de uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Compartir el trabajo y los aprendizajes ayuda al equipo a mejorar el uso de las herramientas de IA. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartir o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` disponibles en tu versión.
2. Si quieres compartir la sesión, elige el destino adecuado, por ejemplo, `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo o publicarlo. Las exportaciones pueden incluir prompts, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de la conversación que el equipo no quiera compartir.

## Opcional: amplía el trabajo o delégalo

El flujo principal del taller ha terminado. Copilot CLI también ofrece comandos para tareas más amplias:

- `/fleet` puede dividir tareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un worktree de Git aislado para otra tarea.
- `/delegate` puede enviar una tarea al agente en la nube de Copilot, que trabaja de forma asíncrona y puede abrir una PR.

Estos comandos son opcionales porque pueden crear worktrees adicionales o trabajo remoto. Antes de probarlos, inicia una tarea nueva y acotada, y revisa los resultados mediante el flujo de trabajo habitual. Para obtener más información sobre el trabajo asíncrono con agentes, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y pasos siguientes

En esta lección:

- has utilizado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- has utilizado `/model` para explorar los modelos disponibles.
- has aprendido cómo `/share` puede exportar o compartir una sesión.
- has explorado comandos opcionales para el trabajo en paralelo, los worktrees y la delegación al agente en la nube.

A continuación, [repasarás lo aprendido][next-lesson] y descubrirás los siguientes pasos.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Administración del contexto en Copilot CLI][context-management]
- [Acerca del agente en la nube de Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
