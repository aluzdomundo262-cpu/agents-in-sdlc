---
title: "Exercício 4 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos últimos exercícios, você pediu ao agente de nuvem do Copilot que executasse três tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente de nuvem trabalhe de forma assíncrona e autônoma, ainda é importante monitorar essas tarefas.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse Mission Control, você pode ver todas as tarefas do agente com pull requests (PRs) abertos, explorar as operações realizadas e até orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar as tarefas do agente de nuvem.
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe percebeu que seria útil adicionar também um modo claro. Como o trabalho já envolve atualizar o estilo do site e adicionar controles de alternância, faz sentido incluir essa funcionalidade. Oriente o trabalho do agente para que ele adicione o modo claro junto com o modo de alto contraste.

## Revise as tarefas do agente de nuvem do Copilot

Confira o status atual de todas as tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel à esquerda. Ela deve incluir as tarefas atribuídas ao Copilot:
   - Atualizar a documentação da base de código.
   - Gerar APIs para modificar jogos.
   - Adicionar um modo de alto contraste ao site.
3. Selecione uma das tarefas em execução e revise as operações realizadas pelo Copilot. Elas podem incluir:
   - Clonar o código do repositório.
   - Criar o ambiente de trabalho do Copilot.
   - Configurar servidores do Model Context Protocol (MCP).
   - Executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas exatas exibidas variam de acordo com o estado do trabalho do Copilot e a abordagem usada.

4. Observe também o painel do pull request (PR), que aparece à direita. Ele permite acompanhar o PR e os arquivos alterados.

## Oriente o agente de nuvem

Agora que você conhece as tarefas ativas, peça ao Copilot que inclua o controle do modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente à adição do modo de alto contraste. O título exato varia conforme o nome escolhido pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no Mission Control](../../../_images/ex6-accessibility-session.png)

2. Aguarde alguns minutos, até que a sessão indique que a configuração foi concluída e o trabalho começou. Você verá mensagens semelhantes às mostradas abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione este prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de tela da tarefa do agente de nuvem na página de agentes, com a caixa de diálogo para orientar a sessão ativa do Copilot destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe que o Copilot confirma o recebimento do prompt e o inclui no fluxo de trabalho.

## Deixe o Copilot trabalhar

Como antes, o Copilot trabalhará na tarefa atualizada. Ele incorporará a nova solicitação ao fluxo depois de concluir a etapa que estava executando quando você enviou a mensagem.

Isso levará alguns minutos, então aproveite para fazer uma pausa e refletir sobre o que você aprendeu até agora.

## Resumo e próximos passos

Nesta lição, você explorou a página de agentes do Copilot, o ponto central para monitorar e orientar as tarefas do agente de nuvem do GitHub Copilot. Nesse Mission Control, você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho e redirecionar tarefas em andamento para ajustar o escopo ou fornecer orientações adicionais.

Você explorou estes conceitos:

- explorou o Mission Control e a página de agentes para monitorar as tarefas do agente de nuvem.
- redirecionou uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, você pode [iterar nos pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Exercício anterior: Agentes personalizados][previous-lesson] | [Próximo exercício: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
