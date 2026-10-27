# Dados de Demonstração

Massa de dados mínima para demonstrar o ContratAI funcionando na apresentação, com um contrato e pelo menos um registro em cada um dos 7 objetos do modelo.

Os registros ficam versionados aqui em vez de serem cadastrados só na org, para que qualquer integrante do grupo consiga recriar o mesmo cenário em segundos, numa org nova ou depois de um reset.

## Arquivos

| Arquivo | Objeto | Registros |
|---|---|---|
| `Contrato_de_Servico__c.json` | Contrato de Serviço | 1 |
| `Clausula_Contratual__c.json` | Cláusula Contratual | 3 |
| `Aditivo__c.json` | Aditivo | 2 |
| `Renovacao__c.json` | Renovação | 1 |
| `Reajuste__c.json` | Reajuste | 1 |
| `Historico_Contratual__c.json` | Histórico Contratual | 3 |
| `Endereco__c.json` | Endereço | 1 |
| `plan.json` | ordem de importação | |

## Como importar na org

A partir da pasta `salesforce/`:

```bash
sf data import tree --plan data/plan.json --target-org sf-gestao-contratos
```

O `plan.json` define a ordem: o Contrato entra primeiro e guarda sua referência (`saveRefs`), e os demais objetos resolvem essa referência (`resolveRefs`) através do `"@ContratoDemo"` presente no campo `Contrato__c`. É assim que os relacionamentos Master-Detail e Lookup são amarrados sem precisar conhecer os IDs da org.

## Cenário montado

Um contrato de suporte de TI com valor mensal de R$ 8.500,00, vigência de 01/03/2025 a 01/03/2027, em status "Em Renovação", com:

- 3 cláusulas (Pagamento, SLA e Rescisão)
- 2 aditivos, um de Valor (R$ 1.200,00) e um de Prazo (R$ 800,00)
- 1 renovação em negociação
- 1 reajuste pelo IPCA de 4,50%
- 3 eventos de histórico (Criação, Aditivo e Reajuste)
- 1 endereço preenchido manualmente

Os números foram escolhidos para que os campos calculados fiquem visíveis na demonstração:

- **Total de Aditivos** (Roll-Up COUNT) deve mostrar **2**
- **Valor Acumulado** (Roll-Up SUM de `Valor_do_Ajuste__c`) deve mostrar **R$ 2.000,00**
- **Valor Reajustado** no Reajuste (fórmula `Valor_Anterior__c * (1 + Percentual_de_Reajuste__c / 100)`) deve mostrar **R$ 8.882,50**
- **Dias para Vencimento** no Contrato (fórmula `Data_de_Termino__c - TODAY()`) varia conforme a data em que a importação for feita

## O que foi deixado de fora de propósito

- **Campos de Auto Number** (`Name`): são gerados pela própria org (CONT-0001, CLA-0001, etc.), então não podem ser informados no arquivo.
- **Campos fórmula e Roll-Up Summary**: `Dias_para_Vencimento__c`, `Total_de_Aditivos__c`, `Valor_Acumulado__c` e `Valor_Reajustado__c` são somente leitura e calculados pela plataforma. Informá-los faria a importação falhar.
- **Lookups para `User`** (`Responsavel__c`, `Responsavel_Comercial__c`, `Usuario_Responsavel__c`, `Aprovado_Por__c`, `Responsavel_pela_Renovacao__c`): o ID do usuário muda de org para org e de pessoa para pessoa, então ficam em branco. Dá para preencher pela tela depois da importação.
- **`Cliente__c`** (Lookup para `Account`): depende de uma conta já existente na org. Dá para vincular pela tela em poucos segundos, ou criar a conta antes e referenciá-la.
- **Record Type do Contrato** (Anual, Bienal, Corporativo): o `sf data import tree` não resolve Record Type por nome, então o registro entra com o Record Type padrão do usuário. Para a demonstração, vale trocar pela tela, no botão "Alterar tipo de registro".

## Para limpar e reimportar

Não existe um comando de "desfazer" a importação. Se precisar recomeçar, apague os registros pela tela (apagar o Contrato leva junto as Cláusulas, os Aditivos e as Renovações, porque o relacionamento é Master-Detail) e rode a importação de novo.
