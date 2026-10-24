# Residência Capgemini — Gestão de Contratos e Renovações

Repositório de código e documentação do grupo para o projeto de residência em Salesforce (parceria com a Capgemini). Tema do grupo: **Gestão de Contratos e Renovações**.

Este repositório é o próprio entregável do critério "Repositório de Código e Configurações" (ver [docs/00-requisitos-obrigatorios.md](docs/00-requisitos-obrigatorios.md)).

## Estrutura

```
residencia/
├── docs/                           # toda a documentação do projeto
│   ├── 00-requisitos-obrigatorios.md   # regras valendo para TODOS os temas
│   ├── 01-tema-e-objetivo.md           # objetivo, objetos e relacionamentos do nosso tema
│   ├── 02-marca.md                     # nome, slogan, identidade visual
│   ├── 03-modelo-de-dados.md           # campos de cada objeto customizado
│   ├── 04-plano-entrega-27-10.md       # checklist e passo a passo da entrega desta semana
│   └── 05-prompts-mentor.md            # prompts de IA sugeridos pelo mentor
├── salesforce/                     # projeto SFDX (metadados do Salesforce)
│   ├── sfdx-project.json
│   └── force-app/main/default/     # objects, applications, flows, classes, lwc, etc.
├── Sugestões de Prompts.pdf        # material original do mentor
└── Temas de Projetos.pdf           # material original da Capgemini (requisitos + temas)
```

## Por onde começar

1. Leia [docs/00-requisitos-obrigatorios.md](docs/00-requisitos-obrigatorios.md) e [docs/01-tema-e-objetivo.md](docs/01-tema-e-objetivo.md)
2. Siga o checklist de [docs/04-plano-entrega-27-10.md](docs/04-plano-entrega-27-10.md) — é o que vale para a apresentação desta semana
3. Use [docs/05-prompts-mentor.md](docs/05-prompts-mentor.md) para validar/refinar nome, marca e campos com IA
4. Crie os objetos no Salesforce pela UI, depois instale o Salesforce CLI e traga os metadados para `salesforce/` (instruções em 04-plano-entrega-27-10.md)

## Status

- [x] Marca definida (nome, slogan, logo) — ver [docs/02-marca.md](docs/02-marca.md)
- [ ] Objetos e campos criados na org
- [ ] App customizado criado
- [ ] Metadados versionados neste repositório
- [ ] Apresentação de 27/10 preparada
