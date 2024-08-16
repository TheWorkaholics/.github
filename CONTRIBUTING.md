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

## Referências

- [GitHub flow - GitHub Docs](https://docs.github.com/en/get-started/using-github/github-flow)

