---
name: spot
description: Execute CFD and spread betting trades on the IG Platform. Open and close positions, place working orders, manage stop-losses and take-profits. Use this skill when the user wants to buy, sell, trade, or manage positions.
metadata:
  version: "1.0.0"
  author: IG-Aus
license: MIT
---

# Spot Trading

Execute trades and manage positions on the IG Trading Platform.

## Capabilities

- Open positions (market orders)
- Close positions (full or partial)
- Place working orders (limit/stop)
- Modify stop-loss and take-profit
- View open positions and orders

## Examples

```
"Buy 1 share of Apple"
"Sell 0.5 lots of EUR/USD"
"Close my Tesla position"
"Set limit order to buy Gold at $2000"
"Add stop loss at $150 to my Apple position"
"What are my open positions?"
```

## Tools

| Tool | Endpoint | Description |
|------|----------|-------------|
| `get_positions` | GET `/positions` | List open positions |
| `open_position` | POST `/positions/otc` | Open new position |
| `close_position` | DELETE `/positions/otc/{dealId}` | Close position |
| `update_position` | PUT `/positions/otc/{dealId}` | Modify stop/limit |
| `get_orders` | GET `/workingorders` | List working orders |
| `create_order` | POST `/workingorders/otc` | Create working order |
| `update_order` | PUT `/workingorders/otc/{dealId}` | Modify order |
| `delete_order` | DELETE `/workingorders/otc/{dealId}` | Cancel order |
| `confirm_trade` | GET `/confirms/{dealReference}` | Verify execution |

## Parameters

### Open Position

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `epic` | string | Yes | Market identifier |
| `direction` | string | Yes | `BUY` or `SELL` |
| `size` | number | Yes | Position size |
| `orderType` | string | No | `MARKET` or `LIMIT` |
| `stopLevel` | number | No | Stop loss price |
| `limitLevel` | number | No | Take profit price |
| `guaranteedStop` | boolean | No | Guaranteed stop |

### Working Order

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `epic` | string | Yes | Market identifier |
| `direction` | string | Yes | `BUY` or `SELL` |
| `size` | number | Yes | Order size |
| `level` | number | Yes | Trigger price |
| `type` | string | Yes | `LIMIT` or `STOP` |
| `goodTillDate` | string | No | Expiry datetime |

## Safety

- Always confirm trades before execution
- Use DEMO environment for testing
- Set stop-losses on every position
- Check available margin before trading
- Verify market hours before placing orders
