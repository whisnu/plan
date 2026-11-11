# NEXA PE-02 — GATE B BOUNDED PLANNING EVIDENCE RETURN
## Programmer Evidence Return for Architecture-Feasibility & Prerequisite Disposition
### Targeted Corrective Reconciliation (Ref: PLAN §16.21.9 & §16.21.10)

---

## 1. HEADER AND PHASE DECLARATION

- **Deliverable File:** `PE-02_GATE_B_BOUNDED_PLANNING_EVIDENCE_RETURN.md`
- **Delivery Path (Local Staging):** `evidence/postsprint16-presprint17/PE-02_GATE_B_BOUNDED_PLANNING_EVIDENCE_RETURN.md`
- **Author / Submitting Role:** Lead Programmer (Nexa Core Engineering)
- **Target Recipient:** Architecture Authority (AA) / Product Owner (PO)
- **Date & Session Timestamp:** 2026-11-11T11:25:00+07:00
- **Governing Specification:** `evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (§16.21.9 & §16.21.10)
- **Phase Declaration:** **`PLANNING ONLY`**.
- **Mandatory Governance Attestation:**
  - This document provides a targeted corrective evidence return assessing whether existing Nexa persistence and native-proof foundations are compatible with the approved PE-02 architecture under Zero-DDL constraints.
  - **No implementation work has been performed.**
  - **Zero Source Code Mutation:** No application, SDK, viewer, or tool source code has been created, modified, or deleted.
  - **Zero Database Migration / DDL:** No SQL schema, migration, table, column, index, constraint, or DML was executed.
  - **Zero Root Pollution:** The repository root `/opt/antigravity/projects/nexa/` remains 100% clean (Rule D honored).
  - **Baseline Protection:** Sprint 16 and PE-01 remain strictly 🔒 `CLOSED / FROZEN`.
  - **Implementation Status:** PE-02 implementation remains strictly 🔒 `NOT AUTHORIZED`.

---

## 2. A1 SOURCE BASELINE & DISCREPANCY DISCLOSURE

### 2.1 Authoritative Baseline Pinned from Original A1 Report
In compliance with §16.21.10.2, the source baseline is copied verbatim from the original A1 evidence report (`evidence/postsprint16-presprint17/PE-02_SOURCE_EVIDENCE_AND_GAP_IDENTIFICATION_REPORT.md#L4-L14`):

| Parameter | Authoritative Value from A1 Report | Verification Method on Remote Host |
|---|---|---|
| **Repository Target** | `whisnu/nexa` | Verified via `git remote -v` |
| **Active Branch** | `main` | Verified via `git branch --show-current` |
| **Commit SHA (HEAD)** | `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` | Verified via `git rev-parse HEAD` |
| **Remote HEAD (`origin/main`)** | `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` | Verified via `git rev-parse origin/main` |
| **Canonical Plan Baseline Blob** | `5dcb5ff0261aea9ae434d02af451ca4d4cde5a62` | Verified via `git hash-object` on Plan baseline |
| **A1 Inspection Timestamp** | `2026-11-10T16:26:00+07:00` | Recorded in A1 report §1 |
| **Examined Source Scope** | `marketplace/`, `storage/`, `internal/`, `sdk/`, `studio-desktop/`, `player-desktop/`, `mobile/` | Documented in A1 Search Manifest |

### 2.2 PLAN Cross-Reference Commit SHA Discrepancy Disclosure (§16.21.10.2)
In accordance with §16.21.10.2 item 2, Programmer explicitly flags the following discrepancy within the canonical PLAN document:
1. **PLAN §16.8.2 (`PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md:L3965`):** Cites commit `fc08a5c7ac6aa1b0e4bcf64dc2cce066f149e1956` (contains typographical segment `...dc2cce066f...`).
2. **PLAN §16.16.2 (`PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md:L4116`) & Original A1 Report (`L6`):** Cites commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (contains segment `...dc264666f...`).
3. **Discrepancy Resolution:** Programmer does not infer or guess between the two strings. Programmer adopts the exact SHA `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` directly from the original A1 report (which matches remote `origin/main` HEAD) and submits this discrepancy in §16.8.2 to AA for plan reconciliation.

---

## 3. EXECUTIVE DISPOSITION

In strict accordance with §16.21.10.3, §16.21.10.4, and §16.21.10.7 item 3, Programmer provides separate preliminary dispositions for the two Gate-B prerequisite groups:

| Prerequisite Group | Architectural Scope | Preliminary Evidence Status | Planning Feasibility Disposition |
|---|---|---|---|
| **B-04 / B-05 / NC-06** | Zero-DDL Durable Persistence (Checkout Manifest, Per-Member Receipts, Child Hash, Album Identity & Association) | `FEASIBILITY NOT VERIFIED FROM EXISTING EVIDENCE` | **`BLOCKED`** — Existing PostgreSQL schema is strictly flat 1:1 (`acquisitions` $\leftrightarrow$ `entitlements`). No durable tables or columns store multi-member checkout receipts, parent-child mappings, or child member hashes in examined scope. Candidate `StorageEngine` provides flat binary payload streaming and JSON sidecars, but does not provide composite relational correlation, ACID transaction boundaries across multi-entity records, or conditional update controls under Zero-DDL. |
undefined

> **Gate B Recommendation:** In accordance with §16.21.10.7 item 3, Programmer makes **NO RECOMMENDATION TO PASS GATE B**. Gate B remains independently **`BLOCKED`**. Gate A remains **`PASS — PLAN / CONTRACT READINESS ONLY`**. Implementation remains **`NOT AUTHORIZED`**.

---

## 4. MATRIX A — ZERO-DDL PERSISTENCE FEASIBILITY (B-04 / B-05 / NC-06)

*Evaluation Question (§16.21.10.3):* Can the approved logical records and relationships be represented, written, read, correlated, protected from overwrite, and recovered using identified existing durable storage mechanisms, without DDL or schema change?

| Req ID | Required Logical Record / Invariant | Existing Mechanism / Object / Field | Producer | Write Operation & Transaction Boundary | Durable Lookup / Consumer | Immutability & Concurrency Primitive | Restart / Recovery / Retention / Backup Evidence | Exact Source Citations | A1 Status | Planning Feasibility Disposition / Gap |
|---|---|---|---|---|---|---|---|---|---|---|
| **A-WP01-01** | Immutable Checkout Manifest SSOT (`bundle_checkout_id`, total price, currency, member list, commercial intent) | **None in PostgreSQL.** Candidate Storage Engine (`StorageEngine`) has `StorePackageStream` producing an object payload and sidecar metadata. | No producer for multi-member checkout manifest in `marketplace/server.js`. | PostgreSQL `withTransaction` only writes single-item `acquisitions` (`server.js:L3581-L3602`). Storage Engine writes local disk sidecar JSON (`storage_engine.go:L205-L228`). | No consumer lookup for checkout manifest by `bundle_checkout_id`. | Storage Engine: `O_EXCL` is used when creating a staging temporary file (`storage_engine.go:L176`); this establishes exclusive creation of that path, not immutability of the promoted object. PostgreSQL: `SELECT FOR UPDATE` is used on `payment_orders` (`server.js:L3801`), not as proof of composite receipt immutability. | `NOT VERIFIED FROM A1`. No automated restore, WAL archiving, or recovery procedure for composite checkout manifests is evidenced in A1. | `marketplace/db/schema.postgres.sql:L63-L75`, `marketplace/server.js:L3581-L3602`, `storage/internal/store/storage_engine.go:L164-L230` | `NOT FOUND IN EXAMINED SCOPE` | **FEASIBILITY NOT VERIFIED**. Neither PostgreSQL nor Storage Engine provides an existing durable Checkout Manifest record in examined scope. Storing it as a sidecar in Storage Engine requires inventing an unevidenced caller mapping to PostgreSQL. |
| **A-WP01-02** | Per-member execution receipt & separate `member_execution_key` correlation | `acquisitions` table stores 1 row per checkout (`acquisition_id`, `asset_id`, `buyer_id`, `state`). | `marketplace/server.js:L3583-L3592` | Single `INSERT INTO acquisitions` inside local `withTransaction` (`server.js:L3583`). No batch or per-member loop. | `SELECT * FROM acquisitions WHERE acquisition_id = $1` (`server.js:L3808`). | Primary key constraint on `acquisition_id VARCHAR(128)` (`schema.postgres.sql:L64`). | `NOT VERIFIED FROM A1`. The cited code establishes a local transaction for the single-row acquisition write; WAL configuration/archiving and per-member recovery state are not evidenced. | `marketplace/db/schema.postgres.sql:L63-L75`, `marketplace/server.js:L3581-L3602, L3800-L3865` | `NOT FOUND IN EXAMINED SCOPE` | **FEASIBILITY NOT VERIFIED**. Existing table stores single-item acquisitions only. No `member_execution_key`, `bundle_checkout_id`, or per-member sub-receipt field exists under Zero-DDL in examined scope. |
| **A-WP01-03** | External License Daemon request identity & status/receipt lookup (PENDING/UNKNOWN vs confirmed) | HTTP calls to `/api/v1/licensing/prepare`, `/sign`, `/submit`. Response returns `licenseKey`. | `marketplace/server.js:L248-L303` | Panggilan HTTP di tengah transaksi PostgreSQL sebelum `COMMIT` (`server.js:L3836`). Timeout 2500ms (`server.js:L212`). | No status query or receipt lookup endpoint in `marketplace/server.js`. | None. No 2PC, no idempotency header, no distributed compensation. | `NOT FOUND IN EXAMINED SCOPE`. No reconciliation worker exists. If HTTP fails post-commit, ghost grant occurs without local tracking. | `marketplace/server.js:L210-L305, L3794-L3870` | `NOT FOUND IN EXAMINED SCOPE` | **FEASIBILITY NOT VERIFIED**. HTTP client does not support status lookup (`GET /api/v1/licensing/:id/status` absent). PENDING/UNKNOWN cannot be queried from daemon using existing code. |
| **A-WP01-04** | Operational durability, retention, backup, restore guarantees for checkout receipts | PostgreSQL relational database cluster (`marketplace/db/store.js:L89-L103`). | PostgreSQL engine. | Local PostgreSQL transaction wrapper (`store.js:L89-L103`); WAL configuration/archiving is not established by this citation. | Application database connection pool (`store.js:L60`). | PostgreSQL ACID engine with row-level locks on `payment_orders`. | **`NOT VERIFIED FROM A1`**. The presence of PostgreSQL transactions and single-row locks proves local ACID execution for single acquisitions, but does not prove operational durability, retention, backup, restore, or recovery guarantees for PE-02 multi-member checkout receipts under Zero-DDL. | `marketplace/db/store.js:L89-L103`, `marketplace/db/schema.postgres.sql:L63-L135` | `NOT VERIFIED FROM A1` | **NOT VERIFIED**. PostgreSQL primitives exist in code, but operational backup/restore procedures, retention rules, and multi-entity recovery contracts for Album checkout persistence are not evidenced in A1. |
| **A-WP02-01** | Wrapper ZIP package hash preservation (`acquired_package_sha256`) | Column `acquired_package_sha256 VARCHAR(64)` on `acquisitions` and `entitlements`. | `marketplace/server.js:L2231` (`computeFileSha256(session.spool_path)`). | Written during catalog upload (`server.js:L2396`) and copied to `acquisitions` (`L3853`) and `entitlements` (`L3858`). | Download authorization: `marketplace/server.js:L4271, L4309, L4366, L4458`. | Schema column constraint: `VARCHAR(64)` (`schema.postgres.sql:L72, L112`). | Database field and write/read references are cited; operational durability, retention, backup, restore, and recovery guarantees are not established by those references. | `marketplace/db/schema.postgres.sql:L72, L112`, `marketplace/server.js:L762-L770, L2231, L3853, L3858` | `SUPPORTED BY EXISTING A1 EVIDENCE` | **FEASIBLE FROM EXISTING EVIDENCE** (as wrapper hash only). The byte domain is strictly verified as the complete ZIP delivery package spool. |
| **A-WP02-02** | Child member `.nx` `member_sha256` storage & immutable mapping | **None in PostgreSQL schema.** `catalog_snapshots`, `acquisitions`, and `entitlements` have no column for child member hash. | No producer for child member hashes in `marketplace/server.js`. | None. | None. | None. | None. | `marketplace/db/schema.postgres.sql:L4-L135`, `marketplace/server.js:L2230-L2410` | `NOT FOUND IN EXAMINED SCOPE` | **FEASIBILITY NOT VERIFIED**. Storing individual child member `.nx` hashes without DDL requires an unevidenced external mapping. Repurposing `acquired_package_sha256` is strictly prohibited. |
| **A-WP05-01** | Stable Album ID & ordered member association persistence / reload | **None in NX Studio or Marketplace.** Studio only supports single-asset forging and publication. | `studio-desktop/main.js:L682-L870` (`forge-asset`), `L1097-L1240` (`publish-asset`). | Single `.nx` file creation via IPC. No album project format. | Single-asset load in Studio. | None for collective albums. | None. | `studio-desktop/main.js:L682-L870, L1097-L1240`, `marketplace/db/schema.postgres.sql:L4-L62` | `NOT FOUND IN EXAMINED SCOPE` | **FEASIBILITY NOT VERIFIED**. No existing Studio project file format or Marketplace catalog structure supports ordered Album member association under Zero-DDL. |

---

## 5. MATRIX B — NATIVE-PROOF COMPATIBILITY (B-09: SIX CATEGORIES)

*Evaluation Question (§16.21.10.4):* Can the native proof material required by the approved three-tier Membership Authority design be embedded as evidence while preserving its original signed bytes/preimage and verified through existing authoritative Nexa trust/identity foundations?

| Category | Native Proof / Serialized Representation | Signed Bytes & Exact Preimage / Canonicalization | Authoritative Verifier & Caller Path | Issuer & Subject / Key Lineage | Validity / Rotation / Revocation / Time Semantics | Independent Trust-Anchor Termination | Embedding Compatibility Without Changing Native Proof | Exact Source Citations | A1 Status | Planning Feasibility Disposition |
|---|---|---|---|---|---|---|---|---|---|---|
| **1. Genesis credential & trust-anchor termination** | `GenesisOwnershipCertificate` (JSON) embedded in Registry Certificate (`sdk.ts:L220-L240`). | Canonical JSON string of exactly 8 fields (`asset_id`, `creator_public_key`, `effective_at`, `issued_at`, `issuer_id`, `previous_cert_ref`, `subject_id`, `underlying_cert_id`). Ed25519 signature over UTF-8 bytes. | Verifier: `NexaCrypto.verify(creator_public_key, canonGenesisBytes, signatureBytes)` in `sdk/typescript/src/sdk.ts:L239`. Go: `pkg/nexa/identity.go:L91`. | Issuer is Creator (`creator_public_key`). Binds `subject_id` to `asset_id`. | Static validity (`effective_at`, `issued_at`). No key rotation in individual genesis cert. Fail-closed on signature mismatch (`sdk.ts:L227-L229`). | In baseline, trust terminates at pinned `registryPubKey` (for outer cert) and self-signed `creator_public_key` (for genesis). Independent offline trust anchor file is not evidenced in A1. | **COMPATIBLE (WITH RESIDUAL)**. Can be embedded as an intact JSON object inside Tier-1 evidence. Inner preimage is preserved. | `sdk/typescript/src/sdk.ts#L205-L260`, `sdk/typescript/src/ownership.ts:L26-L55`, `pkg/nexa/identity.go:L91` | `NOT VERIFIED FROM A1` (for offline anchor) | **COMPATIBLE IN PREIMAGE; TRUST ANCHOR UNVERIFIED**. Serialized 8-field representation can be embedded intact; however, local offline trust anchor termination remains unverified in examined scope. |
| **2. Organization & Individual subject/key lineage** | **(A) Organization:** `RootRecoveryAssertion`, `ActiveKeyAuthorizationAssertion` (`internal/domain/identity.go:L81-L114`).<br><br>**(B) Individual:** Raw Ed25519 public key hex string (`internal/domain/identity.go:L30`). | **(A) Org:** Canonical JCS (RFC 8785) over assertion structs (`internal/engine/identity/verifier.go:L23-L65`).<br><br>**(B) Ind:** 8-field canonical JSON in Genesis cert. | **(A) Org:** `internal/engine/identity/lineage.go:L95-L154` (`ResolveRootAuthorityAt`), `verifier.go:L152-L175`.<br><br>**(B) Ind:** `sdk/typescript/src/sdk.ts:L239`. | **(A) Org:** URN `urn:nexa:id:<sha256(genesisPubKey)>` (`subject.go:L13-L25`). Monotonic sequence lineage.<br><br>**(B) Ind:** Direct hex public key binding; no URN derivation formula in `subject.go`. | **(A) Org:** Monotonic sequence numbers, competing recovery branch conflict detection (`ErrCodeLineageBranchingConflict`). Active key resolved at timestamp via `ResolveRootAuthorityAt`.<br><br>**(B) Ind:** Static timestamps (`effective_at`, `issued_at`). No rotation or recovery chain evidenced. | **(A) Org:** Genesis Root public key digest serves as anchor (`lineage.go:L47-L51`).<br><br>**(B) Ind:** Self-asserted key; independent trust anchor is `NOT VERIFIED FROM A1`. | **(A) Org: COMPATIBLE**. Organization assertion objects can be embedded intact without modifying JCS preimage.<br><br>**(B) Ind: PARTIAL**. Individual creator has no native lineage or rotation object. | `internal/domain/identity.go:L62-L114`, `internal/engine/identity/lineage.go:L16-L154`, `internal/engine/identity/subject.go:L13-L56`, `tests/identity/lineage_test.go:L218` | `SUPPORTED BY EXISTING A1 EVIDENCE` (for Org); `PARTIAL / NOT VERIFIED FROM A1` (for Individual) | **COMPATIBLE FOR ORGANIZATION; GAP FOR INDIVIDUAL**. Organization identity lineage can be embedded and verified natively. Individual creator lacks key rotation, lineage, and anchor termination foundations in examined scope. |
| **3. Album-wide rights/authority basis** | None for Albums. Existing: `OwnershipCertificate` for individual `asset_id` (`sdk/typescript/src/ownership.ts:L1-L120`). | Preimage binds single `asset_id` to single owner/creator (`ownership.ts:L35-L50`). | `pkg/nexa/identity.go:L91`, `sdk/typescript/src/sdk.ts:L239`. | Binds single `asset_id`. No multi-asset or album authority binding in native structures. | Single-asset validity window. | Pinned Registry key. | **NOT FOUND IN EXAMINED SCOPE**. Existing proof binds single `asset_id` only. Album-wide authority designation does not exist in native proof. | `sdk/typescript/src/ownership.ts:L1-L120`, `internal/domain/ownership.go:L1-L110` | `NOT FOUND IN EXAMINED SCOPE` (A1 report §6, B09-03) | **Existing evidence:** `OwnershipCertificate` binds an individual `asset_id`; it does not establish authority over an Album collection. **Planning treatment:** the Album-wide Authority Designation is a new Album-specific carrier already specified by the approved PE-02 architecture and assigned to WP-04. Its absence from current source is `NOT APPLICABLE TO PLANNING FEASIBILITY`, not a pre-authorization existence blocker. Do not infer Album-wide authority from child certificates. |
| **4. Registry/Federated issuer provenance & offline trust** | `RegistryCertificate` in SDK (`sdk.ts:L205-L218`), table `registries` (`migrations/003_registry_identity.sql:L1-L30`). | Canonical 6-field JCS string (`certificate_id`, `issued_at`, `issuer`, `status`, `valid_until`, `creatorKey`). Ed25519 signature. | SDK: `NexaRegistry.canonicalJcs` + `NexaCrypto.verify` (`sdk.ts:L215-L218`). | Issuer string matching `registry_id`. Public key fetched via HTTP from registry or DB table. | `valid_until` timestamp check. Online status query via HTTP (`sdk/typescript/src/registry.ts:L45-L80`). | DB table `registries.public_key`. No locally pinned root certificate file evidenced in A1. | **PARTIAL**. 6-field JCS preimage can be embedded intact; but offline trust anchor verification path is unverified in A1. | `migrations/003_registry_identity.sql:L1-L30`, `sdk/typescript/src/sdk.ts:L205-L225`, `sdk/typescript/src/registry.ts:L1-L120` | `NOT VERIFIED FROM A1` (for offline anchor) | **PARTIAL COMPATIBILITY**. Native 6-field Registry Certificate can be embedded without altering preimage, but independent offline anchor verification is not evidenced. |
| **5. Signed revocation/status evidence & Dual-Horizon evaluation** | **(A) Native Revocation Proof:** Table `registries.trust_status` (`003_registry_identity.sql:L6`) and status enums `domain.FreshnessContext` (`identity.go:L158-L165`).<br><br>**(B) Verification Path:** `verifier.go:L110-L135`.<br><br>**(C) Dual-Horizon:** §16.16.4B architecture design. | **(A)** No signed CRL or OCSP-equivalent signed preimage found in examined scope.<br><br>**(B)** Status evaluated locally; signed status attestation over revoked key set is unevidenced.<br><br>**(C)** Approved Dual-Horizon evaluation rules for Albums. | **(A)** No signed revocation verifier.<br><br>**(B)** Evaluates `FreshnessContext` enum.<br><br>**(C)** Post-authorization Album evaluator. | Registry authority. | Database row update or in-memory freshness context. | Pinned DB registry row. | **(A) NOT FOUND IN EXAMINED SCOPE** for signed revocation proof.<br><br>**(B) NOT VERIFIED FROM A1** for signed payload verification path.<br><br>**(C) NOT APPLICABLE TO PLANNING FEASIBILITY** for future Album Dual-Horizon evaluator. | `internal/domain/identity.go:L158-L165`, `internal/engine/identity/verifier.go:L110-L135`, `migrations/003_registry_identity.sql:L1-L30` | `NOT FOUND IN EXAMINED SCOPE` (for signed proof); `NOT APPLICABLE` (for Album evaluator) | **NOT FOUND IN EXAMINED SCOPE (NATIVE PROOF); NOT APPLICABLE (ALBUM EVALUATOR)**. Database columns and freshness enums exist, but signed revocation proof covering revoked key sets is absent from examined scope. The Album Dual-Horizon evaluator is future WP-04 implementation. |
| **6. Tier-2 issuer / delegation evidence** | `DelegationAssertion` (`internal/domain/identity.go:L125-L144`), `AllowedDelegationScopes` (`internal/domain/ownership.go:L100-L106`). | Canonical JCS over `DelegationAssertion` struct (`delegator_subject_id`, `delegate_public_key`, `scope`, `sequence`, `expires_at`). | `internal/engine/identity/verifier.go:L180-L210` (`VerifyDelegation`). | Delegator binds delegate key to specific scope string. Issuer key lineage supported for Organization delegators. | Monotonic `sequence`, `expires_at`. Revocation of delegation is `NOT VERIFIED FROM A1`. Delegation depth and subdelegation constraints are `NOT VERIFIED FROM A1`. | Terminates at delegator's active key. | **COMPATIBLE IN STRUCTURE; SCOPE ABSENT**. The `DelegationAssertion` structure can support Tier-2 delegation, but `ALBUM_MEMBERSHIP_SIGNING` scope is not registered. | `internal/domain/identity.go:L125-L144, L207-L210`, `internal/domain/ownership.go:L100-L106`, `internal/engine/identity/verifier.go:L180-L210` | `PARTIAL / NOT VERIFIED FROM A1` (for depth & revocation) | **NATIVE PREDICATES NOT VERIFIED; ALBUM-SPECIFIC SCOPE REGISTRATION IS FUTURE WORK.** A native JCS `DelegationAssertion` representation and verifier are evidenced. However, the evidence does not establish delegation depth, subdelegation enforcement, or delegation revocation semantics; those native predicates remain `NOT VERIFIED`. The absence of `ALBUM_MEMBERSHIP_SIGNING` from the current allowed-scope list is a separate Album-specific scope-registration task for WP-04 and is `NOT APPLICABLE TO PLANNING FEASIBILITY`. The current structure's existence alone is not sufficient to declare full Tier-2 compatibility. |

---

## 6. BOUNDED CLARIFICATION LOG (§16.21.10.5)

In strict accordance with §16.21.10.5, only three read-only clarifications were performed on exact existing interfaces identified in A1:

### Clarification 1: Storage Engine Candidate Interface
- **Exact Path & Line Range:** `/opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go#L29-L260`
- **Necessity:** Test candidate Storage Engine against §16.8.1 (object creation, read-by-ID, conditional create/update, immutability, concurrency, durability, recovery).
- **Inspected Material:**
  - `ObjectMeta` struct (`L29-L37`): fields `storage_object_id`, `package_sha256`, `state`, `physical_object_key`, `size_bytes`, `created_at`, `verified_at`.
  - Methods: `StorePackageStream` (`L164-L230`), `GetMeta` (`L233-L254`), `GetVerifiedFileStream` (`L256-L260`), `ClaimNonce` (`L88-L130`).
- **Result & Observation:**
  - `StorePackageStream` writes a payload to a staging path, computes/verifies its SHA-256, then renames it to `verified/<package_sha256>.nx` and writes sidecar JSON under `meta/<storage_object_id>.json`.
  - Concurrency: `ClaimNonce` uses `O_CREAT|O_EXCL` for nonce-file creation (`L110`). `StorePackageStream` uses `O_CREAT|O_EXCL` for staging temporary-file creation (`L176`). These excerpts establish exclusive creation at those paths only; they do not establish general object immutability, conditional update semantics, or concurrency control across related records.
  - Immutability: A hash-derived filename identifies the promoted payload by its content hash. The cited naming and write sequence alone do not prove that an existing verified object cannot later be replaced or deleted.
  - **Limitation:** The inspected interface is an object store for opaque binary payloads (`.nx`) with sidecar metadata. The cited methods do not establish relational querying, a composite transaction boundary across multiple records, or parent-child Album member indexing. It therefore does not, on this evidence, provide the checkout-receipt correlation required by PE-02 under Zero-DDL.

### Clarification 2: License Daemon Operation Status Contract
- **Exact Path & Line Range:** `/opt/antigravity/projects/nexa/marketplace/server.js#L210-L305` & `#L3794-L3870`
- **Necessity:** Determine if existing Marketplace client provides status/receipt query to distinguish UNKNOWN/PENDING outcomes from definitive failures (§16.21.10.5 item 2).
- **Inspected Material:**
  - Functions: `invokeSprint12LicensingAuthority` calls `/api/v1/licensing/prepare` (`L248`), `/sign` (`L277`), and `/submit` (`L303`).
  - Timeout handling: `setTimeout(..., 2500)` (`L212, L223`).
  - Error throwing: Throws raw `Error` with message string on non-200 responses.
- **Result & Observation:**
  - **No status lookup endpoint exists.** There is no `GET /api/v1/licensing/:operation_id` or `/status` call in `server.js`.
  - On network timeout or HTTP 5xx during `/submit`, the local PostgreSQL transaction rolls back (`store.js:L68`), but the License Daemon request may have committed remotely.
  - The client treats any failure as a terminal exception; it cannot query whether the grant is PENDING or ALREADY_ISSUED.

### Clarification 3: Individual Creator vs Organization Native Key Lineage
- **Exact Path & Line Range:** `/opt/antigravity/projects/nexa/internal/domain/identity.go#L30-L55` & `sdk/typescript/src/ownership.ts#L26-L55`
- **Necessity:** Resolve internal ambiguity between Organization URN lineage and Individual Creator hex binding (§16.21.10.5 item 3).
- **Inspected Material:**
  - `internal/domain/identity.go:L30`: `SubjectTypeIndividual = "INDIVIDUAL"`.
  - `sdk/typescript/src/ownership.ts:L30-L45`: Genesis certificate binds raw hex string `creator_public_key` directly to `asset_id`.
- **Result & Observation:**
  - Organization creators have a full URN derivation (`urn:nexa:id:<sha256>`), monotonic root recovery assertions, and active key authorization lineages in Go.
  - Individual creators have **no URN derivation and no key rotation lineage**. The key is static and tied directly to the individual Genesis certificate.

---

## 7. UNRESOLVED ITEMS AND EXACT REASON

In compliance with §16.21.10.7 item 7 and §3.1 of the corrective handoff, the following table details every unresolved planning item using strictly authorized classification statuses:

| Item ID | Area | Unresolved Predicate | Exact Authorized Classification | Detailed Reason & Missing Evidence Locator |
|---|---|---|---|---|
| **UNRES-01** | B-04 / Persistence | Durable Checkout Manifest SSOT under Zero-DDL | `NOT FOUND IN EXAMINED SCOPE` | A1 examined Marketplace DDL (`schema.postgres.sql`) and Storage Engine (`storage_engine.go`). No database table or structured storage mechanism was found to store `bundle_checkout_id`, member list, and commercial intent without schema migration. Missing: Zero-DDL storage adapter for composite objects. |
| **UNRES-02** | B-04 / Persistence | Per-member execution receipt & separate execution key | `NOT FOUND IN EXAMINED SCOPE` | A1 examined PostgreSQL schema and found strictly 1:1 single-acquisition schema (`acquisitions` $\leftrightarrow$ `payment_orders`). No sub-receipt or execution key column exists under Zero-DDL in examined scope. |
| **UNRES-03** | B-04 / Transaction | License Daemon PENDING status query & reconciliation | `NOT FOUND IN EXAMINED SCOPE` | A1 examined `marketplace/server.js:L210-L305`. No status/receipt query endpoint to external License Daemon was found. Protocol only supports forward push (`/submit`). |
| **UNRES-04** | B-05 / Storage | Child `.nx` `member_sha256` durable mapping | `NOT FOUND IN EXAMINED SCOPE` | A1 examined active DDL and found no column for child member hash. `acquired_package_sha256` is strictly the wrapper ZIP hash. Missing: Durable location for child hash under Zero-DDL. |
| **UNRES-05** | NC-06 / Persistence | Stable Album ID & ordered member relation in Studio | `NOT FOUND IN EXAMINED SCOPE` | A1 examined `studio-desktop/main.js` and found no data model, project file, or publication path for multi-member Albums. |
| **UNRES-06** | B-09 / Native Proof | Album-wide rights/authority basis carrier | `NOT APPLICABLE TO PLANNING FEASIBILITY` (POST-AUTHORIZATION ALBUM CAPABILITY) | Existing `OwnershipCertificate` evidence binds one `asset_id` and does not itself prove Album-wide authority. The Album-wide Authority Designation carrier is a new PE-02 capability assigned to WP-04 under the approved architecture. Its absence from current source is expected and is not a pre-coding blocker. |
| **UNRES-07** | B-09 / Native Proof | Album-specific `ALBUM_MEMBERSHIP_SIGNING` scope registration | `NOT APPLICABLE TO PLANNING FEASIBILITY` (POST-AUTHORIZATION ALBUM CAPABILITY) | Registration and recognition of this new Album-specific scope belong to WP-04 after authorization. This classification applies only to the future scope registration; it does not close the separate native delegation-depth, subdelegation, or revocation predicates, which remain `NOT VERIFIED` in Matrix B category 6. |
| **UNRES-08** | B-09 / Trust Store | Standalone offline trust anchor termination path | `NOT VERIFIED FROM A1` | Registry verification in SDK and Go relies on online HTTP or pre-seeded database rows. Available A1 evidence does not contain a locally pinned, self-contained offline trust anchor file for independent termination. Universal absence cannot be claimed without repository-wide search. |
| **UNRES-09** | B-07 / Resource | ZIP benchmark numeric resource caps | `NOT APPLICABLE TO PLANNING FEASIBILITY` (POST-AUTHORIZATION ALBUM CAPABILITY) | In accordance with §16.7, §16.14, and §16.21.3, 4-class payload benchmark execution is post-authorization acceptance work under WP-03. Not a pre-coding blocker. |
| **UNRES-10** | NC-13 / Viewer | Normalized `VIEWER_COMPLETED` multi-platform adapters | `NOT APPLICABLE TO PLANNING FEASIBILITY` (POST-AUTHORIZATION ALBUM CAPABILITY) | In accordance with §16.21.5, viewer completion adapters for video, document, image, and mobile are post-authorization acceptance under WP-06. |

---

## 8. SCOPE ATTESTATION

In compliance with §16.21.10.6 and §16.21.10.7 item 8, Lead Programmer hereby formally attests:

1. **No Repeated Search or Audit:** Programmer has not repeated A1, PSV-R10/R10A, or any search scope already closed in §16.18.
2. **No Repository-Wide Sweeps:** Programmer has not executed repository-wide grep sweeps, full test-suite runs, load tests, benchmarks, or runtime experiments.
3. **No Implementation or Mutation:** Programmer has not built, prototyped, implemented, refactored, or modified Album Handling, Album Signer, Membership Authority, Manifest verifier, persistence adapters, or proof adapters.
4. **Zero Source / Schema Change:** Programmer has not modified any source code, SQL, DDL, migrations, endpoints, configurations, secrets, or deployment state.
5. **No Synthetic Artifacts:** Programmer has not created sample credentials, synthetic certificates, generic proof envelopes, new trust anchors, or substitute proof formats.
6. **No Inferred Invariants:** Programmer has not inferred durability, immutability, atomicity, idempotency, or offline trust from names or comments.
7. **Baseline Protection:** Sprint 16 and PE-01 frozen baselines remain completely untouched and preserved 100%.
8. **No Unilateral Decisions:** Programmer has made no product or architecture decisions, and has reported all gaps strictly as `NOT VERIFIED FROM A1`, `NOT FOUND IN EXAMINED SCOPE`, or `NOT APPLICABLE TO PLANNING FEASIBILITY`.

---

## 9. EVIDENCE INDEX

Exact source citations supporting positive claims in this return (Commit: `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):

1. **Marketplace DDL (Flat 1:1 Schema):**
   - **Path:** `marketplace/db/schema.postgres.sql#L63-L75`
     - *Excerpt:* `CREATE TABLE acquisitions ( acquisition_id VARCHAR(128) PRIMARY KEY, asset_id VARCHAR(128) NOT NULL REFERENCES catalog_snapshots(asset_id), ... acquired_package_sha256 VARCHAR(64) ... );`
     - *Establishes:* Schema stores single acquisitions linked to `catalog_snapshots(asset_id)` with `acquired_package_sha256`. No multi-member checkout receipt or parent-child columns exist.
   - **Path:** `marketplace/db/schema.postgres.sql#L107-L114, L131-L135`
     - *Excerpt:* `CREATE TABLE entitlements ( entitlement_id VARCHAR(128) PRIMARY KEY, acquisition_id VARCHAR(128) NOT NULL UNIQUE REFERENCES acquisitions(acquisition_id), ... );`
     - *Establishes:* Enforces a strict 1:1 relationship between `acquisition_id` and `entitlement_id`.

2. **PostgreSQL Local Transaction Wrapper & Call Path:**
   - **Path:** `marketplace/db/store.js#L89-L103`
     - *Excerpt:* `async function withTransaction(callback) { ... await client.query('BEGIN'); ... await client.query('COMMIT'); ... catch(err) { await client.query('ROLLBACK'); ... } }`
     - *Establishes:* Provides local PostgreSQL transaction boundaries. Does not provide 2PC or distributed compensation across external services.
   - **Path:** `marketplace/server.js#L3581-L3602`
     - *Excerpt:* Single transaction writing one row each to `acquisitions`, `payment_orders`, and `payment_proofs`.
     - *Establishes:* Order creation transaction boundary is strictly single-item.
   - **Path:** `marketplace/server.js#L3794-L3870`
     - *Excerpt:* `const licenseKey = await invokeSprint12LicensingAuthority(order.acquisition_id, acqRow.asset_id, acqRow.buyer_id);` inside transaction before `COMMIT`.
     - *Establishes:* License daemon invocation occurs before commit; HTTP failure triggers local DB rollback but external daemon side-effect cannot be compensated.

3. **Delivery Package Spool & Wrapper Hash:**
   - **Path:** `marketplace/server.js#L762-L770`
     - *Excerpt:* `async function computeFileSha256(filePath) { const stream = fs.createReadStream(filePath); ... }`
     - *Establishes:* Calculates SHA-256 over entire file stream from byte 0 to EOF.
   - **Path:** `marketplace/server.js#L2231`
     - *Excerpt:* `packageSha256 = await computeFileSha256(session.spool_path);`
     - *Establishes:* Hash byte-domain is strictly the creator-uploaded package spool file (wrapper ZIP).
   - **Path:** `marketplace/server.js#L4271, L4309, L4366, L4458`
     - *Establishes:* Authorizes download of package payload matching package SHA-256.

4. **Candidate Storage Engine:**
   - **Path:** `storage/internal/store/storage_engine.go#L29-L37`
     - *Excerpt:* `type ObjectMeta struct { StorageObjectID string; PackageSHA256 string; State string; PhysicalObjectKey string; SizeBytes int64; ... }`
     - *Establishes:* Metadata structure stores flat binary package attributes; lacks relational or multi-member fields.
   - **Path:** `storage/internal/store/storage_engine.go#L88-L130`
     - *Excerpt:* `ClaimNonce(nonce string, timestamp int64)` with `O_CREAT|O_EXCL` on `nonces/<nonceHex>.json`.
     - *Establishes:* Replay prevention and concurrency primitive for nonces within a 300s window.
   - **Path:** `storage/internal/store/storage_engine.go#L164-L230`
     - *Excerpt:* `StorePackageStream(reader io.Reader, expectedSHA256 string)` writes to `staging/`, verifies hash, and moves to `verified/<package_sha256>.nx`.
     - *Establishes:* The method writes a staging payload, verifies its hash, renames it to a hash-derived verified path, and produces sidecar JSON in `meta/`. This excerpt alone does not establish filesystem atomicity guarantees or immutability against later replacement/deletion.

5. **Organization Identity Lineage & Verifier (Sprint 14):**
   - **Path:** `internal/domain/identity.go#L62-L114`
     - *Excerpt:* Struct definitions for `IdentityAssertion`, `RootRecoveryAssertion`, and `ActiveKeyAuthorizationAssertion`.
     - *Establishes:* Native Go data representations for Organization root recovery and active key lineage.
   - **Path:** `internal/engine/identity/subject.go#L13-L56`
     - *Excerpt:* `func DeriveSubjectID(rawGenesisEd25519PubKeyBytes []byte) (string, error)` producing `"urn:nexa:id:" + hexHash`.
     - *Establishes:* Deterministic, immutable URN derivation for Organization identities.
   - **Path:** `internal/engine/identity/lineage.go#L16-L154`
     - *Excerpt:* `Verify2StepRootRecovery` and `ResolveRootAuthorityAt(rootGenesisPubKeyDigest, timestamp)`.
     - *Establishes:* 2-step root recovery and active key resolution at a specific timestamp for Organization roots.
   - **Path:** `tests/identity/lineage_test.go#L218`
     - *Establishes:* Test `TestVerify2StepRootRecovery` passes (exit code 0).

6. **Delegation Assertion Primitives:**
   - **Path:** `internal/domain/identity.go#L125-L144`
     - *Excerpt:* `type DelegationAssertion struct { DelegatorSubjectID string; DelegatePublicKey string; Scope string; Sequence int64; ExpiresAt int64; ... }`
     - *Establishes:* Native JCS assertion struct for delegation.
   - **Path:** `internal/domain/ownership.go#L100-L106`
     - *Excerpt:* `AllowedDelegationScopes = []string{ "METADATA_UPDATE_CLAIM", "OWNERSHIP_EVIDENCE_SUBMISSION", "OWNERSHIP_HISTORY_ADMINISTRATION" }`
     - *Establishes:* Existing allowed scopes in Go. `ALBUM_MEMBERSHIP_SIGNING` is not in this slice.
   - **Path:** `internal/engine/identity/verifier.go#L180-L210`
     - *Excerpt:* `VerifyDelegation(assertion, delegatorPubKey)`
     - *Establishes:* Verifies Ed25519 signature over canonical JCS delegation payload.

7. **Genesis Ownership Certificate Verification:**
   - **Path:** `sdk/typescript/src/sdk.ts#L205-L260`
     - *Excerpt:* Verification of 8-field canonical Genesis string (`asset_id`, `creator_public_key`, `effective_at`, `issued_at`, `issuer_id`, `previous_cert_ref`, `subject_id`, `underlying_cert_id`) with `creator_public_key`.
     - *Establishes:* Serialized 8-field Genesis certificate representation and client verification.
   - **Path:** `sdk/typescript/src/ownership.ts#L26-L55`
     - *Establishes:* Individual Creator identity binds raw hex string `creator_public_key` directly to asset.

8. **NX Studio Single-Asset Pipeline:**
   - **Path:** `studio-desktop/main.js#L682-L870, L1097-L1240`
     - *Establishes:* Studio desktop IPC handlers `forge-asset` and `publish-asset` operate strictly on single `.nx` files.
