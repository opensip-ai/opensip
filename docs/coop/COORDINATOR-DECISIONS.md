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

## D-001 — Definition of "completed" (RESERVED, in progress)

- **Date:** opened 2026-08-12; scope set by the user mid-conversation: **the
  completion target is the V2 design**, anchored at
  `docs/v2/architecture/08-decision-and-readiness-register.md`.
- **Status:** IN PROGRESS
- **What it will decide:** the operational finish line. The register defines
  its own: the five-condition **Blueprint-readiness decision** (register §
  "Blueprint-readiness decision"), ending with authorization of
  `docs/v2/implementation/`. D-001 will adopt that checklist as the
  definition of done and decide, per row, the closure ROUTE:
  1. DR-001..DR-011 — V1 successor through the coop process, versus an
     explicit, scoped, reviewed pre-blueprint disposition (the register's own
     alternative), per row. DR-012 is release-only and explicitly NOT part of
     completion.
  2. DR-101..DR-129 — which rows affect the FIRST BLUEPRINT SLICE (the slice
     definition is itself a preference-laden decision, expected to become
     D-002) and must be decided; which get explicit deferral dispositions.
  3. DR-201..DR-205 — adversarial re-reviews dispatched and ACCEPTED, or
     findings individually routed.
  4. DR-G01..DR-G22 — named harness and owner per required gate; no
     QUALIFIED/DEMONSTRATED claims anywhere.
  5. The final authorization act — made under D-000 on the user's behalf,
     marked PREFERENCE-LADEN, reviewed adversarially, and staged as the last
     commit so it is trivially revertible.
- **Known input facts:** the register's whole-document freeze pins
  (`e1cdb71d…`) were re-stranded by today's freeze riders (freeze now
  `c4560fc3…`) — the register's own pin-move record calls this a known defect
  of the citation form and prescribes verify-then-move; today's coop work
  already advances DR-009 (r1 v1.9 candidate + gate), DR-011-R07/R09 (checker
  review standing), and the DR-002/DR-006 routes (evidence lineage v9 owed).
- **Process:** a register-verification workflow is running — parallel readers
  verifying each register section against live corpus state and classifying
  every row's closure route and decision type. Its output becomes the D-001
  draft, which then goes to adversarial review per D-000.
