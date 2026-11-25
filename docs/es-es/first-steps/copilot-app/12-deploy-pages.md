---
title: "Lección 12 - Despliega el sitio con GitHub Pages"
description: "Utiliza la aplicación GitHub Copilot para configurar un flujo de trabajo de Pages, revisar su solicitud de incorporación de cambios y comprobar el cuestionario espacial publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Dale al cuestionario espacial una dirección pública desplegándolo con GitHub Pages. Copilot puede preparar el flujo de trabajo y guiar el despliegue, pero tú eres responsable de revisar los cambios y confirmar que el sitio esté activo.

En esta lección:

- pedirás a Copilot que configure un despliegue de GitHub Pages;
- revisarás el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarla;
- seguirás el despliegue y comprobarás el sitio publicado.

## Escenario

El cuestionario espacial ya está en un repositorio de GitHub, pero las personas necesitan una forma sencilla de probarlo. Publicar el sitio de un único archivo con GitHub Pages lo hará accesible desde una URL pública sin añadir un servidor ni una dependencia de ejecución.

## Pide a Copilot que prepare el despliegue

> [!WARNING]
> Crear una solicitud de incorporación de cambios puede confirmar y enviar código. Revisa la configuración de aprobaciones y el repositorio de destino antes de enviar esta indicación. Con **Approve all**, no esperes una solicitud de confirmación independiente.

En la sesión de la aplicación Copilot para `space-quiz`, envía esta indicación:

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## Revisa el flujo de trabajo y la solicitud de incorporación de cambios

1. Confirma que el README se añade solo si el repositorio aún no tiene uno.
2. Revisa los cambios de la solicitud de incorporación de cambios, incluidos los pasos de compilación y despliegue del flujo de trabajo, los activadores y los permisos.
3. Confirma que el flujo de trabajo se despliega desde la rama predeterminada, no desde una solicitud de incorporación de cambios sin combinar.
4. Solicita las correcciones necesarias y revisa las diferencias actualizadas. Espera a que las comprobaciones necesarias de la solicitud de incorporación de cambios sean correctas antes de autorizar la combinación.

## Autoriza la combinación y el despliegue

> [!WARNING]
> La indicación siguiente autoriza al agente a combinar la solicitud de incorporación de cambios revisada, cambiar la configuración de Pages del repositorio y publicar el sitio. Envíala solo después de completar la revisión y confirmar el repositorio y la solicitud de incorporación de cambios. La configuración de aprobaciones puede permitir estas acciones sin otra solicitud de confirmación.

Sustituye `<PR_NUMBER>` por el número de la solicitud de incorporación de cambios que has revisado y, después, envía esta indicación independiente:

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![Diagrama de tres etapas: una solicitud de incorporación de cambios de space-quiz ya combinada; una ejecución correcta de GitHub Actions Deploy website con los pasos Build website, Upload artifact y Deploy to Pages; y el cuestionario espacial activo en tu-nombre-de-usuario.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Comprueba el despliegue

1. Sigue la ejecución de despliegue de GitHub Actions hasta que finalice correctamente.
2. Abre la URL indicada y confirma que el cuestionario espacial se carga.

Si el agente no puede habilitar Pages ni combinar la solicitud de incorporación de cambios, sigue las instrucciones específicas que proporcione. No consideres que la tarea ha terminado hasta que el despliegue se complete y el sitio activo se cargue.

## Resumen y próximos pasos

Tu cuestionario espacial ya está disponible como sitio activo y has comprobado el despliegue en lugar de depender del informe del agente. Continúa con la [Lección 13: Repaso y próximos pasos][next-lesson].

[next-lesson]: ../13-review/
