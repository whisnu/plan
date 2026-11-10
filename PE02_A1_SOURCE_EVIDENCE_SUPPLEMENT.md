# NEXA PE-02 A1 — TARGETED SOURCE-EVIDENCE SUPPLEMENT
## ARCHITECTURAL FACTUAL EVIDENCE DOSSIER (RECONCILED & BOUNDED)

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Source Revision:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (reported in Programmer evidence; not independently verified by AA)
- **Working Tree Classification:** `DIRTY — UNTRACKED FILES`
  - Tracked files modified: **NONE** (`git diff` is empty)
  - Untracked files present:
    - `docs/roadmaps/Nexa_Development_Roadmap_v4_8.md`
    - `docs/whitepapers/Nexa_White_Paper_v5_6.md`
- **Inspection Date:** 2026-11-10
- **Task Nature:** Read-Only Source-Evidence Verification & Documentation Correction (Zero Code/Schema/Config Changes)
- **Reference Plan:** `whisnu/plan` -> `main` -> `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (§16.16.4A, §16.16.4B)

---

## 1. REVISION & WORKING-TREE STATUS CLARIFICATION

- **Working-Tree Classification:** `DIRTY — UNTRACKED FILES`.
- **Justification:** `git status --porcelain` returns two untracked documentation files (`docs/roadmaps/Nexa_Development_Roadmap_v4_8.md` and `docs/whitepapers/Nexa_White_Paper_v5_6.md`). There are zero modified tracked files (`git diff --stat` is empty).
- **Commit Lineage:** The commit inspected in this supplement is `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (reported HEAD of `main` in Programmer evidence). All line numbers and source citations correspond to this revision.

---

## 2. EXECUTIVE SUMMARY OF SUPPLEMENTAL FINDINGS

| Group | Topic | Status | Evidence IDs | Core Supplemental Finding |
| :--- | :--- | :--- | :--- | :--- |
| **A** | Genesis Root Certificate & Creator Genesis Identity | `PARTIAL` | `A-SUP-01`, `A-SUP-02` | `IdentityAssertion` verifies JCS Ed25519 signature against `ActivePublicKey`; however, `GenesisRootKey` is ingested purely as untrusted caller data from the assertion itself. There is **zero trust-anchor store, zero pinned root certificate store, and zero trust-anchor lookup** in the identity engine within examined scope. |
| **B** | Individual Creator vs Organization Key Lineage | `PARTIAL` | `B-SUP-01`, `B-SUP-02` | `ResolveActiveSigningAuthorityAt` and `ActiveKeyAuthorizationAssertion` are **structurally generic** and do not evaluate `subject_type`. Pipeline invokes resolver for both subject types without branching. In tested identity pipeline execution (`TestVerificationPipelineVerified`), fixtures explicitly specify Organization; mathematical primitives are subject-agnostic; **zero dedicated end-to-end Individual Creator pipeline tests exist in examined scope**. |
| **C** | Album-wide Ownership vs per-asset Evidence | `NOT FOUND IN EXAMINED CODE DIRECTORIES` | `C-SUP-01`, `C-SUP-02` | `OwnershipCertificate` is strictly bound to scalar `asset_id`. A targeted search across 11 documented code directories (`cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/` at reported revision `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`) confirms zero structures exist for multi-asset aggregation, compilation rights, or publisher-origin authority. Does not prove repository-wide absence across unexamined paths or alternative non-Go schemas. |
| **D** | Registry Authority & Federated Trust | `PARTIAL` | `D-SUP-01`, `D-SUP-02`, `D-SUP-03` | Registry public keys are trusted strictly via caller-injected `RegistryTarget.PublicKey` pinning (`AllowUnpinnedRegistries=false`). Field `SupportedFeatures` is **strictly excluded from `CanonicalJCS()` and signature verification**; `IdentitySignature` does not authenticate `SupportedFeatures`. `Evaluator.Evaluate` relies exclusively on dynamic HTTP network queries; **no offline self-contained cryptographic Registry proof structure exists in examined scope**. |
| **E** | Revocation Proof & Status/Freshness | `PARTIAL` | `E-SUP-01`, `E-SUP-02`, `E-SUP-03` | `isRevoked` and `isOffline` are raw boolean inputs. `RegistryKeyRevocationList.ListSignature` **does not bind `RevokedKeys`** (preimage signs only `registry_id` and `updated_at`). Signing key `s.cfg.IssuerPrivateKey` is loaded from local node config with counterpart `IssuerPublicKey`; key authority and verifier distribution are `NOT VERIFIED FROM AVAILABLE EVIDENCE`. Verifiers for `ListSignature` and Dual-Horizon evaluation logic are **`NOT FOUND IN EXAMINED SEARCH SCOPE`**. `ONLINE_FRESH` is merely an online path classification (`ONLINE_CLASSIFICATION — ONLINE FRESHNESS NOT ESTABLISHED`). |
| **F** | Tier-2 Membership Authority & Signer Delegation | `PARTIAL` | `F-SUP-01`, `F-SUP-02` | `DelegationAssertion` supports 3-level scoped delegation; however, capability `ALBUM_MEMBERSHIP_SIGNING` is `NOT FOUND IN EXAMINED SEARCH SCOPE` (0 matches), `album_id` is **not in the struct or signed preimage**, and verifier has zero wiring to Album Manifest parsing. |

---

## 3. TARGETED EVIDENCE SUPPLEMENT PER GROUP (A–F)

### Group A: Genesis Root Certificate and Creator Genesis Identity

#### Evidence `A-SUP-01`: Structure, Canonicalization & Signature Preimage of `IdentityAssertion`
- **File:** `internal/domain/identity.go` (lines 62–78)
- **Struct Definition:**
```go
type IdentityAssertion struct {
	SpecVersion        string                `json:"spec_version"`
	AssertionID        string                `json:"assertion_id"`
	SubjectID          string                `json:"subject_id"`
	SubjectType        SubjectType           `json:"subject_type"`
	GenesisRootKey     string                `json:"genesis_root_key"`
	CurrentRootKey     string                `json:"current_root_key"`
	ActivePublicKey    string                `json:"active_public_key"`
	RecoveryKeyDigest  TriStateValue[string] `json:"recovery_key_digest"`
	IssuedAt           string                `json:"issued_at"`
	EffectiveAt        string                `json:"effective_at"`
	ExpiresAt          string                `json:"expires_at"`
	Nonce              string                `json:"nonce"`
	SignatureAlgorithm string                `json:"signature_algorithm"`
	Metadata           map[string]string     `json:"metadata,omitempty"`
	Signature          string                `json:"signature"`
}
```
- **Canonicalization Function:** `crypto.CanonicalizeJCS(payloadToVerify)` (`internal/engine/crypto/jcs.go:L18-L45`) implementing RFC 8785 JSON Canonicalization Scheme.
- **Exact Signed Preimage Fields:**
  In `internal/engine/identity/verifier.go:L199-L214`:
  ```go
  payloadToVerify := map[string]interface{}{
      "spec_version":        assertion.SpecVersion,
      "assertion_id":        assertion.AssertionID,
      "subject_id":          assertion.SubjectID,
      "subject_type":        string(assertion.SubjectType),
      "genesis_root_key":    assertion.GenesisRootKey,
      "current_root_key":    assertion.CurrentRootKey,
      "active_public_key":   assertion.ActivePublicKey,
      "recovery_key_digest": recoveryDigestValue,
      "issued_at":           assertion.IssuedAt,
      "effective_at":        assertion.EffectiveAt,
      "expires_at":          assertion.ExpiresAt,
      "nonce":               assertion.Nonce,
      "signature_algorithm": assertion.SignatureAlgorithm,
  }
  ```
- **Excluded Fields:** `Signature` and `Metadata` are strictly excluded from the canonical preimage.
- **Verification Function:** `ed25519.Verify(pubKey, canonicalBytes, sigBytes)` in `verifier.go:L224`.
- **Public Key Used:** Raw 32-byte Ed25519 public key decoded from `activeSigningKeyAtT` (resolved by `ResolveActiveSigningAuthorityAt`).

#### Evidence `A-SUP-02`: Absence of Independent Trust-Anchor Store in Verifier
- **Files:** `internal/engine/identity/verifier.go` (lines 14–31, 131), `pkg/nexa/identity.go` (lines 17–30)
- **Data Flow of Genesis Root Key:**
  1. The caller instantiates an empty `IdentityVerifier{}` (no state, no database connection, no configuration store).
  2. In `verifier.go:L131`, the verifier passes `assertion.GenesisRootKey` directly to `ResolveRootAuthorityAt`.
  3. In `verifier.go:L156`, the verifier passes `assertion.GenesisRootKey` directly to `ResolveActiveSigningAuthorityAt`.
  4. In `verifier.go:L181-L224`, `ed25519.Verify` verifies the assertion signature against the derived active key.
- **Factual Determination on Trust-Anchor Source:**
  - **Source of Genesis Key:** Ingested entirely from untrusted caller input (`assertion.GenesisRootKey`).
  - **Trust Anchor Store:** **NOT FOUND IN EXAMINED SCOPE**. There is no trust-anchor repository, no pinned root key store, and no external certificate authority lookup in `IdentityVerifier`.
  - **Distinction for AA:** `ExecutePipeline` proves that the signature is **cryptographically valid and consistent with the asserted genesis key and active key sequence**, but it **does NOT prove that the Genesis Root Key is trusted by the client or system**. Trust in the Genesis Root Key is an unverified caller assumption.

---

### Group B: Individual Creator vs Organization Key Lineage

#### Evidence `B-SUP-01`: Organization Lineage & Recovery Mechanisms
- **File:** `internal/engine/identity/lineage.go` (lines 15–92, 95–153), `internal/engine/identity/active_key.go` (lines 14–90, 93–154)
- **Organization Primitives:**
  1. `RootRecoveryAssertion` carrying `CompromisedRootKey`, `RecoveryPublicKey`, and `SuccessorRootKey`.
  2. `Verify2StepRootRecovery` enforces Step 1 (SHA-256 pre-image digest match against `genesis_recovery_key_digest`) and Step 2 (Ed25519 signature over JCS canonical payload using `RecoveryPublicKey`).
  3. `ResolveRootAuthorityAt` enforces effective timestamp sequencing, rejects competing branches (`ErrCodeLineageBranchingConflict`), and traverses predecessor key continuity (`CompromisedRootKey == currentRoot`).
  4. `ActiveKeyAuthorizationAssertion` carrying `AuthorizingRootKey`, `ActivePublicKey`, `SequenceNumber`, and `PreviousActiveKey`.
  5. `ResolveActiveSigningAuthorityAt` strictly requires sequence number monotonically increasing (`SequenceNumber == pred + 1`), predecessor key match (`PreviousActiveKey == pred.ActivePublicKey`), and rejects competing sequence numbers (`ErrCodeActiveKeyConflict`).
- **Tests:** Verified by `TestVerify2StepRootRecovery`, `TestUnboundedRecoveryLineageDepth`, and `TestActiveKeyAuthorizationSequenceRules` in `tests/identity/`.

#### Evidence `B-SUP-02`: Scope of `ResolveActiveSigningAuthorityAt` for Individual & Organization
- **Files:** `internal/domain/identity.go` (lines 30, 99–114), `internal/engine/identity/active_key.go` (lines 93–154), `internal/engine/identity/verifier.go` (lines 77–81, 156–170)
- **Function Definition:**
  ```go
  func ResolveActiveSigningAuthorityAt(
      genesisRootKey string,
      recoveryAssertions []*domain.RootRecoveryAssertion,
      activeKeyAssertions []*domain.ActiveKeyAuthorizationAssertion,
      genesisRecoveryKeyDigest *string,
      targetTimestamp string,
  ) (string, error)
  ```
- **Detailed Findings:**
  1. **Absence of Subject-Type Branching:** `ResolveActiveSigningAuthorityAt` does **not accept or evaluate `subject_type`**. It operates purely on `genesisRootKey`, recovery assertions, and active key assertions.
  2. **Call-Site Inspection in `IdentityVerifier.ExecutePipeline`:**
     - On line 77, `verifier.go` validates that `assertion.SubjectType` is either `ORGANIZATION` or `INDIVIDUAL`.
     - On line 156, it invokes `ResolveActiveSigningAuthorityAt` identically for both subject types.
     - There is **no branching** that diverts `SubjectTypeIndividual` away from the resolver or alters active key evaluation based on subject type.
  3. **Structure of `ActiveKeyAuthorizationAssertion`:**
     - Delineated in `internal/domain/identity.go:L99-L114`.
     - Field `SubjectID string` holds the canonical URN `urn:nexa:id:` + hex(sha256(GenesisKey)), which is the exact same derivation format for both Individual and Organization subjects.
     - Contains **no `subject_type` field**.
     - Signature is verified against `RootAuthorityAt(assertion.EffectiveAt)` via Ed25519.
  4. **Consequences:**
     - The resolver and assertion struct are **structurally generic and capable of binding both subject types**.
  5. **Status in Existing Tests:**
     - In tested identity verification pipeline executions (`TestVerificationPipelineVerified`), test fixtures explicitly specify `SubjectTypeOrganization`.
     - Primitives (JCS RFC 8785, UTF-8 validation, Ed25519 interoperability, Subject ID derivation) and active key sequence rules are subject-agnostic.
     - Exactly **0 tests** in `tests/identity/` or `tests/audit/sprint14/` execute end-to-end assertion verification with `SubjectTypeIndividual`.
  6. **Reconciled & Bounded Conclusion:**
     - The source code resolver does not accept or evaluate `subject_type`.
     - The identity verification pipeline invokes the resolver for both subject types without structural restriction.
     - Dedicated end-to-end Individual Creator pipeline tests are absent from the examined test suite.
     - *Interpretive boundary:* This evidence does NOT prove that Individual Creators succeed through end-to-end production flow, nor does it indicate that Individual Creators are blocked or rejected by the resolver.

---

### Group C: Album-wide Ownership Evidence and Publisher-Origin Authority

#### Evidence `C-SUP-01`: Structure & Preimage of `OwnershipCertificate`
- **File:** `internal/domain/ownership.go` (lines 53–68), `internal/engine/ownership/cert.go` (lines 15–39, 42–99)
- **Struct Definition:**
```go
type OwnershipCertificate struct {
	OwnershipCertID   string            `json:"ownership_cert_id"`
	AssetID           string            `json:"asset_id"`
	UnderlyingCertID  string            `json:"underlying_cert_id"`
	SubjectID         string            `json:"subject_id"`
	CreatorPublicKey  string            `json:"creator_public_key"`
	CreatorSignature  string            `json:"creator_signature"`
	IssuerID          string            `json:"issuer_id"`
	IssuedAt          time.Time         `json:"issued_at"`
	EffectiveAt       time.Time         `json:"effective_at"`
	PreviousCertRef   string            `json:"previous_cert_ref,omitempty"`
	SignatureAlgorithm string           `json:"signature_algorithm"`
	IssuerSignature   string            `json:"issuer_signature"`
	Metadata          map[string]string `json:"metadata,omitempty"`
	Status            string            `json:"status"` // "ACTIVE" | "SUPERSEDED" | "REVOKED"
}
```
- **Canonical Preimage (`CanonicalGenesisPayload`):**
```go
type CanonicalGenesisPayload struct {
	AssetID          string `json:"asset_id"`
	CreatorPublicKey string `json:"creator_public_key"`
	EffectiveAt      string `json:"effective_at"`
	IssuedAt         string `json:"issued_at"`
	IssuerID         string `json:"issuer_id"`
	PreviousCertRef  string `json:"previous_cert_ref"`
	SubjectID        string `json:"subject_id"`
	UnderlyingCertID string `json:"underlying_cert_id"`
}
```
- **Signatures:** Binds Creator and certifying authority strictly to a single scalar `AssetID`.

#### Evidence `C-SUP-02`: Search Results in Documented Code Directories
- **Search Scope:** Strictly bounded across 11 documented code directories:
  `cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`.
- **Search Commands:**
  ```bash
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules --exclude-dir=vendor --exclude-dir=evidence --exclude-dir=docs --exclude-dir=scratch -i -E "album|collection|multi.?asset|asset.?list|asset_ids|member_ids" cmd internal pkg marketplace studio-desktop player-desktop verify-desktop mobile storage sdk migrations
  grep -RIn --exclude-dir=.git --exclude-dir=node_modules -E "type Ownership[A-Za-z]+ struct" .
  ```
- **Findings:**
  - `collection` matched only standard library references (C# `System.Collections.Generic`, JS `which-collection`, open-source license texts).
  - All ownership structures (`OwnershipCertificate`, `OwnershipTransfer`, `OwnershipDelegation`, `OwnershipEvent`) require scalar `AssetID string`.
  - Zero structures, interfaces, schemas, or API endpoints exist for Album-wide ownership or publisher-origin authority within the examined code directories.
- **Bounded Conclusion:**
  **`NOT FOUND IN EXAMINED CODE DIRECTORIES`** (examined: `cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/` at reported source revision `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`).
  *Scope boundary:* This finding is strictly bounded to the 11 examined code directories and does not prove repository-wide absence across unexamined paths (e.g. `tests/`, `docs/`, `evidence/`, `scratch/`) or alternative non-Go schemas.

---

### Group D: Registry Authority and Federated Trust

#### Evidence `D-SUP-01`: Structure, Canonicalization & Exclusion of `SupportedFeatures` in `RegistryIdentity`
- **File:** `internal/domain/registry_identity.go` (lines 13–63), `internal/service/service.go` (lines 62–71)
- **Struct Definition:**
```go
type RegistryIdentity struct {
	RegistryID        string    `json:"registry_id"`
	PublicKey         string    `json:"public_key"`
	EndpointURL       string    `json:"endpoint_url"`
	APIVersion        string    `json:"api_version"`
	SupportedFeatures []string  `json:"supported_features"`
	IssuedAt          time.Time `json:"issued_at"`
	ExpiresAt         time.Time `json:"expires_at"`         // 14-day validity window
	IdentitySignature string    `json:"identity_signature"` // JCS Ed25519 signature
}
```
- **Preimage String (`CanonicalJCS()`):**
```go
func (r *RegistryIdentity) CanonicalJCS() string {
	issuedStr := r.IssuedAt.UTC().Format("2006-01-02T15:04:05.000000000Z")
	expiresStr := r.ExpiresAt.UTC().Format("2006-01-02T15:04:05.000000000Z")
	return fmt.Sprintf(`{"api_version":%s,"endpoint_url":%s,"expires_at":%s,"issued_at":%s,"public_key":%s,"registry_id":%s}`,
		quoteJSON(r.APIVersion), quoteJSON(r.EndpointURL), quoteJSON(expiresStr), quoteJSON(issuedStr), quoteJSON(r.PublicKey), quoteJSON(r.RegistryID))
}
```
- **Signing & Verification:**
  - Signing in `service.go:L69`: `sigBytes := ed25519.Sign(s.cfg.IssuerPrivateKey, []byte(identity.CanonicalJCS()))`.
  - Verification in `registry_identity.go:L62`: `ed25519.Verify(pubKey, []byte(r.CanonicalJCS()), sigBytes)`.
- **Status of `SupportedFeatures`:**
  - `SupportedFeatures` is **strictly excluded** from `CanonicalJCS()`.
  - In `internal/service/service.go:L63`, it is populated with string literals, but is never referenced by `Evaluator.Evaluate`.
- **Cryptographic Consequences:**
  1. Signature `RegistryIdentity.IdentitySignature` does **NOT** provide cryptographic integrity over `SupportedFeatures`.
  2. Modifying `SupportedFeatures` does not cause `VerifySignature()` to fail.
  3. Consumers cannot assume `SupportedFeatures` has been authenticated merely because `VerifySignature()` succeeded.
  4. `NO ALTERNATIVE AUTHENTICATION MECHANISM FOUND IN EXAMINED SCOPE` protects `SupportedFeatures`.

#### Evidence `D-SUP-02`: Source of Trust for Registry Keys
- **File:** `internal/domain/federation.go` (lines 5–18), `internal/engine/federation/evaluator.go` (lines 203–273)
- **Mechanism:**
  - Trust in a Registry is established **exclusively by key pinning in the caller's configuration** (`RegistryTarget.PublicKey`).
  - In `evaluator.go:L204-L211`, `queryRegistry` enforces a strict fail-closed check: if `target.PublicKey == ""` and `!allowUnpinned`, the registry is rejected as untrusted (`res.RegistryTrusted = false`).
  - In `evaluator.go:L265`, it confirms `regId.PublicKey == target.PublicKey` and `regId.VerifySignature() == true`.

#### Evidence `D-SUP-03`: Dynamic HTTP Reliance & Absence of Offline Proofs
- **File:** `internal/engine/federation/evaluator.go` (lines 57–90, 214–290)
- **Offline Behavior (`evaluator.go:L74-L85`):**
  If `len(cfg.Registries) == 0` or offline network failure occurs, `Evaluator.Evaluate` immediately returns `TrustResult: UNKNOWN` and `EvidenceCompleteness: NONE`.
- **Finding:** There is **zero support** in the codebase for verifying embedded, offline static Registry attestations without live HTTP queries within the examined scope.

---

### Group E: Revocation Proof and Status/Freshness

#### Evidence `E-SUP-01`: Tracking of `FreshnessContext` & Clarification of `ONLINE_FRESH`
- **File:** `internal/domain/identity.go` (lines 158–174), `internal/engine/identity/verifier.go` (lines 34–49)
- **Data Flow in Verifier:**
  ```go
  freshness := domain.FreshnessOnlineFresh
  if isOffline {
      freshness = domain.FreshnessOfflineCached
  }
  ```
- **Clarification of `ONLINE_FRESH`:**
  - `FreshnessOnlineFresh` is a direct mapping from the caller-supplied boolean argument `!isOffline`.
  - There is **no verification of network connectivity, no registry ping, no cache TTL validation, and no freshness timestamp check**.
  - Therefore, `ONLINE_FRESH` represents an **online path classification (`ONLINE_CLASSIFICATION — ONLINE FRESHNESS NOT ESTABLISHED`)**, NOT an established temporal or cryptographic freshness proof.

#### Evidence `E-SUP-02`: Key Relations, Preimage Analysis, and Verifier Boundaries of `RegistryKeyRevocationList`
- **Files:** `internal/domain/registry_identity.go` (lines 24–29), `internal/service/service.go` (lines 75–88), `internal/config/config.go` (lines 140–158)
- **Issuance Logic in `service.go:L75-L88`:**
  ```go
  func (s *service) GetRegistryKeyRevocations(ctx context.Context) (*domain.RegistryKeyRevocationList, error) {
      now := time.Now().UTC().Truncate(time.Second)
      crl := &domain.RegistryKeyRevocationList{
          RegistryID:  "nexa-registry-primary",
          RevokedKeys: []string{},
          UpdatedAt:   now,
      }
      canonStr := fmt.Sprintf(`{"registry_id":"%s","updated_at":"%s"}`, crl.RegistryID, crl.UpdatedAt.Format("2006-01-02T15:04:05.000000000Z"))
      sigBytes := ed25519.Sign(s.cfg.IssuerPrivateKey, []byte(canonStr))
      crl.ListSignature = hex.EncodeToString(sigBytes)
      return crl, nil
  }
  ```
- **Signing Private Key & Public Key Counterpart:**
  - `s.cfg.IssuerPrivateKey` is loaded from `ISSUER_PRIVATE_KEY_HEX` in `internal/config/config.go:L140-L158`.
  - The node configuration also defines `s.cfg.IssuerPublicKey`, loaded from `ISSUER_PUBLIC_KEY_HEX`.
- **Preimage Analysis & Omission of `RevokedKeys`:**
  - The signed preimage `canonStr` contains **only `registry_id` and `updated_at`**.
  - Field `RevokedKeys` is **completely omitted from the signed preimage**.
  - **Explicit Statement:**
    > **Signature yang dihasilkan oleh mekanisme tersebut tidak mengikat isi `RevokedKeys`. Keberhasilan verifikasi signature hanya membuktikan integritas field yang benar-benar tercakup dalam signature preimage (`registry_id` dan `updated_at`), bukan integritas daftar key yang dicabut.**
- **Key Authority and Trust Verification:**
  - How verifiers obtain `IssuerPublicKey`, who owns or holds authority over the key beyond local node config, and how it is distributed are **`NOT VERIFIED FROM AVAILABLE EVIDENCE`**.
- **Verifier Scope Boundary:**
  - Functions verifying `ListSignature` are **`NOT FOUND IN EXAMINED SEARCH SCOPE`** (searched across `internal/`, `pkg/`, `apps/`).
  - No alternative authentication mechanism was found in the examined scope.

#### Evidence `E-SUP-03`: Unimplemented Dual-Horizon Time Evaluation
- **Files:** `internal/service/service.go` (line 306), `internal/domain/ownership.go` (line 108)
- **Finding:** `revoked_at` exists only in audit log metadata (`service.go:L306`); `recorded_at` exists only as a database column in `OwnershipEvent`. There is **zero code** comparing `revoked_at` with `recorded_at` in any verifier. Dual-Horizon time evaluation is **`NOT FOUND IN EXAMINED SCOPE`**.

---

### Group F: Tier-2 Membership Authority and Album Signer Delegation

#### Evidence `F-SUP-01`: Structure & Scope Subsetting of `DelegationAssertion`
- **File:** `internal/domain/identity.go` (lines 124–144), `internal/engine/identity/delegation.go` (lines 13–115)
- **Preimage Fields:** All fields except `Signature` are canonicalized via RFC 8785 JCS in `VerifyDelegationAssertion:L50-L73` and verified using `ParentPublicKey`.
- **Depth Limiting:** `CheckSubdelegationDepth` (`delegation.go:L100-L114`) prohibits Level-2 keys from delegating (`DelegatorLevel >= 2 || CurrentDepth >= 2`).

#### Evidence `F-SUP-02`: Absence of `ALBUM_MEMBERSHIP_SIGNING` and `album_id` Binding
- **Findings:**
  - `ALBUM_MEMBERSHIP_SIGNING` has **0 matches** across the examined code paths.
  - `DelegationAssertion` contains generic `DelegatedScope []string` and has **zero fields for `album_id`**.
  - No caller connects delegation verification to Album Manifest parsing.
  - **Conclusion:** **`NOT FOUND IN EXAMINED SEARCH SCOPE`**.

---

## 4. TEST EXECUTION RECONCILIATION SUMMARY

- **Command Executed:**
  ```bash
  GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -count=1 -v ./tests/identity/... ./tests/audit/sprint14/... ./internal/engine/ownership/... ./internal/engine/federation/...
  ```
- **Reconciled Test Counts:**
  - **Top-Level Tests Run:** **39 tests** (all PASS)
    - `tests/identity`: 14 tests
    - `tests/audit/sprint14`: 16 tests
    - `internal/engine/ownership`: 1 test (`TestGoldenOwnershipScenarios`)
    - `internal/engine/federation`: 8 tests
  - **Nested Subtests Run:** **19 subtests** (all PASS)
    - `tests/audit/sprint14`: 8 subtests (`JCS-AUDIT-VEC-01` through `08`)
    - `internal/engine/ownership`: 11 subtests (`OWN-CERT-01_And_02` through `OWN-FEDERATION-01B`)
  - **Total Test Invocations:** **58 invocations** (39 top-level + 19 nested).
- **Classification Reconciliation:**
  - Tests in `internal/engine/ownership` test asset certificates and transfers (`[ASSET-LEVEL]`).
  - Tests in `internal/engine/federation` test dynamic registry consensus and local overlays (`[FEDERATION-LEVEL]`).
  - Tests in `tests/identity` validating RFC 8785 JCS, UTF-8 fail-closed rejection, Ed25519 vectors, and Subject ID derivation test mathematical and serialization primitives (`[SUBJECT-AGNOSTIC PRIMITIVE]`).
  - Tests validating active key sequences, delegation depth, and lineage traversal test sequence algorithms (`[SUBJECT-AGNOSTIC MECHANISM]`).
  - Historical regression suites in `tests/audit/sprint14` and `tests/identity` test baseline regression protection without subject differentiation (`[NOT CLASSIFIED]`).
  - Only specific identity assertion verification fixtures (such as `TestVerificationPipelineVerified`) instantiate `IdentityAssertion` with `subject_type: "ORGANIZATION"`.
  - Zero dedicated end-to-end Individual Creator pipeline tests exist in the examined scope.
