# Coordinator Decision Register

Every decision made on the user's behalf under the delegation protocol is
recorded here, in order, with its rationale, its adversarial review, its
reversibility class, and its overturn procedure. This file is the surface the
user reviews later; nothing decided under delegation lives only in
conversation.

Entry format: id, date, title, status, decision, alternatives considered,
rationale, reviewer + verdict + digest, decision type
(`MECHANICAL` | `RULE-GOVERNED` | `PREFERENCE-LADEN`), reversibility, overturn
procedure, commit.

Statuses: `ADOPTED` (consensus reached or user-made), `CONTESTED` (no
consensus after 3 turns each; parked for the user), `SUPERSEDED`,
`OVERTURNED`.

---

## D-000 — Delegation protocol adopted

- **Date:** 2026-08-12
- **Status:** ADOPTED (made directly by the user in conversation; no subagent
  review required — the delegation itself is the user's decision, recorded
  here verbatim rather than made on their behalf)
- **Decision:** The assistant completes the coop design end-to-end, making
  coordinator/product-authority decisions on the user's behalf, under these
  terms:
  1. Any decision that would have needed the user is put to an ADVERSARIAL
     subagent review (prompted to refute, not confirm), iterating to
     consensus.
  2. **Termination clause: 3 turns each side.** If no consensus after three
     exchanges per party, the decision is recorded `CONTESTED` with both
     positions, parked, and batched to the user; work proceeds on other
     surfaces. A forced consensus is never recorded as consensus.
  3. Every such decision is documented in this register — decision,
     alternatives, rationale, reviewer verdict with digest, reversibility
     class, overturn procedure.
  4. **Commit and push per decision** (user amendment 2026-08-12), so the
     user can roll back or cherry-pick at decision granularity. Commits land
     on `main` (`origin` = github.com:opensip-ai/opensip), matching the
     corpus's existing history.
  5. Decisions that turn on the user's preferences rather than on judgment
     are additionally marked `PREFERENCE-LADEN`, and their overturn
     procedure is written to cost less than the decision did.
- **Sequencing note (standing):** `artifacts/check-completeness.py` and
  `artifacts/check-completeness-v2.py` are EXCLUDED from commits until the
  in-flight independent review of the dialect repair completes — that
  review's dispatch pins the pre-edit instrument bytes via
  `git show HEAD:docs/coop/artifacts/check-completeness.py` (`6c52a5f9…`) and
  `…check-completeness-v2.py` (`b08824e8…`); committing them mid-review would
  break its verification instruction. They commit, with their review, when it
  lands.
- **Reversibility:** the protocol itself is revocable by the user at any
  message; per-decision commits are individually revertible by design.
- **Commit:** the delegation-baseline commit accompanying this file.

---

## D-001 — Definition of "completed" for the V2 design

- **Date:** opened 2026-08-12; scope set by the user mid-conversation: the
  completion target is the V2 design, anchored at
  `docs/v2/architecture/08-decision-and-readiness-register.md`
  (sha256 `528cab56ae2459876a1c17a60c11681eaa3190849dc9c2ad3d253d31f1cfce8a`).
  Draft synthesized from a six-reader register verification against live
  corpus bytes at HEAD `0ada5b3` (freeze `e4797f47…`, blueprint `a8c16cca…`,
  claim register `95097b3f…`), persisted as
  `docs/coop/artifacts/v2-register-verification.v1.json`
  (`172cffb47319123aaa0c2d03e889cfedae00675680dc65b1eb61ee9216ccbc2b`) so
  every citation below is auditable from corpus bytes (adversarial review
  MF-7). HEAD has since advanced (v10, `4cfd9d4`); route texts below are
  written head-relative for exactly that reason (reviewer NOTE-2 / freeze
  §7.10: pin properties, not current values).
- **Amended 2026-08-13** in response to the turn-1 adversarial review
  (`coordinator-decisions.D-001.review-adversarial.json`, `6de5a03b…`,
  OBJECTIONS: 8 MUST-FIX, 4 SHOULD-FIX, 2 NOTE — every objection accepted;
  none rebutted).
- **Status:** **ADOPTED 2026-08-13** — consensus reached under D-000 at turn
  3 of 3: final verdict CONSENT, on the merits, at
  `artifacts/coordinator-decisions.D-001.review-adversarial.turn3.json`
  (`97b20341…`). Three non-blocking observations are recorded in that
  verdict, including one routed onward: the applied EIR v6 rests on a
  candidate-grade warrant — the class the route-A acceptance property now
  forbids prospectively — flagged as DR-204/DR-011 audit material.
- **Decision type:** RULE-GOVERNED in its adoption (the checklist already
  exists and is the register's sole active one — verified: no topic doc
  maintains a competing list); PREFERENCE-LADEN in the specific routes marked
  in §4 below. This entry does not hide the second kind inside the first.

### 1. The definition of done

D-001 adopts the five-condition **Blueprint-readiness decision** of register
file 08 as the complete and only definition of "completed" for the V2 design,
quoted byte-for-byte from the register (MF-1 — the previous draft
paraphrased while claiming verbatim, dropping condition 3's guard sentence
and DR-012's "or authoritative launch"):

> Readiness requires all of the following in this register, and this
> paragraph is the only active readiness checklist:
>
> 1. DR-001 through DR-011 are `SATISFIED` or the owning V1 authority records
>    an explicit, scoped, reviewed pre-blueprint disposition that names what
>    may be designed without pretending the blocked semantics are settled.
>    DR-012 is not a blueprint-entry prerequisite; it remains mandatory
>    before release or authoritative launch.
> 2. DR-101 through DR-127 that affect the first blueprint slice are
>    `SATISFIED`; deferred items have explicit product/architecture scope
>    dispositions.
> 3. Each DR-201 through DR-205 re-review is `ACCEPTED`; alternatively, every
>    rejecting finding is individually identified, closed or lawfully routed
>    to an owning authority/register item, and backed by retained evidence.
>    Merely receiving a rejecting disposition never satisfies this gate.
> 4. Required release gates have named harnesses and owners; no document
>    claims `QUALIFIED` or `DEMONSTRATED` without retained evidence.
> 5. Product and architecture authorities explicitly authorize creation of
>    `docs/v2/implementation/` against a refreshed exact authority baseline.

Completion is an evidence state, not a declaration. Measured starting
position (HEAD `0ada5b3`): condition 4's claims half is ALREADY satisfied
(zero affirmative QUALIFIED/DEMONSTRATED claims in docs/v2; the obligation is
continued abstinence); condition 3 stands at zero of five re-reviews
dispatched; condition 4's harness half at 0 of 22 named; condition 5's
precondition holds (`docs/v2/implementation/` absent); condition 1 has one
row satisfied-but-reopened (DR-001 — the baseline drifted 28/31 through
lawful post-anchor session work and its own scope clause re-opens it), one
partially satisfied (DR-008), nine hard-blocked, and DR-011's 16-row
subledger (R07 NARROWED, the rest OPEN).

### 2. D-002 isolated: the first blueprint slice

Conditions 2 and 4 quantify over "the first blueprint slice," which no
document defines (measured: referenced in files 07/08/10, defined nowhere).
That selection — commands, language roles, closures, statefulness — is
preference-laden, though not unbounded (SF-2): the register already fixes
part of the space — DR-123 makes the CLI baseline mandatory for every
slice, DR-128 excludes third-party/untrusted scope from MVP, DR-129 makes a
TUI optional and projection-only, and file 10 bounds MVP scope. D-002
selects within those recorded bounds and cannot quietly relitigate them.
It is isolated as **D-002**, sequenced FIRST among product asks because
DR-118, DR-108, DR-G13 and readiness conditions 2/4 are unevaluable until
it lands. D-001 deliberately smuggles no slice choice.

### 3. Closure routes, per row

Three lawful routes: **(A)** V1 successor through the coop process (author →
independent review → coordinator apply → freeze/claim-register motion);
**(B)** an explicit, scoped, reviewed pre-blueprint disposition (condition
1's own alternative); **(C)** a product decision through the
product-disposition process.

**Condition 1:**
- **DR-001** route A, two stages (MF-8): regeneration of both manifests at
  HEAD is mechanical and may run now, recorded as MEASURED; the SATISFIED
  re-record happens only after DR-204's re-review audits the disposition —
  re-recording before it would repeat the exact provenance defect D-001
  flags (SATISFIED requires independent review; the 2026-08-12 disposition
  was coordinator-recorded without one).
- **DR-002** route A: `evidence.v11` disposing EV10-IR-01..03, carrying
  `sealedCapabilityContract`/`availabilityDifferential`. The item-4 carrier
  choice — route (b) evidence.v11 versus route (a) retention v29 restore —
  is RECOMMENDED (b) here but DECIDED only at its own D-000-reviewed entry
  (SF-4: previously pre-selected in one section and parked open in another).
  Reviewer NOTE-1 adopted as a standing instruction: the successor's checker
  must not be named `check-evidence-v11.py` — that name is already taken by
  v10's own checker (the corpus's recorded naming trap); the new instrument
  carries an unambiguous name and the change record says why.
- **DR-003** route A, stated completely (SF-1): applying the reviewed
  `v10-disposition.v4` is necessary but NOT sufficient — its own PASS review
  states it "ADJUDICATES NOTHING" and leaves one item NOT DISCHARGED; the
  row closes only with the V10/custody + G19 demonstration and TM's final
  disposition recorded by the owning authorities.
- **DR-004** route A: the exact eight-bullet Phase-1A packet; plus commission
  the missing §3.1-item-to-supplier binding instrument.
- **DR-005** route A joint (evidence + storage + operability).
- **Standing route-A acceptance property (T2-02),** stated once and
  referenced wherever a candidate's applicability is at issue: a candidate
  is applicable when its independent review returns **0 blockers AND grants
  application-grade acceptance with no express reservation** — no
  candidate-only limitation, no EXPRESSLY-NOT-FOR-APPLICATION language, no
  named apply-condition left undischarged on the record — and the
  coordinator then applies per route A. "0 blockers" alone is measured
  insufficient by three corpus precedents (EIR v6: accepted as CANDIDATE
  only; delivery.v5: expressly not for application; r1 v1.9: apply-condition
  chain), so the weaker phrase is struck everywhere.
- **DR-006** route A, head-relative (MF-2, corrected per T2-01's census):
  acceptance of the evidence-identity lineage head satisfying the route-A
  acceptance property. Measured lineage at this amendment: v6 reviewed
  **ACCEPT AS A CANDIDATE, 0 blockers** (`7a0d93e4…`) and APPLIED
  2026-08-12; v1–v5 and v7–v10 REJECTED; v11 (`cf273bf5…`) is the head,
  under review. Then binding per-surface recipes; the §7.1 PROPERTY is the
  boundary.
- **DR-007** route A: D9 successor to v1.14.
- **DR-008** posture CLOSED; join half via DR-002/004; the checker review
  (R07 dispatch) closes the checker residual.
- **DR-009** route A, gated on DR-204's adjudication of the dialect-repair
  review's date anomaly before reliance.
- **DR-010** route C PREFERENCE-LADEN (P-1/P-2/G3 successor, jointly with
  DR-117 and R16).
- **DR-011**, all sixteen residuals routed by name (MF-4):
  R01 FACT-PLANE successor closing subject-set agreement, the sufficiency
  `view` type and the `rungUnavailableBecause` vocabulary with a refreshed
  D9 join, or a reviewed scoped disposition keeping facts/Coverage design
  blocked (depends DR-006/007). R02 FACT-IDENTITY: close or lawfully
  preserve every checker-declared limitation (13/14 implementable;
  capability property NOT DISCHARGED) with exact corpus/authority evidence —
  its own route, owned by the fact-identity surface. R03 C2 checker
  standing: instrument-review dispatch (`check-c2-v12.py`) plus pinned
  effective-checker standing. R04 DELIVERY (MF-3): a successor discharging
  the §7.1 disqualifier its own review names — that review is EXPRESSLY not
  an application warrant — or a scoped disposition retaining OBS-1 (the
  contestable half); "apply delivery.v5" is struck as unlawful. R05 protocol
  adjudication of PC-7 preserving the merged-major-2 demarcation. R06
  EVIDENCE residuals: closes with the DR-002 chain. R07 retention checker
  review dispatch; join half with DR-002/004. R08 D9 advisories and the
  three contract gaps: the DR-007 successor. R09 R-1 (T2-03, head-relative
  with the apply-condition chain named): application of the r1 lineage head
  satisfying the route-A acceptance property — at this writing v1.9, whose
  review's express condition (DO-NOT-APPLY-UNTIL-CORPUS-RESOLVER-CHECK) is
  discharged on the record at corpus-resolution.v1 (REFUSED, pre-repair) →
  corpus-resolution.v2 (POSITIVE, whose instrument-reliance caveat chains
  into the DR-204 gate, = DR-009's gate) — plus retained-validator standing
  and CIR-B1 closure.
  R10 the final blind consumer-B litmus — structurally LAST. R11
  OPERABILITY G19: the DR-005 successor. R12 evaluation-proof BOTH halves
  (MF-4): the v8 claim-shape obligation reconciled separately AND v13's
  19 limitations + 7 observations + 4 escapes individually closed or
  lawfully disposed. R13 VERSIONING successor covering stale D9, RC-14, the
  name collision, rejected v14–v16 and unreviewed v17. R14 RESOLVED-INPUTS
  stale-note reconciliation — rule-governed, not mechanical (T2-04,
  implementing the accepted turn-1 objection's named half): the
  reconciliation must not reopen the resolved CFG-6 threat root nor mask
  live TM blockers, so it is recorded as a disposition with that scope
  stated, never made as a silent edit. R15 TRUSTED-REQUEST-CONTEXT:
  the DR-006 lineage under the §7.1 property. R16 with DR-010/DR-117
  (route C). Parent DR-011 reconciles only after new rows open for the
  2026-08-12/13 lineage motion.
- **DR-012** excluded from completion per the register's own text (quoted
  above): not a blueprint-entry prerequisite; mandatory before release or
  authoritative launch.

**Condition 2 — all 29 rows classified (MF-5 closed the DR-108 gap):**
product decisions (route C, PREFERENCE-LADEN): DR-104, DR-115, DR-116,
DR-117, DR-118, DR-119, DR-123, DR-128, DR-129. Rule-governed architecture
authoring with review: DR-101, DR-102, DR-103, DR-105, DR-107 (+DR-G18),
DR-110, DR-111, DR-112, DR-114, DR-120, DR-121, DR-122, DR-125, DR-126,
DR-127. Inherit-blocked: DR-106, DR-109, DR-113, DR-124 (its evidence
class). **DR-108** slice-conditional: decided if and only if D-002's slice
includes credential-requiring features, else it receives an explicit
deferral disposition — named here so its handling is never silence.
Register-content changes are DECISIONS, not hygiene (MF-6): the V1→V2
transition-contract row (V2TOPIC-F-02) and the DR-117 widening to file 02's
seven binding items (V2TOPIC-F-04) each get their own D-000-reviewed entry
and commit. New-row rule (SF-3): condition 2's quantifier is evaluated over
the register as it stands at readiness evaluation; adding a row is itself a
reviewed decision under this protocol, so the quantifier can only grow by a
recorded act, never by drift — and because the quoted condition's literal
text reads "DR-101 through DR-127," the C4a commit that adds a row MUST also
amend file 08's condition-2 wording through the register's own process, so
the checklist text and the register never disagree (turn-2 NOTE-1). Only
V2TOPIC-F-01 (a stale prose recital) and
status-label normalization are hygiene. Items D-002 excludes get explicit
deferral dispositions, never silence.

**Condition 3:** dispatch all five adversarial re-reviews against the frozen
digests recorded by the verification (DR-201: file 01 @ `40ab9a3e…`; DR-202:
04 @ `fcb70d2f…` + 03 @ `52158469…`; DR-203: prototype ref @ `69a71aac…` +
05 @ `1a57c9ca…`; DR-204: baseline/pin apparatus — must audit DR-001's
disposition, verify-then-move the six stranded `e1cdb71d…` pins, correct the
pin-move record's two measured defects (the unanchored `4314af9e…` digest;
the factually false "unresolvable" claim about the matrix-L45 stdout
digests, which reproduce byte-exactly), and adjudicate the future-dated
instrument review; DR-205: 02 @ `1811c682…` + 10 @ `5378cdba…`).

**Condition 4:** claims half — maintain abstinence. Harness half — after
D-002 fixes the required set: one named harness identifier per required gate
under its named owner; fix DR-G16's vague owner cell; DR-G10's selector
refresh + a named V2 runner over pinned goldens; DR-G17's named parity
runner; DR-G13 waits on DR-118. DR-G06/G11 may be named now but execute only
after the condition-1 chain.

**Condition 5:** the final authorization is a separate PREFERENCE-LADEN act,
taken under D-000, adversarially reviewed, staged as the last commit so
reverting it costs one `git revert`.

### 4. Honesty about preference

Decided only via D-000 adversarial consensus or parked CONTESTED: D-002;
DR-010/DR-117/DR-011-R16; DR-104; DR-115; DR-116; DR-118; DR-119; DR-123;
DR-128; DR-129; the item-4 route choice (a vs b); OBS-1 retention in R04;
reliance timing on the future-dated instrument review; the condition-5
authorization itself. Everything else closes on evidence.

### 5. Staged commit plan (D-000 clause 4)

C1 `D-001 adopted`; C2 `D-002 slice` (or CONTESTED parking); C3 `DR-001
manifests regenerated @ HEAD — MEASURED, disposition pending DR-204`
(MF-8: the SATISFIED re-record is a separate later commit, after DR-204);
C4 `register hygiene` — ONLY genuinely mechanical items (MF-6): pin-move
record corrections, the six verify-then-moves, V2TOPIC-F-01's stale-prose
fix, status-label normalization; C4a and C4b: V2TOPIC-F-02 (new transition
row) and V2TOPIC-F-04 (DR-117 widening) as separate D-000-reviewed decision
commits; C5..C9 one per re-review disposition; onwards one commit per
product decision, per V1 apply/acceptance, per V2 decision closure, per
gate-naming batch (grouped by owner); matrix/baseline refresh commits after
each head repoint; C-final `Blueprint-readiness: conditions 1–5 evaluated;
docs/v2/implementation authorized` — standalone, last, trivially
revertible.

### 6. Reversibility and overturn

Every commit individually revertible. Preference-laden entries carry an
overturn procedure cheaper than the decision: one-line register supersession
plus `git revert` of the single commit. Overturning D-001 itself means
recording a successor definition of done here; nothing hard-codes this
checklist anywhere but the register that already owned it.

- **Reviewer (D-001):** adversarial review under D-000. Turn 1: OBJECTIONS (8
  MUST-FIX, 4 SHOULD-FIX, 2 NOTE) at
  `artifacts/coordinator-decisions.D-001.review-adversarial.json`
  (`6de5a03b…`); all fourteen accepted and amended, none rebutted. Turn 2:
  OBJECTIONS narrowed to 2 MUST-FIX + 2 SHOULD-FIX + 2 NOTE at
  `artifacts/coordinator-decisions.D-001.review-adversarial.turn2.json`
  (`82484bf6…`), with 12 of 14 turn-1 items RESOLVED-VERIFIED against bytes
  and a recorded expectation of CONSENT; all four turn-2 items accepted and
  amended above (T2-01 lineage census corrected, T2-02 route-A acceptance
  property adopted as standing, T2-03 R09 chain named, T2-04 R14
  reclassified), plus turn-2 NOTE-1's file-08 wording rule (the verdict
  file's id for it is ADV-D001-T2-05 — citation note per turn 3). Turn 3:
  **CONSENT**, on the merits, all four items verified against bytes
  (`…turn3.json`, `97b20341…`).
- **Commit:** C1 (this commit), with the verification artifact and all
  three verdict files.

---

## D-002 — The first blueprint slice

- **Date:** opened 2026-08-13, per D-001 §2 (the slice is referenced by
  readiness conditions 2 and 4 and defined nowhere; its selection is
  preference-laden and sequenced first among product asks).
- **Status:** **ADOPTED 2026-08-13** — consensus reached under D-000 at
  turn 3 of 3: final verdict CONSENT, on the merits, at
  `artifacts/coordinator-decisions.D-002.review-adversarial.turn3.json`
  (`a15f9ac2…`). The verdict records OBS-T3-01 against the coordinator's
  process (twice this lane, a report ran slightly ahead of bytes; reports
  must trail measurements — absorbed as standing discipline: register
  edits land before messages send).
- **Decision type:** PREFERENCE-LADEN (route C), decided on the user's
  behalf under D-000. Bounded, not free: DR-123 makes the CLI baseline
  mandatory for every slice; DR-128 excludes third-party/untrusted scope
  from MVP; DR-129 makes a TUI optional and projection-only; file 10's
  scope map and the pinned prototype evidence (`prototype-evidence-reference.md`,
  commit `a62509d6…`) bound the candidate space. D-002 selects within
  those recorded bounds.

### The slice: "Trusted TypeScript analysis — CLI-first, offline, contained"

**Commands:** `analyze` (non-interactive project analysis), `doctor`
(read-only/no-network default, consented probes), plus the trivial
`--help`/`--version` surfaces DR-G03 already names. Stable human and
machine (JSON) output for every command; **SARIF 2.1.0 advertised for
`analyze` only** (DR-122's preserved-projection shape; DR-G17 gates then
apply to exactly that surface). SARIF's parity evidence requires canonical
Run/Finding IDs — parked identities; see the Identity-dependencies section
below (MF-01).

### Identity dependencies — named, not avoided (turn-1 MF-01/MF-02)

The previous draft claimed the slice "touches nothing the V1 chain blocks";
that was FALSE on the freeze's own bytes, and the honest structure is
better: readiness condition 1 requires DR-001..011 SATISFIED or lawfully
disposed BEFORE any blueprint starts, so the slice does not need to avoid
parked identities — it needs to NAME which of its features ride which
condition-1 closure, presuming nothing settled now:

- **SARIF for `analyze`** rides DR-006's closure of the RunId derivation
  recipe and the Finding fingerprint (§7.1 parks both). If DR-006 closes by
  scoped disposition rather than binding recipes, SARIF drops from slice 1
  by that disposition's terms.
- **The rebuildable cache/index state class** rides the parked
  cache/regeneration-key recipes (DR-006).
- **Coverage on the TypeScript provider dispatch path** rides the parked
  `subjectScopeCommitment` (DR-006).
- **PlanId for the TypeScript role** rides a producing rule for
  `typescriptStdlibMerkleRoot`, which the freeze records as PlanId-affecting
  with no rule (DR-006's park-coverage property).
- **Doctor's D9 mapping (DR-114) and containment goldens (DR-G21)** ride
  DR-007's successor closing the observation→faultCause gap.

Every one of these is already in D-001's condition-1 routes; the slice adds
no new blocker and settles none of them by prose. The SARIF consequence
clause holds SYMMETRICALLY for all five rides (T2-04): if any named
condition-1 closure lands by scoped disposition rather than binding
recipes, the dependent feature — including the three rides under `analyze`
itself — ships reduced, re-scoped, or waits, by that disposition's terms;
none of them survives on prose.

**Language roles:** **TypeScript, alone.** The prototype's strongest
inventory; DR-119 names it as the role that "must not require user-managed
Node." D-002 selects the slice-1 role set; it does NOT close DR-118, which
still requires the capability/parity matrix, digest-pinned corpus and
thresholds for this one role.

**Components:** first-party/explicitly-trusted only (DR-128's MVP
boundary), under the one host lifecycle/control model, with DR-G21 fault
containment required immediately.

**State:** local, non-authoritative only — rebuildable cache/index and
operational metadata classes (DR-124), plus doctor/purge honesty (DR-G12).
**Authoritative sealed closure, replay, and evidence custody are OUT of
slice 1**, and — correcting the previous draft's unlawful row splits
(turn-1 MF-03) — **DR-106, DR-109 and DR-113 are deferred WHOLLY**: their
acceptance-evidence cells all begin with applied DR-002..008 successors,
and DR-113's "purge half" would have designed the typed purge result DR-007
expressly forbids inventing. The slice's local purge/doctor needs route
through DR-124/DR-114/DR-G12/DR-107 instead. **Baseline/ratchet is a
CONDITIONAL deferral** (turn-1 axis-6): OUT of slice 1 as drafted, but if
DR-006's closure lands binding fingerprint recipes, the slice-2 decision
revisits it first. **The trade, recorded in bytes (T2-02):** deferring it
gives up the prototype's proven highest-leverage CI behavior — gating
net-new findings against a recorded corpus — so slice 1 ships analysis
without ratcheting, a materially weaker CI story; in exchange the slice
presumes nothing about the parked fingerprint recipe and takes on no
analysis-affecting durable state class. A product owner could defensibly
choose the opposite; this entry chooses honesty about the park over early
CI leverage, and the conditional-revisit rule is the hedge.

**Platforms:** macOS (arm64, x86_64) and Linux (x86_64, arm64). Windows
deferred with explicit disposition.

**Explicit deferrals (each gets its recorded disposition, never
silence):** DR-108 (no credential-requiring features in slice 1), DR-110
(self-update/repair — install is fresh signed download in slice 1),
DR-116 (no third-party support policy needed yet), DR-128 (post-MVP by
register), DR-129 (no TUI in slice 1), Windows platform support,
baseline/ratchet (conditional — see State), and **DR-106, DR-109, DR-113,
each deferred WHOLLY** (T2-01: the previous "halves" wording here
contradicted the entry's own MF-03 withdrawal and is struck). Each scoped
inclusion elsewhere in this entry (DR-105, DR-124/G19, G09, and G08 —
added per the turn-3 observation) is likewise recorded as a scope
disposition with its own artifact and commit when executed, so no scope
exists only inside this register entry (turn-1 NOTE-10). The DR-110
disposition, when authored, must draw the DR-107/G18
generation-rollback versus self-update-rollback boundary and address file
02's unexercised "updates" inventory entry (turn-3 observation).

**Condition-2 affected-row set under this slice:** DR-101, DR-102,
DR-103, DR-104, DR-105 (scoped to the permissions the slice actually
exercises: local read/write + consented doctor probes — a scoping the row's
own per-platform truth-table text supports), DR-107, DR-111, DR-112,
DR-114, DR-115, DR-117 (the slice's install shape presumes the small-core /
component-closure split, whose product-boundary half rides the DR-010/117
successor — named per turn-1 SF; it proceeds on that track regardless),
DR-118 (TypeScript role), DR-119, DR-120, DR-121, DR-122, DR-123, DR-124
(touched classes), DR-125, DR-126, DR-127. **DR-106, DR-109, DR-113:
deferred wholly** (MF-03), closing via the condition-1 chain; their design
enters a later slice. **Condition-4 required-gate set:** DR-G01..G05, G07,
G08 (SCOPED to the trust surfaces the slice ships — root/index/core/
component install trust; the repair-media/rollback surfaces defer with
DR-110, named per turn-1 SF), G09 (scoped), **G10 (in the required set —
the TypeScript provider is the slice's substrate; its own selector-refresh
precondition stands)**, G12, G14 (TypeScript), G15, G16, G17 (analyze),
G18, G19 (touched classes), G20, G21, G22. **G06/G11: NOT
slice-1-required** — both guard AUTHORITATIVE closure/storage, which the
slice excludes; pre-named now for hygiene, required by the first slice
that includes an authoritative closure (turn-1 NOTE-09). DR-G13
(TypeScript) after DR-118.

### Rationale

Smallest coherent product that maximizes the architectural surface whose
DESIGN work is unblocked (CLI, distribution, packaging, containment,
protocol, state classes, doctor), with every identity-dependent feature
NAMED and mapped to the condition-1 closure it rides (see
Identity-dependencies above) — never designed as if settled. Blueprint
work starts when conditions 1–4 land; the slice adds no blocker beyond
that chain and settles nothing by prose. One language role minimizes the
DR-118/G13/G14 acceptance surface while the prototype supplies real
migration evidence for it. Every exclusion is reversible by a later slice
decision; nothing here forecloses slice 2.

- **Overturn:** one-line supersession here + `git revert` of the C2
  commit; slice-2+ decisions are separate entries. The one-revert path is
  available only BEFORE dependent commits (deferral dispositions, gate
  namings, DR-118 corpus work) land on the slice; after that, overturn is
  a successor slice decision that must also disposition or supersede the
  dependents (turn-1 NOTE-11).
- **Reviewer:** adversarial review under D-000. Turn 1: OBJECTIONS (3
  MUST-FIX, 5 SHOULD-FIX, 3 NOTE) at
  `artifacts/coordinator-decisions.D-002.review-adversarial.json`
  (`ea0e397b…`) — the central refutation (blocked-semantics leakage)
  accepted in full and restructured as the Identity-dependencies section;
  the unlawful DR-106/109/113 splits withdrawn (deferred wholly); G08
  scoped, G10 admitted to the required set, the small-core/DR-010
  presumption named, baseline/ratchet made a conditional deferral. Turn 2:
  OBJECTIONS narrowed to 1 MUST-FIX + 1 SHOULD-FIX + 2 NOTE at
  `artifacts/coordinator-decisions.D-002.review-adversarial.turn2.json`
  (`e17659fb…`), 7 of 11 turn-1 items RESOLVED-VERIFIED, expectation of
  CONSENT recorded; all four accepted and landed (T2-01 stale "halves"
  line struck, T2-02 the baseline trade recorded in bytes, turn-1 NOTEs
  09/10/11 each implemented, T2-04 symmetry clause added). Turn 3:
  **CONSENT**, on the merits, all four items verified landed in bytes,
  set arithmetic re-verified 27/27 + 22/22 (`…turn3.json`, `a15f9ac2…`).
- **Commit:** C2 (this commit), with all three verdict files.

---

## D-003 — Apply evidence-identity-recipes.v12

- **Date:** 2026-08-13
- **Status:** ADOPTED — rule-governed application under the standing
  route-A acceptance property (D-001, T2-02), with the property's
  conditions measured rather than inferred; no separate consensus loop is
  required where the adopted property makes the act mechanical, and the
  evidence is attached.
- **Decision type:** RULE-GOVERNED.
- **The property's conditions, measured:** (1) independent review verdict
  `ACCEPT` at 0 blockers
  (`artifacts/evidence-identity-recipes.v12.review-independent.json`,
  `d5f748b2…`) — the FIRST acceptance in this lineage after seven
  consecutive REJECTs; (2) application-grade with NO express reservation —
  a reservation-language sweep over the verdict file returns zero hits
  (no DO-NOT-APPLY, no candidate-only limitation, no application-warrant
  carve-out), in deliberate contrast to this lineage's v6 precedent whose
  verdict said "ACCEPT AS A CANDIDATE"; (3) no named apply-condition
  exists to discharge. The subject's own CANDIDATE-NOT-APPLIED
  self-declaration is the author's pre-review posture, not a verdict
  (blueprint reading rule 2, per the TM-row precedent).
- **What is applied:** `evidence-identity-recipes.v12` (`f0bfaebd…`) as
  the EIR lineage head, superseding applied v6. Resolved canonical
  `872883db…` (byte-identical from v9 onward; the resolved delta versus
  applied v6 is the v7/v8/v9 prose corrections — every digest, pin,
  golden, recipe and vector byte-identical, verified across eight
  independent reviews). `sealRecommendation: DO-NOT-SEAL` stands; applying
  is not sealing.
- **What this advances:** DR-006's route (the accepted head exists; the
  binding per-surface recipes remain successor work), DR-011-R15's flank.
  It does NOT close DR-006.
- **Advisories carried:** the v12 review's three advisories (warrant
  misfiled to a sibling declared input; a terminology dual-use; citation
  hygiene) are birth requirements for the next EIR successor, not
  repairable in reviewed bytes.
- **Overturn:** supersession entry here + `git revert` of the C-D003
  commit; the freeze line then re-records the prior head.
- **Commit:** C-D003 (this commit).

---

## D-004 — Instrument-standing and citation reconciliation

- **Date:** 2026-08-13
- **Status:** ADOPTED — rule-governed execution of independently-reviewed
  rulings: the DR-204 adjudications (verdict `0934ffbe…`) and the three
  instrument-standing reviews. No consensus loop is required where every
  act executes a reviewed ruling with its evidence attached; nothing here
  is preference-laden.
- **Acts, each with its warrant:**
  1. **Claim-register repairs** (per DR-204 + `check-c2-v12` review):
     C-2's `bindingArtifactSha256` moved from v9's digest to v11's
     (`d35b677d…`) with the v11 review (`d25e77e9…`, PASS, 0 blockers)
     installed as the binding review; ARCH.RETENTION-TIERS moved from
     v24's digest/review to the v28 pair (`e622b3cc…` / `58113366…`, with
     all six IR-RT28-N ids recorded). History retained in both notes per
     the register's own 2026-08-03 repair precedent; claim status stays
     CANDIDATE per the DELIVERY convention (application is freeze-recorded,
     not claim status). Register now `ef59f860…`.
  2. **Freeze corrections** (per the retention-checker review `3b548c28…`):
     the §3 retention row's 160/160 misattribution corrected (the figure is
     the executed v26 reference's; the instrument's own suite is 57/57);
     the checker's UNREVIEWED gap closed with its ACCEPT-STANDING; the
     permanent live-tree refusal recorded as correct §7.8.1 behavior; the
     `check-retention-custody-v29` and `check-c2-v13` successors
     commissioned as named work.
  3. **Instrument-standings rider** added (delivery-v5 `e6a1b3b2…`, c2-v12
     `15bff475…`, retention-v28 `3b548c28…`), including the R04 fixture-
     skew characterization.
  4. **EIR v6 lawful-disposition note** (per DR-204 adjudication 5): the
     candidate-grade warrant window 2026-08-12→13, closed by v12's
     property-compliant application, residual NIL on the two-prose-leaf
     v6→v12 delta evidence.
  5. **Pin re-move**: the six freeze pins re-moved `2650bc14…` →
     `f877f30e…` with the three D-004 diff hunks verified outside every
     cited section.
- **Overturn:** `git revert` of the C-D004 commit restores all surfaces at
  once; the individual rulings remain in their verdict files regardless.
- **Commit:** C-D004 (this commit).

---

## D-005 — Apply r1-lifetime-neutrality.conformance.v1.9

- **Date:** opened 2026-08-13
- **Status:** **ADOPTED 2026-08-13** — consensus at turn 3 of 3: final
  verdict CONSENT on the merits
  (`artifacts/coordinator-decisions.D-005.review-adversarial.turn3.json`,
  `7ddace47…`), with the grade ruling SUSTAINED FOR APPLICATION across all
  three turns and the chain independently re-resolved as the fourth
  reproduction. OBS-D005-T3-01 recorded against the coordinator: the
  third report-ahead-of-bytes instance in this lane (both digests in the
  verdict); "edits land before messages send" is now load-bearing
  standing discipline. Executed at C-D005.
- **Commit structure (OBS-D005-T3-02):** the application and the DR-001
  re-record route land as SEPARATE commits for decision-granularity
  revert — C-D005 carries the application (freeze R-1 record + register
  R-1 repair-with-history + this adoption); the DR-001 route commit
  follows, sharing the R-1 repair by citation, never by re-edit.
  OBS-D005-T3-03 noted: the turn-3 consent covers this entry's spec only;
  the DR-001 review is its own lane.
- **Decision type:** RULE-GOVERNED if the grade question resolves as
  proposed; the grade question itself is the reviewable judgment.
- **The measured chain, all discharged (amended per turn-1 SF-3/MF-2 —
  verbatim sentences, no splicing):** v1.9 (`37897be0…`) reviewed at 0
  blockers, 6 advisories (`3914c9c5…`). The review's
  `recommendationToTheCoordinator.disposition`, verbatim: *"All three
  blockers against v1.8 are cleared by v1.9, verified by independent
  recomputation at zero disagreements on every published figure. No new
  blocker. Accept as candidate. Do not seal; do not apply until a corpus
  resolver (check-completeness.py or -v2) has positively resolved the
  chain, which freeze 7.3 requires and which no review substitutes for."*
  And its `whatIDidNotCheck`, verbatim: *"…Freeze 7.3 requires a positive
  corpus-resolver run before APPLYING any derivation; my resolver's
  success does not substitute. This is the one gate still owed before
  application, hence the apply recommendation."* The condition is
  discharged at corpus-resolution.v1 (REFUSED, pre-repair) → v2
  (POSITIVE, canonical `27d27bc0…`), on instrument bytes whose dialect
  repair was independently reviewed PASS. The DR-204 reliance ruling is
  CONDITIONAL and is quoted with its proviso (MF-2): reliance is clean
  *"PROVIDED reliance continues to bind the reviewed instrument digests
  and carries the five advisories as live advisories"* — the application
  motion therefore re-verifies at motion time that the instruments remain
  at their reviewed digests (`af9f8837…`, `dbe1e695…`) and carries the
  five dialect-repair advisories as live. The D-005 adversarial review
  independently re-resolved the chain with a fresh resolver — 34/34
  operations, canonical `27d27bc0…` reproduced exactly, the FOURTH
  independent reproduction on record.
- **The grade question, both readings stated:**
  - *For application:* the verdict's construction is
    DO-NOT-APPLY-**UNTIL** — the reviewer contemplated application and
    named its single precondition, unlike EIR v6 (bare candidate
    acceptance, no apply path) and delivery.v5 (EXPRESSLY NOT FOR
    APPLICATION). A named, now-discharged condition plus 0 blockers is
    the property's "application-grade acceptance with no express
    reservation and no undischarged named condition."
  - *Against:* the verdict labels itself "ACCEPT-AS-CANDIDATE," and the
    property's text forbids "candidate-only limitation"; on that reading
    the until-clause governs when candidacy may be RECONSIDERED, not an
    application warrant, and application requires a fresh acceptance.
- **Proposed ruling:** the FOR reading, on the ground that the property's
  candidate-only clause exists to block promotions the reviewer never
  contemplated — and this reviewer's own words name the apply path and
  its gate. If the adversarial review does not consent, the AGAINST
  reading's remedy is a targeted grade-clarification review putting the
  NEUTRAL question — "is this acceptance application-grade once its named
  condition is discharged?" — to a fresh reviewer against the review's
  frozen bytes (reworded per turn-1 NOTE: a remedy must ask, never
  request an outcome), and this entry parks CONTESTED meanwhile.
- **What application would do (amended per turn-1 MF-1/SF-1):** record
  v1.9 as the applied r1 head in the freeze, advancing DR-009/DR-011-R09's
  first half, with the motion carrying the §7.9 site census the D-005
  review enumerated (`7c5f590d…`): the claim-register R-1 row's validator
  column, the PC-6/CHK-5 finding movements, and the resolved canonical.
  The motion ALSO repairs, with history retained, the live defect that
  review found (MF-1, previously recorded nowhere): R-1's
  `bindingArtifact` names v1.6 while `bindingArtifactSha256` carries
  v1.5's digest (`557b9f97…`) and the binding review is v1.5's — the
  promote-by-name class DR-204 adjudicated for C-2. On application the
  row moves coherently to the v1.9 pair (artifact `37897be0…`, review
  `3914c9c5…`) with the found defect recorded in the note. The freeze
  application record carries the review's `standingPosition` verbatim, as
  that review instructs (turn-2 ADV-D005-T2-01 / turn-1 item 04):
  *"OPEN-DEP-FI-01..07 remain open in the resolved value and v1.9 says so.
  Whatever happens to the advisories, this design remains implementable as
  a library and NOT shippable as production finding identity. That
  statement survives resolution intact and should keep being carried
  forward verbatim."* It does NOT
  close DR-009 (LN-13, derivationDigest, R1-PARK-*, retained-validator
  standing and CIR-B1 remain), does not seal, and moves no design
  decision.
- **Overturn:** supersession here + `git revert` of the application
  commit.
- **Reviewer:** adversarial review under D-000. Turn 1: OBJECTIONS (2
  MUST-FIX, 3 SHOULD-FIX, 1 NOTE) at
  `artifacts/coordinator-decisions.D-005.review-adversarial.json`
  (`7c5f590d…`) — **with the grade ruling itself SUSTAINED FOR
  APPLICATION** on the review's own bytes, and the chain independently
  re-resolved as the fourth reproduction. All six items accepted and
  amended above; none rebutted. Turn 2 pending.
- **Commit:** C-D005, on adoption.

---

## D-006 — DR-115: numeric size/startup/memory thresholds

- **Date:** opened 2026-08-13
- **Status:** DRAFT — UNDER ADVERSARIAL REVIEW per D-000.
- **Decision type:** PREFERENCE-LADEN (route C). Numbers are not derivable
  from any rule; the register says so ("numeric open"). Decided on the
  user's behalf; overturn is one supersession line + one revert.
- **Scope:** thresholds for the D-002 slice's platforms (macOS arm64/x86_64,
  Linux x86_64/arm64) over gates DR-G01..G05, plus the regression rule.
  These are ARCHITECTURE TARGETS gating qualification measurements — not
  qualification claims (DR-012 untouched; nothing here is QUALIFIED).
- **DR-115's fate on adoption (turn-1 MF-1):** the row's acceptance cell
  conjoins "reproducible measurements AND product-owned threshold
  decision"; this entry supplies the DECISION half, and the measurement
  half structurally cannot exist pre-blueprint. On adoption, C-D006
  carries the file-08 edits: the DR-115 row status moves to
  **`DECIDED-V1-NOT-INTEGRATED`** — the register's existing label, whose
  definition fits exactly (turn-2 NOTE-03: the closed status vocabulary
  stays closed; coining an analog would itself be a register-content
  decision) — annotated "thresholds DECIDED (D-006); measurement half
  discharged at qualification" — with a condition-2
  scope disposition recorded to exactly that effect, and the now-false
  "numeric open" cells in the DR-G01..G05 rows and the gate-registry
  preamble sentence updated to cite this decision.
- **Reference-runner class, named now (turn-1 MF-2):** all ms/RSS numbers
  bind to this runner class — macOS arm64: base-configuration Apple
  Silicon entry chip (M1-class), 8 GB; **macOS x86_64: native Intel-class
  hardware, never Rosetta-on-Apple-Silicon (turn-2 SF-02 — measurements
  on translated binaries measure the translator, and the platform's users
  run native Intel)**; Linux x86_64 and arm64: 4-vCPU / 8 GB standard
  cloud-runner class. The EXACT machine identifiers, OS versions
  and cache-state protocol are pinned by the G03/G04 harness-naming,
  which is itself a REVIEWED decision commit with product sign-off on
  representativeness — the harness-namer executes this class, never
  co-authors the threshold.
- **Proposed thresholds:**
  1. **DR-G01 (core download):** signed compressed distribution-core
     ≤ 25 MB per platform. Rationale: several-fold below typical
     Electron-class tooling (arithmetic corrected per turn-1 NOTE — ~4×,
     not an order), holding the "small core" direction falsifiable without
     starving a native binary + signing + index client. The core excludes
     every language runtime closure (file 02's split; the TS/Node closure
     is a DR-119/G14 component — verified by the turn-1 review).
  2. **DR-G02 (installed core/TCB):** immutable installed tree ≤ 80 MB;
     mandatory-closure inventory enumerated, zero undeclared dependencies
     (the qualitative half is DR-126's).
  3. **DR-G03 (startup):** `--help`/`--version` on the named runner class:
     cold-cache p50 ≤ 100 ms, p95 ≤ 150 ms, p99 ≤ 250 ms; warm p95
     ≤ 50 ms, p99 ≤ 100 ms (all five percentiles bounded per turn-1 NOTE);
     loads no components and no project (the gate's own text).
  4. **DR-G04 (memory), tightened per turn-1 SF-4:** the gate's two
     quantities bound separately — `--help`/`--version` RSS: steady
     baseline ≤ 40 MB, peak ≤ 50 MB (a runtime-in-core regression MUST
     fail this gate; the prior 100 MB bar could not discriminate it —
     adopted from the review, with its general-knowledge caveat recorded);
     `doctor` read-only RSS: steady baseline ≤ 60 MB, peak ≤ 100 MB
     (turn-2 NOTE-04 — no quantity left silently unbounded). **Explicit exclusion, not
     silence (turn-1 NOTE):** `analyze` and doctor-with-consented-probes
     RSS are DELIBERATELY outside D-006 — they need real workloads and are
     set by the qualification-harness decisions with product sign-off.
  5. **DR-G05 (component delta):** slice 1 mandates MEASUREMENT AND
     VISIBILITY (download/install/start/RSS delta published per component,
     per platform) with NO numeric cap in this decision — caps become
     product decisions at the first component-acceptance decision under
     DR-G05's own evidence column. **Trigger defined (turn-1 SF-1):**
     since slice 1's TypeScript provider IS a component, that trigger
     fires within slice 1's own qualification cycle — the deferral is
     short-lived by design, and that is recorded here, not discovered
     later.
  6. **Regression rule (operative sentence restored per turn-2 MF-01; the
     turn-1 amendment had polished the frame and dropped the rule):**
     a qualified clause 1–4 measurement may not REGRESS more than 10%
     against the previous qualified release without a waiver in the
     register's full form — regress-only, one direction; improvements are
     unbounded. Domain: the CORE quantities of clauses 1–4 only; component
     deltas (clause 5) are visibility-only until their cap decision sets
     their own regime — this clause is NOT a hidden growth cap on them.
     Base case: the FIRST qualified release qualifies against the clause
     1–4 thresholds alone; the rule activates from the second qualified
     release onward. Waivers per the register's full form (turn-1 SF-2):
     product AND release authority, an expiry, a MEASURED RESIDUAL, and
     never waiving an inherited semantic/trust blocker.
- **Falsifiability note:** every number binds a HARNESS measurement under
  DR-G01..G05's own evidence columns (raw samples, cache state, traces
  retained). If early implementation shows a number infeasible, the lawful
  path is a successor decision with the measurement attached — never a
  silent waiver.
- **Reviewer:** adversarial review under D-000. Turn 1: OBJECTIONS (3
  MUST-FIX, 4 SHOULD-FIX, 3 NOTE) at
  `artifacts/coordinator-decisions.D-006.review-adversarial.json`
  (`048d5623…`) — all structural, with the numbers' quantification
  verified in D-006's favor (the core excludes language-runtime closures;
  the corpus contains no contradicting numeric prose). All ten items
  accepted and amended above: DR-115's fate and file-08 edits named
  (MF-1), the runner class named now with exact pinning as a reviewed act
  (MF-2), clause 6's domain and base case stated (MF-3/SF-3), the G05
  trigger defined and its slice-1 collapse recorded (SF-1), the waiver
  form restored in full (SF-2), the RSS bar tightened to discriminate the
  runtime-in-core regression (SF-4), the arithmetic corrected, all five
  percentiles bounded, and the analyze/probes exclusion made explicit
  (NOTEs). Turn 2 pending.
- **Commit:** C-D006, on adoption.
