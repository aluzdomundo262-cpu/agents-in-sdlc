---
title: "Lección 1 - Crear en el área de trabajo"
description: "Crea el Space Quiz en Visual Studio Code (VS Code), previsualízalo en el navegador integrado y perfecciona un elemento seleccionado."
authors:
  - jamesmontemagno
lastUpdated: 2026-09-28
---

Mantén juntos el editor, el chat, los archivos y la vista previa. Crearás el cuestionario, lo probarás en el navegador integrado y, después, enviarás un elemento concreto directamente al chat para realizar un cambio acotado.

En esta lección:

- crearás el cuestionario en un único `index.html`.
- previsualizarás el cuestionario en el navegador integrado.
- seleccionarás un elemento en el navegador y lo perfeccionarás.

## Crea el cuestionario

Envía el siguiente prompt en Copilot Chat:

```plaintext
Crea un cuestionario colorido y accesible sobre exploración espacial con 10 preguntas en un único archivo index.html. Añade una barra de progreso, un contador de puntuación, indicadores animados para las respuestas correctas e incorrectas y una pantalla de resultados. No utilices servidor ni dependencias. Ábrelo en el navegador integrado de VS Code.
```

1. Revisa el archivo generado en el editor.
2. Abre el navegador integrado y responde a varias preguntas.
3. Abre **Source Control** en cualquier momento para ver los archivos modificados y las diferencias.

## Selecciona un elemento y perfecciónalo

El navegador integrado puede enviar un elemento concreto directamente al chat, así que no tienes que describir a qué botón te refieres.

1. Con el cuestionario abierto en el navegador integrado, inicia la selección de un elemento desde su barra de herramientas.
2. Selecciona los botones de respuesta para adjuntar ese elemento al siguiente mensaje de chat.
3. Envía el siguiente prompt y observa cómo se vuelve a cargar la vista previa:

   ```plaintext
   Usa el elemento seleccionado para mejorar la sensación táctil de los botones de respuesta: añade un estado de pulsación sutil, un indicador de foco más visible para quienes usan el teclado y una transición más fluida a los colores de respuesta correcta e incorrecta. No cambies nada más.
   ```

4. Lee las diferencias en **Source Control** antes de conservar el cambio.
5. Pulsa <kbd>Tab</kbd> para desplazarte por las respuestas y confirma que el indicador de foco es visible.

## Resumen y pasos siguientes

Has creado, previsualizado y perfeccionado el cuestionario sin salir del editor. Continúa con la [lección 2: Generar las instrucciones del proyecto][next-lesson].

[next-lesson]: ../2-project-instructions/
