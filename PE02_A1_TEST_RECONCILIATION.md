# NEXA PE-02 A1 — TEST EXECUTION RECONCILIATION REPORT

- **Repository:** `whisnu/nexa`
- **Branch:** `main`
- **Commit SHA:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
- **Working Directory:** `/opt/antigravity/projects/nexa`
- **Test Command:**
  ```bash
  GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -count=1 -v ./tests/identity/... ./tests/audit/sprint14/... ./internal/engine/ownership/... ./internal/engine/federation/...
  ```
- **Exit Code:** `0` (ALL PASS)

---

## 1. RECONCILIATION OF PREVIOUS TEST COUNT ("43")

### 1.1 The Discrepancy
In the initial preliminary report, the summary statement noted:
> *"Total Test Cases Executed: 43 tests (43 PASS, 0 FAIL)"*
However, an inspection of the raw `go test` output across all four suites reveals:
- **39 lines** of top-level `=== RUN   Test...`
- **19 lines** of nested subtest `=== RUN   Test.../...`
- **39 lines** of top-level `--- PASS: Test...`
- **19 lines** of nested subtest `--- PASS: Test.../...`
- Total individual test invocations = **58 invocations**.

### 1.2 Mathematical Derivation of "43"
The figure "43" was derived from an unnormalized aggregation of three specific test suites in the preliminary handoff:
1. `tests/identity`: **14** top-level test functions.
2. `tests/audit/sprint14`: **18** assertions/tests counted historically (16 top-level test functions plus 2 standalone audit vectors).
3. `internal/engine/ownership`: **11** subtests executed within `TestGoldenOwnershipScenarios`.
4. Calculation: `14 + 18 + 11 = 43`.

**Why this was inaccurate:**
1. It mixed top-level test functions (in `tests/identity` and `tests/audit/sprint14`) with nested subtests (in `internal/engine/ownership`).
2. It completely omitted the **8 top-level tests** of `internal/engine/federation` from the sum.

### 1.3 Correct Normalized Test Inventory
- **Top-Level Tests:** **39** (all PASS)
- **Nested Subtests:** **19** (all PASS)
- **Total Test Invocations:** **58** (all PASS)
- **Failed / Skipped:** **0**

---

## 2. EXHAUSTIVE LIST OF TEST CASES & SUITES

### Suite 1: `tests/identity` (14 Top-Level Tests, 0 Subtests)
1. `TestActiveKeyAuthorizationSequenceRules` (PASS)
2. `TestThreeLevelDelegationAuthorityChain` (PASS)
3. `TestRFC8785AuthoritativeIndependentConformanceCorpus` (PASS)
4. `TestRFC8785InvalidUnicodeFailClosedRejection` (PASS)
5. `TestSignatureInteroperabilityVector` (PASS)
6. `TestRootLineageFailureMappings` (PASS)
7. `TestRecoveryKeyDigestJSONPresence` (PASS)
8. `TestVerify2StepRootRecovery` (PASS)
9. `TestUnboundedRecoveryLineageDepth` (PASS)
10. `TestClosedBaselineRegressionProtection` (PASS)
11. `TestDeriveSubjectID` (PASS)
12. `TestVerifySubjectIDContinuity` (PASS)
13. `TestVerificationPipelineVerified` (PASS)
14. `TestValidateRevocationKeyScope` (PASS)

### Suite 2: `tests/audit/sprint14` (16 Top-Level Tests, 8 Nested Subtests)
#### Top-Level Tests:
1. `TestAuditActiveKeyAuthorizationSequenceRules` (PASS)
2. `TestAuditThreeLevelDelegationAuthorityChain` (PASS)
3. `TestAuditRevocationAuthorityValidation` (PASS)
4. `TestAuditRFC8785IndependentJCSCorpus` (PASS)
5. `TestAuditRFC8785InvalidUnicodeFailClosedRejection` (PASS)
6. `TestAuditMultiStepLineageResolution` (PASS)
7. `TestAuditLineageBranchingConflict` (PASS)
8. `TestAuditTriStateRecoveryCommitment` (PASS)
9. `TestAudit2StepRecoveryProtocol` (PASS)
10. `TestAuditSprint10Regression` (PASS)
11. `TestAuditSprint11Regression` (PASS)
12. `TestAuditSprint112Regression` (PASS)
13. `TestAuditSprint12Regression` (PASS)
14. `TestAuditSprint13Regression` (PASS)
15. `TestAuditPublicSDKAdaptation` (PASS)
16. `TestAuditSubjectIDDerivationAndInvariance` (PASS)
#### Nested Subtests under `TestAuditRFC8785IndependentJCSCorpus`:
- `JCS-AUDIT-VEC-01` (PASS)
- `JCS-AUDIT-VEC-02` (PASS)
- `JCS-AUDIT-VEC-03` (PASS)
- `JCS-AUDIT-VEC-04` (PASS)
- `JCS-AUDIT-VEC-05` (PASS)
- `JCS-AUDIT-VEC-06` (PASS)
- `JCS-AUDIT-VEC-07` (PASS)
- `JCS-AUDIT-VEC-08` (PASS)

### Suite 3: `internal/engine/ownership` (1 Top-Level Test, 11 Nested Subtests)
#### Top-Level Test:
1. `TestGoldenOwnershipScenarios` (PASS)
#### Nested Subtests under `TestGoldenOwnershipScenarios`:
- `OWN-CERT-01_And_02_ValidGenesisCertificate` (PASS)
- `OWN-CERT-05_InvalidCreatorSignatureRejection` (PASS)
- `OWN-TRANSFER-01_ValidUnilateralTransfer` (PASS)
- `OWN-HISTORY-01_SequentialLineageEvaluation` (PASS)
- `OWN-DELEGATION-01_And_04_ClosedScopeAllowlist` (PASS)
- `OWN-CONFLICT-01_MultiBranchConflictPreservation` (PASS)
- `OWN-COMPAT-01_LegacyAssetBackwardCompatibility` (PASS)
- `OWN-SECURITY-01_ReplayProtection` (PASS)
- `OWN-TRANSFER-02_UnauthorizedTransferRejection` (PASS)
- `OWN-FEDERATION-01A_MultiRegistryConsistentEvidence` (PASS)
- `OWN-FEDERATION-01B_MultiRegistryContradictoryValidEvidence` (PASS)

### Suite 4: `internal/engine/federation` (8 Top-Level Tests, 0 Subtests)
1. `TestAssetIsolationForLocalOverride` (PASS)
2. `TestNonMutationOverlayInvariant` (PASS)
3. `TestExpiredAndNoTrustedRegistrySemantics` (PASS)
4. `TestUnpinnedRegistryFailClosedPolicy` (PASS)
5. `TestLevel1IdentityVerificationSuite` (PASS)
6. `TestNonMutationOverlayInvariantByteLevel` (PASS)
7. `TestGoActivePartialFederationSemantics` (PASS)
8. `TestGoActiveRevokedConflictTraceability` (PASS)

---

## 3. MAPPING OF TESTS TO TECHNICAL CLAIMS (GROUPS A–F)

| Group | Technical Claim | Direct Test Evidence | Exact Test Names |
| :--- | :--- | :--- | :--- |
| **A** | JCS RFC 8785 canonicalization & Ed25519 verification | `PASS` | `TestRFC8785AuthoritativeIndependentConformanceCorpus`, `TestSignatureInteroperabilityVector`, `TestAuditRFC8785IndependentJCSCorpus` |
| **A** | Deterministic Subject ID derivation & immutability | `PASS` | `TestDeriveSubjectID`, `TestVerifySubjectIDContinuity`, `TestAuditSubjectIDDerivationAndInvariance` |
| **A** | Independent trust-anchor pinning store | **NO TEST (GAP)** | Zero tests exist because no trust-anchor store is implemented in `IdentityVerifier`. |
| **B** | Organization 2-step root recovery protocol | `PASS` | `TestVerify2StepRootRecovery`, `TestAudit2StepRecoveryProtocol`, `TestRecoveryKeyDigestJSONPresence` |
| **B** | Organization monotonic Level-1 active key sequence | `PASS` | `TestActiveKeyAuthorizationSequenceRules`, `TestAuditActiveKeyAuthorizationSequenceRules` |
| **B** | Individual Creator key rotation / recovery | **NO TEST (GAP)** | Zero tests exist with `SubjectTypeIndividual`; tests exclusively exercise Organization identity. |
| **C** | Scalar per-asset `OwnershipCertificate` creation/verification | `PASS` | `TestGoldenOwnershipScenarios/OWN-CERT-01_And_02_ValidGenesisCertificate` |
| **C** | Album-wide ownership / publisher-origin authority | **NO TEST (GAP)** | Zero tests exist for multi-asset aggregation or album ownership. |
| **D** | Registry identity verification & pinned fail-closed policy | `PASS` | `TestLevel1IdentityVerificationSuite`, `TestUnpinnedRegistryFailClosedPolicy` |
| **D** | Multi-registry conflict & live federation consensus | `PASS` | `TestGoActiveRevokedConflictTraceability`, `TestExpiredAndNoTrustedRegistrySemantics` |
| **D** | Offline self-contained Registry proof verification | **NO TEST (GAP)** | Zero tests exist; offline execution immediately results in `UNKNOWN / INCOMPLETE`. |
| **E** | Revocation boolean evaluation in identity pipeline | `PASS` | `TestVerificationPipelineVerified`, `TestAuditRevocationAuthorityValidation` |
| **E** | `RegistryKeyRevocationList` verification & Dual-Horizon time | **NO TEST (GAP)** | Zero verifier tests exist for `ListSignature` or `revoked_at` vs `recorded_at`. |
| **F** | 3-level generic scoped delegation & depth limits | `PASS` | `TestThreeLevelDelegationAuthorityChain`, `TestAuditThreeLevelDelegationAuthorityChain` |
| **F** | Capability `ALBUM_MEMBERSHIP_SIGNING` & `album_id` binding | **NO TEST (GAP)** | Zero tests exist; capability token and album scoping do not exist in the codebase. |

---

## 4. RAW TEST EXECUTION OUTPUT

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
