# IG Skills

Skills for AI agents to interact with the IG Trading Platform API.

## What This Is

A collection of structured prompts that teach AI agents how to trade. Each skill maps natural language to IG REST API endpoints.

```
User: "Buy 1 share of Tesla"
  ↓
Agent reads spot skill
  ↓
POST /positions/otc {epic: "TSLA.US", direction: "BUY", size: 1}
  ↓
"Bought 1 Tesla share at $248.50"
```

## Skills

| Skill | Description |
|-------|-------------|
| [spot](skills/ig/spot/) | Execute trades, manage positions, working orders |
| [market-data](skills/ig/market-data/) | Search markets, prices, sentiment, historical data |
| [account](skills/ig/account/) | Balances, margin, activity and transaction history |
| [watchlist](skills/ig/watchlist/) | Create and manage watchlists |

## Structure

```
skills/ig/
├── spot/
│   ├── SKILL.md
│   └── LICENSE.md
├── market-data/
├── account/
└── watchlist/
```

Each `SKILL.md` contains:
- YAML frontmatter (name, description, version)
- Available tools and endpoints
- Parameters and types
- Usage examples

## Quick Example

An agent with the `market-data` skill can handle:

```
"What's the price of Gold?"     → GET /markets?searchTerm=Gold
"Show me EUR/USD details"       → GET /markets/CS.D.EURUSD.CFD.IP
"Get daily candles for Bitcoin" → GET /prices/{epic}/DAY
"What's sentiment on the S&P?"  → GET /clientsentiment/{marketId}
```

## Integration

See [AGENTS.md](AGENTS.md) for:
- Authentication flow
- Framework examples (MCP, LangChain, CrewAI)
- Safety requirements
- Rate limits and error handling

## Requirements

- IG Trading account ([Demo](https://www.ig.com/au/demo-account) or Live)
- API key from [IG Labs](https://labs.ig.com/)

## Contributing

1. Fork and branch: `git checkout -b feature/<skill-name>`
2. Add `SKILL.md` and `LICENSE.md` to a new folder
3. Follow existing skill format
4. Open a PR

## Disclaimer

Informational tool only. Not financial advice. Trading CFDs involves risk. You're responsible for your own decisions. Full terms at [IG.com](https://www.ig.com).

## License

MIT
