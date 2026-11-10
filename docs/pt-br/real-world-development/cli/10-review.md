---
title: "Lição 10 - Encerramento e próximos passos"
description: "Recapitule o fluxo de trabalho do Copilot CLI, os dois pull requests, as personalizações reutilizáveis e outros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Você usou o GitHub Copilot CLI em um fluxo de trabalho contínuo na Tailspin Toys. Você:

- preparou um Codespace, instalou o Copilot CLI, explorou o projeto e encontrou a issue de filtragem existente.
- adicionou classificações por estrelas, revisou o resultado em um navegador encaminhado e mesclou manualmente seu primeiro pull request (PR).
- começou pela issue de filtragem, definiu a abordagem no modo Plan, desenvolveu no modo Autopilot e revisou no modo Interactive.
- orientou o agente com instruções personalizadas, personalizou a skill existente `quality-checks` e a usou para executar testes unitários, lint e verificações de tipos.
- adicionou o servidor Model Context Protocol (MCP) do Playwright e o usou para explorar a filtragem em um navegador real.
- criou e selecionou um agente personalizado de garantia de qualidade (QA) para avaliar requisitos, cobertura, resultados da skill e evidências do navegador.
- revisou a mudança completa da filtragem e autorizou o Agent Merge para o PR de filtragem.
- explorou comandos de barra para contexto, modelos, compartilhamento e delegação opcional para a nuvem.

## O que você entregou

O workshop inclui dois marcos de PR, cada um em seu próprio branch criado a partir do `main` atualizado:

1. **Classificações por estrelas:** exiba o `starRating` existente e um estado explícito para jogos sem classificação nos cartões.
2. **Filtragem e fluxo de qualidade:** implemente a filtragem, atualize as instruções e aplique-as ao recurso, personalize o relatório de `quality-checks`, crie um perfil de QA e inclua os testes relacionados.

Do planejamento da filtragem à abertura do PR, você usou a mesma conversa e o mesmo branch. Para simplificar o workshop, reunimos esse trabalho em um único PR.

## Diferentes tipos de verificação

Você verificou o código de várias formas: com testes automatizados, uma inspeção própria no navegador e a exploração do navegador pelo Copilot usando MCP. A skill `quality-checks` executou testes unitários, lint e verificações de tipos e apresentou os resultados no novo formato. O QA reuniu esses resultados com uma revisão dos requisitos e da cobertura de testes antes do PR.

Os testes adicionados devem preencher lacunas reais; uma execução de QA que conclua que não são necessários testes novos também pode estar correta. Revise o código e as evidências antes de autorizar a mesclagem e atualize as evidências afetadas depois de qualquer mudança.

## Práticas recomendadas

O contexto e as ferramentas fornecidos ao Copilot influenciam o trabalho dele. Neste workshop, você atualizou instruções, personalizou uma skill, criou um perfil de QA e configurou um servidor MCP. Reutilize essas personalizações em outras conversas e ajuste-as conforme as necessidades da equipe mudarem. As instruções definem padrões, as skills descrevem tarefas repetíveis, os agentes personalizados definem funções especialistas e os servidores MCP conectam ferramentas externas. Revise as mudanças reais e os resultados das ferramentas, não apenas o resumo do agente.

Escolha o **modo e o modelo** adequados à tarefa. Use **Plan** para avaliar uma abordagem antes de desenvolver, **Interactive** para acompanhar mudanças pontuais e **Autopilot** para tarefas bem delimitadas. Escolha um modelo mais rápido para edições rotineiras e outro mais capaz para trabalhos complexos.

O contexto continua sendo tão importante quanto a infraestrutura. Descrever com clareza *o que* você quer desenvolver, *por que* e *como* influencia significativamente os resultados.

## Mais para explorar

Você concluiu o fluxo de trabalho principal. Confira mais alguns recursos do CLI:

- `/review` para pedir ao agente de revisão de código que analise as mudanças.
- `/rubber-duck` para conversar sobre um problema e obter outra perspectiva.
- `/fleet` para coordenar subtarefas independentes em paralelo.
- `/worktree` para isolar uma tarefa separada.
- `/delegate` para enviar uma tarefa ao agente de nuvem do Copilot.

## Próximos passos

A melhor maneira de aprimorar o uso de qualquer ferramenta é continuar usando-a. Use-a em código de produção, em projetos pessoais ou naquele pequeno aplicativo que você planeja desenvolver há anos. Compartilhe seus aprendizados com a equipe e aprenda com os outros. E, como sempre, explore a documentação.

Para ampliar a Tailspin Toys pelo terminal, continue com a série opcional [Foundry Backer Concierge][foundry]. Para comparar outros ambientes, explore os workshops do [VS Code][vscode], do [aplicativo GitHub Copilot][app] ou do [agente de nuvem do Copilot][cloud].

## Recursos

- [Sobre o GitHub Copilot CLI][about-cli]
- [Referência de comandos do Copilot CLI][cli-reference]
- [Personalize o Copilot CLI][customize-cli]
- [Gerencie pull requests com o Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
