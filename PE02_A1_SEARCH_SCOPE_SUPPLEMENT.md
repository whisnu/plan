# NEXA PE-02 A1 — SEARCH SCOPE & METHODOLOGY SUPPLEMENT (CORRECTED)

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Commit SHA:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
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
- **Conclusion:** **`NOT FOUND`**. The verifier is entirely stateless and does not check Genesis Root Keys against any trusted anchor list.

### Group B: Individual Creator Key Rotation and Active Key Resolution
- **Search Goal:** Identify whether `SubjectTypeIndividual` has any separate logic, rotation mechanism, or dedicated tests, and whether `ResolveActiveSigningAuthorityAt` restricts by subject type.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "SubjectTypeIndividual" internal pkg tests
  grep -rn --exclude-dir=.git "ResolveActiveSigningAuthorityAt" internal pkg tests
  grep -rn --exclude-dir=.git -E "IndividualRotation|IndividualLineage|IndividualKey" internal pkg tests
  ```
- **Results:**
  - `ResolveActiveSigningAuthorityAt` does not accept `subject_type` and does not branch on subject type (`internal/engine/identity/active_key.go:L93-L154`).
  - `ActiveKeyAuthorizationAssertion` has no `subject_type` field and binds to any `SubjectID` URN (`internal/domain/identity.go:L99-L114`).
  - `SubjectTypeIndividual` appears only at its declaration (`internal/domain/identity.go:L30`) and in an enum validation check (`internal/engine/identity/verifier.go:L77`).
  - Exactly **0 tests** in `tests/identity/` or `tests/audit/sprint14/` pass `SubjectTypeIndividual`.
- **Conclusion:** **Source code supports a generic active-key resolver for both Individual and Organization subject types; there is no source-level barrier prohibiting Individual Creator active key authorization. However, test evidence demonstrating assertion issuance specifically for Individual Creators is currently absent from the test suite.**

### Group C: Album-wide Ownership & Publisher-Origin Authority
- **Search Goal:** Search for multi-asset ownership certificates, compilation rights, or album publisher authority across all code directories.
- **Examined Directories in Initial Pass:** `internal/`, `pkg/`.
- **Additional Directories Examined in Supplement Pass:**
  - `cmd/` (CLI tools and daemons)
  - `marketplace/` (Marketplace backend and frontend services)
  - `studio-desktop/` (Nexa Studio authoring app)
  - `player-desktop/` (Nexa Player Electron desktop app)
  - `verify-desktop/` (Nexa Verify Desktop app)
  - `mobile/` (React Native mobile apps and packages)
  - `storage/` (Storage engine and daemons)
  - `sdk/` (C, .NET, Java, Python, TypeScript SDKs)
  - `migrations/` (Database migration scripts)
- **Commands Executed:**
  ```bash
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules --exclude-dir=vendor --exclude-dir=evidence --exclude-dir=docs --exclude-dir=scratch -i -E "album|collection|multi.?asset|asset.?list|asset_ids|member_ids" cmd internal pkg marketplace studio-desktop player-desktop verify-desktop mobile storage sdk migrations
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules -E "type Ownership[A-Za-z]+ struct" .
  ```
- **Results:**
  - `collection` matched only standard library references (C# `System.Collections.Generic`, JS `which-collection`, open-source license texts).
  - All ownership structures (`OwnershipCertificate`, `OwnershipTransfer`, `OwnershipDelegation`, `OwnershipEvent`) reside strictly in `internal/domain/ownership.go` and `pkg/nexa/ownership.go`, and require scalar `AssetID string`.
  - Zero structures, interfaces, schemas, or API endpoints exist for Album-wide ownership or publisher-origin authority.
- **Conclusion:** **`NOT FOUND IN REPOSITORY AT REVISION fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` across all relevant product code directories.**

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
- **Conclusion:** **`SupportedFeatures` is NOT bound by `IdentitySignature` (`EXCLUDED`). Offline Registry proof verification is `NOT FOUND`.**

### Group E: Revocation Verification, `RevokedKeys` Preimage & Dual-Horizon Time Rule
- **Search Goal:** Find verification logic for `RegistryKeyRevocationList`, analyze signature preimage for `RevokedKeys`, and check for `revoked_at` vs `recorded_at` evaluation.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "ListSignature" internal pkg apps
  grep -rn --exclude-dir=.git "RevokedKeys" internal pkg
  grep -rn --exclude-dir=.git "IssuerPrivateKey" internal/
  grep -rn --exclude-dir=.git "revoked_at" internal pkg apps
  grep -rn --exclude-dir=.git "recorded_at" internal pkg apps
  ```
- **Results:**
  - `ListSignature` is signed in `service.go:L85` with `s.cfg.IssuerPrivateKey` (local registry node private key).
  - Signed preimage `canonStr` in `service.go:L83` signs ONLY `registry_id` and `updated_at`. Field `RevokedKeys` is completely omitted from the preimage.
  - Zero functions in the codebase verify `ListSignature`.
  - `revoked_at` appears only as an audit log metadata field (`service.go:L306`); `recorded_at` appears only as an event store column. No verifier logic compares them.
- **Conclusion:** **`RevokedKeys` is NOT bound by `ListSignature` (`EXCLUDED`). Verifier functions for CRL and Dual-Horizon evaluation logic are `NOT FOUND IN EXAMINED SCOPE`.**

### Group F: Capability `ALBUM_MEMBERSHIP_SIGNING` and Album ID Binding
- **Search Goal:** Find definition or usage of `ALBUM_MEMBERSHIP_SIGNING` and any field binding `DelegationAssertion` to `album_id`.
- **Commands Executed:**
  ```bash
  grep -rnw --exclude-dir=.git "ALBUM_MEMBERSHIP_SIGNING" .
  grep -rn --exclude-dir=.git "album_id" internal/domain/identity.go internal/engine/identity/
  ```
- **Results:**
  - Exactly **0 matches** for `ALBUM_MEMBERSHIP_SIGNING` in the entire repository.
  - Exactly **0 matches** for `album_id` in `internal/domain/identity.go` or `internal/engine/identity/`.
- **Conclusion:** **`NOT FOUND IN EXAMINED SCOPE`**. The capability and scoping fields do not exist.

---

## 2. BOUNDS AND LIMITATIONS OF SEARCH

1. **Repository Exhaustiveness:** The search commands encompassed all tracked and untracked code within the workspace `/opt/antigravity/projects/nexa` at commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`.
2. **Third-Party / External Dependencies:** No external closed-source libraries were consulted; all Nexa core packages were inspected from local source.
3. **Firm Negative Conclusions:** The `NOT FOUND` determinations are absolute for the codebase at commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`.
