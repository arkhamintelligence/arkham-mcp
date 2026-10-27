<p align="center"><img src="assets/arkham-icon-dark-512.png" width="96" alt="Arkham"></p>

# Arkham MCP server

Arkham's official MCP server connects Claude, ChatGPT, Cursor, VS Code, Gemini CLI and other MCP clients to [Arkham](https://arkm.com)'s blockchain intelligence. Arkham hosts it at **`https://mcp.arkm.com/mcp`**, so there is nothing to install or run. This repository holds only the manifests that MCP directories and client plugin galleries read; the server itself isn't open source.

Ask who is behind any wallet, how money moved, and what an entity holds. Arkham attributes on-chain activity to real-world entities (exchanges, funds, market makers, individuals) across 16 chains, including Ethereum, Bitcoin, Solana, Tron and Base. The server's 142 tools cover:

| Area | Tools |
| --- | --- |
| Polymarket: markets, positions, wallets, leaderboards | 22 |
| Tokens: prices, holders, flows, trending | 21 |
| Addresses: intelligence, balances, flows, history | 19 |
| HyperCore (Hyperliquid): positions, balances, trades | 16 |
| Entities: intelligence, balances, flows, history | 15 |
| Alerts, labels and private entities (your own) | 15 |
| Live transfer streams (WebSocket setup) | 11 |
| Transfers, transactions, swaps and networks | 9 |
| Intelligence update feeds and tags | 6 |
| Risk scores for addresses and entities | 5 |
| Account usage and billing | 3 |

## Connect

You sign in with your Arkham account: the client opens Arkham, you create a key for it (or pick the one you made last time), and the client keeps it working. The full setup guide, including troubleshooting, is the [MCP Server guide](https://arkm.com/api/docs).

| Client | How |
| --- | --- |
| **Claude** (desktop, web, mobile) | **Customize → Connectors → Add custom connector**, URL `https://mcp.arkm.com/mcp`. Under **Advanced settings**, set the OAuth Client ID to `claude`. |
| **Claude Code** | `/plugin marketplace add arkhamintelligence/arkham-mcp`, then `/plugin install arkham@arkham`. Or: `claude mcp add --transport http arkham https://mcp.arkm.com/mcp --client-id claude-code --callback-port 8765 --scope user` |
| **Cursor** | [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=arkham&config=eyJ1cmwiOiJodHRwczovL21jcC5hcmttLmNvbS9tY3AiLCJhdXRoIjp7IkNMSUVOVF9JRCI6ImN1cnNvciJ9fQ==), or add the `arkham` entry from [`mcp.json`](mcp.json) to `~/.cursor/mcp.json`. |
| **Codex** | `codex mcp add arkham --url https://mcp.arkm.com/mcp`, then `codex mcp login arkham` |
| **Gemini CLI** | `gemini extensions install https://github.com/arkhamintelligence/arkham-mcp` |
| **Kiro** | **Powers → Add Custom Power → Import power from GitHub**, `https://github.com/arkhamintelligence/arkham-mcp/tree/main/kiro` |
| **VS Code, ChatGPT and others** | Add a remote MCP server with the URL `https://mcp.arkm.com/mcp`. The client registers itself, so Arkham's sign-in page shows its name as an unverified app. |

### Use an API key instead of signing in

Any client that can send a header can use a key from the [API Dashboard](https://arkm.com/api-dashboard?tab=api-keys):

```
Authorization: Bearer YOUR_API_KEY
```

## Access and credits

Using the server needs an Arkham API plan or trial ([Getting Access](https://arkm.com/api/docs)). Tool calls use the same API credits as the REST API, and each tool's description states its price; most lookups cost 5 credits or fewer. Each answer is capped at 4 MiB, so ask for narrow time ranges or fewer results, and use the [API](https://arkm.com/api/docs) for large exports.

The tools read data, and write only to your own alerts, labels and private entities. None of them move funds or place trades. The server forwards each tool call's arguments and your key to `api.arkm.com` and keeps no conversation content.

## What's in this repository

| Path | For |
| --- | --- |
| [`server.json`](server.json) | Official MCP Registry entry `com.arkm/mcp` |
| [`.claude-plugin/`](.claude-plugin), [`.mcp.json`](.mcp.json) | Claude Code plugin and marketplace |
| [`.cursor-plugin/`](.cursor-plugin), [`mcp.json`](mcp.json) | Cursor plugin |
| [`gemini-extension.json`](gemini-extension.json), [`GEMINI.md`](GEMINI.md) | Gemini CLI extension |
| [`kiro/`](kiro) | Kiro power |
| [`assets/`](assets) | Square icons (dark and light) at 400, 512 and 1024 px, with SVG sources |

Every manifest carries the same `version`; bump them together on a release and tag it.

## Listings

- Official MCP Registry: [`com.arkm/mcp`](https://registry.modelcontextprotocol.io/v0/servers?search=com.arkm)
- Glama: [Arkham connector](https://glama.ai/mcp/connectors/com.arkm/mcp)

## Support

- API and MCP: [api@arkm.com](mailto:api@arkm.com)
- Terms: [API terms of service](https://arkm.com/api-terms-of-service) · [Privacy policy](https://info.arkm.com/privacy-policy)
