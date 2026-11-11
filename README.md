# Google Maps Places Scraper MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-google-maps-places-scraper/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-google-maps-places-scraper) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-google-maps-places-scraper%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-google-maps-places-scraper&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-google-maps-places-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-google-maps-places-scraper) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-google-maps-places-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-google-maps-places-scraper) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-google-maps-places-scraper)](https://github.com/mambalabsdev/mcp-google-maps-places-scraper/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-google-maps-places-scraper)

An MCP server for the Mamba Labs Google Maps Places Scraper actor on Apify. Google Maps place data as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes searches or known place IDs and returns one row per place with phone, website, address, coordinates, categories, rating, review count, hours, and attributes.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-google-maps-places-scraper": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-google-maps-places-scraper"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `search_google_maps_places` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 20 coffee shops in Austin, TX with their phone and website."
- "Look up this Google place ID and give me its hours."

## Tool

`search_google_maps_places`. One tool. Example arguments:

```json
{
  "search_terms": [
    "coffee shop in Austin, TX"
  ],
  "max_places_per_search": 5
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `search_terms` | array | no | What to search on Google Maps, such as dentist in Austin, TX. One search per entry. Each search returns up to about 120 to 200 places, so split a large area into neighborhoods. |
| `locations` | array | no | Optional. Each search term is run once per location, as "term in location". Leave empty when your searches already name the place. |
| `places` | array | no | Optional. Look up places you already know: a ChIJ place ID, or a Google Maps place URL. Each costs one place row. |
| `max_places_per_search` | number | no | Whole number from 1 to 500. Default 20. Google stops most searches between 120 and 200 places. |
| `only_country` | string | no | Optional 2 letter country code, such as DE. Places in other countries are dropped and not charged. A search for Berlin can otherwise return Berlin, New Jersey, on later pages. |
| `dedupe` | boolean | no | yes or no. Default yes: a place found twice in a run is returned and charged once. |
| `language` | string | no | Language code for names and categories, such as en or de. Default en. |
| `results_country` | string | no | 2 letter code Google uses to tailor results. Default us. It does not limit results to that country; use only_country for that. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `place-row`, one place | $0.0015 | $0.001425 | $0.00135 | $0.001275 |
| `apify-actor-start`, per run start | $0.007 | $0.007 | $0.007 | $0.007 |

Summaries, repeats, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/google-maps-places-scraper](https://apify.com/mambalabs/google-maps-places-scraper)

## License

MIT. See [LICENSE](LICENSE).
