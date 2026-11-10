# NEXA PE-02 A1 — SEARCH SCOPE & METHODOLOGY SUPPLEMENT (RECONCILED & BOUNDED)

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Source Revision:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (reported in Programmer evidence; not independently verified by AA)
- **Search Tooling:** GNU grep / ripgrep, Go AST inspection, Git commit inspection
- **Root Path:** `/opt/antigravity/projects/nexa`

---

## 1. REPRODUCIBLE SEARCH METHODOLOGY BY WORKSTREAM (GROUPS A–F)

### Group A: Genesis Root Public Key Trust-Anchor Store
- **Search Goal:** Locate any persistent store, configuration file, database table, or in-memory map storing trusted Genesis Root Public Keys for the identity engine.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git -E "TrustAnchor|TrustStore|RootKeyStore|PinnedGenesis|GenesisTrust" internal pkg
  grep -rn --exclude-dir=.git "NewIdentityVerifier" internal pkg apps tests
  ```
- **Results:**
  - `NewIdentityVerifier` is only referenced in `internal/engine/identity/verifier.go:L18`, `pkg/nexa/identity.go:L27`, and `tests/identity/verifier_test.go:L125`.
  - Zero results for any trust-anchor store structs or functions.
- **Conclusion:** **`NOT FOUND IN EXAMINED SCOPE`**. Within the examined scope, the verifier is stateless and does not check Genesis Root Keys against an independent trusted anchor store.

### Group B: Individual Creator Key Rotation and Active Key Resolution
- **Search Goal:** Identify whether `SubjectTypeIndividual` has separate logic, rotation mechanism, or dedicated tests, and whether `ResolveActiveSigningAuthorityAt` restricts by subject type.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "SubjectTypeIndividual" internal pkg tests
  grep -rn --exclude-dir=.git "ResolveActiveSigningAuthorityAt" internal pkg tests
  grep -rn --exclude-dir=.git -E "IndividualRotation|IndividualLineage|IndividualKey" internal pkg tests
  ```
- **Results:**
  - `ResolveActiveSigningAuthorityAt` does not accept `subject_type` and does not branch on subject type (`internal/engine/identity/active_key.go:L93-L154`).
  - `ActiveKeyAuthorizationAssertion` has no `subject_type` field and binds to any `SubjectID` URN (`internal/domain/identity.go:L99-L114`).
  - `IdentityVerifier.ExecutePipeline` invokes the active key resolver identically for both `ORGANIZATION` and `INDIVIDUAL` (`internal/engine/identity/verifier.go:L77-L81, L156`).
  - In tests that instantiate and verify complete `IdentityAssertion` pipelines (such as `TestVerificationPipelineVerified`), test fixtures explicitly specify `SubjectTypeOrganization`.
  - Primitives and algorithmic tests (JCS RFC 8785, Ed25519 vectors, SHA-256 Subject ID derivation) do not specify or evaluate subject types (they are subject-agnostic).
  - Exactly **0 tests** in `tests/identity/` or `tests/audit/sprint14/` execute end-to-end assertion verification with `SubjectTypeIndividual`.
- **Bounded Conclusion:**
  - The source code resolver does not accept or evaluate `subject_type`.
  - The identity verification pipeline invokes the resolver for both subject types without structural restriction.
  - Dedicated end-to-end Individual Creator pipeline tests are absent from the examined test suite.
  - This finding neither proves end-to-end success for Individual Creators nor indicates that Individual Creators are blocked or rejected by the resolver.

### Group C: Album-wide Ownership & Publisher-Origin Authority
- **Search Goal:** Search for multi-asset ownership certificates, compilation rights, or album publisher authority across documented code directories.
- **Examined Code Directories:**
  1. `cmd/` (CLI tools and daemons)
  2. `internal/` (Core engine, domain, service, and infrastructure packages)
  3. `pkg/` (Public Go API packages)
  4. `marketplace/` (Marketplace backend and frontend services)
  5. `studio-desktop/` (Nexa Studio authoring app)
  6. `player-desktop/` (Nexa Player Electron desktop app)
  7. `verify-desktop/` (Nexa Verify Desktop app)
  8. `mobile/` (React Native mobile apps and packages)
  9. `storage/` (Storage engine and daemons)
  10. `sdk/` (C, .NET, Java, Python, TypeScript SDKs)
  11. `migrations/` (Database migration scripts)
- **Commands Executed:**
  ```bash
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules --exclude-dir=vendor --exclude-dir=evidence --exclude-dir=docs --exclude-dir=scratch -i -E "album|collection|multi.?asset|asset.?list|asset_ids|member_ids" cmd internal pkg marketplace studio-desktop player-desktop verify-desktop mobile storage sdk migrations
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules -E "type Ownership[A-Za-z]+ struct" .
  ```
- **Results:**
  - `collection` matched only standard library references (C# `System.Collections.Generic`, JS `which-collection`, open-source license texts).
  - All ownership structures (`OwnershipCertificate`, `OwnershipTransfer`, `OwnershipDelegation`, `OwnershipEvent`) reside strictly in `internal/domain/ownership.go` and `pkg/nexa/ownership.go`, and require scalar `AssetID string`.
  - Zero structures, interfaces, schemas, or API endpoints exist for Album-wide ownership or publisher-origin authority within the examined code directories.
- **Bounded Conclusion:**
  **`NOT FOUND IN EXAMINED CODE DIRECTORIES`** (examined: `cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/` at reported source revision `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`).
  *Scope boundary:* This finding is strictly bounded to the 11 examined code directories and does not prove repository-wide absence across unexamined paths (e.g. `tests/`, `docs/`, `evidence/`, `scratch/`) or non-Go structural definitions.

### Group D: Offline Registry Attestations & `SupportedFeatures` Preimage
- **Search Goal:** Determine if `SupportedFeatures` is bound by `RegistryIdentity.IdentitySignature` and if Registries emit offline attestations.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "SupportedFeatures" internal pkg sdk
  grep -rn --exclude-dir=.git "CanonicalJCS" internal/domain/
  grep -rn --exclude-dir=.git "queryRegistry" internal pkg
  ```
- **Results:**
  - `CanonicalJCS()` in `internal/domain/registry_identity.go:L32-L37` strictly excludes `SupportedFeatures`.
  - `queryRegistry` is exclusively an HTTP query function using `http.Client.Do` (`internal/engine/federation/evaluator.go:L192-L300`).
  - If `len(cfg.Registries) == 0`, `Evaluator.Evaluate` returns `TrustResult: UNKNOWN` and `EvidenceCompleteness: NONE`.
- **Bounded Conclusion:**
  - `SupportedFeatures` is **strictly excluded** from `CanonicalJCS()` and is NOT cryptographically bound by `IdentitySignature` (`EXCLUDED`).
  - Offline Registry proof verification is **`NOT FOUND IN EXAMINED SCOPE`**.

### Group E: Revocation Verification, `RevokedKeys` Preimage & Dual-Horizon Time Rule
- **Search Goal:** Find verification logic for `RegistryKeyRevocationList`, analyze signature preimage for `RevokedKeys`, inspect signing and public keys, and check for `revoked_at` vs `recorded_at` evaluation.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "ListSignature" internal pkg apps
  grep -rn --exclude-dir=.git "RevokedKeys" internal pkg
  grep -rn --exclude-dir=.git "IssuerPrivateKey" internal/
  grep -rn --exclude-dir=.git "IssuerPublicKey" internal/
  grep -rn --exclude-dir=.git "revoked_at" internal pkg apps
  grep -rn --exclude-dir=.git "recorded_at" internal pkg apps
  ```
- **Results:**
  - `ListSignature` is signed in `service.go:L85` with `s.cfg.IssuerPrivateKey`, loaded from `ISSUER_PRIVATE_KEY_HEX` in `internal/config/config.go:L140-L158`.
  - The configuration also defines `s.cfg.IssuerPublicKey`, loaded from `ISSUER_PUBLIC_KEY_HEX`.
  - The signed preimage `canonStr` in `service.go:L83` signs ONLY `registry_id` and `updated_at`:
    ```go
    canonStr := fmt.Sprintf(`{"registry_id":"%s","updated_at":"%s"}`, crl.RegistryID, crl.UpdatedAt.Format("2006-01-02T15:04:05.000000000Z"))
    ```
    Field `RevokedKeys` is completely omitted from the preimage.
  - How verifiers obtain, distribute, or trust `IssuerPublicKey`, who owns the key beyond the local node configuration, and whether verifiers evaluate CRL signatures are **`NOT VERIFIED FROM AVAILABLE EVIDENCE`**.
  - Functions verifying `ListSignature` are **`NOT FOUND IN EXAMINED SEARCH SCOPE`** (searched across `internal/`, `pkg/`, `apps/`).
  - No alternative authentication mechanism was found in the examined scope.
  - `revoked_at` appears only as an audit log metadata field (`service.go:L306`); `recorded_at` appears only as an event store column. No verifier logic compares them.
- **Bounded Conclusion:**
  - `RevokedKeys` is **NOT bound** by `ListSignature` (`EXCLUDED`).
  - Key authority, trust relationship, and distribution of `IssuerPublicKey` are **`NOT VERIFIED FROM AVAILABLE EVIDENCE`**.
  - Verifier functions for CRL signatures and Dual-Horizon evaluation logic are **`NOT FOUND IN EXAMINED SEARCH SCOPE`**.

### Group F: Capability `ALBUM_MEMBERSHIP_SIGNING` and Album ID Binding
- **Search Goal:** Find definition or usage of `ALBUM_MEMBERSHIP_SIGNING` and any field binding `DelegationAssertion` to `album_id`.
- **Commands Executed:**
  ```bash
  grep -rnw --exclude-dir=.git "ALBUM_MEMBERSHIP_SIGNING" internal pkg apps tests
  grep -rn --exclude-dir=.git "album_id" internal/domain/identity.go internal/engine/identity/
  ```
- **Results:**
  - Exactly **0 matches** for `ALBUM_MEMBERSHIP_SIGNING` across the examined code paths.
  - Exactly **0 matches** for `album_id` in `internal/domain/identity.go` or `internal/engine/identity/`.
- **Conclusion:** **`NOT FOUND IN EXAMINED SEARCH SCOPE`**.

---

## 2. BOUNDS AND LIMITATIONS OF SEARCH

1. **Explicitly Bounded Scope:** The negative findings documented in this report are strictly limited to the examined code directories (`cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`) and specific search queries.
2. **Reported Source Revision:** All inspections were performed against local source tree at reported revision `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`. This revision represents the baseline reported in Programmer evidence and has not been independently verified by AA.
3. **Unexamined Scope Boundary:** The searches conducted did not encompass exhaustive examination of `tests/`, `docs/`, `evidence/`, `scratch/`, or serialization schemas defined outside Go structs. Therefore, findings are strictly framed as `NOT FOUND IN EXAMINED CODE DIRECTORIES` or `NOT FOUND IN EXAMINED SEARCH SCOPE`.
4. **Architectural Interpretation:** The absence of Album-wide ownership, CRL verifiers, or Album Membership Authority in the examined code reflects unimplemented new capabilities for PE-02, not a defect in existing single-asset Sprint 14/16 architecture.
