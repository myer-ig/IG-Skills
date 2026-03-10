---
name: account
description: View account balances, check available margin, review activity history, and get transaction records from the IG Platform. Use this skill when the user wants to check their balance, see account details, or review trading history.
metadata:
  version: "1.0.0"
  author: IG-Aus
license: MIT
---

# Account Management

View account information and trading history on the IG Trading Platform.

## Capabilities

- List trading accounts
- View balances and margin
- Review activity history
- Get transaction records
- Check account preferences

## Examples

```
"What's my account balance?"
"Show my available margin"
"List my trading accounts"
"Show my recent activity"
"Get my transaction history for last week"
```

## Tools

| Tool | Endpoint | Description |
|------|----------|-------------|
| `get_accounts` | GET `/accounts` | List all accounts |
| `get_account_preferences` | GET `/accounts/preferences` | Account settings |
| `get_activity` | GET `/history/activity` | Activity history |
| `get_transactions` | GET `/history/transactions` | Transaction records |

## Parameters

### Activity History

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `from` | string | No | Start datetime |
| `to` | string | No | End datetime |
| `detailed` | boolean | No | Include details |
| `pageSize` | number | No | Results per page |

### Transaction History

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | No | Transaction type |
| `from` | string | No | Start datetime |
| `to` | string | No | End datetime |
| `pageSize` | number | No | Results per page |
| `pageNumber` | number | No | Page number |

### Transaction Types

| Value | Description |
|-------|-------------|
| `ALL` | All transactions |
| `ALL_DEAL` | All deals |
| `DEPOSIT` | Deposits |
| `WITHDRAWAL` | Withdrawals |

## Response Fields

### Account

| Field | Description |
|-------|-------------|
| `accountId` | Account identifier |
| `accountName` | Display name |
| `accountType` | CFD or SPREADBET |
| `balance` | Current balance |
| `deposit` | Funds on deposit |
| `profitLoss` | Unrealized P&L |
| `available` | Available to trade |

### Activity

| Field | Description |
|-------|-------------|
| `date` | Activity timestamp |
| `dealId` | Deal reference |
| `epic` | Market identifier |
| `period` | Expiry period |
| `channel` | Source channel |
| `type` | Activity type |
| `status` | Outcome status |
