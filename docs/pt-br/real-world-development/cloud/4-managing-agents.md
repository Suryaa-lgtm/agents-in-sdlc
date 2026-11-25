---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos dois exercícios anteriores, você pediu ao agente na nuvem do Copilot que executasse três tarefas distintas para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente na nuvem tenha sido criado para trabalhar de forma assíncrona e autônoma, ainda é importante monitorar essas tarefas.

Há várias ferramentas disponíveis para gerenciar as tarefas atribuídas ao agente na nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse painel de controle, você pode ver todas as tarefas do agente que têm pull requests (PRs) abertos. Você pode explorar as operações realizadas e até orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar as tarefas do agente na nuvem.
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a tarefa de criar um modo de alto contraste, a equipe percebeu que seria um bom momento para adicionar também um modo claro. Como o trabalho já envolvia atualizar o estilo do site e adicionar uma funcionalidade de alternância, pareceu lógico incluir esse modo. Você orientará o trabalho do agente para garantir que ele adicione um modo claro além do modo de alto contraste.

## Revisar as tarefas do agente na nuvem do Copilot

Vamos conferir o estado atual de todas as tarefas atribuídas ao agente na nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel esquerdo. Você deverá ver as tarefas atribuídas ao Copilot, incluindo:
    - atualizar a documentação da base de código.
    - gerar APIs para modificar jogos.
    - adicionar um modo de alto contraste ao site.
3. Selecione uma das tarefas em execução. Revise as operações já realizadas pelo Copilot. Elas podem incluir:
    - obter o código do repositório.
    - criar o ambiente de trabalho do Copilot.
    - configurar servidores MCP.
    - executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas exatas exibidas variam de acordo com o estado do trabalho do Copilot e a abordagem adotada.

4. Observe também o painel de pull request (PR), que aparece à direita. Ele permite acompanhar o PR e os arquivos alterados.

## Orientar o agente na nuvem

Agora que você viu as tarefas em andamento, vamos pedir ao Copilot que inclua o modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente à adição do modo de alto contraste. O título exato varia conforme o nome escolhido pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no painel de controle](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração foi concluída e o trabalho começou. Você saberá que isso aconteceu quando começar a ver mensagens semelhantes aos exemplos abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o prompt a seguir:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de tela da tarefa do agente na nuvem na página de agentes, com a caixa de diálogo de orientação da sessão ativa do Copilot destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento do prompt e o inclui no fluxo de trabalho.

## Deixar o Copilot trabalhar

Como antes, o Copilot começará a trabalhar na tarefa atualizada! Ele incorporará a nova solicitação ao fluxo de trabalho depois de concluir a etapa específica que estava executando quando você enviou a mensagem.

Como isso levará vários minutos, aproveite para fazer uma pausa e refletir sobre tudo que aprendeu e explorou até agora.

## Resumo e próximos passos

Neste exercício, você explorou a página de agentes do Copilot, o ponto central para monitorar e orientar as tarefas do agente na nuvem do GitHub Copilot. Nesse painel de controle, você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho e redirecionar tarefas em andamento para ajustar o escopo ou oferecer orientações adicionais.

Você explorou estes conceitos:

- explorou o painel de controle e a página de agentes para monitorar as tarefas do agente na nuvem.
- redirecionou uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, vamos [iterar nos pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
