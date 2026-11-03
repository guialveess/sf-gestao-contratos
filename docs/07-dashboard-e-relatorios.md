# Dashboard e Relatórios

> Atende ao feedback pós-apresentação de adicionar indicadores visuais (charts), e também avança o requisito obrigatório de Dashboard Executivo/Operacional.

## Reports criados (via API, já na org)

| Report | Agrupado por | Mostra |
|---|---|---|
| **ContratAI - Contratos por Status** | Status__c | Valor Mensal e Data de Término de cada contrato |
| **ContratAI - Contratos por Tipo** | Record Type (Anual/Bienal/Corporativo) | Status e Valor Mensal de cada contrato |

Pasta: **ContratAI Dashboards** (criada especificamente para o projeto).

Esses dois reports foram criados diretamente via **API REST de Analytics do Salesforce** (`/services/data/v62.0/analytics/reports`), em vez de montados na tela — mesmo princípio de todo o resto do projeto (configuração registrada via comando, não clique avulso).

## Dashboard — passo a passo para montar (manual, 2 minutos)

A criação de Dashboard via API tem um formato de JSON mais complexo e não documentado de forma acessível publicamente; o caminho mais confiável é montar pela interface, usando os reports que já existem:

1. **App Launcher → "Dashboards"** → **Novo Dashboard**
2. Nome: **"ContratAI - Visão Geral"**, pasta: **ContratAI Dashboards**
3. **+ Componente** → report **"ContratAI - Contratos por Status"** → gráfico tipo **Rosca (Donut)**
4. **+ Componente** → report **"ContratAI - Contratos por Tipo"** → gráfico tipo **Coluna (Vertical Column)**
5. Salvar

## Pendências (fase de automação/analytics completa)

- [ ] Dashboard "ContratAI - Visão Geral" montado na UI (passo a passo acima)
- [ ] Reports adicionais sugeridos pelo tema: "Receita recorrente" (soma de Valor Mensal dos contratos Ativos) e "Contratos próximos do vencimento" (filtro por Dias para Vencimento)
