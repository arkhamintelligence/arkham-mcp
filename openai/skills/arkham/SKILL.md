---
name: arkham
description: Answer questions about blockchain wallets, entities, transfers, tokens, Hyperliquid positions and Polymarket with Arkham's on-chain intelligence. Use when the user asks who owns an address, what an entity or wallet holds, how funds moved, or about a token, transaction or prediction market.
---

# Arkham

Arkham attributes blockchain addresses to real-world entities, such as exchanges, funds and market makers, and serves balances, transfers and market data for them. Most Arkham tools only look things up. A few manage the user's own alerts, labels, private entities and live transfer streams: use those only when the user asks for that change.

## Finding the right tool

- **An address:** `GetAddressIntelligence` says who it belongs to. `GetAddressBalances`, `GetAddressCounterParty` and `GetAddressFlow` say what it holds, who it deals with and how value moved.
- **An entity named in words** ("Binance", "Jump Trading"): resolve it with `IntelligenceSearchHandler` first. Entity tools take Arkham's entity ID (for example `binance`), which is case-sensitive.
- **A transaction hash:** `GetTransaction`. Write the hash as its chain does: `0x`-prefixed hex on EVM chains.
- **A token:** `GetTokenCurrentMarketData` and `GetTokenHistoryFromPricingID` take the CoinGecko pricing ID (for example `ethereum`, `usd-coin`). `GetTopTokenHoldersByChainAddress` takes the chain and the token's contract address.
- **Transfers:** `GetTransfers` filters by address, entity, token, chain, time and value.
- **Hyperliquid:** the `GetHypercore…` tools cover accounts, entities, perp positions and trades.
- **Polymarket:** the `GetPolymarket…` tools cover events, positions, top holders, wallet PnL and the leaderboard.
- **Which chains are covered:** `GetSupportedChains`.

## Keeping calls small

Each call draws on the user's Arkham API credits, and each tool's description states its cost. Filter by chain when the user names one: an entity's balances across every chain can run to hundreds of tokens. Ask for a limit or a time window on transfer and history queries rather than fetching everything.

## Answering

- Say which entity an address belongs to only when Arkham returns an attribution, and name it as Arkham's attribution.
- Give USD values with the time they apply to. Balances are current, and transfer values are as of the transfer.
- Arkham has no personal contact details for the people behind wallets. Decline requests for them, and offer the entity attribution instead.
- The tools cannot move funds or place trades. Say so when asked to buy, sell or send.
- Don't predict prices or give investment advice. Offer historical prices, flows and holdings instead.
