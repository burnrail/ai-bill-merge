# Changelog

## v0.1.2 — 2026-09-27
- The HTML file now starts with its own license line: `SPDX-License-Identifier: MIT`, Copyright (c) 2026 Burnrail.
- The bundled LiteLLM price data keeps its MIT notice in the page footer and in THIRD_PARTY_NOTICES.md.
- No change to how bills are read or totals are computed.

## v0.1.1 — 2026-09-27
- Security: the Content Security Policy now also sets `form-action 'none'` and `base-uri 'none'`.
- CI: the release workflow checks out with `persist-credentials: false`.
- README states precisely what the policy blocks (background requests and form submission; the waitlist link navigates only on click).

## v0.1.0 — 2026-09-27
- First public release of `burnrail-preview.html`: merges OpenAI and Anthropic cost-report JSON files in the browser and lists the top 3 estimated savings.
- Price table: LiteLLM at commit `e73abe6` (OpenAI and Anthropic chat models).
- SHA-256 of the release file is in `dist/burnrail-preview.html.sha256`.
