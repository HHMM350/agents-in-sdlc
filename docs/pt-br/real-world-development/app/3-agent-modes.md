---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Explore os modos de agente: use Plan para definir uma abordagem, Autopilot para criar os filtros a partir de uma issue e Interactive para revisar e verificar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Começamos adicionando um pequeno recurso ao projeto. Mudanças maiores exigem um processo mais robusto. Felizmente, o aplicativo GitHub Copilot foi desenvolvido para trabalhar com o fluxo existente de uma organização e ajudar a criar as soluções certas da maneira correta. Esta é a primeira de várias lições nas quais você seguirá um processo típico de desenvolvimento orientado por agentes: começará por uma issue para criar um recurso, verificará se o código é válido e se o recurso se comporta como esperado e, por fim, fará a mesclagem bem-sucedida ao projeto.

> [!NOTE]
> Você continuará o fluxo de trabalho do recurso usando a mesma sessão. Normalmente, você usaria sessões ou PRs diferentes para os vários tipos de arquivos com os quais trabalharia, mas faremos um atalho para nos concentrarmos nos conceitos principais.

Nesta lição, você vai:

- iniciar uma nova sessão de agente a partir de uma issue do GitHub.
- definir os requisitos no modo **Plan**.
- implementar o novo recurso usando o modo **Autopilot**.
- revisar o código.
- validar manualmente o recurso em um canvas de navegador.

Ao continuar este recurso, você atualizará as instruções do repositório, personalizará a skill existente `quality-checks`, adicionará a validação MCP, criará um agente de QA e abrirá o PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve o recurso, mas detalhes como combinar categorias precisam ser acordados antes de escrever o código. Você usará o modo Plan para decidir esses pontos e, em seguida, autorizará uma implementação com escopo definido pelo Autopilot.

## Contexto

Adicionar agentes de programação com IA ao fluxo de desenvolvimento não muda os conceitos fundamentais. Na verdade, eles se tornam ainda mais importantes! A maioria das pessoas desenvolvedoras segue um fluxo semelhante a este:

1. Abrir uma issue registrada com os detalhes do que precisa ser feito.
2. Criar um plano do que precisa ser desenvolvido.
3. Desenvolver e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e o processo de integração contínua for concluído com sucesso, mesclar o código.

> [!NOTE]
> Os detalhes exatos variam de acordo com a equipe e a organização, mas a maioria segue alguma variação do processo listado acima.

Ao seguir essa abordagem padrão, você garante que o código gerado por IA atenda aos requisitos definidos e passe pelo mesmo processo de revisão que o código escrito manualmente.

## Modos de sessão

O **modo de sessão** controla o nível de autonomia do agente. Você pode defini-lo no menu suspenso abaixo do campo do prompt e alterá-lo a qualquer momento:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere mudanças e aguarda sua orientação antes de continuar.
- **Plan**: o agente cria primeiro um plano. Você o revisa e aprova antes que o agente o execute.
- **Autopilot**: o agente trabalha de forma totalmente autônoma, escrevendo código, executando testes e iterando sem aguardar orientação.

Comece no modo Plan, revise o plano e, em seguida, use o Autopilot para implementá-lo.

## Iniciar uma sessão a partir da issue

Confirme que o PR de classificação por estrelas foi mesclado e que sua `main` local está atualizada antes de começar.

1. Em **Sessions**, na barra lateral, selecione a pasta do repositório Tailspin Toys e, em seguida, **Issues** na navegação superior do repositório. Abra **Allow users to filter games by category and publisher**. Essa issue já foi criada para você; não é necessário criar outra.
2. Selecione **New session** e escolha uma **new working tree** baseada na `main` atualizada.

    ![Visualização da issue no aplicativo GitHub Copilot com uma seta apontando para o botão New session](../../../_images/app-new-session-from-issue.png)

3. Confirme que a issue está anexada à sessão e selecione **Plan** no seletor de modo.

> [!NOTE]
> Se o Node.js ou o npm não forem encontrados, peça ao agente que execute `node --version` e `npm --version`. Se os comandos funcionarem no terminal, mas não na sessão, verifique o PATH ou a configuração do gerenciador de versões do aplicativo e feche-o completamente antes de reabri-lo. Repita a operação e as verificações que falharam; não reinstale o npm apenas porque o agente não consegue encontrá-lo.

## Planejar o recurso de filtragem

O planejamento permite revisar a abordagem antes de o Copilot escrever código. Como você começou pela issue, o Copilot já tem a solicitação do recurso como contexto. Envie:

```plaintext
Build this feature.
```

Responda às perguntas do Copilot e compare o plano com os critérios de aceitação da issue. Confirme se ele inclui filtragem por categoria e editora, controles acessíveis, alterações no acesso a dados e testes. Discuta qualquer comportamento que não esteja claro, como combinar várias categorias ou o que acontece quando nenhum jogo corresponde aos filtros.

O plano deve incluir lint, testes unitários, testes E2E e verificação de tipos com as ferramentas existentes do projeto. Mantenha o escopo em implementar e testar a filtragem; você criará o PR após concluir o fluxo de qualidade. Peça alterações no plano antes de aprová-lo e deixe à mão a URL da issue e quaisquer esclarecimentos acordados para a validação posterior.

## Aprovar explicitamente o Autopilot

Quando estiver satisfeito com o plano, selecione **Approve and implement this plan** ou a opção equivalente na sua versão. Verifique qual modo está ativo, em vez de presumir que a aprovação o altera. Confirme que o indicador de modo mostra **Autopilot**.

O Copilot começará a trabalhar na implementação. Você verá que ele seguirá o plano de forma iterativa, gerando código e executando testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente; por isso, revise o plano primeiro. Se o Copilot informar que faltam dependências ou que há conflito de portas, resolva o problema de configuração antes de considerar as verificações concluídas. Interrompa apenas os servidores que você iniciou.

## Revisar e verificar a implementação

Depois que o código for gerado, ele precisará ser revisado antes da mesclagem, assim como qualquer outro código. Vamos revisar o código e executar o site para garantir que tudo esteja correto.

1. Abra **Changes** e inspecione a implementação dos filtros e os testes.
2. Compare o resultado com a issue e os esclarecimentos aprovados, incluindo combinações de várias categorias e editoras. Verifique se as mudanças seguem as instruções existentes do repositório.
3. Examine os resultados de lint, testes unitários, testes E2E e verificação de tipos. Uma verificação ignorada não conta como aprovação.
4. Resolva as falhas e execute novamente as verificações afetadas antes de aceitar a implementação. A configuração E2E do Playwright cria e disponibiliza uma versão de pré-visualização e pode reutilizar um servidor local. Confirme que o servidor testado pertence a esta worktree, e não a uma lição anterior.

## Explorar a nova funcionalidade

O código parece correto — mas será que funciona? Vamos iniciar o aplicativo como antes e abrir o site em um canvas de navegador.

1. Use o seguinte prompt para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Selecione uma categoria e confirme se os resultados correspondem a ela. Limpe o filtro e, depois, selecione uma editora e confirme os resultados.
4. Combine filtros de categoria e editora e compare os resultados com a issue e o plano aprovado. Se houver suporte a várias categorias, verifique o comportamento combinado acordado.
5. Teste uma combinação sem jogos correspondentes e confira o estado vazio. Limpe ou redefina os filtros e confirme se a lista completa volta a aparecer.
6. Quando terminar, use o seguinte prompt para pedir ao Copilot que interrompa o servidor de desenvolvimento iniciado para esta sessão:

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## Manter esta sessão para as próximas lições

Ainda não crie nem mescle o PR de filtragem. Mantenha esta sessão, a worktree e a branch para as Lições 4 a 8. Em seguida, você aplicará instruções personalizadas ao código de filtragem e adicionará melhorias para a skill e o agente de QA antes de criar e mesclar o PR combinado na Lição 8. Você pode deixar a sessão ociosa depois de parar o servidor de desenvolvimento e retomá-la na próxima lição.

## Resumo e próximos passos

Você usou diferentes modos de agente para criar e revisar um recurso. Nesta lição, você:

- iniciou uma nova sessão de agente a partir de uma issue do GitHub.
- definiu os requisitos no modo **Plan**.
- implementou o novo recurso usando o modo **Autopilot**.
- revisou o código.
- validou manualmente o recurso em um canvas de navegador.

Em seguida, você aprenderá mais sobre a geração de código e como garantir que ela siga as práticas documentadas [usando instruções personalizadas][next-lesson].

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
