---
title: "Lição 9 - Comandos slash no GitHub Copilot CLI"
description: "Explore comandos slash para gerenciar contexto, selecionar modelos, compartilhar sessões e delegar tarefas opcionalmente para a nuvem."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como toda boa ferramenta de CLI, o GitHub Copilot CLI inclui vários comandos slash para interagir com ela. Esses comandos expõem funcionalidades avançadas, informações internas e opções adicionais de configuração. Você já usou comandos como `/diff`, `/mcp`, `/skills`, `/agent` e `/pr`. Vamos explorar outros comandos úteis.

Nesta lição, você vai:

- usar `/context` e `/compact` para explorar como o Copilot gerencia o contexto da conversa.
- usar `/model` para explorar os modelos disponíveis.
- aprender como `/share` pode exportar ou compartilhar uma sessão.
- explorar comandos opcionais para trabalho paralelo, worktrees e delegação para o agente na nuvem.

## Cenário

Você concluiu o fluxo de trabalho principal da CLI. Agora vamos conhecer alguns recursos adicionais — gerenciamento de contexto, troca de modelos, compartilhamento de sessões e delegação opcional para o [agente na nuvem do Copilot][about-cloud-agent].

## Explorar o contexto do Copilot CLI

Ao trabalhar em tarefas maiores ou mais complexas, você poderá atingir o limite da janela de contexto do modelo. O Copilot CLI compacta a conversa automaticamente quando necessário, e você pode inspecionar ou compactar o contexto manualmente com comandos slash.

1. Retorne ao Codespace e inicie o Copilot CLI na raiz do repositório, se ele ainda não estiver aberto.
2. Digite:

   ```plaintext
   /context
   ```

3. Observe o modelo, o uso atual de tokens e a divisão do contexto entre instruções do sistema, ferramentas, mensagens e espaço livre.
4. Compacte a conversa:

   ```plaintext
   /compact
   ```

5. Digite `/context` novamente e compare o resultado. Talvez não haja uma mudança drástica se a conversa já for pequena.

> [!NOTE]
> O Copilot CLI compacta o contexto automaticamente à medida que a janela se enche. Use `/compact` se quiser escolher o momento. Use `/clear` ou `/new` quando mudar para uma tarefa sem relação e quiser iniciar uma conversa limpa.

## Escolher seu modelo

Os modelos têm pontos fortes diferentes, e cada desenvolvedor tem suas próprias preferências. O Copilot CLI permite listar e selecionar o modelo que você quer usar.

1. Digite:

   ```plaintext
   /model
   ```

2. Explore os modelos disponíveis e as informações de uso.
3. Mantenha o modelo atual, selecione outro ou pressione <kbd>Esc</kbd> para fechar a lista.

## Compartilhar uma sessão

Trabalhar em equipe e compartilhar aprendizados ajuda todos a usar melhor as ferramentas de IA. O comando `/share` pode exportar uma sessão para um arquivo Markdown ou HTML, criar um link compartilhável ou publicar um gist do GitHub.

1. Digite `/help` e revise as opções de `/share` na versão instalada.
2. Se quiser compartilhar esta sessão, escolha o destino mais adequado às suas necessidades, como `/share file` para exportar um arquivo Markdown local.
3. Revise o conteúdo exportado antes de enviá-lo a alguém ou publicá-lo. As exportações de sessões podem incluir prompts, respostas e detalhes do projeto.

Publicar um link ou gist é opcional. Não publique conteúdo do repositório ou da conversa que sua equipe não pretenda compartilhar.

## Opcional: ampliar ou delegar o trabalho

O fluxo principal do workshop está concluído. O Copilot CLI também oferece comandos para tarefas maiores:

- `/fleet` pode dividir subtarefas independentes entre subagentes e executá-las em paralelo.
- `/worktree` pode criar uma worktree Git isolada para uma tarefa separada.
- `/delegate` pode enviar uma tarefa ao agente na nuvem do Copilot, que trabalha de forma assíncrona e pode abrir um pull request.

Esses comandos são opcionais porque podem criar worktrees adicionais ou trabalho remoto. Comece uma tarefa nova e bem delimitada antes de experimentá-los e revise o resultado pelo fluxo de trabalho normal. Se quiser saber mais sobre o trabalho assíncrono com agentes, continue com o [workshop do agente na nuvem][cloud-workshop].

## Resumo e próximos passos

Os comandos slash do Copilot CLI permitem configurá-lo, compartilhar sessões e observar o que acontece nos bastidores. Nesta lição, você:

- usou `/context` e `/compact` para explorar como o Copilot gerencia o contexto da conversa.
- usou `/model` para explorar os modelos disponíveis.
- aprendeu como `/share` pode exportar ou compartilhar uma sessão.
- explorou comandos opcionais para trabalho paralelo, worktrees e delegação para o agente na nuvem.

Há muitos outros comandos slash e recursos para explorar no Copilot CLI! Vamos concluir nossa jornada [revisando o que aprendemos][next-lesson] e alguns próximos passos para continuar aprendendo.

## Recursos

- [Referência de comandos do Copilot CLI][cli-reference]
- [Gerenciamento de contexto no Copilot CLI][context-management]
- [Sobre o agente na nuvem do Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
