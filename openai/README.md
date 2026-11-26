# OpenAI plugin package

This directory is Arkham's submission package for OpenAI's plugin directory, which lists plugins in ChatGPT and Codex. It uses the portable Agent Plugins layout described in OpenAI's [build guide](https://developers.openai.com/plugins/build/plugins) and [submission guide](https://developers.openai.com/apps-sdk/deploy/submission).

| File | Purpose |
| --- | --- |
| `plugin.json` | Listing copy, links, starter prompts, logo, and the review test cases (5 the plugin handles, 3 it declines) |
| `mcp.json` | The server: `https://mcp.arkm.com/mcp/core`, the read-only core catalog, signed in with OAuth through dynamic client registration |
| `skills/arkham/SKILL.md` | Onboarding skill: which tool answers which question, keeping calls small, and what the plugin declines |
| `assets/` | The logo, also used as the composer icon |

## Submitting

The submission must come from an owner of Arkham's OpenAI organization, or a member with Apps Management Write. That organization needs business verification on platform.openai.com first.

1. Check that `review.demo_recording_url` in `plugin.json` still opens the demo video for someone outside Arkham.
2. Zip this directory with `plugin.json` at the root of the archive, leaving out this README:

   ```sh
   cd openai && zip -r ../arkham-openai-plugin.zip . -x README.md -x '.*'
   ```

3. Upload the ZIP at platform.openai.com, under the plugin directory's submission page, and complete the dashboard steps:
   - **With MCP:** connect `https://mcp.arkm.com/mcp/core` and run the tool scan.
   - **Domain verification:** `https://mcp.arkm.com/.well-known/openai-apps-challenge` already serves Arkham's token.
   - **Review details:** the reviewer account's credentials. OpenAI rejects them in the ZIP, and the account must sign in without MFA or emailed codes.
4. Run each positive test case with the reviewer account, then submit for review.
