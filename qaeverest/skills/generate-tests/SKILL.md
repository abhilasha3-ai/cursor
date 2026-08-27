---
name: generate-tests
description: >-
  Generate QA test cases with QAEverest from a user story, a requirements file
  in the repo, an OpenAPI/Swagger spec, a Postman collection, or a described UI
  or mobile flow. Use when the user asks for test cases, a test plan, test
  scenarios, API tests, UI/E2E automation scenarios, or mobile test scenarios —
  and when they want Gherkin scenarios saved into the repo.
---

# Generate test cases with QAEverest

## Find the source material

1. If the user named a file, read it and use its contents as the story. Requirements live in `.md`, `.txt`, `.docx`, Jira exports, `openapi.yaml`/`swagger.json`, or a Postman collection `.json`.
2. If they described a feature inline, use that.
3. If they pointed at code, read enough of it to state the behaviour under test in plain language — the tools take a story, not a diff.
4. If you have neither, ask what to generate tests for. Don't guess: a vague story costs a credit and returns vague coverage.

## Pick the tool

| Source | Tool |
|---|---|
| Functional or system requirement | `generate_testcases` |
| API description, OpenAPI/Swagger spec, or Postman collection | `generate_api_tests` |
| Browser flow, end to end | `generate_ui_tests` |
| Mobile app flow | `generate_mobile_tests` |

`generate_ui_tests` and `generate_mobile_tests` run as background jobs — tell the user it may take a few minutes rather than going quiet.

## Fill the arguments properly

- `domain_name` / `module_name` — infer from the repo (the service, package or feature folder the story belongs to) rather than leaving them empty.
- `additional` — the constraints the story doesn't state: validation rules, error states, roles and permissions, rate limits, anything the user called out as risky.
- `test_type` / `tc_type` on `generate_testcases` — `automated` when the user intends to automate these, `manual` when they're for a QA team to execute.

## Present and save

1. Summarize the coverage first: how many scenarios, and which positive / negative / edge areas they hit. Don't paste every scenario before the user has said they want them.
2. Offer to save. Default to `qaeverest-tests/<module>.feature` in Gherkin, unless the repo already has a test layout — then follow it.
3. Offer to scaffold automation from the saved scenarios (Playwright, Cypress, RestAssured, Appium — whatever the repo already uses).

Each call consumes QAEverest credits. Run `get_usage` first if the user wants to know their balance, and never retry a failed generation in a loop.
