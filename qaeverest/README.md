# QAEverest — Cursor Plugin

Generate AI-powered test cases — and run security & performance checks — from inside Cursor's agent. This plugin bundles the [QAEverest MCP server](https://www.npmjs.com/package/@qaeverestsupport.ai/qaeverest-mcp) plus skills that tell the agent which tool fits which request.

> Want the **QAEverest chat panel** in Cursor's sidebar — tabs, document attachments, saving `.feature` files — rather than agent-side tools? That's the QAEverest Cursor extension (a VSIX) — see [qaeverest.ai](https://qaeverest.ai). The two work side by side; the extension also registers this same MCP server for you.

## What you get

**MCP tools** — the same QAEverest MCP server the Claude Code plugin and the IDE extensions run. The agent picks these automatically when you describe what you want:

<!-- qaeverest:tools surface=cursor-plugin -->
<!-- Generated from mcp-server/src/manifest.js by `npm run sync` in mcp-server/. -->

| Area | Tool | What it does | Uses credits |
|---|---|---|---|
| Chat | `qae_chat` | Ask the QA copilot anything: generate tests, build or run a suite, ask about a run | yes |
|  | `qae_approve` | Settle an approval `qae_chat` asked for, with the user's own answer | yes |
|  | `qae_new_chat` | Start a fresh conversation | no |
|  | `qae_history` | List this project's conversations | no |
|  | `qae_open_chat` | Make an earlier conversation active again | no |
| Generate | `qae_generate_testcases` | Functional, system, SIT, database and other test cases from a story | yes |
|  | `qae_generate_api_tests` | API test cases from a description, an OpenAPI/Swagger spec or a Postman collection | yes |
|  | `qae_generate_ui_tests` | End-to-end UI automation test cases (navigate / click / type / assert) | yes |
|  | `qae_generate_mobile_tests` | Mobile automation test cases: gestures, device states, platform behaviour | yes |
| Your code | `qae_scan_project` | Repo Map: languages, frameworks, entry points, files worth testing (local) | no |
|  | `qae_index_project` | Index the codebase so generation can cite real code | no |
|  | `qae_search_project` | Semantic search over the indexed codebase | no |
|  | `qae_build_inventory` | Ranked inventory of testable features, with the files each came from | no |
|  | `qae_select_features` | Re-show the inventory with the ids to generate from | no |
|  | `qae_generate_from_features` | Test cases for inventory features, grounded in their source files | yes |
| Suites and runs | `qae_list_suites` | Automation suites on the account, with their ids | no |
|  | `qae_run_suite` | Execute an automation suite against an environment | yes |
|  | `qae_save_report` | Write the HTML report for the last run into `qaeverest-reports/` | no |
|  | `qae_open_report` | Path of the most recently saved report | no |
| AI agent testing | `qae_agent_suites` | Saved AI agent suites, the agent each tests, baseline status | no |
|  | `qae_agent_run` | Run a saved AI agent suite against the agent or another endpoint | yes |
|  | `qae_agent_run_status` | Progress, trust score, release gate and verdict of an agent run | no |
| Security and performance | `qae_security_scan` | Security headers, SSL/TLS and common vulnerability checks on a URL | yes |
|  | `qae_performance_test` | Load, stress, spike or soak test: latency percentiles, throughput, error rate | yes |
| Mobile | `qae_mobile_setup` | Device farm, app binary and handset configuration (links to the web app) | no |
| Account | `qae_status` | Connection, backend, key type, credits, requests this month, enabled services | no |
|  | `qae_connect` | Store an API key, or start browser sign-in | no |
|  | `qae_disconnect` | Forget the stored API key on this machine | no |

<!-- /qaeverest:tools -->

**MCP prompts** — ready-made workflows:

<!-- qaeverest:prompts surface=cursor-plugin -->
<!-- Generated from mcp-server/src/manifest.js by `npm run sync` in mcp-server/. -->

| Prompt | What it does |
|---|---|
| `agent-test` | Run a saved AI agent suite and report its release-gate verdict |
| `chat` | Ask the QAEverest QA copilot anything — generate tests, build and run suites, or ask about a run |
| `connect` | Connect a QAEverest account, or check the current connection |
| `generate-tests` | Generate QA test cases from a story, a file, or a feature description via QAEverest |
| `index-project` | Index this project into QAEverest so generated tests cite real code |
| `inventory` | Build (or re-show) the ranked inventory of testable features in this project |
| `mobile-setup` | Configure QAEverest mobile automation — device farm, app binary, and handset |
| `new-chat` | Start a fresh QAEverest conversation |
| `performance-test` | Run a load, stress, spike or soak test against a URL |
| `report` | Save and show the HTML execution report for the last QAEverest run |
| `run-suite` | Run a QAEverest automation suite against an environment |
| `scan-project` | Build a QAEverest Repo Map of this project — languages, frameworks, and the files worth testing |
| `search-project` | Semantic search over the indexed codebase — ask in plain English |
| `security-scan` | Run a QAEverest security scan against a URL |
| `usage` | Show QAEverest credits remaining, key type, and which backend this project talks to |

<!-- /qaeverest:prompts -->

**Skills** — `generate-tests`, `security-scan`, `performance-test`, `usage`. Each one carries the judgement that turns a tool call into a useful answer: which tool fits the request, what to put in `additional`, where generated scenarios belong in the repo, and when to ask before pointing a scan at a host.

**A rule** — `rules/qaeverest.mdc`, attached when the conversation is about testing: the tool-selection table, the credit cost of each call, and the authorization rule for scan and run targets.

## Prerequisites

- **Node.js 18+** (the plugin runs the server via `npx @qaeverestsupport.ai/qaeverest-mcp@^2`)
- A **QAEverest API key** (`qae_...`) — [sign up free](https://qaeverest.ai/api-client/signup?source=cursor) (no card) or get one from **Admin → API Management**.

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
