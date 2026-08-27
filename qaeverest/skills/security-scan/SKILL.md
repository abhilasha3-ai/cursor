---
name: security-scan
description: >-
  Run a QAEverest security scan against a URL — security headers, SSL/TLS
  configuration, and common vulnerabilities — and report findings by risk. Use
  when the user asks to scan a site or endpoint for security issues, check
  their headers or certificate, or audit a staging environment before release.
---

# Security scan with QAEverest

## Confirm the target

1. The target is a full URL including the scheme. If the user gave a bare host, ask them to confirm `https://…` rather than assuming.
2. **Only scan hosts the user is authorized to test.** If the target isn't obviously their own environment, ask before calling.

## Run it

Call `security_scan`:

- `url` — the confirmed target.
- `scanType` — `full` unless the user asked for only `headers`, `ssl`, or `vulnerability`.
- `method` / `headers` — pass an auth header when the endpoint needs one to return its real response; a scan of a login redirect tells you nothing about the app behind it.

## Report

1. Group findings by risk, critical first.
2. Lead with the single most important thing to fix, and say what fixing it looks like — a header to add, a protocol version to disable, a certificate to renew.
3. Note anything the scan could NOT reach (auth walls, redirects), so a clean result isn't mistaken for full coverage.
4. Offer to open the fixes as changes in the repo when the finding maps to something in the codebase (a missing CSP header in a server config, for instance).

This consumes QAEverest credits and probes a live external target.
