# Countries API — Claude Code Plugin

A Claude Code plugin that teaches Claude how to use the free
[countries.dev](https://countries.dev) REST API — no API key, no signup, no
rate-limit tiers.

Once installed, just ask questions in natural language and Claude picks the
right endpoint, parameters, and workarounds automatically:

- "Which countries border Germany?"
- "Top 10 countries by population in Asia"
- "What currency does Taiwan use?"
- "Coordinates and timezone of Taipei"
- "Which country is the IP 8.8.8.8 in?"
- "Look up ZIP code 90210"
- "How far is Taipei from Tokyo?"

## What the skill covers

| Area | Endpoints |
|---|---|
| Country data | lookup by ISO/IOC/numeric code or name, filter by region, currency, language, timezone, TLD, demonym, population/area range, independence, borders |
| Cities & places | ~34k cities and ~12M GeoNames features, search and reverse geocoding (`/cities`, `/places`, `/*/near`) |
| Postal codes | ~1.8M ZIP/postal codes across ~121 countries |
| IP geolocation | single, own-IP, and batch lookups |
| Distance | great-circle distance between coordinates or GeoNames IDs |
| Reference data | regions, subregions, currencies, languages, timezones |

Every endpoint in [`skills/countries-api/references/endpoints.md`](skills/countries-api/references/endpoints.md)
was **verified against the live API**, including gotchas the official docs
don't mention (e.g. `/borders` only accepts country *names*, `/distance`
doesn't accept city names, unknown query params fail silently).

## Installation

**As a plugin** (recommended):

```
/plugin install countries-api
```

or add this repository as a marketplace source and install from there.

**As a standalone skill** — copy the skill folder into your skills directory:

```bash
# available in every project
cp -r skills/countries-api ~/.claude/skills/

# or per-project
cp -r skills/countries-api <your-project>/.claude/skills/
```

## Repository layout

```
.claude-plugin/plugin.json          # plugin manifest
skills/countries-api/
├── SKILL.md                        # main skill: quick start, endpoint chooser, conventions
└── references/endpoints.md         # full reference: every endpoint, parameter, schema
```

## License

[MIT](LICENSE) © 2026 NanookAI. Country and geographic data is served by
[countries.dev](https://countries.dev) (backed by GeoNames).
