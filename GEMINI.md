# TextKit

The `textkit` MCP server sends and receives SMS, verifies phone numbers, buys and manages phone numbers, and runs contacts, segments, broadcasts and automations on the user's TextKit account.

## Connecting

- If a tool answers "Authentication required", tell the user to run `/mcp auth textkit`. A browser opens; they approve the connection and pick test or live data.
- Test data runs in the sandbox: no real phone gets a text. Suggest it for trying things out.
- Docs: https://jointextkit.com/docs/mcp

## How to use the tools

- Phone numbers are E.164: `+15551234567`.
- Before texting many people, call `send_batch` with `dry_run: true` and show the user the recipient count, cost and skipped recipients. Send only after they approve.
- To bring people in (an audience, cohort or customer list) when the user has not said from where, call `plan_import` and ask its questions instead of assuming a CSV. `import_contacts` with `dry_run: true` first.
- Consent comes from the source. Set `opt_in` only where the source recorded one. Never mark people as opted in yourself.
- For "who did X" questions about existing contacts, use `query_audience` (saves nothing). To save an audience, use `create_segment`, then `send_batch` with `segment_id`.
- Results of tools that change the account include `console_url`: give the user that link.
- When building an app that should send texts itself, call `create_api_key` and store the key as the secret `TEXTKIT_API_KEY`. Never print a live key in code or logs.
- Results and stats: `get_batch_results`, `get_deliverability`, `get_usage`, `list_messages`, `export_csv`.

## REST API

For code, use the REST API: base URL `https://api.jointextkit.com/v1`, header `Authorization: Bearer ssms_sk_...`. OpenAPI: https://jointextkit.com/api/v1/openapi.yaml.

```bash
curl https://api.jointextkit.com/v1/messages \
  -H "Authorization: Bearer $TEXTKIT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"to": "+15005550006", "body": "Your order shipped."}'
```
