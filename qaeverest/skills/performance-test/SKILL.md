---
name: performance-test
description: >-
  Run a QAEverest load, stress, spike or soak test against a URL and report
  latency, throughput and error rate. Use when the user asks how fast an
  endpoint is under load, wants a load or stress test, asks about throughput or
  p95 latency, or wants to check an endpoint before a release.
---

# Performance test with QAEverest

## Confirm the target — this one sends real traffic

1. The target is a full URL including the scheme.
2. `performance_test` drives actual load at whatever it is pointed at. **Confirm the user owns or is authorized to load-test the target before calling**, and prefer a staging URL when one exists. Never point it at a third party's site.

## Choose the profile

| The user wants to know | `testMode` |
|---|---|
| How it behaves under expected traffic | `load` |
| Where it starts to break | `stress` |
| How it handles a sudden surge | `spike` |
| Whether it degrades over time | `soak` |

Pass `method`, `headers` and `body` when the endpoint needs them — testing a 401 response measures nothing useful. `virtualUsers`, `duration` and `rampUp` are optional; server-side caps apply (load ≤ 60s, soak ≤ 90s), so a single call is bounded at roughly a minute. Heavier runs belong in the QAEverest app's Performance module — say so rather than looping calls to simulate a longer run.

## Report

1. Lead with p95 latency, throughput and error rate — the three numbers that decide whether this ships.
2. Compare against the user's target if they gave one; if they didn't, ask what their threshold is before calling the result good or bad.
3. Point at the likely bottleneck when the repo makes it visible (an N+1 query, a missing index, a synchronous call in a request path), and offer to look.

This consumes QAEverest credits.
