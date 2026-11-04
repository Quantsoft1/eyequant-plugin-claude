# EyeQuant for Claude

Discover quantitative trend signals from EyeQuant AI across stocks, ETFs, crypto, and forex. Explore current and historical signals, track the assets you care about, and manage your watchlists. EyeQuant models are validated using out-of-sample data. For informational and research purposes only; not investment advice or a recommendation to buy, sell, or hold any financial asset.

This plugin connects Claude to EyeQuant's remote MCP server at `https://www.eyequant.ai/mcp`. It includes a skill for interpreting signals, reviewing history, checking account access, and managing watchlists. The plugin contains no local server or credentials.

## Install from GitHub

While the repository is hosted under `cristaros`, run:

```sh
claude plugin marketplace add cristaros/eyequant-plugin-claude
claude plugin install eyequant@EyeQuant
```

After the repository is transferred to `Quantsoft1`, replace `cristaros` with `Quantsoft1` in the marketplace command and update the `repository` field in `.claude-plugin/plugin.json`.

In Claude Code, open `/mcp` and complete EyeQuant's OAuth sign-in when prompted. The connection requests `eyequant:read` and `eyequant:watchlist.write`. Watchlist changes also depend on your EyeQuant plan and require an explicit request. The remote server must support Claude Code's local OAuth callback for sign-in to complete.

The skill is available as `/eyequant:eyequant`. Claude can also use it when a request is relevant.

For support and contact details, visit [EyeQuant support](https://www.eyequant.ai/landing). See the [privacy policy](https://www.eyequant.ai/privacy) for information about the data used by EyeQuant and its MCP integrations.

Example requests:

- "Show me the current signal for NVDA."
- "How many open signals are available in my account?"
- "Review SPY's signal history for September."
- "Add AAPL to my main watchlist."

## Data and permissions

Claude sends the tool name and the parameters needed for your request to EyeQuant's declared MCP endpoint. Depending on the request, these parameters include tickers, filters, date ranges, watchlist identifiers or names, and requested watchlist changes. Responses can include your account profile and plan, watchlist contents, signals, historical data, and signal cards. Results may be shown in the conversation and handled under the client's own data policies.

The plugin uses OAuth for the connection. Never paste passwords, verification codes, or tokens into the conversation. The plugin has no local executable, package installer, telemetry script, or additional MCP destination. It does not need your full conversation history or unrelated files. EyeQuant's server-side handling and retention are described in its [privacy policy](https://www.eyequant.ai/privacy); service access is subject to its [terms](https://www.eyequant.ai/terms).

## Troubleshooting

- If the connection is unavailable, open `/mcp`, inspect the EyeQuant connection, and complete or renew its OAuth authorization.
- If a read or write is denied, check the granted permissions and your EyeQuant plan. Do not try to bypass an access restriction.
- If a watchlist change times out, check the watchlist before repeating the change.
- If signal cards are unavailable in your client, ask for the textual signal data.
- For unresolved issues, use the contact information on the [support page](https://www.eyequant.ai/landing). Do not include credentials in a support report.

## License

This plugin is proprietary software owned by Quantum Software Systems SpA (Quantsoft). The [LICENSE](LICENSE) permits each individual user to download and use the unmodified plugin with their own EyeQuant account and the data available under their plan, and permits authorized distribution through Claude. Modification and other redistribution require permission except where the license or applicable law permits them. The license does not grant an EyeQuant account, access beyond the user's plan, or rights to the server, models, or market data.

## Test locally

From the root of this plugin repository, run:

```sh
claude plugin validate . --strict
claude plugin validate . --profile directory
claude --plugin-dir .
```

Claude discovers the current tool schemas from the connected MCP server; those schemas take precedence over examples in the skill.
