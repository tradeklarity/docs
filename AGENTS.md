# Documentation project instructions

## About this project

- Public documentation for Klarity's data services, built on [Mintlify](https://mintlify.com).
- Pages are MDX files with YAML frontmatter. Navigation and site config live in `docs.json`.
- Documents three consumable surfaces: the **Telegram monitor** and **X (Twitter) monitor** realtime WebSocket streams, and the **UMA API** (REST).
- Payload and endpoint shapes must match the service source — do not invent fields. Sources:
  - Telegram stream: `klarity-telegram-monitor/src/websocket.ts`
  - X stream: `klarity-x-monitor/src/websocket.ts`
  - UMA API: `klarity-uma-api/src/routes/*` and `src/server.ts`

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
