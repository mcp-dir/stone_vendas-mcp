# Ferramentas

Stone Vendas expõe 9 ferramentas (todas somente leitura).

### 1. `stone_vendas_contas`
**Input**: `account` (opcional)

Lista os StoneCodes (estabelecimentos) Stone conectados neste install, com id e apelido.

### 2. `stone_vendas_listar`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `forma_pagamento` (opcional), `bandeira` (opcional), `status` (opcional), `limite` (opcional), `account` (opcional)

Lista as vendas do adquirente Stone no período, uma linha por transação capturada, com data e hora, valor bruto e líquido, forma de pagamento (crédito, débito, pré-pago, voucher, boleto), bandeira, cartão truncado, ti…

### 3. `stone_vendas_resumo`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `agrupar_por` (opcional), `incluir_pix` (opcional), `account` (opcional)

Totais consolidados das vendas Stone no período, o equivalente ao Resumo de vendas do painel.

### 4. `stone_vendas_cancelamentos`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `account` (opcional)

Cancelamentos, chargebacks e reapresentações de chargeback da conta Stone no período, com o NSU da venda de origem, valor, datas e motivo.

### 5. `stone_vendas_recebiveis`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `account` (opcional)

Agenda de recebíveis Stone: as parcelas ainda não pagas com a data prevista de pagamento, detalhadas e totalizadas por data.

### 6. `stone_vendas_liquidacoes`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `account` (opcional)

Liquidações da Stone no período, o que foi efetivamente depositado, com valor total e a conta bancária favorecida.

### 7. `stone_vendas_pix`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `apenas_maquininha` (opcional), `status` (opcional), `limite` (opcional), `account` (opcional)

Vendas por Pix na maquininha Stone no período, com data e hora, valor, taxa, status (paga ou cancelada), terminal, chave Pix, e2e id e dados do pagador.

### 8. `stone_vendas_limpar_cache`
**Input**: `data_inicio` (opcional), `data_fim` (opcional), `account` (opcional)

Força a Stone a regerar o arquivo de conciliação do período, descartando o extrato que ela mantém em cache.

### 9. `stone_vendas_arquivo`
**Input**: `data`, `account` (opcional)

Arquivo de conciliação completo de um único dia, já convertido de XML para JSON, com todos os blocos (vendas, liquidações na conta, agenda prevista, eventos financeiros, pagamentos e posição de carteira).

## Prompts de exemplo

```
Qual foi o resumo de vendas da Stone no mês passado por forma de pagamento?
Liste as vendas Stone da semana passada por bandeira
Quanto tenho para receber da Stone nos próximos dias?
Teve algum chargeback ou cancelamento na Stone neste mês?
Quanto entrou de Pix na maquininha Stone na semana passada?
```
