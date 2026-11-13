---
title: "Exercício 5: Iterar sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisar o trabalho

Durante este laboratório, você trabalhou com o GitHub Copilot em várias tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Pediu ao Copilot que documentasse o código, criasse o recurso de jogos relacionados para a equipe de design testar e implementasse recursos de acessibilidade, incluindo alternâncias para os modos de alto contraste e claro. Agora vamos explorar as mudanças de código e, se necessário, fornecer feedback ao Copilot para aprimorar o trabalho antes de habilitar a revisão para o restante da equipe.

### Cenário

Como já destacamos várias vezes, os fundamentos de design de software e DevOps não mudam com a chegada da IA generativa. Sempre precisamos revisar o código gerado e seguir nosso processo normal de DevOps. Com isso em mente, vamos revisar as sugestões do GitHub Copilot para a documentação, o recurso de jogos relacionados e os recursos de acessibilidade.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem do Copilot executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança para manter o ambiente seguro. Entre elas:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** à branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions em um ambiente separado e temporário.
- Os workflows do GitHub Actions precisam de aprovação de uma pessoa antes de serem executados.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo servidores MCP.

## Revisar a documentação gerada

Vamos começar pelo primeiro pull request (PR) gerado pelo agente de nuvem do GitHub Copilot: a adição de documentação ao código. Você fará isso na interface padrão de PRs do GitHub.com.

> [!NOTE]
> Ao explorar o PR, você poderá ver um aviso de que o firewall bloqueou o GitHub Copilot. Isso é **esperado**, pois o acesso do Copilot a recursos externos é limitado por padrão, incluindo chamadas a servidores MCP externos. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem do Copilot][agent-firewall].

1. Retorne ao repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o pull request com título semelhante a **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request terá a indicação **[WIP]**. Nesse caso, aguarde a conclusão do trabalho. Isso pode levar alguns minutos; aproveite para fazer uma pausa ou refletir sobre o que aprendeu até aqui.

4. Quando o pull request estiver pronto, selecione a guia **Files changed** e revise as mudanças.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código atualizado, que inclui os comentários TSDoc recém-criados e outras documentações. As mudanças exatas podem variar.

   Ao examinar as mudanças, procure comentários TSDoc, convenções TypeScript e cabeçalhos de comentários. Eles foram definidos nos arquivos de instruções personalizadas que você revisou no início do Exercício 2.

6. Depois de revisar as atualizações, retorne à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows entrarão na fila na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para a aplicação Astro serão aprovadas. Isso pode levar alguns minutos.

## Pedir mudanças ao GitHub Copilot

Trabalhar com o Copilot em um pull request não é uma via de mão única. Você pode mencionar o Copilot em comentários do PR — como faria com outra pessoa da equipe — ou em comentários em linha no código. O Copilot verá esses comentários e iniciará outra sessão para atendê-los. Como os resultados não são determinísticos, não há um texto prescritivo único. Por exemplo, você pode pedir ao Copilot que:

- adicione cabeçalhos de comentários no início de cada arquivo de código com uma breve descrição.
- adicione comentários TSDoc a arquivos TypeScript e Astro.
- crie um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma mudança na documentação gerada e mencione **@copilot**, como faria com qualquer pessoa. Use uma das ideias acima ou outra sugestão de documentação que gostaria de ver na base de código.
2. Selecione **View Session** para acompanhar o trabalho do Copilot. Observe que ele inicia uma nova sessão para fazer as atualizações.
3. Selecione **Back to pull request** para retornar ao pull request.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot concluir as mudanças, um novo commit aparecerá no pull request.
5. Selecione **Files changed** para revisar as mudanças.

Você pode continuar iterando até ficar satisfeito. Quando estiver tudo pronto, converta o PR de rascunho em pronto para revisão e mescle-o à branch principal.

![Converter PR em pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revisar o recurso de jogos relacionados

Vamos voltar ao PR que o Copilot gerou para resolver a issue de exibir jogos relacionados na página de detalhes de um jogo.

1. Retorne ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com título semelhante a **Show related games on the game details page**.
4. Selecione **Files changed** para revisar o código gerado.
5. Depois da revisão, retorne à guia **Conversation** e role a página para baixo.
6. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
7. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

8. Os workflows entrarão na fila na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para a aplicação Astro serão aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** você pode alternar o Codespace para essa branch e testar manualmente o recurso de jogos relacionados. Acesse o Codespace, abra o terminal e execute estes comandos (substitua `<branch-name>` pelo nome da branch criada pelo Copilot, por exemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados! Como antes, você pode iterar com o agente de nuvem do Copilot para solicitar atualizações, como ajustar a quantidade de jogos relacionados ou adicionar cabeçalhos e comentários TSDoc (lembre-se: a tarefa foi atribuída **antes** da atualização das instruções personalizadas). Faça as solicitações em um novo comentário na guia **Conversation**; o Copilot o verá e iniciará outra sessão.

## Revisar os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade implementados com o agente personalizado de acessibilidade. Este PR deve incluir o modo de alto contraste atribuído no Exercício 3 e o modo claro solicitado no painel de controle do Exercício 4.

1. Retorne ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR com título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o pull request terá a indicação **[WIP]**. Nesse caso, aguarde a conclusão. Isso pode levar alguns minutos.

4. Selecione **Files changed** para revisar o código gerado.
5. Revise a implementação, prestando atenção especial a:
   - componentes de interface para alternar os modos.
   - uso do armazenamento local para persistir as preferências.
   - mudanças de CSS ou estilo para os modos de alto contraste e claro.
   - atributos de acessibilidade (rótulos ARIA, navegação pelo teclado etc.).
   - código JavaScript/TypeScript que gerencia a alternância entre os modos.

6. Depois da revisão, retorne à guia **Conversation** e role a página para baixo.
7. Você deverá ver um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows entrarão na fila na seção de verificações do pull request. Se tudo correr bem, as verificações do projeto para a aplicação Astro serão aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** alterne o Codespace para essa branch e teste manualmente os recursos de acessibilidade. No terminal do Codespace, execute os comandos a seguir (substitua `<branch-name>` pelo nome da branch criada pelo Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Em seguida, inicie o aplicativo e teste os modos de alto contraste e claro no navegador para confirmar se funcionam e se as preferências persistem após recarregar a página.

Observe como o agente personalizado de acessibilidade ajudou a orientar a implementação segundo as práticas recomendadas de acessibilidade. Se encontrar problemas ou oportunidades de melhoria, mencione **@copilot** em um comentário para solicitar atualizações, como fez com os PRs anteriores.

## Exercício opcional — continuar delegando

O agente de nuvem funciona melhor quando você pode delegar itens reais do backlog e se dedicar a outras atividades. Para desenvolver esse hábito, registre mais algumas issues no repositório e atribua-as ao Copilot. Algumas ideias:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo.
- implementar paginação na página de listagem de jogos.
- adicionar validação de entrada e tratamento de erros aos auxiliares de acesso a dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Nestas lições, você:

- **Inspecionou os arquivos de instruções personalizadas do repositório** para ver como eles afetam o resultado do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, incluindo alternâncias para os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como painel de controle** para monitorar e orientar a sessão de acessibilidade em andamento.
- **Revisou e iterou sobre os pull requests do agente de nuvem**, mencionando `@copilot` para solicitar mudanças e aprovando workflows.

## Revisão e próximos passos

Você concluiu o percurso do agente de nuvem. Se quiser continuar aprendendo, os outros percursos complementam o que praticou:

- 🖥️ **[Percurso do VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Percurso da CLI](../../cli/)** — entregue duas mudanças revisadas pelo terminal com os modos Plan e Autopilot, skills de agente, agente personalizado de QA, Playwright MCP, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

No seu próprio repositório, experimente estas ideias:

- atribuir ao agente de nuvem uma issue de refatoração ou cobertura de testes.
- criar um agente personalizado para outro domínio.
- configurar `copilot-setup-steps.yml` para outra pilha de tecnologias.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
