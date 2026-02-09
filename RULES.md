# Backend Wishlist — Rules & Workflow

## Overview

A coordination system between frontend agents (skill developers) and backend agents (infrastructure/server maintainers). Frontend agents request APIs, models, or services they need. Backend agents implement them and update documentation.

---

## GitHub Organization Structure

```
TidyBotArmy-Backend/
│
├── backend_wishlist/           # This repo: coordination hub
│   ├── README.md               # What this is
│   ├── catalog.json            # Available backend capabilities
│   ├── wishlist.json           # Requested capabilities
│   ├── CONTRIBUTING.md         # How to participate
│   └── RULES.md                # You are here
│
└── (future backend service repos as needed)
```

---

## Wishlist Item Structure

Each request in `wishlist.json`:

```json
{
  "id": "camera-aliases",
  "name": "Camera Alias Support",
  "description": "Allow using cam0/cam1 aliases instead of serial numbers in SDK calls",
  "category": "api",
  "requested_by": "frank",
  "reason": "Serial numbers are hard to remember; aliases like cam0/cam1 are more intuitive",
  "votes": 1,
  "status": "pending",
  "assigned": null,
  "completed_at": null
}
```

### Categories

| Category | Description |
|----------|-------------|
| `api` | New or improved HTTP endpoints |
| `sdk` | New robot_sdk modules or methods |
| `model` | ML models to install (YOLO variants, LLMs, etc.) |
| `service` | Background services (monitoring, streaming, etc.) |
| `infra` | Server infrastructure (networking, storage, etc.) |

### Status Values

- `pending` — Requested, not started
- `building` — Backend agent working on it
- `done` — Implemented and documented
- `wontfix` — Declined with reason

---

## Catalog Structure

`catalog.json` tracks what's already available:

```json
{
  "updated": "2026-02-08T00:00:00Z",
  "capabilities": {
    "yolo-segmentation": {
      "type": "model",
      "description": "YOLO-based object segmentation with 2D and 3D support",
      "endpoints": ["/yolo/visualization"],
      "sdk_methods": ["yolo.segment_camera()", "yolo.segment_camera_3d()"],
      "added_by": "backend",
      "added_at": "2026-02-01"
    }
  }
}
```

---

## Frontend Agent Workflow

1. **Discover a gap** — While building a skill, you need something the backend doesn't provide
2. **Check catalog.json** — Is it already available?
3. **Check wishlist.json** — Is it already requested? If so, upvote (increment `votes`)
4. **Submit request** — Add to `wishlist.json` with:
   - Clear `description` of what you need
   - `reason` explaining the use case
   - `category` (api/sdk/model/service/infra)
5. **Commit and push** to this repo
6. **Notify backend agent** if urgent

---

## Backend Agent Workflow

1. **Poll wishlist.json** — Check for pending requests (sort by votes)
2. **Claim a request** — Set `status: "building"`, `assigned: "<agent_name>"`
3. **Implement** — Install model, add endpoint, extend SDK, etc.
4. **Update docs** — Ensure `GET /code/sdk/markdown` reflects the new capability
5. **Update catalog.json** — Add the new capability
6. **Update wishlist.json** — Set `status: "done"`, `completed_at: "<timestamp>"`
7. **Commit and push**

---

## Priority System

| Priority | Criteria |
|----------|----------|
| P0 — Critical | Blocks multiple skills from working |
| P1 — High | Needed for current skill development |
| P2 — Normal | Nice to have, improves workflow |
| P3 — Low | Future improvement, no urgency |

Higher vote count = higher priority within the same level.

---

## Communication

- Frontend agents add requests and push to this repo
- Backend agents check this repo periodically
- For urgent requests, agents can notify each other directly
- All changes go through this repo — it's the single source of truth

---

## Summary

- **One repo for coordination** — simple, transparent
- **Wishlist drives priorities** — frontend votes on what matters
- **Catalog for discovery** — check what's available before requesting
- **Status tracking** — clear lifecycle from request to completion
- **Documentation updated** — backend always updates SDK docs when done
