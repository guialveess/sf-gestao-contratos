# Requisitos Obrigatórios para Todos os Projetos

> Fonte: `Temas de Projetos.pdf` (documento da Capgemini), páginas 1–3.
> Isso vale para **todos os grupos**, independentemente do tema escolhido. Parte disso é cobrada já na entrega parcial de 27/10, parte fica para as próximas aulas (automações).

## Segurança

**Perfis**
- Perfil Operacional
- Perfil Gestor
- Perfil Administrativo

**Papéis (Role Hierarchy)**
- Operador
- Coordenador
- Diretor

**Compartilhamento**
- Role Hierarchy
- Sharing Rule baseada em critérios
- Permission Set para funções especiais

## Dados

Cada projeto deve possuir:
- Mínimo de **5 objetos customizados**
- Relacionamentos **Master-Detail**
- Relacionamentos **Lookup**
- Campos **Fórmula**
- **Roll-Up Summary**
- **Record Types**
- **Page Layouts** específicos por perfil

## Automação

**Flow**
- 3 Record Triggered Flows
- 1 Screen Flow
- Flows encadeados (Subflows)

**Aprovação**
- Processo de Aprovação com pelo menos 2 níveis
- Aprovação baseada em valor, categoria ou prioridade

**Apex**
- Trigger Framework
- Integração ViaCEP (ver seção específica abaixo)
- Queueable ou Batch
- Testes com cobertura mínima de 85%

**Interface**
- Lightning App personalizada
- Dynamic Forms
- Dynamic Actions
- 2 a 3 LWCs

## Analytics

- **Dashboard Executivo**: indicadores estratégicos para gestão
- **Dashboard Operacional**: indicadores para acompanhamento diário da equipe

## Itens para Avaliação (critérios oficiais)

- **Repositório de Código e Configurações**: todo projeto deve ter um repositório dedicado para armazenar e versionar os artefatos gerados (é este repositório aqui).
- **Construção da Marca**: a solução deve ser apresentada como produto de mercado, com nome comercial e identidade visual (logomarca) relacionada ao domínio de negócio.

## Integração ViaCEP (obrigatória em todos os projetos)

Todo projeto deve ter um **objeto de endereço** relacionado ao processo principal, contendo:
- CEP
- Logradouro
- Número
- Complemento
- Bairro
- Cidade
- Estado

Regras:
- A consulta ao CEP deve ser feita via **Apex Callout** para a API do ViaCEP.
- Pode ser acionada por: LWC, Screen Flow, ou Trigger + Queueable.
- Os dados retornados devem preencher automaticamente os campos de endereço.
- Deve registrar **logs de integração** para auditoria.

> Isso é parte da fase de automação (próximas aulas), mas já vale desenhar o objeto `Endereço__c` agora, relacionado ao `Contrato de Serviço`, para não precisar redesenhar o modelo de dados depois. Ver [03-modelo-de-dados.md](03-modelo-de-dados.md).

## O que é cobrado especificamente na entrega de 27/10

Segundo a orientação do mentor (ver [04-plano-entrega-27-10.md](04-plano-entrega-27-10.md)), a apresentação parcial de 27/10 avalia apenas:
- Aspectos Gerais: Repositório de Código e Configurações + Construção da Marca
- Aspectos Técnicos: Objetos Customizados + Relacionamentos
- Critério de destaque: Aplicativo customizado agrupando os objetos

Segurança, automação (Flows/Apex/Aprovação) e Analytics ficam para as próximas entregas — segundo o aviso do professor, "a próxima aula ainda vai ter um pouco do tema de automações".
