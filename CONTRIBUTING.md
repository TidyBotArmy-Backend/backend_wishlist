# Contributing to the Backend Wishlist

## For Frontend Agents — Requesting a Capability

### Before Requesting

1. Check `catalog.json` — maybe it already exists
2. Check `wishlist.json` — maybe it's already requested (upvote instead)
3. Check the robot SDK docs (`GET /code/sdk/markdown`) — maybe the method exists but you missed it

### Submitting a Request

Add an entry to `wishlist.json`:

```json
{
  "id": "short-kebab-case-id",
  "name": "Human Readable Name",
  "description": "What you need the backend to provide",
  "category": "api|sdk|model|service|infra",
  "requested_by": "your-agent-name",
  "reason": "Why you need it — what skill or task is blocked",
  "votes": 1,
  "status": "pending",
  "assigned": null,
  "completed_at": null
}
```

Then commit and push.

### Good Request Example

```json
{
  "id": "camera-aliases",
  "name": "Camera Alias Support",
  "description": "Allow using cam0/cam1 aliases instead of device serial numbers in yolo.segment_camera() and other camera SDK methods",
  "category": "sdk",
  "requested_by": "frank",
  "reason": "Serial numbers like 336222071022 are hard to work with; cam0/cam1 aliases are intuitive and less error-prone",
  "votes": 1,
  "status": "pending",
  "assigned": null,
  "completed_at": null
}
```

---

## For Backend Agents — Fulfilling a Request

1. **Claim it** — Set `status: "building"` and `assigned: "your-name"` in `wishlist.json`
2. **Implement** — Whatever is needed (new endpoint, model install, SDK extension)
3. **Document** — Update the robot server's SDK docs so frontend agents can discover it
4. **Update catalog.json** — Add the new capability with endpoints/methods
5. **Close it** — Set `status: "done"` and `completed_at` in `wishlist.json`
6. **Push** — Commit all changes

### Declining a Request

If a request isn't feasible:

1. Set `status: "wontfix"`
2. Add a `"reason_declined"` field explaining why
3. Push — the frontend agent will see the explanation
