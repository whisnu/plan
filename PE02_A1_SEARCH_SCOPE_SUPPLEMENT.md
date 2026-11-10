# NEXA PE-02 A1 — SEARCH SCOPE & METHODOLOGY SUPPLEMENT

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

### Group B: Individual Creator Key Rotation and Succession
- **Search Goal:** Identify whether `SubjectTypeIndividual` has any separate logic, rotation mechanism, or dedicated tests.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "SubjectTypeIndividual" internal pkg tests
  grep -rn --exclude-dir=.git -E "IndividualRotation|IndividualLineage|IndividualKey" internal pkg tests
  ```
- **Results:**
  - `SubjectTypeIndividual` appears only at its declaration (`internal/domain/identity.go:L30`) and in an enum validation check (`internal/engine/identity/verifier.go:L77`).
  - Exactly **0 tests** in `tests/identity/` or `tests/audit/sprint14/` pass `SubjectTypeIndividual`.
  - Zero functions exist for individual rotation.
- **Conclusion:** **`NOT FOUND`**. Individual Creator key rotation does not exist in Nexa; the identity engine only implements Organization Level-1 key authorization.

### Group C: Album-wide Ownership & Publisher-Origin Authority
- **Search Goal:** Search for multi-asset ownership certificates, compilation rights, or album publisher authority.
- **Commands Executed:**
  ```bash
  grep -RIn --exclude-dir=.git -i "album" internal pkg
  grep -rn --exclude-dir=.git -E "AlbumOwnership|PublisherOrigin|MultiAssetOwnership" internal pkg apps
  ```
- **Results:**
  - `grep -RIn --exclude-dir=.git -i "album" internal pkg`: Exit code `1` (**0 matches across entire Go codebase**).
  - All ownership types in `internal/domain/ownership.go` take scalar `AssetID string`.
- **Conclusion:** **`NOT FOUND IN EXAMINED SCOPE`**. Multi-asset / Album-wide ownership mechanisms do not exist in native Nexa code.

### Group D: Offline Registry Attestations
- **Search Goal:** Determine if Registries can emit static offline attestations or if `Evaluator` can verify registry claims without HTTP calls.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git -E "OfflineRegistry|RegistryAttestation|RegistryProof" internal pkg
  grep -rn --exclude-dir=.git "queryRegistry" internal pkg
  ```
- **Results:**
  - `queryRegistry` is exclusively an HTTP query function using `http.Client.Do` (`internal/engine/federation/evaluator.go:L192-L300`).
  - If `len(cfg.Registries) == 0`, `Evaluator.Evaluate` returns `TrustResult: UNKNOWN` and `EvidenceCompleteness: NONE`.
- **Conclusion:** **`NOT FOUND`**. There is no offline Registry proof verification support.

### Group E: Revocation Verification and Dual-Horizon Time Rule
- **Search Goal:** Find verification logic for `RegistryKeyRevocationList` and any comparison between `revoked_at` and `recorded_at`.
- **Commands Executed:**
  ```bash
  grep -rn --exclude-dir=.git "ListSignature" internal pkg apps
  grep -rn --exclude-dir=.git "revoked_at" internal pkg apps
  grep -rn --exclude-dir=.git "recorded_at" internal pkg apps
  ```
- **Results:**
  - `ListSignature` appears only in `internal/domain/registry_identity.go:L28` and `internal/service/service.go:L85`. No function ever verifies it.
  - `revoked_at` appears only in `service.go:L306` inside an audit log map (`"revoked_at": now`).
  - `recorded_at` appears only as an event store column in `OwnershipEvent`.
  - Zero functions compare `revoked_at` against `recorded_at`.
- **Conclusion:** **`NOT FOUND`**. Standalone revocation assertion verifiers and Dual-Horizon verifier logic are entirely absent from executable code.

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
