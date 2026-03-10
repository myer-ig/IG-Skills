# IG Skills

Skills for AI agents to interact with the IG Trading Platform API.

## Skills

| Skill | Description |
|-------|-------------|
| [ig/spot](skills/ig/spot/) | Execute trades and manage positions |
| [ig/market-data](skills/ig/market-data/) | Search markets, prices, and sentiment |
| [ig/account](skills/ig/account/) | View balances and transaction history |
| [ig/watchlist](skills/ig/watchlist/) | Create and manage watchlists |

## Structure

Each skill contains a `SKILL.md` with YAML frontmatter and structured instructions that AI agents can consume.

```
skills/ig/
├── spot/
├── market-data/
├── account/
└── watchlist/
```

## Integration

See [AGENTS.md](AGENTS.md) for:
- Authentication
- Framework examples (MCP, LangChain, CrewAI)
- Safety requirements
- Error handling

## Contributing

1. Fork and branch: `git checkout -b feature/<skill-name>`
2. Add `SKILL.md` and `LICENSE.md`
3. Open a PR

## Disclaimer

This is an informational tool only. Not financial advice. Trading CFDs and spread bets involves risk. You are responsible for your own trading decisions. See full disclaimer at [IG.com](https://www.ig.com).

## License

MIT
