# Modelo de Dados — Gestão de Contratos e Renovações

> Proposta de campos (10–12 por objeto, conforme Prompt 04) a partir dos objetos e relacionamentos oficiais do tema. Validem/ajustem rodando o Prompt 04 no ChatGPT colando o conteúdo de [01-tema-e-objetivo.md](01-tema-e-objetivo.md).
>
> Convenção de API Name: `Nome_Do_Campo__c` em objetos customizados.

## 1. Contrato de Serviço (`Contrato_de_Servico__c`) — objeto principal

| Campo | Tipo | Observação |
|---|---|---|
| Nome do Contrato | Auto Number (`CONT-{0000}`) | Name field |
| Cliente | Lookup (Account) | contraparte do contrato |
| Data de Início | Date | |
| Data de Término | Date | |
| Valor Mensal | Currency | |
| Valor Total do Contrato | Currency | pode virar Roll-Up de Aditivos |
| Status | Picklist: Ativo, Em Renovação, Encerrado, Cancelado, Suspenso | |
| Record Type | Anual / Bienal / Corporativo | conforme requisito de Record Types |
| Responsável Comercial | Lookup (User) | |
| Renovação Automática | Checkbox | |
| Dias para Vencimento | Fórmula (Data de Término − HOJE()) | atende requisito de campo fórmula |
| Total de Aditivos | Roll-Up Summary (COUNT de Aditivo) | atende requisito de Roll-Up Summary |
| Valor Acumulado | Roll-Up Summary (SUM de Valor do Ajuste em Aditivo) | atende requisito de Roll-Up Summary |

> Correção: removido o campo "Endereço de Faturamento" (Lookup de Contrato → Endereço) que constava numa versão anterior deste documento — ele duplicava, em sentido invertido, o relacionamento já definido no item 7 (Endereço → Contrato). Mantido só um relacionamento entre os dois objetos.

## 2. Cláusula Contratual (`Clausula_Contratual__c`) — Master-Detail → Contrato

| Campo | Tipo |
|---|---|
| Contrato | Master-Detail → Contrato de Serviço |
| Título da Cláusula | Text(80) |
| Número da Cláusula | Number |
| Tipo de Cláusula | Picklist: Pagamento, Rescisão, Confidencialidade, SLA, Penalidade, Renovação |
| Descrição | Long Text Area |
| Obrigatória | Checkbox |
| Status | Picklist: Vigente, Em Revisão, Revogada |
| Data de Inclusão | Date |

## 3. Aditivo (`Aditivo__c`) — Master-Detail → Contrato

| Campo | Tipo |
|---|---|
| Número do Aditivo | Auto Number |
| Contrato | Master-Detail → Contrato de Serviço |
| Tipo de Aditivo | Picklist: Valor, Prazo, Escopo, Partes |
| Data do Aditivo | Date |
| Descrição | Long Text Area |
| Valor do Ajuste | Currency |
| Novo Valor do Contrato | Currency |
| Status | Picklist: Em Análise, Aprovado, Rejeitado |
| Responsável | Lookup (User) |

> Base do Roll-Up "Total de aditivos" e "Valor acumulado" no Contrato.

## 4. Renovação (`Renovacao__c`) — Master-Detail → Contrato

| Campo | Tipo |
|---|---|
| Número da Renovação | Auto Number |
| Contrato | Master-Detail → Contrato de Serviço |
| Data da Renovação | Date |
| Novo Prazo Final | Date |
| Valor Renovado | Currency |
| Status da Renovação | Picklist: Pendente, Aprovada, Recusada, Em Negociação |
| Percentual de Reajuste Aplicado | Percent |
| Responsável pela Renovação | Lookup (User) |
| Data Limite para Decisão | Date |
| Observações | Long Text Area |

## 5. Reajuste (`Reajuste__c`) — Lookup → Contrato

| Campo | Tipo |
|---|---|
| Contrato | Lookup → Contrato de Serviço |
| Data do Reajuste | Date |
| Índice Aplicado | Picklist: IPCA, IGP-M, INPC, Fixo |
| Percentual de Reajuste | Percent |
| Valor Anterior | Currency |
| Valor Reajustado | Fórmula (Currency) |
| Status | Picklist: Programado, Aplicado, Cancelado |
| Aprovado Por | Lookup (User) |

## 6. Histórico Contratual (`Historico_Contratual__c`) — Lookup → Contrato

| Campo | Tipo |
|---|---|
| Contrato | Lookup → Contrato de Serviço |
| Data do Evento | Date/Time |
| Tipo de Evento | Picklist: Criação, Alteração, Aditivo, Renovação, Cancelamento, Reajuste |
| Descrição do Evento | Long Text Area |
| Usuário Responsável | Lookup (User) |
| Valor Anterior | Text |
| Valor Novo | Text |

> Em geral alimentado por automação (Flow/Trigger) nas próximas semanas, não só por cadastro manual.

## 7. Endereço (`Endereco__c`) — obrigatório em todos os temas (integração ViaCEP)

| Campo | Tipo |
|---|---|
| Contrato | Lookup → Contrato de Serviço |
| CEP | Text(9) |
| Logradouro | Text(255) |
| Número | Text(10) |
| Complemento | Text(255) |
| Bairro | Text(100) |
| Cidade | Text(100) |
| Estado | Text(2) |
| Log de Integração | Long Text Area |

> Este objeto só entra em uso de fato quando a integração Apex Callout com o ViaCEP for implementada (fase de automação). Para 27/10 vocês só precisam **criar o objeto e o relacionamento**, não a integração.

## Resumo de relacionamentos para o Object Manager

```
Contrato_de_Servico__c (objeto principal)
├─ Clausula_Contratual__c   (Master-Detail)
├─ Aditivo__c                (Master-Detail)
├─ Renovacao__c              (Master-Detail)
├─ Reajuste__c               (Lookup)
├─ Historico_Contratual__c   (Lookup)
└─ Endereco__c               (Lookup)
```

Isso cobre o requisito obrigatório de ter **Master-Detail e Lookup ao mesmo tempo**.
