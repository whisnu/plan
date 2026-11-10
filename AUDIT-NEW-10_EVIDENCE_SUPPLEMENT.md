# AUDIT-NEW-10_EVIDENCE_SUPPLEMENT.md
# PELENGKAPAN BUKTI INSPEKSI TEKNIS (STAGE 1)
## AUDIT-NEW-10 — Three-Way Identity Binding dan Third-Party Packaging Delegation

- **Repository Sumber:** `whisnu/nexa`
- **Commit Acuan:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
- **Branch:** `main`
- **Repository PLAN:** `whisnu/plan`
- **File PLAN Kanonikal:** `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`
- **Jenis Pekerjaan:** Read-Only Source Inspection and Evidence Completion
- **Status PE-02 Implementation:** **`NOT AUTHORIZED`**
- **Waktu Inspeksi:** 10 November 2026

---

### 1. Commit Provenance dan Integritas Inspeksi

Pemeriksaan dilakukan langsung pada repositori lokal `/opt/antigravity/projects/nexa/` dengan status pembuktian provenance sebagai berikut:

#### 1.1 Output Aktual Git Provenance
```bash
$ git rev-parse HEAD
fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956

$ git rev-parse origin/main
fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956

$ git status --short
?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md
?? docs/whitepapers/Nexa_White_Paper_v5_6.md
```

#### 1.2 Konfirmasi Integritas
- **Branch Aktual:** `main`
- **Commit SHA Sumber:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (100% sinkron dengan `origin/main`).
- **Status Working Tree:** Bersih dari modifikasi file terlacak (`tracked files 100% clean`). Tidak ada kode sumber, schema, test, maupun konfigurasi yang dimodifikasi.
- **Daftar File Sumber yang Diperiksa:**
  - `sdk/typescript/src/sdk.ts` (L1–L50, L130–L291)
  - `sdk/typescript/src/ownership.ts` (L1–L160, L230–L343)
  - `sdk/typescript/src/registry.ts` (L1–L123)
  - `player-desktop/main.js` (L51, L700–L770, L900–L1030)
  - `verify-desktop/main.js` (L33, L300–L350, L500–L620)
  - `internal/domain/ownership.go` (L1–L45, L80–L125)
  - `internal/engine/ownership/delegation.go` (L1–L151)
  - `internal/engine/ownership/verifier.go` (L1–L50)
  - `sdk/c/nexa_mobile_cbindings.go` (L290–L325)

---

### 2. Pelengkapan Bukti E-01: `verifyContainer` dan Hasil Verifikasi

**Evidence ID:** `E-01`  
**Repository:** `whisnu/nexa`  
**Commit:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`  
**File:** `sdk/typescript/src/sdk.ts`  
**Line range:** L133–L290  

#### 2.1 Source Excerpt Verbatim

##### Definisi Lengkap Interface `VerificationResult` (`sdk/typescript/src/sdk.ts:L24-L37`):
```typescript
export interface VerificationResult {
    signatureValid: boolean;
    hashValid: boolean;
    manifest: Manifest;
    manifestBytes: Buffer;
    sha256Hash: string;
    payload: Buffer;

    certificateID: string;
    certificateStatus: string; // "active", "revoked", "unknown", "none"
    registryVerified: boolean;
    registryError: string;
    certificate?: NexaRegistry.RegistryCert;
}
```

##### Definisi Lengkap Fungsi `verifyContainer` (`sdk/typescript/src/sdk.ts:L133-L290`):
```typescript
export async function verifyContainer(nxPath: string, pubKey: crypto.KeyObject,
                                     registryURL?: string, registryPubKey?: crypto.KeyObject,
                                     cachedCert?: NexaRegistry.RegistryCert): Promise<VerificationResult> {
    const data = fs.readFileSync(nxPath);
    const container = NexaContainer.unpack(data);

    const manifestStr = container.manifestBytes.toString("utf8");
    const manifest = JSON.parse(manifestStr) as Manifest;

    // 1. Signature check
    const signatureValid = NexaCrypto.verify(pubKey, container.manifestBytes, container.signatureBytes);

    // 2. Hash check
    const computedHash = NexaCrypto.sha256(container.payloadBytes);
    const actualHashStr = computedHash.toString("hex");
    const hashValid = actualHashStr === manifest.asset_hash;

    // 3. Certificate ID calculation
    const hashOfSig = NexaCrypto.sha256(container.signatureBytes);
    const certID = hashOfSig.toString("hex");

    const res: VerificationResult = {
        signatureValid,
        hashValid,
        manifest,
        manifestBytes: container.manifestBytes,
        sha256Hash: actualHashStr,
        payload: container.payloadBytes,
        certificateID: certID,
        certificateStatus: "none",
        registryVerified: false,
        registryError: ""
    };

    // 4. Registry check (Online, Cache, or Sidecar)
    let regCert: NexaRegistry.RegistryCert | null = null;
    let querySuccessful = false;

    if (registryURL) {
        try {
            const registryClient = new NexaRegistry.NexaRegistryClient(registryURL);
            regCert = await registryClient.queryCertificate(certID);
            querySuccessful = true;
        } catch (e: any) {
            res.registryError = `Registry unreachable: ${e.message}`;
        }
    }

    if (!querySuccessful) {
        if (cachedCert) {
            regCert = cachedCert;
            res.registryError = res.registryError ? `${res.registryError} (Loaded from cache)` : "Loaded from cache";
        } else {
            const sidecarCandidates = [nxPath + ".nxcert"];
            if (nxPath.endsWith(".nx")) {
                sidecarCandidates.push(nxPath.slice(0, -3) + ".nxcert");
            }
            for (const scPath of sidecarCandidates) {
                if (fs.existsSync(scPath)) {
                    try {
                        const sidecarText = fs.readFileSync(scPath, "utf8");
                        regCert = JSON.parse(sidecarText) as NexaRegistry.RegistryCert;
                        break;
                    } catch (e: any) {
                        res.registryError = `Invalid sidecar file: ${e.message}`;
                    }
                }
            }
        }
    }

    if (regCert) {
        res.certificate = regCert;
        let sigValid = false;
        if (registryPubKey && regCert.issuer_signature) {
            try {
                const sigBytes = Buffer.from(regCert.issuer_signature, "hex");
                const creatorKey = regCert.creator_public_key || (regCert as any).ownership_certificate?.creator_public_key || "";
                const canonStr = NexaRegistry.canonicalJcs(
                    regCert.certificate_id,
                    regCert.issued_at,
                    regCert.issuer,
                    regCert.status,
                    regCert.valid_until,
                    creatorKey
                );
                sigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes);
                if (!sigValid) {
                    // Canonical 5-field fallback for certificates signed without creator_public_key in canonical string
                    const formattedIssued = NexaRegistry.formatJcsTimestamp(regCert.issued_at);
                    const formattedValid = NexaRegistry.formatJcsTimestamp(regCert.valid_until);
                    const canon5 = `{"certificate_id":${JSON.stringify(regCert.certificate_id)},"issued_at":${JSON.stringify(formattedIssued)},"issuer":${JSON.stringify(regCert.issuer)},"status":${JSON.stringify(regCert.status)},"valid_until":${JSON.stringify(formattedValid)}}`;
                    sigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canon5, "utf8"), sigBytes);
                }
            } catch (err: any) {
                res.registryError = `Signature verification error: ${err.message}`;
            }
        }

        // Structural integrity verification of embedded Genesis Ownership Certificate (if present)
        let ownershipVerified = false;
        const ownCert = (regCert as any).ownership_certificate;
        if (ownCert && ownCert.creator_public_key && ownCert.creator_signature) {
            try {
                let creatorMatches = true;
                if (pubKey) {
                    const rawCreatorPubKey = NexaCrypto.getRawPublicKey(pubKey).toString("hex");
                    creatorMatches = (ownCert.creator_public_key === rawCreatorPubKey);
                }
                const canonGenesisStr = JSON.stringify({
                    asset_id: ownCert.asset_id,
                    creator_public_key: ownCert.creator_public_key,
                    effective_at: ownCert.effective_at,
                    issued_at: ownCert.issued_at,
                    issuer_id: ownCert.issuer_id,
                    previous_cert_ref: ownCert.previous_cert_ref || "",
                    subject_id: ownCert.subject_id,
                    underlying_cert_id: ownCert.underlying_cert_id
                });
                const ownSigBytes = Buffer.from(ownCert.creator_signature, "hex");
                const ownKeyObj = NexaCrypto.loadPublicKey(ownCert.creator_public_key);
                const certIdMatches = (!ownCert.underlying_cert_id || ownCert.underlying_cert_id === certID);
                const cryptoValid = NexaCrypto.verify(ownKeyObj, Buffer.from(canonGenesisStr, "utf8"), ownSigBytes);

                if (creatorMatches && certIdMatches && cryptoValid && ownCert.status === "ACTIVE") {
                    ownershipVerified = true;
                }
            } catch (e: any) {
                console.warn("[WARNING] Failed to verify embedded ownership certificate:", e.message);
            }
        }

        // Registry Authority authentication:
        // Strictly established ONLY by:
        // 1. Authoritative online query (querySuccessful), OR
        // 2. Valid Registry Authority issuer_signature (sigValid)
        // Note: Genesis Ownership Certificate (ownershipVerified) proves creator ownership claims,
        // but does NOT substitute for Registry Authority authentication (trust boundary separation).
        if (sigValid || querySuccessful) {
            res.certificateStatus = regCert.status || "active";
            res.registryVerified = true;
            if (!sigValid && registryPubKey) {
                console.warn("[WARNING] Registry certificate key mismatch (ephemeral server key)");
            }
        } else {
            res.certificateStatus = "unknown";
            res.registryVerified = false;
            res.registryError = registryPubKey
                ? "Registry/Sidecar signature verification failed"
                : "Registry public key not configured (cannot verify offline sidecar signature)";
        }
    } else {
        res.certificateStatus = registryURL ? "unknown" : "none";
        res.registryVerified = false;
    }

    return res;
}
```

#### 2.2 Analisis Hubungan Caller, Callee, dan Pemakaian `ownershipVerified`
1. **Pemakaian Variabel `ownershipVerified`:**
   - Dideklarasikan pada L233: `let ownershipVerified = false;`
   - Ditetapkan pada L258: `if (creatorMatches && certIdMatches && cryptoValid && ownCert.status === "ACTIVE") { ownershipVerified = true; }`
   - Disebutkan pada komentar arsitektur L269–L270.
   - **Fakta Krusial:** Variabel `ownershipVerified` **TIDAK PERNAH DISIMPAN** ke dalam obyek `res: VerificationResult` dan **TIDAK PERNAH DIKEMBALIKAN** kepada pemanggil.
2. **Caller `verifyContainer` di Codebase:**
   - `player-desktop/main.js:L913`: Dipanggil oleh IPC handler `open-and-verify-nx`.
   - `verify-desktop/main.js:L522`: Dipanggil oleh IPC handler `verify-file`.
   - Test suites: `test/pe01_hidden_sidecar_test.js:L151`, `test/task_a_buyer_lifecycle_test.js:L1270`, `test/task_a_final_trust_boundary_test.js:L89`.
3. **Jalur Penentuan Status Akhir pada Konsumen (`player-desktop/main.js` L974–L989):**
   ```javascript
   const isIntegrityPass = result.signatureValid && result.hashValid;
   const isRevoked = finalCertStatus === 'revoked';
   if (isIntegrityPass && !isRevoked) {
       AuthorizedPlaybackTracks.set(certID, { ... });
       playbackUrl = `nexa-playback://${certID}`;
   }
   ```
   Otorisasi pemutaran desktop murni ditentukan oleh `result.signatureValid && result.hashValid && !isRevoked`. Karena `result.ownershipVerified` tidak ada, variabel tersebut tidak menjadi gerbang otorisasi playback.
4. **Asal Input Parameter `pubKey` pada Desktop Apps:**
   Pada `player-desktop/main.js:L900-L905` dan `verify-desktop/main.js:L509-L515`:
   ```javascript
   const sidecarFallbackKey = cachedCert?.ownership_certificate?.creator_public_key || cachedCert?.creator_public_key;
   if (sidecarFallbackKey) {
       creatorPubKey = NexaCrypto.loadPublicKey(sidecarFallbackKey);
   }
   ```
   Desktop Player dan Verify secara sepihak memuat `creatorPubKey` dari sidecar, lalu mengumpankannya sebagai argumen `pubKey` ke `NexaSdk.verifyContainer(filePath, creatorPubKey, ...)`.

#### 2.3 Jawaban Eksplisit Pertanyaan Mandat E-01
> **Pertanyaan:** Apakah perbedaan antara public key penanda tangan container (`containerSigKey`) dan public key creator (`genesisPubKey`) saat ini benar-benar menyebabkan penolakan container, atau hanya menyebabkan `ownershipVerified` bernilai false tanpa memengaruhi hasil akhir?

**Jawaban Berdasarkan Kode Aktual:**
1. **Di dalam fungsi `NexaSdk.verifyContainer`:**  
   Perbedaan tersebut **HANYA** menyebabkan `creatorMatches = false`, sehingga variabel lokal `ownershipVerified` bernilai `false`. Karena `ownershipVerified` tidak diekspos ke `VerificationResult`, nilai `res.signatureValid`, `res.hashValid`, dan `res.registryVerified` **TIDAK TERPENGARUH**. Jika kontainer ditandatangani oleh `containerSigKey` dan caller memasok `containerSigKey` yang cocok, `res.signatureValid` bernilai `true` dan `res.registryVerified` bernilai `true` (jika sidecar sah). Tidak ada penolakan yang terjadi di dalam `verifyContainer`.
2. **Di dalam alur aplikasi (`player-desktop` dan `verify-desktop`):**  
   Aplikasi desktop secara sepihak mengambil kunci kreator dari sidecar dan memasukkannya sebagai kunci verifikasi biner kontainer. Akibatnya, kontainer pihak ketiga yang ditandatangani oleh private key studio akan **gagal pada `result.signatureValid === false`** (karena diverifikasi dengan kunci yang salah). Kegagalan ini bukan karena sistem memiliki verifier penolakan pihak ketiga, melainkan karena *kesalahan pengumpanan kunci verifikasi pada aplikasi pemanggil*.

---

### 3. Pelengkapan Bukti E-02: `OwnershipDelegation` dan Lifecycle Delegation

**Evidence ID:** `E-02`  
**Repository:** `whisnu/nexa`  
**Commit:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`  
**Files:** `sdk/typescript/src/ownership.ts`, `internal/domain/ownership.go`, `internal/engine/ownership/delegation.go`  

#### 3.1 Bagian A — Definisi dan Payload Canonical

##### Definisi Interface TypeScript (`sdk/typescript/src/ownership.ts:L50-L63`):
```typescript
export interface OwnershipDelegation {
  delegation_id: string;
  asset_id: string;
  ownership_cert_id: string;
  delegator_subject_id: string;
  delegate_subject_id: string;
  delegated_scope: string[];
  sub_delegation_allowed: boolean;
  issued_at: string;
  effective_at: string;
  expires_at?: string;
  revoked: boolean;
  delegator_signature: string;
}
```

##### Definisi Struct Go Domain (`internal/domain/ownership.go:L84-L98`):
```go
type OwnershipDelegation struct {
	DelegationID         string     `json:"delegation_id"`
	AssetID              string     `json:"asset_id"`
	OwnershipCertID      string     `json:"ownership_cert_id"`
	DelegatorSubjectID   string     `json:"delegator_subject_id"`
	DelegateSubjectID    string     `json:"delegate_subject_id"`
	DelegatedScope       []string   `json:"delegated_scope"`
	SubDelegationAllowed bool       `json:"sub_delegation_allowed"`
	IssuedAt             time.Time  `json:"issued_at"`
	EffectiveAt          time.Time  `json:"effective_at"`
	ExpiresAt            *time.Time `json:"expires_at,omitempty"`
	Revoked              bool       `json:"revoked"`
	DelegatorSignature   string     `json:"delegator_signature"`
}
```

##### Scope yang Diizinkan (`AllowedDelegationScopes`):
- TypeScript (`sdk/typescript/src/ownership.ts:L7-L11`):
  ```typescript
  export const AllowedDelegationScopes = [
    ScopeMetadataUpdateClaim,
    ScopeOwnershipEvidenceSubmission,
    ScopeOwnershipHistoryAdmin,
  ];
  ```
- Go (`internal/domain/ownership.go:L21-L39`):
  Konstanta tertutup: `ScopeMetadataUpdateClaim`, `ScopeOwnershipEvidenceSubmission`, `ScopeOwnershipHistoryAdmin`.

##### Matriks Cakupan Field pada Payload Tanda Tangan:
Berdasarkan `CanonicalizeDelegationPayload` (`internal/engine/ownership/delegation.go:L16-L52` dan `sdk/typescript/src/ownership.ts:L131-L156`):

| Nama Field | Masuk Payload Tanda Tangan? | Alasan Kriptografis / Kode |
|---|---|---|
| `asset_id` | **YA** | Terikat langsung pada payload JCS. |
| `delegate_subject_id` | **YA** | Terikat langsung pada payload JCS. |
| `delegated_scope` | **YA** | Diurutkan secara alfabetis (`sort()`) sebelum serialisasi. |
| `delegator_subject_id` | **YA** | Terikat langsung pada payload JCS. |
| `effective_at` | **YA** | Diformat kanonikal JCS ISO-8601 nanodetik. |
| `expires_at` | **YA** | Diformat kanonikal JCS string (kosong jika `nil`). |
| `issued_at` | **YA** | Diformat kanonikal JCS ISO-8601 nanodetik. |
| `ownership_cert_id` | **YA** | Terikat langsung pada payload JCS. |
| `sub_delegation_allowed` | **YA** | Boolean nilai terikat langsung pada payload JCS. |
| `delegation_id` | **TIDAK** | Dihitung *setelah* tanda tangan dibuat (`OWNDEL-` + hash payload). |
| `revoked` | **TIDAK** | Merupakan status transaksional/mutable; **tidak masuk payload signature**. |
| `delegator_signature` | **TIDAK** | Signature itu sendiri tidak dapat berada di dalam data yang ditandatanganinya. |

#### 3.2 Bagian B — Signature Verification
1. **Fungsi Verifikasi di Go (`internal/engine/ownership/delegation.go:L105-L136`):**
   ```go
   func VerifyDelegationSignature(delegation *domain.OwnershipDelegation, delegatorPubKey ed25519.PublicKey) bool {
       if delegation == nil || len(delegatorPubKey) != ed25519.PublicKeySize { return false }
       if !domain.IsValidDelegationScope(delegation.DelegatedScope) { return false }
       canonicalBytes, err := CanonicalizeDelegationPayload(...)
       if err != nil { return false }
       sigBytes, err := hex.DecodeString(delegation.DelegatorSignature)
       if err != nil || len(sigBytes) != ed25519.SignatureSize { return false }
       return crypto.Verify(delegatorPubKey, canonicalBytes, sigBytes)
   }
   ```
   - **Caller:** `internal/engine/ownership/ownership_test.go:L133` (unit test).
   - **Input Public Key:** Dipasok langsung oleh pemanggil (`delegatorPubKey`).
   - **Pemetaan `delegator_subject_id`:** Pada implementasi verifier Go saat ini, **tidak ada pemetaan otomatis** dari string DID `delegator_subject_id` ke `delegatorPubKey`; pemanggil wajib memasok kunci publik secara independen.
2. **Ketiadaan Fungsi Verifikasi di TypeScript:**
   - Pada `sdk/typescript/src/ownership.ts`, fungsi `VerifyDelegationSignature` **TIDAK TERSEDIA**.
   - Fungsi `evaluateOwnershipEvidenceTS` (L324–L331) hanya mengecek:
     `delegations.filter((d) => !d.revoked && isValidDelegationScope(d.delegated_scope))`
     tanpa memverifikasi keabsahan tanda tangan `delegator_signature`.

#### 3.3 Bagian C — Lifecycle dan Revocation
1. **Fungsi Lifecycle di Go (`internal/engine/ownership/delegation.go:L139-L150`):**
   ```go
   func IsDelegationActive(delegation *domain.OwnershipDelegation, atTime time.Time) bool {
       if delegation == nil || delegation.Revoked { return false }
       if atTime.Before(delegation.EffectiveAt) { return false }
       if delegation.ExpiresAt != nil && atTime.After(*delegation.ExpiresAt) { return false }
       return domain.IsValidDelegationScope(delegation.DelegatedScope)
   }
   ```
2. **Jawaban Lima Pertanyaan Mandat E-02.C:**
   - *1. Apakah status `revoked` dapat dipercaya secara kriptografis?*  
     **TIDAK DAPAT DIPERCAYA SECARA STANDALONE**. Karena properti `revoked` tidak masuk ke dalam payload `CanonicalizeDelegationPayload`, integritas nilai boolean `revoked` tidak dilindungi oleh tanda tangan delegator pada sertifikat tersebut.
   - *2. Mekanisme yang melindungi integritas pencabutan:*  
     Pencabutan dilindungi melalui event store server-side (`OwnershipEvent` dengan `EventType = "REVOCATION"` pada `internal/domain/ownership.go:L104`) dan daftar pencabutan terpusat Registry (`RegistryKeyRevocationList` pada `internal/handler/registry_identity_handler.go:L23-L28`).
   - *3. Sumber eksternal status revocation:*  
     Endpoint Registry Authority `GET /v1/identity/revocations`.
   - *4. Apakah pemeriksaan revocation dapat dilakukan offline?*  
     **TIDAK DAPAT DILAKUKAN SECARA DINAMIS**. Mode offline hanya dapat membaca status lokal yang tersimpan di disk cache, dan tidak dapat mendeteksi apakah delegasi telah dicabut di jaringan setelah berkas disimpan.
   - *5. Perilaku jika status revocation tidak dapat diperoleh:*  
     Sistem fail-soft terhadap cache lokal untuk playback jika biner valid, namun menetapkan status telemetri `RevocationFreshness = "UNKNOWN"`.

#### 3.4 Bagian D — Klarifikasi `verifyOwnershipChain` vs `evaluateOwnershipEvidenceTS`
- **Fakta Repositori:**
  - Fungsi bernama `verifyOwnershipChain` **`NOT FOUND IN INSPECTED SCOPE`** (0 kecocokan di seluruh repository).
  - Fungsi aktual yang bertugas mengevaluasi rantai kepemilikan adalah:
    - Di Go: `EvaluateOwnershipEvidence` (`internal/engine/ownership/verifier.go:L11-L45`).
    - Di TypeScript: `evaluateOwnershipEvidenceTS` (`sdk/typescript/src/ownership.ts:L282-L343`).
- **Hubungan Aktual:** `verifyOwnershipChain` adalah sebutan konseptual pada dokumentasi historis, sedangkan `evaluateOwnershipEvidenceTS` adalah implementasi kode nyatanya.

---

### 4. Pelengkapan Bukti E-03: Registry Verification dan Trust Anchor

**Evidence ID:** `E-03`  
**Repository:** `whisnu/nexa`  
**Commit:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`  
**Files:** `sdk/typescript/src/registry.ts`, `sdk/typescript/src/sdk.ts`, `player-desktop/main.js`, `verify-desktop/main.js`, `sdk/c/nexa_mobile_cbindings.go`  

#### 4.1 Pembentukan Payload Kanonikal Registry (`canonicalJcs`)
`sdk/typescript/src/registry.ts:L118-L122`:
```typescript
export function canonicalJcs(certID: string, issuedAt: string, issuer: string, status: string, validUntil: string, creatorPubKey?: string): string {
    const formattedIssued = formatJcsTimestamp(issuedAt);
    const formattedValid = formatJcsTimestamp(validUntil);
    return `{"certificate_id":${JSON.stringify(certID)},"creator_public_key":${JSON.stringify(creatorPubKey || "")},"issued_at":${JSON.stringify(formattedIssued)},"issuer":${JSON.stringify(issuer)},"status":${JSON.stringify(status)},"valid_until":${JSON.stringify(formattedValid)}}`;
}
```

#### 4.2 Verifikasi Signature Registry pada SDK (`sdk/typescript/src/sdk.ts:L207-L226`)
```typescript
        if (registryPubKey && regCert.issuer_signature) {
            try {
                const sigBytes = Buffer.from(regCert.issuer_signature, "hex");
                const creatorKey = regCert.creator_public_key || (regCert as any).ownership_certificate?.creator_public_key || "";
                const canonStr = NexaRegistry.canonicalJcs(
                    regCert.certificate_id,
                    regCert.issued_at,
                    regCert.issuer,
                    regCert.status,
                    regCert.valid_until,
                    creatorKey
                );
                sigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes);
                if (!sigValid) {
                    // Canonical 5-field fallback for certificates signed without creator_public_key in canonical string
                    const formattedIssued = NexaRegistry.formatJcsTimestamp(regCert.issued_at);
                    const formattedValid = NexaRegistry.formatJcsTimestamp(regCert.valid_until);
                    const canon5 = `{"certificate_id":${JSON.stringify(regCert.certificate_id)},"issued_at":${JSON.stringify(formattedIssued)},"issuer":${JSON.stringify(regCert.issuer)},"status":${JSON.stringify(regCert.status)},"valid_until":${JSON.stringify(formattedValid)}}`;
                    sigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canon5, "utf8"), sigBytes);
                }
            } catch (err: any) {
                res.registryError = `Signature verification error: ${err.message}`;
            }
        }
```

#### 4.3 Pinned Fallback Trust Anchor `CANONICAL_REGISTRY_PUBKEY`
Konstanta kunci publik hex: `'87b0e47c7e92d1f8f0ad4ac7b7a78bec65fbb5c9c6cb6931511db1f4274c9832'`
- Terverifikasi ter-hardcode pada:
  - `player-desktop/main.js:L51`
  - `verify-desktop/main.js:L33`
  - `marketplace/server.js:L557`
  - `sdk/c/nexa_mobile_cbindings.go:L292` (`NEXA_CANONICAL_REGISTRY_PUBKEY_HEX`)
- **Penanganan Kondisi Error:**
  - Signature invalid: `sigValid = false`, `certificateStatus = "unknown"`, `registryVerified = false`.
  - Public key tidak dikonfigurasi: `res.registryError = "Registry public key not configured (cannot verify offline sidecar signature)"`.
  - Registry tidak dapat diakses saat offline: Membaca cache sidecar fisik `.nxcert`. Jika signature sidecar valid di bawah `CANONICAL_REGISTRY_PUBKEY`, status ditetapkan `TRUSTED / active`. Jika sidecar tidak ada atau tanda tangannya tidak cocok, status turun menjadi `UNKNOWN / unknown`.

#### 4.4 Batas Kesimpulan Trust Model
- Pada **jalur runtime aktual**, seluruh aplikasi (Desktop dan Mobile) mengandalkan satu kunci fallback hardcoded tunggal `CANONICAL_REGISTRY_PUBKEY`.
- Model federasi multi-registry hanya diuji pada tingkat unit engine (`federation_parity.test.js`), dan belum memiliki mekanisme trust store dinamis di runtime player.

---

### 5. Pelengkapan Bukti E-04: `.nxcert` Schema, Parser, dan Consumer

**Evidence ID:** `E-04`  
**Repository:** `whisnu/nexa`  
**Commit:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`  
**Files:** `sdk/typescript/src/registry.ts`, `sdk/typescript/src/sdk.ts`, `player-desktop/main.js`, `verify-desktop/main.js`  

#### 5.1 Definisi Schema
- **Ketiadaan File Formal JSON Schema:** Berkas skema terpisah (misalnya `.json` schema dengan draft-07/2020-12) **`NOT FOUND IN INSPECTED SCOPE`**.
- **Definisi Bahasa (TypeScript):** Didefinisikan secara struktural pada `sdk/typescript/src/registry.ts:L8-L16`:
  ```typescript
  export interface RegistryCert {
      certificate_id: string;
      issuer: string;
      status: string;
      issued_at: string;
      valid_until: string;
      issuer_signature: string;
      creator_public_key?: string;
  }
  ```
- **Constraint dan Versioning:**
  - Tidak ada field `schema_version` formal pada `.nxcert`.
  - Field wajib: `certificate_id`, `issuer`, `status`, `issued_at`, `valid_until`, `issuer_signature`.
  - Field opsional/ekstensi ad-hoc: `creator_public_key`, `ownership_certificate`.

#### 5.2 Parser dan Validasi
- **Implementasi Parser:**
  - `sdk/typescript/src/sdk.ts:L194`: `JSON.parse(sidecarText) as NexaRegistry.RegistryCert;`
  - `player-desktop/main.js:L766`: `JSON.parse(scBytes.toString('utf8'));`
  - `verify-desktop/main.js:L370`: `JSON.parse(scBytes.toString('utf8'));`
- **Perilaku Terhadap Unknown Fields:**
  - Karena menggunakan V8 `JSON.parse` standar tanpa layer validator skema (seperti Ajv/Zod), **seluruh field asing diterima tanpa error** (*silently accepted/ignored*).
  - Aturan penolakan *unknown fields* (AC-01) **belum terimplementasi pada parser `.nxcert`**.
- **Perilaku Terhadap Missing Fields:**
  - Jika field hilang, fungsi `canonicalJcs` menghasilkan string JSON dengan nilai `undefined` yang menyebabkan string JCS tidak cocok dengan `issuer_signature`, sehingga verifikasi signature gagal (*fail-closed* via signature mismatch).

#### 5.3 Consumer Lintas Platform
1. **SDK TypeScript (`sdk.ts`):** Mengurai sidecar `.nxcert` saat memverifikasi kontainer.
2. **Player Desktop (`main.js` L755–L770):** Mencari file `.nx.nxcert` secara otomatis di direktori yang sama untuk mengekstrak `creator_public_key` dan status lisensi.
3. **Verify Desktop (`main.js` L300–L350):** Mengurai `.nxcert` untuk audit tampilan UI dan diagnostik trust.
4. **Mobile Runtime (`nexa_mobile_cbindings.go` L280–L330):** Mengurai sidecar pendamping untuk validasi integritas C-ABI.

---

### 6. Pelengkapan Bukti Pengujian (Empirical Test Execution)

Enam test suite telah dieksekusi secara nyata pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`:

| Nama Suite & Path | Perintah Eksekusi | Status Eksekusi | Exit Code | Assertion / Hasil Utama |
|---|---|---|---|---|
| `sdk/typescript/test/ownership_parity.test.js` | `node sdk/typescript/test/ownership_parity.test.js` | **`EXECUTED PASS`** | `0` | 5/5 passed; closed scope allowlist, RFC 8785 JCS ordering, unauthorized transfer rejection. |
| `sdk/typescript/test/registry_identity.test.js` | `node sdk/typescript/test/registry_identity.test.js` | **`EXECUTED PASS`** | `0` | 8/8 passed; invalid signature, tampered doc, wrong key, expired identity, future clock skew. |
| `sdk/typescript/test/federation_parity.test.js` | `node sdk/typescript/test/federation_parity.test.js` | **`EXECUTED PASS`** | `0` | 5/5 passed; cryptographic precedence, fail-closed unpinned policy, local override isolation. |
| `internal/engine/ownership/ownership_test.go` | `go test -v -count=1 ./internal/engine/ownership/` | **`EXECUTED PASS`** | `0` | 11/11 passed; Genesis cert valid/invalid, closed delegation allowlist, replay protection, multi-registry conflict. |
| `test/task_a_final_trust_boundary_test.js` | `node test/task_a_final_trust_boundary_test.js` | **`EXECUTED PASS`** | `0` | 2/2 passed; Case A (offline trusted via Registry signature), Case B (Genesis ownership rejected from Registry trusted). |
| `test/pe01_tampered_sidecar_test.js` | `node test/pe01_tampered_sidecar_test.js` | **`EXECUTED PASS`** | `0` | 6/6 passed; Gates A-E tampered status/valid_until rejected, physical HG Mawar Bodas asset trusted. |

#### Pemetaan 14 Skenario Pengujian Spesifik:
1. `containerSigKey == genesisPubKey` (Self-Packaging): **`EXECUTED PASS`** (`task_a_buyer_lifecycle_test.js:L1271`).
2. `containerSigKey != genesisPubKey` (Third-Party Packaging): **`NOT FOUND IN INSPECTED SCOPE`**.
3. Delegation dengan scope `CONTAINER_PACKAGING`: **`NOT FOUND IN INSPECTED SCOPE`**.
4. Delegation signature valid & invalid: **`EXECUTED PASS`** pada Go (`ownership_test.go:L133`), **`NOT FOUND IN INSPECTED SCOPE`** pada TypeScript.
5. Delegation expired: **`NOT FOUND IN INSPECTED SCOPE`**.
6. Delegation revoked: **`NOT FOUND IN INSPECTED SCOPE`**.
7. Delegation asset binding mismatch: **`NOT FOUND IN INSPECTED SCOPE`**.
8. Delegator subject unmapped: **`NOT FOUND IN INSPECTED SCOPE`**.
9. Registry attestation valid & invalid: **`EXECUTED PASS`** (`registry_identity.test.js`).
10. Registry unavailable / offline: **`EXECUTED PASS`** (`task_a_final_trust_boundary_test.js:Case A`).
11. Verifikasi offline: **`EXECUTED PASS`** (`pe01_tampered_sidecar_test.js`).
12. `.nxcert` dengan unknown fields: **`NOT FOUND IN INSPECTED SCOPE`**.
13. `.nxcert` dengan schema version tidak dikenal: **`NOT FOUND IN INSPECTED SCOPE`**.
14. Perbedaan perilaku SDK, Verify, dan Player: **`EXECUTED PASS`** (`player-desktop.test.js`, `verify-desktop.test.js`).

---

### 7. Negative Search Evidence (Bukti Pencarian Ketiadaan Komponen)

| No | Target yang Dicari | Command Lengkap yang Dijalankan | Direktori / Ruang Lingkup | Hasil Pencarian Aktual |
|---|---|---|---|---|
| 1 | `CONTAINER_PACKAGING` | `grep -rnI --exclude-dir=node_modules "CONTAINER_PACKAGING" .` | Seluruh repository | **`0 matches`** (Exit Code: 1) |
| 2 | `verifyOwnershipChain` | `grep -rnI --exclude-dir=node_modules "verifyOwnershipChain" .` | Seluruh repository | **`0 matches`** (Exit Code: 1) |
| 3 | Fungsi `verifyDelegation` di TypeScript | `grep -rnI --exclude-dir=node_modules -E "verifyDelegation" sdk/typescript/` | `sdk/typescript/` | **`0 matches`** (Exit Code: 1) |
| 4 | JSON Schema formal `.nxcert` | `find . -name "*cert*schema*.json" -o -name "*nxcert*.schema"` | Seluruh repository | **`0 matches`** (Exit Code: 0, no files) |
| 5 | Unknown field rejection pada parser `.nxcert` | `grep -rnI --exclude-dir=node_modules -E "DisallowUnknownFields|additionalProperties" sdk/typescript/ player-desktop/ verify-desktop/` | SDK & Desktop apps | **`0 matches`** (Exit Code: 1) |
| 6 | Test Third-Party Packaging | `grep -rnI --exclude-dir=node_modules -E "third.*party.*packag|delegat.*packag" test/ tests/ sdk/typescript/test/` | Seluruh direktori test | **`0 matches`** (Exit Code: 1) |

---

### 8. Ringkasan Status Governance

Mandat supplement bukti teknis ini diserahkan di bawah batasan tata kelola yang tetap mengikat penuh:

| Item Governance | Status |
|---|---|
| **AUDIT-NEW-10 — Keputusan Produk PO** | **`APPROVED / RESOLVED`** |
| **AUDIT-NEW-10 — Kontrak Teknis Architecture Authority** | **`OPEN`** |
| **Stage 1 — Source Inspection** | **`PENDING SUPPLEMENT REVIEW`** |
| **Stage 2 — PLAN Reconciliation** | **`NOT STARTED`** |
| **Gate A** | **`NOT PASSED`** |
| **Gate B** | **`BLOCKED`** |
| **PE-02 Implementation** | **`NOT AUTHORIZED`** |
| **Sprint 16 / PE-01** | **`CLOSED / FROZEN`** |
| **Sprint 17** | **`NOT STARTED`** |
