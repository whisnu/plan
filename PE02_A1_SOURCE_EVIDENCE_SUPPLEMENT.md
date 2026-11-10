# NEXA PE-02 A1 — TARGETED SOURCE-EVIDENCE SUPPLEMENT
## ARCHITECTURAL FACTUAL EVIDENCE DOSSIER

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Commit SHA:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
- **Working Tree Classification:** `DIRTY — UNTRACKED FILES`
  - Tracked files modified: **NONE** (`git diff` is empty)
  - Untracked files present:
    - `docs/roadmaps/Nexa_Development_Roadmap_v4_8.md`
    - `docs/whitepapers/Nexa_White_Paper_v5_6.md`
- **Inspection Date:** 2026-11-10
- **Task Nature:** Read-Only Source-Evidence Supplement (Zero Code/Schema/Config Changes)
- **Reference Plan:** `whisnu/plan` -> `main` -> `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (§16.16.4A, §16.16.4B)

---

## 1. REVISION & WORKING-TREE STATUS CLARIFICATION

In the previous preliminary handoff, the repository status was colloquially described as "Clean" while simultaneously mentioning two untracked markdown documents in `docs/`. 

To strictly comply with Section 3 of this Mandate:
- **Corrected Working-Tree Classification:** `DIRTY — UNTRACKED FILES`.
- **Justification:** `git status --porcelain` returns two untracked files (`?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md` and `?? docs/whitepapers/Nexa_White_Paper_v5_6.md`). There are zero modified tracked files (`git diff --stat` is empty). No source files have been altered, added, or removed.
- **Commit Lineage:** The commit inspected in this supplement is identical to the baseline: `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (HEAD of `main`). All line numbers and source citations in this supplement correspond exactly to this commit.

---

## 2. EXECUTIVE SUMMARY OF SUPPLEMENTAL FINDINGS

| Group | Topic | Status | Evidence IDs | Core Supplemental Finding |
| :--- | :--- | :--- | :--- | :--- |
| **A** | Genesis Root Certificate & Creator Genesis Identity | `PARTIAL` | `A-SUP-01`, `A-SUP-02` | `IdentityAssertion` verifies JCS Ed25519 signature against `ActivePublicKey`; however, `GenesisRootKey` is ingested purely as untrusted caller data from the assertion itself. There is **zero trust-anchor store, zero pinned root certificate store, and zero trust-anchor lookup** in the identity engine. |
| **B** | Individual Creator vs Organization Key Lineage | `PARTIAL` | `B-SUP-01`, `B-SUP-02` | Organization has comprehensive 2-step root recovery and monotonic Level-1 active key sequencing. Individual Creator (`SubjectTypeIndividual`) has **zero key rotation, zero recovery mechanisms, and zero tests in `tests/identity/`**; verifier unconditionally fails with `ERR_ACTIVE_KEY_PROOF_INCOMPLETE` if Level-1 assertions are absent. |
| **C** | Album-wide Ownership vs per-asset Evidence | `PARTIAL` | `C-SUP-01`, `C-SUP-02` | `OwnershipCertificate` is strictly bound to scalar `asset_id`. A repository-wide regex search across all Go packages for `album` yields **0 matches**. Zero native mechanisms exist for multi-asset aggregation, compilation rights, or publisher-origin authority. |
| **D** | Registry Authority & Federated Trust | `PARTIAL` | `D-SUP-01`, `D-SUP-02`, `D-SUP-03` | Registry public keys are trusted strictly via caller-injected `RegistryTarget.PublicKey` pinning (`AllowUnpinnedRegistries=false`). `Evaluator.Evaluate` relies exclusively on dynamic HTTP network queries; **no offline self-contained cryptographic Registry proof structure exists**. |
| **E** | Revocation Proof & Status/Freshness | `PARTIAL` | `E-SUP-01`, `E-SUP-02`, `E-SUP-03` | `isRevoked` and `isOffline` are raw boolean inputs. `RegistryKeyRevocationList` is signed at service issuance but has **zero verification functions** in the codebase. Dual-Horizon time evaluation (`revoked_at` vs `recorded_at`) is **completely unimplemented** in verifiers. |
| **F** | Tier-2 Membership Authority & Signer Delegation | `PARTIAL` | `F-SUP-01`, `F-SUP-02` | `DelegationAssertion` supports 3-level scoped delegation; however, capability `ALBUM_MEMBERSHIP_SIGNING` is `NOT FOUND` (0 matches), `album_id` is **not in the struct or signed preimage**, and verifier has zero wiring to Album Manifest parsing. |

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
- **Public Key Used:** The raw 32-byte Ed25519 public key decoded from `activeSigningKeyAtT` (resolved by `ResolveActiveSigningAuthorityAt`).

#### Evidence `A-SUP-02`: Absence of Independent Trust-Anchor Store in Verifier
- **Files:** `internal/engine/identity/verifier.go` (lines 14–31, 131), `pkg/nexa/identity.go` (lines 17–30)
- **Verifier Entry Point:**
```go
type IdentityVerifier struct{}

func NewIdentityVerifier() *IdentityVerifier {
	return &IdentityVerifier{}
}

func (v *IdentityVerifier) ExecutePipeline(
	assertion *domain.IdentityAssertion,
	recoveryAssertions []*domain.RootRecoveryAssertion,
	activeKeyAssertions []*domain.ActiveKeyAuthorizationAssertion,
	delegationAssertions []*domain.DelegationAssertion,
	isRevoked bool,
	targetTimestamp string,
	isOffline bool,
) *domain.VerificationResult
```
- **Data Flow of Genesis Root Key:**
  1. The caller instantiates an empty `IdentityVerifier{}` (no state, no database connection, no configuration store).
  2. In `verifier.go:L131`, the verifier passes `assertion.GenesisRootKey` directly to `ResolveRootAuthorityAt`:
     ```go
     rootAuthorityAtT, err := ResolveRootAuthorityAt(assertion.GenesisRootKey, recoveryAssertions, recoveryDigestPtr, targetTimestamp)
     ```
  3. In `verifier.go:L156`, the verifier passes `assertion.GenesisRootKey` directly to `ResolveActiveSigningAuthorityAt`:
     ```go
     activeSigningKeyAtT, err := ResolveActiveSigningAuthorityAt(assertion.GenesisRootKey, recoveryAssertions, activeKeyAssertions, recoveryDigestPtr, targetTimestamp)
     ```
  4. In `verifier.go:L181-L224`, `ed25519.Verify` verifies the assertion signature against the derived active key.
- **Factual Determination on Trust-Anchor Source:**
  - **Source of Genesis Key:** Ingested entirely from the untrusted caller input (`assertion.GenesisRootKey`).
  - **Trust Anchor Store:** **NOT FOUND / DOES NOT EXIST**. There is no trust-anchor repository, no file on disk, no pinned root key store, and no external certificate authority lookup in `IdentityVerifier`.
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
- **Tests:** Fully verified by `TestVerify2StepRootRecovery`, `TestUnboundedRecoveryLineageDepth`, and `TestActiveKeyAuthorizationSequenceRules` in `tests/identity/`.

#### Evidence `B-SUP-02`: Individual Creator Lineage & Active Key Resolution Gap
- **Files:** `internal/domain/identity.go` (line 30), `internal/engine/identity/verifier.go` (lines 77–81, 156–170), `internal/engine/identity/active_key.go` (lines 99–102)
- **Factual Trace of Individual Creator:**
  1. `SubjectTypeIndividual` is defined in `internal/domain/identity.go:L30`:
     ```go
     const (
         SubjectTypeIndividual   SubjectType = "INDIVIDUAL"
         SubjectTypeOrganization SubjectType = "ORGANIZATION"
     )
     ```
  2. In `verifier.go:L77-L81`, the verifier checks that `SubjectType` is either Organization or Individual:
     ```go
     if assertion.SubjectType != domain.SubjectTypeOrganization && assertion.SubjectType != domain.SubjectTypeIndividual {
         result.ErrorCode = domain.ErrCodeSubjectTypeUnknown
         return result
     }
     ```
  3. **Critical Discovery:** Beyond line 77, `verifier.go` **never branches on `SubjectType`**. It subjects Individual Creator assertions to the exact same Organization pipeline!
  4. In `verifier.go:L156`, `ResolveActiveSigningAuthorityAt` is called unconditionally:
     ```go
     activeSigningKeyAtT, err := ResolveActiveSigningAuthorityAt(assertion.GenesisRootKey, recoveryAssertions, activeKeyAssertions, recoveryDigestPtr, targetTimestamp)
     ```
  5. In `active_key.go:L99-L102`, `ResolveActiveSigningAuthorityAt` contains a hard fail-closed guard:
     ```go
     // Rule (HR-14-IMP-02): Active key authorization proof MUST be present.
     if len(activeKeyAssertions) == 0 {
         return "", fmt.Errorf("%s: missing active key authorization proof", domain.ErrCodeActiveKeyProofIncomplete)
     }
     ```
  6. **Consequence:** If an Individual Creator submits an `IdentityAssertion` with their permanent Genesis Key (and provides no `activeKeyAssertions`), verification **fails unconditionally with `ERR_ACTIVE_KEY_PROOF_INCOMPLETE`**!
  7. **Test Audit Result:** A search across `tests/identity/` and `tests/audit/sprint14/` reveals **0 test cases with `SubjectTypeIndividual`**. All 43 test cases in these suites exclusively test `SubjectTypeOrganization`.
  8. **Conclusion for AA:** Nexa has **no native key rotation, no key succession, and no separate verification path for Individual Creators**. An Individual Creator currently cannot verify their identity assertion without fabricating Organization-style Level-1 active key assertions.

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
- **Signatures and Meanings:**
  1. `CreatorSignature`: Ed25519 signature generated with `creatorPrivKey` over `CanonicalGenesisPayload`. Binds Creator to initial claim over single asset `AssetID`.
  2. `IssuerSignature`: Ed25519 signature generated with `issuerPrivKey` over the same `CanonicalGenesisPayload`. Binds the certifying registry/authority to the certificate.

#### Evidence `C-SUP-02`: Search Results Proving Absence of Album-Wide Ownership Mechanisms
- **Search Command:**
  ```bash
  grep -RIn --exclude-dir=.git -i "album" internal pkg
  ```
- **Output:** Exit Code `1` (0 matches across all Go source files in `internal/` and `pkg/`).
- **Targeted Package Searches:**
  1. `internal/domain/ownership.go`: `AssetID string` is strictly scalar; all methods (`OwnershipTransfer`, `OwnershipDelegation`, `OwnershipEvent`) operate on scalar `AssetID`.
  2. `internal/engine/ownership/cert.go`: `CanonicalGenesisPayload` accepts exactly one `assetID string`.
  3. `internal/engine/ownership/verifier.go`: `VerifyOwnershipCertificate` evaluates only `cert.AssetID`.
- **Conclusion for AA:** **`NOT FOUND IN EXAMINED SCOPE`**. Nexa possesses zero data structures, zero interfaces, and zero verifier logic for Album-wide ownership, compilation rights, multi-asset aggregation, or publisher-origin authority.

---

### Group D: Registry Authority and Federated Trust

#### Evidence `D-SUP-01`: Structure & Self-Signed Preimage of `RegistryIdentity`
- **File:** `internal/domain/registry_identity.go` (lines 13–63)
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
- **Verification (`VerifySignature()`):** Validates that `r.IdentitySignature` was generated by `r.PublicKey` over `CanonicalJCS()`, verifies expiry (`now.After(ExpiresAt)`), and allows maximum 5-minute clock skew on `IssuedAt`.

#### Evidence `D-SUP-02`: Source of Trust for Registry Keys
- **File:** `internal/domain/federation.go` (lines 5–18), `internal/engine/federation/evaluator.go` (lines 203–273)
- **Mechanism of Trust:**
  1. Trust in a Registry is established **exclusively by key pinning in the caller's configuration**:
     ```go
     type RegistryTarget struct {
         RegistryID string `json:"registry_id"`
         URL        string `json:"url"`
         PublicKey  string `json:"public_key,omitempty"` // Pinned public key hex
     }
     ```
  2. In `evaluator.go:L204-L211`, `queryRegistry` enforces a strict fail-closed check:
     ```go
     if target.PublicKey == "" && !allowUnpinned {
         res.RegistryTrusted = false
         res.Error = "Unpinned Registry rejected by fail-closed policy (AllowUnpinnedRegistries = false)"
         res.ResponseStatus = "untrusted"
         return
     }
     ```
  3. In `evaluator.go:L265`, `queryRegistry` verifies that the downloaded `regId.PublicKey == target.PublicKey` and `regId.VerifySignature() == true`. If the keys mismatch or signature fails, `res.RegistryTrusted` is set to `false`.
- **Meaning of `AllowUnpinnedRegistries=false`:** Discards any registry target that does not have an explicitly pre-pinned Ed25519 public key in the client's `FederationConfig`.

#### Evidence `D-SUP-03`: Dynamic HTTP Reliance & Absence of Offline Proofs
- **File:** `internal/engine/federation/evaluator.go` (lines 57–90, 214–290)
- **Call Flow:**
  - `Evaluator.Evaluate` receives `assetHash`, `certID`, and `cfg domain.FederationConfig`.
  - Spawns goroutines calling `e.queryRegistry` for each target.
  - Queries `GET {target.URL}/v1/identity` and `GET {target.URL}/v1/certificates/{certID}` via `http.Client`.
  - Aggregates status: `ACTIVE`, `REVOKED`, `CONFLICT`, `UNKNOWN`.
- **Offline Behavior (`evaluator.go:L74-L85`):**
  ```go
  if len(cfg.Registries) == 0 {
      res.TrustResult = "UNKNOWN"
      res.EvidenceCompleteness = "NONE"
      res.InternalState = domain.InternalStateIncomplete
      res.CanonicalUIState = domain.UICanonicalVerificationIncomplete
      return res
  }
  ```
- **Factual Determination for AA:**
  1. `RegistryIdentity` **only proves service endpoint identity** (that the server possesses the pinned key); it does not attest to specific assets or albums.
  2. **Offline Registry Proof:** **NOT FOUND / DOES NOT EXIST**. There is zero support in `evaluator.go` for verifying embedded, offline static Registry attestations without live HTTP queries.

---

### Group E: Revocation Proof and Status/Freshness

#### Evidence `E-SUP-01`: Tracking of `FreshnessContext` and `RevocationFinality`
- **File:** `internal/domain/identity.go` (lines 158–174), `internal/engine/identity/verifier.go` (lines 34–49)
- **Data Flow in Verifier:**
  ```go
  freshness := domain.FreshnessOnlineFresh
  if isOffline {
      freshness = domain.FreshnessOfflineCached
  }

  finality := domain.RevocationFinalityNone
  if isRevoked {
      finality = domain.RevocationFinalityRecoverable
  }
  ```
- **Observations:**
  1. `FreshnessContext` is a direct mapping from the caller-supplied `isOffline bool`.
  2. `FreshnessOfflineUnchecked` is defined in `domain/identity.go:L164` but **is never referenced or assigned anywhere else in the repository**.
  3. `RevocationFinality` is a direct mapping from caller-supplied `isRevoked bool`.
  4. `RevocationFinalityTerminal` is defined in `domain/identity.go:L173` but **is never referenced or assigned anywhere else in the repository**.

#### Evidence `E-SUP-02`: Incomplete Verification of `RegistryKeyRevocationList`
- **Files:** `internal/domain/registry_identity.go` (lines 24–29), `internal/service/service.go` (lines 75–88)
- **Issuance Logic in `service.go`:**
  ```go
  crl := &domain.RegistryKeyRevocationList{
      RegistryID:  "nexa-registry-primary",
      RevokedKeys: []string{},
      UpdatedAt:   now,
  }
  canonStr := fmt.Sprintf(`{"registry_id":"%s","updated_at":"%s"}`, crl.RegistryID, crl.UpdatedAt.Format("2006-01-02T15:04:05.000000000Z"))
  sigBytes := ed25519.Sign(s.cfg.IssuerPrivateKey, []byte(canonStr))
  crl.ListSignature = hex.EncodeToString(sigBytes)
  ```
- **Verification Search:** A grep for `ListSignature` across the entire codebase finds only its struct declaration (`registry_identity.go:L28`) and issuance assignment (`service.go:L85`).
- **Finding:** **ZERO verification functions exist for `RegistryKeyRevocationList`**. The signature is produced by the service but is never parsed or verified by any client or verifier.

#### Evidence `E-SUP-03`: Unimplemented Dual-Horizon Time Evaluation
- **Files:** `internal/service/service.go` (line 306), `internal/domain/ownership.go` (line 108)
- **Factual Trace:**
  - `revoked_at` exists exclusively as an arbitrary key in an audit logging map in `service.go:L306`:
    ```go
    _ = s.logAudit(ctx, domain.OpRevoke, id, operatorIdentity, requestID, map[string]interface{}{
        "reason_code": reasonCode,
        "revoked_at":  now,
    })
    ```
  - `recorded_at` exists exclusively as a database column and struct field in `OwnershipEvent` (`ownership.go:L108`).
  - **Absence of Dual-Horizon Logic:** There is **zero code** comparing `revoked_at` (signer time) with `recorded_at` (ledger recording time) in any verifier. The Dual-Horizon Time Rule exists as an architectural invariant in PLAN §16.16, but is completely unimplemented in source code.

---

### Group F: Tier-2 Membership Authority and Album Signer Delegation

#### Evidence `F-SUP-01`: Structure & Scope Subsetting of `DelegationAssertion`
- **File:** `internal/domain/identity.go` (lines 124–144), `internal/engine/identity/delegation.go` (lines 13–115)
- **Struct Definition:**
```go
type DelegationAssertion struct {
	SpecVersion        string   `json:"spec_version"`
	AssertionType      string   `json:"assertion_type"` // "DELEGATION"
	AssertionID        string   `json:"assertion_id"`
	SubjectID          string   `json:"subject_id"`
	DelegatorSubjectID string   `json:"delegator_subject_id"`
	DelegatorLevel     int      `json:"delegator_level"`
	ParentPublicKey    string   `json:"parent_public_key"`
	DelegatePublicKey  string   `json:"delegate_public_key"`
	DelegatedScope     []string `json:"delegated_scope"`
	AllowSubdelegation bool     `json:"allow_subdelegation"`
	MaxDelegationDepth int      `json:"max_delegation_depth"`
	CurrentDepth       int      `json:"current_depth"`
	IssuedAt           string   `json:"issued_at"`
	EffectiveAt        string   `json:"effective_at"`
	ExpiresAt          string   `json:"expires_at"`
	Nonce              string   `json:"nonce"`
	SignatureAlgorithm string   `json:"signature_algorithm"`
	Signature          string   `json:"signature"`
}
```
- **Preimage Fields:** All fields except `Signature` are canonicalized via RFC 8785 JCS in `VerifyDelegationAssertion:L50-L73` and verified using `ParentPublicKey`.
- **Scope Subsetting:** `CheckScopeSubsetting` (`delegation.go:L84-L97`) ensures that every scope string in `childScopes` is present in `parentScopes`.
- **Depth Limiting:** `CheckSubdelegationDepth` (`delegation.go:L100-L114`) prohibits Level-2 keys from delegating (`DelegatorLevel >= 2 || CurrentDepth >= 2`).

#### Evidence `F-SUP-02`: Absence of `ALBUM_MEMBERSHIP_SIGNING` and `album_id` Binding
- **Search Queries:**
  1. `grep -rnw "ALBUM_MEMBERSHIP_SIGNING" .` -> **0 matches**.
  2. `grep -rni "album_id" internal/domain/identity.go internal/engine/identity/` -> **0 matches**.
- **Factual Trace:**
  1. `DelegatedScope` is a slice of arbitrary strings (`[]string`).
  2. The only constants defined in `internal/domain/identity.go:L208-L209` are:
     ```go
     const (
         ScopeRevocation = "SCOPE_REVOCATION"
         ScopeDelegation = "SCOPE_DELEGATION"
     )
     ```
  3. `DelegationAssertion` has **zero fields for `album_id`**.
  4. There is no caller in `player-desktop`, `player-mobile`, or `verify-desktop` that invokes `ResolveDelegatedAuthorityChain` or `VerifyDelegationAssertion` in connection with Album Manifest verification.
- **Conclusion for AA:** **`NOT FOUND IN EXAMINED SCOPE`**. Generic delegation exists, but Album-specific capability, `album_id` scoping, and production verifier wiring are entirely absent.

---

## 4. TEST EXECUTION RECONCILIATION SUMMARY

The previous report mentioned "43 tests" without detailing the breakdown between top-level tests, nested subtests, and package boundaries. 

The exact reconciliation is documented in [PE02_A1_TEST_RECONCILIATION.md](file:///opt/antigravity/projects/nexa/scratch/pe02_a1_supplement/PE02_A1_TEST_RECONCILIATION.md) and summarized below:

- **Command Executed:**
  ```bash
  GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -count=1 -v ./tests/identity/... ./tests/audit/sprint14/... ./internal/engine/ownership/... ./internal/engine/federation/...
  ```
- **Top-Level Tests Run:** **39 tests** (all PASS)
  - `tests/identity`: 14 top-level tests
  - `tests/audit/sprint14`: 16 top-level tests
  - `internal/engine/ownership`: 1 top-level test (`TestGoldenOwnershipScenarios`)
  - `internal/engine/federation`: 8 top-level tests
- **Nested Subtests Run:** **19 subtests** (all PASS)
  - `tests/audit/sprint14`: 8 subtests (`JCS-AUDIT-VEC-01` through `08`)
  - `internal/engine/ownership`: 11 subtests (`OWN-CERT-01_And_02` through `OWN-FEDERATION-01B`)
- **Total Test Invocations:** **58 invocations** (39 top-level + 19 nested).
- **Explanation of Discrepancy ("43"):** In the previous report, the author combined 14 (`tests/identity` top-level) + 18 (historical `tests/audit/sprint14` count including 2 assertion vectors) + 11 (`internal/engine/ownership` subtests) = 43, while omitting the 8 tests of `internal/engine/federation`. The reconciliation confirms 100% test passing across 39 top-level tests and 19 nested subtests.

---

## 5. REPRODUCIBLE SEARCH SCOPE & METHODOLOGY

All search queries, paths, exit codes, and limitations are fully documented in [PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md](file:///opt/antigravity/projects/nexa/scratch/pe02_a1_supplement/PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md).
- Search tooling: GNU ripgrep / grep with `--exclude-dir=.git`.
- All scopes were bounded within `/opt/antigravity/projects/nexa`.
- Exact commands and raw outputs confirm that negative findings (`NOT FOUND`) are exhaustive within the repository.
