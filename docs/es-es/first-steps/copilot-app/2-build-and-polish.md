---
title: "Lección 2 - Crear y perfeccionar el cuestionario"
description: "Crea un Space Quiz en un solo archivo y perfecciónalo con el navegador integrado y el selector de elementos."
authors:
  - jamesmontemagno
lastUpdated: 2026-09-28
---

El flujo de trabajo combina un prompt detallado para crear el Space Quiz, la comprobación en el navegador integrado y un ajuste visual con el selector de elementos.

En esta lección:

- crearás un cuestionario sin dependencias en `index.html`.
- probarás el cuestionario en el navegador integrado.
- inspeccionarás el código generado.
- perfeccionarás un elemento seleccionado sin perder la accesibilidad.

## Crea el cuestionario

El siguiente prompt genera el cuestionario en la sesión `space-quiz`:

1. Envía este prompt:

   ```plaintext
   Create a space exploration quiz with 10 questions, a progress bar, score counter, and colorful animated feedback (green for correct, red shake for wrong). Show a results screen with emoji reaction at the end. Center in a narrow column. Single index.html, no server/dependencies. Polished, sans-serif, 14–16px body, prefers-color-scheme. Open in the integrated browser.
   ```

Cuando el agente termine, comprueba el funcionamiento del cuestionario:

1. Responde a varias preguntas y comprueba que la barra de progreso avanza.
2. Comprueba que la puntuación se actualiza.
3. Comprueba que las respuestas correctas muestran un estado verde.
4. Comprueba que las respuestas incorrectas utilizan una animación de sacudida roja.
5. Comprueba que la pantalla de resultados aparece después de la última pregunta.

## Inspecciona el código generado

El área de código ampliada permite revisar el archivo y ver cómo está construido el cuestionario:

1. Contrae la barra lateral izquierda y el panel del navegador de la derecha.
2. Revisa `index.html` y observa cómo el lenguaje de marcado de hipertexto (HTML), las hojas de estilo en cascada (CSS) y JavaScript funcionan juntos en un único archivo.
3. Restaura ambos paneles cuando termines.

## Perfecciona con el selector de elementos

El selector de elementos permite ajustar un elemento concreto sin perder la accesibilidad:
1. Selecciona el selector de elementos en la barra de herramientas del navegador.
2. Selecciona el encabezado del cuestionario o el área de respuestas.
3. Envía el siguiente prompt:

   ```plaintext
   Make the selected element feel more like a mission-control display. Keep it accessible and preserve the existing light and dark themes.
   ```

4. Observa cómo se actualiza el navegador integrado y comprueba el cambio.

## Ajustes opcionales

Si quieres seguir experimentando, puedes pedir al agente estos ajustes:

1. Añada un fondo sutil de estrellas que respete `prefers-reduced-motion`.
2. Haga que la pantalla de resultados sea más festiva cuando la puntuación sea de 8 o más.
3. Mejore los estados de foco del teclado; después, comprueba el cuestionario sin ratón.

## Resumen y pasos siguientes

- Has creado un cuestionario sin dependencias en `index.html`.
- Has probado el cuestionario en el navegador integrado.
- Has inspeccionado el código generado.
- Has perfeccionado un elemento seleccionado sin perder la accesibilidad.

Continúa con la [lección 3: Inspeccionar la sesión y probar el cuestionario][next-lesson].

[next-lesson]: ../3-inspect-and-test/
