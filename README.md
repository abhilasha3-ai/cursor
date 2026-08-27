# QAEverest for Cursor

The [QAEverest](https://qaeverest.ai) plugin for Cursor — generate AI-powered
functional, API, UI and mobile test cases, and run security and performance
checks, from inside Cursor's agent.

| | |
|---|---|
| **Plugin** | [`qaeverest/`](qaeverest/) — see its [README](qaeverest/README.md) |
| **Version** | 1.0.0 |
| **License** | MIT |

## Install

**From the Cursor Marketplace** — open **Customize** in the sidebar, search for
**QAEverest**, and click Install. Cursor prompts for your QAEverest API key.

**From this repository**, as a marketplace: Dashboard → Plugins → **Add
Marketplace** → *Import from Repo*, and point it at this repo.

**Locally**, for development:

```bash
git clone https://github.com/abhilasha3-ai/cursor.git
ln -s "$PWD/cursor/qaeverest" ~/.cursor/plugins/local/qaeverest
```

Then run **Developer: Reload Window** in Cursor.

## What it needs

Node.js 18+ (the plugin runs the MCP server via `npx`) and a QAEverest API key
(`qae_…`) — [sign up free](https://app.qaeverest.ai/api-client/signup?source=cursor-plugin),
or take one from **Admin → API Management** in your QAEverest account. Your key
is stored by Cursor and passed to the server at launch; it is never written into
this repository.

## Privacy

[`qaeverest/PRIVACY.md`](qaeverest/PRIVACY.md) — what the server sends to the QAEverest
backend, and how it is handled.
