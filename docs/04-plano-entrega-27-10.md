# Plano de Entrega — Apresentação Parcial de 27/10

## Dinâmica da apresentação

- Data: 27 de outubro de 2026
- Duração: 20 minutos (apresentar a solução desenvolvida + tirar dúvidas de implementação)

## O que é avaliado nesta entrega

- **Aspectos Gerais**: Repositório de Código e Configurações / Construção da Marca
- **Aspectos Técnicos**: Objetos Customizados / Relacionamentos
- **Critério de destaque**: criação de um aplicativo customizado para agrupar e navegar pelos objetos

## Checklist de execução

### 1. Marca (ver [02-marca.md](02-marca.md))
- [ ] Nome comercial definido
- [ ] Slogan definido
- [ ] Logotipo gerado e salvo em `docs/assets/`

### 2. Modelo de dados (ver [03-modelo-de-dados.md](03-modelo-de-dados.md))
- [ ] Validar a lista de campos de cada objeto rodando o Prompt 04 no ChatGPT
- [ ] Criar os 6 objetos do tema no Object Manager (Contrato de Serviço, Cláusula Contratual, Aditivo, Renovação, Reajuste, Histórico Contratual)
- [ ] Criar o objeto Endereço (obrigatório em todos os temas)
- [ ] Criar os campos de cada objeto
- [ ] Criar os relacionamentos (Master-Detail e Lookup) conforme o diagrama
- [ ] Criar os Record Types do objeto Contrato (Anual, Bienal, Corporativo)

### 3. Aplicativo customizado
- [ ] App Manager → New Lightning App
- [ ] Nome do app = nome comercial escolhido (ex.: "ContratAI")
- [ ] Adicionar logotipo do app
- [ ] Adicionar abas de todos os objetos do modelo
- [ ] Definir perfis de acesso ao app (mínimo: visível para todos por enquanto, perfis detalhados entram na fase de Segurança)

### 4. Repositório de Código e Configurações (este repositório)
- [ ] Projeto SFDX criado em `salesforce/` (feito — ver `salesforce/sfdx-project.json`)
- [ ] Instalar o Salesforce CLI (ver abaixo)
- [ ] Autenticar com a Org/Developer Edition/Trailhead Playground do grupo
- [ ] Rodar `sf project retrieve start` para puxar os metadados reais (objetos, campos, app, layouts) para dentro de `salesforce/force-app`
- [ ] Commitar os metadados retornados

## Passo a passo técnico no Salesforce (via UI)

1. **Setup → Object Manager → Create → Custom Object** — repetir para os 7 objetos listados acima
2. Em cada objeto, usar **Fields & Relationships → New** para criar os campos da tabela correspondente em [03-modelo-de-dados.md](03-modelo-de-dados.md)
3. Ao criar campos de relacionamento, escolher **Master-Detail Relationship** ou **Lookup Relationship** conforme indicado
4. Em **Contrato de Serviço → Record Types**, criar Anual / Bienal / Corporativo
5. **App Manager → New Lightning App** — montar o app com nome, logotipo e abas

## Descobrindo se já existe Org/CLI configurado

Rodamos a checagem nesta máquina e **o Salesforce CLI (`sf`/`sfdx`) ainda não está instalado** e não há nenhuma org autenticada localmente.

Para instalar (via npm, recomendado):
```bash
npm install --global @salesforce/cli
sf --version
```

Para conectar à org do grupo (Developer Edition ou Trailhead Playground):
```bash
sf org login web -a sf-gestao-contratos
```
Isso abre o navegador para login; depois de autenticado, a org fica salva com o alias `sf-gestao-contratos`.

Se o grupo ainda não tem nenhuma org:
- Criar uma **Developer Edition** gratuita em developer.salesforce.com, ou
- Usar um **Trailhead Playground** (se o curso já fornece um)

## Depois de criar tudo pela UI: trazendo para o repositório

```bash
cd salesforce
sf project retrieve start -o sf-gestao-contratos -m "CustomObject:Contrato_de_Servico__c" -m "CustomObject:Clausula_Contratual__c" -m "CustomObject:Aditivo__c" -m "CustomObject:Renovacao__c" -m "CustomObject:Reajuste__c" -m "CustomObject:Historico_Contratual__c" -m "CustomObject:Endereco__c" -m "CustomApplication"
```
(ou, de forma mais simples enquanto o projeto é pequeno: `sf project retrieve start -o sf-gestao-contratos -x manifest/package.xml` com um manifest gerado pelo próprio VS Code + extensão Salesforce)

## Pendências para depois de 27/10 (não é desta entrega)

- Segurança: Perfis, Papéis, Sharing Rules, Permission Sets
- Automação: 3 Record Triggered Flows, 1 Screen Flow, Subflows, Processo de Aprovação (2 níveis)
- Apex: Trigger Framework, Integração ViaCEP, Queueable/Batch, testes com 85% de cobertura
- Interface: Dynamic Forms, Dynamic Actions, 2–3 LWCs
- Analytics: Dashboard Executivo e Operacional
