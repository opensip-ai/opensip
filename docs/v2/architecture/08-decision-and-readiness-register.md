# OpenSIP V2 Decision and Readiness Register

> **Status:** ACTIVE WORKING REGISTER — non-binding
> **Authority:** None. V1 sources remain authoritative; this register controls
> only V2 review workflow and the decision to begin a later blueprint.
> **Blueprint readiness:** **BLOCKED**.

This is the single human-readable checklist for V2 architecture readiness. Topic
documents explain the design and link here; they do not maintain competing
open-decision, blocker, review, or release-gate lists.

## How to use the register

Each row names an owner or decision authority, exact source pin, required
acceptance evidence, status, and blueprint impact. A row may close only by
linking the exact reviewed successor or retained evidence. Narrative agreement,
a passing checker, or a V2-local edit cannot close an inherited V1 prerequisite.

Status vocabulary:

- `HARD-BLOCKED` — blueprint may not start.
- `OPEN` — architecture/product decision not yet taken; blueprint impact is in
  the row.
- `PROPOSED-CLOSED-FOR-REVIEW` — V2 prose now addresses the review finding, but
  no binding successor or qualification is implied.
- `DECIDED-V1-NOT-INTEGRATED` — product authority decided the posture, while the
  required accepted successor remains missing.
- `SATISFIED` — exact acceptance evidence is linked and independently reviewed.

## Inherited V1 prerequisites

| ID | Condition | Owner / decision authority | Exact source pin or selector | Required acceptance evidence | Status | Blueprint impact |
|---|---|---|---|---|---|---|
| DR-001 | Authority baseline and status evidence must resolve without path/SHA/selector/status/disposition conflict | V1 coordinator/status authority | [`v1-authority-baseline.json`](v1-authority-baseline.json); [`v1-status-evidence.json`](v1-status-evidence.json); [claim matrix](09-v1-to-v2-claim-matrix.md) | Re-generated manifests; full digest match; every standing selector read from pinned review/adjudication/closure/checker bytes; resolved derivations; explicit design delta for every conflict | HARD-BLOCKED | Any mismatch stops all blueprint work |
| DR-002 | EVIDENCE needs an applied successor and Phase-1A result | Evidence authority + V1 coordinator | freeze §3 EVIDENCE; `evidence.v10` `62a3a07194062c8499f6e943b4986d7a77bdecc0c4ec499851ac078fd548e9b4`; claim `EVIDENCE=CANDIDATE` | Applied evidence successor, independent review, final claim/status disposition, Phase-1A proof/custody insertion | HARD-BLOCKED | Structural host authority may be documented; recipes/schemas/replay results may not be designed as settled |
| DR-003 | TM remains `UNSET — BLOCKS FREEZE` | Threat-model authority + V1 coordinator | freeze §3 TM; `threat-model.v3` `56734a4047b61e1fc702f75ccb21e8721b334adb449093d266756d0b08adc499`; applied namespace derivation `94b68f6d504967b61c9daf4884cad90d2e5de63af3b40aeda99d28b59513b5be` | Reviewed closure of V10/custody and G19, publication block satisfied by required demonstration, final disposition | HARD-BLOCKED | No V2 blueprint or security-complete claim |
| DR-004 | Mandatory Phase-1A proof/custody insertion is absent | Evidence/retention authority | freeze `010f9b11a243b4a84357cad435a9e09c0bc44d7d4596fad1b16b68e07c29a27e` §3.1; product `CD-RT-5.whatThisDecisionDoesNOTDo.phase1A` | Exact packet inserted through the V1 process with retained proof, custody, joins, and status update | HARD-BLOCKED | Blocks EVIDENCE, TM, G19, authoritative analysis blueprint |
| DR-005 | V10/custody and G19 durable-authoritative mechanism remain unresolved | Evidence, storage, operability authorities | freeze `010f9b11a243b4a84357cad435a9e09c0bc44d7d4596fad1b16b68e07c29a27e` §3 EVIDENCE/TM/OPERABILITY; `operability.v10` `9bacbbf43dfb941a0d87330f79844d395b3ac838ae5bf54026ef4d69681696be` G19 limitation | Applied evidence/retention/D9 integration with executable custody and durable-authoritative negative controls | HARD-BLOCKED | Blocks authoritative storage/recovery/replay implementation design |
| DR-006 | Freeze §7.1 identity-recipe property and exact FACT-PLANE closure items remain open | Each identity-owning V1 surface + FACT-PLANE/evidence authorities + coordinator | freeze `010f9b11a243b4a84357cad435a9e09c0bc44d7d4596fad1b16b68e07c29a27e` §3 FACT-PLANE, §7.1/§9, laws 6/19 | Binding recipes; Phase-1A subject-set agreement; declared sufficiency `view` type and closed `rungUnavailableBecause` vocabulary; retained negative controls; exact derivation/custody joins; independent review | HARD-BLOCKED | Run/evidence identities stay conceptual; facts/Coverage blueprint cannot invent sufficiency view or unavailable-rung vocabulary |
| DR-007 | D9 JSON still has three checker-derived gaps and no accepted retention-loss result/exit integration | D9 authority + evidence/retention owner | freeze §3 D9; `d9-exit-contract.v1.14` `8dd3303855f49bfdbb2751ee65f54a906405f0654159ebe815472f73cdf7da31`; `CD-RT-5` correction | D9 successor for observation→faultCause, optional presence, success/policy/interrupted branch, plus reviewed retention degradation/refusal integration without invented codes | HARD-BLOCKED | V2 cannot define replay/purge/degradation typed result or exit |
| DR-008 | Retention product posture is decided, but accepted retention/evidence successor is missing | Product owner (`sfbreen`) for posture; evidence/retention authority for contract | product `bbe24527f732f9c265f9cf71b988303a326e45fec0c6adb0d934536d515d6017#$.decisions["CD-RT-5"]`; retention v24 `ba29c115a9064ab1cd66ea01751b238acf092b3d699ca43027de7a8dfe55a277` NOT APPLIED; v25 review REJECT 4 | Applied successor that implements the exact decided posture and joins EVIDENCE/D9; no silent demotion; retained checker/review | DECIDED-V1-NOT-INTEGRATED | Blocks retention mechanics and authoritative offline closure blueprint; default itself is not open |
| DR-009 | R-1 identity-dependent laws and instrument standing remain conditional | R-1/evidence authorities | `r1-lifetime-neutrality.conformance.v1.6` `14c46b6582b573c1ac253d891e4813bcc436117adacaa5fc74ede0ab5ae23d3c`; freeze §3 R-1 | Close `LN-13`, `policyOutcome.derivationDigest`, `R1-PARK-*`; reviewed retained validator or explicit accepted alternative | HARD-BLOCKED | One-shot/no-reuse law is preserved; identity-dependent implementation waits |
| DR-010 | V1 product boundaries P-1/P-2/G3 conflict with an independent component ecosystem unless succeeded | Product owner | product packet `bbe24527f732f9c265f9cf71b988303a326e45fec0c6adb0d934536d515d6017#$.decisions.{P-1,P-2,G3-SUBSTRATE}` | Explicit product-owner successor covering catalog/lifecycle depth, contribution ontology, default substrate/profile, trust and enforcement evidence | HARD-BLOCKED | Independent third-party catalog/lifecycle cannot be accepted by architecture alone |
| DR-011 | Every live V1 checker/status residual, cross-cutting open, and stale citation in the matrix must close or receive a lawful explicit disposition | V1 coordinator and each surface owner | blueprint `ccd3d5bef708fadbd5d36489848e84e353f43409a0215b0663d68618b47e65ba` §1.1; freeze `010f9b11a243b4a84357cad435a9e09c0bc44d7d4596fad1b16b68e07c29a27e` §3/§7/§7.8/§7.9 and R2-FINAL-03; exact items DR-011-R01–R16 below | Every residual row below is `CLOSED` by its owning V1 authority or `LAWFULLY-DISPOSED` with scope, rationale, evidence, reviewer, and effect on blueprint claims; no green-checker elevation | HARD-BLOCKED | DR-011 cannot become `SATISFIED` while any enumerated row is OPEN, PARTIAL, stale, rejected, unreviewed, or merely carried in prose |
| DR-012 | Product is not release-qualified | Product/release authority | freeze `010f9b11a243b4a84357cad435a9e09c0bc44d7d4596fad1b16b68e07c29a27e` §6 law 17; staging record reports `NOT-RELEASE-QUALIFIED (0/25 demonstrated)` | Separate QUALIFIED and DEMONSTRATED evidence for the exact release closure | RELEASE-QUALIFICATION-ONLY | Not a prerequisite to authoring a lawfully authorized blueprint; remains mandatory before release or authoritative launch, and no blueprint may claim qualification |

### Exact DR-004 Phase-1A contents

Freeze §3.1 requires an accepted independently reviewed packet containing: proof
for match/no-match/indeterminate-error/verdict; retained verification or
regeneration objects; custody/retention behavior; immutable sealed assurance
versus mutable availability; typed expiry/purge degradation; purge semantics
that do not rewrite a sealed Run; EVIDENCE/TM/OPERABILITY-G19/VERSIONING/claim
reconciliation; and a retained checker/mutation suite. CD-RT-5 supplies the
default posture only; it does not supply this packet.

### Exact DR-006 park coverage

Freeze §7.1 currently names `RunId`, sealed-Run semantic-manifest identity,
`EvidenceDigest`, finding fingerprint, `FactViewId`, cache/regeneration keys,
`executionPlanCommitment`, and `subjectScopeCommitment` computation/verification.
Related named gaps are `policyOutcome.derivationDigest` and
`capabilityManifestId`. The property also covers unlisted identity-affecting
fields; the freeze specifically records `rustcDevLlvmDigest` and
`typescriptStdlibMerkleRoot` as PlanId-affecting digests with no producing rule.
The property—not this enumeration—is the boundary; refresh must search for all
members and cannot close only the listed rows.

### Exact DR-011 residual reconciliation

This is the exhaustive residual subledger for the current matrix snapshot. A
new matrix residual must be assigned a new row before DR-011 is reconsidered.

| Item | Exact residual and source pin | Required closure/disposition | Status |
|---|---|---|---|
| DR-011-R01 | FACT-PLANE `fact-plane.v1.json` `9057200822c5be59bcf8e691e3755cfa1acf2c89f0b1c2bc89237afaa0925b4d`; pinned checker `c7ebcd3ee2c206ae8cdd6dfd1750236e465bdab7e9a104b105fe8e85330e29ac` executes green but still cross-checks D9 v1.6. Live Phase-1A subject-set agreement, sufficiency `view` type, and closed `rungUnavailableBecause` vocabulary remain absent. | Applied V1 closure for all three named semantic items, refreshed D9 join, retained checker/review, or a reviewed scoped disposition that keeps facts/Coverage design blocked. | OPEN |
| DR-011-R02 | FACT-IDENTITY `fact-identity-policy.v2.json` `10055004e6919a55b29c38d9c474857280fbbb6f561dfff6ed88b7e54efbd110`; checker `be7b36d301c4b3710865779d53e8cb43740d54e6273b4dbd1c85cec38f9b3216` executes green while stating 13/14 implementable and capability property `NOT DISCHARGED`; corpus and imperative-authority parks remain. | Close or lawfully preserve every checker-declared limitation with exact corpus/authority evidence. | OPEN |
| DR-011-R03 | C2 effective schema/checker line retains a checker-review/subject-standing mismatch surfaced in the claim matrix and status manifest. | Pin the effective checker and its independent standing or record a V1-owned alternative; do not infer acceptance from execution alone. | OPEN |
| DR-011-R04 | DELIVERY has live OBS-1, checker/fixture skew: reviewed v4 checker standing does not elevate later unreviewed `check-delivery-v5.py`, and release fixtures remain inconsistent with the effective major-1 substrate. | Applied/reviewed successor plus fixture/checker convergence, or scoped product/architecture disposition retaining the limitation. | OPEN |
| DR-011-R05 | Rust provider base v2 remains independently REJECTED with PC-7; merged major-2 v4 is the usable negotiated contract, not a repair that silently rewrites base standing. Later checker surfaces do not by themselves close the base review. | Exact successor/adjudication of PC-7 and checker standing, preserving merged-major-2 demarcation until then. | OPEN |
| DR-011-R06 | EVIDENCE v10 remains PASS-WITH-RESIDUALS/NOT APPLIED and is still blocked by Phase-1A, identity, custody, retention, and D9 joins. | DR-002–008 V1 successor chain with review/checker/status evidence. | OPEN |
| DR-011-R07 | Retention v24 is unapplied; v25 is rejected; retained checker/product-checker constraints and later candidate/checker surfaces cannot override `CD-RT-5` or substitute for an accepted evidence/retention successor. | Accepted successor implementing exact product posture, executable checker/product-checker convergence, and D9/EVIDENCE join. | OPEN |
| DR-011-R08 | D9 v1.14 keeps independent-review advisories `R-V114-F1` and `R-V114-F2` plus the three checker-derived contract gaps; required-output post-commit golden is authoritative for public exit behavior. | Applied D9 successor/adjudication retaining exact v1.14 ordering and goldens, including retention integration. | OPEN |
| DR-011-R09 | R-1 v1.6 is the reviewed base; `check-r1-v1.7.py` is not independently reviewed and v1.6 checker carries CIR-B1. Identity-dependent LN-13/digest/park items remain. | Reviewed retained validator or accepted alternative plus CIR-B1 and identity-park closure. | OPEN |
| DR-011-R10 | `R2-FINAL-03` remains OPEN pending the final blind consumer-B implementer litmus after all surface adjudications and V10 resolution. | Execute, retain, review, and lawfully disposition the final blind litmus. | OPEN |
| DR-011-R11 | OPERABILITY v10 remains implementable with retained limitations including G19; a green checker cannot establish qualification or durable-authoritative storage. | Applied G19/custody successor and exact checker/status reconciliation. | OPEN |
| DR-011-R12 | Evaluation proof has non-interchangeable heads: v8 `4bb33f772c8c510c470643082f6bfb8a4df28a050b4720dda6cdd5187bd3e303` is the unapplied V10 item-1 claim-shape artifact with a wrong-plan-identity checker defect; v13 `1497e8872217e7f2b196888483d2e443d25d554a3023c3bcede9e5722d0c5abe` is PASS-WITH-RESIDUALS, CANDIDATE-NOT-APPLIED provenance lineage and does not supersede v8. The complete v13 open set is routed below: 19 `RES-EP13-01..19` limitations, 7 `IR-EP13-NB-01..07` review observations, and escaping AX6/AX9/MD5/RX2c. Default and 75-mutation selftest executions exit 0 but retain the checker-scope/DO-NOT-SEAL boundary. | V1-owned dual-head reconciliation; **individual** `CLOSED` or `LAWFULLY-DISPOSED` evidence for every routed limitation and observation and the four measured escapes, without erasing v8 obligations or treating exit 0 as closure/application/correctness. | OPEN |
| DR-011-R13 | VERSIONING v8 pins stale D9 v1.6. Pinned `check-versioning-v8.py` execution exits 1 at RC-14. The pinned file named `check-versioning-v14.py` explicitly validates v8 and accounts for—but does not close—RC-14. v14, v15, and v16 independent reviews are CHANGES-REQUIRED; v17 is CANDIDATE-NOT-APPLIED with no pinned independent review. | Reviewed applied successor or explicit V1 disposition covering stale D9, RC-14, name collision, rejected v14–v16, and unreviewed v17. | OPEN |
| DR-011-R14 | RESOLVED-INPUTS exact CFG-6 selector is `resolved-inputs.v2.json#$.configuration.rules[5]`. Its TM-v2-era note is stale: TM v3 restores V11 and records `$.resolves["A1-TM2-01"]`, while TM remains UNSET for V10/custody/G19 rather than a missing CFG-6 threat root. | Reconcile the stale cross-artifact note without reopening the resolved CFG-6 threat root or masking live TM blockers. | OPEN |
| DR-011-R15 | TRUSTED-REQUEST-CONTEXT and freeze §7.1 still depend on RequestId/evidence and other exact identity recipes; review/checker success cannot make absent computation/custody recipes settled. | Applied identity/evidence successor or scoped disposition preserving conceptual-only V2 claims. | OPEN |
| DR-011-R16 | Product-disposition checker/status surfaces constrain P-1/P-2/G3 and `CD-RT-5`; later checkers or candidate amendments are not product authority and cannot silently change those decisions. | Exact product-owner successor/adjudication with independent standing, or explicit preservation of the current product boundary/posture. | OPEN |

#### DR-011-R12 complete EP13 routing

The reproducibility source is
[`v1-status-evidence.json`](v1-status-evidence.json): it pins the candidate,
review, checker, exact selectors, canonical selector digests, default execution,
and selftest execution. The following is one routed residual set, not three ways
to claim closure:

- Candidate limitations `$.knownLimitations[0..18]` are exactly
  `RES-EP13-01..19`. Their scope/effect is: unrepaired inner C-2 and canonical/
  durable-identity defects (01, 06, 07); bounded corpus/generalization limits
  (03, 08, 14); checker self-byte, float-admission, text-only, and anchor/
  meaning limits (05, 10, 17, 19); provenance-not-correctness and dependent
  checker/adjudication limits (09, 11, 15); and guard/escape/sole-guard/window/
  side-channel limits (02, 04, 12, 13, 16, 18). Each object has its own exact
  selector and digest; none is closed by the default green execution.
- Independent review observations `$.nonBlockingObservations[0..6]` are exactly
  `IR-EP13-NB-01..07`: stronger gate-routing severity; punctuation escape in the
  scope self-scan; the false `independentPathIsUnreachable` measurement;
  unenforced stale scope/count prose; contradictory prose around anchors;
  attacker-cost characterization; and environment/reproduction standing. Each
  observation has its own exact selector/digest. `PASS-WITH-RESIDUALS` records
  them; it does not dispose them.
- AX6, AX9, MD5, and RX2c are the exact four members of both
  `$.evasionMeasurement.escapedEveryGuard` and
  `$.evasionMeasurement.declaredBlindSpotVariants`. Their pinned per-variant
  rows show no scored guard catches them and `answerProvenance == false`; the
  tripwire flags AX6/AX9 but not MD5/RX2c. Their effect is the declared scope:
  answer provenance is not established against a route region that can
  distinguish measured from unmeasured calls and answer honestly when observed.

DR-011-R12 cannot become `CLOSED` merely because the pinned default run exits 0
or `--selftest` prints `SELFTEST-PASS` for 75 mutations. Closure requires a V1
owner to record, for every one of the 19 limitations and 7 observations and for
each of the four escapes, either accepted successor evidence or an explicit
lawful disposition naming retained scope, effect, dependencies, and blueprint
constraint. The v8 claim-shape obligation must be reconciled separately.

## V2 architecture and product decisions

| ID | Decision | Owner / decision authority | Source pin / affected sections | Required acceptance evidence | Status | Blueprint impact |
|---|---|---|---|---|---|---|
| DR-101 | Native signed distribution-core language, mandatory closure/TCB inventory, layering, signing/notarization, platforms | Architecture + release engineering | [Distribution](02-distribution-and-components.md) | Reviewed closure inventory and dependency graph; gate harnesses DR-G01–G05 | OPEN | Hard blocker for core implementation blueprint |
| DR-102 | Common control transport/framing/handshake; opaque subprotocol negotiation only | Protocol authority | [Protocol demarcation](02-distribution-and-components.md) | Contract proving no TS/Rust frame translation plus hostile conformance | OPEN | Hard blocker for component protocol blueprint |
| DR-103 | Canonical component manifest/index/lock schemas, delegated roles, IDs, provenance/SBOM/attestation binding | Delivery + security | [Distribution](02-distribution-and-components.md), [Security](03-configuration-and-security.md) | Reviewed canonical schemas, duplicate/path rejection, signatures, exact-byte test corpus | OPEN | Hard blocker |
| DR-104 | Stable component identity, alias/rename/ownership governance, command namespace/collision policy | Product/CLI architecture | [Distribution](02-distribution-and-components.md) | Product-approved namespace and migration rules with negative tests | OPEN | Hard blocker |
| DR-105 | Platform permission truth tables, deterministic grant-revocation linearization, and enforced-confinement versus trusted-code consent | Security + platform owners | [Security](03-configuration-and-security.md#proposed-permissions-with-honest-outcomes) | Per-platform requested/granted/denied/enforced/disclosed matrix; durable monotonic ordering of request acceptance, reversible/irreversible effect-commit, revocation, cleanup, and audit; race tests for already accepted/in-flight requests and irreversible effects; enforcement evidence | OPEN | Hard blocker for any permissioned broker/effect surface; third-party execution remains excluded separately |
| DR-106 | Signed offline analysis closure contents and mandatory verified storage mechanics/minimal backend | Product + evidence + release | [Distribution](02-distribution-and-components.md), [Operations](04-lifecycle-delivery-and-operations.md) | Applied DR-002–008; clean-machine no-network tests; durable retention and typed storage-failure results | OPEN / inherits hard blockers | Hard blocker for authoritative analysis profile |
| DR-107 | Project/operation lock and multi-version generation semantics | Lifecycle + versioning | [Operations](04-lifecycle-delivery-and-operations.md) | DR-G18 crash-point harness; concurrent conflicting locks; immutable installs; leases/refcounts; reference-safe GC/removal; atomic dependency/state closure and migration | PROPOSED-CLOSED-FOR-REVIEW | Still hard blocker until reviewed successor and DR-G18 harness acceptance |
| DR-108 | Secret credential storage via keychain and secure-file fallback | Security + platform owners | [Configuration](03-configuration-and-security.md) | Platform threat model, permissions, migration/recovery, redaction tests | OPEN | Hard blocker only for features requiring stored credentials; not a V1 secret law |
| DR-109 | Host-owned storage-mechanics interface | Evidence + storage architecture | [Operations](04-lifecycle-delivery-and-operations.md) | Applied evidence successor; one-writer commit, custody, recovery, inventory, doctor and failure tests | OPEN / inherits hard blockers | Hard blocker for authoritative closure |
| DR-110 | Core self-update/repair/rollback and repair-media trust | Release + platform owners | [Operations](04-lifecycle-delivery-and-operations.md) | Signed clean-machine repair, crash injection, revocation-aware rollback, removable-media/expiry tests | OPEN | Hard blocker |
| DR-111 | Separate compatibility windows for core/index/control, each provider major, component API, state schema, and evidence formats | Versioning authority | [Operations](04-lifecycle-delivery-and-operations.md) | Per-surface matrices and cross-version conformance; no shared same-version assumption | OPEN | Hard blocker |
| DR-112 | Signed-index refresh, expiry, last-known revocation, quorum loss, root recovery, emergency running-component policy | Security + operations | [Security](03-configuration-and-security.md) | Reviewed state machine, air-gap/removable-media fixtures, recovery ceremony, audit/waiver expiry | OPEN | Hard blocker |
| DR-113 | Replay/verification/inspection/purge/degradation behavior and retained executable/reference window | Evidence + product | [Operations](04-lifecycle-delivery-and-operations.md) | DR-002–008 successors; exact typed results/exits; pin/GC/removal tests | OPEN / inherits hard blockers | Hard blocker |
| DR-114 | Doctor stable machine schema, exit semantics, redaction, and consented probes/egress | Operability + security | [Operations](04-lifecycle-delivery-and-operations.md) | Read-only/no-code/no-network default tests, stable schema, D9 mapping, redaction corpus | OPEN | Hard blocker |
| DR-115 | Numeric size/startup/memory thresholds and regression tolerances | Product + release engineering | release gates below | Reproducible measurements and product-owned threshold decision | OPEN | Hard blocker for falsifiable “small”; not yet QUALIFIED |
| DR-116 | Third-party publisher/support/vulnerability/revocation policy | Product security | [Security](03-configuration-and-security.md) | Product disposition, support tiers, incident/revocation exercises, honest labels | OPEN | Hard blocker for third-party ecosystem |
| DR-117 | Product-boundary successor for marketplace/catalog depth, imperative contributions, untrusted native/WASM, probes, and network grants | Product owner | DR-010; [Product boundary](02-distribution-and-components.md) | Explicit successor to P-1/P-2/G3 with enforcement evidence | OPEN | Hard blocker; V1 exclusions remain until closed |
| DR-118 | Language-native analysis quality and supported language/tooling roles | Product + language architecture owners | [Language-native quality](02-distribution-and-components.md#language-native-product-quality) | Product-selected role list; per-role capability/parity matrix; language-specific semantic/graph goldens; behavior/performance baseline; known limitations; explicit no-silent-fallback tests | OPEN | Hard blocker for every language/tooling role included in the first blueprint; does not mandate implementation language |
| DR-119 | Self-contained language runtime/tool closure product rule | Product owner + each language component owner + release/security/platform owners | effective DELIVERY TypeScript major-1 substrate as prototype rationale; [Language runtime/tool UX](02-distribution-and-components.md#language-runtime-and-toolchain-ux) | For every supported language role: signed platform-qualified closure of runtime/parser/compiler/language-server or analogous non-system dependencies; manifest licenses/SBOM/attestation/platform/capability/performance declarations; clean-machine offline tests; ambient/implicit-download refusal; typed remediation. Any unbundleable customer-owned external-system exception needs explicit product approval and doctor contract | PROPOSED PRODUCT RULE — OPEN ACCEPTANCE | Hard blocker for every supported language role; TypeScript specifically must not require user-managed Node |
| DR-120 | Common component packaging contract and per-language build-adapter template | Component architecture + release/developer-experience + language owners | [Common packaging model](02-distribution-and-components.md#common-component-packaging-and-language-build-adapters); DR-103/118/119 | Reviewed canonical output contract; adapter interface/template; deterministic/hermetic CI expectations; local developer validation flow; fixtures proving full-tree/provenance/SBOM/licenses/platform/compatibility/health/offline/update/rollback/gate compliance across representative language closures | OPEN | Hard blocker before language component implementation blueprints; concrete packagers/toolchains remain deferred |
| DR-121 | Monorepo isolated component CI and independent release qualification | Release engineering + component owners + core/protocol/integration owners | [Monorepo CI model](02-distribution-and-components.md#monorepo-ci-and-independent-component-releases); DR-103/111/118/120 | Ownership/dependency selection model; per-component relevant-platform lane contract for build/test/package/sign/attest/SBOM/quality; shared-core lane; cross-component protocol/authority/lock/offline/bundle gates; change-impact and missed-dependency negative tests; independent release evidence | OPEN | Hard blocker for release architecture; does not require separate repositories or lockstep versions |
| DR-122 | Preserve SARIF 2.1.0 as an optional host-owned projection for applicable findings/results | Output/operability owner + CLI/product owner | V1 `operability.v10.json` `9bacbbf43dfb941a0d87330f79844d395b3ac838ae5bf54026ef4d69681696be` `$.projectionParity` / `$.projectionFixtures`; [V2 output projections](01-semantic-model-and-host-authority.md#output-projections-including-sarif) | Explicit per-command/capability applicability; stable machine/schema/version contract; parity/loss goldens preserving canonical Run/Finding IDs, Coverage, verdict, truncation, and artifact references; negative tests proving a renderer cannot affect policy/evidence/sealed termination or choose D9/exit, plus exact host-owned required-output failure golden | PROPOSED-CLOSED-FOR-REVIEW | Hard blocker for any first-slice command or reporting component that advertises SARIF; does not require every command to emit SARIF |
| DR-123 | Standard command-oriented CLI with stable human and machine output is mandatory baseline UX | Product/CLI + output/operability owners | [Output projections](01-semantic-model-and-host-authority.md#output-projections-including-sarif); DR-114/122; DR-G01–G05/G12/G17 | Every first-slice core command works in non-interactive CI without a TUI; stable human/machine schema, exit, redaction, output-failure, offline, and footprint evidence | OPEN ACCEPTANCE | Hard blocker for **every** first blueprint slice; it is not conditional on TUI scope |
| DR-124 | Closed state-class/owner/writer architecture | Semantic/evidence/storage/lifecycle owners | [State classes](04-lifecycle-delivery-and-operations.md#state-classes-and-authority) | Matrix for authoritative evidence, analysis-affecting durable state, rebuildable cache/index, operational metadata; Plan/Run, custody/backup/purge/migration rules and cross-class negative tests | OPEN | Hard blocker for stateful component blueprint |
| DR-125 | Common component SDK/control contract owns cross-cutting product behavior | Component architecture + CLI/operability/security owners | [Developer contract](02-distribution-and-components.md#common-component-developer-and-operability-contract) | Structured envelopes/logs/progress/config/provenance/brokers/cancellation/doctor/exit integration; common look-and-feel goldens; no direct rendering/unstructured host logs/authority escape | OPEN | Hard blocker for analyzer/tool SDK blueprint; exact APIs/frameworks deferred |
| DR-126 | Platform base/host-ABI TCB and loader closure | Security + release + platform owners | [Exact-byte delivery](04-lifecycle-delivery-and-operations.md#exact-byte-delivery) | Closed OS ABI/loader/libc/framework/cert/font/ICU-class allowlist and identity rules; retained loader traces; undeclared-system-resolution negative tests | OPEN | Hard blocker for platform qualification |
| DR-127 | Anti-lockstep compatibility and host-owned control/data race precedence | Protocol + versioning + release owners | [Control demarcation](02-distribution-and-components.md#exact-controldata-plane-demarcation); [compatibility](04-lifecycle-delivery-and-operations.md#separate-compatibility-matrices) | Bidirectional N/N+1 skew, independent rollback/coexistence, no bundle promotion gate; hostile dual-channel race/fault/EOF/duplicate/teardown goldens with byte-opaque provider frames | OPEN | Hard blocker for independent-release blueprint |
| DR-128 | Future third-party sandbox/product boundary | Product security + product owner + platform owners | DR-010/117; [Confinement honesty](03-configuration-and-security.md#preserved-confinement-honesty) | Explicit post-MVP successor/approval; demonstrated OS/WASM enforcement, permission/platform matrix, escape tests, revocation and incident ownership | DEFERRED POST-MVP | Not an MVP blueprint blocker. MVP permits first-party/explicitly trusted components with DR-G21 fault containment only; public marketplace/untrusted native/WASM/imperative/network-granted roles stay excluded |
| DR-129 | Optional interactive TUI is only a host-owned projection | Product/CLI + output/operability owners | [Output projections](01-semantic-model-and-host-authority.md#output-projections-including-sarif); DR-123; DR-G01–G05/G12/G17 | If a slice includes TUI: parity/non-authority, non-packaging, offline, footprint, cancellation, and fallback-to-CLI evidence; concrete framework remains implementation design | DEFERRED / OPEN IF SELECTED | Blocks only a slice that elects to include a TUI; never blocks or replaces the mandatory CLI baseline |

## Five-review findings and dispositions

| ID | Review | Finding accepted | Owner | Source/evidence required | Status | Blueprint impact |
|---|---|---|---|---|---|---|
| DR-201 | Semantic correctness | Happy-path/pre-admission branches, Run-versus-command finalization, post-commit output failure, and parked recipes were blurred | V2 architecture editor; semantic/D9 authority reviews successor | [Review record](07-review-record.md); corrected [semantic lifecycle](01-semantic-model-and-host-authority.md); D9 v1.14 output golden in matrix | PROPOSED-CLOSED-FOR-REVIEW | Must be re-reviewed; inherited DR-002/006/007 remain hard |
| DR-202 | Delivery/operations | Generation coexistence, mandatory storage, recovery, repair, permissions, state classes, loader TCB, and gate evidence were underspecified | Lifecycle/evidence/release owners | Corrected [operations](04-lifecycle-delivery-and-operations.md); DR-106–115/124/126/127; DR-G18/G19/G22 | PROPOSED-CLOSED-FOR-REVIEW | Architecture prose corrected; decisions remain blocking |
| DR-203 | Prototype lessons | Prototype strengths lacked a clean source pin and enforceable no-lockstep/single-lifecycle/failure-containment path; no digest-pinned language-quality corpus or accepted measurement baseline is yet recorded | Component/protocol + product/language owners | [Prototype reference](prototype-evidence-reference.md); [V1 relationship](05-v1-to-v2-relationship.md); DR-102/107/118/125/127; DR-G10/G13/G18/G20/G21 | PARTIAL — SOURCE PINNED; QUALITY EVIDENCE OPEN | Re-review required; language-quality claims remain blocked by DR-118/DR-G13 |
| DR-204 | V1/coop invariant coverage | Newest-head heuristics and baseline-only standing could promote candidates or hide blockers/divergences | V1 status coordinator + V2 editor | Authority and status-evidence manifests, claim matrix, this register; exact selector/digest validation | PROPOSED-CLOSED-FOR-REVIEW | DR-001/011 remain hard until independently refreshed |
| DR-205 | Small-core/components | Core/TCB/product boundaries, storage, compatibility, quality, packaging, component SDK/UX, fault containment, and MVP/future scope were incomplete | Architecture/product/release/language owners | Corrected distribution/operations/scope docs; DR-101/106/111/115/117–128 | PROPOSED-CLOSED-FOR-REVIEW | Re-review and product dispositions required; DR-128 is post-MVP only |

## Release gate registry

These are architecture gate requirements, not qualification claims. All rows are
currently below `QUALIFIED` and `DEMONSTRATED`; numeric pass/fail thresholds are
open under DR-115. Waivers require product and release authority, an expiry, a
measured residual, and cannot waive an inherited semantic/trust blocker.

| Gate ID | Claim | Platform matrix / harness | Required retained evidence | Owner | Assurance stage now | Threshold / waiver | Status |
|---|---|---|---|---|---|---|---|
| DR-G01 CORE-DOWNLOAD | Distribution core is small | every supported release platform; exact signed compressed closure | artifact list, bytes, signatures, SBOM, raw measurement | Release engineering | SPECIFIED, not QUALIFIED | numeric open; expiring waiver only | OPEN |
| DR-G02 CORE-INSTALLED | Minimal mandatory closure/TCB is bounded | clean install per platform | immutable tree inventory, dependency/TCB classification, size | Architecture + release | SPECIFIED | numeric open | OPEN |
| DR-G03 CORE-STARTUP | `--help`/`--version` remain fast and load no components/project | cold-cache harness, p50/p95/p99, fixed runner image | raw samples, cache state, process/module trace | Release engineering | SPECIFIED | numeric/regression open | OPEN |
| DR-G04 CORE-MEMORY | Baseline/peak RSS is bounded | same runners and lifecycle commands | raw RSS traces and methodology | Release engineering | SPECIFIED | numeric/regression open | OPEN |
| DR-G05 COMPONENT-DELTA | Each component cost is independently visible | platform × component matrix | download/install/start/RSS delta | Component publisher + release | SPECIFIED | numeric open | OPEN |
| DR-G06 OFFLINE-CLOSURE | Supported authoritative product installs/runs with no network and mandatory storage | clean machines, DNS/egress blocked, air-gap/removable media, each supported platform | signed root/index/revocation/payload closure; analysis/evidence/doctor results | Product + release + evidence | BLOCKED by DR-002–008 | no waiver of durable authority | HARD-BLOCKED |
| DR-G07 EXACT-BYTES | Verified bytes equal executed bytes | hostile archive/path/loader/TOCTOU corpus on supported filesystems | extraction, canonicalization, descriptor/identity and race results | Security + platform | SPECIFIED | pass all; waiver requires platform removal | OPEN |
| DR-G08 TRUST-RECOVERY | Root/index/core/component/repair trust survives expiry, revocation, quorum loss, rollback | online/offline/air-gap/removable-media state-machine harness | signed metadata history, recovery and refusal audit | Security + release | SPECIFIED | pass all safety cases | OPEN |
| DR-G09 PERMISSIONS | Requested/granted/denied and enforced/disclosed outcomes are truthful | per-platform truth table plus component-generation/process-descendant/Run/operation grant harness; races at request acceptance, reversible commit, irreversible effect-commit, revocation, and process death | consent and CI records; durable monotonic linearization trace; successive-call expiry/revocation; cancellation/cleanup closure; completed-before-revocation disclosure; proof that no effect commits after revocation | Security | SPECIFIED | required confinement has no trusted-code waiver; trusted-code use needs explicit consent; wall-clock/component ordering is forbidden | OPEN |
| DR-G10 PROVIDER-CONFORMANCE | TS major 1 and Rust merged major 2 remain opaque, one-shot, fate-compatible subprotocols | exact V1 goldens, D9/fault joins, no-reuse/process cleanup | byte/fate parity and lifetime results | Protocol + semantic owners | V1 IMPLEMENTABLE; V2 not QUALIFIED | any semantic change needs successor | HARD-BLOCKED pending selector refresh |
| DR-G11 STORAGE-CUSTODY | Authoritative closure cannot succeed without verified durable storage | missing/failing/partial commit/recovery/retention corpus | one-writer commit, inventory, custody, recovery, typed non-success | Evidence + storage | BLOCKED by DR-002–008 | no waiver | HARD-BLOCKED |
| DR-G12 DOCTOR-PURGE | Doctor and purge are safe, stable, and honest | core/project modes; crash/backup/external-store cases | schema/exit/redaction/probe consent; preview/audit/idempotence | Operability + security | SPECIFIED | pass/fail open with no honesty waiver | OPEN |
| DR-G13 LANGUAGE-QUALITY | Each supported language/tooling role delivers language-native quality rather than a lowest-common-denominator abstraction | future product-selected role × platform × digest-pinned corpus matrix; no such accepted corpus/measurement manifest exists in this V2 snapshot | capability/parity matrix, exact corpus/golden digests, quality/performance measurements, limitations, and fallback-refusal cases | Product + language owners | OPEN FUTURE ACCEPTANCE EVIDENCE; not QUALIFIED | threshold/parity decision per role; semantic degradation has no silent waiver | OPEN |
| DR-G14 LANGUAGE-RUNTIME-UX | Supported language analyzers are self-contained; users manage no non-system runtime/tool dependencies | language-role × clean supported-platform matrix; offline signed closure; hostile PATH/loader/system-tool substitutions | signed component/runtime/tool tree, manifest licenses/SBOM/attestation/platform/parity declarations, identity/loader trace, quality corpus, typed remediation and approved-exception diagnostics | Product + language + release + security | TypeScript V1 shape IMPLEMENTABLE; V2 rule not QUALIFIED | all supported roles/platforms; exception only by explicit product approval and never labeled self-contained | OPEN |
| DR-G15 PACKAGING-ADAPTER-CONFORMANCE | Different language build adapters emit the same verifiable OpenSIP component contract | adapter × supported platform × clean/offline/upgrade matrix | canonical manifest/tree commitment, provenance/SBOM/license inventory, compatibility/health results, air-gap install, update/rollback, budget measurements, developer/CI reproduction evidence | Component architecture + language publisher + release/DevEx | PROPOSED; not QUALIFIED | all selected adapters; no waiver for missing signed closure fields | OPEN |
| DR-G16 CI-ISOLATION-INTEGRATION | Monorepo changes run all and only required component/core/integration qualification lanes from declared ownership/dependencies | change-impact corpus × component/language/platform matrix; forced dependency/ownership mutations; aggregate release selection | selected-lane explanation, per-lane signed closure evidence, skipped-lane proof, shared-core and cross-component protocol/semantic/lock/offline/bundle results | Release engineering + owners | PROPOSED; not QUALIFIED | no waiver for an affected omitted lane; platform scope follows component manifest | OPEN |
| DR-G17 SARIF-PROJECTION-PARITY | Every advertised SARIF 2.1.0 projection is a stable, lossless host view of the same applicable result | advertised command/capability × canonical Run corpus × supported platform; V1 parity fixtures plus drop/change/truncation mutations | serialized typed/native and namespaced fields for Run/Finding IDs, Coverage, verdict, truncation, artifact references; schema/version/refusal behavior; human/JSON comparison; no renderer authority; exact required-output serialization-failure/exit-4 behavior | Output/operability + CLI/product owners | V1 contract preserved; V2 not QUALIFIED | all advertised SARIF surfaces; omission is allowed only by not advertising applicability, never by silent semantic loss | OPEN |
| DR-G18 LIFECYCLE-GENERATION-RECOVERY | Activation, migration, rollback, locks, leases, and removal are journaled and crash-safe | crash at every journal write/fsync/rename/pointer and migration prepare/commit/abort/no-return transition; conflicting project locks; process death | old-or-new atomicity, fail-closed recovery, dependency/state/permission closure, leases/refcounts, reference-safe retained-evidence/rollback removal | Lifecycle + storage + versioning | PROPOSED; not QUALIFIED | every reachable durable transition; no waiver for ambiguous authoritative state | OPEN |
| DR-G19 STATE-CLASS-AUTHORITY | Every durable/rebuildable state byte has one declared class, owner, writer, and lifecycle | state-class × migration/backup/purge/recovery matrix; cross-class mutations | Plan/Run consequence, custody, retention, backup, purge, migration and corruption results; rejected component evidence writes/cache promotion/hidden inputs | Semantic + evidence + storage | PROPOSED; not QUALIFIED | all stateful first-slice roles | OPEN |
| DR-G20 COMPONENT-OPERABILITY | Components use common host behavior rather than reimplementing product UX/operations | component-role × human/JSON/SARIF/doctor/fault/config/progress/log corpus | structured envelope and diagnostic parity; redaction/bounds/audit correlation; broker/cancellation/resource behavior; no direct UI/unstructured logs/final authority | Component architecture + CLI/operability | PROPOSED; not QUALIFIED | all external roles; SDK implementation may vary behind contract | OPEN |
| DR-G21 COMPONENT-FAILURE-CONTAINMENT | One component failure never crashes the core or leaks uncommitted authority | crash/panic/timeout/resource/malformed/truncated/duplicate/EOF/process-tree/recovery corpus | core survival, kill/reap/cleanup, candidate discard, sealed-evidence preservation, bounded redacted diagnostics/audit, Coverage/D9/UI/exit goldens | Supervisor + protocol + operability | PROPOSED; not QUALIFIED | all external components; does not claim security confinement | OPEN |
| DR-G22 PLATFORM-ABI-LOADER | Executed closure uses only declared platform TCB dependencies | supported OS/filesystem/architecture × hostile loader/system library/tool environment | full loader trace, identity/version allowlist, negative undeclared libc/framework/cert/font/ICU/tool resolution and alternate-loader search | Security + release + platform | PROPOSED; not QUALIFIED | pass all declared platforms or remove platform support | OPEN |

## Blueprint-readiness decision

V2 is **not blueprint-ready**. Readiness requires all of the following in this
register, and this paragraph is the only active readiness checklist:

1. DR-001 through DR-011 are `SATISFIED` or the owning V1 authority records an
   explicit, scoped, reviewed pre-blueprint disposition that names what may be
   designed without pretending the blocked semantics are settled. DR-012 is not
   a blueprint-entry prerequisite; it remains mandatory before release or
   authoritative launch.
2. DR-101 through DR-127 that affect the first blueprint slice are `SATISFIED`;
   deferred items have explicit product/architecture scope dispositions.
3. Each DR-201 through DR-205 re-review is `ACCEPTED`; alternatively, every
   rejecting finding is individually identified, closed or lawfully routed to
   an owning authority/register item, and backed by retained evidence. Merely
   receiving a rejecting disposition never satisfies this gate.
4. Required release gates have named harnesses and owners; no document claims
   `QUALIFIED` or `DEMONSTRATED` without retained evidence.
5. Product and architecture authorities explicitly authorize creation of
   `docs/v2/implementation/` against a refreshed exact authority baseline.

Until then, `docs/v2/implementation/` remains reserved and absent.
