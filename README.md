# TidyBot Services Wishlist

API and software requests from skill agents to service agents.

## What's Here

- **[RULES.md](RULES.md)** — Complete workflow for requesting and fulfilling services
- **[catalog.json](catalog.json)** — Catalog of all recently added new APIs and services
- **[wishlist.json](wishlist.json)** — Requested APIs/models/services not yet available
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — How to request or fulfill a service

## How It Works

1. **Skill agent** encounters a missing API, model, or service, wish to have it.
2. **Skill agent** adds a request to [wishlist.json](wishlist.json)
3. **Service agent** picks up the request and implements it
4. **Service agent** marks it done, updates [catalog.json](catalog.json) and API docs
5. **Skill agent** uses the new capability via `robot_sdk` or the HTTP API

## The Two Sides

```
Skill Agent (e.g., Frank)             Service Agent
─────────────────────────────         ─────────────────────
• Builds robot skills                 • Installs models/services
• Calls robot_sdk / HTTP API          • Creates new API endpoints
• Discovers missing capabilities      • Updates server code
• Adds requests to wishlist.json      • Updates SDK documentation
• Uses new APIs once available        • Marks requests as done
```

## For Skill Agents

When you need something the services don't provide:

1. Check [catalog.json](catalog.json) — maybe it is recently added
2. Check [wishlist.json](wishlist.json) — maybe it's already requested, so you just wait.
3. If not, add it to `wishlist.json` with a clear description of what you need and why
4. Notify the service agent

## For Service Agents

1. Check [wishlist.json](wishlist.json) for pending requests
2. Pick a request, mark it as `building`
3. Implement the capability (install model/software, add endpoint, extend SDK)
4. Update the robot server's API docs (`GET /code/sdk/markdown`)
5. Add to [catalog.json](catalog.json), mark wishlist item as `done`

## License

MIT
