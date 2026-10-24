# Semrush Extension for Claude SEO

Live Semrush data without an API key of your own. The `seo-semrush` skill uses
the first route that works:

1. **Semrush MCP connector** (claude.ai connector or a manual MCP install). Tool
   names are matched by suffix (`execute_report`, `get_report_schema`, ...), so
   the random server prefix of a claude.ai connector does not matter.
2. **Semrush web UI in the built-in browser**, when the connector is missing or
   out of API units. You log in to Semrush yourself; Claude never types
   credentials.
3. **Nothing**: no numbers are written, and the gap is reported.

Every result is saved to `~/.cache/claude-seo/semrush/` as JSON. The
`seo-semrush` agent reads those files only, so it works in any account without
MCP permissions.

## Installation

Plugin installs ship the skill and agent already (`skills/seo-semrush`,
`agents/seo-semrush.md`). Manual installs copy them with the root `install.sh`
or `install.ps1`, which picks up every `extensions/*/skills` and
`extensions/*/agents` folder. There is no MCP server to configure: connect
Semrush in claude.ai (Settings, Connectors) or log in to semrush.com in the
built-in browser.

## Commands

| Command | Description |
|---|---|
| `/seo semrush overview <domain> [db]` | Domain overview |
| `/seo semrush organic <domain> [db]` | Organic keywords and positions |
| `/seo semrush keywords <kw1, kw2> [db]` | Volume, KD, CPC, intent |
| `/seo semrush ideas <seed> [db]` | Keyword ideas |
| `/seo semrush backlinks <domain>` | Backlink summary |
| `/seo semrush competitors <domain> [db]` | Organic competitors |
| `/seo semrush tracking <project>` | Position Tracking results |

## Limits

- The web UI route is slower and depends on Semrush's page layout.
- Connector calls spend Semrush API units; web UI reads spend the web
  account's daily report quota.
- Semrush has no geo-grid, business listing, Lighthouse, or LLM mention data.
