---
title: "Lección 3 - Inspeccionar la sesión y probar el cuestionario"
description: "Revisa los detalles del proyecto y del uso de la sesión y, después, ejecuta una prueba de humo en el navegador antes de que Git escriba nada."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

El trabajo que ya ha realizado la sesión permite inspeccionar qué está haciendo el agente. La prueba en el navegador integrado muestra lo que ha ocurrido realmente, no solo lo que el agente pretendía hacer.

En esta lección:

- revisarás el proyecto y los controles de la sesión en el menú del título.
- comprobarás el plan, el uso de la sesión, los tokens y el contexto en el menú de uso.
- ejecutarás una prueba de humo en el navegador y corregirás los fallos.

## Revisa los detalles del proyecto

El menú del proyecto muestra qué carpeta y sesión está usando el agente:

1. Selecciona **Build a space quiz** en la barra de título.

![Ilustración del menú de título Build a space quiz. Identifica la sesión que trabaja en la carpeta del proyecto space-quiz y proporciona controles para la ruta, el control remoto, el nombre, las sesiones anidadas, el identificador (ID) de sesión, el uso compartido, el archivado y la eliminación.](../../../_images/first-steps-app-project-details.svg)

Este menú identifica el proyecto en el que trabaja la sesión y proporciona controles para administrar la sesión.

2. Confirma que la sesión está asociada al proyecto `space-quiz`.
3. Selecciona **Path** para confirmar que la sesión trabaja en la carpeta esperada.
4. Observa los controles de acceso remoto, cambio de nombre, sesiones anidadas, uso compartido, archivado y eliminación.

## Revisa los detalles de uso

El menú de uso presenta el plan y las cifras de la sesión:

1. Selecciona el control de uso a la izquierda del micrófono. El micrófono está entre el control de uso y **Send**.

![Ilustración del menú de uso con el micrófono entre el control de uso y el botón Send. Muestra el plan GitHub Copilot Pro+, los créditos de inteligencia artificial (IA) de la sesión, los recuentos de tokens de entrada y salida y un uso del contexto del 16 % de 400 000 tokens.](../../../_images/first-steps-app-usage-details.svg)

Este menú separa el uso de la cuenta y de la sesión de los controles del proyecto:

- **Plan** muestra el uso del plan cuando esa información está disponible.
- **Session** muestra los créditos de IA utilizados por la sesión actual.
- **Tokens** muestra los recuentos de tokens de entrada, almacenados en caché, de salida y de razonamiento.
- **Context** muestra cuánto de la ventana de contexto ha utilizado la sesión.

2. Comprueba **Context** a medida que crece la sesión. Cuando se llena, al agente le queda menos espacio para la tarea, y esa es la señal para iniciar una sesión nueva.

> [!TIP]
> **La mayoría de los resultados deficientes se deben al contexto**
>
> Una carpeta equivocada o una ventana de contexto casi llena explican muchas más sorpresas que un mal prompt.

## Prueba antes de que Git escriba nada

Una prueba de humo en el navegador integrado permite comprobar el cuestionario antes de que Git escriba cambios:

1. Envía el siguiente prompt:

   ```plaintext
   Run a browser-level smoke test for the quiz in the integrated browser. Check keyboard navigation, score updates, correct and incorrect feedback, and the results screen. Fix any failures, then report what passed.
   ```

2. Observa el navegador integrado mientras el agente recorre las preguntas.
3. Si algo falla, deja que el agente lo corrija y vuelva a ejecutar la prueba hasta que todo pase.
4. Continúa solo cuando la creación del proyecto y las pruebas se hayan completado correctamente.

Todavía no se ha escrito nada en Git. En la siguiente lección ejecutarás `/init create simple rules for the project`, que lee el proyecto tal como está, así que conviene asegurarte primero de que funciona.

## Resumen y pasos siguientes

- Has revisado el proyecto y los controles de la sesión en el menú del título.
- Has comprobado el plan, el uso de la sesión, los tokens y el contexto en el menú de uso.
- Has ejecutado una prueba de humo en el navegador y corregido los fallos.

Continúa con la [lección 4: Recoger las instrucciones del proyecto][next-lesson].

[next-lesson]: ../4-project-instructions/
