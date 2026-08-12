# OpenSIP Distribution and Component Transition Brief

**Status:** PROPOSED — non-binding transition brief

**Authority:** NONE. This document does not amend, supersede, apply, seal, or
freeze an existing architecture decision or binding artifact.

**Scope:** Physical distribution, component ownership, lifecycle, protocol,
delivery, and operational qualification for the next OpenSIP implementation.

## How to read this brief

The current architecture remains authoritative. In particular, the binding
contracts and status records under [`coop/`](coop/) win over this proposal if
they disagree. The words *must*, *should*, and *may* in proposed sections below
describe acceptance criteria for a future reviewed successor; they do not
silently change the current status lattice.

This brief records one focused transition:

> Preserve OpenSIP's semantic and trust architecture. Change the physical
> distribution from a full analysis platform shipped as one default closure to
> a small signed native OpenSIP core plus optional, independently released
> components governed by one lifecycle.

The transition should be adopted, if at all, through explicit successor
artifacts and the ordinary independent-review and application process.

Narrative architecture files explain intent but are not status authority. A
successor must resolve the exact applied heads and their predecessor chains from
the pin table in [`IMPLEMENTER-BLUEPRINT.md` §1.1](coop/IMPLEMENTER-BLUEPRINT.md)
and the disposition table in [`IMPLEMENTATION-FREEZE.md`
§3](coop/IMPLEMENTATION-FREEZE.md), then reconcile the
[`claim-register.v1.json`](coop/artifacts/claim-register.v1.json) binding. At the
time of this proposal, the exact heads needed by this transition are:

| Surface | Exact head and status source |
|---|---|
| Plan/stages | [`c2-plan-stage-schema.v11.json`](coop/artifacts/c2-plan-stage-schema.v11.json), SHA-256 `d35b677d6726a8f9b9fc70e2e0f3307af909eca876cd6670d238829ba95a81f8`, applied 2026-08-05 as the v11 → v10 → v9 → v4 derivation recorded in the blueprint pin table |
| Facts | [`fact-plane.v1.json`](coop/artifacts/fact-plane.v1.json), SHA-256 `9057200822c5be59bcf8e691e3755cfa1acf2c89f0b1c2bc89237afaa0925b4d`, and [`fact-identity-policy.v2.json`](coop/artifacts/fact-identity-policy.v2.json), SHA-256 `10055004e6919a55b29c38d9c474857280fbbb6f561dfff6ed88b7e54efbd110`, with their recorded `SEAL-WITH-CHANGES` dispositions |
| Resolved inputs | [`resolved-inputs.v2.json`](coop/artifacts/resolved-inputs.v2.json), SHA-256 `0114205aaa5d3f7c0aecc58c10522711aacaa6aa404a41563245627b27b88f43`, with its recorded `SEAL-WITH-CHANGES` disposition |
| Host termination | [`d9-exit-contract.v1.14.json`](coop/artifacts/d9-exit-contract.v1.14.json), SHA-256 `8dd3303855f49bfdbb2751ee65f54a906405f0654159ebe815472f73cdf7da31`, independently passed with the residuals recorded by the freeze |
| Delivery | [`delivery.v4.json`](coop/artifacts/delivery.v4.json), SHA-256 `3cffece076289a4e62f3e0680cb8cc7c6a134b3190a6b39b7ec14b007704a121`, applied 2026-08-05 as the verified `delivery.v2` plus 21-operation derivation |
| One-shot lifetime | [`r1-lifetime-neutrality.conformance.v1.6.json`](coop/artifacts/r1-lifetime-neutrality.conformance.v1.6.json), SHA-256 `14c46b6582b573c1ac253d891e4813bcc436117adacaa5fc74ede0ab5ae23d3c`, applied 2026-08-05 |
| Operability | [`operability.v10.json`](coop/artifacts/operability.v10.json), SHA-256 `9bacbbf43dfb941a0d87330f79844d395b3ac838ae5bf54026ef4d69681696be`, independently passed at its recorded candidate standing |
| Versioning | [`versioning-policy.v8.json`](coop/artifacts/versioning-policy.v8.json), SHA-256 `ea4b52b5a4d187ec35ad994d8ffcd888db287566c8fb53f3df17e5203d84ae2e`, remains the passed head in the blueprint pin table; later files do not silently replace it |
| Rust provider data plane | Resolve the merged contract from [`rust-provider-protocol.v4.json`](coop/artifacts/rust-provider-protocol.v4.json), SHA-256 `3e34934720a78f823d3d4c7ceb73735d444f09a4a1ec964a894bd1ac5daf2909`, its v2 base and exact v4 delivery/resolved-input joins as instructed by the blueprint/freeze; never implement the rejected v2 base alone |
| Threat model | [`threat-model.v3.json`](coop/artifacts/threat-model.v3.json), SHA-256 `56734a4047b61e1fc702f75ccb21e8721b334adb449093d266756d0b08adc499`, plus the applied [`threat-model-storage-namespace.v4.json`](coop/artifacts/threat-model-storage-namespace.v4.json) derivation for `$.storageNamespace`; TM remains `UNSET — BLOCKS FREEZE` outside that applied subtree |
| Product posture | [`product-dispositions.v1.json`](coop/artifacts/product-dispositions.v1.json), SHA-256 `bbe24527f732f9c265f9cf71b988303a326e45fec0c6adb0d934536d515d6017`, is the binding product packet; its decided retention posture does not make an unapplied retention candidate authoritative |
| Evidence/retention | [`evidence.v10.json`](coop/artifacts/evidence.v10.json), SHA-256 `62a3a07194062c8499f6e943b4986d7a77bdecc0c4ec499851ac078fd548e9b4`, is passed but `DO-NOT-SEAL` / not applied; [`retention-tiers.v24.json`](coop/artifacts/retention-tiers.v24.json), SHA-256 `ba29c115a9064ab1cd66ea01751b238acf092b3d699ca43027de7a8dfe55a277`, is passed but not applied. A successor must preserve their accepted shapes without falsely promoting their standing |

Hashes and statuses above are navigation aids pinned to the current status
sources, not a new authority table. If the blueprint/freeze pin table advances,
the successor must use the advanced exact heads rather than treating this brief
as definitive.

## 1. Binding existing principles to preserve

The transition is not permission to redesign the product model. A successor
must preserve these existing principles.

### 1.1 Semantic identity and authority

- Preserve the existing fact schemas, Coverage semantics, fact provenance, and
  predicate-relative sufficiency rules.
- Preserve the existing `PlanId` derivation policy. Only selected,
  analysis-affecting inputs enter semantic identity; available but unselected
  components, update metadata, presentation preferences, and telemetry settings
  do not.
- Preserve one `Run` identity and the existing Run/evidence contracts. Do not
  import a second Session ontology from the earlier prototype.
- Preserve the existing D9 host outcome and numeric-exit derivation. Components
  return typed results and faults; they do not invent public exits, verdicts, or
  evidence authority.
- Preserve a single authoritative Run/evidence commit path. Componentization
  must not create peer writers or let analyzers, graph engines, reports, or
  telemetry mint authoritative state.

OpenSIP core retains non-delegable semantic authority. Components may calculate
bounded candidate material or execute storage mechanics, but no installed
component, bundle, lockfile, profile, or user selection can transfer the
following decisions out of the core:

| Responsibility | OpenSIP core MUST | Component MAY | Component MUST NOT |
|---|---|---|---|
| Snapshot | Resolve scope; capture and seal immutable snapshot bytes/read set; derive and verify `SnapshotId` | Consume only the host-sealed snapshot/VFS subset named in the operation | Read the live worktree as semantic input; mint/replace `SnapshotId`; expand scope |
| Plan | Resolve configuration/contributions/grants; construct the Plan; recompute and verify `PlanId` | Declare typed requirements and return capability negotiation data | Supply authoritative Plan fields, classify config, mint/replace `PlanId`, or change selected inputs after admission |
| Facts | Validate candidate relation/payload/anchor/provenance; construct admitted records; compute and verify `FACT-ID` | Produce bounded fact candidates against the sealed request | Mint authoritative fact IDs, write admitted facts, or bypass host validation |
| Coverage | Define requested domains; validate response keys/completeness; aggregate exact Coverage | Report typed candidate Coverage for the assigned domain | Widen/narrow the requested domain, convert unknown to covered, or choose adequacy |
| Policy/verdict | Evaluate project-owned policy, waivers, baselines, required Coverage, and derive the verdict | Return findings, scores, proof candidates, or pure evaluation intermediates | Set thresholds, waivers, verdicts, gate outcomes, or final policy state |
| Termination | Derive D9 `HostTermination`, public errors, and the sole numeric process exit | Return typed operation result/fault/cancellation detail | Choose a public exit, relabel a host/user fault, or terminate as authoritative success |
| Run/evidence | Build and verify `RunManifest`, compute `EvidenceDigest`, authorize seal, and bind the selected execution closure | Return candidate artifacts and commitments for host verification | Mint `RunId`, seal a Run, compute an authoritative digest, or claim evidence adequacy |
| Durable commit | Authorize exactly one atomic evidence commit under the host-owned protocol and verify the committed result | A storage component may perform transactional bytes/ledger/CAS mechanics | Be selected as evidence authority, independently commit/seal a Run, accept another writer, or reinterpret historical authority |

The MUST/MUST-NOT boundary is closed for this transition. A successor may split
code into libraries or processes, but it cannot reassign these authorities
without reopening the semantic architecture rather than implementing this brief.

### 1.2 Local-first and offline operation

- Local analysis remains fully useful offline. Network access is default-deny
  and no verdict depends on Cloud availability.
- Before initialization, OpenSIP resolves the same strict project intent in
  memory and writes no files to the repository.
- Later adoption into tracked project state is explicit and transactional. It
  preserves existing project, snapshot, plan, Run, and evidence references and
  does not silently move, duplicate, rewrite, or discard user-scoped evidence.
- Missing optional capability returns a typed unavailable or delivery-required
  result with remediation. It never triggers an implicit component download.

### 1.3 Strict configuration and provenance

Preserve the existing six-layer configuration order exactly:

1. compiled defaults;
2. user-global settings;
3. tracked project intent;
4. untracked local override;
5. allowlisted environment; and
6. command flags.

CI and other non-interactive profiles do not load layer 4. Local-interactive use
may resolve layer 4, but every analysis-affecting winning value and its deciding
layer enter the existing provenance path. Unknown tracked keys fail closed.
Every effective analysis-affecting field remains explainable by source without
disclosing a secret value.

### 1.4 Secrets and trust material

- Secret values are represented by handles. Values never enter `PlanId`,
  evidence digests, diagnostics, component lockfiles, support bundles, or
  ordinary logs.
- Secrets and private credentials belong in an OS keychain where available,
  with a verified-permission user-scoped file fallback.
- Public update trust metadata belongs in a user-scoped signed trust store. The
  initial root digest remains pinned in the core or installer; rotation,
  revocation, expiry, threshold verification, and anti-rollback remain explicit.
- The transition does not add mandatory login, online identity, billing, or
  entitlement behavior. The core may broker secret handles and optional
  authenticated update/component channels.

### 1.5 Signed delivery and confinement honesty

- Independent release indexes extend rather than replace the existing canonical
  signed metadata, pinned-root bootstrap, threshold roles, root rotation,
  revocation, expiry, exact digest/size closure, offline verification bundle,
  staged activation, and anti-rollback model.
- A child process is fault containment, not a security sandbox.
- An OS or WASM sandbox may be claimed only when demonstrated enforcement
  prevents alternate ambient access and matches the effective grants.
- Otherwise the component is explicitly trusted code and part of the trusted
  computing base. Broker use by an unconstrained same-user process is an API
  convention, not confinement.

Trusted-code status is not a determinism exception. Every analysis component,
including first-party trusted code, consumes host-sealed inputs and a closed
read set. Ambient `PATH`, loader search, system runtimes, live-worktree reads,
environment, clock, entropy, network state, or install-time substitution are
forbidden unless the existing resolved-input rules classify and enforce them as
neutralized, keyed, or forbidden. The core reviews each component configuration
schema's analysis-affecting classification and maps admitted semantic values to
the existing Plan fields; a component cannot declare its own input outside that
mapping.

### 1.6 Semantic inputs and operational provenance

| Class | Examples | Identity treatment |
|---|---|---|
| **Semantic input** | Selected component manifest/artifact digest; provider/toolchain/subprotocol identity; analysis-affecting config; sealed Snapshot/read set; requested relations; budgets; effective Run grants | Host maps the value into the existing Snapshot/Plan/fact/Run contract. It enters `PlanId` only where the applied contract says it does. |
| **Operational provenance** | Available-but-unselected catalog rows; UI-only core build; index refresh time; update channel metadata not selected by the lock; telemetry exporter/config; download mirror; diagnostic correlation | May be audited or reported, but never changes `PlanId`, Coverage, verdict, `EvidenceDigest`, or Run identity. |

The full available catalog is never a semantic input. This transition introduces
no Session identity and no parallel plan recipe.

## 2. Proposed distribution boundary

### 2.1 Terminology

This proposal uses three distinct terms:

| Term | Meaning |
|---|---|
| **OpenSIP core** | The small signed native executable and its minimal distribution closure. |
| **Evaluation core** | The existing pure evaluation function and semantic contracts. Pure calculation may be hosted in a component or library, but final Snapshot/Plan/fact/Coverage/policy/Run/evidence authority remains non-delegably in the OpenSIP core. |
| **Core profile** | The current install-profile label. A successor should retire or rename it so it cannot be confused with the OpenSIP core. |

### 2.2 OpenSIP core responsibilities

The default installation is one small signed native OpenSIP core. It may own:

- static command grammar, help, completion, catalog routing, and collision rules;
- project and user configuration resolution;
- Snapshot capture; Plan construction and identity verification; fact-candidate
  admission; Coverage validation; policy/verdict derivation; D9 finalization;
  Run/evidence sealing; and durable commit authorization;
- secret-reference and optional authenticated-channel brokering;
- signature, trust, revocation, compatibility, and admission verification;
- component discovery, install, update, rollback, disable, remove, purge, and
  doctor orchestration;
- the common component control protocol and process supervision;
- host-owned output envelopes, D9 mapping, numeric exit selection, human/JSON
  rendering, bounded diagnostics, and security audit records;
- narrow brokers for approved state, artifact, secret-reference, network, and
  subprocess operations; and
- only the durable state required for configuration, signed trust metadata,
  component locks, install/update leases and journals, rollback counters,
  operator authorization, and lifecycle/security audit.

The default core must not link or require:

- syntax or semantic analyzers and language runtimes;
- rule matchers, graph algorithms, indexes, or query engines;
- report generators or report stores;
- analysis/evidence databases;
- telemetry exporters or telemetry backends; or
- provider-specific implementations.

The core still owns bounded diagnostics and security/lifecycle audit. Making
telemetry optional does not externalize the evidence needed to explain an
admission, update, rollback, or recovery decision.

### 2.3 Default distribution

- Core-only is the default supported install on every platform.
- Core-only is a management/recovery surface, not the current full offline
  analysis product. It cannot truthfully claim TypeScript/Rust/syntax/rule/graph
  analysis while those components are absent.
- TypeScript, Rust, syntax analysis, rule evaluation, graphing, reporting,
  analysis/evidence persistence, and telemetry are independently installable
  components.
- A signed convenience bundle may select a compatible component collection, but
  it is neither the OpenSIP core nor the default dependency closure.
- OpenSIP must publish at least one signed, locally installable, fully offline
  analysis closure (as a convenience bundle and/or air-gap bundle) that realizes
  the supported analysis product without network access after installation.
- CI selects an exact signed index snapshot, lockfile, platform closure, and
  payload set hermetically; it never resolves against a changing live catalog.
- Core-only remains useful for `--help`, `--version`, completion, configuration,
  component management, status, and doctor without loading project config or
  writing repository state.
- An analysis command with an absent required component returns a stable typed
  missing-capability/delivery-required response naming the exact requirement and
  explicit install/air-gap remediation. No command implicitly downloads,
  refreshes an index, or changes the lockfile.

## 3. One component model

### 3.1 Stable identity

Every component has a stable opaque component ID distinct from its display name,
aliases, and release version. The format need not be a UUID. Alias, rename,
deprecation, and ownership migrations are explicit and cannot silently create a
new identity or adopt another component's state.

Role-specific SDKs may exist for analyzers, providers, scanners, graph engines,
reports, persistence, and telemetry, but there is one lifecycle, one manifest
family, one catalog/status model, and one common control protocol.

### 3.2 Manifest-first discovery

Help, completion, catalog mounting, `component list`, and `component inspect`
read authenticated manifest/index data only. They do not:

- start component code;
- load a language runtime or grammar;
- open analysis/evidence storage;
- resolve project configuration; or
- probe customer-owned native prerequisites.

Runtime probes occur only after signature/digest verification and explicit
permission admission. Failed, staged, or quarantined candidates never enter the
public command catalog or normal dispatch, but lifecycle inventory, doctor, and
audit expose their state and exact refusal reason.

### 3.3 Proposed component manifest

A closed, versioned manifest should contain at least:

| Field group | Required content |
|---|---|
| Identity | stable component ID, display name, aliases, roles, release version, manifest schema version |
| Artifact | full immutable tree digest, per-file digest/size/type/mode, archive digest, media type, platform tuple, verified entrypoint, license identifiers, SBOM and attestation digests |
| Publisher | publisher identity, source/channel, signatures, provenance evidence, revocation identifiers |
| Compatibility | core control-protocol epoch, negotiated subprotocols, data-format read/write/migration epochs, supported platforms |
| Commands | host-routed operation shells under reserved host grammar, admission class, common flags, machine-surface mapping |
| Capabilities | provided capabilities, required core capabilities, component dependencies, customer-owned prerequisites |
| Permissions | closed requested permissions per operation, parameter schema, determinism class, required confinement, and trusted-code fallback policy |
| Configuration | strict namespaced configuration schema, analysis-affecting classification, secret-handle fields |
| State | state owner, independently versioned schema, migration/rollback support, retention and purge class |
| Update | signed index/channel identifiers, dependency/conflict constraints, deprecation/replacement information |

Manifests declaratively advertise operations. The core retains the public
grammar, parser, reserved names, collision/shadow policy, common flags, dispatch,
rendering, and exit semantics. Components do not install arbitrary root verbs or
component-defined renderers.

Speculative fields that no consumer enforces are forbidden. Future variation
uses versioned extension namespaces or negotiated capabilities.

Manifest and index signed bytes use a closed canonical serialization selected by
the successor contract. Duplicate keys, floats outside the selected profile,
unknown fields, Unicode/path aliases, non-canonical order, and a mismatch between
published ID and recomputed canonical bytes are typed refusals.

## 4. Lifecycle and recovery

### 4.1 Host-owned command family

The proposed common family is:

```text
opensip component discover|list|inspect|verify
opensip component install|update|rollback|disable|remove|purge
opensip component doctor
```

Role-specific configuration or invocation remains host-routed, but role-specific
installers and lifecycle vocabularies do not reappear.

### 4.2 State machine

The installed candidate and the active pointer are distinct:

```text
discovered
  -> staged
  -> cryptographically-verified
  -> permission-admitted
  -> probed-healthy
  -> atomically-active
```

Every pre-active state has defined refusal and quarantine transitions. Rollback
atomically restores the last known-good active pointer. A platform that requires
a post-switch probe marks the switch provisional and excludes it from normal
dispatch until health commits.

The admission order is fixed:

1. parse the closed manifest and selected signed-index metadata;
2. verify pinned-root continuity, thresholds, revocation, expiry, and rollback
   counters;
3. select the exact platform and dependency closure;
4. verify every artifact length and digest;
5. resolve project policy and user/operator authorization;
6. run a constrained probe or an explicitly authorized trusted-code probe over
   the exact staged bytes; and
7. atomically activate one verified generation.

No later step re-resolves, substitutes, repacks, or downloads an artifact.

Activation selects one **system generation**, not one executable in isolation.
The generation commits the exact component dependency closure, platform
alternatives, effective permission decisions, confinement/disclosure state,
configuration/state schema epochs, prepared migrations, and active executable
tree digests. One atomic pointer publishes that complete generation. Per-process
reference counts or generation leases keep its bytes and schema readers alive
until every operation pinned to it completes.

### 4.3 Concurrency and crash recovery

Install, update, rollback, remove, and purge share one reusable state machine and
must define:

- scoped leases and conflict policy;
- an append-only or transactionally updated journal;
- an atomic active-generation pointer mutation, separate from trust metadata;
- recovery after a crash at every transition;
- orphaned-stage inventory and cleanup;
- quarantine of ambiguous or unverifiable state; and
- idempotent resume or rollback;
- fsync of staged files/directories and journals before publication;
- same-filesystem rename/replace preconditions and typed refusal when unavailable;
- crash injection before and after every write, fsync, rename, pointer switch,
  migration transition, and cleanup; and
- process liveness, generation lease, and open-file/reference-count reconciliation.

A crash exposes either the previous complete generation or the new complete
verified generation, never a mixture.

Root trust versions, revocation snapshots, expiry observations, and anti-rollback
counters are monotonic security state. They are never included in executable
pointer rollback and can never move backward when an older generation is
reactivated. A known-good executable is not rollback-eligible if current trust
state revokes it or its publisher.

### 4.4 Remove, purge, and migration

- `remove` deactivates a component while retaining user- or project-owned data by
  default. Executable/provider/schema bytes referenced by retained authoritative
  evidence remain pinned until replay obligations expire or a contract-approved
  typed degradation is recorded.
- `purge` is a separate explicit, audited operation with preview and recovery
  semantics.
- Component state schemas and data-format schemas are versioned independently
  from the executable release.
- Upgrade, rollback, alias migration, or state migration cannot reinterpret or
  rewrite historical Run/evidence meaning.
- Uninstall and update document what is retained, where it is stored, who owns
  it, and which component versions can migrate or read it.

Every state/data migration uses a closed `prepare -> commit | abort` protocol.
Preparation writes a complete independently verified target without changing
authority. Commit atomically publishes the new schema/generation only after all
required readers and backward-read obligations are available. Abort leaves the
old state authoritative and cleans or inventories the target. A migration
declares the old versions it can read, the versions it writes, whether rollback
is possible after commit, and exact recovery for a crash at every transition.

Garbage collection computes reachability from retained Run/evidence manifests,
active/provisional generations, rollback slots, in-flight operation leases,
prepared migrations, and explicit retention policy. It must not remove any bytes
needed for promised replay, inspection, proof verification, migration, or
rollback. If product policy permits replay degradation instead, the host appends
a typed, addressable degradation/tombstone that names the unavailable closure and
the contract rule authorizing loss; absence never masquerades as reproducibility.

Purge is honest about its boundary: preview names OpenSIP-controlled evidence,
component state, caches, and executable closures, while explicitly excluding OS
backups, snapshots, dumps, swap, indexes, remote/external stores, and user copies.
Execution is tombstoned, journaled, idempotent, crash-recoverable, and observable
through inventory until completion.

### 4.5 Exact-byte and path security

Installation and execution bind the same authenticated immutable tree:

- extraction uses a private staging root, restrictive permissions, no archive
  traversal/absolute paths, no device/FIFO/socket entries, and an explicit policy
  for symlinks, hard links, sparse files, case folding, and Unicode normalization;
- every accepted path, type, mode, length, and digest is committed by the signed
  manifest's full-tree closure, including the entrypoint and runtime libraries;
- the entrypoint resolves within that tree after canonical path and link checks;
- execution uses an absolute descriptor/path or verified handle from the active
  generation, never `PATH`, loader search, system runtime substitution, shell
  lookup, or project dependency resolution;
- the core binds verification to execution using immutable/versioned locations,
  open-handle/identity checks where supported, and a digest/identity recheck when
  the platform cannot provide a stable handle; and
- any change between verification and spawn is quarantine/refusal, never a
  best-effort retry against new bytes.

Conformance includes hostile archives, duplicate/case/Unicode aliases, link
escapes, entrypoint replacement, loader injection, directory swap, same-path
inode replacement, concurrent updater/remover races, and verify-to-exec TOCTOU
tests on every supported filesystem/platform combination.

## 5. Protocol, supervision, and results

### 5.1 Common control protocol

OpenSIP should define one stable out-of-process control/lifecycle protocol. Stdio
JSON-RPC is a candidate, not a decision. The common contract includes:

- handshake and version/capability negotiation;
- component identity and exact manifest/artifact binding;
- start, operation, cancel, health, shutdown, and fault envelopes;
- typed operation results and structured diagnostics;
- deadlines, heartbeat, bounded messages, and backpressure;
- declared resource limits and observed-limit faults; and
- broker requests for host-mediated effects.

The protocol does not expose product-internal host objects as its public API.
Higher-level role SDKs are projections over the common control contract.

### 5.2 Existing provider data planes

The current TypeScript and Rust canonical-CBOR data planes remain distinct
negotiated subprotocols with their existing majors, ordering, bounds,
commitments, state machines, and conformance goldens. A common lifecycle does not
force their re-encoding or merge their evidence-affecting contracts. Any future
data-plane successor requires explicit compatibility rules and independent
goldens.

### 5.3 Supervisor contract

The core supervisor enforces or records, as applicable:

- startup, operation, cancellation, and shutdown deadlines;
- cancellation propagation and graceful-then-forced termination;
- heartbeat/liveness;
- bounded message, stdout, stderr, diagnostic, and artifact output;
- memory and process-count limits;
- backpressure;
- process-group/tree kill and orphan reaping;
- recovery after a core crash; and
- typed startup, protocol, resource, cancellation, and crash faults.

A crash, truncated stream, invalid frame, or failed commitment discards every
uncommitted candidate output from that operation.

### 5.4 Uniform outcomes

Components return one common typed operation/result/fault envelope. The host
alone maps it through existing D9 outcome/exit derivation and projects it to:

- the stable JSON/machine envelope;
- the human terminal frame;
- SARIF, HTML, MCP, or other host-owned projections where installed; and
- bounded fallback diagnostics.

Human and JSON views preserve the same semantic result. A renderer never changes
policy, evidence, or process termination.

## 6. Trust, permissions, and lockfiles

### 6.1 Multidimensional trust

Do not collapse these independent facts into one `trusted` boolean:

| Dimension | Question |
|---|---|
| Publisher | Who signed or attested the component? |
| Artifact | Which exact bytes and manifest were verified? |
| Channel | From which signed index, bundle, or local-development source did they arrive? |
| Operator authorization | Did this user authorize these bytes for installation or execution? |
| Requested permission | What authority does the manifest request for this operation? |
| Effective grant | What exact authority did project policy and the user grant for this Run? |
| Confinement | Is that authority mechanically enforced or merely disclosed? |
| Evidence authority | May this role contribute candidates, commit evidence, or only project a result? |

`managed`, hash-matched, or successfully installed is not synonymous with
publisher-verified, authorized, confined, or evidence-authoritative.

### 6.2 Per-operation grants

Static component-wide permission descriptions are insufficient. Requested
filesystem, network, subprocess, state, secret-handle, and artifact access is
declared per host-routed operation where possible. Install permission and Run
permission remain separate. Every analysis-affecting effective grant enters the
existing Plan identity/provenance path.

Permission resolution is a closed record, not a boolean:

```text
authorization: requested | granted | denied
outcome: enforced | disclosed-trusted-code | refused
source: project-policy | user-authorization | ci-policy | product-deny
```

`requested` is non-authoritative input; resolution must end in `granted` or
`denied`, and execution must end in `enforced`, `disclosed-trusted-code`, or
`refused`. No other state or implicit default is admitted.

- Deny has precedence over grant at every layer; absence is deny.
- A manifest and project repository may request authority but cannot grant it to
  themselves. Publisher verification never grants runtime authority.
- Every supported platform has a truth table mapping each permission mechanism
  to `enforceable`, `trusted-code-only`, or `unavailable`. Admission then emits
  only the closed execution outcome `enforced`, `disclosed-trusted-code`, or
  `refused`. Marketing and doctor report both the platform fact and the exact
  decision; neither invents a fourth outcome.
- An operation whose manifest says confinement is required refuses when the
  platform cannot enforce every required grant. It cannot fall back to trusted
  code.
- A trusted-code fallback requires explicit user consent bound to exact component
  ID, manifest/tree digest, operation, requested authority, and platform. CI and
  non-interactive modes require pre-existing policy; they never prompt or infer
  consent.
- A broker request is bound to `RequestId`, admitted `ExecutionId`/Run attempt,
  component ID and active generation, process instance/handshake, operation ID,
  grant ID/version, scope, and expiry. It cannot be replayed by another process,
  operation, generation, or project.
- Revocation or grant withdrawal during a Run follows a closed policy: deny new
  broker requests immediately, signal cancellation, bound cleanup, and let the
  core derive the typed terminal outcome. A component cannot continue with an
  already revoked ambient capability.

### 6.3 Project lockfile and user trust state

The tracked project component lockfile records:

- the selected signed-index snapshot/version/digest and channel identity;
- exact selected component IDs, versions, manifest IDs, and artifact digests;
- platform selector plus all signed acceptable platform alternatives used by the
  deterministic solver;
- canonical solver inputs, ordered decisions, conflicts, rejected alternatives,
  dependency closure, and final result digest;
- resolved compatibility/read/write/migration epochs and activation order;
- requested-permission schema/digests;
- selected data-format/migration epochs; and
- project-owned pins, holds, and policy constraints.

It does not contain secret values, publisher trust decisions, or self-granted
ambient authority. Publisher trust and user/operator authorization live in
user-scoped state and are bound to exact component identity and digest, and to an
operation where required.

The lockfile has one closed canonical serialization, duplicate-key/type/path
rejection, deterministic ordering, and a recomputed content identity. A stale
index snapshot may continue only under the declared offline policy; a revoked
selected artifact blocks new Runs and update/rollback selection even when locked.
Local-development entries are explicit, cannot claim publisher verification,
cannot acquire blocking policy authority, are excluded from CI unless an exact
CI policy admits their digest, and never weaken the signed closure around other
components.

### 6.4 Signed-index and emergency trust policy

The signed-index successor must retain the current pinned-root threshold model
and define, as closed protocol states:

- delegated publisher/component namespaces and path/role constraints;
- root, targets/index, snapshot, and timestamp/expiry roles or an equivalently
  explicit threshold design;
- snapshot/version binding that prevents mix-and-match and freeze attacks;
- monotonic revocation versions covering keys, manifests, trees, SBOMs, and
  attestations;
- quorum loss behavior: cached verified generations may follow a narrowly defined
  offline-running policy, but no install/update/trust change is accepted without
  quorum;
- root recovery/rotation ceremonies, including compromise and offline roots;
- emergency policy for an already-running or retained-replay component newly
  revoked during use; and
- an auditable break-glass process whose authority, scope, duration, and
  non-semantic effect are explicit.

The manifest binds the exact SBOM and attestation digests as artifacts in its
signed closure. A detached filename or mutable URL is not a binding reference.
Expired or stale metadata never silently reads as current; the offline policy
below decides whether an already verified closure may continue, with age and
limitation disclosed.

## 7. Evidence, persistence, and upgrade identity

Analysis/evidence persistence mechanics may be an optional component, but the
OpenSIP core remains the only evidence authority. The core authorizes and verifies
exactly one atomic commit through the host-owned protocol; the storage component
is a replaceable transaction/CAS/ledger mechanism, not a selectable authority.
It cannot seal a Run, accept a peer writer, derive evidence adequacy, or turn a
mechanical success into authoritative success. All non-storage components are
candidate producers or projections.

Each Run records the exact selected execution closure necessary to explain and
reproduce it:

- host semantic recipe/algorithm versions required by the applied Snapshot,
  Plan, fact, Coverage, policy, D9, and evidence contracts;
- stable component ID, release version, and artifact/manifest digest;
- negotiated control and semantic subprotocol epochs;
- analysis-affecting effective configuration digest and per-field provenance;
- declared inputs and effective capability grants; and
- relevant producer and authority classification.

Only analysis-affecting values enter `PlanId`. The complete available catalog,
UI-only core versions, update timestamps, unselected components, and telemetry
configuration remain operational provenance. A selected component closure or
lock snapshot may be retained without pretending the entire catalog was an
execution input.

Activation of a newer component never rewrites a historical `RunId`, Plan,
manifest, evidence digest, or recorded execution closure. Resume, replay, and
inspection of a retained Run use its recorded generation and protocol/schema
epochs, or return the contract-approved typed degradation; they never silently
substitute the currently active release. A genuinely new analysis follows the
existing Plan/Run identity rules rather than inheriting identity from an update.

## 8. Release, update, and offline indexes

### 8.1 Independent releases

The OpenSIP core and components release independently. A signed index binds
component identity, versions, platforms, hashes, manifests, compatibility,
dependencies, revocation state, and channels. A convenience bundle is a signed
selection over independent releases, not a coordinated package-version train.

Every released core/component artifact has:

- exact hashes and sizes;
- publisher signatures and provenance/attestation material;
- a CycloneDX or SPDX SBOM reference;
- license and dependency metadata;
- cross-platform qualification for the exact distributed bytes; and
- rollback qualification from the supported prior versions.

### 8.2 Offline and update policy

- Catalog refresh is explicit, policy-visible, and off the analysis path.
- Cached signed indexes support offline list, resolution, and install where
  payloads are present.
- Air-gap bundles carry the required root chain, revocation snapshot, index,
  manifests, and exact payloads.
- Channels, pins, holds, dependency solving, downgrade refusal, forced-downgrade
  audit, revocation, quarantine, and rollback are explicit.
- Update checks do not become ambient default-on network behavior.

No-network first use is a supported path: a core plus signed air-gap bundle can
verify roots, index snapshot, revocation state, lock, manifests, payloads,
permissions, and the complete offline analysis closure without DNS, OCSP, registry,
or artifact fetches. A missing payload produces typed remediation rather than a
fetch.

Expired timestamp/index metadata blocks new install, update, lock regeneration,
and trust changes. An already active, previously verified generation may continue
offline only when the signed offline-running policy permits it; output/doctor
disclose metadata age and limitation. Revoked bytes never become eligible merely
because the index is expired or the machine is offline.

### 8.3 Dependency and prerequisite model

Manifests distinguish:

- another OpenSIP component;
- a capability supplied by the core;
- an operating-system facility; and
- a customer-owned native binary, compiler, database, or service.

Doctor reports absent, incompatible, denied, shadowed, unhealthy, revoked, and
prerequisite-blocked states with exact remediation. It never silently installs a
customer-owned prerequisite.

### 8.4 Compatibility and deterministic resolution

Every release publishes a closed compatibility matrix rather than relying on
package semver:

- core/control/manifest/index major `N` reads `N`, `N-1`, and `N-2` where the
  matrix lists them; an unlisted or future major is a typed refusal, never a
  partial parse;
- the core writes only the current supported format `N`;
- user-custody data declares independent `readMajors`, `writeMajor`, and
  `migrateFromMajors`, with the current-plus-two window retained until a reviewed
  successor changes it;
- component executable version, control-protocol major, semantic subprotocol
  major, and data-format major negotiate independently; and
- rollback is allowed only when the target can read current authoritative state,
  current trust permits the bytes, and no committed migration crossed a declared
  no-return boundary.

The resolver is a pure deterministic function over the canonical signed-index
snapshot, lock constraints, platform, core capabilities, requested product
profile, compatibility matrix, project pins/holds, and policy. It rejects cycles
and unsatisfied conflicts. Candidate ordering and tie-breaks are canonical and
published; the lock records the exact inputs and result. Update preparation uses
a deterministic dependency/migration topological order, but publication is one
atomic system-generation activation so observers never see intermediate order.

An old core that authenticates an index envelope but does not understand its
schema reports `index-too-new` and may use only its last cached, unexpired,
compatible signed snapshot under offline policy. It never ignores unknown signed
fields, guesses compatibility, or rewrites the lock from a partially understood
index.

### 8.5 Core self-update, repair, and rollback

The core has a signed path that does not depend on loading an analysis component:

1. authenticate the new core and its platform closure with the pinned-root trust
   state;
2. stage and verify its exact immutable tree;
3. prove it can read current lifecycle/trust/lock state and the selected component
   generation;
4. quiesce or hand off active operations and fsync recovery state;
5. atomically switch a two-slot/versioned core pointer or use an equivalently
   crash-safe platform mechanism; and
6. retain a last-known-good core only while current trust and state compatibility
   permit rollback.

Repair can reinstall the current core from a signed offline bundle without
rolling back root/revocation/anti-rollback state. A failed start restores the
eligible last-known-good core and records a typed audited recovery. Exact
platform mechanism remains open, but self-update cannot be delegated to an
ordinary analysis component.

### 8.6 Doctor modes and probe consent

Doctor has a stable versioned machine schema and redaction contract. Its default
mode is read-only, no-network, and no-component-code: it verifies core files,
trust/index/lock/journal state, manifests, active-generation closure, permissions,
retained-evidence references, and static prerequisites from authenticated
metadata only.

- **Core mode** works without a project and diagnoses install/trust/update/core
  recovery state.
- **Project mode** additionally resolves the project lock and configuration under
  normal six-layer/CI rules, but does not admit analysis.
- Active probes, component execution, customer-binary invocation, or egress each
  require a named explicit flag/consent and appear in machine output with scope,
  bytes/endpoint, result, and residual limitation.
- Secrets and source excerpts remain redacted; doctor never mutates trust,
  permissions, lock, state, or prerequisites as a side effect.

## 9. Delivery budgets and conformance

### 9.1 Release-blocking budgets

CI must implement these named normative gates for the core-only closure:

| Gate ID | Requirement |
|---|---|
| `DL-BUDGET-CORE-DOWNLOAD` | Maximum compressed bytes for the signed core-only platform closure |
| `DL-BUDGET-CORE-INSTALLED` | Maximum installed bytes for the verified immutable core tree and mandatory lifecycle/trust state fixture |
| `DL-BUDGET-CORE-HELP` | Cold `opensip --help` p50/p95 wall time with empty OS/file cache and no project/component load |
| `DL-BUDGET-CORE-VERSION` | Cold `opensip --version` p50/p95 under the same method |
| `DL-BUDGET-CORE-RSS` | Baseline and peak RSS for help/version plus idle lifecycle command |
| `DL-BUDGET-COMPONENT-DELTA` | Per-component download/install/startup/RSS delta against the same core baseline |
| `DL-BUDGET-OFFLINE-BUNDLE` | Aggregate download/install/startup/RSS for the supported full offline analysis closure |

Each optional component reports its independent download, install, cold-start,
and memory contribution. A convenience bundle reports aggregate cost and cannot
redefine the core budget.

Exact numeric thresholds remain explicit open product decisions and must be
filled before release; the gate requirements themselves are not optional. Each
gate publishes supported-platform reference runners, filesystem/cache state,
network state, corpus/fixture, warm-up rule, sample count, p50/p95 (and p99 where
relevant), variance/outlier policy, toolchain/build profile, raw results, and
reproduction command. Release engineering owns execution and raw evidence;
product authority owns thresholds; architecture review owns what is included in
the core/component/bundle closure.

A release fails on threshold breach or an unexplained regression beyond the
published tolerance versus the last supported release. Budget increases require
an explicit product disposition with measured cause; a convenience bundle cannot
hide a core regression by changing its aggregate budget.

### 9.2 Component conformance kit

Release qualification covers the exact distributed bytes and includes:

- manifest/index/runtime coherence and closed-schema rejection;
- canonical manifest/index/lock serialization and ID recomputation;
- safe extraction, full-tree closure, entrypoint/path/loader refusal, and
  verify-to-exec TOCTOU attacks;
- common-control and negotiated-subprotocol fixtures;
- hostile, duplicate, missing, oversized, unordered, and truncated frames;
- cancellation, deadline, heartbeat, backpressure, and resource exhaustion;
- process-tree cleanup and orphan recovery;
- crash injection at every install/update/migration/remove/purge write, fsync,
  rename, pointer switch, and cleanup transition;
- system-generation closure, process/reference-count pinning, rollback,
  quarantine, revocation-during-run, expiry, quorum loss, and downgrade refusal;
- strict configuration and per-value provenance;
- platform permission truth tables, required-confinement refusal, trusted-code
  consent, CI/noninteractive denial, and broker instance/Run binding;
- deterministic dependency solving, conflicts, cycles, platform alternatives,
  old-core/new-index behavior, and update order;
- state migration prepare/commit/abort, backward read, retained-evidence replay
  closure, garbage collection, retained-on-remove, and explicit purge;
- doctor core/project modes, default no-code/no-network/no-mutation behavior,
  redaction, and consented probe/egress records;
- no-network first run, expired index, cached-index, air-gap install, core
  self-update, repair, and rollback; and
- supported-platform installation and prior-version rollback of both core and
  full offline analysis closure.

Third-party components are never described as safe merely because they pass the
kit. The result states exactly which properties were tested and which ambient
authority remains.

## 10. Validated prototype lessons

The earlier OpenSIP CLI is evidence, not an implementation template.

### 10.1 Carry forward

| Proven contract | Required successor property |
|---|---|
| No-write first value | Same validated in-memory intent before init; explicit identity-preserving adoption later. |
| Manifest-first discovery | Inventory, help, completion, and command shells without executing component code. |
| Stable identity | Opaque IDs distinct from aliases, names, and versions, with migration rules. |
| Exact-byte activation | Stage, verify, admit, and activate the same bytes; never re-resolve after validation. |
| Explainable admission | Deny by default; expose source, hash, publisher state, policy, permissions, shadowing, and reason. |
| Supervised execution | Limits, cancellation, heartbeat, backpressure, process-tree cleanup, and typed recovery/faults. |
| Host-mediated effects | Narrow broker contracts, with an honest distinction between enforced grants and trusted-code conventions. |
| Uniform outcomes | One component result envelope; host-owned human/JSON rendering and stable exit precedence. |
| Durable local evidence | Offline reads, stable Run references, retained data on remove, explicit purge. |
| Strict config and secrets | Closed schemas, deterministic precedence, per-value provenance, and secret handles only. |
| Verifiable releases | Signed exact bytes, SBOMs, attestations, staged qualification, rollback, and no-downgrade trust. |
| Shared adapter operations | Common doctor, version, parsing, redaction, provenance, and progress semantics in SDKs. |

### 10.2 Add explicitly

- State ownership, schema migration, retention, remove-versus-purge, rollback, and
  orphan-state recovery.
- Leased and journaled crash-safe lifecycle operations with active-pointer
  atomicity and separately monotonic trust mutation.
- Component, core-capability, and customer-prerequisite dependency types.
- Multidimensional trust rather than `managed == trusted`.
- Per-operation requested permissions and effective grants.
- Selected component closure and analysis identity across upgrades.
- Per-effective-value configuration provenance.
- Signed cached/offline indexes, visible refresh policy, pins, holds, dependency
  solving, rollback, and air-gap bundles.
- A publisher conformance kit covering hostile transport, lifecycle recovery,
  config, storage, permissions, and exact release artifacts.

### 10.3 Do not carry forward

- A large lockstep npm monorepo or coordinated same-version package train.
- Node/npm as the default runtime and installation burden.
- A full analysis platform bundled into the default install.
- Rebootstrapping the complete CLI as a component worker.
- Product-internal context objects as the public component RPC.
- Separate tool, plugin, pack, scanner, and native-binary lifecycle vocabularies.
- Duplicate transaction/recovery machinery per command.
- A manifest hash or managed install treated as publisher provenance.
- Monkey-patching or a bare process boundary marketed as confinement.
- Default-on ambient update checks without visible egress policy.
- Speculative manifest fields with no enforcing consumer.

## 11. Explicit non-goals

This transition does not:

- redesign facts, Coverage, `PlanId`, Run/evidence, D9 outcomes, or policy;
- add a second graph/query semantic path, a selectable evidence authority, or a
  component that independently seals/commits Runs;
- introduce mandatory Cloud, login, billing, entitlement, or model calls;
- permit components to mutate source or project policy implicitly;
- create arbitrary component-owned root commands or renderers;
- promise source confidentiality from code allowed to read source;
- claim a process boundary is a sandbox;
- choose JSON-RPC over another control transport without a reviewed contract;
- force the existing provider data planes into one encoding;
- select final performance budgets without product evidence; or
- authorize implementation before binding successors are independently reviewed
  and applied.

## 12. Open decisions

The following require explicit owners and reviewed successors:

1. Final native implementation language and platform-specific signing/notarization
   details for the OpenSIP core.
2. Common control-protocol transport and extension mechanism; current provider
   data-plane majors remain negotiated subprotocols.
3. Component manifest/index/lock canonical encoding and exact signed-index role,
   delegation, snapshot, expiry, and recovery schema.
4. Stable component-ID syntax and alias governance.
5. Exact host-owned command namespace and collision/shadow rules.
6. Supported OS/WASM confinement mechanisms, permission truth-table rows, and
   honest trusted-code fallback labels per platform.
7. Which storage-mechanics component is supported first and the exact host-owned
   commit/replay interface; core evidence authority is not open.
8. Lockfile filename, canonicalization, platform alternatives, update workflow,
   merge-conflict rules, and local-development policy.
9. Keychain and secure-file fallback behavior on each supported platform.
10. Exact contents/platforms of the supported signed fully offline analysis
    closure and air-gap bundle.
11. Core self-update atomic mechanism and last-known-good repair slots per
    platform.
12. Release-blocking numeric thresholds and regression tolerances for the named
    core/component/bundle gates.
13. Signed-index refresh defaults, channel/pin/hold governance, metadata expiry,
    quorum-loss, emergency running-component, and offline cache policy.
14. Retained-evidence replay window versus contract-approved typed degradation
    and executable/schema garbage-collection policy.
15. Doctor machine-schema version, consented probe set, and egress disclosure.
16. Third-party support, vulnerability-response, revocation, publisher-policy,
    and break-glass authority ownership.

## 13. Adoption and review checklist

Before this proposal can become binding, reviewers should require all of the
following:

- [ ] One successor decision defines the OpenSIP core/component ownership
      boundary and resolves the three meanings of *core*.
- [ ] The closed responsibility matrix leaves Snapshot, Plan/`PlanId`, fact
      admission/`FACT-ID`, Coverage, policy/verdict, D9, Run/evidence sealing, and
      commit authorization non-delegably in the OpenSIP core.
- [ ] Product boundary and delivery successors replace full-by-default with a
      management-only core default and publish a signed locally installable full
      offline analysis closure with hermetic CI selection.
- [ ] Existing fact, Coverage, Plan, Run, evidence, and D9 goldens remain
      unchanged or any intentional successor is separately justified.
- [ ] Trusted and untrusted analysis components consume only host-sealed
      snapshots/read sets and obey existing neutralized/keyed/forbidden ambient
      input rules; semantic inputs and operational provenance are mechanically
      separated without PlanId churn or a Session identity.
- [ ] The six-layer configuration model, CI layer-4 exclusion, per-value
      provenance, and secret-value exclusion remain exact.
- [ ] Signed-index and independent-release changes preserve pinned roots,
      rotation, revocation, expiry, anti-rollback, offline verification, and
      exact-byte activation, and close delegation/snapshot/freeze/quorum-loss/
      emergency policy with SBOM/attestation digests signed into the closure.
- [ ] The manifest schema, lifecycle state machine, recovery journal, trust
      matrix, permission model, lockfile, protocol envelopes, and conformance kit
      are closed and independently reviewed.
- [ ] Safe extraction, immutable full-tree closure, canonical serialization,
      verified entrypoint/loader resolution, and verify-to-exec binding pass
      hostile path and TOCTOU tests on every supported platform.
- [ ] Activation publishes one dependency/permission/schema/migration system
      generation; fsync/rename/crash recovery and process/refcount pinning are
      exact, while root/revocation/rollback-counter state remains monotonic and
      outside executable rollback.
- [ ] Existing TypeScript and Rust semantic data planes remain valid negotiated
      subprotocols or have explicit reviewed successors with compatibility
      goldens.
- [ ] The core remains the sole evidence authority and verifies one atomic
      host-owned commit; optional storage mechanics never independently
      seal/commit a Run or become selectable authority.
- [ ] Remove retains user data by default; purge and migration are explicit,
      recoverable, and audited.
- [ ] Retained evidence pins required executable/schema/subprotocol replay bytes
      until GC eligibility or appends a contract-approved typed degradation;
      migration prepare/commit/abort and backward-read rules are closed.
- [ ] Manifest-only discovery executes no component code and loads no analysis
      runtime or store.
- [ ] Human and JSON outcomes remain one host-owned semantic projection.
- [ ] Security claims distinguish publisher provenance, authorization, grants,
      enforcement, trusted code, and evidence authority.
- [ ] Permission decisions use closed requested/granted/denied and
      enforced/disclosed outcomes with deny precedence, no self-grant, platform
      truth tables, CI policy, required-confinement refusal, trusted-code consent,
      revocation-during-run, and broker Run/operation/instance binding.
- [ ] Compatibility covers `N`/`N-1`/`N-2`, read/write/migration windows,
      deterministic solving/conflict/cycle/order, old-core/new-index behavior,
      core self-update/repair, expired metadata, and no-network first use.
- [ ] The canonical lock binds the selected signed-index snapshot/channel,
      platform alternatives, solver inputs/results, permissions, stale/revoked
      behavior, and local-development limits.
- [ ] Doctor is read-only/no-network/no-code/no-mutation by default, has stable
      redacted machine output, distinct core/project modes, and explicit consent
      for probes or egress.
- [ ] Purge previews and tombstones its OpenSIP-controlled scope, is idempotent and
      crash-recoverable, and honestly excludes backups/external stores/user copies.
- [ ] Core and component delivery budgets have reproducible, release-blocking CI
      methods, named normative gate IDs, supported-platform/core/component/bundle
      coverage, regression policy, and explicit threshold ownership.
- [ ] Migration from the current full-default profile is documented without
      rewriting historical evidence or silently changing user custody.
- [ ] Successors pin the exact advanced heads from the blueprint/freeze status
      tables and do not treat this brief or narrative architecture prose as
      application/status authority.

## 14. Expected successor touch points

If accepted, the change should be reconciled narrowly through successors to the
current product-boundary, rules/extensions, surfaces/command grammar, delivery,
implementation blueprint, open-decisions, and traceability material. This brief
does not make those edits itself.

The intended deliverable from the design phase is a concise delta containing:

1. changed binding decisions;
2. a core-versus-component responsibility matrix;
3. the closed component manifest and signed-index schemas;
4. lifecycle and crash-recovery state machines;
5. control-protocol handshake and operation/result envelopes;
6. trust and permission matrices plus residual-risk language;
7. configuration, lockfile, state, evidence, and migration rules;
8. independent release/update/rollback/offline flows;
9. migration from the current full-default architecture; and
10. measurable acceptance gates and remaining open product decisions.
