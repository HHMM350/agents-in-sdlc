---
title: "Lição 2 - Adicionar classificações por estrelas: uma melhoria rápida"
description: "Inicie sua primeira sessão de agente no aplicativo GitHub Copilot, faça uma pequena mudança nos cartões de jogos e mescle-a como seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Agora que você conheceu o espaço de trabalho e usou um chat rápido, é hora de iniciar uma **sessão de agente** e fazer sua primeira mudança no projeto. Ela será pequena: os jogos já têm uma classificação por estrelas nos dados, mas os cartões da página inicial ainda não a exibem. Você pedirá ao agente que mostre a classificação, revisará a mudança e a mesclará como seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma sessão de agente e aprender como ela é estruturada.
- pedir ao agente que faça uma pequena mudança específica no projeto.
- revisar a mudança na visualização de diff do espaço de trabalho.
- executar o aplicativo localmente para confirmar a mudança no navegador.
- abrir e mesclar seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma classificação por estrelas, que já aparece na página de detalhes do jogo. Porém, os cartões da página inicial mostram apenas o título, a categoria, a editora e a descrição. Como aquecimento, você pedirá ao agente que exiba a classificação existente em cada cartão — uma mudança pequena e independente, ideal para sua primeira sessão.

## Anatomia de uma sessão

Uma **sessão** é uma conversa com um agente executada em seu próprio espaço de trabalho isolado. Cada sessão recebe um **git worktree e uma branch dedicados**, o que permite executar várias sessões ao mesmo tempo — uma adicionando um recurso e outra corrigindo um bug — sem que as mudanças entrem em conflito. Suas sessões aparecem na barra lateral, agrupadas por repositório. Selecione uma delas para acessá-la.

Em uma sessão, você verá três elementos: a **conversa** com o agente, a **atividade de ferramentas** do agente enquanto ele explora e edita arquivos e a lista de **arquivos alterados** com os respectivos diffs.

## Iniciar uma sessão e solicitar a mudança

Vamos iniciar uma nova sessão para explorar o projeto e implementar o recurso. Durante a [configuração do aplicativo][prior-lesson], você adicionou o projeto por meio do repositório do GitHub. Vamos criar uma sessão para esse repositório e solicitar a mudança.

1. Retorne ao aplicativo GitHub Copilot ou abra-o.
2. Selecione **+** na parte superior da barra lateral para iniciar uma sessão.
3. Selecione `tailspin-toys` como repositório.
4. Escolha uma **new working tree** e o modo **Interactive** abaixo da caixa de prompt. Use este prompt para solicitar a mudança:

    ```plaintext
    Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
    ```

5. Pressione <kbd>Enter</kbd> para enviar o prompt ao Copilot.

O aplicativo Copilot começa criando um worktree novo, uma cópia isolada do projeto. Em seguida, explora o projeto, localiza os arquivos que precisam ser atualizados para adicionar o recurso e cria o código necessário. Você acabou de adicionar um recurso com o aplicativo Copilot!

## Revisar o diff

Todas as mudanças geradas por IA devem ser revisadas antes da mesclagem, mesmo as pequenas. Vamos explorar as mudanças diretamente no aplicativo Copilot.

1. No canto superior direito do aplicativo, selecione **Toggle review panel**. No painel que será aberto, selecione **Changes** para ver os arquivos alterados e seus diffs.

    ![Barra de ferramentas superior do aplicativo GitHub Copilot com uma seta apontando para o botão Toggle review panel à direita de Create PR](../../../_images/app-2-review-panel.png)

2. Você verá código adicionado a `GameCard.astro`, o arquivo principal usado para exibir os detalhes do jogo. Ele deverá ser semelhante ao exemplo a seguir: um pequeno bloco que renderiza a classificação quando ela existe e exibe `No rating yet` quando `starRating` é `null`:

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como o Copilot, assim como todas as ferramentas de IA generativa, é probabilístico e não determinístico, o código exato pode variar. No entanto, ele deverá ser relativamente semelhante.

## Verificar as mudanças

Revise os resultados das verificações automatizadas do agente antes de abrir o navegador. Confirme se os testes cobrem um `starRating` numérico e a alternativa para `null`. Um pré-requisito ausente ou uma verificação ignorada não conta como aprovação; revise qualquer solicitação de instalação antes de aprová-la.

Não devemos apenas ler o código e presumir que funciona. Vamos pedir ao Copilot que abra o site para que possamos examinar a interface atualizada. Para isso, pediremos que ele inicie o site e o abra em um canvas de navegador.

> [!TIP]
> Um canvas é um widget interativo disponível dentro do próprio aplicativo Copilot. Você explorará canvases personalizados e até criará um mais adiante, mas, por enquanto, usaremos o canvas de navegador integrado.

1. Use o seguinte prompt para pedir ao Copilot que inicie o aplicativo e abra a página no canvas de navegador:

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. Em alguns instantes, o aplicativo será iniciado e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Confirme que os cartões de jogos avaliados exibem a nota em uma escala de cinco estrelas.
4. Quando terminar, use o seguinte prompt para pedir ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão:

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## Abrir e mesclar seu primeiro pull request

Você criou o recurso! Agora é hora de criar um pull request (PR) para mesclar o novo código à base de código existente.

1. Selecione **Create PR** no canto superior direito.
2. Se solicitado, selecione **Sign in with your browser** e siga as instruções para se autenticar.
3. Se o Copilot explicar que a política do repositório exige uma issue correspondente antes de criar o PR, confirme que ele deve seguir esse processo.
4. O Copilot começará a criar o PR.
5. Selecione o indicador **PR** logo acima do chat para abrir o pull request no painel de revisão. Revise-o conforme necessário.
6. Quando estiver tudo pronto, selecione **Ready to merge**.
7. Na nova janela de diálogo, selecione **Merge pull request** para mesclar o pull request.

## Resumo e próximos passos

Parabéns! Você entregou sua primeira mudança usando o aplicativo GitHub Copilot. Em especial, você:

- iniciou uma sessão de agente e aprendeu como as sessões são estruturadas.
- orientou o agente para fazer uma pequena mudança específica nos cartões de jogos.
- revisou a mudança na visualização de diff do espaço de trabalho.
- executou o aplicativo localmente para confirmar a classificação por estrelas no navegador.
- abriu o PR 1, revisou as verificações e fez a mesclagem explicitamente.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para criar um recurso maior.

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Gerenciar issues e pull requests com o aplicativo GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instalar-e-configurar-o-aplicativo-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
