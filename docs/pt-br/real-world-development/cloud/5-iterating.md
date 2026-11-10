---
title: "Exercício 5 - Iterando no trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Exercício anterior: Monitoramento e gerenciamento de agentes][previous-lesson] |
|:--|

## Revise o trabalho

Ao longo deste laboratório, você trabalhou com o GitHub Copilot em várias tarefas voltadas à melhoria da experiência do usuário e à adição de funcionalidades. Você pediu ao Copilot que adicionasse documentação ao código, criasse um recurso de jogos relacionados para a equipe de design iterar e implementasse recursos de acessibilidade, incluindo opções para alternar entre os modos de alto contraste e claro. Vamos examinar as alterações no código e, se necessário, enviar comentários ao Copilot para aprimorar o trabalho.

### Cenário

Como já destacamos várias vezes, os fundamentos de design de software e desenvolvimento e operações (DevOps) não mudam com a inclusão da inteligência artificial (IA) generativa. Sempre precisamos revisar o código gerado e seguir nosso processo normal de DevOps. Com isso em mente, vamos revisar as sugestões do GitHub Copilot para criar a documentação, o recurso de jogos relacionados e os recursos de acessibilidade antes de habilitarmos a revisão pelo restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem do Copilot executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança para manter tudo protegido. Entre elas:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** ao branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions, que cria um ambiente separado e temporário para o trabalho.
- Uma pessoa precisa aprovar a execução de qualquer workflow do GitHub Actions.
- [Por padrão, o acesso a recursos externos é limitado](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), inclusive o acesso a servidores do Model Context Protocol (MCP).

## Revise a documentação gerada

Vamos começar examinando o primeiro pull request (PR) gerado pelo agente de nuvem do GitHub Copilot: aquele que adiciona documentação ao código. Você fará isso na interface padrão de PRs do GitHub.com.

> [!NOTE]
> Ao examinar o PR, você poderá ver um aviso de que o GitHub Copilot foi bloqueado por um firewall. Isso é **esperado**, pois, por padrão, o acesso do Copilot a recursos externos é limitado, inclusive chamadas a servidores MCP externos. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem do Copilot][agent-firewall].

1. Volte ao seu repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de PRs.
3. Abra o PR com um título parecido com **Add missing documentation** ou outro título mais descritivo.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o PR terá a indicação **[WIP]**. Nesse caso, aguarde a conclusão do trabalho. Isso pode levar alguns minutos; aproveite para fazer uma pausa ou refletir sobre o que aprendeu até aqui.

4. Quando o PR estiver pronto, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Examine o código atualizado, que inclui os comentários de documentação do TypeScript (TSDoc) recém-criados e outras documentações. As alterações exatas podem variar.

    Ao examinar as alterações, procure comentários de documentação TSDoc, convenções de TypeScript e cabeçalhos de comentário. Eles vêm dos arquivos de instruções personalizadas que você examinou no início do exercício 2.

6. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução de workflows](../../../_images/shared-approve-workflows.png)
9. Os workflows deverão entrar na fila da seção de verificações do PR. Se tudo correr bem, as verificações do projeto para o único aplicativo Astro serão aprovadas. Isso pode levar alguns minutos.

## Solicite alterações ao GitHub Copilot

Trabalhar com o Copilot em um PR não é uma via de mão única. Você também pode marcar o Copilot em comentários no PR, como faria com outras pessoas da equipe, ou em comentários de linha no código. O Copilot verá esses comentários e iniciará outra sessão para atendê-los. Como os resultados não são determinísticos, não podemos fornecer um texto exato para você usar. Algumas sugestões do que pedir ao Copilot:

- Adicionar cabeçalhos de comentário no início de cada arquivo de código, com uma breve descrição do que ele faz.
- Adicionar comentários de documentação TSDoc a arquivos TypeScript e Astro.
- Criar um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração à documentação gerada e marque **@copilot**, como faria com qualquer pessoa. Use uma das ideias acima ou outra sugestão de documentação que você gostaria de ver na base de código.
2. Selecione **View Session** para acompanhar o trabalho do Copilot. Observe como ele inicia uma nova sessão para fazer as atualizações.
3. Você pode selecionar **Back to pull request** para voltar ao PR.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot concluir as alterações, deverá aparecer um novo commit no PR.
5. Selecione a guia **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Quando estiver tudo pronto, você poderá converter o PR de rascunho em pronto para revisão e mesclá-lo ao branch principal.

![Converter PR em pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revise o recurso de jogos relacionados

Vamos voltar ao PR que o Copilot gerou para resolver a issue sobre exibir jogos relacionados na página de detalhes de cada jogo.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título parecido com **Show related games on the game details page** ou outro título mais descritivo.
4. Selecione a guia **Files changed** para revisar o código gerado.
5. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
6. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
7. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução de workflows](../../../_images/shared-approve-workflows.png)
8. Os workflows deverão entrar na fila da seção de verificações do PR. Se tudo correr bem, as verificações do projeto para o único aplicativo Astro serão aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** você pode mudar para esse branch no Codespace para testar manualmente o recurso de jogos relacionados. Acesse o Codespace, abra o terminal e execute os comandos a seguir (substitua `<branch-name>` pelo nome do branch criado pelo Copilot, por exemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados. Assim como antes, você pode iterar com o agente de nuvem do Copilot e pedir atualizações. Por exemplo, talvez você queira ajustar a quantidade de jogos relacionados exibidos ou garantir a inclusão de cabeçalhos de comentário e comentários de documentação TSDoc (lembre-se: a tarefa foi atribuída **antes** das atualizações às instruções personalizadas). Como antes, faça esses pedidos adicionando um comentário na guia **Conversation**. O Copilot verá o comentário e iniciará uma nova sessão.

## Revise os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade implementados com o agente personalizado de acessibilidade. Esse PR deve incluir tanto o modo de alto contraste, atribuído no exercício 3, quanto o modo claro, solicitado no Mission Control no exercício 4.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com um título parecido com **Add high contrast mode to website** ou outro título mais descritivo.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o PR terá a indicação **[WIP]**. Nesse caso, aguarde a conclusão do trabalho. Isso pode levar alguns minutos.

4. Selecione a guia **Files changed** para revisar o código gerado.
5. Revise a implementação, prestando atenção especial a:
   - Os componentes da interface do usuário para alternar entre os modos.
   - O uso do armazenamento local para manter as preferências do usuário.
   - As alterações nas folhas de estilo em cascata (CSS) ou em outros estilos para os modos de alto contraste e claro.
   - Os atributos de acessibilidade (rótulos Accessible Rich Internet Applications (ARIA), navegação pelo teclado etc.).
   - O código JavaScript/TypeScript que gerencia a alternância entre os modos.

6. Depois de revisar as atualizações e confirmar que estão corretas, volte à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovação e execução de workflows](../../../_images/shared-approve-workflows.png)
9. Os workflows deverão entrar na fila da seção de verificações do PR. Se tudo correr bem, as verificações do projeto para o único aplicativo Astro serão aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** você pode mudar para esse branch no Codespace para testar manualmente os recursos de acessibilidade. Acesse o Codespace, abra o terminal e execute os comandos a seguir (substitua `<branch-name>` pelo nome do branch criado pelo Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Em seguida, inicie o aplicativo e teste os controles dos modos de alto contraste e claro no navegador para confirmar se funcionam como esperado e se as preferências continuam ativas após recarregar a página.

Observe como o agente personalizado de acessibilidade ajudou a orientar o Copilot na implementação desses recursos de acordo com as práticas recomendadas de acessibilidade. Se você encontrar problemas ou oportunidades de melhoria, pode marcar **@copilot** em um comentário e solicitar alterações, como fez com os PRs anteriores.

## Exercício opcional — continue delegando

O agente de nuvem funciona melhor quando você pode delegar tarefas reais da lista de pendências e se concentrar em outra coisa. Para desenvolver esse hábito, crie mais algumas issues no seu repositório e atribua-as ao Copilot. Algumas ideias:

- Criar um formulário para demonstrar interesse em um jogo na página de detalhes.
- Implementar paginação na página de lista de jogos.
- Adicionar validação de entrada e tratamento de erros aos auxiliares de acesso a dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Ao longo dessas lições, você:

- **Examinou os arquivos de instruções personalizadas deste repositório** para ver como eles influenciam o trabalho do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, adicionando opções para os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como Mission Control** para monitorar e orientar uma sessão de acessibilidade em andamento.
- **Revisou e aprimorou os PRs do agente de nuvem**, marcando `@copilot` para solicitar alterações e aprovando workflows.

## Revisão e próximos passos

Você concluiu o percurso do agente de nuvem. Se quiser continuar explorando, os outros percursos complementam o que você praticou:

- 🖥️ **[Percurso do VS Code](../../vscode/)** — explore o modo agente do Copilot Chat e a integração com MCP diretamente no ambiente de desenvolvimento integrado (IDE).
- 💻 **[Percurso da interface de linha de comando (CLI)](../../cli/)** — entregue duas alterações revisadas pelo terminal usando os modos Plan e Autopilot, habilidades de agente, um agente personalizado de garantia de qualidade (QA), Playwright MCP, Agent Merge e uma ponte opcional `/delegate` de volta ao agente de nuvem.

No seu próprio repositório, experimente estas ideias:

- Atribua ao agente de nuvem uma issue de refatoração ou de cobertura de testes.
- Crie um agente personalizado para outro domínio.
- Configure `copilot-setup-steps.yml` para outra pilha de tecnologias.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre os agentes do Copilot][copilot-agents]
- [Atribuição de issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem do Copilot][cloud-agent-best-practices]
- [Configuração do firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Exercício anterior: Monitoramento e gerenciamento de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
