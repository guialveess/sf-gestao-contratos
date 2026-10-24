# Tema do Grupo: Gestão de Contratos e Renovações

> Fonte: `Temas de Projetos.pdf`, item 5 (dos 8 temas disponíveis no documento).

## Objetivo

Controlar contratos, aditivos e renovações de serviços.

## Objetos Customizados (conforme o documento oficial)

- Contrato de Serviço
- Aditivo
- Renovação
- Histórico Contratual
- Cláusula Contratual
- Reajuste

(6 objetos — acima do mínimo de 5 exigido. Ver também o objeto `Endereço` obrigatório para todos os temas, em [00-requisitos-obrigatorios.md](00-requisitos-obrigatorios.md).)

## Relacionamentos (conforme o documento oficial)

```
Contrato
├─ Cláusula
├─ Aditivo
├─ Renovação
├─ Histórico
└─ Reajuste
```

Todos os demais objetos se relacionam diretamente ao Contrato (não há hierarquia de 3 níveis neste tema). Ver a definição de tipo de relacionamento (Master-Detail vs Lookup) por objeto em [03-modelo-de-dados.md](03-modelo-de-dados.md).

## Record Types sugeridos

**Contrato**
- Anual
- Bienal
- Corporativo

## Fórmulas e Roll-Ups sugeridos

**Fórmulas**
- Dias para Vencimento
- Valor Reajustado

**Roll-Ups**
- Total de aditivos
- Valor acumulado

## Processo de Aprovação sugerido

- Jurídico
- Diretor Comercial

(2 níveis — atende ao requisito mínimo de aprovação em 2 níveis.)

## Dashboards sugeridos

**Dashboard Executivo**
- Receita recorrente
- Retenção

**Dashboard Operacional**
- Contratos próximos do vencimento
- Renovações pendentes
