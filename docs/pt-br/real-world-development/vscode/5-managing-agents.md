---
title: "Exercício 5 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Quando você usa o GitHub Copilot no modo de agente, ele trabalha de forma autônoma: explora a base de código, propõe mudanças, edita arquivos e executa comandos. Como esse trabalho ocorre em tempo real no seu computador, o Copilot Chat no VS Code mostra cada chamada de ferramenta e edição de arquivo à medida que acontece. Você pode revisar cada diff no chat, aceitar ou rejeitar mudanças individuais e orientar a conversa com prompts de acompanhamento sem sair do editor.

Nesta lição, você vai:

- monitorar em tempo real o trabalho do agente de acessibilidade.
- revisar e aceitar as edições de arquivo propostas.
- orientar o agente durante a sessão para adicionar um controle do modo claro junto com o modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade usado no [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho está em andamento, a equipe de design fez outra solicitação: também quer um controle do modo claro para quem considera o tema padrão escuro demais. Em vez de começar uma nova conversa, oriente a sessão existente para ampliar o trabalho.

## Acompanhe o progresso do Copilot

A exibição Copilot Chat mostra cada etapa do agente: os arquivos que explora, os comandos que executa e as edições que propõe. Cada edição aparece no chat com um diff e os controles **Keep** e **Undo**.

1. Volte à exibição Copilot Chat do Exercício 4.
2. Enquanto o agente trabalha, percorra o chat para acompanhar cada chamada de ferramenta. Você verá leituras e edições de arquivos e os comandos de terminal cuja execução ele solicitar.
3. Quando o agente propuser uma edição, o diff aparecerá no chat:
   - Selecione **Keep** para aceitar a mudança.
   - Selecione **Undo** para desfazê-la e permitir que o agente tente novamente.
4. Você também pode abrir o indicador **Files changed**, na parte superior do chat, para ver todos os arquivos alterados pelo agente durante a sessão.

> [!NOTE]
> Se uma chamada de ferramenta pedir permissão, por exemplo, para executar um comando de terminal, o agente pausará e exibirá o pedido **Allow**. Aprove somente os comandos que considerar seguros.

5. Aguarde até que o agente termine de implementar o modo de alto contraste. Uma mensagem final resumirá as mudanças realizadas.

## Oriente o agente para adicionar o modo claro

Agora que o modo de alto contraste está implementado, amplie a mesma conversa para adicionar um controle do modo claro. Como você continuará na mesma sessão de chat, o agente manterá o contexto do trabalho anterior, incluindo os componentes alterados, a abordagem de estilo e o padrão de armazenamento local.

1. No campo de entrada do Copilot Chat, envie este prompt de acompanhamento:

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. O agente continuará o trabalho, explorando as mudanças existentes e propondo adições para o modo claro.
3. Revise cada nova edição à medida que aparecer, como fez com o modo de alto contraste. Use **Keep** ou **Undo** em cada diff.
4. Se o agente seguir uma direção indesejada — por exemplo, se tentar refatorar os controles de uma forma que você não queira — interrompa-o com o botão **Stop**, ao lado do campo de entrada do chat, e envie uma mensagem de acompanhamento para esclarecer o pedido.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que começar de novo. Use prompts de acompanhamento para pedir ajustes ("simplifique as folhas de estilo em cascata (CSS) — use variáveis CSS em vez de duplicar seletores"), corrigir o rumo ("não adicione um terceiro controle; integre o modo claro ao painel de configurações existente") ou ampliar o escopo ("adicione também atalhos de teclado para os dois controles").

## Revise o conjunto de trabalho

Antes de fazer commit do trabalho, revise rapidamente tudo o que o agente alterou.

1. Abra a exibição **Source Control** no VS Code.
2. Revise a lista completa de arquivos alterados. Você deverá ver atualizações nos componentes Astro, nos estilos e nos testes relacionados.
3. Abra alguns arquivos alterados e examine os diffs. Confirme que eles refletem os padrões de acessibilidade do agente personalizado: atributos de Accessible Rich Internet Applications (ARIA), navegação por teclado, linguagem de marcação de hipertexto (HTML) semântica e persistência no armazenamento local.
4. Quando estiver satisfeito, prepare e faça commit das mudanças no painel Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximos passos

Você usou o modo de agente do Copilot Chat para monitorar e orientar uma sessão em andamento: revisou cada edição de arquivo, aceitou ou rejeitou mudanças e enviou prompts de acompanhamento para ampliar o trabalho sem perder o contexto.

Nesta lição, você explorou:

- como monitorar o trabalho de um agente em tempo real.
- como aceitar e rejeitar edições individuais.
- como orientar uma sessão em andamento com prompts de acompanhamento.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade em um pull request e revisará as mudanças produzidas pelo agente personalizado local durante o laboratório.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo de agente][agent-mode]

---

| [← Exercício anterior: Agentes personalizados][previous-lesson] | [Próximo exercício: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
