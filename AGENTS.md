# Agent Guide — countries-api plugin

This repository is a **Claude Code plugin** that packages one skill teaching
AI agents how to use the free https://countries.dev REST API. There is no
application code, build system, or test suite — the deliverables are Markdown.

## Layout

```
.claude-plugin/plugin.json               # plugin manifest (name, version, author)
skills/countries-api/SKILL.md            # skill entry point (frontmatter drives triggering)
skills/countries-api/references/endpoints.md   # exhaustive endpoint reference
.clawhubignore                           # files excluded when publishing to ClawHub
.skillignore                             # files excluded when packaging a .skill bundle
```

`skills/` at the plugin root is the location Claude Code auto-loads plugin
skills from — do not move it under `.claude/skills/`.

## Conventions

- **All repo content is in English** (docs, skill text, commit messages).
  Conversation language with the maintainer may differ; file content may not.
- **Verify before documenting.** Everything in `endpoints.md` was confirmed
  with live `curl` requests, because the official docs are incomplete and in
  places wrong. When editing endpoint documentation, re-test the endpoint
  first and document actual behavior, not what the docs claim. Keep the
  documented gotchas (e.g. `/borders/{name}` rejects ISO codes, `/distance`
  rejects city names, unknown query params are silently ignored, wrong paths
  return HTML instead of a JSON 404).
- **Keep SKILL.md lean, endpoints.md exhaustive.** SKILL.md holds the quick
  start, the endpoint-chooser table, and the numbered conventions; full
  parameter tables and response schemas belong in `references/endpoints.md`.
- The skill `description` frontmatter is the triggering mechanism — if you
  change it, keep it broad and example-rich so the skill fires on country /
  city / postal / IP / distance questions that never mention countries.dev.

## Releasing

- Bump `version` in `.claude-plugin/plugin.json` when the skill content
  changes.
- `.skillignore` restricts a packaged `.skill` bundle to the skill files
  themselves; `.clawhubignore` restricts a ClawHub listing to the skill plus
  README. Update both if you add new top-level files that should not ship.
