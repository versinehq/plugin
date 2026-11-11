# Versine

Pay friends back, split costs and ask people for money from a conversation
with Claude, through your own [Versine](https://versine.com) account.

## Use it

1. Add the plugin, then connect the Versine connector from the plugin's
   **Connectors** tab and sign in to Versine.
2. Ask Claude things like "Pay Maya back $12 for lunch", "Split dinner with
   Sam and Alex" or "Ask Jordan for $40 for the tickets".

Claude finds the person in your Versine contacts and drafts the payment or
request. Each payment waits for you to approve it in the Versine app.
Claude can't approve payments, add money, withdraw to a bank or change what
it's allowed to do.

## Components

| Component | Path | What it does |
| --- | --- | --- |
| Connector | `.mcp.json` | Connects to Versine at `https://mcp.versine.com` |
| Skill | `skills/versine/` | When to use Versine, and how to find people, pay, request and report each result |

## Data

The plugin sends the names, numbers, amounts and notes you give Claude to
your Versine account through mcp.versine.com, over the connector you sign
in to. The plugin itself stores nothing. Everything Claude does shows up in
the Versine app, where you can remove its access at any time.

You need a Versine account. Get the app at [versine.com](https://versine.com).

- Privacy: https://versine.com/legal/privacy
- Terms: https://versine.com/legal/terms
- Support: https://versine.com/support

## License

MIT
