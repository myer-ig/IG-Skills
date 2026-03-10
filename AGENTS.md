# Building Agents with IG Skills

This guide explains how to integrate IG Skills into your AI agent.

## How Skills Work

Each skill is a structured prompt that teaches your agent how to interact with the IG REST API. Your agent reads the `SKILL.md` file and gains the knowledge to:

1. Understand user intent
2. Map requests to API endpoints
3. Format parameters correctly
4. Handle responses appropriately

## Quick Start

### 1. Load Skills

Point your agent at the skill files:

```python
# Example: LangChain
from langchain.document_loaders import TextLoader

skills = [
    "skills/ig/spot/SKILL.md",
    "skills/ig/market-data/SKILL.md",
    "skills/ig/account/SKILL.md",
    "skills/ig/watchlist/SKILL.md"
]

for skill in skills:
    loader = TextLoader(skill)
    agent.add_knowledge(loader.load())
```

### 2. Configure API Access

```json
{
  "ig_api": {
    "base_url": "https://demo-api.ig.com/gateway/deal",
    "api_key": "your-api-key",
    "credentials": {
      "identifier": "your-username",
      "password": "your-password"
    }
  }
}
```

### 3. Authenticate

```
POST /session
Headers:
  X-IG-API-KEY: {api_key}
  Content-Type: application/json
  Version: 2

Body:
  {"identifier": "username", "password": "password"}

Response Headers:
  CST: {client_session_token}
  X-SECURITY-TOKEN: {security_token}
```

Store `CST` and `X-SECURITY-TOKEN` for subsequent requests.

## Agent Architecture

```
┌─────────────────────────────────────────────────┐
│                   User Input                     │
│            "Buy 1 share of Apple"               │
└─────────────────────┬───────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────┐
│                  AI Agent                        │
│  ┌───────────────────────────────────────────┐  │
│  │           Skills Knowledge                 │  │
│  │  • spot: positions, orders                │  │
│  │  • market-data: prices, search            │  │
│  │  • account: balances, history             │  │
│  │  • watchlist: manage lists                │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────┬───────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────┐
│              Intent Recognition                  │
│         Skill: spot | Action: open_position     │
└─────────────────────┬───────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────┐
│               IG REST API                        │
│  POST /positions/otc                            │
│  {epic, direction: BUY, size: 1}               │
└─────────────────────┬───────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────┐
│                  Response                        │
│   "Bought 1 Apple share at $187.50"            │
└─────────────────────────────────────────────────┘
```

## Framework Examples

### Claude Desktop (MCP)

```json
{
  "mcpServers": {
    "ig-trading": {
      "command": "node",
      "args": ["ig-mcp-server/index.js"],
      "env": {
        "IG_API_KEY": "your-api-key",
        "IG_USERNAME": "your-username",
        "IG_PASSWORD": "your-password",
        "IG_ENVIRONMENT": "DEMO"
      }
    }
  }
}
```

### LangChain

```python
from langchain.agents import Tool, AgentExecutor

tools = [
    Tool(name="search_markets", func=ig_search, description="Search IG markets"),
    Tool(name="get_positions", func=ig_positions, description="Get open positions"),
    Tool(name="place_order", func=ig_order, description="Place a trade"),
]

agent = AgentExecutor(tools=tools, llm=llm)
```

### CrewAI

```python
from crewai import Agent, Task

trader = Agent(
    role="Trader",
    goal="Execute trades on IG platform",
    backstory="Expert trader with IG API access",
    tools=[ig_search, ig_order, ig_positions]
)
```

## Safety Requirements

### 1. Environment Isolation

```python
# Always default to DEMO
environment = os.getenv("IG_ENVIRONMENT", "DEMO")

if environment == "LIVE":
    require_explicit_confirmation = True
```

### 2. Trade Confirmation

```python
def place_order(params):
    # Always confirm before execution
    confirmation = agent.ask_user(
        f"Confirm: {params['direction']} {params['size']} {params['epic']}?"
    )
    if confirmation != "CONFIRM":
        return "Order cancelled"
```

### 3. Size Limits

```python
MAX_POSITION_SIZE = {
    "DEMO": 100,
    "LIVE": 10
}

def validate_size(size, environment):
    if size > MAX_POSITION_SIZE[environment]:
        raise ValueError(f"Size exceeds limit for {environment}")
```

### 4. Credential Security

```python
# Never log credentials
# Never include in responses
# Use environment variables only

MASKED_FIELDS = ["password", "api_key", "CST", "X-SECURITY-TOKEN"]
```

## Rate Limits

| Request Type | Limit |
|--------------|-------|
| Trading | 1/second |
| Non-trading | 30/minute |
| Historical data | Weekly cap |

```python
from ratelimit import limits

@limits(calls=1, period=1)
def trading_request(endpoint, params):
    ...

@limits(calls=30, period=60)
def data_request(endpoint, params):
    ...
```

## Error Handling

```python
IG_ERRORS = {
    "authentication.failure": "Re-authenticate and retry",
    "position.not-found": "Position may be closed",
    "market.closed": "Check trading hours",
    "insufficient.funds": "Check available margin",
    "rate.limit.exceeded": "Wait and retry"
}

def handle_error(response):
    error_code = response.get("errorCode")
    return IG_ERRORS.get(error_code, "Unknown error")
```

## Testing Your Agent

### 1. Use DEMO Environment

Always test with virtual money first.

### 2. Test Cases

```
✓ "What's the price of Gold?"
✓ "Show my account balance"
✓ "Buy 1 lot of EUR/USD" → Requires confirmation
✓ "Close all positions" → Requires confirmation
✓ "Add Tesla to my watchlist"
```

### 3. Edge Cases

```
✓ Market closed errors
✓ Insufficient margin
✓ Invalid instrument
✓ Rate limit handling
```

## Resources

- [IG REST API Reference](https://labs.ig.com/rest-trading-api-reference)
- [IG Labs](https://labs.ig.com/)
- [Demo Account Signup](https://www.ig.com/au/demo-account)
