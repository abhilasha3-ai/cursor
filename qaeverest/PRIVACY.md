# QAEverest MCP Server — Privacy Policy

_Last updated: 2026-08-27_

This policy covers the **QAEverest MCP server** (`qaeverest-mcp`), the QAEverest
Claude Code plugin, the QAEverest Cursor plugin, and the QAEverest desktop
extension (MCPB). All of them are thin clients that call the QAEverest public
API (`https://api.qaeverest.ai` by default). For the QAEverest platform's full
privacy policy, see <https://qaeverest.ai/privacy>.

## What data is collected and sent

The server only sends data to the QAEverest backend when you (via your AI agent)
invoke a tool. It sends:

- **Your QAEverest API key** — read from the `QAEVEREST_API_KEY` environment
  variable (or the extension's secure config) and exchanged for a short-lived
  access token. Used solely to authenticate and meter your account.
- **The content you pass to a tool** — for example the user story, API spec, or
  target URL you ask it to generate tests for or scan. This is transmitted to
  the QAEverest backend to produce the requested result.

The server does **not** read your source files on its own, scan your machine,
collect telemetry, or transmit anything except the arguments of the tool call
you explicitly trigger.

## How data is used

- To authenticate your account and meter credit usage.
- To generate the requested test cases or run the requested security/performance
  check, using QAEverest's AI engine and scanners.

## Storage and retention

- The API key and generated results are handled by the QAEverest platform under
  the QAEverest privacy policy (<https://qaeverest.ai/privacy>).
- The MCP server itself is **stateless**: it keeps the exchanged access token in
  memory only for the life of the process and writes nothing to disk.

## Third-party sharing

QAEverest does not sell your data. Content you submit is processed by QAEverest's
own backend and its AI subprocessors solely to fulfill your request. See the
platform policy for the current list of subprocessors.

## Data flows out of your environment

Both **inputs** (stories, specs, URLs) and **API credentials** leave your machine
and are sent to the QAEverest backend over HTTPS. Do not pass secrets or data you
are not permitted to share to an external service.

## Contact

Questions or data requests: **support@qaeverest.ai** ·
<https://github.com/pooja10404/CreateMyTestcases/issues>
