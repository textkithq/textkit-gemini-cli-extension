# TextKit extension for Gemini CLI

Adds the [TextKit](https://jointextkit.com) MCP server to Gemini CLI: send and receive SMS, verify phone numbers, buy numbers, load contacts, build segments, and run broadcasts and automations from the terminal.

## Install

```bash
gemini extensions install https://github.com/textkithq/textkit-gemini-cli-extension
```

Start `gemini` and sign in to TextKit:

```
/mcp auth textkit
```

A browser opens: approve the connection and pick test or live data. Test data runs in the sandbox, so no real phone gets a text.

Then ask for something, for example:

- Buy a number in area code 512 and text +15005550006 "Your order shipped."
- Send everyone tagged vip "Doors open at 9 on Saturday." Do a dry run first and show me the count and cost.
- How did yesterday's broadcast do?

## Use an API key instead of signing in

Skip the extension and add the server with a header:

```bash
gemini mcp add --transport http --header "Authorization: Bearer ssms_sk_test_..." textkit https://mcp.jointextkit.com
```

Get a key at [jointextkit.com/console](https://jointextkit.com/console).

## What's inside

- `gemini-extension.json`: the remote server `https://mcp.jointextkit.com` (streamable HTTP).
- `GEMINI.md`: usage notes loaded into Gemini's context (dry runs before bulk sends, consent, E.164 numbers).

Docs: https://jointextkit.com/docs/mcp

## License

MIT
