---
name: usage
description: >-
  Check the QAEverest account behind this plugin — credits used and remaining,
  requests this month, and which services are enabled for the API key. Use when
  the user asks about their QAEverest balance or quota, when a QAEverest tool
  fails with an auth or entitlement error, or before a large batch of
  generations.
---

# QAEverest usage and entitlements

Call `get_usage` and report, concisely:

- Credits used and remaining.
- Requests this month, and the limit if there is one.
- Which QAEverest services are enabled for this API key.

## Reading the result

- **A service the user needs is disabled.** That is an account setting, not a bug — an admin enables it under **Admin → API Management**. Say that instead of retrying the failing tool.
- **Credits are nearly gone.** Say how many generations that leaves before they start a batch, rather than discovering it mid-run.
- **The call itself fails with an auth error.** The `QAEVEREST_API_KEY` variable is missing or wrong. Point the user at the plugin's settings in Cursor (**Customize → Plugins → QAEverest**) — do not ask them to paste the key into the chat.
