# Vimeo MCP server for ChatGPT and Claude

Vimeo has an API and an official MCP server, according to the Cotlet.dev page checked 17 October 2026. Cotlet.dev offers a hosted connection to your signed-in Vimeo account for ChatGPT, Claude and other AI agents, with 13 task tools for videos, folders, showcases, captions, comments and analytics. Privacy changes, caption uploads and comment deletion ask for confirmation by default.

## What you can ask

> Upload the missing English captions.

> Move loose webinars to Webinars.

> Which videos lose viewers earliest?

## Connect in 2 minutes

Sign up at https://cotlet.dev/signup?app=vimeo, enable Vimeo and sign in at https://vimeo.com in your Cloud Browser. Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

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

## Run the local MCP bridge

Python 3.10+, with no dependencies. Clone this repository, set your Cotlet.dev API key, then run:

```bash
export COTLET_API_KEY="your-key"
python3 vimeo_agent.py serve
```

This local stdio bridge lists seven browser helper tools: `vimeo_guide`, `vimeo_status`, `vimeo_open`, `vimeo_read`, `vimeo_click`, `vimeo_type` and `vimeo_close`.
It forwards calls to the hosted Cotlet.dev MCP server.
The 13 task tools described on the integration page are available through the hosted connection.

Without a key, the local bridge can list its helpers; calls return setup instructions.

```bash
python3 vimeo_agent.py connect
python3 vimeo_agent.py guide
python3 vimeo_agent.py status
```

## Questions from Vimeo users

**Does Vimeo have an API or official MCP server?**

Yes. The Cotlet.dev page checked 17 October 2026 describes a Vimeo REST API with OAuth 2.0 and an official remote MCP server in public beta requiring a Pro plan or above.

**How do I connect Vimeo to ChatGPT or Claude?**

Sign up at https://cotlet.dev/signup?app=vimeo, enable Vimeo and sign in to your own account in its Cloud Browser. Follow the connector instructions in your Cotlet.dev console. No API key is needed for the ChatGPT or Claude hosted connector.

**What needs confirmation?**

Privacy changes, caption uploads and comment deletion wait for your approval by default. Keep confirmation enabled for comment deletion.

**Is Cotlet.dev affiliated with Vimeo?**

No. Cotlet.dev is independent and is not affiliated with Vimeo.

## Integration details

[Vimeo tools and setup on Cotlet.dev](https://cotlet.dev/integrations/vimeo-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=vimeo)

---

More: https://cotlet.dev/integrations/vimeo-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=vimeo

Start free: https://cotlet.dev/signup?app=vimeo&utm_source=github&utm_medium=readme&utm_campaign=vimeo
