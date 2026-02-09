# TidyBotArmy Backend Wishlist

API and software requests from frontend agents to backend agents.

## What's Here

- **[RULES.md](RULES.md)** — Complete workflow for requesting and fulfilling backend capabilities
- **[catalog.json](catalog.json)** — Catalog of all available backend APIs and services
- **[wishlist.json](wishlist.json)** — Requested APIs/models/services not yet available
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — How to request or fulfill a backend capability

## How It Works

1. **Frontend agent** encounters a missing API, model, or backend capability
2. **Frontend agent** adds a request to [wishlist.json](wishlist.json)
3. **Backend agent** picks up the request and implements it
4. **Backend agent** marks it done, updates [catalog.json](catalog.json) and API docs
5. **Frontend agent** uses the new capability via `robot_sdk` or the HTTP API

## The Two Sides

```
Frontend Agent (e.g., Frank)          Backend Agent
─────────────────────────────         ─────────────────────
• Builds robot skills                 • Installs models/services
• Calls robot_sdk / HTTP API          • Creates new API endpoints
• Discovers missing capabilities      • Updates server code
• Adds requests to wishlist.json      • Updates SDK documentation
• Uses new APIs once available        • Marks requests as done
```

## For Frontend Agents

When you need something the backend doesn't provide:

1. Check [catalog.json](catalog.json) — maybe it already exists
2. Check [wishlist.json](wishlist.json) — maybe it's already requested
3. If not, add it to `wishlist.json` with a clear description of what you need and why
4. Notify the backend agent

## For Backend Agents

1. Check [wishlist.json](wishlist.json) for pending requests
2. Pick a request, mark it as `building`
3. Implement the capability (install model, add endpoint, extend SDK)
4. Update the robot server's API docs (`GET /code/sdk/markdown`)
5. Add to [catalog.json](catalog.json), mark wishlist item as `done`

## License

MIT
