# Arkham Intelligence

Arkham attributes blockchain addresses to real-world entities, such as exchanges, funds and market makers, and serves balances, transfers, transactions and market data for them. This connector gives Copilot that intelligence through Arkham's remote MCP server at `https://mcp.arkm.com/mcp/core`.

## Tools

The connector exposes 44 read-only tools, described in `mcptools.json`. None moves funds, places trades or changes the user's account.

| Area | What it answers |
| --- | --- |
| Addresses | Who owns an address, what it holds, its counterparties, flows and portfolio history |
| Entities | An entity's summary, balances, balance changes, counterparties, flows and portfolio history |
| Transfers and transactions | Transfers filtered by address, entity, token, chain, time and value; a transaction by hash; swaps |
| Tokens | Current market data, price history, volume, top holders, top flows and trending tokens |
| Risk | Risk scores for addresses and entities |
| Hyperliquid (HyperCore) | Account and entity summaries, perp positions and trades |
| Polymarket | Events, positions, top holders, wallet PnL and the leaderboard |
| Search and account | Search for entities and addresses, supported chains, and the user's own credit usage |

## Setup

1. Add the Arkham Intelligence connector in Copilot Studio or Microsoft 365 Copilot.
2. Sign in with an Arkham account when prompted. The account needs Arkham API access.
3. Ask a question, such as one of the sample prompts below.

## Authentication

OAuth 2.0 authorization code flow against Arkham's authorization server (`https://api.arkm.com`), with a confidential client. The access token is an Arkham API key scoped to the user's account, and calls draw on that account's API credits.

## Sample prompts

| Prompt | Tool | Expected answer |
| --- | --- | --- |
| Which blockchains does Arkham cover? | `GetSupportedChains` | 16 chains, including Ethereum, Bitcoin, Solana, Tron, Base, and Hyperliquid's HyperEVM and HyperCore |
| Who owns 0x28C6c06298d514Db089934071355E5743bf21d60? | `GetAddressIntelligence` | A Binance hot wallet on Ethereum |
| What tokens does Binance hold on Ethereum? | `GetEntityBalances` | Binance's largest Ethereum holdings with USD values, led by USDT, WBETH and ETH |
| What's the current price and market cap of Ethereum? | `GetTokenCurrentMarketData` | ETH's current price, market cap, 24-hour volume and circulating supply |
| Show me transaction 0x5c504ed432cb51138bcf09aa5e8a410dd4a1e204ef84bfed1be16dfba1b22060. | `GetTransaction` | The Ethereum transaction from block 46147 (7 August 2015), sent from thanateros.eth, with its recipient, value and fee |

## Known issues and limitations

- Results are limited to the chains `GetSupportedChains` lists.
- Arkham attributes addresses to entities. It has no personal contact details for the people behind wallets.
- An entity's balances across every chain can run to hundreds of tokens. Filtering by chain keeps answers small.
- Each call costs Arkham API credits, stated in each tool's description. A user whose credits run out gets an error until they are replenished.
