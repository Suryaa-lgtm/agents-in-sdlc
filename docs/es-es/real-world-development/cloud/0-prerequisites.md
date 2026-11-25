---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios del agente en la nube de Copilot, prepara todo lo necesario. Crearás tu propia copia del repositorio Tailspin Toys y pondrás en marcha un [codespace][codespaces] para editar archivos de instrucciones y revisar el trabajo que produzca el agente en la nube.

## Configura el repositorio del laboratorio

Para crear una copia del repositorio para el código que desarrollarás, crearás una instancia a partir de la [plantilla][template-repository]. La nueva instancia contendrá todos los archivos necesarios para el laboratorio y la utilizarás durante los ejercicios.

1. En una nueva ventana del navegador, abre la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando el botón **Use this template** en la página del repositorio del laboratorio. Después, selecciona **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si realizas el taller en un evento organizado por GitHub o Microsoft, sigue las instrucciones de las personas que lo tutorizan. De lo contrario, puedes crear el nuevo repositorio en una organización donde tengas acceso a GitHub Copilot.

    ![Configuración del repositorio creado a partir de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio que has creado (**organization-or-user-name/repository-name**), ya que la necesitarás más adelante en el laboratorio.

## Crea un codespace

A continuación, utilizarás un codespace para completar los ejercicios del laboratorio.

[GitHub Codespaces][codespaces] son entornos de desarrollo basados en la nube que te permiten escribir, ejecutar y depurar código directamente en el navegador. Proporcionan un IDE completo con compatibilidad con varios lenguajes de programación, extensiones y herramientas.

1. Abre el repositorio que acabas de crear.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y selecciona el botón **+** para crear un codespace.

    ![Crea un codespace](../../../_images/ex0-create-codespace.png)

La creación del codespace tardará varios minutos, aunque sigue siendo mucho más rápido que instalar todos los servicios manualmente. Mientras tanto, puedes explorar otras funciones de GitHub Copilot, que veremos a continuación.

> [!CAUTION]
> Volverás al codespace en un ejercicio futuro. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está preparado para ejecutarse dentro de un codespace o de un [contenedor de desarrollo local][dev-containers]. Ambos garantizan que el entorno tenga todos los requisitos previos necesarios para que la experiencia sea fluida. Si prefieres trabajar en local, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te indique; VS Code creará el mismo contenedor de desarrollo que utiliza el codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Resumen

¡Enhorabuena! Has creado una copia del repositorio del laboratorio y has iniciado la creación de tu codespace, que utilizarás mientras trabajas con el agente en la nube de Copilot.

## Próximo paso

A continuación, añade instrucciones personalizadas que seguirá el agente en la nube. Continúa con el [Ejercicio 1: Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
