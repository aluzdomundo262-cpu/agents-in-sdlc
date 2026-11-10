---
title: "Lição 2 - Adicione classificações por estrelas: uma vitória rápida"
description: "Use o Copilot CLI para fazer uma pequena mudança nos cartões de jogos, revisar em um navegador encaminhado e mesclar seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e experimentou uma conversa, é hora de fazer sua primeira mudança no projeto. Você começará com algo pequeno: os jogos já têm uma classificação por estrelas nos dados, mas ela ainda não aparece nos cartões da página inicial. Peça ao agente que a exiba, revise a mudança e mescle-a como seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em um branch de recurso.
- pedir ao agente que faça uma pequena mudança no projeto.
- revisar a mudança com `/diff`.
- executar o aplicativo e confirmar a mudança em um navegador encaminhado.
- abrir e mesclar seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma classificação por estrelas, que já aparece na página de detalhes do jogo. Os cartões de jogos na página inicial, porém, mostram apenas o título, a categoria, a editora e a descrição. Como aquecimento, peça ao agente que exiba a classificação existente em cada cartão — uma mudança pequena e independente, ideal para sua primeira sessão.

## Estrutura de uma conversa

Uma **conversa** é onde você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal do CLI usa o repositório e o branch do Git atualmente selecionados no terminal, em vez de criar um worktree dedicado. As conversas salvas permitem retomar a mesma discussão depois, enquanto os arquivos e o branch continuam sendo o estado comum do Git no disco.

Em uma conversa, você verá três elementos: seus prompts e as respostas do agente, a atividade das ferramentas que o agente usa para explorar e editar arquivos e as mudanças que você pode inspecionar com `/diff`.

## Inicie uma conversa e solicite a mudança

Inicie uma conversa para começar a implementar o recurso.

1. Volte ao Codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Se o Copilot ainda não estiver em execução, inicie-o com este comando:

   ```bash
   copilot --yolo
   ```

4. Inicie uma nova sessão com o comando de barra `/new` e pressione <kbd>Enter</kbd>.
5. Use este prompt para solicitar a mudança:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

O Copilot explora o projeto, localiza os arquivos que exibem os detalhes dos jogos e cria o código necessário. Você acabou de adicionar um recurso com o Copilot CLI.

## Revise as diferenças

Todas as mudanças geradas por inteligência artificial (IA) precisam ser revisadas antes da mesclagem, mesmo as pequenas. Revise as mudanças diretamente no Copilot CLI.

1. Digite `/diff` e inspecione cada arquivo alterado.
2. Confirme que o cartão de jogo exibe a classificação numérica quando ela está disponível e `No rating yet` quando `starRating` é `null`.
3. Confirme que os testes cobrem os dois estados.
4. Revise os resultados das verificações executadas pelo Copilot e peça que ele corrija qualquer falha.
5. Ao concluir a revisão, pressione <kbd>Esc</kbd> para sair da tela de diferenças.

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, não determinístico, então o código exato pode variar. Revise o comportamento em vez de esperar uma implementação específica.

## Verifique as mudanças

Não basta ler o código e presumir que funciona. Peça ao Copilot que inicie o site para que você possa examinar a interface do usuário (UI) atualizada no navegador encaminhado pelo Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme que os cartões de jogos exibem as classificações de cinco estrelas.
4. Volte ao Copilot e peça que pare o servidor iniciado:

   ```plaintext
   Stop the development server you started.
   ```

## Abra e mescle seu primeiro pull request

Você criou o recurso. Agora, abra um pull request (PR) para mesclar o novo código ao projeto.

1. Peça ao agente padrão que faça commit da mudança:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Digite `/pr create`. Ao criar o PR, o Copilot CLI envia o commit existente e exibe o localizador uniforme de recursos (URL) do PR.
3. Abra o PR mantendo pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver tudo pronto, selecione **Merge pull request** e confirme a mesclagem.
6. Volte ao Codespace e saia do Copilot CLI com `/exit`.
7. Atualize o `main` local:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Parabéns! Você entregou sua primeira mudança com o GitHub Copilot CLI. Especificamente, você:

- iniciou uma conversa focada do Copilot em um branch de recurso.
- orientou o agente a fazer uma pequena mudança nos cartões de jogos.
- revisou a mudança com `/diff`.
- executou o aplicativo e confirmou a classificação por estrelas em um navegador encaminhado.
- abriu e mesclou seu primeiro pull request.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para desenvolver um recurso maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
