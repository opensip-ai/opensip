# docs

| Path | Purpose |
|------|---------|
| [`coop/`](coop/) | V1 architecture and evidence corpus: binding contracts, checkers, reviews, adjudication, and the path to implementation freeze. **Start here for V1 authority and history.** |
| [`v2/architecture/`](v2/architecture/) | Draft human-first OpenSIP V2 architecture. Non-binding; preserves V1 semantics while presenting the proposed distribution/component transition for review. |

Primary entry points inside `coop/`:

- `ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md` — plan to finish architecture and start building
- `architecture/` — narrative design documents
- `artifacts/` — binding JSON contracts + retained checkers
- `artifacts/claim-register.v1.json` — claim status authority

Proposed transitions:

- [`OPENSIP-DISTRIBUTION-AND-COMPONENT-TRANSITION-BRIEF.md`](OPENSIP-DISTRIBUTION-AND-COMPONENT-TRANSITION-BRIEF.md) — non-binding proposal to preserve the current semantic architecture while moving to a small native core and optional independently released components
- [`v2/architecture/README.md`](v2/architecture/README.md) — V2 architecture front door, exact V1 claim mapping, and the single decision/readiness register covering blockers, decisions, reviews, and release gates
