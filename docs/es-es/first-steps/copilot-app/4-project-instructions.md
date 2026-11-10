---
title: "Lección 4 - Recoger las instrucciones del proyecto"
description: "Ejecuta /init para generar instrucciones del agente que describan el Space Quiz terminado y adáptalas a tu forma de trabajar."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-05
---

Ahora que el cuestionario está creado, perfeccionado y probado, conviene documentar cómo deben tratarlo las sesiones futuras. Cada sesión lee las instrucciones del agente antes de empezar a trabajar, así que estas instrucciones evitan repetir las mismas directrices en cada prompt.

En esta lección:

- generarás instrucciones del agente con `/init`.
- revisarás el archivo generado antes de aceptarlo.
- reducirás y personalizarás las instrucciones.

## Recoge las reglas con `/init`

El comando `/init` requiere un prompt adicional; si se envía sin texto, puede aparecer `Command input required`.

1. Ejecuta `/init create simple rules for the project` en la sesión de la aplicación.
2. Revisa el archivo de instrucciones del agente generado antes de aceptarlo.
3. Redúcelo a directrices que reflejen este proyecto: un único archivo, sin dependencias, accesible y probado en el navegador.

> [!IMPORTANT]
> **¿Por qué después de perfeccionarlo?**
>
> `/init` lee el proyecto tal como existe en ese momento. Ejecutarlo después de crear y probar el cuestionario produce instrucciones que describen código real en lugar de una carpeta vacía.

## Adáptalo a ti

El archivo de instrucciones no sirve solo para recoger datos del proyecto. Puede incluir preferencias que de otro modo repetirías en cada prompt, como la forma de escribir código, las convenciones de nomenclatura, las bibliotecas que deben evitarse y la cantidad de comentarios deseada. Cada sesión futura lee este archivo antes de leer tu prompt.

1. Añade al archivo las preferencias que quieras aplicar en sesiones futuras.

## Resumen y pasos siguientes

- Has generado instrucciones del agente con `/init`.
- Has revisado el archivo generado antes de aceptarlo.
- Has reducido y personalizado las instrucciones.

Continúa con la [lección 5: Publicar el proyecto][next-lesson].

[next-lesson]: ../5-publish/
