# Diagrama do Modelo de Dados

> Diagrama visual dos 7 objetos e seus relacionamentos. O GitHub renderiza este diagrama automaticamente (é um diagrama Mermaid, escrito em texto e versionado como qualquer outro arquivo).

```mermaid
erDiagram
    CONTRATO_DE_SERVICO ||--o{ CLAUSULA_CONTRATUAL : "Master-Detail"
    CONTRATO_DE_SERVICO ||--o{ ADITIVO : "Master-Detail"
    CONTRATO_DE_SERVICO ||--o{ RENOVACAO : "Master-Detail"
    CONTRATO_DE_SERVICO ||--o{ REAJUSTE : "Lookup"
    CONTRATO_DE_SERVICO ||--o{ HISTORICO_CONTRATUAL : "Lookup"
    CONTRATO_DE_SERVICO ||--o{ ENDERECO : "Lookup"
    CONTRATO_DE_SERVICO }o--|| ACCOUNT : "Lookup (Cliente)"

    CONTRATO_DE_SERVICO {
        autonumber Numero_do_Contrato
        text Objeto_do_Contrato
        lookup Cliente
        date Data_de_Inicio
        date Data_de_Termino
        currency Valor_Mensal
        picklist Status
        recordtype Record_Type "Anual, Bienal, Corporativo"
        lookup Responsavel_Comercial
        checkbox Renovacao_Automatica
        formula Dias_para_Vencimento
        rollup Total_de_Aditivos
        rollup Valor_Acumulado
    }
    CLAUSULA_CONTRATUAL {
        masterdetail Contrato
        text Titulo_da_Clausula
        number Numero_da_Clausula
        picklist Tipo_de_Clausula
        longtext Descricao
        checkbox Obrigatoria
        picklist Status
        date Data_de_Inclusao
    }
    ADITIVO {
        masterdetail Contrato
        picklist Tipo_de_Aditivo
        date Data_do_Aditivo
        longtext Descricao
        currency Valor_do_Ajuste
        currency Novo_Valor_do_Contrato
        picklist Status
        lookup Responsavel
    }
    RENOVACAO {
        masterdetail Contrato
        date Data_da_Renovacao
        date Novo_Prazo_Final
        currency Valor_Renovado
        picklist Status_da_Renovacao
        percent Percentual_de_Reajuste_Aplicado
        lookup Responsavel_pela_Renovacao
        date Data_Limite_para_Decisao
        longtext Observacoes
    }
    REAJUSTE {
        lookup Contrato
        date Data_do_Reajuste
        picklist Indice_Aplicado
        percent Percentual_de_Reajuste
        currency Valor_Anterior
        formula Valor_Reajustado
        picklist Status
        lookup Aprovado_Por
    }
    HISTORICO_CONTRATUAL {
        lookup Contrato
        datetime Data_do_Evento
        picklist Tipo_de_Evento
        longtext Descricao_do_Evento
        lookup Usuario_Responsavel
        text Valor_Anterior
        text Valor_Novo
    }
    ENDERECO {
        lookup Contrato
        text CEP
        text Logradouro
        text Numero
        text Complemento
        text Bairro
        text Cidade
        text Estado
        longtext Log_de_Integracao
    }
    ACCOUNT {
        text Name "empresa cliente"
    }
```

## Como ler o diagrama

- `||--o{` = relacionamento **Master-Detail** (pai/filho forte — se o Contrato for excluído, o filho vai junto)
- `}o--||` = relacionamento **Lookup** (ligado, mas independente)
- Cada caixa lista os principais campos daquele objeto, com o tipo entre o nome do campo e sua descrição

Documentação completa de cada campo: [03-modelo-de-dados.md](03-modelo-de-dados.md).
