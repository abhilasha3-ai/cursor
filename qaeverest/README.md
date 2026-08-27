# QAEverest — Cursor Plugin

Generate AI-powered test cases — and run security & performance checks — from inside Cursor's agent. This plugin bundles the [QAEverest MCP server](https://www.npmjs.com/package/qaeverest-mcp) plus skills that tell the agent which tool fits which request.

> Want the **QAEverest chat panel** in Cursor's sidebar — tabs, document attachments, saving `.feature` files — rather than agent-side tools? That's the QAEverest Cursor extension (a VSIX) — see [qaeverest.ai](https://qaeverest.ai). The two work side by side; the extension also registers this same MCP server for you.

## What you get

**MCP tools** — the agent picks these automatically when you describe what you want:

| Tool | What it does |
|---|---|
| `generate_testcases` | Functional/system test cases from a user story — Gherkin, positive/negative/edge |
| `generate_api_tests` | API test cases from a description, OpenAPI/Swagger spec, or Postman collection |
| `generate_ui_tests` | End-to-end UI automation scenarios (navigate/click/type/assert) |
| `generate_mobile_tests` | Mobile automation scenarios (gestures, device states) |
| `security_scan` | Headers, SSL/TLS, and vulnerability checks against a URL |
| `performance_test` | Load/stress/spike/soak metrics against a URL |
| `get_usage` | Credits remaining, requests this month, enabled services |

**Skills** — `generate-tests`, `security-scan`, `performance-test`, `usage`. Each one carries the judgement that turns a tool call into a useful answer: which tool fits the request, what to put in `additional`, where generated scenarios belong in the repo, and when to ask before pointing a scan at a host.

**A rule** — `rules/qaeverest.mdc`, attached when the conversation is about testing: the tool-selection table, the credit cost of each call, and the authorization rule for scan targets.

## Prerequisites

- **Node.js 18+** (the plugin runs the server via `npx`)
- A **QAEverest API key** (`qae_...`) — [sign up free](https://app.qaeverest.ai/api-client/signup?source=cursor-plugin) (100 credits, no card) or get one from **Admin → API Management**.

## Setup

1. Install the plugin — from the Cursor marketplace, or by adding this repository as a plugin marketplace (**Customize → Plugins → Add marketplace**), or for local development by cloning it into `~/.cursor/plugins/local`.
2. Cursor prompts for the plugin's variables on install. Paste your key into **QAEVEREST_API_KEY**. Leave **QAEVEREST_API_URL** alone unless you run a self-hosted or enterprise instance.
3. Ask the agent: *"What's my QAEverest usage?"*

Your key is stored by Cursor and interpolated into the server's environment at launch — it is never written into this repository. (See [`mcp.json`](mcp.json): the values are `${QAEVEREST_API_KEY}` / `${QAEVEREST_API_URL}` placeholders.)

## Example prompts

> *"Generate functional test cases for the login story in `auth/README.md` and save them as a feature file."*
>
> *"Generate API tests from this `openapi.yaml`, then scaffold Playwright specs from them."*
>
> *"Run a full security scan against https://staging.example.com."*
>
> *"Load-test https://staging.example.com/api/search with 50 virtual users for a minute."*

## Billing & scope

Each generation/scan/performance call is billed to your QAEverest account at an admin-configured per-service credit cost. Whether a given tool works depends on which services are **enabled** for your API key — ask the agent for your usage to check. Only scan or load-test hosts you are authorized to test.

## Privacy

See [PRIVACY.md](PRIVACY.md) for what data the server sends to the QAEverest backend and how it's handled.

## License

MIT — see [LICENSE](LICENSE).
