# Microsoft Copilot certification package

This directory is Arkham's package for Microsoft's MCP server certification, which lists the connector in Copilot Studio and Microsoft 365 Copilot. Microsoft's process is in [MCP certification](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-certification). The offer type in Partner Center is "Apps and Agents for M365 and Copilot".

| File | Purpose |
| --- | --- |
| `manifest.json` | App manifest (schema v1.30): listing name, descriptions, links, icons, and the connector to `https://mcp.arkm.com/mcp/core` |
| `mcptools.json` | The 44 read-only tools of the core catalog, as the server lists them |
| `intro.md` | What the connector answers, setup, authentication, sample prompts with expected answers, and known limitations |
| `color.png` | 192×192 full-color icon |
| `outline.png` | 32×32 white-on-transparent icon |

`mcptools.json` copies the server's tool definitions. Regenerate it whenever the core catalog changes, because Microsoft re-certifies on tool changes.

## Order of steps

1. A Partner Center account for Arkham Intelligence, with business verification complete and the Microsoft 365 and Copilot program joined. The intake form asks for the Partner Center ID.
2. The [intake form](https://forms.cloud.microsoft/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR9r8NB1yEjBHvyRFUGv3hYVUQUc3WkpTSDNYSzFTRTNXRThBMUtFWkwyMi4u&route=shorturl). Microsoft takes a limited number of preview submissions and replies to the ones it accepts.
3. Credentials, in an Azure Key Vault, for Microsoft's service to sign users in. Microsoft does not send PKCE, so Arkham registers a confidential OAuth client for it; the redirect URI comes from Microsoft.
4. Zip this directory with the manifest at the archive root, leaving out this README, and submit it in the Partner Center offer with the reviewer account's credentials:

   ```sh
   cd microsoft && zip -r ../arkham-copilot.zip . -x README.md -x '.*'
   ```

## Key Vault

`manifest.json` names the vault `https://arkham-copilot.vault.azure.net/`. Vault names are global, so change `referenceId` if that name is taken. The vault holds these secrets, with names exactly as written:

| Secret | Value |
| --- | --- |
| `ClientId` | The confidential client Arkham registers for Microsoft |
| `ClientSecret` | That client's secret |
| `AuthorizationUrl` | `https://arkm.com/oauth/authorize` |
| `TokenUrl` | `https://api.arkm.com/oauth/token` |
| `RefreshUrl` | `https://api.arkm.com/oauth/token` |

Grant Microsoft's service principal `8e91e74f-afe9-41cd-8c3f-17a9562a74ea` the "Key Vault Secrets User" role on the vault.
