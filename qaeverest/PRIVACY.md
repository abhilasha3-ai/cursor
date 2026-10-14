# QAEverest MCP Server — Privacy Policy

_Last updated: 2026-10-12_

This policy covers the **QAEverest MCP server** (`qaeverest-mcp`) wherever it
runs: on its own, in the QAEverest Claude Code plugin, the QAEverest Cursor
plugin, the desktop extension (MCPB), and as the agent tools of the QAEverest
VS Code, Cursor and JetBrains extensions. They all run this same server, which
calls the QAEverest public API (`https://api.qaeverest.ai` by default). For the QAEverest platform's full
privacy policy, see <https://qaeverest.ai/privacy>.

## What data is collected and sent

The server only sends data to the QAEverest backend when you (via your AI agent)
invoke a tool. It sends:

- **Your QAEverest API key** — read from the `QAEVEREST_API_KEY` environment
  variable, the IDE extension that started the server, or the key you stored
  with `qae_connect`, and sent with each request. Used solely to authenticate
  and meter your account.
- **The content you pass to a tool** — for example the user story, API spec, or
  target URL you ask it to generate tests for or scan, and any files you attach
  to `qae_chat`.
- **Project files, for the tools that work on your code.** `qae_index_project`
  sends the project's source files, in chunks, to build a search index.
  `qae_build_inventory` and `qae_generate_from_features` send the files a feature
  was derived from. During a `qae_chat` turn the copilot can ask to read a file
  or search the project, and the server sends back what it finds.
  `qae_scan_project` reads the project locally and sends nothing.

The server does **not** run in the background, scan your machine outside the
project, or collect telemetry. It reads project files only during a tool call
you trigger, and only for the tools above.

## How data is used

- To authenticate your account and meter credit usage.
- To generate the requested test cases or run the requested security/performance
  check, using QAEverest's AI engine and scanners.

## Storage and retention

- The API key and generated results are handled by the QAEverest platform under
  the QAEverest privacy policy (<https://qaeverest.ai/privacy>).
- Security scans and performance tests run with a **personal API key** are saved
  to your QAEverest account, like scans run in the app: the target URL, the
  settings used and the results, so they appear in your Security and
  Performance history, Scan Trends and Quality Center (load and soak tests;
  stress and spike tests appear in history only). If your account belongs to an
  organisation, the run is shared with the organisation's members, like scans
  run in the app; it is saved only while the organisation and your membership
  are active and your role may run that kind of scan.
- The full target URL is stored, without any user name and password
  (`user:password@`); your teammates see it with its query values hidden.
  Header names are kept but their values are not, and request bodies are not
  stored.
- At most 12 runs of the same target (and test mode or scan type) are saved per
  hour; later runs in that hour still run but are not saved.
- Runs made with an ApiClient key (marketplace, device-login and IDE keys) are
  not saved.
- On your machine, the server writes: the key you store with `qae_connect` to
  `~/.qaeverest/credentials.json` (readable only by you); conversation history,
  the project map and rendered reports under the project's `.qaeverest/`
  folder; and test cases and reports you save to `qaeverest-tests/` and
  `qaeverest-reports/`.

## Third-party sharing

QAEverest does not sell your data. Content you submit is processed by QAEverest's
own backend and its AI subprocessors solely to fulfill your request. See the
platform policy for the current list of subprocessors.

## Data flows out of your environment

**Inputs** (stories, specs, URLs, and the project files described above) and **API credentials** leave your machine
and are sent to the QAEverest backend over HTTPS. Do not pass secrets or data you
are not permitted to share to an external service.

## Contact

Questions or data requests: **support@qaeverest.ai** ·
<https://github.com/pooja10404/CreateMyTestcases/issues>
