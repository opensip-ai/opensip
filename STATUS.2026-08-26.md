# OpenSIP V2 architecture — status at 2026-08-26 (Claude orchestrator, after D-281)

Live HEAD `e4b20dd9` = D-281 (last COORD heading). File 08 digest `e503b75b…`. Git ahead of origin; not pushed.
Every number below was measured from file 08 / COORD bytes by independent readers and re-counted by an adversarial verifier.

## 1. Where the five readiness conditions stand (file 08, the only definition of "complete" — D-001)

| # | Condition | Standing | What the number really means |
|---|---|---|---|
| 1 | DR-001–011 SATISFIED or explicitly disposed | **MET (preview scope only)** | 1 of 11 SATISFIED (DR-001); 9 HARD-BLOCKED + 1 PARTIAL carry owner-recorded *preview* dispositions (D-058…D-083). Nothing blocked is settled; it is scoped around. |
| 2 | Every slice-affecting V2 row SATISFIED | **NOT MET — 5 of 32** | SATISFIED: DR-102 (Class A), DR-104, DR-115, DR-119, DR-123 (Class B). 3 rows deferred by disposition (DR-128/129/130). **24 slice-affecting rows remain** (22 OPEN, DR-118 DECIDED-V1-NOT-INTEGRATED, DR-107/122 PROPOSED-CLOSED-FOR-REVIEW). |
| 3 | DR-201–205 re-reviews ACCEPTED | **MET** | 5 of 5. |
| 4 | Gates named + owned; no unevidenced QUALIFIED | **MET (naming half)** | 28 of 28 required-now gates named; 32 of 32 owners; 0 QUALIFIED claims. Execution half is qualification work, not architecture. |
| 5 | Authorities authorize `docs/v2/implementation/` | **NOT MET — structurally last** | Directory absent; this is a separate PREFERENCE-LADEN act reserved to you (D-001). |

The handoff's own five-item completion bar (from your D-132 grant: DR-131, DR-133, DR-117 SATISFIED; Condition 2 MET; identity cited via D-077/D-078): **all five NOT MET** (identity citation exists only at candidate grade).

## 2. Why the 24 remaining rows cannot simply be marked SATISFIED

D-056 allows SATISFIED only when five eligibility gates hold. Two things block almost every remaining row:

1. **Gate 1 Class A is unopened.** DR-117, DR-131, DR-133 each have an independently accepted *candidate* contract, but every recording carries an express reservation ("CANDIDATE-NOT-APPLIED; Class A not opened"). COORD says the only venue for a lift is "a reviewed coordinator act, not an artifact" — a D-000 cycle recording *application-grade, no-express-reservation* (T2-02) acceptance. The file-08 owners of those rows are **Product owner** (DR-117), **Product + CLI/output** (DR-131), **Semantic/component architecture** (DR-133). D-001 classes DR-117 as a route-C PREFERENCE-LADEN product decision. **This is your decision, not a reviewer's.**
2. **Leftover-design remains on every other row** (71 obligations measured across the 38 current leftover-joins). D-056 clause 5: authoring fixtures is design work, so a row with unauthored fixtures is ineligible.

## 3. The remaining work, by who can do it

### A. Mechanical remasurement queue — AI does this, no decisions needed (in progress)
Occupancy-stale leftover-joins (they cite a superseded harness occupancy as the specification). Each act = author successor → dual Stage A ACCEPT 0/0 → COORD draft → dual Stage B CONSENT → COORD-only commit (~30–45 min per act when reviews pass first time).
1. component-manifest v6 → v8 (**in flight**: v7 was Dual REJECT on wording only, all three findings landed in v8, Stage A running)
2. permission v9 → v10 (G09 occupancy v3→v4) — generator ready
3. state-class v3 (G19 v1→v2)
4. doctor-actor v11 (G12 v4→v6, G21 v3→v4, G32 v1→v3)
5. exact-bytes v5 (G07 v3→v4)
6. distribution-core v7 (G01–G05 v1→v9/v4/v5/v4/v4) — not in Grok's handoff list but the same class; confirmed on bytes
7. identity-namespace v6 (G31 v2→v5) — **row already SATISFIED (D-236)**; remasuring is harmless but optional — your call
Not candidates: lifecycle/monorepo/signed-index/DR-117 joins only cite a superseded *GATE* join; COORD (D-276/D-278/D-281) explicitly keeps those current.

### B. Leftover-design an AI cycle could author *if the bytes were uniquely determined by closed types* — 39 obligations
Fixture authoring for ~20 gates (G07, G08, G09 ×14 FX classes, G12 ×12 FC, G14, G15/AT ×8, G16, G18, G19, G20, G21, G22, G24–G30, DR-114 JOIN ×13, DR-122 SARIF, DR-127 hostile goldens, DR-105 R-6/R-10) plus two schema successors (DR-103 unicode-norm, OD-2 fold).
Grok's standing judgment (handoff): "uniquely determined leftover-design of fixture bytes from closed types is exhausted — do not invent." I.e. **what is left requires choices** (envelope shapes, byte-sets, corpus contents) that the register does not determine. Closing these means either (a) you decide the shapes/inputs, or (b) you explicitly authorize the orchestrator to choose on your behalf under D-000 adversarial review, accepting the CONTESTED risk.

### C. Decisions only you (product/release/architecture authority) can make — 25 obligations + 10 parked contests
Reserved numbers and lists (each row stays OPEN until set):
- DR-112 quorum / clock-skew / emergency / waiver numbers (OD-112-1..4)
- DR-118 per-row language-quality thresholds + matrix corpus acceptance; G13 reserved gate
- DR-111 numeric reader-support windows
- DR-126 per-OS TCB allowlist tables / selectors
- DR-121 CI encodings (provider, YAML, path filters, caches, commands)
- DR-107 lifecycle encodings (atomic-rename equivalent, quarantine/journal format, lock grammar)
- DR-103 OD-1 owner assignment + size caps; DR-101 OD-101-1 core language (Rust-as-core not minted) / OD-101-2 signing ceremony; DR-115 D-006 unit & tree accounting; G07 filesystem coverage
- DR-105/DR-114 FC-C1 joint-owner recording and BLK-1..4 routing (D-032); DR-124 grant-journal assignment; DR-127 AL-1/2/5 & AL-3 execution routes
- DR-120 adapter implementations, DR-125 SDK APIs, DR-107/121 encodings are reserved to *after Condition 5* — implementation, not design
Parked CONTESTED entries batched to you (D-000 clause 2): D-017/019–024, D-051/052/053, D-059, D-067, D-094, D-095, D-098, D-099, D-101 (most were superseded by later ADOPTED successors — you need only confirm), and **D-272** (both reviewers found the orchestrator's fourth-turn dispatch a clause-2 breach; D-273 recorded the same subject in a new cycle — a ruling is needed).
Then: **Class A lifts for DR-117 / DR-131 / DR-133**, and finally **Condition 5**.

## 4. Honest bottom line
- The register is internally consistent and heavily cross-verified; the naming/ownership scaffolding (Condition 4) is done.
- Architecture completion is now **decision-bound, not effort-bound**: after the ~6 remaining mechanical remasurements, no further row can move without a product/architecture decision from you (numbers, lists, envelope shapes, Class A opening).
- Risk notes: (a) several artifacts cited by recorded joins are untracked in git (e.g. `at-named-corpus-catalog.v1.json`, `compatibility-leftover-join.v1.json`, `doctor-leftover-join.v1.json`) — recorded custody points at files git history does not hold; (b) Codex reports "1 usage limit reset available" — reviewer capacity may run out; (c) HEAD is ahead of origin and unpushed.

## 5. Suggested next decisions from you (cheapest first)
1. Confirm the mechanical queue order above (and whether to include identity-namespace).
2. Rule on D-272 and confirm the superseded CONTESTED entries.
3. Decide whether to open Class A for DR-131 / DR-133 / DR-117 (or state what you need to see first).
4. Pick which reserved numbers/lists you will set now vs. defer post-slice with an explicit disposition (a deferral disposition also satisfies Condition 2's wording for deferred items).
5. State whether the orchestrator may choose fixture shapes/byte-sets on your behalf (D-000 review) or whether you want to specify them.
