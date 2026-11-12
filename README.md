# EZ Lawn Biller MCP server for ChatGPT and Claude

Connect EZ Lawn Biller to ChatGPT, Claude and other AI agents through Cotlet. Work with routes, customer records, visit history and payments in your own signed-in account. Cotlet is independent and not affiliated with EZ Lawn Biller. If EZ Lawn Biller offers an official API for your needs, we recommend it.

## What you can ask

> Show the customers with past-due balances.

> Prepare changes to the stops I name in a private schedule draft and ask me before publishing.

> Record the cash payment I provide, with its amount, reference and date. Ask me before saving.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its EZ Lawn Biller tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"ez-lawn-biller": {"command": "python3", "args": ["/absolute/path/to/ez-lawn-biller-mcp/ez_lawn_biller_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t ez-lawn-biller-mcp .
docker run -i --rm -e COTLET_API_KEY ez-lawn-biller-mcp
```

Tools: `ez_lawn_biller_guide`, `ez_lawn_biller_status`, `ez_lawn_biller_open`, `ez_lawn_biller_read`, `ez_lawn_biller_click`, `ez_lawn_biller_type`, `ez_lawn_biller_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 ez_lawn_biller_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 ez_lawn_biller_agent.py status    # is EZ Lawn Biller ready in your Cotlet.dev account
python3 ez_lawn_biller_agent.py guide     # EZ Lawn Biller screens and sign-in link
python3 ez_lawn_biller_agent.py read      # open EZ Lawn Biller, read the page, close the browser
python3 ez_lawn_biller_agent.py tools     # list Cotlet.dev tools
python3 ez_lawn_biller_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from EZ Lawn Biller users

**How do I connect EZ Lawn Biller to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to EZ Lawn Biller once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your EZ Lawn Biller account through Cotlet, in their phone apps too.

**Can ChatGPT reschedule lawn visits in EZ Lawn Biller?**

ChatGPT moves the stops you name in a private schedule draft and publishes it after you approve, so technicians' phones get the new routes.

**Can ChatGPT record a payment in EZ Lawn Biller?**

ChatGPT records the cash or check payment you give it, with amount, method, reference and date, on the customer's account.

**Can ChatGPT send past-due notices in EZ Lawn Biller?**

ChatGPT selects the customers who owe you, previews each personalized notice and sends them with their statements after you approve the run.

**Is Cotlet affiliated with EZ Lawn Biller?**

No. Cotlet is independent and not affiliated with EZ Lawn Biller.

## Find it on

- [EZ Lawn Biller on Cotlet](https://cotlet.dev/integrations/ez-lawn-biller-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/ez-lawn-biller-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=ez-lawn-biller

Request access: https://cotlet.dev/signup?app=ez-lawn-biller&utm_source=github&utm_medium=readme&utm_campaign=ez-lawn-biller
