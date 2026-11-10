---
title: "Lección 0: Requisitos previos y configuración"
description: "Comprueba los requisitos previos, instala la aplicación GitHub Copilot y familiarízate con su espacio de trabajo."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-05
---

Antes de crear el Space Quiz, confirma que tienes todo lo necesario, instala la aplicación GitHub Copilot y familiarízate con su espacio de trabajo.

En esta lección:

- comprobarás los requisitos previos del taller.
- instalarás la aplicación GitHub Copilot e iniciarás sesión.
- elegirás un modelo para tus sesiones.
- identificarás las principales áreas de trabajo de la aplicación.
- probarás un chat rápido.

## Requisitos previos

Necesitas:

- una cuenta de GitHub. [Crea una cuenta de GitHub][github-signup] o utiliza una cuenta que ya tengas.
- un plan activo de Copilot. [Activa Copilot Free o un plan de pago de Copilot][copilot-plans]. Si tu organización ya te proporciona acceso a Copilot, utiliza esa cuenta.
- un equipo con macOS, Windows o Linux.

> [!IMPORTANT]
> Copilot Free no incluye la revisión de código de Copilot para solicitudes de incorporación de cambios (PR). La solicitud de revisión de la [lección 8][review-lesson] requiere [acceso a la revisión de código de Copilot][code-review]. Si no tienes acceso, sigue la alternativa de revisión manual de esa lección.

La aplicación incluye Git, así que no tienes que instalarlo por separado.

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, el administrador debe habilitar la directiva **Copilot CLI** para que funcionen las sesiones de agente.

## Instala y configura la aplicación

Instala la aplicación e inicia sesión en GitHub.

1. Descarga e instala la [aplicación GitHub Copilot][download-app] para tu sistema operativo.
2. Abre la aplicación.
3. Selecciona **Sign in to GitHub** e inicia sesión.
4. Elige un tema y selecciona **Finish**.

## Elige un modelo

Sigue este orden de preferencia y selecciona el primer modelo que tengas disponible:

1. **GPT-6-Luna** (recomendado).
2. **Auto**, como alternativa equilibrada.
3. Cualquier modelo de la [lista de modelos activos][active-models].

La disponibilidad depende del plan, de la directiva de la organización y de la versión del producto.

## Familiarízate con la aplicación

La aplicación reúne el flujo de desarrollo en un solo lugar:

- **New**: inicia una sesión en un proyecto o selecciona **Chat** para hacer una pregunta.
- **Pull requests**: revisa y sigue las solicitudes de incorporación de cambios en todos los repositorios.
- **Issues**: busca incidencias que tengas asignadas, hayas creado o te mencionen.
- **Automations**: programa tareas recurrentes del agente en un repositorio.
- **Customize**: cambia los temas y los modelos, y administra las extensiones de Canvas.
- **Projects**: abre tus repositorios y consulta las sesiones asociadas a cada uno.

## Prueba un chat rápido

No todas las preguntas necesitan un espacio de trabajo. Desde **New**, selecciona **Chat** en lugar de un proyecto. El chat no está asociado a un repositorio y no puede editar archivos; es una forma rápida de hacer una pregunta, obtener una explicación o pensar en un enfoque antes de iniciar una sesión de trabajo.

1. Envía este prompt en un chat:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

## Resumen y pasos siguientes

En esta lección:

- has comprobado los requisitos previos.
- has instalado la aplicación GitHub Copilot e iniciado sesión.
- has elegido un modelo para tus sesiones.
- has identificado las principales áreas de trabajo de la aplicación.
- has probado un chat rápido.

A continuación, continúa con la [lección 1: Crear el espacio de trabajo de Space Quiz][next-lesson].

[github-signup]: https://github.com/signup
[copilot-plans]: https://github.com/features/copilot/plans
[download-app]: https://gh.io/app
[active-models]: https://docs.github.com/copilot/reference/copilot-billing/models-and-pricing
[review-lesson]: ../8-review-loop/
[code-review]: https://docs.github.com/copilot/concepts/agents/code-review
[next-lesson]: ../1-create-workspace/
