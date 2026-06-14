# Documentation project instructions

## About this project

- Public documentation for the Klarity ecosystem (a prediction-market trading terminal and the tools around it), built on [Mintlify](https://mintlify.com).
- Pages are MDX files with YAML frontmatter. Navigation and site config live in `docs.json`.
- Documents these consumable surfaces:
  - **Klarity API** (the core prediction-market data platform — REST + SSE) under the **API Reference** tab: markets, events/discovery, **Hyperliquid (HIP-4)**, users, leaderboard, clusters, funding, cohorts, correlations, alert rules, copy trading, and live trade/wallet streams. Source: the `klarity-toolsets` monorepo (`apps/api`, `apps/stream`). These pages are **OpenAPI-driven** — each page's frontmatter references a spec file at the repo root as `openapi: <file> <METHOD> <path>` (`openapi-api.yaml`, `openapi-users.yaml`, `openapi-stream.yaml`, `openapi-hyperliquid.yaml`). To change a shape, edit the spec (ideally regenerate it from the toolsets route schemas) — do not invent fields.
  - **Realtime streams** — the **Telegram monitor** and **X (Twitter) monitor** WebSocket feeds. Sources: `klarity-telegram-monitor/src/websocket.ts`, `klarity-x-monitor/src/websocket.ts`.
  - **UMA API** (REST). Source: `klarity-uma-api/src/routes/*` and `src/server.ts`.
- Payload and endpoint shapes must match the service source — do not invent fields.
- **Hyperliquid terminology:** use Hyperliquid's native terms — **questions** (containers, ≈ Polymarket events) and **outcomes** (tradeable binaries, ≈ Polymarket markets). Standalone (question-less) outcomes exist and surface as single-outcome cards. Do not reintroduce "market"/"event" wording for HIP-4.

## Terminology

- "**Realtime stream**" for the WebSocket feeds, not "feed" or "socket".
- "**X (Twitter)**" on first mention, "X" thereafter — the endpoint is `x.klarity.trade`.
- "**Resolution**" is the UMA event; its `type` is either "**proposal**" or "**dispute**". Do not call a resolution a "market".
- "**DVM vote**" for UMA token-holder votes (not "validator" or "oracle vote").
- "**frame**" for a single WebSocket message; "**payload**" for its JSON body.
- Endpoints are written with their full host (`wss://telegram.klarity.trade`, `https://uma.klarity.trade/v1`).

## Style preferences

- Use active voice and second person ("you").
- Keep sentences concise — one idea per sentence.
- Use sentence case for headings.
- Bold for UI elements: Click **Settings**.
- Code formatting for file names, commands, paths, field names, and code references.
- Document field shapes with `<ResponseField>` and parameters with `<ParamField>`; show a realistic JSON example after the field list.
- Keep JSON examples minimal and plausible; never paste real tokens, cookies, or secrets.

## Content boundaries

- Document only the consumable surfaces above. Do **not** document internal workers (news-pinger, uma-fetcher), infrastructure (AWS/DynamoDB, the EC2 box), or deployment.
- Never include real `klarity_access_token` values, API keys, or wallet/secret material — use placeholders like `<token>`.
- Auth is a Klarity session cookie (`klarity_access_token`); describe it, don't expose how it's signed.
