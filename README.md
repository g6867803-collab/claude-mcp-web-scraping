# Claude MCP Web Scraping — Give Claude Live Web Access

Connect Claude (Desktop, Code, or any MCP client) to a **web scraping MCP server** so it can fetch pages, run Google searches and extract structured data on its own — no copy-pasting HTML into the chat.

## Claude Desktop

Add to `claude_desktop_config.json` (Settings → Developer → Edit Config):

```json
{
  "mcpServers": {
    "quantumproxies": {
      "command": "npx",
      "args": ["-y", "quantumproxies-mcp"],
      "env": {
        "QUANTUMPROXIES_API_KEY": "qp_live_your_key_here"
      }
    }
  }
}
```

Restart Claude Desktop — done.

## Claude Code (CLI)

```bash
claude mcp add quantumproxies \
  -e QUANTUMPROXIES_API_KEY=qp_live_your_key_here \
  -- npx -y quantumproxies-mcp
```

## What Claude can do once connected

| Tool | What it does |
| --- | --- |
| `scrape` | any URL → clean markdown (JS rendering + anti-bot handled) |
| `search` | live Google/Bing results as structured JSON |
| `crawl` / `map` | walk a whole site, or list its URLs |
| `batch` | scrape many URLs in one job |

Example prompts that just work afterwards:

> "Read https://competitor.com/pricing and summarize the tiers in a table."
>
> "Search for 'best CRM for startups', open the top 3 results, and compare their positioning."

## Why route it through a scraping backend

Claude's built-in fetch gets blocked by anything with bot protection and can't render SPAs. The MCP server proxies every request through a residential network with rendering and retries — so "read this page" works on real-world sites, not just blogs.

Server details & tool list: [quantumproxies.io/mcp-server](https://quantumproxies.io/mcp-server) · npm: [`quantumproxies-mcp`](https://www.npmjs.com/package/quantumproxies-mcp) · API key: [app.quantumproxies.io/api-keys](https://app.quantumproxies.io/api-keys).
