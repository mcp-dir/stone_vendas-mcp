# Stone Vendas

### Stone Vendas for Claude, ChatGPT and AI agents

Stone acquirer (card machine) sales via the Conciliação API, read-only. Lists transactions for a period with date and time, gross and net amounts, payment method, card brand, capture type, installments and status, and consolidates totals by payment method, brand or day. Also covers cancellations, chargebacks, the receivables schedule and the settlements deposited into the account. Each StoneCode is one connection, and the same key works for every StoneCode under the same tax id. Auth uses the key the account holder creates in the Stone portal, under authentication keys. Complements Stone Pagamentos, which reads the bank account through Open Finance.

- 📊 **9 tools**
- 🔒 **Read-only**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Versão em português](README.pt.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `Stone Vendas` and **URL** `https://api.mcp.ai/p_stone_vendas`.

### Cursor

[➕ Install Stone Vendas in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=stone_vendas&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zdG9uZV92ZW5kYXMifQ==)

### VS Code (Copilot Chat)

[➕ Install Stone Vendas in VS Code](vscode:mcp/install?name=stone_vendas&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_stone_vendas%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_stone_vendas
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
What was the Stone sales summary last month by payment method?
List last week's Stone sales by card brand
How much am I due to receive from Stone in the coming days?
Were there any chargebacks or cancellations on Stone this month?
How much came in through Pix on the Stone card machine last week?
```

---

## 9 tools available

| Tool | Description |
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

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## Privacy & data protection

- **Read-only**, no tool changes data at the source.
- **Sub-processors**: Stone, the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is the server open source?**
The server is proprietary (hosted). This repository is the public wrapper with manifests, docs and skills, all MIT.

**Can I use it with my own agent (not Claude/Cursor)?**
Yes, any client that speaks MCP over HTTP. URL: `https://api.mcp.ai/p_stone_vendas`.


---

## Support

- 📧 [stone_vendas@mcp.ai](mailto:stone_vendas@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/stone_vendas-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_stone_vendas` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
