---
title: "Exercício 3 - Teste o recurso com o servidor Model Context Protocol (MCP) do Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Exercício anterior: Modo de agente][previous-lesson] · [Próximo exercício: Agentes personalizados →][next-lesson]

Você acabou de criar o recurso de filtragem com o modo de agente. Antes de abrir um pull request, confirme que ele funciona no navegador. Em vez de navegar pelo aplicativo por conta própria, conecte o servidor MCP do Playwright e deixe o Copilot controlar um navegador real para testar o recurso. Depois, publique o branch e abra o pull request (PR).

Neste exercício, você vai:

- aprender o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionar o servidor MCP do Playwright ao espaço de trabalho.
- pedir ao Copilot que use o servidor para testar manualmente o recurso de filtragem em um navegador.
- publicar o branch e abrir um pull request para o trabalho de filtragem.

## O que é o Model Context Protocol (MCP)?

O modo de agente se torna muito mais poderoso quando pode acessar recursos além do editor. O Model Context Protocol (MCP) permite isso: é um padrão para o agente se comunicar com ferramentas e serviços externos.

![Diagrama que mostra como o modo de agente interage com contexto, modelo de linguagem de grande porte (LLM) e ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de inteligência artificial (IA) se comuniquem com ferramentas e serviços externos. Com o MCP, os agentes podem acessar informações atualizadas usando recursos e executar ações em seu nome usando ferramentas.

Essas ferramentas e esses recursos são acessados por um servidor MCP, que funciona como uma ponte entre o agente de IA e as ferramentas e os serviços externos. O servidor MCP gerencia a comunicação entre o agente e as ferramentas externas, como interfaces de programação de aplicações (APIs) existentes ou ferramentas locais, por exemplo, pacotes npm. Cada servidor MCP representa um conjunto diferente de ferramentas e recursos que o agente pode acessar.

Alguns servidores MCP conhecidos:

- **[GitHub MCP Server][github-mcp-server]**: fornece acesso a APIs para gerenciar repositórios do GitHub. O agente de IA pode, por exemplo, criar repositórios, atualizar os existentes e gerenciar issues e pull requests.
- **[Playwright MCP Server][playwright-mcp-server]**: fornece recursos de automação de navegador com o Playwright. O agente de IA pode, por exemplo, navegar por páginas da Web, preencher formulários e selecionar botões.

Há muitos outros servidores MCP que fornecem acesso a diferentes ferramentas e recursos. O GitHub hospeda um [registro de MCP][mcp-registry] para facilitar a descoberta de servidores e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique o publicador e considere as implicações de segurança. Use somente servidores MCP confiáveis e tenha cuidado ao conceder acesso a recursos ou operações confidenciais.

## Revise a configuração do MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste espaço de trabalho do VS Code.

1. Abra `.vscode/mcp.json` no Codespace.
2. Confirme que já há um servidor `github` configurado:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

A entrada `github` vem do modelo do projeto. Por isso, o Copilot conseguiu ler o backlog de issues no exercício anterior. Ela usa o [servidor MCP remoto do GitHub][remote-github-mcp-server], então não é necessário instalar nada localmente: o VS Code se conecta por HTTP e você se autentica no GitHub na primeira vez que o Copilot usa uma das ferramentas.

## Adicione o servidor MCP do Playwright

Agora, adicione um segundo servidor. O [servidor MCP do Playwright][playwright-mcp-server] fornece ao Copilot um navegador que ele pode controlar, permitindo testar o recurso.

1. Em `.vscode/mcp.json`, adicione uma entrada `playwright` ao lado de `github`, para que o arquivo fique assim:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. Salve o arquivo.

Diferentemente do servidor remoto `github`, `playwright` é um servidor **local**: o VS Code o inicia no computador executando `npx @playwright/mcp@latest`. O sinalizador `--headless` faz o Playwright executar o navegador sem uma janela visível. Isso é necessário em um Codespace, que não tem um desktop para exibi-la.

> [!NOTE]
> O projeto Tailspin Toys já usa o Playwright para testes de ponta a ponta, então o navegador necessário geralmente já está instalado. Se o Copilot informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Inicie e autorize o servidor

O VS Code inicia servidores MCP **sob demanda**: na primeira vez que o Copilot precisa das ferramentas de um servidor, o VS Code o inicia e pede que você confirme que confia nele.

1. Em `.vscode/mcp.json`, localize a ação **Start**, exibida acima da entrada `playwright`. Selecione-a para iniciar o servidor agora e confirmar que a configuração está correta.
2. Se o VS Code pedir que você confirme se confia no servidor, revise a configuração e escolha a opção para confiar nele.

Iniciar o servidor manualmente é opcional. Se você ignorar essas etapas, o VS Code iniciará o servidor e pedirá que você confie nele na primeira vez que o Copilot precisar das ferramentas, na próxima etapa.

## Teste o recurso de filtragem

O [servidor MCP do Playwright][playwright-mcp-server] fornece ao Copilot um navegador real. Em vez de navegar pelo aplicativo por conta própria, o agente pode abrir uma página, navegar, aplicar filtros, ler os resultados e resumir o que observou. Assim, você pode confirmar rapidamente se o recurso se comporta como esperado sem sair da conversa.

O servidor MCP do Playwright usa a [árvore de acessibilidade][playwright-mcp-server] da página, não capturas de tela. Isso significa que o agente analisa elementos estruturados e rotulados — botões, links e itens de lista — da mesma forma que a tecnologia assistiva. Assim, uma verificação funcional rápida também oferece uma avaliação básica de acessibilidade.

Com o servidor conectado e o aplicativo em execução, peça ao Copilot que teste o recurso de filtragem:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

O Copilot abrirá um navegador pelo servidor MCP do Playwright, seguirá cada etapa e informará o que encontrou. Compare o resumo com os critérios de aceitação da issue. Se algo parecer errado, faça perguntas de acompanhamento ou peça que ele corrija o código antes de abrir um pull request.

> [!NOTE]
> O aplicativo precisa estar em execução em `http://localhost:4321` para este teste. Se você parou o servidor de desenvolvimento, inicie-o novamente antes de enviar o prompt. Na primeira vez que o Copilot usar o servidor MCP do Playwright, talvez seja necessário baixar um navegador. Se o Copilot informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publique o branch e crie um pull request

Agora que confirmou que o recurso funciona, abra um pull request (PR) para que a equipe possa revisá-lo. Primeiro, publique o branch `filtering-vscode`.

1. No Codespace, abra o painel **Source Control** e revise as mudanças feitas pelo Copilot.
2. Prepare as mudanças selecionando o ícone **+**.
3. Gere uma mensagem de commit usando o botão **Sparkle**.

   ![Captura de tela do painel Source Control com as mudanças feitas](../../../_images/ex3-source-control-changes.png)

4. Selecione **Publish** para enviar o branch ao repositório.

## Crie o pull request

Há várias maneiras de criar um pull request, incluindo o github.com e a interface de linha de comando do GitHub (CLI). Como você já está usando o GitHub Copilot, peça que ele crie o PR. Ele pode localizar a issue correspondente e associá-la ao PR.

1. Abra o painel Copilot Chat e selecione **New Chat** para iniciar uma sessão.
2. No seletor de agentes, confirme que **Agent** está selecionado para que o Copilot possa usar as ferramentas do GitHub.
3. Peça ao Copilot que crie o PR:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Quando necessário, selecione **Continue** para permitir que o Copilot reúna informações e execute operações. Na primeira vez que ele usar uma ferramenta do GitHub, talvez seja necessário autenticar-se. Siga as instruções para permitir o acesso.
5. Observe o Copilot pesquisar as issues, localizar a correta e criar o PR.
6. Selecione o link criado pelo Copilot para revisar o pull request, mas **não o mescle ainda**.

## Resumo e próximos passos

Parabéns! Neste exercício, você:

- aprendeu o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionou o servidor MCP do Playwright ao espaço de trabalho.
- usou o servidor para testar manualmente o recurso de filtragem em um navegador antes da entrega.
- publicou o branch e abriu um pull request para o trabalho de filtragem.

Você usou um servidor MCP para *testar* um recurso, mas o MCP é apenas uma das maneiras de ampliar o Copilot. Em seguida, [crie um agente personalizado][next-lesson] para agilizar tarefas específicas, como revisões de acessibilidade.

## Recursos

- [O que é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP do GitHub][github-mcp-server]
- [Registro de MCP do GitHub][mcp-registry]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
