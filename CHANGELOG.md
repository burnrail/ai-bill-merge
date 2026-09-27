# Changelog

## v0.1.1 — 2026-09-27
- Security: the Content Security Policy now also sets `form-action 'none'` and `base-uri 'none'`.
- CI: the release workflow checks out with `persist-credentials: false`.
- README states precisely what the policy blocks (background requests and form submission; the waitlist link navigates only on click).

## v0.1.0 — 2026-09-27
- First public release of `burnrail-preview.html`: merges OpenAI and Anthropic cost-report JSON files in the browser and lists the top 3 estimated savings.
- Price table: LiteLLM at commit `e73abe6` (OpenAI and Anthropic chat models).
- SHA-256 of the release file is in `dist/burnrail-preview.html.sha256`.
