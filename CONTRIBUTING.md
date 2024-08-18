# Contribuição

## Antes de começar

Novas ideias sobre organização, bibliotecas e arquiteturas são sempre bem-vindas!

Este projeto está aberto a todo tipo de contribuição. No entanto, é importante que todas as mudanças significativas sejam discutidas previamente. Caso queira compartilhar uma ideia, abra uma `issue` com a tag apropriada para que possamos discutir isso no futuro.

## Sumário

As regras descritas neste documento estão organizadas em quatro seções, que implementam total ou parcialmente workflows amplamente reconhecidos e utilizados na comunidade:

- [GitHub Flow](#) - Como gerenciar `projetos`, `forks` e `pull requests`.
- [Git Flow](#) - Orientações para organizar `branches` por `features`.
- [Versionamento Semântico](#) - Como lidar com `versões` e `lançamentos`.
- [Conventional Commits](#) - Práticas recomendadas para fazer bons `commits`.

## GitHub Flow

Antes de tudo, é importante destacar que `GitHub Flow` e `Git Flow` **não** são a mesma coisa.

O `GitHub Flow`, como descrito na documentação oficial [Fluxo do GitHub](https://docs.github.com/pt/get-started/using-github/github-flow), é um "fluxo de trabalho leve e baseado em branches". Embora essa descrição possa parecer vaga, na prática, a maioria já utilizou esse fluxo: criar uma branch, fazer alterações, e abrir um pull request.

Por outro lado, o `Git Flow` é um processo focado na organização das branches. Ele dita como nomear, organizar, mesclar, corrigir, além de outras práticas. Enquanto o `GitHub Flow` é leve e ágil, o `Git Flow` adiciona estrutura e formalidade ao processo de desenvolvimento.

Dito isso, podemos resumir o fluxo do GitHub da seguinte forma:

1. **Branch**: Crie sua própria branch. A menos que haja um motivo muito específico, evite fazer commits diretamente na `dev`, e ainda menos na `main`.
2. **Commit**: Um dia você precisará encontrar o que causou um problema, e nesse dia, será útil ter commits com nomes claros e descritivos.
3. **Pull Request**: Lembre-se de que alguém, possivelmente eu, irá revisar seu pull request. Por favor, tenha misericórdia e evite enviar alterações em 120 arquivos de uma só vez.
4. **Revisão**: Esta é uma etapa delicada onde os revisores devem deixar perguntas, comentários e sugestões. Embora nem sempre seja realizada, quando for, é importante ser construtivo e respeitoso com os colegas.
5. **Merge**: Após a revisão e aprovação do pull request, o merge é feito, e o código passa a fazer parte das branches principais.
6. **Deletar a Branch**: Geralmente, a branch é deletada automaticamente durante o merge, mas é importante também removê-la localmente.

Embora o `GitHub Flow` seja simples, ele apresenta alguns pontos sensíveis entre o pull request e o merge.

Imagine que você esteja trabalhando em um projeto com várias outras pessoas. Após clonar o repositório, criar sua branch e realizar as modificações, você decide, no seu repositório local, fazer o merge diretamente na `dev` e, em seguida, sincronizar com o GitHub. Como isso é diferente de alterar a `dev` diretamente?

A verdade é que, para quem faz a revisão ou gerencia o repositório, essa diferença é inexistente. Ao adotar essa prática, você perde a oportunidade de ter seu código revisado, pode causar problemas com o CI/CD, prejudica o histórico de commits, se obriga a resolver conflitos de código sozinho, reduz a transparência, e, em alguns casos, pode simplesmente ter seu push bloqueado.

Outro ponto importante é a revisão. Embora seja comum que não haja nenhuma revisão, quando ela ocorre, especialmente em times que não estão familiarizados com o processo, é normal surgirem conflitos. Esses conflitos podem ser causados por diversas razões, como regras rígidas, demora na revisão ou falta de disponibilidade para resolver problemas. Nesse contexto, dois pontos são importantes:

- O pull request é atualizado automaticamente sempre que você modifica sua branch. Isso significa que, caso seu código não passe na revisão, basta fazer as alterações necessárias e o pull request será atualizado, sem a necessidade de reenvio.
- O revisor não é responsável por corrigir o código, mas sim por impedir que código problemático seja introduzido. Às vezes, o erro é simples, como um arquivo fora de lugar ou um nome mal escrito, e pode ser tentador fazer o merge e corrigir com outro commit. No entanto, isso não deve ser feito, pois incentiva maus hábitos e polui o histórico do código.

Finalmente, o merge. Embora o `GitHub Flow` não especifique onde o merge deve ser feito, geralmente ele é direcionado para as branches `dev` ou `main`. Isso significa que o pull request aceito contém o código mais recente e mais próximo da produção. Tenha isso em mente ao realizar merges.

## Git Flow

A ideia do Git Flow é organizar as branches, e suas regras não são exatamente complicadas. No entanto, como todo padrão, é importante saber quando evitar excessos.

Nesse fluxo de trabalho, temos dois tipos de branches: as padrões e as temporárias. Branches padrões são os suspeitos usuais: main e dev, enquanto as branches temporárias recebem nomes de acordo com a situação.

**Branches padrões:**

- **Master ou Main**: Onde fica o código em produção. Eventualmente, tudo vem parar aqui.
- **Development ou Dev**: Aqui fica o código em desenvolvimento, que será o próximo a entrar em produção. É a branch mais atualizada e a com maior atividade.

As branches temporárias seguem a nomenclatura `<branch_subtype>/<name>`. O subtipo pode ser `feature`, `bugfix`, `hotfix` ou `release`. O nome varia de acordo com a implementação e necessidade.

- **Feature**: São as branches com novas implementações. Elas são sempre criadas a partir da `dev`. Alguns exemplos são "feature/buttons" ou "feat/home-page".
- **Bugfix**: Parecidas com as features, também são criadas a partir da `dev`, porém com a intenção de corrigir bugs e problemas específicos. Por exemplo, "bugfix/login-issue".
- **Hotfix**: Essas são usadas para resolver bugs críticos que precisam ser corrigidos imediatamente no código de produção. Elas são criadas a partir da ramificação `main` e mescladas de volta na nela mesma e na `development`. Por exemplo, "hotfix/security-patch".
- **Release**: Serve para manter o histórico de lançamento. Segue o versionamento semântico como parte do nome.

No geral, o `Git Flow` é uma faca de dois gumes. Enquanto `features` e `fixes` são relativamente compreensíveis, `release` pode pecar pelo excesso.

Pense em um time Scrum, com sprints entre uma semana e um mês. Ao final de cada sprint, sempre haverá um "entregável", ou seja, a cada semana haverá uma nova versão do produto. Isso significa que, em um ano, facilmente haverá 50 branches só de release. Tenha em mente que alguns projetos podem durar décadas.

Nesse sentido, não é recomendado o uso de branches de release em times ágeis. Também pode não ser apropriado dedicar mais esforço ao nome das branches do que aos comentários em si. Sendo assim, eu recomendo a seguinte abordagem:

- **feat**: Equivalente a features, mas com um nome mais simples. Essa escolha será discutida mais adiante, mas se resume ao fato de que a maioria dos seus commits terá essa palavra incluída.
- **fix**: Seja bugfix ou hotfix, ambos servem ao mesmo propósito: corrigir bugs. Bugfix tende a ser menos urgente, portanto, é incluído apenas na branch dev, enquanto hotfix é incluído tanto em dev quanto em main. No final do dia, tudo o que você precisa lembrar é de enviar qualquer branch para dev; o resto é detalhe.
- **release**: Enquanto não faz sentido criar releases toda semana, alguns são mais relevantes que outros. A primeira versão de produção, a primeira `1.0.0`. Não é necessário salvar cada nova versão, apenas as mais importantes. Isso você quem define.

Por fim, é fácil compreender como isso complementa o GitHub Flow de forma eficiente. Boa parte do nosso trabalho é feita em branches, e algo tão vago quanto "crie sua própria branch" não tem muito significado. Um bom nome de branch, assim como bons commits, ajudam a encontrar alterações no futuro e entender como o sistema se desenvolve ao longo do tempo. No início, isso não parece ter importância, mas com o passar dos anos, é um esforço que se paga.


## Referências

- [GitHub flow - GitHub Docs](https://docs.github.com/en/get-started/using-github/github-flow)
- [Git Flow: entenda o que é, como e quando utilizar](https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar)

