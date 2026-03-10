---
name: watchlist
description: Create and manage watchlists on the IG Platform. Add markets to track, organize instruments, and monitor favourites. Use this skill when the user wants to create watchlists, add markets to watch, or manage tracked instruments.
metadata:
  version: "1.0.0"
  author: IG-Aus
license: MIT
---

# Watchlist Management

Create and manage watchlists on the IG Trading Platform.

## Capabilities

- List all watchlists
- Create new watchlists
- Add markets to watchlist
- Remove markets from watchlist
- Delete watchlists

## Examples

```
"Show my watchlists"
"Create a watchlist called Tech Stocks"
"Add Tesla to my watchlist"
"Remove Gold from my watchlist"
"Delete my Forex watchlist"
```

## Tools

| Tool | Endpoint | Description |
|------|----------|-------------|
| `get_watchlists` | GET `/watchlists` | List watchlists |
| `get_watchlist` | GET `/watchlists/{watchlistId}` | Get watchlist markets |
| `create_watchlist` | POST `/watchlists` | Create watchlist |
| `add_to_watchlist` | PUT `/watchlists/{watchlistId}` | Add market |
| `remove_from_watchlist` | DELETE `/watchlists/{watchlistId}/{epic}` | Remove market |
| `delete_watchlist` | DELETE `/watchlists/{watchlistId}` | Delete watchlist |

## Parameters

### Create Watchlist

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Watchlist name |
| `epics` | array | No | Initial markets |

### Add to Watchlist

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `epic` | string | Yes | Market to add |

## Response Fields

### Watchlist

| Field | Description |
|-------|-------------|
| `id` | Watchlist identifier |
| `name` | Display name |
| `editable` | Can be modified |
| `deleteable` | Can be deleted |
| `defaultSystemWatchlist` | System default |

### Watchlist Market

| Field | Description |
|-------|-------------|
| `epic` | Market identifier |
| `instrumentName` | Display name |
| `instrumentType` | Asset class |
| `high` | Day high |
| `low` | Day low |
| `bid` | Current bid |
| `offer` | Current offer |
| `change` | Price change |
| `changePercentage` | Change % |
| `marketStatus` | Trading status |
