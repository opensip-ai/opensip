# NEXT OpenSIP CLI — Architecture Freeze v1

> **DRAFT / NOT FROZEN / DO NOT IMPLEMENT AGAINST AS A SIGNED FREEZE**

**Drafted:** 2026-07-31  
**Freeze status:** NOT DECLARED  
**Consumer:** B — build this  
**Freeze date:** `[UNSET]`  
**Freeze payload hash:** `[UNSET]`  
**Snapshot/tag:** `[UNSET]`  
**Signers:** `[UNSET]`

This is the Phase-3 sign-off skeleton. It becomes the architecture freeze only
after every blocking placeholder below is replaced, the converged tree passes
the full checker/mutation suite, the implementer litmus passes, and the date,
payload hash, snapshot reference, and signers are recorded.

At draft time, the Phase 1A V10/retention candidate has failed independent
review with seven OPEN findings; it is not an accepted closure. The retention
product decision `CD-RT-5` therefore remains blocked. This draft does not select
a proof, retention default, degradation behavior, or purge semantics, and no
implementation may infer one from the surrounding text.

The first implementer litmus also failed with six non-V10 week-one forks. Binding
repairs for PlanId/RequestId, TypeScript topology, pre-admission PlanIntent,
external-scanner rejection, and ProjectId storage namespaces have landed at
`IMPLEMENTABLE_UNEXECUTED`; independent repair reviews and the final package
re-run remain mandatory before signature.

A second, blind consumer-B implementer litmus
([`consumer-b-implementer-litmus.v1.json`](artifacts/consumer-b-implementer-litmus.v1.json))
also returned `LITMUS-FAIL`, with five BLOCKING and fifteen FORK escalations that
no document named as a residual. Its failure was **not** V10 — that item it found
consistently named in six places. It clustered in three package defects, and this
revision of the freeze and of the blueprint repairs the packaging half of all
three:

1. every artifact link in the package pointed at a stale version, and no rule
   stated which bytes were normative — repaired by the pin table in
   [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1 and by the version
   rule in §2 below;
2. two independently `PASSED` surfaces — the Rust sidecar wire protocol and the
   trusted request context — were unreachable from every package document,
   leaving the Rust substrate unimplementable while the TypeScript one was
   byte-exact — repaired by binding them in §3 and §3.2 below and in blueprint
   §3.1/§3.3/§5; and
3. six identity recipes that `operability.v10` itself records as not yet
   existing were named in no residual table, while §6.6 of this record positively
   asserted that one of them did — repaired by §6.6 and §7.1 below.

The residue is a real contract gap, not a packaging gap, and is now named rather
than hidden: see §7.1. Naming it does not close it, and this revision closes no
finding, seals no surface, and signs nothing.

## 1. What this freeze will mean

When signed, Architecture Freeze v1 means:

- the first implementation slice and exclusions are fixed;
- each load-bearing surface is `SEAL` or `SEAL-WITH-CHANGES` with named,
  non-blocking residuals only;
- the Rust host/core factoring, one-shot topology floor, provider substrate,
  process ownership, crate dependency direction, and contract-to-code mapping are
  specific enough for week-one implementation;
- every remaining open item is explicitly parked, a measurement/release gate, or
  a written post-freeze delta—not an implementer choice; and
- architecture readiness remains distinct from product qualification.

It will **not** mean the product is release-qualified, that privacy/offline claims
may be published, that a resident host should ship, or that any process boundary
is a security sandbox.

## 2. Freeze authority set

The signed payload consists of:

- this freeze record and
  [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md);
- the accepted [`v1-slice.md`](v1-slice.md), SHA-256
  `6b8717fef545fe73f0de5879a7389fbc0c7c499c70e06b344789e5150478bee3`
  (14 217 bytes, recomputed 2026-08-04) — see **Pinning the non-JSON payload
  members** below for why this digest exists, what enforces it, and what it costs;
- the binding product packet
  [`product-dispositions.v1.json`](artifacts/product-dispositions.v1.json);
- the binding contracts and current adjudications in [`artifacts/`](artifacts/),
  at exactly the versions and digests pinned in
  [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1, including the
  Phase-1A artifact once accepted;
- [`claim-register.v1.json`](artifacts/claim-register.v1.json);
- the retained `check-*.py` instruments and mutation selftests, including
  `check-d9-v1.14.py` (SHA-256
  `513d69dd879dcb678d53d8df89a907d05dacd4b078ec43c7fedc939732c5e83e`), whose
  `derive` functions the D9 contract names as its own `referenceDerivation` and
  which is therefore normative for the axes-to-class step the D9 JSON does not
  itself state. What is normative is the **behaviour of that module when executed**
  under its sole admitted invocation `python3 -I -B`. It reaches the inherited
  derivation body by hash-verifying a 25-file closure — the 22 files its
  independently passed v1.13 predecessor declares, plus that predecessor, its
  checker `check-d9-v1.13.py`
  (`a905ab0e4b932c2ef4c565e847a12cb398abf9cd7a74abd92f95cbc85ffc8717`) and its
  independent review — and then executing the verified bytes; that closure is an
  implementation detail of the retained instrument, is recorded in full in
  [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1 note **N-5**, and is
  not itself part of the normative byte set an implementer builds against; and
- narrative [`architecture/`](architecture/) only where it does not conflict with
  the binding set; and
- [`GORTEX-BORROW-REGISTER.md`](GORTEX-BORROW-REGISTER.md) as a pinned external
  source/provenance map and implementation checklist only. It carries no contract,
  claim, product-disposition, or seal authority of its own.

Authority order is: binding artifact/checker plus per-claim register status →
accepted product scope/dispositions → signed blueprint/freeze mapping → narrative
rationale. A checker establishes only what it inspects. `implementable: true`, a
green checker, or this freeze never means DISCHARGED, QUALIFIED, or DEMONSTRATED.

**Version selection.** Authority order alone does not say *which version* of a
binding artifact is normative, and that ambiguity was itself a blocking litmus
finding. The rule is now explicit:

1. The normative bytes of every binding artifact are the ones pinned by filename
   **and SHA-256** in [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1.
   A link anywhere — in this record, in the blueprint, in
   [`v1-slice.md`](v1-slice.md), in
   [`ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md`](ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md),
   or in narrative — that carries no digest is a pointer, not authority.
2. An artifact's own `status` / `reviewStatus` field is the author's
   self-declaration, written before review. It is not a review verdict. The
   verdict is the independent review artifact named in §1.1.
3. A version whose independent review is `REJECTED` is not normative and must not
   be implemented, and its superseded predecessors do not become a fallback.
4. If a file's recomputed digest differs from its §1.1 pin, that is a detected
   conflict with a binding artifact under §8 — stop and record a design delta.
5. Rules 3 and 4 scope the *contract you implement*. They do not scope the files a
   retained checker verifies and executes inside itself. A `PASSED` checker whose
   independent review covered its execution closure may hash-verify and run its own
   superseded — including `REJECTED` — predecessors to expose a derivation it
   inherits unchanged; those predecessors remain runtime inputs of the instrument
   and acquire no normative standing from being executed. Running a pinned checker
   to obtain a value is therefore always compliant. Transcribing a predecessor
   contract's bytes into the implementation is not, and remains a rule 3/4
   violation. See §7.3 and blueprint §1.1 note **N-5**.

Both this record's §3 ledger and blueprint §1.1 carry the digests. They are one
fact recorded twice; §9.1 requires the signer to verify they agree.

**Pinning the non-JSON payload members — recorded 2026-08-04.** Rule 1 is written
without exception: *"A link anywhere … that carries no digest is a pointer, not
authority."* §1.1's table is a table of **binding JSON contract artifacts and their
retained checkers**, so the `.md` files rule 1 names sit outside it. A careful reader
checked the three of them — `v1-slice.md`, `ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md` and
`GORTEX-BORROW-REGISTER.md` — found none carrying a digest in either document, and
concluded that rule 1 fails on its own package. Each was measured separately. They are
three different situations and **only one was a defect**. Note that they do not even
share a standing: the first and third are signed-payload members listed above; the
second is not a payload member at all and appears in rule 1 only as a *place links
occur*.

1. **[`v1-slice.md`](v1-slice.md) — the defect, now closed.** The payload list above
   puts it in the signed payload, §4 calls it *"The detailed authority"*, blueprint §1
   ranks it
   **authority level 2** — above this record's own implementation mapping — and §7.1's
   `RunId` row cites `v1-slice §2.2` and `§7.5` as the load-bearing sites justifying a
   parked recipe. Under rule 1 as written, the package's number-two authority was
   therefore **not authority**. Its digest is now recorded at the payload bullet above,
   recomputed for that entry rather than copied:
   `6b8717fef545fe73f0de5879a7389fbc0c7c499c70e06b344789e5150478bee3`, 14 217 bytes.
   It is **not** added to §1.1: it is not a JSON contract, has no retained checker and
   is not a surface, and listing it there would assert a kind of authority it does not
   have.

   **What enforces it, stated exactly, because an unenforced digest is the defect it
   is meant to repair.** `check-package-coherence.py`'s `PC-2` does **not** cover this
   pin — its row binder discards any path not ending `.json`, so no amount of table
   placement would make it check a `.md` file, and claiming otherwise would make this
   entry the very `B-VER9R-01` shape §7.2.2 names: a recorded measurement never
   compared to the measurement it records. Two comparisons do reach it, and a signer
   owes one of them. **At signature:** `shasum -a 256 docs/coop/v1-slice.md` must equal
   the value above. **Standing, after signature:** §9.2's payload manifest covers every
   file in `docs/coop/` except this record and the manifest itself, so `v1-slice.md` is
   inside it, and §9.3's `python3 -I -B artifacts/make-freeze-manifest.py --verify`
   re-derives and diffs it by name. That is the durable hard comparison; the `shasum`
   line is what a reader runs before the manifest exists.

   **What it costs, said plainly so nobody is surprised later.** This makes
   `v1-slice.md` immutable in exactly the way
   [`ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md`](ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md)
   already is. Any edit — including a typo fix, a reflowed line, or a trailing
   newline — changes the digest, and under rule 4 that is a detected conflict: the
   `shasum` and `--verify` comparisons above go red, and this record must be amended in
   the same change through a §10 delta. That is rule 1 working as designed, not a
   side-effect: the whole point of pinning an authority is that it stops being editable
   in silence. **Do not repair a drifted `v1-slice.md` by updating this digest alone**;
   a digest edited to match whatever is on disk is a pointer wearing a pin, and it
   would restore the exact condition this entry closed.

2. **[`ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md`](ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md)
   — not a defect; it is the most strongly pinned file in the corpus, and neither
   document said where.** It carries no digest here or in §1.1, and that is **correct**:
   it is not a binding contract artifact and not a member of the signed payload. But its
   absence from both documents is what made it read as unpinned, since rule 1 names it
   by filename. It is pinned **in the checkers**. Measured 2026-08-04, its
   digest `47df412dba5d62a823ca7c008c382c489b8a10c797fd8656f3d4dd5d6c342e2e` appears in
   **seven** retained instruments — `check-retention-custody-v16.py` through
   `check-retention-custody-v22.py` — each of which hash-verifies it as a declared
   dependency before doing any work. Re-measure with
   `grep -rl 47df412dba5d62a823ca7c008c382c489b8a10c797fd8656f3d4dd5d6c342e2e docs/coop/artifacts/*.py`
   rather than quoting the seven.

   **What happens on drift is not hypothetical — it happened on 2026-08-04.** The file
   was edited; all seven checkers exited **2**, and the edit had to be reverted
   byte-exactly to restore them. Reproduced deliberately for this entry, on a scratch
   copy of the tree so the live file was never touched: appending **one newline** — a
   change no reader would call substantive — is sufficient, and all seven then print to
   stderr and exit 2, e.g.

   ```text
   cannot freeze RT22 authority: AuthorityError: dependency hash drift: ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md
   ```

   So this file sits under a **stricter** regime than a §1.1 pin: a §1.1 digest mismatch
   is a finding a human must notice, while this one halts seven instruments in
   `main()` before any contract is checked, and the exit code is **2** — distinct from
   the **1** those checkers use for findings, so drift can never be mistaken for a
   contract defect. Treat the file as read-only. Editing it is a §10 design delta that
   must re-pin all seven in the same change, and nothing in this package authorises
   editing it in place.

3. **[`GORTEX-BORROW-REGISTER.md`](GORTEX-BORROW-REGISTER.md) — not a defect; rule 1 is
   satisfied by its claiming nothing.** Rule 1 says an undigested link is *a pointer,
   not authority*. That is only a defect where authority was claimed. This file's own
   header declares its status `NON-AUTHORITATIVE SOURCE MAP AND IMPLEMENTATION
   CHECKLIST`, and its opening paragraph that it is *"**not** a new approval lane,
   binding contract, claim status, product disposition, or reason to expand the accepted
   v1 slice"* and that *"If this register conflicts with that authority set, this
   register loses."* The payload bullet above admits it *"as a pinned external
   source/provenance map and implementation checklist only … no contract, claim,
   product-disposition, or seal authority of its own."* Pointer is precisely its
   standing, so rule 1 returns the right answer with no digest at all. Recorded here so
   the next reader closes the question instead of re-raising it. If it is ever cited as
   binding anything, that citation is the defect — not the missing digest.

**And a fourth case nobody had written down: this record is itself pinned, by
*content anchors*, and editing the wrong sentence turns a checker red.** Found while
repairing the above — not reported by any litmus. `check-retention-custody-v23.py` and
`check-retention-custody-v24.py` each carry a `FREEZE_ANCHORS` tuple of **six verbatim
excerpts of this file**, whitespace and line breaks included, and raise
`RT23-RECORD IMPLEMENTATION-FREEZE.md anchor[n]: the cited text is absent from the live
file` when one stops matching. The six anchor §4.5's heading and two of its sentences,
§5's `CI layer 4` disposition row, §6 law 2's first two sentences, and §6's
`ExecutionId` allocation sentence. **This was demonstrated the hard way on 2026-08-04:**
adding a clause to the end of §6 law 2 — an edit that changed no meaning — deleted
anchor[4] and took `check-retention-custody-v24.py` from exit 0 to exit 1 on a single
finding. The sentence was restored verbatim and the clarification added after it.

The anchors are deliberate and their rationale is in the checker's own source: a
whole-file digest of a document *"under concurrent edit by other lanes … would
manufacture a false refusal on an unrelated edit while adding nothing, and a digest
recorded for a file under edit is false the moment it is written."* So this record gets
**semantic gates over the sentences that bind, not a byte pin** — §7.2.2's rule applied
correctly, and the reason this file is deliberately *not* pinned the way `v1-slice.md`
now is. Two consequences for anyone editing here:

- **Before rewording §4.5, §5's disposition table, or §6 laws 2 and 6, run
  `python3 -I -B artifacts/check-retention-custody-v24.py`.** Exit 1 naming an
  `anchor[n]` means the edit deleted an anchored sentence; restore it verbatim and put
  new wording adjacent to it, not inside it.
- **The same reasoning is why `v1-slice.md` gets a digest and this file does not.**
  `v1-slice.md` is an accepted, settled product boundary that should not be moving; this
  record is under active multi-lane edit until signature. Pinning the first is rule 1
  working; pinning the second would be the paper seal §7.2.2 warns about.

## 3. Surface disposition ledger

The values in this table are **draft candidates**, not declarations. The Phase-4
signer must replace every “candidate” with the final claim-register disposition
after the last integration run.

Draft capture on 2026-08-03, re-measured live **2026-08-04** by
`python3 -I -B artifacts/check-completeness.py`: contract shape **11/13**,
independent review **13/13**, seal-ready **9/13**, cross-cutting opens **1**
(`R2-FINAL-03`), and product qualification 0/25 demonstrated —
`NOT-RELEASE-QUALIFIED`. The instrument exits 1 on the live cross-cutting open,
which is expected and pre-existing. Re-run; do not freeze this snapshot from
memory.

**Shape and seal-readiness each moved +1 on 2026-08-04, and the move is an
instrument repair, not an artifact change.** An earlier revision recorded
**10/13** and **8/13** and said C-2's 2/4 "cannot be patched away". That was
true of a *regex* and false of a *reader*: `c2-plan-stage-schema.v9` is a
**derivation** whose `derivedFrom.rule` states the effective contract is the
verified predecessor with thirteen listed operations applied *"and nothing else.
No byte of the predecessor is transcribed into this file."* None of the thirteen
touches `stageSchemas` or any of the five fixture arrays, so the delta file
presents no key for a name-based predicate to match — **but the effective
contract carries both**, and resolving the derivation reaches it. C-2 is now
**4/4**. `CMP-IR-01` (§7) carries the full record: the reader detects a
derivation **by shape, never by key name**, fails closed on a digest mismatch,
and was **independently reviewed at 0 blockers** by a reviewer who wrote a third
resolver from scratch and confirmed all three agree byte-for-byte. Exactly one
surface moved.

**Read the 11/13 as a FLOOR, not as a score.** Two surfaces remain below 4/4 —
`TRUSTED-REQUEST-CONTEXT` at **2/4** and `RUST-PROVIDER-PROTOCOL` at **3/4** —
and **neither lost anything an artifact carries.** That is now measured rather
than assumed: RPP carries 6 `semanticConformanceVectors` and TRC carries 30
`adversarialControls` plus a 13-member `capabilityContract`, all invisible to the
instrument because **both predicates scan top-level keys only** and these sit
nested and named outside the alternation. `check-completeness.py` still infers
*"carries a contract schema"* and *"carries goldens"* from **key names** for
**12 of 13** surfaces — it prints that reach itself — so the measurement stays
sensitive to naming rather than to content. Treat contract shape as a weak
instrument, and never read a one-point move as an artifact change without first
checking the key names.

**Seal-ready moved 9 → 8 on 2026-08-03 — out of a denominator that was 11 then
and is 13 now — and the fall is the honest number.** The register's binding
citations were reconciled to the heads in blueprint §1.1 that day; before that it
still bound D9 to `d9-exit-contract.v1.6`, C-2 to `v3`, EVIDENCE to
`evidence.v1`, OPERABILITY to `operability.v2`, VERSIONING to
`versioning-policy.v2`, and `ARCH.RETENTION-TIERS` to the independently
**REJECTED** `retention-tiers.v5`. C-2 then dropped out because reconciling it to
`v4` surfaced `IR-C2V4-01`. **That explanation expired on 2026-08-03**: after the
repoint to `v9`, C-2's open-finding count is **0**, its `sealBlockers` are empty and its `review.ready` is
**True**. **And on 2026-08-04 the last thing holding C-2 out of the seal-ready column — a 2/4
contract-shape score that was an instrument artifact — was removed by repairing the instrument, not the
artifact: C-2 is now 4/4 and seal-ready, taking the figure to 9/13.** See `CMP-IR-01`. **Note carefully
that the 9 above and the 9 today are not the same measurement** and must never be read as a round trip:
the old 9 was out of **11**, measured over superseded artifacts two of which were independently
**REJECTED**; today's is out of **13** over reconciled heads. The fall to 8 was an instrument ceasing to
agree with a stale mirror of itself; the return to 9 is a different surface qualifying for a different
reason.
**The denominator moved separately and for an unrelated reason**, and moved in
the good direction: registering `TRUSTED-REQUEST-CONTEXT` and
`RUST-PROVIDER-PROTOCOL` took the register from eleven measured surfaces to
thirteen. That is a **widening of coverage**, not a regression — two independently
reviewed surfaces the instrument previously could not see are now inside every
figure it prints. Do not compare an `/11` reading to a `/13` reading as though
they were the same measurement.

**Two things this capture still does not say.** First, `check-completeness.py`
measures only the surfaces registered in
[`claim-register.v1.json`](artifacts/claim-register.v1.json), at that register's
`bindingArtifact` and `validator` paths. Those now agree with §1.1, and
`check-package-coherence.py` (`PC-6`) enforces that agreement mechanically each
run — but the figure remains a statement about **registered** surfaces and about
nothing else. An earlier revision of this paragraph said the register carried
eleven surfaces and that `TRUSTED-REQUEST-CONTEXT` and `RUST-PROVIDER-PROTOCOL`
appeared in the ledger below *"with no register claim at all."* **That is no
longer true and is withdrawn:** both are registered — the string
`TRUSTED-REQUEST-CONTEXT` occurs 4× and `RUST-PROVIDER-PROTOCOL` 8× in the
register — the instrument prints **thirteen** surface rows including both, and
both are counted in every figure above. Second, **EVALUATION-PROOF is still not a
registered surface**, so the instrument neither confirms nor contradicts the
defect record below; it is silent on EP. Nothing in the 9/13 figure may be
read as EVALUATION-PROOF being seal-ready — it is not.

Every artifact below is named at its **current head** with the exact SHA-256 an
implementer must build against, and with the verdict of the independent review of
**those exact bytes**. `PASSED` here means one independent reviewer reproduced
the bytes and recorded zero blocking findings; it never means applied, sealed, or
demonstrated. These digests must equal blueprint §1.1.

| Surface | Binding artifact at head — SHA-256 | Independent review of those bytes | Draft freeze disposition | Blocking work before signature |
|---|---|---|---|---|
| D9 | [`d9-exit-contract.v1.14.json`](artifacts/d9-exit-contract.v1.14.json)<br>`8dd3303855f49bfdbb2751ee65f54a906405f0654159ebe815472f73cdf7da31` | **PASSED**, 0 blocking — [review](artifacts/d9-exit-contract.v1.14.review-independent-prefreeze.json); 2 advisories, `R-V114-F1` and `R-V114-F2`, tabled as verifier residuals in §7 | `SEAL` candidate | re-run live adjudication/checker; DELIVERY and RUST-PROVIDER-PROTOCOL joins are bound in §3.2, and RUST-PROVIDER-PROTOCOL's `d9JoinV4` is now pinned one version behind this row — see §3.2 item 6. Observation-to-`faultCause` selection, optional-field presence policy, and the `success`/`policy-failed`/`interrupted` branch remain contract gaps carried by the checker's `referenceDerivation`, not by the JSON. Those three are obtained by **executing** `check-d9-v1.14.py`, whose verified 25-file execution closure and its standing are recorded in blueprint §1.1 note **N-5** and governed by §2 rule 5 and §7.3. Closing them in the D9 JSON itself is a successor's job and is not closed by this record. v1.14's own delta is API/coherence only: cause values are now enum-closed and `hostTerminationUnion.details` carries an explicit no-authority disposition — the derivation is unchanged, all 45 goldens, 4 core-completion rows and 6 reductions rederive identically to v1.13 |
| FACT-PLANE / C-1 | [`fact-plane.v1.json`](artifacts/fact-plane.v1.json)<br>`9057200822c5be59bcf8e691e3755cfa1acf2c89f0b1c2bc89237afaa0925b4d` | **PASSED with changes** — post-adjudication `SEAL-WITH-CHANGES` ([adjudication](artifacts/fact-plane.adjudication-agent-c.json)) | `SEAL` candidate | re-run live adjudication/checker; retained subject-set proof must agree with Phase 1A; declare the sufficiency `view` type and the `rungUnavailableBecause` vocabulary |
| C-2 | [`c2-plan-stage-schema.v9.json`](artifacts/c2-plan-stage-schema.v9.json)<br>`321faeaa3b70c83991f1cceefc9335891d69fa502b3d62cfa133494bb4e9c5a1` | **PASSED — 0 blockers**, 5 non-blocking — [review](artifacts/c2-plan-stage-schema.v9.review-independent.json) `3a411de77332019d910368e2f033cb9f5c60250f11f33180af4476c204df9f6c`, over checker `check-c2-v9.py` `ae9525f1d2efa7688fb6b678e89161f5cf1e3b38f7fd3a9f712c1b6a75be3035` | `SEAL` candidate | **Converged after seven rounds** — v3 `REJECTED`, v4 adjudicated **BLOCKING**, v5 `REJECT`(4), v6 `REJECT`(1), v7 `REJECT`(1), v8 `REJECT`(1), v9 **PASS**. Each round closed a strictly different layer of one defect: the wire comparison (`!= 1`), the census counters, a set-subset test (`{2487} <= {2487.0}`), the **parse** (a duplicate JSON key whose parsed object is byte-identical), the **type** dimension (boolean leaves unenumerated), and finally the **identity** dimension — `document_skeleton` hashed a `/`-join with no escaping, so `{"a":{"b":1}}` and `{"a":{},"a/b":1}` shared a skeleton and an 11-byte reparenting ran fully green. v9's repair is one line: hash `jx_canon(steps)`, which is length-framed and invertible, so injectivity is **proved by the existence of the inverse** and re-executed every run. The reviewer could not break it over **440,495** distinct step lists — 0 collisions, 0 round-trip failures — having re-implemented `jx_canon` from its docstring and got byte-for-byte agreement across all 1124 paths. Float/bool sweep **257 cases, 0 admitted, 0 collateral, 0 hand overrides**, the best in the lineage (v4 admitted 57 of 136). Selftest run to termination **twice**, byte-identical, 203 rows, 0 escapes. **`IR-C2V4-01` is thereby superseded, not withdrawn** — `check-c2-v4.py`'s own census remains falsifiable on its frozen bytes and the population of files pinning the defective `c2-plan-stage-schema.v3.json` `3c488ff6…` **drifts upward and must be re-measured, never quoted** — `grep -rl 3c488ff66a1ec9ab746e99e0701d59460aff3e1d66cd072d9d564a1382b9d285 docs/coop | wc -l` read **84** early on 2026-08-03 and **89** later the same day, because every successor that pins its predecessors inherits the citation (§7.4); §7.2 forbids re-pinning them in place. `subjectScopeCommitment` computation stays owned by the retention/evidence surface (§7.1) |
| RESOLVED-INPUTS | [`resolved-inputs.v2.json`](artifacts/resolved-inputs.v2.json)<br>`0114205aaa5d3f7c0aecc58c10522711aacaa6aa404a41563245627b27b88f43` | **PASSED with changes** — post-adjudication `SEAL-WITH-CHANGES` ([adjudication](artifacts/resolved-inputs.adjudication-agent-c.json)) | `SEAL` candidate | independently rederive `PLAN-ID-V1` (done blind and byte-exact by the consumer-B litmus); preserve CI layer-4 exclusion; supply the missing `capabilityManifestId` derivation, which is a `PLAN-ID-V1` input with no rule |
| VERSIONING | [`versioning-policy.v8.json`](artifacts/versioning-policy.v8.json)<br>`ea4b52b5a4d187ec35ad994d8ffcd888db287566c8fb53f3df17e5203d84ae2e` | **PASSED** — [review](artifacts/versioning-policy.v8.review-independent-cold-rejoin.json) | `SEAL-WITH-CHANGES` candidate | retain provisional/GUESSED support-window label and run-manifest no-breaking-change restriction **Named version divergence, detected 2026-08-03 (not repairable in place).** `versioning-policy.v8` is the head and it is `PASSED`, but its `decisionDependencies[4].source` cites **`artifacts/d9-exit-contract.v1.6.json`** — eight versions behind the D9 head `v1.14`. `check-versioning.py` exits 1 — but on **`versioning-policy.v4.json`**, its hardcoded subject, not on v8 (`VER-DEP`, `B-SCV2-06`); pointed at v8 it raises `AttributeError` and also exits 1, so it is permanently red **by construction** and is not VERSIONING's registered validator. The register names `check-versioning-v8.py`, which exits 0 — see §9.1. It was silent until 2026-08-03 only because the claim register carried the same stale citation: **two instruments wrong in the same direction read as agreement**, the identical mechanism that hid 17 `CHK-5` findings in the architecture prose. §7.2 forbids editing reviewed bytes, so this is recorded rather than patched, and closed only by a successor. **Bounded, not dismissed — and corrected.** An earlier revision of this row justified the bound by citing D9 v1.14's independent review as having re-derived identically "under both versions". **That was a misattribution and is withdrawn:** that review's `crossVersionIdentity` states *"All 55 derived rows are IDENTICAL under **v1.13** and v1.14"*, and the string `v1.6` does not occur in it anywhere. It attests the v1.13→v1.14 step, not the v1.6→v1.14 span this citation crosses. The span was instead **measured directly** while authoring `versioning-policy.v9`: the six `exitClasses` are unchanged with none added or removed; `classToExitCode` is **byte-identical** (`success 0`, `policy-failed 1`, `request-rejected 2`, `indeterminate 3`, `operational-failed 4`, `interrupted 130`) so nothing is renumbered; across 44 shared goldens there are **0** exit-class, reason/error-code and numeric exit-code mismatches; `reasonCodes` and `errorCodes` are byte-identical; v1.14 adds one golden inside the pre-existing `request-rejected` class and removes none. **The additive-only exit-class rule (V4) this row depends on is therefore unaffected — established by measurement, not by the review that was cited for it.** The same shape is recorded for `rust-provider-protocol.v4#d9JoinV4`, which pins `d9-exit-contract.v1.13`. |
| OPERABILITY | [`operability.v10.json`](artifacts/operability.v10.json)<br>`9bacbbf43dfb941a0d87330f79844d395b3ac838ae5bf54026ef4d69681696be` | **PASSED** — [review](artifacts/operability.v10.review-independent-prefreeze.json) | `SEAL-WITH-CHANGES` candidate | preserve assurance-state separation; Phase-1A must make G19 implementable; the six parked identity recipes it records are tabulated in §7.1 and are **blocking**, not residual |
| TRUSTED-REQUEST-CONTEXT | [`trusted-request-context.v3.json`](artifacts/trusted-request-context.v3.json)<br>`bc53c2679a977fd2c2c8369ec9d5794f2295b0df5100b1e360a42c155d04008a` | **PASSED** — [review](artifacts/trusted-request-context.v3.review-independent-prefreeze.json) | `SEAL-WITH-CHANGES` candidate | reconcile with OPERABILITY `REQUEST-ID-V1` in one claim-register pass; the artifact's own `sealRecommendation` is `DO-NOT-SEAL-OR-APPLY` pending that reconciliation, so it binds the host capability shape and not a seal **Checker susceptibility, measured 2026-08-03 (§7.4):** `check-trusted-request-context-v3.py` admits a type-variant respelling at **all three** of its contract's integer leaves and at its one boolean position — `version: 3 → 3.0` yields exit 0, **reproduced independently by the coordinator**. It is the most susceptible surface measured, at 100%. The reviewed contract shape is unaffected and this row's `PASSED` verdict stands on the artifact; what is compromised is the checker's ability to detect a respelled contract. Closed by adopting the canonical-encoding primitive (`c2-plan-stage-schema.v9` (`c2-plan-stage-schema.v6` was **REJECTED**; the primitive landed at v9 as `jx_canon`)) or an equivalent, then a new verdict under §7.2. |
| DELIVERY | [`delivery.v2.json`](artifacts/delivery.v2.json)<br>`47b6cfd17338fafd407c554afe1951ab23d2896aac99bcfd272fc0894e3cabf3` | **PASSED with changes** — reviewer-2 `DO-NOT-SEAL` ([review](artifacts/delivery.v2.review-reviewer2.json)) adjudicated to `SEAL-WITH-CHANGES` ([adjudication](artifacts/delivery.adjudication-agent-b.json)) | `SEAL-WITH-CHANGES` candidate | independently re-review TypeScript worker and external-scanner overlay; no release evidence implied. The Rust substrate fork reviewer-2 named is closed by RUST-PROVIDER-PROTOCOL below, **not** by DELIVERY's five prose keys. `releaseFixtures` expectations are internally inconsistent and must be repaired before they are used as an oracle |
| RUST-PROVIDER-PROTOCOL (v4 overlay + joins) | [`rust-provider-protocol.v4.json`](artifacts/rust-provider-protocol.v4.json)<br>`3e34934720a78f823d3d4c7ceb73735d444f09a4a1ec964a894bd1ac5daf2909`<br>with [`delivery-rust-provider-join.v4.json`](artifacts/delivery-rust-provider-join.v4.json)<br>`02d7c925eceedceafdf70073b6d8e19dfde046b830b25d9187b776e533456146`<br>and [`resolved-inputs-rust-provider-join.v4.json`](artifacts/resolved-inputs-rust-provider-join.v4.json)<br>`4ce77f694df56edbe60a673e6c3c24c916bffe14ec09b4457d943cdc2aa6763e` | **PASSED**, 0 blocking — [review](artifacts/rust-provider-protocol.v4.review-independent-prefreeze.json), over the five v4-lineage subjects itemised in the five-file precision below | `SEAL-WITH-CHANGES` candidate | apply the five v4 files together as the artifact's own `applicationRule` requires; cross-reference from `delivery.v2#rustSemanticSubstrate` so DELIVERY stops appearing to own the Rust wire format; residuals are the unimplemented host adapter, sidecar, platform matrix and corpus. **The normative wire contract is this overlay merged with the v2 base in the row below, and that base carries its own standing `REJECT`** — read that row and the base-rejection record before building the merge; §3.2 item 5 carries the §2 rule 3 resolution |
| RUST-PROVIDER-PROTOCOL (v2 base — merge input, never built alone) | [`rust-provider-protocol.v2.json`](artifacts/rust-provider-protocol.v2.json)<br>`6308a98c1183d75d671655b2a351334b62f4f2c00316983731ceabb86e90793b` | **`REJECT`, 2 blocking, on these exact bytes** — [review](artifacts/rust-provider-protocol.v2.review-independent-prefreeze.json), which binds this digest with `sha256AtStart == sha256AtEnd` and `stable: true`. Both blockers are adjudicated **`DISCHARGED-BY-V4`** — [adjudication](artifacts/rust-provider-protocol.v2-blockers.adjudication.json) — **by deletion**, not by argument | **no seal disposition of its own** — it is a merge input, not a surface to build | the row above carries the disposition for the merged contract. Do **not** implement these bytes alone; §2 rule 3 forbids it and §3.2 item 5 records why the *merge* is nonetheless normative. `PC-7` (§9.1) fires on this row and will keep firing until a successor stops pinning these bytes |
| EVIDENCE | [`evidence.v10.json`](artifacts/evidence.v10.json)<br>`62a3a07194062c8499f6e943b4986d7a77bdecc0c4ec499851ac078fd548e9b4` plus Phase-1A result | **PASSED**, 0 blocking — [review](artifacts/evidence.v10.review-independent-prefreeze.json), which is itself `DO-NOT-SEAL` / `CANDIDATE-NOT-APPLIED` / `integrationAuthorized: false`. The independently reviewed successor this row previously demanded now exists; `evidence.v8` and `evidence.v9` were both `REJECTED` and are history. 3 non-blocking findings `EV10-IR-01`..`03` are tabled as verifier residuals in §7 | **UNSET — BLOCKS FREEZE** | v10 closes the *review* obligation and makes the wire grammar, the five `…V1` record types and the store/API boundary portable (blueprint §1.1 note **N-3**). It closes **no identity recipe**: it defines no `EvidenceBundle`, `EvaluationEvidence`, `SubjectSetCommitment`, `outcomeSetDigest` or subject-set Merkle framing at all; it imports `universeCommitment` and `outcomeSetCommitment` by equality from an unapplied `evaluation-proof.v8` vector whose companion checker carries the defect recorded below; and it states in its own residuals that the v5/v6/v8/v9 `EvidenceDigest`, `RunId`, `TerminalRun` and `runSeal` identities are **unchanged** — it repaired verifier totality, not identity. `EvidenceDigest`, `universeCommitment`, `outcomeSetDigest` and the subject-set Merkle framing therefore remain parked under §7.1 and must still become reproducible byte recipes in a binding artifact. Also still required: exact proof/verification-closure/cost-residual reconciliation, the §3.1 Phase-1A packet, and the final claim-register seal. Note v10 deliberately pins `d9-exit-contract.v1.13`, not the D9 head in this table |
| FACT-IDENTITY | [`fact-identity-policy.v2.json`](artifacts/fact-identity-policy.v2.json)<br>`10055004e6919a55b29c38d9c474857280fbbb6f561dfff6ed88b7e54efbd110` + [closure](artifacts/fact-identity-policy.freeze-closure-coordinator.v1.json)<br>`2aee126e78b5d709a6d64028b502bd0199383561d43fc7cf5ec7fe2c69ac16d7` | **PASSED with changes** — reviewer-2 `DO-NOT-SEAL` ([review](artifacts/fact-identity-policy.v2.review-reviewer2.json)) adjudicated to `SEAL-WITH-CHANGES` by the closure | `SEAL-WITH-CHANGES` candidate | residuals only: `FI-CORPUS-EVIDENCE`, `FI-PARK-IMPERATIVE-AUTHORITY`; re-run live claim reconciliation |
| R-1 | [`r1-lifetime-neutrality.conformance.v1.5.json`](artifacts/r1-lifetime-neutrality.conformance.v1.5.json)<br>`557b9f973c22b7ea959a884f56d5bac81c5383e227cac73a47605c1be317a815` + [closure](artifacts/r1-lifetime-neutrality.freeze-closure-coordinator.v1.json)<br>`6bf90f21178007a2df2313a18d230cf0d3b8f309dd2937c5668603b27a11569d` | **PASSED** — [review](artifacts/r1-lifetime-neutrality.conformance.v1.5.review-independent-prefreeze.json) | `SEAL-WITH-CHANGES` candidate | residuals only: `R1-PARK-RESIDENCY`, `R1-PARK-RUNTIME-DENIAL`; re-run live claim reconciliation. `LN-13` (`EvidenceDigest` stable across `ExecutionId`) stays unverifiable until §7.1 closes, and `policyOutcome.derivationDigest` needs a recipe **Checker susceptibility, measured 2026-08-03 (§7.4):** `check-r1-v1.5.py` bans floats at the parser — 0 of 64 float positions admit — but leaves **40 of 52 boolean positions** open. It is the clearest instance of the corpus-wide asymmetry §7.4 records: authors who thought about `1.0` did not think about `True`. The reviewed contract shape is unaffected; the checker's detection of a respelled contract is. Same closure path as TRUSTED-REQUEST-CONTEXT. |
| TM | [`threat-model.v3.json`](artifacts/threat-model.v3.json)<br>`56734a4047b61e1fc702f75ccb21e8721b334adb449093d266756d0b08adc499` plus Phase-1A result | **PARTIAL** — reviewer-1 `SEAL-WITH-CHANGES`, reviewer-2 `DO-NOT-SEAL`, adjudicated `DO-NOT-SEAL` on the V10 choice alone ([adjudication](artifacts/threat-model.adjudication-agent-b.json)) | **UNSET — BLOCKS FREEZE** | ~~independently re-review physical ProjectId namespace~~ — **PERFORMED 2026-08-04, returned [`REJECT` at 3 blockers](artifacts/threat-model.v3.storage-namespace.review-independent.json)**, scoped to `$.storageNamespace` and deliberately excluding the five `PI-*` runtime observations (release-gated under G14, `demonstrationEvidenceIds` empty), so the verdict quantifies over nothing it cannot observe. **The condition is now bounded rather than open**, and the finding is one structural property: **the physical namespace is a pair `(admitted root, ProjectId)`, and only the `ProjectId` half is governed.** `ProjectId` is total, injective, collision-free, and — verified — a persisted CSPRNG allocation never derived from mutable state, so renaming a directory does **not** orphan artifacts. The **root** half is bound by no rule: `SN-IR-01` `activeRootId` has **zero specified consumers corpus-wide** (measured: 3 occurrences total — the field list, this review, and the checker's assertion *about* that list), and record creation is specified nowhere; `SN-IR-02` `rootId` uniqueness is a create-time **procedure**, never a property — *"unique" occurs 0 times in the subtree* — so **copying a root duplicates it**, and the namespace layer lacks the collision rule its own identity owner already has; `SN-IR-03` the purge commit renames `projects/<ProjectId>` into `quarantine/` but **nothing requires an admitted root be one filesystem** — the artifact writes *"on the single user-state filesystem"* for the *authority-record* rename and omits it for the more critical one, so a nested mount yields `EXDEV`, for which the closed 6-row recovery table has **no transition** (`EXDEV` occurs 0 times). Repairs are proposed as properties, not call-site lists — chiefly *make `activeRootId` dispositive and `activeRootCanonicalPath` an advisory hint*. Attacks the design **defeated** are recorded too: case-insensitivity (probed on this host, which does fold `Foo`/`foo`; immune because every component is lowercase-ASCII, making case-folding the identity function), unicode normalisation, and traversal. **This review raises the second `PC-7` finding (§9.1) and that is correct.** **A candidate repair now exists — `artifacts/threat-model-storage-namespace.v4.json` (`94b68f6d…`), `CANDIDATE-NOT-APPLIED`, `AWAITING-INDEPENDENT-REVIEW`, binds nothing.** *(Named without a markdown link, deliberately. `check-package-coherence.py` reads the **link set of a §3 row as that row's binding-artifact set** — an earlier revision linked it and correctly drew `PC-2-NO-DIGEST` and `PC-3-ARTIFACT-ONLY-IN-FREEZE`, because the freeze was then declaring a candidate as binding for TM. **The available fix that turns both findings green — record its digest here and add it to blueprint §1.1 — is the wrong one**: it would promote a `NOT-APPLIED` candidate to binding in order to quiet an instrument, which is the paper seal §2 rule 3 and §4.4 exist to prevent. A candidate is cited by path, never linked, until a reviewer accepts it and a coordinator applies it.)* It is a **machine-resolvable derivation** (12 `set` + 1 `add`), verified with `check-completeness.py`'s own `resolve_derivation()` at 0 errors with only `rootBinding` added and every closed collection byte-identical. **It found one cause beneath all three symptoms:** `PROJECT-ID-V1` is collision-safe because its identity carries **two** custody records — marker *and* registry — with a uniqueness constraint between them, and callers may not supply it; **`rootId` carried one.** `SN-P2` supplies the second **without inventing a store**, because the authority-record set already *is* the registry the predecessor names. The three repairs are properties: `SN-P1` makes resolution **unary** — not *"compare the root against `activeRootId`"* but *there is no argument position for a root*; `SN-P2` states uniqueness as a **function-invariant** of the record set (`activeRootId → activeRootCanonicalPath`), **explicitly rejecting the reviewer's own proposed "equal `rootId`, different path" criterion because it re-promotes the path one clause after demoting it**; `SN-P3` states one-device **once**, at `pathSafety.resolution`, and **retypes rather than extends** `pathSafety.unsupported` — atomic rename is a capability of the ordered `(source, target)` pair, so a cross-device pair simply lacks it and no predicate was added. **All three failing scenarios were executed, not argued.** The decoy-root split: the predecessor returned `RESOLVED` with an **empty read-set of the authority record**, reproducing dynamically what the review found statically; the successor returned `STORAGE_ROOT_IDENTITY_MISMATCH` **even with the advisory hint repointed at the decoy**, which is the test separating a dispositive identity from an authoritative path. The copied root: a real `cp -r` reproduced `rootId` byte-for-byte, predecessor `RESOLVED`, successor `STORAGE_ROOT_COLLISION` — while the same root *moved* returned `STORAGE_ROOT_LOCATOR_STALE`, so the rule **discriminates rather than refusing both**. The nested mount: a real 12 MiB HFS+ mount at `projects/<ProjectId>` produced **errno 18 `EXDEV`**, and admission returned `STORAGE_ROOT_NOT_ONE_DEVICE` before any user-derived write. **It also refined the review**: a mount point can present as `EBUSY` rather than `EXDEV`, so binding the rule to one errno *"would have been the law-18 mistake in another register."* **The recovery table's closure is now stated as a property** — both tables are total over (reachable durable nonterminal state × path-presence tuple) with **durable state as the domain**, so a further row is admissible **iff** `reachableDurableNonterminalStates` gains a member and an operation persisting nothing contributes no point; purge stays 6 rows, migration 10, with the falsification condition written down. **Honest bounds it states against itself:** `rootBinding` is **unenforced** — deliberately, since adding to `storageNamespace.fixtures` would break the pinned checker on application and the author may not write one, so `checkerImpact` names the six assertions a successor checker must carry — and deleting `rootBinding` entirely **changed no checker output**, which the author reports as *measuring* its own paper-seal disclosure rather than asserting it. **This does not clear TM.** Still open and untouched: reconcile V10/custody and G19; preserve publication block until demonstrated |
**Five-file precision, RUST-PROVIDER-PROTOCOL — which five, exactly.** The v4 review
bound five subjects and they are **all v4-lineage**. Its `scope.candidateSet` and
`exactByteReviewBasis.subjects` agree and list, verbatim and re-read for this entry:

1. `rust-provider-protocol.v4.json`
2. `check-rust-provider-protocol-v4.py`
3. `rust-provider-protocol.v4.adjudication-v3-rejection-response.json`
4. `delivery-rust-provider-join.v4.json`
5. `resolved-inputs-rust-provider-join.v4.json`

**The base `rust-provider-protocol.v2.json` is not among them — the string `6308a98c`
occurs zero times in the review artifact, re-measured 2026-08-04.** So "five files" is
never "the four artifacts in the ledger plus the base": two of the five are a *checker*
and an *adjudication*, which are not files an implementer applies at all. What the
review did with the base was reconstruct its retained ordered projection (18
protocol-v2 selectors, `compactOrderedCommitmentsMatched: true`); the base is
byte-pinned by the overlay itself. §3.2 item 7's wording — *"all five **v4** files"* —
and `rust-provider-protocol.v4#narrowJoinReferencesV4.applicationRule`'s *"All five
exact v4 files"* both agree with the review.

**Where the uncorrected phrase actually is, corrected 2026-08-04.** An earlier revision
of this paragraph opened *"This row's phrase 'the exact five-file set' sits beside a
list of four files."* Measured: the string `the exact five-file set` occurs **zero**
times in this record and **once** in
[`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1, in the
RUST-PROVIDER-PROTOCOL (overlay) row. The correction had been written into the document
that did not contain the defect, so the live occurrence went on reading as though the
five were the five bytes you build. Blueprint §1.1's row now names the five explicitly;
this paragraph is the itemisation both documents point at.

**Base-rejection record, RUST-PROVIDER-PROTOCOL — disclosed 2026-08-04.** The base
this row pins, `rust-provider-protocol.v2.json` (`6308a98c…`), carries a standing
independent **`REJECT`** on those exact bytes, and until this entry neither this record
nor the blueprint said so: the review's filename and the string `RPPV2-PF` each
occurred **zero** times in both documents.
[The review](artifacts/rust-provider-protocol.v2.review-independent-prefreeze.json)
binds that digest with `sha256AtStart == sha256AtEnd` and `stable: true`, records
`blockingFindingCount: 2`, and states its `effect` as *"The five-file v2 set must
remain CANDIDATE-NOT-APPLIED. It must not replace v1, enter architecture freeze, or be
used as implementation authority."* The two blockers are
`RPPV2-PF-01-TRANSITION-AST-GRAMMAR-UNDERBOUND` and
`RPPV2-PF-02-HOST-FINALIZER-CONTEXT-CANNOT-DERIVE-EXACT-D9`, both `SOUNDNESS-BLOCKING`.
That silence is the defect the gating implementer litmus returned `LITMUS-FAIL` on, and
`PC-7` (§9.1) is the instrument built from it.

**Both blockers are adjudicated `DISCHARGED-BY-V4`, and the measurement is
negative-space.**
[The adjudication](artifacts/rust-provider-protocol.v2-blockers.adjudication.json) is
`INDEPENDENT-ADJUDICATION-EVIDENCE`: it applies nothing, seals nothing, and does not
supersede the `REJECT`, which stands as the verdict on the five-file **v2** set. It
grades each finding against that finding's own `requiredRepair`, and its decisive step
is to locate every surface the findings named as **defective** and ask whether it
survives the merge. None does. `RPPV2-PF-01`'s defect is
`#/orderingAndStateMachine/transitionAstV2`; `/orderingAndStateMachine` is one of the
overlay's eight `replacedSelectors`, and `transitionAstV2` occurs nowhere in
`orderingAndStateMachineV4`. `RPPV2-PF-02`'s defects are `#/hostFinalizerContextV2`,
`#/hostFinalizerProjection` and `#/exhaustivenessRule` — which are, exactly and
entirely, `delivery-rust-provider-join.v4.json`'s `replacedSelectors` list. **Not one of
the 18 inherited selectors was ever a blocking surface.** Re-verified against the live
bytes for this entry, not taken from any artifact's self-description.

**The findings were driven, not argued.** The adjudicator built an AST validator from
the merged bytes alone, never reading the authored checker, and logged **0 forced
inventions and 0 shape violations** across all 28 `transitionRulesV4` and 5
`stateInvariantsV4` — the exact experiment `PF-01` said could only agree *"after the
reviewer invented per-operator schemas and semantics."* For `PF-02` it imported
`check-d9-v1.14.py` and used that checker's **own** `derive_class` / `derive_codes`:
**148 of 148** admitted finalizer contexts derived a complete, unique D9 termination —
**0** missing axes, **0** contexts with no matching rule, **0** non-unique terminations —
and the 2,156-member invalid complement rejected without deferral.

**Premise correction — `#/schemaLanguage/maps` is a yardstick citation, not a defect
citation.** `/schemaLanguage` is inherited **unreplaced**, and an earlier reading treated
that as showing the overlay does not touch what `PF-01` is about. That is backwards. The
finding's own words are: *"The protocol's own schemaLanguage says a closed map has exact
required and optional fields, but transitionAstV2 supplies no such grammar for these
records."* `schemaLanguage` is the standard and `transitionAstV2` is the thing that
failed it, so inheriting it unchanged is **correct** — the overlay's obligation was to
*satisfy* that rule, not to amend it, and the merged AST now meets it at 0 inventions.
Measured: v2's `schemaLanguage` (`maps`, `arrays`, `integer`, `text`, `bytes`,
`external`, `union`) and v4's additive `schemaLanguageV4` (`closedMap`, `taggedUnion`,
`exactType`, `array`, `referencePathGrammar`, `recursiveBounds`, `artifactFailure`,
`runtimeFailure`) share **zero** key names, so there is no collision and no precedence
question to resolve.

**Why no artifact formally closes the two ids — the mechanism, not an incident
(`OBS-4`).** `rust-provider-protocol.v4.json`'s own `dependencyPins` pins the v2 review
at `52cf1b32…` with role *"binding independent REJECT and exact two-finding repair
authority"*: the producer knew exactly what it was repairing. Its independent reviewer
never had that review in scope — the v4 review's `scope.candidateSet` is all-v4-lineage,
and `6308a98c`, `RPPV2-PF` and `v2.review-independent-prefreeze` each occur **zero**
times in it. The ids fell through the gap between a producer that named them and a
reviewer whose `decisionRule` did not enumerate them. **The counterweight is what the
discharge actually rests on:** that same reviewer independently measured the two demanded
properties item for item without ever using the ids —
`independentReconstruction.hostFinalizer.exactD9ClassCodesExitDerived: 148` and
`forbiddenDeferPreserveUnknownResults: 0`, and `independentReconstruction.typedAst`
`rules: 28`, `guardOps: 15`, `invariants: 5`, `allRulesBehaviorallyCovered: true` — and
the adjudicator's own numbers reproduce every one of them. The discharge rests on that
measurement, not on the naming.

**`OBS-3` — merge-binding granularity is asymmetric; non-blocking.** Both v4 joins
publish per-selector commitments and both recompute exactly:
`delivery-rust-provider-join.v4.json#retainedV2SemanticProjection.inheritedSelectorSha256`
carries **10** rows (10 of 10 verified) and
`resolved-inputs-rust-provider-join.v4.json#exactSemanticProjectionOfV2.selectorCommitments`
carries **13** (13 of 13). The protocol overlay publishes **none** —
`inheritedSelectorSha256`, `selectorCommitments` and `compactOrderedJsonSha256` each
occur zero times in `rust-provider-protocol.v4.json` — yet the v4 review reports a single
`compactOrderedCommitmentsMatched: true` spanning all **41** selectors (18 + 10 + 13).
Value equality for the protocol's 18 is still guaranteed by the whole-file `6308a98c`
pin, so this is not a soundness gap; but the protocol is the one place where
selector-level drift could not be localised from published bytes, and it is the largest
of the three inherited sets.

**`PC-7` fires on this row and will keep firing.** It tests the pinned artifact's
**review outcome**, not this record's prose, so no wording here can quiet it — and it
must not be narrowed to make the console green. What the disclosure changes is that its
firing is now **informative rather than misleading**: a reader who hits it finds the
`REJECT`, the discharge and the §3.2 item 5 rule-3 resolution recorded in both documents
instead of finding nothing at all. Its cost is real and a signer must meet it with its
cause — `check-package-coherence.py` exits **1** on this single finding, and its
`--selftest` refuses the suite with `SELFTEST-REFUSED: base is dirty` at **0 of 9
mutations executed**. Both are recorded against §9.1's checkbox. Closing them is
successor work: a RUST-PROVIDER-PROTOCOL successor that states the whole contract in its
own bytes and stops pinning rejected ones.

**Scope of this entry.** It corrects the record and nothing else. It does not apply the
v4 five-file set, which remains `CANDIDATE-NOT-APPLIED` under §3.2 item 7; it does not
supersede the v2 `REJECT`; it does not touch the stale `d9-exit-contract.v1.13` pin of
§3.2 item 6, which the adjudication measured as semantically safe for the finalizer axes
but explicitly did not close; and `CD-RT-5` remains `BLOCKED_ON_PHASE_1A`.

| PRODUCT | [`product-dispositions.v1.json`](artifacts/product-dispositions.v1.json)<br>`b9a87839606981a5be46f62aca2d85a17c3da5082c8d0aad02a211f3025fd91c` | binding product packet | decided rows are frozen per §5 | `CD-RT-5` remains **blocked**; no artifact in this repository may amend it |
| CLAIMS | [`claim-register.v1.json`](artifacts/claim-register.v1.json)<br>`1a16f7510a9ab3347c5dae2a6d2c2c7b846ed3dfcdc6a582bb545cb44e8f3df9` | per-claim status register | not a surface | final reconciliation against every row above |

Independently `PASSED` but **explicitly unapplied** Phase-1A candidates, recorded
so their existence is visible and escalable and for no other purpose:

| Candidate | SHA-256 | Independent review | Standing |
|---|---|---|---|
| [`retention-tiers.v24.json`](artifacts/retention-tiers.v24.json) | `ba29c115a9064ab1cd66ea01751b238acf092b3d699ca43027de7a8dfe55a277` | **PASSED — both parts, 0 blockers** — [review](artifacts/retention-tiers.v24.review-independent.json) `633301d5fb6400858a1e10acca50aefe8e58502ef346d5f3d06f6da5cff0084a`, over checker `check-retention-custody-v24.py` `9a309302df6d2f1108f1fbfb4978bfc93b102eb0394c99ba7be7fc550d7fa909` | `CANDIDATE-NOT-APPLIED`. Not the §3.1 insertion. **Does not close `CD-RT-5`** — it selects no retention default, and `durableDefault` remains `UNSELECTED` in its own bytes. | **Carries the V10 item-3 discharge** (§4.6). Part B is carried byte-identically from v23 — canonical `sha256:199b55e1…`, verified independently by the reviewer — and v24 **enforces `predecessorPartBVerdictAppliesToTheseBytes: false`**, refusing to inherit its own predecessor's verdict because the instrument and the shared base both changed. The reviewer re-earned it and named which part it inherited. Part A repairs `IR-RT23-01` by **measuring** the PLAN-ID-V1 closure rather than enumerating it: 191 positions probed, 39 refused, 152 admitted, 0 admitted positions leaving the PlanId unchanged. Two non-blocking corrections stand against it — a **sixth** open sub-structure (`$.resolvedConfiguration[*].value`, which the contract closes to four keys while putting **no type** on `value`), so the published count of five understates; and `RT24-A-RES-08` states its own error in the wrong **direction** — its one checker-side literal `STAGE_KEYS` (9 keys) is *narrower* than the live `c2-plan-stage-schema.v4#stageSchemas` (12), so it **understates** the admitting set rather than overstating it. Neither blocks, because `RT24-A-INV-08` is universally quantified over any preimage position — the repair v23's reviewer prescribed. |
| [`evaluation-proof.v13.json`](artifacts/evaluation-proof.v13.json) | `1497e8872217e7f2b196888483d2e443d25d554a3023c3bcede9e5722d0c5abe` | **PASSED** — `PASS-WITH-RESIDUALS`, **0 blockers**, 7 non-blocking observations — [review](artifacts/ep13.review-independent.json) `c7b80c396caa51d67db5fbade110f7ff1ade44c962b50de9bfc905a2b585d53d`, over checker `check-evaluation-proof-v13.py` `0de5b5bfe16dcee539abcfd9f10de74062c90582fb0eeaebb92b52e33f3e04a1` | `CANDIDATE-NOT-APPLIED`. Not the §3.1 insertion. Does not close `CD-RT-5`. | **Converged after five rounds** — v9 `REJECT`(2), v10 `REJECT`(1), v11 `REJECT`(2), v12 `REJECT`(1), v13 **PASS**. Each round established a strictly different property: v9 that the guard exists **in source**; v10 that a **call** was made; v11 that the **seat** named the repaired module; v12 that the returned value **is** the anchored object, compared by `is`; v13 that the published **scope** is a characterisation of the class rather than a list of variant names. The reviewer that routed the gate built its own `MD2`/`MD3` and reproduced the v12 defeat exactly (stdout byte-identical to an honest run), then found a **fourth** means of distinguishing (`SB-MD6`) which routes the accept/reject gate itself and is disclosed as `IR-EP13-NB-01`. It ruled the terminus acceptable on a stated test — *does a reader applying the published boundary draw a false conclusion?* — and recorded that **v13 nowhere claims the class is unclosable**, so rejecting it for not closing a hole it never claimed to close would be rejecting it for accuracy. The disclosure is **enforced, not intended**: a declared escape that is ever *caught* raises a finding, so the live escape cannot be retired by quietly breaking it. **The v8 defect record below stands as history** and is superseded, not withdrawn: `check-evaluation-proof-v8.py` still admits a wrong plan identity on its own frozen bytes, and seven `evaluation-proof` versions still pin the defective C-2 v3 bytes (§7.2 forbids re-pinning in place). **CRITICAL — v13 DOES NOT SUPERSEDE v8 FOR V10, and the two are not interchangeable.** Measured 2026-08-03 while authoring the V10 disposition, and independently reproduced by the coordinator: the `evaluation-proof` lineage **changed the claim it serves at v10**. `evaluation-proof.v8` carries `claimId: EVIDENCE` with `proofObligationsByClaimShape` — a closed six-shape map (local-match, relationship-match, aggregate-match, no-match, indeterminate, error) with 7 positive vectors. `v10` through `v13` carry **zero** occurrences of `no-match`, `relationship` or `proofObligationsByClaimShape`; the coverage is present through v9 and drops at v10, while each of v10..v13 declares `supersedesProofObligationsOf` its predecessor. The `claimId` moves separately and later: v8..v11 carry `EVIDENCE`, and the switch to `CD-RT-5` happens at **v12** — measured, after an earlier revision of this row wrongly placed it at v10. **The obligations lapse two versions before the declared claim changes**, which is why neither signal alone would have caught it. **The v10..v13 chain repairs C-2 join answer-provenance; it does not carry the claim-shape proof obligations V10's `requiredResolution` item 1 names.** The corpus already resolved this correctly on its own: `evidence.v10` pins `evaluation-proof.v8` and **not** the chain head. So `v13` is the head of the provenance lineage and `v8` remains the artifact discharging V10 item 1; neither is stale and a signer must not read one as replacing the other. |

**Defect record — `check-evaluation-proof-v8.py` (`c80ac50e21dcd350e5f5285958a6cfb94d52c5c3f7d64f2396d91b544fa82769`), recorded 2026-08-02.**
The `evaluation-proof.v8.json` *artifact* passed independent cold-reconstruction
review and that verdict stands on those bytes. The defect is in the companion
**checker**, which is not merely an instrument: its `authorize_evaluation` is the
reference realization of admission, and an implementer reading it for the
admission shape would reproduce the defect.

Executing the frozen bytes, `authorize_evaluation` **admits** a candidate whose
`frozenPlanIntent.schemaVersion` is JSON `true` and mints a complete, durable,
cold-reconstructible `AdmittedEvaluationAuthorityV1` over the **wrong plan
identity** — `sha256:5d748405d6d02ad460c54b078edfd6a627d6bd5273c41e7ba5febdd6153020d9`
in place of the true `sha256:7c3174f6358f40a36f19b97eab6b247086f7a5411141fb9ee056535904fa7a85`.
C-2 v4 rejects that same `PlanIntent` with `C2I-02`. An independent reviewer
reproduced it as an honest **producer** — changing one wire value and recomputing
every derived field with the pinned encoders — so it is not an artifact of a
private path or a hand-built candidate. Three durable identities move beneath a
**byte-identical** `EvaluationAuthoritySealRef`, and the reconstructed store still
returns `assert_store_continuity() == True`.

Root cause is the `LB-C2-01` equivalence class, now closed as an architecture
requirement by **§6 law 18**. Two things follow, and they are different:

- **The architecture gap is closed.** No successor may admit a type-variant
  closed scalar, and no identity may be derived from an ungated admission record.
- **The verifier residual is not.** `check-evaluation-proof-v8.py` is a pinned
  predecessor; repairing it in place would break every checker that pins it and
  would violate §7.2. The repair is a successor that gates above it. The first
  successor attempt, `evaluation-proof.v9`, was **REJECTED** — 2 blockers
  ([review](artifacts/ep9.review-independent.json),
  `46b244235321c8a36549d0b92ebf843b1561ea6c37a5a7bcc49a498f7899c8cf`) — for
  asserting an identity-inertness mitigation that is false, and for an AST scan
  that was the sole guard for its central routing property. **EVALUATION-PROOF is
  therefore not seal-ready**, and no seal disposition may cite `v8` as if the
  companion checker were sound.

Listing a candidate is not accepting it. §3.1 still requires an accepted,
independently reviewed Phase-1A packet, and §5's `CD-RT-5` row is unchanged.

The following are not legal final table values: `OPEN`, `REOPENED` without a
freeze disposition, “implementable therefore sealed,” or an unnamed residual.

### 3.1 Phase-1A insertion — mandatory

Before signature, insert all of the following from the accepted, independently
reviewed Phase-1A packet:

- exact evaluation-proof model for match, no-match, indeterminate/error, and
  verdict claims;
- exact retained objects for independent verification or regeneration;
- selected default custody/retention behavior, including whether any retention is
  implicit;
- immutable sealed assurance versus mutable external availability;
- typed degradation/unavailability behavior after expiry or purge;
- purge/deletion semantics that do not rewrite a sealed Run;
- the resulting EVIDENCE, TM, OPERABILITY G19, VERSIONING, and claim-register
  reconciliation; and
- independent review plus a retained checker/mutation suite.

`A1-RTV4-02` may remain a named measurement residual. Absence of a proof/custody
decision may not.

An embedded “product sign-off” assertion authored by the retention candidate
does not close `CD-RT-5`. The binding product packet must be explicitly amended
or adjudicated by product authority after independent Phase-1A review.

### 3.2 Cross-contract joins — bound

DELIVERY's `terminationIntegration` binds the joins without creating a second
public vocabulary:

1. A provider framing/integrity/handshake/closed-protocol fault maps to D9
   `faultCause=provider-protocol` and public
   `errorCode=PROVIDER.PROTOCOL_VIOLATION`.
2. An excluded capability form retains domain reason
   `FEATURE.REQUIRES_CAPABILITY_RUNTIME` in rejection details and maps to D9
   `rejectionCause=extension-admission-rejected` and public
   `errorCode=EXTENSION.ADMISSION_REJECTED`.
3. A C-2-valid but v1-excluded external scanner retains domain reason
   `FEATURE.EXTERNAL_SCANNER_NOT_IN_V1` and maps to the same existing D9
   rejection cause/code. This is a product-overlay rejection, not a claim that
   the scanner required `ARCH.PROBE-CONTRACT`.
4. A valid provider `Unavailable` or deterministic `BudgetExhausted` is exact
   Coverage; a malformed/partial protocol or crash is provider-protocol; and a
   signed-profile artifact that is missing or unspawnable is delivery-required.

The retained DELIVERY checker cross-checks these values against the live D9
artifact. Implementation may not add another spelling.

RUST-PROVIDER-PROTOCOL binds the Rust half of join 1 and 4 at the byte level,
which DELIVERY does not:

5. The normative wire contract for the `rustc_driver` sidecar is
   `rust-provider-protocol.v2.json` merged with the `rust-provider-protocol.v4.json`
   overlay under the v4 artifact's own `retainedV2SemanticProjection.mergeAlgorithm`
   (see blueprint §1.1 note **N-2**). `delivery.v2#rustSemanticSubstrate.providerProtocol`
   states that the boundary exists; it does not specify framing, and it is not the
   byte authority. Where the two describe the same value, RUST-PROVIDER-PROTOCOL
   governs the bytes and DELIVERY governs packaging, pinning and supply chain.
   Adopting the TypeScript `wireSchema` for the Rust sidecar is an architecture
   change, not an implementation choice.

   **§2 rule 3 versus this item — resolved, not papered over.** Rule 3 reads *"A
   version whose independent review is `REJECTED` is not normative and must not be
   implemented, and its superseded predecessors do not become a fallback,"* and
   `rust-provider-protocol.v2.json` carries exactly such a review — `REJECT`, 2
   blocking, on its exact digest (§3, base-rejection record). This item names those
   bytes as half the wire contract, so the two read as contradicting each other, and
   **rule 5's carve-out does not reach the case**: rule 5 scopes *"the files a
   retained checker verifies and executes inside itself,"* predecessors that *"remain
   runtime inputs of the instrument and acquire no normative standing from being
   executed."* The base is not a runtime input of an instrument here; it is a merge
   input to the contract an implementer implements. The tension is therefore genuine
   and textual, and this is its resolution.

   **What is normative is the *merged* contract, not the base bytes.** Every surface
   either v2 blocker named as defective is a **replaced** selector and is deleted by
   the merge — `PF-01`'s `transitionAstV2` with `/orderingAndStateMachine`, and
   `PF-02`'s three finalizer selectors as the delivery join's entire `replacedSelectors`
   list. The base contributes only its 18 inherited selectors, and **not one of them was
   ever a blocking surface**. So no `REJECTED` version is implemented and no predecessor
   becomes a fallback: the version implemented is the merge, which carries neither
   blocker, and the v2 review's own `effect` is scoped to *"the five-file v2 set,"* which
   the merged contract is not. What made this legible as a rule-3 violation was **a bare
   digest pin of rejected bytes with no statement of what survives the merge** — the pin
   was correct and the silence was the defect. Read this narrowly: it holds because the
   discharge was measured selector-by-selector in §3, and it licenses nothing for any
   other rejected artifact.
6. `delivery-rust-provider-join.v4.json#hostFinalizerBoundaryV4` binds the
   finalizer side: the host validates the normalized provider fate and complete
   host-owned base D9 axes, recomputes the final axes and the exact D9
   termination, and **never** accepts a provider-produced class, code, or axis.
   `rust-provider-protocol.v4#d9JoinV4` pins its D9 counterpart to
   `d9-exit-contract.v1.13.json` at `fc2c546a…`.

   **Detected divergence, recorded rather than papered over.** `fc2c546a…` is now
   the D9 **predecessor**; §3 records the head as `d9-exit-contract.v1.14.json` at
   `8dd33038…`. The join is one version behind, and it may not be repaired here:
   editing `rust-provider-protocol.v4.json` would void the five-file `PASSED`
   verdict under §7.2, and re-pinning is successor work. Two facts bound the
   exposure and neither discharges it. The v1.14 independent review re-derived all
   45 goldens, 4 retained core-completion rows and 6 pre-reduction reductions
   **identically under v1.13 and v1.14**, so the axes-to-class derivation this join
   depends on has not moved — the divergence is in the pin, not the semantics. But
   v1.14's own delta closes the pre-reduction cause enums and strips `details` of
   any authority, and a join pinned to v1.13 does not carry those. An implementer
   implements the join rule against the §3 head and escalates the stale pin under
   §8; a signer may not treat this row as self-consistent until a
   RUST-PROVIDER-PROTOCOL successor re-pins it. The same stale pin exists in
   `evidence.v10` (see the EVIDENCE row), which discloses it deliberately.
7. All five v4 files were reviewed and passed as one set, and the artifact's own
   `applicationRule` requires them to be applied together. Applying a subset is
   prohibited.

## 4. Accepted v1 product slice

The detailed authority is [`v1-slice.md`](v1-slice.md) at SHA-256
`6b8717fef545fe73f0de5879a7389fbc0c7c499c70e06b344789e5150478bee3` — the pin
recorded in §2, which is what makes this sentence's word *authority* true under §2
rule 1 rather than merely asserted. Recompute it before relying on this section;
if it differs, that is a §8 detected conflict and a §10 delta, not a stale digest
to overwrite. The implementation milestone is one local, deterministic,
offline-capable path:

> mint `RequestId` → resolve and validate closed `PlanIntent` → admit attempt →
> capture immutable Snapshot → derive and verify `PLAN-ID-V1` and facts with exact Coverage → evaluate bundled declarative
> rules and policy in the pure core → assemble the Phase-1A proof → seal an
> authoritative Run → derive D9 termination → inspect it from a second process.

### 4.1 Required

- one-shot Rust CLI/orchestration host and lifetime-neutral pure Rust core;
- host-owned `REQUEST-ID-V1`, persisted `PROJECT-ID-V1`, exact
  `SNAPSHOT-ID-V1`, closed pre-admission C-2 `PlanIntent`, and independently
  verifiable `PLAN-ID-V1` derivation;
- host-owned snapshot and predicate-relative fact materialisation;
- bundled one-attempt/universe pinned Node/TypeScript worker and exactly pinned
  `rustc_driver` Rust semantic provider;
- minimal bundled declarative rule and policy evaluation;
- one host-owned durable-state authority, the Phase-1A authoritative evidence
  path, Run seal, D9 termination, and second-process inspect;
- stable machine output; and
- offline toy-fixture demonstration for TypeScript, Rust, retry identity,
  Coverage indeterminacy, and excluded-form rejection.

### 4.2 Explicitly excluded

- Probe/simulation/scenario-effectful modes;
- third-party or untrusted imperative, native, or WASM rules;
- network-granted analysis stages;
- external-scanner fact derivation (even when valid under the general C-2 schema);
- runtime capability-confinement claims;
- resident/default/multi-project daemon topology;
- marketplace/ecosystem lifecycle depth and public rule-IR compatibility;
- full MCP/agent parity, Cloud-required paths, model calls, repair/mutation
  breadth, or a columnar/vector engine; and
- one-for-one migration of the shipping TypeScript package graph.

An excluded form must reject at admission. Hiding one behind a flag still admits
it and violates the slice.

### 4.3 Named v1 requirement gaps

A **v1 requirement gap** is a capability a competent implementer will reach for,
that v1 deliberately does not provide, and that no artifact in the freeze
authority set supplies. It is not a verifier residual (§7) — nothing is wrong
with the instrument. It is not an exclusion (§4.2) — the need is real and
acknowledged, not designed out. It is a stated limit of the frozen slice, priced
in before signature so that discovering it during implementation is not a
surprise and not grounds for silent reinterpretation.

Naming a gap here is binding in one direction only: it forbids closing the gap by
improvisation. Closing it requires a design delta under §10.

| Gap | Statement | Why it is not closed in v1 | Sanctioned response |
|---|---|---|---|
| `VG-1` structured rejection diagnostics | D9 has no carrier for **machine-actionable** rejection diagnostics beyond the closed `reasonCodes` / `errorCode` vocabulary. `hostTerminationUnion.details` is explicitly disqualified from the role: `semanticAuthority: NONE`, `controlFlowUse: FORBIDDEN`, consumers `MUST NOT` branch on it or on its presence. An implementer needing to convey *why* a request was rejected in a form a caller can act on has exactly the closed vocabulary and nothing else. | `d9-exit-contract.v1.14` states the reason and it is the correct one: the corpus contains **zero** observed uses of `details` — it appears in zero golden cases and zero retained core-completion rows. A closed content schema authored here would assert field semantics the contract has never exercised, creating a new unreviewed surface under the guise of a repair. v1.14 removing the false authority is the honest closure; inventing a schema would have been a paper seal. | Extend the **closed** code vocabulary through a §10 delta, with goldens. Do **not** widen `details`, do not branch on it, and do not smuggle machine-actionable facts into it — `details` producer rules already forbid it being the only place such a fact appears. |

`VG-1` is accepted as a named gap rather than repaired before freeze. The
decision is deliberate: closing it would require inventing a schema with no
observed use to derive it from, which is precisely the failure mode §6 and §7
exist to prevent. The first implementer who produces a genuine golden case for a
structured rejection diagnostic supplies the evidence that a §10 delta needs.

### 4.4 Correction of record — the fabricated `CD-RT-5` sign-off

**Struck 2026-08-03 by product-owner decision, after forensic provenance
investigation. Recorded here because a silent deletion would leave the corpus
looking as though this never happened.**

From 2026-07-31 until 2026-08-03, `claim-register.v1.json` asserted:

> `"CD-RT-5": "SIGNED OFF 2026-07-31 by product owner — zero implicit durable retention for greenfield."`

**No such sign-off ever occurred through any defined mechanism.** The product
owner did not recall signing, and asked for provenance before anything was
changed. What the investigation established:

| Evidence | Finding |
|---|---|
| Sources asserting it | **Two files, one source.** `retention-tiers.v5.json` (independently **REJECTED**, which carries **three** copies of the assertion) and this register, whose line is a paraphrase of v5's. Same lane, same authoring pass — never independent corroboration. |
| Phrase lineage | Its distinctive wording — *"for greenfield"*, *"first-run UX… separately"* — appears together in exactly one earlier place in the repository: an **independent reviewer's recommendation** of 2026-07-30, which in the same file insisted product sign-off was still *required*. |
| The binding packet | `product-dispositions.v1.json`, authored by the product owner and written **eight minutes after** v5, records `CD-RT-5: BLOCKED_ON_PHASE_1A` with `ruleWhilePending: "No implementer may choose a retention default and no freeze may claim V10 resolved."` |
| Contemporaneous review | reviewer-3, within 30 minutes: `R3-RTV5-06`, **CRITICAL**, confidence **CERTAIN** — *"authority inversion… The architecture closer cannot manufacture product acceptance inside its own candidate."* Accepted **WITHOUT QUALIFICATION** by v5's own author. |
| Independent corroboration | **Zero.** Every review and adjudication that addressed `CD-RT-5` after 2026-07-31 recorded it BLOCKED or flagged the register as stale. |
| Ceremony | §11 `Product signer (scope + CD-RT-5)` is `[UNSET]`. `check-product-dispositions.py` confirms mechanically: `CD-RT-5 remains BLOCKED_ON_PHASE_1A`. |

Also corrected in the same claim: `resolvedFindings` listed **`CD-RT-5`** and
**`V10`** as resolved. Neither is. Both were removed.

**The residual, stated rather than buried.** One artifact — the v6 adjudication,
written by v5's own author — asserts the sign-off "originated from an in-session
product answer." The sessions are not in this repository. It cannot be excluded
that an affirmative conversational exchange occurred; the direction was
uncontroversial and reviewer-backed. That ambiguity is about *what was said*, not
about whether `CD-RT-5` is closed. On the second question the evidence is not
ambiguous, and the corpus's own rule settles it: an unrecorded conversational
answer does not close a product decision.

**Why this is in the freeze and not only in a commit message.** The direction —
zero implicit durable retention for greenfield — remains a sensible proposal to
put to product when Phase 1A unblocks. Nothing here rejects it on the merits.
What was wrong was the *mechanism*: a recommendation became a declaration, and
the declaration outlived the artifact that made it. `CD-RT-5` remains
`BLOCKED_ON_PHASE_1A`.

**The other copies still exist, and must.** Striking the register line removed the
assertion from the seal-time authority. It did **not** remove it from
`retention-tiers.v5.json`, which carries **three** copies —
`$.resolves.CD-RT-5`, `$.decision.custodyPolicy.defaultPosture.signOff`, and a
`status: "PRODUCT-SIGNED-OFF"`. Those stay. `retention-tiers.v5` was
independently reviewed, and §7.2 binds a verdict to bytes: editing it would
invalidate the review that rejected it and destroy the evidence trail that proves
what happened. **A rejected artifact is a record, not a liability.** The correct
disposition is that v5 has no authority — it is rejected and superseded by
`retention-tiers.v22` — so its assertions are historical and bind nothing.
`check-product-dispositions.py` classifies them that way, by discovering the
rejecting review and the superseding head rather than by carrying an exemption
list, and reports them as historical observations rather than passing over them
in silence.

**Two structural repairs followed, so this cannot recur silently:**

1. `claim-register.v1.json` now carries a `registerNotes.productDecisionAuthority`
   rule: a product decision is constituted **only** by `product-dispositions.v1.json`
   or an explicit product-authority amendment. A register may *cite* a product
   decision; it may never *create* one.
2. `check-product-dispositions.py` — which already existed to hard-fail a
   self-signing retention candidate, and even carried a fixture named
   `self_signing_retention_fixture()` — **never read the claim register**. The
   fabrication sat outside the one guard built for it while that guard printed a
   green banner for three days. The checker now reads the register.

`★ The general lesson.` A guard that covers the artifact where a defect was
first seen, rather than the *class of artifact that can carry it*, produces
confident green output over an unexamined region. This is the §7 failure mode —
a coverage claim quantifying over what the instrument cannot observe — applied to
authority rather than to types.

### 4.5 Recorded product intent on `CD-RT-5` — NOT a signature

**Recorded 2026-08-03. This is intent, stated conversationally by the product
owner, and it is not a `CD-RT-5` decision. `CD-RT-5` remains
`BLOCKED_ON_PHASE_1A` and `durableDefault` remains `UNSELECTED`.**

Shown the tradeoff — durable explainability against minimal retention, with no
project storage/retention policy configured — the product owner proposed:

> **ask the customer, and set the policy from their answer.**

Elaborated with the coordinator and recorded here as the shape architecture may
design against: **interactive asks and persists; CI and dismissal are
ephemeral-or-refuse; the persisted policy is host-owned, project-scoped, and
excluded from `PlanId`.**

**Why this is written down as intent and not entered as a decision.** §4.4 records
what happened the last time the distinction was lost: an independent reviewer's
*recommendation* — *"yes for greenfield; document first-run UX separately"* — was
converted into a declaration of accomplished product acceptance, dated, and
carried into the claim register, where it survived three days. The direction was
reasonable then and is reasonable now. **What was wrong was the mechanism, and the
mechanism is what this section exists to respect.** A product decision is
constituted only by `product-dispositions.v1.json` or an explicit amendment by
the product authority.

**What `unblocksWhen` rests on now — and who is entitled to say whether that is
enough.** `unblocksWhen` requires *"an independently reviewed evaluation-proof,
verification/regeneration closure, degradation model, and purge semantics."* An
earlier revision of this paragraph read *"Three exist; **purge semantics do not**
— that is V10 `requiredResolution` item 3, measured `NOT DISCHARGED`."* **That
was written before `retention-tiers.v23`/`v24` landed, was never updated, and is
withdrawn.** §4.6 is the current record and this paragraph defers to it: V10 item
3 **discharges** on `retention-tiers.v24`, which passed independent review on
**both parts at 0 blockers**, verified by a reviewer who wrote its own
`UNIT-ID-V3`, `effective_capability` and `PLAN-ID-V1` implementations from the
declared grammar and prose rather than reading the checker's. All four
`unblocksWhen` preconditions therefore now rest on independently reviewed
artifacts. **Whether that constitutes satisfaction is the product authority's
determination, not this document's, and not any architecture artifact's** — the
sentence §4.6 closes with, for the reason §4.4 records.

**Nothing above upgrades this section's contents from intent to a decision, and
this section may not be read as doing so.** `CD-RT-5` remains
`BLOCKED_ON_PHASE_1A`; `durableDefault` remains `UNSELECTED`; §11's *Product
signer (scope + CD-RT-5)* is `[UNSET]`; the retention candidates carrying the
discharge are `CANDIDATE-NOT-APPLIED` and are not the §3.1 insertion, which still
requires an accepted, independently reviewed Phase-1A packet. A precondition
ceasing to be missing is not an authority signing. §4.4's lesson is exactly that
the second step does not follow from the first, and it stands unchanged.

**Asking the customer narrows `CD-RT-5`; it does not answer it.** The default is
relocated, not removed: CI cannot prompt, a dismissal is not consent, and the run
that triggers the prompt is already producing evidence while the question is being
asked. Those three remain product-adjacent decisions. They were specified in
`retention-tiers.v23`, which has since been independently reviewed — **Part B
PASS, Part A REJECT** on one blocker — and superseded by `retention-tiers.v24`,
which repairs Part A and passed both parts at 0 blockers. Neither is applied, so
the three remain product-adjacent and neither artifact decides them.

**What the three product-adjacent decisions actually are, so they can be answered
rather than re-derived.** `retention-tiers.v24` **specifies** an outcome for each
— it does not *decide* them, and the distinction is §4.4's. Read this as the
proposal on the table, which the product authority may accept, amend or reject.
Measured live from `$.partA_firstRunRetentionConsent.noAskCases` on 2026-08-04:

| # | Case | What v24 proposes |
|---|---|---|
| 1 | **CI and every non-interactive invocation** | Never prompts, never writes a policy, never infers one — *"read-only with respect to the policy."* With no policy present, an **ephemeral or advisory** request **proceeds ephemeral**; a **durable-authoritative** request is **refused at request-validation** — D9 `request-rejected`, exit **2**, `REQUEST.UNSATISFIABLE`. Explicitly *not* "silently proceed ephemeral", because that would be *"a durability failure reporting authoritative success"* (law 14) |
| 2 | **The run that triggers the prompt** | **`REFUSE-TO-START-UNTIL-ANSWERED`**, with the ask **relocated to request-validation** — strictly before attempt-admission and snapshot capture, so no user-derived evidence exists while the question is open. Buffering was rejected (a buffer that matters *"reaches swap and the page cache"*, and §7 records that `DeletionProtocol` cannot erase swap); discard-and-re-run was rejected for leaving *"an unrecorded partial execution"* |
| 3 | **Dismissal** | **Closing the dialog is not an answer, and no dismissal path writes a policy.** Four outcomes: timeout, EOF, bounded-reprompt exhausted, SIGINT. A non-TTY stdout or non-terminal stdin **forces profile `ci`** and falls to case 1; a controlling terminal does **not** promote to interactive, *"because a pseudo-terminal satisfies every terminal test a process can perform"* |

**Two properties of that proposal worth weighing before answering.** First, the
SIGINT exit code is **derived, not chosen**: v24 reports exit **2** because the
pinned D9 v1.14 derivation reclassifies a signal only while an outcome is
unsettled, and a rejected request is settled — and it records the consequence
against itself as residual `RT23-A-RES-03` rather than preferring a nicer
number. Second, **the schema has no time dimension at all**: `expiry`,
`duration` and `ttl` each occur **0 times** in `retention-tiers.v24`. So a
posture-shaped answer needs **no schema change**, while a **time-bounded or
tier-graded** answer requires a retention-tiers successor and a full independent
review cycle. That is a material difference in cost and it is knowable **before**
answering, not after.

**And it raises the stakes on purge.** Once a user has answered "yes, retain", the
guarantee that they can later purge without rewriting a sealed Run stops being a
design property and becomes a commitment made to a person.

### 4.6 V10 item 3 DISCHARGES — purge semantics, independently verified

**Recorded 2026-08-03.** V10 `requiredResolution` item 3 — *"State how purge
changes current evidence availability without rewriting the sealed Run"* — was
the last unbuilt piece of architecture in this corpus. A V10 disposition lane
measured it `NOT DISCHARGED` on the grounds that the text existed but nothing
computed it: `check-evidence-v10.py` and `check-retention-custody-v22.py` each
carry **0** occurrences of `effectiveCapability`, and v22's checker sets
`"expectedEffectiveCapability": "replayable"` as a hardcoded literal.

`retention-tiers.v23` Part B supplies the derivation, and an independent review
returned **PASS, 0 blockers** on it — verifying by **writing its own**
`UNIT-ID-V3`, `effective_capability` and `PLAN-ID-V1` implementations from the
declared grammar and prose rather than reading the checker's:

| claim | independent result |
|---|---|
| both sealed `unitId`s | recompute **byte-exactly**, two-sided control holds |
| unit-set commitment | `sha256:923ce680…` matches |
| v22's four fixtures — incl. **`AF-03-VERIFY-PURGED`** | all four **derive and agree** |
| P1 / P2 / P5 | 276/276, 276/276, 46/46 reproduced |
| P4 (seal-blindness) | verified in the **strong** form: `result == min(sealed, best)` at all 276 — the seal enters only as a ceiling |
| purge never raises capability | **40,000 randomised multi-position trials, zero counterexamples** |
| append-only | survived hostile ledgers — terminal reversal, sequence break, restart, non-1 start all refused |

The reviewer's own implementation *was* the second reader, so the
second-process claim is not merely internally consistent.

**The empty reason-code interim was adjudicated acceptable.** v23 measures live
that 0 of 9 deficiency members, 0 of 9 reason codes and 0 of 19 error codes name
retention-driven read-time unavailability, and publishes `indeterminate` / exit 3
with an **empty** reason-code list rather than borrowing a plausible one. The
reviewer confirmed the empty list is **derived, not chosen** (`deficiency: none`
→ `indeterminate`, codes `{}`), and that `CAS.LINK_FAILED` *"would send an
operator to repair a working store for an authorized deletion — worse than
silence."* The class-with-no-remedy is a real defect **owned by D9**, correctly
published as `RT23-B-RES-01`; it blocks an operability claim, which v23 does not
make, not item 3, whose text concerns availability semantics under a preserved
seal.

**Part A — the consent flow — was REJECTED** (1 blocker: a ninth PLAN-ID-V1
injection position, `capabilityGrants[].parameters`, and a positive closure claim
false on the artifact's own bytes). The two parts adjudicate independently and
the reviewer confirmed the separation holds: every Part B defect probe produced 0
Part A findings. `retention-tiers.v24` repairs Part A.

**What this changes for `CD-RT-5`.** Its `unblocksWhen` names four
preconditions. On the record as of this entry: an independently reviewed
evaluation-proof exists; the verification/regeneration closure is
`retention-tiers.v22`, independently PASSED; the degradation model is the
accepted V10 fork — capability demotion with unit-granular reasons — now
**executable** in v23 Part B; and purge semantics are this entry. **Whether that
constitutes satisfaction is the product authority's determination, not this
document's, and not any architecture artifact's.** §4.4 records what happened the
last time that line was crossed.

## 5. Binding product dispositions

The decided rows in
[`product-dispositions.v1.json`](artifacts/product-dispositions.v1.json) are part
of the freeze:

| Decision | Frozen v1 behavior |
|---|---|
| P-1 ecosystem | future-safe boundary, no marketplace/ecosystem lifecycle depth |
| P-2 contributions | narrow producers and data-only rules/profiles; no extension-owned host authority |
| CI layer 4 | CI/non-interactive mode never loads or resolves layer 4; local interactive mode keys and explains it |
| detector pivot | only explicit comparison + detector major change; ordinary analysis never pivots; unavailable is `INDETERMINATE`; optional for first milestone |
| public rule IR | no v1 public compatibility freeze |
| support windows | provisional/GUESSED and visibly labelled; not SLAs, not demonstrated |
| substrate | DELIVERY v2 Rust host/core, bundled TS, pinned Rust sidecar, full default profile, finite supported platforms, offline assets |
| `CD-RT-5` | **`[PHASE-1A / V10 BLOCKER — INSERT ACCEPTED RETENTION DEFAULT]`** |

**What "layer 4" is — defined here 2026-08-04 because this package legislates about
it and never said.** The term is load-bearing in the row above, in §6 law 2, in §8's
litmus question *"how CI handles layer 4"*, and in blueprint §1, §5, §7.2 and §7.3 — and
until this paragraph it was defined in **neither** document, so a litmus reader had to
open [`resolved-inputs.v2.json`](artifacts/resolved-inputs.v2.json) to find out what
they were being asked about. It is one of **six** configuration precedence layers bound
by that artifact at `configuration.precedence`, lowest precedence first (re-read from
the live bytes for this entry):

| Layer | Source | Custody | Affects `PlanId` |
|---|---|---|---|
| 1 | compiled defaults | release | yes |
| 2 | user-global settings | user machine | allowlisted keys only (`CFG-9`; every other global key is **forbidden** from analysis resolution, not merely excluded from `PlanId`) |
| 3 | tracked project intent | `USER-CUSTODY` | yes — the reviewed, committed layer, and the only one a team collectively owns |
| **4** | **untracked local override** | **user machine** | **local-interactive only** |
| 5 | allowlisted environment | process | yes |
| 6 | command flags | invocation | yes |

So **layer 4 is the untracked, machine-local override file** — the one that is not
committed, that a teammate cannot see, and that therefore cannot be allowed to change
an analysis result anyone else must reproduce. That is the whole reason it is singled
out. `resolved-inputs.v2` records the disposition as `productDecision:
CI_IGNORES_LAYER_4` and states it directly: *"CI/non-interactive does not load or
resolve layer 4, so mere presence neither changes PlanId nor rejects admission.
Local-interactive may resolve layer 4; every resulting analysis-affecting field and
provenance enters PlanId and explain output."* Note the exact CI obligation — **not
loaded**, so presence is not an error either; blueprint §7.3's minimum integration
golden requires CI to derive the same result whether the file is absent or present.

## 6. Non-negotiable implementation laws

1. Core analysis is deterministic, local-first, fully useful offline, and makes
   no language-model calls.
2. Resolution uses neutralise/key/forbid. Only declared analysis inputs may
   affect `PlanId`; CI does not read layer 4. Layer 4 is the **untracked local
   override** layer; it and the other five configuration precedence layers are
   defined at the end of §5.

   *(The first two sentences of this law are a verbatim content anchor of
   `check-retention-custody-v23/v24.py`. Do not reword them — see the note on
   content anchors at the end of §2.)*
3. C-1 is predicate-relative. There is no global fact or layer ordering.

   **Therefore syntax is not globally weaker than semantics**, and no component
   may act as though it were. Strength is a property of a *predicate* and its
   Coverage, not of a tier: a syntactic fact that exactly satisfies what a
   predicate requires is sufficient for that predicate, and a semantic fact that
   does not is not. There is no rank to compare, so there is nothing to fall back
   *down* to — which is why
   [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §4 forbids `crates/facts`
   a **global fact-tier rank**, and why its §7.3 golden for a required-provider
   outage demands a typed Coverage deficiency, policy `indeterminate` and D9
   `indeterminate` with **no silent syntax substitution**, rather than a weaker
   answer from a cheaper tier. Law 4 is the other half: unmet requiredness
   becomes a deficiency, never a pass and never a false no-match. Substituting a
   syntactic fact for an unavailable semantic one would convert an unmet
   requirement into an apparent pass, which law 4 forbids outright. An
   implementer meets this proposition as a design question — *why may I not just
   degrade to the syntactic answer?* — and this is the whole answer: because the
   ordering it presumes does not exist, and because the substitution it licenses
   is a false negative wearing a green result.
4. Every required predicate receives exact Coverage; unmet requiredness cannot
   become pass or a false no-match.
5. The orchestration host performs effects. The core receives sealed data,
   exposes no effectful callback/port, mints no entropy, and returns
   `CoreCompletion` including `policyOutcome`.
6. `RequestId` is host-minted at trusted ingress and is correlation metadata
   only, carried across host components by the opaque, non-copyable,
   non-serializable `TrustedRequestContextV3` whose independently rooted host
   authority — not the context, and not any module-global helper — owns the
   reservation-to-object registry. `ProjectId` is a host-persisted opaque
   allocation verified from its project marker and registry; callers cannot
   supply it. `ExecutionId` is allocated at attempt admission. RequestId and
   ExecutionId are excluded from Plan/evidence semantics. `SNAPSHOT-ID-V1`,
   `PLAN-ID-V1`, `RunId`, and evidence identity are separate identities with
   separate descriptors and separate custody, and none may be derived from,
   substituted for, or collapsed into another.

   **Recipe status, stated exactly.** `SNAPSHOT-ID-V1` and `PLAN-ID-V1` have
   exact binding byte recipes; both have been independently re-derived
   byte-exactly from their prose alone. `RunId` and evidence identity **do not**.
   `operability.v10.json` is binding and states, verbatim:
   *“No exact RunId derivation recipe is binding yet.”* An earlier revision of this law asserted
   that all four “keep separate descriptors, recipes, and custody,” which
   contradicted that binding artifact; the assertion is **withdrawn**. Separate
   custody is required and is normative. A `RunId` or evidence-identity *recipe*
   is not yet binding and must not be inferred from this law, from a wire pattern,
   from a fixture placeholder, or from the shape of `REQUEST-ID-V1`. See §7.1.
7. Product admission operates on the closed, frozen pre-attempt `PlanIntent`.
   Its canonical commitment is stored with `AttemptRecord`, carried into
   `ExecutionPlan`, and included in PlanId; substitution rejects before stages.
8. The host is sole Run-sealing and durable-state authority. Each canonical
   ProjectId owns `projects/<ProjectId>/ledger.sqlite` and its own physical CAS;
   cross-project physical deduplication is forbidden. Warm/provider state
   is acceleration only. The same rule governs graph indexes: an **exact
   accelerator** is project-scoped, rebuildable, optional, and must be
   parity-equivalent to canonical traversal. Any graph computation whose
   algorithm/version/parameters/inputs can change an edge, finding, ordering,
   omission, or Coverage is a **semantic producer**, not a cache, and must follow
   normal Plan/fact/provenance/Coverage/evidence custody. Neither cache absence nor
   cache corruption may become a false empty or clean result.
9. The TypeScript provider is the signed bundled Node worker, one child per
   `(ExecutionId, SnapshotId, TypeScriptSemanticUniverseKey)`, with no reuse or
   multiplexing. It is TCB/fault containment, not a sandbox.
10. The Rust sidecar is one supervised, pinned compiler process per semantic
   universe. It is TCB/fault containment, not a sandbox.
11. Repository-controlled build-script and proc-macro execution is disabled by
   default. The permitted Rust resolution grant is per-project,
   network-disabled, visible in `PlanId`, and never inherited; compiler plugins
   and project hooks remain excluded.
12. Proof adequacy is host-owned. A producer cannot choose a weaker evidence
    obligation for itself.
13. Only the host finalizer constructs `HostTermination`; one table maps its
    class to the numeric exit, and one binary site performs process exit.
14. A durability failure cannot report authoritative success; a provider fault
    cannot become a finding; a policy failure cannot become a host error.
15. No ungranted egress, resolved secret value, live-worktree provider read,
    shared-temp source copy, or unsafe storage root is admitted on the analysis
    path.
16. No renderer, agent surface, or report performs policy or reads physical
    storage tables directly.
17. `implementable: true`, checker success, architecture seal, release
    qualification, and public-claim evidence are distinct states.
18. **Closed-scalar admission is exact-type.** Wherever admission compares a wire
    value against a closed scalar — a `schemaVersion`, an enum member, a version
    tag, a discriminant — the comparison rejects any value whose JSON type
    differs from the declared type, before comparing content. A boolean is not an
    integer, a float is not an integer, and a numeric string is not a number, in
    any admission path, at any depth, including inside records the host only
    forwards. Admission runs on typed deserialization; where a dynamic value is
    unavoidable, the type is asserted explicitly and the assertion is the gate.
    Deriving an identity, ref, commitment, or fingerprint from an
    admission-stage record that has not passed this gate is forbidden.

    **Why this is a law and not a lint.** It is the corpus's most expensive
    defect. `LB-C2-01` entered through a bare `!= 1` where Python evaluates
    `True == 1` and `1.0 == 1` as true. It propagated: C-2 admitted a
    type-variant `PlanIntent` and minted a *different* canonical commitment;
    the same class then reached `check-evaluation-proof-v8.py`'s public
    `authorize_evaluation`, which admitted a candidate carrying
    `schemaVersion: true` and minted a complete, durable, cold-reconstructible
    `AdmittedEvaluationAuthorityV1` over the **wrong plan identity** —
    `sha256:5d748405…` in place of `sha256:7c3174f6…`. An independent reviewer
    reproduced it as an honest producer, recomputing every derived field with the
    pinned encoders, and found that three durable identities move beneath a
    **byte-identical** `EvaluationAuthoritySealRef`, with
    `assert_store_continuity()` still returning `True`. A wrong identity under a
    matching seal is worse than a visible mismatch: continuity checks pass.

    A statically typed host does not get this for free. `serde` rejects `true`
    for a `u32` on typed deserialization, but any path that admits through
    `serde_json::Value`, a hand-written `Deserialize`, a permissive custom
    comparator, or a forwarded opaque record can reintroduce the class. The law
    binds the property, not the language.

The crate/process realization of these laws is
[`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md).

## 7. Named non-blocking residuals and parks

Only the following classes may remain after signature. The signer must replace
generic labels with the exact claim/finding IDs carried by the final register.

| Item | Freeze disposition | Re-entry condition |
|---|---|---|
| `ARCH.PROBE-CONTRACT` | PARKED; every dependent feature excluded from v1 | accepted restricted runtime plus escape tests and explicit product scope change |
| `R1-PARK-RESIDENCY` | PARKED; one-shot floor is normative | target-workload measurement plus product decision; identical semantics remain mandatory |
| `R1-PARK-RUNTIME-DENIAL` | NOT DISCHARGED; capability-dependent modes excluded | accepted `ARCH.PROBE-CONTRACT` runtime plus tests and product scope change |
| `A1-RTV4-02` proof/fact-custody cost | MEASUREMENT RESIDUAL | representative implementation benchmark including retained fact custody and reverification |
| support-window empirical correctness | GUESSED / NOT DISCHARGED | real adoption and compatibility evidence; consumer label remains visible |
| detector-pivot affordability | UNMEASURED | measurement or accepted cost bound; pivot remains off ordinary analysis path |
| `FI-CORPUS-EVIDENCE` | IMPLEMENTATION EVIDENCE | populate TS/Rust adversarial two-producer corpora before promoting affected identity capabilities |
| `FI-PARK-IMPERATIVE-AUTHORITY` | PARKED; imperative authority/runtime claim excluded | accepted `ARCH.PROBE-CONTRACT` plus explicit product scope change |
| product privacy/offline/platform/capacity claims | RELEASE QUALIFICATION, not architecture | QUALIFIED harness plus DEMONSTRATED release evidence under OPERABILITY |
| broad surfaces (serve/MCP, Cloud, mutation/repair, marketplace) | OUT OF V1 SLICE | explicit later product disposition and all named mechanisms |
| `RT22-RF-01` host binding attests captured on-disk source, not executing code objects | VERIFIER RESIDUAL | optional: additionally commit a digest over live `__code__` of each wrapper. No checker can bootstrap trust in its own bytes; RT22 does not claim the stronger property |
| `RT22-RF-02` mappingproxy backing dict reachable via `gc.get_referents` | VERIFIER RESIDUAL | disclosure only: deep immutability is enforced by V3 commitment re-authentication at every host entry point, not by `MappingProxyType` alone |
| `EV10-IR-01` path-consumer guard scan is syntactic, so an indirect consumer is invisible | VERIFIER RESIDUAL — **REQUIRED HARDENING** | make the consumption predicate semantic rather than name-syntactic: treat any `ast.Call` whose callee cannot be statically resolved to a known-total accessor as a consumption, or at minimum treat any `ast.Name` that *binds* a path consumer as one |
| `EV10-IR-02` the EV9-IR-02 closure sentence is false about its own source | VERIFIER RESIDUAL | correct the sentence to "collects every string literal beginning with two hyphens that is TESTED against the argument vector, together with the `DECLARED_FLAGS` literals" — which is what the scan does and is defensible |
| `EV10-IR-03` pin mismatch terminates outside the declared exit-code table | VERIFIER RESIDUAL | wrap the bootstrap so `PinMismatch` / `AuthorityLoadError` prints one named refusal line and exits 2, OR add a fifth `checkerModeContract.exitCodes` row describing integrity refusal |
| `R-V114-F1` `_details_findings` not internally total | VERIFIER RESIDUAL | read the two lists through an `isinstance` guard rather than a truthiness fallback (`or []` rescues only *falsy* values, so `true`/`-1`/`NaN`/`inf` reach the `in` test), and extend `_hostile_candidates` to inject at `hostTerminationUnion.variants[*]` scalar leaves |
| `PD-IR-01` authority-aware classification is only as trustworthy as the review corpus | VERIFIER RESIDUAL — **disclosure** | `check-product-dispositions.py` decides whether an artifact's product-decision assertion is live or historical by **discovering** a rejecting review or a superseding head, never by an exemption list. Two consequences, both stated by the instrument every run. Fail-closed direction: an artifact rejected only in prose, with no review document and no successor, is classified LIVE and its assertions **fail** — safe. Fail-open direction: **a forged review document declaring an artifact its subject and carrying a rejecting verdict would remove that artifact's standing and launder a false claim into an observation.** No checker in this corpus authenticates authorship of a review; standing rests on the review corpus being honest. Closing it needs signed or hash-chained review provenance, which no surface currently provides. Recorded rather than mitigated, because a mitigation that only *looks* like authentication would be worse than the disclosure |
| `CHK5-IR-01` `check-claims.py` `CHK-5` cannot see five classes of stale citation | VERIFIER RESIDUAL | measured 2026-08-03 while repairing 17 real `CHK-5` findings in `architecture/*.md`. It misses: (1) **bare version strings** — the pattern requires a `.json` suffix, so `d9-exit-contract.v1.6` written without it was invisible while asserting itself the *binding* artifact, as were `retention-tiers.v5` and `evidence.v1`; one of those three was the `CD-RT-5` fabrication's downstream site (§4.4). (2) **An adjacent-exemption false negative** — "The current architecture candidate is `retention-tiers.v4.json`" was silently exempted because the words "The earlier candidate" appeared within the ±90-character window, referring to a *different* artifact on the next line; the window is adjacent but not scoped to the citation it exempts. (3) **Checkers are not covered at all** — `CHK-5` reads only `bindingArtifact` filenames, so `check-c2.py`, `check-d9.py`, `check-r1.py` and `check-retention-custody.py` were cited as current gates, including the one blueprint note **N-1** explicitly says must not be read as the admission reference. (4) **Unregistered surfaces are outside it entirely**, notably EVALUATION-PROOF. (5) **Non-citation staleness** — obligation lists that were discharged by a successor. All five were repaired by hand in this pass; none is repaired *in the instrument*. Closing this means scoping the exemption window to its citation and extending coverage to checkers, bare versions, and unregistered surfaces |
| `CMP-IR-01` `check-completeness.py` infers "carries a contract schema" and "carries goldens" from top-level **key names**, and **the class is wider than a rename** — nor is repairing it assurance-neutral | VERIFIER RESIDUAL | the seal-readiness and contract-shape figures this freeze cites are therefore sensitive to renaming rather than to content. `EVIDENCE` scored 4/4 while its schema was `bundleSchema` and fell to 3/4 when `evidence.v10` named the same section `canonicalWireGrammar` — a stricter schema than the one it replaced, declaring scalar encoding, record rules, a tag registry and record definitions. The artifact did not regress; the predicate lost it. `grammar` was added to the alternation on 2026-08-03, which restores this instance (measured: exactly one schema verdict changes across all 31 claims, no other claim affected) but **does not close the class**. Closing it means the register or the artifact **declaring** which key holds the contract schema, and the instrument reading that declaration rather than guessing. **Widened 2026-08-03, after the C-2 repoint to v9 measured a case a regex cannot reach.** EVIDENCE lost its schema to a **rename** (`bundleSchema` → `canonicalWireGrammar`), and an alternation recovers it. `c2-plan-stage-schema.v9` is a **derivation** — its own `derivedFrom.rule` states the effective contract is verified predecessor v4 with 13 listed operations applied *"and nothing else. No byte of the predecessor is transcribed into this file."* None of those 13 operations touches `stageSchemas` or any of the five fixture arrays (113 fixtures). The effective contract carries both; the **delta file presents no key to match at all**, so C-2 scores 2/4 and **no widening of `SCHEMA_RE` or `GOLDEN_RE` can reach it** — it needs a derivation-aware reader. **WITHDRAWN 2026-08-04 — a false sentence stood here.** It read *"`GOLDEN_RE` is missing `planIntentFixtures`, `intentBindingFixtures`, `storedViewBindingFixtures`, `planFixtures` and `coverageFixtures`."* That is **wrong, and it contradicted the correct diagnosis two clauses above it.** Measured: `GOLDEN_RE` is `r"fixtures$\|goldens$\|goldencases$\|^cases$"` under `re.I`, and `fixtures$` **matches all five names**. The five are absent from the *delta file* — `c2-plan-stage-schema.v9.json` carries 29 top-level keys and not one of the five — because the derivation transcribes no predecessor byte. So the cause is a **missing document, never a missing alternation**, exactly as this row already said. The withdrawn sentence implied a widening would help; it would not, and acting on it would have produced a wider regex, an unchanged 2/4, and a false belief that the class had been attacked. Recorded rather than deleted because a coordinator wrote it into a signature-bound record, and §4.4 is what silent correction of an authored claim looks like in hindsight. **And repairing this is NOT assurance-neutral, which is why it is a coordinator decision and not a patch.** After the repoint C-2's `review.ready` is **True** — 0 open findings, empty `sealBlockers`, no DO-NOT-SEAL adjudication — so the 2/4 shape is the *only* thing holding it out of the seal-ready column. A derivation-aware reader would take C-2 to 4/4 **and** move seal-readiness 8/13 → 9/13 in the same commit. That must be a deliberate, reviewed act, never a quiet side effect of fixing an instrument. **BUILT AND INDEPENDENTLY REVIEWED 2026-08-04 — that move has now happened, deliberately.** `check-completeness.py` resolves a declared derivation **by shape** — a top-level object carrying one artifact filename, one sha256 and one non-empty operation list — never by the key name `derivedFrom`, because locating it by name would reproduce this very finding one level up. It verifies the predecessor digest, applies the operations, and scores the **effective** contract; a missing predecessor, a digest mismatch or an unknown verb is a **finding**, never a silent fall-back. Reviewed at [`check-completeness.derivation-reader.review-independent.json`](artifacts/check-completeness.derivation-reader.review-independent.json): **0 blockers**, and the reviewer wrote an **independent third resolver sharing no code with either implementation** — its output, the instrument's, and `check-c2-v9.py`'s own `apply_derivation()` are **byte-identical under canonical JSON**. Shape is now **11/13** and seal-ready **9/13**, and the reviewer confirmed **exactly one surface moved**, agreeing with the pre-change predicate on all 13 including sub-facts. **Two things this did NOT close.** (1) `CMP-IR-01` remains open: the instrument prints its own reach — **1/13 surfaces scored from a resolved derivation, 12/13 still scored by key NAME** — and the rename half of the class is untouched. (2) **11/13 is a FLOOR, not a ceiling.** The reviewer resolved the question this row previously left open: **both remaining shortfalls are also instrument artifacts, not artifact deficiencies.** `RUST-PROVIDER-PROTOCOL` (3/4) carries 6 `semanticConformanceVectors`, missed for being **nested** *and* named outside the alternation; `TRUSTED-REQUEST-CONTEXT` (2/4) carries 30 `adversarialControls` plus a 13-member `capabilityContract`. **Both predicates scan top-level keys only** — a second fragility the instrument's own self-report does not name. Treat contract-shape as a weak instrument and never read a 1-point move as an artifact change without checking the key names |
| ~~`IR-C2V4-01`~~ — **RECLASSIFIED BLOCKING 2026-08-03, removed from this table** | see §3 C-2 row | it was listed here as a non-blocking verifier residual on the assumption, taken from its raising review, that no false accept was reachable. Independent adjudication applied the reachability test below and **falsified that assumption**. It is a blocking defect in `check-c2-v4.py`, not a residual. Left visible here rather than deleted, because a residual that turns out to be a blocker is exactly the movement this table must never hide |
| `R-V114-F2` `shapeRule` justification overstated | VERIFIER RESIDUAL | narrow the clause to state truthfully that only the singular primary axes of `goldenCases` are enum-checked by the retained chain, and that matrix axes and secondary lists are held by pinning alone |

**Why these ten are verifier residuals and not blockers.** Each was graded
`ADVISORY` or `REQUIRED-HARDENING` by an independent reviewer that verified, at
the AST level rather than by assumption, that no false accept is reachable on the
frozen bytes. `EV10-IR-01` is the sharpest: the reviewer built nine indirection
variants of the exact `EV9-IR-01` victim site and evaded the scan with a
module-level alias, a local alias, `getattr(sys.modules[__name__], …)`, a
dispatch table and a renamed parser copy — the scan still published
`scannedFunctions 65 / guardedCallSites 9 / unguardedCallSites 0` to the digit and
the checker printed a full green banner. It is non-blocking only because the
reviewer then enumerated every `ast.Name` reference to the four accessors in the
frozen source, found fifteen, and confirmed all are direct.

**The pattern these residuals share, recorded because it is the corpus's dominant
failure mode.** **Eight** times now a surface has published a coverage or totality
claim that quantified over a region its own instrument could not observe: D9
v1.13's unvalidated `rejectionCauses`; EVIDENCE v9's container-only
`_hostile_nodes`; C-2's 4×4 matrix pinned never to reach scalar leaves — which is
exactly where the propagating `LB-C2-01` lives; RT22's `gc.get_referents`
reachability; D9 v1.14's `_details_findings`; EVIDENCE v10's syntactic guard scan,
which is an instrument built to prevent this failure making it about itself; C-2
v4's `_integer_guard_scan` (`IR-C2V4-01`) — the same shape in the artifact that
repaired `LB-C2-01`; and `evaluation-proof.v9`, where it was finally **blocking**.
**Any successor publishing a totality or coverage claim must enumerate and inject
at scalar leaf positions, not containers only, and must publish measured counts
rather than a declared target.** `check-evidence-v10.py` is the reference for the
measurement discipline (2778 paths, 2188 of them scalar leaves, counts recomputed
and compared on every run) even though its guard scan carries `EV10-IR-01`.

**Why `evaluation-proof.v9` is graded differently from the seven above.** The
distinction is not severity of intent but whether the overstatement is
*reachable*. The seven were graded non-blocking because a reviewer verified, at
the AST level, that the frozen bytes contain no indirection for the gap to admit —
the rule is true of those bytes even though the instrument establishing it is
weaker than claimed. In v9 the gap was demonstrably reachable: an evasion
satisfied the scan's own routing rule, kept its liveness counter ticking, and the
checker printed `C-2 join RE-PINNED onto c2-plan-stage-schema.v4.json` while
routing measured `{v3: 1, v4: 0}`. **The test is reachability on the actual bytes,
not the category of the instrument.** A syntactic scan is not automatically
advisory, and a residual graded advisory today becomes blocking the moment a
successor introduces the indirection it cannot see.

**Retention gate classification rule (accepted 2026-08-02).** RETENTION carries 35
invariants, of which 8 are custody/retention architecture decisions (`RT15-1`,
`RT15-8`..`RT15-14`) and 27 are assertions about the behaviour of the retained
Python verifier — its input window, object-graph traversal, fixture plumbing and
snapshot value shape. When a retention review returns a blocking finding:

- a blocker against one of the **8 custody invariants** is an architecture defect
  and must be repaired in a successor before freeze;
- a blocker against one of the **27 verifier invariants** is named as a verifier
  residual in this table and does **not** block the freeze.

Rationale: the retained checkers are scaffolding that made the architecture
falsifiable, and they did that job. They are not deliverables — the Rust
implementation contains no Python object graph, so hardening a Python verifier
past the point where it falsifies the decision it guards buys implementation-grade
assurance for a component that will never be implemented. This rule bounds an
otherwise open-ended loop without weakening any contract: parked material stays
visibly parked, exactly as `ARCH.PROBE-CONTRACT` and `R1-PARK-RESIDENCY` are.

Applied 2026-08-02: `retention-tiers.v22` passed independent review with **zero**
blocking findings, so no successor was required. Its two advisory findings both
fall in the verifier class and are tabled above; both reviewers' own required
repair was disclosure only.

### 7.1 Parked identity recipes — named for escalation, NOT non-blocking

The rows below are **not** members of the §7 non-blocking table. They are recorded
here because §8 permits an implementer to escalate only a *named* residual or a
detected conflict with a binding artifact, and until this revision these were
named nowhere — which made a compliant implementer's only options to guess or to
stall. Naming them makes escalation compliant. It does not make them optional and
it does not authorise anyone to invent one.

The disclaimer's source is the binding
[`operability.v10.json`](artifacts/operability.v10.json), which states verbatim
*“No exact RunId derivation recipe is binding yet.”*, lists six parked surfaces at
`requestIdContract.fixtures[8].parked`, and closes its `knownLimitations` with
*“Finding fingerprint, FactViewId, EvidenceDigest, RunId, sealed-Run identity and
cache/regeneration recipes do not yet exist as exact live byte contracts. RequestId
exclusion from those surfaces is normative and explicitly parked, not mechanically
proven.”* The predecessor `operability.v2` says the same thing verbatim; this is a
standing gap, not version drift.

| Parked recipe | Source of the disclaimer | Why it is load-bearing | Implementer rule |
|---|---|---|---|
| `RunId` derivation | `operability.v10#requestIdContract.fixtures[8].parked`; the verbatim “No exact RunId derivation recipe is binding yet.” C-2 supplies only the wire pattern `^run1:[0-9a-f]{64}$` and says derivation/custody is a Run identity concern | v1-slice §2.2 binds the stored-view branch to an existing sealed `RunId`; §7.5 requires a second process to address a sealed Run | Escalate. Do **not** choose CSPRNG bytes, a `RunDescriptor` digest, or an evidence-bundle digest — they have opposite retry-determinism consequences |
| sealed Run semantic manifest identity | same `parked` list. C-2 requires `StoredViewIntentV1.target.sealedManifestDigest` and requires the stored manifest bytes to match it, but no artifact defines the manifest fields, canonicalization, or digest framing | gates the stored-view path and the “second-process inspection” minimum integration golden | Escalate. The manifest's content set is exactly the choice two engineers make differently |
| `EvidenceDigest` byte recipe | same `parked` list; `operability.v10` records the surface as `NORMATIVE-EXCLUSION-NOT-MECHANICALLY-PROVEN` with blocker *“EVIDENCE binds structure but not an exact EvidenceDigest byte recipe.”* | R-1 `LN-13` asserts byte-identical `EvidenceDigest` across differing `ExecutionId`, and `AttemptMetadata` is “excluded by construction” — an assertion about an undefined value | Escalate. This single value carries the deterministic-retry golden |
| Finding fingerprint recipe | same `parked` list | `CoreCompletion::completed` carries `findings`; `operability.v10#projectionParity` makes `findings` an exact-mode required field across five surfaces. No artifact defines a Finding schema | Escalate. Distinct from `PUBLIC-RULE-IR`, which legitimately delegates the *internal rule representation* and delegates nothing about the evidence-relevant result type |
| `FactViewId` derivation | same `parked` list. C-2 defines only the pattern `factview1:sha256:<64 hex>` | `read-fact-view` is inside the closed stored-view query union that v1 admission must validate | Escalate |
| cache and regeneration key recipes | same `parked` list | Coverage keys are compared for exact equality across cache lookup and provider dispatch; a divergent key silently changes cache behavior | Escalate |
| `subjectScopeCommitment` | **not** in the operability list — its own owner is `c2-plan-stage-schema.v4#knownLimitations`, verbatim: *“subjectScopeCommitment: v4 binds its WIRE TYPE (sha256Id) and enforces it. HOW a real subject-scope commitment is computed and verified is still owned by the retention/evidence surface and is still REOPENED. The example digests in the coverage fixtures are reproducible over declared preimages so that the shape binding is not satisfied by an opaque constant; they are not a product commitment recipe.”* FACT-PLANE concurs. v3's blanket *“this contract does not say how one is computed or verified”* is superseded on shape only | required on every Coverage key; DELIVERY's `CoverageKeyV1` carries a concrete fixture value with no derivation | Escalate. v4 narrows the park to **computation and verification** — the wire type is now bound and enforced, and a fixture digest is still not a recipe. Recorded here because it is the same class of gap and belongs to the same owner |

Related contract gaps of the same character, named here for the same reason:
`policyOutcome.derivationDigest` is a required field of the required
`policyOutcome` on `CoreCompletion` with no preimage or domain separator, and
`capabilityManifestId` is `PLAN-ID-V1` preimage field 3 with no derivation rule
while every other `PLAN-ID-V1` input has one. Both are escalations, not choices.

Every row above must be closed by a binding artifact before signature. None may
be closed by this record, by the blueprint, by a checker, or by an implementer.

These are not residuals and must be closed before signature:

- V10/evaluation proof/custody/default/degradation/purge;
- `CD-RT-5`;
- every §7.1 parked identity recipe, and the two related contract gaps named
  under it;
- any load-bearing surface without a final seal disposition;
- an EVIDENCE head whose independent review is `REJECTED` — satisfied at
  `evidence.v10`, which passed at 0 blockers, and satisfied by nothing else: the
  EVIDENCE §3 disposition is still `UNSET`, every §7.1 recipe above is still open,
  and a passing review is not an applied artifact;
- `R2-FINAL-02`, `R2-FINAL-03`, or any other live cross-cutting open;
- any silent process/domain error-code mismatch; and
- any meta claim left `OPEN` without an explicit park/abandon/narrow disposition.

**A candidate now exists for the EVIDENCE cluster, and it closes nothing yet.**
[`evidence-identity-recipes.v1.json`](artifacts/evidence-identity-recipes.v1.json)
(`7661c58b…`) proposes byte recipes for `EvidenceDigest` and — via one
parameterised fold, not three separate constructions — `universeCommitment`,
`outcomeSetCommitment` and `subjectSetCommitment`, with 26 pinned vectors.
**`CANDIDATE-NOT-APPLIED`, `AWAITING-INDEPENDENT-REVIEW`, binds nothing**, and it
addresses exactly **one** literal §7.1 row (`EvidenceDigest byte recipe`); the
other rows above are untouched and it says so itself rather than implying
coverage. Two things make it worth reviewing rather than restarting: **two
independently written encoders agreed across 96 digest comparisons with zero
disagreements**, and **7 of its vectors reproduce digests this corpus pinned
before the artifact existed** — verified independently: each of those seven
appears in **11 to 21 other artifacts**. Injectivity is argued the way
`jx_canon`'s was — by exhibiting a **total decoder** with `decode(encode(x)) == x`
over every record of every vector — not by enumerating collisions.

**Independently reviewed 2026-08-04 —
[`REJECT`, 2 blockers](artifacts/evidence-identity-recipes.v1.review-independent.json).**
The reviewer wrote a **third encoder from the candidate's prose alone**, sharing
no code with the author, and reproduced **all 26 vectors — 52 assertions, zero
failures, first run, no value adjusted** — plus `evidence.v10`'s
`rawProofInventoryHex`, `semanticEvidenceHex` and `evidenceDigestPreimageHex`
byte-exactly. All 7 corpus digests were resolved to exact JSON paths and
confirmed **same values in the same roles**, not coincidental hex matches. Every
encoding attack failed: 1024 subsets → 1024 distinct roots; N=0..17 distinct;
folds agree to N=32; 9 domains → 9 distinct commitments. **The recipes are not
where the defects are.**

**CORRECTION — an earlier revision of this section stated a false claim as fact,
and it was mine, not the candidate's.** It read: *"The framing rule for typed
scalars is nowhere stated in prose … no artifact says which … no vector in the
corpus distinguishes them by construction."* **That is withdrawn. Both halves are
false, and both are measurable.** `evaluation-proof.v8` **does** state the rule —
`canonicalCommitmentGrammar.component` is verbatim
`"uint8(typeTag) || uint32be(len(utf8)) || utf8"`, the `utf8` settling it, with
`componentFrame` applied at ~40 typed identity/ref positions (**50 occurrences**,
measured). And a vector **does** distinguish the readings: the raw-bytes reading
yields **2271 bytes** against `evidence.v10`'s pinned **3560**. The candidate had
recovered the rule from a golden and honestly flagged it
`PROPOSED-INFERENCE-REVIEWER-MUST-CONFIRM`; **I recorded its negative claim here
as established without verifying it**, which is precisely the §7.2.2 defect — a
recorded measurement carried forward instead of compared — committed in the
record that defines §7.2.2. Recovery from a golden was **not** circular: the
reviewer found the rule stands on four independent legs. `B-EIR-01` is raised
against the candidate for the overclaimed negative; the propagation into this
record is mine.

**The remaining adjudications.**

1. **`DIV-1` — measurement confirmed exactly**: `[a,a,b]` and `[a,b]` both yield
   `6c73ad6a…`, byte-equal, so under *deduplicate* the commitment would not bind
   the multiset while `subjectCount` stays separately unbound. **Adopting REJECT
   was correct**, and the divergence is sharper than first recorded: it is **also
   an inconsistency inside `evaluation-proof.v8` itself** — its
   `recordRules.duplicates` says duplicates are *"forbidden"* while its
   `ordering` says *"deduplicate exact record bytes"*. REJECT is faithful to both
   surfaces' record rules.
2. **`DIV-2` — real, material and correctly escalated, but this record
   overstated one leg and understated the worse one.** An earlier revision tied
   it to *"blueprint §1.1's requirement that secrets be represented by handles
   only."* **Withdrawn: a path is not a credential, and that clause is §8.1, not
   §1.1.** The substantive problem is larger — the subject list is retained **in
   plaintext in the bundle** (`partitionContents[].members`), which defeats
   `evidence.v1`'s own *"~100 bytes independent of subject count"* argument. And
   R-4 specifies **no audit-path format**, so the sorting rationale
   (non-membership proofs) is currently unrealised.
3. **`outcomeSetDigest` — identification CONFIRMED, and coverage does not
   shrink.** The candidate rested it on the superseded `evidence.v2` and flagged
   it reviewer-must-confirm; the reviewer found it supported by **two current
   documents** by parallel structure. The candidate rested on a weaker base than
   exists.
4. **`B-EIR-02`** — the candidate silently drops `evaluation-proof.v8`'s
   `<= 4096 bytes` bound while keeping the other three clauses of the same
   sentence, falsifying its own universal claim that every departure is declared.
5. **No retained checker — a fair residual for a candidate, disqualifying for
   application.** The author's own objection (*"a byte recipe with no retained
   checker is a description that happens to contain digests"*) lost its premise
   when the reviewer reproduced everything by hand — but 7 vectors are pinned to
   **two unapplied, actively-moving artifacts, and nothing will notice when they
   move.** That is `B-VER9R-01` (§7.2.2) waiting to happen.

**Two things a later reader needs.** The reviewer notes the candidate is
consistently wrong **in the direction of understating itself**, which is the rare
failure mode worth naming because it is invisible to ordinary scepticism — it
argued against its own position harder than the corpus warranted and published a
false negative this record then absorbed. And: **§7.1 now contains a narrative
*about* the candidate, so it can no longer corroborate the candidate's claims.**
Anything here that reads like independent support for `evidence-identity-recipes.v1`
is not; go to the artifact and its review.

### 7.2 Standing rule — a verdict binds bytes AND an environment

**Accepted 2026-08-02. Applies to every surface, retroactively and going forward.**

> An independent review verdict binds the exact bytes reviewed and the environment
> in which they were executed. Changing either invalidates the verdict for the
> changed subject. A change to reviewed bytes requires a version bump and a new
> verdict; it may never be made in place. An environment dependency that affects
> whether the retained checker runs must be declared, or the verdict is
> environment-conditional and must say so.

Three defects found on 2026-08-02 are instances of one shape — the evidence ritual
succeeded while the property it attests did not hold. This rule covers all three:

| Instance | What happened | What the rule requires |
|---|---|---|
| `EVIDENCE v8` dead `--selftest` | `main()` returned at the errors branch before the mutation suite, so normal and `--selftest` produced byte-identical output and the 57-mutation suite never executed. The standard normal+selftest pair verified nothing while appearing to | A checker must make "the suite did not run" a distinct observable. `check-evidence-v9.py` is the reference: dirty base prints `SELFTEST-REFUSED` / `SELFTEST-NOT-RUN` and exits **3**, distinct from green (0), findings (1) and bad invocation (2) |
| `C-2 v3` post-verdict edit | `c2-storage.rereview2-reviewer7.json` returned PASS at 17:28 binding `fbba5d0a…`; `c2-plan-stage-schema.v3.json` was edited at 18:19 under the same version number. The reviewed bytes no longer exist on disk, and the live bytes `3c488ff6…` — pinned by RT22, all seven `evaluation-proof` versions and the downstream chain — carried no C-2 surface verdict | The edit required a `v4` and a new verdict. A version number binds nothing; only a digest does. **Both have since happened, and the rule was vindicated.** An independent review of the live v3 bytes returned `REJECT` with two blockers, `LB-C2-01` and `LB-C2-02` ([review](artifacts/c2-plan-stage-schema.v3.review-independent-livebytes.json)); `c2-plan-stage-schema.v4` repairs both and passed independently at 0 blockers, and is the §3 head. The unreviewed byte state was not merely unattested — it was defective, and the defect propagated into the evaluation-proof chain exactly as the pinning discipline allowed |
| `RUST-PROVIDER-PROTOCOL v4` undeclared `rg` | Checker shells out to `ripgrep` with `check=True`; absent it, both modes abort with a traceback and the `PASSED` verdict cannot be reproduced | Declared as an environment prerequisite in `IMPLEMENTER-BLUEPRINT.md` §1.1, with the verdict recorded as environment-conditional |

**Why this rule rather than three patches.** Hash-pinning in this corpus guards the
*consumption* boundary — no successor executes unverified predecessor bytes, and
that discipline works. It does not guard the *authorship* boundary. Nothing
prevented C-2 v3 from being edited after its verdict, and every downstream pin
then faithfully propagated the new bytes, hash-verified and unreviewed. This rule
closes that boundary.

**Recording obligation — a verdict must record what it verified.**

> Every independent review artifact MUST record, as data in the artifact, the
> filename and SHA-256 of **every input its verdict depends on** — the reviewed
> subject, its retained checker, and every member of the execution closure the
> checker hash-verifies and runs. A count is not a record. A prose assertion that
> *N* pins were verified is not a record. If a digest is not written down, the
> verdict does not cover it for signer purposes, however thoroughly it was checked
> during the review.

**Why this clause exists.** The signer check below compares *recorded* digests
against live ones. That comparison silently assumes review artifacts record the
digests they verify, and they do not. Measured on 2026-08-02:

| Review | Inputs the reviewer reported verifying | Digests recorded in the artifact |
|---|---|---|
| `retention-tiers.v22` | 57-path closed read set (55 pins + checker + candidate) | 12 |
| `ep8-rt13` (evaluation-proof v8) | chain through `check-evaluation-proof-v7.py` | v6 and `check-c2.py` named nowhere |

Neither is a verification failure — RT22's reviewer did the work and reported it.
Both are *recording* failures, and they have the same effect at signature: for
every input whose digest is absent, the signer has nothing to compare and the
check passes vacuously on exactly the rows it cannot see. The EP case is the
demonstration: `check-evaluation-proof-v6.py` is where the C-2 defect
`LB-C2-01` enters the evaluation-proof chain, and it sat outside every recorded
window while EP8 held a clean PASS.

**Signer check.** Before signature, confirm for every row of §3:

1. the review artifact **records** a digest for the subject, its checker, and each
   member of the verified execution closure — not a count, not prose;
2. every recorded digest equals the live digest;
3. any environment dependency is declared (see `IMPLEMENTER-BLUEPRINT.md` §1.1).

A missing record is a §8 conflict in its own right, not a residual, and may not be
discharged by a reviewer's after-the-fact statement that the input was checked.
Re-review recording the digests is the only remedy.

### 7.2.1 Standing rule — a review's subject must be frozen before dispatch

**Recorded 2026-08-03, after the second occurrence.** `check-c2-v6.py` was handed
to an independent reviewer at `6f601904…`. Its author then continued working and
the live file became `08c283d4…` while that review was in progress. The reviewer
was re-baselined mid-flight and told to record which digest each measurement was
taken against. Earlier in this corpus, `c2-plan-stage-schema.v3` was edited twice
in place after its PASS, one of those edits entirely unrecorded.

§7.2 already says a verdict binds bytes. What these two incidents show is that the
rule is not self-enforcing under concurrency: an author who has not finished, and
a reviewer who has started, will silently produce a verdict about bytes that no
longer exist. The failure is invisible from both ends — the author sees ordinary
iteration, the reviewer sees a stable file it has no reason to re-hash.

**Therefore, binding on this process:**

1. **An artifact is frozen at dispatch.** Its author must stop writing to it once
   a review is dispatched against it. Continuing work belongs in a successor.
2. **The dispatching coordinator records the digest in the dispatch itself**, and
   the reviewer re-hashes before finalising. A mismatch is a re-baseline, not a
   footnote.
3. **A review must record the digest it actually reviewed**, not the digest it was
   given. Where the two differ, the review states which measurements were taken
   against which bytes.
4. **Drift discovered mid-review is a fact about that review's conditions** and is
   recorded in it, not silently absorbed by re-running.

Neither incident produced a false verdict — the first was caught by an audit, the
second by the coordinator re-hashing before relaying a completion claim. Both were
caught by chance rather than by a mechanism, which is why this is now a rule.

### 7.2.2 Standing rule — measurements get hard comparison, invariants get semantic gates

**Articulated by an independent reviewer on 2026-08-03, adjudicating a design
split that had been made correctly and justified incompletely.** It resolves a
tension this corpus hit repeatedly: a byte-exact pin catches falsification but
breaks whenever the pinned thing legitimately advances, while a semantic gate
survives advance and is exactly what lets a declared value drift unchecked.

The axis is not strictness. It is **what the declaration is**:

| kind | example | gate | why |
|---|---|---|---|
| **recorded measurement** — "at authoring, X was Y" | a register binding, a counted total, an observed digest | **hard comparison** | an uncompared measurement is *prose that looks like evidence*. Going stale is a **true positive about these bytes**, not a false alarm |
| **continuing invariant** — "X must always hold of Y" | a dependency's direction, a closed-vocabulary membership | **semantic gate** | a byte pin fails on the very advance the invariant anticipates |

`versioning-policy.v9` gated the claim register semantically and was **vindicated
three times** as the register drifted mid-review. `v10` hard-compared a recorded
register binding and was **also** right — the reviewer explicitly declined to ask
for it to be weakened. Both are correct because they are gating different kinds
of thing.

**The failure this prevents.** `B-VER9R-01`: a checker computed the whole
v1.6→v1.14 span into a `measured` dict and then compared only 26 of 102 declared
evidence leaves against it. Seventy-six could be individually falsified and still
exit 0 — including a flag asserting the exact circularity the record existed to
refute. The evidence was gathered and then not used. No amount of widening a scan
catches that; only the rule that **a recorded measurement must be compared to the
measurement it records**.

**Corollary, learned the same day.** A registry sized from the artifact cannot
police that artifact. `versioning-policy.v10` enforced 116 of 116 carried
positions and then left 79 of its own new ones inside four loops whose length is
read from the data they check — `VER10-COVER` was structurally unreachable there,
and a **paper seal** was planted inside the block asserting
`checkerEnforcesEveryDeclaredEvidenceLeaf: true`. A partition must be bound to
something the artifact does not supply.

### 7.3 Standing rule — executing a verified closure is not building against it

**Accepted 2026-08-02. Applies to every surface, retroactively and going forward.**

> A retained checker that hash-verifies a set of files before executing them, and
> whose independent review covered that set, may internally execute superseded or
> `REJECTED` predecessors. Those files are runtime inputs of the instrument. They
> do not become normative, they do not become a fallback contract, and their
> presence does not weaken the successor's verdict — the verdict covers the
> closure it verified. An implementer obtains such a value by **running the pinned
> successor**, never by reading a predecessor's bytes into the implementation.

The blind consumer-B implementer litmus, re-run against the repaired package
([`consumer-b-implementer-litmus.v2.json`](artifacts/consumer-b-implementer-litmus.v2.json)),
raised this as `ESC2-B01`, `BLOCKING`, and was right to: at that revision the
package told an implementer both that the pinned D9 checker — then
`check-d9-v1.13.py` — is the D9 derivation oracle and that a
`REJECTED` head is not implementable and a lower version is not a fallback, while
the only route to the derivation body ran through the `REJECTED`
`d9-exit-contract.v1.12` lineage down to `check-d9-v1.10.py:769`. A compliant
implementer could not reach the oracle, and an implementer who reached it had
broken a stated rule. **That was a guidance defect, not a D9 defect**, and the fix
is the rule above plus the disclosure in blueprint §1.1 note **N-5**. The oracle is
now `check-d9-v1.14.py`; v1.13 and its checker are unchanged, retain their own
`PASSED` verdict, and are three of the 25 files v1.14 hash-verifies and executes.
Nothing here alters any byte under `artifacts/`.

Why the rule is safe on the one surface that exercises it:

- The chain is verified rather than trusted. `check-d9-v1.14.py` verifies all 25
  pinned files — the 22 its v1.13 predecessor declares, plus that predecessor, its
  checker and its independent review — before executing any retained source, and
  then executes the verified in-memory bytes; each nested level repeats this over
  its own inherited set. v1.14 additionally requires the executed v1.13 closure to
  expose byte-identical snapshots and asserts that the executed v1.13 module's own
  `PINS` equals its `INHERITED_PINS`. The v1.13 independent reviewer confirmed 22
  of 22 pins recomputed exact and that all 22 one-input corruptions, a
  verified-buffer replacement and a transitive path swap were rejected with zero
  callbacks; the v1.14 reviewer independently re-confirmed hash-before-execution
  and drove 25 pin corruptions.
- The successor's review covered the chain. The v1.13 review binds a 28-input hash
  window with `startEqualsEnd: true` and `inputHashDrift: false`, names the
  v1.11/v1.10 lineage and the retained v1.9/v1.8/v1.7/v1.6 and RT14 inputs among
  what it reviewed, and independently re-derived the class predicate, code maps and
  reducer to match all 49 rows and 399,600 reducer cases with zero mismatches. It
  states its own boundary verbatim: *"This review does not accept or apply v1.12,
  v1.11, v1.10, v1.8 or RT14. They remain exact pinned repair, runtime or consumer
  inputs only."* The v1.14 review inherits that boundary and re-derives all 45
  goldens, 4 retained core-completion rows and 6 reductions identically under both
  versions, so advancing the head did not move the derivation.
- The predecessor's rejection is bound, not bypassed, and is not a semantic
  rejection. The loader refuses to proceed unless the pinned v1.12 review is exactly
  the recorded `REJECT` with its single blocker
  `D9V112-PF-01-PREAUTH-PYTHONPATH-EXECUTION` — a defect in v1.12's declared
  `python3 -B` launch boundary, which that same review paired with
  `semanticAndReducerIdentity: PASS`. v1.13's authorized delta is precisely the
  repair: `python3 -I -B` is the sole admitted invocation. The closure is executed
  under the repaired boundary.

**Scope limit.** This rule licenses *executing* a verified closure. It licenses
nothing else. It does not apply a candidate, does not promote RT14 or any other
consumer input, does not create a fallback for a surface whose head is `REJECTED`,
and does not relieve a successor of stating its own contract. In particular it
does **not** promote the `c2-plan-stage-schema.v3` / `check-c2.py` pair that
`retention-tiers.v22` and the `evaluation-proof` chain execute inside themselves:
those bytes carry `LB-C2-01` and are runtime inputs of those instruments, never a
C-2 contract to build against — the C-2 head is **`v9`**, which passed independent
review with 0 blockers. Nor does EVIDENCE's head
passing review unpark anything: `evidence.v10`'s shape is portable under blueprint
note **N-3**, and every §7.1 identity recipe is still open. Where a
derivation exists only as an executable, that is still a real contract gap: the D9
row of §3 carries it, and it is closed by a binding artifact, not by this record.

### 7.4 Measured: the `1.0 == 1` class across the checker corpus

**Exhaustive sweep, 2026-08-03**
([`corpus-float-admission-sweep.v1.json`](artifacts/corpus-float-admission-sweep.v1.json)).
Every integer leaf of each contract was replaced, one at a time, by its float
equivalent and by `True` where the value was 0 or 1, and the checker was run.
1,279 runs, nothing sampled. Results are classified in **three** outcomes, not
two, because a non-zero exit is not evidence a guard fired — a trap that has now
caught three separate agents in this corpus:

| outcome | meaning |
|---|---|
| `ADMITTED` | exit 0. A false accept. |
| `REJECTED-BY-POSITION` | non-zero, and the finding **names the mutated leaf**. Guarded. |
| `REJECTED-COLLATERAL` | non-zero for an unrelated reason. **Not a defence** — proved by execution: a collateral-rejected bool in `check-c2-v4.py` reaches a fully green exit 0 with three edits. |

| checker | float swept / admitted | bool swept / admitted |
|---|---|---|
| `check-c2-v4.py` *(control)* | 136 / **57** | 66 / 0 |
| `check-c2-v5.py` | 66 / **13** | 4 / 0 |
| `check-trusted-request-context-v3.py` | 3 / **3** | 1 / **1** |
| `check-r1-v1.5.py` | 64 / 0 | 52 / **40** |
| `check-evidence-v10.py` | 97 / 0 | 30 / 0 |
| `check-d9-v1.14.py` | 79 / 0 | 31 / 0 |
| `check-evaluation-proof-v11.py` | 117 / 0 | 14 / 0 |
| `check-evaluation-proof-v10.py` | 84 / 0 | 12 / 0 |
| `check-retention-custody-v22.py` | 271 / 0 | 47 / 0 |
| `check-operability-v10.py` | 88 / 0 | 17 / 0 |

**Read this table correctly.** The harness was validated against the published
control and reproduced 57/136 with an *identical position set*. An earlier harness
version measured 70/136; that was a race in the sweep's own worker trees, found
and corrected before any claim was published — recorded in the artifact.

**Four findings that matter.**

1. **`check-c2-v5.py` is not clean** — 13 of 66 leaves admitted, banner
   **byte-identical** to a clean run, and all 13 survive `--selftest`, which
   prints `SELFTEST-PASS`. The admitted set includes `successorRejectedByName`,
   the counter certifying that v5 rejected all six retained false-accept vectors
   *by name*. This is `LB-C2-01`'s third occurrence, in the artifact written to
   repair its second. `c2-plan-stage-schema.v6` was in authoring when this was
   written; it was **REJECTED** on one blocker, as were v7 and v8, and the lineage
   converged at **v9**. See §3's C-2 row.
2. **`trusted-request-context.v3` and `r1-lifetime-neutrality.conformance.v1.5`
   are both `PASSED` surfaces in §3 whose checkers admit.** TRC admits at all
   three of its integer leaves and its one boolean position — including
   `version: 3 → 3.0`, **reproduced independently by the coordinator**. R-1 bans
   floats at the parser and leaves **40 of 52** boolean positions open.
3. **`resolved-inputs.v2.json` admits a float at `version`, and 29 checkers read
   it.** The sweep called this the widest blast radius. **Coordinator
   re-measurement on 2026-08-03 refines that, and the refinement matters:** with
   `version: 2 → 2.0`, of the 26 readers that could be run, **7 admit (exit 0)**
   — `check-delivery.py`, `check-evaluation-proof.py`, `check-fact-plane.py`,
   `check-operability.py`, `check-product-dispositions.py`,
   `check-resolved-inputs.py`, `check-retention-custody.py` — while **13 fail
   closed at exit 2 on pin mismatch** and 6 exit non-zero otherwise. **The
   hash-pin architecture works.** A consumer that pins the digest cannot be
   reached by a respelling at all, because the respelling changes the bytes and
   the pin catches it before any comparison happens. The exposure is confined to
   readers that consume the file **without** pinning it — which is a stronger and
   narrower statement than the sweep's, and points at a different repair: pinning
   coverage, not only comparison discipline.
4. **The recently hardened surfaces are genuinely clean.** EVIDENCE v10, D9 v1.14,
   EVALUATION-PROOF v10 and v11, RETENTION v22 and OPERABILITY v10 admit
   **nothing** on either arm. Hardening works when it is done; it has simply not
   been done uniformly.

**Why it is uniform nowhere.** A bounded screen over 17 further current-head
checkers found **10 of 11 screenable ones admit**, across 31 of 39 load-bearing
checker/input pairs. Five distinct defence designs were measured with five
different outcomes. **Nothing is shared** — every checker re-implements its own
type discipline, so coverage is a per-author accident rather than a property of
the corpus. The boolean arm is systematically weaker than the float arm
(41/208 vs 16/869 admitted across non-control pairs), because authors who thought
about `1.0` did not think about `True`.

**This is verifier apparatus, not architecture** — the classification rule in §7
applies. No contract admission surface was shown to admit: C-2's
`validate_plan_intent` correctly rejects `True`/`1.0`/`"1"`/`0`/`2` and its seven
commitments are unmoved. What is compromised is the **evidence** a checker
publishes about itself. That still matters, because §3's verdicts rest on that
evidence, which is why `IR-C2V4-01` was adjudicated **BLOCKING** rather than
advisory: where a checker's self-measurement is the only backstop, a falsifiable
counter is a falsifiable verdict.

**The standing requirement this creates.** §6 law 18 already binds the *product*.
For the *verifier apparatus*: a checker may not publish a measured counter that
its own run does not recompute and bind, and no comparison of a wire-supplied
value against a computed one may use a bare operator. The operator space is wider
than equality — `<=`, `>=`, `in`, set operations, `dict` key lookup, `max`/`min`,
`Counter` — because `hash(1.0) == hash(1)`. `c2-plan-stage-schema.v6` was tasked
with supplying this as a single reusable primitive the other checkers can adopt
unchanged. **v6 was REJECTED and the primitive landed at v9**: `jx_canon` is
length-framed and invertible, its injectivity is proved by the existence of the
inverse and re-executed on every run, and `check-c2-v9.py` sweeps 257 cases at 0
admitted. Adopting it into the other checkers is still open, and is still the
closure path §3 names for TRUSTED-REQUEST-CONTEXT and R-1.

**Bounds of the sweep, stated.** 54 checkers were never executed. Only float and
bool spellings were tried, so every count is a **lower bound**. No multi-leaf
sweep was run, `.md` inputs were not read, pin coverage was a two-leaf screen and
was not run for `check-evidence-v10.py`, and no admitted-leaf count is published
for the 17 screened checkers.

### 7.5 Measured: duplicate JSON keys across the checker corpus

**Exhaustive sweep, 2026-08-03**
([`corpus-duplicate-key-sweep.v1.json`](artifacts/corpus-duplicate-key-sweep.v1.json)).
493 checker executions, nothing sampled. `json.loads` without an
`object_pairs_hook` keeps the **last** of duplicate keys, so a document can say
one thing to a reader and another to every instrument while the parsed object
stays byte-identical to the honest one.

```
92 checkers   43 closed at their own parse sites   49 with >=1 unhooked site
40 EXPLOITABLE      47 CLOSED      zero overlap
59 admitted positions across 42 distinct artifacts
```

**It is a binary adoption gap, not partial coverage.** A checker either carries
the hook and rejects everywhere attacked, or carries none and admits. 51
checkers already define a duplicate-rejecting hook; the class was found and
repaired in the C-2 lineage days ago, and `check-d9-v1.14.py` — which
`check-versioning-v12.py` subprocesses on every run — carries the fix while its
caller does not. **A repair confined to one lineage does not propagate, and
nothing in this corpus makes a solved class stay solved elsewhere.**

**Worst single finding.** `check-versioning-v12.py`: 6 of 6 positions admitted at
exit 0. A **107-byte** insert produces the full green banner asserting *"coverage
census: 3600 leaf positions — 0 ungated"* and *"carried byte-identical … and
gated against those bytes"*, while `dischargeStatus` — whose real value carries
`BLOCKED` — reads `"SEALED: ACCEPTED"` to a human. **The gate executes on the
parsed value, not on the bytes.**

**Three methodology findings that changed the answer, and generalise.**

1. **Collateral is not a defence — measured, not argued.** `check-d9-v1.7.py`
   returned non-zero and would have read as defended; the finding was a
   **key-order** comparison. An **order-preserving** insert — the duplicate placed
   immediately before the real member, so dict key order is also identical —
   flipped both positions to **exit 0**.
2. **53 collateral rejections are sha/pin comparisons.** That is a real barrier
   for *pinned* inputs and does nothing for a checker's own candidate. **Every
   admitted position is on an unpinned input** — the hash-before-execution trust
   order covering half of yet another defect class it was not designed for.
3. **Naming the key is part of the fix.** 6 of 47 rejecting checkers never say
   which key was duplicated — in three because the hook is generic, in three
   because the hook names it and the reporting layer discards it. An operator
   learns the file is bad but not where.

**The transitive tier is larger than the direct one.** 36 checkers inherit
unhooked parses from predecessors they import in-process — **21 of them carry the
fix themselves**. `check-evidence-v10.py` has 0 own and 280 inherited.
`check-d9-v1.14.py` carries the hook and still executes 170 unhooked decodes via
`check-d9-v1.12.py`. The widest single site is
**`check-evaluation-proof.py:269` in `_grammar()` — the normative preimage
grammar — reached in-process by 15 unrelated checkers.** Repairing that one site
and `check-d9-v1.12.py` closes inherited exposure for 21 already-hooked checkers.

**Repaired on discovery:** `check-package-coherence.py` was on the exploitable
list at **1,810 unhooked decodes per run**. All three of its parse sites now route
through one hooked entry point that **names** the duplicated key.

**Bounds, stated.** No `--selftest` runs, so whether a checker's own suite catches
this is unmeasured for all 92. Nested duplication was executed on 5 paths only, so
blast-radius object counts are a structural bound rather than a measured nested
admission rate. One key per (checker, input). Subprocess-spawned parses were not
instrumented, so inherited counts are a **lower bound**. `check-adjudication.py`
exits 2 before reaching JSON and was not exploit-tested.

### 7.6 Structural: immutability prevents a proven fix from propagating

§7.5 ends with *"a repair confined to one lineage does not propagate, and nothing
in this corpus makes a solved class stay solved elsewhere."* That was written as
an observation about habit. **It is not. It is a consequence of §7.2, and it is
load-bearing.** §7.2 binds a verdict to bytes, so a reviewed checker cannot be
edited — which means the corpus is, by construction, **almost entirely
unrepairable in place**.

**Measured 2026-08-04, independently of the adoption pass, and it agrees with
it.** Every `artifacts/check-*.py` digest was computed and the whole tree
searched for each at 64-, 32-, 16-, 12- and 8-character prefixes in both cases,
excluding each file's own bytes and excluding the three documents that declare
themselves measurement-only:

```
93 checkers    88 pinned at their CURRENT bytes    5 carry no current-byte pin
no current-byte pin: check-adjudication.py       check-completeness.py
                     check-method-dispositions.py  check-package-coherence.py
                     check-retention-v3.py
```

**But one of those five is not free, and the way it stopped being pinned is
this section's whole point.** `check-completeness.py` **is** pinned — at
**predecessor** bytes, by **11 review and adjudication artifacts** across two
distinct digests (`f6760454…` in 6, `b0bf852f…` in 5), each recorded as a
`sha256` in an object naming the file. It carries no *current*-byte pin because
it was **edited on 2026-08-04**, and the edit silently invalidated all eleven.
Nothing stopped it. Nothing reported it. **The corpus reproduced this section's
finding on itself, in miniature, on the same day the section was written** —
which is precisely why the count above is stated as *"pinned at their current
bytes"* and not as *"unpinned"*. A current-digest scan measures which pins are
**satisfied**, never which pins **exist**, and reading the first as the second
is how an editor concludes a reviewed file is free.

**So the genuinely editable surface is 4 files out of 93, and all 4 are already
repaired.** The duplicate-key adoption pass closed everything it lawfully could
and stopped — not from lack of effort but because there was nothing left it was
permitted to touch.

**What the eleven broken pins do and do not mean.** They do **not** falsify
those reviews' findings about their own subjects; each still binds its own
artifact's bytes. What they lose is §7.2's *other* half — **a verdict binds bytes
AND an environment** — so eleven recorded environments no longer reproduce. That
is a real cost, it was incurred to repair a genuine instrument defect
(`CMP-IR-01`, §7 — the repair was independently reviewed at 0 blockers), and it
is recorded here rather than absorbed. **A signer should know that
`check-completeness.py`'s figures are produced by bytes that eleven prior
reviews did not run.**

**36 checkers remain exploitable and none of them can be fixed** — 26 hard-pinned
by another checker, 10 pinned only by review artifacts. **Both Tier-1
multipliers are among them**, which is the sharp end: repairing
`check-evaluation-proof.py:269` (`_grammar()`, reached in-process by 15
unrelated checkers) and `check-d9-v1.12.py` would close inherited exposure for
**21 checkers that already carry the fix themselves** and are undermined by
their dependencies. It is the highest-value repair available anywhere in this
corpus, it is fully understood, and **it is prohibited.** `check-evaluation-proof.py`
is pinned by 54 files including 17 checkers; `check-d9-v1.12.py` by 26 including
11 checkers and the blueprint.

**The same arithmetic governs contracts, not just checkers, and the worst case
is the architecture plan itself.** Measured 2026-08-04:
`ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md` at `47df412d…` is recorded by **40
files** — 7 checkers, 18 review and adjudication artifacts, 12 further
contracts, and 3 markdown documents. It is the most heavily pinned object in
the corpus, and **a single appended newline is enough**: seven
`check-retention-custody-v16…v22.py` exit **2** with `AuthorityError: dependency
hash drift` before any contract is examined, which is not a hypothetical — it
happened during this session's Gortex work and had to be reverted. **Editing
that file is not expensive; it is closed.** Any change to it is a §10 successor
exercise across 40 recorded citations, and no one should discover that mid-edit.

**One thing that is NOT a defect, recorded because it looks like one.**
`retention-tiers.v24.json` records the plan's digest at
`$.recordedInputs.citedNotGated[1]`, and `check-retention-custody-v24.py`
validates that row's shape, path and count but **never recomputes the digest**.
That is disclosed, not hidden: the key is named `citedNotGated`, the row's own
`gate` field reads `RECORDED-ONLY`, and the checker **prints** *"N further inputs
recorded with a digest and not gated"* in its banner. A surface that names its
ungated region is doing the opposite of §7's dominant failure mode. Contrast
`citedNotGated[0]`, whose `gate` is `CONTENT-ANCHOR-PREDICATE` — that one **is**
enforced, and is the mechanism described in §2 that makes this record itself
semantically pinned. **Do not "repair" a `RECORDED-ONLY` row into a gate without
deciding that it should be one**; the honest disclosure is the feature.

**This is a correct outcome, not a defect in §7.2.** A rule that let a
coordinator edit reviewed bytes because the edit *looked* safe is exactly the
rule that produced §4.4. The cost is real and belongs in the record; the rule
stays.

**What follows for the signer — three things, and the third is the one that
matters.**

1. **The lawful repair path is a successor plus a re-issued review**, never an
   edit. For the two Tier-1 multipliers that is two authored successors and two
   independent reviews, and it cascades: every checker pinning the old digest
   needs a successor too. Nobody should start it before signature.
2. **10 of the 36 are pinned by review artifacts only.** Re-issuing those
   reviews against successor bytes is materially cheaper than the hard-pinned
   26. **Whether to spend that is the product owner's call, not the
   coordinator's** — it is recorded here unspent.
3. **Retrofit is the wrong instrument and must not become the plan.** The
   editable surface is bounded at 5 files *by design* and shrinks every time a
   review is issued, so a strategy of chasing defect classes through the frozen
   corpus converges on doing nothing. **The correct response is build-time, not
   repair-time**: duplicate-key rejection (§7.5) and exact-type scalar admission
   (§6 law 18) are normative for every checker written during implementation, so
   the property is carried from birth. That is recorded in the blueprint as a
   construction requirement, and it is why neither is listed here as
   remediation work.

**Scope, stated plainly so it is not read as worse than it is.** These are
**verification instruments, not shipped product code**; no v1 binary inherits
this exposure. What a reader may *not* conclude is that a green corpus is a
corpus that resists a hostile document. 36 of these checkers do not, they cannot
be made to, and every one of them will still report exit 0 while doing it.

## 8. Implementer litmus

Before signature, give a strong Rust implementer only this freeze record, the
blueprint, and direct contract links. The package passes if they can answer,
without reading `agentlog*`:

- which lifecycle point allocates each identity;
- which component may read the worktree, spawn a provider, write durable state,
  seal a Run, derive policy, and exit the process;
- how CI handles layer 4;
- why syntax is not globally weaker than semantics (§6 law 3 states the
  proposition and names its corroborating sites; it is meant to be read there,
  not reassembled);
- what a provider-unavailable predicate does;
- how an exact graph accelerator differs from a semantic graph producer, and what
  happens when the accelerator is absent, corrupt, partial, or stale;
- which process contains `rustc_driver`, how it is identified, and why it is not
  a sandbox;
- how to obtain the D9 axes-to-class derivation, and why executing the pinned
  checker's verified closure is compliant while transcribing a predecessor
  contract is not;
- what retained objects establish a no-match and verdict after Phase 1A;
- what happens after proof expiry/purge without rewriting the sealed Run;
- which crate owns every binding contract and first golden; and
- which apparent features must reject rather than be stubbed.

They may escalate only a named residual or a detected conflict with a binding
artifact. The named set is: the §7 non-blocking residual table, the §7.1 parked
identity recipes and the two related contract gaps under it, the
**`[PHASE-1A / V10 BLOCKER]`** markers, the three D9 contract gaps named in the §3
D9 row — observation-to-`faultCause` selection, optional-field presence policy, and
the `success`/`policy-failed`/`interrupted` branch — and any file whose recomputed
digest disagrees with its §3 / blueprint §1.1 pin. Being unable to execute
`check-d9-v1.14.py` is a detected conflict of the same class: escalate it, and do
not substitute a hand-written axes-to-class function. The `rust-provider-protocol.v4`
`d9JoinV4` pin recorded in §3.2 item 6 is a named detected divergence and is
escalable on the same footing.

**A withheld disposition is escalable in its own right, and this list did not say so.** Added
2026-08-03 after a litmus rehearsal reached `IR-C2V4-01`, which the enumerated set above described
only through the residual table it had been **removed from**. That particular case has since
closed: C-2 converged on `c2-plan-stage-schema.v9.json`, whose §3 row records **PASSED — 0
blockers** and disposition **`SEAL` candidate**, and `IR-C2V4-01` is **superseded, not withdrawn**
— it remains falsifiable on `check-c2-v4.py`'s frozen bytes, which no longer bind any surface. The
gap the case exposed is not closed by its closing, so the rule stands as a property: **any surface
whose §3 disposition column withholds a seal is escalable under this section's other limb — *a
detected conflict with a binding artifact* — whatever the review verdict column says.** A `PASSED`
verdict records what that review found; a finding inside it may later be adjudicated to a different
grade, and the verdict column is then necessary but not sufficient. The surfaces this applies to
today are **EVIDENCE** and **TM**, both **`UNSET — BLOCKS FREEZE`**. Read the disposition column,
not the verdict column, and read it at the time you build.

That this list needed amending — and then needed amending again when the case it named was
repaired — is itself the §7.4 lesson: an enumeration of named items goes stale silently in **both**
directions, while the limb stated as a property — *a detected conflict with a binding artifact* —
covered the case correctly without being edited either time. If they must choose retention, invent
a second store authority, decide the core effect boundary, select a Rust
substrate, choose layer-4 CI behavior, create an exit mapping, or decide which
version of a binding artifact is normative, this freeze fails.

Give them the package at the digests in §3 and blueprint §1.1. A litmus run
against stale links measures the links, not the architecture — that is what the
second litmus found, and it is why §1.1 exists.

## 9. Phase-4 verification record

Fill this section from a clean run against the converged payload.

### 9.1 Required checks

- [ ] `check-claims.py` passes.
- [ ] `check-completeness.py` reports **13/13 independently reviewed**, **zero
      cross-cutting opens**, and the agreed final seal-ready bar; and its
      contract-shape figure is recorded with every surface scoring below 4/4
      accounted for by `CMP-IR-01` (§7) or by a named finding.

      **The denominator is 13, not 11.** An earlier revision of this checkbox
      required *"11/11 shape, 11/11 independently reviewed"* — a bar the
      instrument can no longer express and that no signer could ever tick. It is
      withdrawn. The denominator moved when `TRUSTED-REQUEST-CONTEXT` and
      `RUST-PROVIDER-PROTOCOL` were registered in
      [`claim-register.v1.json`](artifacts/claim-register.v1.json), which is a
      **widening of coverage**, not a regression: two independently reviewed
      surfaces the instrument previously could not see are now inside every
      figure it prints.

      **Contract shape is deliberately not required to reach 13/13**, and after
      2026-08-04 that is *more* true rather than less. `CMP-IR-01` records that
      the predicate is name-based for **12 of 13** surfaces — the instrument
      prints that reach itself. C-2's 2/4 was an instrument artifact and was
      repaired by making the reader resolve derivations, taking it to 4/4; the
      **two remaining shortfalls are instrument artifacts too**, now measured and
      not merely suspected. `RUST-PROVIDER-PROTOCOL` (3/4) carries 6
      `semanticConformanceVectors` and `TRUSTED-REQUEST-CONTEXT` (2/4) carries 30
      `adversarialControls` and a 13-member `capabilityContract`, all invisible
      because **both predicates scan top-level keys only**. **So 13/13 shape is
      reachable only by further instrument work on surfaces that are already
      complete**, and requiring it would make the checkbox untickable for the
      second time. The signer's obligation is to record the figure and account
      for each shortfall, not to drive it to the maximum — and both shortfalls
      are accounted for here.

      Live at the time of writing: shape **11/13**, reviewed **13/13**,
      seal-ready **9/13**, cross-cutting opens **1** (`R2-FINAL-03`), exit 1 on
      that open. **An earlier revision recorded 10/13 and 8/13**; both moved +1
      on 2026-08-04 when the derivation-aware reader was built and independently
      reviewed at 0 blockers, and **exactly one surface moved**. Re-measure; do
      not copy these.

      **The single cross-cutting open cannot be closed by running another
      litmus, and a signer must not read it that way.** The register states the
      condition in full at `crossCuttingSealBlockers[0]`: *"`R2-FINAL-03` remains
      OPEN pending final blind consumer-B implementer litmus **after all surface
      adjudications and V10 resolution**."* The litmus is **necessary and not
      sufficient** — it is gated on **V10 resolution**, which is §3.1's Phase-1A
      insertion and therefore on `CD-RT-5`. A litmus run *before* V10 resolves is
      a **staging** litmus: it is worth running, it finds real defects, and it
      **is not the final one**, because the register requires the final one to
      come afterwards. The gating litmus of 2026-08-04 returned `LITMUS-PASS` and
      found eight defects, all since repaired; **it did not close `R2-FINAL-03`
      and could not have.** Do not record any pre-V10 litmus as discharging it.
- [ ] Every retained binding checker passes normally. **Two known exceptions, named
      here so a signer meets them with their cause instead of discovering them at
      the console.** An unexplained red checker at signature time is the §7.4
      failure mode.
    - **VERSIONING has two checkers on disk and only one is retained.**
      `check-versioning-v8.py` **is the registered validator** — it is what
      [`claim-register.v1.json`](artifacts/claim-register.v1.json) names at the
      VERSIONING claim's `validator`, it is the checker in blueprint §1.1's
      VERSIONING row, and it **exits 0**. `check-versioning.py` is its superseded
      predecessor and is **permanently red by construction**, so its exit code
      carries no information about VERSIONING: it hardcodes
      `BINDING = "versioning-policy.v4.json"` as its subject, so invoked bare it
      reports the `VER-DEP` / `B-SCV2-06` stale-D9-citation finding recorded in
      §3's VERSIONING row and exits 1; pointed at the v8 head it raises
      `AttributeError: 'str' object has no attribute 'get'` at
      `check-versioning.py:1249` and exits 1 there too — **indistinguishably from
      a finding**, which is itself why it is not the retained instrument. Neither
      exit is a VERSIONING defect and neither may be recorded as one. §7.2 forbids
      editing it in place; it is superseded, not repairable.
    - **`check-threat-claims.py` exits 1 on TWO findings, not one.** It is TM's
      retained binding checker per blueprint §1.1. Measured live 2026-08-04, the
      complete output is:

      ```text
      2 finding(s):
        - T1 07-outcomes-and-failure.md: unqualified confinement claim
        - T1 08-surfaces-and-topology.md: unqualified confinement claim
      ```

      **An earlier revision of this exception said "its single finding is `T1
      07-outcomes-and-failure.md`" and named the second file nowhere in either
      document. That is withdrawn.** The correction changes no build decision and
      is recorded anyway, because an exception that understates its own
      measurement defeats the purpose of writing it here: a signer who meets a
      two-finding console having been promised one cannot tell an accounted
      exception from a fresh regression, which is the §7.4 failure mode this
      checkbox exists to prevent.

      **This was `B-VER9R-01`'s shape (§7.2.2) inside the freeze's own
      verification record.** §7.2.2 classifies "at authoring, X was Y" as a
      **recorded measurement** owed a **hard comparison**, and its named failure is
      *"a recorded measurement must be compared to the measurement it records."*
      A finding count is exactly such a measurement, and this one was carried
      forward instead of re-run. The rule the corpus wrote for its checkers had
      not been applied to its checklist. **Do not copy the count above; re-run the
      instrument and record what it prints.**

      **Both findings are the same class and neither moves a build decision.**
      Both are `T1`, raised by the same scan over `architecture/*.md` — which §2
      admits only as **narrative rationale**, last in the authority order and
      binding on nothing — and both report the same predicate on a different
      narrative file. Neither is against `threat-model.v3.json`: **every JSON
      self-consistency check in the instrument passes**, and the T1 scan is marked
      in the checker's own source as *"prose claims, still outside JSON
      self-consistency."* TM's §3 disposition is already **`UNSET — BLOCKS
      FREEZE`**, and blueprint §1.1 records the storage/namespace/read-set
      surfaces as buildable while durable-authoritative retention is not. Closing
      them means either qualifying the confinement sentence in **each** narrative
      file or a TM successor carrying a new verdict — successor work under §10,
      not a condition an implementer can discharge. Until then this checkbox is
      ticked **only** with this exception, at its re-measured count, written into
      the record beside it.
- [ ] Every retained checker mutation/selftest passes, including Phase-1A and
      product-disposition instruments.
- [ ] The checker inventory in OPERABILITY design-integrity and the actual
      binding artifacts agree.
- [ ] The implementer litmus in §8 passes.

The next five are **mechanised** — do not perform them by hand. Run
`python3 -I -B artifacts/check-package-coherence.py` and record its output; it
must exit 0. Its `--selftest` must also exit 0, having executed its full
mutation suite rather than refusing on a dirty base. Checking these by eye is
how the ledger and the blueprint drifted apart in the first place, and how the
claim registry drifted from both. *(An earlier revision said "the next four",
written before `PC-7` was added below; there are five.)*

**Neither of those two conditions is met today, and the cause is `PC-7`.** Measured
live 2026-08-04: the checker exits **1** on **two** `PC-7` findings — the pinned
`rust-provider-protocol.v2.json` base, and `threat-model.v3.json` — and
`--selftest` returns `SELFTEST-REFUSED: base is dirty` at **0 of 9 mutations
executed**, so the mutation suite is currently unexercised.

**The second `PC-7` appeared on 2026-08-04 and is a true positive. Do not read it
as a regression, and do not narrow the check to remove it.** TM's §3 row required
*"independently re-review physical ProjectId namespace"*; that review has now been
performed and returned
[**`REJECT` at 3 blockers**](artifacts/threat-model.v3.storage-namespace.review-independent.json)
scoped to `$.storageNamespace`. `PC-7` grades an artifact by its own review's
outcome, so a fresh `REJECT` against pinned bytes is exactly what it exists to
surface — the finding's own detail reads *"freeze says PARTIAL, blueprint says
PARTIAL"*, which is accurate. **This is the check working on new evidence, and the
count moving from one to two is the corpus learning something, not breaking.**

**Note what the reviewer declined to do, because it generalises.** `PC-7` scores
**counts before prose**: `len(blockers)` drives it, so filing an honest blocker
under the mandated review filename *necessarily* raises the finding count. A
verdict-object shape would have scored `UNCLEAR` and silenced it — the reviewer
verified that it works and **refused to use it**, on the grounds that the
checker's own source names that manoeuvre *"how a guard becomes a rubber
stamp."* Any future reviewer meeting the same coupling should refuse it the same
way: **the correct response to an instrument that reports your finding is to
report the finding.** **That is the check working, not a defect**, and it is
named here so a signer meets it with its cause rather than at the console. `PC-7`
grades the pinned artifact's own review outcome, so no prose in this record can clear
it; §3's base-rejection record supplies the disclosure and the discharge that make its
firing informative rather than misleading, and §3.2 item 5 carries the §2 rule 3
resolution. Only a RUST-PROVIDER-PROTOCOL successor that stops pinning rejected bytes
clears it. **Do not narrow `PC-7` to tick these boxes.**

- [ ] All relative links in this record and the blueprint resolve. *(mechanised:
      `PC-1`, over prose links as well as table rows.)*
- [ ] Every filename and SHA-256 in §3 equals the corresponding row of
      [`IMPLEMENTER-BLUEPRINT.md`](IMPLEMENTER-BLUEPRINT.md) §1.1, and every
      pinned digest equals the recomputed digest of the live file. *(mechanised:
      `PC-2` recomputes every recorded digest against the live bytes; `PC-3`
      compares the two documents artifact-by-artifact; `PC-4` compares verdicts.)*
- [ ] No document in the signed payload links a binding artifact at a version
      other than its §1.1 head, and no linked head has a `REJECTED` independent
      review. *(mechanised: `PC-5`, which grades staleness by **review outcome**
      rather than version number — a higher-numbered sibling whose review records
      blocking findings is correctly **not** treated as head.)*
- [ ] The claim register's binding citations equal the §1.1 heads. *(mechanised:
      `PC-6`. Added after the register was found citing an independently
      **REJECTED** `retention-tiers.v5` while v22 was head, and `evidence.v1`
      while v10 was head — with `check-completeness.py` computing seal-readiness
      from those stale citations the whole time.)*
- [ ] **No artifact pinned as normative carries a `REJECT` on its own bytes.**
      *(mechanised: `PC-7`. Added 2026-08-04 after the gating implementer litmus
      found `rust-provider-protocol.v2.json` pinned in §1.1's normative byte set
      and named by §3.2 as half the Rust wire contract, while the review binding
      its exact digest — `sha256AtStart == sha256AtEnd`, `stable: true` — returns
      **`REJECT`, 2 blocking**, with `effect`: "must not … be used as
      implementation authority". At the time `PC-7` was written neither document
      mentioned that review — zero occurrences in each — and §2 rule 3 forbids
      implementing a `REJECTED` version. **That silence is now repaired:** §3 carries
      the base-rejection record disclosing the `REJECT` and adjudicating both blockers
      `DISCHARGED-BY-V4`, blueprint §1.1's base row states the same verdict and links
      both artifacts, and §3.2 item 5 resolves the rule-3 tension. `PC-7` still fires,
      because the pinned artifact's review outcome has not changed and cannot without a
      successor.)*

      **Why the existing checks did not catch it, which is the transferable
      part.** Verdict comparison asked only whether the two documents **agree**.
      They did — the freeze said `PASSED`, the blueprint said nothing, and
      one-sided silence had been classified as benign row-grouping. But
      **agreement between two documents is not a fact about the artifact.** A
      recorded verdict must also be true of the bytes it pins, and only the
      review answers that. `PC-1`…`PC-6` compare documents to each other and to
      disk; `PC-7` is the first that compares a document to a **verdict**.

      Building it exposed two defects in the checker itself, both of which failed
      in the unsafe direction for `PC-5` as well:
      **(a)** `review_state_of` substring-matched `"REJECT"` before consulting
      the blocker count, so a paragraph-length verdict that merely *mentions*
      rejecting scored REJECT — it produced a false positive against
      `c2-plan-stage-schema.v9`, which passed with `blockers: []`. Counts now
      decide first; prose is read only as a **leading token**, because a verdict
      states its outcome first and explains after.
      **(b)** A review declaring its subject as the *sentence* "repairs to
      `check-claims.py`, `claim-register.v1.json`, and status restatements" was
      attaching its `reject-require-v2` verdict to the claim register. A
      **structured** subject declaration assigns subjecthood; a bare string
      naming several paths describes a pass over them. This is the third
      instrument in this corpus to need that exact distinction.

      **Swept after repair: 46 artifacts referenced by the two documents, exactly
      one carries a `REJECT`** — `rust-provider-protocol.v2.json`. The defect is
      isolated, not systemic. The referenced-path count is a live figure and has
      since moved to **48**, the two additions being the v2 review and its blocker
      adjudication linked by the §3 base-rejection record; the finding count is
      unchanged at one. Re-measure it from the checker's `pathsReferenced` line; do
      not quote either number from here.

- [ ] **The §2 non-JSON payload pins are recomputed and equal.** Run
      `shasum -a 256 docs/coop/v1-slice.md docs/coop/ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md`
      and compare to §2: `v1-slice.md` =
      `6b8717fef545fe73f0de5879a7389fbc0c7c499c70e06b344789e5150478bee3`;
      `ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md` =
      `47df412dba5d62a823ca7c008c382c489b8a10c797fd8656f3d4dd5d6c342e2e`. **This one
      is deliberately not mechanised by `check-package-coherence.py`** — `PC-2` binds
      only paths ending `.json`, so it cannot see either file, and no table placement
      would change that. It is listed as a signer action precisely so the `v1-slice.md`
      pin added on 2026-08-04 is a *compared* measurement rather than the uncompared
      kind §7.2.2 names. The plan's digest carries a second, stronger enforcement of
      its own: seven retained `check-retention-custody-v16..v22.py` instruments
      hash-verify it and exit **2** before checking anything if it has drifted.
- [ ] Every §7.1 row has been closed by a binding artifact, or signature is
      withheld.
- [ ] The snapshot/tag contains the otherwise-easy-to-lose `docs/coop/` tree.

Record exact command, tool versions, and output reference:

```text
Python: [UNSET]
Commands: [UNSET]
Retained output/evidence: [UNSET]
Completeness: [UNSET]
Cross-cutting opens: [UNSET]
Product qualification: expected NOT-RELEASE-QUALIFIED unless separately demonstrated
```

**STAGING CAPTURE 2026-08-04 — NOT the signature record above, which stays
`[UNSET]` deliberately.** §9 requires the block above to be filled *"from a clean
run against the converged payload"*, and **the payload is not converged**:
EVIDENCE and TM still carry `UNSET — BLOCKS FREEZE` in §3, and §3.1's Phase-1A
insertion has not happened. Filling the signer's block from a pre-convergence
tree would be the §7.2.2 defect — a recorded measurement that looks like
evidence. So the values below are recorded **separately, and with the tree they
were taken against**, so a signer can test in one command whether they still
hold rather than trusting them:

```text
Python:      3.14.6 (main, Jun 10 2026, 10:03:53) [Clang 21.0.0]
Host:        Darwin 25.5.0 arm64 (macOS 26.5.2, build 25F84)
Taken against:
  ARCHITECTURE-TO-IMPLEMENTATION-PLAN.md  47df412dba5d62a823ca7c008c382c489b8a10c797fd8656f3d4dd5d6c342e2e
  claim-register.v1.json                  1a16f7510a9ab3347c5dae2a6d2c2c7b846ed3dfcdc6a582bb545cb44e8f3df9
  check-completeness.py                   6c52a5f9a4ac6a3ec3dae9fb0c87e82552744b18eb8cc38d1c4522ade3e549d6

Command:     python3 -I -B artifacts/check-completeness.py          -> exit 1
  contract-shape completeness:          11/13
  independently reviewed completeness:  13/13
  seal readiness:                       9/13
  cross-cutting open findings:          1  (open: R2-FINAL-03)
  product qualification:                NOT-RELEASE-QUALIFIED (0/25 demonstrated)

Command:     python3 -I -B artifacts/check-package-coherence.py     -> exit 1
  FINDINGS 1 (PC-7, accounted above)   freezeRows 18   pathsReferenced 49
  pathsMissing 0                       digestsBound 40   digestsVerified 40
```

**How to use this block: re-run, do not read.** If any digest above has moved,
every figure under it is void — that is the point of recording them together.
Exit 1 on both instruments is expected and accounted for above; an exit 0 from
either would itself be the surprise worth investigating.

### 9.2 Payload hash and snapshot

The signer must create a deterministic file manifest for the complete
`docs/coop/` snapshot, excluding this file and the manifest itself so neither is
self-referential. The manifest records every other sorted relative path, byte
length, and SHA-256 digest. Hash the canonical manifest bytes with SHA-256 and
record that digest in this file. The git tag/commit or tarball captures the
payload, the manifest, and this signed record together.

```text
Manifest artifact: [UNSET]
Manifest SHA-256: [UNSET]
Snapshot/tag/commit: [UNSET]
Freeze date/timezone: [UNSET]
```

### 9.3 Payload manifest tooling

§9.2's recipe is executable: `python3 -I -B artifacts/make-freeze-manifest.py`
writes `artifacts/freeze-payload-manifest.txt` and prints the digest to record.
It is deterministic — nothing about the run enters the hashed bytes, so two runs
on the same tree agree, and a manifest that embedded a timestamp would make the
payload hash unfalsifiable rather than merely unverified.

`--verify` re-derives the manifest and diffs it against the stored one, naming
every added, removed and changed path. **That is the reason to generate it with a
tool rather than by hand: the question "does the payload still hash to what the
signature claims" stays answerable after signature, by anyone, at any time.**

## 10. Post-freeze change control

After signature, a change to a binding artifact, v1 scope/product disposition,
non-negotiable law, process authority, or dependency direction requires a short
written delta under `docs/coop/deltas/` containing:

1. the reason and new evidence;
2. affected claims, artifacts, modules, fixtures, and product behavior;
3. old and new normative text/shape;
4. checker and mutation changes;
5. independent review/adjudication;
6. compatibility/migration impact; and
7. the new freeze version, payload manifest, and snapshot reference.

An internal refactor needs no architecture delta only when it preserves every
binding behavior and forbidden dependency edge. An implementation discovery that
contradicts a contract is a design delta, not permission to silently reinterpret
the contract.

## 11. Signature block

Architecture Freeze v1 is declared only when all fields are complete:

```text
Disposition: [NOT FROZEN]
Freeze version: [UNSET]
Date: [UNSET]
Payload hash: [UNSET]
Snapshot/tag: [UNSET]
Architecture signer: [UNSET]
Product signer (scope + CD-RT-5): [UNSET]
Implementer litmus reviewer: [UNSET]
Named non-blocking residual IDs: [UNSET]
```

Until then, this file is a coordination artifact and carries no permission to
start Phase-5 product implementation.
