# NEXA PE-02 A1 — TEST EXECUTION RECONCILIATION REPORT (RECONCILED & SYNCHRONIZED)

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Source Revision:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (reported in Programmer evidence; not independently verified by AA)
- **Working Directory:** `/opt/antigravity/projects/nexa`
- **Test Command:**
  ```bash
  GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -count=1 -v ./tests/identity/... ./tests/audit/sprint14/... ./internal/engine/ownership/... ./internal/engine/federation/...
  ```
- **Execution Rule:** Verified against already-executed raw outputs; no re-execution of test suite is required.
- **Exit Code:** `0` (ALL PASS)

---

## 1. RECONCILIATION OF PREVIOUS TEST COUNT ("43")

### 1.1 The Discrepancy
In early preliminary reporting, an unnormalized statement noted:
> *"Total Test Cases Executed: 43 tests (43 PASS, 0 FAIL)"*

An inspection of the raw `go test` output across all four test suites demonstrates:
- **39 lines** of top-level `=== RUN   Test...`
- **19 lines** of nested subtest `=== RUN   Test.../...`
- **39 lines** of top-level `--- PASS: Test...`
- **19 lines** of nested subtest `--- PASS: Test.../...`
- Total individual test invocations = **58 invocations**.

### 1.2 Mathematical Derivation of "43"
The figure "43" was derived from an unnormalized aggregation of three specific test suites:
1. `tests/identity`: **14** top-level test functions.
2. `tests/audit/sprint14`: **18** assertions/vectors counted historically (16 top-level test functions plus 2 standalone vectors).
3. `internal/engine/ownership`: **11** subtests executed within `TestGoldenOwnershipScenarios`.
4. Calculation: `14 + 18 + 11 = 43`.

**Why this was inaccurate:**
1. It mixed top-level test functions (in `tests/identity` and `tests/audit/sprint14`) with nested subtests (in `internal/engine/ownership`).
2. It completely omitted the **8 top-level tests** of `internal/engine/federation` from the sum.
3. Therefore, "43" must NOT be retained as a total test invocation count.

### 1.3 Correct Normalized Test Inventory
- **Top-Level Tests:** **39** (all PASS)
- **Nested Subtests:** **19** (all PASS)
- **Total Test Invocations:** **58** (all PASS)
- **Failed / Skipped:** **0**

Distribution across suites:

| Test Suite | Top-Level Tests | Nested Subtests | Total Invocations | Result |
| :--- | :---: | :---: | :---: | :---: |
| `tests/identity` | 14 | 0 | 14 | PASS |
| `tests/audit/sprint14` | 16 | 8 | 24 | PASS |
| `internal/engine/ownership` | 1 | 11 | 12 | PASS |
| `internal/engine/federation` | 8 | 0 | 8 | PASS |
| **TOTAL** | **39** | **19** | **58** | **ALL PASS** |

---

## 2. EXHAUSTIVE LIST OF TEST CASES & SUBJECT CLASSIFICATION

Every test case is categorized to distinguish explicit Organization assertions from subject-agnostic primitives, asset-level mechanics, or unclassified suites.

### Suite 1: `tests/identity` (14 Top-Level Tests, 0 Subtests)
1. `TestActiveKeyAuthorizationSequenceRules` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`: Validates sequence continuity and competing sequence rejection for active signing keys.
2. `TestThreeLevelDelegationAuthorityChain` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`: Validates 3-level scoped identity delegation depth constraints.
3. `TestRFC8785AuthoritativeIndependentConformanceCorpus` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates RFC 8785 JCS canonicalization across edge cases.
4. `TestRFC8785InvalidUnicodeFailClosedRejection` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates fail-closed rejection of invalid UTF-8 string sequences.
5. `TestSignatureInteroperabilityVector` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates Ed25519 signature interoperability across canonical byte payloads.
6. `TestRootLineageFailureMappings` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`: Validates deterministic error codes for corrupted lineage chains.
7. `TestRecoveryKeyDigestJSONPresence` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates tri-state recovery key digest JSON unmarshaling.
8. `TestVerify2StepRootRecovery` (PASS) — `[ORGANIZATION EXPLICIT]`: Validates 2-step root recovery protocol requiring non-null genesis recovery key digest.
9. `TestUnboundedRecoveryLineageDepth` (PASS) — `[ORGANIZATION EXPLICIT]`: Validates root recovery lineage traversal across depth transitions.
10. `TestClosedBaselineRegressionProtection` (PASS) — `[NOT CLASSIFIED]`: Validates non-regression against Sprint 10–13 baselines without evaluating subject types.
11. `TestDeriveSubjectID` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates SHA-256 derivation of `urn:nexa:id:...` from raw 32-byte Ed25519 public keys.
12. `TestVerifySubjectIDContinuity` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`: Validates continuity between genesis public key and Subject ID URN.
13. `TestVerificationPipelineVerified` (PASS) — `[ORGANIZATION EXPLICIT]`: Validates full 5-step `ExecutePipeline` specifically using a `SubjectTypeOrganization` assertion fixture.
14. `TestValidateRevocationKeyScope` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`: Validates scope checks for key revocation operations.

### Suite 2: `tests/audit/sprint14` (16 Top-Level Tests, 8 Nested Subtests)
#### Top-Level Tests:
1. `TestAuditActiveKeyAuthorizationSequenceRules` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`
2. `TestAuditThreeLevelDelegationAuthorityChain` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`
3. `TestAuditRevocationAuthorityValidation` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`
4. `TestAuditRFC8785IndependentJCSCorpus` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`
5. `TestAuditRFC8785InvalidUnicodeFailClosedRejection` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`
6. `TestAuditMultiStepLineageResolution` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`
7. `TestAuditLineageBranchingConflict` (PASS) — `[SUBJECT-AGNOSTIC MECHANISM]`
8. `TestAuditTriStateRecoveryCommitment` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`
9. `TestAudit2StepRecoveryProtocol` (PASS) — `[ORGANIZATION EXPLICIT]`
10. `TestAuditSprint10Regression` (PASS) — `[NOT CLASSIFIED]`
11. `TestAuditSprint11Regression` (PASS) — `[NOT CLASSIFIED]`
12. `TestAuditSprint112Regression` (PASS) — `[NOT CLASSIFIED]`
13. `TestAuditSprint12Regression` (PASS) — `[NOT CLASSIFIED]`
14. `TestAuditSprint13Regression` (PASS) — `[NOT CLASSIFIED]`
15. `TestAuditPublicSDKAdaptation` (PASS) — `[SDK ADAPTATION / NOT CLASSIFIED]`
16. `TestAuditSubjectIDDerivationAndInvariance` (PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`
#### Nested Subtests under `TestAuditRFC8785IndependentJCSCorpus`:
- `JCS-AUDIT-VEC-01` through `08` (8 subtests, all PASS) — `[SUBJECT-AGNOSTIC PRIMITIVE]`

### Suite 3: `internal/engine/ownership` (1 Top-Level Test, 11 Nested Subtests)
#### Top-Level Test:
1. `TestGoldenOwnershipScenarios` (PASS) — `[ASSET-LEVEL]`
#### Nested Subtests:
1. `OWN-CERT-01_And_02_ValidGenesisCertificate` (PASS) — `[ASSET-LEVEL / SCALAR]`
2. `OWN-CERT-05_InvalidCreatorSignatureRejection` (PASS) — `[ASSET-LEVEL / SCALAR]`
3. `OWN-TRANSFER-01_ValidUnilateralTransfer` (PASS) — `[ASSET-LEVEL / SCALAR]`
4. `OWN-HISTORY-01_SequentialLineageEvaluation` (PASS) — `[ASSET-LEVEL / SCALAR]`
5. `OWN-DELEGATION-01_And_04_ClosedScopeAllowlist` (PASS) — `[ASSET-LEVEL / SCALAR]`
6. `OWN-CONFLICT-01_MultiBranchConflictPreservation` (PASS) — `[ASSET-LEVEL / SCALAR]`
7. `OWN-COMPAT-01_LegacyAssetBackwardCompatibility` (PASS) — `[ASSET-LEVEL / SCALAR]`
8. `OWN-SECURITY-01_ReplayProtection` (PASS) — `[ASSET-LEVEL / SCALAR]`
9. `OWN-TRANSFER-02_UnauthorizedTransferRejection` (PASS) — `[ASSET-LEVEL / SCALAR]`
10. `OWN-FEDERATION-01A_MultiRegistryConsistentEvidence` (PASS) — `[ASSET-LEVEL / SCALAR]`
11. `OWN-FEDERATION-01B_MultiRegistryContradictoryValidEvidence` (PASS) — `[ASSET-LEVEL / SCALAR]`

### Suite 4: `internal/engine/federation` (8 Top-Level Tests, 0 Subtests)
1. `TestAssetIsolationForLocalOverride` (PASS) — `[FEDERATION / OVERLAY]`
2. `TestNonMutationOverlayInvariant` (PASS) — `[FEDERATION / OVERLAY]`
3. `TestExpiredAndNoTrustedRegistrySemantics` (PASS) — `[FEDERATION / FAIL-CLOSED]`
4. `TestUnpinnedRegistryFailClosedPolicy` (PASS) — `[FEDERATION / FAIL-CLOSED]`
5. `TestLevel1IdentityVerificationSuite` (PASS) — `[FEDERATION / IDENTITY]`
6. `TestNonMutationOverlayInvariantByteLevel` (PASS) — `[FEDERATION / OVERLAY]`
7. `TestGoActivePartialFederationSemantics` (PASS) — `[FEDERATION / CONSENSUS]`
8. `TestGoActiveRevokedConflictTraceability` (PASS) — `[FEDERATION / TRACEABILITY]`

---

## 3. RECONCILIATION OF TEST CLAIMS (B-SUP-02 & SUBJECT SCOPE)

### 3.1 Correction of Overbroad Claims
Previous documentation contained statements generalizing that all tests in `tests/identity/` and `tests/audit/sprint14/` were "Organization-specific". That characterization was inaccurate:
- Mathematical and serialization primitives (JCS RFC 8785, UTF-8 fail-closed, Ed25519 interoperability, Subject ID derivation) operate purely on byte payloads and public keys without subject classification (`[SUBJECT-AGNOSTIC PRIMITIVE]`).
- Algorithmic and sequence continuity tests (`TestActiveKeyAuthorizationSequenceRules`, etc.) validate sequence monotonic progression and conflict rejection regardless of subject type (`[SUBJECT-AGNOSTIC MECHANISM]`).
- Ownership tests (`internal/engine/ownership`) evaluate single-asset certificates and transfer events (`[ASSET-LEVEL]`).
- Federation tests (`internal/engine/federation`) evaluate multi-registry trust consensus and local overlay behavior (`[FEDERATION-LEVEL]`).
- Historical regression suites test baseline protection without differentiating subject types (`[NOT CLASSIFIED]`).

### 3.2 Where Organization Assertions Actually Reside
The presence of `SubjectTypeOrganization` is strictly confined to:
1. End-to-end identity assertion pipeline fixtures, notably `TestVerificationPipelineVerified` in `tests/identity/`.
2. Two-step root recovery test cases (`TestVerify2StepRootRecovery`, `TestAudit2StepRecoveryProtocol`), which require a non-null recovery key digest commitment defined at Organization genesis.

### 3.3 Bounded Findings and Strict Interpretive Limits
Based on the reconciled source and test evidence:
1. **Resolver Behavior:** `ResolveActiveSigningAuthorityAt` does not accept or evaluate `subject_type`; it operates on generic URN and active key authorization sequences.
2. **Pipeline Behavior:** `IdentityVerifier.ExecutePipeline` invokes the active key resolver identically for both `ORGANIZATION` and `INDIVIDUAL` subjects without branching.
3. **Test Scope Reality:** In the examined test suite, there are **0 dedicated end-to-end test cases** validating an `IdentityAssertion` with `subject_type: "INDIVIDUAL"`.
4. **Strict Boundaries:**
   - This finding does **NOT** prove that Individual Creator assertions succeed through end-to-end production flow.
   - This finding does **NOT** indicate that Individual Creators are blocked or rejected by the resolver.
   - Existing test suites prove only the capabilities explicitly tested; they do not prove Album Handling, Album Membership Authority, or Individual Creator end-to-end flows.

---

## 4. RAW TEST EXECUTION OUTPUT (FOR REPRODUCIBILITY)

```text
=== RUN   TestActiveKeyAuthorizationSequenceRules
--- PASS: TestActiveKeyAuthorizationSequenceRules (0.00s)
=== RUN   TestThreeLevelDelegationAuthorityChain
--- PASS: TestThreeLevelDelegationAuthorityChain (0.00s)
=== RUN   TestRFC8785AuthoritativeIndependentConformanceCorpus
--- PASS: TestRFC8785AuthoritativeIndependentConformanceCorpus (0.00s)
=== RUN   TestRFC8785InvalidUnicodeFailClosedRejection
--- PASS: TestRFC8785InvalidUnicodeFailClosedRejection (0.00s)
=== RUN   TestSignatureInteroperabilityVector
--- PASS: TestSignatureInteroperabilityVector (0.00s)
=== RUN   TestRootLineageFailureMappings
--- PASS: TestRootLineageFailureMappings (0.00s)
=== RUN   TestRecoveryKeyDigestJSONPresence
--- PASS: TestRecoveryKeyDigestJSONPresence (0.00s)
=== RUN   TestVerify2StepRootRecovery
--- PASS: TestVerify2StepRootRecovery (0.00s)
=== RUN   TestUnboundedRecoveryLineageDepth
--- PASS: TestUnboundedRecoveryLineageDepth (0.01s)
=== RUN   TestClosedBaselineRegressionProtection
--- PASS: TestClosedBaselineRegressionProtection (0.33s)
=== RUN   TestDeriveSubjectID
--- PASS: TestDeriveSubjectID (0.00s)
=== RUN   TestVerifySubjectIDContinuity
--- PASS: TestVerifySubjectIDContinuity (0.00s)
=== RUN   TestVerificationPipelineVerified
--- PASS: TestVerificationPipelineVerified (0.00s)
=== RUN   TestValidateRevocationKeyScope
--- PASS: TestValidateRevocationKeyScope (0.00s)
PASS
ok  	nexa/tests/identity	0.361s
=== RUN   TestAuditActiveKeyAuthorizationSequenceRules
--- PASS: TestAuditActiveKeyAuthorizationSequenceRules (0.00s)
=== RUN   TestAuditThreeLevelDelegationAuthorityChain
--- PASS: TestAuditThreeLevelDelegationAuthorityChain (0.00s)
=== RUN   TestAuditRevocationAuthorityValidation
--- PASS: TestAuditRevocationAuthorityValidation (0.00s)
=== RUN   TestAuditRFC8785IndependentJCSCorpus
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-01
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-02
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-03
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-04
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-05
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-06
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-07
=== RUN   TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-08
--- PASS: TestAuditRFC8785IndependentJCSCorpus (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-01 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-02 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-03 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-04 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-05 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-06 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-07 (0.00s)
    --- PASS: TestAuditRFC8785IndependentJCSCorpus/JCS-AUDIT-VEC-08 (0.00s)
=== RUN   TestAuditRFC8785InvalidUnicodeFailClosedRejection
[JCS-AUDIT-VEC-09] Invalid UTF-8 fail-closed rejection verified: JCS pre-marshal Unicode validation failed: invalid UTF-8 string byte sequence
--- PASS: TestAuditRFC8785InvalidUnicodeFailClosedRejection (0.00s)
=== RUN   TestAuditMultiStepLineageResolution
--- PASS: TestAuditMultiStepLineageResolution (0.01s)
=== RUN   TestAuditLineageBranchingConflict
--- PASS: TestAuditLineageBranchingConflict (0.00s)
=== RUN   TestAuditTriStateRecoveryCommitment
--- PASS: TestAuditTriStateRecoveryCommitment (0.00s)
=== RUN   TestAudit2StepRecoveryProtocol
--- PASS: TestAudit2StepRecoveryProtocol (0.00s)
=== RUN   TestAuditSprint10Regression
--- PASS: TestAuditSprint10Regression (0.00s)
=== RUN   TestAuditSprint11Regression
--- PASS: TestAuditSprint11Regression (0.00s)
=== RUN   TestAuditSprint112Regression
--- PASS: TestAuditSprint112Regression (0.00s)
=== RUN   TestAuditSprint12Regression
--- PASS: TestAuditSprint12Regression (0.00s)
=== RUN   TestAuditSprint13Regression
--- PASS: TestAuditSprint13Regression (0.40s)
=== RUN   TestAuditPublicSDKAdaptation
--- PASS: TestAuditPublicSDKAdaptation (0.00s)
=== RUN   TestAuditSubjectIDDerivationAndInvariance
--- PASS: TestAuditSubjectIDDerivationAndInvariance (0.00s)
PASS
ok  	nexa/tests/audit/sprint14	0.428s
=== RUN   TestGoldenOwnershipScenarios
=== RUN   TestGoldenOwnershipScenarios/OWN-CERT-01_And_02_ValidGenesisCertificate
=== RUN   TestGoldenOwnershipScenarios/OWN-CERT-05_InvalidCreatorSignatureRejection
=== RUN   TestGoldenOwnershipScenarios/OWN-TRANSFER-01_ValidUnilateralTransfer
=== RUN   TestGoldenOwnershipScenarios/OWN-HISTORY-01_SequentialLineageEvaluation
=== RUN   TestGoldenOwnershipScenarios/OWN-DELEGATION-01_And_04_ClosedScopeAllowlist
=== RUN   TestGoldenOwnershipScenarios/OWN-CONFLICT-01_MultiBranchConflictPreservation
=== RUN   TestGoldenOwnershipScenarios/OWN-COMPAT-01_LegacyAssetBackwardCompatibility
=== RUN   TestGoldenOwnershipScenarios/OWN-SECURITY-01_ReplayProtection
=== RUN   TestGoldenOwnershipScenarios/OWN-TRANSFER-02_UnauthorizedTransferRejection
=== RUN   TestGoldenOwnershipScenarios/OWN-FEDERATION-01A_MultiRegistryConsistentEvidence
=== RUN   TestGoldenOwnershipScenarios/OWN-FEDERATION-01B_MultiRegistryContradictoryValidEvidence
--- PASS: TestGoldenOwnershipScenarios (0.01s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-CERT-01_And_02_ValidGenesisCertificate (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-CERT-05_InvalidCreatorSignatureRejection (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-TRANSFER-01_ValidUnilateralTransfer (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-HISTORY-01_SequentialLineageEvaluation (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-DELEGATION-01_And_04_ClosedScopeAllowlist (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-CONFLICT-01_MultiBranchConflictPreservation (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-COMPAT-01_LegacyAssetBackwardCompatibility (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-SECURITY-01_ReplayProtection (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-TRANSFER-02_UnauthorizedTransferRejection (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-FEDERATION-01A_MultiRegistryConsistentEvidence (0.00s)
    --- PASS: TestGoldenOwnershipScenarios/OWN-FEDERATION-01B_MultiRegistryContradictoryValidEvidence (0.00s)
PASS
ok  	nexa/internal/engine/ownership	0.011s
=== RUN   TestAssetIsolationForLocalOverride
    evaluator_test.go:43: R-05 Asset Isolation Test Passed: Asset A override did NOT affect Asset B!
--- PASS: TestAssetIsolationForLocalOverride (0.00s)
=== RUN   TestNonMutationOverlayInvariant
    evaluator_test.go:97: R-06 Non-Mutation Overlay Invariant Test Passed!
--- PASS: TestNonMutationOverlayInvariant (0.00s)
=== RUN   TestExpiredAndNoTrustedRegistrySemantics
    evaluator_test.go:126: R-02 / R-03 Expired & No Trusted Registry Test Passed!
--- PASS: TestExpiredAndNoTrustedRegistrySemantics (0.00s)
=== RUN   TestUnpinnedRegistryFailClosedPolicy
    evaluator_test.go:154: Correction 5 Unpinned Registry Fail-Closed Policy Test Passed!
--- PASS: TestUnpinnedRegistryFailClosedPolicy (0.00s)
=== RUN   TestLevel1IdentityVerificationSuite
    evaluator_test.go:174: FC-04 Level 1 Identity Failure Verification Passed!
--- PASS: TestLevel1IdentityVerificationSuite (0.00s)
=== RUN   TestNonMutationOverlayInvariantByteLevel
    evaluator_test.go:220: FC-06 Byte-Level Non-Mutation Invariant Verified PASS!
--- PASS: TestNonMutationOverlayInvariantByteLevel (0.00s)
=== RUN   TestGoActivePartialFederationSemantics
    evaluator_test.go:251: C-02 Real Go ACTIVE + PARTIAL Test Passed!
--- PASS: TestGoActivePartialFederationSemantics (0.00s)
=== RUN   TestGoActiveRevokedConflictTraceability
    evaluator_test.go:286: C-03 Real ACTIVE + REVOKED -> CONFLICT Traceability Test Passed!
--- PASS: TestGoActiveRevokedConflictTraceability (0.00s)
PASS
ok  	nexa/internal/engine/federation	0.006s
```
