# Stone Vendas

### Stone Vendas para Claude, ChatGPT e agentes de IA

Vendas do adquirente Stone (maquininha) pela API de Conciliação, somente leitura. Lista as transações por período com data e hora, valor bruto e líquido, forma de pagamento, bandeira, tipo de captura, parcelas e status, e consolida os totais por forma de pagamento, bandeira ou dia. Também traz cancelamentos, chargebacks, agenda de recebíveis e as liquidações depositadas na conta. Cobre também o Pix na maquininha, que a Stone entrega num arquivo separado por CNPJ. Cada StoneCode é uma conexão, e a mesma chave vale para todos os StoneCodes do CNPJ. Autenticação pela chave que o titular cria no Portal Stone, em Chaves de Autenticação. Complementa o Stone Pagamentos, que lê a conta bancária pelo Open Finance.

- 📊 **9 ferramentas**
- 🔒 **Somente leitura**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Stone Vendas` e **URL** `https://api.mcp.ai/p_stone_vendas`.

### Cursor

[➕ Instalar Stone Vendas no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=stone_vendas&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zdG9uZV92ZW5kYXMifQ==)

### VS Code (Copilot Chat)

[➕ Instalar Stone Vendas no VS Code](vscode:mcp/install?name=stone_vendas&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_stone_vendas%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_stone_vendas
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Qual foi o resumo de vendas da Stone no mês passado por forma de pagamento?
Liste as vendas Stone da semana passada por bandeira
Quanto tenho para receber da Stone nos próximos dias?
Teve algum chargeback ou cancelamento na Stone neste mês?
Quanto entrou de Pix na maquininha Stone na semana passada?
```

---

## 9 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `stone_vendas_contas` | Lista os StoneCodes (estabelecimentos) Stone conectados neste install, com id e apelido. |
| `stone_vendas_listar` | Lista as vendas do adquirente Stone no período, uma linha por transação capturada, com data e hora, valor bruto e líquido, forma de pagamento (crédito, débito, pré-pago, voucher, boleto), bandeira, cartão truncado, ti… |
| `stone_vendas_resumo` | Totais consolidados das vendas Stone no período, o equivalente ao Resumo de vendas do painel. |
| `stone_vendas_cancelamentos` | Cancelamentos, chargebacks e reapresentações de chargeback da conta Stone no período, com o NSU da venda de origem, valor, datas e motivo. |
| `stone_vendas_recebiveis` | Agenda de recebíveis Stone: as parcelas ainda não pagas com a data prevista de pagamento, detalhadas e totalizadas por data. |
| `stone_vendas_liquidacoes` | Liquidações da Stone no período, o que foi efetivamente depositado, com valor total e a conta bancária favorecida. |
| `stone_vendas_pix` | Vendas por Pix na maquininha Stone no período, com data e hora, valor, taxa, status (paga ou cancelada), terminal, chave Pix, e2e id e dados do pagador. |
| `stone_vendas_limpar_cache` | Força a Stone a regerar o arquivo de conciliação do período, descartando o extrato que ela mantém em cache. |
| `stone_vendas_arquivo` | Arquivo de conciliação completo de um único dia, já convertido de XML para JSON, com todos os blocos (vendas, liquidações na conta, agenda prevista, eventos financeiros, pagamentos e posição de carteira). |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Somente leitura**, nenhuma ferramenta altera dados na origem.
- **Sub-processadores**: Stone, o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_stone_vendas`.


---

## Suporte

- 📧 [stone_vendas@mcp.ai](mailto:stone_vendas@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/stone_vendas-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_stone_vendas` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
