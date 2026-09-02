---
name: stone_vendas-mcp
description: Skill da REST API do Stone Vendas na MCP.AI: 9 endpoints em /api/stone-vendas. Vendas do adquirente Stone (maquininha) pela API de Conciliação, somente leitura. Lista as transações por período com data e hora, valor bruto e líquido, forma de pagamento, bandeira, tipo de captura, parcelas e status, e consolida os totais por forma de pagamento, bandeira ou dia. Também traz cancelamentos, chargebacks, agenda de recebíveis e as liquidações depositadas na conta. Cobre também o Pix na maquininha, que a Stone entrega num arquivo separado por CNPJ. Cada StoneCode é uma conexão, e a mesma chave vale para todos os StoneCodes do CNPJ. Autenticação pela chave que o titular cria no Portal Stone, em Chaves de Autenticação. Complementa o Stone Pagamentos, que lê a conta bancária pelo Open Finance. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Stone Vendas — REST API skill

Você tem acesso à **Stone Vendas** REST API na MCP.AI.

> Vendas do adquirente Stone (maquininha) pela API de Conciliação, somente leitura. Lista as transações por período com data e hora, valor bruto e líquido, forma de pagamento, bandeira, tipo de captura, parcelas e status, e consolida os totais por forma de pagamento, bandeira ou dia. Também traz cancelamentos, chargebacks, agenda de recebíveis e as liquidações depositadas na conta. Cobre também o Pix na maquininha, que a Stone entrega num arquivo separado por CNPJ. Cada StoneCode é uma conexão, e a mesma chave vale para todos os StoneCodes do CNPJ. Autenticação pela chave que o titular cria no Portal Stone, em Chaves de Autenticação. Complementa o Stone Pagamentos, que lê a conta bancária pelo Open Finance.

## Base URL

```
https://api.mcp.ai/api/stone-vendas
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/stone-vendas/arquivo \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"data":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/stone-vendas/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (9)

#### `stone_vendas_arquivo`

Arquivo de conciliação completo de um único dia, já convertido de XML para JSON, com todos os blocos (vendas, liquidações na conta, agenda prevista, eventos financeiros, pagamentos e posição de cartei _(POST /api/stone-vendas/arquivo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data` | string | Sim | Dia do arquivo no formato AAAA-MM-DD. |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_cancelamentos`

Cancelamentos, chargebacks e reapresentações de chargeback da conta Stone no período, com o NSU da venda de origem, valor, datas e motivo. _(POST /api/stone-vendas/cancelamentos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_contas`

Lista os StoneCodes (estabelecimentos) Stone conectados neste install, com id e apelido. _(POST /api/stone-vendas/contas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_limpar_cache`

Força a Stone a regerar o arquivo de conciliação do período, descartando o extrato que ela mantém em cache. _(POST /api/stone-vendas/limpar/cache)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_liquidacoes`

Liquidações da Stone no período, o que foi efetivamente depositado, com valor total e a conta bancária favorecida. _(POST /api/stone-vendas/liquidacoes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_listar`

Lista as vendas do adquirente Stone no período, uma linha por transação capturada, com data e hora, valor bruto e líquido, forma de pagamento (crédito, débito, pré-pago, voucher, boleto), bandeira, ca _(POST /api/stone-vendas/listar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `forma_pagamento` | string | Não | Filtra por forma de pagamento. (credito, debito, pre_pago_debito, pre_pago_credito, voucher, boleto) |
| `bandeira` | string | Não | Filtra por bandeira, por exemplo Visa, MasterCard, Elo, Amex, Hipercard, Cabal. |
| `status` | string | Não | Filtra pelo status da venda no período. (aprovada, cancelada, contestada, liquidada, registrada) |
| `limite` | integer | Não | Máximo de vendas retornadas (padrão 200). O campo total traz a contagem completa. |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_pix`

Vendas por Pix na maquininha Stone no período, com data e hora, valor, taxa, status (paga ou cancelada), terminal, chave Pix, e2e id e dados do pagador. _(POST /api/stone-vendas/pix)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 7 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `apenas_maquininha` | boolean | Não | Padrão true, só o Pix capturado na maquininha. Use false para ver também o Pix por QR code e cobrança online do mesmo CNPJ. |
| `status` | string | Não | Filtra pelo status da transação Pix. (paid, canceled) |
| `limite` | integer | Não | Máximo de transações retornadas (padrão 200). |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_recebiveis`

Agenda de recebíveis Stone: as parcelas ainda não pagas com a data prevista de pagamento, detalhadas e totalizadas por data. _(POST /api/stone-vendas/recebiveis)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

#### `stone_vendas_resumo`

Totais consolidados das vendas Stone no período, o equivalente ao Resumo de vendas do painel. _(POST /api/stone-vendas/resumo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data_inicio` | string | Não | Data inicial no formato AAAA-MM-DD (padrão: 30 dias atrás). |
| `data_fim` | string | Não | Data final no formato AAAA-MM-DD (padrão: ontem). |
| `agrupar_por` | string | Não | Critério de agrupamento (padrão: forma_pagamento). (forma_pagamento, bandeira, dia, status, captura, terminal) |
| `incluir_pix` | boolean | Não | Padrão true, soma também o Pix na maquininha (que a Stone entrega num arquivo separado). O campo pix da resposta diz se entrou e, se não entrou, por quê. |
| `account` | string | Não | Quando há mais de um StoneCode conectado: id, apelido ou StoneCode da conexão. Veja stone_vendas_contas. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_stone_vendas` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
