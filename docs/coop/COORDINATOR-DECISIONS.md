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
