---
title: "Lección 5: Supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

En el modo de agente, GitHub Copilot explora el código, propone cambios, edita archivos y ejecuta comandos de forma autónoma. Como el trabajo se realiza en tu equipo y en tiempo real, Copilot Chat en VS Code muestra las llamadas a herramientas y las ediciones de archivos. Puedes revisar cada diff, aceptar o rechazar los cambios y dirigir la conversación con prompts adicionales sin salir del editor.

En esta lección:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos en los archivos.
- pedirás al agente, durante la sesión, que añada un control de modo claro junto al de alto contraste.

## Escenario

El agente personalizado de accesibilidad de la [lección 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita también un control para el modo claro. En lugar de empezar una conversación nueva, ampliarás la tarea desde la sesión actual.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra los pasos del agente: archivos que explora, comandos que ejecuta y cambios que propone. Las ediciones aparecen en el chat con un diff y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat que abriste en la lección 4.
2. Mientras trabaja el agente, desplázate por el chat para ver las llamadas a herramientas, las lecturas y ediciones de archivos y los comandos de terminal que solicita ejecutar.
3. Cuando proponga una edición, revisa el diff:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para deshacerlo y permitir que el agente vuelva a intentarlo.
4. Selecciona **Files changed** en la parte superior del chat para revisar todos los archivos modificados durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta requiere permiso, por ejemplo, para ejecutar un comando de terminal, el agente se detendrá y mostrará **Allow**. Aprueba solo los comandos que hayas revisado y aceptes ejecutar.

5. Espera a que el agente termine de implementar el modo de alto contraste. Debería mostrar un mensaje final que resuma los cambios.

## Pide al agente que añada el modo claro

Ahora ampliarás la conversación para añadir un control de modo claro. Al continuar en la misma sesión, el agente conserva el contexto de los cambios, los estilos y el patrón de almacenamiento local que acaba de utilizar en la interfaz de usuario (UI).

1. Envía este prompt desde el cuadro de Copilot Chat:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. El agente revisará los cambios realizados y propondrá los necesarios para añadir el modo claro.
3. Revisa cada cambio cuando aparezca y selecciona **Keep** o **Undo**, como hiciste con el modo de alto contraste.
4. Si el agente sigue un enfoque que no quieres —por ejemplo, intenta reorganizar los controles de forma que no te convence—, detenlo con **Stop**, junto al cuadro de entrada, y envía otra indicación para aclarar lo que necesitas.

> [!TIP]
> Dirigir una sesión en curso es más rápido que empezar de nuevo. Utiliza prompts de seguimiento para simplificar las hojas de estilo en cascada (CSS), corregir el enfoque o ampliar el alcance. Por ejemplo, puedes pedir que use variables CSS en lugar de duplicar selectores, que integre el modo claro en el panel de ajustes existente en lugar de añadir un tercer control o que añada atajos de teclado para ambos controles.

## Revisa los cambios

Antes de confirmar el trabajo, revisa todos los archivos modificados por el agente.

1. Abre la vista **Source Control** en VS Code.
2. Revisa la lista completa de archivos modificados. Puede incluir componentes de Astro, estilos y pruebas relacionadas.
3. Abre algunos archivos y revisa los diffs. Confirma que se han aplicado las prácticas de accesibilidad del agente personalizado: atributos de aplicaciones de Internet enriquecidas y accesibles (Accessible Rich Internet Applications, ARIA), navegación con teclado, lenguaje de marcado de hipertexto (HTML) semántico y persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel **Source Control**. Los publicarás en la siguiente lección.

## Resumen y pasos siguientes

Has utilizado el modo de agente de Copilot Chat para supervisar y dirigir una sesión en curso: has revisado cada edición, aceptado o rechazado cambios y enviado prompts de seguimiento para ampliar el trabajo sin perder el contexto.

En esta lección:

- has supervisado el trabajo de un agente en tiempo real.
- has aceptado y rechazado ediciones de archivos.
- has dirigido una sesión en curso con prompts de seguimiento.

En la [siguiente lección][next-lesson] publicarás el trabajo de accesibilidad en una solicitud de incorporación de cambios (PR) y revisarás los cambios del agente personalizado local que has utilizado en el taller.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo de agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
