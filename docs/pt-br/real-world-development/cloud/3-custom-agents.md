---
title: "Exercício 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot permitem criar assistentes de inteligência artificial (IA) especializados em tarefas ou domínios específicos do fluxo de desenvolvimento. Ao definir agentes em arquivos Markdown na pasta `.github/agents` do repositório, você fornece instruções direcionadas, práticas recomendadas, padrões de codificação e conhecimento de domínio para orientar o Copilot em tipos específicos de trabalho. As equipes podem transformar sua experiência em agentes reutilizáveis — por exemplo, um agente de acessibilidade que aplica as [Diretrizes de Acessibilidade para Conteúdo da Web (WCAG)][wcag], um agente de segurança que segue práticas seguras de codificação ou um agente de testes que mantém padrões de teste consistentes.

Os agentes personalizados são definidos em arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem metadados na linguagem YAML Ain't Markup Language (YAML), com pelo menos `name` e `description`, seguidos de um prompt Markdown que define o comportamento, a especialização e as instruções do agente.

### Agentes personalizados e skills de agente

Há alguma sobreposição entre agentes personalizados e [skills de agente][agent-skills-concept]. Ambos são definidos principalmente em arquivos Markdown e orientam uma IA na execução de operações. A distinção mais simples é: um **agente personalizado** é quem executa o trabalho, e as **skills** são as ferramentas.

Os agentes personalizados têm sua própria janela de contexto e são criados para orquestrar skills — e até outros agentes — durante o trabalho. Neste laboratório, o agente personalizado de acessibilidade revisará e atualizará o site de acordo com as diretrizes de acessibilidade. Como parte desse trabalho, ele poderá chamar skills, como uma skill de fluxo de pull requests ou outra que execute e gerencie testes.

> [!NOTE]
> Não existe uma única forma correta de criar um agente personalizado. Como em qualquer trabalho com IA, teste e faça iterações para encontrar a abordagem adequada aos seus ambientes e cenários.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Com os agentes personalizados, você explorará:

- como os agentes personalizados são definidos.
- como atribuir uma tarefa a um agente personalizado.

## Cenário

A Tailspin Toys está comprometida em tornar sua plataforma de financiamento coletivo acessível a todas as pessoas, independentemente das capacidades ou preferências visuais. Comentários recentes de usuários indicaram que algumas pessoas têm dificuldade para ler o tema escuro atual por causa do contraste insuficiente entre as cores do texto e do plano de fundo. Para resolver essa questão de acessibilidade, a equipe de design solicitou um modo de alto contraste que as pessoas usuárias possam ativar e desativar.

Como a acessibilidade é essencial, você quer implementar esse recurso o mais rápido possível. Para gerar a funcionalidade, usará um agente personalizado.

## Revise o agente personalizado de acessibilidade

Um agente personalizado de acessibilidade já foi criado. Revise o conteúdo para entender como ele orientará o Copilot.

Volte ao Codespace e revise o arquivo do agente personalizado de acessibilidade:

1. Abra `.github/agents/accessibility.md`.
2. Observe os metadados na linguagem YAML Ain't Markup Language (YAML), com os campos `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório para agentes personalizados.

3. Examine as seções seguintes, que destacam:
   - responsabilidades principais ao gerar código para um site acessível.
   - práticas recomendadas de acessibilidade.
   - exemplos de código para a linguagem de marcação de hipertexto (HTML), folhas de estilo em cascata (CSS) e JavaScript.
   - problemas e erros comuns.

## Crie e atribua uma issue

O Mission Control é o local central para trabalhar com agentes no seu ambiente. Você pode atribuir tarefas ao agente de nuvem do Copilot, monitorar as tarefas e até redirecionar o trabalho e fornecer orientações adicionais. Comece atribuindo ao Copilot uma tarefa para criar o modo de alto contraste.

1. Acesse seu repositório.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue** para criar a issue.
5. Defina **Title** como `Add high contrast mode to website`.
6. Defina **Description** como:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.
9. Na lista de agentes personalizados, selecione **Accessibility agent**.

    ![Captura de tela da atribuição do agente de nuvem, com o agente personalizado e o agente Accessibility destacados](../../../_images/ex5-select-custom-agent.png)

10. Selecione **Assign**.
11. O Copilot começará a trabalhar na tarefa em segundo plano.

## Resumo e próximos passos

Neste exercício, você explorou os [agentes personalizados][custom-agents], assistentes de IA especializados em tarefas e domínios específicos. Com agentes personalizados, você pode transformar a experiência e os padrões da equipe em agentes reutilizáveis que orientam o Copilot a realizar determinados tipos de trabalho com mais eficiência.

Você explorou estes conceitos:

- como os agentes personalizados são definidos.
- como atribuir uma tarefa a um agente personalizado.

Enquanto o Copilot implementa o modo de alto contraste, você pode [monitorar e orientar a sessão do agente][next-lesson] no Mission Control.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Prepare sua organização para usar agentes personalizados][org-custom-agents]
- [Prepare sua empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Exercício anterior: Agente de nuvem do GitHub Copilot][previous-lesson] | [Próximo exercício: Monitoramento e gerenciamento de agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
