# EyeQuant for Claude

Discover quantitative trend signals from EyeQuant AI across stocks, ETFs, crypto, and forex. Explore current and historical signals, track the assets you care about, and manage your watchlists. EyeQuant models are validated using out-of-sample data. For informational and research purposes only; not investment advice or a recommendation to buy, sell, or hold any financial asset.

This plugin connects Claude to EyeQuant's remote MCP server at `https://www.eyequant.ai/mcp`. It includes a skill for interpreting signals, reviewing history, checking account access, and managing watchlists. The plugin contains no local server or credentials.

## Install from GitHub

After the repository has been transferred to `Quantsoft1`, run:

```sh
claude plugin marketplace add Quantsoft1/eyequant-plugin-claude
claude plugin install eyequant@EyeQuant
```

In Claude Code, open `/mcp` and complete EyeQuant's OAuth sign-in when prompted. The connection requests `eyequant:read` and `eyequant:watchlist.write`. Watchlist changes also depend on your EyeQuant plan and require an explicit request. The remote server must support Claude Code's local OAuth callback for sign-in to complete.

The skill is available as `/eyequant:eyequant`. Claude can also use it when a request is relevant.

Example requests:

- "Show me the current signal for NVDA."
- "How many open signals are available in my account?"
- "Review SPY's signal history for September."
- "Add AAPL to my main watchlist."

## Test locally

From the root of this plugin repository, run:

```sh
claude plugin validate . --strict
claude --plugin-dir .
```

While working in the EyeQuant application repository, use `./plugins/eyequant` as the plugin path. Claude discovers the current tool schemas from the connected MCP server; those schemas take precedence over examples in the skill.
