---
title: "Exercício 2: Adicione uma nova funcionalidade com o modo de agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até as atualizações mais simples de um aplicativo normalmente exigem alterações em vários arquivos e tarefas como executar testes. Em geral, o fluxo de trabalho de desenvolvimento envolve localizar todos os arquivos necessários, fazer as alterações, executar os testes, depurar, descobrir qual arquivo ficou de fora, atualizá-lo e assim por diante.

É aí que entra o modo de agente do Copilot.

O modo de agente do Copilot foi desenvolvido para agir com mais autonomia no ambiente de desenvolvimento integrado (IDE). Ele funciona de maneira semelhante à de uma pessoa desenvolvedora: começa explorando a estrutura do projeto, faz as atualizações necessárias, executa tarefas como testes e corrige automaticamente os problemas encontrados. Veja como usar o modo de agente para adicionar uma nova funcionalidade ao site.

> [!NOTE]
> Embora os nomes sejam parecidos, o modo de agente e o agente na nuvem oferecem experiências diferentes. O modo de agente executa tarefas no IDE, o que permite ciclos rápidos de feedback e interação. O agente na nuvem atua como uma pessoa desenvolvedora parceira, trabalha de forma assíncrona como integrante da equipe e interage com você por meio de issues e pull requests.

Neste exercício, você aprenderá como:

- usar o modo de agente do Copilot para explorar o projeto, identificar os arquivos relevantes e coordenar alterações;
- usar o modo de agente do GitHub Copilot para implementar novos recursos na interface do usuário (UI) e na camada de dados;
- revisar as alterações e os testes gerados pelo modo de agente do GitHub Copilot antes de mesclá-los à base de código.

## Cenário

À medida que a lista de jogos cresce, você quer permitir que as pessoas usuárias filtrem os jogos por categoria e editora. No exercício anterior, você adicionou uma função auxiliar para editoras. Agora, com o modo de agente do Copilot, concluirá o trabalho restante na camada de dados, na interface e nos testes.

## Execute o site Tailspin Toys

Antes de fazer alterações, explore o site Tailspin Toys para entender as funcionalidades atuais.

O site é uma plataforma de financiamento coletivo de jogos de tabuleiro com um tema voltado a pessoas desenvolvedoras. Ele permite listar jogos e exibir detalhes sobre eles. O site é um único aplicativo Astro que renderiza suas páginas como linguagem de marcação de hipertexto (HTML) estática durante a compilação. As páginas consultam diretamente um banco de dados SQLite local por meio do Drizzle, um mapeador objeto-relacional (ORM), no frontmatter; não há uma interface de programação de aplicações (API) de back-end separada nem uma estrutura de interface no lado do cliente. As funções auxiliares reutilizáveis de acesso a dados ficam em `src/lib/`, e a interatividade é implementada com um elemento `<script>` do Astro com escopo restrito, usando APIs padrão do modelo de objeto de documento (DOM).

### Inicie o site

Para facilitar a execução do site, há uma tarefa `npm run dev` que inicia o único servidor de desenvolvimento do Astro. Siga estas etapas para executá-la no GitHub Codespaces:

1. Volte ao Codespace. Você deve estar no branch `main`, após o exercício anterior.
2. Abra um novo terminal no Codespace pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie um branch para o trabalho de filtragem e alterne para ele:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Execute o seguinte comando para iniciar o site:

   ```bash
   npm run dev
   ```

   Quando o servidor de desenvolvimento Astro estiver pronto, você verá um aviso com o endereço, semelhante a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se for aberta uma caixa de diálogo perguntando se você quer abrir uma janela do navegador para `http://localhost:4321`, feche-a selecionando **x**.

5. Abra o site mantendo <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) pressionada enquanto seleciona o endereço do servidor Astro `http://localhost:4321` no terminal.

> [!NOTE]
> Em um Codespace, selecionar o link do endereço localhost no terminal redireciona você automaticamente para `https://<your-codespace-name>-4321.app.github.dev/`. Esse endereço é um túnel privado para o Codespace, que agora está hospedando o servidor Web.

### Explore o site

Com o site em execução, explore suas funcionalidades. Os principais recursos incluem:

- **Página inicial**: exibe uma lista de jogos de tabuleiro com títulos, imagens e descrições.
- **Página de detalhes do jogo**: quando você seleciona um jogo, é direcionado a uma página com mais informações sobre ele, incluindo título, descrição, editora e categoria.

## Explore o backlog com o Copilot

> [!TIP]
> **Abra o Copilot Chat**
>
> Uma conversa limpa ajuda a manter o contexto relevante para a tarefa. O modo e a seleção do modelo variam conforme o exercício — cada etapa indicará o que fazer quando isso for relevante.

A primeira versão do site funciona, mas queremos aprimorá-la com novos recursos. Comece revisando o backlog. A configuração do projeto a partir do modelo criou automaticamente um conjunto de issues; peça ao GitHub Copilot que mostre esses itens.

1. Volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa.
2. No seletor de agentes da exibição Chat, selecione **Agent**. A opção **Agent** planeja e implementa alterações em vários arquivos de forma autônoma, executa comandos no terminal e usa ferramentas.

   ![Captura de tela do seletor de agentes na exibição Chat.](../../../_images/shared-chat-mode-selector.png)

3. Selecione **Claude Sonnet 4.5** na lista de modelos disponíveis.

> [!CAUTION]
> Os autores deste workshop não estão recomendando um modelo em particular. Durante a criação do workshop, usamos o Claude Sonnet 4.5 e o incluímos nas instruções para que as sugestões de código fossem relativamente consistentes e a experiência fosse boa. No entanto, como os modelos de linguagem de grande porte (LLMs) são probabilísticos, as sugestões podem ser diferentes das indicadas no workshop. Isso é normal e esperado.

> [!NOTE]
> Devido à natureza probabilística dos LLMs, o Copilot pode usar um comando do Model Context Protocol (MCP) diferente, mas ainda deve conseguir concluir a tarefa.

4. Peça ao Copilot que mostre o backlog de issues enviando o seguinte prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

5. Selecione **Continue** para executar o comando que lista todas as issues.
6. Revise a lista de issues gerada.

Observe que o Copilot também priorizou os itens de acordo com o que considera mais útil para as pessoas usuárias.

## Revise os arquivos de instruções

Antes de pedir ao agente que gere código, revise o arquivo de instruções que fornecerá contexto ao Copilot. Você usará o arquivo de instruções da [interface do usuário (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que explica como abordar a adição de funcionalidades ao site.

1. No Codespace, acesse `.github/instructions/ui.instructions.md`.
2. Observe as orientações gerais para adicionar funcionalidades, incluindo:
   - uma visão geral da arquitetura;
   - princípios de design de componentes, capacidade de teste e acessibilidade;
   - links para arquivos de instruções específicos de vários tipos de arquivo, incluindo:
     - Astro;
     - Tailwind CSS;
     - Drizzle.

> [!TIP]
> Os arquivos de instruções permitem fazer referência a outros arquivos de instruções e a arquivos do projeto. Os caminhos são relativos ao arquivo de instruções. Assim, você pode reutilizar orientações, dividir conjuntos maiores de instruções em arquivos menores e fornecer exemplos e modelos.

## Implemente a funcionalidade de filtragem

Para concluir a filtragem, serão necessárias pelo menos três alterações distintas no aplicativo:

- adicionar ou aprimorar a lógica restante de filtragem na camada de dados (`src/lib/`);
- adicionar ou atualizar testes do comportamento de filtragem;
- atualizar a página de listagem de jogos para incluir a interface de filtragem.

Além disso, os testes precisam ser executados e aprovados antes de mesclar tudo à base de código. O modo de agente do Copilot pode realizar essas tarefas. Vamos adicionar a funcionalidade.

1. Continue a conversa atual com o Copilot ou selecione **New Chat** para iniciar outra.
2. Selecione **Add Context**, **Instructions** e **ui** como o arquivo de instruções.

   ![Captura de tela mostrando um exemplo de seleção do arquivo de instruções da interface do usuário.](../../../_images/ex3-select-instructions-file.png)

3. No seletor de agentes da exibição Chat, confirme que **Agent** continua selecionado.

   ![Captura de tela do seletor de agentes na exibição Chat.](../../../_images/shared-chat-mode-selector.png)

4. Confirme que **Claude Sonnet 4.5** continua selecionado como modelo.
5. Peça ao Copilot que implemente a funcionalidade conforme os requisitos da issue relacionada no backlog, usando o seguinte prompt:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observe o Copilot explorar o projeto e localizar os arquivos relacionados à funcionalidade. Ele deve encontrar as funções auxiliares da camada de dados, a interface e os testes. Em seguida, começará a modificar os arquivos e executar os testes.

   ![Captura de tela do Copilot explorando os arquivos do projeto.](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot executará várias tarefas, como explorar o projeto, modificar arquivos e rodar testes. Isso pode levar alguns minutos, dependendo da complexidade da tarefa e da base de código. Durante o processo, talvez apareçam os botões **Keep** e **Undo** no editor. Quando o Copilot terminar, haverá um botão **Keep** ou **Undo** para cada alteração; por isso, não é necessário selecioná-los enquanto o trabalho estiver em andamento.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.

   ![Captura de tela de uma caixa de diálogo no painel Copilot Chat pedindo confirmação para executar os testes.](../../../_images/ex3-agent-mode-run-tests.png)

8. Pode haver pausas e até falhas em alguns testes durante o processo. Não há problema: o Copilot alterna entre gerar código e executar testes até concluir a tarefa e não detectar erros.

   ![Captura de tela de uma sessão completa do Copilot no modo de agente.](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Examine o código gerado para identificar possíveis problemas.

> [!CAUTION]
> É sempre importante revisar o código gerado pelo Copilot ou por qualquer outra ferramenta de inteligência artificial (IA).

10. Volte ao navegador com o site em execução e explore a nova funcionalidade.
11. Depois de confirmar que tudo funciona e revisar o código, selecione **Keep** na janela Copilot Chat.

## Resumo e próximos passos

Neste exercício, você:

- usou o modo de agente do Copilot para explorar o projeto, identificar os arquivos relevantes e coordenar alterações;
- usou o modo de agente do GitHub Copilot para implementar novos recursos na UI e na camada de dados;
- revisou as alterações e os testes gerados pelo modo de agente do GitHub Copilot antes de mesclá-los à base de código.

Agora, [teste o recurso com o servidor MCP do Playwright][next-lesson] e abra um pull request.

### Exercício extra: implemente a paginação

À medida que a lista de jogos crescer, será necessário implementar a paginação. Use o que aprendeu neste exercício para pedir ao Copilot que atualize o site com esse recurso.

1. Peça ao Copilot que implemente a paginação e forneça as orientações necessárias para obter o resultado desejado.
2. Ao elaborar o prompt, considere as seguintes decisões:
   - seguir as práticas recomendadas existentes, incluindo o uso dos arquivos de instruções atuais;
   - decidir como implementar a paginação, por exemplo, se as pessoas usuárias poderão selecionar o tamanho da página ou se ele será fixo;
   - talvez seja necessário iterar com o GitHub Copilot, pedindo alterações e fornecendo contexto. Esse é o fluxo normal ao trabalhar com o Copilot.

## Recursos

- [Modos ask, edit e agent do Copilot: o que fazem e quando usar cada um][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
