---
title: "Exercício 1 - Instruções personalizadas (agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Exercício anterior: Pré-requisitos][previous-lesson] · [Próximo exercício: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial (IA) generativa. Se uma tarefa precisar ser feita de uma maneira específica — ou houver informações de contexto que o Copilot deva conhecer — disponibilize esse contexto. Os [arquivos de instruções][instruction-files] fornecem orientações para que o Copilot entenda não apenas *o que* você quer, mas também *como* o trabalho deve ser feito.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e de arquivos de instruções com escopo por caminho.
- adicionar um novo padrão para todo o repositório a `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos percursos do VS Code e do CLI, aqui você não executará um prompt *antes e depois*. O agente de nuvem do Copilot trabalha de forma assíncrona com issues do GitHub, então é mais difícil demonstrar o impacto lado a lado em tempo real. Você verá a influência do arquivo de instruções mais adiante, ao revisar os pull requests produzidos pelo agente.

## Arquivos de instruções

### Cenário

Como toda boa empresa de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para suas práticas de desenvolvimento. Eles incluem:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário deve usar o modo escuro e ter uma aparência moderna.
- O código deve incluir documentação do TypeScript (TSDoc) em comentários.
- O início de cada arquivo deve conter um bloco de comentários que descreva a finalidade do arquivo.

Com os arquivos de instruções, você fornecerá ao Copilot as informações necessárias para executar as tarefas de acordo com essas práticas.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot para que ele entenda melhor seu estilo e seus requisitos de codificação. Esse recurso permite orientar o Copilot a sugerir trechos de código mais relevantes. Você pode especificar convenções de codificação, bibliotecas e até os tipos de comentários que prefere. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos, com contexto adequado à tarefa.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações feitas ao Copilot, como a pilha de tecnologias, uma visão geral do que está sendo desenvolvido, práticas recomendadas e orientações gerais.
- Arquivos `.github/instructions/*.instructions.md`, que podem ser criados para tarefas ou tipos específicos de arquivo. Você pode usá-los para orientar linguagens como TypeScript ou Astro, ou tarefas como criar um componente de interface ou um conjunto de testes unitários.

> [!NOTE]
> No ambiente de desenvolvimento integrado (IDE), os arquivos de instruções são usados somente para a geração de código no Copilot Chat, não para conclusões de código nem sugestões de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam as instruções do repositório e os arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [oferece suporte a arquivos de instruções em outros padrões][custom-instructions-support], como AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma explicação completa sobre como criar arquivos de instruções está fora do escopo deste workshop. No entanto, os exemplos do projeto mostram uma abordagem representativa. Em linhas gerais:

- Mantenha as instruções de `copilot-instructions.md` focadas em orientações para todo o projeto, como uma descrição do que está sendo desenvolvido, a estrutura do projeto e os padrões gerais de codificação.
- Use arquivos `*.instructions.md` para orientar tipos específicos de arquivo — como testes unitários, componentes Astro e a camada de dados — ou tarefas específicas.
- Use linguagem natural e mantenha as orientações claras. Inclua exemplos de como o código deve ou não deve ser escrito.

Não há uma única maneira certa de criar arquivos de instruções nem de usar IA. A experimentação ajudará você a descobrir o que funciona melhor para o projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deve ter um conjunto sólido de arquivos de instruções. Ao explorar os arquivos deste projeto, você encontrará instruções para diversas tarefas, incluindo [atualizações da interface do usuário (UI)][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface apresenta esse recurso de forma diferente — por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI. O exercício do ambiente usado indicará o recurso quando ele for relevante.
>
> Para encontrar modelos ou um ponto de partida, explore o [awesome-copilot][awesome-copilot], um repositório com arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas deste projeto

Leia os arquivos de instruções incluídos no repositório: há um arquivo principal, `copilot-instructions.md`, e vários arquivos `*.instructions.md` para tarefas diferentes. Abra-os no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo e observe a breve descrição do projeto e as seções **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas sobre **GitHub Actions Workflows**. Essas instruções se aplicam a todas as interações com o Copilot neste repositório.
3. Abra a pasta `.github/instructions` e explore seu conteúdo. Observe que há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros itens.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início do arquivo: ele define um padrão glob, relativo à raiz do repositório, que determina a quais arquivos as instruções se aplicam. Neste caso, ele corresponde a arquivos de teste TypeScript, por exemplo, os que seguem o padrão `**/*.test.ts`.
5. Observe as instruções específicas para criar testes unitários neste projeto.
6. Abra `.github/instructions/drizzle.instructions.md` e vá até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Assim, você pode dividir conjuntos maiores de instruções em arquivos menores e reutilizáveis e indicar exemplos para o Copilot. Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.

> [!NOTE]
> A seção **Code formatting requirements** de `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentário nos arquivos.

## Adicione um novo padrão para o repositório

Agora, adicione uma regra para todo o projeto que exija documentação no código por meio de comentários TSDoc e um cabeçalho de comentário no início do arquivo. O agente de nuvem usará essa regra ao trabalhar nas issues que você atribuir mais adiante neste percurso.

Antes de editar o arquivo, crie um branch. O agente de nuvem lê as instruções do branch de destino da issue, mas você fará commit das mudanças em um branch próprio.

1. No terminal do Codespace, crie e selecione um novo branch:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como explicado anteriormente, `.github/copilot-instructions.md` fornece informações sobre o projeto ao Copilot. Registre os padrões de codificação para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Observe que ela documenta os padrões de codificação, mas ainda não inclui uma regra de documentação no código.
3. Adicione as linhas Markdown a seguir logo após os padrões existentes, para orientar o Copilot a incluir cabeçalhos de comentário e comentários TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu no exercício anterior, os arquivos de instruções podem ficar no nível do repositório (`.github/copilot-instructions.md`) para fornecer orientações gerais, ou em arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo do repositório é o lugar certo para padrões gerais, como a regra de comentários de documentação que você acabou de adicionar.

## Faça commit, envie e mescle a atualização das instruções

O agente de nuvem lê os arquivos de instruções do branch de destino da issue. Ao atribuir uma issue ao Copilot no próximo exercício, ele criará um branch a partir de `main`. Portanto, suas mudanças precisam chegar a `main` para que o agente de nuvem as use.

1. Prepare e faça commit da atualização:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie o branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. No github.com, abra um pull request de `custom-instructions-cloud` para `main` e faça a mesclagem. O agente de nuvem lerá essas instruções ao trabalhar nas issues que você atribuir no próximo exercício.

> [!TIP]
> Se preferir trabalhar diretamente em `main` durante o workshop, ignore as etapas de branch e faça commit diretamente em `main`. A criação de um branch foi incluída para aproximar o exercício do fluxo de um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções do projeto e adicionou um novo padrão para todo o repositório a `.github/copilot-instructions.md`. Você verá esse padrão nos pull requests produzidos pelo agente de nuvem nos próximos exercícios.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [Cinco dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — conjunto de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
