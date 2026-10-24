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
- [x] Nome comercial definido
- [x] Slogan definido
- [x] Logotipo gerado e salvo em `docs/assets/`

### 2. Modelo de dados (ver [03-modelo-de-dados.md](03-modelo-de-dados.md))
- [x] Criar os 6 objetos do tema (Contrato de Serviço, Cláusula Contratual, Aditivo, Renovação, Reajuste, Histórico Contratual)
- [x] Criar o objeto Endereço (obrigatório em todos os temas)
- [x] Criar os campos de cada objeto
- [x] Criar os relacionamentos (Master-Detail e Lookup) conforme o diagrama
- [x] Criar os Record Types do objeto Contrato (Anual, Bienal, Corporativo)
- [x] Criar os 2 Roll-Up Summary (Total de Aditivos, Valor Acumulado)
- [ ] (Opcional) Validar/ajustar a lista de campos rodando o Prompt 04 no ChatGPT, se o grupo quiser revisar algo

### 3. Aplicativo customizado
- [x] Lightning App "ContratAI" criado com as 7 abas dos objetos
- [ ] Subir o logotipo (`docs/assets/logo-contratai.png`) no app pela UI (Setup → App Manager → editar ContratAI → Branding) — upload de imagem não é feito via deploy
- [ ] Definir perfis de acesso ao app (mínimo: visível para todos por enquanto, perfis detalhados entram na fase de Segurança)

### 4. Repositório de Código e Configurações (este repositório)
- [x] Projeto SFDX criado em `salesforce/`
- [x] Salesforce CLI instalado e autenticado na org (`sf-gestao-contratos`)
- [x] Objetos/campos/app escritos como metadados neste repositório e deployados na org via `sf project deploy start`
- [x] Commit e push realizados

## Como os objetos foram criados (via metadados + deploy, não via UI manual)

Em vez de criar cada objeto/campo clicando no Object Manager, o modelo de dados inteiro foi escrito como arquivos de metadados (`salesforce/force-app/main/default/objects/...`) e enviado para a org de uma vez com:
```bash
cd salesforce
sf project deploy start --source-dir force-app --target-org sf-gestao-contratos
```
Isso é equivalente ao resultado de criar tudo manualmente no Object Manager, só que fica registrado e versionado no repositório desde o início — e qualquer alteração futura (adicionar um campo, mudar um picklist) é feita editando o XML e rodando o deploy de novo, em vez de caçar o que foi mudado na UI depois.

**Se o grupo preferir conferir visualmente**: entrem em Setup → Object Manager na org e naveguem pelos 7 objetos — tudo que está documentado em [03-modelo-de-dados.md](03-modelo-de-dados.md) já deve estar lá.

**Se alguém do grupo criar algo direto pela UI** (ex.: ajustar um Page Layout, criar um Flow na fase de automação), o caminho é o inverso — trazer para o repositório com:
```bash
cd salesforce
sf project retrieve start --target-org sf-gestao-contratos --metadata "Flow:NomeDoFlow"
```
e depois commitar o que for baixado.

## Org conectada

- **Tipo**: Developer Edition (criada em developer.salesforce.com, conforme orientação do Gabriel_vds/João Medeiros no Discord)
- **Instance URL**: `https://orgfarm-fe59a2912e-dev-ed.develop.my.salesforce.com`
- **Alias no CLI**: `sf-gestao-contratos` (definida como org padrão deste projeto)
- **Salesforce CLI**: instalado via npm (`@salesforce/cli`)

Para qualquer integrante do grupo reconectar nesta mesma org pelo CLI (cada pessoa precisa logar com a própria sessão de navegador, mesmo usando a mesma org):
```bash
sf org login web -a sf-gestao-contratos --instance-url https://orgfarm-fe59a2912e-dev-ed.develop.my.salesforce.com
```

Para checar se a conexão está ativa a qualquer momento:
```bash
sf org display --target-org sf-gestao-contratos
```

## Pendências para depois de 27/10 (não é desta entrega)

- Segurança: Perfis, Papéis, Sharing Rules, Permission Sets
- Automação: 3 Record Triggered Flows, 1 Screen Flow, Subflows, Processo de Aprovação (2 níveis)
- Apex: Trigger Framework, Integração ViaCEP, Queueable/Batch, testes com 85% de cobertura
- Interface: Dynamic Forms, Dynamic Actions, 2–3 LWCs
- Analytics: Dashboard Executivo e Operacional
