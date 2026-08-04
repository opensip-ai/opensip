# Map vs Control — product planes

**Status:** product boundary (guidance)  
**Date:** 2026-07-31  
**Scope:** greenfield OpenSIP (`opensip` repo) and relationship to shipping `opensip-cli`  
**Does not:** change binding coop contracts, claim-register, or v1-slice scope  
**Related:** [`coop/v1-slice.md`](coop/v1-slice.md) (control-plane first milestone), [`coop/TREE-ENDSTATE.md`](coop/TREE-ENDSTATE.md) (docs layout)

This document freezes the **two-plane** product model and naming guidance so future “Graft-like” work does not collapse into the evidence compiler.

---

## 1. One-line model

| Plane | Job | Must not |
|-------|-----|----------|
| **Control** | Measure, gate, and **prove** claims about a codebase under declared intent | Optimize primarily for chat-session token cost |
| **Map** | Orient, navigate, and **cheaply contextualize** a codebase for agents and humans | Mint authoritative policy outcomes or sealed Runs |

> **Control is the instrument. Map is the floor plan.**  
> Floor plans help you move; instruments tell you what is true.

Agents may use both. Only Control issues **authoritative** results (findings, baselines, D9 exit, sealed evidence).

---

## 2. Why two planes

Coding agents need:

1. **Orientation** — where is X, who calls Y, what do I open next, blast radius while editing (Graft-class).  
2. **Proof** — did rules fail, did we regress, can CI trust this offline without a model (OpenSIP-class).

Merging them into one muddled product causes:

- wrong defaults (LLM summaries treated as gates),
- confused exit codes (map-stale vs policy-fail),
- architecture forks (effectful “context inject” inside pure evaluation),
- brand dilution (OpenSIP becomes “another agent map”).

Keeping them **named and packaged as planes** (even if one monorepo) preserves the greenfield hard law: **no model calls on the Control product path**.

---

## 2A. Single installer, host, and “tools”

### 2A.1 The idea (user-facing)

One install. One command brand:

```text
opensip                  ← single installer / entrypoint
opensip run …            ← Control (built-in)
opensip map …            ← Map (first-party capability, later)
opensip <future> …       ← other first-party or admitted capabilities
opensip tools list|…     ← discovery / enablement (later)
```

That UX is **right**. It matches “extensible OpenSIP” without forcing users to install five binaries.

### 2A.2 The corrected ontology (architecture)

Do **not** model this as:

```text
opensip-core
  └── peer tools: [opensip-cli, map, fitness, …]   ← rejected shape
```

That is the old **“CLI that hosts five peer tools”** center. Architecture already seals the inversion: OpenSIP is an **evidence compiler over a project snapshot**. Producers feed it; surfaces project it; **the host is the only writer of durable authoritative state**.

Prefer:

```text
┌─────────────────────────────────────────────────────────────┐
│  opensip  (one install)                                      │
│  composition root + host shell + admission + surfaces        │
├─────────────────────────────────────────────────────────────┤
│  BUILT-IN CONTROL PATH (not an optional peer “tool”)         │
│  plan · snapshot · facts · pure core · seal Run · D9         │
│  host-owned evidence store                                   │
├─────────────────────────────────────────────────────────────┤
│  CAPABILITIES / CONTRIBUTIONS (extensible)                   │
│  first-party: map, optional profiles, later surfaces         │
│  third-party: admitted only under sealed extension rules     │
│  (v1: marketplace + untrusted imperative EXCLUDED)           │
└─────────────────────────────────────────────────────────────┘
```

| Layer | What it is | User says |
|-------|------------|-----------|
| **Host / shell** | One binary, one installer, admission, identity, storage root, MCP/CLI routing | `opensip` |
| **Control path** | The product center — analysis spine + seal + D9 | `opensip run`, `opensip show`, … (no need to type “control”) |
| **Pure core** | Library inside Control — not a user “tool” | never invoked alone |
| **Capability** | Optional or pluggable job (Map, future) | `opensip map …` |
| **Contribution / producer** | Emits facts or non-authoritative scores into a Plan | configured, not “peer CLI silo” |
| **Surface** | CLI, MCP, SARIF, HTML — projections | how you talk to the host |

### 2A.3 Where `opensip-cli` fits

| Framing | Verdict |
|---------|---------|
| **`opensip-cli` as a peer tool under a new core** | **No** — that freezes the old monorepo as a plugin and reintroduces tool-private persistence / peer silos |
| **`opensip-cli` as legacy package name for the shipping TS product** | **Yes** — transitional brand until cutover |
| **Greenfield: `opensip` binary = host + Control path** | **Yes** — `opensip-cli` is not a tool you install beside core; it is the historical name of “the product” |
| **CLI as a surface of the host** | **Yes** — TTY/JSON/MCP are projections, not separate products |

So: **one installer named OpenSIP; Control is built-in; Map is a future capability under the same installer; do not reify “opensip-cli” as a tool id.**

### 2A.4 Extensibility that stays compatible with sealed law

Architecture already allows extension **at the right altitude**:

| Extension kind | When | Authority |
|----------------|------|-----------|
| Fact / semantic providers | First-party TS+Rust in v1; more later under delivery rules | Facts only; host still seals |
| Declarative rules / packs | Grow after spine | Evaluated in pure core |
| Map capability | After Control dogfood | Structure/context; **not** sealed policy |
| Data-only workflow profiles | Product-gated | No extension-owned command code as authority |
| Untrusted imperative / WASM / marketplace | **Excluded until** restricted runtime + threat model | Must not write authoritative ledger |

**Hard rules (carry from product boundary):**

1. **No public in-process plugin ABI** as day-one security theater.  
2. **No tool-private authoritative persistence** — host owns the ledger.  
3. **Process boundary ≠ sandbox** unless confinement is real.  
4. **Marketplace is not v1.**  
5. Capabilities may be invoked as subcommands (`opensip map`) without being **peer products** that each seal their own truth.

### 2A.5 Command shape (illustrative, not frozen)

```bash
# Control (built-in) — default product
opensip run …
opensip show run …
opensip baseline …

# Map (capability, later) — same installer
opensip map build
opensip map ask "…"
opensip map check

# Discovery (later)
opensip tools list          # or: opensip capabilities
opensip tools enable map    # if Map is optional install component

# MCP: one host can expose multiple capability namespaces
opensip mcp                 # Control tools + (later) map_* tools, clearly prefixed
```

Optional install components under one brand are fine (`opensip` full profile includes Map later; minimal profile is Control-only). That is **delivery packaging**, not “five peer tools with five stores.”

### 2A.6 Decision on the user’s proposal

| Proposal element | Decision |
|------------------|----------|
| One installer: just `opensip` | **Accept** |
| From `opensip`, run Map and future capabilities | **Accept** |
| Extensible for full other tools | **Accept with tiers** — producers/capabilities under admission; not ungoverned peer CLIs |
| Core + tools model | **Accept if “core” means host+Control path**, not a thin dispatcher |
| `opensip-cli` as a tool among peers | **Reject** — legacy name / surface, not a plugin id |
| Control as optional peer tool equal to Map | **Reject** — Control is built-in product center; Map is optional capability |

---

## 3. Control plane (now)

### 3.1 Product center

Local-first, deterministic **evidence-and-enforcement control plane**:

`intent → analysis → evidence → surfaces`  
First vertical slice: admit → PlanId → snapshot → facts → pure core → seal Run → D9.

Binding scope for the first milestone: [`coop/v1-slice.md`](coop/v1-slice.md).

### 3.2 In (Control)

| In | Notes |
|----|--------|
| Config resolve, PlanId, plan validate | Host-owned admission |
| Snapshot + fact derivation (TS + Rust providers) | Predicate-relative sufficiency (C-1) |
| Pure evaluation core → `policyOutcome` | No effectful ports, no entropy minting |
| Seal Run + durable evidence path | Host seals; D9 terminates |
| Baselines / pivot compare (when in slice) | Versioning ship-gates apply |
| CI / exit codes / machine JSON as first-class | Agents and CI are clients |
| MCP/CLI **projections of sealed or store-backed results** | Graph tools OK when they answer from analysis state |

### 3.3 Out (Control) — do not grow these into the core

| Out of Control core | Belongs on Map (later) or never |
|---------------------|----------------------------------|
| “Inject repo map into every agent turn” as product center | Map |
| LLM concept-node / prose architecture graph as truth | Map optional enrichment only; never Control authority |
| Session prefs, goals, multi-agent memory pool | Out of both → companion memory (e.g. ai-knot class) |
| Probe / untrusted imperative / scenario effects | Parked per architecture until contracts exist |
| Resident multi-project daemon as default | Parked / measurement-gated |

### 3.4 Success metrics (Control)

- Reproducible Runs and PlanIds  
- Correct D9 termination  
- Offline verdict without model calls  
- Baseline/regression semantics  
- Evidence readable from a second process  

**Not** primary: agent tool-call count or session wall-clock (those are Map metrics).

---

## 4. Map plane (future — not v1)

### 4.1 Product center

Local, refreshable **structural context** so agents (and humans) stop re-onboarding every session.

Inspired by Graft-class tools; **OpenSIP-native** differentiator: Map may **cite** Control evidence, never replace it.

### 4.2 In (Map) — when built

| In | Notes |
|----|--------|
| Structural extract (tree-sitter and/or shared providers) | Default path: **no LLM** |
| Symbol / file graph: callers, callees, depth-N blast radius | Working-tree aware refresh |
| Repo map / hubs / hotspots | Token-budgeted orientation |
| Cheap lexical or structure-seeded rank (“ask” / find) | No embeddings required on default path |
| Freshness check (map vs tree) | Exit code = *map drift*, not policy fail |
| MCP tools optimized for agent explore loops | Separate server name or tool prefix |
| Optional agent wiring (hooks, statusline, init) | Product packaging, not Control law |
| Optional LLM enrichment (`--deep`) | Explicit, never auto-required; never authoritative |

### 4.3 Out (Map)

| Out | Why |
|-----|-----|
| Sealed Runs, policy outcomes, D9 | Control only |
| CI gate semantics (“fail build on finding”) | Control only |
| Claiming map prose is “the architecture of record” | Trust collapse |
| Untrusted imperative rules / Probe | Same park list as Control |
| Long-term agent memory / prefs | Separate memory product class |

### 4.4 Success metrics (Map)

- Fewer explore tool calls / tokens / latency for agent tasks  
- Freshness lag (map vs working tree)  
- Correct structural edges for supported languages  
- Agent can open file:line without full-file thrash  

**Not** primary: sealed evidence quality (Control).

### 4.5 Timing

| When | Map work |
|------|----------|
| **Now → freeze + Control vertical slice** | **Do not build Map product** |
| After offline Control spine works | Optional: improve Control MCP **projections** (who-calls from facts/evidence) |
| After dogfood shows agent explore gap remains | Spike Map plane (shared extract, separate surface) |
| Only with explicit product acceptance | Ship Map as companion CLI/MCP |

**Default path before Map ships:** document coexistence with external Graft-class tools if users need explore UX immediately.

---

## 5. Authority and trust boundary

### 5.1 Authority order (agents and humans)

1. **Sealed Control evidence + policy outcome + D9**  
2. **Control store-backed analysis results** (runs, findings, baselines)  
3. **Map structural graph** (symbols, edges, spans)  
4. **Map optional LLM prose** (summaries, concept nodes)  
5. **Agent memory / chat** (out of band)

If (4) or (5) conflicts with (1)–(2), **Control wins**. Map and memory must not gate CI.

### 5.2 One-way glue (allowed later)

```text
Control Run sealed
    │
    ▼ optional one-way
Map or agent memory may store a *citation*
  ("opensip run R: N new findings on auth")
    │
    ✗ never
Control Plan/Run admission must NOT require Map or memory
```

### 5.3 Exit codes (do not conflate)

| Domain | Example meaning |
|--------|-----------------|
| Control | Policy fail, coverage indeterminate, admission rejected |
| Map | Graph missing, map stale vs tree, unsupported language |

A Map freshness failure must **not** reuse Control’s “analysis failed” semantics without an explicit, separate code family.

---

## 6. MCP / CLI surface split

### 6.1 Control surfaces (v1 and ongoing)

Illustrative — exact names follow implementer package / freeze:

| Kind | Examples |
|------|----------|
| Lifecycle | admit/run, show run, list runs |
| Evidence | show findings, baseline compare |
| Structure-as-evidence | who-calls / impact **when backed by Control facts** |
| Termination | D9-derived process exit |

### 6.2 Map surfaces (future)

| Kind | Examples |
|------|----------|
| Orient | map, hubs, hotspots |
| Navigate | find_code / ask, file_api / skeleton |
| Structure | trace_calls, callers depth-N |
| Search | grep-by-symbol coupling |
| Hygiene | check_freshness (map drift) |

### 6.3 Shared code (intended later)

| Share | Keep separate |
|-------|----------------|
| Language extract / symbol IR where possible | Host orchestration and Run seal (Control only) |
| Path identity, project root rules | Policy evaluation pure core |
| Fingerprint / incremental parse cache ideas | D9, evidence custody, retention |
| Some graph walk algorithms | Agent hook installers, statusline, markdown concept graph |

**Rule:** one parse, two projections — when Map exists. Until then, Control may expose limited structure tools without becoming Map.

---

## 7. Naming

### 7.1 Recommendation (binding guidance for this repo)

| Role | Name | Rationale |
|------|------|-----------|
| **Umbrella brand + single installer** | **OpenSIP** / **`opensip`** | One entrypoint; host shell + built-in Control |
| **Control plane (built-in path)** | Commands under **`opensip`** (run/show/…) | Users need not say “control”; docs still say Control |
| **Internal plane label** | **Control** | Architecture precision |
| **Map capability (future)** | **`opensip map …`** (preferred) or optional component | Same installer; not a second brand day one |
| **Extensibility word** | **capability** / **contribution** / **producer** | Prefer over peer **tool** for first-party jobs; “tool” is OK in MCP/UX slang only |
| **This greenfield repo** | **`opensip`** | Already correct |
| **Shipping TS monorepo** | **`opensip-cli`** (historical package) | **Not** a future plugin id under core |

### 7.2 Should we rename to `opensip-control`?

**No as the default user-facing name.**

| Option | Verdict | Why |
|--------|---------|-----|
| **`opensip-control` as primary CLI/npm name** | **Avoid** | “Control” is internal architecture jargon; longer; weak discovery; implies a multi-product suite users must learn on day one |
| **`opensip` = Control (default)** | **Yes** | Instrument is the product; Map is optional add-on |
| **`opensip-cli` forever** | **Transitional only** | “CLI” undersells MCP/CI/agent surfaces; fine as legacy package id until cutover |
| **`opensip-map` / `opensip map`** | **Yes when Map ships** | Symmetric, job-shaped, does not rename Control |
| **`opensip-core` for pure evaluation crate** | **Yes (Rust crate)** | Crate-level name, not product binary |
| **`opensip-host` / `opensip-cli` crate** | **OK** | Composition root; binary can still be `opensip` |

**Rule of thumb:**

- **Product / binary / npm:** short job or brand (`opensip`, `opensip-map`).  
- **Docs / architecture:** plane names (`Control`, `Map`).  
- **Crates / packages:** technical (`opensip-core`, `opensip-host`, `opensip-facts`).  

Do **not** rename the user-facing command to `opensip-control` unless you deliberately market a suite of peer products (Control, Map, Cloud, …) and accept the naming tax.

### 7.3 Suggested future package layout (illustrative)

```text
opensip/                          # single product / installer brand
  crates/cli                      # `opensip` binary (host shell)
  crates/host                     # orchestration, admission, seal, D9
  crates/core                     # pure evaluation (not a user tool)
  crates/plan, facts, evidence, …
  crates/map                      # Map capability (later; same binary or feature)
  # optional: feature-flag or package component "map" in the installer
```

Separate `opensip-map` binary is optional packaging; **default recommendation is same binary, subcommand namespace**, so “one installer” stays true.

### 7.4 What *not* to call Map

| Name | Avoid because |
|------|----------------|
| `opensip-graft` | Competitor’s brand; sounds derivative |
| `opensip-context` | Vague; everything is “context” |
| `opensip-agent` | Implies the agent product is OpenSIP |
| `opensip-graph` alone | Collides with Control graph projections; under-specifies job |

Prefer **Map** / **Orient** / **Explore** — **Map** is short and dual-use (human + agent).

---

## 8. Competitive adjacency (external)

| External | Plane | Stance |
|----------|-------|--------|
| [Graft](https://github.com/NanoNets/Graft) | Map-class | Learn UX; coexist or compete only on explore; do not copy LLM concept-as-truth |
| [ai-knot](https://github.com/alsoleg89/ai-knot) | Agent memory | Coexist; not Map, not Control |
| Memoria-class | Agent memory + heavy DB | Generally out of scope for OpenSIP core |

Positioning line:

> **Graft-class tools help agents look. OpenSIP decides and proves.**  
> **OpenSIP Map (if shipped) is our floor plan — never our verdict.**

---

## 9. Decision checklist

Use this before any PR that “adds Graft-like features” or “plugin tools”:

- [ ] Does this change **mint or alter** policy outcomes, sealed Runs, or D9? → **Control only**; Map must not.  
- [ ] Does this require a **model on the default path**? → Forbidden for Control; Map only if opt-in and labeled non-authoritative.  
- [ ] Is the success metric **agent token cost**? → Map (later), not Control freeze work.  
- [ ] Can this wait until Control vertical slice works offline? → **Yes → wait.**  
- [ ] Are we renaming the default binary to `opensip-control`? → **No** (see §7).  
- [ ] Are we making Control a **peer optional tool** next to Map? → **No** (see §2A).  
- [ ] Are we reintroducing **tool-private authoritative stores**? → **No**.  
- [ ] Is “extension” really a **contribution/producer** under admission, or an ungoverned CLI silo? → Prefer contribution.

---

## 10. Change log

| Date | Change |
|------|--------|
| 2026-07-31 | Initial Map vs Control boundary + naming guidance (`opensip` default; Map later; avoid `opensip-control` as primary user name). |
| 2026-07-31 | §2A: single installer / host shell; Control built-in; Map as capability; reject `opensip-cli` as peer tool id. |
