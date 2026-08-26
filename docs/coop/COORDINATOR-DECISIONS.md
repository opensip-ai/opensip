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

*(Pin-note 2026-08-13, D-010: the blockquote above reflects the register as
adopted; D-010 later made condition 2's wording range-free and added DR-130
per D-001's own new-row rule. The quote is history; the register is
operative.)*

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
- **Status:** **ADOPTED 2026-08-13** — consensus at turn 3 of 3: CONSENT
  on the merits (`artifacts/coordinator-decisions.D-006.review-adversarial.turn3.json`,
  `bfd8a758…`). Fourteen findings across two turns, all accepted and
  landed in bytes, none rebutted or waived. OBS-T3-02 recorded: native
  Intel Mac hardware is scarcity-exposed — the G03/G04 harness-naming act
  must verify procurability under its product sign-off, and
  unprocurability routes through this entry's successor-decision path,
  never silent Rosetta substitution.
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
  (NOTEs). Turn 2: OBJECTIONS narrowed to 1 MUST-FIX + 1 SHOULD-FIX + 2
  NOTE (`…turn2.json`, `b9ff5c17…`) — the amendment had dropped the
  operative regression sentence itself; restored regress-only, the macOS
  x86_64 runner class decided (native Intel, never Rosetta), the closed
  status vocabulary respected, doctor's steady baseline bounded. Turn 3:
  **CONSENT** (`…turn3.json`, `bfd8a758…`), all fourteen findings
  verified landed (three-turn record completed per OBS-T3-01).
- **Commit:** C-D006 = commit `bf6538b` (verdict artifacts; its message
  overclaimed — it carried NO register or file-08 edits due to a staging
  script fault) plus the completion commit that follows, which carries
  the adoption edits and the named file-08 edits. Recorded honestly, not
  rewritten.

---

## D-007 — DR-118: TypeScript role acceptance structure

- **Date:** opened 2026-08-13
- **Status:** **ADOPTED 2026-08-13** — CONSENT on the merits at turn 2
  (`artifacts/coordinator-decisions.D-007.review-adversarial.turn2.json`,
  `1fbbce62…`), the lane's fastest convergence: all ten turn-1 findings
  verified RESOLVED per-item against their governing sources, none
  partially landed. Two observations routed within the consent:
  OBS-T2-01 (performance-baseline runner/environment recording — to
  matrix authoring and the DR-G13/G14 acceptance checklist) and OBS-T2-02
  (the manifest/DR-125 dual boundary — to those closure acts).
- **Decision type:** PREFERENCE-LADEN (route C). D-002 selected the
  slice-1 role list ({TypeScript}); this entry decides WHAT ACCEPTANCE
  REQUIRES for that role — the matrix shape, pinning discipline, baseline
  reference and threshold ownership DR-118's row names. The matrix and
  corpus themselves are ACCEPTANCE EVIDENCE authored during
  qualification; deciding their required structure now is what unblocks
  that authoring without pretending it done.
- **Decided requirements for the TypeScript role's acceptance (amended
  per the turn-1 review — five dropped source elements restored):**
  1. **Matrix shape — role × capability × PLATFORM (MF-3):** the platform
     axis is D-002's four; a cell may state "platform-invariant"
     explicitly (a verifiable claim), never omit the axis. One row per
     capability the role's component manifest advertises, derived from
     the host-contract capability declaration (DR-125's contract) — the
     five named areas (parse fidelity, semantic resolution, graph
     construction, finding classes, output projections) are an
     ILLUSTRATIVE FLOOR; the manifest is the boundary source (SF-6, the
     register's own quantifier-as-boundary cure). Each row carries: the
     capability's DEFINITION by host-contract reference; the
     prototype-baseline measurement at the pinned commit; the V2 target;
     the measurement method with digest-pinned corpus.
  2. **Known limitations (MF-1, restored):** every row carries its
     documented known limitations and unsupported tiers; a row with none
     states that explicitly — absence of limitations is a claim, not a
     default.
  3. **Performance (MF-2, restored and routed):** every row carries a
     BEHAVIOR baseline and a PERFORMANCE baseline (prototype-measured at
     the pin where applicable, else the explicit absence statement), with
     V2 performance targets product-approved at acceptance. Workload-level
     RSS/latency for `analyze` join the same qualification-harness
     decision D-006 routed them to — named here so the two entries route
     to ONE place, silence nowhere.
  4. **Corpus discipline:** digest-pinned per file, product-approved
     before any measurement claim, versioned by supersession; the EIR
     measured-or-cited-at-digest discipline applies to every cell.
  5. **Baseline reference (SF-7/NOTE-10, completed):** the prototype at
     `a62509d6…` is the only admissible EXISTING-behavior reference —
     with DR-203's caveats carried (SHA-1 identity, out-of-corpus
     custody; the commit is re-verified at each measurement time) — and
     rows state "no prototype baseline exists" OR "prototype baseline
     inapplicable" per the reference's own rule; a missing or
     inapplicable baseline is replaced ONLY by a product-approved
     language-native corpus, the reference's lawful replacement path.
  6. **Identity and Coverage golden classes ride DR-006 (MF-4):** file
     02's required identity and Coverage goldens depend on parked recipes
     (finding fingerprint, `subjectScopeCommitment`,
     `typescriptStdlibMerkleRoot`, `capabilityManifestId`). Per D-002's
     symmetry clause: those matrix rows are authored only on the DR-006
     closure they ride, and matrix prose can NEVER settle a parked
     recipe — if DR-006 closes by disposition, the dependent rows follow
     that disposition's terms.
  7. **Thresholds:** parity-or-improvement per row is a PRODUCT approval
     at matrix acceptance (the DR-115 pattern); no row ships with a
     silent regression against its stated baseline.
  8. **No-silent-fallback (MF-5, full enumeration):** a required NEGATIVE
     test class per capability — the role REFUSES (typed, loud) rather
     than degrading to a weaker parser, syntactic tier, semantic model,
     graph, or finding model.
  9. **Row disposition on adoption (NOTE-9):** DR-118 moves to
     `DECIDED-V1-NOT-INTEGRATED` — role list (D-002) and acceptance
     structure (this entry) DECIDED — with the annotation stating that
     PER-ROW THRESHOLDS REMAIN UNDECIDED (unlike DR-115, whose numbers
     were decided); the matrix/corpus evidence half discharges at
     DR-G13/G14 qualification.
- **Alternatives considered (SF-8, recorded per D-000 clause 3):**
  a THINNER slice-1 matrix (parse+findings only) was rejected — it would
  defer exactly the capability rows (semantic, graph) where the
  prototype's value concentrates and invite scope disputes at
  qualification; THRESHOLDS-NOW was rejected — no measured denominator
  exists pre-blueprint, and inventing numbers would repeat the class
  D-006's reviewer struck (a threshold whose runner/workload is unnamed
  measures nothing). Either remains reachable by successor decision.
- **What this does NOT do:** author the matrix or corpus; qualify
  anything; extend the role list (a slice-2+ decision); touch DR-119's
  self-contained-closure acceptance (its own entry).
- **Overturn:** supersession here + revert of C-D007.
- **Reviewer:** adversarial review under D-000. Turn 1: OBJECTIONS (5
  MUST-FIX, 3 SHOULD-FIX, 2 NOTE) at
  `artifacts/coordinator-decisions.D-007.review-adversarial.json`
  (`78a5f7dc…`) — five dropped source elements (known limitations,
  performance, the platform axis, the identity/Coverage DR-006 rides, the
  full fallback enumeration), the capability-list boundary, the completed
  missing-baseline rule, and the recorded alternatives; all ten accepted
  and amended above, none rebutted. The reviewer confirmed the
  structure-now/evidence-later frame itself survives refutation. Turn 2:
  **CONSENT** (`…turn2.json`, `1fbbce62…`), all ten verified in a single
  hunk confined to this entry, the edits-before-messages discipline
  explicitly confirmed held.
- **Commit:** C-D007 (this commit), with the DR-118 row edit.

---

## D-008 — DR-119 acceptance: self-contained language-closure product rule

- **Date/Status:** opened 2026-08-13; **ADOPTED 2026-08-13** — per-entry CONSENT at turn 3 of the batch review (turn 1 `15838fe8…` OBJECTIONS ×4, turn 2 `f0e0457e…`, turn 3 `cd08c5f0…` CONSENT ×4 on the merits, nothing waived).
- **Decision type:** PREFERENCE-LADEN (route C).
- **Decision (amended per turn 1):** the proposed product rule (file 02,
  DR-119 row) is **ACCEPTED UNIVERSALLY** — it binds EVERY supported
  language role, per the row's own unconditional quantifier (turn-1 MF:
  the draft's per-role re-acceptance hook is struck); only the EVIDENCE
  is slice-scoped (TypeScript now, each future role's closure evidence at
  its own DR-G14 qualification). The accepted rule, restated at full
  source fidelity (turn-1 SF): every supported role ships a signed,
  platform-qualified, self-contained closure of runtime/parser/compiler/
  language-server-class (or analogous non-system) dependencies, with
  MANIFEST DECLARATIONS of licenses/SBOM/attestation/platform/capability/
  performance; clean-machine offline tests; refusal of ambient/implicit
  downloads AND typed remediation as separate obligations; any
  unbundleable customer-owned external-system exception needs explicit
  product approval and a doctor contract, is VISIBLE in the manifest with
  typed absence/failure behavior, NAMES its ownership, trust, network and
  prerequisite expectations, and is never marketed or silently treated as
  self-contained; and the role NEVER SILENTLY SUBSTITUTES a system tool
  or weakens semantics (turn-2 SF — the anti-fallback heart of the rule,
  restored so "full source fidelity" is true). TypeScript must not
  require user-managed Node. The row's SOURCE cell also carries the D-008
  citation per the DR-115/118 pattern (turn-2 NOTE).
- **File-08 edit C-D008 carries (turn-1 MF):** the DR-119 row moves to
  `DECIDED-V1-NOT-INTEGRATED`, annotated "rule ACCEPTED universally
  (D-008); closure evidence per role at DR-G14 qualification."
- **Alternatives considered (D-000 clause 3):** per-role acceptance was
  the draft's shape and is rejected as a re-litigation hook against the
  row's quantifier; declining the rule entirely would force a register
  amendment and contradict file 10's MVP commitment — the dissent path
  remains a successor decision.
- **Overturn:** supersession + revert of C-D008.

---

## D-009 — DR-123 acceptance: mandatory CLI baseline

- **Date/Status:** opened 2026-08-13; **ADOPTED 2026-08-13** — per-entry CONSENT at turn 3 of the batch review (turn 1 `15838fe8…` OBJECTIONS ×4, turn 2 `f0e0457e…`, turn 3 `cd08c5f0…` CONSENT ×4 on the merits, nothing waived).
- **Decision type (relabeled per turn 1):** RULE-GOVERNED IN SUBSTANCE —
  the register and file 01 already mandate the CLI baseline for every
  slice; this entry is the awaited assent, and PREFERENCE-LADEN would
  overstate the discretion. The dissent path is named as the alternative:
  a product owner could decline and force a register amendment; declining
  is rejected because every recorded surface (DR-123, file 01, file 10,
  D-002) already builds on the baseline.
- **Decision:** ACCEPTED as binding: every slice-1 command works
  non-interactively in CI without a TUI; stable human and machine output
  schemas, exit vocabulary, redaction, output-failure behavior, offline
  operation and footprint evidence per the row's cell. The acceptance
  changes no gate; DR-G01..G05/G12/G17 carry the evidence.
- **File-08 edit C-D009 carries (turn-1 MF — the draft named none, the
  C-D006 overclaim class):** the DR-123 row moves to
  `DECIDED-V1-NOT-INTEGRATED`, annotated "baseline acceptance DECIDED
  (D-009) for EVERY FIRST-SLICE CORE COMMAND (the turn-2 consent's rider
  carried); evidence at DR-G01..G05/G12/G17."
- **Overturn:** supersession + revert of C-D009.

---

## D-010 — Register content: the V1→V2 transition-contract row (V2TOPIC-F-02)

- **Date/Status:** opened 2026-08-13; **ADOPTED 2026-08-13** — per-entry CONSENT at turn 3 of the batch review (turn 1 `15838fe8…` OBJECTIONS ×4, turn 2 `f0e0457e…`, turn 3 `cd08c5f0…` CONSENT ×4 on the merits, nothing waived).
- **Decision type:** RULE-GOVERNED register-content change (the
  verification record measured the gap: no DR row owns the V1→V2
  product/state transition), reviewed per D-001's MF-6 discipline.
- **Decision:** add register row **DR-130**: "V1→V2 transition contract —
  migration/coexistence posture for existing V1-prototype users and their
  local state" — owner: product + lifecycle; source pin: file 05 (V1→V2
  relationship, §Migration constraints by anchor) and the prototype
  reference PINNED at `69a71aac…` / commit `a62509d6…` (turn-2 SF); acceptance evidence (turn-1 MF — bound by REFERENCE, the
  D-007 SF-6 cure, because the draft's "no-silent-loss rule" was defined
  nowhere): an INDEPENDENTLY REVIEWED transition statement satisfying
  file 05 §Migration constraints AS WRITTEN — its six-member "No
  migration silently…" enumeration, its five-item preserve list, and its
  five distinctions, cited by anchor and count-pinned (6/5/5; any change
  to those enumerations re-opens this row); status OPEN; blueprint
  impact: blocks any slice claiming upgrade continuity; slice 1 claims
  none and its deferral disposition is RECORDED IN THE ROW ITSELF at
  C-D010 (the named artifact and commit, per turn-1 SF). Per D-001's
  new-row rule, C-D010 amends file 08's condition-2 wording — adopting
  the RANGE-FREE form the D-001 turn-2 verdict recorded (turn-1 SF: a
  range-to-range edit re-arms the staleness trap): the condition
  quantifies over "every row of the V2 architecture and product decisions
  table that affects the first blueprint slice." The now-historical range
  in D-001's §1 blockquote is handled by a dated PIN-NOTE appended to
  D-001's entry (adopted bytes are quoted history, never silently
  edited): the quote reflects the register as adopted; the register is
  operative. Turn-2 residual notes, landed: DR-130 IS the C4a item of
  D-001's commit plan (the equivalence stated); file 05's Readiness
  banner is untouched by this row's addition and stays governed by its
  own refresh rule; and the range-free wording pulls DR-128/129 into
  condition 2's literal text for the first time — warranted by D-001
  MF-5, benign because both carry D-002 dispositions, and STATED in
  C-D010's change record so the delta never lands silently (the
  reviewer's own turn-1 miss, credited).
- **Overturn:** supersession + revert of C-D010.

---

## D-011 — Register content: DR-117 widened to file 02's seven binding items (V2TOPIC-F-04)

- **Date/Status:** opened 2026-08-13; **ADOPTED 2026-08-13** — per-entry CONSENT at turn 3 of the batch review (turn 1 `15838fe8…` OBJECTIONS ×4, turn 2 `f0e0457e…`, turn 3 `cd08c5f0…` CONSENT ×4 on the merits, nothing waived).
- **Decision type:** RULE-GOVERNED register-content change (the
  verification record measured the mismatch: file 02 enumerates seven
  binding product-boundary items; DR-117's decision column names five),
  reviewed per MF-6.
- **Decision (amended per turn 1 — reference, not duplication):** DR-117's
  decision column is widened by COUNT-PINNED REFERENCE: it covers "the
  SEVEN binding product-boundary items file 02's product-boundary section
  enumerates (count pinned at seven; any change to that enumeration
  re-opens this row)" — the lane's boundary-source-by-reference cure,
  because a verbatim second copy would reproduce the exact drift
  mechanism under repair (the ALTERNATIVE, verbatim duplication with a
  same-commit sync obligation, is recorded and rejected for that reason).
  The seven-vs-five mismatch and file 02's byte-identity with the DR-205
  frozen digest (`1811c682…`) were independently verified by the turn-1
  review; status, owner and evidence cells unchanged. **Edit-time
  re-verification restored (turn-2 SF — the dropped-clause class):**
  C-D011 re-verifies file 02 at `1811c682…` immediately before the row
  edit; on mismatch it ABORTS to the DR-205 successor path (a moved
  source needs its re-review refreshed before the row may cite it).
- **Overturn:** supersession + revert of C-D011.

---

## D-012 — DR-104: component identity, namespace and collision policy

- **Date/Status:** opened 2026-08-13; **ADOPTED 2026-08-13** — CONSENT on
  the merits at turn 3 (`artifacts/coordinator-decisions.D-012.review-adversarial.turn3.json`,
  `e7b5c2b9…`; turns 1–2 at `b08c5f8d…`/`016160c1…`): 11 findings, all
  landed on bytes, none waived; the no-drop sweep clean; OBS-D012-T3-01
  (authenticated manifest declarations) routed to C-D012's change
  record. Closes the slice-1 product-decision phase.
- **Decision type:** PREFERENCE-LADEN (route C). The last undecided
  product row of the slice-1 set (DR-116/128/129 carry D-002 deferral
  dispositions; DR-117's successor rides the DR-010 process).
- **Decided policy (bounded by the prototype's admission evidence —
  manifest-first, deny-by-default, stable IDs distinct from versions and
  aliases, and no implicit execution during discovery — the full bounding
  quote per turn-1 NOTE):**
  1. **Component identity (T1-01, realigned to the pinned bytes and the
     pattern's TRUE strength):** the component ID is an author-declared
     immutable UUID in the manifest — the pinned prototype's model
     (`stableId`) — and the HOST enforces global uniqueness at admission
     against its persisted admission registry: TWO custody records
     (manifest declaration + host registry) with a uniqueness constraint
     between them, which is PROJECT-ID-V1's actual two-record shape
     adapted to author-supplied identity. A UUID is never derived from
     mutable state; a retired ID is retained in the registry and never
     readmitted for a different component; display names and aliases are
     mutable metadata resolving THROUGH the ID, never the reverse.
  2. **Command namespace (T1-02, corrected to the pinned model):** the
     ROOT namespace is host-owned and flat; below a component's mounted
     root command, sub-command grammar is DECLARATIVE (CommandSpec with
     parent relationships) and HOST-INTERPRETED — the component declares,
     the host owns all parsing and dispatch, and manifest discovery never
     hands a component raw root parser authority. A collision at
     admission — over name, alias, OR parent linkage — is a typed
     REFUSAL, never silent shadowing or auto-renaming.
  3. **Host-reserved commands (T1-04, restored from the pinned
     mechanism):** the host maintains a static reserved root-command list
     (the prototype's ADR-0159 shape); no component may claim or alias a
     reserved name; a CI parity test between the reserved list and the
     live grammar is part of the negative-test evidence.
  4. **Scope precedence (turn-1 SF, decided rather than regressed):** a
     component admitted at both project and global scope resolves by the
     DECLARED precedence order project-shadows-global with a required
     disclosure at resolution — a deterministic declared order, which is
     not the forbidden ordering-dependence; the pin's warn-first-wins
     variant is the recorded alternative.
  5. **Rename/alias governance (T1-03, the number decided HERE, the
     DR-111 borrow struck as an undefined-rule citation):** a rename
     keeps the old name as a deprecated alias for AT LEAST one minor
     release cycle AND no fewer than 90 days from the deprecating
     release, whichever is longer; alias cycles are refused at admission;
     an alias may never shadow any live name or reserved name.
  6. **Ownership transfer (T1-06, quote corrected):** slice 1 is
     first-party/EXPLICITLY-TRUSTED (D-002's actual class); transfer
     within that class is registry bookkeeping under host authority WITH
     the same two-custody update discipline; namespace depth beyond the
     mounted-root model AND third-party transfer/dispute policy are both
     EXPLICITLY DEFERRED to the DR-117 successor process (owned by
     DR-010), with DR-116 carrying the support/vulnerability policy side
     — routing made consistent.
  7. **Migration and negative tests (turn-1 SF, completed; T2-02
     landed):** reservation and collision computation are METADATA-ONLY —
     derived from manifest declarations alone, with NO component
     execution during admission or discovery (the bounding quote's
     operative half, now a clause) — and the negative-test evidence
     covers collision, cycle, shadow, stale-alias, parent-linkage
     collision, reserved-name claim, the scope-precedence disclosure,
     ID/version distinctness, multi-version coexistence (file 05's
     goldens class), AND a no-execution-during-admission probe, at
     qualification. Namespace migrations require a recorded deprecation
     entry with typed `doctor` remediation.
- **File-08 edit C-D012 carries (annotation honesty, T2-01 landed):** the
  DR-104 row moves to `DECIDED-V1-NOT-INTEGRATED`, annotated "DECIDED
  (D-012): identity model, root namespace + sub-grammar ownership,
  reservation, scope precedence, alias window, in-class ownership
  transfer, metadata-only admission; DEFERRED by name: namespace depth
  beyond mounted roots and third-party transfer/dispute, to the DR-117
  successor (DR-010); negative-test evidence at qualification"; the
  source cell carries the D-012 citation. C-D012's change record also
  carries the four routed turn-2 observations: the registry's uniqueness
  universe is PER-INSTALL (not global); custody records are
  provenance-bound so the same-vs-different-component discriminator is
  the (ID, provenance) pair; "one minor release cycle" means the HOST
  CORE's release train; and the lane's report-ahead-of-bytes note now
  extends to per-item landing claims.
- **Alternatives considered (corrected per turn-1 — the previous block
  misdescribed the pin):** admission-time host-minted IDs (the draft's
  own first shape) rejected because the pinned prototype's
  author-declared-UUID model is working evidence and host-minting would
  break manifest portability — the host's registry custody supplies the
  missing uniqueness enforcement instead; a STRICTLY flat namespace with
  no sub-grammar (the draft's second shape) rejected because the pin
  itself mounts declarative sub-grammar and flatness-only would regress
  it; warn-first-wins scope resolution (the pin's variant) rejected in
  favor of declared precedence with required disclosure — quieter
  failure modes lose to explicit ones under this corpus's discipline.
- **Overturn:** supersession + revert of C-D012.
- **Reviewer:** adversarial review dispatched 2026-08-13; verdict recorded
  here.
- **Commit:** C-D012, on adoption.

## D-013 — DR-103: the accepted manifest/index/lock design contract

- **Status:** ADOPTED 2026-08-13.
- **Decision type:** RULE-GOVERNED (D-001 §3 classes DR-102/DR-103 as evidence-closing
  rows; no product preference is exercised).
- **Subject:** `component-manifest-schemas.v2.json`
  `73114ddec12d3ec6dfbcb51b7002d983ff9dbfa1fa39189bb025008f1f501381`.
- **Verdict:** `component-manifest-schemas.v2.review-independent.json`
  `42004c95474a66a8bd7685862c9e205fe7c4a7fadc97ab90e408a2fb04f238dd` — **ACCEPT, 0
  blockers**, 1 new advisory (V2-A1, latent in carried v1 bytes, not repair-minted).
  Predecessor v1 `2733d766…` REJECTED at 6 blockers, verdict `27965f38…`.
- **Route-A acceptance property (D-001 T2-02):** MET. 0 blockers; application-grade
  language; reservation-language sweep of the VERDICT clean — 5 `reserv` hits, all
  schema-local (three reserved binding points, one reserved-name refusal-family member, one
  `recordedInputs` filename); zero acceptance reservations. The subject itself carries 60
  such hits, all schema-local by construction. Zero named apply-conditions.

**Decision.** Record the artifact as DR-103's accepted design contract. Reviewed bytes stay
immutable (freeze §7.2), so the register row carries the acceptance. The row edit is this
decision's only effect: DR-103 stays `OPEN`, because the fourth acceptance-evidence element
(exact-byte test corpus) is unmet on the verdict's own words — the artifact carries fixture
CLASSES, and no fixtures exist to run.

- **Alternatives considered:** (a) *Use `SATISFIED`* — rejected: `SATISFIED` is
  legend-defined as "exact acceptance evidence is linked and independently reviewed", and the
  fourth element is unmet. (b) *Coin a new status label* (the turn-1 draft proposed
  `DESIGN-ACCEPTED`) — rejected: D-006 turn-2 NOTE-03 states *"the closed status vocabulary
  stays closed; coining an analog would itself be a register-content decision"*, so the path
  exists but requires its own D-000-reviewed register-content decision, never a rider on an
  application. (c) *Defer the row move until fixtures exist* — rejected: it would leave an
  independently accepted contract unrecorded.
- **Readiness effect:** condition 2 gains **zero** `SATISFIED` rows; conditions 1, 3, 4, 5
  untouched. Condition 2's literal text needs no amendment — the row stays inside its
  quantifier and stays unsatisfied.
- **No freeze or claim-register motion; no pins move.** The subject's freeze and register
  citations sit at `/sources/bindingSources` under its own `sources.citationDiscipline`:
  stated as (path, digest-at-authoring, named property), so a later digest move re-points
  nothing and strands nothing. Verified: file 08's own digest `f0d72536…` is pinned in no live
  source.
- **Reversibility:** total; no pinned source moves.
- **Overturn:** supersession here + `git revert` of C-D013; revert is total.
- **Reviewer:** three turns under D-000's clause. Turn 1 — five-lens adversarial panel plus
  synthesis: 19 MUST-FIX, 7 SHOULD-FIX, 5 objections withdrawn by the reviewer's own
  re-measurement. Turn 2 — 9 MUST-FIX, 4 SHOULD-FIX. Turn 3 — 13/13 turn-2 findings verified
  discharged, 2 MUST-FIX, disposition **RECORD**. All 30 MUST-FIX and 11 SHOULD-FIX accepted;
  **zero rebutted** across three turns.
- **Commit:** C-D013.
- **Provenance/environment:** the start-and-end record for file 08 (`f0d72536…`) and this
  file (`a3d0d266…`) is the control-protocol verdict's `environment.registerAndDecisions`;
  both re-measured identical at adoption.

## D-015 — DR-102: the accepted control-protocol design contract

- **Status:** ADOPTED 2026-08-13.
- **Decision type:** RULE-GOVERNED.
- **Subject:** `control-protocol-contract.v2.json`
  `c50a79fef566ecccbd8913a3d309b0cf7332f7d77f892474a548ef3d7b4ebdca`.
- **Verdict:** `control-protocol-contract.v2.review-independent.json`
  `937626695418d1cad10962bdded0d2aa29dadb005b345408edb7e8fbdc84b015` — **ACCEPT, 0
  blockers**, 2 new advisories (A-CPC2-01/02). Predecessor v1 `17fa1bcb…` REJECTED at 3
  blockers, verdict `5ff15a05…`.
- **Route-A acceptance property:** MET. Reservation-language sweep of the VERDICT clean —
  three `reserv` hits, all forms of "preserve" (two order-preservation statements, one the
  technical term "write-boundary non-preservation"); zero acceptance reservations. The subject
  carries 9, likewise none an acceptance reservation. No apply-conditions.

**Decision.** Record the artifact as DR-102's accepted design contract, on the same terms and
in the same vocabulary as D-013 — the row stays `OPEN`, because the classes are
specifications and no harness executes them.

**Correction of record.** The turn-1 draft routed conformance-fixture authoring to
"DR-120/DR-G15". Measured in the subject: `DR-G15` **0**, `DR-G21` **8**, `DR-120` **4**; the
verdict likewise carries `DR-G15` 0. DR-G15 is the PACKAGING-ADAPTER-CONFORMANCE gate —
DR-103's route (correct there, per that artifact's ID-DEP-8), pasted onto this decision. A
named-but-wrong route reads as closed while stranding CC-1..CC-11 at a gate whose owner set
contains neither DR-102's protocol authority nor the containment authority. DR-G15 is dropped
from this row entirely; DR-120 is kept only where the subject puts it (T-4).

- **Alternatives considered:** as D-013 — use `SATISFIED`; coin a label; defer the row move.
  Rejected on the same grounds.
- **Readiness effect:** condition 2 gains **zero** `SATISFIED` rows. DR-127 gains **no**
  design-level supplier from CC-1..CC-11 — the classes are specifications, not executed
  evidence — and its cell is untouched. Conditions 1, 3, 4, 5 untouched.
- **No freeze or claim-register motion; no pins move** — same basis as D-013. The subject
  carries its citations under `recordedInputs.governingSources`, scoped by the sibling field
  `recordedInputs.discipline` to the authoring session.
- **One-vocabulary guarantee:** D-013 and D-015 use the same wording class, adopted together
  after both reached consensus, so no window existed in which the two rows could disagree.
  They remain separately revertible commits. Verified: `f0d72536…` (file 08), `797d4624…`
  (claim matrix) and `a3d0d266…` (this file) are pinned in no live document, so C-D013 and
  C-D015 strand nothing at any ordering relative to C-D014.
- **Reversibility:** total; no pinned source moves.
- **Overturn:** supersession here + `git revert` of C-D015; revert is total.
- **Reviewer:** the same three-turn cycle recorded at D-013.
- **Commit:** C-D015.

## D-016 — §3.1 item-4 carrier: route (b), the evidence lineage

- **Status:** ADOPTED 2026-08-13.
- **Decision type:** **PREFERENCE-LADEN.** D-001 §4 "Honesty about preference" names "the
  item-4 route choice (a vs b)" explicitly, and D-001's DR-002 entry (SF-4) required it be
  "DECIDED only at its own D-000-reviewed entry". This is that entry. The turn-1 draft carried
  it as part 4 of D-014 and declined the marking; both were wrong, and the turn-2 review
  showed why the bundling was not merely untidy: a decision recorded inside another decision's
  freeze rider cannot be overturned by reverting its own commit, so the overturn procedure
  would have been formal only.

**Decision.** The §3.1 item-4 carrier is **route (b)**, the evidence lineage.

**Measured basis.** The lineage carries `sealedCapabilityContract` and
`availabilityDifferential` exact-equal to `evidence.v10.json`'s values in each of the five
generations, v11 through v15 — measured by canonical-JSON subtree digests at v11
(`059d0b99…`, `a098bbab…`) and by direct structural comparison from v12 onward, which the v12
verdict states in terms ("measured by direct structural comparison … not by digest
convention"). The v15 verdict's `verifiedClean.item4Carriage` records it for both resolved v14
and v15.

**Attribution.** The supporting analysis is the register's own DR-004/DR-008 finding note
(file 08, recorded 2026-08-12): *"its two closure routes are (a) a `v29` restoring
`partB_purgeSemantics.distinction` from v24's reviewed bytes, or (b) applying an evidence
successor, which is DR-002 AC-1. Route (b) closes two things at once and is the better
trade"* — unrebutted. **D-001's** own words are weaker: its DR-002 entry RECOMMENDED (b) and
parked the decision to this entry. The turn-1 draft attributed the register's sentence to
D-001, which is the EV10-IR-02 defect class — a closure sentence false about its own source —
inside the decision register.

- **Alternatives considered:** *route (a)* — a `v29` restoring
  `retention-tiers.v24#$.partB_purgeSemantics.distinction` from v24's reviewed bytes. **Named
  as reachable, not foreclosed**, at the cost of a new authored artifact, a new independent
  review, and a **new instrument** (`check-retention-custody-v28.py` permanently refuses on
  the live tree, so a v29 cannot reuse it). Rejected here on the register note's trade, not on
  availability.
- **Reversibility:** total, and genuinely so — this decision touches exactly one file and no
  pinned source. C-D014's freeze rider names this decision by reference and asserts nothing
  about it, so reverting D-016 leaves no pinned source asserting a decision that no longer
  stands.
- **Overturn:** supersession here + `git revert` of C-D016; revert is total and costs no
  freeze edit, no pin cascade and no DR-001 re-open.
- **Severability:** had this entry alone failed consensus it would have parked CONTESTED
  without parking the v15 application, the AC-2 record, the AC-1 routing or the validator
  commissioning — all of which are D-014's and stand independently.
- **Reviewer:** the same three-turn cycle recorded at D-013. The turn-3 reviewer verified the
  split itself lawful against D-001 SF-4's actual words and confirmed D-014 reads coherently
  without it.
- **Commit:** C-D016 — this file only.

## D-014 — EVIDENCE: apply `evidence.v15`; AC-2 satisfied; AC-1 routed; validator commissioned

- **Status:** ADOPTED 2026-08-13.
- **Decision type:** RULE-GOVERNED throughout. The §3.1 item-4 carrier, which D-001 §4 marks
  preference-laden, is **not** decided here — it is **D-016**, and this decision asserts
  nothing about it.
- **Subject:** `evidence.v15.json`
  `28dc3c1aaa97f723afa8c079682a43999ca5c79686e7cde0f11e38421a179b29`.
- **Verdict:** `evidence.v15.review-independent.json`
  `3018c2f9cb14ba68e4a347092266e807ef620050e6eb2d7a0a5924af82d45aa1` — **ACCEPT, 0 blockers**,
  1 record-only advisory. Arc: v11 REJECT(3) → v12 REJECT(5) → v13 REJECT(1) → v14 REJECT(2) →
  v15 ACCEPT. Verdict standing: `sealRecommendation: DO-NOT-SEAL`,
  `integrationAuthorized: false`.
- **Route-A property:** MET; the verdict records `routeAAcceptanceProperty: "MET (0 blockers
  required; 0 measured)"` in its own bytes.

**Part 1 — applied.** The effective contract is the FULL-CHAIN resolution
v15→v14→v13→v12→v11→v10 — 20 declared operations over five links, every declared link digest
equal to measured — resolving at **0 errors** under both corpus resolvers to canonical
`4976151e6ccfd6fd25487e2ebf9e20af3b971e5bc4879b66f11b11c43ba3c573` (163,784 bytes, 43
top-level keys). `evidence.v10` is the full-text TERMINUS. A one-hop application of v15's three
operations directly over v10 **REFUSES at 3 errors** and must not be attempted: §7.3's terminus
rule is retention-v28's shape, and this lineage is its exact inverse. The turn-1 draft's
"one-hop per §7.3" was measurably false and was struck.

**Part 2 — AC-2 satisfied; AC-1 not discharged, and routed.** AC-2: five independent reviews,
each dispatched against frozen bytes not under authoring (§7.2.1). AC-1's descent chain and
resolved pointers are recorded in the DR-002 cell. The composition across five verdicts is the
**coordinator's**; the only verdict adjudicating AC-1 by name (v11) recorded `EV10-IR-01: NOT
DISPOSED` and `EV10-IR-02: PARTIALLY DISPOSED`, and no later verdict reverses those by name.
DR-204 already held the 2026-08-12 DR-001 disposition unlawful for its grade because it was
coordinator-recorded without independent review; recording a coordinator-composed AC-1 as
discharged would repeat that defect. **AC-1 is therefore routed to a focused independent
adjudication**, and the pending position is carried in the register row only — never in the
freeze rider — so the adjudication's return costs one register edit and no freeze motion, no
pin cascade and no further DR-001 re-open. No new status token is minted.

**Part 3 — AC-3 and AC-4 not discharged.** AC-3 rests on two true grounds: this decision
authorises no claim-register motion (the bound both the C-2 and R-1 records name), and AC-3's
own text requires binding artifact and validator to move together. The commissioned instrument
`check-evidence-resolved-head-28dc3c1a.py` (`e01d3524…`) exists and discharges both limbs of
D-001 NOTE-1, but its independent review **RETURNED REJECT at 1 blocker** (`IR-EVRH-B1`,
hostile-input totality; acceptance property NOT MET; verdict `5ad6b9a5…`), so the validator
half requires a **repaired successor and a fresh review**, not the return of a pending one; a
repair is commissioned. Stated correctly, the corpus precedents are: **C-2 is the model** — its
binding moved once the instrument carried standing; **R-1 is the counter-example the corpus
records** — its binding sits at v1.9 with the UNREVIEWED `check-r1-v1.7.py`, and
`check-package-coherence.py` reports `PC-6-REGISTER-AHEAD-OF-LEDGER` on the live tree. A
binding *has* moved with an unreviewed validator; this decision declines to do it again. AC-4:
the §3.1 eight-bullet packet does not exist (DR-004). The freeze §3 EVIDENCE seal stays
`UNSET — BLOCKS FREEZE`.

**Part 4 — DR-001 re-opens**, recorded in its status cell in this same commit, because
readiness condition 1 is evaluated over row status. Condition 1 nets to **zero** `SATISFIED`
rows until the re-record lands.

**Edits — one atomic commit.** Atomicity is necessary, not stylistic: this commit moves the
freeze **and** the blueprint, which together strand the same seven citations the 2026-08-12
record named, and §7.10 rule 2 holds that an intermediate state is not a pinnable state.
Landed: the freeze §3 EVIDENCE rider (chain members as **bare code-span digests, never links**,
because `bind_pairs()` binds any linked non-review `.json` in a §3 row as a binding artifact —
the tree already carries two `PC-3-ARTIFACT-ONLY-IN-FREEZE` findings created exactly that way
by the D-005 record); the blueprint §1.1 applied-head row; the register's DR-002, DR-001 and
DR-011-R06 cells (the last **NARROWED**, a word already in use on the sibling row); the five
live freeze pins (DR-004, DR-005, DR-006, DR-011, DR-012) and DR-011's blueprint pin; a new
pin-move record stating the count and **expressly superseding** the terminal-sync note's two
present-tense sentences, with property verification covering every cited property including §3
FACT-PLANE, §9, §7 outside the rider, R2-FINAL-03 and blueprint §1.1; the claim matrix's **Key
sealed laws** pin and its Evidence row; and both v1 manifests, which remain **MEASURED**, not a
SATISFIED re-record. New freeze `e809d4395f394a507c36c23c069d566c838b2283c931b6d2d13797be53406dbd`; new blueprint `909394c54dbd3588b9e455391f0fb2c5b1d2af51c9ca03b6802b1db47e44b7ad`.

**§7.9 census, measured before and after on this commit.** `check-package-coherence.py`:
**12 → 12**. `PC-5-STALE-HEAD(evidence)` **closed**; `PC-6-REGISTER-STALE-BINDING(EVIDENCE)`
**opened by design**, because reconciling the claim register is a separate coordinator act not
authorised here (the R-1 record of 2026-08-05 records the identical shape); `PC-3` did **not**
open for the evidence chain — the link discipline held, and the blueprint §1.1 row moved in the
same commit. Pre-existing and untouched: two `PC-7`, two `PC-3-ARTIFACT-ONLY-IN-FREEZE` and two
`PC-2-NO-DIGEST` from the D-005 record's links, one `PC-2-DIGEST-DRIFT` and one
`PC-3-DIGEST-DISAGREE` on the claim register, one `PC-5-STALE-HEAD(delivery)`, one
`PC-5-STALE-HEAD(r1)`, one `PC-6-REGISTER-AHEAD-OF-LEDGER(R-1)`.

**A standing condition measured and routed, not created here.** `artifacts/freeze-payload-manifest.txt`
is the §9.2 payload manifest, rooted at `docs/coop` and excluding the freeze itself. Measured at
this commit: **619 recorded paths against 694 live**, 3 already drifted
(`check-completeness.py` and `check-completeness-v2.py` from the reviewed dialect repair, and
`claim-register.v1.json`) and **75 absent**, including `COORDINATOR-DECISIONS.md` itself — the
coordinator lane's entire output post-dates the manifest's capture. This commit's blueprint edit
adds a fourth drift. The condition **predates this decision and is not caused by it**;
regenerating the manifest is a §9.2 act with its own recorded procedure and authority, so it is
**routed as its own act and is expressly not authorised here**. Recorded rather than left
silent, because a manifest that is 75 files behind is exactly the kind of surface that reads as
current to a later auditor.

- **Alternatives considered:** (a) *State the provenance plainly and grade AC-1 discharged* —
  rejected: DR-204 ruled that shape unlawful for its grade on DR-001, and repeating it inside
  the decision that repairs an instance of it is indefensible. (b) *One-hop application over
  v10* — rejected: measured, refuses at 3 errors. (c) *Defer the whole application until the
  adjudication returns* — rejected: the application is independently warranted at 0 blockers,
  and deferring would leave the corpus's documents naming v10 while a reviewed successor sits on
  disk (the live `PC-5-STALE-HEAD(evidence)` finding). (d) *Move the claim-register binding now*
  — rejected: AC-3 requires artifact and validator together, the validator's review returned
  REJECT, and the R-1 counter-example shows the cost. (e) *The item-4 carrier route (a)* — not
  this decision's; see D-016.
- **Reversibility:** one hop. `git revert C-D014` restores the freeze, blueprint, both manifests
  and every pin together — which is why it is atomic.
- **Overturn:** supersession here + `git revert C-D014`; the revert also restores DR-001's
  SATISFIED standing and re-opens `PC-5-STALE-HEAD(evidence)`. D-016 overturns independently.
- **Reviewer:** three turns under D-000's clause — turn 1: 19 MUST-FIX, 7 SHOULD-FIX, 5
  withdrawn; turn 2: 9 MUST-FIX, 4 SHOULD-FIX; turn 3: 13/13 discharges verified, 2 MUST-FIX,
  disposition **RECORD**. All 30 MUST-FIX and 11 SHOULD-FIX accepted; **zero rebutted**. The
  turn-3 reviewer additionally verified that routing AC-1 is honest rather than a route to
  failure, by resolving the chain independently and reading the three dispositions.
- **Commit:** C-D014.
- **Recorded limit.** No review turn examined the SUBSTANCE of the applied artifact; every
  objection audited whether this entry's statements about the verdict replicate. If the v15
  verdict is wrong on the merits, nothing in this cycle catches it.

---

## D-018 — Name D-002's slice an architecture preview

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13** — CONSENT from both independent reviewers at turn 2 of
  the D-017/D-018 cycle. Claude 2
  (`artifacts/coordinator-decisions.D-017-021.review-adversarial.claude2.turn2.json`,
  `36b60ca596a726913b27681674346fd8e214770790a7add3de51b66fef47bf44`): D-018 CONSENT, 0
  MUST-FIX, 0 SHOULD-FIX, 1 NOTE. Codex
  (`artifacts/coordinator-decisions.D-017-021.review-adversarial.codex.turn2.json`,
  `0bfa404f410fc63f7fe2a5dc835b67bc1dd595b4b3b512a8172e7b7eff0ae36e`): D-018 CONSENT, 0
  MUST-FIX, 0 SHOULD-FIX, 0 NOTE. The NOTE (cite DR-123/DR-G17 as the basis for "verdict and
  D9 exit") is recorded, not adopted into this entry's bytes.
- **Decision type:** **PREFERENCE-LADEN** (route C). D-002 already selected the first
  blueprint slice. This entry names that slice. It does not select Route B, does not adopt
  an execution sequence, and does not change D-002's command set, language-role set,
  platform set, deferral set, identity-dependency rides, condition-2 affected-row set, or
  condition-4 required-gate set.
- **Subject:** D-002's name only.

### Decision

1. **Naming.** D-002's adopted slice is the first milestone and is named **architecture
   preview**. "Slice 0" is an accepted synonym in new prose. Existing adopted bytes that
   say "first blueprint slice" or "slice 1" remain historically accurate names for the same
   D-002 decision; they are not silently rewritten. New coordinator and register prose uses
   "architecture preview" or "D-002 preview."
2. **What the name does not change.** This entry does not add or remove commands, language
   roles, platforms, deferrals, identity rides, or gates from D-002. Narrowing those sets
   is not decided here. If chosen later, that is a scoped D-002 successor with its own
   D-000 review.
3. **What the name forbids in later prose.** No later document may describe the D-002
   slice as:
   - producing an **authoritative sealed gate**,
   - **OpenSIP MVP**, or
   - **upgrade continuity** for `opensip-cli` users.
   The slice does produce a verdict and a D9 exit. What it cannot produce is a durable
   authoritative record of having gated, and it has no baseline/ratchet. That is D-002's
   T2-02 trade (this file, D-002 State paragraph), not a new surrender. DR-130 already
   records that the first slice claims no upgrade continuity.
4. **This entry does not select a condition-1 route** for any inherited row. Route
   selection is D-019 and D-020, if adopted.
5. **This entry does not authorize `docs/v2/implementation/`.** Condition 5 still forbids
   that until D-001's five conditions hold.
6. **File 11 item 1 is consumed only in part:** the preview-versus-MVP *naming*. The
   parallel-product posture half of file 11 item 1 remains undecided.

Changing any of the above requires a separately reviewed successor or supersession of this
entry.

- **Alternatives considered:** (a) *Treat D-002 as product MVP and leave the name
  unchanged* — rejected on D-002's own bytes: the slice's declared state classes are
  rebuildable cache/index and operational metadata; authoritative sealed closure, replay,
  and evidence custody are out; baseline/ratchet is deferred. Calling that slice MVP would
  describe a product the slice cannot be. (b) *Also select Route B, or also adopt an
  execution sequence, in this entry* — rejected: turn-1 bundling; D-016. (c) *Shrink
  D-002's platforms or independent-release machinery as part of the rename* — named as
  reachable, not foreclosed; rejected in this entry because it would rewrite D-002's
  adopted sets.
- **Honesty about the trade (D-000 clause 5):** What is given up: the first milestone will
  not be described as "measure, gate, and prove," and a prototype user still has no
  ratchet reason to switch. What is gained: later prose cannot overclaim the slice. A
  product owner could defensibly keep the D-002 name and accept the overclaim risk. This
  entry chooses the name.
- **Readiness effect:** Zero. No file 08 status cell moves. No freeze, claim-register, or
  pin motion.
- **Reversibility:** total.
- **Overturn:** one-line supersession plus `git revert` of C-D018. Revert restores D-002's
  unlabeled slice name and does not touch Route B selections or any sequence.
- **Reviewer:** two independent adversarial reviewers under D-000, turn 2 of 3. Both
  CONSENT on this entry. All MUST-FIX and SHOULD-FIX against the predecessor bundle were
  accepted and this entry is the naming-only remainder. Zero rebutted.
- **Commit:** C-D018.

---

## D-017 / D-019–D-024 — first completion-sequence cycle (CONTESTED)

- **Date:** 2026-08-13
- **Status:** **CONTESTED** after three turns under D-000 clause 2. Not adopted. No
  forced consensus. Parked. Successor drafts are D-025–D-031, a **new** cycle, not a
  fourth turn of this one.
- **Decision type:** mixed; see the terminated drafts. D-018 was severed and ADOPTED
  at C-D018 and is not part of this contest.
- **Subject drafts:**
  - turn 1 `coordinator-decisions.D-017-018.draft.md` `920667f9…`
  - turn 2 `coordinator-decisions.D-017-021.turn2.draft.md` `744ad8e3…`
  - turn 3 `coordinator-decisions.D-017-024.turn3.draft.md` `4cffad69…`
- **Terminal verdicts (turn 3):**
  - Claude 2 `coordinator-decisions.D-017-024.review-adversarial.claude2.turn3.json`
    `3fdc6294e2a1d5a3dc73d03328911fc44de7d42fdbdc4fc1677a0f4f34b2940c` — OBJECTIONS;
    consensus unavailable; surviving MUST-FIX: D-020/D-022 inherit D-019 operative
    clauses; shared recording rule extends D-000 to V1 surface authorities it does
    not name.
  - Codex `coordinator-decisions.D-017-024.review-adversarial.codex.turn3.json`
    `3d89052eeddcab30f2f250cb7474fa5ce699babb1b90321a3c14b925e4ce1548` — OBJECTIONS
    except D-024 CONSENT; surviving MUST-FIX: D-019–D-023 not self-contained
    (shared blocks + D-020/D-022 inherit D-019).
- **Both positions (required by D-000 clause 2):**
  - **Coordinator:** the destination acts (consume file 11 via D-001 routes; per-row
    preview Route B; scoped TM; two-lane sequence) remain the intended next
    decisions. The surviving defects are mechanical: inline operative text; do not
    extend D-000 to V1 surface owners; distinguish scheduling from live work.
  - **Reviewers:** CONSENT is unavailable on the turn-3 bytes. Claude 2 notes the
    MUST-FIX items are narrow and repairable in a fresh dispatch. Codex CONSENTs
    only D-024.
- **What proceeds:** work continues on other surfaces and on successor entries
  D-025–D-031. This contest does not authorize `docs/v2/implementation/`, write a
  Route B disposition, or move any file 08 status cell.
- **Commit:** C-D017-cycle-CONTESTED (this record plus the retained turn-3
  verdicts).

---

## D-028 — Select Route B for DR-005 (preview scope)

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Claude 2 turn-3 CONSENT
  (`42878e36…`). Codex: no MUST-FIX; operative bytes pass; remaining
  SHOULD-FIX is the shared draft header, not this entry
  (`bc5172c4…`).
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-005 only.
- **Owning V1 authority (file 08):** Evidence, storage, and operability
  authorities.
- **Decision:** Select Route B for DR-005, architecture preview only.
  Preview-scoped. Full V10/custody and G19 demonstration remains owed
  whether or not a scoped-TM selection is adopted. Coordinator selects;
  named owners record; coordinator may draft; D-000 does not make the
  coordinator those authorities. Writes no disposition. Marks nothing
  `SATISFIED`. A completed, reviewed, owner-recorded disposition may
  discharge condition 1 for DR-005 within its preview scope. Conditions
  2–5 remain independently required. Condition 5 remains the only
  authorization for `docs/v2/implementation/`.
- **Alternatives:** Leave on full Route A (reachable; rejected for
  preview scope). Fold into TM selection (rejected: different fact).
- **Honesty:** Preview does not wait for G19; full demonstration remains
  owed.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition lands.
  After one lands, overturn also requires that disposition's
  owning-authority supersession. **Commit:** C-D028.

---

## D-029 — Select Route B for DR-008's integration half (preview scope)

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Claude 2 turn-3 CONSENT. Codex:
  no MUST-FIX; operative effect accurate; remaining SHOULD-FIX is the
  shared header.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-008 EVIDENCE/D9 integration half only. Posture remains
  closed.
- **Owning V1 authority:** evidence/retention authority (contract half).
- **Decision:** Select Route B for that half, preview only. Authoritative
  remaining work (evidence-side successor consuming retention **and**
  Phase-1A) remains owed. Adoption permits authoring the later
  disposition; it is not itself design permission. Condition 1
  discharges only after an owner-recorded reviewed disposition.
  Conditions 2–5 remain. Condition 5 is the only implementation
  authorization.
- **Readiness effect:** Zero.
- **Reversibility:** total before dependents; then also revert those
  dispositions. **Commit:** C-D029.

---

## D-030 — Select Route B for a scoped preview threat model under DR-003

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Claude 2 turn-3 CONSENT. Codex:
  operative bytes pass; remaining SHOULD-FIX is the shared header.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-003, preview scope only.
- **Owning V1 authority:** Threat-model authority + V1 coordinator.
- **Decision:** Select Route B for a scoped preview TM covering every
  boundary D-002 ships, including but not limited to command, input,
  process/protocol, state, output, platform, and trust (hostile
  repository/source, parser/provider admission, four-platform matrix,
  first-install trust, doctor, signed delivery, Node closure). Full TM
  / V10 / G19 / publication-block stay Route A. D-028 does not
  discharge that. Wave-through rejected. Writes no TM artifact. Marks
  nothing `SATISFIED`. Authorizes no blueprint.
- **Readiness effect:** Zero.
- **Reversibility:** total before dependents. **Commit:** C-D030.

---

## D-035 — Record doctor-contract.v4 as DR-114's accepted design contract

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13** — RULE-GOVERNED recording of an
  independent ACCEPT-WITH-ADVISORIES (0 blockers).
- **Subject:** `doctor-contract.v4.json`
  `df2e717555616db096e61548458f23b442f7f0e37b2d2461eabc2c33201e94b3`.
- **Verdict:** `doctor-contract.v4.review-independent.json`
  `d63288079bcc9d7a68e2de54069e83910eaaf3aa53c53707a45d5730908196b2`.
- **Decision:** Record v4 as DR-114's accepted design contract on the
  same terms as D-013/D-015. The row stays `OPEN`: actor-scope and
  fixture execution unmet. Advisories A1–A6 are not blockers; they do
  not prevent this recording. No freeze motion. No `SATISFIED`.
- **Readiness effect:** condition 2 gains zero `SATISFIED` rows.
- **Overturn:** supersession + revert of C-D035. **Commit:** C-D035.

---

## D-032 — DR-105 / DR-114 actor scope (Option B + measured tails)

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 3 of 3: zero MUST-FIX from
  either reviewer. Claude 2 SHOULD-FIX (BLK-6 write token) and Codex
  SHOULD-FIX (catalog + CA-3 routes) accepted into these bytes.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** whether host surfaces under the user's direct
  instruction are subject to DR-105 component permissions.
- **Decision:** Host-under-instruction is outside DR-105 (fourth
  deliberate non-token). Doctor consent is a doctor-side
  invocation-bound record, not a grant. Component tails (CA-1 spawn,
  component CA-4 egress) stay in DR-105. Host-actor owners:
  Operability + security jointly with Security + platform owners. A
  scoped host-effect authorization contract is **necessary, not
  sufficient**, before CA-1 host head, CA-2, CA-3, or host CA-4 is
  exercisable; until then fail-closed. That contract's mandatory
  minimum includes typed host outcomes: completed,
  definitely-not-performed, unknown/indeterminate (BLK-3 stays
  STILL-ROUTED, not discharged). CA-2 also needs DR-119 (and
  DR-117/128 if third-party). CA-3: out-of-root read, local
  socket/pipe, privileged facility → host-effect contract;
  keychain → DR-108, still deferred, unexercisable. `permissionRef`
  permanently reserved. Slice-1 doctor egress execution side remains
  for that contract. Join blockers: BLK-1/2/3/4 STILL-ROUTED as
  above; BLK-5 DISCHARGED; BLK-6 DISCHARGED-AS-INAPPLICABLE for host
  default **reads and** doctor's operational-metadata write
  (FS-WRITE-HOST-STATE is not a component grant; fail-closed if that
  class is denied); BLK-7 REPAIRED-IN-V4. Applies no candidate.
- **Readiness effect:** Zero. No SATISFIED. No blueprint.
- **Reversibility:** total before conforming successors; then also
  their owning-authority supersession. **Commit:** C-D032.

---

## D-036 — Coordinator execution sequence (partial order)

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Claude 2 turn-3 CONSENT
  (`…claude2.turn3.json`). Codex no MUST-FIX; remaining SHOULD-FIX
  (pin turn-2 verdicts) accepted into the catalog below.
- **Decision type:** PREFERENCE-LADEN.
- **Depends on:** D-018 (ADOPTED). Uses D-028, D-029, D-030
  (ADOPTED) when their dispositions are authored. Does not require
  D-025.
- **Decision:** Two lanes. Lane R = condition-1 Route A work, starts
  now, including the §3.1 supplier-coverage instrument (one
  instruction: it starts). Lane P is a **partial order**: P1 product
  decisions, P2 register-mechanics, P3 actor-scope, P4a D-028
  disposition, P4b D-029 disposition are independently ready; P4c
  D-030 waits on P3 only if the TM must name the actor split (test:
  adopted D-030 bytes + DR-003 file-08 cell); P5 analyze contracts
  wait on P1 only. Changing that node set requires a successor.
  Owner = file-08/D-001 surface owner. Contended owner: Lane R item
  before that owner's Lane P item. Scheduling authorizes drafting
  only. Authorizes no blueprint. Condition 5 remains the only
  implementation authorization. Condition 2 follows SF-3; condition
  4 follows D-001/D-002; this entry changes neither.
- **Turn-2 verdicts pinned:** Claude 2
  `cd626b909619fa59b128b0c23478b60d53c90be7370bbd4a916a25c4ae32dbcb`;
  Codex
  `cca4d2e53a0090a37205cbfa0c642e4ddefea5a77cf4d3bcbfb40aa1a867983a`.
- **Readiness effect:** Zero.
- **Reversibility:** total before execution; then prospective.
  **Commit:** C-D036.

---

## D-037 — Consume file 11 via D-001 routes

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-037.review-adversarial.claude2.turn2.json`,
  `a296494f32c9e2f3151a360074579f108d14970141ff189bb4831ddb7320af93`).
  Codex
  (`artifacts/coordinator-decisions.D-037.review-adversarial.codex.turn2.json`,
  `f7b995208a740ed4beb3322684ccf71229e20e0bc515dd07411779b58bbe5999`).
  Turn-1 Claude 2 SHOULD-FIX C2-D037-01 and C2-D037-02 accepted into
  the adopted bytes. Codex NOTE-D037-T2-01 is this recording.
- **Decision type:** RULE-GOVERNED. Restates file 08's only-checklist
  rule, file 07/10 competing-list disclaimers, file 11's header, and
  D-001 A/B/C. Adds no fourth route.
- **Supersedes:** CONTESTED D-017 and the unadopted D-025 draft only.
  D-025 has no register entry and is not CONTESTED. D-028, D-029,
  and D-030 from that cycle are ADOPTED and are not superseded.
- **Subject:** the relationship between file 08 and file 11.

### Decision

1. File 11 has no authority. File 08 wins on workflow; V1 on
   meaning; D-001 on done.
2. "Complete 08 then turn to 11" is not a lawful sequence.
3. File 11 items become live work only via D-001 A, B, or C.
   Route C recording forms this corpus has used include, but are
   not limited to: product packet; user-made coordinator-register
   record; D-000 on-behalf entry. New forms still need authority
   from the product-disposition process, D-000, or the user.
   File-08 amendments are not a fourth route. Per MF-6, any
   file-08 content change still needs its own D-000-reviewed
   entry. A product act is not a substitute for that review.
4. Scheduling (D-036) authorizes drafting only, not live work.
5. D-001 is not amended. No wholesale gap import. File 11
   placement not decided.
6. After an item becomes live work, file 11 is historical for
   that item, not a queue. This entry creates no execution
   checklist.

- **Alternatives considered:** (a) Treat 11 as a second checklist —
  rejected. (b) Closed three-form Route C set — rejected (D-025
  defect). (c) Product packet substitutes for MF-6 — rejected.
  (d) Call the unadopted D-025 draft CONTESTED — rejected: no such
  register record exists; CONTESTED is a closed status word.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D037. If D-036's scheduling
  citation of this rule exists, that citation is independent
  (D-036 already states the rule in full).
- **Reviewer:** two independent adversarial reviewers under D-000,
  turn 2 of 3. Both CONSENT. Zero rebutted.
- **Commit:** C-D037.

---

## D-038 — Record host-effect-authorization.v8 as the accepted host-effect design contract

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-038.review-adversarial.claude2.json`,
  `294bf1bc9ab8022ae47f0626c3fd0204e7fd84236d40032cb6317c70592afc12`).
  Codex
  (`artifacts/coordinator-decisions.D-038.review-adversarial.codex.json`,
  `f4142a15ad0908448ebaf536e51d37b20757ca3de2c036082b52c9836d61a007`).
  Claude 2 NOTE-C2-D038-N1 recorded: v8's own header remains
  AWAITING-INDEPENDENT-REVIEW in its frozen bytes; this entry is
  the coordinator standing, the same split D-035 used for doctor
  v4. Codex NOTE-D038-01 is this recording.
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT
  (0 blockers from both reviewers) of the contract adopted D-032
  commissioned. Same recording form as D-035.
- **Subject:** `docs/coop/artifacts/host-effect-authorization.v8.json`
  `2cbad5612e546d3bf915074a8ad3fc4cae444122c997e2ddb3fe067d3cd022dc`.
- **Verdicts:** Claude 2
  `host-effect-authorization.v8.review-independent.claude2.json`
  `36a961e82a375778e71a08e7a66067843abb29a26170c84c38a12f15e121dec9`
  ACCEPT, 0 blockers. Codex
  `host-effect-authorization.v8.review-independent.codex.json`
  `3be46716fd7156e1b1ea23d4e2c5b55e16fafc8b834d824cedc3a8a66d15de93`
  ACCEPT, 0 blockers.

### Decision

1. Record `host-effect-authorization.v8.json` as the accepted
   host-effect **design contract** D-032 required.
2. This recording is the D-035 analogue. It is not FC-C1. FC-C1
   remains: Operability+security jointly with Security+platform
   must record a live instance. Coordinator recording of the
   accepted candidate is not that instance. Host acts stay
   unexercisable.
3. DR-105 and DR-114 stay `OPEN`. No `SATISFIED`. No freeze
   motion. No blueprint. No `docs/v2/implementation/`.
4. Join blockers BLK-1/2/3/4 remain STILL-ROUTED. This entry
   discharges none of them.
5. A later file-08 cell note that names this recording is a
   separate MF-6 act if it changes register content. This entry
   does not edit file 08.

- **Alternatives considered:** (a) Leave v8 unrecorded until owners
  write an instance — rejected: D-035 already records an accepted
  design contract while the row stays OPEN. (b) Treat this as
  FC-C1 — rejected: v8's own fail-closed rule forbids it. (c) Mark
  DR-105 or DR-114 SATISFIED — rejected.
- **Readiness effect:** Zero. No SATISFIED. No blueprint.
- **Reversibility:** total. Overturn: C-D038.
- **Reviewer:** two independent adversarial reviewers under D-000,
  turn 1 of 3. Both CONSENT. Zero rebutted.
- **Commit:** C-D038.

---

## D-033 — Property pins for DR-001 citations

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-033.review-adversarial.claude2.turn2.json`,
  `d7a50cf0442be1c79b8b45eea998eddd5de987396085a4070f5a2b6c88fd2fe3`).
  Codex
  (`artifacts/coordinator-decisions.D-033.review-adversarial.codex.turn2.json`,
  `e687ef1e13e80a1a4adaa07c13cc59d36f4528aee6b5315745cc357cc25c4373`).
  Turn-1 MUST-FIX C2-D033-01 / ADV-D033-01 accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Applies freeze §7.10 to the
  register's own DR-001 citations. Adds no file-08 status token.
  Does not amend D-001's five conditions.
- **Subject:** DR-001 citation form only. Not live-versus-history.
  Not DESIGN-READY. Not condition 5.

### Decision

1. **Citation form.** Whole-document freeze and blueprint pins used
   as DR-001 (and, when those rows cite the same way, DR-004 / DR-005
   / DR-006 / DR-011 / DR-012) standing citations convert to property
   pins: `(path, named section or selector, segment hash)`. A later
   edit that does not change the cited property does not re-open the
   row.
2. **Scope clause.** DR-001's live scope clause is rewritten, by a
   later register-content act under MF-6, so the row re-opens only
   when a *cited property* changes, not on any baseline or freeze
   motion. This entry authorizes that rewrite. It does not perform
   it. Performing it is a file-08 content change and needs its own
   D-000-reviewed commit (D-001 MF-6).
3. **One last lawful re-open.** Executing clause 2 will re-open
   DR-001 by today's scope clause. That re-open is expected. The
   SATISFIED re-record remains the D-001 two-stage act (regeneration
   MEASURED now; SATISFIED only after DR-204 audits the disposition).
   This entry is not that re-record.
4. **No new status token.** File 08 status vocabulary stays closed
   (D-006 turn-2 NOTE-03).
5. **No implementation authorization.** Condition 5 is unchanged.

- **Alternatives considered:** (a) Keep whole-document pins —
  rejected: recorded DR-001 treadmill. (b) Also convert live cells
  to history and also coin DESIGN-READY — rejected in this entry:
  bundling. (c) Perform the file-08 rewrite in this same commit —
  rejected: MF-6.
- **Readiness effect:** Zero at adoption. Zero SATISFIED. The later
  MF-6 rewrite will re-open DR-001 once, by today's clause.
- **Reversibility:** total before the MF-6 rewrite lands. After that
  rewrite, overturn also requires reverting or superseding the
  rewrite commit. Overturn: C-D033.
- **Reviewer:** two independent adversarial reviewers under D-000,
  turn 2 of 3. Both CONSENT. Zero rebutted.
- **Commit:** C-D033.

---

## D-040 — Record the DR-008 integration-half preview Route B disposition

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-040.review-adversarial.claude2.json`,
  `1c111016a270b5ea311a99c9a9c805460313a8ab198352b35bd63e077bbe03ab`).
  Codex
  (`artifacts/coordinator-decisions.D-040.review-adversarial.codex.json`,
  `464bbb02a586f93921a286edde51ed5e834e80484f48340f4ae8ac781138958f`).
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT of
  the D-029 disposition draft. Same form as D-038.
- **Subject:** `route-b.DR-008.preview-disposition.v2.json`
  `8b2d21392bde0906ea75a6c29b1083e3b441205fd3eafb66a13135734a9ca41c`.
- **Decision:** Record that v2 disposition as the accepted draft
  D-029 authorized, for the EVIDENCE/D9 integration half only.
  Posture half stays closed. Owner remains evidence/retention
  authority. This is not owner recording. DR-008 stays PARTIALLY
  SATISFIED. Condition 1 does not discharge for that half until
  the owner records. Conditions 2–5 remain. Condition 5 remains
  the only implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D040.
- **Commit:** C-D040.

---

## D-041 — Record the DR-003 scoped preview TM disposition

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-041.review-adversarial.claude2.json`,
  `1f6e121eb0731669d380dfd12b83ffe8a36d26d5cf4f9d018ad93bc3bad3f96b`).
  Codex
  (`artifacts/coordinator-decisions.D-041.review-adversarial.codex.json`,
  `c198509689a2312a144add0795cb9ca0fcfd1b8eb3b18f8f70dd22693a8007ff`).
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT of
  the D-030 scoped TM draft. Same form as D-038.
- **Subject:** `route-b.DR-003.preview-tm.v2.json`
  `d9084d4dc16bb450562520c2bed77cd80129bc65763f7ec2f55f3476c8989f52`.
- **Decision:** Record that v2 scoped preview TM as the accepted
  draft D-030 authorized. Owners remain Threat-model authority +
  V1 coordinator. This is not owner recording and is not a
  security-complete claim. DR-003 stays HARD-BLOCKED / TM UNSET
  for the freeze. Full TM / V10 / G19 / publication-block remain
  Route A. Condition 1 does not discharge until the owners record.
  Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D041.
- **Commit:** C-D041.

---

## D-039 — Record the DR-005 preview Route B disposition

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-039.review-adversarial.claude2.turn2.json`,
  `0e1994b213e2afc663b13eb7514d557569dfb20d0b20999123d947ade6e9ba5c`).
  Codex
  (`artifacts/coordinator-decisions.D-039.review-adversarial.codex.turn2.json`,
  `8800c096d604f37386adf00b24c799bda133d1aafe2697275f246621691ff578`).
  Turn-1 Claude 2 SHOULD-FIX C2-D039-01 and C2-D039-02 accepted
  into these bytes.
- **Decision type:** RULE-GOVERNED. Records an independently
  reviewed disposition draft. Codex independent verdict was
  ACCEPT-WITH-ADVISORIES, not ACCEPT. Same recording form as D-038.
- **Subject:** `route-b.DR-005.preview-disposition.v2.json`
  `3b50bcf15e207b698283cb51e77335bceaf46f053f961f0de2b9b8d20982b809`
  plus the adopted rider in clause 2.

### Decision

1. Record the v2 disposition as the accepted draft D-028
   authorized. Owners remain Evidence, storage, and operability
   authorities. This is not owner recording. An ACCEPT or
   ACCEPT-WITH-ADVISORIES verdict is not owner recording.
2. The disposition owners must record is v2 plus this rider
   (RB-DR005-V2-A1): if the Operational metadata class is denied,
   doctor fails closed (D-032 BLK-6); this disposition supplies no
   grant or class admission. The rider is operative disposition
   text.
3. DR-005 stays HARD-BLOCKED / not SATISFIED. Condition 1 does
   not discharge until those owners record v2 plus the rider.
   Conditions 2–5 remain. Condition 5 remains the only
   implementation authorization.
4. Does not edit file 08 (MF-6).

- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D039.
- **Commit:** C-D039.

---

## D-042 — Record permission-truth-tables.v2 as DR-105's accepted design-contract candidate

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-042.review-adversarial.claude2.turn2.json`,
  `dd663c6c23c9b8c1532edb69d9c392cf6708b055cb61911cc16679c9b1924677`).
  Codex
  (`artifacts/coordinator-decisions.D-042.review-adversarial.codex.turn2.json`,
  `171b22f60bf72311fdb5be909d269b0d492112957a43ddc7c031bcf1143aa889`).
  Turn-1 Claude 2 SHOULD-FIX C2-D042-01 accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Records independent
  ACCEPT-WITH-ADVISORIES (0 blockers from both reviewers). Same
  form as D-035 / D-038.
- **Subject:** `docs/coop/artifacts/permission-truth-tables.v2.json`
  `cce3afcaee90bbca388825a474751d6ebb17b30722b35dadcf6c631b34a8731a`.
- **Verdicts:** Claude 2
  `permission-truth-tables.v2.review-independent.claude2.json`
  `021bacaf071dfa682e3e85574f42306adc3f2b12607e0bbd94b01aa344389301`
  ACCEPT-WITH-ADVISORIES, 0 blockers. Codex
  `permission-truth-tables.v2.review-independent.codex.json`
  `c32f98751b848e3d2ccbe6e9927e60ea8e640f0b655315ebd1fc295c5a1e856d`
  ACCEPT-WITH-ADVISORIES, 0 blockers.

### Decision

1. Record v2 as DR-105's accepted design-contract candidate.
2. The row stays `OPEN`. Remaining unmet, named: fixture execution
   (DR-G09); join blockers BLK-1/2/3/4 STILL-ROUTED;
   host-under-instruction outside this vocabulary (D-032);
   host-effect live instance (FC-C1) unmet. This recording
   discharges none of those.
3. Advisories P2-01, P2-02, P2-03, and PT2-CX-A1 remain owed as
   honesty work on a successor.
4. No `SATISFIED`. Does not make any host or component act
   exercisable. Does not edit file 08. No freeze motion. No
   blueprint.

- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D042.
- **Commit:** C-D042.

---

## D-043 — Record section31-supplier-coverage.v3 as the accepted Lane R instrument

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-043.review-adversarial.claude2.turn2.json`,
  `9c254021fb8b7a1e0b20cf8b0d3ada6717b2a3a9f699d49dfa4c81efe27ddb1e`).
  Codex
  (`artifacts/coordinator-decisions.D-043.review-adversarial.codex.turn2.json`,
  `4d548c6bbdeefd27a3de3c3491eb4f62c22482750a9319664d962f2794c0932f`).
  Turn-1 Claude 2 SHOULD-FIX C2-D043-01 and NOTE-C2-D043-01
  accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Records independent
  ACCEPT-WITH-ADVISORIES (0 blockers from both reviewers). Same
  form as D-035 / D-038 / D-042.
- **Subject:** `docs/coop/artifacts/section31-supplier-coverage.v3.json`
  `9a544eb2a60012d0c312cbb9ce237e7743942472ba9834fe35821bdd1f1e80d0`
  and `docs/coop/artifacts/check-section31-supplier-coverage-v3.py`
  `b139c43a6af3237a6d1d3b20791d51d35a7bcf9eefe472fb09601b14b13f6446`.
- **Verdicts:** Claude 2
  `section31-supplier-coverage.v3.review-independent.claude2.json`
  `08cc0583ad1d01a8816480bd671ea70e680bbf004b2445a3fd58373ea08c9fe9`
  ACCEPT-WITH-ADVISORIES, 0 blockers. Codex
  `section31-supplier-coverage.v3.review-independent.codex.json`
  `d7b0fbfba1a6b345a7a691b5de51e81a14de1b322dcf2e2ea0e688b39d85fe41`
  ACCEPT-WITH-ADVISORIES, 0 blockers.

### Decision

1. Record v3 as the accepted §3.1 item-to-supplier binding
   instrument D-001 commissioned and D-036 started on Lane R.
2. It is not the Phase-1A packet. It is not SATISFIED evidence.
   Bound=1 (CD-RT-5 default posture), unbound=7. Item 1 stays
   UNBOUND because no head supplies verdict claims together with
   match / no-match / indeterminate / error.
3. Remaining unmet, named: the seven UNBOUND items; checker
   typed-FAIL on a BOUND row with no supplier key (S31V3-01);
   PASS does not prove semantic completeness of a bound head
   (S31V3-02); predecessor Codex verdict token is recited in
   lowercase rather than the pinned `ACCEPT-WITH-ADVISORIES`
   enum (S31V3-CX-A1). Those advisories remain owed on a
   successor.
4. DR-002 and DR-004 stay HARD-BLOCKED. This recording
   discharges neither. Condition 1 does not discharge. DR-004's
   Route A still needs the eight-bullet Phase-1A packet, of
   which this instrument is the other commissioned limb.
   Conditions 2–5 remain. Condition 5 remains the only
   implementation authorization. Does not edit file 08 (MF-6).
   A later file-08 cell note that names this recording is a
   separate MF-6 act if it changes register content. No freeze
   motion. No blueprint.

- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D043.
- **Commit:** C-D043.

---

## D-044 — Perform the D-033 property-pin rewrite

- **Date:** 2026-08-13
- **Status:** **ADOPTED 2026-08-13.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-044.review-adversarial.claude2.turn2.json`,
  `a87772f698942eb50d4232ab3aadb5c99692adda1aa2d4dd0b35bb1c2db87edd`).
  Codex
  (`artifacts/coordinator-decisions.D-044.review-adversarial.codex.turn2.json`,
  `2f4255025b1ec2105a691deed61a510b362c555510a999ce79959983701afab3`).
  Turn-1 Claude 2 SHOULD-FIX C2-D044-01 accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Performs the file-08 rewrite
  D-033 authorized and refused to perform in the same commit
  (D-001 MF-6). Adds no file-08 status token. Does not amend
  D-001's five conditions.
- **Subject:** file 08 citation form and DR-001 live scope clause
  only.

### Decision

1. **Perform the citation conversion.** In file 08, whole-document
   freeze and blueprint pins used as standing citations on
   DR-001 / DR-004 / DR-005 / DR-006 / DR-011 / DR-012 convert
   to the property pins in the adopted table. A later edit that
   does not change a cited property does not re-open that row.
2. **Perform the scope rewrite.** DR-001's live scope clause
   becomes: this row re-opens only when a cited property pin in
   its source-pin cell changes (path missing, named
   section/selector/law/row unresolvable, or segment hash
   mismatch). A whole-document motion of the freeze, blueprint,
   baseline, or this register that does not change a cited
   property does not re-open the row. The sentences "A baseline
   refresh re-opens it" and turn-3 R5 "any pinned-source motion
   re-opens the row" cease to be live scope. They remain
   history. Both occurrences of "A baseline refresh re-opens it"
   in the DR-001 cell cease to be live scope.
3. **Expected re-open.** This rewrite re-opens DR-001 by today's
   (pre-rewrite) scope clause. That is the one last lawful
   re-open D-033 clause 3 predicted. Live standing stays `OPEN`.
   The 2026-08-13 SATISFIED disposition stays history.
   SATISFIED re-record remains the D-001 two-stage act
   (MEASURED regeneration now; SATISFIED only after independent
   review). This entry is not that re-record.
4. **Does not edit** `v1-authority-baseline.json` or
   `v1-status-evidence.json`. Those files stay whole-document
   until a later MEASURED regeneration. This entry is not that
   regeneration.
5. **No new status token.** File 08 status vocabulary stays
   closed (D-006 turn-2 NOTE-03).
6. **No implementation authorization.** Condition 5 is unchanged.
   No freeze motion. No blueprint. No `docs/v2/implementation/`.
   No row becomes `SATISFIED`.
7. **Snapshot.** The dated current-position block's condition-1
   clause is updated so its leading label still matches the
   DR-001 cell (OPEN, now by D-044). Rows remain authoritative.

The claim-matrix **Key sealed laws** pin is outside this entry's
file-08 scope and outside D-033 clause 1. Routed to a later
file-09 D-000 act. Left whole-document until then.

- **Readiness effect:** Zero SATISFIED. DR-001 stays OPEN.
- **Reversibility:** compound after the rewrite lands. Overturn:
  C-D044, plus restore of the prior scope clause.
- **Commit:** C-D044.

---

## D-045 — Record section31-supplier-coverage.v4 as the Lane R successor

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-045.review-adversarial.claude2.turn3.json`,
  `bf7ba92d2fa8fcd9d54c861840e8c05d74e3ac81492e41bb1bede8e42b927f80`).
  Codex
  (`artifacts/coordinator-decisions.D-045.review-adversarial.codex.turn3.json`,
  `78de029a47e80cf31f72985690b2e115562e724da639446b9deea55cbc8acbbb`).
  Turn-1 Codex SHOULD-FIX ADV-D045-T1-01 and turn-2 Claude 2
  SHOULD-FIX C2-D045-T2-01 accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Records independent
  ACCEPT-WITH-ADVISORIES (0 blockers from both reviewers). Same
  form as D-035 / D-038 / D-042 / D-043.
- **Subject:** `docs/coop/artifacts/section31-supplier-coverage.v4.json`
  `97727684af2d812d3a677add9b15287db81d6fe36aeaa96d72d5118890a847f6`
  and `docs/coop/artifacts/check-section31-supplier-coverage-v4.py`
  `a30928260e9ddd36c680a13925d40353c362151f8729b99b021d400b5c2f96c2`.
- **Verdicts:** Claude 2
  `section31-supplier-coverage.v4.review-independent.claude2.json`
  `7bef5029c22dba134db62d7f2c055a631ef9960fdd5caeeb03f99d57bdcf22c7`
  ACCEPT-WITH-ADVISORIES, 0 blockers. Codex
  `section31-supplier-coverage.v4.review-independent.codex.json`
  `1db18b810262bb57ac2b56cb462a5b24bcb91146510f71258c52bd55b8f08fa9`
  ACCEPT-WITH-ADVISORIES, 0 blockers.

### Decision

1. Record v4 as the accepted §3.1 item-to-supplier binding
   instrument succeeding D-043's v3. D-043 remains history.
   S31V3-01 is discharged by execution on these bytes.
   S31V3-02 and S31V3-CX-A1 are discharged by byte comparison —
   the doesNotFailWhen disclosure and the pinned predecessor
   verdict tokens respectively.
2. It is not the Phase-1A packet. It is not SATISFIED evidence.
   Bound=1 (CD-RT-5 default posture), unbound=7. Item 1 stays
   UNBOUND because no head supplies verdict claims together with
   match / no-match / indeterminate / error.
3. Remaining unmet, named: the seven UNBOUND items; stale
   recordedInputs on COORD and file 08 (S31V4-01 / S31V4-CX-A1);
   whole-file freeze gate after D-044 gave DR-004 a §3.1 segment
   pin (S31V4-02); adjacent malformed supplier shapes still
   untyped (S31V4-CX-A2). Those advisories remain owed on a
   successor.
4. DR-002 and DR-004 stay HARD-BLOCKED. This recording
   discharges neither. Condition 1 does not discharge. DR-004's
   Route A still needs the eight-bullet Phase-1A packet, of
   which this instrument is the other commissioned limb.
   Conditions 2–5 remain. Condition 5 remains the only
   implementation authorization. Does not edit file 08 (MF-6).
   A later file-08 cell note that names this recording is a
   separate MF-6 act if it changes register content. No freeze
   motion. No blueprint.

- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D045.
- **Commit:** C-D045.

---

## D-046 — Convert the claim-matrix Key sealed laws pin

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-046.review-adversarial.claude2.turn2.json`,
  `6e279b84ab89c7e14d594107d5fc0140f297652cac4813cd23a7eca7e0666a74`).
  Codex
  (`artifacts/coordinator-decisions.D-046.review-adversarial.codex.turn2.json`,
  `e89db7c4c5f306f22d94226796c22c5565cbab9741ae709d354dac147e253982`).
  Turn-1 Claude 2 SHOULD-FIX C2-D046-01 and Codex SHOULD-FIX
  ADV-D046-T1-01 accepted into these bytes.
- **Decision type:** RULE-GOVERNED. Performs the file-09 conversion
  D-044 named and routed. Same extraction rule as D-033 / D-044.
- **Subject:** file 09 Key sealed laws standing citation only.

### Decision

1. Convert the Key sealed laws source pin from whole-file freeze
   digest `e809d439…` to the §6 property pin
   (`docs/coop/IMPLEMENTATION-FREEZE.md`, heading `## 6.
   Non-negotiable implementation laws`, segment
   `bfa71f42fb1e25d7d9556ea7549723b8e91af205147d3cca0d34558e1eba3b5e`).
2. Does not edit file 08. Does not edit the baseline JSON.
   Does not convert any other file-09 row.
3. No SATISFIED. Condition 1 does not discharge. Conditions
   2–5 remain. Condition 5 remains the only implementation
   authorization. No freeze motion. No blueprint.
   File-09 content change is this D-000-reviewed act (MF-6).
4. **Refresh-rule classification.** This is property-pin
   maintenance outside file 09's "Refreshing this matrix"
   rule. The source path, freeze bytes, section selector,
   laws 1–19, standings, and every other row remain unchanged.
   `v1-authority-baseline.json` `/sources/1` intentionally
   retains the whole-file freeze snapshot. Any later
   substantive matrix change still triggers the full
   baseline / every-row / five-lane refresh.

- **Readiness effect:** Zero.
- **Reversibility:** compound after the rewrite lands. Overturn:
  C-D046, plus restore of the prior whole-file freeze pin
  `e809d439…` as the Key sealed laws source pin.
- **Commit:** C-D046.

---

## D-047 — Select Route B for DR-002 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-047-048.review-adversarial.claude2.turn2.json`,
  `c0326396aa26863fd68d25da08075664b3989ee2028ab24c067686496e1a5d25`).
  Codex
  (`artifacts/coordinator-decisions.D-047-048.review-adversarial.codex.turn2.json`,
  `1bd7d8ad53ae503bbf67496cd9a5d16c2a7a14dd2e4ef3b13fe0c992de551f7e`).
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-002 only.
- **Owning V1 authority (file 08):** Evidence authority + V1
  coordinator.
- **Decision:** Select Route B for DR-002, architecture preview
  only. This selection is one row. Preview-scoped. AC-1
  adjudication, AC-3 validator + claim-register motion, and
  AC-4 Phase-1A packet remain owed on the authoritative path.
  Coordinator selects; named owners record; coordinator may
  draft. D-000 does not make the coordinator the Evidence
  authority. Independent review is required. A
  coordinator-composed SATISFIED is unlawful (DR-204). Writes
  no disposition. Marks nothing SATISFIED. Authorizes no
  blueprint. A completed, reviewed, owner-recorded disposition
  may discharge condition 1 for DR-002 within the scope it
  names. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D047.
- **Commit:** C-D047.

---

## D-048 — Select Route B for DR-004 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-2
  verdicts as D-047.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-004 only.
- **Owning V1 authority (file 08):** Evidence/retention authority.
- **Decision:** Select Route B for DR-004, architecture preview
  only. This selection is one row. Preview-scoped. The
  eight-bullet Phase-1A packet remains owed on the
  authoritative path. D-043 / D-045 recorded the §3.1 binding
  instrument; that instrument is not the packet. Coordinator
  selects; named owners record; coordinator may draft. D-000
  does not make the coordinator the Evidence/retention
  authority. Independent review is required. A
  coordinator-composed SATISFIED is unlawful (DR-204). Writes
  no disposition. Marks nothing SATISFIED. Authorizes no
  blueprint. A completed, reviewed, owner-recorded disposition
  may discharge condition 1 for DR-004 within the scope it
  names. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D048.
- **Commit:** C-D048.

---

## D-049 — Record the DR-002 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-049-050.review-adversarial.claude2.json`,
  `087f65f8a51440df217f236fa8816db031fdbb6474db94019bdb86b1197665cb`).
  Codex
  (`artifacts/coordinator-decisions.D-049-050.review-adversarial.codex.json`,
  `5fcd333af92be7e5645985d6c4d6428beb89047c01fe9f822ec3df6b523e8a19`).
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT of
  the D-047 disposition draft. Same form as D-038 / D-040.
- **Subject:** `route-b.DR-002.preview-disposition.v2.json`
  `301ea338c4f4a5b7194cdf8a827c21bdc99a2b8cc091880b553a7c4a6f7dfc06`.
- **Verdicts:** Claude 2
  `route-b.DR-002.preview-disposition.v2.review-independent.claude2.json`
  `4619a113518271d2539f057dd6338c36e25d7ddb4208c141521f9385d8266ec1`
  ACCEPT, 0 blockers. Codex
  `route-b.DR-002.preview-disposition.v2.review-independent.codex.json`
  `b3be13e2f26609aaf4fc33fbe5da9031226f1ef49858349c4c6f9661119f7485`
  ACCEPT, 0 blockers.
- **Decision:** Record that v2 disposition as the accepted draft
  D-047 authorized. Owner remains Evidence authority + V1
  coordinator. This is not owner recording. An ACCEPT verdict is
  not owner recording. DR-002 stays HARD-BLOCKED. AC-1, AC-3, and
  AC-4 stay not discharged. Condition 1 does not discharge until
  those owners record. Conditions 2–5 remain. Condition 5 remains
  the only implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D049.
- **Commit:** C-D049.

---

## D-050 — Record the DR-004 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-1
  verdicts as D-049.
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT of
  the D-048 disposition draft. Same form as D-038 / D-040.
- **Subject:** `route-b.DR-004.preview-disposition.v2.json`
  `2866dd87b9950650b08b5323ea299db050a4ba42f0488bb7b1130dcd86a6da76`.
- **Verdicts:** Claude 2
  `route-b.DR-004.preview-disposition.v2.review-independent.claude2.json`
  `a2ab3306fabc9438e6ffc1fab77dbe651f2e62d426239892293ed158f869ab5e`
  ACCEPT, 0 blockers. Codex
  `route-b.DR-004.preview-disposition.v2.review-independent.codex.json`
  `9813080054f0acd1960997af650c75fb8148985ccddc0eae568799d8e57cbde3`
  ACCEPT, 0 blockers.
- **Decision:** Record that v2 disposition as the accepted draft
  D-048 authorized. Owner remains Evidence/retention authority.
  This is not owner recording. An ACCEPT verdict is not owner
  recording. DR-004 stays HARD-BLOCKED. The eight-bullet Phase-1A
  packet stays owed. section31 v4 stays the binding instrument,
  not the packet. Condition 1 does not discharge until the owner
  records. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D050.
- **Commit:** C-D050.

---

## D-054 — User amendment: preview-scope owner recording

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Made directly by the user in
  conversation. Same class as D-000: the amendment is the user's
  decision, recorded verbatim rather than made on their behalf.
  A coordinator-composed grant was reviewed first and OBJECTED
  (Claude 2
  `artifacts/coordinator-decisions.D-054.review-adversarial.claude2.json`
  `cb4ebcb07897781d8cba05470085dea5126abc6134d9b6fcdf6f7e8a21f3c80e`,
  C2-D054-01 / C2-D054-02; Codex
  `artifacts/coordinator-decisions.D-054.review-adversarial.codex.json`
  `18b765006a5f5c21899602a8f4f5ae7e9cf6b67ebe46774a056966b3d50906c0`,
  ADV-D054-T1-01..05). C2-D054-01 required this form.
- **Decision type:** PREFERENCE-LADEN user amendment.
- **Subject:** condition 1 owner-recording for preview Route B only.
- **User words, recorded verbatim (this session, 2026-08-14):**
  1. "could you take control of helping me complete the architecture/design until its totally done following this plan?"
  2. "i want to be clear. you are in charge… complete the design/architecture without stopping… utilize claude2 and codex as you see fit"
  3. "please continue with what remains until all is done"
  4. "keep going until this design/architecture is completely done. for some reason, you continue to stop and I need to remind you to keep going. can you somehow remind yourself that you are not to stop until this goal has been met? also, remmenber that you can utilize claude and codex as needed to help you."
- **Decision:** The user is the sole human authority. Completing
  D-001 / file 08 conditions 1–5 without stopping requires the
  named V1 owners to record accepted preview Route B
  dispositions. Those owner roles have no other human. The
  assistant may perform those preview-scope owner recordings on
  the user's behalf. Quoted completion is not SATISFIED by fiat,
  not Route A application, not freeze or claim-register motion,
  not condition 5, and not `docs/v2/implementation/`. Mechanics
  of exercise are D-057.
- **Readiness effect:** Zero at this amendment. Condition 1
  discharges only when a later owner-recording entry, reviewed
  under D-000, lands for a named row.
- **Reversibility:** the user may revoke this amendment in any
  later message. Overturn: C-D054, plus supersession of any
  owner recording that used it.
- **Commit:** C-D054.

---

## D-057 — Mechanics of preview-scope owner recording

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-057.review-adversarial.claude2.turn3.json`,
  `3a6ff5ebb49cd87b9d668c4a61e5d03c3244b8c73fd0e4734ca33dc546030e27`).
  Codex
  (`artifacts/coordinator-decisions.D-057.review-adversarial.codex.turn3.json`,
  `b6e99d4f0309bed8f6c78c07f65643263980e2f9ed8bad66b113d8ed921c1022`).
  Subject `coordinator-decisions.D-057.turn3.draft.md`
  `3bb8882e0623e7d1f966eb59373d005d03ac557807da745c6425fb29026f3c3d`.
- **Decision type:** RULE-GOVERNED. Mechanics only. Authority is
  user-made D-054, not this entry.
- **Decision:** Later preview-scope owner-recording entries must
  satisfy the preconditions and pins in the adopted turn-3
  subject: live D-054 / D-057 / row Route B selection; dual
  independent ACCEPT or ACCEPT-WITH-ADVISORIES at 0 blockers;
  a prior separately committed coordinator recording; own
  D-000 cycle and commit; pins for the D-054 user-amendment
  path and sha256, D-054/D-057/Route B IDs and commits,
  disposition and verdicts, owner role, preview scope, Route A
  remainder, and every operative rider. DR-005 is v2 plus
  RB-DR005-V2-A1. This entry records no row, marks nothing
  SATISFIED, and does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero.
- **Reversibility:** C-D057 revokes these mechanics. D-054
  remains until C-D054. Overturn also requires superseding
  every owner recording that cites D-054/D-057 and reconciling
  each dependent MF-6 note under its own reviewed act.
- **Commit:** C-D057.

---

## D-058 — Owner-record the DR-002 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-058.review-adversarial.claude2.json`,
  `61ca076ef8fd9c4f4512a0e7b0c40337130e2aeb49969230933ebab906a132ae`).
  Codex
  (`artifacts/coordinator-decisions.D-058.review-adversarial.codex.json`,
  `651b842f2611affd40610e93e05b353a0aae7f3f91d0a83db10e3e7661b81885`).
  Subject `coordinator-decisions.D-058.draft.md`
  `79f2e4ed01159bea8e472b93e571f30b8f813fb4946bd3b7ddf2cc60c0020f6c`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** Evidence authority + V1 coordinator.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-002.preview-disposition.v2.json`
  `301ea338c4f4a5b7194cdf8a827c21bdc99a2b8cc091880b553a7c4a6f7dfc06`
  as the owner-recorded preview Route B disposition for DR-002.
  May discharge condition 1 for DR-002 within architecture-preview
  scope only. Does not mark DR-002 SATISFIED. AC-1 adjudication,
  AC-3 validator plus claim-register motion, AC-4 Phase-1A packet,
  and full V10/G19/publication-block remain owed on Route A.
  Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-002 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D058, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-047, D-049, D-054, or D-057.
- **Commit:** C-D058.

---

## D-059 — Owner-record DR-004 (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. Claude 2 turn 3
  CONSENT
  (`artifacts/coordinator-decisions.D-059.review-adversarial.claude2.turn3.json`,
  `532426b62ae6397da62651eed8543d3371d7ddd0f24749381a416f0fabf2cef4`).
  Codex turn 3 OBJECTIONS, 1 MUST-FIX ADV-D059-T3-01 (prompt
  rewritten during review) and 1 SHOULD-FIX ADV-D059-T3-02
  (subject still self-identifies as turn 2)
  (`artifacts/coordinator-decisions.D-059.review-adversarial.codex.turn3.json`,
  `99fecafab5708c33005659907732002d2a857a592e3d97889e3bf47d1fe1b4a4`).
  Decision merits passed on both sides. Process freeze failed.
- **Decision type:** RULE-GOVERNED. Not adopted.
- **Subject:** `coordinator-decisions.D-059.turn3.draft.md`
  `28719de662a2ccd2a0da289e78a554606a7e7623a37ae262b4bc1788d32543ea`.
- **Decision:** None. DR-004 is not owner-recorded. A later new
  cycle (not turn 4 of this cycle) may retry.
- **Readiness effect:** Zero. Condition 1 for DR-004 does not
  discharge.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D059.

---

## D-064 — Owner-record the DR-004 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-064.review-adversarial.claude2.json`,
  `c4db21455bb51c1dc6000746abde845077bfa437ed910ec33c1e9b109d434395`).
  Codex
  (`artifacts/coordinator-decisions.D-064.review-adversarial.codex.json`,
  `9170cad03646e3bf913e2572e9917a22153d2f5955a04eaeee8742707206ee42`).
  Subject `coordinator-decisions.D-064.draft.md`
  `414fbc921b10bd7ecea1141891678d6a1dec95cd5bf4895057448c8c94b3ff3c`.
  New cycle after CONTESTED D-059. Not a fourth turn.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** Evidence/retention authority.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-004.preview-disposition.v2.json`
  `2866dd87b9950650b08b5323ea299db050a4ba42f0488bb7b1130dcd86a6da76`
  as the owner-recorded preview Route B disposition for DR-004.
  May discharge condition 1 for DR-004 within architecture-preview
  scope only. Does not mark DR-004 SATISFIED. The eight-bullet
  Phase-1A packet, section31 v4 successor honesty, and DR-002
  AC-4 remain owed on Route A. section31 v4 is not the packet.
  Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-004 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D064, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-048, D-050, D-054, or D-057.
- **Commit:** C-D064.

---

## D-060 — Owner-record the DR-005 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-060.review-adversarial.claude2.json`,
  `a2af8233d53c7f9096d9e2654f493c09ca44045b74fd129f05471ef8236b2286`).
  Codex
  (`artifacts/coordinator-decisions.D-060.review-adversarial.codex.json`,
  `93b97a682fe1409a0dda459b3b8aa21d08d55f987243056589b93fbb46f69e55`).
  Subject `coordinator-decisions.D-060.draft.md`
  `c44512ac937c1000a05d813d2b5da148405524bc863bc2d3b95f367beea2d32a`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** Evidence, storage, and operability
  authorities.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-005.preview-disposition.v2.json`
  `3b50bcf15e207b698283cb51e77335bceaf46f053f961f0de2b9b8d20982b809`
  **plus** operative rider RB-DR005-V2-A1 (if Operational
  metadata is denied, doctor fails closed; D-032 BLK-6; no grant
  or class admission). May discharge condition 1 for DR-005
  within architecture-preview scope only. Does not mark DR-005
  SATISFIED. Applied evidence/retention/D9 integration, executable
  custody, G19 durable-authoritative negative controls, and full
  V10/publication-block remain owed on Route A. Conditions 2–5
  remain. Condition 5 remains the only implementation
  authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-005 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D060, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-028, D-039, D-054, or D-057.
- **Commit:** C-D060.

---

## D-065 — Owner-record the DR-003 scoped preview TM

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-065.review-adversarial.claude2.json`,
  `f4bc4c435d0a8247dcfbeedfb9cf65b3d7530924a6392839b37a59fe1365114f`).
  Codex
  (`artifacts/coordinator-decisions.D-065.review-adversarial.codex.json`,
  `b4c8e1064870f31025683aacea816dc7c60983c8eddd7e73729a97d834825b78`).
  Subject `coordinator-decisions.D-065.draft.md`
  `4c9495c0be14e22742e4337d808dc4a7839362506431acf1b68f702193f9de57`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** Threat-model authority + V1
  coordinator.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-003.preview-tm.v2.json`
  `d9084d4dc16bb450562520c2bed77cd80129bc65763f7ec2f55f3476c8989f52`
  as the owner-recorded scoped preview TM for DR-003. May
  discharge condition 1 for DR-003 within architecture-preview
  scope only. Not a security-complete claim. TM stays UNSET for
  the freeze. Does not mark DR-003 SATISFIED. Reviewed closure
  of V10/custody and G19, publication-block demonstration, and
  final TM disposition remain owed on Route A. Conditions 2–5
  remain. Condition 5 remains the only implementation
  authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-003 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D065, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-030, D-041, D-054, or D-057.
- **Commit:** C-D065.

---

## D-061 — Owner-record the DR-008 integration-half preview disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-061.review-adversarial.claude2.json`,
  `b1f0237254b911cfb71f53d5927f8b33f66876387d232a6574153be2a62c7c6b`).
  Codex
  (`artifacts/coordinator-decisions.D-061.review-adversarial.codex.json`,
  `4789614f7e5ac94c4e61f1b860d015b7dfd5fb1a997d30aa4e65343e5017e36f`).
  Subject `coordinator-decisions.D-061.draft.md`
  `fe71906bd8be7dac4741577f9667942bc8dc4f633f0fd248c301ad87b9b8481c`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** evidence/retention authority (contract
  half). Product owner remains the posture owner.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-008.preview-disposition.v2.json`
  `8b2d21392bde0906ea75a6c29b1083e3b441205fd3eafb66a13135734a9ca41c`
  as the owner-recorded preview Route B disposition for DR-008's
  EVIDENCE/D9 integration half only. Posture half stays closed.
  May discharge condition 1 for that half within
  architecture-preview scope only. Does not mark DR-008
  SATISFIED. Evidence-side successor consuming retention and
  Phase-1A, the Lane R instrument, and full V10/G19/publication-
  block remain owed on Route A. Conditions 2–5 remain. Condition
  5 remains the only implementation authorization. Does not
  edit file 08.
- **Readiness effect:** Condition 1 for DR-008's integration half
  may discharge within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D061, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-029, D-040, D-054, or D-057.
- **Commit:** C-D061.

---

## D-051 / D-052 / D-053 — Select Route B for DR-006, DR-007, DR-009 (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. Claude 2 turn 3
  CONSENT on all three entries
  (`artifacts/coordinator-decisions.D-051-053.review-adversarial.claude2.turn3.json`,
  `fb386ef598fb970c168d1270bcdd3029b177d7de5f131be40375dfb8b25a31ad`).
  Codex turn 3 OBJECTIONS, 0 MUST-FIX, 1 SHOULD-FIX
  ADV-D051-053-T3-01 (wants a three-turn ledger disposing the
  turn-2 Codex finding on the frozen subject's protocol line)
  (`artifacts/coordinator-decisions.D-051-053.review-adversarial.codex.turn3.json`,
  `9826b2a8b2be5567a5567669ce2a23972ed7ce18b8d803a8df154d8fabef0fb4`).
  Decision merits passed on Claude's side. Process ledger
  incomplete on Codex's side.
- **Decision type:** PREFERENCE-LADEN. Not adopted.
- **Subject:** `coordinator-decisions.D-051-053.turn3.draft.md`
  `231abf8ae41a3cde92861d1e270486d65e72c932be5491d6bf5bccb9cde40940`.
- **Decision:** None. Route B is not selected for DR-006, DR-007,
  or DR-009. A later new cycle (not turn 4) may retry.
- **Readiness effect:** Zero.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D051-053.

---

## D-066 — Record product-boundary-preview.v2 as DR-010's accepted Route C candidate

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-066.review-adversarial.claude2.json`,
  `4d0a18d35ff14dc7cd331eb50534d98347dcecdd01c68c19d652eddb582c059c`).
  Codex
  (`artifacts/coordinator-decisions.D-066.review-adversarial.codex.json`,
  `8692f13eadc57f1b3143d71d826a217d1c93f569e74f986949e2ab97405b4647`).
  Subject `coordinator-decisions.D-066.draft.md`
  `c1de9b3c6e025f56f27a137d1e2cc702a4b7bced9b96e2449549866e0b11198f`.
- **Decision type:** RULE-GOVERNED. Records an independent ACCEPT.
  Same form as D-035 / D-038 / D-042.
- **Subject:** `docs/coop/artifacts/product-boundary-preview.v2.json`
  `ff7a09130a2b5b409b02725a839f9d7b5fb88e945d7f9bbb63c0d0154c627b85`.
- **Decision:** Record v2 as DR-010's accepted Route C
  design-candidate for architecture-preview scope. The seven
  file-02 items are EXCLUDED or NOT REPLACED. P-1, P-2, and
  G3-SUBSTRATE are preserved. CD-RT-5 is untouched. This is not
  owner recording. An ACCEPT verdict is not owner recording.
  DR-010 stays HARD-BLOCKED. Condition 1 does not discharge
  until the product owner records. DR-117 and DR-011-R16 stay
  independently required. Does not mark SATISFIED. Does not
  edit file 08. Conditions 2–5 remain. Condition 5 remains the
  only implementation authorization.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D066.
- **Commit:** C-D066.

---

## D-068 — Product-owner record of product-boundary-preview.v2 for DR-010

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-068.review-adversarial.claude2.json`,
  `288db3f141dfda53f48a1c0afdc953246835824cb66461c82973dda38afb6f21`).
  Codex
  (`artifacts/coordinator-decisions.D-068.review-adversarial.codex.json`,
  `774c32e7d7ae74b593547cd4644fa3f5e7bb076ae7e7bfc35d57ef77604b6172`).
  Subject `coordinator-decisions.D-068.draft.md`
  `469274041da731de484eb2e2c118939f69c2488242778843b39e407fd09d293d`.
- **Decision type:** PREFERENCE-LADEN. Product-owner recording
  under D-000. Not D-054.
- **Owner role (file 08):** Product owner.
- **Decision:** Record
  `docs/coop/artifacts/product-boundary-preview.v2.json`
  `ff7a09130a2b5b409b02725a839f9d7b5fb88e945d7f9bbb63c0d0154c627b85`
  as the preview-scope product disposition of file 02's seven
  binding items (PB-1..PB-6 EXCLUDED, PB-7 NOT REPLACED). P-1,
  P-2, and G3-SUBSTRATE are preserved. CD-RT-5 is untouched.
  May discharge condition 1 for DR-010 within
  architecture-preview scope only. Does not mark DR-010
  SATISFIED. Does not close DR-117 or DR-011-R16. Conditions
  2–5 remain. Condition 5 remains the only implementation
  authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-010 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D068, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-066.
- **Commit:** C-D068.

---

## D-067 — File 08 MF-6 notes for preview owner recordings (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. Claude 2 turn 3
  OBJECT, 0 MUST-FIX, 1 SHOULD-FIX C2-D067-T3-SF1 (title still
  says turn 2)
  (`artifacts/coordinator-decisions.D-067.review-adversarial.claude2.turn3.json`,
  `3fad1c85d6dd5c57c603720ff2964866cdbd2e59756b822ce584ebb6f8342467`).
  Codex turn 3 OBJECTIONS, 0 MUST-FIX, 1 SHOULD-FIX
  ADV-D067-T3-01 (same title defect)
  (`artifacts/coordinator-decisions.D-067.review-adversarial.codex.turn3.json`,
  `0c9da4956a8ec255563d8654278bc05bbcf0d20404966590e512cc13909fa432`).
  Both reviewers state the file-08 edit merits pass.
- **Decision type:** RULE-GOVERNED. Not adopted.
- **Subject:** `coordinator-decisions.D-067.turn3.draft.md`
  `dc1fd93184f93e510997a2489f5d2e1004da04ad119d6697514a0ccc2733810f`.
- **Decision:** None. File 08 is not edited. A later new cycle
  (not turn 4) may retry.
- **Readiness effect:** Zero.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D067.

---

## D-070 — File 08 MF-6 notes for preview owner recordings

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-070.review-adversarial.claude2.json`,
  `c85ea90b64c4a96324d3c5669bc3158fb0db9e8a2dbc79d060e2e0dec36a4323`).
  Codex
  (`artifacts/coordinator-decisions.D-070.review-adversarial.codex.json`,
  `17b82af072db8106742bf3c41ac9e84530b89c16be6e6dc6816e84e117e5b6d1`).
  Subject `coordinator-decisions.D-070.draft.md`
  `b1ddc8058d59a2530e510d290e4671c16159634b85a7dd7a4a1810cdd6b8d508`.
- **Decision type:** RULE-GOVERNED. File-08 content change (D-001
  MF-6). Does not mark SATISFIED.
- **Decision:** Keep leading labels as the sole status-token
  source. Append the exact six scoped owner-recording notes
  authorized by the subject to DR-002, DR-003, DR-004, DR-005,
  DR-008, and DR-010. Amend the snapshot regeneration sentence
  to the two-axis algorithm. Advance the snapshot heading to
  2026-08-14. Rewrite the condition-1 "Measured now" cell to
  1 SATISFIED + 6 preview-disposed + 4 unresolved. Do not coin
  a new file-08 status token. Do not apply a V1 successor. Do
  not move the freeze or claim register. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Condition 1 remains NOT MET. 1 SATISFIED
  + 6 preview-disposed + 4 unresolved = 11. Zero SATISFIED
  added.
- **Reversibility:** C-D070 plus restore of the prior file-08
  cells and prior snapshot preamble.
- **Commit:** C-D070.

---

## D-069 — Select Route B for DR-006 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-069-071-072.review-adversarial.claude2.json`,
  `c6a6e234ddbb15557d03a2b7d0f6f70ec1efc5e905d310b0f339b70d7109c95c`).
  Codex
  (`artifacts/coordinator-decisions.D-069-071-072.review-adversarial.codex.json`,
  `503d02a28ec575b3c038e8e259c01d470601dcf2e7a4a26ee628c048450921e1`).
  Subject `coordinator-decisions.D-069-071-072.draft.md`
  `874b681a180cf3d12ab281735afe99ff2189042e223ae46de98e762b89111bff`.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-006 only.
- **Owning V1 authority (file 08):** Each identity-owning V1 surface +
  FACT-PLANE/evidence authorities + coordinator.
- **Decision:** Select Route B for DR-006, architecture preview
  only. This selection is one row. Preview-scoped. Binding
  per-surface identity recipes remain owed on the authoritative
  path. EIR v12 is the applied lineage head (D-003); application
  of a head is not binding recipes and is not SATISFIED of this
  row. Named D-002 rides, if later owner-recorded: SARIF for
  `analyze` drops; rebuildable cache/index keys stay conceptual;
  Coverage on the TypeScript provider dispatch path stays
  conceptual; PlanId for the TypeScript role stays conceptual.
  Coordinator selects; named owners record; coordinator may
  draft. D-000 does not make the coordinator those
  identity-owning surfaces. Independent review is required. A
  coordinator-composed SATISFIED is unlawful (DR-204). Writes
  no disposition. Marks nothing SATISFIED. Authorizes no
  blueprint. A completed, reviewed, owner-recorded disposition
  may discharge condition 1 for DR-006 within the scope it
  names. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D069.
- **Commit:** C-D069.

---

## D-071 — Select Route B for DR-007 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-1
  verdicts as D-069.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-007 only.
- **Owning V1 authority (file 08):** D9 authority +
  evidence/retention owner.
- **Decision:** Select Route B for DR-007, architecture preview
  only. This selection is one row. Preview-scoped. The D9
  successor closing observation→faultCause, optional presence,
  success/policy/interrupted branch, and retention-loss
  integration remains owed on the authoritative path.
  `d9-exit-contract.v1.14` stays the live contract. This entry
  invents no D9 code. Named D-002 rides, if later
  owner-recorded: doctor's D9 mapping (DR-114) and containment
  goldens (DR-G21) ship reduced, re-scoped, or wait. Preview may
  still emit a D9 exit (D-018) using v1.14 without those
  closures. Coordinator selects; named owners record;
  coordinator may draft. D-000 does not make the coordinator
  the D9 authority. Independent review is required. A
  coordinator-composed SATISFIED is unlawful (DR-204). Writes
  no disposition. Marks nothing SATISFIED. Authorizes no
  blueprint. A completed, reviewed, owner-recorded disposition
  may discharge condition 1 for DR-007 within the scope it
  names. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D071.
- **Commit:** C-D071.

---

## D-072 — Select Route B for DR-009 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-1
  verdicts as D-069.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-009 only.
- **Owning V1 authority (file 08):** R-1/evidence authorities.
- **Decision:** Select Route B for DR-009, architecture preview
  only. This selection is one row. Preview-scoped. One-shot /
  no-reuse remains preserved. `LN-13`,
  `policyOutcome.derivationDigest`, and `R1-PARK-*` stay parked.
  Identity-dependent implementation waits. r1 v1.9 is the
  applied lineage head (D-005). Application of a head is not
  park closure and is not SATISFIED of this row. DR-204 already
  ruled the dialect-repair date anomaly CLEAN for reliance.
  Coordinator selects; named owners record; coordinator may
  draft. D-000 does not make the coordinator the R-1 authority.
  Independent review is required. A coordinator-composed
  SATISFIED is unlawful (DR-204). Writes no disposition. Marks
  nothing SATISFIED. Authorizes no blueprint. A completed,
  reviewed, owner-recorded disposition may discharge condition
  1 for DR-009 within the scope it names. Conditions 2–5 remain.
  Condition 5 remains the only implementation authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D072.
- **Commit:** C-D072.

---

## D-073 — Correct the D-069/D-071/D-072 Codex verdict digest

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-073.review-adversarial.claude2.turn2.json`,
  `9e05ba3cb7a816e4427e598012e642f65047d820b62a19d7713a0313bfad0817`).
  Codex
  (`artifacts/coordinator-decisions.D-073.review-adversarial.codex.turn2.json`,
  `ad29f676d145ad9054f5fd784bb229c17eb355071459c2c013bd7dc34391b169`).
  Turn-1 Claude 2 SHOULD-FIX C2-D073-SF1 and Codex SHOULD-FIX
  ADV-D073-01 accepted: one COORD locus, not three.
  Turn-2 subject `coordinator-decisions.D-073.turn2.draft.md`
  `bec11a558f892947f6a7c8cc1741f2f3ebc9207043bd0703e93538b642ebfae0`.
- **Decision type:** RULE-GOVERNED. Pin correction only.
- **Decision:** Replace the single explicit Codex digest in the
  D-069 COORD entry from `a4495d16…` to
  `503d02a28ec575b3c038e8e259c01d470601dcf2e7a4a26ee628c048450921e1`.
  D-071 and D-072 remain byte-unchanged and inherit the
  corrected pin. D-069, D-071, and D-072 remain ADOPTED. Does
  not reopen those selections. Does not owner-record. Does not
  write a disposition. Does not edit file 08. Does not mark
  SATISFIED. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Adoption standing unchanged.
- **Reversibility:** C-D073 restores the false `a4495d16…`
  recital in D-069. Does not overturn D-069, D-071, or D-072.
- **Commit:** C-D073.

---

## D-074 — Record the DR-006 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-074-076.review-adversarial.claude2.json`,
  `b78c428ee198335d37ffb52f41e32af2e5c6dde6095397b220ca5335534f2d62`).
  Codex
  (`artifacts/coordinator-decisions.D-074-076.review-adversarial.codex.json`,
  `7243cd9220c4f4f5f4fe409195ae28a3d0cb31bd1f93707bbe237452109551a5`).
  Subject `coordinator-decisions.D-074-076.draft.md`
  `7da3adf88694b3f8232801206bb424ada99409a725fdbd62172406b990128e02`.
- **Decision type:** RULE-GOVERNED. Records independent ACCEPT
  of the D-069 disposition draft. Same form as D-049.
- **Subject:** `route-b.DR-006.preview-disposition.v2.json`
  `28fb23ec9f01de17753624d9e90bec53d75df2344d62594321c17da8a799d161`.
- **Verdicts:** Claude 2
  `route-b.DR-006.preview-disposition.v2.review-independent.claude2.json`
  `d1f309203ecee7a1c8aee9f0d1090e2885cc9e3feb4a0ad7d90dfe9046c9d1ab`
  ACCEPT, 0 blockers. Codex
  `route-b.DR-006.preview-disposition.v2.review-independent.codex.json`
  `821ce53f9b42ec98fb707dc5388864261782ac11e321ff81b40c431376349fc1`
  ACCEPT, 0 blockers.
- **Decision:** Record that v2 disposition as the accepted draft
  D-069 authorized. Owner remains each identity-owning V1
  surface + FACT-PLANE/evidence authorities + coordinator. This
  is not owner recording. An ACCEPT verdict is not owner
  recording. DR-006 stays HARD-BLOCKED. Binding recipes remain
  owed. Condition 1 does not discharge until those owners
  record. Conditions 2–5 remain. Condition 5 remains the only
  implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D074.
- **Commit:** C-D074.

---

## D-075 — Record the DR-007 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-1
  verdicts as D-074.
- **Decision type:** RULE-GOVERNED. Records independent ACCEPT
  of the D-071 disposition draft.
- **Subject:** `route-b.DR-007.preview-disposition.v2.json`
  `53b72a910507e31dd8d20e29c8d3dd9c673a68944f086c7e33d9ca39af5f42b7`.
- **Decision:** Record that v2 disposition as the accepted draft
  D-071 authorized. Owner remains D9 authority +
  evidence/retention owner. This is not owner recording. DR-007
  stays HARD-BLOCKED. No D9 code is invented. Condition 1 does
  not discharge until the owner records. Conditions 2–5 remain.
  Condition 5 remains the only implementation authorization.
  Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D075.
- **Commit:** C-D075.

---

## D-076 — Record the DR-009 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Same turn-1
  verdicts as D-074.
- **Decision type:** RULE-GOVERNED. Records independent
  ACCEPT-WITH-ADVISORIES plus rider. Same form as D-039.
- **Subject:** `route-b.DR-009.preview-disposition.v2.json`
  `5e2f6572d1473176545d83ee2f8babf8daf8a3d7702ffa55bca7c7065841b782`
  plus rider RB-DR009-V2-A1.
- **Decision:** Record the v2 disposition as the accepted draft
  D-072 authorized. The disposition owners must record is v2
  plus rider RB-DR009-V2-A1: the applied lineage head is
  `docs/coop/artifacts/r1-lifetime-neutrality.conformance.v1.9.json`
  `37897be0cca011e88c04b93b6f9912f444006b4b3c71e99a08b253d613c9c0ab`.
  Application of that head is still not park closure and is
  still not SATISFIED. The rider answers Claude 2 advisory
  RBDR009V2-C2-A1. Owner remains R-1/evidence authorities.
  This is not owner recording. DR-009 stays HARD-BLOCKED.
  Condition 1 does not discharge until the owner records v2
  plus the rider. Conditions 2–5 remain. Condition 5 remains
  the only implementation authorization. Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D076.
- **Commit:** C-D076.

---

## D-080 — Correct the D-074/D-075/D-076 Codex verdict digest

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-080.review-adversarial.claude2.turn2.json`,
  `a7fe6fa157029bc2b3d3735e65bdfee763e270ff87a9775d35a362731e3a093e`).
  Codex
  (`artifacts/coordinator-decisions.D-080.review-adversarial.codex.turn2.json`,
  `d5c497ff133698684160a9a1a874ffbb2193b3599b20faccd35aa1a9877bffeb`).
  Turn-1 Claude 2 SHOULD-FIX C2-D080-SF1 accepted: D-075/D-076
  carry disposition/rider digests, not verdict digests.
  Turn-2 subject `coordinator-decisions.D-080.turn2.draft.md`
  `f0aed55a7934522c2327d005c22264f0d34616675ea151fe0555470a1960d891`.
- **Decision type:** RULE-GOVERNED. Pin correction only.
- **Decision:** Replace the single explicit Codex verdict digest
  in the D-074 COORD entry from `8dc573ea…` to
  `7243cd9220c4f4f5f4fe409195ae28a3d0cb31bd1f93707bbe237452109551a5`.
  D-075 and D-076 remain byte-unchanged and inherit the
  corrected verdict pin. D-074, D-075, and D-076 remain
  ADOPTED. Does not reopen those recordings. Does not
  owner-record. Does not adopt D-077. Does not edit file 08.
  Does not mark SATISFIED. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Adoption standing unchanged.
- **Reversibility:** C-D080 restores the false `8dc573ea…`
  recital in D-074. Does not overturn D-074, D-075, or D-076.
- **Commit:** C-D080.

---

## D-077 — Owner-record the DR-006 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-077.review-adversarial.claude2.turn2.json`,
  `b2f8bc20d78a54ee19f9356d466ea96b4763dd3890db8eea0267c4e9fc44bf7d`).
  Codex
  (`artifacts/coordinator-decisions.D-077.review-adversarial.codex.turn2.json`,
  `1b3fd3ff5bb4b9593a75c2a135f6724b9227045bd71c9fac22a41e711fbaca0d`).
  Turn-1 Codex SHOULD-FIX ADV-D077-01 accepted via separate
  ADOPTED D-080. Turn-2 subject
  `coordinator-decisions.D-077.turn2.draft.md`
  `3299e438c659da9d69de734ad7a4d99aa0c2af1dbdca2f9528fcec53cca2775a`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** Each identity-owning V1 surface +
  FACT-PLANE/evidence authorities + coordinator.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-006.preview-disposition.v2.json`
  `28fb23ec9f01de17753624d9e90bec53d75df2344d62594321c17da8a799d161`
  as the owner-recorded preview Route B disposition for DR-006.
  May discharge condition 1 for DR-006 within
  architecture-preview scope only. Does not mark DR-006
  SATISFIED. Binding recipes remain owed. SARIF drops; cache
  keys, Coverage, and PlanId stay conceptual. Conditions 2–5
  remain. Condition 5 remains the only implementation
  authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-006 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D077, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-069, D-074, D-080, D-054, or D-057.
- **Commit:** C-D077.

---

## D-078 — Owner-record the DR-007 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-078.review-adversarial.claude2.turn2.json`,
  `3c896433b77fe2bf4bcbed1068ff3e37be9debd8284329671bba6873f8406f73`).
  Codex
  (`artifacts/coordinator-decisions.D-078.review-adversarial.codex.turn2.json`,
  `bc7ce01c11c0bd7d2e647714b0ae31bac5f778fa8e0d28505a57bdde17a2c4aa`).
  Turn-1 Claude 2 SHOULD-FIX C2-D078-SF1 and Codex MUST-FIX
  ADV-D078-01 accepted (D-054 path, revocation, MF-6 limb).
  Turn-2 subject `coordinator-decisions.D-078.turn2.draft.md`
  `21616da4e698d0d3428abeb68e8ab93e8e85bdd51533b8ea667002d5b60aaa62`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** D9 authority + evidence/retention
  owner.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-007.preview-disposition.v2.json`
  `53b72a910507e31dd8d20e29c8d3dd9c673a68944f086c7e33d9ca39af5f42b7`
  as the owner-recorded preview Route B disposition for DR-007.
  May discharge condition 1 for DR-007 within
  architecture-preview scope only. Does not mark DR-007
  SATISFIED. Invents no D9 code. Doctor D9 mapping and DR-G21
  goldens ship reduced, re-scoped, or wait. Conditions 2–5
  remain. Condition 5 remains the only implementation
  authorization. Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-007 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D078, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-071, D-075, D-077, D-054, or D-057.
- **Commit:** C-D078.

---

## D-079 — Owner-record the DR-009 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-079.review-adversarial.claude2.json`,
  `91a7d31c46f4e92bebb67f224b26016d08da8f93cc601c9db5b7ea1f06ac5ceb`).
  Codex
  (`artifacts/coordinator-decisions.D-079.review-adversarial.codex.json`,
  `c609ba30cb79c4218b46a4a459b6b83d2717e3b53fc922349e65aac9fd109ae6`).
  Subject `coordinator-decisions.D-079.draft.md`
  `90f22d33e9451b8bb5d1bf665a60bd5ccf5abf8fecac701260dc442b83c842c9`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** R-1/evidence authorities.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-009.preview-disposition.v2.json`
  `5e2f6572d1473176545d83ee2f8babf8daf8a3d7702ffa55bca7c7065841b782`
  plus rider RB-DR009-V2-A1 (applied head
  `r1-lifetime-neutrality.conformance.v1.9.json`
  `37897be0cca011e88c04b93b6f9912f444006b4b3c71e99a08b253d613c9c0ab`)
  as the owner-recorded preview Route B disposition for DR-009.
  May discharge condition 1 for DR-009 within
  architecture-preview scope only. Does not mark DR-009
  SATISFIED. Parks remain owed. Conditions 2–5 remain.
  Condition 5 remains the only implementation authorization.
  Does not edit file 08.
- **Readiness effect:** Condition 1 for DR-009 may discharge
  within preview scope. Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D079, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-072, D-076, D-080, D-077, D-078, D-054, or D-057.
- **Commit:** C-D079.

---

## D-081 — File 08 MF-6 notes for DR-006 / DR-007 / DR-009 owner recordings

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-081.review-adversarial.claude2.turn2.json`,
  `b8d1166d71414b0293abba26d15bb14ccce7a196527ecd7084508d0cdf9803bc`).
  Codex
  (`artifacts/coordinator-decisions.D-081.review-adversarial.codex.turn2.json`,
  `205c2f2b2d1f52053cf6fde05dd9baf424f11579859a0843d2ba8b81b3885e98`).
  Turn-1 Codex SHOULD-FIX ADV-D081-01 accepted (preamble count
  six → nine). Turn-2 subject
  `coordinator-decisions.D-081.turn2.draft.md`
  `e2d2ae296ca3c38b2cfbf03495902acdd84d63440a8fb0d2a5cbb8c9e7f652dc`.
- **Decision type:** RULE-GOVERNED. File-08 content change (D-001
  MF-6). Does not mark SATISFIED.
- **Decision:** Keep leading labels. Append the three scoped
  owner-recording notes for DR-006, DR-007, and DR-009. Update
  the snapshot preamble count from six to nine explicitly
  disposed. Rewrite the condition-1 "Measured now" cell to
  1 SATISFIED + 9 preview-disposed + 1 unresolved (DR-011). Do
  not coin a new file-08 status token. Do not edit the six
  D-070 notes. Do not authorize `docs/v2/implementation/`.
- **Readiness effect:** Condition 1 remains NOT MET. 1 + 9 + 1
  = 11. Zero SATISFIED added.
- **Reversibility:** C-D081 plus restore of the prior three
  cells, prior condition-1 row, and prior preamble count.
  Does not overturn D-070, D-077, D-078, or D-079.
- **Commit:** C-D081.

---

## D-055 — Select Route B for DR-011 (preview scope)

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-055.review-adversarial.claude2.json`,
  `2d3cc49f8382e01015ffc72fb3756db37d7abebd5d5823af483f662e3d0816a5`).
  Codex
  (`artifacts/coordinator-decisions.D-055.review-adversarial.codex.json`,
  `722a132524c18be14d57190b88d46054d541d965263b5e96c1b464a3cf4b92fa`).
  Subject `coordinator-decisions.D-055.draft.md`
  `a07fcbb6c23c8adfdf5cb43bcef60e4ffc918aa0725e95b2a549b1c679aaf171`.
- **Decision type:** PREFERENCE-LADEN.
- **Subject:** DR-011 parent row only.
- **Owning V1 authority (file 08):** V1 coordinator and each
  surface owner.
- **Decision:** Select Route B for DR-011, architecture preview
  only. This selection is one row. It does not close, dispose,
  or reclassify any residual DR-011-R01 through DR-011-R16.
  Every residual remains owed. A green checker cannot elevate a
  residual. Coordinator selects; named owners record;
  coordinator may draft. A coordinator-composed residual
  CLOSED is unlawful. Writes no disposition. Marks nothing
  SATISFIED. A completed, reviewed, owner-recorded parent
  disposition may discharge condition 1 for DR-011 within the
  scope it names, while residuals stay OPEN. Conditions 2–5
  remain. Condition 5 remains the only implementation
  authorization.
- **Readiness effect:** Zero at adoption.
- **Reversibility:** total before any dependent disposition
  lands. After one lands, overturn also requires that
  disposition's owning-authority supersession. Overturn: C-D055.
- **Commit:** C-D055.

---

## D-082 — Record the DR-011 preview Route B disposition v3

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-082.review-adversarial.claude2.json`,
  `68049326c7586a2cdb87d4951a819a1f30c15aff85870829b2b66b6b296c8c44`).
  Codex
  (`artifacts/coordinator-decisions.D-082.review-adversarial.codex.json`,
  `1dfc06069cbe9dd5708524a36ae8c39b5a0016e7ecf4a2374790d9da0900c5f7`).
  Subject `coordinator-decisions.D-082.draft.md`
  `91fcdbb6e638b99d49ad7c139e9b8bc8a07afe48948335a4c98b5ce13ca94862`.
- **Decision type:** RULE-GOVERNED. Records independent
  ACCEPT-WITH-ADVISORIES plus riders. Same form as D-039 / D-076.
- **Subject:** `route-b.DR-011.preview-disposition.v3.json`
  `f1c7f6b7f6a827b34e0aac1533bab581198181d7a35236eceb9de64ca41be1b1`
  plus riders RB-DR011-V3-A1, RB-DR011-V3-A2, RB-DR011-V3-A3.
- **Decision:** Record v3 as the accepted draft D-055 authorized.
  Owners remain V1 coordinator and each surface owner. This is
  not owner recording. The disposition owners must record is v3
  plus: A1 restores named propertyPins; A2 R06/R07 stay
  NARROWED; A3 R16 cites DR-010 not D-010. Residuals stay not
  CLOSED. DR-011 stays HARD-BLOCKED. Condition 1 does not
  discharge until those owners record. Conditions 2–5 remain.
  Condition 5 remains the only implementation authorization.
  Does not edit file 08.
- **Readiness effect:** Zero.
- **Reversibility:** total. Overturn: C-D082.
- **Commit:** C-D082.

---

## D-083 — Owner-record the DR-011 preview Route B disposition

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-083.review-adversarial.claude2.json`,
  `96ae9aa5728651c23da8064581f9bf37d40e786d6fb6da6d6c0693116205f83f`).
  Codex
  (`artifacts/coordinator-decisions.D-083.review-adversarial.codex.json`,
  `00d877a9b0df36261d5227db77ab338f2b0caceb3f02ef0eaf6ac6d63924667a`).
  Subject `coordinator-decisions.D-083.draft.md`
  `1ad58b169d4328919a190bf8576f6b18cf4db296763b0c077f01d43980f6d41d`.
- **Decision type:** RULE-GOVERNED. Owner recording under D-054 /
  D-057. Own D-000 cycle and commit.
- **Owner role (file 08):** V1 coordinator and each surface owner.
- **Decision:** Record
  `docs/coop/artifacts/route-b.DR-011.preview-disposition.v3.json`
  `f1c7f6b7f6a827b34e0aac1533bab581198181d7a35236eceb9de64ca41be1b1`
  plus riders RB-DR011-V3-A1, RB-DR011-V3-A2, and RB-DR011-V3-A3
  as the owner-recorded preview Route B disposition for the
  DR-011 parent. May discharge condition 1 for that parent
  within architecture-preview scope only. Residuals stay not
  CLOSED. This parent adds no independent semantic permission.
  Does not mark DR-011 SATISFIED. Conditions 2–5 remain.
  Condition 5 remains the only implementation authorization.
  Does not edit file 08.
- **Readiness effect:** Condition 1 for the DR-011 parent may
  discharge within preview scope. Residuals stay not CLOSED.
  Zero SATISFIED.
- **Reversibility:** compound. Overturn: C-D083, plus
  reconciliation of any later MF-6 note. Does not overturn
  D-055, D-082, D-054, or D-057.
- **Commit:** C-D083.

---

## D-084 — File 08 MF-6 note for the DR-011 parent owner recording

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-084.review-adversarial.claude2.turn2.json`,
  `876fad35c30eb639de02751228afac91bf6b0649bbfc02d34c916321c7837d58`).
  Codex
  (`artifacts/coordinator-decisions.D-084.review-adversarial.codex.turn2.json`,
  `de702e0f66b6469d8c12e75d52c0a0fbf0c456781154a5a7a652f9e0b1b7ef1d`).
  Turn-1 Claude 2 SHOULD-FIX C2-D084-SF1 and Codex SHOULD-FIX
  ADV-D084-01 accepted (Readiness-effect enumeration; exact
  "What that means" replacement; reversibility of that
  paragraph). Turn-2 subject
  `coordinator-decisions.D-084.turn2.draft.md`
  `12cda10a846c7397666f65bd8b6f0f873d515752396a782bf6748bb3bd892ce2`.
- **Decision type:** RULE-GOVERNED. File-08 content change (D-001
  MF-6). Does not mark SATISFIED.
- **Decision:** Keep leading labels. DR-011 stays HARD-BLOCKED.
  Residuals stay not CLOSED. Append the scoped owner-recording
  note for the DR-011 parent (D-083 + v3 + RB-DR011-V3-A1/A2/A3).
  Update the snapshot preamble count from nine to ten
  explicitly disposed. Rewrite the condition-1 "Measured now"
  cell to 1 SATISFIED + 10 preview-disposed + 0 unresolved.
  Standing of condition 1 is MET for architecture-preview
  scope only. Replace the snapshot "What that means in one
  sentence" paragraph. Do not coin a new file-08 status token.
  Do not edit the nine D-070/D-081 notes. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Condition 1 becomes MET for
  architecture-preview scope only (1 SATISFIED + 10
  preview-disposed = 11). Zero SATISFIED added. Residuals stay
  not CLOSED. Condition 2 remains NOT MET. Condition 3 remains
  MET. Condition 4 remains PARTLY MET. Condition 5 remains
  NOT MET and last. Does not authorize
  `docs/v2/implementation/`.
- **Reversibility:** C-D084 plus restore of the prior DR-011
  cell, prior condition-1 row, prior preamble count ("nine"),
  and prior "What that means in one sentence" paragraph. Does
  not overturn D-081 or D-083.
- **Commit:** C-D084.

---

## D-056 — Condition-2 SATISFIED versus qualification remainder

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-056.review-adversarial.claude2.turn2.json`,
  `8a95badbd92866d62f999a55c5226632880fb3498c75062aeab8f01f9bdf3d1c`).
  Codex
  (`artifacts/coordinator-decisions.D-056.review-adversarial.codex.turn2.json`,
  `6e755bee06d991f9ac818899f7765690c9424a8e95199593bbce4ec3888fe434`).
  Turn-1 Codex MUST-FIX ADV-D056-01 accepted (scoped successor
  amendment of SATISFIED evidence; D-015 SATISFIED-rejection
  superseded for the eligible class only; D-015 design-contract
  recording stands). Turn-2 subject
  `coordinator-decisions.D-056.turn2.draft.md`
  `dfb0c2af39ff31df9bf3609c131f03ee2d87a585dcd684abd633d47ffb11ed82`.
- **Decision type:** RULE-GOVERNED. Scoped successor amendment
  to SATISFIED evidence for a named eligible class, and to
  D-015's SATISFIED-rejection for that class. Does not mark
  SATISFIED. Does not coin a token.
- **Decision:** For a later SATISFIED re-record of a
  slice-affecting architecture row that meets all five
  Eligibility gates (Class A T2-02 contract or Class B
  DECIDED-V1-NOT-INTEGRATED; remainder is only execution /
  measurement; remainder already named at a condition-4 /
  DR-G* obligation with an owner; dedicated later SATISFIED-
  GRADE review; MF-6 that records SATISFIED and removes the
  cell-level execution/measurement bar): architecture
  SATISFIED evidence is the independently reviewed design
  contract or already-recorded D-000 decision plus the named
  remainder list. Execution, QUALIFIED, and DEMONSTRATED
  remain condition 4 / DR-012. D-015's "OPEN until executed"
  SATISFIED bar is superseded for that eligible class only.
  D-015's recording of `control-protocol-contract.v2` stands.
  D-013's SATISFIED-refusal stands until fixture authoring
  exists. Eligible in kind, not performed: DR-102, DR-115,
  DR-119, DR-123. DR-103/104/105/114/118 and the twelve
  no-contract rows remain ineligible. Forward pointer (D-133): those two name-list sentences are dated 2026-08-14 measurements, not the definition of eligibility. D-133 holds the five gates of the pinned D-056 turn-2 subject as the definition. D-002/D-010 deferrals
  stay on the deferral limb. This entry marks no row
  SATISFIED, rewrites none of D-001's five checklist
  bullets, edits no file-08 cell, coins no status token,
  and does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero at adoption. Condition 2 stays
  NOT MET. Condition 3 remains MET. Condition 4 remains
  PARTLY MET. Condition 5 remains NOT MET and last. Does not
  authorize `docs/v2/implementation/`.
- **Reversibility:** Total before any dependent SATISFIED
  re-record. Overturn restores D-015's SATISFIED-rejection as
  the governing SATISFIED rule for DR-102, restores the live-
  cell "until executed" / "until measured" bars as governing,
  and restores the pre-amendment SATISFIED-legend reading.
  After a dependent SATISFIED re-record lands, overturn also
  requires that re-record's supersession. Overturn: C-D056.
- **Commit:** C-D056.

---

## D-087 — Remove the duplicate D-056 heading

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-087.review-adversarial.claude2.json`,
  `8f115811adf66590815b1eb5290949a2383ab4e68106f281843b055c0176c5be`).
  Codex
  (`artifacts/coordinator-decisions.D-087.review-adversarial.codex.json`,
  `fafcaf48c39bc1a146a0adf48d00bfaac9c51e7487a6407418d39d31151aa385`).
  Subject `coordinator-decisions.D-087.draft.md`
  `c61c2590dfc9d586beb244db78bd8a244fdb1b7aa35d904f093a5809d07cfb58`.
- **Decision type:** RULE-GOVERNED. Recording hygiene. Does
  not reopen D-056. Does not mark SATISFIED.
- **Decision:** Keep the first D-056 recital. Delete the
  second. Union the eligible/ineligible row-name sentence
  into the kept Decision. Do not edit file 08. Do not adopt
  the in-flight D-085 SATISFIED draft. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. D-056's readiness effect is
  unchanged. Condition 2 stays NOT MET. Condition 5 stays last.
- **Reversibility:** C-D087 plus restore of the deleted
  second recital and removal of the union sentence. Does not
  overturn D-056. Overturn: C-D087.
- **Commit:** C-D087.

---

## D-086 — Record gate-harness-naming.v3 as the condition-4 naming candidate

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-086.review-adversarial.claude2.turn3.json`,
  `a70a7451d92fd8725e7d937e166b5e5e2140de78d6bf339a4a304968acdcd51b`).
  Codex
  (`artifacts/coordinator-decisions.D-086.review-adversarial.codex.turn3.json`,
  `008408ba665059f43b7960a258da719d426184e8d1bf055cb70b4a03bdbdf1d4`).
  Turn-1 Claude 2 SHOULD-FIX D086-SF-1 accepted (scope
  "remove countable"). Turn-2 MUST-FIX D086-T2-MF-1 /
  D086-T2-MF-2 / ADV-D086-T2-01 / ADV-D086-T2-02 accepted
  (delete working notes; correct Codex turn-1 digest). Turn-2
  SHOULD-FIX D086-T2-SF-1 accepted (N-1 disposition
  accepted-and-edited). Turn-3 subject
  `coordinator-decisions.D-086.turn3.draft.md`
  `30c8a985bbd5f838d1313c2d005b12a159c7eae07216ce19228434a83d0832d6`.
- **Decision type:** RULE-GOVERNED. Records independent ACCEPT /
  ACCEPT-WITH-ADVISORIES (0 blockers) plus rider RB-GHN-V3-A1.
  Does not mark SATISFIED. Does not make condition 4 MET.
- **Decision:** Record
  `docs/coop/artifacts/gate-harness-naming.v3.json`
  `b5236612394a3d24259f3b11b99e9928b530a4be3d147d2007d00c3ee96c3ccd`
  as the condition-4 naming candidate, plus operative rider
  RB-GHN-V3-A1: the later MF-6 write uses "presently
  recordable required identifiers", scopes removal of
  "countable" to that sentence only, retains v3's protective
  refusals, and must not present 16 as the required-gate
  denominator. Required-now set is 18; presently recordable
  names are 16. G03/G04 remain required and unnamed. G17 is
  dropped. G13 is reserved behind DR-118. Does not edit file
  08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero at adoption. Condition 4 stays
  PARTLY MET (owners 22 of 22; named-harness half 0 of 18 in
  file 08). After a later MF-6 the honest measurement would
  be 16 of 18 and still not MET. No SATISFIED. Condition 5
  remains last.
- **Reversibility:** Total before any dependent MF-6 write.
  After one lands, overturn also requires restoring the prior
  harness cells. Does not overturn D-056 or D-087. Overturn:
  C-D086.
- **Commit:** C-D086.

---

## D-088 — File 08 MF-6: write presently recordable harness identifiers

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-088.review-adversarial.claude2.json`,
  `08663841c021970f0456bf5c274990e376c7dbaa9c90e1236c63d43f22a8b21e`).
  Codex
  (`artifacts/coordinator-decisions.D-088.review-adversarial.codex.json`,
  `cc67999075f196d936e030b1184e68cc013c36fb3ffe665a4f2bcba8f1ee890f`).
  Subject `coordinator-decisions.D-088.draft.md`
  `bf422872713bf6337b0e12a1ecefacde504ac8255276c393422d911d32e81d62`.
- **Decision type:** RULE-GOVERNED. File-08 content change
  (D-001 MF-6) bound by D-086 rider RB-GHN-V3-A1. Does not
  mark SATISFIED. Does not make condition 4 MET.
- **Decision:** Prefix the 16 presently recordable required
  harness identifiers into file 08's harness column. G03/G04
  and G13 receive reservation-only prefixes and are not
  named. G17 receives a dropped/inapplicable prefix and is
  not required-now. G06/G11 unchanged. Rewrite the
  condition-4 snapshot "Measured now" cell to 16 of 18
  required gates named. Do not present 16 of 16. Do not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Condition 4 stays PARTLY MET.
  Named-harness half becomes 16 of 18 required in file 08.
  Owners remain 22 of 22. No QUALIFIED. No SATISFIED.
  Condition 5 remains NOT MET and last.
- **Reversibility:** C-D088 plus restore of the prior
  harness-cell prefixes and the prior condition-4 "Measured
  now" cell. Does not overturn D-086. Overturn: C-D088.
- **Commit:** C-D088.

---

## D-085 — Record DR-102 SATISFIED under D-056 Class A

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-085.review-adversarial.claude2.turn3.json`,
  `828f0fdc25b595a3099e6fc55c99f147988046bc10f633f0829e97b32a05c6b9`).
  Codex
  (`artifacts/coordinator-decisions.D-085.review-adversarial.codex.turn3.json`,
  `1f8adb0ccec93b19f7f4fb76725ec3ab9f89a6374ccb0152eaa42fdb1b163df5`).
  Turn-1 Codex MUST-FIX ADV-D085-01 and Claude 2 SHOULD-FIX
  D085-SF-1 accepted. Turn-2 Codex SHOULD-FIX ADV-D085-T2-01
  accepted (remeasure after D-088). Turn-3 subject
  `coordinator-decisions.D-085.turn3.draft.md`
  `f0c6e54e17f3d67ae2b14fcfbfb81818d1595bf94d1e2fd01143c84a4681aae6`.
- **Decision type:** RULE-GOVERNED. SATISFIED re-record under
  D-056 Class A. File-08 MF-6. Does not execute CC-1..CC-11.
  Does not claim QUALIFIED. Does not overturn D-088.
- **Decision:** Record DR-102 SATISFIED for architecture-preview
  condition 2. CC-1..CC-11 execution remains condition 4 /
  DR-G21 / DR-012. Replace the DR-102 lead, SATISFIED-bar,
  and Blueprint-impact hard-blocker. Rewrite condition 2 to
  1 of 30 SATISFIED, standing NOT MET. Replace only
  "condition 2 remains 0 of 30 SATISFIED" in the one-sentence
  summary. Do not edit D-088 gate-harness cells. Do not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Condition 2 becomes 1 of 30 SATISFIED
  and stays NOT MET. Condition 4 remains PARTLY MET at 16 of
  18. Condition 5 remains NOT MET and last.
- **Reversibility:** C-D085 plus restore of the prior DR-102
  lead, SATISFIED-bar, Blueprint impact cell, condition-2
  snapshot row, and "0 of 30" clause. Does not overturn
  D-056, D-086, D-088, or D-015. Overturn: C-D085.
- **Commit:** C-D085.

---

## D-089 — Record DR-115 SATISFIED under D-056 Class B

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-089.review-adversarial.claude2.turn2.json`,
  `e920fa6ab04422345c0881999959fd3180aadea8a5ab501acef658c23cdad280`).
  Codex
  (`artifacts/coordinator-decisions.D-089.review-adversarial.codex.turn2.json`,
  `a2291f0740920a63b81c1e9cfaed0da4206ef6ec3cd66b213aed6944b8a46b9a`).
  Turn-1 Claude 2 MUST-FIX D089-MF-1 / D089-MF-2 and SHOULD-FIX
  D089-SF-1 accepted. Codex SHOULD-FIX ADV-D089-01 / 02 / 03
  accepted. Turn-2 subject
  `coordinator-decisions.D-089.turn2.draft.md`
  `a31cf8ee0d5d161fde998784dda5a518dd0b1eab87e4e124b5e8ccc180930e62`.
- **Decision type:** RULE-GOVERNED. SATISFIED re-record under
  D-056 Class B. File-08 MF-6. Does not execute measurement
  harnesses. Does not claim QUALIFIED.
- **Decision:** Record DR-115 SATISFIED for architecture-preview
  condition 2. Measurement remains condition 4 / DR-G01..G05 /
  DR-012. Replace the unique DR-115 lead prefix and the
  Blueprint-impact hard-blocker. Rewrite condition 2 to 2 of
  30 SATISFIED, standing NOT MET, preserving D-085 remainders
  and the DR-103 contract note. Replace only "condition 2
  remains 1 of 30 SATISFIED" in the one-sentence summary. Do
  not edit D-088 gate-harness cells. Do not mark
  DR-103/118/119/123 SATISFIED. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Condition 2 becomes 2 of 30 SATISFIED
  and stays NOT MET. Condition 4 remains PARTLY MET at 16 of
  18. Condition 5 remains NOT MET and last.
- **Reversibility:** C-D089 plus restore of the prior unique
  DR-115 lead prefix, Blueprint impact cell, condition-2
  snapshot including D-085 remainder text, and "1 of 30"
  clause. Does not overturn D-006, D-056, D-085, D-086, or
  D-088. Overturn: C-D089.
- **Commit:** C-D089.

---

## D-090 — Remove the duplicate D-089 heading

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-090.review-adversarial.claude2.json`,
  `e3774f1b2cb03194f2130f42e41d0de5c4dbc760a32e5cff0afda26d3f4ce25d`).
  Codex
  (`artifacts/coordinator-decisions.D-090.review-adversarial.codex.json`,
  `fcd104358fdae96f8dd31f16a926228a4b0c33041023f33c1a158660d9d2c7bd`).
  Subject `coordinator-decisions.D-090.draft.md`
  `b240d5e9fd191b4a150ee2107e666aa1138fe80d4a1299eeae3ff5e9627071a4`.
- **Decision type:** RULE-GOVERNED. Recording hygiene. Does
  not reopen D-089. Does not mark SATISFIED.
- **Decision:** Keep the first D-089 recital. Delete the
  second. Do not edit file 08. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. D-089's readiness effect is
  unchanged. Condition 2 stays 2 of 30 SATISFIED and NOT MET.
  Condition 5 stays last.
- **Reversibility:** C-D090 plus restore of the deleted
  second recital. Does not overturn D-089. Overturn: C-D090.
- **Commit:** C-D090.

---

## D-091 — Record DR-119 SATISFIED under D-056 Class B

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-091.review-adversarial.claude2.turn2.json`,
  `31e8e6140f764a417ca0f5ff95957f7e2defb7bbdb024ec9137432da66230794`).
  Codex
  (`artifacts/coordinator-decisions.D-091.review-adversarial.codex.turn2.json`,
  `60d6474725e5a5dc1db21fc24a91f4bc270687c492a913b2c5f0ed83cd32c27c`).
  Turn-1 Claude 2 SHOULD-FIX D091-SF-1 / D091-SF-2 and Codex
  SHOULD-FIX ADV-D091-01 accepted. Turn-2 subject
  `coordinator-decisions.D-091.turn2.draft.md`
  `cf553e4478defab5d0df9126227a46734c7feddb12db7a960a2958a72e978c04`.
- **Decision type:** RULE-GOVERNED. SATISFIED re-record under
  D-056 Class B. File-08 MF-6. Does not execute DR-G14. Does
  not claim QUALIFIED.
- **Decision:** Record DR-119 SATISFIED for architecture-preview
  condition 2. TypeScript-role closure evidence remains
  condition 4 / DR-G14 / DR-012. Replace the unique D-008
  lead prefix and the Blueprint-impact hard-blocker. Rewrite
  condition 2 to 3 of 30 SATISFIED, standing NOT MET,
  preserving D-085 and D-089 remainders and the DR-103
  contract note. Replace only "condition 2 remains 2 of 30
  SATISFIED" in the one-sentence summary. Do not edit D-088
  gate-harness cells. Do not mark DR-103/118/123 SATISFIED.
  Do not authorize `docs/v2/implementation/`.
- **Readiness effect:** Condition 2 becomes 3 of 30 SATISFIED
  and stays NOT MET. Condition 4 remains PARTLY MET at 16 of
  18. Condition 5 remains NOT MET and last.
- **Reversibility:** C-D091 plus restore of the prior unique
  DR-119 lead prefix, Blueprint impact cell, condition-2
  snapshot including D-085/D-089 remainder text, and "2 of 30"
  clause. Does not overturn D-008, D-056, D-085, D-088, D-089,
  or D-090. Overturn: C-D091.
- **Commit:** C-D091.

---

## D-092 — Record DR-123 SATISFIED under D-056 Class B

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-092.review-adversarial.claude2.turn2.json`,
  `6d6b448b4215aa83a5f2f2c1cf5304c20376dbd412677783382880a681985eee`).
  Codex
  (`artifacts/coordinator-decisions.D-092.review-adversarial.codex.turn2.json`,
  `4bd6ef2ef803dd578df2fd7578148d41221608036d78c5633e7f92d2ea6f12ea`).
  Turn-1 Claude 2 SHOULD-FIX D092-SF-1 accepted. Codex turn-1
  NOTE ADV-D092-N1 accepted. Turn-2 subject
  `coordinator-decisions.D-092.turn2.draft.md`
  `3834381774da0cd208ef3f936ad676df9efdfba25c0b441431dec67a9612b603`.
- **Decision type:** RULE-GOVERNED. SATISFIED re-record under
  D-056 Class B. File-08 MF-6. Does not execute DR-G01..G05 /
  G12. Does not claim QUALIFIED. Does not restore G17.
- **Decision:** Record DR-123 SATISFIED for architecture-preview
  condition 2. CLI-baseline evidence remains condition 4 /
  DR-G01..G05 and DR-G12 / DR-012. Replace the unique D-009
  lead-plus-evidence prefix, the unique DR-123 source-pin
  G17 route, and the Blueprint-impact hard-blocker. Rewrite
  condition 2 to 4 of 30 SATISFIED, standing NOT MET,
  preserving D-085, D-089, and D-091 remainders and the
  DR-103 contract note. Replace only "condition 2 remains 3
  of 30 SATISFIED" in the one-sentence summary. Do not edit
  D-088 gate-harness cells. Do not edit the DR-129 source-pin.
  Do not mark DR-103/104/118 SATISFIED. Do not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Condition 2 becomes 4 of 30 SATISFIED
  and stays NOT MET. Condition 4 remains PARTLY MET at 16 of
  18. Condition 5 remains NOT MET and last.
- **Reversibility:** C-D092 plus restore of the prior unique
  DR-123 lead-plus-evidence prefix, unique source-pin cell,
  Blueprint impact cell, condition-2 snapshot including
  D-085/D-089/D-091 remainder text, and "3 of 30" clause.
  Does not overturn D-009, D-056, D-077, D-085, D-088, D-089,
  D-090, or D-091. Overturn: C-D092.
- **Commit:** C-D092.

---

## D-093 — Record host-effect-authorization.v8 as the D-032 host-effect candidate

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3, re-dispatched
  after a freeze-digest mismatch (not a fourth turn; the first
  turn-3 verdicts were freeze-precondition OBJECTs, not merits
  reviews): CONSENT from both independent reviewers, 0 MUST-FIX,
  0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-093.review-adversarial.claude2.turn3.redispatch.json`,
  `b7593d08f7048f052d2ce4d974e87d03bc4719903390caf486f7e9a3a28fc60d`).
  Codex
  (`artifacts/coordinator-decisions.D-093.review-adversarial.codex.turn3.redispatch.json`,
  `9c7afdb068b8edd08aaa8b29d523ec36268eb6d53830a792676fe152c99d4f4c`).
  Turn-1 Claude 2 MUST-FIX D093-MF-1 accepted. Turn-2 Codex
  MUST-FIX ADV-D093-T2-01 accepted. Turn-3 subject
  `coordinator-decisions.D-093.turn3.draft.md`
  `856f7cd23ebb433acdbb3c069cbf7b04087380d4e1c246f6f0e02ade4faaba22`.
- **Decision type:** RULE-GOVERNED. Records independent ACCEPT
  (0 blockers) of a design-contract candidate. Same recording
  class as D-013 / D-015 / D-035 / D-042. File-08 MF-6.
- **Decision:** Record committed
  `host-effect-authorization.v8.json`
  `2cbad5612e546d3bf915074a8ad3fc4cae444122c997e2ddb3fe067d3cd022dc`
  as the host-effect design-contract candidate D-032 requires.
  The artifact stays `CANDIDATE-NOT-APPLIED`, binds NOTHING,
  remains `DO-NOT-SEAL`. Existence plus ACCEPT is not the
  joint-owner FC-C1 recording. DR-105 and DR-114 stay `OPEN`.
  `permission-truth-tables.v2` (D-042) remains DR-105's
  accepted design-contract candidate. A full permission v2
  successor is not owed. Remaining unmet: FC-C1, DR-G09
  fixture execution, BLK-1..BLK-4, D-042 advisory honesty
  work, DR-114 actor-join and fixture-corpus execution.
  Three unique file-08 phrase replacements only. Does not
  change condition-2 SATISFIED counts. Does not record the
  uncommitted working-tree mutation `2d95f22c…`. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays 4
  of 30 and NOT MET. Condition 4 unchanged. Condition 5
  remains NOT MET and last.
- **Reversibility:** C-D093 plus restore of the three unique
  DR-105/DR-114 phrases. Does not overturn D-032, D-035,
  D-042, or D-092. Overturn: C-D093.
- **Commit:** C-D093.

---

## D-094 — D-006 fleet-class successor plus G03/G04 named identifiers (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000
  clause 2. Not adopted. No forced consensus. Parked.
  Claude 2 turn 3 CONSENT, 0 MUST-FIX, 0 SHOULD-FIX, 1 NOTE
  (`artifacts/coordinator-decisions.D-094.review-adversarial.claude2.turn3.json`,
  `ac65e0ee53c04868118f27128aa27dc9a5cfa33f4d9c4d88946e2532103776ee`).
  Codex turn 3 OBJECTIONS, 2 MUST-FIX ADV-D094-T3-01 /
  ADV-D094-T3-02 and 1 SHOULD-FIX ADV-D094-T3-03
  (`artifacts/coordinator-decisions.D-094.review-adversarial.codex.turn3.json`,
  `9af90e32136e6902c91713f697d37e0aca44db8a148209f1bc1ba3930fa382d1`).
- **Decision type:** PREFERENCE-LADEN successor plus
  RULE-GOVERNED naming. Not adopted.
- **Subject:** `coordinator-decisions.D-094.turn3.draft.md`
  `5fd1671050323a84dcd72245cb7ae4fd19e67170dc524ef408dbb5c1bcf19449`.
- **Positions parked:** Claude 2 accepts the hosted-fleet
  contract, class-trade table, and 18-of-18 naming. Codex
  refuses naming until (1) release-to-release regression
  controls CPU-brand and weekly-image drift (paired or
  stratified, not same-class-only) and (2) N=11 plus no
  quantile estimator cannot produce distinct D-006 p95/p99
  measurements. SHOULD-FIX: preflight observables
  underspecified.
- **Decision:** None. File 08 is not edited. G03/G04 stay
  reserved. Condition 4 stays 16 of 18 and PARTLY MET. A
  later new cycle (not turn 4) may retry.
- **Readiness effect:** Zero. Condition 4 unchanged.
  Condition 5 last.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D094.

---

## D-095 — Record the five preview-deferral v2 candidates (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000
  clause 2. Not adopted. No forced consensus. Parked.
  Claude 2 turn 3 CONSENT, 0 MUST-FIX, 0 SHOULD-FIX
  (`artifacts/coordinator-decisions.D-095.review-adversarial.claude2.turn3.json`,
  `4e204b776680b2035a301d5263582a350a11d4408d7dda73324ae5b5c833ef9f`).
  Codex turn 3 OBJECTIONS, 1 MUST-FIX ADV-D095-T3-01
  (`artifacts/coordinator-decisions.D-095.review-adversarial.codex.turn3.json`,
  `8f0f05e1fe06bef22be94cca0f7a662f728e5146278e7bbf3f69a609be3cf64e`).
- **Decision type:** RULE-GOVERNED candidate recording. Not
  adopted.
- **Subject:** `coordinator-decisions.D-095.turn3.draft.md`
  `c0c86be97c11256afc65e8950fb1a8373c42575f2db439a54a46545cacdaea34`.
- **Positions parked:** Claude 2 accepts the coordinator
  recording and the blocked owner path. Codex refuses
  adoption while Decision item 3 still lets a mechanics
  entry substitute for a missing owner grant (`either`
  user amendment `or` mechanics). Required repair:
  grant **and** mechanics; mechanics never grants.
- **Decision:** None. File 08 is not edited. The five v2
  candidates remain independently ACCEPTED and
  unrecorded. A later new cycle (not turn 4) may retry.
- **Readiness effect:** Zero.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D095.

---

## D-096 — Record the five preview-deferral v2 candidates

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-096.review-adversarial.claude2.json`,
  `c9e2045724ef08358bfca51111597ca4ce2e33d8a58fe0498a2391a09a4c9ec7`).
  Codex
  (`artifacts/coordinator-decisions.D-096.review-adversarial.codex.json`,
  `d428d0cdf5e75d9844465485933a6e7a6fe11e27fe6688f4080657b2988736b7`).
  Subject `coordinator-decisions.D-096.draft.md`
  `df7a6143b0b695aa3de4cee2ecd780630da15e206798dbc430a6bb1144398f95`.
  New cycle after D-095 CONTESTED. ADV-D095-T3-01 accepted.
- **Decision type:** RULE-GOVERNED. Coordinator recording of
  independently accepted design-contract / deferral
  candidates. Same class as D-013 / D-035 / D-042 / D-066.
- **Decision:** Record the five preview-deferral v2 artifacts
  as accepted architecture-preview explicit-deferral
  candidates. Each stays `CANDIDATE-NOT-RECORDED`, binds
  NOTHING, remains `DO-NOT-SEAL`. This entry does not make
  the coordinator those owners. D-054 / D-057 do not supply
  the later owner path. Owner-recording remains blocked
  until both (A) an applicable owner grant covering every
  named role for the candidate being recorded and (B)
  separately D-000-reviewed condition-2 owner-recording
  mechanics. A mechanics entry alone never grants. DR-116
  Route C does not generalize. DEF110-C2-A1 remains owed as
  honesty work. Does not edit file 08. Does not mark any
  row SATISFIED. Does not retry D-094. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2
  unchanged. Condition 4 stays 16 of 18 PARTLY MET.
  Condition 5 last.
- **Reversibility:** C-D096. Does not overturn D-002, D-054,
  D-057, D-093, D-094, or D-095.
- **Commit:** C-D096.

---

## D-097 — Withdraw the coordinator-composed C2 owner grant

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-097.review-adversarial.claude2.turn2.json`,
  `41e7830a8e7f4fec7972b34a410ee75bd3ed5dea3489d9e3ef859634a9901415`).
  Codex
  (`artifacts/coordinator-decisions.D-097.review-adversarial.codex.turn2.json`,
  `f33c1b55fc128426107f0a45807bcacac3f1d0332ad1f2816079c7e994bf28da`).
  Turn-1 Claude 2 MUST-FIX D097-MF-1 and Codex MUST-FIX
  ADV-D097-01 accepted. Turn-2 subject
  `coordinator-decisions.D-097.turn2.draft.md`
  `c25cd9771e8e31ce78e80c5cabac9ad1d3435bb8f01164c4b03feceab01fb5eb`.
- **Decision type:** RULE-GOVERNED withdrawal. Does not adopt
  a user amendment.
- **Decision:** Withdraw the turn-1 coordinator-composed
  condition-2 owner grant. Adopt nothing as D-096 (A).
  D-096 (A) remains unsatisfied. Owner-recording of the
  five candidates stays blocked until the user makes an
  express grant. Do not edit file 08. Do not mark SATISFIED.
  Do not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 unchanged.
  Condition 4 stays 16 of 18 PARTLY MET. Condition 5 last.
- **Reversibility:** C-D097 (withdrawal). Overturn: C-D097.
- **Commit:** C-D097.

---

## D-098 — D-006 fleet-class successor plus G03/G04 named identifiers (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. File 08 not edited.
  Claude 2 turn 3 CONSENT, 0 MUST-FIX, 0 SHOULD-FIX, 1 NOTE
  (`artifacts/coordinator-decisions.D-098.review-adversarial.claude2.turn3.json`,
  `414bf343fa61cf42639d99578fd1eeaecea8c335f3090f4aeed5400a36864f2a`).
  Codex turn 3 OBJECTIONS, 0 MUST-FIX, 1 SHOULD-FIX ADV-D098-T3
  process-architecture observation
  (`artifacts/coordinator-decisions.D-098.review-adversarial.codex.turn3.json`,
  `223689de85d9d49b1b06c92acd86f759e524e4e0b38bfb194413f8d24e40859b`).
  Turn-3 subject `coordinator-decisions.D-098.turn3.draft.md`
  `5ad6884a06aa450bc2cbc0f286b3366eb9e029922e92a0ae6937868e37e05031`.
- **Decision type:** PREFERENCE-LADEN. Not adopted.
- **Both positions (required by D-000 clause 2):**
  Claude 2: fleet contract complete; G03/G04 may be named;
  condition 4 may become MET.
  Codex: process-architecture recipe still observes the
  inspector (`file /proc/self/exe`) or a fat-image slice,
  not the launched target process. CONSENT withheld;
  G03/G04 stay reserved; condition 4 stays 16 of 18
  PARTLY MET.
- **Decision:** None. File 08 is not edited. A later new
  cycle (not turn 4) may retry.
- **Readiness effect:** Zero. Condition 4 unchanged.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D098.

---

## D-099 — D-006 fleet-class successor plus G03/G04 named identifiers (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. File 08 not edited.
  Claude 2 turn 3 OBJECT, 1 MUST-FIX D099-T3-MF-1, 1
  SHOULD-FIX D099-T3-SF-1
  (`artifacts/coordinator-decisions.D-099.review-adversarial.claude2.turn3.json`,
  `83b0aefe6487882adff7a7317e10f4445161fc14c65d47aa339d052cafe6f2a7`).
  Codex turn 3 OBJECTIONS, 1 MUST-FIX ADV-D099-T3-01
  (`artifacts/coordinator-decisions.D-099.review-adversarial.codex.turn3.json`,
  `c53c261f71496b86e5c7bf43d6d87d5a606d5a2bc7e129b05db1a8e04a9c1d47`).
  Turn-3 subject `coordinator-decisions.D-099.turn3.draft.md`
  `3249a26c738c35cbd20f31ebe442559fc027acc764a610cb4dc93eac3b4ee47a`.
- **Decision type:** PREFERENCE-LADEN. Not adopted.
- **Both positions (required by D-000 clause 2):**
  Both reviewers: the hosted-fleet contract and unique
  pin table are otherwise in place, but the macOS
  preflight names a `kinfo_proc` CPU-type member and a
  `PROC_PIDT_SHORTBSDINFO` start-time member that those
  structures do not have on macOS 15. CONSENT withheld;
  G03/G04 stay reserved; condition 4 stays 16 of 18
  PARTLY MET.
- **Decision:** None. File 08 is not edited. A later new
  cycle (not turn 4) may retry.
- **Readiness effect:** Zero. Condition 4 unchanged.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D099.

---

## D-101 — D-006 fleet-class successor plus G03/G04 named identifiers (CONTESTED)

- **Date:** 2026-08-14
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. File 08 not edited.
  Claude 2 turn 3 CONSENT, 0 MUST-FIX, 0 SHOULD-FIX, 5 NOTES
  (`artifacts/coordinator-decisions.D-101.review-adversarial.claude2.turn3.json`,
  `8e3828071c789ec2f05903ee1ed44af376b88751957f6ebf8e90bfa10d8c6921`).
  Codex turn 3 OBJECTIONS, 0 MUST-FIX, 1 SHOULD-FIX
  ADV-D101-T3-01 (disposition row vs cold-only sequence)
  (`artifacts/coordinator-decisions.D-101.review-adversarial.codex.turn3.json`,
  `b0819a1dc14522c37d0caef61bdfec9c19778af622e44f9ac6b21e1931da6209`).
  Turn-3 subject `coordinator-decisions.D-101.turn3.draft.md`
  `ba5f8fc8ae336de0073642fd6e3ac2bc549988256b20068e2864df3ff1e66eae`.
- **Decision type:** PREFERENCE-LADEN. Not adopted.
- **Both positions (required by D-000 clause 2):**
  Claude 2: fleet contract and hash/purge split complete;
  G03/G04 may be named; condition 4 may become MET.
  Codex: the D101-T2-MF-1 disposition row still says
  `stat` immediately before each timed launch, which
  contradicts the cold-only numbered sequence. CONSENT
  withheld; G03/G04 stay reserved; condition 4 stays
  16 of 18 PARTLY MET.
- **Decision:** None. File 08 is not edited. A later new
  cycle (not turn 4) may retry.
- **Readiness effect:** Zero. Condition 4 unchanged.
- **Reversibility:** n/a (not adopted).
- **Commit:** C-D101.

---

## D-102 — D-006 fleet-class successor plus G03/G04 named identifiers

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-102.review-adversarial.claude2.turn2.json`,
  `99cb237f572d81490cad2f263751ade5c2b68b2df5bfba38e71c5d3eac070132`).
  Codex
  (`artifacts/coordinator-decisions.D-102.review-adversarial.codex.turn2.json`,
  `212509cb454d30930d2cb9b972060e258367e59199ee543fae57319f6ef5852d`).
  Turn-1 Claude 2 SHOULD-FIX D102-T1-SF-1 accepted
  (`CPU_SUBTYPE_ANY` + `ocount == 1`). Turn-2 subject
  `coordinator-decisions.D-102.turn2.draft.md`
  `7780190e87226e6794f55cf6c15bf7c510c975c8ed40affc4eb0a9129f2e8298`.
  New cycle after D-101 CONTESTED.
- **Decision type:** PREFERENCE-LADEN scoped D-006 successor
  plus RULE-GOVERNED naming of the v3 reserved identifiers.
- **Decision:** Adopt the hosted-fleet-class measurement
  contract. Write G03/G04 reserved identifiers into file 08
  as named. Not authored. Not QUALIFIED. Condition 4 becomes
  18 of 18 named required gates, standing **MET**. MET is
  not QUALIFIED and does not authorize implementation.
  Does not name G13. Does not restore G17. Does not mark
  any row SATISFIED. Does not satisfy D-096 (A).
- **Readiness effect:** Condition 4 becomes MET. Condition 2
  stays 4 of 30 NOT MET. Condition 5 remains NOT MET and last.
- **Reversibility:** C-D102 plus restore of the two reserved
  cells, 16-of-18 fragment, PARTLY MET, one-sentence clause,
  D-006's pre-successor exact-machine and exact-OS
  requirements, and the original D-006 runner classes.
  Does not overturn D-101 CONTESTED.
- **Commit:** C-D102.

---

## D-100 — Condition-2 preview-deferral owner-recording mechanics

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-100.review-adversarial.claude2.turn3.json`,
  `96db1ae053c56dfaaff6575e98ba6d786982d89169855030c2121042aae63ddf`).
  Codex
  (`artifacts/coordinator-decisions.D-100.review-adversarial.codex.turn3.json`,
  `909a9f7c87a180eca33077174b4dc60edbeab29eab67639f92ae032cf707c2a4`).
  Turn-1 Codex MUST-FIX ADV-D100-01 accepted (106/109/113
  severability). Turn-2 Claude 2 MUST-FIX D100-T2-MF-1
  accepted (candidate-keying; Windows is not a file-08
  row). Turn-3 subject
  `coordinator-decisions.D-100.turn3.draft.md`
  `0f41a9f8008a85f4b0e1e5ac785b19aec27a028d252a48fe0008102969b99293`.
- **Decision type:** RULE-GOVERNED. Mechanics only. Authority
  is a later user-made D-096 (A) grant, not this entry.
- **Decision:** Later condition-2 preview-deferral
  owner-recording entries must satisfy the preconditions
  and pins in the adopted turn-3 subject. Eligible
  candidates are the five D-096 artifacts only. The
  106/109/113 artifact is a shared draft: each recording
  names exactly one of those rows, own cycle and commit.
  Windows is not a file-08 row. This file does not grant.
  D-054 / D-057 do not cover these rows. Mechanics alone
  never grants. Does not mark SATISFIED. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. D-096 (A) stays unsatisfied.
  Condition 2 unchanged. Condition 5 last.
- **Reversibility:** C-D100 revokes these mechanics. D-096
  remains until C-D096. Overturn also requires superseding
  every owner recording that cites D-100 and reconciling
  each dependent MF-6 note under its own reviewed act.
- **Commit:** C-D100.

---

## D-103 — Record compatibility-matrices-contract.v5 as DR-111's accepted design-contract candidate

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-103.review-adversarial.claude2.json`,
  `c132520ac57cf63a0b78d62802d0fdfe68f656831ae4a7da352689c5b80377d3`).
  Codex
  (`artifacts/coordinator-decisions.D-103.review-adversarial.codex.json`,
  `e84548551ced78b4cae23dc989f8f3393686f4579b2c1fdf68bff19f2298e8cb`).
  Subject `coordinator-decisions.D-103.draft.md`
  `7f353629e669dfd0ace55163edf637915ab4e5c1d1c2826dddfd4174532eee61`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042.
- **Subject:** `docs/coop/artifacts/compatibility-matrices-contract.v5.json`
  `d0386cee26d8aafd3d07b46f21352cc3d9d03cdc8f406de0adf571f8c81f7f41`.
- **Verdicts:** Claude 2
  `compatibility-matrices-contract.v5.review-independent.claude2.json`
  `40a638d4c80601f77b3ff3c7c8de570b8c4c1669405003f0eb445bdd4df2f55b`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `compatibility-matrices-contract.v5.review-independent.codex.json`
  `453ec57d98b9caa503b969b49fb99846aa19da830e4b21b70a7395ca550d1731`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v5 as DR-111's accepted design-contract
  candidate. Advisories (Claude ADV-1/ADV-2; Codex CMCV5-A1)
  travel as honesty work. Claude D-103 advisories ADV-D103-01
  and ADV-D103-02 also travel and do not reopen the recording.
  DR-111 stays OPEN. No SATISFIED. Numeric windows remain
  RESERVED. S-EVIDENCE remains deferred with DR-113. No lock
  is producible. D-056 Class A is not opened. Does not edit
  file 08. Does not mint a D-096 (A) grant. Does not dispose
  DR-117. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D103.
- **Commit:** C-D103.

---

## D-104 — Record component-manifest-schemas.v11 as DR-103's accepted schema successor

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-104.review-adversarial.claude2.turn2.json`,
  `ce5c7a7e024f9e30c97ab0b4322290c9c840a643fe531a58e799b95ecb4c3555`).
  Codex
  (`artifacts/coordinator-decisions.D-104.review-adversarial.codex.turn2.json`,
  `cda38e9dd8930bf2d215bcd2a00d0441a756623cb8886905cb790262550e5fa8`).
  Turn-1 Codex SHOULD-FIX D104-SF-1 accepted (header no longer
  cites unadopted D-103 as a form precedent). Turn-2 subject
  `coordinator-decisions.D-104.turn2.draft.md`
  `fe51b4fa36ab3efdcc6cd8d1d48e706fb4584ebb83cfc10cb1c602335fa40eb4`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT-WITH-ADVISORIES (0 blockers, 0 SHOULD-FIX from both
  reviewers). Same form as D-013 / D-015 / D-035 / D-042.
- **Subject:** `docs/coop/artifacts/component-manifest-schemas.v11.json`
  `1c0b8868444a097256aaa7d9caf8ebaa1c6f73fb071dbb4dd712334abb17a005`.
- **Verdicts:** Claude 2
  `component-manifest-schemas.v11.review-independent.claude2.json`
  `45785457b25e50e51be7f3a1393427de637022752a9af70b38e87ecb79ce0f20`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX. Codex
  `component-manifest-schemas.v11.review-independent.codex.json`
  `25b2a3fb0200cab5132b333543a708c3bfb024e1fab11b9751c44696e52b1372`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v11 as DR-103's accepted schema successor.
  D-013 remains the historical recording of schemas.v2 and is
  not overturned. Advisories CLAUDE-V11-A1, CLAUDE-V11-A2, and
  CODEX-V11-A1 (distinct findings; same local id) travel as
  honesty work. Claude D-104 turn-2 advisories ADV-D104T2-01
  (draft COORD pin is the pre-D-103 snapshot) and ADV-D104T2-02
  also travel. DR-103 stays OPEN. No SATISFIED. Fixture-corpus
  half remains unmet. No lock is producible. D-013
  SATISFIED-refusal stands. D-056 Class A is not opened. Does
  not edit file 08. Does not mint a D-096 (A) grant. Does not
  dispose DR-117. Does not retarget corpus v2. Does not
  authorize `docs/v2/implementation/`. Corpus v3, if authored,
  may now pin schemas.v11.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D104.
- **Commit:** C-D104.

---

## D-105 — Record signed-index-trust-contract.v8 as DR-112's accepted design-contract candidate

- **Date:** 2026-08-14
- **Status:** **ADOPTED 2026-08-14.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-105.review-adversarial.claude2.json`,
  `913a69918119f1fba003b099967fb7144ea046f5d5d5c41da35553e7f3b34293`).
  Codex
  (`artifacts/coordinator-decisions.D-105.review-adversarial.codex.json`,
  `930dc4af1aa81887ab3f2ce6c6488f24ffd69d4b4633c4919d1de8ad179ceda8`).
  Subject `coordinator-decisions.D-105.draft.md`
  `6cdf1eff18409be9db5d8e4d1730658586979561eaab850c7554f4493ee94107`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104.
- **Subject:** `docs/coop/artifacts/signed-index-trust-contract.v8.json`
  `fc171321e969c74464dbc9ff67edd9b874aac1d1c7375c7dc8e431469442efe0`.
- **Verdicts:** Claude 2
  `signed-index-trust-contract.v8.review-independent.claude2.json`
  `559cfad1f29443326734fe4cc480aca802bfac118668080956af59534029dead`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX. Codex
  `signed-index-trust-contract.v8.review-independent.codex.json`
  `10784a6de2c2767cec5ce55549cc75d4402cd93f4fe5342e8ff95c5236fead13`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v8 as DR-112's accepted design-contract
  candidate. This is coordinator decision D-105, not register
  row DR-105. Advisories CLAUDE-V8-A1 (ADV-V8-01: memberApplicability
  parenthetical omits recovery PRESENT member 18) and CODEX-V8-A1
  (SITCV8-A1: Codex v7 pin) travel as honesty work; they are
  distinct findings. CODEX-V8-A1 is recorded here by pinning
  Codex v7 `ffe079b9c634fe97a2a735fbda99efac386505870e11b31b2b23753c6f38a1e5`
  COMPLETE REJECT, 0/1/0, SITCV7-S1 only. DR-112 stays OPEN. No
  SATISFIED. Quorum, clock/freshness, emergency, and waiver
  numbers remain RESERVED. Repair-media remains DR-110.
  Newly-revoked replay remains DR-113. G06/G08 stay
  named-not-authored / not QUALIFIED. No lock is producible.
  D-056 Class A is not opened. Does not edit file 08. Does not
  mint a D-096 (A) grant. Does not dispose DR-117. Does not
  SATISFY DR-103 or DR-105. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D105.
- **Commit:** C-D105.

---

## D-106 — Record component-manifest-fixture-corpus.v6 as DR-103's accepted fixture-corpus candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-106.review-adversarial.claude2.turn3.json`,
  `2837edaf7bd40541e755e33b21d7b15839e21a3009e65b01f33e3b57311f24ad`).
  Codex
  (`artifacts/coordinator-decisions.D-106.review-adversarial.codex.turn3.json`,
  `e1254ecdefe977ae6cf45ed63afb3eb7fc8fbe26b1489872c1e148ddb30a8e55`).
  Turn-1 Claude OBJECT CLAUDE-D106-M1 accepted (the register is
  `docs/v2/architecture/08-decision-and-readiness-register.md`,
  not `docs/coop/architecture/08-surfaces-and-topology.md`).
  Turn-2 Codex OBJECT CODEX-D106T2-M1 accepted (turn-1 Claude
  pin is the reproducing digest `1e3f4a6a…`, not the
  unretrievable `06f4c343…`). Turn-3 subject
  `coordinator-decisions.D-106.turn3.draft.md`
  `5ff4a9ba3cb9666378c1fe5fabc905f047ee1cb3e6a208ecc2aa744ca8048a44`.
  Claude 2 turn-3 advisory ADV-D106T3-01 travels as honesty
  work.
- **Decision type:** RULE-GOVERNED. Records independent dual
  SATISFIED-GRADE ACCEPT (0 blockers, 0 SHOULD-FIX from both
  reviewers). Same form as D-013 / D-015 / D-035 / D-042 /
  D-103 / D-104 / D-105.
- **Subject:** `docs/coop/artifacts/component-manifest-fixture-corpus.v6.json`
  `8dfa9346ada4fefce0aabca96062208e4fea7371a6aab68eaee75cdc908a21a5`.
- **Verdicts:** Claude 2
  `component-manifest-fixture-corpus.v6.review-independent.claude2.json`
  `b99dda48366dee5e0c90aae2c9475ca82d8152fcf302ad4898f52faaf51d533a`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX. Codex
  `component-manifest-fixture-corpus.v6.review-independent.codex.json`
  `4ff72e1088169f0f11132bdc64d8e664d4add7711ffee604681af088f79c2a71`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v6 as DR-103's accepted fixture-corpus
  candidate. This is coordinator decision D-106, not register
  row DR-106. Advisories CLAUDE-V6-A1 / CODEX-V6-A1 (same
  `/date` roster defect) travel as honesty work; they are
  one class. DR-103 stays OPEN. No SATISFIED. D-013
  SATISFIED-refusal stands. D-104 schemas.v11 recording
  stands. Unicode-norm duplicate remains BLOCKED. Locks
  remain deferred to DR-111. No fixture executed. No lock
  producible. D-056 Class A is not opened. Does not retarget
  corpus v2/v3/v4/v5. Does not mutate `fixtures/dr-103.v2/`
  or `fixtures/dr-103.v4/`. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117.
  Does not SATISFY DR-111, DR-112, or DR-105. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D106.
- **Commit:** C-D106.

---

## D-107 — Record lifecycle-generation-contract.v2 as DR-107's accepted design-contract candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-107.review-adversarial.claude2.json`,
  `004f8923698821d2062a64ea7cc7bc8c1825c64f098ef6b3a902a5fba74f67c2`).
  Codex
  (`artifacts/coordinator-decisions.D-107.review-adversarial.codex.json`,
  `b9f2527664bcd9aa43e426f155e4168d0f8ef5be1a63735edc86d8d9f2ef3bd1`).
  Subject `coordinator-decisions.D-107.draft.md`
  `caffcbe66416a9aa67863d5171824b704ea9517b00c1474291835db874b5d96a`.
  Claude 2 turn-1 advisories CLAUDE-D107T1-A1 and
  CLAUDE-D107T1-A2 travel as honesty work.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106.
- **Subject:** `docs/coop/artifacts/lifecycle-generation-contract.v2.json`
  `a5f9d6a35f83d64687cdd2a00ec3106251ae407e54a5538727c086dd8f9ab77b`.
- **Verdicts:** Claude 2
  `lifecycle-generation-contract.v2.review-independent.claude2.json`
  `b4d47968e6f25a94907b8933887acba811165a9870640f178c35e98fdcfaa9d2`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `lifecycle-generation-contract.v2.review-independent.codex.json`
  `2643387c882d1de9508a6a413c2734ec1516ad43394a4493fba6c594b2ec69ee`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v2 as DR-107's accepted design-contract
  candidate. This is coordinator decision D-107, not register
  row DR-107. Advisory CLAUDE-V2-A1 (`/date` roster) travels as
  honesty work. DR-107 stays PROPOSED-CLOSED-FOR-REVIEW / OPEN.
  No SATISFIED. DR-G18 stays named-not-authored / not QUALIFIED.
  Concrete journal/lock/lease encoding remains reserved.
  Generation-rollback remains distinct from DR-110 self-update
  rollback. No lock is producible. D-056 Class A is not opened.
  Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117.
  Does not SATISFY DR-103, DR-111, DR-112, or DR-105. Does not
  overturn D-106. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D107.
- **Commit:** C-D107.

---

## D-108 — Record component-packaging-contract.v14 as DR-120's accepted design-contract candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-108.review-adversarial.claude2.json`,
  `bfb93b464b197f4ca8d09a099c25a5013b3eeb3f590057853c473ea0653b9ba7`).
  Codex
  (`artifacts/coordinator-decisions.D-108.review-adversarial.codex.json`,
  `bc1c35952974effea42b2ac02013b88a8399da78a0809d69e5d95ed96e00be5f`).
  Subject `coordinator-decisions.D-108.draft.md`
  `2eefe870b4739a04a5a8b09369fffb8ac71901c244fd7fcdcd8deaf958d2b529`.
  Claude 2 turn-1 advisories CLAUDE-D108T1-A1 and
  CLAUDE-D108T1-A2 travel as honesty work.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107.
- **Subject:** `docs/coop/artifacts/component-packaging-contract.v14.json`
  `8321d527843c63592d8e4fd49c3df0ace690da0bcbcd1e268464e578fe30424c`.
- **Verdicts:** Claude 2
  `component-packaging-contract.v14.review-independent.claude2.json`
  `b47485eb9ba2221e223fcecd588e3d6d49e86918aee7e672276c652aabddaf79`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `component-packaging-contract.v14.review-independent.codex.json`
  `ee4fd95833d165a936bd2ba14dac2345dbb59b523985bc30f142f610053170e5`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v14 as DR-120's accepted design-contract
  candidate. This is coordinator decision D-108, not register
  row DR-108. Advisories CLAUDE-V14-A1, CODEX-V14-A1, and
  CODEX-V14-A2 travel as distinct honesty work. DR-120 stays
  OPEN. No SATISFIED. DR-G15 stays named-not-authored / not
  QUALIFIED. Adapter implementations remain reserved. D-056
  Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117.
  Does not SATISFY DR-103, DR-107, DR-111, DR-112, or DR-105.
  Does not overturn D-106 or D-107. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D108.
- **Commit:** C-D108.

---

## D-109 — Record permission-truth-tables.v6 as DR-105's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-109.review-adversarial.claude2.json`,
  `190b4d2654c58f41e949bf47641a67d1abc1cb5b8e26f6e0c923b8c7b8d7551f`).
  Codex
  (`artifacts/coordinator-decisions.D-109.review-adversarial.codex.json`,
  `96163dd33fe4e0a22f5a28808a0d916243d208bcc20f87d3ef9eb03db295d1b0`).
  Subject `coordinator-decisions.D-109.draft.md`
  `0158d9c92ec8d116a98faf286688408ca50ca6a14e28c6cc69b24212a9496acf`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT-WITH-ADVISORIES (0 blockers, 0 SHOULD-FIX from both
  reviewers). Same form as D-013 / D-015 / D-035 / D-042 / D-103 /
  D-104 / D-105 / D-106 / D-107 / D-108.
- **Subject:** `docs/coop/artifacts/permission-truth-tables.v6.json`
  `ad1bb75d7f029f64979d3c4e6fe5dd3446cd30465b36d4a7b3f9471f06a6dd34`.
- **Verdicts:** Claude 2
  `permission-truth-tables.v6.review-independent.claude2.json`
  `9ec9f0563030e5bb06880fff1f8b483fde28e05465e5cc19d9d1087b08b1e20b`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX. Codex
  `permission-truth-tables.v6.review-independent.codex.json`
  `431f9b8629d947825dcaa2ed9289c84c3f376460dcffba80afe700803bbe3a21`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v6 as DR-105's accepted design-contract
  successor candidate. This is coordinator decision D-109, not
  register row DR-109. D-042 remains the historical recording of
  permission-truth-tables.v2 and is not overturned. Advisories
  CLAUDE-V6-A1 and CODEX-V6-A1 travel as distinct honesty work.
  DR-105 stays OPEN. No SATISFIED. Host-effect candidate remains
  D-093 / v8. Joint-owner FC-C1, DR-G09 execution, and BLK-1..BLK-4
  remain. D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-103, DR-107, DR-111, DR-112, or DR-120. Does not
  overturn D-106, D-107, or D-108. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D109.
- **Commit:** C-D109.

---

## D-110 — Record component-sdk-contract.v4 as DR-125's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-110.review-adversarial.claude2.turn2.json`,
  `912d59443532484b3c7c402179d6b052fefd51a0b0490db764d5a90da4efca81`).
  Codex
  (`artifacts/coordinator-decisions.D-110.review-adversarial.codex.turn2.json`,
  `dbda1fb66b5cce37a3ff00fa238e2b6795bc47a7699953c9d8834356c305d0d0`).
  Subject `coordinator-decisions.D-110.turn2.draft.md`
  `99dc617265413e79b09f168621d68fc5dcf029175e4dae83a98501823066b720`.
  Turn-1 OBJECT `CLAUDE-D110-S1` is folded; turn-1 draft
  `dfdc7cce2e20505e4f0f13752a48fec68ede4ae9ce8b985bbe6a4ae99316e5af`
  is not retargeted.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109.
- **Subject:** `docs/coop/artifacts/component-sdk-contract.v4.json`
  `c53d541f12258eb96e86f0f5dbd3924a5f2e189d19c8f8672bae9037532461c3`.
- **Verdicts:** Claude 2
  `component-sdk-contract.v4.review-independent.claude2.json`
  `b4a4b672174ba1893b071984f6cdb0cb56c99fefe0310b821e87ac454a599bff`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, observations O-1/O-2/O-3.
  Codex
  `component-sdk-contract.v4.review-independent.codex.json`
  `c0cfad60a052abefd8ee08ea0f01a60bf9b6b3e459a619d13ddc895b6b0ed559`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v4 as DR-125's accepted design-contract
  successor candidate. This is coordinator decision D-110, not
  register row DR-110. Claude observations CLAUDE-V4-O1/O2/O3
  travel as honesty work. O-4 is resolved. DR-125 stays OPEN.
  No SATISFIED. No QUALIFIED. G20 remains NAMED-NOT-AUTHORED.
  Exact SDK APIs/frameworks remain reserved. The candidate binds
  NOTHING. D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-103, DR-107, DR-108, DR-111, DR-112, DR-120,
  DR-121, DR-122, DR-124, DR-126, or DR-127. Does not overturn
  D-106, D-107, D-108, or D-109. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D110.
- **Commit:** C-D110.

---

## D-111 — Record anti-lockstep-contract.v7 as DR-127's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-111.review-adversarial.claude2.json`,
  `986509724d9207017c944deb03aedadcd0291cd00c7b95e3579083c7c7a416c5`).
  Codex
  (`artifacts/coordinator-decisions.D-111.review-adversarial.codex.json`,
  `8ca86bdc45e3ca79693c0aec6302a4ea48ae3976cbe3052303c17a5fe27537a2`).
  Subject `coordinator-decisions.D-111.draft.md`
  `7eba6fc906cf169952d325f6e62d467556cfa3dad7e41f51bf96a0076f553bdc`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110.
- **Subject:** `docs/coop/artifacts/anti-lockstep-contract.v7.json`
  `8c41bddd7c351abc3a0b4b721f9302df29ba7d053352cb950ec8b23e4afdd671`.
- **Verdicts:** Claude 2
  `anti-lockstep-contract.v7.review-independent.claude2.json`
  `73fb7bde942b1b393faa928c4db3538fb7dfa58faee6bb8f4ad66368d2a67235`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory CLAUDE-V7-A-1.
  Codex
  `anti-lockstep-contract.v7.review-independent.codex.json`
  `9f1adab71c6231a0e72a37f301f5e253453f2a76f1545739e27f40eba30d9663`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v7 as DR-127's accepted design-contract
  successor candidate. This is coordinator decision D-111, not
  register row DR-111. D-110 remains the adopted SDK-v4 recording
  and is not retargeted. Claude advisory CLAUDE-V7-A-1 travels as
  honesty work. DR-127 stays OPEN. No SATISFIED. No QUALIFIED.
  Hostile dual-channel goldens remain named, not authored here.
  CC-1..CC-11 remain specifications (D-015), not this row's
  executed SATISFIED evidence. The candidate binds NOTHING.
  D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-103, DR-107, DR-108, DR-110 (register row),
  DR-111, DR-112, DR-120, DR-121, DR-122, DR-124, DR-125, or
  DR-126. Does not overturn D-106, D-107, D-108, D-109, or D-110.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D111.
- **Commit:** C-D111.

---

## D-112 — Record secret-storage-contract.v3 as DR-108's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-112.review-adversarial.claude2.json`,
  `f657ca3ca43701f2552863124685fde78d384810c5575c0a05381f67b232ce71`).
  Codex
  (`artifacts/coordinator-decisions.D-112.review-adversarial.codex.json`,
  `02e3e170e343a1994a4051dfaf9b568e04a58b4d8e720b3a6deeb0bb3c5cd260`).
  Subject `coordinator-decisions.D-112.draft.md`
  `60e28353d1eff77979e8fdf1bd67a6d0350e40e4d333c56765d3ffa807118ed4`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111.
- **Subject:** `docs/coop/artifacts/secret-storage-contract.v3.json`
  `2919b5cd77782cdb3785650390de6b25725c850bd5b359bf7fccd62265651923`.
- **Verdicts:** Claude 2
  `secret-storage-contract.v3.review-independent.claude2.json`
  `1d198228f0eca04ac0bc62ad845be24156ec6409a698a40b4a356c0ae2b99857`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories ADV-1/ADV-2.
  Codex
  `secret-storage-contract.v3.review-independent.codex.json`
  `9561dee0c1584b00b885135a30b5e145095e4ea9d616005aee3005a7a4513261`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v3 as DR-108's accepted design-contract
  successor candidate. This is coordinator decision D-112, not
  register row DR-112. D-111 remains the adopted anti-lockstep-v7
  recording and is not retargeted. D-110 remains the adopted
  SDK-v4 recording. Claude advisories CLAUDE-V3-A1 (ADV-1) and
  CLAUDE-V3-A2 (ADV-2) travel as honesty work, as does review
  advisory CLAUDE-D112-A1 (unqualified ADV-* ids in the draft).
  DR-108 stays OPEN. No SATISFIED. No QUALIFIED. OS keychain and
  user-file fallback remain proposed and unexercised in the first
  slice. Exact APIs remain reserved. The candidate binds NOTHING.
  D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-103, DR-107, DR-110 (register row), DR-111,
  DR-112, DR-120, DR-121, DR-122, DR-124, DR-125, DR-126, or
  DR-127. Does not overturn D-106, D-107, D-108 (packaging
  recording), D-109, D-110, or D-111. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D112.
- **Commit:** C-D112.

---

## D-113 — Record language-quality-matrix-contract.v13 as DR-118's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-113.review-adversarial.claude2.json`,
  `cec0f279ee1228d0ea41a6596d457f2a537db608589d0979d3a6ead21d4dd919`).
  Codex
  (`artifacts/coordinator-decisions.D-113.review-adversarial.codex.json`,
  `e64005b6cfb46fcd07c8371689c695c27fa2edf383bddf123010080987adbb87`).
  Subject `coordinator-decisions.D-113.draft.md`
  `fd629bc2864d80942670c5a22b18b1b0d06fd78abe7cb8604aad6e2848ee9ecf`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112.
- **Subject:** `docs/coop/artifacts/language-quality-matrix-contract.v13.json`
  `9efffdb3f7ec806bc967db5eff5868aea0a7d11524b1e026993a46505d35c2ae`.
- **Verdicts:** Claude 2
  `language-quality-matrix-contract.v13.review-independent.claude2.json`
  `c98f6332292720d67b2109920fee6aec0df56c726f6729635bc4fa5f14b146a3`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-V13-ADV-1 /
  CLAUDE-V13-ADV-2. Codex
  `language-quality-matrix-contract.v13.review-independent.codex.json`
  `ac5cf60ac2a57557168a776cbe1282ce51e5047e6342381d3a6a1313af98e130`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory LQMCV13-A1.
- **Decision:** Record v13 as DR-118's accepted design-contract
  successor candidate. This is coordinator decision D-113, not
  register row DR-113. D-112 remains the adopted secret-storage-v3
  recording and is not retargeted. D-111 remains the adopted
  anti-lockstep-v7 recording. D-110 remains the adopted SDK-v4
  recording. Claude advisories CLAUDE-V13-ADV-1 / CLAUDE-V13-ADV-2
  and Codex advisory LQMCV13-A1 travel as honesty work, as do
  review advisories CLAUDE-D113-A1 and CLAUDE-D113-A2. DR-118 stays
  DECIDED-V1-NOT-INTEGRATED. No SATISFIED. No QUALIFIED. Numeric
  thresholds remain UNDECIDED (D-007). The matrix/corpus is not
  authored. The candidate binds NOTHING. D-056 Class A is not
  opened. D-056 Class B remains ineligible while thresholds are
  UNDECIDED. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-101, DR-103, DR-108, DR-110 (register row),
  DR-111, DR-112, DR-113, DR-120, DR-121, DR-122, DR-124, DR-125,
  DR-126, or DR-127. Does not overturn D-106, D-107, D-108
  (packaging recording), D-109, D-110, D-111, or D-112. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D113.
- **Commit:** C-D113.

---

## D-114 — Record distribution-core-inventory-contract.v16 as DR-101's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-114.review-adversarial.claude2.json`,
  `e87b9301e0c37932eb080195925f424da648f65562334496ce1267c3e6fda7b8`).
  Codex
  (`artifacts/coordinator-decisions.D-114.review-adversarial.codex.json`,
  `516eb8146c8d46ad63705bc6c52e176bccbf74952034db5e836c14e219361f60`).
  Subject `coordinator-decisions.D-114.draft.md`
  `d212fa63586ab0b134d2206b918ca063ddc436afd5b80f60e8389372fe113567`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113.
- **Subject:** `docs/coop/artifacts/distribution-core-inventory-contract.v16.json`
  `429b8c7a9cd5c8f2b495337c055ccbd262e796ba1cc42efb173779c72018fb5b`.
- **Verdicts:** Claude 2
  `distribution-core-inventory-contract.v16.review-independent.claude2.json`
  `81fadf18b33ecd278246f4296a44d77e7aa05091895ef2657cdf6703eff0ada3`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory CLAUDE-V16-A-1. Codex
  `distribution-core-inventory-contract.v16.review-independent.codex.json`
  `02a6f590bdef98f7dff16c9b5b85062bf679e48fb70fdb0e5b7686a111d2ead6`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v16 as DR-101's accepted design-contract
  successor candidate. This is coordinator decision D-114, not
  register row DR-114 and not the contested C4 decision D-101.
  D-113 remains the adopted langqual-v13 recording and is not
  retargeted. D-112 remains the adopted secret-storage-v3
  recording. Claude advisory CLAUDE-V16-A-1 travels as honesty
  work. DR-101 stays leftover-design / OPEN. No SATISFIED. No
  QUALIFIED. The candidate binds NOTHING. D-056 Class A is not
  opened (the contract itself records Class A ineligibility).
  Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-103, DR-108, DR-110 (register row), DR-111,
  DR-112, DR-113, DR-114, DR-118, DR-120, DR-121, DR-122, DR-124,
  DR-125, DR-126, or DR-127. Does not overturn D-106, D-107,
  D-108 (packaging recording), D-109, D-110, D-111, D-112, or
  D-113. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D114.
- **Commit:** C-D114.

---

## D-115 — Record sarif-projection-contract.v15 as DR-122's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-115.turn2.review-adversarial.claude2.json`,
  `b6c913c1f02d089af28a26898d2474900c02953e89a0e8ace9d7dbe8191abf22`).
  Codex
  (`artifacts/coordinator-decisions.D-115.turn2.review-adversarial.codex.json`,
  `2cae9b6afda69e7082539cef12245be945af579af8b3fda92387ff767ca4e843`).
  Subject `coordinator-decisions.D-115.turn2.draft.md`
  `d7bc919c6a5bec77ea335e3059d6f5e85e1dec0b4541a14556dae0b9e9392a76`.
  Turn 1 OBJECT (D115-MF-1) at
  `coordinator-decisions.D-115.review-adversarial.claude2.json`
  `64c5402f450af4b3ce13154786cccd400162bc6580920d0fb43015c663a642da`
  against frozen turn-1 draft
  `c69557fa3cbdde778252eebc9c349b0d8154bb6b66aad95524740272e0cba2af`
  (not retargeted).
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114.
- **Subject:** `docs/coop/artifacts/sarif-projection-contract.v15.json`
  `8996a92d00ddd47d212dbeecaf51f25b77b90d87aaa618cda9ad00749fd1d589`.
- **Verdicts:** Claude 2
  `sarif-projection-contract.v15.review-independent.claude2.json`
  `fe5f55181b305c5cafd3993b672d30296b7d62c7f10dd236585a81bd99aaaad0`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory ADV-1 (qualify
  CLAUDE-V15-ADV-1). Codex
  `sarif-projection-contract.v15.review-independent.codex.json`
  `9f402c72267ed7c92657a1aa38e4c0fc185a25eaf23bb7aad69042dd9dbfad76`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory SARIFV15-A1.
- **Decision:** Record v15 as DR-122's accepted design-contract
  successor candidate. This is coordinator decision D-115, not
  register row DR-115 (thresholds; SATISFIED at D-089). D-114
  remains the adopted inventory-v16 recording and is not
  retargeted. Claude advisories CLAUDE-V15-ADV-1 and SARIFV15-A1
  travel as honesty work, as does review advisory D115-T2-ADV-1.
  DR-122 stays PROPOSED-CLOSED-FOR-REVIEW. No SATISFIED. No
  QUALIFIED. Preview still does not advertise SARIF. G17 stays
  inapplicable. The candidate binds NOTHING. D-056 Class A is not
  opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-101, DR-103, DR-108, DR-110 (register row),
  DR-111, DR-112, DR-113, DR-114, DR-118, DR-120, DR-121, DR-124,
  DR-125, DR-126, or DR-127. Does not overturn D-106, D-107,
  D-108 (packaging recording), D-109, D-110, D-111, D-112, D-113,
  or D-114. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D115.
- **Commit:** C-D115.

---

## D-116 — Record product-boundary-successor-contract.v8 as DR-117's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-116.review-adversarial.claude2.json`,
  `711c2e42cc7ba17059dd6863fa3589cef41a91e9b5d24bee5e5b228f4a8f2175`).
  Codex
  (`artifacts/coordinator-decisions.D-116.review-adversarial.codex.json`,
  `5d0cb0dc7f516ebbf1a3cd887d4d429f665370656c91572c78b4065a50f86e29`).
  Subject `coordinator-decisions.D-116.draft.md`
  `d7d80c176302baea2a72f39e8aca51de903b212f0aece45b2c428361c280abfa`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115. Claude's independent verdict was
  ACCEPT-WITH-ADVISORIES; Codex's was ACCEPT. Both were 0/0.
- **Subject:** `docs/coop/artifacts/product-boundary-successor-contract.v8.json`
  `52c70f7715fb869bae70bc588043dc5b4d731b73408d2d451e868b8de963f362`.
- **Verdicts:** Claude 2
  `product-boundary-successor-contract.v8.review-independent.claude2.json`
  `7e48d2d4f0c5b5305f9427b04ddb60450dccfe51f708fb639078c28e065a0b48`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX, advisories
  PBSCV8-A1 / PBSCV8-A2 (qualify CLAUDE-V8-A1 / CLAUDE-V8-A2).
  Codex
  `product-boundary-successor-contract.v8.review-independent.codex.json`
  `938666820e114972bef8fd431dccfa16cb189d147f8b08b8580acd30bbd5acda`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v8 as DR-117's accepted design-contract
  successor candidate. This is coordinator decision D-116, not
  register row DR-116. D-115 remains the adopted SARIF-v15
  recording and is not retargeted. Claude advisories CLAUDE-V8-A1 /
  CLAUDE-V8-A2 travel as honesty work on a later successor of the
  recorded candidate (D116-CLAUDE-A1), as do review advisories
  D116-CLAUDE-A1 / D116-CLAUDE-A2. Preview exclusion (D-066/D-068)
  is not this row SATISFIED. DR-117 stays OPEN. No SATISFIED. No
  QUALIFIED. The candidate binds NOTHING. D-056 Class A is not
  opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-108, DR-110 (register row), DR-111, DR-112, DR-113, DR-114,
  DR-115, DR-116 (register row), DR-118, DR-120, DR-121, DR-122,
  DR-124, DR-125, DR-126, or DR-127. Does not overturn D-106,
  D-107, D-108 (packaging recording), D-109, D-110, D-111, D-112,
  D-113, D-114, or D-115. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D116.
- **Commit:** C-D116.

---

## D-117 — Record state-class-contract.v11 as DR-124's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-117.review-adversarial.claude2.json`,
  `b5af88462813f990d962a968aa03a4c6a2123e115d7711748b768beb74b4e4d0`).
  Codex
  (`artifacts/coordinator-decisions.D-117.review-adversarial.codex.json`,
  `53683f974e0064ce140575aecdd0652db2729982a03a3a9af4143922ef2ed5dc`).
  Subject `coordinator-decisions.D-117.draft.md`
  `274414aaaaefd9b5553a20fcc8bdd10212277e3e1f07e6b206bd4e3ecefc391f`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116.
- **Subject:** `docs/coop/artifacts/state-class-contract.v11.json`
  `b5456c63e865b53738b1f11f46a898438afca7890a6069a8653aad6ea78d86bb`.
- **Verdicts:** Claude 2
  `state-class-contract.v11.review-independent.claude2.json`
  `c20dc0cc4fd786ef4c5080dee23fe11bd8bfbfa5f963e831efcf39c39dfa3422`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `state-class-contract.v11.review-independent.codex.json`
  `6c40f95aaa0c2e34345942a19662f035368a81a6008a54709a2fe815f2837c75`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v11 as DR-124's accepted design-contract
  successor candidate. This is coordinator decision D-117, not
  register row DR-117. D-116 remains the adopted
  product-boundary-v8 recording and is not retargeted. DR-124
  stays OPEN. No SATISFIED. No QUALIFIED. Grant-journal assignment
  remains a proposed supersession. The candidate binds NOTHING.
  D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not dispose DR-117. Does
  not SATISFY DR-101, DR-103, DR-108, DR-110 (register row),
  DR-111, DR-112, DR-113, DR-114, DR-115, DR-116 (register row),
  DR-118, DR-120, DR-121, DR-122, DR-125, DR-126, or DR-127.
  Does not overturn D-106, D-107, D-108 (packaging recording),
  D-109, D-110, D-111, D-112, D-113, D-114, D-115, or D-116.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D117.
- **Commit:** C-D117.

---

## D-119 — Record replay-purge-contract.v2 as DR-113's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-119.review-adversarial.claude2.json`,
  `443727f522a277ebae49bb623a8b34abdcd40d29ff28fac8f15e8171b4cb513c`)
  CONSENT, advisory D119-CLAUDE-A1. Codex
  (`artifacts/coordinator-decisions.D-119.review-adversarial.codex.json`,
  `e963a252d87362136df707757e6a5426d44356eaf566da5aa42d05c7c2d05979`).
  Subject `coordinator-decisions.D-119.draft.md`
  `ed3a6b83afaf7b21d4075a11e503786188cc32165a2010483b67e083e4772596`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117.
- **Subject:** `docs/coop/artifacts/replay-purge-contract.v2.json`
  `48cb28a5ea3a5609b2b74474a7599a386daeb7c373ec662241d35cd92b6a82e2`.
- **Verdicts:** Claude 2
  `replay-purge-contract.v2.review-independent.claude2.json`
  `20ad538feeeb3b0e695a9e2b5b9030eb451cd5e8f648346812115ff897da9e2e`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-RP2-ADV-1 /
  CLAUDE-RP2-ADV-2. Codex
  `replay-purge-contract.v2.review-independent.codex.json`
  `969c89fb43db9971cef85a37e729f9c92b38f1c512c472e05036c65e0c4b9e51`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v2 as DR-113's accepted design-contract
  successor candidate. This is coordinator decision D-119, not
  register row DR-119 (already SATISFIED at D-091). D-117 remains
  the last prior adopted recording and is not retargeted. D-118
  remains in review and is not retargeted. Claude advisories
  CLAUDE-RP2-ADV-1 / CLAUDE-RP2-ADV-2 travel as honesty work on a
  later successor of the recorded candidate (D119-CLAUDE-A1), as
  does review advisory D119-CLAUDE-A1. DR-113 stays OPEN /
  inherits hard blockers. No SATISFIED. No QUALIFIED. D-002
  defers this row WHOLLY from slice 1. The candidate binds
  NOTHING. D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-109, DR-110 (register row), DR-111, DR-112,
  DR-114, DR-115, DR-116 (register row), DR-117, DR-118, DR-120,
  DR-121, DR-122, DR-124, DR-125, DR-126, or DR-127. Does not
  overturn D-106, D-107, D-108 (packaging recording), D-109,
  D-110, D-111, D-112, D-113, D-114, D-115, D-116, or D-117.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D119.
- **Commit:** C-D119.

---

## D-118 — Record offline-analysis-closure-contract.v3 as DR-106's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-118.turn2.review-adversarial.claude2.json`,
  `9fefb80ad0e26d1f766405ed1d7ee2cd11f93673dca0b96cd2dc15728761fa65`).
  Codex
  (`artifacts/coordinator-decisions.D-118.turn2.review-adversarial.codex.json`,
  `96672f196dd2f96509f89262ddfb9c0daf38a917f3335f0079ce334a487a5e8f`).
  Subject `coordinator-decisions.D-118.turn2.draft.md`
  `1a650db7246dd8ddb425f31a3c32675b6f1aebf6f0c19c169df48e4b78ec5ef5`.
  Turn-1 draft `coordinator-decisions.D-118.draft.md`
  `c3022178928154c02547187f5fdd90e59c29cccab537d698efbaf4a5369bdc4a`
  is not retargeted. Turn 1: Claude 2 CONSENT 0/0
  (`c724dd44fd94c1ac1849cfac96157c325fa9c50fea3a5f3344ba89c3a3596d7e`,
  advisory CLAUDE-D118-A1 / ADV-D118-01); Codex OBJECT
  (`d6271460e98442d7c3da3ff25915ab10cb86f413eb0930d4172ed3e0011470f1`,
  CODEX-D118-M1).
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119.
- **Subject:** `docs/coop/artifacts/offline-analysis-closure-contract.v3.json`
  `f3b094bfabcaa20c0e8c8b5af64f7d9d9a14dda76fbc9606805e6b3f489bec11`.
- **Verdicts:** Claude 2
  `offline-analysis-closure-contract.v3.review-independent.claude2.json`
  `78f71c24e74bbf3b652f9a5acc9c2c4bb79b0c47f2aebd77087920e2b84d9dbb`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX, advisory
  ADV-OACC-V3-01. Codex
  `offline-analysis-closure-contract.v3.review-independent.codex.json`
  `235f4991499870341a88856a6c56b7cd35dc4a8d6d8a250b917beacc4530f350`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories OACV3-A1 / OACV3-A2.
- **Decision:** Record v3 as DR-106's accepted design-contract
  successor candidate. This is coordinator decision D-118, not
  register row DR-118. D-119 remains the last prior adopted
  recording in file order and is not retargeted. D-117 remains
  adopted and is not retargeted. Claude advisories ADV-OACC-V3-01
  and Codex OACV3-A1 / OACV3-A2 travel as honesty work. Turn-1
  advisory CLAUDE-D118-A1 is discharged by the turn-2 remasurement
  and PASS-NO-SCOPE-EFFECT. DR-106 stays OPEN / inherits hard
  blockers. No SATISFIED. No QUALIFIED. D-002 defers this row
  WHOLLY from slice 1. The candidate binds NOTHING. D-056 Class A
  is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-108, DR-109, DR-110 (register row), DR-111, DR-112, DR-113,
  DR-114, DR-115, DR-116 (register row), DR-117, DR-118, DR-120,
  DR-121, DR-122, DR-124, DR-125, DR-126, or DR-127. Does not
  overturn D-106 (corpus recording), D-107, D-108 (packaging
  recording), D-109, D-110, D-111, D-112, D-113, D-114, D-115,
  D-116, D-117, or D-119. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D118.
- **Commit:** C-D118.


---

## D-120 — Record storage-mechanics-contract.v5 as DR-109's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-120.review-adversarial.claude2.json`,
  `09863c6b0aa8d70c0f9b10add8fbfb2a5f7a1f4da7df6dfc81b4166a5a94ebf5`).
  Codex
  (`artifacts/coordinator-decisions.D-120.review-adversarial.codex.json`,
  `992484d2c021f6c156920cbed6e47b7ae7892c28a4e2534bd7cec98a33bb0d0e`).
  Subject `coordinator-decisions.D-120.draft.md`
  `f8f394f189f68a1a1719fd8c10a815631463cb5d2eb48ded913247872d0d25e1`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118.
- **Subject:** `docs/coop/artifacts/storage-mechanics-contract.v5.json`
  `8a43c5b53367a85615648129915d8b19e5b12b2bb32c972f2147093233bd20fb`.
- **Verdicts:** Claude 2
  `storage-mechanics-contract.v5.review-independent.claude2.json`
  `745afe2a19a362ab0fac5da8da5c2410812e3cc3657a16a31bb854f8b42322eb`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory CLAUDE-V5-O-1 (O-1).
  Codex
  `storage-mechanics-contract.v5.review-independent.codex.json`
  `d9a10da282e3e792dfa2dddef3f2084027f61cad76cde28ecd2a18eb695d50fa`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v5 as DR-109's accepted design-contract
  successor candidate. This is coordinator decision D-120, not
  register row DR-120 (packaging; recorded at D-108). D-118 remains
  the last prior adopted recording and is not retargeted. D-119
  remains adopted and is not retargeted. Claude advisory
  CLAUDE-V5-O-1 travels as honesty work. DR-109 stays OPEN /
  inherits hard blockers. No SATISFIED. No QUALIFIED. D-002
  defers this row WHOLLY from slice 1. The candidate binds NOTHING.
  D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-110 (register row), DR-111, DR-112, DR-113,
  DR-114, DR-115, DR-116 (register row), DR-117, DR-118, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. DR-120 is the
  packaging row recorded at D-108 and is not a row this recording
  could SATISFY. Does not overturn D-106 (corpus recording),
  D-107, D-108 (packaging recording), D-109, D-110, D-111, D-112,
  D-113, D-114, D-115, D-116, D-117, D-118, or D-119. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D120.
- **Commit:** C-D120.


---

## D-121 — Record self-update-repair-contract.v3 as DR-110's accepted design-contract successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-121.review-adversarial.claude2.json`,
  `5eff0d39c01f729128dab966fe1c52aecda3fe8c77aed93fa1bb56e8a6712927`).
  Codex
  (`artifacts/coordinator-decisions.D-121.review-adversarial.codex.json`,
  `a38bbe6b68eecef3f9c4331376f71d1a17b81b7544bc6fc501afd375cc36bccc`).
  Subject `coordinator-decisions.D-121.draft.md`
  `846fc351ada6961d95726c8e90667a219d7034b6227bf8d153d2aef740350759`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120.
- **Subject:** `docs/coop/artifacts/self-update-repair-contract.v3.json`
  `73a44c2b07a2b8e8db48497a04557d99d65f91497a717eaf2fdf07fc8008690a`.
- **Verdicts:** Claude 2
  `self-update-repair-contract.v3.review-independent.claude2.json`
  `c4f3cb59c2aacce310f34cf602560850cd2916b52d6142c9e0a00ea91e11df38`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `self-update-repair-contract.v3.review-independent.codex.json`
  `e21b1e33bf2b235367f80bec53cb2ec950b77d27be4988d87c9e441d8cecc8b3`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v3 as DR-110's accepted design-contract
  successor candidate. This is coordinator decision D-121, not
  register row DR-121 (monorepo CI). D-120 remains the last prior
  adopted recording and is not retargeted. D-118 and D-119 remain
  adopted and are not retargeted. DR-110 stays OPEN. No SATISFIED.
  No QUALIFIED. D-002 defers self-update/repair from slice 1
  (fresh signed download). The candidate binds NOTHING. D-056
  Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-109, DR-111, DR-112, DR-113, DR-114, DR-115,
  DR-116 (register row), DR-117, DR-118, DR-120, DR-121, DR-122,
  DR-124, DR-125, DR-126, or DR-127. Does not overturn D-106
  (corpus recording), D-107, D-108 (packaging recording), D-109,
  D-110 (SDK recording), D-111, D-112, D-113, D-114, D-115,
  D-116, D-117, D-118, D-119, or D-120. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D121.
- **Commit:** C-D121.


---

## D-122 — Record third-party-policy-contract.v1 as DR-116's leftover T2-02 candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-122.review-adversarial.claude2.json`,
  `7b52f0044fc5e8d407db57f8b1d510e7346faa0c69a072806cf22121399a7fe3`).
  Codex
  (`artifacts/coordinator-decisions.D-122.review-adversarial.codex.json`,
  `01ed25bd5bc21859e13f0e6c6ab8829657b43b055df5a614252ff2f1158ed7b6`).
  Subject `coordinator-decisions.D-122.draft.md`
  `baeea88264f10eb8cfbdd94226b38656cbbe791ca2db27684fa5657f8a64c9fb`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 / D-121.
- **Subject:** `docs/coop/artifacts/third-party-policy-contract.v1.json`
  `78386c7a386376508d9f44d8a3fbe1388b7c1b78798bceb74ab83002ab3ef442`.
- **Verdicts:** Claude 2
  `third-party-policy-contract.v1.review-independent.claude2.json`
  `dd8f6f7ace90c598e7fff2282c6d31b595a9a0d00fdbca47613f4e24d26a61f0`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories TPP-C2-A1..A4.
  Codex
  `third-party-policy-contract.v1.review-independent.codex.json`
  `dfb773685e08d552eb166620649b3b2b0ab5901f0b6c882e00a6912ea9c930a9`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v1 as DR-116's leftover T2-02 successor
  candidate. This is coordinator decision D-122, not register
  row DR-122 (SARIF; recorded at D-115). D-121 remains the last
  prior adopted recording and is not retargeted. Claude advisories
  TPP-C2-A1..A4 travel as honesty work. DR-116 stays OPEN. No
  SATISFIED. No QUALIFIED. D-002 records "no third-party support
  policy needed yet." The candidate binds NOTHING. D-056 Class A
  is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-109, DR-110, DR-111, DR-112, DR-113, DR-114,
  DR-115, DR-117, DR-118, DR-120, DR-121, DR-122, DR-124, DR-125,
  DR-126, or DR-127. Does not overturn D-106 (corpus recording),
  D-107, D-108, D-109, D-110, D-111, D-112, D-113, D-114, D-115,
  D-116, D-117, D-118, D-119, D-120, or D-121. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D122.
- **Commit:** C-D122.


---

## D-123 — Record identity-namespace-integration-contract.v3 as DR-104 leftover-integration candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-123.review-adversarial.claude2.json`,
  `3e14dfa307340652537d8ca79fc9cc10fef2f0ac865d23045e8b28bb89dff751`).
  Codex
  (`artifacts/coordinator-decisions.D-123.review-adversarial.codex.json`,
  `5e0c0931be03052475e8d0eabca75a12c464e5d2294071c0d34cfc0fb1cbf764`).
  Subject `coordinator-decisions.D-123.draft.md`
  `0d34ae8557011eefdc9252b41fa847f042459f52f8c7b9a48a6b1671c51b045a`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 / D-121 /
  D-122.
- **Subject:** `docs/coop/artifacts/identity-namespace-integration-contract.v3.json`
  `57bf89826c5c4ff6658bbea5f68b0b049abb134cb19001cd670f15cc0ef97091`.
- **Verdicts:** Claude 2
  `identity-namespace-integration-contract.v3.review-independent.claude2.json`
  `881c9df77635090239172fef7d66aae2105ba259b696c26cbc252e78fa4fbfd7`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories INIC-V3-CL-ADV-1 /
  INIC-V3-CL-ADV-2. Codex
  `identity-namespace-integration-contract.v3.review-independent.codex.json`
  `30fb71405a7286dcfcc7fb73eedd8625d91636fbcd9980f902ba80930fbf1332`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v3 as DR-104's leftover-integration T2-02
  successor candidate. This is coordinator decision D-123, not
  register row DR-123 (CLI baseline; SATISFIED at D-092). D-122
  remains the last prior adopted recording and is not retargeted.
  Claude advisories INIC-V3-CL-ADV-1 / INIC-V3-CL-ADV-2 travel as
  honesty work. DR-104 stays DECIDED-V1-NOT-INTEGRATED.
  leftover-design/OPEN is a finding against a recording of this
  row. No SATISFIED. No QUALIFIED. The candidate binds NOTHING.
  D-056 Class A is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-109, DR-110, DR-111, DR-112, DR-113, DR-114,
  DR-115, DR-116, DR-117, DR-118, DR-120, DR-121, DR-122, DR-124,
  DR-125, DR-126, or DR-127. Does not overturn D-012, D-106
  (corpus recording), D-107, D-108, D-109, D-110, D-111, D-112,
  D-113, D-114, D-115, D-116, D-117, D-118, D-119, D-120, D-121,
  or D-122. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D123.
- **Commit:** C-D123.


---

## D-124 — Record monorepo-ci-contract.v16 as DR-121 leftover T2-02 candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-124.review-adversarial.claude2.json`,
  `989e12d614f2fe3364ffc1014f723febe8666fe49ce06ded051b669d706861e5`).
  Codex
  (`artifacts/coordinator-decisions.D-124.review-adversarial.codex.json`,
  `5c5f27564ea14e8c01a5f93b9a0016064bc021434ce6d2efaebbc41737e54dce`).
  Subject `coordinator-decisions.D-124.draft.md`
  `1d8a05aa065f398cf125268cadb5de55e7e0cb451edb3b7da46b5cd8a2cfb541`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 / D-121 /
  D-122 / D-123.
- **Subject:** `docs/coop/artifacts/monorepo-ci-contract.v16.json`
  `67ca501660a2ba515ce37adc799c5418e4ffd156308189662245e5a5e45a2ddb`.
- **Verdicts:** Claude 2
  `monorepo-ci-contract.v16.review-independent.claude2.json`
  `eb4d3942045710c10923c45f001618a9e006fd885ccbdbe0581f9ecf58e7b8d1`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-V16-A1 /
  CLAUDE-V16-A2. Codex
  `monorepo-ci-contract.v16.review-independent.codex.json`
  `b7ba80924a2c0d910edd9428afa93908e64f10c8d45e18ea274019bfb97fe975`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory MCICV16-A1.
- **Decision:** Record v16 as DR-121's leftover T2-02 successor
  candidate. This is coordinator decision D-124, not register
  row DR-124 (state-class; recorded at D-117). D-123 remains the
  last prior adopted recording and is not retargeted. Claude
  advisories CLAUDE-V16-A1 / CLAUDE-V16-A2 and Codex MCICV16-A1
  travel as honesty work. DR-121 stays OPEN. No SATISFIED. G16
  is not QUALIFIED. The candidate binds NOTHING. D-056 Class A
  is not opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-106, DR-108, DR-109, DR-110, DR-111, DR-112, DR-113, DR-114,
  DR-115, DR-116, DR-117, DR-118, DR-120, DR-122, DR-124, DR-125,
  DR-126, or DR-127. Does not overturn D-106 (corpus recording),
  D-107, D-108, D-109, D-110, D-111, D-112, D-113, D-114, D-115,
  D-116, D-117, D-118, D-119, D-120, D-121, D-122, or D-123. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D124.
- **Commit:** C-D124.

---

## D-125 — Record platform-tcb-contract.v45 as DR-126 leftover T2-02 candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-125.review-adversarial.claude2.json`,
  `f539efd66e46b844b01541cdf3c29eebb11e13951509b66d231e2b86f3777b88`).
  Codex
  (`artifacts/coordinator-decisions.D-125.review-adversarial.codex.json`,
  `75821846b72cde74e011f308902e934c96c24a91fe49ca0306fdd985aa58a963`).
  Subject `coordinator-decisions.D-125.draft.md`
  `42a8fae25c636b436c14cf330ad7cefdc420346130f63c3048f0140fe679076f`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-103 / D-104 / D-105 /
  D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 / D-113 /
  D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 / D-121 /
  D-122 / D-123 / D-124.
- **Subject:** `docs/coop/artifacts/platform-tcb-contract.v45.json`
  `da87bdb4d100c90e9450fb82744b7d327ae6b7332db550ea808bdbdb0444a7e5`.
- **Verdicts:** Claude 2
  `platform-tcb-contract.v45.review-independent.claude2.json`
  `9cb3e5ada811b218be7d5f1145d3a81f31f7e87a1b3f13a81834e350f23e710a`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-V45-A1 /
  CLAUDE-V45-A2 / CLAUDE-V45-A3. Codex
  `platform-tcb-contract.v45.review-independent.codex.json`
  `3849abbaf4beed9f8ea822ca7a16e4d2452c05047c76cccd89b09436fc4931b8`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v45 as DR-126's leftover T2-02 successor
  candidate. This is coordinator decision D-125, not register
  row DR-125 (SDK; recorded at D-110). D-124 remains the last
  prior adopted recording and is not retargeted. Claude
  advisories CLAUDE-V45-A1 / CLAUDE-V45-A2 / CLAUDE-V45-A3 and
  Claude D-000 advisory CLAUDE-D125-A1 travel as honesty work.
  DR-126 stays OPEN. No SATISFIED. G22 is not QUALIFIED. The
  candidate binds NOTHING. D-056 Class A is not opened. Does
  not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-106 (corpus recording), D-107, D-108, D-109, D-110, D-111,
  D-112, D-113, D-114, D-115, D-116, D-117, D-118, D-119, D-120,
  D-121, D-122, D-123, or D-124. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D125.
- **Commit:** C-D125.

## D-126 — Record host-effect-authorization.v25 as DR-105 leftover T2-02 successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-126.review-adversarial.claude2.json`,
  `1c414cb7c54c095f870ccbd664fe6580e8ca77cf0eb27f8fab2e978793d03897`).
  Codex
  (`artifacts/coordinator-decisions.D-126.review-adversarial.codex.json`,
  `871976358812a569bbc9759a322c6f253b4a437d196441e2b8f2acbc525e58e0`).
  Subject `coordinator-decisions.D-126.draft.md`
  `ed897fe4adf6f4252701218ea5d357bdd21f7ec7ec98309a8129b43071bbaa74`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125.
- **Subject:** `docs/coop/artifacts/host-effect-authorization.v25.json`
  `b91b9f739b10b1bd30eb56b9d68feac81c483ad86f50e11ed33b95e98ae2d9b9`.
- **Verdicts:** Claude 2
  `host-effect-authorization.v25.review-independent.claude2.json`
  `e7845d03defac1d5eb409899392cde5bdc5a54d74b992a253ca7caaa0c0c1247`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-HEA25-A1 /
  CLAUDE-HEA25-A2 / CLAUDE-HEA25-A3. Codex
  `host-effect-authorization.v25.review-independent.codex.json`
  `09fe6ec87e0172bb57dfee696c5464e89de45863a20a637bc7ce1e557c676e99`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories HAE25-ADV-01 /
  HAE25-ADV-02 / HAE25-ADV-03.
- **Decision:** Record v25 as DR-105's leftover T2-02 successor
  candidate. This is coordinator decision D-126, not register
  row DR-126 (TCB; recorded at D-125). D-125 remains the last
  prior adopted recording and is not retargeted. Recorded v8
  `2cbad561…` remains the D-093 subject and is not retargeted.
  Claude advisories CLAUDE-HEA25-A1 / CLAUDE-HEA25-A2 /
  CLAUDE-HEA25-A3, Codex advisories HAE25-ADV-01 / HAE25-ADV-02 /
  HAE25-ADV-03, and Claude D-000 advisory CLAUDE-D126-A1 travel
  as honesty work. DR-105 stays OPEN. No SATISFIED. G09 is not
  QUALIFIED. The candidate binds NOTHING. D-056 Class A is not
  opened. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-093, D-106 (corpus recording), D-107, D-108, D-109, D-110,
  D-111, D-112, D-113, D-114, D-115, D-116, D-117, D-118, D-119,
  D-120, D-121, D-122, D-123, D-124, or D-125. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D126.
- **Commit:** C-D126.

---

## D-127 — Record doctor-actor-join-integration-contract.v6 as DR-114 leftover-integration T2-02 candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-127.review-adversarial.claude2.json`,
  `4042e819061e04f47ea8ab5e1c73085ee015236018de38fcb0c08c39532e24ff`).
  Codex
  (`artifacts/coordinator-decisions.D-127.review-adversarial.codex.json`,
  `be4fc2dafdfa4b93204de5f34254ecc136628253f9d76e58c2552e29dab9fd76`).
  Subject `coordinator-decisions.D-127.draft.md`
  `3106281419ce9b8e8885db324f0026ab1b3fdcaa9dfbd9a114397fddd80f90f0`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125 / D-126.
- **Subject:** `docs/coop/artifacts/doctor-actor-join-integration-contract.v6.json`
  `f63554d534d249dfdb674be3c78b61bbd1a4a4bdeb56cb06247b24c647ab38d1`.
- **Verdicts:** Claude 2
  `doctor-actor-join-integration-contract.v6.review-independent.claude2.json`
  `1139228d9955827440ffeaaa5db1335bcf30556a2b446d373282b44794c694bc`
  ACCEPT, 0 blockers, 0 SHOULD-FIX. Codex
  `doctor-actor-join-integration-contract.v6.review-independent.codex.json`
  `987da6b6b00537b2b581a5adb52ce25048a978fda20f1f71aaf11d08808d4bc4`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v6 as DR-114's leftover-integration T2-02
  candidate. This is coordinator decision D-127, not register
  row DR-127 (anti-lockstep; recorded at D-111). D-126 remains
  the last prior adopted recording and is not retargeted.
  Doctor-contract.v4 `df2e7175…` remains the D-035 subject and
  is not retargeted. Recorded host-effect v8 `2cbad561…` remains
  the D-093 subject and is not retargeted. Recorded host-effect
  v25 `b91b9f73…` remains the D-126 subject and is not
  retargeted. Claude D-000 advisories CLAUDE-D127-A1 /
  CLAUDE-D127-A2 travel as honesty work. DR-114 stays OPEN. No
  SATISFIED. G09 is not QUALIFIED. The candidate binds NOTHING.
  D-056 Class A is not opened. D-093 and D-126 leftover
  recordings are not FC-C1. CA-1 IN_PROCESS remains
  UNEXERCISABLE in the architecture preview. The later D-000
  CA-2 product/authorization decision is named and not minted.
  Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-032, D-035, D-093, D-106 (corpus recording), D-107, D-108,
  D-109, D-110, D-111, D-112, D-113, D-114, D-115, D-116, D-117,
  D-118, D-119, D-120, D-121, D-122, D-123, D-124, D-125, or
  D-126. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D127.
- **Commit:** C-D127.

---

## D-128 — Record permission-truth-tables.v9 as DR-105 leftover T2-02 successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-128.review-adversarial.claude2.json`,
  `00d4311a5dc53b0b8e29023534df327bddf9a31fa064d62e99b3937d9fe52e2f`).
  Codex
  (`artifacts/coordinator-decisions.D-128.review-adversarial.codex.json`,
  `7cd33a8d2a24f3c750a0ed8a152527ab570918f922dd5d3a69523ab992f03b00`).
  Subject `coordinator-decisions.D-128.draft.md`
  `cf3113494af9a983f255bcd3ad2e46b990fe6a3f0275934d4f012af373710e32`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125 / D-126 / D-127.
- **Subject:** `docs/coop/artifacts/permission-truth-tables.v9.json`
  `05d559647d103a47c18ed5177b71900a1d9dfcdea6b9a1255aefcec5f09eaccb`.
- **Verdicts:** Claude 2
  `permission-truth-tables.v9.review-independent.claude2.json`
  `ed192b68a08bcafbdc3a3f716e2cf1db77b8b2c60fb7bfa7769fe24c4e7c049f`
  ACCEPT-WITH-ADVISORIES, 0 blockers, 0 SHOULD-FIX, advisories
  CLAUDE-V9-ADV-1 / CLAUDE-V9-ADV-2. Codex
  `permission-truth-tables.v9.review-independent.codex.json`
  `cec59dc540adeb6f87068f949970f813ad0abb30f27214522ed3001b79d3c854`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v9 as DR-105's leftover T2-02 successor
  candidate. This is coordinator decision D-128, not register
  row DR-128 (third-party sandbox; deferred post-MVP). D-127
  remains the last prior adopted recording and is not
  retargeted. Permission-truth-tables.v6 `ad1bb75d…` remains
  the D-109 subject and is not retargeted. Permission-truth-
  tables.v2 `cce3afca…` remains the D-042 subject and is not
  retargeted. Claude D-000 advisories CLAUDE-D128-A1 /
  CLAUDE-D128-A2 / CLAUDE-D128-A3 and Claude v9 advisories
  CLAUDE-V9-ADV-1 / CLAUDE-V9-ADV-2 travel as honesty work.
  DR-105 stays OPEN. No SATISFIED. G09 is not QUALIFIED. The
  candidate binds NOTHING. D-056 Class A is not opened. Does
  not record FC-C1, apply host-effect, admit CA-1 IN_PROCESS,
  or mint the later D-000 CA-2 gate. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-032, D-035, D-042, D-093, D-106 (corpus recording), D-107,
  D-108, D-109, D-110, D-111, D-112, D-113, D-114, D-115, D-116,
  D-117, D-118, D-119, D-120, D-121, D-122, D-123, D-124, D-125,
  D-126, or D-127. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D128.
- **Commit:** C-D128.

---

## D-129 — Record doctor-actor-join-integration-contract.v8 as DR-114 leftover-integration T2-02 successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-129.review-adversarial.claude2.json`,
  `9eec1a652132a314c626e4e608e5a175cfdbde45c41aac171acd734d3aa95307`).
  Codex
  (`artifacts/coordinator-decisions.D-129.review-adversarial.codex.json`,
  `bc7cc464d28b4311b98d57261444911e80967daaccc7a7208ba7afee12f985d3`).
  Subject `coordinator-decisions.D-129.draft.md`
  `5168fb1e41370be2ef51475d150a21686a2cb29e5543f7d2168da02e1c023bbe`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125 / D-126 / D-127 / D-128.
- **Subject:** `docs/coop/artifacts/doctor-actor-join-integration-contract.v8.json`
  `c830f954605a4a1d47c5643230439340994a0c42c4a487359541c578d00bc662`.
- **Verdicts:** Claude 2
  `doctor-actor-join-integration-contract.v8.review-independent.claude2.json`
  `8f596a0b89e73f426295d8053f0e4a5b8a4fc37beff5047479ae67a4856cbbbf`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisory CLAUDE-DAJ7-A1.
  Codex
  `doctor-actor-join-integration-contract.v8.review-independent.codex.json`
  `20e9a013dce668f47f18fdf765ba6d1abeba0cc2d66719ab6b6687e079c1c724`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v8 as DR-114's leftover-integration T2-02
  successor candidate. This is coordinator decision D-129, not
  register row DR-129 (optional TUI; deferred). D-128 remains
  the last prior adopted recording and is not retargeted.
  Actor-join v6 `f63554d5…` remains the D-127 subject and is
  not retargeted. Permission-truth-tables.v9 `05d55964…`
  remains the D-128 subject and is not applied. Doctor-
  contract.v4 `df2e7175…` remains the D-035 subject and is not
  retargeted. Recorded host-effect v8 `2cbad561…` remains the
  D-093 subject and is not retargeted. Recorded host-effect
  v25 `b91b9f73…` remains the D-126 subject and is not
  retargeted. Claude advisory CLAUDE-DAJ7-A1 travels as
  honesty work. DR-114 stays OPEN. No SATISFIED. G09 is not
  QUALIFIED. The candidate binds NOTHING. D-056 Class A is
  not opened. Does not record FC-C1, admit CA-1 IN_PROCESS,
  or mint the later D-000 CA-2 gate. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-032, D-035, D-042, D-093, D-106 (corpus recording), D-107,
  D-108, D-109, D-110, D-111, D-112, D-113, D-114, D-115, D-116,
  D-117, D-118, D-119, D-120, D-121, D-122, D-123, D-124, D-125,
  D-126, D-127, or D-128. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D129.
- **Commit:** C-D129.

---

## D-130 — Record identity-namespace-negative-test-corpus.v1 as DR-104 leftover T2-02 successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-130.review-adversarial.claude2.json`,
  `c9fe21ebfa239abb839f09e46592ae806d17d1ce7b97320da43e499c4e529776`).
  Codex
  (`artifacts/coordinator-decisions.D-130.review-adversarial.codex.json`,
  `deb76ff782d3cce7ee6c9804b01691b244d0ba24f5343fb403ee259657b1dd5e`).
  Subject `coordinator-decisions.D-130.draft.md`
  `d983ccdc0df5f153d98dfe45d43840d077f7b35bc2072e9815f4f8dd44a0c1ab`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125 / D-126 / D-127 / D-128 /
  D-129.
- **Subject:** `docs/coop/artifacts/identity-namespace-negative-test-corpus.v1.json`
  `2c0795cd58e95e56afad46899b3c5d546d4fb520e38e1a8c3f7c132aa69583dd`.
- **Verdicts:** Claude 2
  `identity-namespace-negative-test-corpus.v1.review-independent.claude2.json`
  `7c84969cb06d26c01cd8c5de3f0c99908cc2abe274f5b5f33a2d33258e86fbda`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-NTC-V1-ADV-1
  / CLAUDE-NTC-V1-ADV-2. Codex
  `identity-namespace-negative-test-corpus.v1.review-independent.codex.json`
  `8676bac78cbde7415fb9ba3218f5bb1d0efcb0daf716cf37a1f6bfd805e7ed81`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v1 as DR-104's leftover T2-02 successor
  candidate. This is coordinator decision D-130, not register
  row DR-130 (V1→V2 transition; slice 1 claims no upgrade
  continuity). D-129 remains the last prior adopted recording
  and is not retargeted. Identity v3 `57bf8982…` remains the
  D-123 subject and is not retargeted. Corpus v6 `8dfa9346…`
  remains the D-106 subject and is not applied. Claude
  advisories CLAUDE-NTC-V1-ADV-1 / CLAUDE-NTC-V1-ADV-2 and
  Claude D-000 advisories CLAUDE-D130-A1 / CLAUDE-D130-A2
  travel as honesty work. DR-104 stays
  DECIDED-V1-NOT-INTEGRATED. leftover-design/OPEN is a finding
  against a recording of this row. No SATISFIED. The candidate
  binds NOTHING. D-056 Class A is not opened. This recording
  is not a Class B SATISFIED re-record. Does not mutate
  `fixtures/dr-103.v2/` or `fixtures/dr-103.v4/`. Does not
  execute any fixture. Does not edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-012, D-032, D-035, D-042, D-093, D-104 (schemas recording),
  D-106 (corpus recording), D-107, D-108, D-109, D-110, D-111,
  D-112, D-113, D-114, D-115, D-116, D-117, D-118, D-119, D-120,
  D-121, D-122, D-123, D-124, D-125, D-126, D-127, D-128, or
  D-129. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D130.
- **Commit:** C-D130.

---

## D-131 — Record identity-namespace-integration-contract.v4 as DR-104 leftover-integration T2-02 successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-131.review-adversarial.claude2.json`,
  `eec082e84d8382fac3321efe69244985402f466f1d5c054224634df7dc37b0d8`).
  Codex
  (`artifacts/coordinator-decisions.D-131.review-adversarial.codex.json`,
  `64e1c87745d5a58916c5cd183c1d085e08330d9e2614a47cca7083a879045567`).
  Subject `coordinator-decisions.D-131.draft.md`
  `519bd55fcda20663caf6a94acc11865264f5746151720cc9ee288471a4c488bf`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  form as D-013 / D-015 / D-035 / D-042 / D-093 / D-103 / D-104 /
  D-105 / D-106 / D-107 / D-108 / D-109 / D-110 / D-111 / D-112 /
  D-113 / D-114 / D-115 / D-116 / D-117 / D-119 / D-118 / D-120 /
  D-121 / D-122 / D-123 / D-124 / D-125 / D-126 / D-127 / D-128 /
  D-129 / D-130.
- **Subject:** `docs/coop/artifacts/identity-namespace-integration-contract.v4.json`
  `cd7ff948d95cf595ed1b7654c7ea2a458540f417cf13922373fcf8af8b280e62`.
- **Verdicts:** Claude 2
  `identity-namespace-integration-contract.v4.review-independent.claude2.json`
  `6ebf8851855d0bd67efd6b2d44830a84620c4333516b7800868c9485239756a7`
  ACCEPT, 0 blockers, 0 SHOULD-FIX, advisories CLAUDE-INIC-V4-ADV-1
  / CLAUDE-INIC-V4-ADV-2. Codex
  `identity-namespace-integration-contract.v4.review-independent.codex.json`
  `1a700c520716651b23c6818cf7afb7f5e21c818c5f14b680bc79c7c7f8d49f54`
  ACCEPT, 0 blockers, 0 SHOULD-FIX.
- **Decision:** Record v4 as DR-104's leftover-integration T2-02
  successor candidate. This is coordinator decision D-131, not
  a register row (file 08's slice-affecting V2 rows end at
  DR-130). D-130 remains the last prior adopted recording and
  is not retargeted. Identity v3 `57bf8982…` remains the D-123
  subject and is not rewritten. Corpus v1 `2c0795cd…` remains
  the D-130 subject and is not applied. Claude advisories
  CLAUDE-INIC-V4-ADV-1 / CLAUDE-INIC-V4-ADV-2 and Claude D-000
  advisories CLAUDE-D131-ADV-1 / CLAUDE-D131-ADV-2 travel as
  honesty work. DR-104 stays DECIDED-V1-NOT-INTEGRATED.
  leftover-design/OPEN is a finding against a recording of
  this row. No SATISFIED. The candidate binds NOTHING. D-056
  Class A is not opened. This recording is not a Class B
  SATISFIED re-record. Does not execute any fixture. Does not
  edit
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
  Does not mint a D-096 (A) grant. Does not SATISFY DR-101, DR-103,
  DR-104, DR-105, DR-106, DR-108, DR-109, DR-110, DR-111, DR-112,
  DR-113, DR-114, DR-115, DR-116, DR-117, DR-118, DR-120, DR-121,
  DR-122, DR-124, DR-125, DR-126, or DR-127. Does not overturn
  D-012, D-032, D-035, D-042, D-093, D-104 (schemas recording),
  D-106 (corpus recording), D-107, D-108, D-109, D-110, D-111,
  D-112, D-113, D-114, D-115, D-116, D-117, D-118, D-119, D-120,
  D-121, D-122, D-123, D-124, D-125, D-126, D-127, D-128, D-129,
  or D-130. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total. Overturn: C-D131.
- **Commit:** C-D131.

---

## D-132 — User Route C grant: complete the architecture

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Made directly by the user in
  conversation. Same class as D-000 / D-054: the grant is the
  user's decision, recorded verbatim rather than made on their
  behalf. No subagent review of this entry is required. Later
  process acts this grant names still require their own D-000
  cycles.
- **Decision type:** PREFERENCE-LADEN user amendment. Route C
  under D-037 clause 3.
- **Subject:** architecture-completion goal recorded at
  `docs/v2/architecture/12-architecture-completion-goal.md`.
  This is coordinator decision D-132, not register row DR-132
  (no such row is created). File 08's slice-affecting V2 rows
  still end at DR-130 until a later MF-6 act.
- **User words, recorded verbatim (this session, 2026-08-15):**
  1. "i want to set a goal of completing the architecture. you mentioned 5 items as real architecture work. for example: The preview analyze contract is still underspecified as a product promise."
  2. Architecture-complete means "Five gaps plus lawful blueprint".
  3. "Keep D-002 as adopted".
  4. TypeScript component output: "Provider only — recommended".
  5. Parked identities: "Disposition now — reduce the features".
  6. Organization: "New completion checklist".
  7. Section 1 (five new rows join condition 2; one checklist): "Yes — continue".
  8. Section 2 (SATISFIED means a reviewed binding artifact): "Yes — continue".
  9. "note, you can use claude and codex to help when you need concensus. we are using herdr so you should be able to communicate with them. use them to answer questions and not me. between the 3 of you, decide."
  10. "you are the orchestrator and in charge of getting this work completed"
- **Three-agent repair of the five-new-row shape (Claude w5:p1,
  Codex w4:p1, Grok w6:p1):** both independent reviewers
  OBJECTED to five new condition-2 IDs. The adopted venues are
  those in file 12: new DR-131 and DR-133 only; product
  boundary stays DR-117; identity reductions cite D-077/D-078;
  sequence is a D-036 successor, not a row.
- **Decision:** The user is the sole human authority. Completing
  the architecture under D-001, with the five design gaps
  answered and condition 2 still MET, is now live work. This
  grant authorizes **only**:
  1. recording the non-binding goal at file 12;
  2. after D-000 review, a D-056 successor that states the
     SATISFIED-evidence *property* and does not admit
     leftover-design rows by name;
  3. after D-000 review, a scoped D-002 successor that adds
     only DR-131 and DR-133 to the condition-2 affected-row
     set;
  4. after D-000 review, an MF-6 file-08 edit that adds
     DR-131 and DR-133 as `OPEN` and re-measures the snapshot;
  5. after those acts, authoring and D-000 review of DR-133,
     the DR-117 preview successor, DR-131, and a D-036
     successor;
  6. using Claude and Codex under D-000 / Herdr to decide
     remaining questions.
  This grant is **not** a D-096 (A) owner grant. It marks
  nothing `SATISFIED`. It does not edit file 08. It does not
  add register rows. It does not overturn D-056, D-002, D-013,
  D-015, D-077, D-078, D-097, or D-131. It does not authorize
  `docs/v2/implementation/`. Quoted completion is not SATISFIED
  by fiat.
- **Readiness effect:** Zero at this amendment. Condition 2
  stays 4 of 30 SATISFIED. Condition 5 last. File 12 has no
  authority until the named later acts land.
- **Reversibility:** the user may revoke this grant in any
  later message. Overturn: C-D132, plus supersession of any
  later entry that used it. Does not unwrite file 12.
- **Commit:** C-D132.

---

## D-133 — D-056 successor: SATISFIED eligibility is a property

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-133.review-adversarial.claude2.turn3.json`,
  `7bba79e061b23c4f3ea4e4348e70c78d18cd08c592eb69f3392bf3f269692d56`).
  Codex
  (`artifacts/coordinator-decisions.D-133.review-adversarial.codex.turn3.json`,
  `17d9fb1aa2deb225819363c9af2b11a7f268924fcdb7a39b3c380a6db99ad258`).
  Subject `coordinator-decisions.D-133.turn3.draft.md`
  `0fc51c4e9bb0c9b58d9e98e44deb7ae53096c30f89b4aaaee68103c26063081d`.
  Turn-1 Claude OBJECT (D133-MF-1, D133-SF-1) at
  `5d949c9154914cf778d22cb3fa6d2bae816f59b9b340f8ecd8f5476fafb2df7f`;
  turn-1 Codex CONSENT
  `532314f98e5987518dc5793ba2ceee45d78981241014be0cbfeb0ed9282153e8`.
  Turn-2 Claude OBJECT (D133-T2-SF-1) at
  `f79f2077dd0baf19fcc17b97b5f16a5b251b268ce06314762f28d5a0d8870202`;
  turn-2 Codex CONSENT
  `36f7ec6707b26fa48d4d839a639fee5178dc391bb3f06554a71a75d480ce0e2e`.
- **Decision type:** RULE-GOVERNED. Scoped successor amendment
  to the COORD D-056 Decision paragraph's two name-list
  sentences. Those sentences are dated measurements. D-056's
  pinned turn-2 subject `dfb0c2af…` already states eligibility
  as a property; its five gates govern.
- **Decision:** The COORD D-056 Decision paragraph's two
  name-list sentences ("Eligible in kind, not performed:
  DR-102, DR-115, DR-119, DR-123" and "DR-103/104/105/114/118
  and the twelve no-contract rows remain ineligible") are
  dated 2026-08-14 measurements, not the definition of who may
  use the SATISFIED-evidence rule. A later SATISFIED re-record
  may use D-056 only when all five gates in the pinned turn-2
  subject hold for that row at that later cycle. This entry
  marks no row SATISFIED. It does not admit leftover-design
  rows. It does not name DR-131 or DR-133 as eligible today.
  It does not edit file 08. It does not mint a D-096 (A)
  grant. It does not authorize `docs/v2/implementation/`.
  **Owed later work, not performed here:** a later
  recording-hygiene entry must annotate the live COORD D-056
  Decision paragraph with a forward pointer to this entry
  (D133-T2-SF-1).
- **Readiness effect:** Zero. Condition 2 stays 4 of 30
  SATISFIED. Condition 5 last.
- **Reversibility:** Total before any later SATISFIED
  re-record that relies on this clarification for a row that
  was not among the four 2026-08-14 eligible-in-kind
  measurements. Overturn: C-D133. Overturn restores the two
  COORD name-list sentences as definitions. Overturn does not
  unwrite D-085 / D-089 / D-091 / D-092.
- **Commit:** C-D133.

---

## D-134 — Scoped D-002 successor: add DR-131 and DR-133 to the SATISFIED-requiring set

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-134.review-adversarial.claude2.turn2.json`,
  `0b672021441f146ffe5b3f107344c7d66a9e91bff650ea3dc8c13e6793a1a97e`).
  Codex
  (`artifacts/coordinator-decisions.D-134.review-adversarial.codex.turn2.json`,
  `ec3051593bbba52c3cde7790bb489534f7a36d0aaea3ceee8f55ffb2b1ca443a`).
  Subject `coordinator-decisions.D-134.turn2.draft.md`
  `a7b44ff6ff2ed1d87adfb31a6ff20efdf2b7e0d18de43ff0c60003dd065a57bf`.
  Turn-1 Claude OBJECT (D-134-SF-1, D-134-SF-2) at
  `590d9f790231fc76801a64f0f791ed667e97705178a1f03758834bd752857983`;
  turn-1 Codex CONSENT
  `546b59731c219c23027b64eca9aa4573116b6c3e1245d068b3f018ac15381b27`.
- **Decision type:** RULE-GOVERNED. Scoped successor of D-002's
  condition-2 SATISFIED-requiring affected-row set, authorized
  by D-132 clause 3. Does not change the six D-018 item-2 sets.
- **Decision:** D-002's SATISFIED-requiring affected-row set is
  the 21 rows D-002 named plus **DR-131** and **DR-133**
  (cardinality 23). DR-128, DR-129, and DR-130 remain on the
  deferral limb. This entry does not create file-08 rows. A
  later MF-6 act adds the two rows as `OPEN`; until then the
  live snapshot stays 4 of 30. Marks nothing SATISFIED. Does
  not mint a D-096 (A) grant. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 30.
  Condition 5 last. After the later MF-6 act the snapshot
  becomes 4 of 32.
- **Reversibility:** Total before the later MF-6 row-adding
  act. Overturn: C-D134. Overturn restores D-002's pre-D-134
  21-row SATISFIED-requiring set.
- **Commit:** C-D134.

---

## D-135 — File 08 MF-6: add DR-131 and DR-133 as OPEN

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-135.review-adversarial.claude2.turn3.json`,
  `e1129f77eebc48302a87bdf8b83c5de64fd3b34b3958c1996c8895d44e4dc4ea`).
  Codex
  (`artifacts/coordinator-decisions.D-135.review-adversarial.codex.turn3.json`,
  `d52b22dc206081fdde52cd6543969628fb6f086500389b406b97a99b6a5fadd6`).
  Subject `coordinator-decisions.D-135.turn3.draft.md`
  `d22dfd847590c3e50129269b6de69966ec47fb447b5e69eaf123d221d943b276`.
  Turn-1 Claude OBJECT (D-135-SF-1, D-135-SF-2)
  `76c2d0f9c4a4f08e8b1bb52b7a3b892e34a1bf90071eb6bba8b9e3b3ecf0b620`;
  turn-1 Codex OBJECT (D135-SF-1, D135-SF-2)
  `024d8f9b73480e2e7b474da6fee58c94b4138cfc35f98db7f6aa5e38926c93bd`.
  Turn-2 Claude OBJECT (D-135-T2-SF-1)
  `91bb26d37a668e0639cfb4efdc978f9f0c5d1bf464654b8b5ad8321de289fcc6`;
  turn-2 Codex CONSENT
  `85a3a6c8a2e8bf7bde437d2f6f1c868a6bad88bf11c05a6b868cd3703fa79a8e`.
- **Decision type:** RULE-GOVERNED. File-08 content change
  (D-001 MF-6) authorized by D-132 clause 4.
- **Decision:** Insert DR-131 and DR-133 as `OPEN` after
  DR-130. Snapshot heading 2026-08-15; preamble 65 rows
  (12+32+5+16); condition 2 measured 4 of 32 SATISFIED, 24
  OPEN. Neither row is eligible in kind today. Marks nothing
  SATISFIED. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Condition 2 stays NOT MET. Snapshot
  4 of 32. Zero SATISFIED added. Condition 5 last.
- **Reversibility:** Total only before a dependent
  DR-131/DR-133 contract or status re-record. Overturn
  removes the two rows and restores the snapshot heading,
  63-row figure, and 4-of-30 sentences. Overturn: C-D135.
- **Commit:** C-D135.

---

## D-136 — Record provider-only-output-contract.v3 as DR-133 candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-136.review-adversarial.claude2.turn3.json`,
  `313565b135d13ba205f1c26983935d719d9d969f035ff993bd6fe5483bd7f80d`).
  Codex
  (`artifacts/coordinator-decisions.D-136.review-adversarial.codex.turn3.json`,
  `af91a1b1b7444df847160da91bfa990919a7ddd3147dd79e59bf94402b124265`).
  Subject `coordinator-decisions.D-136.turn3.draft.md`
  `0656ac390b3691f83cff0fd31a16160bfa344558bcc86eeb45c7477588c85185`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `provider-only-output-contract.v3.json`
  `ef2a7416700cc8197486c6e29450673c60e3b94512be3ad278d1995f7d281309`.
  Same no-cell-edit branch as D-116 / D-131.
- **Decision:** Record v3 as DR-133's accepted design-contract
  candidate. DR-133 stays OPEN. No SATISFIED. Candidate binds
  NOTHING. D-056 Class A is not opened. Advisories
  CLAUDE-POOC-V3-ADV-1, CLAUDE-POOC-V3-ADV-2, and POOCV3-ADV1
  travel as honesty work (ADV-2 and POOCV3-ADV1 are one class).
  **Owed later MF-6:** update DR-133's "no contract exists"
  clause. Not performed here.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total only before the owed MF-6 or another
  dependent act. Overturn: C-D136.
- **Commit:** C-D136.

---

## D-137 — Record preview-product-boundary-successor.v5 as DR-117's preview-scoped successor candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-137.review-adversarial.claude2.turn2.json`,
  `226991bef0b90b528d0d9ee277b9f04cdb84b79d3264e58706484611fbf7f925`).
  Codex
  (`artifacts/coordinator-decisions.D-137.review-adversarial.codex.turn2.json`,
  `e74082e484e6680a1a3d55c4c1590d36758fc55d34d32d0f749d0329093495a4`).
  Subject `coordinator-decisions.D-137.turn2.draft.md`
  `a0b31bd7c45c205bb163b8177f7efe0b14f398db8b37b187caf1ab8abecdfe5e`.
  Turn-1 Claude OBJECT (CLAUDE-D137-SF1) at
  `53d0d3b169bf7fe1062e9769e2a080142dd4552827c10c5b751402db6e7665ea`;
  turn-1 Codex OBJECT (D137-SF-1, D137-SF-2)
  `1217aa4dbdd083e080f4f9c8cf1763d56d8656a52c76637ea009aaabfc23c093`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-product-boundary-successor.v5.json`
  (0 blockers, 0 SHOULD-FIX from both reviewers). Same
  no-cell-edit branch as D-116 / D-131 / D-136.
- **Subject:** `docs/coop/artifacts/preview-product-boundary-successor.v5.json`
  `5face6a97b311117569044c0214452571e6d3f051e1ab9b38f46abf442ce1262`.
- **Verdicts:** Claude 2
  `preview-product-boundary-successor.v5.review-independent.claude2.json`
  `51289f8efe15123d18f548507090bfa8b6990b94ec491fa2e4b6940b68e23b45`
  ACCEPT, 0/0, advisories CLAUDE-PPBS-V5-ADV-1 /
  CLAUDE-PPBS-V5-ADV-2; standing CLAUDE-PPBS-V3-ADV-1. Codex
  `preview-product-boundary-successor.v5.review-independent.codex.json`
  `ec1517dc4fade8a43dfaa9f1b174be5c6058a326cc203e392d5f9a8673453dd1`
  ACCEPT, 0/0, advisory PPBSV4-ADV-1.
- **Decision:** Record v5 as DR-117's preview-scoped successor
  candidate, authorized by D-132. This is coordinator decision
  D-137, not a register row. DR-117 stays `OPEN`. No
  `SATISFIED`. The candidate binds NOTHING. D-056 Class A is
  not opened. Recording v5 does not make DR-117 D-056-eligible
  in kind on v5 alone: most enforcement classes are
  candidate-owned with no exact DR-G obligation. v8 remains
  the D-116 leftover T2-02 candidate. D-068 remains the owner
  recording of preview.v2 for DR-010. Advisories
  CLAUDE-PPBS-V5-ADV-1, CLAUDE-PPBS-V5-ADV-2, PPBSV4-ADV-1,
  and standing CLAUDE-PPBS-V3-ADV-1 travel as honesty work.
  Does not edit file 08. Does not mint a D-096 (A) grant.
  Does not SATISFY DR-131, DR-133, or any other row. Does not
  overturn D-116, D-068, D-066, or D-136. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total only before a dependent DR-117
  status re-record, SATISFIED-grade application, MF-6 edit,
  or other dependent act lands. After one lands, overturn
  also requires that act's owning-entry supersession or
  revert and reconciliation of every dependent record under
  its own reviewed act. Pre-dependent overturn: C-D137.
- **Commit:** C-D137.

---

## D-138 — Record preview-analyze-contract.v2 as DR-131's accepted design-contract candidate

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-138.review-adversarial.claude2.turn2.json`,
  `31dbf4a513ae3e3e0f526c55d3564dfe3f4f59aa24f8fb6489221ebf91161acd`).
  Codex
  (`artifacts/coordinator-decisions.D-138.review-adversarial.codex.turn2.json`,
  `b14bb0fe3745a29e9d406e9738273cd689384cb1879d08ea6c94bc496b9596e8`).
  Subject `coordinator-decisions.D-138.turn2.draft.md`
  `c609de64c295105ce1b2ea6927137ea1455758bfea15bad4265585fba12efa99`.
  Turn-1 Claude OBJECT (CLAUDE-D138-SF1) at
  `aaf2e5027233d6180554858ac781e3aad51dae7f993e32ff7b5243ca823b8708`;
  turn-1 Codex CONSENT
  `8c08218688fc8f4e5e37e3fe476a1d4de9469ed7bc6217d6f3a5026a51d2bbf7`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-analyze-contract.v2.json` (0 blockers,
  0 SHOULD-FIX from both reviewers). Same no-cell-edit branch
  as D-116 / D-131 / D-136 / D-137.
- **Subject:** `docs/coop/artifacts/preview-analyze-contract.v2.json`
  `081ff7fb529b34a3db3ac9f4c7505848e2253be12b5a867d39b49b3a26d56970`.
- **Verdicts:** Claude 2
  `preview-analyze-contract.v2.review-independent.claude2.json`
  `22a0d892f3051fd007cd7dc26a215e7aa3004f296f99a67aea83bd3035bfd903`
  ACCEPT, 0/0, advisory CLAUDE-PAC-V2-ADV-1. Codex
  `preview-analyze-contract.v2.review-independent.codex.json`
  `e48cb59253f0fe789e5c448ff197d74d3aea745f7eb9f8fbc394077a993a0db1`
  ACCEPT, 0/0, advisory DR131V1-ADV-1.
- **Decision:** Record v2 as DR-131's accepted design-contract
  candidate. This is coordinator decision D-138, not a
  register row. DR-131 stays `OPEN`. No `SATISFIED`. The
  candidate binds NOTHING. D-056 Class A is not opened.
  Recording v2 does not make DR-131 D-056-eligible in kind on
  v2 alone: NT-1..NT-8 assign no owner and no existingGate;
  no DR-G obligation names them. Advisories CLAUDE-PAC-V2-ADV-1
  and DR131V1-ADV-1 travel as honesty work. Does not edit file
  08. Does not mint a D-096 (A) grant. Does not SATISFY
  DR-117, DR-133, or any other row. Does not overturn D-136
  or D-137. Does not authorize `docs/v2/implementation/`.
  **Owed later work, not performed here:** on adoption the
  live DR-131 status-cell clause `no contract exists` becomes
  stale. A later MF-6 act — its own D-000 cycle and commit —
  updates that cell to record this accepted candidate while
  keeping the row OPEN, Class A unopened, and not SATISFIED.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total only before the owed MF-6 or
  another dependent act lands. After one lands, overturn also
  requires that act's owning-entry supersession or revert and
  reconciliation of its dependent file-08 record under its
  own reviewed act. Pre-dependent overturn: C-D138.
- **Commit:** C-D138.

---

## D-139 — D-036 successor: remaining condition-2 sequence

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-139.review-adversarial.claude2.turn2.json`,
  `16aa867c0181f3a3bc286282193f5b58390d837871ba756df6ba0963602a233d`).
  Codex
  (`artifacts/coordinator-decisions.D-139.review-adversarial.codex.turn2.json`,
  `5a77b7b8c3b6a1d9fd797a949bfdac3f58f98159d663146e58fb5c7c6cbea547`).
  Subject `coordinator-decisions.D-139.turn2.draft.md`
  `b5fa22c304b7b33b365f0a49b44ae920bd949b81d1242fff89de384637f854d1`.
  Turn-1 Claude OBJECT (CLAUDE-D139-SF1) at
  `4e699fa03175ef10e12f429d0a67fc00bf907abad51103ce4dca41e03779320b`;
  turn-1 Codex CONSENT
  `ad7e04d24ead8ad063aa42cc482c354d054d140a50934f5885a6e5c5c0051c62`.
- **Decision type:** PREFERENCE-LADEN. Sequencing only.
  Succeeds D-036's remaining node set. Not a register row.
- **Decision:** Remaining condition-2 work is sequenced as
  H (owed hygiene: D-136/D-138 MF-6 cells; D-133 COORD
  pointer), L (already-recorded leftover-design closures,
  drafting only), and W (wait edges that order drafting of
  later SATISFIED cycles and add no eligibility criteria).
  D-056's five gates remain the only SATISFIED eligibility
  test. Condition 2 follows SF-3; condition 4 follows
  D-001/D-002; this entry changes neither. Deferral limb
  DR-128/129/130: no new work. This entry never schedules a
  SATISFIED re-record, never schedules condition 5, and
  never authorizes `docs/v2/implementation/`. Scheduling
  authorizes drafting only. Does not mark SATISFIED. Does
  not open D-056 Class A. Does not edit file 08. Does not
  mint a D-096 (A) grant. Does not change D-002 commands,
  platforms, independent-release, or deferrals.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total before any dependent H or L act
  lands. After one lands, overturn also requires that act's
  owning-entry supersession or revert. Pre-dependent
  overturn: C-D139. Overturn restores D-036's remaining
  node set and does not unwrite D-136 / D-137 / D-138.
- **Commit:** C-D139.

## D-140 — File 08 MF-6: record accepted candidate on DR-133

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-140.review-adversarial.claude2.turn2.json`,
  `711fcdd36c42fcf5907a548214ec924e80968807bc8b6fc52dad89360a45163e`).
  Codex
  (`artifacts/coordinator-decisions.D-140.review-adversarial.codex.turn2.json`,
  `6ebce63b4832beeec714eb3cc35306c3a3ff8d98e5fe7322fa79fdc4e5e8397b`).
  Subject `coordinator-decisions.D-140.turn2.draft.md`
  `c1fdb84871f2cd9704f69eb952af1503a73b49ffa12963f13ddda19a61c9619f`.
  Turn-1 Claude OBJECT (CLAUDE-D140-SF1/SF2) at
  `3ad3c60733ebb8f6da6771a5cab0bd4b0a2a339902230658fc8bc212309a6a01`;
  turn-1 Codex OBJECT (CODEX-D140-MF1)
  `5c0884da3c478c6f6efba8d8df8a415d4ab8abc642afc43c29fa5adc3d6f82df`.
- **Decision type:** RULE-GOVERNED. File-08 MF-6. Performs
  D-139 H1 only.
- **Decision:** Replace DR-133's Status-cell clause
  `no contract exists` with the recorded D-136 candidate in
  the established form (link, full digest,
  `CANDIDATE-NOT-APPLIED`, binds NOTHING). DR-133 stays
  `OPEN`. Not SATISFIED. Class A not opened. H2 / DR-131
  is not performed. Does not change condition-2 arithmetic.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED added. Condition 2
  stays 4 of 32. Condition 5 last.
- **Reversibility:** Total only before a later dependent
  DR-133 cell rewrite or SATISFIED-grade application.
  Overturn restores the DR-133 `no contract exists` clause.
  Does not touch DR-131. Overturn: C-D140.
- **Commit:** C-D140.

## D-141 — File 08 MF-6: record accepted candidate on DR-131

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-141.review-adversarial.claude2.json`,
  `e6db906a2be7bc874e173f22b2b8d4b468e748671e941cc4b802ad0f7206ecf4`).
  Codex
  (`artifacts/coordinator-decisions.D-141.review-adversarial.codex.json`,
  `6a5f527747afa42422963903caa0f46d71de6679497d01fb7ab1e9e1a92349ed`).
  Subject `coordinator-decisions.D-141.draft.md`
  `956d2d37d8a23d2772d01ab655ba60cd9905e9dd5a669656bc6b9d0700c2e102`.
- **Decision type:** RULE-GOVERNED. File-08 MF-6. Performs
  D-139 H2 only.
- **Decision:** Replace DR-131's Status-cell clause
  `no contract exists` with the recorded D-138 candidate in
  the established form (link, full digest,
  `CANDIDATE-NOT-APPLIED`, binds NOTHING). DR-131 stays
  `OPEN`. Not SATISFIED. Class A not opened. Does not edit
  DR-133. Does not change condition-2 arithmetic. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED added. Condition 2
  stays 4 of 32. Condition 5 last.
- **Reversibility:** Total only before a later dependent
  DR-131 cell rewrite or SATISFIED-grade application.
  Overturn restores the DR-131 `no contract exists` clause.
  Does not touch DR-133. Overturn: C-D141.
- **Commit:** C-D141.

## D-142 — COORD hygiene: D-056 Decision paragraph forward pointer

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-142.review-adversarial.claude2.json`,
  `3d3219eca99bc8c206dc42a10cb27f368f3d7d6387ef1789b7067c2c22ba0ae3`).
  Codex
  (`artifacts/coordinator-decisions.D-142.review-adversarial.codex.json`,
  `c35d99fed2bcae5bc2a027304c335bf24d3b741d0a4ebb22491774e84612c3c3`).
  Subject `coordinator-decisions.D-142.draft.md`
  `330ff320c270e48fc8cde3de85682480af0bd6d61d6866d91c7cb786a00cf842`.
- **Decision type:** RULE-GOVERNED. Recording-hygiene.
  Performs D-139 H3 / D133-T2-SF-1 only.
- **Decision:** Insert one forward-pointer sentence after the
  D-056 Decision paragraph's two name-list sentences:
  those sentences are dated 2026-08-14 measurements, not
  the definition of eligibility; D-133 holds the five
  gates of the pinned D-056 turn-2 subject as the
  definition. The two name-list sentences are not rewritten.
  Marks nothing SATISFIED. Opens no Class A. Admits no
  leftover-design row. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total before a later SATISFIED
  re-record that relies on D-133 for a row that was not
  among the four 2026-08-14 eligible-in-kind measurements.
  Overturn removes the inserted forward-pointer sentence.
  Does not unwrite D-133, D-085, D-089, D-091, or D-092.
  Overturn: C-D142.
- **Commit:** C-D142.

## D-144 — Record provider-only-nt-gate-join.v6 as DR-133 leftover-design measurement

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-144.review-adversarial.claude2.turn2.json`,
  `0f9d56d28da0a18eea3d21aaa190f65f9dbfb59fa35211611e45dbec8c4dc087`).
  Codex
  (`artifacts/coordinator-decisions.D-144.review-adversarial.codex.turn2.json`,
  `400c941757db8e60b2c6774b255af39540af34749318972df9e8b50f49033e55`).
  Subject `coordinator-decisions.D-144.turn2.draft.md`
  `b60191b5876e64339ca11d5fe681bf8d91bd8a64cfde0a29eeecde71c5811caa`.
  Turn-1 Claude OBJECT (CLAUDE-D144-SF1/SF2) at
  `25483934f23b43f86cabde81e54e03a2b16d1a4a71fca5e9317f8210ce92785c`;
  turn-1 Codex OBJECT (D144-SF-1)
  `b7032528ee232a5a142e1b76da2e0bd2ffb03080a961964623f1c2543010cd61`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `provider-only-nt-gate-join.v6.json`
  `93bc62d43751d8037aa2a696209eccbdee0ae3b3f11292d9a05be2bc245082a3`.
  Same no-cell-edit branch as D-136 / D-138.
- **Decision:** Record v6 as DR-133 leftover-design
  measurement. The candidate binds NOTHING. DR-133 stays
  `OPEN`. Leftover-design is not closed. Class A is not
  opened. Gates 2 and 3 do not hold. NT-1/2/4/6/7 are
  capable-of-riding G20/G21 after a later D-086 successor
  names them. NT-3 and NT-5 remain leftover-design.
  **Owed later work, not performed here:** a D-086 successor
  names the riding NT classes at G20/G21. D-143.join is
  withdrawn. The unused D-143 G23 draft is unadopted.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero. Condition 2 stays 4 of 32.
  Condition 5 last.
- **Reversibility:** Total only before a later dependent
  D-086 successor or SATISFIED cycle. Overturn: C-D144.
- **Commit:** C-D144.

## D-145 — Record gate-harness-naming.v6 as D-086 successor

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-145.review-adversarial.claude2.turn2.json`,
  `012e369a6c911e5d99047de98297765b92b7bec666eccc6d939401eaa7c34e9f`).
  Codex
  (`artifacts/coordinator-decisions.D-145.review-adversarial.codex.turn2.json`,
  `3e4f074a2183e36a3b92c6822d5040b461a140d99798cae1e2db17b6c7259fce`).
  Subject `coordinator-decisions.D-145.turn2.draft.md`
  `c3c430d48ca3b7f8286324a1ae3358dfde0e1571436beb38ce90d10f16ef84eb`.
  Turn-1 Claude OBJECT (CLAUDE-D145-SF1) at
  `84b013022cd3bcb82ed495aa13d09ac80acb927c3d5a1b82f7eea31641ce741d`;
  turn-1 Codex CONSENT
  `7582d81adda6abe0a7722be90b9bbe45ced8eafe78dccf028a030084544588eb`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `gate-harness-naming.v6.json` as the D-086
  successor owed by D-144.
- **Subject:** `docs/coop/artifacts/gate-harness-naming.v6.json`
  `b74e30092cf1f5aad55434d2f12465fa31111923c1b2c0c5ddc8a78445b5ffba`.
- **Decision:** Record v6 as the condition-4 naming
  candidate. Naming is not execution. Not QUALIFIED.
  DR-G21 names DR-133 NT-1, NT-2, NT-6. DR-G20 names
  DR-133 NT-4, NT-7. DR-133 stays OPEN. Leftover-design
  is not closed. NT-3 and NT-5 remain leftover-design.
  D-056 gates 2 and 3 do not hold. Condition-4 effect is
  zero. Does not edit file 08. Does not add a DR-G* row.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half.
  Condition 5 last.
- **Reversibility:** Total only before a dependent leftover
  closure, SATISFIED cycle, or file-08 harness-cell rewrite.
  Overturn: C-D145.
- **Commit:** C-D145.

## D-146 — Record provider-only-admission-leftover.v1 as DR-133 NT-3/NT-5 leftover-design measurement

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-146.review-adversarial.claude2.json`,
  `42319e2041a782a891f50a92d09e411560e1c6d5b51e6217f8f282a3587c0a04`)
  CONSENT, advisory CLAUDE-D146-ADV1. Codex
  (`artifacts/coordinator-decisions.D-146.review-adversarial.codex.json`,
  `a9ac0b185ca653c051b0b4625c4ad3828304e9c101e3ffe26014a2fb8313c09c`)
  CONSENT, 0 advisories. Subject
  `coordinator-decisions.D-146.draft.md`
  `6c720e030b5436cca74e2c0ac7564d96e8fd2d5ff7b9c4e4fa415c5c32ccc2d2`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `provider-only-admission-leftover.v1.json`
  `eae27692b4d799df2bd6b2d16497b0cbe3378166b6b541bc77df1989b3181865`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-144.
- **Subject:** `docs/coop/artifacts/provider-only-admission-leftover.v1.json`
  `eae27692b4d799df2bd6b2d16497b0cbe3378166b6b541bc77df1989b3181865`.
- **Decision:** Record v1 as DR-133 leftover-design
  measurement for NT-3 and NT-5. The candidate binds
  NOTHING. DR-133 stays `OPEN`. Leftover-design is not
  closed. NT-3 and NT-5 remain leftover-design. D-056
  Class A is not opened. Gates 2 and 3 do not hold. The
  proposed DR-G23 identifier is candidate-not-adopted.
  This entry does not add a DR-G* row and does not change
  required-now 18. **Proposed later work, not performed
  here:** a later D-000 MF-6, its own cycle, may add one
  DR-G* row with owner Protocol + semantic owners whose
  corpus is hostile-but-well-formed admission inputs
  covering NT-3 and NT-5; that later act assigns or remints
  the number and is a scoped D-002 / D-086 required-now
  successor if it adds the row to the required-now set.
  Advisories CLAUDE-PONAL-V1-ADV1, PAL-V1-A1, and
  CLAUDE-D146-ADV1 travel as honesty work. Does not edit
  file 08. Does not retarget D-145. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 5 last.
- **Reversibility:** Total only before a later dependent
  MF-6, leftover rewrite, or SATISFIED cycle. Overturn:
  C-D146. Does not unwrite D-136, D-144, or D-145.
- **Commit:** C-D146.

## D-147 — Add DR-G23 as required-now well-formed admission obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-147.review-adversarial.claude2.turn2.json`,
  `7a1c67a35dd18029447cfd17ba362ad72169756c18663706fe43f370b21af6ae`).
  Codex
  (`artifacts/coordinator-decisions.D-147.review-adversarial.codex.turn2.json`,
  `364099d7af97baccecb950283a19200610ef6ac55f13aa4ff5109f44250c33cf`).
  Subject `coordinator-decisions.D-147.turn2.draft.md`
  `0ce41a67e2abb3eb34eac7fca0a125d12c5beb2f89eab07bb25ad28c79c025f8`.
  Turn-1 Claude OBJECT (CLAUDE-D147-MF1) at
  `15f382ef54b30cdf8d4dda9cca607d6ff6423829a88541c7ba793a7c8d032baa`;
  turn-1 Codex OBJECT (D147-SF-1)
  `074ae263b66830ca49f0696dcd15470688794a4b5536bb24602b44b932c21a50`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act.
- **Decision:** Assign `DR-G23 PROVIDER-WELL-FORMED-ADMISSION`.
  It owns DR-133 NT-3 and NT-5 only. Required-now becomes
  the prior 18-member set plus G23 (cardinality 19). Harness
  identifier
  `harness.DR-G23.provider-well-formed-admission.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G23 row and the condition-4 measured
  cell becomes 23 of 23 owners / 19 of 19 required names /
  20 OPEN, 3 HARD-BLOCKED. NT-3 and NT-5 leftover-design
  closes: remainder is G23 execution. After this act,
  D-056 Eligibility gates 2 and 3 hold for all seven
  DR-133 NT classes. Class A is not opened. Gate 1's
  application-grade / no-express-reservation limb is not
  established here. Gate 4 reserves eligibility to a later
  dedicated SATISFIED-GRADE cycle. CANDIDATE-NOT-APPLIED
  is not a Class A bar (D-085). Not eligible in kind. Not
  SATISFIED. D-145 naming of NT-1/2/4/6/7 stands. Does not
  change D-002 commands, platforms, deferrals, identity
  rides, or the SATISFIED-requiring row set. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (19 of 19). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D147, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  18-member required-now set. Does not unwrite D-136,
  D-144, D-145, or D-146.
- **Commit:** C-D147.

## D-148 — Record preview-analyze-nt-gate-join.v2 as DR-131 leftover-design measurement

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-148.review-adversarial.claude2.json`,
  `538858e7f8cefab6fc7a2372ace03ef111ff36610fea8bf79a99ee448aa1f8e2`).
  Codex
  (`artifacts/coordinator-decisions.D-148.review-adversarial.codex.json`,
  `76497a73678802425b75daf6829548ceeca024260ad20de0524449d14d76e1b2`).
  Subject `coordinator-decisions.D-148.draft.md`
  `221e3dcec81f7bcbbae9ec1b167e462006ec0c3fb453af465d1fbfabeb7d239d`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-analyze-nt-gate-join.v2.json`
  `4081c7400b3b9eae61089bb807140b4f75f5dd512b664c1f6657553a7da03813`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-144 / D-146.
- **Subject:** `docs/coop/artifacts/preview-analyze-nt-gate-join.v2.json`
  `4081c7400b3b9eae61089bb807140b4f75f5dd512b664c1f6657553a7da03813`.
- **Decision:** Record v2 as DR-131 leftover-design
  measurement. The candidate binds NOTHING. DR-131 stays
  `OPEN`. Leftover-design is not closed. NT-1, NT-2, NT-3,
  NT-5, NT-6, NT-7, and NT-8 remain leftover-design. NT-4
  is not leftover-design: its pass is already named as
  DR-133 execution at G21 (D-145) and G23 (D-147). This
  entry does not name DR-131 NT-4 at those gates. Class A
  is not opened. Gates 2 and 3 do not hold. Required-now
  stays 19. **Proposed later work, not performed here:** a
  later D-000 cycle may close the seven leftover classes
  by naming them at one or more condition-4 / DR-G*
  obligations. Does not edit file 08. Does not retarget
  D-145 or D-147. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (19 of 19). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, or SATISFIED cycle.
  Overturn: C-D148. Does not unwrite D-138, D-145, D-146,
  or D-147.
- **Commit:** C-D148.

## D-149 — Record preview-analyze-admission-leftover.v1 as DR-131 leftover grouping

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-149.review-adversarial.claude2.json`,
  `9b5a2d9f2979418bc107448e82673cf0da83206d2b49612dc4ced7184bd9fb01`).
  Codex
  (`artifacts/coordinator-decisions.D-149.review-adversarial.codex.json`,
  `3032163fc0f912dc9ec2c72a500d6800cb8b03cab444adad76fea773ac34b574`).
  Subject `coordinator-decisions.D-149.draft.md`
  `018e0055f0fa75293f1a146351354a6b8ac00955af9703c596c0650437e81014`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-analyze-admission-leftover.v1.json`
  `1222501032917790832a3ffa8f3953ceb7a73907942a5ea30442346bf59935a5`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-146 / D-148.
- **Subject:** `docs/coop/artifacts/preview-analyze-admission-leftover.v1.json`
  `1222501032917790832a3ffa8f3953ceb7a73907942a5ea30442346bf59935a5`.
- **Decision:** Record v1 as DR-131 leftover-design grouping
  for NT-1, NT-2, NT-3, NT-5, NT-6, NT-7, and NT-8. The
  candidate binds NOTHING. DR-131 stays `OPEN`. Leftover-
  design is not closed. Those seven classes remain leftover-
  design. NT-4 standing from D-148 is not retargeted. The
  five proposed kinds are candidate-not-adopted. This entry
  does not add a DR-G* row, does not assign G24 or any later
  identifier, and does not change required-now 19. Class A
  is not opened. Gates 2 and 3 do not hold. **Proposed later
  work, not performed here:** later D-000 MF-6 cycles may
  add one or more DR-G* rows matching those kinds. Does not
  restore G17. Does not invent a D9 code. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (19 of 19). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, MF-6, or SATISFIED cycle. Overturn:
  C-D149. Does not unwrite D-138, D-147, or D-148.
- **Commit:** C-D149.

## D-150 — Add DR-G24 as required-now preview-analyze admission obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-150.review-adversarial.claude2.json`,
  `bc2537cb7a28290270f8fed140b5070432e84b36e54a923a07af2aa67d2a70fc`).
  Codex
  (`artifacts/coordinator-decisions.D-150.review-adversarial.codex.json`,
  `7ebbcc3e44cd95da84e05b55d23b7a05b5059768009d8b9ab81a69faae5e71f9`).
  Subject `coordinator-decisions.D-150.draft.md`
  `2bdb995bddf5e5170c4e1eb4cc2635609be70eb36ab0f118a100f246e6294298`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. First of
  D-149's five proposed later works.
- **Decision:** Assign `DR-G24 PREVIEW-ANALYZE-WELL-FORMED-ADMISSION`.
  It owns DR-131 NT-1 and NT-2 only. Required-now becomes
  the prior 19-member set plus G24 (cardinality 20). Harness
  identifier
  `harness.DR-G24.preview-analyze-well-formed-admission.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G24 row and the condition-4 measured
  cell becomes 24 of 24 owners / 20 of 20 required names /
  21 OPEN, 3 HARD-BLOCKED. NT-1 and NT-2 leftover-design
  closes: remainder is G24 execution. NT-3, NT-5, NT-6,
  NT-7, and NT-8 remain leftover-design. NT-4 standing from
  D-148 is not retargeted. Gates 2 and 3 do not hold for
  DR-131. Class A is not opened. Not eligible in kind. Not
  SATISFIED. Does not restore G17. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (20 of 20). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D150, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  19-member required-now set. Does not unwrite D-138,
  D-147, D-148, or D-149.
- **Commit:** C-D150.

## D-151 — Add DR-G25 as required-now preview-analyze missing-rung obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-151.review-adversarial.claude2.json`,
  `305173ca1fdc44ae177a1a52517bbc9f4631276952d7b8e6af29569fe1d3e67e`).
  Codex
  (`artifacts/coordinator-decisions.D-151.review-adversarial.codex.json`,
  `1efb1d55b1eafc67e520b2459e7254af13376a5324fa6480309b05dda43df341`).
  Subject `coordinator-decisions.D-151.draft.md`
  `b119f983fda9d5092f9c1c45e24f8b22c75de00818f0fa3300ecf46ee9dbbf63`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Second of
  D-149's five proposed later works.
- **Decision:** Assign `DR-G25 PREVIEW-ANALYZE-MISSING-RUNG`.
  It owns DR-131 NT-3 only. Required-now becomes the prior
  20-member set plus G25 (cardinality 21). Harness identifier
  `harness.DR-G25.preview-analyze-missing-rung.preview` is
  named in the same act. Not authored. Not QUALIFIED. File
  08 gains the G25 row and the condition-4 measured cell
  becomes 25 of 25 owners / 21 of 21 required names / 22
  OPEN, 3 HARD-BLOCKED. NT-3 leftover-design closes:
  remainder is G25 execution. NT-5, NT-6, NT-7, and NT-8
  remain leftover-design. Gates 2 and 3 do not hold for
  DR-131. Class A is not opened. Not eligible in kind. Not
  SATISFIED. Does not restore G17. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (21 of 21). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D151, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  20-member required-now set. Does not unwrite D-138,
  D-147, D-148, D-149, or D-150.
- **Commit:** C-D151.

## D-152 — Add DR-G26 as required-now preview-analyze SARIF-not-advertised obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-152.review-adversarial.claude2.json`,
  `4ff33708d4f2a9d4f3a2e4c7f0ae9c6748f125d87f7df9fe98daec8568b136af`).
  Codex
  (`artifacts/coordinator-decisions.D-152.review-adversarial.codex.json`,
  `cdfcb14c039454df27072a4610b225264fee42d7938546259f7cd7c9475ac177`).
  Subject `coordinator-decisions.D-152.draft.md`
  `7c36b624ee98dca68813d344a6b596f774762cb46e3cd3784c21aeb5e24ba807`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Third of
  D-149's five proposed later works.
- **Decision:** Assign
  `DR-G26 PREVIEW-ANALYZE-SARIF-NOT-ADVERTISED`. It owns
  DR-131 NT-5 only. Required-now becomes the prior 21-member
  set plus G26 (cardinality 22). Harness identifier
  `harness.DR-G26.preview-analyze-sarif-not-advertised.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G26 row and the condition-4 measured
  cell becomes 26 of 26 owners / 22 of 22 required names /
  23 OPEN, 3 HARD-BLOCKED. NT-5 leftover-design closes:
  remainder is G26 execution. NT-6, NT-7, and NT-8 remain
  leftover-design. G17 remains inapplicable. Gates 2 and 3
  do not hold for DR-131. Class A is not opened. Not
  eligible in kind. Not SATISFIED. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (22 of 22). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D152, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  21-member required-now set. Does not unwrite D-138,
  D-147, D-149, D-150, or D-151.
- **Commit:** C-D152.

## D-153 — Add DR-G27 as required-now preview-analyze not-sealed-Run obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-153.review-adversarial.claude2.json`,
  `645c795f193a5e10feff943238372c2588689a06ef28c2ac9424bf31e3bdf8a5`).
  Codex
  (`artifacts/coordinator-decisions.D-153.review-adversarial.codex.json`,
  `bbf2dd4bdca302e40f47ec54696f0ddf05852cfa4e8d94d8d954e31887109c18`).
  Subject `coordinator-decisions.D-153.draft.md`
  `d98bdf3160234314dab0a87108b2c271753ee59fab66e9a629e0fa42f69bddff`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Fourth of
  D-149's five proposed later works.
- **Decision:** Assign `DR-G27 PREVIEW-ANALYZE-NOT-SEALED-RUN`.
  It owns DR-131 NT-6 only. Required-now becomes the prior
  22-member set plus G27 (cardinality 23). Harness identifier
  `harness.DR-G27.preview-analyze-not-sealed-run.preview` is
  named in the same act. Not authored. Not QUALIFIED. File
  08 gains the G27 row and the condition-4 measured cell
  becomes 27 of 27 owners / 23 of 23 required names / 24
  OPEN, 3 HARD-BLOCKED. NT-6 leftover-design closes:
  remainder is G27 execution. NT-7 and NT-8 remain leftover-
  design. Gates 2 and 3 do not hold for DR-131. Class A is
  not opened. Not eligible in kind. Not SATISFIED. Does not
  invent a D9 code. Does not restore G17. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (23 of 23). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D153, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  22-member required-now set. Does not unwrite D-138,
  D-147, D-149, D-150, D-151, or D-152.
- **Commit:** C-D153.

## D-154 — Add DR-G28 as required-now preview-analyze host-must-not-mint obligation

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-154.review-adversarial.claude2.json`,
  `d0db0c19cf801118f2ec3c2a5c554526f7dd13109c2bd60104aa7ad1ae492c0c`).
  Codex
  (`artifacts/coordinator-decisions.D-154.review-adversarial.codex.json`,
  `bfd49f3beac630a91fa68d029eb61c29df494d23c5a7791568e2fabaab1495ae`).
  Subject `coordinator-decisions.D-154.draft.md`
  `90a56a37e3285cba5ada20d5375d1058c12fc727502abbbd9d54d84b94d06064`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Fifth of
  D-149's five proposed later works.
- **Decision:** Assign
  `DR-G28 PREVIEW-ANALYZE-HOST-MUST-NOT-MINT`. It owns
  DR-131 NT-7 and NT-8 only. Required-now becomes the prior
  23-member set plus G28 (cardinality 24). Harness identifier
  `harness.DR-G28.preview-analyze-host-must-not-mint.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G28 row and the condition-4 measured
  cell becomes 28 of 28 owners / 24 of 24 required names /
  25 OPEN, 3 HARD-BLOCKED. NT-7 and NT-8 leftover-design
  closes: remainder is G28 execution. After this act, D-056
  Eligibility gates 2 and 3 hold for DR-131's eight NT
  classes. Class A is not opened. Gate 4 reserves
  eligibility to a later SATISFIED-GRADE cycle. Not eligible
  in kind. Not SATISFIED. Invents no D9 code. Does not
  restore G17. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (24 of 24). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D154, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  23-member required-now set. Does not unwrite D-138,
  D-147, D-149, D-150, D-151, D-152, or D-153.
- **Commit:** C-D154.

## D-155 — Record preview-product-boundary-ee-gate-join.v1 as DR-117 leftover-design measurement

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-155.review-adversarial.claude2.json`,
  `6435aaa5a8e7c7f1fc351acbd01890698c4b79579859d9a98d8ed043ce2fa14f`).
  Codex
  (`artifacts/coordinator-decisions.D-155.review-adversarial.codex.json`,
  `c71d32524b1466ce2173108d0b15f3fc347adca45d0b02f206f4111f2d05dd0f`).
  Subject `coordinator-decisions.D-155.draft.md`
  `e40fc2eb20547c5deeed81737a91a4d7fbc2173e418ab8fe0fab6caefa285d18`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-product-boundary-ee-gate-join.v1.json`
  `ae20b25fcb908a19fcd38dbb8e7c5963eee983b566132936c4bd1e7af34b3de0`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-148.
- **Subject:** `docs/coop/artifacts/preview-product-boundary-ee-gate-join.v1.json`
  `ae20b25fcb908a19fcd38dbb8e7c5963eee983b566132936c4bd1e7af34b3de0`.
- **Decision:** Record v1 as DR-117 leftover-design
  measurement. The candidate binds NOTHING. DR-117 stays
  `OPEN`. Leftover-design is not closed. EE-1, EE-2, EE-3b,
  EE-4, EE-5a, EE-5b, EE-6a, EE-7a, EE-7b, and EE-7d remain
  leftover-design. EE-3a is discharged by named DR-133
  classes. EE-6b / EE-7c / EE-7e are capable-of-riding
  G09 / G14 / G16 and are not named here. Class A is not
  opened. Gates 2 and 3 do not hold. Required-now stays 24.
  Advisory CLAUDE-PPBEEJ-V1-ADV1 travels as honesty work.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (24 of 24). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, or SATISFIED cycle.
  Overturn: C-D155. Does not unwrite D-137 or D-154.
- **Commit:** C-D155.

## D-156 — Record preview-product-boundary-admission-leftover.v1 as DR-117 leftover grouping

- **Date:** 2026-08-15
- **Status:** **ADOPTED 2026-08-15.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-156.review-adversarial.claude2.json`,
  `0594cd427b7b357505bb489fc46c7b7ec7f9d14c8956b9922cd8d5d19f27cce7`)
  CONSENT, advisory CLAUDE-D156-ADV1. Codex
  (`artifacts/coordinator-decisions.D-156.review-adversarial.codex.json`,
  `85a0578043d311d77ada18a0e1ebbb2272ed5040bdca978f802e14028598debc`)
  CONSENT. Subject `coordinator-decisions.D-156.draft.md`
  `9c6c75c58b8b8e6c932a59ec78a4bd3e0c1ed52f47532ac97844be1690fd3ef0`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-product-boundary-admission-leftover.v1.json`
  `6280d64867433a963a4ce0bcc44521c57c485b0eea19404b4740c36c94ef4cce`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-149.
- **Subject:** `docs/coop/artifacts/preview-product-boundary-admission-leftover.v1.json`
  `6280d64867433a963a4ce0bcc44521c57c485b0eea19404b4740c36c94ef4cce`.
- **Decision:** Record v1 as DR-117 leftover-design grouping
  for EE-1, EE-2, EE-3b, EE-4, EE-5a, EE-5b, EE-6a, EE-7a,
  EE-7b, and EE-7d. The candidate binds NOTHING. DR-117
  stays `OPEN`. Leftover-design is not closed. Those ten
  classes remain leftover-design. EE-3a and EE-6b/EE-7c/
  EE-7e standing from D-155 is not retargeted. The two
  proposed kinds are candidate-not-adopted. This entry
  does not add a DR-G* row, does not assign G29 or any
  later identifier, and does not change required-now 24.
  Class A is not opened. Gates 2 and 3 do not hold.
  **Proposed later work, not performed here:** later D-000
  MF-6 cycles may add one or more DR-G* rows matching those
  kinds; each such act is a scoped D-002 condition-4
  required-gate-set successor and a D-086 successor in the
  same act, if it adds a row to the required-now set
  (CLAUDE-D156-ADV1). A later D-086 successor may name
  EE-6b/EE-7c/EE-7e at G09/G14/G16. Advisories
  CLAUDE-PPBAL-V1-ADV1 and CLAUDE-D156-ADV1 travel as
  honesty work. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (24 of 24). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, MF-6, naming successor, or SATISFIED
  cycle. Overturn: C-D156. Does not unwrite D-137, D-154,
  or D-155.
- **Commit:** C-D156.

## D-157 — Add DR-G29 as required-now preview-boundary excluded-form admission obligation

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-157.review-adversarial.claude2.turn2.json`,
  `0a36909d8e57f3338a8a83f9799d351bcf60809f8b207a5143ed355976598fa3`)
  CONSENT, advisory CLAUDE-D157-T2-ADV1. Codex
  (`artifacts/coordinator-decisions.D-157.review-adversarial.codex.turn2.json`,
  `7a809de15dae314ad5aaf07afaf1d78f0a6648512288983dc829ac63386a4ae4`)
  CONSENT. Subject `coordinator-decisions.D-157.turn2.draft.md`
  `d39f18b7162195f930f751f818f66f7eeeb98ed34f8f5a785987a86452aa9b0e`.
  Turn-1 Claude CONSENT
  `dc48ceda613af6fce1664210cac2b98313575c61e8c4dd6e3618bb8cdc9da730`;
  turn-1 Codex OBJECT (D157-MF-1, D157-SF-1)
  `380b932eb6b46b1294c6ed169ac3c477cc1565012f762712219cbd7518d7fcd6`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. First of
  D-156's two proposed later works.
- **Decision:** Assign
  `DR-G29 PREVIEW-BOUNDARY-EXCLUDED-FORM-ADMISSION`. It owns
  DR-117 EE-1, EE-2, EE-3b, EE-4, EE-5a, EE-5b, and EE-6a
  only. Required-now becomes the prior 24-member set plus
  G29 (cardinality 25). Harness identifier
  `harness.DR-G29.preview-boundary-excluded-form-admission.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G29 row and the condition-4 measured
  cell becomes 29 of 29 owners / 25 of 25 required names /
  26 OPEN, 3 HARD-BLOCKED. The live row preserves v1-slice
  §7 item 8's disjunctive fates: admission-time excluded
  forms refused with no ExecutionId; represented
  post-admission substitutions rejected before any stage
  (D157-MF-1). EE-1 uses the source Boolean publisher
  neither first-party nor explicitly trusted (D157-SF-1).
  Those seven leftover-design close: remainder is G29
  execution of both named corpora. EE-7a, EE-7b, and EE-7d
  remain leftover-design. EE-6b, EE-7c, and EE-7e remain
  capable-of-riding and unnamed at G09/G14/G16. After this
  act, D-056 Eligibility gates 2 and 3 do not hold for
  DR-117. Class A is not opened. Not eligible in kind. Not
  SATISFIED. Invents no D9 code. Does not restore G17.
  Does not name EE-6b/EE-7c/EE-7e. Does not authorize
  `docs/v2/implementation/`. Advisory CLAUDE-D157-T2-ADV1
  travels as honesty work.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (25 of 25). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D157, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  24-member required-now set. Does not unwrite D-137,
  D-154, D-155, or D-156.
- **Commit:** C-D157.

## D-158 — Add DR-G30 as required-now preview-boundary install-shape obligation

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-158.review-adversarial.claude2.turn2.json`,
  `453b466f836be89f6840a07f34381adf33cceda7a9a54ae976e59182390e7643`).
  Codex
  (`artifacts/coordinator-decisions.D-158.review-adversarial.codex.turn2.json`,
  `48d365f45639dd3f46b24ff7e06315adfeff81c29e6edfbee044b134e50426c0`).
  Subject `coordinator-decisions.D-158.turn2.draft.md`
  `48769069c15de094948903b39f985c29b7b09ffad33e08e50654306197ceb61b`.
  Turn-1 Claude OBJECT (CLAUDE-D158-SF1) at
  `473797a53a94b80a41a3568b74556eeabc112373bff09e98f7c063b7e36e6b2a`;
  turn-1 Codex CONSENT
  `11bf06f9e977f337450a53a016240be21e7f4d85eb348036705298174a5c3a47`.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Last of
  D-156's two proposed later works.
- **Decision:** Assign
  `DR-G30 PREVIEW-BOUNDARY-INSTALL-SHAPE`. It owns DR-117
  EE-7a, EE-7b, and EE-7d only. Required-now becomes the
  prior 25-member set plus G30 (cardinality 26). Harness
  identifier
  `harness.DR-G30.preview-boundary-install-shape.preview`
  is named in the same act. Not authored. Not QUALIFIED.
  File 08 gains the G30 row and the condition-4 measured
  cell becomes 30 of 30 owners / 26 of 26 required names /
  27 OPEN, 3 HARD-BLOCKED. The live claim recites v5's
  useful-install selection including the future DR-131
  pack (CLAUDE-D158-SF1). The pack is not invented.
  CLAUDE-PPBAL-V1-ADV1 is landed: inline corpus and
  not-that-gate distinctions for DR-101, G13, and DR-131
  pack identity. EE-7a, EE-7b, and EE-7d leftover-design
  close: remainder is G30 execution. Together with D-157,
  leftover-design of the ten D-155/D-156 leftover classes
  is closed. EE-6b, EE-7c, and EE-7e remain
  capable-of-riding and unnamed at G09/G14/G16. After this
  act, D-056 Eligibility gates 2 and 3 do not hold for
  DR-117. Class A is not opened. Not eligible in kind. Not
  SATISFIED. Invents no D9 code. Does not restore G17.
  Does not name G13 into required-now. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D158, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  25-member required-now set. Does not unwrite D-137,
  D-155, D-156, or D-157.
- **Commit:** C-D158.

## D-159 — Record dr117-ee-gate-naming.v3 as D-086 successor

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-159.review-adversarial.claude2.json`,
  `e8628e6e185eb67b43c05067ca5da5720959164d3012744467a87e794ac427c5`).
  Codex
  (`artifacts/coordinator-decisions.D-159.review-adversarial.codex.json`,
  `21b0f5f2fa911c88ee82fde54585ed612b83fddde1ca649916449aa1a873385a`).
  Subject `coordinator-decisions.D-159.draft.md`
  `c56e55dce2e2a4b217ba5972c46ff47673bd54782810f4673633012981a6b7cf`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `dr117-ee-gate-naming.v3.json`
  `fb5e928415098c7726bcd91f455327472b6ae7cfe34f65b288ba99cba3ef82c2`
  (0 blockers, 0 SHOULD-FIX) as the D-086 / D-145 successor
  that D-155 and D-156 deferred. Same no-cell-edit branch
  as D-145.
- **Subject:** `docs/coop/artifacts/dr117-ee-gate-naming.v3.json`
  `fb5e928415098c7726bcd91f455327472b6ae7cfe34f65b288ba99cba3ef82c2`.
- **Decision:** Record v3 as the condition-4 naming
  candidate. Naming is not execution. Not QUALIFIED.
  DR-G09 names DR-117 EE-6b. DR-G14 names DR-117 EE-7c.
  DR-G16 names DR-117 EE-7e. Required-now stays 26.
  Condition-4 effect is zero. Condition 4 stays MET at
  26 of 26 / 30 of 30. After this recording, D-056
  Eligibility gates 2 and 3 hold for DR-117. Gate 1
  Class A remains false under D-137's express reservation.
  Gates 4 and 5 are not performed. DR-117 stays `OPEN`.
  Not eligible in kind. Not SATISFIED. Class A is not
  opened. Does not edit file 08. Does not add a DR-G*
  row. Does not rewrite G29 or G30. Does not convert
  EE-6b honesty into confinement. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08
  harness-cell rewrite. Overturn: C-D159. Does not
  unwrite D-137, D-145, D-157, or D-158.
- **Commit:** C-D159.

## D-160 — Record distribution-core-leftover-join.v3 as DR-101 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-160.review-adversarial.claude2.json`,
  `9358f9bd3d185d64c983864d58256939feaf6a89104fe918021952a85d9a946b`).
  Codex
  (`artifacts/coordinator-decisions.D-160.review-adversarial.codex.json`,
  `faad495df832ce9237c89f0ea08ec95484eab0cffa852a34448c2e2b2ed10cd7`).
  Subject `coordinator-decisions.D-160.draft.md`
  `3ffe95eed8595e398088410090d77b1c07855f32da5e0b571fae5b86ffdfcfd3`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `distribution-core-leftover-join.v3.json`
  `808eeb93c53fbdd88de56e455db25c0821402a30643c6e4fce05cf339c7ee3c4`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-155 / D-148.
- **Subject:** `docs/coop/artifacts/distribution-core-leftover-join.v3.json`
  `808eeb93c53fbdd88de56e455db25c0821402a30643c6e4fce05cf339c7ee3c4`.
- **Decision:** Record v3 as DR-101 leftover-design
  measurement. The candidate binds NOTHING. DR-101 stays
  `OPEN`. Leftover-design is not closed. OBL-2 (unauthored
  G01-G05 harness specifications), OD-101-1 (core language
  reserved), and OD-101-2 (signing ceremony reserved)
  remain leftover-design. OBL-1, OBL-D-INV, OBL-D-LAY, and
  OBL-D3 are capable-of-riding named G01-G05 identifiers.
  Class A is not opened. Gates 2 and 3 do not hold for
  DR-101. Does not decide language or ceremony. Does not
  author harness specifications. Does not retarget D-159.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, harness-spec
  authoring, or SATISFIED cycle. Overturn: C-D160. Does
  not unwrite D-114, D-157, D-158, or D-159.
- **Commit:** C-D160.

## D-161 — Record component-manifest-leftover-join.v2 as DR-103 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-161.review-adversarial.claude2.json`,
  `be619b25742f16dc1faa1c2d4c81f4f7a540292c69ae7945f80abfb3a3ba7082`).
  Codex
  (`artifacts/coordinator-decisions.D-161.review-adversarial.codex.json`,
  `af3b6138b511b18558a92ed061f2878e3982d9912648270c44062a9f455185c0`).
  Subject `coordinator-decisions.D-161.draft.md`
  `81a195e2a88ac42fd0f639e3b3ddec3616133275d02e422e764936e053b3a44d`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `component-manifest-leftover-join.v2.json`
  `068a313dfc59124246882636dd714a2ce25f8843408461dfd164323d3c0129cc`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-160 / D-155.
- **Subject:** `docs/coop/artifacts/component-manifest-leftover-join.v2.json`
  `068a313dfc59124246882636dd714a2ce25f8843408461dfd164323d3c0129cc`.
- **Decision:** Record v2 as DR-103 leftover-design
  measurement. The candidate binds NOTHING. DR-103 stays
  `OPEN`. D-013 SATISFIED-refusal stands. Leftover-design
  is not closed. Remaining leftover-design:
  OBL-G15-HARNESS-SPEC, OBL-WINDOWS-PATH,
  OBL-ENVELOPE-MISMATCH, OBL-UNICODE-NORM, OD-1, and
  OD-2. The 51 authored fixtures exist and are not
  leftover-authoring. V2-A1 is specified/repaired at
  schemas.v11 / D-104. Class A is not opened. Gates 2
  and 3 do not hold for DR-103. Does not execute
  fixtures, decide OD-1, or fold OD-2. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, MF-6, naming successor, or SATISFIED
  cycle. Overturn: C-D161. Does not unwrite D-013, D-104,
  D-106, or D-160.
- **Commit:** C-D161.

## D-162 — Record identity-namespace-leftover-join.v2 as DR-104 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-162.review-adversarial.claude2.json`,
  `093140eeeb563f929066ccaa3bd1a67290e4150ebcec61d621f7cb133923c156`).
  Codex
  (`artifacts/coordinator-decisions.D-162.review-adversarial.codex.json`,
  `5d6adf3d1bff652147c71ec99302ded12d8cea02b625f53c5df6adba570bbf53`).
  Subject `coordinator-decisions.D-162.draft.md`
  `ccb9fdd5e52f00022e743350a8f3391dbf1972492fcad4252216957a5df1f1ff`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `identity-namespace-leftover-join.v2.json`
  `cdb3003bfd2a823730833c05f8cbacb13c98555170ea57d150e0acb055597df3`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-161 / D-160.
- **Subject:** `docs/coop/artifacts/identity-namespace-leftover-join.v2.json`
  `cdb3003bfd2a823730833c05f8cbacb13c98555170ea57d150e0acb055597df3`.
- **Decision:** Record v2 as DR-104 leftover-design
  measurement. The candidate binds NOTHING. DR-104 stays
  `DECIDED-V1-NOT-INTEGRATED`. leftover-design/OPEN is a
  finding against that token. Leftover-design is not
  closed. Remaining leftover-design: OBL-NT-11-EXECUTION
  (no live DR-G* owns identity-namespace negative-test
  execution). D-012 policy and the eleven authored classes
  are not leftover-authoring. Class A is not opened. Class
  B SATISFIED is not recorded. Gates 2 and 3 do not hold
  for DR-104. Advisory CLAUDE-INLJ-V2-ADV1 travels as
  honesty work. Does not execute fixtures. Does not apply
  D-130 or D-131. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, or SATISFIED cycle.
  Overturn: C-D162. Does not unwrite D-012, D-130, D-131,
  or D-161.
- **Commit:** C-D162.

## D-163 — Record permission-leftover-join.v2 as DR-105 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-163.review-adversarial.claude2.turn2.json`,
  `7d5b08c64134d9105b8796236c4b166e26dbafb855b77dd4925a5807fbd37a7e`).
  Codex
  (`artifacts/coordinator-decisions.D-163.review-adversarial.codex.turn2.json`,
  `54e6829ec1bbbce5aca4e57ae73994c20d106bc5104c7135b796bd7797d13035`).
  Subject `coordinator-decisions.D-163.turn2.draft.md`
  `52a5986416af387ffbbfd615691e220639173e705dd4f79adbd30614e85bded3`.
  Turn-1 Claude CONSENT
  `1b199e69e2cb2252921276c5ced9c742876b7c18785316384bb576c27cc660a1`;
  turn-1 Codex OBJECT (CODEX-D163-SF1)
  `fe69b0ff03916b8bb0f2413c37913a5626eb126d246fefb2e9b9f4aeca85e99b`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `permission-leftover-join.v2.json`
  `68ea10e052ae6a2eb6a35fd021be7e72418157a47fa07493ad2f4d927aeb9558`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-162 / D-161.
- **Subject:** `docs/coop/artifacts/permission-leftover-join.v2.json`
  `68ea10e052ae6a2eb6a35fd021be7e72418157a47fa07493ad2f4d927aeb9558`.
- **Decision:** Record v2 as DR-105 leftover-design
  measurement. The candidate binds NOTHING. DR-105 stays
  `OPEN`. leftover-design/OPEN is the token, not a finding.
  Leftover-design is not closed. Remaining leftover-design:
  OBL-G09-HARNESS-SPEC, OBL-FX-AUTHORING, OBL-FC-C1, and
  OBL-BLK-1..4. D-032 actor scope and the recorded v2/v9/v8/v25
  candidates are not leftover-authoring. OBL-ACTOR-JOIN rides
  DR-114; D-129's recorded candidate binds NOTHING. Class A
  is not opened. Gates 2 and 3 do not hold for DR-105. Does
  not execute fixtures. Does not record FC-C1. Does not apply
  D-042, D-093, D-126, or D-128. Does not admit CA-1
  IN_PROCESS or mint the later CA-2 gate. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, FC-C1 recording, or
  SATISFIED cycle. Overturn: C-D163. Does not unwrite
  D-032, D-042, D-093, D-126, D-128, D-129, or D-162.
- **Commit:** C-D163.

## D-164 — Record doctor-actor-leftover-join.v2 as DR-114 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-164.review-adversarial.claude2.json`,
  `a895d5feea5054dcbba15b3d96e7cbdbcbffdcf7756d45e1f1d2101ba0c849aa`).
  Codex
  (`artifacts/coordinator-decisions.D-164.review-adversarial.codex.json`,
  `3b87c460a78921e48ea6b132350845a6ba51153a49d1a36a1f577955a6819372`).
  Subject `coordinator-decisions.D-164.draft.md`
  `9327927be79e6d41d042e0c45dbec1eba78857c14ad0960b70220ceae2101554`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `doctor-actor-leftover-join.v2.json`
  `874af09ad24d21179fb6abb9f4f94332e56eb956b7991295e5c31631e84f80c6`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-163 / D-162.
- **Subject:** `docs/coop/artifacts/doctor-actor-leftover-join.v2.json`
  `874af09ad24d21179fb6abb9f4f94332e56eb956b7991295e5c31631e84f80c6`.
- **Decision:** Record v2 as DR-114 leftover-design
  measurement. The candidate binds NOTHING. DR-114 stays
  `OPEN`. leftover-design/OPEN is the token, not a finding.
  Leftover-design is not closed. Remaining leftover-design:
  OBL-G12-HARNESS-SPEC, OBL-G21-HARNESS-SPEC,
  OBL-DOCTOR-FX-AUTHORING, OBL-JOIN-FX-AUTHORING,
  OBL-JOIN-FX-EXECUTION, OBL-FC-C1, and OBL-BLK-1..4.
  Actor-join fixture execution is not forced onto G09.
  Class A is not opened. Gates 2 and 3 do not hold for
  DR-114. Does not execute fixtures. Does not record FC-C1.
  Does not apply D-035, D-126, D-127, or D-129. Does not
  invent a D9 code. Does not mint a D-096 (A) grant. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`. The competing filename
  `doctor-leftover-join.v1.json` is not this subject.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, FC-C1 recording, or
  SATISFIED cycle. Overturn: C-D164. Does not unwrite
  D-032, D-035, D-126, D-127, D-129, or D-163.
- **Commit:** C-D164.

## D-165 — Record language-quality-leftover-join.v2 as DR-118 leftover-design measurement

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-165.review-adversarial.claude2.json`,
  `11f01bc900b45a3d59a93a2b92a2d1e796b286a74ae7f85277800892df6f35e3`).
  Codex
  (`artifacts/coordinator-decisions.D-165.review-adversarial.codex.json`,
  `68551da8ce2e378d79d369e576e8e857ed89c59af9ad1f8b546176286946ca68`).
  Subject `coordinator-decisions.D-165.draft.md`
  `7add0380abd4dd70410006df707ecfbe7d86cde88747a35f8c7da820b8f058cf`.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-quality-leftover-join.v2.json`
  `a51644fe85ddff1dcee77f24d1b1a6f3c236ca8374a9b5276ab6d496976f87ea`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-164 / D-163.
- **Subject:** `docs/coop/artifacts/language-quality-leftover-join.v2.json`
  `a51644fe85ddff1dcee77f24d1b1a6f3c236ca8374a9b5276ab6d496976f87ea`.
- **Decision:** Record v2 as DR-118 leftover-design
  measurement. The candidate binds NOTHING. DR-118 stays
  `DECIDED-V1-NOT-INTEGRATED`. leftover-design/OPEN is a
  finding against that token. Leftover-design is not
  closed. Remaining leftover-design: OBL-THRESHOLDS,
  OBL-MATRIX-CORPUS, and OBL-G13-RESERVED. D-002 role list
  and D-007 acceptance structure are not leftover-authoring.
  OBL-DR125-ACTIVATION rides DR-125; D-110 binds NOTHING.
  Matrix authoring waits on DR-125 closure or disposition.
  Class A is not opened. Class B SATISFIED is not recorded.
  Gates 2 and 3 do not hold for DR-118. Does not invent
  per-row numeric thresholds. Does not author the matrix or
  corpus. Does not name G13 into required-now. Does not mint
  Rust-as-core. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (26 of 26). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, naming successor, threshold decision, or
  SATISFIED cycle. Overturn: C-D165. Does not unwrite D-007,
  D-113, D-110, or D-164.
- **Commit:** C-D165.

## D-166 — Remove the duplicate D-165 heading

- **Date:** 2026-08-16
- **Status:** **ADOPTED 2026-08-16.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-166.review-adversarial.claude2.json`,
  `e00bfb732bc04609d704a86b6590b72b1f6fdb92a0a2a71b96f0e11163dbaa7e`).
  Codex
  (`artifacts/coordinator-decisions.D-166.review-adversarial.codex.json`,
  `8b6900e9d8a7d22ce337866c9f1e5ad8008edcbf23f7ec80352435038dd5e558`).
  Subject `coordinator-decisions.D-166.draft.md`
  `1cab6a1f891188a91296393ab6193d4401ad44f4dbb6cc5e4b61d212c809c266`.
- **Decision type:** RULE-GOVERNED. Recording hygiene. Same
  class as D-087 / D-156. Does not reopen D-165.
- **Decision:** Keep the first D-165 recital. Delete the
  second. Do not rewrite D-165's Decision. Do not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero. D-165's readiness effect is
  unchanged. Condition 2 stays 4 of 32. Condition 4 stays
  MET on the naming half (26 of 26). Condition 5 last.
- **Reversibility:** C-D166 plus restore of the deleted
  second recital. Does not overturn D-165. Overturn: C-D166.
- **Commit:** C-D166.

## D-167 — Add DR-G31 as required-now identity-namespace negative-test execution obligation

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-167.review-adversarial.claude2.json`,
  `70897ad06981d7007f92b061790997335efc962ebd2fb22dcb3df4416d64aa97`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-167.review-adversarial.codex.json`,
  `af259952ef56c797b6aba646f48f404ea2313963142d9818022f94a2124c9004`)
  CONSENT. Subject `coordinator-decisions.D-167.draft.md`
  `0cc4ce068c37b7c974f0181fb46b5abd6d01d68c401ff011265d57a84229c9bd`.
  Frozen three-limb candidate
  `g31-three-limb-act.v1.json`
  `7d5848439b3cca947f1a9c8be730ca21c716559321306778ab7b24876cf28dd7`
  Stage A Claude ACCEPT
  `0bc2deeb294179005ca668f3d7f2021ba38c51da925bdfc2da9a23c6248e01e9`
  0/0; Stage A Codex ACCEPT
  `e2a977e7f67ea6604d20644182dc287f52222c7cd90936ac8cc9499eb2c520fc`
  0/0.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Same
  class as D-147 / D-150 / D-157 / D-158.
- **Decision:** Assign
  `DR-G31 IDENTITY-NAMESPACE-NEGATIVE-TEST-EXECUTION`. It
  owns the eleven D-012 / identity-v3 negative-test classes
  recorded at D-130, verbatim and in order. Required-now
  becomes the prior 26-member set plus G31 (cardinality
  27). Harness identifier
  `harness.DR-G31.identity-namespace-negative-test.preview`
  is named in the same act at
  `docs/coop/artifacts/harness.DR-G31.identity-namespace-negative-test.preview.v2.json`.
  Not authored. Not QUALIFIED. File 08 gains the G31 row
  and the condition-4 measured cell becomes 31 of 31
  owners / 27 of 27 required names / 28 OPEN, 3
  HARD-BLOCKED. Leftover-design of OBL-NT-11-EXECUTION
  closes: remainder is G31 execution of the eleven D-130
  classes. After this act, D-056 Eligibility gates 2 and 3
  hold for DR-104. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Gates 4 and 5 are not
  performed. DR-104 stays `DECIDED-V1-NOT-INTEGRATED`. Not
  SATISFIED. Does not execute the eleven classes. Does not
  invent a twelfth class. Does not force a ride onto G15.
  Does not steal DR-103 leftover. Does not record G32.
  Does not restore G17. Does not name G13 into
  required-now. Does not invent a D9 code, a section 7.1
  recipe, or a D-006 unit. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (27 of 27). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D167, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  26-member required-now set. Does not unwrite D-012,
  D-056, D-130, D-158, D-162, or D-166.
- **Commit:** C-D167.

## D-168 — Record preview-product-boundary-successor.v7 as DR-117 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-168.review-adversarial.claude2.json`,
  `976ce790b0d920134dd58ab4735a2fe50fb50c8b72254676adb7f344ef339eb2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-168.review-adversarial.codex.json`,
  `f225c5ab751b9b76907874b932db21e10356fe67d648755690303511ec7f48c5`)
  CONSENT. Subject `coordinator-decisions.D-168.draft.md`
  `b181c5d5cffa56920bd9602ec0d9b8ecb2c863b23a29d338049733c3df0e9eab`.
  Frozen successor
  `preview-product-boundary-successor.v7.json`
  `243c12a2389a0f81d059209f5b7050a700498840d036275c7b81eeadc31fe548`
  Stage A Claude ACCEPT
  `d154e94a6c3803aab67600b515303b112844f21593b39fe8a8f441b276ed4e87`
  0/0; Stage A Codex ACCEPT
  `0609c561e50dd50dda81f2c6075deb2e16365e6727d7f1c9f2117efb7c25068c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-product-boundary-successor.v7.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-137 / D-159. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/preview-product-boundary-successor.v7.json`
  `243c12a2389a0f81d059209f5b7050a700498840d036275c7b81eeadc31fe548`.
- **Decision:** Record v7 as DR-117 leftover remasurement
  after D-157 / D-158 / D-159. The candidate binds NOTHING.
  DR-117 stays `OPEN`. leftover-design of unnamed EE classes
  remains closed at D-159. Remainder is named-gate execution.
  D-056 Eligibility gates 2 and 3 continue to hold for
  DR-117 (D-159). Gate 1 Class A remains false under
  D-137's express reservation. v7 does not withdraw that
  reservation. Venue for any later lift is a reviewed
  coordinator act, not an artifact. Gates 4 and 5 are not
  performed. Not eligible in kind. Not SATISFIED. Required-now
  stays 27. Condition-4 effect is zero. Condition 4 stays
  MET at 27 of 27 / 31 of 31. v6 stays frozen; do not record
  v6. Advisories CLAUDE-PPBS-V7-ADV-1 and CLAUDE-PPBS-V7-ADV-2
  travel as honesty work. Standing CLAUDE-PPBS-V3-ADV-1 venue
  limb stands. Does not rewrite G29, G30, or G31. Does not
  record G32. Does not edit file 08. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (27 of 27). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D168. Does not unwrite D-137, D-157, D-158,
  D-159, or D-167.
- **Commit:** C-D168.

## D-169 — Add DR-G32 as required-now actor-join fixture-execution obligation

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-169.review-adversarial.claude2.json`,
  `9cffe2a25c75e387c96991eb42f85c1e632957507c2083f26777e9f6663b11fc`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-169.review-adversarial.codex.json`,
  `b9e9540ce382d1cd4ad3bef9f23efeb94036f00a8345a20150d9b41917de10e9`)
  CONSENT. Subject `coordinator-decisions.D-169.draft.md`
  `c5163db134276d4d27ef65e84fe76d21b11b044859d4e2a0ae81c1a23d5ddb2b`.
  Frozen three-limb candidate
  `g32-three-limb-act.v2.json`
  `8a64123830a95bd7774f171531f7872a34e35aeaf865383311c29dbb7ed5fc31`
  Stage A Claude ACCEPT
  `61dbbf6c22b49cc4c89795ffb7d23507d7b6ed8b4defc6ee239f5b8f28436d40`
  0/0; Stage A Codex ACCEPT
  `93e040fe110c21b7202f94072df3723f5f1e428a422faa427125fa4d48f959d2`
  0/0.
- **Decision type:** RULE-GOVERNED three-limb act. D-001 MF-6
  file-08 write, scoped D-002 condition-4 required-gate-set
  successor, and D-086 successor in the same act. Same
  class as D-147 / D-150 / D-157 / D-158 / D-167.
- **Decision:** Assign
  `DR-G32 ACTOR-JOIN-FIXTURE-EXECUTION`. It owns the thirteen
  already-named actor-join v8 fixture classes, verbatim and
  in order. Required-now becomes the prior 27-member set
  plus G32 (cardinality 28). Harness identifier
  `harness.DR-G32.actor-join-fixture-execution.preview` is
  named in the same act at
  `docs/coop/artifacts/harness.DR-G32.actor-join-fixture-execution.preview.v1.json`.
  Not authored. Not QUALIFIED. Fixture bytes remain
  NOT-AUTHORED. File 08 gains the G32 row and the
  condition-4 measured cell becomes 32 of 32 owners /
  28 of 28 required names / 29 OPEN, 3 HARD-BLOCKED.
  Leftover-design of OBL-JOIN-FX-EXECUTION closes:
  remainder is G32 execution once fixture implementations
  exist. leftover-design of OBL-JOIN-FX-AUTHORING,
  OBL-DOCTOR-FX-AUTHORING, OBL-FC-C1, and OBL-BLK-1..4
  remains. After this act, D-056 Eligibility gates 2 and 3
  do not hold for DR-114. Gate 1 Class A is not opened.
  Class B SATISFIED is not recorded. DR-114 stays `OPEN`.
  Not SATISFIED. Does not execute the thirteen classes.
  Does not invent a fourteenth class. Does not force a ride
  onto G09. Does not steal DR-105 leftover. Does not record
  FC-C1. Does not mint a CA-2 decision. Does not admit CA-1
  IN_PROCESS. Does not record join-fx-gate-naming.v1. Does
  not unwrite D-167. Does not restore G17. Does not name
  G13 into required-now. Does not invent a D9 code. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  SATISFIED cycle, leftover rewrite, or file-08 harness-cell
  rewrite. Overturn: C-D169, plus restore of the prior gate
  table, the prior condition-4 measured cell, and the prior
  27-member required-now set. Does not unwrite D-032,
  D-129, D-164, D-167, or D-168.
- **Commit:** C-D169.

## D-170 — Record doctor-actor-leftover-join.v11 as DR-114 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-170.review-adversarial.claude2.json`,
  `66b9d56bb581d6b8203894ebfac645c364e56059ec95c5b9794726b3e619cbf4`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-170.review-adversarial.codex.json`,
  `56f67c209f100ed8662598ff73ae5885a89716f2da59821df5bc76f8f2a06b55`)
  CONSENT. Subject `coordinator-decisions.D-170.draft.md`
  `4279a1fd7ca605136d1d63227e262c05466577989a3c0f3f6b158e3232883bc0`.
  Frozen leftover-join
  `doctor-actor-leftover-join.v11.json`
  `3943a7bb2813324f1df0960b216fc2703139754283f72b3add307967caa0d950`
  Stage A Claude ACCEPT
  `5ce64f13f3c4ef3001a7c42045fa7887a610bd9322c866b2195c02e5fa21b25b`
  0/0; Stage A Codex ACCEPT
  `9e645f447cb083179c6046e8a27b8f24472daee48967a8ff6038d3b71d1ecb3a`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `doctor-actor-leftover-join.v11.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-164 / D-168. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/doctor-actor-leftover-join.v11.json`
  `3943a7bb2813324f1df0960b216fc2703139754283f72b3add307967caa0d950`.
- **Decision:** Record v11 as DR-114 leftover remasurement
  after D-169. The candidate binds NOTHING. DR-114 stays
  `OPEN`. leftover-design of unnamed JOIN-FX execution
  remainder is closed. Remainder of that obligation is G32
  execution. leftover-design of OBL-JOIN-FX-AUTHORING,
  OBL-DOCTOR-FX-AUTHORING, OBL-FC-C1, and OBL-BLK-1..4
  remains. D-056 Eligibility gates 2 and 3 do not hold for
  DR-114. Gate 1 Class A is not opened. Not eligible in
  kind. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. v8/v9/v10 stay frozen; do not record them.
  Does not invent fixture bytes. Does not record FC-C1.
  Does not mint BLK-1..4. Does not force a ride onto G09.
  Does not rewrite G31 or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D170. Does not unwrite D-032, D-164, D-167,
  D-168, or D-169.
- **Commit:** C-D170.

## D-171 — Record permission-leftover-join.v9 as DR-105 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-171.review-adversarial.claude2.json`,
  `8782b3859d76c6418161cbf7a4e903afae1ac84d977c7183b32dd8e561ac9a1e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-171.review-adversarial.codex.json`,
  `b8532a379f603f4f2a005c98ddcde3504ee2bede7e8f5bb994ccaf272b4bbf4f`)
  CONSENT. Subject `coordinator-decisions.D-171.draft.md`
  `3a596904e0e2f3e2c4cb2d7a01f910956107cdcd88b0eb7a37985b02b8a8b192`.
  Frozen leftover-join
  `permission-leftover-join.v9.json`
  `71c0b80bfd11fe9ae1601cc390d76e01aa67621b550a04e1ad8b8359ce2b97fe`
  Stage A Claude ACCEPT
  `aa50c430a1efe2b4f099464dd004432319afe523927ece06b5631edbe9b9b390`
  0/0; Stage A Codex ACCEPT
  `832242100056ffcb3c8cc648ed5cdf47a53c18e2fa64d1feb01206ab0a774a80`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `permission-leftover-join.v9.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-163 / D-170. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/permission-leftover-join.v9.json`
  `71c0b80bfd11fe9ae1601cc390d76e01aa67621b550a04e1ad8b8359ce2b97fe`.
- **Decision:** Record v9 as DR-105 leftover remasurement
  after D-169 / D-170. The candidate binds NOTHING. DR-105
  stays `OPEN`. Actor-join fixture execution is
  qualification at DR-G32. leftover-design of
  OBL-FX-AUTHORING, OBL-R10-AUTHORING, OBL-R6-AUTHORING,
  OBL-FC-C1, and OBL-BLK-1..4 remains. D-056 Eligibility
  gates 2 and 3 do not hold for DR-105. Gate 1 Class A is
  not opened. Not eligible in kind. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. v7/v8
  stay frozen; do not record them. Does not fold R-10 or
  R-6 into the fourteen. Does not invent a leftover ID,
  fixture bytes, or a decision-record envelope. Does not
  rewrite G31 or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D171. Does not unwrite D-032, D-042, D-163,
  D-169, or D-170.
- **Commit:** C-D171.

## D-172 — Record exact-bytes-leftover-join.v5 as G07 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-172.review-adversarial.claude2.turn2.json`,
  `3ac052b02885e236ea1400812bf67c0a9d08d74d7e99874ae3be0146c99bf107`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-172.review-adversarial.codex.turn2.json`,
  `aac2c2053ef787ad4b9fa2bcd309c74ce376d56cadf1331cac0be5ce2b404a0c`)
  CONSENT. Subject `coordinator-decisions.D-172.turn2.draft.md`
  `a80d557b62b9306178d326479b57e65e0715d69979403c36994faeebfe05c453`.
  Turn-1 Claude OBJECT (CLAUDE-D172-MF1)
  `e985639f0e0f855446b47092f2a39e5c59175438a00ab0daceacd4aca58d3aeb`;
  turn-1 Codex CONSENT
  `6acac68047ff3fc59b1d1ff679207835917b3f1ad54372c02d6eeb7c71148e5f`.
  Frozen leftover-join
  `exact-bytes-leftover-join.v5.json`
  `8ffecd694750d912f11a0f4b933c650db6528fe1b82ce584d63b6140b26df7d8`
  Stage A Claude ACCEPT
  `e99ceaeb182a0697617bfd5542bc6681f81ef71151a0f32b998500000639dfb3`
  0/0; Stage A Codex ACCEPT
  `33c4efaa8e3934101fdd71aaa24d2ae490142f509e1c0f9bd01aeaa0cf43db2a`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `exact-bytes-leftover-join.v5.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 / D-171. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/exact-bytes-leftover-join.v5.json`
  `8ffecd694750d912f11a0f4b933c650db6528fe1b82ce584d63b6140b26df7d8`.
- **Decision:** Record v5 as G07 leftover remasurement
  after D-171. Lands CLAUDE-D172-MF1. The candidate binds
  NOTHING. DR-G07 stays `OPEN`. leftover-design of
  OBL-G07-FX-AUTHORING and OBL-FILESYSTEM-COVERAGE remains.
  OBL-G07-COVERAGE-DOMAIN-ACT is specified-not-leftover.
  D-056 Eligibility gates 2 and 3 do not hold for DR-103.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v4 remains a
  historical measurement as of HEAD `5d5d778` / required-now
  26 and is not recorded as a current remasurement.
  v1/v2/v3/v4 stay frozen; do not record them as current.
  Does not invent fixture bytes. Does not rewrite G07, G31,
  or G32. Does not edit file 08. Does not invent a D9 code
  or a D-006 unit. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D172. Does not unwrite D-086, D-169, D-170,
  or D-171. Does not unwrite the turn-1 OBJECT.
- **Commit:** C-D172.

## D-173 — Record distribution-core-leftover-join.v7 as DR-101 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-173.review-adversarial.claude2.json`,
  `2652bc664616b8186dc56249c1fbafea90fb95dfb2ba136823b4671d00e38038`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-173.review-adversarial.codex.json`,
  `c3ebd0e7a4534724a7b6d3734c1bb285b2dccec2e078d02c9323490e1dca1373`)
  CONSENT. Subject `coordinator-decisions.D-173.draft.md`
  `b400b8fb40315e6db7789d742f11c8a02c969f934bbf052129a5573bfc4ed528`.
  Frozen leftover-join
  `distribution-core-leftover-join.v7.json`
  `ccdae033f09dfa3655003d69bf30d29de28c712943f9d0eefb78eb93dac27ad6`
  Stage A Claude ACCEPT
  `9500da512b7235e0b5d407c6df35bf13806ce608967969797a9f5809df9165db`
  0/0; Stage A Codex ACCEPT
  `63d24a385858b959ee3fc6de77b0625a7d993a7fa8d44ff6b8dc71c4e65c8f5c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `distribution-core-leftover-join.v7.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 / D-171 / D-172. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/distribution-core-leftover-join.v7.json`
  `ccdae033f09dfa3655003d69bf30d29de28c712943f9d0eefb78eb93dac27ad6`.
- **Decision:** Record v7 as DR-101 leftover remasurement
  after D-172. Lands CLAUDE-DCLJ-V6-SF1. The candidate binds
  NOTHING. DR-101 stays `OPEN`. leftover-design of the
  D-006 unit limb, OD-101-1, and OD-101-2 remains. D-056
  Eligibility gates 2 and 3 do not hold for DR-101. Gate 1
  Class A is not opened. Not eligible in kind. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v5 remains a historical measurement as of
  HEAD `5d5d778` / required-now 26. v5/v6 stay frozen; do
  not record them as current. Does not invent a D-006 unit.
  Does not mint Rust-as-core. Does not invent fixture
  bytes. Does not rewrite G01–G05, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D173. Does not unwrite D-114, D-160, D-169,
  D-170, D-171, or D-172.
- **Commit:** C-D173.

## D-174 — Record component-manifest-leftover-join.v6 as DR-103 leftover remasurement

- **Date:** 2026-08-20
- **Status:** **ADOPTED 2026-08-20.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-174.review-adversarial.claude2.turn2.json`,
  `1e25681eb3757f35d01c347d38f97ab1dc60571dcc9d5f272737366a2542b332`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-174.review-adversarial.codex.turn2.json`,
  `7babe78916b15ec9d223189b9e34a0bea489a355db2a2a25d4bc70af37c579e1`)
  CONSENT. Subject `coordinator-decisions.D-174.turn2.draft.md`
  `97a4cb5dce5505763c5a2c26f4a3917c74c2c3d026073fd09cbeb59fb4cd11d4`.
  Turn-1 Claude OBJECT (CLAUDE-D174-SF1)
  `64c6d40f6382e91f16b86037cf26398ec34d0effdee38004fe9ba7231257d95e`;
  turn-1 Codex CONSENT
  `179dec626a18d55a89b76782d94d1682fb40c16568e0c3a48d91f306e027d71f`.
  Frozen leftover-join
  `component-manifest-leftover-join.v6.json`
  `9953f9692379f3f30254df12735d284559da6b6e979fd684296ace02d0e6e212`
  Stage A Claude ACCEPT
  `ef77d31bdf1cab61b8ac05a4bc6d256de46a450572d786a5e895117e313611a1`
  0/0; Stage A Codex ACCEPT
  `6d8014a3a14b4af7801028bfd9b5f85e14d57e9dacfe387a5353db47cfa29863`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `component-manifest-leftover-join.v6.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 / D-171 / D-172 / D-173. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/component-manifest-leftover-join.v6.json`
  `9953f9692379f3f30254df12735d284559da6b6e979fd684296ace02d0e6e212`.
- **Decision:** Record v6 as DR-103 leftover remasurement
  after D-173. Lands CMLJ-V5-SF1 and CLAUDE-CMLJ-V5-SF1.
  Lands CLAUDE-D174-SF1. The candidate binds NOTHING.
  DR-103 stays `OPEN`. leftover-design of Windows-path
  fixture bytes, ENVELOPE_MISMATCH, unicode-norm, OD-1, and
  OD-2 remains. D-056 Eligibility gates 2 and 3 do not hold
  for DR-103. Gate 1 Class A is not opened. Not eligible in
  kind. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Frozen v4 remains a historical measurement
  as of HEAD `5d5d778` / required-now 26. v4/v5 stay frozen;
  do not record them as current. Does not invent fixture
  bytes or a reserved-device-name list. Does not rewrite
  G15, G31, or G32. Does not edit file 08. Does not invent
  a D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D174. Does not unwrite D-013, D-104, D-106,
  D-161, D-169, D-170, D-171, D-172, or D-173. Does not
  unwrite the turn-1 OBJECT.
- **Commit:** C-D174.

## D-175 — Record identity-namespace-leftover-join.v6 as DR-104 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-175.review-adversarial.claude2.turn2.json`,
  `bc4f5e092929d0b1e9381f4d24a8015c3c36444060068f94a711be2e0965c957`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-175.review-adversarial.codex.turn2.json`,
  `1a379f4d4a5454e0e312dffde8bddc9f4d23f0c887001814177741d2f4f3862f`)
  CONSENT. Subject `coordinator-decisions.D-175.turn2.draft.md`
  `2e0fb95d63da32e17cb295b26dc9eb02b23b9b32503e2e4bd24cae173bdabf5d`.
  Turn-1 Claude CONSENT
  `f7fd700eaa4fdec06515d7f50da2716c282ae0c1c51d13d33bcb64a5ac38b9a0`;
  turn-1 Codex OBJECT (D175-SF1)
  `0c934f9b2557a0adcd3ae3ae7c56d0e35fe25d00a02d27155ad2425fde0b61c6`.
  Frozen leftover-join
  `identity-namespace-leftover-join.v6.json`
  `ab31c6075723d34503958a838ad1a3c4da37b3644390b6df8117ae34758099cc`
  Stage A Claude ACCEPT
  `eaa9e3b39eb896315e5f95e60294c0f3bae05ca3881404e732a76c7af91039b2`
  0/0; Stage A Codex ACCEPT
  `6ff7f24bc5025813254a569ef6a0d443c29c4e9bd0db20e0f8581175b20a679e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `identity-namespace-leftover-join.v6.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 / D-171 / D-172 / D-173 / D-174. Not a three-limb
  act.
- **Subject:** `docs/coop/artifacts/identity-namespace-leftover-join.v6.json`
  `ab31c6075723d34503958a838ad1a3c4da37b3644390b6df8117ae34758099cc`.
- **Decision:** Record v6 as DR-104 leftover remasurement
  after D-174. Lands CLAUDE-INLJ-V5-SF1, INLJ-V5-SF1, and
  D175-SF1. The candidate binds NOTHING. DR-104 stays
  `DECIDED-V1-NOT-INTEGRATED`. leftover-design of unnamed
  NT-11 execution remainder is closed. Remainder is G31
  execution. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v4 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26, before D-167. v4/v5 stay frozen; do not
  record them as current. Does not execute the eleven
  classes. Does not rewrite G31 or G32. Does not force a
  ride onto G15. Does not edit file 08. Does not invent a
  D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D175. Does not unwrite D-012, D-130, D-131,
  D-162, D-167, D-168, D-169, D-170, D-171, D-172, D-173,
  or D-174. Does not unwrite the turn-1 OBJECT.
- **Commit:** C-D175.

## D-176 — Record lifecycle-leftover-join.v3 as DR-107 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-176.review-adversarial.claude2.json`,
  `22c91728cba70e697677226c28bc74c29a29d820174a2e11b9bc405a7508328b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-176.review-adversarial.codex.json`,
  `99d325593d23fee4b34b3af54c23c9639891103105176778b7cd7dd3be12d65e`)
  CONSENT. Subject `coordinator-decisions.D-176.draft.md`
  `cd36e84d1ea74e1d78ec45947f95de0005141f11c3913be54bf89e0641b61d35`.
  Frozen leftover-join
  `lifecycle-leftover-join.v3.json`
  `9ca8bdb03af8e6e00f970364e5a1958f0fe88dcd12f0f8948d0d29069dd7042d`
  Stage A Claude ACCEPT
  `8acfbb3fa7c9bb8e4d90b2ba74310a5c53a496aac3bb088f60f6b97a252751e8`
  0/0; Stage A Codex ACCEPT
  `14cb34faba447aa7726db32380614cf11f1da063376785cd5eabffb129bbe4a8`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `lifecycle-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 / D-171 / D-172 / D-173 / D-174 / D-175. Not a
  three-limb act.
- **Subject:** `docs/coop/artifacts/lifecycle-leftover-join.v3.json`
  `9ca8bdb03af8e6e00f970364e5a1958f0fe88dcd12f0f8948d0d29069dd7042d`.
- **Decision:** Record v3 as DR-107 leftover remasurement
  after D-175. The candidate binds NOTHING. DR-107 stays
  `PROPOSED-CLOSED-FOR-REVIEW`. leftover-design of
  OBL-G18-FX-AUTHORING and OBL-ENCODING-RESERVED remains.
  D-056 Eligibility gates 2 and 3 do not hold for DR-107.
  Gate 1 Class A is not opened. Not eligible in kind. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v2 remains a historical measurement as of
  HEAD `5d5d778` / required-now 26. v2 stays frozen; do not
  record it as current. Does not invent fixture bytes, a
  journal, lock-file grammar, lease API, solver, or
  filesystem layout. Does not rewrite G18, G31, or G32.
  Does not edit file 08. Does not invent a D9 code. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D176. Does not unwrite D-107, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, or D-175.
- **Commit:** C-D176.

## D-177 — Record compatibility-leftover-join.v2 as DR-111 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-177.review-adversarial.claude2.json`,
  `67f1073a67ea1a47ba398b360df5579993bfc77eea5b013487545ba583da43d2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-177.review-adversarial.codex.json`,
  `2e2f862ce7d578c5dfa36ecc7cf9fbc2c7ee1f2af86618f63a0a3ba80a2fa187`)
  CONSENT. Subject `coordinator-decisions.D-177.draft.md`
  `6c2dcb078d2c2b97542e1669796a855a11d6403a1ec72689ec02d2c451e14c83`.
  Frozen leftover-join
  `compatibility-leftover-join.v2.json`
  `33e4299d7f65bf37c2f5d54193e004c69d542d3f5da99417e1360efc2f8b7259`
  Stage A Claude ACCEPT
  `a0cef800e46fa394a4cbbf28d4742cfcd494b9f0bbad39a611f5cf263c6ed9ed`
  0/0; Stage A Codex ACCEPT
  `ba6c178ba1e1c3d951d9e4c58c66e9d37b8a49ff15aaf27f2fc83a2878492fdc`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `compatibility-leftover-join.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-176. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/compatibility-leftover-join.v2.json`
  `33e4299d7f65bf37c2f5d54193e004c69d542d3f5da99417e1360efc2f8b7259`.
- **Decision:** Record v2 as DR-111 leftover remasurement
  after D-176. The candidate binds NOTHING. DR-111 stays
  `OPEN`. leftover-design of OBL-NUMERIC-WINDOWS and
  OBL-LOCK-JOIN remains. D-056 Eligibility gates 2 and 3
  do not hold for DR-111. Gate 1 Class A is not opened.
  Not eligible in kind. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Frozen v1 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. v1 stays frozen; do not record it as
  current. Does not invent numeric windows. Does not
  produce a lock. Does not edit file 08. Does not invent
  a D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D177. Does not unwrite D-103, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, or
  D-176.
- **Commit:** C-D177.

## D-178 — Record signed-index-leftover-join.v3 as DR-112 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-178.review-adversarial.claude2.json`,
  `821ad6a22d14731c0482341ad01b7efc6cb64534ec7366aec057da29ab4b84cd`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-178.review-adversarial.codex.json`,
  `0bec745add9acd54ed2c401afb920d80daf1ade2c0013da77de2db9c71545669`)
  CONSENT. Subject `coordinator-decisions.D-178.draft.md`
  `d23c271468e755b5bb4b43c7db87755650d970b9c459f928ee757f0ac99b73b2`.
  Frozen leftover-join
  `signed-index-leftover-join.v3.json`
  `f1fee0cb001fb61d3d6e3a03ccb882903175def1c28eda8525dbe6adaf66a146`
  Stage A Claude ACCEPT
  `324fde14e1a34d6330089edf35c9831465442474cf49c1dadcba94d8ac5a60ad`
  0/0; Stage A Codex ACCEPT
  `e554d403cd0a0f504730749e74a43918195b84219e825000a5e8430d20f36363`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `signed-index-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-177. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/signed-index-leftover-join.v3.json`
  `f1fee0cb001fb61d3d6e3a03ccb882903175def1c28eda8525dbe6adaf66a146`.
- **Decision:** Record v3 as DR-112 leftover remasurement
  after D-177. The candidate binds NOTHING. DR-112 stays
  `OPEN`. leftover-design of OBL-G08-FX-AUTHORING and
  OBL-RESERVED-NUMBERS remains. D-056 Eligibility gates 2
  and 3 do not hold for DR-112. Gate 1 Class A is not
  opened. Not eligible in kind. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or reserved
  numbers. Does not rewrite G08, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D178. Does not unwrite D-105, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  or D-177.
- **Commit:** C-D178.

## D-179 — Record language-runtime-leftover-join.v4 as G14 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-179.review-adversarial.claude2.json`,
  `359fa159d4951c092d4aed376720e88fb41f479f7105cf38826e49787183d209`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-179.review-adversarial.codex.json`,
  `72795e292ece2b7a48a794ce82f8dd4963111e60c966133707e58cc8ce72e66d`)
  CONSENT. Subject `coordinator-decisions.D-179.draft.md`
  `1e530a63b6cec5723eb856874ae99874a2f144b28781bcb89e29ec07c9ee3242`.
  Frozen leftover-join
  `language-runtime-leftover-join.v4.json`
  `301904f0f5071d88c5d9b58a52a0125b0a99d3eead16a23f91479bcac1a34a2c`
  Stage A Claude ACCEPT
  `79b7be63d2126086f3e41057ebea4940355fef8ee88f0ecc3dbaabf7c6933f8f`
  0/0; Stage A Codex ACCEPT
  `b88bda527ba37218b65430c629a832e78083fa7bf2362bf972b0d6554c813227`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-runtime-leftover-join.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-178. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/language-runtime-leftover-join.v4.json`
  `301904f0f5071d88c5d9b58a52a0125b0a99d3eead16a23f91479bcac1a34a2c`.
- **Decision:** Record v4 as G14 leftover remasurement after
  D-178. The candidate binds NOTHING. DR-G14 stays `OPEN`.
  leftover-design of OBL-G14-FX-AUTHORING remains. Does not
  SATISFY DR-118. Does not reopen DR-119 SATISFIED. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Frozen v3 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. v3 stays frozen; do not record it as
  current. Does not invent fixture bytes, numeric
  thresholds, Rust-as-core, or a second slice-1 language
  role. Does not name G13 into required-now. Does not
  rewrite G14, G31, or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D179. Does not unwrite D-091, D-165, D-167,
  D-168, D-169, D-170, D-171, D-172, D-173, D-174, D-175,
  D-176, D-177, or D-178.
- **Commit:** C-D179.

## D-180 — Record packaging-leftover-join.v3 as DR-120 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-180.review-adversarial.claude2.json`,
  `a4ba44a937bf9c6a1272cddf1eb15a2388306b43ff72c7902601871cf15edc54`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-180.review-adversarial.codex.json`,
  `4f42ff54e91a7c2d2c4998259df6ff1855cd3f52601c09064302cb75bf873cb1`)
  CONSENT. Subject `coordinator-decisions.D-180.draft.md`
  `330ef62e11175defd4bdf4514bc99e770a7bd53f2b3321fd44171861087ab21c`.
  Frozen leftover-join
  `packaging-leftover-join.v3.json`
  `0bb1673e058be5325f82d47f6f8d688949afa24be1ba7d42b4bba57394450f15`
  Stage A Claude ACCEPT
  `ab326bc6867923d88a7ff2c2334e7c564f98389193fb7e95e2eb08c76ea6b2bd`
  0/0; Stage A Codex ACCEPT
  `2a08c655e62d66c273457fe1cb65b832fa955228c0ce0a38148fa4ccea246a13`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `packaging-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-179. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/packaging-leftover-join.v3.json`
  `0bb1673e058be5325f82d47f6f8d688949afa24be1ba7d42b4bba57394450f15`.
- **Decision:** Record v3 as DR-120 leftover remasurement
  after D-179. The candidate binds NOTHING. DR-120 stays
  `OPEN`. leftover-design of OBL-ADAPTER-IMPL and
  OBL-AT-FX-AUTHORING remains. D-056 Eligibility gates 2
  and 3 do not hold for DR-120. Gate 1 Class A is not
  opened. Not eligible in kind. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not apply component-packaging-contract.v14.
  Does not steal DR-103 leftover. Does not invent an adapter
  or AT fixture bytes. Does not rewrite G15, G31, or G32.
  Does not edit file 08. Does not invent a D9 code. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D180. Does not unwrite D-108, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, or D-179.
- **Commit:** C-D180.

## D-181 — Record monorepo-leftover-join.v3 as DR-121 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-181.review-adversarial.claude2.json`,
  `9f4a645147834db15264d3eb2c4be84874389392a324f6c287de72fcb5422611`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-181.review-adversarial.codex.json`,
  `4d1d66c333dcdee1ba50d36e1e9955d734597691dd01c6b8a9c694f3db08859c`)
  CONSENT. Subject `coordinator-decisions.D-181.draft.md`
  `34374a75e5c3db199e51c88c0896ce25a65e5c01d48a08624bca2f279401bd4c`.
  Frozen leftover-join
  `monorepo-leftover-join.v3.json`
  `08167a8534aebc6e0398076ed7bed690111399adcd6837e40336a4eb9ee40a70`
  Stage A Claude ACCEPT
  `5bbe591b28d5c83c326d793b20403e44f90786c25b3d5dc18833a113ee604108`
  0/0; Stage A Codex ACCEPT
  `3b5a9d1021fbe327be5a4d0f42c64e3636f6fdadc7129f12780befb1f1afad16`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `monorepo-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-180. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/monorepo-leftover-join.v3.json`
  `08167a8534aebc6e0398076ed7bed690111399adcd6837e40336a4eb9ee40a70`.
- **Decision:** Record v3 as DR-121 leftover remasurement
  after D-180. The candidate binds NOTHING. DR-121 stays
  `OPEN`. leftover-design of OBL-G16-FX-AUTHORING and
  OBL-CI-ENCODING-RESERVED remains. D-056 Eligibility gates 2
  and 3 do not hold for DR-121. Gate 1 Class A is not
  opened. Not eligible in kind. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not apply monorepo-ci-contract.v16. Does
  not steal DR-111, DR-118, or DR-127 leftover. Does not
  SATISFY DR-117. Does not execute EE-7e. Does not name
  G13 into required-now. Does not invent a CI encoding or
  fixture bytes. Does not rewrite G16, G31, or G32. Does
  not edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D181. Does not unwrite D-124, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, or D-180.
- **Commit:** C-D181.

## D-182 — Record sarif-leftover-join.v4 as DR-122 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-182.review-adversarial.claude2.json`,
  `2bca7b9a092faf4d193b4e74865efea694ec81535a52f8c1475a1722f6ecaf4b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-182.review-adversarial.codex.json`,
  `a90867672a82c0c40a6b05c407a150e8cb1b1db8c418d6ab9dc415285711e78b`)
  CONSENT. Subject `coordinator-decisions.D-182.draft.md`
  `fc85c24734bffa3561e7a2520a92c10c0171d37ac7bb5cc13d43282aa3c055b7`.
  Frozen leftover-join
  `sarif-leftover-join.v4.json`
  `a2ab59d79051337906ae610b4c34f8203dcac0d9038f2826b32f68630bd07640`
  Stage A Claude ACCEPT
  `4c97b5256573e90c5dfae5daf73b5dbbca3eb410cf496934c703cb86d3e05a32`
  0/0; Stage A Codex ACCEPT
  `a40256233503e84ddcbcfc610d82e0fde673c0666df9fa9a959696add1fb15c9`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `sarif-leftover-join.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-181. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/sarif-leftover-join.v4.json`
  `a2ab59d79051337906ae610b4c34f8203dcac0d9038f2826b32f68630bd07640`.
- **Decision:** Record v4 as DR-122 leftover remasurement
  after D-181. The candidate binds NOTHING. DR-122 stays
  `PROPOSED-CLOSED-FOR-REVIEW`. leftover-design of
  OBL-FC-OUTFAIL-FX and OBL-FC-NONAUTH-TERM-FX remains.
  D-056 Eligibility gates 2 and 3 do not hold for DR-122.
  Gate 1 Class A is not opened. Not eligible in kind. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v3 remains a historical measurement as of
  HEAD `5d5d778` / required-now 26. v3 stays frozen; do
  not record it as current. Does not apply
  sarif-projection-contract.v15. Does not advertise SARIF.
  Does not resurrect G17. Does not mint a D9 code. Does
  not steal G26 leftover from DR-131. Does not invent
  fixture bytes. Does not rewrite G26, G31, or G32. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D182. Does not unwrite D-077, D-115, D-167,
  D-168, D-169, D-170, D-171, D-172, D-173, D-174, D-175,
  D-176, D-177, D-178, D-179, D-180, or D-181.
- **Commit:** C-D182.

## D-183 — Record state-class-leftover-join.v3 as DR-124 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-183.review-adversarial.claude2.json`,
  `3e513f3cd9f2e226f1770b79d5d47ee347a96f2208267327f7e80b30e7f9db2f`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-183.review-adversarial.codex.json`,
  `ed3af4a8024f50f2430e80fb2926b651e9710a3536be58e333193deeff503b0d`)
  CONSENT. Subject `coordinator-decisions.D-183.draft.md`
  `d4bc49ae2fe21b83535c897ea344f1321c964d43d9f935e51a8c317f0faed927`.
  Frozen leftover-join
  `state-class-leftover-join.v3.json`
  `3313d6af45f5c84d9d4bfb99df2bd90b5cb51b7dd94f88207746868bcb8ec2bd`
  Stage A Claude ACCEPT
  `c53629d95ab56824adfd0b553f71d72ba2687ea2ac3649b877ebf077f0d539ac`
  0/0; Stage A Codex ACCEPT
  `3dcdc66ccb6671cabd0931ea0f54d059ae194b85b461024e69544056911bef0e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `state-class-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-182. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/state-class-leftover-join.v3.json`
  `3313d6af45f5c84d9d4bfb99df2bd90b5cb51b7dd94f88207746868bcb8ec2bd`.
- **Decision:** Record v3 as DR-124 leftover remasurement
  after D-182. The candidate binds NOTHING. DR-124 stays
  `OPEN`. leftover-design of OBL-G19-FX-AUTHORING,
  OBL-GRANT-JOURNAL, OBL-INHERIT-BLOCKED, and OBL-MONOTONIC
  remains. D-056 Eligibility gates 2 and 3 do not hold for
  DR-124. Gate 1 Class A is not opened. Not eligible in
  kind. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Frozen v2 remains a historical measurement
  as of HEAD `5d5d778` / required-now 26. v2 stays frozen;
  do not record it as current. Does not apply
  state-class-contract.v11. Does not apply
  SUP-124-GRANT-JOURNAL. Does not invent a grant journal or
  fixture bytes. Does not rewrite G19, G31, or G32. Does
  not edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D183. Does not unwrite D-117, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, or D-182.
- **Commit:** C-D183.

## D-184 — Record sdk-leftover-join.v5 as DR-125 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-184.review-adversarial.claude2.json`,
  `cc03a4f725b51430825354f39fca0272fd75de30291b66910099721e3854bc7e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-184.review-adversarial.codex.json`,
  `298b2da11f21c3172933b4e91ee556f781329f9fc02faaecdf142ced82b7f8d3`)
  CONSENT. Subject `coordinator-decisions.D-184.draft.md`
  `f66fd2254b51fc4df0b6da701725fad582e7587b4f8b1899230c5a601dff124c`.
  Frozen leftover-join
  `sdk-leftover-join.v5.json`
  `6f73376e93e7e84849ff6bc2de26c9fc88a53438ad2929dbe427b87f3125d187`
  Stage A Claude ACCEPT
  `ee946657727b6c5a0b26b391be9ed7cbee199fa66f58343cd75d7f852ea93fc8`
  0/0; Stage A Codex ACCEPT
  `fec4c9d1d22b0ed7dc82eb1e61ad0c1e90f27264250751f527768d29034e0935`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `sdk-leftover-join.v5.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-183. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/sdk-leftover-join.v5.json`
  `6f73376e93e7e84849ff6bc2de26c9fc88a53438ad2929dbe427b87f3125d187`.
- **Decision:** Record v5 as DR-125 leftover remasurement
  after D-183. The candidate binds NOTHING. DR-125 stays
  `OPEN`. leftover-design of OBL-G20-FX-AUTHORING and
  OBL-SDK-API-RESERVED remains. D-056 Eligibility gates 2
  and 3 do not hold for DR-125. Gate 1 Class A is not
  opened. Not eligible in kind. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v4 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v4 stays frozen; do not record it as
  current. Does not apply component-sdk-contract.v4. Does
  not invent an SDK API or fixture bytes. Does not steal
  DR-118 leftover. Does not rewrite G20, G31, or G32. Does
  not edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D184. Does not unwrite D-110, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, or D-183.
- **Commit:** C-D184.

## D-185 — Record platform-tcb-leftover-join.v6 as DR-126 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-185.review-adversarial.claude2.json`,
  `05e03e941b3ac48c3420e22a2fc5d8998fb36df0fa73e4ed1e293658226f28b3`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-185.review-adversarial.codex.json`,
  `3c7205663c007219649740901e1aab31bbd8a84f6ae83fccc70565e0201f67b0`)
  CONSENT. Subject `coordinator-decisions.D-185.draft.md`
  `92c15295248d0cb03b5f2983b43c28a8ab1678846458f5668b3e84a01bac9b07`.
  Frozen leftover-join
  `platform-tcb-leftover-join.v6.json`
  `c799f4d7f4dc5206b777e82da934ef8812bc11c87f3edc10d234ceaf8fba79b4`
  Stage A Claude ACCEPT
  `c5bb993040a68e7ed772f061453ca75ffad0d94b440f32399f0c9864cc3f3a01`
  0/0; Stage A Codex ACCEPT
  `997d5654bc3cbb09cffbcd0d4724934f457e2aff617cff91f44d64d6086d56da`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `platform-tcb-leftover-join.v6.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-184. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/platform-tcb-leftover-join.v6.json`
  `c799f4d7f4dc5206b777e82da934ef8812bc11c87f3edc10d234ceaf8fba79b4`.
- **Decision:** Record v6 as DR-126 leftover remasurement
  after D-184. The candidate binds NOTHING. DR-126 stays
  `OPEN`. leftover-design of OBL-G22-FX-AUTHORING and
  OBL-RESERVED-TABLES remains. D-056 Eligibility gates 2
  and 3 do not hold for DR-126. Gate 1 Class A is not
  opened. Not eligible in kind. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v5 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v5 stays frozen; do not record it as
  current. Does not apply platform-tcb-contract.v45. Does
  not populate a TCB table. Does not invent fixture bytes.
  Does not rewrite G22, G31, or G32. Does not edit file 08.
  Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D185. Does not unwrite D-125, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, D-183, or
  D-184.
- **Commit:** C-D185.

## D-186 — Record anti-lockstep-leftover-join.v3 as DR-127 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-186.review-adversarial.claude2.json`,
  `0885c3b75380fec59689724abdf4712137a968fb4482b7f32176e27c811d81b2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-186.review-adversarial.codex.json`,
  `339489219abb11b76be2dc0564dbc52f764d170641311ed98d4452ce878f0b11`)
  CONSENT. Subject `coordinator-decisions.D-186.draft.md`
  `3c4ed227813fa7216f1bf163fc0974c20ed426558fea5cd3b9bd0c1482383e8d`.
  Frozen leftover-join
  `anti-lockstep-leftover-join.v3.json`
  `820d724a10a1e11a2188a323a3425cd13f4c483892bb487fb93f6542103c85e1`
  Stage A Claude ACCEPT
  `6e4cf33fa6771047287a6fe3d0e1cd53e23c2c91199d0391f9451cf73552a062`
  0/0; Stage A Codex ACCEPT
  `02c16e8d7f9ce487c7064b4012c5710c8745dff451dd7dcde9ade1a88999843d`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `anti-lockstep-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-185. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/anti-lockstep-leftover-join.v3.json`
  `820d724a10a1e11a2188a323a3425cd13f4c483892bb487fb93f6542103c85e1`.
- **Decision:** Record v3 as DR-127 leftover remasurement
  after D-185. The candidate binds NOTHING. DR-127 stays
  `OPEN`. leftover-design of OBL-HOSTILE-GOLDENS,
  OBL-AL3-CORE-ROLLBACK, and OBL-AL1-AL2-AL5 remains.
  CLAUDE-V7-A-1 travels as honesty work and is not
  discharged. D-056 Eligibility gates 2 and 3 do not hold
  for DR-127. Gate 1 Class A is not opened. Not eligible
  in kind. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. Frozen v2 is the ALJ-V2-SF1 REJECT, not
  current. v2 stays frozen; do not record it as current.
  Does not apply anti-lockstep-contract.v7. Does not author
  hostile dual-channel goldens. Does not invent numeric
  windows. Does not steal G21 leftover from DR-114. Does
  not rewrite G21, G31, or G32. Does not edit file 08.
  Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D186. Does not unwrite D-111, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, D-183, D-184,
  or D-185.
- **Commit:** C-D186.

## D-187 — Record provider-leftover-join.v3 as G10 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-187.review-adversarial.claude2.json`,
  `63814410c2b28c569987aa072e0a92ae9858a1a9576d1c0e3a61d857fd5f1057`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-187.review-adversarial.codex.json`,
  `99bf3da40121ef55df04b32ce18f376ba02eba9c8610810fd0b75be653d36773`)
  CONSENT. Subject `coordinator-decisions.D-187.draft.md`
  `2785fed4784ddb64254b8c84f99acd7ace5a03ecfda852099e793a6e74d52337`.
  Frozen leftover-join
  `provider-leftover-join.v3.json`
  `951ad9776056ecd4ea1f40e6bb503d78b3c90b43e2bb96311962b8725c28a576`
  Stage A Claude ACCEPT
  `1558dab9f2a60be220ca67a85f04974cb6821861a87ed5fefa1799466edf94ed`
  0/0; Stage A Codex ACCEPT
  `820b00534a97521feca033fe2297093af6040a68ccb4d886af08cb0d6dac87fd`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `provider-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-186. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/provider-leftover-join.v3.json`
  `951ad9776056ecd4ea1f40e6bb503d78b3c90b43e2bb96311962b8725c28a576`.
- **Decision:** Record v3 as G10 leftover remasurement after
  D-186. The candidate binds NOTHING. DR-G10 stays
  `HARD-BLOCKED pending selector refresh`. leftover-design
  of OBL-G10-FX-AUTHORING and OBL-SELECTOR-REFRESH remains.
  Does not SATISFY DR-102 a second time. Does not reopen
  DR-102 SATISFIED. Does not steal DR-133 leftover. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Frozen v2 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent a D9 code or selector. Does not
  rewrite G10, G31, or G32. Does not edit file 08. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D187. Does not unwrite D-085, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, D-183, D-184,
  D-185, or D-186.
- **Commit:** C-D187.

## D-188 — Record g08-leftover-join.v3 as G08 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-188.review-adversarial.claude2.json`,
  `c7bc18fd76c690acfbf8fecf5e6f52ad8dd048e0b8f65769c57c02d19e229ace`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-188.review-adversarial.codex.json`,
  `617c36f2614335c50c0bbf650ace06cddc5752e5a6f792b5a9eb6023ad51f363`)
  CONSENT. Subject `coordinator-decisions.D-188.draft.md`
  `90bee1d5bf74443b5f37cad53da90c711a947fa7a1bbf6798e964cce2bc92e74`.
  Frozen leftover-join
  `g08-leftover-join.v3.json`
  `d7a194c5bc743a6dfd01a6196377d8e63b4dc7aea61f4d48dc40d79e90013e87`
  Stage A Claude ACCEPT
  `3f117380bccc934bbd089fa17950fab150a6d76460623d2816b6a617a0af4747`
  0/0; Stage A Codex ACCEPT
  `74796baf9629620e6cc4a8dea1ab8238cb0d28add3a3f643a180175bf1b6cd72`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g08-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-187. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g08-leftover-join.v3.json`
  `d7a194c5bc743a6dfd01a6196377d8e63b4dc7aea61f4d48dc40d79e90013e87`.
- **Decision:** Record v3 as G08 leftover remasurement after
  D-187. The candidate binds NOTHING. DR-G08 stays `OPEN`.
  leftover-design of OBL-G08-FX-AUTHORING remains. Does not
  SATISFY DR-112. Does not steal OBL-RESERVED-NUMBERS.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or reserved
  numbers. Does not rewrite G08, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D188. Does not unwrite D-105, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, D-183, D-184,
  D-185, D-186, or D-187.
- **Commit:** C-D188.

## D-189 — Record g09-leftover-join.v10 as G09 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-189.review-adversarial.claude2.json`,
  `110442004e76c1028b2d6eefe7eb0f6dc6bc94a6a6f4f7c6c69bc24cb09548bc`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-189.review-adversarial.codex.json`,
  `21a367abc7fd180664df4518fbb81635b3cca6958adaa86a087264bbe1765deb`)
  CONSENT. Subject `coordinator-decisions.D-189.draft.md`
  `c3e82acfc1a585cd126788ae23e766fba16b007cbef7fe3c1a3a3fba4418b2c6`.
  Frozen leftover-join
  `g09-leftover-join.v10.json`
  `98cf4849da2aad1f700c4a8ba39b76a505f86a82137ce28f3469c4ffbe16b8c9`
  Stage A Claude ACCEPT
  `d4119330bf528b191f953583fb19ac59bfe03b58cd7a5a7b3b123af51db3b91b`
  0/0; Stage A Codex ACCEPT
  `2064220bdc2ece2450a4234b671ed56593fd862f2d06d3cec5b31f19dd0cf9fa`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g09-leftover-join.v10.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-188. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g09-leftover-join.v10.json`
  `98cf4849da2aad1f700c4a8ba39b76a505f86a82137ce28f3469c4ffbe16b8c9`.
- **Decision:** Record v10 as G09 leftover remasurement after
  D-188. The candidate binds NOTHING. DR-G09 stays `OPEN`.
  leftover-design of OBL-FX-AUTHORING remains. Does not
  SATISFY DR-105. Does not steal DR-114 leftover. Does not
  fold R-10 or R-6 into the fourteen FX. Gate 1 Class A
  is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v3 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. v3 through v9 stay frozen; do not
  record them as current. Does not invent fixture bytes
  or a decision-record envelope. Does not rewrite G09,
  G31, or G32. Does not edit file 08. Does not invent a
  D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D189. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, or D-188.
- **Commit:** C-D189.

## D-190 — Record g12-leftover-join.v3 as G12 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-190.review-adversarial.claude2.json`,
  `8ceb00931b801741f41b6bf6268baab39b9e790a30a27dfa869d55c2859e1db7`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-190.review-adversarial.codex.json`,
  `23fc8b6803b53672067fcbf13e67ab58729761b70f63b34942d73d2fcfe17079`)
  CONSENT. Subject `coordinator-decisions.D-190.draft.md`
  `c565df6bc23eb6f748497ee634a36a47ba1a95f6d68196e0f4866247777bf1af`.
  Frozen leftover-join
  `g12-leftover-join.v3.json`
  `11ebaf973b57ebf9d4b8da931ef0f66a0f299732c13a42e524d0f1f8a609a50a`
  Stage A Claude ACCEPT
  `7f7b60f0b4c7b0ec760decd04429aa046fd2adeb3f4b9290e5478b3c1f74b7c7`
  0/0; Stage A Codex ACCEPT
  `7eb99fe6a92927dfeaf3a0446bd7eecc888d1805eb433be6be694a56659dd0ef`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g12-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-189. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g12-leftover-join.v3.json`
  `11ebaf973b57ebf9d4b8da931ef0f66a0f299732c13a42e524d0f1f8a609a50a`.
- **Decision:** Record v3 as G12 leftover remasurement after
  D-189. The candidate binds NOTHING. DR-G12 stays `OPEN`.
  leftover-design of OBL-DOCTOR-FX-AUTHORING remains. Does
  not SATISFY DR-114. Does not steal DR-114 leftover. Gate
  1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or a D9 code.
  Does not rewrite G12, G31, or G32. Does not edit file
  08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D190. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, or D-189.
- **Commit:** C-D190.

## D-191 — Record g15-leftover-join.v3 as G15 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-191.review-adversarial.claude2.json`,
  `3ccf9d8f0fdcbda315c3f1d0bddfc758d765f67e86f02f28d6ecebbe22b52229`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-191.review-adversarial.codex.json`,
  `93185a1b30d6a4854daa4c2a240ea071cc27566634190400250c1a82350ad8c3`)
  CONSENT. Subject `coordinator-decisions.D-191.draft.md`
  `a293efd5a147c5eef77af0887120da2ab6c0b781c7fc034750ce22dfb41db500`.
  Frozen leftover-join
  `g15-leftover-join.v3.json`
  `31d37bb0dd08bd96f28a976bda803174c518e75ddec80ba64b6bab740e7e3041`
  Stage A Claude ACCEPT
  `d5066b45f417f874417cb8d2084c01a616ec285154458a91b60ead1197b0ce81`
  0/0; Stage A Codex ACCEPT
  `b064bbbd7ee3d782b0f59bdba4cd6e53524fc3c1b1785e4bcc7b90179e18ac39`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g15-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-190. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g15-leftover-join.v3.json`
  `31d37bb0dd08bd96f28a976bda803174c518e75ddec80ba64b6bab740e7e3041`.
- **Decision:** Record v3 as G15 leftover remasurement after
  D-190. The candidate binds NOTHING. DR-G15 stays `OPEN`.
  leftover-design of OBL-AT-FX-AUTHORING remains. Does not
  SATISFY DR-120. Does not SATISFY DR-103. Does not steal
  DR-120 or DR-103 leftover. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Frozen v2 remains a historical measurement as of
  HEAD `5d5d778` / required-now 26. v2 stays frozen; do not
  record it as current. Does not invent fixture bytes, an
  adapter implementation, a numeric threshold, or an
  envelope. Does not rewrite G15, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D191. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, or D-190.
- **Commit:** C-D191.

## D-192 — Record g16-leftover-join.v3 as G16 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-192.review-adversarial.claude2.json`,
  `5d1d173f6692d2bd635e6327949d7d9105bc76a7b7affcddb1565e692c40265c`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-192.review-adversarial.codex.json`,
  `f0f1946d034d33d9d73170d15a29ac0e8c4c064f5fe1592b4df20026a4d5374a`)
  CONSENT. Subject `coordinator-decisions.D-192.draft.md`
  `5a1a6c88e513302215fd0cf0e85927f0797bf046b3b0137ba43857af58b54f05`.
  Frozen leftover-join
  `g16-leftover-join.v3.json`
  `bc87c6b342195a29bd582aa0b48973e5e8e1f76f4bca717d13578c2b2fc181f6`
  Stage A Claude ACCEPT
  `cda15f7d914a1781fdf4afb227871bba8b9d49156e09a5b0b6211b6ec7dbca75`
  0/0; Stage A Codex ACCEPT
  `9bf5f0c04107c06e59850f1fd8d965289af24dfa8b0d8efeb47d6e28004a99c7`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g16-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-191. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g16-leftover-join.v3.json`
  `bc87c6b342195a29bd582aa0b48973e5e8e1f76f4bca717d13578c2b2fc181f6`.
- **Decision:** Record v3 as G16 leftover remasurement after
  D-191. The candidate binds NOTHING. DR-G16 stays `OPEN`.
  leftover-design of OBL-G16-FX-AUTHORING remains. Does not
  SATISFY DR-121. Does not steal OBL-CI-ENCODING-RESERVED.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or reserved CI
  encodings. Does not rewrite G16, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D192. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, or D-191.
- **Commit:** C-D192.

## D-193 — Record g18-leftover-join.v4 as G18 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-193.review-adversarial.claude2.json`,
  `8a3baa6435fa149947dca98eb2a89ab473877a5a597e83aaed0129d50b24291e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-193.review-adversarial.codex.json`,
  `bc28130d54325a09266e2656164aabfa47b7dd9055e780a48105f07802a5fe91`)
  CONSENT. Subject `coordinator-decisions.D-193.draft.md`
  `6e97053447570d4336c65ad2cecff6b405d54aec84bf87fe9f46fc9725dbd8f0`.
  Frozen leftover-join
  `g18-leftover-join.v4.json`
  `f18f08bcb360a68b76e08330b716129a69193a3d91a8e2623f0a396ecba33228`
  Stage A Claude ACCEPT
  `646897da1ff53d1725507d2d1bffa816f8be2012fde69e2485700939a71825c8`
  0/0; Stage A Codex ACCEPT
  `d736e82e2fa7e518445ff5bb97484bfee2d385df7b49a28e711d21cf94f93619`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g18-leftover-join.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-192. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g18-leftover-join.v4.json`
  `f18f08bcb360a68b76e08330b716129a69193a3d91a8e2623f0a396ecba33228`.
- **Decision:** Record v4 as G18 leftover remasurement after
  D-192. The candidate binds NOTHING. DR-G18 stays `OPEN`.
  leftover-design of OBL-G18-FX-AUTHORING remains. Does not
  SATISFY DR-107. Does not steal OBL-ENCODING-RESERVED.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v3 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v3 stays frozen; do not record it as
  current. Does not invent fixture bytes or a journal.
  Does not rewrite G18, G31, or G32. Does not edit file
  08. Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D193. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, or D-192.
- **Commit:** C-D193.

## D-194 — Record g19-leftover-join.v3 as G19 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-194.review-adversarial.claude2.json`,
  `06502dc27ed31b2b208674571b413b4a4ab15a23389381d9ac3282d14c881ac6`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-194.review-adversarial.codex.json`,
  `231c5bbb8c52dc79d29c82e8340b3749f5c5c5f563ff34bbc5bc91883d942599`)
  CONSENT. Subject `coordinator-decisions.D-194.draft.md`
  `9fcde889657e8513264440baaff286cdab4ae72971f39ffaa64c17ffa12eee58`.
  Frozen leftover-join
  `g19-leftover-join.v3.json`
  `8b2fe8447cd87025d301afdab885b12dc33e87043623876b849bdae26bfb4748`
  Stage A Claude ACCEPT
  `54be6c2939e237fb5e676e7c5db687266f20b98d501383ff6d62872fd70fad82`
  0/0; Stage A Codex ACCEPT
  `3dbe0329d830378e15b34ba66c0daa75ea54b0fa615a7dabcc6292a6fafc4746`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g19-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-193. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g19-leftover-join.v3.json`
  `8b2fe8447cd87025d301afdab885b12dc33e87043623876b849bdae26bfb4748`.
- **Decision:** Record v3 as G19 leftover remasurement after
  D-193. The candidate binds NOTHING. DR-G19 stays `OPEN`.
  leftover-design of OBL-G19-FX-AUTHORING remains. Does not
  SATISFY DR-124. Does not steal OBL-GRANT-JOURNAL,
  OBL-INHERIT-BLOCKED, or OBL-MONOTONIC. Gate 1 Class A is
  not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v2 remains a
  historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or a grant-journal.
  Does not rewrite G19, G31, or G32. Does not edit file
  08. Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D194. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, or
  D-193.
- **Commit:** C-D194.

## D-195 — Record g20-leftover-join.v3 as G20 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-195.review-adversarial.claude2.json`,
  `d9e758465980c37d4028918f8955c8db23d6653bc705b90d6bf1ea63a9413868`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-195.review-adversarial.codex.json`,
  `f968b54daeffe57a4c03f256aeca3de7a2ae2fa80764308dbcb58d0bcc75e289`)
  CONSENT. Subject `coordinator-decisions.D-195.draft.md`
  `ef35fbf09851e26db4d4b1d8b89fbe6523185acf739e69b38f364619ebcec6b8`.
  Frozen leftover-join
  `g20-leftover-join.v3.json`
  `1a04325f648b2cede73e932fb5083867dea4de57c1484b89ece8a983225f2617`
  Stage A Claude ACCEPT
  `18ade8fa5f6d757612c166e9be6360551a1c335eb5d6ae7fd5d1ac6aab4df614`
  0/0; Stage A Codex ACCEPT
  `6160f479d17a5e6d5f06ea7b174c1913aa8f5e9e876e8914b53d89fcc3dc1870`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g20-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-194. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g20-leftover-join.v3.json`
  `1a04325f648b2cede73e932fb5083867dea4de57c1484b89ece8a983225f2617`.
- **Decision:** Record v3 as G20 leftover remasurement after
  D-194. The candidate binds NOTHING. DR-G20 stays `OPEN`.
  leftover-design of OBL-G20-FX-AUTHORING remains. Does not
  SATISFY DR-125. Does not steal OBL-SDK-API-RESERVED. Gate
  1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes or reserved SDK
  APIs. Does not rewrite G20, G31, or G32. Does not edit
  file 08. Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D195. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  or D-194.
- **Commit:** C-D195.

## D-196 — Record g21-leftover-join.v4 as G21 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-196.review-adversarial.claude2.json`,
  `01f45038beedfc1c6877811b1a34317e522090a0e931a16ff322c49351918754`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-196.review-adversarial.codex.json`,
  `b1dd78c5fd270a9225d294e9cdc0ac4b2d31316daa4735bfd5834b1b91cc4669`)
  CONSENT. Subject `coordinator-decisions.D-196.draft.md`
  `d8154cab5819a67267c6fc484c7933971eb4c80b3fd370b7f7122e603fa4f262`.
  Frozen leftover-join
  `g21-leftover-join.v4.json`
  `b8696fd134550a9ad15d44a07adcc4030aad3702013cc9de914bbab5b8e74ae4`
  Stage A Claude ACCEPT
  `24fce2ddcb885b56323e27af767ba9a628713384aef8dc3149d94e64344726bb`
  0/0; Stage A Codex ACCEPT
  `406337e883ee6d66817849204bf616a988101724f8a4edcfad308004f8e0b59f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-leftover-join.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-195. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g21-leftover-join.v4.json`
  `b8696fd134550a9ad15d44a07adcc4030aad3702013cc9de914bbab5b8e74ae4`.
- **Decision:** Record v4 as G21 leftover remasurement after
  D-195. The candidate binds NOTHING. DR-G21 stays `OPEN`.
  leftover-design of OBL-G21-FX-AUTHORING remains. Does not
  SATISFY DR-114. Does not reopen DR-102 SATISFIED. Does not
  steal OBL-DOCTOR-FX-AUTHORING, OBL-JOIN-FX-AUTHORING,
  OBL-JOIN-FX-EXECUTION, OBL-FC-C1, or OBL-BLK-1..4. Gate
  1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. Frozen v3 remains dual REJECT 0/1
  G21LJ-V3-SF1. v1, v2, and v3 stay frozen; do not record
  them as current. Does not invent fixture bytes or a D9
  code. Does not rewrite G21, G31, or G32. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D196. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, or D-195.
- **Commit:** C-D196.

## D-197 — Record g22-leftover-join.v3 as G22 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-197.review-adversarial.claude2.json`,
  `7675ae93dba8bad6295eca8997865d163899bf4de345fa47011b56c27220f022`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-197.review-adversarial.codex.json`,
  `4731ef8073637ee1cb79357cba5ca6f2c5616aea02b0a82344483118b407a03a`)
  CONSENT. Subject `coordinator-decisions.D-197.draft.md`
  `9a53973a38f834a557a85213ca1ea1711e850e4a89fe54e524f8295baadd94d1`.
  Frozen leftover-join
  `g22-leftover-join.v3.json`
  `b251605c06dbbeaa0c791ec4874c5b394b186f1858515e9a8af6cc10401bdbbb`
  Stage A Claude ACCEPT
  `f960cfdf9ecb598aefdf2c62e58e44d0dd393b288e0c0601a9b4353c20d38c82`
  0/0; Stage A Codex ACCEPT
  `e8993a247722816716e32f4d571783c11ef2ed91a9eed315eae10433e6c34ee6`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g22-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-196. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g22-leftover-join.v3.json`
  `b251605c06dbbeaa0c791ec4874c5b394b186f1858515e9a8af6cc10401bdbbb`.
- **Decision:** Record v3 as G22 leftover remasurement after
  D-196. The candidate binds NOTHING. DR-G22 stays `OPEN`.
  leftover-design of OBL-G22-FX-AUTHORING remains. Does not
  SATISFY DR-126. Does not steal OBL-RESERVED-TABLES. Gate
  1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical measurement as of HEAD `5d5d778` /
  required-now 26. v2 stays frozen; do not record it as
  current. Does not invent fixture bytes, populate reserved
  TCB tables, or invent Rosetta. Does not rewrite G22, G31,
  or G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D197. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, or D-196.
- **Commit:** C-D197.

## D-198 — Record g23-leftover-join.v4 as G23 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-198.review-adversarial.claude2.json`,
  `43c5c72715ae4f7557f7cc785b190e415e0ebac95238b4bb5e7a216c08b4f15c`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-198.review-adversarial.codex.json`,
  `c23a445334307d1141166391968a79ea5fca33e9404a403f7447cc90e208a353`)
  CONSENT. Subject `coordinator-decisions.D-198.draft.md`
  `2860f9c1a277b7733eb0abc16bbce94e360f45779ecfce82d7ac468bf13b83b6`.
  Frozen leftover-join
  `g23-leftover-join.v4.json`
  `a542dc6b023d07cf8657c76909ded1641efd29277760308d52574fa706fad56e`
  Stage A Claude ACCEPT
  `fde540a9658c750ed5868146258771a79108e18359f3847695a95d76bba6dac8`
  0/0; Stage A Codex ACCEPT
  `5c0e12686215c30d229db438ae300373b477772808629bedf91c46fe73050fa6`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g23-leftover-join.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-197. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g23-leftover-join.v4.json`
  `a542dc6b023d07cf8657c76909ded1641efd29277760308d52574fa706fad56e`.
- **Decision:** Record v4 as G23 leftover remasurement after
  D-197. The candidate binds NOTHING. DR-G23 stays `OPEN`.
  leftover-design of OBL-G23-FX-AUTHORING remains. Does not
  SATISFY DR-133. Does not reopen leftover-design of NT-3
  or NT-5. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v3 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v1, v2, and v3 stay frozen; do not
  record them as current. Does not invent fixture bytes or
  NT-1/2/4/6/7/8 as G23 classes. Does not rewrite G23, G31,
  or G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D198. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, or D-197.
- **Commit:** C-D198.

## D-199 — Record g24-leftover-join.v3 as G24 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-199.review-adversarial.claude2.json`,
  `22b403a635e8b8b30d5a72fc8a3b9b48e796c2214f0658da4ddf2c19d1461a7a`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-199.review-adversarial.codex.json`,
  `a8b1b004f200695d5fdd6b43a94257455c5dbe92ca2195e170388a9ec51afa63`)
  CONSENT. Subject `coordinator-decisions.D-199.draft.md`
  `9aa97895f46adedb727538103a52e0ad3fbaf06fe0ccb6b51807b98b5eea040e`.
  Frozen leftover-join
  `g24-leftover-join.v3.json`
  `c4fa464802f6075de8054a93f10fbc0b80e2bade6d04e510c2fecc52cf8b0f72`
  Stage A Claude ACCEPT
  `f677748458a17b9906bce118dd57e86fbef71b28a551e80b76df670063b2ca9c`
  0/0; Stage A Codex ACCEPT
  `a8ec79ad4789ea126229f00e5d1eaabe34a6462ac2e7c0517884ba0722c4734f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g24-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-198. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g24-leftover-join.v3.json`
  `c4fa464802f6075de8054a93f10fbc0b80e2bade6d04e510c2fecc52cf8b0f72`.
- **Decision:** Record v3 as G24 leftover remasurement after
  D-198. The candidate binds NOTHING. DR-G24 stays `OPEN`.
  leftover-design of OBL-G24-FX-AUTHORING remains. Does not
  SATISFY DR-131. Does not reopen leftover-design of NT-1
  or NT-2. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v1 and v2 stay frozen; do not record
  them as current. Does not invent fixture bytes, a pack
  IR, or a section 7.1 recipe. Does not rewrite G24, G31,
  or G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D199. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, or D-198.
- **Commit:** C-D199.

## D-200 — Record g25-leftover-join.v3 as G25 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-200.review-adversarial.claude2.json`,
  `4844f9e613eb3d5b08a9641e3ea94e98c29d68cf1657b212a98b7021d2aec8f4`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-200.review-adversarial.codex.json`,
  `0f451148b1c6acb6cb1439ee4976c8f5e3ca4a5555d8afd675c47115f6b6abf3`)
  CONSENT. Subject `coordinator-decisions.D-200.draft.md`
  `b3e0c9ef5b4828923b3a77a3ac936ca2d39805f80cc6c6262e2359e280019784`.
  Frozen leftover-join
  `g25-leftover-join.v3.json`
  `df038663c9911cf13a3c1b078eabf54863fe18a1f85d956668ae3ac08662f4db`
  Stage A Claude ACCEPT
  `1fcee8700b41d9ab1e39467f8af45c90e4ec6ebb984e0aa47afbb6c49fb04700`
  0/0; Stage A Codex ACCEPT
  `6de6fbc773182f127d1b0e052d1b3d0a1918b9b57172aacf1b37c5d4d95523e6`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g25-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-199. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g25-leftover-join.v3.json`
  `df038663c9911cf13a3c1b078eabf54863fe18a1f85d956668ae3ac08662f4db`.
- **Decision:** Record v3 as G25 leftover remasurement after
  D-199. The candidate binds NOTHING. DR-G25 stays `OPEN`.
  leftover-design of OBL-G25-FX-AUTHORING remains. Does not
  SATISFY DR-131. Does not take over G23. Does not collapse
  the two NT-3 cells. Does not reopen leftover-design of
  DR-131 NT-3. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v1 and v2 stay frozen; do not record
  them as current. Does not invent fixture bytes. Does not
  rewrite G25, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D200. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, or D-199.
- **Commit:** C-D200.

## D-201 — Record g26-leftover-join.v3 as G26 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-201.review-adversarial.claude2.json`,
  `4b0c921b173c870d9a4c4a958b4e2a3fbfc1024a589e318a0516a3f3a638e066`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-201.review-adversarial.codex.json`,
  `07f8d661e6bcbc7b26b4a726659af43a12713b7017a9933ff0b7be9738f4fb0b`)
  CONSENT. Subject `coordinator-decisions.D-201.draft.md`
  `88978113741e316747110b0fadacc1d43fc36372d15df32133947dced44fc732`.
  Frozen leftover-join
  `g26-leftover-join.v3.json`
  `b02b7a7a7e82ccd2cf6887df37840b407e7ab9b420f5f3326569ef7ec6a0a7ab`
  Stage A Claude ACCEPT
  `fcdadaed2d1a4d353e1752d5cef5e59b8d7b71e239d19ee2df5fd31b5d01f29a`
  0/0; Stage A Codex ACCEPT
  `6ffdb5599c2756aa2dd8423629a4d4ac44dcde7fada52cbc6c34da0ad63c6176`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g26-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-200. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g26-leftover-join.v3.json`
  `b02b7a7a7e82ccd2cf6887df37840b407e7ab9b420f5f3326569ef7ec6a0a7ab`.
- **Decision:** Record v3 as G26 leftover remasurement after
  D-200. The candidate binds NOTHING. DR-G26 stays `OPEN`.
  leftover-design of OBL-G26-FX-AUTHORING remains. Does not
  SATISFY DR-131. Does not restore G17. Does not reopen
  leftover-design of DR-131 NT-5. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v2 remains a historical
  measurement as of HEAD `5d5d778` / required-now 26. v1
  and v2 stay frozen; do not record them as current. Does
  not invent fixture bytes or a SARIF advertisement. Does
  not rewrite G26, G31, or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D201. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, or D-200.
- **Commit:** C-D201.

## D-202 — Record g27-leftover-join.v3 as G27 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-202.review-adversarial.claude2.json`,
  `891e93523b18970b9843330eeba22eb8b5427719e59d63c8c60a103a3a60a4b7`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-202.review-adversarial.codex.json`,
  `4b7d24c18eef08eb00bbd1e3c83f2700e777d8cf1d9c3519c90634a20ae70029`)
  CONSENT. Subject `coordinator-decisions.D-202.draft.md`
  `c3c6f43024ede5b9a03e64d0c508fd6ac79fcab80656abd5c458987dbf95208b`.
  Frozen leftover-join
  `g27-leftover-join.v3.json`
  `38c48e49bb02db824d216115821fbb8ce08cfacfbfa5da902f08912081d8a88d`
  Stage A Claude ACCEPT
  `82d0369e17c95ec2de53c8d5501337b49434a65a46ae39ed01acb1889d4ebfa9`
  0/0; Stage A Codex ACCEPT
  `290dd425e0b74a7df69e7cbddec4f75d0d14718bc1abd1ca750e35b1330022dd`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g27-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-201. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g27-leftover-join.v3.json`
  `38c48e49bb02db824d216115821fbb8ce08cfacfbfa5da902f08912081d8a88d`.
- **Decision:** Record v3 as G27 leftover remasurement after
  D-201. The candidate binds NOTHING. DR-G27 stays `OPEN`.
  leftover-design of OBL-G27-FX-AUTHORING remains. Does not
  SATISFY DR-131. Does not invent a sealed-Run class. Does
  not take over G19. Does not reopen leftover-design of
  DR-131 NT-6. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v1 and v2 stay frozen; do not record
  them as current. Does not invent fixture bytes. Does not
  rewrite G27, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D202. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, or
  D-201.
- **Commit:** C-D202.

## D-203 — Record g28-leftover-join.v3 as G28 leftover remasurement

- **Date:** 2026-08-21
- **Status:** **ADOPTED 2026-08-21.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-203.review-adversarial.claude2.json`,
  `6e5757b33547db416afbd16f74b71553251d14de624a2a1b753ae82efda9f175`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-203.review-adversarial.codex.json`,
  `7d50714af2a1fde832845f46d4058800c4d4ff52cd401326ab07260188e32cc3`)
  CONSENT. Subject `coordinator-decisions.D-203.draft.md`
  `0c3983abacbb9b78e8ee973dc52e1bdbf49dcb85199552e1354663bb810a4f8c`.
  Frozen leftover-join
  `g28-leftover-join.v3.json`
  `14f1c34b86245bdf659b0c8e6ef6946a63675dcca2a32febcb00ca214df6d51c`
  Stage A Claude ACCEPT
  `44cce90cfeb32a0538368db246941bed9f619b68a8d71c30d3f2b467e13ff191`
  0/0; Stage A Codex ACCEPT
  `66b39f7eb27d6d01d47b84e1fabc703564958c57adda959fbe1fc4f27519aeff`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g28-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-202. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g28-leftover-join.v3.json`
  `14f1c34b86245bdf659b0c8e6ef6946a63675dcca2a32febcb00ca214df6d51c`.
- **Decision:** Record v3 as G28 leftover remasurement after
  D-202. The candidate binds NOTHING. DR-G28 stays `OPEN`.
  leftover-design of OBL-G28-FX-AUTHORING remains. Does not
  SATISFY DR-131. Does not invent a D9 code, exit, or
  HostTermination. Does not reopen leftover-design of
  DR-131 NT-7 or NT-8. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v2 remains a historical measurement as of
  HEAD `5d5d778` / required-now 26. v1 and v2 stay frozen;
  do not record them as current. Does not invent fixture
  bytes. Does not rewrite G28, G31, or G32. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D203. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  or D-202.
- **Commit:** C-D203.

## D-204 — Record g29-leftover-join.v3 as G29 leftover remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-204.review-adversarial.claude2.json`,
  `4a359b842bec547b59d4d25c548cde30e05a4bc6a3b839d5418e32098c69df7b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-204.review-adversarial.codex.json`,
  `dabca8b23b7b4b1a6e0fd5d3d28be5be92c3da69fae69716026bce8f75b50c59`)
  CONSENT. Subject `coordinator-decisions.D-204.draft.md`
  `420a2586082e066072f86995d5dda39dd52f0f52541ca65219b1ff7f4f03a026`.
  Frozen leftover-join
  `g29-leftover-join.v3.json`
  `4ab44caebced258a4ba2ef795879bf3afc9427cb5ae547c1138bf1c0e9f7ec5f`
  Stage A Claude ACCEPT
  `32b2f6a2423f716d05e8a3b4d364df342c8b15f6f84fa34e5499475f63c0b506`
  0/0; Stage A Codex ACCEPT
  `71647f678b8dcd3e3910c48d572d096c8372808e34e332830e5f199e2edbc8a0`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g29-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-203. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g29-leftover-join.v3.json`
  `4ab44caebced258a4ba2ef795879bf3afc9427cb5ae547c1138bf1c0e9f7ec5f`.
- **Decision:** Record v3 as G29 leftover remasurement after
  D-203. The candidate binds NOTHING. DR-G29 stays `OPEN`.
  leftover-design of OBL-G29-FX-AUTHORING remains. Does not
  SATISFY DR-117. Does not take over G21, G23, G24, or G30.
  Does not reopen leftover-design of EE-1, EE-2, EE-3b,
  EE-4, EE-5a, EE-5b, or EE-6a. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v2 remains a historical
  measurement as of HEAD `5d5d778` / required-now 26. v1
  and v2 stay frozen; do not record them as current. Does
  not invent fixture bytes or a section 7.1 recipe. Does
  not rewrite G29, G31, or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D204. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, or D-203.
- **Commit:** C-D204.

## D-205 — Record g30-leftover-join.v3 as G30 leftover remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-205.review-adversarial.claude2.json`,
  `19488425288da73371d8191840085c907edd41993c3b3e240b84c18d0177e22b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-205.review-adversarial.codex.json`,
  `430e43c59e01c66cd452b68fb027b6a4a4d92e917516a80c14f131437755f085`)
  CONSENT. Subject `coordinator-decisions.D-205.draft.md`
  `dce58eec385b29b685cfe1f53945621c401bbb592c517aed7ea7ba4cd62bf49f`.
  Frozen leftover-join
  `g30-leftover-join.v3.json`
  `034ccef172c58ab3815c6cd2f91d47cfcc59a35d895d4dc46b9e178dde16da20`
  Stage A Claude ACCEPT
  `4c1b949badbb76e6f0be5dbc07ecbb8a668b23656ba344542b5e10779d42e797`
  0/0; Stage A Codex ACCEPT
  `75bd5df9d5197b11dcbfaad81740e6f96187c240cb8ff22f9db5d5c7825ca20c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g30-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-204. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/g30-leftover-join.v3.json`
  `034ccef172c58ab3815c6cd2f91d47cfcc59a35d895d4dc46b9e178dde16da20`.
- **Decision:** Record v3 as G30 leftover remasurement after
  D-204. The candidate binds NOTHING. DR-G30 stays `OPEN`.
  leftover-design of OBL-G30-FX-AUTHORING remains. Does not
  SATISFY DR-117. Does not reopen leftover-design of EE-7a,
  EE-7b, or EE-7d. Does not take over DR-101, G13, G14, G16,
  G24, or G29. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v1 and v2 stay frozen; do not record
  them as current. Does not invent fixture bytes, a section
  7.1 recipe, or the DR-131 pack. Does not rewrite G30,
  G31, or G32. Does not edit file 08. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D205. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, or D-204.
- **Commit:** C-D205.

## D-206 — Record language-quality leftover-join.v3 as DR-118 leftover remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-206.review-adversarial.claude2.json`,
  `00134646ceb69c46c37cc6e2dd006ceeb1b7ae41928242baefd001b5fb0b6b18`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-206.review-adversarial.codex.json`,
  `53d02e74983cd0de94142569f5b95f99980bb21166f8809ae765d86791b7960c`)
  CONSENT. Subject `coordinator-decisions.D-206.draft.md`
  `f42d0f2ce22ace40d4e7bfda65ecfc33de250c6121085a09b1e4b51efc5c4ef6`.
  Frozen leftover-join
  `language-quality-leftover-join.v3.json`
  `0b90ab1e5712f6e4581029eda919703d3d6bb66dd0ef2c8568f7d3caec13771a`
  Stage A Claude ACCEPT
  `11535a0c9138cf4cb536989e10842821a93951aaafcde4c2fbe8f01a69526818`
  0/0; Stage A Codex ACCEPT
  `4091ff17a79bf0d738aee49af9b4465cc19ef8a8dd773dfd5fdd9116f073e9e4`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-quality-leftover-join.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-205. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/language-quality-leftover-join.v3.json`
  `0b90ab1e5712f6e4581029eda919703d3d6bb66dd0ef2c8568f7d3caec13771a`.
- **Decision:** Record v3 as DR-118 leftover remasurement
  after D-205. The candidate binds NOTHING. DR-118 stays
  `DECIDED-V1-NOT-INTEGRATED`. leftover-design of
  OBL-THRESHOLDS, OBL-MATRIX-CORPUS, and OBL-G13-RESERVED
  remains. D-002 role list and D-007 acceptance structure
  are not leftover-authoring. Does not SATISFY DR-118.
  D-056 Eligibility gates 2 and 3 do not hold for DR-118.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28. G13
  stays reserved, not named. Condition-4 effect is zero.
  Frozen v2 remains a historical measurement as of HEAD
  `c2b77f6` / required-now 26. v1 and v2 stay frozen; do
  not record them as current. Does not invent per-row
  numeric thresholds. Does not author the matrix or corpus.
  Does not steal OBL-SDK-API-RESERVED. Does not rewrite
  G13, G14, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, threshold decision, G13 naming successor,
  SATISFIED cycle, or file-08 cell rewrite. Overturn:
  C-D206. Does not unwrite D-007, D-113, D-110, D-164,
  D-165, D-167, D-168, D-169, D-170, D-171, D-172, D-173,
  D-174, D-175, D-176, D-177, D-178, D-179, D-180, D-181,
  D-182, D-183, D-184, D-185, D-186, D-187, D-188, D-189,
  D-190, D-191, D-192, D-193, D-194, D-195, D-196, D-197,
  D-198, D-199, D-200, D-201, D-202, D-203, D-204, or
  D-205.
- **Commit:** C-D206.

## D-207 — Record preview-product-boundary-successor.v8 as DR-117 leftover remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-207.review-adversarial.claude2.json`,
  `0d439cc827d0b2156a7fac364d01f968eb902021e90a94e0026026e1e14fa9f7`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-207.review-adversarial.codex.json`,
  `f16766e2c47540bf50a0ea7e5b083421eb9d3f196c75f27d06c25ebb456636a2`)
  CONSENT. Subject `coordinator-decisions.D-207.draft.md`
  `82d08f98a5f678aedb5cfd2626ee013a1ee51908feb5a29e08520eb65fab7617`.
  Frozen successor
  `preview-product-boundary-successor.v8.json`
  `f2e788e51c347e1033073f0718e701d164affe51e7f667da9bcd49a08837144c`
  Stage A Claude ACCEPT
  `4f71ccfc3a89fd0b5fc1a2f393a3864e8a2b5f1c792c0b696c63f831c05e2bca`
  0/0; Stage A Codex ACCEPT
  `5176f1de3713915cd8b5fbc2bafbd596b6d6fa285d68a299fdfbfee9375c1078`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `preview-product-boundary-successor.v8.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-206. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/preview-product-boundary-successor.v8.json`
  `f2e788e51c347e1033073f0718e701d164affe51e7f667da9bcd49a08837144c`.
- **Decision:** Record v8 as DR-117 leftover remasurement
  after D-206. The candidate binds NOTHING. DR-117 stays
  `OPEN`. leftover-design of unnamed EE classes remains
  closed at D-159. Remainder is named-gate execution.
  leftover-design of OBL-G29-FX-AUTHORING and
  OBL-G30-FX-AUTHORING remains on the current G29 and G30
  leftover-joins. Does not steal those leftovers. Does not
  SATISFY DR-117. D-056 Eligibility gates 2 and 3 continue
  to hold for DR-117 (D-159). Gate 1 Class A remains false
  under D-137's express reservation. v8 does not withdraw
  that reservation. Venue for any later lift is a reviewed
  coordinator act, not an artifact. Gates 4 and 5 are not
  performed. Not eligible in kind. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v7 remains a historical measurement as of HEAD `5d5d778`
  / required-now 26. v7 stays frozen; do not record it as
  current. Advisories CLAUDE-PPBS-V8-ADV-1 and
  CLAUDE-PPBS-V8-ADV-2 travel as honesty work. Standing
  CLAUDE-PPBS-V3-ADV-1 venue limb stands. Does not invent
  fixture bytes or the DR-131 pack. Does not rewrite G13,
  G14, G29, G30, G31, or G32. Does not name G13 into
  required-now. Does not edit file 08. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, Class A reservation lift, SATISFIED
  cycle, or file-08 cell rewrite. Overturn: C-D207. Does
  not unwrite D-137, D-157, D-158, D-159, D-167, D-168,
  D-169, D-170, D-171, D-172, D-173, D-174, D-175, D-176,
  D-177, D-178, D-179, D-180, D-181, D-182, D-183, D-184,
  D-185, D-186, D-187, D-188, D-189, D-190, D-191, D-192,
  D-193, D-194, D-195, D-196, D-197, D-198, D-199, D-200,
  D-201, D-202, D-203, D-204, D-205, or D-206.
- **Commit:** C-D207.

## D-208 — Record harness.DR-G31.identity-namespace-negative-test.preview.v5 as G31 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-208.review-adversarial.claude2.turn2.json`,
  `51c69e1a6efc5706011537f8c99b7fce646ae1cb466f95f22199717b7bad4d2c`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-208.review-adversarial.codex.turn2.json`,
  `7e255d5f555d6eac030e666afba52437910759f76f0b6c0e014ed45dd44090e8`)
  CONSENT. Subject `coordinator-decisions.D-208.turn2.draft.md`
  `40aa627477fad268a33dcfd82537a031d4d5cb1246d163d52d9e40b6a485baff`.
  Turn-1 Claude OBJECT (CLAUDE-D208-SF1/SF2) at
  `f64e81fd0f18c0fdd24e2541e2a7d806a6213632b149c9ef6f641e88344a7d60`;
  turn-1 Codex OBJECT (CODEX-D208-SF1)
  `2412b49511ef027d462abb759b19c2d39d9956bca9850f7c0bb62e394a391c25`.
  Frozen occupancy
  `harness.DR-G31.identity-namespace-negative-test.preview.v5.json`
  `4cc42b86cf74b95c88c8efc9b85e48b894759712d30fbc1aaee079f301ca00a4`
  Stage A Claude ACCEPT
  `edae073303d893901c7ec7ff7dc6632a86ca8c8c31dbdac290939d56abce44e0`
  0/0; Stage A Codex ACCEPT
  `6caae191cf1d844e3afb6e1255efd8a6d7f14b40996103b29ea6704fbddbd16d`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G31.identity-namespace-negative-test.preview.v5.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-207. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G31.identity-namespace-negative-test.preview.v5.json`
  `4cc42b86cf74b95c88c8efc9b85e48b894759712d30fbc1aaee079f301ca00a4`.
- **Decision:** Record v5 as G31 occupancy remasurement
  after D-207. The candidate binds NOTHING. DR-G31 stays
  `OPEN`. leftover-design of unnamed NT-11 execution
  remainder remains closed at D-175. Remainder is G31
  execution. Does not pin QUALIFIED. Does not SATISFY
  DR-104. Does not SATISFY DR-117. Gate 1 Class A is not
  opened. Class B SATISFIED is not recorded. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical occupancy as of HEAD `5d5d778` /
  required-now 26. Frozen v3 and v4 remain dual-REJECT
  occupancies. v2, v3, and v4 stay frozen; do not record
  them as current. Advisories CLAUDE-G31-V5-ADV-1,
  CLAUDE-G31-V5-ADV-2 / CODEX-G31-V5-ADV-1 (one shared
  class; both identifiers preserved), and
  CLAUDE-G31-V5-ADV-3 travel as honesty work. Does not
  execute the eleven classes. Does not invent fixture
  bytes. Does not rewrite G31 or G32. Does not edit file
  08. Does not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D208. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, or D-207.
- **Commit:** C-D208.

## D-209 — Record harness.DR-G32.actor-join-fixture-execution.preview.v3 as G32 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-209.review-adversarial.claude2.json`,
  `732086131871e95bb297c081a7da4bf1822f5c0891f9464b0c277bbc9e7977d2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-209.review-adversarial.codex.json`,
  `0ddf04d69f57d912d5f3738adfb786ca8b128739898c210191f45c8f22969395`)
  CONSENT. Subject `coordinator-decisions.D-209.draft.md`
  `2ff7a76627d925b45087ef50f7cc767132417bbc1b8b9349ee6843cdd5160fd0`.
  Frozen occupancy
  `harness.DR-G32.actor-join-fixture-execution.preview.v3.json`
  `9c782a50fecd45bcec3b8eaa3fa6b8ea09b240d9cda5d530564b9e84fa48df49`
  Stage A Claude ACCEPT
  `c65fbcc7a8d3e03d2864032a0ff427bf3a10ee1258dcebca537265d194f3b11c`
  0/0; Stage A Codex ACCEPT
  `5cede4b742ad19b150d9889834a200336258191de315e611eb69e263b786315c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G32.actor-join-fixture-execution.preview.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-208. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G32.actor-join-fixture-execution.preview.v3.json`
  `9c782a50fecd45bcec3b8eaa3fa6b8ea09b240d9cda5d530564b9e84fa48df49`.
- **Decision:** Record v3 as G32 occupancy remasurement
  after D-208. The candidate binds NOTHING. DR-G32 stays
  `OPEN`. leftover-design of unnamed JOIN-FX-EXECUTION
  remainder remains closed at D-169. Remainder is G32
  execution once fixture implementations exist.
  leftover-design of OBL-JOIN-FX-AUTHORING remains. Does
  not pin QUALIFIED. Does not invent fixture bytes. Does
  not SATISFY DR-114. Does not SATISFY DR-117. Gate 1
  Class A is not opened. Class B SATISFIED is not recorded.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Frozen v1 remains a historical occupancy as of
  HEAD `5d5d778` / required-now 26. Frozen v2 remains a
  Codex-REJECT occupancy. v1 and v2 stay frozen; do not
  record them as current. Advisory CODEX-G32-V3-ADV-1
  travels as honesty work. Claude Stage A returned zero
  advisories. Does not execute the thirteen classes. Does
  not rewrite G31 or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D209. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, or D-208.
- **Commit:** C-D209.

## D-210 — Record harness.DR-G07.exact-bytes.v4 as G07 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-210.review-adversarial.claude2.json`,
  `e5d992cebc1193af3891bf23a2d99095ddb8165188e59e08d774948195aa3f76`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-210.review-adversarial.codex.json`,
  `ef995d897a73be990d8a7bff89169d2ab960238e1160e06214c2223519c2b6ef`)
  CONSENT. Subject `coordinator-decisions.D-210.draft.md`
  `cff61a53a4934ece493350ff077a2da505494fc3f413a602232c5be9a5e3e2e2`.
  Frozen occupancy
  `harness.DR-G07.exact-bytes.v4.json`
  `99be421cd11a7524c87ee56b31b1c3b8335d8156bdb0d27a3a94ddddae7a56ed`
  Stage A Claude ACCEPT
  `107a23d01e7b0bb580445e6f8eca0045043e681c18ef80318aa47b257e6d00d9`
  0/0; Stage A Codex ACCEPT
  `306396a1aa0e070a1ef0ffcd1d3d31115c2a3214945cbb04c670c153530c800f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G07.exact-bytes.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-209. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G07.exact-bytes.v4.json`
  `99be421cd11a7524c87ee56b31b1c3b8335d8156bdb0d27a3a94ddddae7a56ed`.
- **Decision:** Record v4 as G07 occupancy remasurement
  after D-209. The candidate binds NOTHING. DR-G07 stays
  `OPEN`. leftover-design of OBL-G07-HARNESS-SPEC remains
  measured closed at leftover-join.v5 (D-172). leftover-design
  of OBL-G07-FX-AUTHORING and OBL-FILESYSTEM-COVERAGE remains.
  Remainder is G07 execution once fixture implementations
  exist. Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not populate a filesystem allowlist. Does not
  SATISFY DR-103. Does not SATISFY DR-117. Gate 1 Class A
  is not opened. Class B SATISFIED is not recorded. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v3 remains a historical occupancy as of HEAD
  `5d5d778` / required-now 26. Frozen v1 and v2 remain
  Claude-REJECT occupancies. v1, v2, and v3 stay frozen; do
  not record them as current. Advisories CLAUDE-G07-V4-ADV-1
  and CLAUDE-D210-ADV-1 travel as honesty work. Codex Stage
  A and Stage B returned zero advisories. Does not execute
  fixtures. Does not rewrite G07, G31, or G32. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D210. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, or D-209.
- **Commit:** C-D210.

## D-211 — Record harness.DR-G08.trust-recovery.install-surfaces.v3 as G08 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-211.review-adversarial.claude2.json`,
  `23c8d5b0e453e189e74ec43ee6af1aabe26005ae16f447cc0a1d5273608a2d0b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-211.review-adversarial.codex.json`,
  `6ac999a84f836ed05eef0408199605e8cad6c8584896245f816e57efc948f89e`)
  CONSENT. Subject `coordinator-decisions.D-211.draft.md`
  `4e401843e359e387316b535d22be132dccd85f1c55dbe41dc7be72a62db56fc3`.
  Frozen occupancy
  `harness.DR-G08.trust-recovery.install-surfaces.v3.json`
  `13076be20e4eef0dfe352786b705de09304a69f583529502388e5086f6f098c0`
  Stage A Claude ACCEPT
  `f78c4b0e68f0a080e43133d4f1ab8f231e13479a32fa60077293093774064ab8`
  0/0; Stage A Codex ACCEPT
  `92390c354363e254852787efeb38a3b74ba76e4563b08b3dd9767d2885694e9f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G08.trust-recovery.install-surfaces.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-210. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G08.trust-recovery.install-surfaces.v3.json`
  `13076be20e4eef0dfe352786b705de09304a69f583529502388e5086f6f098c0`.
- **Decision:** Record v3 as G08 occupancy remasurement
  after D-210. The candidate binds NOTHING. DR-G08 stays
  `OPEN`. leftover-design of OBL-G08-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-188). leftover-design
  of OBL-G08-FX-AUTHORING remains. Remainder is G08
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  mint OD-112-1..4. Does not invent TR-ROOT. Does not name
  a repair-media harness. Does not SATISFY DR-112. Does not
  SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. Frozen v1 remains a Claude-REJECT occupancy. v1 and
  v2 stay frozen; do not record them as current. Advisory
  CLAUDE-D211-ADV-1 travels as honesty work. Claude Stage A
  and Codex Stage A and Stage B returned zero advisories.
  Does not execute fixtures. Does not rewrite G07, G08,
  G31, or G32. Does not edit file 08. Does not invent a D9
  code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D211. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  or D-210.
- **Commit:** C-D211.

## D-212 — Record harness.DR-G10.provider-conformance.ts-major-1.v2 as G10 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-212.review-adversarial.claude2.json`,
  `939c24bcd0f5b143c30c1febf7bb8ef0f7d6702dffd52cd42a0f6f455b55502c`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-212.review-adversarial.codex.json`,
  `420dcbd7dd80393316336ad1dbffd0f364081ccb6e30080d54ea7b17989d202e`)
  CONSENT. Subject `coordinator-decisions.D-212.draft.md`
  `b080698512e632d285b25add1e196a49b84587d3e4ef986595d2d0045f4c4a2d`.
  Frozen occupancy
  `harness.DR-G10.provider-conformance.ts-major-1.v2.json`
  `b0cbce06487b96bbe7f6af1dae62ba3b3ca55aaa41305cb96f531099e86bf7c9`
  Stage A Claude ACCEPT
  `04d90eb40a9e1461305cfd3570258180b19ecff8d2dd1ef6e7ce15371e3c0d6c`
  0/0; Stage A Codex ACCEPT
  `de7bb2a593b45182d0c0397a2ec6fb7d1895b4dffdfe05666ba4e02b7ae7e6a2`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G10.provider-conformance.ts-major-1.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-211. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G10.provider-conformance.ts-major-1.v2.json`
  `b0cbce06487b96bbe7f6af1dae62ba3b3ca55aaa41305cb96f531099e86bf7c9`.
- **Decision:** Record v2 as G10 occupancy remasurement
  after D-211. The candidate binds NOTHING. DR-G10 stays
  `HARD-BLOCKED pending selector refresh`. leftover-design of
  OBL-G10-HARNESS-SPEC remains measured closed at leftover-
  join.v3 (D-187). leftover-design of OBL-G10-FX-AUTHORING
  and OBL-SELECTOR-REFRESH remains. Remainder is G10
  execution once fixture implementations exist and after
  the owed selector refresh. Does not pin QUALIFIED. Does
  not invent fixture bytes. Does not invent a V2 selector.
  Does not pull Rust merged-major-2 into the preview runner.
  Does not SATISFY DR-102 a second time. Does not reopen
  DR-102 SATISFIED. Does not SATISFY DR-133. Does not
  SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v1 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. v1 stays frozen; do not record it as current. Claude
  Stage A and Codex Stage A and Stage B returned zero
  advisories. Does not execute fixtures. Does not rewrite
  G07, G08, G10, G31, or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D212. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, or D-211.
- **Commit:** C-D212.

## D-213 — Record harness.DR-G14.language-runtime-ux.typescript.v4 as G14 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-213.review-adversarial.claude2.json`,
  `6f95dd253e591d69d08761b740f413030e82d41f682c92d1c9e3792226bbbf50`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-213.review-adversarial.codex.json`,
  `e4efb3409a123538807fc95fbd830eeed70788fb916efbbd424ae3d7050b29e5`)
  CONSENT. Subject `coordinator-decisions.D-213.draft.md`
  `fbdd63e6dda0fd5f77e6ce522e5eaad61c5d97b73e980379f0cd864c54a4a6f9`.
  Frozen occupancy
  `harness.DR-G14.language-runtime-ux.typescript.v4.json`
  `0b4c25f4c2e5ae7fbf0a9a2762ccce813a6174401d9c51d123ecb2f8b1ddb647`
  Stage A Claude ACCEPT
  `943f7f8b83744914db0ea976d0df923f707e90f4c64888cfcfa3c9f6e75047f4`
  0/0; Stage A Codex ACCEPT
  `695e0b66bdb8fe86b6ee5d038ecc927f5d34303a5f8aa1c5872eeef986227d40`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G14.language-runtime-ux.typescript.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-212. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G14.language-runtime-ux.typescript.v4.json`
  `0b4c25f4c2e5ae7fbf0a9a2762ccce813a6174401d9c51d123ecb2f8b1ddb647`.
- **Decision:** Record v4 as G14 occupancy remasurement
  after D-212. The candidate binds NOTHING. DR-G14 stays
  `OPEN`. leftover-design of OBL-G14-HARNESS-SPEC remains
  measured closed at leftover-join.v4 (D-179). leftover-design
  of OBL-G14-FX-AUTHORING remains. Remainder is G14
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent per-row numeric thresholds. Does not name G13
  into required-now. Does not SATISFY DR-118. Does not
  re-SATISFY DR-119. Does not SATISFY DR-117. Gate 1 Class
  A is not opened. Class B SATISFIED is not recorded. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v1 remains a historical occupancy as of HEAD
  `5d5d778` / required-now 26. Frozen v2 remains a Claude-
  REJECT occupancy. Frozen v3 remains a dual-REJECT
  occupancy. v1, v2, and v3 stay frozen; do not record them
  as current. CLAUDE-G14-V3-SF1 and CODEX-G14-V3-SF1 (one
  shared class; both identifiers preserved) were landed in
  the occupancy bytes. Claude Stage A and Codex Stage A
  and Stage B returned zero advisories. Does not execute
  fixtures. Does not rewrite G07, G08, G10, G14, G31, or
  G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D213. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, or D-212.
- **Commit:** C-D213.

## D-214 — Record harness.DR-G15.packaging-adapter-conformance.v9 as G15 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-214.review-adversarial.claude2.json`,
  `b63d7b914aadacc50b8037ebb009c27584336ea6bf18aa6fcefdefe4eb957e3e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-214.review-adversarial.codex.json`,
  `2c4a0937c8370649c24fdaed821ff9520dcb37d947328e2c50e81aba788b30f9`)
  CONSENT. Subject `coordinator-decisions.D-214.draft.md`
  `22de6c1851c1737d747470b0d6854bc1f9ad8cf614b90f9d6230ff26b20fd7d4`.
  Frozen occupancy
  `harness.DR-G15.packaging-adapter-conformance.v9.json`
  `d82fac570f952cbc234be682b658cf94d5f7571bf4297e777e4e2c4280f98479`
  Stage A Claude ACCEPT
  `6bc29967192086a46a7a17ac7579dab5ac5841953b7ea87e022784a5c58806ac`
  0/0; Stage A Codex ACCEPT
  `4d19a87ff755fb38309c7682aa5f64a06428084dc8233f65c5a17aa57f064fe5`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G15.packaging-adapter-conformance.v9.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-213. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G15.packaging-adapter-conformance.v9.json`
  `d82fac570f952cbc234be682b658cf94d5f7571bf4297e777e4e2c4280f98479`.
- **Decision:** Record v9 as G15 occupancy remasurement
  after D-213. The candidate binds NOTHING. DR-G15 stays
  `OPEN`. leftover-design of OBL-G15-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-191). leftover-design
  of OBL-AT-FX-AUTHORING remains. Remainder is G15
  execution once AT-ARCHIVE-* fixture implementations exist.
  Does not pin QUALIFIED. Does not invent fixture bytes.
  Does not invent an adapter implementation. Does not
  SATISFY DR-120. Does not SATISFY DR-103. Does not SATISFY
  DR-117. Gate 1 Class A is not opened. Class B SATISFIED
  is not recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v7 remains a historical
  occupancy as of HEAD `5d5d778` / required-now 26. Frozen
  v8 remains a Codex-REJECT occupancy. v7 and v8 stay
  frozen; do not record them as current. CODEX-G15H-V8-SF1
  was landed in the occupancy bytes. Claude Stage A and
  Codex Stage A and Stage B returned zero advisories. Does
  not execute fixtures. Does not rewrite G07, G08, G10,
  G14, G15, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D214. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, or D-213.
- **Commit:** C-D214.

## D-215 — Record harness.DR-G16.ci-isolation-integration.v5 as G16 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-215.review-adversarial.claude2.turn2.json`,
  `c25d34d8a846eea6f1712ddd284b43a6bdaa6e775d38cce75bcb019aea9af6d7`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-215.review-adversarial.codex.turn2.json`,
  `1626a826965e505cadadf8ab6ed16498f638189dc29708a9e23f182f5ebd6940`)
  CONSENT. Subject `coordinator-decisions.D-215.turn2.draft.md`
  `0787d3ee9bcdf977f060c49f0bbae6698f872a3b5ac89bc5ec85f7c4f383e3f2`.
  Turn-1 Claude OBJECT (CLAUDE-D215-SF1) at
  `9366bbdd264bf9bce8e781813dc092012e815000bc0da763b16040849f32583e`;
  turn-1 Codex CONSENT 0/0
  `a9bb6157a8492284d3dfb9c51784b9166dc16e0e12f6bba49b32468f06118a5a`.
  Frozen occupancy
  `harness.DR-G16.ci-isolation-integration.v5.json`
  `3e3107499ffb576c11b3d4c290470921062066f518cbd80b6a563b446ebc918e`
  Stage A Claude ACCEPT
  `246993a8c653d129348b4a470e82cc5e68f7724d24406223391e1e9086f44602`
  0/0; Stage A Codex ACCEPT
  `629e5bca9b3df142bf1134f4eb3a7ac7404d48050acc2bdde2c6038e9a43e286`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G16.ci-isolation-integration.v5.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-214. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G16.ci-isolation-integration.v5.json`
  `3e3107499ffb576c11b3d4c290470921062066f518cbd80b6a563b446ebc918e`.
- **Decision:** Record v5 as G16 occupancy remasurement
  after D-214. The candidate binds NOTHING. DR-G16 stays
  `OPEN`. leftover-design of OBL-G16-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-192). leftover-design
  of OBL-G16-FX-AUTHORING remains. Remainder is G16
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent reserved CI encodings. Does not apply v16. Does
  not steal OBL-CI-ENCODING-RESERVED. Does not SATISFY
  DR-121. Does not SATISFY DR-117. Gate 1 Class A is not
  opened. Class B SATISFIED is not recorded. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v2 remains a historical occupancy as of HEAD `5d5d778` /
  required-now 26. Frozen v1, v3, and v4 remain Claude-REJECT
  occupancies. v1, v2, v3, and v4 stay frozen; do not record
  them as current. CLAUDE-G16-V3-MF1, CLAUDE-G16-V3-SF1,
  CLAUDE-G16-V4-MF1, and CLAUDE-G16-V4-SF1 were landed in
  the occupancy bytes. CLAUDE-G16-V1-SF1 remains retained.
  CLAUDE-D215-SF1 was landed in the COORD draft. Codex Stage
  A honesty observations G16V5-OBS-1, G16V5-OBS-2, and
  G16V5-OBS-3 travel as honesty work. G16V5-OBS-2 is one
  shared class with the Claude Stage A notRaised naming-v6
  path standing, which carries no identifier; the Codex
  identifier is preserved. Does not execute fixtures. Does
  not rewrite G07, G08, G10, G14, G15, G16, G31, or G32.
  Does not edit file 08. Does not invent a D9 code. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D215. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, or D-214.
- **Commit:** C-D215.

## D-216 — Record harness.DR-G18.lifecycle-generation-recovery.v4 as G18 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-216.review-adversarial.claude2.json`,
  `5a82a97567e11033fc86f31f1b6d67cbb9a1321f0fe3e801b171b469c9294e95`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-216.review-adversarial.codex.json`,
  `7baf3e5a25fd253d47f64e5077e9f316a17050f5251b57fe80450aa99103cb9f`)
  CONSENT. Subject `coordinator-decisions.D-216.draft.md`
  `474a019dafc671e5c28e8db117bb3e32a3908b909fef9a2cbb6a5eb84f70d665`.
  Frozen occupancy
  `harness.DR-G18.lifecycle-generation-recovery.v4.json`
  `2ce9aa522bf014af27b088d3bd50885a271e5e321ba6c372af527552cb6660cc`
  Stage A Claude ACCEPT
  `ac8da15d81e9e1ebc8e0939960bf0ba6ac8f9eb7636c7bda0d1e282e41caa781`
  0/0; Stage A Codex ACCEPT
  `c086314313fa0315b976039d29078b4060d83a7aeea4e5506277354aafbcdf5e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G18.lifecycle-generation-recovery.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-215. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G18.lifecycle-generation-recovery.v4.json`
  `2ce9aa522bf014af27b088d3bd50885a271e5e321ba6c372af527552cb6660cc`.
- **Decision:** Record v4 as G18 occupancy remasurement
  after D-215. The candidate binds NOTHING. DR-G18 stays
  `OPEN`. leftover-design of OBL-G18-HARNESS-SPEC remains
  measured closed at leftover-join.v4 (D-193). leftover-design
  of OBL-G18-FX-AUTHORING remains. Remainder is G18
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent a journal. Does not apply
  lifecycle-generation-contract.v2. Does not steal
  OBL-ENCODING-RESERVED. Does not SATISFY DR-107. Does not
  SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v2 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. Frozen v1 remains a Claude-REJECT occupancy. Frozen
  v3 remains a dual-REJECT occupancy. v1, v2, and v3 stay
  frozen; do not record them as current. CLAUDE-G18-V3-B1
  and CODEX-G18-V3-SF1 (one shared class; both identifiers
  preserved) were landed in the occupancy bytes.
  CLAUDE-G18-V1-B1 remains retained. Claude Stage A returned
  zero advisories and three unlabeled observations. Codex
  Stage A and Stage B returned zero advisories. Does not
  execute fixtures. Does not rewrite G07, G08, G10, G14,
  G15, G16, G18, G31, or G32. Does not edit file 08. Does
  not invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D216. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, or D-215.
- **Commit:** C-D216.

## D-217 — Record harness.DR-G20.component-operability.v2 as G20 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-217.review-adversarial.claude2.turn2.json`,
  `04528a36fa6b9c02380959ebb7006fa855cef573f624c9983281459e0851232f`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-217.review-adversarial.codex.turn2.json`,
  `2f0c328a2a374f3a8368838b5b0261c112a56792288b5b61c41fc3f44adc5adc`)
  CONSENT. Subject `coordinator-decisions.D-217.turn2.draft.md`
  `faebee24a6f9f5ffa3b1ff075f6dfaf588232553b6b0f954bd20fcef42c76e6a`.
  Turn-1 Claude OBJECT (CLAUDE-D217-SF1) at
  `d47cab867cdccce2c9a2fa5e24a4168386529b76eb1ae15e4b32c546affcc7c8`;
  turn-1 Codex CONSENT 0/0
  `6a18cbf597b63ff6c2317a0accc7de6a7e1a8501350ab9c0d7e0887256efd825`.
  Frozen occupancy
  `harness.DR-G20.component-operability.v2.json`
  `2c4823b7c5feb04afb739602397f81dc34333617c284bff21e82657fa289bb37`
  Stage A Claude ACCEPT
  `f3088806cfc4ec3920cc959b047338a380ce9a965133545574ea311fb37df1ff`
  0/0; Stage A Codex ACCEPT
  `fbe908dd419a5b258510ece4564e6e3099eaa18beee5fda6d7d9d994a3c18356`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G20.component-operability.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-216. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G20.component-operability.v2.json`
  `2c4823b7c5feb04afb739602397f81dc34333617c284bff21e82657fa289bb37`.
- **Decision:** Record v2 as G20 occupancy remasurement
  after D-216. The candidate binds NOTHING. DR-G20 stays
  `OPEN`. leftover-design of OBL-G20-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-195). leftover-design
  of OBL-G20-FX-AUTHORING remains. Remainder is G20
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent SDK APIs. Does not steal OBL-SDK-API-RESERVED.
  Does not execute NT-4 or NT-7 by existing. Does not
  SATISFY DR-125. Does not SATISFY DR-133. Does not SATISFY
  DR-117. Gate 1 Class A is not opened. Class B SATISFIED
  is not recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains a historical
  occupancy as of HEAD `5d5d778` / required-now 26. v1 stays
  frozen; do not record it as current. Claude Stage A
  advisories CLAUDE-G20-V2-A1, CLAUDE-G20-V2-A2, and
  CLAUDE-G20-V2-A3 travel as honesty work. Codex Stage A
  honesty observations G20V2-OBS-01 and G20V2-OBS-02 travel
  as honesty work. G20V2-OBS-02 is one shared class with
  CLAUDE-G20-V2-A1; both identifiers are preserved.
  CLAUDE-D217-SF1 was landed in the COORD draft. Claude
  Stage B turn-2 advisories CLAUDE-D217-T2-A1 and
  CLAUDE-D217-T2-A2 travel as honesty work. Does not execute
  fixtures. Does not rewrite G07, G08, G10, G14, G15, G16,
  G18, G20, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D217. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, or D-216.
- **Commit:** C-D217.

## D-218 — Record harness.DR-G21.component-failure-containment.v4 as G21 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-218.review-adversarial.claude2.json`,
  `79782eeb9c2c738fe560987dfe57c0e086941d8a419e437d8b387e586c80d5b0`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-218.review-adversarial.codex.json`,
  `f76da132d8e7a311c26f0db27c5115173c1d5e1433b9010a1d8eb0af688e1afe`)
  CONSENT. Subject `coordinator-decisions.D-218.draft.md`
  `e369b85bacca23b01001db8ce5f53bacf7f8e9750926b3c2520500999b073494`.
  Frozen occupancy
  `harness.DR-G21.component-failure-containment.v4.json`
  `13addb3cc70611efe22876f84dbe9e15d9a27529446d7e03841d2b2a3f552e0b`
  Stage A Claude ACCEPT
  `08a8cd0cd148d15487ad379e63b3a979038086328bd49ef5a97ffdf5018adb1d`
  0/0; Stage A Codex ACCEPT
  `82c039e829b87e6712112967936d0a65cb3b0acb9ae3d483aaa6bdf18e92cd57`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G21.component-failure-containment.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-217. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G21.component-failure-containment.v4.json`
  `13addb3cc70611efe22876f84dbe9e15d9a27529446d7e03841d2b2a3f552e0b`.
- **Decision:** Record v4 as G21 occupancy remasurement
  after D-217. The candidate binds NOTHING. DR-G21 stays
  `OPEN`. leftover-design of OBL-G21-HARNESS-SPEC remains
  measured closed at leftover-join.v4 (D-196). leftover-design
  of OBL-G21-FX-AUTHORING remains. Remainder is G21
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent a D9 code. Does not steal leftover-join.v11
  leftoverDesign. Does not reopen DR-102 SATISFIED. Does
  not execute CC-1..CC-11 or DR-133 NT-1/NT-2/NT-6 by
  existing. Does not SATISFY DR-114. Does not SATISFY
  DR-102 a second time. Does not SATISFY DR-133. Does not
  SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v3 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. Frozen v1 and v2 remain Claude-REJECT occupancies.
  v1, v2, and v3 stay frozen; do not record them as current.
  Claude Stage A returned zero advisories and three unlabeled
  observations. Codex Stage A honesty observation
  CODEX-G21-V4-OBS1 travels as honesty work. The Codex
  identifier is preserved. The Claude observations carry no
  identifier. Does not execute fixtures. Does not rewrite
  G07, G08, G10, G14, G15, G16, G18, G20, G21, G31, or
  G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D218. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, or
  D-217.
- **Commit:** C-D218.

## D-219 — Record harness.DR-G22.platform-abi-loader.v2 as G22 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-219.review-adversarial.claude2.json`,
  `b810f867d071500eae0e5d5200ace6fb5f98fa457e06f48623fd4639c4cae622`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-219.review-adversarial.codex.json`,
  `310ec73bfec332a8b28f8131c68e07680bd83a8464da9efce7f560b65bb62086`)
  CONSENT. Subject `coordinator-decisions.D-219.draft.md`
  `eae140e7f0dcb66ae6e08f1c7f0f9ec6656d93efebd61a00025459672f0c40b5`.
  Frozen occupancy
  `harness.DR-G22.platform-abi-loader.v2.json`
  `2973cda2adac1b612c084b64606e4fc5b5ed5b78317fc64780a7311172ff1307`
  Stage A Claude ACCEPT
  `8f0444b7f859f7b276ac7f61ffa56c2b79d35596ed2fcb945e81b9cf7b2fa345`
  0/0; Stage A Codex ACCEPT
  `c7f43e3dcf90c4ca5565a0524f17e0143a3e57c9cb981445eb269ee68ea3c416`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G22.platform-abi-loader.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-218. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G22.platform-abi-loader.v2.json`
  `2973cda2adac1b612c084b64606e4fc5b5ed5b78317fc64780a7311172ff1307`.
- **Decision:** Record v2 as G22 occupancy remasurement
  after D-218. The candidate binds NOTHING. DR-G22 stays
  `OPEN`. leftover-design of OBL-G22-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-197). leftover-design
  of OBL-G22-FX-AUTHORING remains. Remainder is G22
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  populate reserved TCB tables. Does not invent Rosetta.
  Does not apply platform-tcb-contract.v45. Does not steal
  platform-tcb leftover-join.v6 leftoverDesign. Does not
  steal OBL-RESERVED-TABLES. Does not SATISFY DR-126. Does
  not SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v1 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. v1 stays frozen; do not record it as current.
  Claude Stage A returned zero advisories. Codex Stage A
  returned zero advisories. Claude Stage B returned three
  unlabeled observationsNotFindings (charged false); they
  carry no identifier. Codex Stage B returned zero
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G10, G14, G15, G16, G18, G20, G21, G22, G31, or
  G32. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D219. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217, or
  D-218.
- **Commit:** C-D219.

## D-220 — Record harness.DR-G09.permissions.preview-scoped.v4 as G09 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-220.review-adversarial.claude2.json`,
  `d11f2b9e9a4bb23aabc960e5f7d15a47e0cf9e866e991ba000c3decde128289b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-220.review-adversarial.codex.json`,
  `65c784a9f34eb84a7483f350f8b63540a9d4bb0c5a7fd9e483bcb5831ea5fa82`)
  CONSENT. Subject `coordinator-decisions.D-220.draft.md`
  `9818136f0e89401e0a784358827214f4ea36eaa0fe7649fa78032c045654b174`.
  Frozen occupancy
  `harness.DR-G09.permissions.preview-scoped.v4.json`
  `603f96ebfd63466ca669ec97701462dd93f0997c398ea87b9f9a41ed495d6646`
  Stage A Claude ACCEPT
  `ef46f34e2e5a346146d685de227f28d0710184a92705bf042b12e0d0080d1ccb`
  0/0; Stage A Codex ACCEPT
  `4241c8f889beffc7f7ad13f14a55b71316539a08f3cacf554d2fc678236ee928`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G09.permissions.preview-scoped.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-219. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G09.permissions.preview-scoped.v4.json`
  `603f96ebfd63466ca669ec97701462dd93f0997c398ea87b9f9a41ed495d6646`.
- **Decision:** Record v4 as G09 occupancy remasurement
  after D-219. The candidate binds NOTHING. DR-G09 stays
  `OPEN`. leftover-design of OBL-G09-HARNESS-SPEC remains
  measured closed at leftover-join.v10 (D-189). leftover-design
  of OBL-FX-AUTHORING remains. Remainder is G09
  execution once the fourteen FX implementations and the
  R-10 and R-6 byte-sets exist. Does not pin QUALIFIED.
  Does not invent fixture bytes. Does not fold R-10 or
  R-6 into the fourteen FX. Does not record FC-C1. Does
  not steal permission leftover-join.v9 leftoverDesign.
  Does not steal doctor-actor leftover-join.v11 leftoverDesign.
  Does not SATISFY DR-105. Does not SATISFY DR-117. Gate 1
  Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v3 remains a
  historical occupancy as of HEAD `5d5d778` / required-now
  26. Frozen v1 and v2 remain Claude-REJECT occupancies.
  v1, v2, and v3 stay frozen; do not record them as current.
  Claude Stage A returned zero advisories and four unlabeled
  observationsNotFindings. Codex Stage A returned zero
  advisories. The Claude observations carry no identifier.
  Codex Stage A returned no observations. Claude Stage B
  returned four unlabeled observationsNotFindings; they
  carry no identifier. Codex Stage B returned zero
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G09, G10, G14, G15, G16, G18, G20, G21, G22,
  G31, or G32. Does not edit file 08. Does not invent a
  D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D220. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, or D-219.
- **Commit:** C-D220.

## D-221 — Record harness.DR-G12.doctor-purge.preview.v6 as G12 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-221.review-adversarial.claude2.json`,
  `ca5c3422ca14698cdacc0c122b4161bbb91e533d5910ca0669f278e5581e4f8b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-221.review-adversarial.codex.json`,
  `4f2349318c3db6f8b74feef25c8e94f4263f50dca89cd221cecbc8d38d5c0493`)
  CONSENT. Subject `coordinator-decisions.D-221.draft.md`
  `cf055e02d151614c26f602687741868ba521479eac411e9a3c49858210dc27c3`.
  Frozen occupancy
  `harness.DR-G12.doctor-purge.preview.v6.json`
  `e6b72a9e0cc7053c991c51c510531c6ecd263bb895c70a3e9ab84bd6b6256735`
  Stage A Claude ACCEPT
  `8f616719f40798913bf71b5cac2a15f4a9cfa3d10adf63297c63b3dc63196b67`
  0/0; Stage A Codex ACCEPT
  `57176369eeebec50c792fed50d57ef15b3f8442c1eb2209e396678b7577d4274`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G12.doctor-purge.preview.v6.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-220. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G12.doctor-purge.preview.v6.json`
  `e6b72a9e0cc7053c991c51c510531c6ecd263bb895c70a3e9ab84bd6b6256735`.
- **Decision:** Record v6 as G12 occupancy remasurement
  after D-220. The candidate binds NOTHING. DR-G12 stays
  `OPEN`. leftover-design of OBL-G12-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-190). leftover-design
  of OBL-DOCTOR-FX-AUTHORING remains. Remainder is G12
  execution once the twelve doctor FC implementations exist.
  Does not pin QUALIFIED. Does not invent fixture bytes.
  Does not invent a D9 code. Does not steal leftover-join.v11
  leftoverDesign. Does not deny the 618cb5be v2 dispatch
  or the 618cb5be Claude ACCEPT. Does not SATISFY DR-114.
  Does not SATISFY DR-117. Gate 1 Class A is not opened.
  Class B SATISFIED is not recorded. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v4 remains a historical occupancy as of HEAD `5d5d778` /
  required-now 26. Frozen v5 remains a dual-REJECT occupancy.
  Frozen v1 and v3 remain Claude-REJECT occupancies. Frozen
  v2 remains the 618cb5be Claude-ACCEPT occupancy. v1
  through v5 stay frozen; do not record them as current.
  Claude Stage A returned zero advisories and four unlabeled
  observationsNotFindings. Codex Stage A returned zero
  advisories. The Claude observations carry no identifier.
  Codex Stage A returned no observations. CLAUDE-G12H-V5-B1
  and CODEX-G12H-V5-SF1 (one shared class; both identifiers
  preserved) were landed in the occupancy bytes. Claude
  Stage B returned four unlabeled observationsNotFindings;
  they carry no identifier. Codex Stage B returned zero
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G09, G10, G12, G14, G15, G16, G18, G20, G21,
  G22, G31, or G32. Does not edit file 08. Does not invent
  a D9 code. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D221. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, or D-220.
- **Commit:** C-D221.

## D-222 — Record harness.DR-G19.state-class-authority.preview-classes.v2 as G19 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-222.review-adversarial.claude2.json`,
  `db8382457fd8b1d56e0e668780f176eca8dcdef15aaed4c8fd0a3d0a93dd3901`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-222.review-adversarial.codex.json`,
  `a4a71cece8d7433705f65ba1d6f02041e20224a3f33051612a76782340ed843c`)
  CONSENT. Subject `coordinator-decisions.D-222.draft.md`
  `407dc663cd601e7d6197db0e39d83e6fd2ed57e46f4148903ea4ce324d14aec5`.
  Frozen occupancy
  `harness.DR-G19.state-class-authority.preview-classes.v2.json`
  `57f392b2cc30302e3c354781c56c37a30a9241e16e067fda6a281b27ed8691ac`
  Stage A Claude ACCEPT
  `236dd38f9ea90a1a7626dc245e820d326974eb4917c810bb18d5f5eede2e139d`
  0/0; Stage A Codex ACCEPT
  `c6d611d3ee349aea9ef731517310c00077adea5a14ded031a7fa15e962634fe4`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G19.state-class-authority.preview-classes.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-221. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G19.state-class-authority.preview-classes.v2.json`
  `57f392b2cc30302e3c354781c56c37a30a9241e16e067fda6a281b27ed8691ac`.
- **Decision:** Record v2 as G19 occupancy remasurement
  after D-221. The candidate binds NOTHING. DR-G19 stays
  `OPEN`. leftover-design of OBL-G19-HARNESS-SPEC remains
  measured closed at leftover-join.v3 (D-194). leftover-design
  of OBL-G19-FX-AUTHORING remains. Remainder is G19
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent a grant-journal. Does not invent a sealed-Run
  class. Does not apply state-class-contract.v10 or v11.
  Does not apply SUP-124-GRANT-JOURNAL. Does not steal
  OBL-GRANT-JOURNAL, OBL-INHERIT-BLOCKED, or
  OBL-MONOTONIC. Does not SATISFY DR-124. Does not
  SATISFY DR-117. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v1 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. v1 stays frozen; do not record it as current.
  Claude Stage A returned zero advisories and four unlabeled
  observationsNotFindings. Codex Stage A returned zero
  advisories. The Claude observations carry no identifier.
  Codex Stage A returned no observations. Claude Stage B
  returned four unlabeled observationsNotFindings; they
  carry no identifier. Codex Stage B returned zero
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G09, G10, G12, G14, G15, G16, G18, G19, G20,
  G21, G22, G31, or G32. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D222. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, or D-221.
- **Commit:** C-D222.

## D-223 — Record harness.DR-G23.provider-well-formed-admission.preview.v2 as G23 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-223.review-adversarial.claude2.json`,
  `c235c38f8929024a41d137c6a5de2d1f68f5f4fd47ce1c8641c1610a4d8fb09e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-223.review-adversarial.codex.json`,
  `fd5b88c82f8e2e2856f7f61e26e5b7f11b64daf972baeb44b39453c5d36fe284`)
  CONSENT. Subject `coordinator-decisions.D-223.draft.md`
  `e4e46d1c22f548bd60be48f5a086dd831f439192857d63b4d8ccd723cfd17299`.
  Frozen occupancy
  `harness.DR-G23.provider-well-formed-admission.preview.v2.json`
  `f48ba637bdf193785c05906a1686ce268b27b6ce7355de07fa5effefdd84fb0b`
  Stage A Claude ACCEPT
  `521743ea4bbae8789fb9d510396212a48f292bfd27001b2844b9d1b971e2e1bb`
  0/0; Stage A Codex ACCEPT
  `2dcade2af1281eeb46d2ef0aa73a9f5b12d6ea34c4dbf39456b5b471a6bba74e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G23.provider-well-formed-admission.preview.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-222. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G23.provider-well-formed-admission.preview.v2.json`
  `f48ba637bdf193785c05906a1686ce268b27b6ce7355de07fa5effefdd84fb0b`.
- **Decision:** Record v2 as G23 occupancy remasurement
  after D-222. The candidate binds NOTHING. DR-G23 stays
  `OPEN`. leftover-design of OBL-G23-HARNESS-SPEC,
  OBL-G23-NAMED-CORPUS, and OBL-G23-INPUT-CORPUS remains
  measured closed at leftover-join.v4 (D-198). leftover-design
  of OBL-G23-FX-AUTHORING remains. Remainder is G23
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-3 or NT-5 by existing. Does not reopen
  leftover-design of NT-3 and NT-5 as unnamed remainders.
  Does not treat naming v6 as naming G23. Does not import
  the unadopted D-143 G23 draft. Does not SATISFY DR-133.
  Does not SATISFY DR-117. Does not SATISFY DR-131. Gate 1
  Class A is not opened. Class B SATISFIED is not recorded.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Frozen v1 remains a historical occupancy as of
  HEAD `5d5d778` / required-now 26. v1 stays frozen; do not
  record it as current. Naming parent is D-147 turn-2 dual
  CONSENT, not naming v6. Claude Stage A returned zero
  advisories. Codex Stage A returned zero advisories.
  Claude Stage A returned no observations. Codex Stage A
  returned no observations. Claude Stage B returned zero
  advisories and no observations. Codex Stage B returned
  zero advisories and no observations. Does not execute
  fixtures. Does not rewrite G07, G08, G09, G10, G12, G14,
  G15, G16, G18, G19, G20, G21, G22, G31, or G32. Does not
  rewrite frozen G23 v1. Does not edit file 08. Does not
  invent a D9 code. Does not invent a finding schema. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D223. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, or D-222.
- **Commit:** C-D223.

## D-224 — Record harness.DR-G24.preview-analyze-well-formed-admission.preview.v3 as G24 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-224.review-adversarial.claude2.json`,
  `4e24bbf018586423fb2842c869d3dfbab357419d581acda6e157feaddce2741d`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-224.review-adversarial.codex.json`,
  `f8902eabdd939fe8e43366f84d972f2b082311f29c04ce232272192070f03598`)
  CONSENT. Subject `coordinator-decisions.D-224.draft.md`
  `5de3c23825bba31894f53d0c5b348bf75b33d85d4aef3dfc2973cd7a33412615`.
  Frozen occupancy
  `harness.DR-G24.preview-analyze-well-formed-admission.preview.v3.json`
  `ee41d14c7896ce97ebbf6611054991688ef1755499fbdc9d7f274498ebf9fdd4`
  Stage A Claude ACCEPT
  `f7a606a781287a774b84eb4c1333596bb71de1fb1ebbcbfdbeb1456e4e995ea5`
  0/0; Stage A Codex ACCEPT
  `e816a9cb76acdcca7dbd0500e40ebcd3be0d4a4343de20b98dc9dfb39bab8324`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G24.preview-analyze-well-formed-admission.preview.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-223. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G24.preview-analyze-well-formed-admission.preview.v3.json`
  `ee41d14c7896ce97ebbf6611054991688ef1755499fbdc9d7f274498ebf9fdd4`.
- **Decision:** Record v3 as G24 occupancy remasurement
  after D-223. The candidate binds NOTHING. DR-G24 stays
  `OPEN`. leftover-design of OBL-G24-HARNESS-SPEC,
  OBL-G24-NAMED-CORPUS, and OBL-G24-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-199). leftover-design
  of OBL-G24-FX-AUTHORING remains. Remainder is G24
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-1 or NT-2 by existing. Does not reopen
  leftover-design of NT-1 and NT-2 as unnamed remainders.
  Does not treat naming v6 as naming G24. Does not SATISFY
  DR-131. Does not SATISFY DR-117. Does not SATISFY DR-133.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains a historical
  occupancy as of HEAD `5d5d778` / required-now 26. Frozen v2
  remains a rejected occupancy (Claude MF-1 / Codex
  CODEX-G24-V2-SF1, one shared class: `$.doesNot[27]` said
  required-now 26). v3 repairs that sentence to `Does not
  change live required-now 28.` Naming parent is D-150 dual
  CONSENT, not naming v6. Occupancy v2 Claude returned
  advisories A-1 and A-2. Occupancy v2 Codex returned no
  advisories. Occupancy v3 Claude Stage A returned zero
  advisories. Occupancy v3 Codex Stage A returned zero
  advisories and no observations. Claude Stage B returned
  zero advisories and no observations. Codex Stage B
  returned zero advisories and no observations. The Claude
  v2 identifiers A-1 and A-2 are preserved. Codex v3
  returned no observation identifiers. Does not execute
  fixtures. Does not rewrite G07, G08, G09, G10, G12, G14,
  G15, G16, G18, G19, G20, G21, G22, G23, G31, or G32.
  Does not rewrite frozen G24 v1 or rejected G24 v2. Does
  not edit file 08. Does not invent a D9 code. Does not
  invent a pack IR. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D224. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, or D-223.
- **Commit:** C-D224.

## D-225 — Record harness.DR-G25.preview-analyze-missing-rung.preview.v3 as G25 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-225.review-adversarial.claude2.json`,
  `13c19cd44b9f128a5c0d592040cadb4e1729fb27c964d4aa93c7d12a96ca03c5`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-225.review-adversarial.codex.json`,
  `129dcdd867398d18f8980f55654f8434211915f6e8756b20d3f3179be9fe0927`)
  CONSENT. Subject `coordinator-decisions.D-225.draft.md`
  `52567a4b6354d6311a35ecc2febc1156d14f16e3ad1fd1aea70218d6351bff6d`.
  Frozen occupancy
  `harness.DR-G25.preview-analyze-missing-rung.preview.v3.json`
  `4f124cd763974b603fb307e13830cc7f79bc559c3b05ab7d39c59194d2f5dfde`
  Stage A Claude ACCEPT
  `1d7ccc76ddbd06298a5734362508153ca6f7f5781d0d1ec1834cd6f881e5d863`
  0/0; Stage A Codex ACCEPT
  `09f78d505b7bbb76987f020c5bf1fd87e66837f4796a2ed3dbd9dfd9d28059cb`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G25.preview-analyze-missing-rung.preview.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-224. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G25.preview-analyze-missing-rung.preview.v3.json`
  `4f124cd763974b603fb307e13830cc7f79bc559c3b05ab7d39c59194d2f5dfde`.
- **Decision:** Record v3 as G25 occupancy remasurement
  after D-224. The candidate binds NOTHING. DR-G25 stays
  `OPEN`. leftover-design of OBL-G25-HARNESS-SPEC,
  OBL-G25-NAMED-CORPUS, and OBL-G25-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-200). leftover-design
  of OBL-G25-FX-AUTHORING remains. Remainder is G25
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-3 by existing. Does not reopen leftover-design
  of DR-131 NT-3 as an unnamed remainder. Does not collapse
  the two NT-3 cells. Does not take over G23 DR-133 NT-3.
  Does not treat naming v6 as naming G25. Does not SATISFY
  DR-131. Does not SATISFY DR-117. Does not SATISFY DR-133.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains frozen.
  Frozen v2 remains a historical occupancy as of HEAD
  `5d5d778` / required-now 26. v1 and v2 stay frozen; do not
  record them as current. Naming parent is D-151 dual
  CONSENT, not naming v6. Claude Stage A returned three
  unlabeled observationsNotFindings. They carry no
  identifier. Codex Stage A returned zero advisories and no
  observations. Claude Stage B returned four unlabeled
  observationsNotFindings. They carry no identifier. Codex
  Stage B returned zero advisories and no observations.
  Does not invent identifiers for those unlabeled
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G09, G10, G12, G14, G15, G16, G18, G19, G20,
  G21, G22, G23, G24, G31, or G32. Does not rewrite frozen
  G25 v1 or frozen G25 v2. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D225. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, or D-224.
- **Commit:** C-D225.

## D-226 — Record harness.DR-G26.preview-analyze-sarif-not-advertised.preview.v2 as G26 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-226.review-adversarial.claude2.json`,
  `6bf6d9a352a9678013bc7a61a2a83719ad8d4a26585b5712b5fc6a80cb1c77ab`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-226.review-adversarial.codex.json`,
  `8daa5aab7bd8fd7968014a494e04a57c3c743f69a8472be39f52f762e93f8000`)
  CONSENT. Subject `coordinator-decisions.D-226.draft.md`
  `b56cabfbc438edbe42b7f0fbd3b60f6ef5a17999d8722397a9232b1d23f11692`.
  Frozen occupancy
  `harness.DR-G26.preview-analyze-sarif-not-advertised.preview.v2.json`
  `3a6f13799ef960170370a2a74930d62778a9671b2065ac3e83ca485c21721ffb`
  Stage A Claude ACCEPT
  `70a5accdbf11e61f3c792d253cf31cd329ead0fefbc142230236813fb217fb98`
  0/0; Stage A Codex ACCEPT
  `4fad0aaa9f7d6158a225257342f9e887dc85969052f205af18161d022a3979f2`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G26.preview-analyze-sarif-not-advertised.preview.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-225. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G26.preview-analyze-sarif-not-advertised.preview.v2.json`
  `3a6f13799ef960170370a2a74930d62778a9671b2065ac3e83ca485c21721ffb`.
- **Decision:** Record v2 as G26 occupancy remasurement
  after D-225. The candidate binds NOTHING. DR-G26 stays
  `OPEN`. leftover-design of OBL-G26-HARNESS-SPEC,
  OBL-G26-NAMED-CORPUS, and OBL-G26-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-201). leftover-design
  of OBL-G26-FX-AUTHORING remains. Remainder is G26
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-5 by existing. Does not reopen leftover-design
  of DR-131 NT-5 as an unnamed remainder. Does not take
  over G23 DR-133 NT-5. Does not restore G17 or name G17
  into required-now. Does not treat naming v6 as naming G26.
  Does not SATISFY DR-131. Does not SATISFY DR-117. Does
  not SATISFY DR-133. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v1 remains a
  historical occupancy as of HEAD `5d5d778` / required-now
  26. v1 stays frozen; do not record it as current. Naming
  parent is D-152 dual CONSENT, not naming v6. Claude
  Stage A returned zero advisories. Codex Stage A returned
  zero advisories and no observations. Claude Stage B
  returned zero advisories and no observations. Codex
  Stage B returned zero advisories and no observations.
  Does not execute fixtures. Does not rewrite G07, G08,
  G09, G10, G12, G14, G15, G16, G18, G19, G20, G21, G22,
  G23, G24, G25, G31, or G32. Does not rewrite frozen G26
  v1. Does not edit file 08. Does not invent a D9 code.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D226. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, or D-225.
- **Commit:** C-D226.

## D-227 — Record harness.DR-G27.preview-analyze-not-sealed-run.preview.v2 as G27 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-227.review-adversarial.claude2.json`,
  `c2b097d4a44af54120cf9915a8db9f291b3e0b32a3d16b7fa434eb05efbbfd77`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-227.review-adversarial.codex.json`,
  `3ad0d05b255b081edc327924edcfcc647c24cb0759df0badbd1e78bef956a4c1`)
  CONSENT. Subject `coordinator-decisions.D-227.draft.md`
  `adc02f50bbcb7180ec46d0554efb3db2e52df53f066dabc9313b30dd6f933aa6`.
  Frozen occupancy
  `harness.DR-G27.preview-analyze-not-sealed-run.preview.v2.json`
  `436a60117e50d8716e52b7700195dd9fd053151abb0130148efab99f28a65794`
  Stage A Claude ACCEPT
  `ad85731a624e696e0a4bf3492884a3cc152faa88ad03a886bf5ad68501a724fb`
  0/0; Stage A Codex ACCEPT
  `2f43e047a1ce6dd5baf873b0c2d1113704a56b9f05c2b0be00f12d03c1b9985e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G27.preview-analyze-not-sealed-run.preview.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-226. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G27.preview-analyze-not-sealed-run.preview.v2.json`
  `436a60117e50d8716e52b7700195dd9fd053151abb0130148efab99f28a65794`.
- **Decision:** Record v2 as G27 occupancy remasurement
  after D-226. The candidate binds NOTHING. DR-G27 stays
  `OPEN`. leftover-design of OBL-G27-HARNESS-SPEC,
  OBL-G27-NAMED-CORPUS, and OBL-G27-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-202). leftover-design
  of OBL-G27-FX-AUTHORING remains. Remainder is G27
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-6 by existing. Does not reopen leftover-design
  of DR-131 NT-6 as an unnamed remainder. Does not take
  over G21 DR-133 NT-6. Does not invent a sealed-Run class.
  Does not take over G19. Does not treat naming v6 as
  naming G27. Does not SATISFY DR-131. Does not SATISFY
  DR-117. Does not SATISFY DR-133. Gate 1 Class A is not
  opened. Class B SATISFIED is not recorded. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v1 remains a historical occupancy as of HEAD `5d5d778` /
  required-now 26. v1 stays frozen; do not record it as
  current. Naming parent is D-153 dual CONSENT, not naming
  v6. Claude Stage A returned seven unlabeled
  observationsNotFindings. They carry no identifier. Codex
  Stage A returned zero advisories and no observations.
  Claude Stage B returned six unlabeled
  observationsNotFindings. They carry no identifier. Codex
  Stage B returned zero advisories and no observations.
  Does not invent identifiers for those unlabeled
  observations. Does not execute fixtures. Does not rewrite
  G07, G08, G09, G10, G12, G14, G15, G16, G18, G19, G20,
  G21, G22, G23, G24, G25, G26, G31, or G32. Does not
  rewrite frozen G27 v1. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D227. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  or D-226.
- **Commit:** C-D227.

## D-228 — Record harness.DR-G28.preview-analyze-host-must-not-mint.preview.v4 as G28 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-228.review-adversarial.claude2.json`,
  `ba8ca842073f3f828421d688a484b7edd885ccb0f8a9c9068c786092216e853e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-228.review-adversarial.codex.json`,
  `da15cf6125c3d74bc609c73a5c3837c7d244aee5677d1aba22221824c7212dc6`)
  CONSENT. Subject `coordinator-decisions.D-228.draft.md`
  `7c27037feedb838507859be1a99ca6a47ccd9af0509dd3ac9ea9ea219d5b829a`.
  Frozen occupancy
  `harness.DR-G28.preview-analyze-host-must-not-mint.preview.v4.json`
  `e540ea53b8cfd4e75c05eabfb4c321dca566161b135dc630c2bd1fec5d31ff4d`
  Stage A Claude ACCEPT
  `7c1916d16f08c9564cd788749335bd8c945b57818161d5641c1a2e790e6ff1cd`
  0/0; Stage A Codex ACCEPT
  `308ac423a4548040187dd9304a576f4ac153c6906788f7ef135651f9131eaf54`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G28.preview-analyze-host-must-not-mint.preview.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-227. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G28.preview-analyze-host-must-not-mint.preview.v4.json`
  `e540ea53b8cfd4e75c05eabfb4c321dca566161b135dc630c2bd1fec5d31ff4d`.
- **Decision:** Record v4 as G28 occupancy remasurement
  after D-227. The candidate binds NOTHING. DR-G28 stays
  `OPEN`. leftover-design of OBL-G28-HARNESS-SPEC,
  OBL-G28-NAMED-CORPUS, and OBL-G28-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-203). leftover-design
  of OBL-G28-FX-AUTHORING remains. Remainder is G28
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute NT-7 or NT-8 by existing. Does not reopen
  leftover-design of DR-131 NT-7 and NT-8 as unnamed
  remainders. Does not invent a D9 code. Does not treat
  naming v6 as naming G28. Does not SATISFY DR-131. Does
  not SATISFY DR-117. Does not SATISFY DR-133. Gate 1 Class
  A is not opened. Class B SATISFIED is not recorded. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v1, v2, and v3 remain historical. v3 remains
  a historical occupancy as of HEAD `5d5d778` / required-now
  26. Do not record them as current. Naming parent is D-154
  dual CONSENT, not naming v6. Claude Stage A returned
  advisories CLAUDE-G28-V4-A1 and CLAUDE-G28-V4-A2. Codex
  Stage A returned zero advisories and no observations.
  Claude Stage B returned observations OBS-1, OBS-2, OBS-3,
  OBS-4, and OBS-5. They carry those identifiers. Codex
  Stage B returned zero advisories and no observations.
  The Claude identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G07, G08, G09, G10, G12, G14, G15, G16, G18,
  G19, G20, G21, G22, G23, G24, G25, G26, G27, G31, or
  G32. Does not rewrite frozen G28 v1, v2, or v3. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D228. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, or D-227.
- **Commit:** C-D228.


## D-229 — Record harness.DR-G29.preview-boundary-excluded-form-admission.preview.v3 as G29 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-229.review-adversarial.claude2.json`,
  `eea97a3d23f9b7965b0b204b1c25cc000a5b8953acec0e8dde699b0cc1e75dab`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-229.review-adversarial.codex.json`,
  `f35c8568cc766efabe49c9c2c4ee222dc83b7a5fe317abcb4ca2455e94e938c0`)
  CONSENT. Subject `coordinator-decisions.D-229.draft.md`
  `ab669080e771d7f3a8ff9b4deaf769712ef1cf86f43d31c4d08a71a3dc89d901`.
  Frozen occupancy
  `harness.DR-G29.preview-boundary-excluded-form-admission.preview.v3.json`
  `94a40de95097afbf51e50461bac54f5fc95326215cf94e89a2f3655c731be96d`
  Stage A Claude ACCEPT
  `1293c3dda996285f58a32ca2ad4592763df8f54e563aac17bc840a231dab109f`
  0/0; Stage A Codex ACCEPT
  `7e3ed317c94e2278a637fae728a2d32b535e42c1056dfec78c111c1e05fe0e53`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G29.preview-boundary-excluded-form-admission.preview.v3.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-228. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G29.preview-boundary-excluded-form-admission.preview.v3.json`
  `94a40de95097afbf51e50461bac54f5fc95326215cf94e89a2f3655c731be96d`.
- **Decision:** Record v3 as G29 occupancy remasurement
  after D-228. The candidate binds NOTHING. DR-G29 stays
  `OPEN`. leftover-design of OBL-G29-HARNESS-SPEC,
  OBL-G29-NAMED-CORPUS, and OBL-G29-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-204). leftover-design
  of OBL-G29-FX-AUTHORING remains. Remainder is G29
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute EE-1, EE-2, EE-3b, EE-4, EE-5a, EE-5b, or EE-6a
  by existing. Does not reopen leftover-design of those EE
  classes as unnamed remainders. Does not invent a D9 code.
  Does not invent a section 7.1 recipe. Does not treat
  naming v6 as naming G29. Does not SATISFY DR-117. Does
  not SATISFY DR-131. Does not SATISFY DR-133. Gate 1 Class
  A is not opened. Class B SATISFIED is not recorded. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Frozen v1 and v2 remain historical. v2 remains a
  historical occupancy as of HEAD `5d5d778` / required-now
  26. Do not record them as current. Naming parent is D-157
  turn-2 dual CONSENT, not naming v6, and not D-157 turn-1
  Codex OBJECT. Claude Stage A returned six
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage A returned zero advisories and no observations.
  Claude Stage B returned seven observationsNotFindings
  strings. They carry no identifiers. Codex Stage B returned
  zero advisories and no observations. This entry does not
  invent identifiers for those observations and does not
  claim that both reviewers' identifiers are preserved.
  Codex returned no observation identifiers. Does not
  execute fixtures. Does not rewrite G07, G08, G09, G10,
  G12, G14, G15, G16, G18, G19, G20, G21, G22, G23, G24,
  G25, G26, G27, G28, G30, G31, or G32. Does not rewrite
  frozen G29 v1 or v2. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D229. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, or D-228.
- **Commit:** C-D229.

## D-230 — Record harness.DR-G30.preview-boundary-install-shape.preview.v2 as G30 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-230.review-adversarial.claude2.json`,
  `43a61197296c44e65c6a8a8e695d800a2245ed9e0300a729ef9d2d64076d1252`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-230.review-adversarial.codex.json`,
  `cc9c81e15e9de2d5ee090cbb113a8ceb1fea58ec501174a4f09a6a92513c0837`)
  CONSENT. Subject `coordinator-decisions.D-230.draft.md`
  `564a7abdcaae464c3ef7db7440e431dcca35cdbb4b377e4e7d8db8431ccfe89a`.
  Frozen occupancy
  `harness.DR-G30.preview-boundary-install-shape.preview.v2.json`
  `371695b8fc7b5cf61e016508da69436fbe6146683979f0c2468f52757a16cfda`
  Stage A Claude ACCEPT
  `43d6b2c576ba745686b2c4a7004722d7a8eecbf6da556b00bde86401c7398003`
  0/0; Stage A Codex ACCEPT
  `e968cbeee48a8f8a402c60c6fbd57263ff06c73030cfb68c4bb06a1e0924d897`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G30.preview-boundary-install-shape.preview.v2.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-229. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G30.preview-boundary-install-shape.preview.v2.json`
  `371695b8fc7b5cf61e016508da69436fbe6146683979f0c2468f52757a16cfda`.
- **Decision:** Record v2 as G30 occupancy remasurement
  after D-229. The candidate binds NOTHING. DR-G30 stays
  `OPEN`. leftover-design of OBL-G30-HARNESS-SPEC,
  OBL-G30-NAMED-CORPUS, and OBL-G30-INPUT-CORPUS remains
  measured closed at leftover-join.v3 (D-205). leftover-design
  of OBL-G30-FX-AUTHORING remains. Remainder is G30
  execution once fixture implementations exist. Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  execute EE-7a, EE-7b, or EE-7d by existing. Does not
  reopen leftover-design of those EE classes as unnamed
  remainders. Does not invent a D9 code. Does not invent
  a PlanIntent schema. Does not invent a section 7.1 recipe.
  Does not treat naming v6 as naming G30. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains a historical
  occupancy as of HEAD `5d5d778` / required-now 26. Do not
  record it as current. Naming parent is D-158 turn-2 dual
  CONSENT, not naming v6, and not D-158 turn-1 Claude OBJECT.
  Claude Stage A returned seven observationsNotFindings
  strings. They carry no identifiers. Codex Stage A returned
  zero advisories and no observations. Claude Stage B
  returned seven observationsNotFindings strings. They carry
  no identifiers. Codex Stage B returned zero advisories
  and no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G07, G08, G09, G10, G12, G14, G15, G16, G18,
  G19, G20, G21, G22, G23, G24, G25, G26, G27, G28, G29,
  G31, or G32. Does not rewrite frozen G30 v1. Does not
  edit file 08. Does not invent a D9 code. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D230. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, or D-229.
- **Commit:** C-D230.

## D-231 — Record harness.DR-G01.core-download.v9 as G01 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-231.review-adversarial.claude2.json`,
  `a2661f8d7d7c6b23290e2d91f982ab866a3fea20b21b5bebdcedb5f5761da656`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-231.review-adversarial.codex.json`,
  `7604fac547af1c3cfb020a46182504813adab78b3c8e2b2181798ea826636560`)
  CONSENT. Subject `coordinator-decisions.D-231.draft.md`
  `6baf018e8ce2e0b1fd547b0f0c2ed9162b593b78f9af30450b5f5a5533e7d05e`.
  Frozen occupancy
  `harness.DR-G01.core-download.v9.json`
  `f28b0d97723550c8690eec2a6ac7803efba93fd797f266600b038b14e269277b`
  Stage A Claude ACCEPT
  `6f697ee39f5cb170693f1f23f6daf36b56ee63ad37aef8685e004f73bfab7a01`
  0/0; Stage A Codex ACCEPT
  `b9755e1ea407c25da1acb43e66264467da397603c7f87e2591935d80ecfc213f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G01.core-download.v9.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-230. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G01.core-download.v9.json`
  `f28b0d97723550c8690eec2a6ac7803efba93fd797f266600b038b14e269277b`.
- **Decision:** Record v9 as G01 occupancy remasurement
  after D-230. The candidate binds NOTHING. DR-G01 stays
  `OPEN`. leftover-design of the G01 specification-authoring
  limb of OBL-2 remains measured stale at leftover-join.v7
  (D-173). leftover-design of OBL-2, OBL-D1, and OBL-D2
  remains. Remainder of OBL-2 is (a) D-006 unit and G02
  tree-accounting UNDECIDED, so size comparison cannot be
  scored, and (b) G01-G05 execution, which remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D-006 unit or
  authorize 26214400 as the bound. Does not mint
  Rust-as-core. Does not take over G02, G03, G04, G05, G07,
  G14, or G22. Does not SATISFY DR-101. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains the CGHS
  promised-path occupancy. Frozen v3 remains a historical
  thin-extraction occupancy as of HEAD `5d5d778` /
  required-now 26. Frozen v4 through v8 remain historical
  reject-cycle occupancies. Do not record v1 through v8 as
  current. Naming parent is naming v6 (D-145) dual ACCEPT
  0/0, not leftover-join.v7. This occupancy does not occupy
  the G30 identifier. Advisory CLAUDE-G01H-V9-ADV1 travels
  as honesty work. Codex Stage A returned zero advisories
  and no observations. Claude Stage B returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G02, G03, G04, G05, G07, G08, G09, G10, G12,
  G14, G15, G16, G18, G19, G20, G21, G22, G23, G24, G25,
  G26, G27, G28, G29, G30, G31, or G32. Does not rewrite
  frozen G01 v1 through v8. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D231. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, D-229, or D-230.
- **Commit:** C-D231.

## D-232 — Record harness.DR-G02.core-installed.v4 as G02 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-232.review-adversarial.claude2.json`,
  `41ad4bea3c7476c7745e6ea945b9fff2e1035b71fd0b47ba8d3f5ef3fe7d2c72`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-232.review-adversarial.codex.json`,
  `9e4ec2b494e184da72f9984a34e66117373009253bc1673cf180e4447e1610fb`)
  CONSENT. Subject `coordinator-decisions.D-232.draft.md`
  `60356948565d0f228ba751cca3b2c3c170571d0e568e363fee58fedc9318e680`.
  Frozen occupancy
  `harness.DR-G02.core-installed.v4.json`
  `1bc247f779fa980ecde7d7a244effa6116f02a79be4a0ee74e0cedb168ccf360`
  Stage A Claude ACCEPT
  `e5d6d9aacbc090381ae85ef792f0c1beb8cf510f4dfd5020873ca32b7de18a1b`
  0/0; Stage A Codex ACCEPT
  `dad3667f6c92b514822d1222428b5ef7d9aba51b49b01c3fefdb9d20a9eb309f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G02.core-installed.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-231. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G02.core-installed.v4.json`
  `1bc247f779fa980ecde7d7a244effa6116f02a79be4a0ee74e0cedb168ccf360`.
- **Decision:** Record v4 as G02 occupancy remasurement
  after D-231. The candidate binds NOTHING. DR-G02 stays
  `OPEN`. leftover-design of the G02 specification-authoring
  limb of OBL-2 remains measured stale at leftover-join.v7
  (D-173). leftover-design of OBL-2, OBL-D1, and OBL-D2
  remains. Remainder of OBL-2 is (a) D-006 unit and G02
  tree-accounting UNDECIDED, so size comparison cannot be
  scored, and (b) G01-G05 execution, which remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D-006 unit or
  authorize 83886080 as the bound. Does not invent G02
  tree-accounting. Does not mint Rust-as-core. Does not
  decide L-TCB identity. Does not populate the per-OS TCB
  table. Does not retarget DR-126. Does not take over G01,
  G03, G04, G05, G07, G14, or G22. Does not SATISFY DR-101.
  Does not SATISFY DR-117. Does not SATISFY DR-131. Does
  not SATISFY DR-133. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v1 remains
  the CGHS promised-path occupancy. Frozen v3 remains a
  historical thin-extraction occupancy as of HEAD `5d5d778`
  / required-now 26. Frozen v2 remains a historical
  thin-extraction occupancy. Do not record v1 through v3 as
  current. Naming parent is naming v6 (D-145) dual ACCEPT
  0/0, not leftover-join.v7. This occupancy does not occupy
  the G01 identifier. Claude Stage A returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage A returned zero advisories and
  no observations. Claude Stage B returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G01, G03, G04, G05, G07, G08, G09, G10, G12,
  G14, G15, G16, G18, G19, G20, G21, G22, G23, G24, G25,
  G26, G27, G28, G29, G30, G31, or G32. Does not rewrite
  frozen G02 v1 through v3. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D232. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, D-229, D-230, or D-231.
- **Commit:** C-D232.

## D-233 — Record harness.DR-G03.core-startup.v5 as G03 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-233.review-adversarial.claude2.json`,
  `092551fff0203a8f46325f232d08a51e46a7150fa0bae8935a04ae919736a686`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-233.review-adversarial.codex.json`,
  `74f4ed01c1a0aecd19c241dcd78fbf1bdc78473f35701103666797aac92982b8`)
  CONSENT. Subject `coordinator-decisions.D-233.draft.md`
  `756471d245710002be2d7c88136a3b10c6d6924b599afb97de6e7f232a82d830`.
  Frozen occupancy
  `harness.DR-G03.core-startup.v5.json`
  `398ec6474eacbc4b873488dd07bce0e6295c2149d9d2794a177d13a96ebb8324`
  Stage A Claude ACCEPT
  `59ecb89a05d252aaf12f7dd8a2e836a78a6f1c45fd9d36906f19f65bb202237d`
  0/0; Stage A Codex ACCEPT
  `b4830b00e1fa69e731c477af43aa19b3fc931e65f9a4cbd99c706be67003df4c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G03.core-startup.v5.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-232. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G03.core-startup.v5.json`
  `398ec6474eacbc4b873488dd07bce0e6295c2149d9d2794a177d13a96ebb8324`.
- **Decision:** Record v5 as G03 occupancy remasurement
  after D-232. The candidate binds NOTHING. DR-G03 stays
  `OPEN`. leftover-design of the G03 specification-authoring
  limb of OBL-2 remains measured stale at leftover-join.v7
  (D-173). leftover-design of OBL-2, OBL-D1, and OBL-D2
  remains. Remainder of OBL-2 is (a) D-006 unit and G02
  tree-accounting UNDECIDED, so size comparison cannot be
  scored, and (b) G01-G05 execution, which remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D-006 unit. Does
  not amend D-102. Does not invent a machine identifier
  outside D-102. Does not treat warm p50 as a
  fail-qualification bound. Does not take over G01, G02,
  G04, G05, G07, G14, or G22. Does not SATISFY DR-101. Does
  not SATISFY DR-117. Does not SATISFY DR-131. Does not
  SATISFY DR-133. Gate 1 Class A is not opened. Class B
  SATISFIED is not recorded. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Frozen v4 remains
  the CGHS promised-path occupancy. Frozen v1 remains a
  historical occupancy that was Claude REJECT 0/1
  CLAUDE-G03-V1-SF1. Do not record v1 through v4 as current.
  Naming parent is naming v6 (D-145) dual ACCEPT 0/0, not
  leftover-join.v7. This occupancy does not occupy the G01
  or G02 identifier. Claude Stage A returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage A returned zero advisories and
  no observations. Claude Stage B returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G01, G02, G04, G05, G07, G08, G09, G10, G12,
  G14, G15, G16, G18, G19, G20, G21, G22, G23, G24, G25,
  G26, G27, G28, G29, G30, G31, or G32. Does not rewrite
  frozen G03 v1 through v4. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D233. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, D-229, D-230, D-231, or D-232.
- **Commit:** C-D233.

## D-234 — Record harness.DR-G04.core-memory.v4 as G04 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-234.review-adversarial.claude2.json`,
  `47e3d7c530d29f23c2fac658ace1655649e475334a37a10a97887ee944342217`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-234.review-adversarial.codex.json`,
  `084d4d8a4f80e9314aab8d53042d7c4fa77dd7f8ca4a48043ce8f160d9b552cf`)
  CONSENT. Subject `coordinator-decisions.D-234.draft.md`
  `0049578230e1aa69abc96482f490cb61b7fc3ea9c2ac0dce7a87cc981fe34bbf`.
  Frozen occupancy
  `harness.DR-G04.core-memory.v4.json`
  `f664f7fd7a428dc9fd05a3142f5a50a242704659d72f66fb509c66106e4e7845`
  Stage A Claude ACCEPT
  `ddb984e5ff3a4fc7c3f7ccb27229827a2e44d3a4b3307c72f967a215fca43808`
  0/0; Stage A Codex ACCEPT
  `b883e6914e3d5a1fad59fe767d5f9993b6584a215e2f37e19509e82eaad5cc15`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G04.core-memory.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-233. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G04.core-memory.v4.json`
  `f664f7fd7a428dc9fd05a3142f5a50a242704659d72f66fb509c66106e4e7845`.
- **Decision:** Record v4 as G04 occupancy remasurement
  after D-233. The candidate binds NOTHING. DR-G04 stays
  `OPEN`. leftover-design of the G04 specification-authoring
  limb of OBL-2 remains measured stale at leftover-join.v7
  (D-173). leftover-design of OBL-2, OBL-D1, and OBL-D2
  remains. Remainder of OBL-2 is (a) D-006 unit and G02
  tree-accounting UNDECIDED, so size comparison cannot be
  scored, and (b) G01-G05 execution, which remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D-006 unit or
  authorize a binary-MB byte constant. Does not amend
  D-102. Does not score analyze RSS or consented-probe RSS
  as this gate. Does not take over G01, G02, G03, G05, G07,
  G14, or G22. Does not SATISFY DR-101. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Gate 1 Class A is not opened. Class B SATISFIED is not
  recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains the CGHS
  promised-path occupancy. Frozen v3 remains a historical
  occupancy that was Claude REJECT 1 BLOCKER
  CLAUDE-G04H-V3-B1. CLAUDE-G04H-V3-B1 is landed. Do not
  record v1 through v3 as current. Naming parent is naming
  v6 (D-145) dual ACCEPT 0/0, not leftover-join.v7. This
  occupancy does not occupy the G03 identifier. Claude
  Stage A returned four observationsNotFindings strings.
  They carry no identifiers. Codex Stage A returned zero
  advisories and no observations. Claude Stage B returned
  three observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G01, G02, G03, G05, G07, G08, G09, G10, G12,
  G14, G15, G16, G18, G19, G20, G21, G22, G23, G24, G25,
  G26, G27, G28, G29, G30, G31, or G32. Does not rewrite
  frozen G04 v1 through v3. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D234. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, D-229, D-230, D-231, D-232, or
  D-233.
- **Commit:** C-D234.

## D-235 — Record harness.DR-G05.component-delta.v4 as G05 occupancy remasurement

- **Date:** 2026-08-22
- **Status:** **ADOPTED 2026-08-22.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-235.review-adversarial.claude2.json`,
  `e7d2bd64243a789b5b1e8bf6a0d21c1c0dd3d9ffecd989f6160a1cc8a012ee5a`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-235.review-adversarial.codex.json`,
  `5286cc6719ea3025ba2c26dfb6713a47e4007e38255ca8db6cdfb132a6b006c2`)
  CONSENT. Subject `coordinator-decisions.D-235.draft.md`
  `9df3a3d769c760657504ea7f3c5af3de7ab09a69f4019baf7dd5adc1935fc640`.
  Frozen occupancy
  `harness.DR-G05.component-delta.v4.json`
  `fb1b2158f16d07814a6c5f67166faadb12d122353f26d23e804060f7687b7875`
  Stage A Claude ACCEPT
  `104794547ae7cf489faf06f797d8ce2ce05c4810ef77d76696ed7d90da6f5877`
  0/0; Stage A Codex ACCEPT
  `54ab5290aee27b0d8eef5bc7173f40754ef81f83c56c809a513507e522098839`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of
  `harness.DR-G05.component-delta.v4.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-234. Not a three-limb act.
- **Subject:** `docs/coop/artifacts/harness.DR-G05.component-delta.v4.json`
  `fb1b2158f16d07814a6c5f67166faadb12d122353f26d23e804060f7687b7875`.
- **Decision:** Record v4 as G05 occupancy remasurement
  after D-234. The candidate binds NOTHING. DR-G05 stays
  `OPEN`. leftover-design of the G05 specification-authoring
  limb of OBL-2 remains measured stale at leftover-join.v7
  (D-173). leftover-design of OBL-2, OBL-D1, and OBL-D2
  remains. Remainder of OBL-2 is (a) D-006 unit and G02
  tree-accounting UNDECIDED, so size comparison cannot be
  scored, and (b) G01-G05 execution, which remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D-006 unit. Does
  not invent a numeric cap. Does not invent G02
  tree-accounting. Does not take over G01, G02, G03, G04,
  G07, G14, or G22. Does not SATISFY DR-101. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Gate 1 Class A is not opened. Class B SATISFIED
  is not recorded. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v1 remains the CGHS
  promised-path occupancy. Frozen v3 remains a historical
  thin-extraction occupancy. Do not record v1 through v3 as
  current. Naming parent is naming v6 (D-145) dual ACCEPT
  0/0, not leftover-join.v7. This occupancy does not occupy
  the G04 identifier. Advisory CLAUDE-G05H-V4-ADV1 travels
  as honesty work. Codex Stage A returned zero advisories
  and no observations. Claude Stage A returned four
  observationsNotFindings strings. They carry no
  identifiers. Claude Stage B returned three
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute fixtures. Does
  not rewrite G01, G02, G03, G04, G07, G08, G09, G10, G12,
  G14, G15, G16, G18, G19, G20, G21, G22, G23, G24, G25,
  G26, G27, G28, G29, G30, G31, or G32. Does not rewrite
  frozen G05 v1 through v3. Does not edit file 08. Does not
  invent a D9 code. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  4 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D235. Does not unwrite D-167, D-168, D-169,
  D-170, D-171, D-172, D-173, D-174, D-175, D-176, D-177,
  D-178, D-179, D-180, D-181, D-182, D-183, D-184, D-185,
  D-186, D-187, D-188, D-189, D-190, D-191, D-192, D-193,
  D-194, D-195, D-196, D-197, D-198, D-199, D-200, D-201,
  D-202, D-203, D-204, D-205, D-206, D-207, D-208, D-209,
  D-210, D-211, D-212, D-213, D-214, D-215, D-216, D-217,
  D-218, D-219, D-220, D-221, D-222, D-223, D-224, D-225,
  D-226, D-227, D-228, D-229, D-230, D-231, D-232, D-233,
  or D-234.
- **Commit:** C-D235.

---

## D-236 — Record DR-104 SATISFIED under D-056 Class B

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-236.review-adversarial.claude2.json`,
  `b21f6e3bca54ad0cb2bd3e21b9bf9fab04a9eb94082b4aa41181a92790a1a048`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-236.review-adversarial.codex.json`,
  `113f19ace51bd43fa22bad3966117cd2cc120e93261e23ebb881273ed76ab97b`)
  CONSENT. Subject `coordinator-decisions.D-236.draft.md`
  `fb64e7b986274f459907cc47eebfe8302bbfb3217e06a1792c1e52073712ed15`.
  Both SATISFIED-GRADE reviews returned 0 blockers, 0 MUST-FIX,
  0 SHOULD-FIX.
- **Decision type:** RULE-GOVERNED. SATISFIED re-record under
  D-056 Class B. File-08 MF-6. Does not execute G31. Does not
  claim QUALIFIED. Not a three-limb act. Not a required-now
  successor.
- **Subject:** `docs/coop/artifacts/coordinator-decisions.D-236.draft.md`
  `fb64e7b986274f459907cc47eebfe8302bbfb3217e06a1792c1e52073712ed15`.
- **Decision:** Record DR-104 SATISFIED for architecture-preview
  condition 2 under D-056 Class B. Negative-test execution
  remains condition 4 / DR-G31 / DR-012 qualification. It is
  not architecture SATISFIED evidence and is not an
  architecture hard blocker. Not QUALIFIED. D-012's decided
  identity/namespace policy stands. D-012 deferrals remain
  deferred. D-130's eleven classes stand. leftover-join.v6
  binds NOTHING and is not this SATISFIED. Replace the unique
  DR-104 lead prefix
  `**DECIDED-V1-NOT-INTEGRATED** — DECIDED (D-012):` and the
  unique Blueprint-impact suffix
  `negative-test evidence at qualification | Hard blocker |`.
  Rewrite condition 2 to 5 of 32 SATISFIED, standing NOT MET,
  preserving D-085 / D-089 / D-091 / D-092 remainders, adding
  the DR-104 G31 remainder, and restoring the DR-103 contract
  note and the DR-131/DR-133 ineligible-in-kind note. Replace
  only "condition 2 remains 4 of 32 SATISFIED" in the
  one-sentence summary. Do not edit gate-harness cells. Do
  not mark DR-103/105/114/117/118/131/133 SATISFIED. Do not
  SATISFY DR-101. Do not open Class A. Do not apply
  identity-namespace-integration-contract.v4. Do not execute
  the eleven classes. Do not invent leftover-design or
  fixture bytes. Do not add a DR-G* row. Do not change live
  required-now 28. Do not authorize `docs/v2/implementation/`.
  Claude SATISFIED-GRADE returned five
  observationsNotFindings strings. They carry no
  identifiers. Codex SATISFIED-GRADE returned zero
  advisories and no observations. This entry does not invent
  identifiers for those observations and does not claim that
  both reviewers' identifiers are preserved. Codex returned
  no observation identifiers.
- **Readiness effect:** Condition 2 becomes 5 of 32 SATISFIED
  and stays NOT MET. Condition 4 stays MET on the naming
  half (28 of 28). Condition 5 remains NOT MET and last.
- **Reversibility:** C-D236 plus restore of the prior unique
  DR-104 lead prefix, prior Blueprint impact cell, prior
  condition-2 snapshot including every named remainder this
  rewrite preserves, and the prior "4 of 32" clause. Does
  not overturn D-012, D-056, D-085, D-089, D-091, D-092,
  D-130, D-131, D-133, D-135, D-137, D-167, D-175, D-208,
  or D-235. Overturn: C-D236.
- **Commit:** C-D236.

---

## D-237 — Record g23-fixture-corpus.v3 as G23 leftover-design fixture implementations

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-237.review-adversarial.claude2.json`,
  `5e573bfe9a20e44622edb71079967785eae324c7bd399c65a1856ea1d31eaead`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-237.review-adversarial.codex.json`,
  `e7acfe640baeb0a941018572da5fb1bce68406f6c884ae3afdd2517690bde52c`)
  CONSENT. Subject `coordinator-decisions.D-237.draft.md`
  `fe20a1e22f59b90c257d0be83b3d3d7942f9a794cceff82db4ef1ba078aaf263`.
  Frozen corpus
  `g23-fixture-corpus.v3.json`
  `3576e2e606b3eed68feced5b83a34247263d3b563274ef3fd9054c8b2a2ba6a7`
  Stage A Claude ACCEPT
  `9d8d3919b8f17d60a0d526398093ed8447d53acf9cf009431ab5d290d5a071d5`
  0/0; Stage A Codex ACCEPT
  `0285ff4a3a6a783e7ca4fe0fbf49bb032b1de0389b450a06461cf91cc582b044`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g23-fixture-corpus.v3.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g23-fixture-corpus.v3.json`
  `3576e2e606b3eed68feced5b83a34247263d3b563274ef3fd9054c8b2a2ba6a7`.
- **Decision:** Record v3 as G23 leftover-design fixture
  implementations after D-236. The candidate binds NOTHING.
  DR-G23 stays `OPEN`. leftover-design of
  OBL-G23-FX-AUTHORING remains on leftover-join.v4 (D-198).
  Remainder of G23 execution, including host
  relation-registry refusal observation and
  subsequent-session view, remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent a finding schema.
  Does not invent a D9 code. Does not invent a section 7.1
  recipe. Does not collapse EV-2 into EV-3. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-101. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Frozen v1 and v2 remain historical REJECT. Do
  not record v1 or v2 as current. Naming parent is D-147,
  not leftover-join.v4. Claude Stage A returned five
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage A returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Claude Stage B returned five
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. Does not execute G23. Does not rewrite
  leftover-join.v4. Does not rewrite occupancy v2. Does not
  edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D237. Does not unwrite D-147, D-198, D-223,
  or D-236.
- **Commit:** C-D237.

## D-238 — Record g23-leftover-join.v7 as G23 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-238.review-adversarial.claude2.turn2.json`,
  `cd542ae209f9d73de75a66e313ce93445be3eb40e394a46f96d751cdfc3ed53d`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-238.review-adversarial.codex.turn2.json`,
  `1911a17683666200a4754b543de9126e82159d76bf4fc5205b7274221761012b`)
  CONSENT. Subject `coordinator-decisions.D-238.turn2.draft.md`
  `8f30fd4a286166ae767ff6d5a7f92f0025ae0a051081ee08a7edc35b87ed7ba5`.
  Turn-1 Claude OBJECT (CLAUDE-D238-M1) at
  `4f78b0e00ec3a2a1966a829551c0a35d3535de66410180cb46dc4fcd769a4f0a`;
  turn-1 Codex OBJECT (D238-SF-1)
  `3b34bd4464e2823a5bb3d367ffa5e761a6e85963730f157b3a12327090f39266`.
  Frozen leftover-join
  `g23-leftover-join.v7.json`
  `22a52b01a58a44e6162999d1b18bd76945086e3563724106ca05d62eeba90c5b`
  Stage A Claude ACCEPT
  `14817c408761d3c6c8e537431c654d55a92e6674e7881352fca9af6d7000452b`
  0/0; Stage A Codex ACCEPT
  `5e1bd98eaf5d11688a61963907afb927f71cea36527614e37227056c8cb216b8`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g23-leftover-join.v7.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-235 and D-237. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g23-leftover-join.v7.json`
  `22a52b01a58a44e6162999d1b18bd76945086e3563724106ca05d62eeba90c5b`.
- **Decision:** Record v7 as G23 leftover remasurement after
  D-237. Lands CLAUDE-D238-M1 / D238-SF-1. The candidate
  binds NOTHING. DR-G23 stays `OPEN`. leftoverDesign remains
  `[OBL-G23-FX-AUTHORING]`, scoped to per-D-002-platform
  copies of the four D-237 implementations. leftover-design
  of those four implementations is stale as an authoring
  claim. Host-refusal observation and subsequent-session
  view remain qualification at OBL-G23-EXECUTION (D-056).
  Does not pin QUALIFIED. Does not invent fixture bytes,
  observation bytes, per-platform copies, or a D-002
  platform list. Does not reopen leftover-design of NT-3
  or NT-5. Does not SATISFY DR-133. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-101.
  Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero.
  Naming parent is D-147. Frozen v4 remains a historical
  measurement as of D-198. Frozen v5 remains a historical
  split (Codex REJECT G23LJ-V5-M1/S1; Claude ACCEPT 0/0).
  Frozen v6 remains a historical split (Codex ACCEPT 0/0;
  Claude REJECT CLAUDE-G23LJ-V6-M1/S1). Do not record v4,
  v5, or v6 as current. Claude Stage A returned observation
  CLAUDE-G23LJ-V7-O1; no change requested. Codex Stage A
  returned zero advisories and no observations. Claude
  Stage B turn 2 returned CLAUDE-D238-T2-O1 and
  CLAUDE-D238-T2-O2; no change requested. Codex Stage B
  returned zero advisories and no observations. This entry
  names those Claude identifiers. It does not invent Codex
  identifiers. It does not claim that both reviewers'
  identifiers are preserved. Codex returned no observation
  identifiers. Does not execute G23. Does not rewrite
  occupancy v2. Does not rewrite corpus v3. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D238. Does not unwrite D-147, D-198, D-223,
  D-236, or D-237.
- **Commit:** C-D238.

## D-239 — Record g23-fixture-corpus.v4 as G23 leftover-design per-D-002-platform copies

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-239.review-adversarial.claude2.json`,
  `a9024386a8a430524483d131f5b5863a6af899f4f336e4bd8ad2036fc86d18a9`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-239.review-adversarial.codex.json`,
  `70da96af3350c21dde59acda328cff895b5803cde098659a0bb339450d9c1cb7`)
  CONSENT. Subject `coordinator-decisions.D-239.draft.md`
  `61608c80949e1d13c09cd4cc7e468241405be14678c15caaac6df5f78cf7d3af`.
  Frozen corpus
  `g23-fixture-corpus.v4.json`
  `b3fce9f5bab6764919f5dc43c28a43f3d9c3b6be310e45c2c1bd08a617c755c5`
  Stage A Claude ACCEPT
  `4e91a1d810ab81d5bca7a55cdbc4cc08c224eca6f1f6ba23bd84b00e1d9bb2b2`
  0/0; Stage A Codex ACCEPT
  `923ba5c973ae91938492f0d3c7e34f78163a576d5a4f5f332beed29b64fd25ac`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g23-fixture-corpus.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g23-fixture-corpus.v4.json`
  `b3fce9f5bab6764919f5dc43c28a43f3d9c3b6be310e45c2c1bd08a617c755c5`.
- **Decision:** Record v4 as G23 leftover-design
  per-D-002-platform copies after D-238. The candidate binds
  NOTHING. DR-G23 stays `OPEN`. leftover-design of
  OBL-G23-FX-AUTHORING remains on leftover-join.v7 (D-238).
  Remainder of G23 execution, including host
  relation-registry refusal observation and
  subsequent-session view, remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent a D-002 platform
  list. Does not copy onto Windows. Does not invent a
  finding schema. Does not invent a D9 code. Does not
  invent a section 7.1 recipe. Does not collapse EV-2 into
  EV-3. Does not SATISFY DR-133. Does not SATISFY DR-117.
  Does not SATISFY DR-131. Does not SATISFY DR-101. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Frozen v1 and v2 remain
  historical REJECT. Frozen v3 remains the D-237 payload
  subject. Do not record v1, v2, or v3 as current. Naming
  parent is D-147, not leftover-join.v7. Claude Stage A
  returned four observationsNotFindings strings. They
  carry no identifiers. Codex Stage A returned zero
  advisories and no observations. Claude Stage B returned
  four observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute G23. Does not
  rewrite leftover-join.v7. Does not rewrite occupancy v2.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D239. Does not unwrite D-147, D-223, D-237,
  or D-238.
- **Commit:** C-D239.

## D-240 — Record g23-leftover-join.v8 as G23 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-240.review-adversarial.claude2.turn3.json`,
  `1325d19ad7d00f340ee63fead2da7465f409c9c2b875b931a130906a5774d778`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-240.review-adversarial.codex.turn3.json`,
  `27a79da001cddd7f82e3ff6315e0f35fe8320a046e95c963d9f3b5600f8885df`)
  CONSENT. Subject `coordinator-decisions.D-240.turn3.draft.md`
  `b0a2bad23855b2d87a1f77a0db86ea9694ee11c16b4f546aba5f2cbd1cb3fdf3`.
  Turn-1 Claude OBJECT (CLAUDE-D240-SF1) at
  `9b08c6416d2252a8308d5a6d869de147bc258dc831740895a81005300698b9ba`;
  turn-1 Codex CONSENT
  `9fc11806f5e2b49c62fe574c0643b470198d86d0f3b6547ebc4454aeb6d0d38d`.
  Turn-2 Claude OBJECT (CLAUDE-D240-T2-SF1) at
  `375aae6c2832166070a57f10a1c107bcb20da1ccb68efdf944a9b329eda1daae`;
  turn-2 Codex CONSENT
  `7944ce3c93185d4854e8d7ce907dd4ac44c51667528edd444dbf52bb50732943`.
  Frozen leftover-join
  `g23-leftover-join.v8.json`
  `498324e5e456562317c7681b44cdac9138ca1e947aa363dad5a331caa3eef812`
  Stage A Claude ACCEPT
  `269d49e231f347e5220c6010e0f806737951ea2ecc2fef6b560dbd2f40c71a61`
  0/0; Stage A Codex ACCEPT
  `a6809f658b9f78b5ab1fd32556c0227d3b8899c2a3734e1c697548c0e54a9f08`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g23-leftover-join.v8.json`
  (0 blockers, 0 SHOULD-FIX). Same no-cell-edit branch as
  D-170 through D-235 and D-237 and D-238 and D-239. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g23-leftover-join.v8.json`
  `498324e5e456562317c7681b44cdac9138ca1e947aa363dad5a331caa3eef812`.
- **Decision:** Record v8 as G23 leftover remasurement after
  D-239. Lands CLAUDE-D240-SF1 and CLAUDE-D240-T2-SF1. The
  candidate binds NOTHING. DR-G23 stays `OPEN`.
  leftoverDesign is `[]`. leftover-design of the four
  D-237 implementations is stale as an authoring claim.
  leftover-design of per-D-002-platform copies is stale as
  an authoring claim after D-239. Host-refusal observation
  and subsequent-session view remain qualification at
  OBL-G23-EXECUTION (D-056). Does not pin QUALIFIED. Does
  not invent observation bytes. Does not invent a D-002
  platform list. Does not copy onto Windows. Does not
  reopen leftover-design of NT-3 or NT-5. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY
  DR-131. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is D-147.
  Frozen v4, v5, v6, and v7 are not recorded as current.
  Claude Stage A returned observations CLAUDE-G23LJ-V8-O1,
  CLAUDE-G23LJ-V8-O2, and CLAUDE-G23LJ-V8-O3. No change
  requested. Codex Stage A returned zero advisories and no
  observations. Claude Stage B turn 1 returned observations
  CLAUDE-D240-O1 and CLAUDE-D240-O2. No change requested.
  Codex Stage B returned zero advisories and no
  observations at every turn. This entry names those
  Claude identifiers. It does not invent Codex identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Codex returned no observation identifiers.
  Does not execute G23. Does not rewrite occupancy v2.
  Does not rewrite corpus v4. Does not edit file 08. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D240. Does not unwrite D-147, D-223, D-237,
  D-238, or D-239.
- **Commit:** C-D240.

## D-241 — Record g21-fixture-corpus.v1 as G21 leftover-design NT-1/NT-2 fixture implementations

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-241.review-adversarial.claude2.turn2.json`,
  `72c32bdecbb9c7d39ba01d21c8cb3883f303128b04bec0b62ba591fdc482e097`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-241.review-adversarial.codex.turn2.json`,
  `12b242d2d74533b141ec5ce27be02e14df49ebea92bd5ecda39397edc43d8617`)
  CONSENT. Subject `coordinator-decisions.D-241.turn2.draft.md`
  `271eebc0683c7c45b83fa629fa3e6bfec3023949ccfde200adc6c29590be9236`.
  Turn-1 Claude OBJECT (CLAUDE-D241-SF1) at
  `e7782f01a752879cd3a2c968aa160e5783a7e912f9066e6782bc05721d5faddc`;
  turn-1 Codex OBJECT (CODEX-D241-SF1)
  `b61d59ce1b14825ed0eb03e7fdb9e2655d651c3e076bd0ac83f534229a3ce9a1`.
  Frozen corpus
  `g21-fixture-corpus.v1.json`
  `861bb4e7d26a80158cc1cc3a0518c5e8e95311bee4d8c8ce63acd1e60d6c906d`
  Stage A Claude ACCEPT
  `ad9234df10c7952cd21b63945fceffea76509eb8a3d261951efd2e4575c20de1`
  0/0; Stage A Codex ACCEPT
  `5b547afdad83c46e83e608c26f59a693994f6a11a5bd10eaa94c26f269dc6368`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-fixture-corpus.v1.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-fixture-corpus.v1.json`
  `861bb4e7d26a80158cc1cc3a0518c5e8e95311bee4d8c8ce63acd1e60d6c906d`.
- **Decision:** Record v1 as G21 leftover-design NT-1/NT-2
  fixture implementations after D-240. Lands CLAUDE-D241-SF1
  and CODEX-D241-SF1 as one class. The candidate binds
  NOTHING. DR-G21 stays `OPEN`. leftover-design of
  OBL-G21-FX-AUTHORING remains on leftover-join.v4 (D-196).
  Remainder of G21 execution, including candidate-buffer
  digest and subsequent-session view, remains qualification
  (D-056). Remaining G21 classes stay unauthored. Does not
  pin QUALIFIED. Does not invent a finding schema. Does not
  invent a D9 code, exit number, or HostTermination. Does
  not invent a pack IR. Does not invent a section 7.1
  recipe. Does not invent a D-002 platform list. Does not
  author NT-6. Does not take over G23. Does not reopen
  DR-102 SATISFIED. Does not SATISFY DR-114. Does not
  SATISFY DR-133. Does not SATISFY DR-117. Does not SATISFY
  DR-131. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is D-145 /
  naming v6, not leftover-join.v4. Frozen turn-1 subject
  remains historical OBJECT. Do not record the turn-1 draft
  as current. Claude Stage A returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage A returned zero advisories and no
  observations. Claude Stage B turn 2 returned three
  unlabeled observationsNotFindings objects. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations at every turn. This entry does not invent
  identifiers for those observations and does not claim
  that both reviewers' identifiers are preserved. Codex
  returned no observation identifiers. Does not execute
  G21. Does not rewrite leftover-join.v4. Does not rewrite
  occupancy v4. Does not rewrite leftover-join.v8. Does not
  edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D241. Does not unwrite D-086, D-145, D-196,
  D-218, or D-240.
- **Commit:** C-D241.

## D-242 — Record g21-leftover-join.v7 as G21 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-242.review-adversarial.claude2.json`,
  `e1199a5d705806ac579ab03656561aa967479ec5980a0601199b2668667e3f7f`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-242.review-adversarial.codex.json`,
  `7f2f91495f5999031229fbb571dcc5e8f0769b904c151f6826ef276e1fc12490`)
  CONSENT. Subject `coordinator-decisions.D-242.draft.md`
  `69d772bec6c9fb5a0d5c220d6184b21746236a9224fa62e38f5edb14f500c002`.
  Frozen leftover-join
  `g21-leftover-join.v7.json`
  `5a48c4626c44c4016390dc5868754da136715b72c76c5de09b89e49aad76eb04`
  Stage A Claude ACCEPT
  `15710285e149c89e8fa9a01396a893769555dab41b283d66954dc278033741cd`
  0/0; Stage A Codex ACCEPT
  `2b15089ad1ed9bddbdef7c5fdce612bbd77884d13412c2ee8f3d29e0ce48ec33`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-leftover-join.v7.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241.
  Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-leftover-join.v7.json`
  `5a48c4626c44c4016390dc5868754da136715b72c76c5de09b89e49aad76eb04`.
- **Decision:** Record v7 as G21 leftover remasurement after
  D-241. Lands G21LJ-V5-M1, G21LJ-V5-SF1, and G21LJ-V6-SF1.
  The candidate binds NOTHING. DR-G21 stays `OPEN`.
  leftoverDesign remains `[OBL-G21-FX-AUTHORING]`.
  leftover-design of NT-1 and NT-2 implementations is stale
  as an authoring claim. leftover-design of
  per-D-002-platform copies of those implementations
  remains. Remaining G21 classes stay unauthored. Remainder
  of G21 execution, including candidate-buffer digest,
  subsequent-session view, and host-projection goldens,
  remains qualification (D-056). Does not pin QUALIFIED.
  Does not invent a D-002 platform list. Does not author
  those copies. Does not invent a finding schema. Does not
  invent a D9 code, exit number, or HostTermination. Does
  not invent a pack IR. Does not invent a section 7.1
  recipe. Does not author NT-6. Does not take over G23.
  Does not reopen DR-102 SATISFIED. Does not SATISFY
  DR-114. Does not SATISFY DR-133. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero.
  Naming parent is D-145 / naming v6, not leftover-join.v4.
  Frozen leftover-join.v4 remains D-196. Frozen leftover-join.v5
  and leftover-join.v6 remain split. Do not record v4, v5,
  or v6 as current. Claude Stage A returned five unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage A returned zero advisories and no
  observations. Claude Stage B returned five unlabeled
  observationsNotFindings objects. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute G21. Does not
  rewrite occupancy v4. Does not rewrite corpus v1. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D242. Does not unwrite D-086, D-145, D-196,
  D-218, or D-241.
- **Commit:** C-D242.

## D-243 — Record g21-fixture-corpus.v2 as G21 leftover-design per-D-002-platform copies

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-243.review-adversarial.claude2.json`,
  `56d276d6b4bf237d9d14b7d06d84a71ca26a1598c0901775c68a2b443906ca17`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-243.review-adversarial.codex.json`,
  `c52120ab61faee374f726f953837c669d06e61fa6d94ed5f9f520081d0d33fee`)
  CONSENT. Subject `coordinator-decisions.D-243.draft.md`
  `987b324da27e6ce8c34fe340a2448530c4cbcd073925e86b440df7106a1c4247`.
  Frozen corpus
  `g21-fixture-corpus.v2.json`
  `af24c6e7294c5802e02063ad0875907b68e264581f6521325dc6d6b60a97fba1`
  Stage A Claude ACCEPT
  `d0e4dcdad94de2f199baeef2f50226c5b281ffcdb9817e15b422fc785e9bd809`
  0/0; Stage A Codex ACCEPT
  `01bab40acb37742fbecb2e7616bddef49ab36f8c38fbe54cc9d33715cbe12cb8`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-fixture-corpus.v2.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-fixture-corpus.v2.json`
  `af24c6e7294c5802e02063ad0875907b68e264581f6521325dc6d6b60a97fba1`.
- **Decision:** Record v2 as G21 leftover-design
  per-D-002-platform copies after D-242. The candidate binds
  NOTHING. DR-G21 stays `OPEN`. leftover-design of
  OBL-G21-FX-AUTHORING remains on leftover-join.v7 (D-242).
  Remainder of G21 execution, including candidate-buffer
  digest, subsequent-session view, and host-projection
  goldens, remains qualification (D-056). Remaining G21
  classes stay unauthored. Does not pin QUALIFIED. Does not
  invent a D-002 platform list. Platforms are quoted from
  G10 occupancy v2 (`macos/arm64`, `macos/x86_64`,
  `linux/x86_64`, `linux/arm64`), ORDERED-EQUAL to G23
  occupancy v2. G21 occupancy v4 has no platforms array.
  Does not copy onto Windows. Does not invent a finding
  schema. Does not invent a D9 code, exit number, or
  HostTermination. Does not invent a pack IR. Does not
  invent a section 7.1 recipe. Does not author NT-6. Does
  not take over G23. Does not reopen DR-102 SATISFIED. Does
  not SATISFY DR-114. Does not SATISFY DR-133. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Frozen
  v1 remains the D-241 payload subject. Do not record v1 as
  current copies. Naming parent is D-145 / naming v6, not
  leftover-join.v7. Claude Stage A returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage A returned zero advisories and no
  observations. Claude Stage B returned four unlabeled
  observationsNotFindings objects. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Codex returned no
  observation identifiers. Does not execute G21. Does not
  rewrite leftover-join.v7. Does not rewrite occupancy v4.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D243. Does not unwrite D-145, D-212, D-218,
  D-241, or D-242.
- **Commit:** C-D243.

## D-244 — Record g21-leftover-join.v9 as G21 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-244.review-adversarial.claude2.json`,
  `6a52576c9c969b64e7bbd4a8c35b6ada7b0a321313fd6062c872f9f1bae9db58`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-244.review-adversarial.codex.json`,
  `19491c21780f81aa972b1b1fe08be17282548ec4e61e0be3db72c6ed3dc5c8e1`)
  CONSENT. Subject `coordinator-decisions.D-244.draft.md`
  `d202511a61c83dba0097ab36b0fb05b1f6aa627dcf861e555608998bcc782036`.
  Frozen leftover-join
  `g21-leftover-join.v9.json`
  `d0fda8926b5f2e494d1b7c1f3ec716ded3d58ef3b9c498f73d0a3220f893a4de`
  Stage A Claude ACCEPT
  `994de8607a09543b6106c1fb07e6b0cf2a170768466e088ad11d59e4df89affb`
  0/0; Stage A Codex ACCEPT
  `b4ff28d515c834e9208c23318f5f50bce8159b21cba4b6f3a3b6b7ab1e2c6e96`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-leftover-join.v9.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-leftover-join.v9.json`
  `d0fda8926b5f2e494d1b7c1f3ec716ded3d58ef3b9c498f73d0a3220f893a4de`.
- **Decision:** Record v9 as G21 leftover remasurement after
  D-243. Lands G21LJ-V8-SF1. The candidate binds NOTHING.
  DR-G21 stays `OPEN`. leftoverDesign remains
  `[OBL-G21-FX-AUTHORING]`. leftover-design of NT-1 and
  NT-2 implementations is stale as an authoring claim.
  leftover-design of per-D-002-platform copies of those
  implementations is stale as an authoring claim.
  Remaining G21 classes stay unauthored. Remainder of G21
  execution, including candidate-buffer digest,
  subsequent-session view, and host-projection goldens,
  remains qualification (D-056). Does not pin QUALIFIED.
  Does not invent a D-002 platform list. Does not invent a
  finding schema. Does not invent a D9 code, exit number,
  or HostTermination. Does not invent a pack IR. Does not
  invent a section 7.1 recipe. Does not author NT-6. Does
  not take over G23. Does not reopen DR-102 SATISFIED. Does
  not SATISFY DR-114. Does not SATISFY DR-133. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero.
  Naming parent is D-145 / naming v6, not leftover-join.v7.
  Frozen leftover-join.v4 remains D-196. Frozen leftover-join.v5
  and leftover-join.v6 remain split. Frozen leftover-join.v7
  remains D-242. Frozen leftover-join.v8 remains Dual REJECT
  0/1 G21LJ-V8-SF1. Do not record v4 through v8 as current.
  Claude Stage A returned three observationsNotFindings
  strings. They carry no identifiers. Codex Stage A
  returned zero advisories and no observations. Claude
  Stage B returned three unlabeled observationsNotFindings
  objects, each an observation paired with a whyNotAFinding.
  They carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers for those observations and does not claim that
  both reviewers' identifiers are preserved. Codex returned
  no observation identifiers. Does not execute G21. Does not
  rewrite occupancy v4. Does not rewrite corpus v1 or corpus
  v2. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D244. Does not unwrite D-145, D-196, D-218,
  D-241, D-242, or D-243.
- **Commit:** C-D244.

## D-245 — Record g21-fixture-corpus.v7 as G21 leftover-design CC-5 prefix injections

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1 OBJECT:
  Claude D245-M1 MUST-FIX
  (`artifacts/coordinator-decisions.D-245.review-adversarial.claude2.json`,
  `a5f706c5a22573798e4c6c880f17877bc796b1844b00abac328aa2981d225d44`);
  Codex CODEX-D245-SF1 SHOULD-FIX
  (`artifacts/coordinator-decisions.D-245.review-adversarial.codex.json`,
  `5f090d2f3d902d128e6f20ad3dc932064fd80ae8b017df315ffc7d5ddf307a84`).
  Same class. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-245.turn2.review-adversarial.claude2.json`,
  `490d67d95742049d2490e32ccfa0ab99486a604b427aac86b1ea5802809ef5b8`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-245.turn2.review-adversarial.codex.json`,
  `06f2daf5de56a77810d90b7d00be65888686da8af5f1ac0d5af5bfa8420bb607`)
  CONSENT. Subject `coordinator-decisions.D-245.turn2.draft.md`
  `cb5c03d2861446d004d30106510987ca111bc742ecff82cce9a814e1afbbfcf5`.
  Frozen corpus
  `g21-fixture-corpus.v7.json`
  `20bf75a4b404f54d16b531659af825ef6f86d3721ea10cb3c0c435b0e496c57f`
  Stage A Claude ACCEPT
  `69fb819c9a9f0cee60bd67131b2ed90defd23cab37ed8dc4c1c310a0ad7aaddd`
  0/0; Stage A Codex ACCEPT
  `8ac4ed5c24c5461c86e8682088a0e79b08fa5146a1107d5a218f354720751a66`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-fixture-corpus.v7.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-fixture-corpus.v7.json`
  `20bf75a4b404f54d16b531659af825ef6f86d3721ea10cb3c0c435b0e496c57f`.
- **Decision:** Record v7 as G21 leftover-design of two CC-5
  prefix injections after D-244. Lands G21FXV3-M1,
  G21FXV4-M1, G21FXV5-S1, G21FXV6-S1, D245-M1, and
  CODEX-D245-SF1. The candidate binds NOTHING. DR-G21 stays
  `OPEN`. leftoverDesign of OBL-G21-FX-AUTHORING remains on
  leftover-join.v9 (D-244). Remaining G21 classes stay
  unauthored. Remaining CC-5 injections stay unauthored.
  Per-D-002-platform copies of these bytes stay unauthored.
  Remainder of G21 execution, including candidate-buffer
  digest, subsequent-session view, host-projection goldens,
  and EV-5 diagnostic/audit bytes, remains qualification
  (D-056). Does not pin QUALIFIED. Does not remasure
  leftover-join.v9. Does not invent a D-002 platform list.
  Does not invent a ping body schema. Does not invent
  26214400. Does not classify non-object top level as CC-5.
  Does not invent a finding schema. Does not invent a D9
  code, exit number, or HostTermination. Does not invent a
  pack IR. Does not invent a section 7.1 recipe. Does not
  author NT-6. Does not take over G23. Does not reopen
  DR-102 SATISFIED. Does not SATISFY DR-114. Does not
  SATISFY DR-133. Does not SATISFY DR-117. Does not SATISFY
  DR-131. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is D-145 /
  naming v6, not leftover-join.v9. Frozen leftover-join.v9
  remains current G21 leftover-join. Frozen corpus v3
  through v6 remain split. Do not record them as current.
  Claude Stage A returned three observationsNotFindings
  objects with identifiers O-G21FXV7-01, O-G21FXV7-02, and
  O-G21FXV7-03, each an object with keys id and observation.
  Claude Stage A also returned advisories A-G21FXV7-01 and
  A-G21FXV7-02. They travel as honesty work on a later
  successor and are not SATISFIED-bars. Codex Stage A
  returned zero advisories and no observations. Claude
  Stage B turn 2 returned three observationsNotFindings
  objects with identifiers O-D245T2-01, O-D245T2-02, and
  O-D245T2-03. They carry identifiers. Codex Stage B
  returned zero advisories and no observations. This entry
  names those Claude identifiers and does not invent
  identifiers. It does not claim that both reviewers'
  identifiers are preserved. Codex returned no observation
  identifiers and no advisory identifiers. Does not execute
  G21. Does not rewrite leftover-join.v9. Does not rewrite
  occupancy v4. Does not rewrite corpus v1 or corpus v2.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D245. Does not unwrite D-145, D-218, D-241,
  D-243, or D-244.
- **Commit:** C-D245.

## D-246 — Record g21-leftover-join.v11 as G21 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1 OBJECT:
  Claude D246-S1 SHOULD-FIX
  (`artifacts/coordinator-decisions.D-246.review-adversarial.claude2.json`,
  `da2ece9cc8f8f5a65970bf8bcfa41b0ce3e6a369394a1764e14924459a8d7934`);
  Codex CODEX-D246-SF1 SHOULD-FIX
  (`artifacts/coordinator-decisions.D-246.review-adversarial.codex.json`,
  `da1c4f8ca296886f2d13e68c0a1d42fd2467b7556348cd7730d30e756d24c1fc`).
  Not Dual REJECT. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-246.turn2.review-adversarial.claude2.json`,
  `511989c24f1191401e65473c67a3355441f001d0c8f184a03c25a385ee55077f`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-246.turn2.review-adversarial.codex.json`,
  `6d3c99fa1e7522ef4408d9821d9aac96661bfd4d4f933680cbfe7b2ac9a03324`)
  CONSENT. Subject `coordinator-decisions.D-246.turn2.draft.md`
  `bde7b8629be73deb15807b0dcac2de325916256bd6675e12d5ed1ddaa3beb62a`.
  Frozen leftover-join
  `g21-leftover-join.v11.json`
  `ea8d2c52723a46eef3388b93e2a529a5af999d24363a695719d6d7a1bd08224f`
  Stage A Claude ACCEPT
  `2e45c8ff487421a3ffdea7098fddf7d52da8aae1e83e647c12932d2ba2729856`
  0/0; Stage A Codex ACCEPT
  `f52f947df1bb90013fcc6d546a057225527cd81828d921423d876c0ea0e930fb`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-leftover-join.v11.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-leftover-join.v11.json`
  `ea8d2c52723a46eef3388b93e2a529a5af999d24363a695719d6d7a1bd08224f`.
- **Decision:** Record v11 as G21 leftover remasurement after
  D-245. Lands G21LJ-V10-SF1, D246-S1, and CODEX-D246-SF1.
  The candidate binds NOTHING. DR-G21 stays `OPEN`.
  leftoverDesign remains `[OBL-G21-FX-AUTHORING]`.
  leftover-design of the two CC-5 prefix injections is stale
  as an authoring claim. leftover-design of NT-1 and NT-2
  implementations, and of per-D-002-platform copies of those
  implementations, is stale as an authoring claim.
  leftover-design of per-D-002-platform copies of the two
  CC-5 payloads remains. Remaining CC-5 injections stay
  unauthored. Remaining G21 classes stay unauthored.
  Remainder of G21 execution, including candidate-buffer
  digest, subsequent-session view, host-projection goldens,
  and EV-5 diagnostic/audit bytes, remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent a D-002
  platform list. Does not claim CC-5 fully authored. Does
  not classify non-object top level as CC-5. Does not invent
  a ping body schema. Does not invent 26214400. Does not
  invent a finding schema. Does not invent a D9 code, exit
  number, or HostTermination. Does not invent a pack IR.
  Does not invent a section 7.1 recipe. Does not author
  NT-6. Does not take over G23. Does not reopen DR-102
  SATISFIED. Does not SATISFY DR-114. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-101. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Naming parent is D-145 / naming v6, not
  leftover-join.v9. Frozen leftover-join.v9 was current at
  D-245 / draft time. Frozen leftover-join.v4 through v8
  and split leftover-join.v10 were not current at draft
  time. After this recording, leftover-join.v4 through v10
  are not current. leftover-join.v5, leftover-join.v6, and
  leftover-join.v10 remain split. leftover-join.v8 remains
  Dual REJECT 0/1 G21LJ-V8-SF1. Claude Stage A returned no
  observationsNotFindings. Codex Stage A returned one
  observation object with identifier G21LJ-V11-OBS-1, an
  observation paired with a whyNotShouldFix. Claude Stage B
  turn 2 returned two observationsNotFindings objects with
  identifiers D246-T2-OBS-1 and D246-T2-OBS-2, each an
  observation paired with a whyNotShouldFix. Codex Stage B
  returned zero advisories and no observations. This entry
  names those identifiers and does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage A returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G21. Does not rewrite
  occupancy v4. Does not rewrite corpus v1, corpus v2, or
  corpus v7. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D246. Does not unwrite D-145, D-196, D-218,
  D-241, D-243, D-244, or D-245.
- **Commit:** C-D246.

## D-247 — Record g21-fixture-corpus.v8 as G21 leftover-design per-D-002-platform copies of two CC-5 payloads

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1
  split: Claude CONSENT
  (`artifacts/coordinator-decisions.D-247.review-adversarial.claude2.json`,
  `161f9ae41f375765bf3a92342dbe2f91505a8052e7c9658d0a03ede067fedc89`);
  Codex OBJECT 0/1 CODEX-D247-SF1
  (`artifacts/coordinator-decisions.D-247.review-adversarial.codex.json`,
  `dc063bfab4ac89e3e2cf7ca96ca78773632b9d99ad79fbdb4bc0ec712120779d`).
  Not Dual REJECT. Not Dual CONSENT. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-247.turn2.review-adversarial.claude2.json`,
  `b8b413573ce1821a051624672b7eba6a11be71f0515dde50b348e1c21231b49b`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-247.turn2.review-adversarial.codex.json`,
  `b4505fa71e6bc38d717062819e13f9a9ab87536cf3b7eb310ab671fadbe1c675`)
  CONSENT. Subject `coordinator-decisions.D-247.turn2.draft.md`
  `a8b81da1367af6f5eb08267c9d07503596b5e9cc7b5f2b7caad6eaf5ddf08c82`.
  Frozen turn 1 draft
  `coordinator-decisions.D-247.draft.md`
  `027444d4ec6b0ce0ad18fea9e97a447369bcd37285f87362154f97ca3fe3af6c`.
  Frozen corpus
  `g21-fixture-corpus.v8.json`
  `e8149a865e49bdcda9eda923e9918f332a83078f43ab6a3af9a10d6d31ef6359`
  Stage A Claude ACCEPT
  `210fb795a33b40792b7a354178489694e84b2c192aee8148727ec5fef5d44111`
  0/0; Stage A Codex ACCEPT
  `37a65061aff45022cdccdc2ffe7660b0c6c713b9d6d36ad72a44df98aca9a0b1`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-fixture-corpus.v8.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-fixture-corpus.v8.json`
  `e8149a865e49bdcda9eda923e9918f332a83078f43ab6a3af9a10d6d31ef6359`.
- **Decision:** Record v8 as G21 leftover-design
  per-D-002-platform copies of the two D-245 CC-5 payloads
  after D-246. Lands CODEX-D247-SF1. The candidate binds
  NOTHING. DR-G21 stays `OPEN`. leftover-design of
  OBL-G21-FX-AUTHORING remains on leftover-join.v11 (D-246).
  leftover-join.v11 remains the current G21 leftover-join.
  Remainder of G21 execution, including candidate-buffer
  digest, subsequent-session view, host-projection goldens,
  and EV-5 diagnostic/audit bytes, remains qualification
  (D-056). Remaining G21 classes stay unauthored. Remaining
  CC-5 injections stay unauthored. CC-5 is not fully
  authored. Does not pin QUALIFIED. Does not remasure
  leftover-join.v11. Does not invent a D-002 platform list.
  Platforms are quoted from G10 occupancy v2 (`macos/arm64`,
  `macos/x86_64`, `linux/x86_64`, `linux/arm64`),
  ORDERED-EQUAL to G23 occupancy v2. G21 occupancy v4 has
  no platforms array. Does not copy onto Windows. Does not
  mutate fixtures/g21.v7/. Does not invent a finding schema.
  Does not invent a D9 code, exit number, or
  HostTermination. Does not invent a pack IR. Does not
  invent a section 7.1 recipe. Does not invent a ping body
  schema. Does not invent 26214400. Does not classify
  non-object top level as CC-5. Does not claim CC-5 fully
  authored. Does not author NT-6. Does not take over G23.
  Does not reopen DR-102 SATISFIED. Does not SATISFY DR-114.
  Does not SATISFY DR-133. Does not SATISFY DR-117. Does not
  SATISFY DR-131. Does not SATISFY DR-101. Gate 1 Class A is
  not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Frozen v7 remains the D-245
  payload subject. Do not record v7 as current copies.
  Frozen v3 through v6 are not recorded as current.
  leftover-join.v4 through leftover-join.v10 are not
  recorded as current. leftover-join.v9 is not current.
  Naming parent is D-145 / naming v6, not leftover-join.v11.
  Claude Stage A returned four unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Claude Stage A returned zero advisories.
  Codex Stage A returned one unlabeled observations object,
  an observation paired with a whyNotShouldFix. It carries
  no identifier. Codex Stage A returned zero advisories.
  Claude Stage B turn 1 returned five unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B turn 1 returned zero advisories
  and no observations; its finding is CODEX-D247-SF1, landed
  at turn 2. Claude Stage B turn 2 returned five unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B turn 2 returned zero advisories
  and no observations. This entry does not invent identifiers
  for those observations and does not claim that both
  reviewers' identifiers are preserved. Claude returned no
  observation identifiers. Codex returned no observation
  identifiers. Does not execute G21. Does not rewrite
  leftover-join.v11. Does not rewrite occupancy v4. Does not
  rewrite corpus v7. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D247. Does not unwrite D-145, D-212, D-218,
  D-241, D-243, D-245, or D-246.
- **Commit:** C-D247.

## D-248 — Record g21-leftover-join.v12 as G21 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-248.review-adversarial.claude2.json`,
  `8b28cd2829fd1e99efd777c4d50c4d244bffcdaba220b0256eabfecba068aa98`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-248.review-adversarial.codex.json`,
  `83f719b15d527cc63367bee857db6e79a6b8b70ef61bfc22d9c42951988b1b36`)
  CONSENT. Subject `coordinator-decisions.D-248.draft.md`
  `a4e80e741ba2c63d101aed8e9358dae935fd2c5da0cfe4e72a369e41823c0f42`.
  Frozen leftover-join
  `g21-leftover-join.v12.json`
  `6442b17ad08743601cc06683d6a4c0d33c3885d7c7de5700fd11325bffabe63d`
  Stage A Claude ACCEPT
  `e5766c2466a401e06da130909fbf1f2a872527af62800c94a70670a88e35645e`
  0/0; Stage A Codex ACCEPT
  `8eed526ddff919103dd6d78555434344f299644c45f4d2ddb6146e9b35739c24`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g21-leftover-join.v12.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g21-leftover-join.v12.json`
  `6442b17ad08743601cc06683d6a4c0d33c3885d7c7de5700fd11325bffabe63d`.
- **Decision:** Record v12 as G21 leftover remasurement after
  D-247. The candidate binds NOTHING. DR-G21 stays `OPEN`.
  leftoverDesign remains `[OBL-G21-FX-AUTHORING]`.
  leftover-design of the two CC-5 prefix injections is stale
  as an authoring claim. leftover-design of
  per-D-002-platform copies of those two CC-5 payloads is
  stale as an authoring claim. leftover-design of NT-1 and
  NT-2 implementations, and of per-D-002-platform copies of
  those implementations, is stale as an authoring claim.
  Remaining CC-5 injections stay unauthored. Remaining G21
  classes stay unauthored. Remainder of G21 execution,
  including candidate-buffer digest, subsequent-session
  view, host-projection goldens, and EV-5 diagnostic/audit
  bytes, remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent a D-002 platform list. Does not
  claim CC-5 fully authored. Does not classify non-object
  top level as CC-5. Does not invent a ping body schema.
  Does not invent 26214400. Does not invent a finding
  schema. Does not invent a D9 code, exit number, or
  HostTermination. Does not invent a pack IR. Does not
  invent a section 7.1 recipe. Does not author NT-6. Does
  not take over G23. Does not reopen DR-102 SATISFIED. Does
  not SATISFY DR-114. Does not SATISFY DR-133. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent is D-145 / naming v6, not leftover-join.v11. Frozen
  leftover-join.v11 was current at D-247 / draft time.
  Frozen leftover-join.v4 through v10 were not current at
  draft time. After this recording, leftover-join.v4 through
  leftover-join.v11 are not current. leftover-join.v5,
  leftover-join.v6, and leftover-join.v10 remain split.
  leftover-join.v8 remains Dual REJECT 0/1 G21LJ-V8-SF1.
  Claude Stage A returned no observationsNotFindings field
  and no advisories. Codex Stage A returned zero advisories
  and no observations. Claude Stage B returned zero
  observations and zero advisories. Codex Stage B returned
  zero advisories and no observations. This entry does not
  invent identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G21. Does not rewrite occupancy v4. Does
  not rewrite corpus v7 or corpus v8. Does not edit file 08.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D248. Does not unwrite D-145, D-196, D-218,
  D-241, D-243, D-245, D-246, or D-247.
- **Commit:** C-D248.

## D-249 — Record g25 leftover-join.v5 as G25 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1
  split: Claude CONSENT
  (`artifacts/coordinator-decisions.D-249.review-adversarial.claude2.json`,
  `9ea0f940190b7013cad1588c88bf39944e0be79f93fe9fb3c9c3e9b07bcceda9`);
  Codex OBJECT 0/1 CODEX-D249-SF1
  (`artifacts/coordinator-decisions.D-249.review-adversarial.codex.json`,
  `faf59d788257eeeca7a55375ec1d346e7394cae8c9fcab2e85428f7a2b205908`).
  Not Dual REJECT. Not Dual CONSENT. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-249.turn2.review-adversarial.claude2.json`,
  `640c8acc93546fa77d5eaaf0175b0f35650032463571c64eff5e2956c448602e`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-249.turn2.review-adversarial.codex.json`,
  `d1f96457dea24aa7d306caf7afc704290620d08b77469d610fa4b49aa3a1be08`)
  CONSENT. Subject `coordinator-decisions.D-249.turn2.draft.md`
  `31ea60272b4ac96997db464a3a22dacb31449f47cb7f7b89c2f0bfcb2f62c33c`.
  Frozen turn 1 draft
  `coordinator-decisions.D-249.draft.md`
  `f26185b2382446a82ffada67564eb5607bb85e215399debad1b28bbfb8c2f903`.
  Frozen leftover-join
  `g25-leftover-join.v5.json`
  `9f2b137fe0b01830b4113ef26c8283214a75982f588f164391d61c5510f67aa3`
  Stage A Claude ACCEPT
  `de346fc88b4a99f11184a0b9ebf490f00135686d437de714f25bb48ba920772c`
  0/0; Stage A Codex ACCEPT
  `6f4e28dda440c89f34e67a42cb64fdccf5bcbdc2befc10f80e4c42c05edbd2c2`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g25-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g25-leftover-join.v5.json`
  `9f2b137fe0b01830b4113ef26c8283214a75982f588f164391d61c5510f67aa3`.
- **Decision:** Record v5 as G25 leftover remasurement after
  D-248. Lands G25LJ-V4-CL-SF1 and G25LJ-V4-CL-SF2. Lands
  CODEX-D249-SF1. The candidate binds NOTHING. DR-G25 stays
  `OPEN`. leftover-design of OBL-G25-FX-AUTHORING remains on
  leftover-join.v5. leftover-join.v8 leftoverDesign `[]` is
  the current G23 leftover-join. Remainder of G25 execution
  remains qualification (D-056). Does not pin QUALIFIED. Does
  not invent fixture bytes. Does not collapse the two NT-3
  readings. Does not take over G23. Does not invent a pack
  IR. Does not invent a D9 code. Does not invent a section
  7.1 recipe. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY DR-114.
  Does not SATISFY DR-101. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. leftover-join.v4 remains split. leftover-join.v3
  is not current after this successor is recorded.
  leftover-join.v4 (G23) is not recorded as current. Naming
  parent is D-151, not leftover-join.v5. Claude Stage A
  leftover-join.v5 returned six unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage A leftover-join.v5 returned zero
  advisories and no observations. Claude Stage B turn 1
  returned zero observations and zero advisories. Codex
  Stage B turn 1 returned zero advisories and no
  observations; its finding is CODEX-D249-SF1, landed in
  this turn 2. Claude Stage B turn 2 returned zero
  observations and zero advisories. Codex Stage B turn 2
  returned zero advisories and no observations. This entry
  does not invent identifiers and does not claim that both
  reviewers' identifiers are preserved. Claude returned no
  observation identifiers. Codex returned no observation
  identifiers. Does not execute G25. Does not rewrite
  occupancy v3. Does not rewrite leftover-join.v8. Does not
  edit file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D249. Does not unwrite D-151, D-200, D-225,
  D-240, or D-248.
- **Commit:** C-D249.

## D-250 — Record g24 leftover-join.v4 as G24 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1
  split: Claude OBJECT 0/2 CLAUDE-D250-SF1, CLAUDE-D250-SF2
  (`artifacts/coordinator-decisions.D-250.review-adversarial.claude2.json`,
  `48be6bc5536e61932f3788c74fc6cde2e07a302606a1618b7bb291a98d9b5439`);
  Codex CONSENT
  (`artifacts/coordinator-decisions.D-250.review-adversarial.codex.json`,
  `fd95f94ba45f6404d76b194f2e2f2ab3da571716db20e791a67355c2e8e0deb0`).
  Not Dual REJECT. Not Dual CONSENT. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-250.turn2.review-adversarial.claude2.json`,
  `49a73d1cd6b8cf01ae63dd81fc589c3afbff7af3561d48b439066cc118bfe8e8`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-250.turn2.review-adversarial.codex.json`,
  `5de4a99265b952a418d421ea478eb7654469b4a541a52c95a222ec2a19f456c2`)
  CONSENT. Subject `coordinator-decisions.D-250.turn2.draft.md`
  `8c4707990266ccf1fa6f974a5fb54e3fc3a0f943470d74cb4d29b4923a1b433e`.
  Frozen turn 1 draft
  `coordinator-decisions.D-250.draft.md`
  `dadb52620b0c28d1a4f5dfa2067359afce04ac027992eac43615849271f859c6`.
  Frozen leftover-join
  `g24-leftover-join.v4.json`
  `c451f7ce20e93442172322ff2fd29a029a9a0ca209538ece7c590d32c72e43d7`
  Stage A Claude ACCEPT
  `64ae502fbe7d2d267e1d19a990a63de38fdb3961647fc3ca7b5ab63ceda23f8f`
  0/0; Stage A Codex ACCEPT
  `b956658feb003dbb1f5ea2c8d581e1d8b80afb554b870136b58dc8d50a0d99df`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g24-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g24-leftover-join.v4.json`
  `c451f7ce20e93442172322ff2fd29a029a9a0ca209538ece7c590d32c72e43d7`.
- **Decision:** Record v4 as G24 leftover remasurement after
  D-249. Lands CLAUDE-D250-SF1 and CLAUDE-D250-SF2. The
  candidate binds NOTHING. DR-G24 stays `OPEN`. leftover-design
  of OBL-G24-FX-AUTHORING remains on leftover-join.v4.
  leftover-join.v3 remains current at draft time. After this
  successor is recorded, leftover-join.v3 is not current.
  Occupancy v3 is the current G24 occupancy remasurement.
  Occupancy v1 is not current. leftover-join.v8 leftoverDesign
  `[]` is the current G23 leftover-join. leftover-join.v4
  (G23) is not current. leftover-join.v5 is the current G25
  leftover-join. leftover-join.v4 (G25) remains split.
  Remainder of G24 execution remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent fixture bytes. Does
  not invent a pack IR. Does not invent a D9 code. Does not
  invent a section 7.1 recipe. Does not reopen leftover-design
  of NT-1 or NT-2. Does not occupy the identifier. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-117. Does not SATISFY DR-114. Does not SATISFY DR-101.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Naming parent is
  D-150, not leftover-join.v4. naming v6 does not name G24.
  Claude Stage A leftover-join.v4 returned three unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage A leftover-join.v4 returned an empty
  observationsNotFindings list, zero advisories, and no
  observations. Claude Stage B turn 1 returned two unlabeled
  observations objects, each an observation paired with a
  standing. They carry no identifiers. Codex Stage B turn 1
  returned zero advisories and no observations; its verdict is
  CONSENT 0/0. Claude Stage B turn 2 returned four unlabeled
  observations objects. They carry no identifiers. Codex
  Stage B turn 2 returned zero advisories and no observations.
  This entry does not invent identifiers and does not claim
  that both reviewers' identifiers are preserved. Claude
  returned no observation identifiers. Codex returned no
  observation identifiers. Does not execute G24. Does not
  rewrite occupancy v3. Does not rewrite leftover-join.v8.
  Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D250. Does not unwrite D-150, D-199, D-224,
  D-240, or D-249.
- **Commit:** C-D250.

## D-251 — Record g26 leftover-join.v4 as G26 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-251.review-adversarial.claude2.json`,
  `59ef281831368a0ae350cc733f8a945d772313128eb9c60ce77bf75d81b88260`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-251.review-adversarial.codex.json`,
  `b3d29883d827268098a347109c6c20d4e94d26ea4a782736ab014cba53d98fb6`)
  CONSENT. Subject `coordinator-decisions.D-251.draft.md`
  `a8299c2727f474a88212e367d8200a4d55a69146bef9e40650665deb279e3652`.
  Frozen leftover-join
  `g26-leftover-join.v4.json`
  `aba91c5a43f77ccb9244977c746ca8238b54a4e3af5f431b37b74ce6e5e68591`
  Stage A Claude ACCEPT
  `0d9efc7dc6076f8fbadc1aa32c5e9fe77b6b40414d00ff1b4ea64cb1c338c114`
  0/0; Stage A Codex ACCEPT
  `ce19730b0389cc7e8cf6f5b351dbba4730a1245e59f6ba27df1d9550dce699b1`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g26-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g26-leftover-join.v4.json`
  `aba91c5a43f77ccb9244977c746ca8238b54a4e3af5f431b37b74ce6e5e68591`.
- **Decision:** Record v4 as G26 leftover remasurement after
  D-250. The candidate binds NOTHING. DR-G26 stays `OPEN`.
  leftover-design of OBL-G26-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G26 occupancy remasurement. Occupancy v1 is not
  current. Remainder of G26 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent SARIF goldens. Does not invent a
  D9 code. Does not invent a section 7.1 recipe. Does not
  restore G17. Does not reopen leftover-design of NT-5.
  Does not occupy the identifier. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-117. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A is
  not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is D-152, not
  leftover-join.v4. naming v6 does not name G26. Claude
  Stage A leftover-join.v4 returned three unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage A leftover-join.v4 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned three unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  and does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not
  execute G26. Does not rewrite occupancy v2. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D251. Does not unwrite D-152, D-201, D-226,
  or D-250.
- **Commit:** C-D251.

## D-252 — Record g27 leftover-join.v4 as G27 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-252.review-adversarial.claude2.json`,
  `47ad61dfae9ff5193479927068f628ac915d4ac298f7dbc7b43111a8aba271d4`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-252.review-adversarial.codex.json`,
  `bb8ad463cb7aa4b0036bc52709c298cd609af12eef26bdcc37a8803f1d66dd8d`)
  CONSENT. Subject `coordinator-decisions.D-252.draft.md`
  `9872285cfaeb32db93599424b3875d956bd866ed2309efbd3a93aba58a617ad9`.
  Frozen leftover-join
  `g27-leftover-join.v4.json`
  `630b226a852e2d6479513559cb0773fad67f80271d4814e726fc69c3aa943a5f`
  Stage A Claude ACCEPT
  `fecdb4e7839512b4ce9e888eb1a64b119c499a5b8fb09002fb970e324aacde2d`
  0/0; Stage A Codex ACCEPT
  `4ef134a69af303c540c733fc9cb6ab6755353e25242ea5770b93b1ca94334e56`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g27-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g27-leftover-join.v4.json`
  `630b226a852e2d6479513559cb0773fad67f80271d4814e726fc69c3aa943a5f`.
- **Decision:** Record v4 as G27 leftover remasurement after
  D-251. The candidate binds NOTHING. DR-G27 stays `OPEN`.
  leftover-design of OBL-G27-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G27 occupancy remasurement. Occupancy v1 is not
  current. Remainder of G27 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent sealed-Run goldens. Does not invent
  a D9 code. Does not invent a section 7.1 recipe. Does not
  reopen leftover-design of NT-6. Does not occupy the
  identifier. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY DR-114.
  Does not SATISFY DR-101. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Naming parent is D-153, not leftover-join.v4.
  naming v6 does not name G27. Claude Stage A leftover-join.v4
  returned no observationsNotFindings field and no
  advisories. Codex Stage A leftover-join.v4 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned an empty
  observationsNotFindings list. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G27. Does not rewrite occupancy v2. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D252. Does not unwrite D-153, D-202, D-227,
  or D-251.
- **Commit:** C-D252.

## D-253 — Record g28 leftover-join.v4 as G28 leftover remasurement

- **Date:** 2026-08-23
- **Status:** **ADOPTED 2026-08-23.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-253.review-adversarial.claude2.json`,
  `e2601a6c3497742e6c35af5720fc279c4a5a2f96f3ff1bd60a618e21efaf4c1a`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-253.review-adversarial.codex.json`,
  `76ce3aa88b27c4c2f8e88992289402b1d06e1dfb15b8c9d303f265dac71f85ba`)
  CONSENT. Subject `coordinator-decisions.D-253.draft.md`
  `12ef1053a4a0eacd15cabcdd69cee053403971a42aea4fdf8ab230606ec17f48`.
  Frozen leftover-join
  `g28-leftover-join.v4.json`
  `604dc98dfc4fd6ec2df1c22f2169b5ec921f2f43ab43ef7e0c98b48750dee085`
  Stage A Claude ACCEPT
  `1e58abe49f630cb59a185209673002b442be3546c7d304707d6d763a4937c90a`
  0/0; Stage A Codex ACCEPT
  `070fce7410a8721125b1e0906284a0cd6f88a84e282dbfd5b30b6155ec852c4d`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g28-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252.
  Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g28-leftover-join.v4.json`
  `604dc98dfc4fd6ec2df1c22f2169b5ec921f2f43ab43ef7e0c98b48750dee085`.
- **Decision:** Record v4 as G28 leftover remasurement after
  D-252. The candidate binds NOTHING. DR-G28 stays `OPEN`.
  leftover-design of OBL-G28-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v4 is the
  current G28 occupancy remasurement. Occupancy v3 is not
  current. Remainder of G28 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code, exit, or HostTermination.
  Does not invent a section 7.1 recipe. Does not reopen
  leftover-design of NT-7 or NT-8. Does not occupy the
  identifier. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Does not SATISFY DR-117. Does not SATISFY DR-114.
  Does not SATISFY DR-101. Gate 1 Class A is not opened.
  Not SATISFIED. Required-now stays 28. Condition-4 effect
  is zero. Naming parent is D-154, not leftover-join.v4.
  naming v6 does not name G28. Claude Stage A leftover-join.v4
  returned no observationsNotFindings field and no
  advisories. Codex Stage A leftover-join.v4 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned an empty
  observationsNotFindings list. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G28. Does not rewrite occupancy v4. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D253. Does not unwrite D-154, D-203, D-228,
  or D-252.
- **Commit:** C-D253.

## D-254 — Record g29 leftover-join.v4 as G29 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1
  split: Claude OBJECT 1/0 D254-MF-1
  (`artifacts/coordinator-decisions.D-254.review-adversarial.claude2.json`,
  `0e0073358fa5ba70ab5b80b762928890beea57de90115bf31e904809b7f51774`);
  Codex CONSENT
  (`artifacts/coordinator-decisions.D-254.review-adversarial.codex.json`,
  `07e05d62ecd527815efd690b002bf38a514721c29b1cc0002f750147b8365bcc`).
  Not Dual REJECT. Not Dual CONSENT. Claude 2 turn 2
  (`artifacts/coordinator-decisions.D-254.turn2.review-adversarial.claude2.json`,
  `ddebac333238651d93377d746dbc283e9a01c3d148bb12c44bd0935f77cd3c56`)
  CONSENT. Codex turn 2
  (`artifacts/coordinator-decisions.D-254.turn2.review-adversarial.codex.json`,
  `5f3bfde7483aab39f33323feededf3d61149f74fd467f56f9ee989d5f8657f5d`)
  CONSENT. Subject `coordinator-decisions.D-254.turn2.draft.md`
  `ecf5d165f015c5f110c77b7b81e9bd54e924a5971af11dc6e14e7e6ba72dc027`.
  Frozen turn 1 draft
  `coordinator-decisions.D-254.draft.md`
  `a91add3e4494f540a3b03fbf59661772b74c53639d03a22ae361a9ea5f4765db`.
  Frozen leftover-join
  `g29-leftover-join.v4.json`
  `9e1af4ba3b21e483154825fa2c6d275f7ee805d1fb455f01c9d35e48411c3f64`
  Stage A Claude ACCEPT
  `9c900fe4294b154c3b81c3d2df66676fe8ea22bfd975513f6f9016cfdb4d731a`
  0/0; Stage A Codex ACCEPT
  `39e4509b542588b15f3fe2bdc4be028a15b75c3fac73a1b21b82c49e9b3b53f4`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g29-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g29-leftover-join.v4.json`
  `9e1af4ba3b21e483154825fa2c6d275f7ee805d1fb455f01c9d35e48411c3f64`.
- **Decision:** Record v4 as G29 leftover remasurement after
  D-253. Lands D254-MF-1. The candidate binds NOTHING.
  DR-G29 stays `OPEN`. leftover-design of
  OBL-G29-FX-AUTHORING remains on leftover-join.v4.
  leftover-join.v3 remains current at draft time. After this
  successor is recorded, leftover-join.v3 is not current.
  Occupancy v3 is the current G29 occupancy remasurement.
  Occupancy v2 is not current. Remainder of G29 execution
  remains qualification (D-056). Does not pin QUALIFIED.
  Does not invent fixture bytes. Does not invent a D9 code.
  Does not invent a section 7.1 recipe. Does not reopen
  leftover-design of EE-1, EE-2, EE-3b, EE-4, EE-5a, EE-5b,
  or EE-6a. Does not take over G21, G23, G24, or G30. Does
  not occupy the identifier. Does not SATISFY DR-117. Does
  not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A
  is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is D-157, not
  leftover-join.v4. naming v6 does not name G29. Claude
  Stage A leftover-join.v4 returned no observationsNotFindings
  field and no advisories. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. Claude Stage B turn 1
  returned one unlabeled observationsNotFindings object, an
  observation paired with a whyNotCharged. It carries no
  identifier. Codex Stage B turn 1 returned zero advisories
  and no observations; its verdict is CONSENT 0/0. Claude
  Stage B turn 2 returned one unlabeled
  observationsNotFindings object, an observation paired with
  a whyNotCharged. It carries no identifier. Codex Stage B
  turn 2 returned zero advisories and no observations. This
  entry does not invent identifiers and does not claim that
  both reviewers' identifiers are preserved. Claude returned
  no observation identifiers. Codex returned no observation
  identifiers. Does not execute G29. Does not rewrite
  occupancy v3. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D254. Does not unwrite D-157, D-204, D-229,
  or D-253.
- **Commit:** C-D254.

## D-255 — Record g30 leftover-join.v4 as G30 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-255.review-adversarial.claude2.json`,
  `ef7ca05ec2413fc164259fa1de439cf38b2aa4c3de9ed464e804fe38f109ab13`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-255.review-adversarial.codex.json`,
  `08089af5e7d1a1d9a2dfeb354830d70e8d395e2b8352fa85bf7890329c9d771a`)
  CONSENT. Subject `coordinator-decisions.D-255.draft.md`
  `98451b08a9693b5c0c10bb02d37956130c0cba43cbe161e93779ed3cf053ddbb`.
  Frozen leftover-join
  `g30-leftover-join.v4.json`
  `3f3d84e0e24a2aea0ba95c282f809c8343d1827d0577ca8396d4560c5e012c75`
  Stage A Claude ACCEPT
  `07667a941ffca1d77685e26a7dc9761e7ce57047777f1df74e5b682e48596dde`
  0/0; Stage A Codex ACCEPT
  `86457508d22f4b75adfa8f9c3f4571a1e6852d51b4026c11f70e6a4658d221e0`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g30-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g30-leftover-join.v4.json`
  `3f3d84e0e24a2aea0ba95c282f809c8343d1827d0577ca8396d4560c5e012c75`.
- **Decision:** Record v4 as G30 leftover remasurement after
  D-254. The candidate binds NOTHING. DR-G30 stays `OPEN`.
  leftover-design of OBL-G30-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G30 occupancy remasurement. Occupancy v1 is not
  current. Remainder of G30 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent the DR-131 pack. Does
  not mint Rust-as-core. Does not reopen leftover-design of
  EE-7a, EE-7b, or EE-7d. Does not take over DR-101, G13,
  G14, G16, G24, or G29. Does not occupy the identifier.
  Does not SATISFY DR-117. Does not SATISFY DR-131. Does
  not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Naming parent is D-158, not leftover-join.v4.
  naming v6 does not name G30. Claude Stage A leftover-join.v4
  returned six unlabeled observationsNotFindings strings.
  They carry no identifiers. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. Claude Stage B returned
  three unlabeled observationsNotFindings strings. They
  carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G30. Does not rewrite occupancy v2. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D255. Does not unwrite D-158, D-205, D-230,
  or D-254.
- **Commit:** C-D255.

## D-256 — Record g19 leftover-join.v4 as G19 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-256.review-adversarial.claude2.json`,
  `aed4affb598fabbc2397a2850ac96d4e5bc52de096820775bce31862aa64f567`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-256.review-adversarial.codex.json`,
  `18b3294df22b63dca45dadd6c1e941ab20cd4c284e8488e2321df2b134f53b98`)
  CONSENT. Subject `coordinator-decisions.D-256.draft.md`
  `fb153bb35e2deb8d26bb3850714244e1026a53a527023b192bb8da1a3516a2a4`.
  Frozen leftover-join
  `g19-leftover-join.v4.json`
  `dd16d1607e7105e93f4bc6da252a9e33d008707f39cd84eb5322ffaf9b7a707f`
  Stage A Claude ACCEPT
  `b57e492bf45fabea5640db133a59d16c603615b3fcf3dbe8a001c72d0c26d6ce`
  0/0; Stage A Codex ACCEPT
  `93c0d45e65bad97caeeffbc7e79dbcc53654678c3f482098f6bc16fb1bfb4a2b`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g19-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g19-leftover-join.v4.json`
  `dd16d1607e7105e93f4bc6da252a9e33d008707f39cd84eb5322ffaf9b7a707f`.
- **Decision:** Record v4 as G19 leftover remasurement after
  D-255. The candidate binds NOTHING. DR-G19 stays `OPEN`.
  leftover-design of OBL-G19-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G19 occupancy remasurement. Occupancy v1 is not
  current. Remainder of G19 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent a grant-journal,
  inherit-blocked envelope, or monotonic window. Does not
  invent a sealed-Run class. Does not steal
  OBL-GRANT-JOURNAL, OBL-INHERIT-BLOCKED, or OBL-MONOTONIC.
  Does not take over G27. Does not occupy the identifier.
  Does not SATISFY DR-124. Does not SATISFY DR-117. Does
  not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A
  is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v4. D-086 named the identifier.
  Claude Stage A leftover-join.v4 returned three unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage A leftover-join.v4 returned an empty
  observationsNotFindings list, zero advisories, and no
  observations. Claude Stage B returned four unlabeled
  observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and
  no observations. This entry does not invent identifiers
  and does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not
  execute G19. Does not rewrite occupancy v2. Does not
  edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D256. Does not unwrite D-086, D-194, D-222,
  or D-255.
- **Commit:** C-D256.

## D-257 — Record g09 leftover-join.v11 as G09 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-257.review-adversarial.claude2.json`,
  `b30c519d42121d1fe3684b8041f15a788ef277a877bf62cb3de697a41a866cb8`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-257.review-adversarial.codex.json`,
  `826f352337b6e537c7cfc6b47c122c4ebded3318b016b11a0cd47deecb7a2f92`)
  CONSENT. Subject `coordinator-decisions.D-257.draft.md`
  `74be56ea2865d12d6728d3641e721a126e1821b705a13678e6ba5fff56c0c6dc`.
  Frozen leftover-join
  `g09-leftover-join.v11.json`
  `945f8faeb8998a461cc66bcce700437968bae7c53f40cafdd71175fba85c191d`
  Stage A Claude ACCEPT
  `be19f80649a463e09736a35012badd05eb1a35e332fb34548e83e54d18b046b6`
  0/0; Stage A Codex ACCEPT
  `14c676f7d8bb60c368cee7ec78a2d83c15439712ba00c5cdc71c3b387daa79db`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g09-leftover-join.v11.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g09-leftover-join.v11.json`
  `945f8faeb8998a461cc66bcce700437968bae7c53f40cafdd71175fba85c191d`.
- **Decision:** Record v11 as G09 leftover remasurement after
  D-256. The candidate binds NOTHING. DR-G09 stays `OPEN`.
  leftover-design of OBL-FX-AUTHORING remains on
  leftover-join.v11. leftover-join.v10 remains current at
  draft time. After this successor is recorded,
  leftover-join.v10 is not current. Occupancy v4 is the
  current G09 occupancy remasurement. Occupancy v3 is not
  current. Remainder of G09 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent a decision-record
  envelope. Does not steal OBL-R10-AUTHORING,
  OBL-R6-AUTHORING, OBL-FC-C1, or OBL-BLK-1..4. Does not
  occupy the identifier. Does not SATISFY DR-105. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Does not SATISFY DR-114. Does not SATISFY DR-101.
  Gate 1 Class A is not opened. Not SATISFIED. Required-now
  stays 28. Condition-4 effect is zero. Naming parent is
  naming v6 (D-145), not leftover-join.v11. D-086 named the
  identifier. Claude Stage A leftover-join.v11 returned
  three unlabeled observationsNotFindings objects, each an
  observation paired with a whyNotAFinding. They carry no
  identifiers. Codex Stage A leftover-join.v11 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage B returned zero advisories and no
  observations. This entry does not invent identifiers and
  does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not
  execute G09. Does not rewrite occupancy v4. Does not
  edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D257. Does not unwrite D-086, D-189, D-220,
  or D-256.
- **Commit:** C-D257.

## D-258 — Record g12 leftover-join.v4 as G12 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-258.review-adversarial.claude2.json`,
  `14684aa6c1c21814e0c1ab90d093d6e0cbc6d95542d278eca314311da7f2e2e5`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-258.review-adversarial.codex.json`,
  `493e6f5374a122c971c2a7afdb706dbc73f06dca134420d9f69d765d980e203b`)
  CONSENT. Subject `coordinator-decisions.D-258.draft.md`
  `38fb63decdcf9b903427d845f5053303c0f6c00079f58cd3dfcb98bcbca1500d`.
  Frozen leftover-join
  `g12-leftover-join.v4.json`
  `60eed5d42ec4c52ed042d6c069abddbadf055cf97cf6c151c3d35952ee4a481c`
  Stage A Claude ACCEPT
  `b40f29217a891627df5eca7ac2d58ccee84d1bac5117070bb875285d77867eb8`
  0/0; Stage A Codex ACCEPT
  `5581d18f79e640075010f466b0d67e9afcb2d751b08783ab85bb4c7bb8ec9d5d`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g12-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g12-leftover-join.v4.json`
  `60eed5d42ec4c52ed042d6c069abddbadf055cf97cf6c151c3d35952ee4a481c`.
- **Decision:** Record v4 as G12 leftover remasurement after
  D-257. The candidate binds NOTHING. DR-G12 stays `OPEN`.
  leftover-design of OBL-DOCTOR-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v6 is the
  current G12 occupancy remasurement. Occupancy v4 is not
  current. Remainder of G12 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not steal OBL-JOIN-FX-AUTHORING,
  OBL-JOIN-FX-EXECUTION, OBL-FC-C1, or OBL-BLK-1..4. Does
  not take over G21. Does not occupy the identifier. Does
  not SATISFY DR-114. Does not SATISFY DR-117. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-105. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v4. D-086 named the identifier.
  Claude Stage A leftover-join.v4 returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage A leftover-join.v4 returned an empty
  observationsNotFindings list, zero advisories, and no
  observations. Claude Stage B returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage B returned zero advisories and no
  observations. This entry does not invent identifiers and
  does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not
  execute G12. Does not rewrite occupancy v6. Does not
  edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D258. Does not unwrite D-086, D-190, D-221,
  or D-257.
- **Commit:** C-D258.

## D-259 — Record g08 leftover-join.v4 as G08 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-259.review-adversarial.claude2.json`,
  `380be26bd185d1e6751ba29bd7b578e729c9286a833672b6503a0df80d8bb7c1`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-259.review-adversarial.codex.json`,
  `a7839e42858213ca12e49cb41a0ab5718cf2a6c1a329b36c869d11f83465e023`)
  CONSENT. Subject `coordinator-decisions.D-259.draft.md`
  `ca270a87a01665198d19724c58c00577c70e4b9335f055078918ddf35c2c9035`.
  Frozen leftover-join
  `g08-leftover-join.v4.json`
  `7bec9b40624dd81e717709ae6f16f6ef922396eddf2e96aa157d45e89b91c663`
  Stage A Claude ACCEPT
  `0dd601c79ff45bfae07a8f54877045f093f6a7a06faf0ed51bcbac36cfd446c8`
  0/0; Stage A Codex ACCEPT
  `7c3e5f00bc970f471c28ff55342e73a9019208957c3c797b3065b21f2c2edd99`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g08-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g08-leftover-join.v4.json`
  `7bec9b40624dd81e717709ae6f16f6ef922396eddf2e96aa157d45e89b91c663`.
- **Decision:** Record v4 as G08 leftover remasurement after
  D-258. The candidate binds NOTHING. DR-G08 stays `OPEN`.
  leftover-design of OBL-G08-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v3 is the
  current G08 occupancy remasurement. Occupancy v2 is not
  current. signed-index leftover-join.v3 remains the current
  DR-112 leftover-join. signed-index leftover-join.v2 is not
  current. Remainder of G08 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not steal OBL-RESERVED-NUMBERS.
  Does not mint quorum, clock, emergency, or waiver numbers.
  Does not invent a recovery ceremony implementation. Does
  not occupy the identifier. Does not SATISFY DR-112. Does
  not SATISFY DR-117. Does not SATISFY DR-131. Does not
  SATISFY DR-133. Does not SATISFY DR-114. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent is naming v6 (D-145), not leftover-join.v4. D-086
  named the identifier. Claude Stage A leftover-join.v4
  returned three unlabeled observationsNotFindings strings.
  They carry no identifiers. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. Claude Stage B returned
  four unlabeled observationsNotFindings strings. They
  carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G08. Does not rewrite occupancy v3. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D259. Does not unwrite D-086, D-188, D-211,
  or D-258.
- **Commit:** C-D259.

## D-260 — Record language-runtime leftover-join.v5 as G14 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 3 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Turn 1
  split: Claude OBJECT 1/0 MF-1
  (`artifacts/coordinator-decisions.D-260.review-adversarial.claude2.json`,
  `119bedc533b2a8337f695eedf1ea393be8b755172ba8f8ba18f86492e9498fa4`);
  Codex OBJECT 1/0 D260-MF-1
  (`artifacts/coordinator-decisions.D-260.review-adversarial.codex.json`,
  `bfef175206f5df59dafa79a1000fbe995e4ce4f3e9879adf4b5aa13e89cd5452`).
  Same class: live remasurement recited DR-118 as `OPEN`; live
  file 08 token is `DECIDED-V1-NOT-INTEGRATED`. Dual OBJECT.
  Not Dual REJECT. Not Dual CONSENT. Turn 2 split: Claude
  OBJECT 1/0 MF-2
  (`artifacts/coordinator-decisions.D-260.turn2.review-adversarial.claude2.json`,
  `5c0c93a38e5567e5fb9ea53b9b4c74f570179f99dff25f114411f3b0cd3d63ac`);
  Codex OBJECT 1/0 D260-T2-MF-1
  (`artifacts/coordinator-decisions.D-260.turn2.review-adversarial.codex.json`,
  `ab3da96190e0bee5bc060c342790b5db8611be6edfdcccb9bce46cf61a1d935c`).
  Same class: turn 2 draft pinned the frozen turn-1 Codex
  review at
  `d54d007bb4a4399d613d2c2d26a4b4768b75c6551bc586678dd3086af1432ba0`;
  live mode-0444 file hashes to
  `bfef175206f5df59dafa79a1000fbe995e4ce4f3e9879adf4b5aa13e89cd5452`.
  Dual OBJECT. Not Dual REJECT. Not Dual CONSENT. Claude 2
  turn 3
  (`artifacts/coordinator-decisions.D-260.turn3.review-adversarial.claude2.json`,
  `d3d8a3e865a99220f605698212ae8e63593162afacd84932e66415912aef820b`)
  CONSENT. Codex turn 3
  (`artifacts/coordinator-decisions.D-260.turn3.review-adversarial.codex.json`,
  `fa1e5fd3df1fb0011473a8e0fbfa2c82f5f08304bb785c3a40e1c545e5e76434`)
  CONSENT. Subject `coordinator-decisions.D-260.turn3.draft.md`
  `c74f50a869754e10b721575fe3893973365c014cc418aca701ead6e9fe82aecd`.
  Frozen turn 1 draft
  `coordinator-decisions.D-260.draft.md`
  `9aa31e6b66137530c7784c44889435c8a32b34a6e3de4b84151dfae62215b41a`.
  Frozen turn 2 draft
  `coordinator-decisions.D-260.turn2.draft.md`
  `2e0f1fbe8654f40019e381c60074189ccdac9465ea56c1e934bf8efa850ea0df`.
  Frozen leftover-join
  `language-runtime-leftover-join.v5.json`
  `c92884f7c9d69132de418063cb755a616898f9b80b4dc46ad98dfa648b3e449c`
  Stage A Claude ACCEPT
  `20b8ff5f76192bef9bbcbbb332ddbd5ad0a6100bee962e4b40e6019b2b5d3838`
  0/0; Stage A Codex ACCEPT
  `78ef66418232e63119e376177e7601617b56e5514ad95b4745d234a07f0368eb`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-runtime-leftover-join.v5.json` (0 blockers,
  0 SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/language-runtime-leftover-join.v5.json`
  `c92884f7c9d69132de418063cb755a616898f9b80b4dc46ad98dfa648b3e449c`.
- **Decision:** Record leftover-join.v5 as G14 leftover
  remasurement after D-259. Lands D260-T2-MF-1 / MF-2. Lands
  D260-MF-1 / MF-1. The candidate binds NOTHING. DR-G14 stays
  `OPEN`. leftover-design of OBL-G14-FX-AUTHORING remains on
  leftover-join.v5. leftover-join.v4 remains current at
  draft time. After this successor is recorded,
  leftover-join.v4 is not current. Occupancy v4 is the
  current G14 occupancy remasurement. Occupancy v1 is not
  current. language-quality leftover-join.v3 remains the
  current DR-118 leftover-join. language-quality leftover-join.v2
  is not current. Remainder of G14 execution remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D9 code. Does not
  invent a section 7.1 recipe. Does not invent a numeric
  threshold. Does not mint Rust-as-core. Does not steal
  OBL-THRESHOLDS, OBL-MATRIX-CORPUS, or OBL-G13-RESERVED.
  Does not name G13 into required-now. Does not occupy the
  identifier. Does not SATISFY DR-118. Live remasurement
  recites DR-118 as `DECIDED-V1-NOT-INTEGRATED`, not `OPEN`.
  Does not reopen DR-119 SATISFIED. Does not SATISFY DR-117.
  Does not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A is
  not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v5. D-086 named the identifier.
  Claude Stage A leftover-join.v5 returned four unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage A leftover-join.v5 returned an empty
  observationsNotFindings list, zero advisories, and no
  observations. Claude Stage B turn 1 returned four unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage B turn 1 returned zero advisories and no
  observations; its verdict is OBJECT 1/0 D260-MF-1. Claude
  Stage B turn 2 returned four unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage B turn 2 returned zero advisories and no
  observations; its verdict is OBJECT 1/0 D260-T2-MF-1. Claude
  Stage B turn 3 returned four unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Codex Stage B turn 3 returned zero advisories and no
  observations. This entry does not invent identifiers and
  does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not execute
  G14. Does not rewrite occupancy v4. Does not edit file 08.
  Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D260. Does not unwrite D-086, D-179, D-213,
  or D-259.
- **Commit:** C-D260.

## D-261 — Record g15 leftover-join.v4 as G15 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-261.review-adversarial.claude2.json`,
  `8f9974c03bc1fbd38b2830aa09c4aab9d77a237f0169b2d3017f34d2a51e70e2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-261.review-adversarial.codex.json`,
  `2a5d02178bf64426d8b506223cb3e55feff38e8dff6348e4f903c13e5ecf255d`)
  CONSENT. Subject `coordinator-decisions.D-261.draft.md`
  `5ec040d0aa040f2ed2c0875f732452b75655176fc26a346ab47e41ecd5e03b16`.
  Frozen leftover-join
  `g15-leftover-join.v4.json`
  `fadc9c0c0c7f466b95d2cbf6ad50d743da9463720b30b280b8b36caaa4f3666d`
  Stage A Claude ACCEPT
  `86a50b85132d991076177090b6b26341e97be1bb0da48b581e3fef3d02287658`
  0/0; Stage A Codex ACCEPT
  `cbbb84cb79f59ce6081c7531646b8c65ae0f926d074de8c36e27a40857af6a7e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g15-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g15-leftover-join.v4.json`
  `fadc9c0c0c7f466b95d2cbf6ad50d743da9463720b30b280b8b36caaa4f3666d`.
- **Decision:** Record v4 as G15 leftover remasurement after
  D-260. The candidate binds NOTHING. DR-G15 stays `OPEN`.
  leftover-design of OBL-AT-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v9 is the
  current G15 occupancy remasurement. Occupancy v7 is not
  current. packaging leftover-join.v3 remains the current
  DR-120 leftover-join. packaging leftover-join.v2 is not
  current. component-manifest leftover-join.v6 remains the
  current DR-103 leftover-join. component-manifest leftover-join.v4
  is not current. Remainder of G15 execution remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a D9 code. Does not
  invent a section 7.1 recipe. Does not invent an adapter
  implementation. Does not invent a numeric threshold. Does
  not mint a Rust adapter as slice-1 required. Does not steal
  OBL-ADAPTER-IMPL, OBL-WINDOWS-PATH, OBL-ENVELOPE-MISMATCH,
  OBL-UNICODE-NORM, OBL-OD-1, or OBL-OD-2. Does not occupy
  the identifier. Does not SATISFY DR-120. Does not SATISFY
  DR-103. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Naming parent is naming v6 (D-145), not leftover-join.v4.
  D-086 named the identifier. Claude Stage A leftover-join.v4
  returned three unlabeled observationsNotFindings strings.
  They carry no identifiers. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. Claude Stage B returned
  five unlabeled observationsNotFindings strings. They
  carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not invent
  identifiers and does not claim that both reviewers'
  identifiers are preserved. Claude returned no observation
  identifiers. Codex returned no observation identifiers.
  Does not execute G15. Does not rewrite occupancy v9. Does
  not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D261. Does not unwrite D-086, D-191, D-214,
  or D-260.
- **Commit:** C-D261.

## D-262 — Record g16 leftover-join.v4 as G16 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-262.review-adversarial.claude2.json`,
  `b513c9ddd75de07a6337e68532cca93592e3f684592b1607c44ae2bc2b8d0d57`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-262.review-adversarial.codex.json`,
  `86b18b636f0120fee0386a15139e2d16200c2ca7c4afb113cf2083619650dcfb`)
  CONSENT. Subject `coordinator-decisions.D-262.draft.md`
  `4ec36d0fe18d6319b22efdfa6832ec7efdc8ac10253f8caf81de01196c2bacfb`.
  Frozen leftover-join
  `g16-leftover-join.v4.json`
  `446c6bbe121c72e247b3f4af313f18b5cf76aad3d6b91328c3860606bed314e8`
  Stage A Claude ACCEPT
  `beb61b4f3b4de298067e16e863aef231f46d62a2e7874220d50bb6c308b29a6d`
  0/0; Stage A Codex ACCEPT
  `d0e2043cbb7e945bd1d186be8c6d736b5a2b225d9768c5854399880c4727261a`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g16-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g16-leftover-join.v4.json`
  `446c6bbe121c72e247b3f4af313f18b5cf76aad3d6b91328c3860606bed314e8`.
- **Decision:** Record v4 as G16 leftover remasurement after
  D-261. The candidate binds NOTHING. DR-G16 stays `OPEN`.
  leftover-design of OBL-G16-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v5 is the
  current G16 occupancy remasurement. Occupancy v2 is not
  current. monorepo leftover-join.v3 remains the current
  DR-121 leftover-join. monorepo leftover-join.v2 is not
  current. Remainder of G16 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent reserved CI encodings.
  Does not apply monorepo-ci-contract.v16. Does not steal
  OBL-CI-ENCODING-RESERVED. Does not mint Rust-as-core. Does
  not name G13 into required-now. Does not occupy the
  identifier. Does not SATISFY DR-121. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Does not SATISFY DR-114. Does not SATISFY DR-101. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Naming parent is naming
  v6 (D-145), not leftover-join.v4. D-086 named the
  identifier. Claude Stage A leftover-join.v4 returned four
  unlabeled observationsNotFindings objects, each an
  observation paired with a whyNotAFinding. They carry no
  identifiers. Codex Stage A leftover-join.v4 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned four unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage B returned zero advisories and no
  observations. This entry does not invent identifiers and
  does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers. Does not
  execute G16. Does not rewrite occupancy v5. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D262. Does not unwrite D-086, D-192, D-215,
  or D-261.
- **Commit:** C-D262.

## D-263 — Record g18 leftover-join.v5 as G18 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-263.review-adversarial.claude2.json`,
  `f6474afb90115dccfb0454d74db38e27aa2f7c0a500e299044a5daf7f56ae0af`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-263.review-adversarial.codex.json`,
  `ae64d1559ded41e3729fee73c7ca5a094118bfc5db5e7cd63723043140e86c96`)
  CONSENT. Subject `coordinator-decisions.D-263.draft.md`
  `15485a2fdb3c3c8a6a653fbedeebae1f4cebd2218fd211836bdda8d8e06472cc`.
  Frozen leftover-join
  `g18-leftover-join.v5.json`
  `3d9aa52369c53d4a22667bf7616afe0bb2c6da2af4d22ed6a6b9f10ac1073c8a`
  Stage A Claude ACCEPT
  `1d00171ff3ebbfe2de8d831792e36613b6664cde23da111b75a52d061823a4dd`
  0/0; Stage A Codex ACCEPT
  `70584f28506b5cb38d583f59d3ad8b80ad5a7dab97a1219d009e767aa1a4279b`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g18-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g18-leftover-join.v5.json`
  `3d9aa52369c53d4a22667bf7616afe0bb2c6da2af4d22ed6a6b9f10ac1073c8a`.
- **Decision:** Record v5 as G18 leftover remasurement after
  D-262. The candidate binds NOTHING. DR-G18 stays `OPEN`.
  leftover-design of OBL-G18-FX-AUTHORING remains on
  leftover-join.v5. leftover-join.v4 remains current at
  draft time. After this successor is recorded,
  leftover-join.v4 is not current. Occupancy v4 is the
  current G18 occupancy remasurement. Occupancy v2 is not
  current. lifecycle leftover-join.v3 remains the current
  DR-107 leftover-join. lifecycle leftover-join.v2 is not
  current. Remainder of G18 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent a journal. Does not
  steal OBL-ENCODING-RESERVED. Does not occupy the
  identifier. Does not SATISFY DR-107. Live remasurement
  recites DR-107 as `PROPOSED-CLOSED-FOR-REVIEW`, not
  `OPEN`. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Naming parent is naming v6 (D-145), not leftover-join.v5.
  D-086 named the identifier. Claude Stage A leftover-join.v5
  returned no observationsNotFindings field and no
  advisories. Codex Stage A leftover-join.v5 returned an
  empty observationsNotFindings list, zero advisories, and
  no observations. Claude Stage B returned two unlabeled
  observationsNotFindings objects, each an observation
  paired with a whyNotAFinding. They carry no identifiers.
  Codex Stage B returned zero advisories and no
  observations. This entry does not invent identifiers and
  does not claim that both reviewers' identifiers are
  preserved. Claude returned no observation identifiers.
  Codex returned no observation identifiers.
  CLAUDE-G18LJ-V2-SF1 already landed in this lineage at
  leftover-join.v4. This entry does not re-land it. Does not
  execute G18. Does not rewrite occupancy v4. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D263. Does not unwrite D-086, D-193, D-216,
  or D-262.
- **Commit:** C-D263.

## D-264 — Record g20 leftover-join.v4 as G20 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-264.review-adversarial.claude2.json`,
  `6f486332e7acfb8059fa742208d4a8a6bc75aec8ff8042c6231f710327b3fdcc`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-264.review-adversarial.codex.json`,
  `3ae4044a02aa1c14ae6b68029fad93e35e61ec80ac736c3c892dea93311c0880`)
  CONSENT. Subject `coordinator-decisions.D-264.draft.md`
  `787b80fae01502973bb7ee7a659763dfc2dde8d28673fc77aca982b082883426`.
  Frozen leftover-join
  `g20-leftover-join.v4.json`
  `9de955ea25b2e896f1fc31e2c7b10f507a99157acfa7711dbbbb844cd16b5ff2`
  Stage A Claude ACCEPT
  `859b0d965544fddb5a9918033b59a24b0bb85860fbd30c186f82f67f7ba9d07a`
  0/0; Stage A Codex ACCEPT
  `5548f330e95a35cf70f9603cb78a9414a2d7d371085ffa297999304a59cb7802`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g20-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263.
  Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g20-leftover-join.v4.json`
  `9de955ea25b2e896f1fc31e2c7b10f507a99157acfa7711dbbbb844cd16b5ff2`.
- **Decision:** Record v4 as G20 leftover remasurement after
  D-263. The candidate binds NOTHING. DR-G20 stays `OPEN`.
  leftover-design of OBL-G20-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G20 occupancy remasurement. Occupancy v1 is not
  current. sdk leftover-join.v5 remains the current
  DR-125 leftover-join. sdk leftover-join.v4 is not
  current. Remainder of G20 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not invent reserved SDK APIs.
  Does not steal OBL-SDK-API-RESERVED. Does not close
  OBL-DR125-ACTIVATION. Does not occupy the identifier.
  Does not SATISFY DR-125. Does not SATISFY DR-117. Does
  not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A
  is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v4. D-086 named the
  identifier. Claude Stage A leftover-join.v4 returned
  four named advisories ADV-1, ADV-2, ADV-3, and ADV-4.
  No change requested. They carry those identifiers.
  Codex Stage A leftover-join.v4 returned an empty
  observationsNotFindings list, zero advisories, and no
  observations. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim
  that both reviewers' identifiers are preserved. Codex
  Stage A returned no observation identifiers. Claude
  Stage B returned four unlabeled observationsNotFindings
  objects, each an observation paired with a whyNotAFinding.
  They carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not
  invent identifiers. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G20. Does not rewrite
  occupancy v2. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D264. Does not unwrite D-086, D-195, D-217,
  or D-263.
- **Commit:** C-D264.

## D-265 — Record g22 leftover-join.v4 as G22 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-265.review-adversarial.claude2.json`,
  `dd18989fdbd9718988261b253284a901e1d7e5edacf043220e6da5a0ff993871`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-265.review-adversarial.codex.json`,
  `62246a09a500736ad27b77b90c5ec4612299b0e6f7ca393d1f95589509d71cd3`)
  CONSENT. Subject `coordinator-decisions.D-265.draft.md`
  `0c174a60e0445756e6c1c37fd22b84d90fbed059a34018fc4455bb4d4e32562f`.
  Frozen leftover-join
  `g22-leftover-join.v4.json`
  `e5cd19661b977c5ab2d57d0347cd0d18523f4927829bfd55b9568d5dc4cdc4df`
  Stage A Claude ACCEPT
  `66fd4cfa82c55ec0df8b537b8529ca6c00a5a9f76c7efa5685cfc09d9a547c86`
  0/0; Stage A Codex ACCEPT
  `9ffc8c6fef104ffc798975eab0aad40d5f8cee5309896708084b24482ccfee0d`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g22-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g22-leftover-join.v4.json`
  `e5cd19661b977c5ab2d57d0347cd0d18523f4927829bfd55b9568d5dc4cdc4df`.
- **Decision:** Record v4 as G22 leftover remasurement after
  D-264. The candidate binds NOTHING. DR-G22 stays `OPEN`.
  leftover-design of OBL-G22-FX-AUTHORING remains on
  leftover-join.v4. leftover-join.v3 remains current at
  draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v2 is the
  current G22 occupancy remasurement. Occupancy v1 is not
  current. platform-tcb leftover-join.v6 remains the current
  DR-126 leftover-join. platform-tcb leftover-join.v5 is not
  current. Remainder of G22 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not populate reserved TCB tables.
  Does not invent Rosetta. Does not apply TCB v45. Does not
  steal OBL-RESERVED-TABLES. Does not occupy the identifier.
  Does not SATISFY DR-126. Does not SATISFY DR-117. Does
  not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A
  is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v4. D-086 named the
  identifier. Claude Stage A leftover-join.v4 returned
  three unlabeled observationsNotFindings strings. They
  carry no identifiers. No advisories field. Codex Stage A
  leftover-join.v4 returned an empty observationsNotFindings
  list, zero advisories, and no observations. This entry
  does not invent identifiers. It does not claim that both
  reviewers' identifiers are preserved. Claude Stage A
  returned no observation identifiers. Codex Stage A
  returned no observation identifiers. Claude Stage B
  returned four unlabeled observationsNotFindings strings.
  They carry no identifiers. Codex Stage B returned zero
  advisories and no observations. This entry does not
  invent identifiers. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G22. Does not rewrite
  occupancy v2. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D265. Does not unwrite D-086, D-197, D-219,
  or D-264.
- **Commit:** C-D265.

## D-266 — Record packaging leftover-join.v4 as DR-120 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-266.review-adversarial.claude2.json`,
  `aac3c703c2df60170a7e00a7d60fa2289767bbcc37db1e8018ddfd10ad138c78`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-266.review-adversarial.codex.json`,
  `448c9e02b75f2744bc0a753390e40f887f2b5c15a60f2fb3f1b5c53a10603fa9`)
  CONSENT. Subject `coordinator-decisions.D-266.draft.md`
  `d31b6d4bb61a1d6f8e3a805e5b58fb0787557d05610910507b6efa1e60df8c14`.
  Frozen leftover-join
  `packaging-leftover-join.v4.json`
  `03251cc80cc774c12335ad038eedbb38ce73431623306f11fa1e75e40db61d07`
  Stage A Claude ACCEPT
  `ea6c5b3244efd8a4290e840ff9b073ef0e94e89f9e408c4a47cc17b5890ded41`
  0/0; Stage A Codex ACCEPT
  `d4ceebd19e4bda2b82b7d9428434ef8b7122d4006a4e7aedb6d460720d20c5cd`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `packaging-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/packaging-leftover-join.v4.json`
  `03251cc80cc774c12335ad038eedbb38ce73431623306f11fa1e75e40db61d07`.
- **Decision:** Record v4 as DR-120 leftover remasurement after
  D-265. The candidate binds NOTHING. DR-120 stays `OPEN`.
  leftover-design of OBL-ADAPTER-IMPL and OBL-AT-FX-AUTHORING
  remains on leftover-join.v4. leftover-join.v3 remains
  current at draft time. After this successor is recorded,
  leftover-join.v3 is not current. Occupancy v9 is the
  current G15 occupancy remasurement. Occupancy v7 is not
  current. component-manifest leftover-join.v6 remains the
  current DR-103 leftover-join. component-manifest leftover-join.v3
  is not current. Remainder of G15 execution remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent an adapter. Does not
  invent a D9 code. Does not invent a section 7.1 recipe.
  Does not steal OBL-WINDOWS-PATH, OBL-ENVELOPE-MISMATCH,
  OBL-UNICODE-NORM, OBL-OD-1, or OBL-OD-2. Does not occupy
  the identifier. Does not SATISFY DR-120. Does not SATISFY
  DR-103. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Naming parent of G15 is naming v6 (D-145), not
  leftover-join.v4. D-086 named DR-G15. Claude Stage A
  leftover-join.v4 returned no observationsNotFindings field
  and an empty advisories list. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. This entry does not invent
  identifiers. It does not claim that both reviewers'
  identifiers are preserved. Claude Stage A returned no
  observation identifiers. Codex Stage A returned no
  observation identifiers. Claude Stage B returned three
  unlabeled observationsNotFindings strings. They carry no
  identifiers. Codex Stage B returned zero advisories and no
  observations. This entry does not invent identifiers.
  Claude Stage B returned no observation identifiers. Codex
  Stage B returned no observation identifiers. Does not
  execute G15. Does not rewrite occupancy v9. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D266. Does not unwrite D-086, D-180, D-214,
  or D-265.
- **Commit:** C-D266.

## D-267 — Record sdk leftover-join.v6 as DR-125 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-267.review-adversarial.claude2.json`,
  `bd53c2955755d04bf4760a58789622b0cc21eb2256921ada087deaad313c0674`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-267.review-adversarial.codex.json`,
  `e6b8746b8181b6d23724cf55ef9204761c2bc6948e34c036e8e59ef2879411c2`)
  CONSENT. Subject `coordinator-decisions.D-267.draft.md`
  `1021ab2b57d82fb9f035f89dc3646d83c563ec2df25855ad490863d548872935`.
  Frozen leftover-join
  `sdk-leftover-join.v6.json`
  `e91d6e926830833d563bb89f3693d65328173af6f0d42275ad5339ef73880341`
  Stage A Claude ACCEPT
  `92a4ba004ab4fde2ea6f361546854ba51ed725b858628b07bb12c1d78ae00975`
  0/0; Stage A Codex ACCEPT
  `9c3e3b2a6e9214b6509f74852d4b9fbaeb53af99569f5549c7ac46d705decf0c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `sdk-leftover-join.v6.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/sdk-leftover-join.v6.json`
  `e91d6e926830833d563bb89f3693d65328173af6f0d42275ad5339ef73880341`.
- **Decision:** Record v6 as DR-125 leftover remasurement after
  D-266. The candidate binds NOTHING. DR-125 stays `OPEN`.
  leftover-design of OBL-G20-FX-AUTHORING and
  OBL-SDK-API-RESERVED remains on leftover-join.v6.
  leftover-join.v5 remains current at draft time. After this
  successor is recorded, leftover-join.v5 is not current.
  Occupancy v2 is the current G20 occupancy remasurement.
  Occupancy v1 is not current. leftover-join.v4 is not
  current. Remainder of G20 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture
  bytes. Does not invent reserved SDK APIs. Does not invent
  a D9 code. Does not invent a section 7.1 recipe. Does not
  steal OBL-SDK-API-RESERVED. Does not close
  OBL-DR125-ACTIVATION. Does not occupy the identifier. Does
  not SATISFY DR-125. Does not SATISFY DR-117. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-114. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Naming parent of G20 is naming v6 (D-145),
  not leftover-join.v6. D-086 named DR-G20. Claude Stage A
  leftover-join.v6 returned one named observation
  CLAUDE-SDKLJ-V6-O1. No change requested. It carries that
  identifier. No observationsNotFindings field. No advisories
  field. Codex Stage A leftover-join.v6 returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry names CLAUDE-SDKLJ-V6-O1.
  It does not invent a Codex identifier. It does not claim
  that both reviewers' identifiers are preserved. Codex
  Stage A returned no observation identifiers.
  CLAUDE-G20CAT-V1-SF1 and CLAUDE-PTLJ-V3-SF1 already landed
  in this lineage at leftover-join.v5. This entry does not
  re-land them. Claude Stage B returned one named
  observation CLAUDE-D267-B-O1. No change requested. It
  carries that identifier. No observationsNotFindings field.
  No advisories field. Codex Stage B returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry names CLAUDE-D267-B-O1.
  It does not invent a Codex identifier. Codex Stage B
  returned no observation identifiers. Does not execute G20.
  Does not rewrite occupancy v2. Does not edit file 08. Does
  not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D267. Does not unwrite D-086, D-184, D-217,
  or D-266.
- **Commit:** C-D267.

## D-268 — Record platform-tcb leftover-join.v9 as DR-126 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 2 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-268.turn2.review-adversarial.claude2.json`,
  `69213516ca7f67d4e1a64b4ebac30bbb3280c459487f03a99e0cd846a206bce4`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-268.turn2.review-adversarial.codex.json`,
  `57dfae06d937a1fdc0151193eae0826bf14dc37845064b59778f9a13f83ae75e`)
  CONSENT. Subject `coordinator-decisions.D-268.turn2.draft.md`
  `b294220e2a5594682b72ebf7542376f74739e86424eacdbd82d18dfcf7d4ca0e`.
  Turn 1 subject `coordinator-decisions.D-268.draft.md`
  `d0bb29ed759b32f2565f6d87ff74b96aef2b0cc532627190330d37d91c1e0350`
  Dual OBJECT CLAUDE-D268-B-SF1 / CODEX-D268-SF1. Frozen leftover-join
  `platform-tcb-leftover-join.v9.json`
  `1774427e9500940d24f75fbaee622142a8be72547d68a026e18d6e957369e26a`
  Stage A Claude ACCEPT
  `408c6fde1428ea3c7e5ed88ea345882e996c3784b7fe2e48d249f92463be1251`
  0/0; Stage A Codex ACCEPT
  `1383c328558062138ce5c3b090afc468d1e8d2a93e8e8cd32c7db90a4f81d078`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `platform-tcb-leftover-join.v9.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/platform-tcb-leftover-join.v9.json`
  `1774427e9500940d24f75fbaee622142a8be72547d68a026e18d6e957369e26a`.
- **Decision:** Record v9 as DR-126 leftover remasurement after
  D-267. The candidate binds NOTHING. DR-126 stays `OPEN`.
  leftover-design of OBL-G22-FX-AUTHORING and
  OBL-RESERVED-TABLES remains on leftover-join.v9.
  leftover-join.v6 remains current at draft time. After this
  successor is recorded, leftover-join.v6 is not current.
  Occupancy v2 is the current G22 occupancy remasurement.
  Occupancy v1 is not current. leftover-join.v7 is not
  current. leftover-join.v8 is not current. Remainder of G22
  execution remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not populate
  reserved TCB tables. Does not invent Rosetta. Does not
  apply TCB v45. Does not invent a D9 code. Does not invent
  a section 7.1 recipe. Does not steal OBL-RESERVED-TABLES.
  Does not occupy the identifier. Does not SATISFY DR-126.
  Does not SATISFY DR-117. Does not SATISFY DR-131. Does not
  SATISFY DR-133. Does not SATISFY DR-114. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent of G22 is naming v6 (D-145), not leftover-join.v9.
  D-086 named DR-G22. Claude Stage A leftover-join.v9
  returned four unlabeled observationsNotFindings strings.
  They carry no identifiers. No advisories field. Codex
  Stage A leftover-join.v9 returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage A returned no observation
  identifiers. Codex Stage A returned no observation
  identifiers. CLAUDE-PTLJ-V3-SF1 already landed in this
  lineage at leftover-join.v5. This entry does not re-land
  it. CLAUDE-PTLJ-V7-SF1 already landed in this lineage at
  leftover-join.v8. This entry does not re-land it.
  leftover-join.v9 lands CLAUDE-PTLJ-V8-SF1 and
  CODEX-PTLJ-V8-SF1 (same class: predecessorV6.role leftover
  this-v7 speaker). Both identifiers are named. Turn 1 Dual
  OBJECT CLAUDE-D268-B-SF1 / CODEX-D268-SF1 (same class:
  Measured-inputs leftover-join.v8 label said split Dual
  REJECT; leftover-join.v8 is Dual REJECT, not split). This
  turn 2 lands both identifiers. Claude Stage B turn 2
  returned one unlabeled advisory object (site paired with
  note and whyNotCharged). It carries no identifier. Codex
  Stage B turn 2 returned zero advisories and no
  observations. This entry does not invent identifiers.
  Claude Stage B returned no observation identifiers. Codex
  Stage B returned no observation identifiers. Does not
  execute G22. Does not rewrite occupancy v2. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D268. Does not unwrite D-086, D-185, D-219,
  or D-267.
- **Commit:** C-D268.

## D-269 — Record g20 leftover-join.v6 as G20 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-269.review-adversarial.claude2.json`,
  `f40843eb21324ebab6b8e16512576c9ec9473b0148cdb68bc30f068f1e5d2297`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-269.review-adversarial.codex.json`,
  `df303500c88774feee431b00893b6bda98ecf727404d97722b09641f96afb7c6`)
  CONSENT. Subject `coordinator-decisions.D-269.draft.md`
  `9320ebe74620c9ab943d60a895219d0b2b56af3b5b3cfaecea53a45249c8df64`.
  Frozen leftover-join
  `g20-leftover-join.v6.json`
  `d666a4492ef3c598b53606fff453cb14a968822b9c29b25b0b535ebde01b2d97`
  Stage A Claude ACCEPT
  `053a2813b6dfb618a78f9e719455192ed9b0b53bd093a0bcbe1c9836a8b7768a`
  0/0; Stage A Codex ACCEPT
  `d7c8e3929f77358a4f6b6828b19f31a066ec74764f21f5299c1a1f8a79e03451`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g20-leftover-join.v6.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g20-leftover-join.v6.json`
  `d666a4492ef3c598b53606fff453cb14a968822b9c29b25b0b535ebde01b2d97`.
- **Decision:** Record v6 as G20 leftover remasurement after
  D-268. The candidate binds NOTHING. DR-G20 stays `OPEN`.
  leftover-design of OBL-G20-FX-AUTHORING remains on
  leftover-join.v6. leftover-join.v4 remains current at
  draft time. After this successor is recorded,
  leftover-join.v4 is not current. leftover-join.v5 is
  CANDIDATE-NOT-APPLIED (Dual REJECT MUST-FIX-1 /
  SHOULD-FIX-1 / CODEX-G20LJ-V5-SF1) and is not current.
  leftover-join.v5 is not Dual ACCEPT. Occupancy v2 is the
  current G20 occupancy remasurement. Occupancy v1 is not
  current. sdk leftover-join.v6 remains the current DR-125
  leftover-join. sdk leftover-join.v5 is not current.
  Remainder of G20 execution remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent fixture bytes.
  Does not invent reserved SDK APIs. Does not invent a D9
  code. Does not invent a section 7.1 recipe. Does not steal
  OBL-SDK-API-RESERVED. Does not close OBL-DR125-ACTIVATION.
  Does not occupy the identifier. Does not SATISFY DR-125.
  Does not SATISFY DR-117. Does not SATISFY DR-131. Does not
  SATISFY DR-133. Does not SATISFY DR-114. Does not SATISFY
  DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent is naming v6 (D-145), not leftover-join.v6. D-086
  named the identifier. Claude Stage A leftover-join.v6
  returned four named advisories ADV-1, ADV-2, ADV-3, and
  ADV-4. No change requested. They carry those identifiers.
  No observationsNotFindings field. Codex Stage A leftover-join.v6
  returned an empty observationsNotFindings list, zero
  advisories, and no observations. This entry names those
  Claude identifiers. It does not invent a Codex identifier.
  It does not claim that both reviewers' identifiers are
  preserved. Codex Stage A returned no observation
  identifiers. leftover-join.v6 lands MUST-FIX-1,
  SHOULD-FIX-1, and CODEX-G20LJ-V5-SF1. MUST-FIX-1 and
  CODEX-G20LJ-V5-SF1 are the same class. All three
  identifiers are named. Claude Stage B returned two
  unlabeled observationsNotFindings strings. They carry no
  identifiers. Zero advisories. Codex Stage B returned an
  empty observationsNotFindings list, an empty observations
  list, and zero advisories. This entry does not invent
  identifiers. It does not claim that both reviewers'
  identifiers are preserved. Claude Stage B returned no
  observation identifiers. Codex Stage B returned no
  observation identifiers. Does not execute G20. Does not
  rewrite occupancy v2. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D269. Does not unwrite D-086, D-217, D-264,
  or D-268.
- **Commit:** C-D269.

## D-270 — Record g15 leftover-join.v5 as G15 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-270.review-adversarial.claude2.json`,
  `ec2a52555d11b6b934499923519a990e3b26e140f1c3e20f9d1cbd219e2cf0a2`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-270.review-adversarial.codex.json`,
  `6aedc6fb3c155f8152e95e11b11e3923266e21d44f59a9016304fdc92a5b010e`)
  CONSENT. Subject `coordinator-decisions.D-270.draft.md`
  `6d02fac5bea8cbcef196f9f73afa09d6183060838814f100896130d96621efda`.
  Frozen leftover-join
  `g15-leftover-join.v5.json`
  `cc457032e866c578d117bf03fd45a964ec4ae4923af0030aad3ca876a2253e6e`
  Stage A Claude ACCEPT
  `71820eb4df3f7a468543e61765afa4bb4a87bf865bd4f33cdd68d5e000307ce0`
  0/0; Stage A Codex ACCEPT
  `4d7a30933ab5192f6d890235a44ff56bdd9ccdb6075b405378d9f4c1806cb696`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g15-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g15-leftover-join.v5.json`
  `cc457032e866c578d117bf03fd45a964ec4ae4923af0030aad3ca876a2253e6e`.
- **Decision:** Record v5 as G15 leftover remasurement after
  D-269. The candidate binds NOTHING. DR-G15 stays `OPEN`.
  leftover-design of OBL-AT-FX-AUTHORING remains on
  leftover-join.v5. leftover-join.v4 remains current at
  draft time. After this successor is recorded,
  leftover-join.v4 is not current. leftover-join.v3 is not
  current. Occupancy v9 is the current G15 occupancy
  remasurement. Occupancy v7 is not current. packaging leftover-join.v4
  remains the current DR-120 leftover-join. packaging leftover-join.v3
  is not current. component-manifest leftover-join.v6 remains
  the current DR-103 leftover-join. Remainder of G15 execution
  remains qualification (D-056). Does not pin QUALIFIED. Does
  not invent fixture bytes. Does not invent an adapter
  implementation. Does not invent a numeric threshold. Does
  not invent an envelope. Does not invent a D9 code. Does
  not invent a section 7.1 recipe. Does not steal
  OBL-ADAPTER-IMPL, OBL-WINDOWS-PATH, OBL-ENVELOPE-MISMATCH,
  OBL-UNICODE-NORM, OBL-OD-1, or OBL-OD-2. Does not occupy
  the identifier. Does not SATISFY DR-120. Does not SATISFY
  DR-103. Does not SATISFY DR-117. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent is naming v6 (D-145), not leftover-join.v5. D-086
  named the identifier. Claude Stage A leftover-join.v5
  returned three unlabeled observationsNotFindings strings.
  They carry no identifiers. No advisories field. Codex Stage A
  leftover-join.v5 returned an empty observationsNotFindings
  list, zero advisories, and no observations. This entry recites
  those Claude observations as strings. It does not invent a
  Claude identifier. It does not invent a Codex identifier.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage A returned no observation
  identifiers. Codex Stage A returned no observation
  identifiers. Claude Stage B returned three unlabeled
  observationsNotFindings strings. They carry no identifiers.
  Zero advisories. Codex Stage B returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G15. Does not rewrite occupancy
  v9. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D270. Does not unwrite D-086, D-214, D-261,
  D-266, or D-269.
- **Commit:** C-D270.

## D-271 — Record g22 leftover-join.v5 as G22 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-271.review-adversarial.claude2.json`,
  `50b032b154a85b807cfc5b507702502a718816dc40bccdf38912d48f56ce234b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-271.review-adversarial.codex.json`,
  `b6650735bfba4899e567ebecb62121c0bb1fb55f140e31542485d68626a12efa`)
  CONSENT. Subject `coordinator-decisions.D-271.draft.md`
  `28c85c38b47e3dd8d475cdcb7d979f780edbcec22bf544df9a7d1c7d4d85f613`.
  Frozen leftover-join
  `g22-leftover-join.v5.json`
  `70e0efd68e9003d7828c93e2d7d26dad81664adebfcb1c8d38b006c80e620d3f`
  Stage A Claude ACCEPT
  `1879de4fa51ef72f44c07e8e31337c2954ffa1d200091cfd374d1f5345e98551`
  0/0; Stage A Codex ACCEPT
  `35454c10cbcd5097afbc1f9a49ffaedc0ae7f518ec2f106b0b34e993be4224bb`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g22-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g22-leftover-join.v5.json`
  `70e0efd68e9003d7828c93e2d7d26dad81664adebfcb1c8d38b006c80e620d3f`.
- **Decision:** Record v5 as G22 leftover remasurement after
  D-270. The candidate binds NOTHING. DR-G22 stays `OPEN`.
  leftover-design of OBL-G22-FX-AUTHORING remains on
  leftover-join.v5. leftover-join.v4 remains current at
  draft time. After this successor is recorded,
  leftover-join.v4 is not current. leftover-join.v3 is not
  current. Occupancy v2 is the current G22 occupancy
  remasurement. Occupancy v1 is not current. platform-tcb leftover-join.v9
  remains the current DR-126 leftover-join. platform-tcb leftover-join.v6
  is not current. Remainder of G22 execution remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not populate reserved TCB
  tables. Does not invent Rosetta. Does not invent a D9
  code. Does not invent a section 7.1 recipe. Does not steal
  OBL-RESERVED-TABLES. Does not apply TCB v45. Does not occupy
  the identifier. Does not SATISFY DR-126. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Does not SATISFY DR-114. Does not SATISFY DR-101. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent is naming v6
  (D-145), not leftover-join.v5. D-086 named the identifier.
  Claude Stage A leftover-join.v5 returned four unlabeled
  observationsNotFindings strings. They carry no identifiers.
  No advisories field. Codex Stage A leftover-join.v5 returned
  an empty observationsNotFindings list, zero advisories, and
  no observations. This entry recites those Claude observations
  as strings. It does not invent a Claude identifier. It does
  not invent a Codex identifier. It does not claim that both
  reviewers' identifiers are preserved. Claude Stage A returned
  no observation identifiers. Codex Stage A returned no
  observation identifiers. Claude Stage B returned four
  unlabeled observationsNotFindings strings. They carry no
  identifiers. Zero advisories. Codex Stage B returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G22. Does not rewrite occupancy
  v2. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D271. Does not unwrite D-086, D-219, D-265,
  D-268, or D-270.
- **Commit:** C-D271.

## D-272 — Record language-quality leftover-join.v5 as DR-118 leftover remasurement (CONTESTED)

- **Date:** 2026-08-24
- **Status:** **CONTESTED** after three turns under D-000 clause 2.
  Not adopted. No forced consensus. Parked. Successor drafts are
  a **new** cycle, not a fourth turn of this one. Turn 1 split.
  Claude CONSENT 0/0
  (`artifacts/coordinator-decisions.D-272.review-adversarial.claude2.json`,
  `7abe90763627cc3682f855d48c1d71263bb6456303590d4da40433abffd7d04a`)
  four unlabeled observationsNotFindings strings. Codex OBJECT
  0/1 CODEX-D272-SF1
  (`artifacts/coordinator-decisions.D-272.review-adversarial.codex.json`,
  `c1706699ac9ec613cb725eb559823d517a316f8e6946ba34e0d3ec2242057710`).
  Not Dual CONSENT. Not Dual REJECT. Turn 2 Dual OBJECT. Claude
  OBJECT 2/2 MF-1 / MF-2 / SF-1 / SF-2
  (`artifacts/coordinator-decisions.D-272.turn2.review-adversarial.claude2.json`,
  `6336fe44ae0d18fbd149092fddc7df0dd9dc317cf0937ba6fff130bbe71d4051`).
  Codex OBJECT 0/1 CODEX-D272-T2-SF1
  (`artifacts/coordinator-decisions.D-272.turn2.review-adversarial.codex.json`,
  `3932afc992dc38cbf5fc8657369d453ce9301e6bbc2e2befe892b6717c8bd741`).
  Same class as SF-1. Turn 3 Dual OBJECT. Claude OBJECT 1/3
  MF-1 / SF-1 / SF-2 / SF-3
  (`artifacts/coordinator-decisions.D-272.turn3.review-adversarial.claude2.json`,
  `7638af9ea9a664c6d3eb396db8fb4da932d138bb8dbf7e189604d622c25c5154`).
  Codex OBJECT 1/1 CODEX-D272-T3-MF1 / CODEX-D272-T3-SF1
  (`artifacts/coordinator-decisions.D-272.turn3.review-adversarial.codex.json`,
  `032b5907136b3357f7025f9064ff03f79bbe6ee9ad073b25331b3218a1a852eb`).
  CODEX-D272-T3-MF1 same class as Claude turn-3 MF-1.
  CODEX-D272-T3-SF1 same class as Claude turn-3 SF-1 / SF-2.
  A fourth exchange was dispatched as
  `coordinator-decisions.D-272.turn4.draft.md`
  `802ca3ec7efcb11c90475dfadd6230778b362daa8d94da68d9e1bec5e6a6c665`
  and Dual OBJECT Claude MF-1 / SF-1 / SF-2
  (`artifacts/coordinator-decisions.D-272.turn4.review-adversarial.claude2.json`,
  `4110cae842bac61d00448655e7f04fbfc2eb63c48fd2c73290bd9fb305795899`)
  and Codex CODEX-D272-T4-MF1 / CODEX-D272-T4-MF2 / CODEX-D272-T4-SF1
  (`artifacts/coordinator-decisions.D-272.turn4.review-adversarial.codex.json`,
  `982397057a394642bc7391df5951eb8839c57230359ac92e11750e771778509e`).
  Claude MF-1 and CODEX-D272-T4-MF1 are the same class: D-000
  clause 2 forbids a fourth turn. That exchange is not D-000
  consensus and is not this cycle's terminal merits review.
  Terminal merits review is turn 3 Dual OBJECT.
- **Decision type:** RULE-GOVERNED. Not adopted.
- **Subject drafts:**
  - turn 1 `coordinator-decisions.D-272.turn1.draft.md`
    `aa66e2cc7d673e5e62c9d7cf59fcd0396871f1ca85d35c35e2a6549a7f96ed68`
  - turn 2 `coordinator-decisions.D-272.draft.md`
    `14cc56ada3a3bfab67a021f3e977b9000d47a2536a641b48741b25e979bd6f2a`
  - turn 3 `coordinator-decisions.D-272.turn3.draft.md`
    `c7d0ec6b9f2e55daa110470e4209a0f7a8edc76aa50d8a4a09b6bff52ee5482b`
- **Frozen leftover-join under review:**
  `language-quality-leftover-join.v5.json`
  `e12101736f9a320a06a3311f405981801fad73c42ba9b7537f506e6c4859bd53`
  Stage A Dual ACCEPT 0/0. leftoverDesign remains
  `[OBL-THRESHOLDS, OBL-MATRIX-CORPUS, OBL-G13-RESERVED]`.
  CANDIDATE-NOT-APPLIED. Not recorded as current. leftover-join.v3
  remains the current recorded DR-118 leftover-join (D-206).
  leftover-join.v4 Dual REJECT is not current.
- **Decision:** None. DR-118 stays `DECIDED-V1-NOT-INTEGRATED`.
  leftover-join.v5 is not recorded as current. A later new cycle
  (not turn 4 of this cycle) may retry. Does not SATISFY DR-118.
  Does not flatten `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does
  not edit file 08. Does not authorize `docs/v2/implementation/`.
- **Both positions (required by D-000 clause 2):**
  - **Coordinator:** leftover-join.v5 Stage A Dual ACCEPT 0/0
    remasures leftover-join.v3 after sdk leftover-join.v6 (D-267)
    and lands leftover-join.v4 Dual REJECT. COORD Stage B failed
    on observation-field custody, then on missing prior-turn
    Stage B tables, then on D-000 clause 2. The destination act
    remains a later new-cycle leftover remasurement of DR-118.
  - **Reviewers:** Turn 3 Dual OBJECT. Turn 4 Dual OBJECT on
    D-000 clause 2: after three exchanges without consensus the
    decision is CONTESTED, parked, and not a fourth turn.
- **What proceeds:** work continues on other leftover remasurement
  surfaces and on a successor new cycle. This contest does not
  authorize `docs/v2/implementation/` or move any file 08 status
  cell. Gate 1 Class A is not opened.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays 5 of 32.
  Condition 4 stays MET on the naming half (28 of 28). Condition 5
  last.
- **Reversibility:** n/a (not adopted). Overturn: n/a. Does not
  unwrite D-007, D-165, D-206, D-267, or D-271.
- **Commit:** C-D272.

## D-273 — Record language-quality leftover-join.v5 as DR-118 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-273.review-adversarial.claude2.json`,
  `b6a6d2d7fb714e7a2fbcdb7738127207100088866d178ca6c27abd76275da3a5`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-273.review-adversarial.codex.json`,
  `b201f62dbdb68c3ea9d93544fb6a22dc4df606328acc6cf149f16801580d2a57`)
  CONSENT. Subject `coordinator-decisions.D-273.draft.md`
  `6a134f700b2316ebf7fa85dbc8237f6cf87d95bdfc686bd8edc7749236422218`.
  Frozen leftover-join
  `language-quality-leftover-join.v5.json`
  `e12101736f9a320a06a3311f405981801fad73c42ba9b7537f506e6c4859bd53`
  Stage A Claude ACCEPT
  `f1dc8c40908004e94533b31f3e73855e97de97642d9e39de269ac3bf44e00839`
  0/0; Stage A Codex ACCEPT
  `eae8cdc30aecfde435f668af382f5aa9df5bdbacff15ca23ba12cf718adeed49`
  0/0. New cycle after CONTESTED D-272. Not a fourth turn.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-quality-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271. D-272 is CONTESTED and is not
  on this no-cell-edit adoption branch. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/language-quality-leftover-join.v5.json`
  `e12101736f9a320a06a3311f405981801fad73c42ba9b7537f506e6c4859bd53`.
- **Decision:** Record v5 as DR-118 leftover remasurement after
  CONTESTED D-272. The candidate binds NOTHING. DR-118 stays
  `DECIDED-V1-NOT-INTEGRATED`. leftover-design of
  OBL-THRESHOLDS, OBL-MATRIX-CORPUS, and OBL-G13-RESERVED
  remains on leftover-join.v5. leftover-join.v3 remains current
  at draft time. After this successor is recorded,
  leftover-join.v3 is not current. leftover-join.v4 is Dual
  REJECT CANDIDATE-NOT-APPLIED and is not current. Occupancy
  is not this join's specification. sdk leftover-join.v6
  remains the current DR-125 leftover-join. sdk leftover-join.v5
  is not current. Does not pin QUALIFIED. Does not invent
  per-row numeric thresholds. Does not author the matrix or
  corpus. Does not steal OBL-SDK-API-RESERVED. Does not name
  G13 into required-now. Does not SATISFY DR-118. Does not
  SATISFY DR-125. Does not SATISFY DR-117. Does not SATISFY
  DR-131. Does not SATISFY DR-133. Does not SATISFY DR-114.
  Does not SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is
  zero. Claude Stage A leftover-join.v5 returned three named
  observations CLAUDE-LQLJ-V5-O1, CLAUDE-LQLJ-V5-O2, and
  CLAUDE-LQLJ-V5-O3. No change requested. They carry those
  identifiers. They are objects (id paired with text). No
  observationsNotFindings field. No advisories field. Codex
  Stage A leftover-join.v5 returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim
  that both reviewers' identifiers are preserved. leftover-join.v5
  lands CLAUDE-LQLJ-V4-SF1 and CODEX-LQLJ-V4-SF1. Both
  identifiers are named. CLAUDE-LQLJ-V1-SF1 and LQLJ-V1-SF1
  already landed in this lineage at leftover-join.v2.
  leftover-join.v3 carried that repair forward. This entry
  does not re-land them. Claude Stage B returned four
  unlabeled observationsNotFindings strings. They carry no
  identifiers. Zero advisories. Codex Stage B returned an
  empty observationsNotFindings list, no observations field,
  and zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not treat D-272 as adopted. Does not
  edit file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D273. Does not unwrite D-007, D-113, D-165,
  D-206, D-267, D-271, or D-272.
- **Commit:** C-D273.

## D-274 — Record language-runtime leftover-join.v7 as G14 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-274.review-adversarial.claude2.json`,
  `ed52a683665e3a3604e7d0cf70e51a7c1a26742863c17b6ff797b45013dfca97`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-274.review-adversarial.codex.json`,
  `a266c1d9fab2951cb80a32f211992d8830a6996578da6a70fa7f1d4bdee78241`)
  CONSENT. Subject `coordinator-decisions.D-274.draft.md`
  `1ecebca1c16aca18254ed94ee1d44fd296cbf3a37837cd3033770c79b252b644`.
  Frozen leftover-join
  `language-runtime-leftover-join.v7.json`
  `90e29696f0b3ed2b23c3a5f1d7c089d54aef6887e6f3a8d9d9dfe988282fb4e3`
  Stage A Claude ACCEPT
  `01679e15c042b60bdec97fdae24bbc62501dec7aa0b3d022782498ae57ac9337`
  0/0; Stage A Codex ACCEPT
  `d4c47262880facfcec5f600e84e58700574567c9712e1969b56ebd40823c8698`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `language-runtime-leftover-join.v7.json` (0 blockers,
  0 SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273. D-272 is CONTESTED
  and is not on this no-cell-edit adoption branch. Not a
  three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/language-runtime-leftover-join.v7.json`
  `90e29696f0b3ed2b23c3a5f1d7c089d54aef6887e6f3a8d9d9dfe988282fb4e3`.
- **Decision:** Record leftover-join.v7 as G14 leftover
  remasurement after D-273. The candidate binds NOTHING.
  DR-G14 stays `OPEN`. leftover-design of
  OBL-G14-FX-AUTHORING remains on leftover-join.v7.
  leftover-join.v5 remains current at draft time. After this
  successor is recorded, leftover-join.v5 is not current.
  leftover-join.v6 is CANDIDATE-NOT-APPLIED (Split Claude
  REJECT CLAUDE-LRLJ-V6-SF1 / Codex ACCEPT 0/0) and is not
  current. leftover-join.v6 is not Dual ACCEPT.
  leftover-join.v6 is not Dual REJECT. Occupancy v4 is the
  current G14 occupancy remasurement. Occupancy v1 is not
  recorded as current occupancy. language-quality leftover-join.v5
  remains the current DR-118 leftover-join.
  language-quality leftover-join.v3 is not recorded as
  current DR-118 leftover-join. language-quality leftover-join.v4
  is Dual REJECT CANDIDATE-NOT-APPLIED and is not current.
  Remainder of G14 execution remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent fixture bytes. Does
  not invent a D9 code. Does not invent a section 7.1 recipe.
  Does not invent a numeric threshold. Does not mint
  Rust-as-core. Does not steal OBL-THRESHOLDS,
  OBL-MATRIX-CORPUS, or OBL-G13-RESERVED. Does not name G13
  into required-now. Does not occupy the identifier. Does not
  SATISFY DR-118. Does not reopen DR-119 SATISFIED. Does not
  SATISFY DR-117. Does not SATISFY DR-131. Does not SATISFY
  DR-133. Does not SATISFY DR-114. Does not SATISFY DR-101.
  Does not flatten DR-118 `DECIDED-V1-NOT-INTEGRATED` to
  `OPEN`. Does not flatten DR-107 `PROPOSED-CLOSED-FOR-REVIEW`
  to `OPEN`. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming
  parent is naming v6 (D-145), not leftover-join.v7. D-086
  named the identifier. Claude Stage A leftover-join.v7
  returned four named observations CLAUDE-LRLJ-V7-O1,
  CLAUDE-LRLJ-V7-O2, CLAUDE-LRLJ-V7-O3, and CLAUDE-LRLJ-V7-O4.
  No change requested. They carry those identifiers. They
  are objects (id paired with text). No
  observationsNotFindings field. No advisories field. Codex
  Stage A leftover-join.v7 returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim
  that both reviewers' identifiers are preserved. Codex
  Stage A returned no observation identifiers.
  leftover-join.v7 lands CLAUDE-LRLJ-V6-SF1. CLAUDE-LRLJ-V1-SF1
  already landed in this lineage at leftover-join.v2.
  leftover-join.v4 and leftover-join.v5 carried the repair
  forward. This entry does not re-land CLAUDE-LRLJ-V1-SF1.
  basedOn.d273.role is last-heading custody only. Claude
  Stage B returned no observations field, no
  observationsNotFindings field, and no advisories field.
  Codex Stage B returned an empty observationsNotFindings
  list, no observations field, and zero advisories. This
  entry does not invent identifiers. It does not claim that
  both reviewers' identifiers are preserved. Claude Stage B
  returned no observation identifiers. Codex Stage B returned
  no observation identifiers. Does not execute G14. Does not
  rewrite occupancy v4. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D274. Does not unwrite D-086, D-179, D-213,
  D-260, or D-273.
- **Commit:** C-D274.

## D-275 — Record lifecycle leftover-join.v4 as DR-107 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-275.review-adversarial.claude2.json`,
  `92069f9cabcc03826f70ac96e3bb421a29e0502b6c5bb991ddbed30623bf310e`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-275.review-adversarial.codex.json`,
  `fd13f4a23f4827101e8c75b3eda57d344ceac182b08df119eba6dd0ec4be1275`)
  CONSENT. Subject `coordinator-decisions.D-275.draft.md`
  `85c07ba502a9d01bc21dd74d3604c953eaea4b0e48e875f97123d7d6ad173e22`.
  Frozen leftover-join
  `lifecycle-leftover-join.v4.json`
  `bcc76ee3d99c88c258496dcc5591682d4ad655e06049b802a383ba03d3f1ddfb`
  Stage A Claude ACCEPT
  `4d99ba4d68627c873b78bb90bcbd3602b90968b3101c0225315b51e9137727df`
  0/0; Stage A Codex ACCEPT
  `9999384a82a233c20dd95aa8619b7f8a8b4a49fe9ad212b87ac61b44fac0b4e6`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `lifecycle-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274. D-272 is
  CONTESTED and is not on this no-cell-edit adoption
  branch. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/lifecycle-leftover-join.v4.json`
  `bcc76ee3d99c88c258496dcc5591682d4ad655e06049b802a383ba03d3f1ddfb`.
- **Decision:** Record leftover-join.v4 as DR-107 leftover
  remasurement after D-274. The candidate binds NOTHING.
  DR-107 stays `PROPOSED-CLOSED-FOR-REVIEW`. leftover-design of
  OBL-G18-FX-AUTHORING and OBL-ENCODING-RESERVED remains on
  leftover-join.v4. leftover-join.v3 remains current at draft
  time. After this successor is recorded, leftover-join.v3 is
  not current. Occupancy v4 is the current G18 occupancy
  remasurement. Occupancy v2 is not recorded as current
  occupancy. g18 leftover-join.v5 remains the current G18
  GATE leftover-join. Remainder of G18 execution remains
  qualification (D-056). Does not pin QUALIFIED. Does not
  invent fixture bytes. Does not invent a journal. Does not
  invent a D9 code. Does not invent a section 7.1 recipe.
  Does not steal OBL-G18-FX-AUTHORING as a GATE closure. Does
  not occupy the identifier. Does not SATISFY DR-107. Does
  not flatten DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`.
  Does not flatten DR-118 `DECIDED-V1-NOT-INTEGRATED` to
  `OPEN`. Does not reopen DR-119 SATISFIED. Does not SATISFY
  DR-117. Does not SATISFY DR-131. Does not SATISFY DR-133.
  Does not SATISFY DR-114. Does not SATISFY DR-101. Gate 1
  Class A is not opened. Not SATISFIED. Required-now stays
  28. Condition-4 effect is zero. Naming parent of G18 is
  naming v6 (D-145), not leftover-join.v4. D-086 named
  DR-G18. Claude Stage A leftover-join.v4 returned three
  unlabeled observationsNotFindings strings. They carry no
  identifiers. No observations field. No advisories field.
  Codex Stage A leftover-join.v4 returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry recites those Claude
  observations as strings. It does not invent a Claude
  identifier. It does not invent a Codex identifier. It does
  not claim that both reviewers' identifiers are preserved.
  Claude Stage A returned no observation identifiers. Codex
  Stage A returned no observation identifiers. leftover-join.v4
  lands no new finding identifier. basedOn.d274.role is
  last-heading custody only. Claude Stage B returned three
  unlabeled observationsNotFindings strings. They carry no
  identifiers. No observations field. No advisories field.
  Codex Stage B returned an empty observationsNotFindings
  list, no observations field, and zero advisories. This
  entry does not invent identifiers. It does not claim that
  both reviewers' identifiers are preserved. Claude Stage B
  returned no observation identifiers. Codex Stage B returned
  no observation identifiers. Does not execute G18. Does not
  rewrite occupancy v4. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D275. Does not unwrite D-086, D-176, D-216,
  D-263, or D-274.
- **Commit:** C-D275.

## D-276 — Record g18 leftover-join.v6 as G18 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-276.review-adversarial.claude2.json`,
  `050377590e3bfa7f0020aaac1d70778b155838f0b45543a4f09a5ea41c08247a`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-276.review-adversarial.codex.json`,
  `666b8b0672ff0a3b9e5c18cf36bc5542c90236826471cfb7f7ca6b2fbe680dbe`)
  CONSENT. Subject `coordinator-decisions.D-276.draft.md`
  `110a5d58b31cc3674f51ddc8307877d53cb8b4d7eb76a379b017c81aa3b94530`.
  Frozen leftover-join
  `g18-leftover-join.v6.json`
  `f531ba6a952c8c55733454c19e46ac388f0eec4d31f3b5d29bfe04fbdeaac66e`
  Stage A Claude ACCEPT
  `43ca6cfca11993b199212bb72899c663427dbcb2f0fcd1e129922a880c46c262`
  0/0; Stage A Codex ACCEPT
  `ada654ad26b930146dd0c283796617ef3c92b37cc642e6880ec2d62bd67243d9`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g18-leftover-join.v6.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275.
  D-272 is CONTESTED and is not on this no-cell-edit adoption
  branch. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g18-leftover-join.v6.json`
  `f531ba6a952c8c55733454c19e46ac388f0eec4d31f3b5d29bfe04fbdeaac66e`.
- **Decision:** Record leftover-join.v6 as G18 leftover
  remasurement after D-275. The candidate binds NOTHING.
  DR-G18 stays `OPEN`. leftover-design of OBL-G18-FX-AUTHORING
  remains on leftover-join.v6. leftover-join.v5 remains current
  at draft time. After this successor is recorded,
  leftover-join.v5 is not current. Occupancy v4 is the current
  G18 occupancy remasurement. Occupancy v2 is not recorded as
  current occupancy. lifecycle leftover-join.v4 remains the
  current DR-107 leftover-join. lifecycle leftover-join.v3 is
  not recorded as current DR-107 leftover-join. Remainder of
  G18 execution remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not invent a
  journal. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not steal OBL-ENCODING-RESERVED.
  Does not occupy the identifier. Does not SATISFY DR-107.
  Does not flatten DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to
  `OPEN`. Does not flatten DR-118 `DECIDED-V1-NOT-INTEGRATED`
  to `OPEN`. Does not import DR-107 `PROPOSED-CLOSED-FOR-REVIEW`
  onto DR-G18. Does not SATISFY DR-117. Does not SATISFY
  DR-131. Does not SATISFY DR-133. Does not SATISFY DR-114.
  Does not SATISFY DR-101. Gate 1 Class A is not opened. Not
  SATISFIED. Required-now stays 28. Condition-4 effect is zero.
  Naming parent of G18 is naming v6 (D-145), not leftover-join.v6.
  D-086 named DR-G18. Claude Stage A leftover-join.v6 returned
  three unlabeled observationsNotFindings strings. They carry
  no identifiers. No observations field. No advisories field.
  Codex Stage A leftover-join.v6 returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry recites those Claude
  observations as strings. It does not invent a Claude
  identifier. It does not invent a Codex identifier. It does
  not claim that both reviewers' identifiers are preserved.
  Claude Stage A returned no observation identifiers. Codex
  Stage A returned no observation identifiers.
  CLAUDE-G18LJ-V2-SF1 already landed in this lineage at
  leftover-join.v4. leftover-join.v5 carried the repair
  forward. This entry does not re-land CLAUDE-G18LJ-V2-SF1.
  basedOn.d275.role is last-heading custody only. Claude
  Stage B returned three unlabeled observationsNotFindings
  strings. They carry no identifiers. No observations field.
  No advisories field. Codex Stage B returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G18. Does not rewrite occupancy
  v4. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D276. Does not unwrite D-086, D-193, D-216,
  D-263, or D-275.
- **Commit:** C-D276.

## D-277 — Record monorepo leftover-join.v4 as DR-121 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-277.review-adversarial.claude2.json`,
  `786a2e9fa21094973111264f282d3d71a6ce48bb089fc1e5b8c2b49d8f508529`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-277.review-adversarial.codex.json`,
  `6efee77f5d04477953226bfeb653e4e6f99db1d8cacfdc1536646acd1301cdd0`)
  CONSENT. Subject `coordinator-decisions.D-277.draft.md`
  `189584aad1919b00fe4a5b59fcd4295517a74510375e3265cc61f6e29602eb46`.
  Frozen leftover-join
  `monorepo-leftover-join.v4.json`
  `03d4478c3ce6ea843f8a4ee3ea1dcc6d8c06bd661f71970fe836ce107b611481`
  Stage A Claude ACCEPT
  `9658f36deceaa89159d4b6e244e108fd10fd5a1b39261779a12446ea25dc3744`
  0/0; Stage A Codex ACCEPT
  `f704c3b2045a6d454f33566d6a214c5ba635ffd7acc684d52426582774db1524`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `monorepo-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275
  and D-276. D-272 is CONTESTED and is not on this
  no-cell-edit adoption branch. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/monorepo-leftover-join.v4.json`
  `03d4478c3ce6ea843f8a4ee3ea1dcc6d8c06bd661f71970fe836ce107b611481`.
- **Decision:** Record leftover-join.v4 as DR-121 leftover
  remasurement after D-276. The candidate binds NOTHING.
  DR-121 stays `OPEN`. leftover-design of OBL-G16-FX-AUTHORING
  and OBL-CI-ENCODING-RESERVED remains on leftover-join.v4.
  leftover-join.v3 remains current at draft time. After this
  successor is recorded, leftover-join.v3 is not current.
  Occupancy v5 is the current G16 occupancy remasurement.
  Occupancy v2 is not recorded as current occupancy. g16 leftover-join.v4
  remains the current G16 GATE leftover-join. Remainder of
  G16 execution remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not invent
  reserved CI encodings. Does not name G13 into required-now.
  Does not invent a D9 code. Does not invent a section 7.1
  recipe. Does not steal OBL-G16-FX-AUTHORING as a GATE
  closure. Does not occupy the identifier. Does not SATISFY
  DR-121. Does not SATISFY DR-117. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten
  DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-114. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Naming parent of G16 is naming v6 (D-145),
  not leftover-join.v4. D-086 named DR-G16. Claude Stage A
  leftover-join.v4 returned three named observations MLJ4-O1,
  MLJ4-O2, and MLJ4-O3. No change requested. They carry those
  identifiers. They are objects (id paired with text). No
  observations field. No advisories field. Codex Stage A
  leftover-join.v4 returned an empty observationsNotFindings
  list, an empty observations list, and zero advisories. This
  entry names those Claude identifiers. It does not invent a
  Codex identifier. It does not claim that both reviewers'
  identifiers are preserved. Codex Stage A returned no
  observation identifiers. basedOn.d276.role is last-heading
  custody only. Claude Stage B returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. Codex Stage B returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry does not invent identifiers.
  It does not claim that both reviewers' identifiers are
  preserved. Claude Stage B returned no observation
  identifiers. Codex Stage B returned no observation
  identifiers. Does not execute G16. Does not rewrite occupancy
  v5. Does not edit file 08. Does not authorize
  `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D277. Does not unwrite D-086, D-181, D-215,
  D-262, or D-276.
- **Commit:** C-D277.

## D-278 — Record g16 leftover-join.v5 as G16 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-278.review-adversarial.claude2.json`,
  `3b815a1e618cb65e40e9d6ab690af864e2c8cc335b96dfa98ee428865952716f`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-278.review-adversarial.codex.json`,
  `bc2d9bbf2a7b6bf4f7e71f9946adae0aa83a0a07289ead2d0647ee8c8b82f5c3`)
  CONSENT. Subject `coordinator-decisions.D-278.draft.md`
  `0c828d904b576fd7ad1da5fba478b8d4544dfcd39ad89560af74ce95655d987e`.
  Frozen leftover-join
  `g16-leftover-join.v5.json`
  `7ce75ea514322a6e17546ec8e9b91c4fb2f66128271d6c6d757e3f627e05ab78`
  Stage A Claude ACCEPT
  `a6885511e4851afd19d608653152745c8aab805c3b95eb3dfb9667e54d42831b`
  0/0; Stage A Codex ACCEPT
  `efcb84f9a34229c7dd215dcb6e8913bec4685371a4b39ad08a22727bb73c1784`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g16-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275
  and D-276 and D-277. D-272 is CONTESTED and is not on this
  no-cell-edit adoption branch. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g16-leftover-join.v5.json`
  `7ce75ea514322a6e17546ec8e9b91c4fb2f66128271d6c6d757e3f627e05ab78`.
- **Decision:** Record leftover-join.v5 as G16 leftover
  remasurement after D-277. The candidate binds NOTHING.
  DR-G16 stays `OPEN`. leftover-design of OBL-G16-FX-AUTHORING
  remains on leftover-join.v5. leftover-join.v4 remains current
  at draft time. After this successor is recorded,
  leftover-join.v4 is not current. Occupancy v5 is the current
  G16 occupancy remasurement. Occupancy v2 is not recorded as
  current occupancy. monorepo leftover-join.v4 remains the
  current DR-121 leftover-join. monorepo leftover-join.v3 is
  not recorded as current DR-121 leftover-join. Remainder of
  G16 execution remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not invent
  reserved CI encodings. Does not name G13 into required-now.
  Does not invent a D9 code. Does not invent a section 7.1
  recipe. Does not steal OBL-CI-ENCODING-RESERVED. Does not
  occupy the identifier. Does not SATISFY DR-121. Does not
  SATISFY DR-117. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten
  DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-114. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Naming parent of G16 is naming v6 (D-145),
  not leftover-join.v5. D-086 named DR-G16. Claude Stage A
  leftover-join.v5 returned four named observations G16LJ5-O1,
  G16LJ5-O2, G16LJ5-O3, and G16LJ5-O4. No change requested.
  They carry those identifiers. They are objects (id paired
  with text). No observations field. No advisories field.
  Codex Stage A leftover-join.v5 returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry names those Claude
  identifiers. It does not invent a Codex identifier. It does
  not claim that both reviewers' identifiers are preserved.
  Codex Stage A returned no observation identifiers.
  basedOn.d277.role is last-heading custody only. Claude
  Stage B returned one named observation D278-O1. No change
  requested. It carries that identifier. It is an object (id
  paired with text). Empty observations list. Empty advisories
  list. Codex Stage B returned an empty
  observationsNotFindings list, no observations field, and
  zero advisories. This entry names that Claude identifier.
  It does not invent a Codex identifier. It does not claim
  that both reviewers' identifiers are preserved. Codex
  Stage B returned no observation identifiers. Does not
  execute G16. Does not rewrite occupancy v5. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D278. Does not unwrite D-086, D-192, D-215,
  D-262, or D-277.
- **Commit:** C-D278.

## D-279 — Record provider leftover-join.v4 as G10 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-279.review-adversarial.claude2.json`,
  `2b9fb78597b8026ec37bda8c126154dc642db19f03acfd8bde5fac3ecbf2441b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-279.review-adversarial.codex.json`,
  `52dab7d6622a9aaadca68f27f220a5c07f70a27c1d37e27a0038768eb54b6497`)
  CONSENT. Subject `coordinator-decisions.D-279.draft.md`
  `dbcb817f2425fb4c377ea29c4d46a808ee58bd263431e43f366c8416d9eeeb16`.
  Frozen leftover-join
  `provider-leftover-join.v4.json`
  `0e31f5b558e77b55a5aa42b711e5f5927062f67ed9f150d78c875326b79f16d4`
  Stage A Claude ACCEPT
  `c247c7144c1d51164d5969925c11400398a52f879f339a6371589e5b657d8fb4`
  0/0; Stage A Codex ACCEPT
  `6e75e84fb9690120df565068d8955d23d281563bc9d20b7c6c5c6c8cc3e08d0a`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `provider-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275
  and D-276 and D-277 and D-278. D-272 is CONTESTED and is
  not on this no-cell-edit adoption branch. Not a three-limb
  act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/provider-leftover-join.v4.json`
  `0e31f5b558e77b55a5aa42b711e5f5927062f67ed9f150d78c875326b79f16d4`.
- **Decision:** Record leftover-join.v4 as G10 leftover
  remasurement after D-278. The candidate binds NOTHING.
  DR-G10 stays `HARD-BLOCKED pending selector refresh`.
  leftover-design of OBL-G10-FX-AUTHORING and
  OBL-SELECTOR-REFRESH remains on leftover-join.v4.
  leftover-join.v3 remains current at draft time. After this
  successor is recorded, leftover-join.v3 is not current.
  Occupancy v2 is the current G10 occupancy remasurement.
  Occupancy v1 is not recorded as current occupancy. There
  is no separate GATE leftover-join family for G10. Remainder
  of G10 execution remains qualification (D-056). Does not
  pin QUALIFIED. Does not invent fixture bytes. Does not
  invent a D9 code. Does not invent a V2 selector. Does not
  invent a section 7.1 recipe. Does not occupy the identifier.
  Does not SATISFY DR-102 a second time. Does not reopen
  DR-102 SATISFIED. Does not flatten `HARD-BLOCKED pending
  selector refresh` to `OPEN`. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten
  DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-114. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Naming parent of G10 is naming v6 (D-145),
  not leftover-join.v4. D-086 named DR-G10. Claude Stage A
  leftover-join.v4 returned five unnamed observation strings.
  No change requested. They are strings. No identifiers. No
  observations field. No advisories field. This entry does
  not invent Claude identifiers. Codex Stage A leftover-join.v4
  returned an empty observationsNotFindings list, an empty
  observations list, and zero advisories. This entry does
  not invent a Codex identifier. It does not claim that both
  reviewers' identifiers are preserved. Codex Stage A
  returned no observation identifiers. Claude Stage A
  returned no observation identifiers. basedOn.d278.role is
  last-heading custody only. Claude Stage B returned four
  named observations D279-O1, D279-O2, D279-O3, and D279-O4.
  No change requested. They carry those identifiers. They
  are objects (id paired with observation). Empty
  observations list. Empty advisories list. Codex Stage B
  returned an empty observationsNotFindings list, no
  observations field, and zero advisories. This entry names
  those Claude identifiers. It does not invent a Codex
  identifier. It does not claim that both reviewers'
  identifiers are preserved. Codex Stage B returned no
  observation identifiers. Does not execute G10. Does not
  rewrite occupancy v2. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D279. Does not unwrite D-086, D-085, D-187,
  D-212, or D-278.
- **Commit:** C-D279.

## D-280 — Record signed-index leftover-join.v4 as DR-112 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-280.review-adversarial.claude2.json`,
  `4672b91a95ec1f6c5f04ca8d870cd9f8dd3e0fb17c486ec73e90b6dafb55b01b`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-280.review-adversarial.codex.json`,
  `4f46fd2353d66f8e39e1ff11c6613d79512f2dba3c2b9aa82d906e757b0bb6d4`)
  CONSENT. Subject `coordinator-decisions.D-280.draft.md`
  `86e070ced9981e3c074e474e081a5efe9c580b927f693e8e1ab035d001b4ffbd`.
  Frozen leftover-join
  `signed-index-leftover-join.v4.json`
  `ae5176e2a420be75b8aade77e7f265bc411968a75a35647ae01bfc708835a174`
  Stage A Claude ACCEPT
  `1ff13ff46581bbaab502f1df4640bd32c2476da0af16ba52a3c5cd6601722b51`
  0/0; Stage A Codex ACCEPT
  `581cf0631eaf24f49ef587e4ff7ed47965d06f1a4b3003cc23b7a31d9707855c`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `signed-index-leftover-join.v4.json` (0 blockers,
  0 SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275
  and D-276 and D-277 and D-278 and D-279. D-272 is
  CONTESTED and is not on this no-cell-edit adoption
  branch. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/signed-index-leftover-join.v4.json`
  `ae5176e2a420be75b8aade77e7f265bc411968a75a35647ae01bfc708835a174`.
- **Decision:** Record leftover-join.v4 as DR-112 leftover
  remasurement after D-279. The candidate binds NOTHING.
  DR-112 stays `OPEN`. leftover-design of OBL-G08-FX-AUTHORING
  and OBL-RESERVED-NUMBERS remains on leftover-join.v4.
  leftover-join.v3 remains current at draft time. After this
  successor is recorded, leftover-join.v3 is not current.
  Occupancy v3 is the current G08 occupancy remasurement.
  Occupancy v2 is not recorded as current occupancy. g08
  leftover-join.v4 remains the current G08 GATE leftover-join.
  Remainder of G08 execution remains qualification (D-056).
  Does not pin QUALIFIED. Does not invent fixture bytes. Does
  not mint reserved numbers. Does not invent a recovery
  ceremony implementation. Does not invent a D9 code. Does
  not invent a section 7.1 recipe. Does not steal
  OBL-G08-FX-AUTHORING as a GATE closure. Does not steal
  OBL-RESERVED-NUMBERS. Does not occupy the identifier. Does
  not SATISFY DR-112. Does not SATISFY DR-117. Does not
  flatten DR-118 `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does
  not flatten DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`.
  Does not SATISFY DR-131. Does not SATISFY DR-133. Does not
  SATISFY DR-114. Does not SATISFY DR-101. Gate 1 Class A is
  not opened. Not SATISFIED. Required-now stays 28.
  Condition-4 effect is zero. Naming parent of G08 is naming
  v6 (D-145), not leftover-join.v4. D-086 named DR-G08.
  Claude Stage A leftover-join.v4 returned three unnamed
  observation strings. No change requested. They are strings.
  No identifiers. No observations field. No advisories field.
  This entry does not invent Claude identifiers. Codex Stage
  A leftover-join.v4 returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry does not invent a Codex
  identifier. It does not claim that both reviewers'
  identifiers are preserved. Codex Stage A returned no
  observation identifiers. Claude Stage A returned no
  observation identifiers. basedOn.d279.role is last-heading
  custody only. Claude Stage B returned one named observation
  D280-O1. No change requested. It carries that identifier.
  It is an object (id paired with observation). Empty
  observations list. Empty advisories list. Codex Stage B
  returned an empty observationsNotFindings list, no
  observations field, and zero advisories. This entry names
  that Claude identifier. It does not invent a Codex
  identifier. It does not claim that both reviewers'
  identifiers are preserved. Codex Stage B returned no
  observation identifiers. Does not execute G08. Does not
  rewrite occupancy v3. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D280. Does not unwrite D-086, D-178, D-211,
  D-259, or D-279.
- **Commit:** C-D280.

## D-281 — Record g08 leftover-join.v5 as G08 leftover remasurement

- **Date:** 2026-08-24
- **Status:** **ADOPTED 2026-08-24.** Turn 1 of 3: CONSENT from both
  independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-281.review-adversarial.claude2.json`,
  `8b06f3d7a89c233d99f3e3805894e31b6230b711c9a41687c3e9b1e19677855d`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-281.review-adversarial.codex.json`,
  `d5a7cf80f187532e7047a65dd93a5df811ffaf7f721920b8e45ab4b4b9bae09e`)
  CONSENT. Subject `coordinator-decisions.D-281.draft.md`
  `cd548e784dd0bbd4aeef9034f547c690c1f0e53325c1252a4ae9e3f107ebaa84`.
  Frozen leftover-join
  `g08-leftover-join.v5.json`
  `ba1c19d7f5e6ec4b67fc5b7589e0b5ef3c946d186166660ccdf63ea916d9a60f`
  Stage A Claude ACCEPT
  `052264d70f8bfa95bdcdc2ab8c0aa55a07f88fe2cfe6d733c12ee3bc527fdc17`
  0/0; Stage A Codex ACCEPT
  `15ae0351e32083f3ab4a2f40b513757037e8cd3ca3053d6c1f55795790c8a39f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `g08-leftover-join.v5.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through
  D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and
  D-247 and D-248 and D-249 and D-250 and D-251 and D-252
  and D-253 and D-254 and D-255 and D-256 and D-257 and
  D-258 and D-259 and D-260 and D-261 and D-262 and D-263
  and D-264 and D-265 and D-266 and D-267 and D-268 and
  D-269 and D-270 and D-271 and D-273 and D-274 and D-275
  and D-276 and D-277 and D-278 and D-279 and D-280. D-272
  is CONTESTED and is not on this no-cell-edit adoption
  branch. Not a three-limb act. Not SATISFIED-GRADE.
- **Subject:** `docs/coop/artifacts/g08-leftover-join.v5.json`
  `ba1c19d7f5e6ec4b67fc5b7589e0b5ef3c946d186166660ccdf63ea916d9a60f`.
- **Decision:** Record leftover-join.v5 as G08 leftover
  remasurement after D-280. The candidate binds NOTHING.
  DR-G08 stays `OPEN`. leftover-design of OBL-G08-FX-AUTHORING
  remains on leftover-join.v5. leftover-join.v4 remains current
  at draft time. After this successor is recorded,
  leftover-join.v4 is not current. Occupancy v3 is the current
  G08 occupancy remasurement. Occupancy v2 is not recorded as
  current occupancy. signed-index leftover-join.v4 remains the
  current DR-112 leftover-join. signed-index leftover-join.v3 is
  not recorded as current DR-112 leftover-join. Remainder of
  G08 execution remains qualification (D-056). Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not mint
  reserved numbers. Does not invent a recovery ceremony
  implementation. Does not invent a D9 code. Does not invent
  a section 7.1 recipe. Does not steal OBL-RESERVED-NUMBERS.
  Does not occupy the identifier. Does not SATISFY DR-112.
  Does not SATISFY DR-117. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten
  DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not
  SATISFY DR-131. Does not SATISFY DR-133. Does not SATISFY
  DR-114. Does not SATISFY DR-101. Gate 1 Class A is not
  opened. Not SATISFIED. Required-now stays 28. Condition-4
  effect is zero. Naming parent of G08 is naming v6 (D-145),
  not leftover-join.v5. D-086 named DR-G08. Claude Stage A
  leftover-join.v5 returned three named observations G08LJ5-O1,
  G08LJ5-O2, and G08LJ5-O3. No change requested. They carry
  those identifiers. They are objects (id paired with
  observation). No observations field. No advisories field.
  Codex Stage A leftover-join.v5 returned an empty
  observationsNotFindings list, an empty observations list,
  and zero advisories. This entry names those Claude
  identifiers. It does not invent a Codex identifier. It does
  not claim that both reviewers' identifiers are preserved.
  Codex Stage A returned no observation identifiers.
  basedOn.d280.role is last-heading custody only. Claude
  Stage B returned one named observation D281-ADV-O1. No
  change requested. It carries that identifier. It is an
  object (id paired with observation). Empty observations
  list. Empty advisories list. Codex Stage B returned an
  empty observationsNotFindings list, no observations field,
  and zero advisories. This entry names that Claude
  identifier. It does not invent a Codex identifier. It does
  not claim that both reviewers' identifiers are preserved.
  Codex Stage B returned no observation identifiers. Does not
  execute G08. Does not rewrite occupancy v3. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays
  5 of 32. Condition 4 stays MET on the naming half
  (28 of 28). Condition 5 last.
- **Reversibility:** Total only before a later dependent
  leftover rewrite, SATISFIED cycle, or file-08 cell rewrite.
  Overturn: C-D281. Does not unwrite D-086, D-188, D-211,
  D-259, or D-280.
- **Commit:** C-D281.

## D-282 — Record component-manifest leftover-join.v9 as DR-103 leftover remasurement

- **Date:** 2026-08-26
- **Status:** **ADOPTED 2026-08-26.** Turn 2 of 3: CONSENT from
  both independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-282.review-adversarial.claude2.turn2.json`,
  `90dbe124f607f1107c6216b14b884f8fddbffabcc208e085179f958955f4b3cd`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-282.review-adversarial.codex.turn2.json`,
  `d91bb90bbef69d1af39c4d638e9888c4792a20111f84b27e65471b663b76502f`)
  CONSENT. Subject `coordinator-decisions.D-282.turn2.draft.md`
  `2063177aaf2e3632472066d6721babbc4df3a47b4e9d6fedd2aa54bcd0a71ec6`.
  turn-1 Claude OBJECT (CLAUDE-D282-SF1 / CLAUDE-D282-SF2)
  `e094b9e06c15013a8aa32f49f2975ca700af4227f3eef6510257797826f8aa7a`;
  turn-1 Codex OBJECT (CODEX-D282-SF1 / CODEX-D282-SF2 /
  CODEX-D282-SF3)
  `d423eb263e355d1eef2d793db5efaa7c6f5899dded4048754100d2229420aa24`.
  Frozen leftover-join `component-manifest-leftover-join.v9.json`
  `e71dca64c78a8feea9e72df5ae846eb2843be50fb10d01d54d5b65714ed1d2c4`
  Stage A Claude ACCEPT
  `db852c4d21f955230744891390dd1cd3d15d1fe9cc9b9e955f7976a2ba38f1f6`
  0/0; Stage A Codex ACCEPT
  `46b67eb621e6beb528c07335a0981bbad477a2ec2bc54dc6e46c9a7a4baf7e6f`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `component-manifest-leftover-join.v9.json` (0
  blockers, 0 SHOULD-FIX). Same no-cell-edit branch as D-170
  through D-235 and D-237 and D-238 and D-239 and D-240 and D-241
  and D-242 and D-243 and D-244 and D-245 and D-246 and D-247 and
  D-248 and D-249 and D-250 and D-251 and D-252 and D-253 and
  D-254 and D-255 and D-256 and D-257 and D-258 and D-259 and
  D-260 and D-261 and D-262 and D-263 and D-264 and D-265 and
  D-266 and D-267 and D-268 and D-269 and D-270 and D-271 and
  D-273 and D-274 and D-275 and D-276 and D-277 and D-278 and
  D-279 and D-280 and D-281. D-272 is CONTESTED and is not on this
  no-cell-edit adoption branch. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:**
  `docs/coop/artifacts/component-manifest-leftover-join.v9.json`
  `e71dca64c78a8feea9e72df5ae846eb2843be50fb10d01d54d5b65714ed1d2c4`.
- **Decision:** Record leftover-join.v9 as DR-103 leftover
  remasurement after D-281. Lands CODEX-D282-SF1, CODEX-D282-SF2,
  CODEX-D282-SF3, CLAUDE-D282-SF1, CLAUDE-D282-SF2. CODEX-D282-SF1
  and CLAUDE-D282-SF1 are the same class. CODEX-D282-SF3 and
  CLAUDE-D282-SF2 are the same class. All five identifiers are
  named. The candidate binds NOTHING. DR-103 stays `OPEN`.
  leftover-design of OBL-WINDOWS-PATH, OBL-ENVELOPE-MISMATCH,
  OBL-UNICODE-NORM, OBL-OD-1, and OBL-OD-2 remains on
  leftover-join.v9. leftover-join.v6 remains current at draft
  time. After this successor is recorded, leftover-join.v6 is not
  current. leftover-join.v7 is CANDIDATE-NOT-APPLIED (Dual REJECT:
  Codex CMLJ-V7-SF1; Claude CLAUDE-CMLJ-V7-SF1 /
  CLAUDE-CMLJ-V7-SF2) and is not current. leftover-join.v8 is
  CANDIDATE-NOT-APPLIED (Stage A REJECT: Codex CMLJ-V8-SF1 /
  CMLJ-V8-SF2; Claude CLAUDE-CMLJ-V8-SF1) and is not current.
  Occupancy v9 is the current G15 occupancy remasurement.
  Occupancy v7 is not recorded as current occupancy. g15
  leftover-join.v5 remains the current G15 GATE leftover-join.
  packaging leftover-join.v4 remains the current DR-120 ROW
  leftover-join. OBL-G15-HARNESS-SPEC authoring remains measured
  closed against occupancy v9; G15 execution remains qualification
  (D-056). D-013's SATISFIED-refusal stands. Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not invent a
  reserved-device-name list. Does not invent a schema successor.
  Does not decide OD-1 or assign its owner. Does not fold OD-2.
  Does not invent a D9 code. Does not invent a section 7.1 recipe.
  Does not steal OBL-AT-FX-AUTHORING or OBL-ADAPTER-IMPL. Does not
  occupy the identifier. Does not SATISFY DR-103. Does not SATISFY
  DR-120. Does not SATISFY DR-117. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten DR-107
  `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming parent
  of G15 is naming v6 (D-145), not leftover-join.v9. D-086 named
  DR-G15. Claude Stage A leftover-join.v9 returned 4 unlabeled
  observationsNotFindings strings (no identifiers). It returned no
  observations field and no advisories field. Codex Stage A
  leftover-join.v9 returned no observationsNotFindings field. It
  returned no observations field and no advisories field. This
  entry does not invent identifiers. It does not claim that both
  reviewers' identifiers are preserved. Claude Stage A returned no
  observation identifiers. Codex Stage A returned no observation
  identifiers. leftover-join.v9 lands CMLJ-V8-SF1, CMLJ-V8-SF2,
  and CLAUDE-CMLJ-V8-SF1. CMLJ-V8-SF1 and CLAUDE-CMLJ-V8-SF1 are
  the same class. All three identifiers are named. It carries the
  leftover-join.v8 landings of CMLJ-V7-SF1, CLAUDE-CMLJ-V7-SF1,
  and CLAUDE-CMLJ-V7-SF2 (CMLJ-V7-SF1 and CLAUDE-CMLJ-V7-SF1 are
  the same class) and re-lands nothing. basedOn.d281.role is
  last-heading custody only. Claude Stage B returned 4 named
  observationsNotFindings objects D282-T2-ADV-O1, D282-T2-ADV-O2,
  D282-T2-ADV-O3, D282-T2-ADV-O4 (each an id paired with an
  observation and a whyNotAFinding); no change requested; they
  carry those identifiers. It returned an empty observations list
  and zero advisories. Codex Stage B returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B
  returned no observation identifiers. Claude Stage B turn 1
  returned 4 named observationsNotFindings objects D282-ADV-O1,
  D282-ADV-O2, D282-ADV-O3, D282-ADV-O4 (each an id paired with an
  observation and a whyNotAFinding); no change requested; they
  carry those identifiers. It returned an empty observations list
  and zero advisories. Codex Stage B turn 1 returned no
  observationsNotFindings field. It returned no observations field
  and no advisories field. This entry names those Claude
  identifiers. It does not invent a Codex identifier. It does not
  claim that both reviewers' identifiers are preserved. Codex
  Stage B turn 1 returned no observation identifiers. Does not
  execute G15. Does not rewrite occupancy v9. Does not edit file
  08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays 5 of 32.
  Condition 4 stays MET on the naming half (28 of 28). Condition 5
  last.
- **Reversibility:** Total only before a later dependent leftover
  rewrite, SATISFIED cycle, or file-08 cell rewrite. Overturn:
  C-D282. Does not unwrite D-013, D-086, D-104, D-106, D-174,
  D-214, D-266, D-270, or D-281. Does not unwrite the turn-1
  OBJECTs.
- **Commit:** C-D282.

## D-283 — Record permission leftover-join.v12 as DR-105 leftover remasurement

- **Date:** 2026-08-26
- **Status:** **ADOPTED 2026-08-26.** Turn 3 of 3: CONSENT from
  both independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-283.review-adversarial.claude2.turn3.json`,
  `ecb647ffcf78219d84c0ce05dda647a3304da99699892fd2cf1c51201c5cec93`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-283.review-adversarial.codex.turn3.json`,
  `736d24f6401b1f58b1217f74f3c5a12170c72993ff3094ca41661f3a37b0dda9`)
  CONSENT. Subject `coordinator-decisions.D-283.turn3.draft.md`
  `d0649b4a3d3dc84fc9218670d1f43eccb2f3066c00884f3772811cb8ac1c893e`.
  turn-1 Claude OBJECT (CLAUDE-D283-SF1)
  `7f3b9002817a2690dc34425ce2b5cddcbaa6f9c2473fcc451d6e026e895a132e`;
  turn-1 Codex CONSENT
  `27df9e65fa2f5e8417a55f58870f7bdf33494227ed36ed5b13fc54ecb590a170`.
  turn-2 Claude OBJECT (CLAUDE-D283-T2-SF1)
  `823add97b27a7d540fded40cb9e3c18340a258f539125e6a1f6bc1eeb7053e92`;
  turn-2 Codex OBJECT (CODEX-D283-SF1)
  `12dd3ec3fea22129701a3be332a575c77ea24682f33b6f57bd26005b12cd3e6f`.
  Frozen leftover-join `permission-leftover-join.v12.json`
  `496b75c60c6540c3272c2c57d86c43ca71a77a1ed2eceaa6e3a1c49251374fb3`
  Stage A Claude ACCEPT
  `7918e1456f7cb8438d6e693e2f1d42bfab9691614c316ce55537180150ccb50e`
  0/0; Stage A Codex ACCEPT
  `03a2202d28b42822322d17d71f1610e4bb99631a84cbe8331187da77ac49db64`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `permission-leftover-join.v12.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through D-235 and
  D-237 and D-238 and D-239 and D-240 and D-241 and D-242 and
  D-243 and D-244 and D-245 and D-246 and D-247 and D-248 and
  D-249 and D-250 and D-251 and D-252 and D-253 and D-254 and
  D-255 and D-256 and D-257 and D-258 and D-259 and D-260 and
  D-261 and D-262 and D-263 and D-264 and D-265 and D-266 and
  D-267 and D-268 and D-269 and D-270 and D-271 and D-273 and
  D-274 and D-275 and D-276 and D-277 and D-278 and D-279 and
  D-280 and D-281 and D-282. D-272 is CONTESTED and is not on this
  no-cell-edit adoption branch. Not a three-limb act. Not
  SATISFIED-GRADE.
- **Subject:**
  `docs/coop/artifacts/permission-leftover-join.v12.json`
  `496b75c60c6540c3272c2c57d86c43ca71a77a1ed2eceaa6e3a1c49251374fb3`.
- **Decision:** Record leftover-join.v12 as DR-105 leftover
  remasurement after D-282. Lands CODEX-D283-SF1,
  CLAUDE-D283-T2-SF1. CODEX-D283-SF1 and CLAUDE-D283-T2-SF1 are
  the same class (the Reversibility sentence that pluralised the
  single turn-1 objection; it now reads the turn-1 Claude OBJECT).
  All identifiers are named. CLAUDE-D283-SF1 (turn 1) landed in
  the turn-2 subject and is carried, not re-landed. The candidate
  binds NOTHING. DR-105 stays `OPEN`. leftover-design of
  OBL-FX-AUTHORING, OBL-R10-AUTHORING, OBL-R6-AUTHORING,
  OBL-FC-C1, OBL-BLK-1, OBL-BLK-2, OBL-BLK-3, OBL-BLK-4 remains on
  leftover-join.v12. leftover-join.v9 remains current at draft
  time. After this successor is recorded, leftover-join.v9 is not
  current. leftover-join.v10 is CANDIDATE-NOT-APPLIED (Stage A
  Split: Codex REJECT 0/1 PLJ-V10-SF1; Claude ACCEPT 0/0 with
  advisory A-CLAUDE-PLJ-V10-01) and is not current.
  leftover-join.v11 is CANDIDATE-NOT-APPLIED (Stage A Dual REJECT:
  Codex PLJ-V11-SF1; Claude CLAUDE-PLJ-V11-SF1) and is not
  current. G09 occupancy v4 is the current G09 occupancy
  remasurement (D-220). G09 occupancy v3 is not recorded as
  current occupancy. g09 leftover-join.v11 remains the current
  DR-G09 GATE leftover-join (D-257). doctor-actor
  leftover-join.v11 remains the current DR-114 ROW leftover-join
  (D-170). Actor-join fixture execution is qualification at DR-G32
  (Operability + security); authoring/integration still rides
  DR-114. OBL-G09-HARNESS-SPEC authoring remains measured closed
  against occupancy v4; G09 execution remains qualification
  (D-056). Does not pin QUALIFIED. Does not invent fixture bytes.
  Does not invent a decision-record envelope, journal bytes, an
  expiry-age number, a cleanup-bound number, or a wall-clock
  comparison. Does not fold R-10 or R-6 into the fourteen FX. Does
  not record FC-C1. Does not invent a D9 code. Does not invent a
  section 7.1 recipe. Does not steal OBL-FX-AUTHORING as a GATE
  closure. Does not steal OBL-DOCTOR-FX-AUTHORING or
  OBL-JOIN-FX-AUTHORING. Does not occupy the identifier. Does not
  SATISFY DR-105. Does not SATISFY DR-114. Does not SATISFY
  DR-117. Does not flatten DR-118 `DECIDED-V1-NOT-INTEGRATED` to
  `OPEN`. Does not flatten DR-107 `PROPOSED-CLOSED-FOR-REVIEW` to
  `OPEN`. Does not SATISFY DR-131. Does not SATISFY DR-133. Does
  not SATISFY DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming parent
  of G09 is naming v6 (D-145), not leftover-join.v12. D-086 named
  DR-G09. Claude Stage A leftover-join.v12 returned 3 unlabeled
  observationsNotFindings strings (no identifiers). It returned no
  observations field and zero advisories. Codex Stage A
  leftover-join.v12 returned no observationsNotFindings field. It
  returned no observations field and zero advisories. This entry
  does not invent identifiers. It does not claim that both
  reviewers' identifiers are preserved. Claude Stage A returned no
  observation identifiers. Codex Stage A returned no observation
  identifiers. leftover-join.v12 lands PLJ-V11-SF1 and
  CLAUDE-PLJ-V11-SF1 (the same class; both identifiers are named)
  and carries the leftover-join.v11 landing of PLJ-V10-SF1 (same
  class as Claude Stage A advisory A-CLAUDE-PLJ-V10-01; both
  named) without re-landing it; the earlier cumulative entries
  (CLAUDE-PLJ-V3-B1 at leftover-join.v4; CLAUDE-PTLJ-V3-SF1 at
  leftover-join.v6; PLJ-V7-SF1, CLAUDE-PLJ-V8-SF1, PLJ-V8-SF1, and
  PLJ-V8-SF2 at leftover-join.v9) are carried unchanged.
  basedOn.d282.role is last-heading custody only. Claude Stage B
  returned 4 named observationsNotFindings objects
  CLAUDE-D283-T3-O1, CLAUDE-D283-T3-O2, CLAUDE-D283-T3-O3,
  CLAUDE-D283-T3-O4 (each an id paired with an observation and a
  whyNotAFinding); no change requested; they carry those
  identifiers. It returned an empty observations list and zero
  advisories. Codex Stage B returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B
  returned no observation identifiers. Claude Stage B turn 1
  returned 4 named observationsNotFindings objects D283-ADV-O1,
  D283-ADV-O2, D283-ADV-O3, D283-ADV-O4 (each an id paired with an
  observation and a whyNotAFinding); no change requested; they
  carry those identifiers. It returned an empty observations list
  and zero advisories. Codex Stage B turn 1 returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B turn 1
  returned no observation identifiers. Claude Stage B turn 2
  returned 3 named observationsNotFindings objects
  CLAUDE-D283-T2-O1, CLAUDE-D283-T2-O2, CLAUDE-D283-T2-O3 (each an
  id paired with an observation and a whyNotAFinding); no change
  requested; they carry those identifiers. It returned an empty
  observations list and zero advisories. Codex Stage B turn 2
  returned an empty observationsNotFindings list. It returned no
  observations field and zero advisories. This entry names those
  Claude identifiers. It does not invent a Codex identifier. It
  does not claim that both reviewers' identifiers are preserved.
  Codex Stage B turn 2 returned no observation identifiers. Does
  not execute G09. Does not rewrite occupancy v4. Does not edit
  file 08. Does not authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays 5 of 32.
  Condition 4 stays MET on the naming half (28 of 28). Condition 5
  last.
- **Reversibility:** Total only before a later dependent leftover
  rewrite, SATISFIED cycle, or file-08 cell rewrite. Overturn:
  C-D283. Does not unwrite D-032, D-086, D-163, D-170, D-171,
  D-220, D-257, or D-282. Does not unwrite the turn-1 Claude
  OBJECT or the turn-2 OBJECTs.
- **Commit:** C-D283.

## D-284 — Record state-class leftover-join.v4 as DR-124 leftover remasurement

- **Date:** 2026-08-26
- **Status:** **ADOPTED 2026-08-26.** Turn 3 of 3: CONSENT from
  both independent reviewers, 0 MUST-FIX, 0 SHOULD-FIX. Claude 2
  (`artifacts/coordinator-decisions.D-284.review-adversarial.claude2.turn3.json`,
  `524ba235dcffbfeed4d51520d48fe5d1fbe18857ee1d290b8a6f2f04258a8121`)
  CONSENT. Codex
  (`artifacts/coordinator-decisions.D-284.review-adversarial.codex.turn3.json`,
  `1859138f3586fded3928783ea7befed24759c8b23224fa35787b8215ad26b5ac`)
  CONSENT. Subject `coordinator-decisions.D-284.turn3.draft.md`
  `2ad237d2d2dd5c7e648dd8178798de9632dfd469c5dcdc1e5e5c7824cafdaa68`.
  turn-1 Claude OBJECT (CLAUDE-D284-SF1)
  `7a7a5c612b8a3082b332cf148df94dd8a710a356c89bbc0ad441734708979478`;
  turn-1 Codex OBJECT (CODEX-D284-SF1)
  `51ca1699761be24fd6449278c4baf7750f0619b11212267174ab473f64616045`.
  turn-2 Claude OBJECT (CLAUDE-D284-T2-SF1)
  `80cfa6f9bce76d15d68883699e43fb11b2a31cedd4e9c78db3c137105d12490c`;
  turn-2 Codex CONSENT
  `09d9368d4ef60f8b4e38053b40cf3669f78d5650d441a7a44527e8ac21a48e10`.
  Frozen leftover-join `state-class-leftover-join.v4.json`
  `16b00ce69fea9e5fe83f44892ffee0a69f5b41a4ad18a6aca1ce7e77e830c902`
  Stage A Claude ACCEPT
  `8f627b70ceb106d2624f056042edb77ea8c1e01152a4e028af516267c4b4f5e1`
  0/0; Stage A Codex ACCEPT
  `d8e0877eca4df8040ad0493f4a053417c0517f9983ff773d22baa1d9c467075e`
  0/0.
- **Decision type:** RULE-GOVERNED. Records independent dual
  ACCEPT of `state-class-leftover-join.v4.json` (0 blockers, 0
  SHOULD-FIX). Same no-cell-edit branch as D-170 through D-235 and
  D-237 and D-238 and D-239 and D-240 and D-241 and D-242 and
  D-243 and D-244 and D-245 and D-246 and D-247 and D-248 and
  D-249 and D-250 and D-251 and D-252 and D-253 and D-254 and
  D-255 and D-256 and D-257 and D-258 and D-259 and D-260 and
  D-261 and D-262 and D-263 and D-264 and D-265 and D-266 and
  D-267 and D-268 and D-269 and D-270 and D-271 and D-273 and
  D-274 and D-275 and D-276 and D-277 and D-278 and D-279 and
  D-280 and D-281 and D-282 and D-283. D-272 is CONTESTED and is
  not on this no-cell-edit adoption branch. Not a three-limb act.
  Not SATISFIED-GRADE.
- **Subject:**
  `docs/coop/artifacts/state-class-leftover-join.v4.json`
  `16b00ce69fea9e5fe83f44892ffee0a69f5b41a4ad18a6aca1ce7e77e830c902`.
- **Decision:** Record leftover-join.v4 as DR-124 leftover
  remasurement after D-283. Lands CLAUDE-D284-T2-SF1. The
  identifier is named. CODEX-D284-SF1, CLAUDE-D284-SF1 (turn 1)
  landed in the turn-2 subject and are carried, not re-landed. The
  candidate binds NOTHING. DR-124 stays `OPEN`. leftover-design of
  OBL-G19-FX-AUTHORING, OBL-GRANT-JOURNAL, OBL-INHERIT-BLOCKED,
  OBL-MONOTONIC remains on leftover-join.v4. leftover-join.v3
  remains current at draft time. After this successor is recorded,
  leftover-join.v3 is not current.  G19 occupancy v2 is the
  current G19 occupancy remasurement (D-222). G19 occupancy v1 is
  not recorded as current occupancy. g19 leftover-join.v4 remains
  the current DR-G19 GATE leftover-join (D-256).
  OBL-G19-HARNESS-SPEC authoring remains measured closed against
  occupancy v2; G19 execution remains qualification (D-056).
  OBL-G19-NAMED-CATALOG naming is measured closed. Does not pin
  QUALIFIED. Does not invent fixture bytes. Does not invent a
  grant journal or grant-journal envelope. Does not invent a
  PURGED typed result. Does not invent a sealed-Run class. Does
  not invent a D-006 unit. Does not apply state-class-contract.v11
  or SUP-124-GRANT-JOURNAL. Does not settle the monotonic
  trust-store class. Does not treat inherit-blocked evidence as
  settled. Does not invent a D9 code. Does not invent a section
  7.1 recipe. Does not steal OBL-G19-FX-AUTHORING as a GATE
  closure. Does not occupy the identifier. Does not retarget
  DR-113. Does not SATISFY DR-124. Does not SATISFY DR-113. Does
  not SATISFY DR-117. Does not flatten DR-118
  `DECIDED-V1-NOT-INTEGRATED` to `OPEN`. Does not flatten DR-107
  `PROPOSED-CLOSED-FOR-REVIEW` to `OPEN`. Does not SATISFY DR-131.
  Does not SATISFY DR-133. Does not SATISFY DR-114. Does not
  SATISFY DR-101. Gate 1 Class A is not opened. Not SATISFIED.
  Required-now stays 28. Condition-4 effect is zero. Naming parent
  of G19 is naming v6 (D-145), not leftover-join.v4. D-086 named
  DR-G19. Claude Stage A leftover-join.v4 returned 4 named
  observationsNotFindings objects OBS-1, OBS-2, OBS-3, OBS-4 (each
  with members id, class, where, text); no change requested; they
  carry those identifiers. It returned no observations field and
  no advisories field. Codex Stage A leftover-join.v4 returned an
  empty observationsNotFindings list. It returned no observations
  field and zero advisories. This entry names those Claude
  identifiers. It does not invent a Codex identifier. It does not
  claim that both reviewers' identifiers are preserved. Codex
  Stage A returned no observation identifiers. leftover-join.v4
  lands no new finding; this lineage carries no lands record and
  no findingDisposition, and no reviewer finding has ever landed
  in it. basedOn.d283.role is last-heading custody only. Claude
  Stage B returned 5 named observationsNotFindings objects
  D284-T3-ADV-O1, D284-T3-ADV-O2, D284-T3-ADV-O3, D284-T3-ADV-O4,
  D284-T3-ADV-O5 (each with members id, observation,
  whyNotAFinding); no change requested; they carry those
  identifiers. It returned an empty observations list and zero
  advisories. Codex Stage B returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B
  returned no observation identifiers. Claude Stage B turn 1
  returned 5 named observationsNotFindings objects D284-ADV-O1,
  D284-ADV-O2, D284-ADV-O3, D284-ADV-O4, D284-ADV-O5 (each with
  members id, observation, whyNotAFinding); no change requested;
  they carry those identifiers. It returned an empty observations
  list and zero advisories. Codex Stage B turn 1 returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B turn 1
  returned no observation identifiers. Claude Stage B turn 2
  returned 4 named observationsNotFindings objects D284-T2-ADV-O1,
  D284-T2-ADV-O2, D284-T2-ADV-O3, D284-T2-ADV-O4 (each with
  members id, observation, whyNotAFinding); no change requested;
  they carry those identifiers. It returned an empty observations
  list and zero advisories. Codex Stage B turn 2 returned an empty
  observationsNotFindings list. It returned no observations field
  and zero advisories. This entry names those Claude identifiers.
  It does not invent a Codex identifier. It does not claim that
  both reviewers' identifiers are preserved. Codex Stage B turn 2
  returned no observation identifiers. Does not execute G19. Does
  not rewrite occupancy v2. Does not edit file 08. Does not
  authorize `docs/v2/implementation/`.
- **Readiness effect:** Zero SATISFIED. Condition 2 stays 5 of 32.
  Condition 4 stays MET on the naming half (28 of 28). Condition 5
  last.
- **Reversibility:** Total only before a later dependent leftover
  rewrite, SATISFIED cycle, or file-08 cell rewrite. Overturn:
  C-D284. Does not unwrite D-086, D-117, D-183, D-222, D-256, or
  D-283. Does not unwrite the turn-1 OBJECTs or the turn-2 Claude
  OBJECT.
- **Commit:** C-D284.
