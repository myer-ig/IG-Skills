---
name: market-data
description: Search markets, get real-time prices, view historical data, and check trader sentiment on the IG Platform. Use this skill when the user wants to research instruments, check prices, analyze charts, or see market sentiment.
metadata:
  version: "1.0.0"
  author: IG-Aus
license: MIT
---

# Market Data

Research markets and get pricing data from the IG Trading Platform.

## Capabilities

- Search markets by name or symbol
- Get real-time bid/ask prices
- View market specifications
- Retrieve historical OHLC data
- Check trader sentiment

## Examples

```
"What's the price of Tesla?"
"Search for Bitcoin markets"
"Show me EUR/USD details"
"Get daily candles for Gold last month"
"What's the sentiment on S&P 500?"
```

## Tools

| Tool | Endpoint | Description |
|------|----------|-------------|
| `search_markets` | GET `/markets?searchTerm={term}` | Search markets |
| `get_market` | GET `/markets/{epic}` | Market details |
| `get_prices` | GET `/prices/{epic}` | Current prices |
| `get_price_history` | GET `/prices/{epic}/{resolution}/{start}/{end}` | Historical data |
| `get_sentiment` | GET `/clientsentiment/{marketId}` | Trader positioning |

## Parameters

### Search Markets

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `searchTerm` | string | Yes | Search query |

### Price History

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `epic` | string | Yes | Market identifier |
| `resolution` | string | Yes | Candle period |
| `startDate` | string | No | Start datetime |
| `endDate` | string | No | End datetime |
| `max` | number | No | Max data points |

### Resolution Values

| Value | Period |
|-------|--------|
| `SECOND` | 1 second |
| `MINUTE` | 1 minute |
| `MINUTE_5` | 5 minutes |
| `MINUTE_15` | 15 minutes |
| `MINUTE_30` | 30 minutes |
| `HOUR` | 1 hour |
| `HOUR_4` | 4 hours |
| `DAY` | 1 day |
| `WEEK` | 1 week |
| `MONTH` | 1 month |

## Common EPICs

**Forex**
- `CS.D.EURUSD.CFD.IP` - EUR/USD
- `CS.D.GBPUSD.CFD.IP` - GBP/USD
- `CS.D.USDJPY.CFD.IP` - USD/JPY
- `CS.D.AUDUSD.CFD.IP` - AUD/USD

**Indices**
- `IX.D.SPTRD.IFE.IP` - S&P 500
- `IX.D.DOW.IFE.IP` - Dow Jones
- `IX.D.NASDAQ.IFE.IP` - NASDAQ 100
- `IX.D.ASX.IFM.IP` - ASX 200

**Commodities**
- `CS.D.USCGC.TODAY.IP` - Gold
- `CS.D.USCSI.TODAY.IP` - Silver
- `CC.D.CL.UNC.IP` - Crude Oil

**Crypto**
- `CS.D.BITCOIN.CFD.IP` - Bitcoin
- `CS.D.ETHUSD.CFD.IP` - Ethereum

## Rate Limits

- Historical data: Weekly datapoint limit applies
- Search: 30 requests per minute
- Prices: Real-time with streaming available
