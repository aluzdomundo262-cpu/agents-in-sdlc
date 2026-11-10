---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Exercício anterior: Instruções personalizadas][previous-lesson] |
|:--|

É provável que poucas organizações não enfrentem problemas com dívida técnica. Isso pode incluir problemas de segurança não resolvidos, código legado que precisa de atualizações ou solicitações de funcionalidades que ficaram paradas na lista de pendências por falta de tempo para implementá-las. O agente de nuvem do GitHub Copilot foi desenvolvido para executar tarefas como atualizar código e adicionar funcionalidades de forma autônoma. Quando termina o trabalho, ele gera um pull request (PR) em rascunho para que um desenvolvedor revise. Assim, é possível delegar tarefas tediosas, acelerar o processo de desenvolvimento e liberar os desenvolvedores para se concentrarem em questões mais amplas.

Neste exercício, você vai explorar os seguintes aspectos do agente de nuvem do Copilot:

- personalizar o ambiente usado para gerar código.
- garantir que as operações sejam executadas com segurança.
- entender a importância de issues com escopo bem definido.
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys tem algumas dívidas técnicas que gostaria de resolver. Os prestadores de serviço contratados inicialmente para criar a primeira versão do site deixaram a documentação em um estado insatisfatório: ela está completamente ausente. Como primeiro passo, a equipe gostaria de adicionar comentários de documentação do TypeScript (TSDoc) a todas as funções exportadas do aplicativo.

Além disso, a equipe de design está pronta para melhorar a descoberta de jogos. A página de detalhes de cada jogo deve mostrar jogos relacionados — outros títulos da mesma categoria — para que as pessoas continuem navegando. A equipe ainda não precisa de uma implementação refinada; quer apenas algo que possa usar para testes de aceitação da experiência do usuário (UX). No momento, isso é um impedimento, mas há outras issues com prioridade maior.

Esses são exemplos de tarefas que podem acabar sendo adiadas e que são ótimas candidatas para atribuir ao agente de nuvem do Copilot. O agente pode trabalhar nelas de forma assíncrona enquanto o desenvolvedor se dedica a outras tarefas e, depois, volta para revisar o trabalho e confirmar se está tudo como esperado.

## Apresentação do agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) pode executar tarefas em segundo plano, de maneira semelhante a um desenvolvedor. Assim como no trabalho com um desenvolvedor, há várias formas de atribuir tarefas, inclusive [atribuindo uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois que você atribui a issue, o Copilot cria um PR em rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar na tarefa. Você pode acompanhar a sessão do Copilot enquanto ela está em andamento ou depois que termina. Quando a solução proposta estiver pronta para revisão, o Copilot marcará você no PR.

## A importância de instruções com escopo bem definido

Não há mágica no GitHub Copilot: não é possível deixar de pensar no problema. Até operações aparentemente simples ficam complexas quando examinadas de perto; por isso, [defina com cuidado o escopo das tarefas para o agente de nuvem do Copilot][cloud-agent-best-practices]. Trate-o como um parceiro de programação com inteligência artificial (IA): trabalhe em etapas, aprenda, experimente e adapte o processo. Os fundamentos do desenvolvimento de software não mudam com a inclusão da IA generativa.

## Instruções personalizadas neste repositório

Os exercícios anteriores apresentaram instruções personalizadas e explicaram como elas orientam o Copilot. Se você já fez o exercício prático sobre instruções personalizadas, viu o arquivo `.github/copilot-instructions.md` em ação; caso contrário, esta é uma boa oportunidade para examiná-lo rapidamente. Antes de atribuir tarefas ao agente de nuvem do Copilot, consulte os arquivos de instruções já incluídos neste repositório, sem alterá-los, para depois identificar seus efeitos.

Abra os arquivos a seguir na interface Web do GitHub para seu repositório ou em um codespace, caso já tenha um em execução:

- `.github/copilot-instructions.md` — examine a seção **Code standards**, especialmente as expectativas sobre convenções de TypeScript e comentários de documentação TSDoc.
- `.github/instructions/unit-tests.instructions.md` — observe o frontmatter `applyTo`, que define o escopo dessas instruções para arquivos `**/*.test.ts`.

Quando você atribuir ao agente de nuvem a issue `Code lacks documentation` na próxima seção, observe se o PR resultante inclui comentários de documentação TSDoc, segue as convenções de TypeScript e tem cabeçalhos de comentário. Esses elementos vêm dos arquivos de instruções. Voltaremos a isso ao revisar PRs em um exercício posterior.

## Configure o ambiente de desenvolvimento do agente de nuvem do Copilot

A criação de código, independentemente de quem a executa, geralmente exige um ambiente específico e scripts de configuração para garantir que tudo esteja em boas condições. O mesmo vale ao atribuir tarefas ao Copilot, que trabalha de maneira semelhante a um engenheiro de software (SWE).

O agente de nuvem usa o [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente criando um [workflow de configuração especial][setup-workflow], definido no arquivo `.github/workflows/copilot-setup-steps.yml`, para ser executado antes de o agente começar a trabalhar. Assim, ele tem acesso às ferramentas e dependências de desenvolvimento necessárias. Esse workflow já foi configurado para facilitar o andamento do laboratório e permitir que você conheça esse recurso. Ele garante que o Copilot tenha acesso ao Node.js, às dependências do projeto, aos binários de navegador para testes de ponta a ponta e ao banco de dados SQLite migrado e preenchido com dados para o único aplicativo Astro:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões no menor nível possível para *suas etapas*. O Copilot receberá o próprio token para as operações dele.
    permissions:
      # Se quiser clonar o repositório como parte das etapas de configuração, por exemplo, para instalar dependências, você precisará da permissão `contents: read`. Se não clonar o repositório nessas etapas, o Copilot fará isso automaticamente depois que elas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend/aplicativo - Node.js (o aplicativo inteiro agora usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra e preenche o banco de dados SQLite local para que compilações e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

Esse arquivo se parece com qualquer outro workflow do GitHub, mas tem alguns pontos importantes:

- Ele contém um único job chamado `copilot-setup-steps`. Esse job é executado no GitHub Actions antes de o Copilot começar a trabalhar no PR.
- Observe o gatilho `workflow_dispatch`, que permite executar o workflow manualmente na guia **Actions** do repositório. Isso é útil para testar se o workflow funciona corretamente, sem precisar esperar o Copilot executá-lo.

## Adicione a documentação

Embora todos reconheçam a importância da documentação, a maioria dos projetos tem informações desatualizadas ou não tem documentação. Esse tipo de dívida técnica costuma ficar sem solução, o que reduz a produtividade e dificulta a manutenção da base de código ou a integração de novos desenvolvedores. Felizmente, o Copilot é muito útil para criar documentação, e esta é uma issue ideal para atribuir ao agente de nuvem. Ele trabalhará em segundo plano para gerar a documentação necessária. Em um exercício futuro, você voltará para revisar o trabalho.

1. Abra seu repositório no github.com em uma nova guia do navegador.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para criar a issue.
5. Defina **Title** como `Code lacks documentation`.
6. Defina **Description** como:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição de uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.
10. Selecione a guia **Pull Requests**.
11. Abra o PR recém-gerado, cujo título será parecido com `[WIP]: Code lacks documentation`. Se nenhum PR novo aparecer na lista, aguarde um ou dois minutos e atualize a janela do navegador.
12. Depois de alguns minutos, o Copilot deverá criar uma lista de tarefas.

> [!NOTE]
> A lista de tarefas do Copilot pode levar vários minutos para aparecer no PR. O Copilot está criando o ambiente (executando o workflow mencionado anteriormente), analisando o projeto e determinando a melhor abordagem para resolver o problema.

13. Examine a lista e as tarefas que o Copilot executará.
14. Role a linha do tempo do PR para baixo. Você deverá ver uma atualização informando que o Copilot começou a trabalhar na issue.
15. Selecione o botão **View session**.

  ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode percorrer a sessão em tempo real e acompanhar como o Copilot resolve o problema. Isso inclui explorar o código e entender o estado do projeto, fazer pausas para analisar e decidir o plano adequado e criar código.

Esse processo provavelmente levará alguns minutos. Um dos principais objetivos do agente de nuvem do Copilot é executar tarefas de forma assíncrona, liberando você para se concentrar em outras atividades. Vamos aproveitar esse recurso: enquanto o agente recebe outra tarefa, você começará a escrever código para adicionar funcionalidades ao aplicativo.

## Adicione uma seção de jogos relacionados à página de detalhes do jogo

Como já vimos, uma das grandes vantagens do agente de nuvem do GitHub Copilot é dividir o trabalho para que você possa se concentrar em um conjunto de tarefas enquanto ele cuida de outro. Mesmo que a criação de uma seção de jogos relacionados para a equipe de design não leve muito tempo, esse tempo pode ser usado em outras atividades. Vamos atribuir a tarefa ao agente de nuvem do Copilot.

1. Volte ao seu repositório no github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para usar o modelo em branco.
5. Defina **Title** como `Show related games on the game details page`.
6. Defina **Description** como:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecione **Create** para criar a issue.
8. No lado direito, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

  ![Atribuição de uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Logo depois, você verá um conjunto de 👀 no primeiro comentário da issue, indicando que o Copilot começou a trabalhar nela.

![O Copilot usa o emoji de olhos para indicar que está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

Agora o Copilot está trabalhando na segunda solicitação. O agente de nuvem do Copilot funciona de maneira semelhante a um SWE, então você não precisa acompanhá-lo ativamente: basta revisar o trabalho quando ele estiver concluído. Agora, vamos criar e usar agentes personalizados.

## Resumo e próximos passos

Neste exercício, você explorou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com o agente de nuvem, você pode atribuir issues ao Copilot para que ele as execute de forma assíncrona. Você pode usar o Copilot para resolver dívidas técnicas, criar funcionalidades ou ajudar a migrar código de uma estrutura para outra.

Você explorou estes conceitos:

- personalizar o ambiente usado para gerar código.
- garantir que as operações sejam executadas com segurança.
- entender a importância de issues com escopo bem definido.
- atribuir issues ao Copilot.

Enquanto o agente de nuvem trabalha em segundo plano, você pode se concentrar em criar e usar agentes personalizados. O [agente de nuvem do Copilot também pode usar servidores do Model Context Protocol (MCP)][cloud-agent-mcp] e tem acesso a instruções personalizadas, que foram abordadas em módulos anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuição de issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem do Copilot][cloud-agent-best-practices]

| [Próximo exercício: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
