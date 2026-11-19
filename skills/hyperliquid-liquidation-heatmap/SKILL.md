---
name: hyperliquid-liquidation-heatmap
description: Read the free HyperPerps Hyperliquid liquidation heatmap — liquidation clusters, stop-loss pools, take-profit walls and crowd positioning. Use when the user asks where Hyperliquid traders get liquidated, where stops or take-profits rest, how the crowd is positioned, or wants liquidation levels for a Hyperliquid perp.
---

# Hyperliquid liquidation heatmap

Live, anonymized map of Hyperliquid perps: where positions get force-closed, where stop-losses and take-profits rest, and how the crowd leans. Free, no API key. Explains the data; it does not prescribe a strategy.

## How to use

1. Call `get_liquidation_heatmap` with the market's `symbol`. The server lists the supported markets in its instructions and in the tool's input description.
2. Check `_meta.stale` and `_meta.age_seconds` before treating the snapshot as current.
3. For a field you don't know, call `get_heatmap_field_definitions`. It is always current; prefer it over memory.

The default view holds the walls nearest price. Pass `range` and/or `levels` for the full ladder.

## Reading it

- `liquidations`, `stop_losses` and `take_profits` each split into `longs` and `shorts` levels with price, notional, wallet count and signed distance from price.
- Positioning fields describe Hyperliquid's crowd only. Price levels are the stronger layer: other venues pile stops and liquidations at the same prices, so read each wall as a lower bound.
- Cite the snapshot time when you report levels; prices move.

Live chart: https://hyperperps.app/hyperliquid-liquidation-heatmap

*Anonymized cluster data. Not financial advice.*
