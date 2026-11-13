---
title: "Lição 10 - Encerramento e próximos passos"
description: "Recapitule o fluxo de trabalho do Copilot CLI, os dois pull requests, as personalizações reutilizáveis e outros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Você usou o GitHub Copilot CLI em um fluxo contínuo de trabalho na Tailspin Toys. Você:

- preparou um Codespace, instalou o Copilot CLI, explorou o projeto e localizou a issue de filtragem criada no backlog.
- adicionou classificações por estrelas, revisou o resultado em um navegador encaminhado e mesclou manualmente seu primeiro pull request (PR).
- começou pela issue de filtragem, definiu a abordagem no modo Plan, implementou no modo Autopilot e revisou no modo Interactive.
- orientou o agente com instruções personalizadas, personalizou a skill existente `quality-checks` e a usou para executar testes unitários, lint e verificações de tipos.
- adicionou o servidor Model Context Protocol (MCP) do Playwright e o usou para explorar os filtros em um navegador real.
- criou e selecionou um agente personalizado de garantia de qualidade (QA) para avaliar requisitos, cobertura, resultados da skill e evidências do navegador.
- revisou a mudança completa dos filtros e autorizou o Agent Merge para o PR correspondente.
- explorou comandos de barra para contexto, modelos, compartilhamento e delegação opcional à nuvem.

## O que você entregou

O workshop tem dois marcos de PR, cada um em sua própria branch baseada em `main` atualizada:

1. **Classificações por estrelas:** exibir nos cartões de jogos o valor existente de `starRating` e um estado explícito para jogos sem classificação.
2. **Filtragem e fluxo de qualidade:** implementar os filtros, atualizar as instruções e aplicá-las ao recurso, personalizar o relatório de `quality-checks`, criar um perfil de QA e incluir os testes correspondentes.

Desde o planejamento dos filtros até a abertura do PR, você usou a mesma conversa e a mesma branch. Para simplificar o workshop, reunimos todo esse trabalho em um único PR.

## Diferentes tipos de verificação

Você verificou o código de várias maneiras: testes automatizados, sua própria inspeção no navegador e a exploração do navegador pelo Copilot via MCP. A skill `quality-checks` executou testes unitários, lint e verificações de tipos e apresentou os resultados no novo formato. O QA reuniu esses resultados com a revisão dos requisitos e da cobertura de testes antes da abertura do PR.

Os testes adicionados devem preencher lacunas reais; uma execução de QA sem necessidade de novos testes também pode ser correta. Revise o código e as evidências antes de autorizar a mesclagem e atualize as evidências afetadas depois de qualquer mudança.

## Práticas recomendadas

O contexto e as ferramentas fornecidos ao Copilot influenciam o trabalho. Neste workshop, você atualizou instruções, personalizou uma skill, criou um perfil de QA e configurou um servidor MCP. Reutilize essas personalizações em outras conversas e ajuste-as conforme as necessidades da equipe. As instruções definem padrões, as skills descrevem tarefas repetíveis, os agentes personalizados definem funções especialistas e os servidores MCP conectam ferramentas externas. Revise as mudanças reais e os resultados das ferramentas, não apenas o resumo do agente.

Escolha o **modo e o modelo** de acordo com a tarefa. Use **Plan** para definir uma abordagem antes de começar, **Interactive** para acompanhar mudanças específicas e **Autopilot** para tarefas com escopo claro. Escolha um modelo mais rápido para edições rotineiras e outro mais capaz para trabalhos complexos.

O contexto continua tão importante quanto a infraestrutura. Descrever com clareza *o que* você quer criar, *por que* e *como* muda significativamente o resultado.

## Mais recursos para explorar

Você percorreu o fluxo de trabalho principal. Confira estes outros recursos da CLI:

- `/review` para pedir ao agente de revisão de código que analise as mudanças.
- `/rubber-duck` para conversar sobre um problema e obter outra perspectiva.
- `/fleet` para coordenar subtarefas independentes em paralelo.
- `/worktree` para isolar uma tarefa separada.
- `/delegate` para enviar uma tarefa ao agente de nuvem do Copilot.

## Próximos passos

A melhor maneira de melhorar o uso de qualquer ferramenta é continuar usando-a. Use-a em código de produção, em projetos pessoais ou naquele pequeno aplicativo que você sempre quis criar. Compartilhe seus aprendizados com a equipe e aprenda com os de outras pessoas. E, como sempre, explore a documentação.

Se quiser ampliar a Tailspin Toys pelo terminal, continue com a série opcional [Foundry Backer Concierge][foundry]. Para comparar outros ambientes, explore o [workshop do VS Code][vscode], o [workshop do aplicativo GitHub Copilot][app] ou o [workshop do agente de nuvem do Copilot][cloud].

## Recursos

- [Sobre o GitHub Copilot CLI][about-cli]
- [Referência de comandos do Copilot CLI][cli-reference]
- [Personalizar o Copilot CLI][customize-cli]
- [Gerenciar pull requests com o Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
