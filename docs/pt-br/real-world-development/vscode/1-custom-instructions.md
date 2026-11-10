---
title: "Exercício 1: Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Exercício anterior: Pré-requisitos][previous-lesson] · [Próximo exercício: Modo de agente →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial generativa. Se uma tarefa precisar ser feita de uma maneira específica — ou se houver informações de contexto que o Copilot deva conhecer —, você precisa garantir que ele possa acessá-las. Há várias maneiras de compartilhar contexto específico com o Copilot. Uma das principais é usar os [arquivos de instruções][instruction-files], que permitem orientar a geração de código.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e de arquivos de instruções com escopo por caminho;
- gerar a primeira parte da camada de dados para a filtragem (uma função auxiliar para editoras) com as instruções atuais;
- adicionar um novo padrão para todo o repositório a `.github/copilot-instructions.md`;
- executar o mesmo prompt novamente e observar o código gerado adotar o novo padrão;
- confirmar as atualizações das instruções e a primeira parte da camada de dados para filtragem em `main`, para que o Copilot use as orientações atualizadas no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir alguns dos padrões que você definiu. O Copilot não é determinístico. O objetivo deste exercício é observar a tendência de mudança de comportamento após a atualização das instruções, não obter resultados idênticos caractere por caractere.

## Arquivos de instruções

### Cenário

Como toda boa empresa de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento. Eles incluem:

- a camada de dados sempre precisa ter testes de unidade;
- a interface do usuário deve usar o modo escuro e ter uma aparência moderna;
- o código deve incluir documentação no formato de comentários TSDoc;
- cada arquivo deve começar com um bloco de comentários que descreva sua finalidade.

Com os arquivos de instruções, você garantirá que o Copilot tenha as informações necessárias para executar as tarefas de acordo com essas práticas.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot para que ele entenda melhor seu estilo de codificação e seus requisitos. Elas ajudam a orientar o Copilot a sugerir código e trechos mais relevantes. Você pode especificar convenções de codificação, bibliotecas e até os tipos de comentários que prefere. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos, oferecendo contexto direcionado à tarefa.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`: um único arquivo de instruções enviado ao Copilot em **todas** as solicitações feitas no repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações feitas ao Copilot Chat ou à interface de linha de comando (CLI) do Copilot, como a pilha de tecnologias, uma visão geral do que está sendo desenvolvido, práticas recomendadas e orientações gerais.
- Arquivos `.github/instructions/*.instructions.md`, que podem ser criados para tarefas ou tipos de arquivo específicos. Você pode usá-los para definir orientações para linguagens específicas, como TypeScript ou Astro, ou para tarefas como criar um componente de interface ou um novo conjunto de testes de unidade.

> [!NOTE]
> No ambiente de desenvolvimento integrado (IDE), os arquivos de instruções são usados apenas para gerar código no Copilot Chat — não para conclusões de código nem sugestões de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente na nuvem do Copilot usam os arquivos de instruções do repositório e os arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [oferece suporte a arquivos de instruções][custom-instructions-support] que seguem outros padrões, como AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma conversa completa sobre a criação de arquivos de instruções está fora do escopo deste workshop. No entanto, os exemplos do projeto demonstram uma abordagem representativa. Em linhas gerais:

- Mantenha as instruções em `copilot-instructions.md` focadas nas orientações do projeto, como uma descrição do que está sendo desenvolvido, a estrutura do projeto e os padrões globais de codificação.
- Use arquivos `*.instructions.md` para fornecer orientações específicas a tipos de arquivo (testes de unidade, componentes Astro e camada de dados) ou tarefas.
- Use linguagem natural e mantenha as orientações claras. Inclua exemplos de como o código deve ou não deve ser escrito.

Não há uma única maneira correta de criar arquivos de instruções, assim como não há uma única maneira de usar a inteligência artificial. Ao experimentar, você descobrirá o que funciona melhor para o seu projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deve ter um conjunto sólido de arquivos de instruções. Ao explorar os arquivos deste projeto, você verá instruções para vários tipos de tarefas, incluindo [atualizações da interface do usuário (UI)][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface oferece essa opção de um jeito diferente — por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI. O exercício referente à interface que você está usando indicará a opção quando for relevante.
>
> Para encontrar modelos ou um ponto de partida, explore o [awesome-copilot][awesome-copilot], um repositório com arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas deste projeto

Leia os arquivos de instruções fornecidos com este repositório: há um arquivo principal, `copilot-instructions.md`, e vários arquivos `*.instructions.md` para diferentes tarefas. Abra-os no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo e observe a breve descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Essas orientações, incluindo a subseção **GitHub Actions Workflows** em **Code standards**, aplicam-se a todas as interações com o Copilot.
3. Abra a pasta `.github/instructions` e explore seu conteúdo. Observe que há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início do arquivo: ele define um padrão global relativo à raiz do repositório que determina a quais arquivos as instruções se aplicam. Neste caso, qualquer arquivo de teste TypeScript — por exemplo, um que corresponda a `**/*.test.ts` — será incluído.
5. Observe as instruções específicas para criar testes de unidade neste projeto.
6. Por fim, abra `.github/instructions/drizzle.instructions.md` e vá até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes no projeto. Isso permite dividir conjuntos maiores de instruções em arquivos menores e reutilizáveis, além de indicar ao Copilot exemplos para seguir ao gerar código. Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentários nos arquivos.

## Crie um branch para as alterações

Siga as práticas recomendadas criando um branch para as alterações.

1. Volte ao Codespace do exercício anterior.
2. Abra um novo terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie um branch e alterne para ele:

   ```bash
   git checkout -b custom-instructions
   ```

## Use o Copilot Chat *antes* de atualizar as instruções

> [!TIP]
> **Abra o Copilot Chat**
>
> Uma conversa limpa ajuda a observar o efeito das instruções. O modo e a seleção do modelo variam conforme o exercício; cada etapa indicará o que fazer quando isso for relevante.

Para observar o impacto das instruções personalizadas, comece enviando um prompt com o arquivo de instruções atual. Mais adiante, você o atualizará e enviará o mesmo prompt novamente para comparar os resultados.

1. Volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa.
2. Feche as guias abertas no editor que vieram dos exercícios anteriores para que o Copilot use somente o contexto desejado.
3. Abra `src/lib/publishers.ts` para indicar ao Copilot onde a função auxiliar deve ficar.
4. No seletor de agentes da exibição Chat, selecione **Agent** para que o Copilot possa aplicar alterações aos arquivos.

   ![Captura de tela do seletor de agentes na exibição Chat.](../../../_images/shared-chat-mode-selector.png)

5. Envie o seguinte prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

6. O Copilot explorará o projeto e aplicará atualizações ao código, muitas vezes incluindo o arquivo da função auxiliar e os testes.
7. Observe que a função auxiliar proposta é tipada, recebe um cliente `db` como primeiro argumento e retorna uma matriz tipada de editoras. Essas características vêm das convenções da camada de dados definidas em `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
8. Observe que o código proposto **não inclui** comentários TSDoc nem um cabeçalho de comentários no arquivo.

> [!CAUTION]
> Como as respostas do Copilot são probabilísticas, ele pode adicionar comentários de documentação mesmo sem essa orientação. Se isso acontecer, tudo bem: o objetivo continua sendo observar a melhoria de consistência após a atualização das instruções.

## Adicione um novo padrão ao repositório

Como explicado anteriormente, `.github/copilot-instructions.md` fornece informações do projeto ao Copilot. Documente os padrões de codificação do repositório para melhorar as sugestões de código.

1. Abra `.github/copilot-instructions.md` novamente.
2. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Observe como ela documenta os padrões de codificação do projeto, mas ainda não tem uma regra para a documentação no código. Por isso, a função auxiliar gerada não tinha comentários de documentação.
3. Adicione as seguintes linhas de Markdown logo abaixo dos padrões existentes para orientar o Copilot a adicionar cabeçalhos de comentários aos arquivos e comentários TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu no exercício anterior, os arquivos de instruções podem ser criados no nível do repositório (`.github/copilot-instructions.md`) para fornecer orientações globais, ou como arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo no nível do repositório é o lugar certo para padrões aplicáveis ao projeto inteiro, como a regra sobre comentários de documentação que você acabou de adicionar.

## Execute o prompt novamente e observe a mudança

Envie o mesmo prompt mais uma vez para verificar se o novo padrão alterou o código proposto.

1. Volte ao Copilot Chat e selecione **New Chat** para limpar o histórico da conversa.
2. Selecione `src/lib/publishers.ts` para que o Copilot se concentre no arquivo correto.
3. Envie novamente o **mesmo prompt**:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Observe que o arquivo proposto agora começa com um bloco de comentários semelhante a este:

   ```typescript
   /**
    * Funções auxiliares de acesso a dados de editoras para a plataforma de financiamento coletivo da Tailspin Toys.
    * Fornece funções para recuperar informações de editoras do banco de dados.
    */
   ```

5. Observe que a função proposta agora inclui um comentário TSDoc semelhante a este:

   ```typescript
   /**
    * Retorna uma lista de todas as editoras com seus identificadores e nomes.
    *
    * @param db - O cliente do banco de dados Drizzle.
    * @returns Uma promessa que é resolvida com uma matriz de objetos de editoras.
    */
   ```

Você orientou o Copilot a seguir um novo padrão do projeto e aplicá-lo a código real que servirá de base para o próximo exercício.

## Faça commit das instruções e publique o branch

Os arquivos de instruções são gerenciados pelo controle de versão como qualquer outro recurso do projeto. Confirme as alterações e publique o branch no repositório.

1. Abra uma nova janela do terminal pressionando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. No terminal, confirme que as instruções atualizadas e as alterações na função auxiliar estão presentes executando:

   ```bash
   git status
   ```

3. No terminal, prepare e confirme as atualizações das instruções e todos os arquivos alterados pelo Copilot para criar a base da função auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Se git status mostrar outras atualizações de suporte (por exemplo, testes), adicione esses arquivos também.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie o branch ao repositório:

   ```bash
   git push -u origin custom-instructions
   ```

## Crie e mescle um pull request

Com o branch publicado, crie um pull request (PR) e associe-o à issue do padrão de documentação no backlog. Peça ao Copilot que localize a issue, crie o PR para encerrá-la e, em seguida, faça a mesclagem.

> [!NOTE]
> Neste exercício, pela primeira vez o Copilot atuará no GitHub por você. O modelo do projeto já conecta as ferramentas do GitHub ao seu espaço de trabalho, então não é necessário configurar nada. Na primeira vez que o Copilot usar uma delas, o VS Code talvez solicite que você entre no GitHub. Siga as instruções para permitir o acesso. Você aprenderá como essa conexão funciona — por meio do Model Context Protocol (MCP) — em um exercício futuro.

1. Abra o Copilot Chat no Codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir a exibição Copilot Chat e confirme que **Agent** está selecionado no seletor de agentes.
3. Peça ao Copilot para localizar a issue relacionada à atualização dos arquivos de instruções e criar um PR a partir do branch atual, descrevendo tanto as atualizações das instruções quanto a nova base da função auxiliar para editoras:

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Quando o Copilot pedir permissão para executar ações no GitHub em seu nome, revise o comando e selecione **Allow** se for apropriado.
5. Depois que o PR for criado, peça ao Copilot que faça a mesclagem e volte para `main`:

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. Quando o Copilot pedir permissão para executar ações no GitHub e comandos do shell em seu nome, revise o comando e selecione **Allow** se for apropriado.

Você criou e mesclou um pull request com a ajuda do GitHub Copilot.

## Resumo e próximos passos

Neste exercício, você:

- explorou como o Copilot usa os arquivos de instruções deste projeto;
- enviou um prompt de geração de código e observou o resultado com as instruções existentes;
- adicionou um novo padrão para todo o repositório a `.github/copilot-instructions.md`;
- executou o mesmo prompt novamente e observou o código proposto adotar o novo padrão;
- confirmou as instruções e a base da função auxiliar para editoras em `main` para que o próximo exercício possa usá-las.

Agora, coloque essas instruções em prática no [modo de agente][next-lesson] enquanto o Copilot adiciona um novo recurso ao código.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
