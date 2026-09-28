# Changelog

## v0.2.0 — 2026-09-28
- New in `burnrail-preview.html`: an early-access link for "monthly automatic report and spend alerts". The note right next to it says the feature does not exist yet, the price is under consideration, and nothing is sold or charged. The file picks one example price (USD 29, 79 or 199) locally each time it opens and adds `utm_content=paid-<price>` to the link. No network request; the link navigates only when clicked.
- The waitlist link's `utm_campaign` is now `ai-bill-merge-v0.2.0` (release version).
- The Content Security Policy is unchanged. Totals, savings estimates and the price table are unchanged.
- Issue-form labels are now `topic:provider`, `topic:next` and `topic:bug`; the release workflow creates them.

## v0.1.3 — 2026-09-28
- Issue forms: provider or format request, "what should come next" (optional spend and price ranges), bug report. Every form asks not to paste company names, account or key ids, or any part of a real bill.
- README: a "Requests and feedback" section.
- `burnrail-preview.html` is unchanged (same file and SHA-256 as v0.1.2).

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
