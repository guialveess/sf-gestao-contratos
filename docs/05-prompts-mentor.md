# Prompts Sugeridos pelo Mentor

> Transcrito de `Sugestões de Prompts.pdf`. Usar em sequência no ChatGPT (ou similar), sempre colando o conteúdo indicado do tema (ver [01-tema-e-objetivo.md](01-tema-e-objetivo.md)).

## Parte 01 — Montando a cara do negócio

**Prompt 01 — Criando o nome do negócio**
> Considere o título e o objetivo apresentados abaixo e gere opções de nomes comerciais para o negócio.
> Conteúdo do documento de temas: `<<Inserir título e objetivo do documento de temas>>`

Observação do mentor: copiar o conteúdo do documento de temas do assunto escolhido, senão o prompt fica sem contexto.

**Prompt 02 — Criando um slogan**
> Gostei da opção X. Agora, gere opções de slogans chamativos que estejam relacionados ao nome escolhido e transmitam a proposta do negócio.

Observação: substituir X pelo nome escolhido no Prompt 01.

**Prompt 03 — Criando a identidade visual**
> Escolho a opção X. Agora, crie uma proposta de logotipo que combine o nome e o slogan escolhidos, representando a identidade e a proposta do negócio.

Observação: pode ser necessário pedir ajustes — explorar alternativas até ficar satisfatório.

## Parte 02 — Gerando objetos e campos

**Prompt 04 — Definindo os campos dos objetos**
> Considerando as escolhas realizadas anteriormente e a lista de objetos e relacionamentos apresentada abaixo, ajude-me a identificar quais campos poderiam ser criados para cada objeto.
> Lembre-se de que estou desenvolvendo uma aplicação Salesforce e preciso de **10 a 12 campos por objeto**, considerando as necessidades do negócio e as informações que deverão ser armazenadas no sistema.
> Conteúdo do documento de temas: `<<Inserir o tópico de objetos e relacionamentos do documento de temas>>`

**Prompt 05 — Explorando o sistema na prática (IMPORTANTE)**
> Considerando os objetos criados e seus respectivos campos, ajude-me a entender como utilizar o sistema na prática, simulando a experiência de um usuário em treinamento. Explique, passo a passo, como o usuário poderia navegar pelo sistema, cadastrar informações, preencher os campos, relacionar registros e realizar as principais atividades do negócio.

> O mentor marcou este como o mais importante para entender o fluxo de funcionamento entre os objetos — rodem ele depois de ter o modelo de dados fechado, antes de sair criando tudo direto no Salesforce.

## Parte 03 — Indo além do básico

**Prompt 06 — Organizando os campos por Record Types (EXTRA)**
> Considerando os campos definidos anteriormente para cada objeto, ajude-me a organizá-los de acordo com os Record Types sugeridos abaixo.
> Conteúdo do documento de temas: `<<Inserir o tópico de Record Types do documento de temas>>`
> Pensando nessa estrutura de Record Types, como os campos sugeridos poderiam ser distribuídos entre eles? Considere quais informações são comuns a todos os tipos de registro e quais são específicas de cada tipo.

---

## Como aplicar isso ao nosso tema (Gestão de Contratos e Renovações)

- Prompt 01/02/03 → usar o objetivo descrito em [01-tema-e-objetivo.md](01-tema-e-objetivo.md); resultado proposto em [02-marca.md](02-marca.md)
- Prompt 04 → usar a lista de objetos/relacionamentos de [01-tema-e-objetivo.md](01-tema-e-objetivo.md); resultado proposto em [03-modelo-de-dados.md](03-modelo-de-dados.md)
- Prompt 05 → rodar depois que o modelo de dados estiver validado pelo grupo; vale documentar a resposta em `docs/06-fluxo-de-uso.md` (criar quando chegar a hora)
- Prompt 06 → aplicar ao Record Type de Contrato (Anual/Bienal/Corporativo) quando chegarem na fase de refinamento
