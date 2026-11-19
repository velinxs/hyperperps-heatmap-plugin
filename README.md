# HyperPerps Liquidation Heatmap — MCP plugin

Free, live liquidation heatmap for Hyperliquid perps, as a remote MCP server. Ask your AI where BTC, ETH, SOL or HYPE traders get liquidated, where their stop-losses and take-profits rest, and how the crowd is positioned. No API key, no account.

- **Server:** `https://hyperperps.app/mcp` (Streamable HTTP, read-only)
- **Tool:** `get_liquidation_heatmap`
- **Markets:** BTC, ETH, SOL, HYPE
- **Live chart:** [hyperperps.app/hyperliquid-liquidation-heatmap](https://hyperperps.app/hyperliquid-liquidation-heatmap)

## What you get

Each call returns a snapshot built from every Hyperliquid leaderboard account plus every account seen trading the coin. Positions are recomputed about every 2 minutes and republished about every 15 seconds with the latest price.

- **Liquidation clusters** — where longs (below price) and shorts (above price) get force-closed, with notional, wallet count and distance from price.
- **Stop-loss pools and take-profit walls** — resting orders that act as fuel and as caps.
- **Crowd positioning** — net open-interest lean, whales vs retail, trapped size, leverage, fresh money, cascade mass.

Data is anonymized: clusters only, never per-wallet rows.

## Install

**Claude Code**

```
/plugin marketplace add velinxs/hyperperps-heatmap-plugin
/plugin install hyperperps-liquidation-heatmap@hyperperps
```

Or add only the MCP server:

```
claude mcp add --transport http hyperperps https://hyperperps.app/mcp
```

**Claude.ai / Claude Desktop:** Settings → Connectors → Add custom connector → `https://hyperperps.app/mcp`.

**Cursor, Windsurf, VS Code and other MCP clients:**

```json
{
  "mcpServers": {
    "hyperperps": { "url": "https://hyperperps.app/mcp" }
  }
}
```

## Tool

`get_liquidation_heatmap`

| Argument | Required | Meaning |
|---|---|---|
| `symbol` | yes | Market, e.g. `BTC`, `ETH`, `SOL`, `HYPE` |
| `range` | no | Percent from price to include, e.g. `25`, or `all` |
| `levels` | no | Walls per side, biggest first, e.g. `50`, or `all` |

Default: walls within 5% of price, the biggest per side.

`get_heatmap_field_definitions` (no arguments) returns what every field means.

Example prompts:

- "Where are the biggest BTC liquidation clusters right now?"
- "Show ETH stop-loss pools within 10% of price."
- "Is the HYPE crowd long or short, and how much of it is underwater?"
- "Give me SOL's full liquidation ladder."

## HTTP API

The same data without MCP:

```
curl https://hyperperps.app/api/public/heatmap/BTC
```

Field definitions: `https://hyperperps.app/api/public/heatmap`, or the `get_heatmap_field_definitions` tool.

## Always current

This plugin is a thin pointer to the hosted server. Tool list, field definitions and usage notes all come from `https://hyperperps.app/mcp` when you connect, so new fields and markets reach you without updating the plugin.

## Support

- Issues: [GitHub issues](https://github.com/velinxs/hyperperps-heatmap-plugin/issues)
- Discord: https://discord.gg/KWKK6Nfpy8
- Privacy: https://hyperperps.app/privacy · Terms: https://hyperperps.app/terms

Anonymized market data. Not financial advice.

## License

MIT
