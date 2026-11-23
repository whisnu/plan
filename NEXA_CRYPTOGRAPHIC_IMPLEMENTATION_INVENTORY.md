# NEXA — Cryptographic Implementation Inventory

**Document Type:** Technical Information Gathering — Read Only (Non-Audit)  
**Repository:** `/opt/antigravity/projects/nexa`  
**Inspected Branch:** `main` (`fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`)  
**Timestamp:** 2026-11-23T16:04:00+07:00  

---

## 1. Repository, Branch, dan Cakupan Pemeriksaan

- **Repository Root:** `/opt/antigravity/projects/nexa`
- **Branch Aktif:** `main` (Commit: `fc08a5c`)
- **Cakupan Komponen yang Diperiksa:**
  1. **Core Engine & CLI (Go):** [`cmd/`](file:///opt/antigravity/projects/nexa/cmd/), [`internal/engine/`](file:///opt/antigravity/projects/nexa/internal/engine/), [`pkg/`](file:///opt/antigravity/projects/nexa/pkg/), [`internal/model/`](file:///opt/antigravity/projects/nexa/internal/model/), [`internal/forge/`](file:///opt/antigravity/projects/nexa/internal/forge/), [`internal/handler/`](file:///opt/antigravity/projects/nexa/internal/handler/)
  2. **Storage Service (Go):** [`storage/`](file:///opt/antigravity/projects/nexa/storage/)
  3. **Official SDKs:**
     - TypeScript SDK: [`sdk/typescript/`](file:///opt/antigravity/projects/nexa/sdk/typescript/)
     - C Native Library / Mobile CGO Bindings: [`sdk/c/`](file:///opt/antigravity/projects/nexa/sdk/c/)
  4. **Desktop Clients (Electron / Node.js):**
     - [`player-desktop/`](file:///opt/antigravity/projects/nexa/player-desktop/)
     - [`studio-desktop/`](file:///opt/antigravity/projects/nexa/studio-desktop/)
     - [`verify-desktop/`](file:///opt/antigravity/projects/nexa/verify-desktop/)
  5. **Web Marketplace & Server (Node.js / Express):** [`marketplace/`](file:///opt/antigravity/projects/nexa/marketplace/)
  6. **Mobile Applications (React Native / Expo):** [`mobile/`](file:///opt/antigravity/projects/nexa/mobile/) (termasuk package `expo-nexa-core`)
- **Batasan Pemeriksaan:** Sesuai batasan pekerjaan, pemeriksaan ini murni inventarisasi teknis faktual berbasis kode sumber (*Read-Only Technical Information Gathering*). Tidak dilakukan evaluasi kepatuhan BSSN, security audit, ataupun pengubahan kode/konfigurasi.

---

## 2. Cryptographic Algorithm Inventory

| ID | Mekanisme / Algoritma | Tujuan Penggunaan | Komponen Pengguna | Lokasi File & Fungsi / Entry Point | Library / Dependency | Status Klasifikasi |
|:---|:---|:---|:---|:---|:---|:---|
| **ALG-01** | **Ed25519 (EdDSA)** | Pembuatan dan verifikasi tanda tangan digital untuk Asset Container `.nx`, Sidecar Certificate, Active Key Assertion, Delegation Assertion, dan Genesis Ownership Certificate | Core Engine, CLI, SDK (TS/C), Desktop Apps, Mobile Bindings, Marketplace | [`internal/engine/crypto/crypto.go:17`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L17) (`GenerateKeyPair`, `Sign`, `Verify`), [`sdk/typescript/src/crypto.ts:11`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L11), [`marketplace/server.js:591`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L591) | Go Standard Library `crypto/ed25519`; Node.js built-in `crypto` (`ed25519`) | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-02** | **SHA-256** | Perhitungan digest integritas payload aset, deduplikasi nonce, pembentukan Certificate ID, serta hashing token sesi/kredensial | Seluruh komponen (Core, Storage, Registry, Marketplace, SDK, Desktop, Mobile) | [`internal/engine/crypto/crypto.go:183`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L183) (`Hash`), [`internal/forge/forge.go:27`](file:///opt/antigravity/projects/nexa/internal/forge/forge.go#L27), [`storage/internal/store/storage_engine.go:133`](file:///opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go#L133) | Go `crypto/sha256`; Node.js built-in `crypto.createHash('sha256')` | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-03** | **HMAC-SHA256** | Autentikasi request antarlayanan (Marketplace ke Storage Engine dan Registry internal API) dengan nonce dan timestamp anti-replay | Marketplace & Storage Engine | [`storage/internal/store/storage_engine.go:153`](file:///opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go#L153) (`ValidateHMACWithBodyHash`), [`marketplace/server.js:782`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L782) | Go `crypto/hmac`; Node.js `crypto.createHmac` | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-04** | **JSON Canonicalization Scheme (RFC 8785 / JCS)** | Kanonikalisasi deterministik representasi JSON sebelum hashing dan penandatanganan digital (pengurutan kunci berbasis UTF-16, validasi Unicode fail-closed) | Core Engine, Identity Lineage, Ownership Engine, TS SDK, Desktop Apps | [`internal/engine/crypto/jcs.go:19`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/jcs.go#L19) (`CanonicalizeJCS`), [`sdk/typescript/src/ownership.ts:86`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/ownership.ts#L86) | Go internal engine; Custom JS/TS stringifier deterministik | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-05** | **bcrypt (Blowfish-based KDF)** | Hash password pengguna dan administrator pada database Marketplace | Marketplace Auth Service | [`marketplace/server.js:1404`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L1404), [`marketplace/db/store.js:138`](file:///opt/antigravity/projects/nexa/marketplace/db/store.js#L138) | npm `bcryptjs` (v3.0.3) | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-06** | **CSPRNG (Cryptographically Secure Pseudo-Random Number Generator)** | Pembuatan key pair Ed25519, token sesi, nonce transfer, dan token otentikasi acak | Seluruh subsistem | [`internal/engine/crypto/crypto.go:18`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L18) (`rand.Reader`), [`marketplace/server.js:1409`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L1409) (`crypto.randomBytes`) | Go `crypto/rand`; Node.js `crypto.randomBytes` | **SOURCE-VERIFIED** (ACTIVE) |
| **ALG-07** | **Symmetric Encryption (AES / ChaCha20)** | Enkripsi data at-rest atau payload container | Tidak ditemukan implementasi enkripsi simetris pada berkas `.nx` container maupun database lokal | Tidak ada pemanggilan cipher simetris (`docs/prompts/Nexa_Sprint9_Super_Prompt.md:21` menegaskan payload `.nx` disimpan sebagai raw unencrypted bytes) | Tidak ada library cipher yang dipanggil | **NOT FOUND IN INSPECTED SCOPE** |
| **ALG-08** | **Authenticated Encryption with Associated Data (AEAD)** | Enkripsi terautentikasi (AES-GCM, ChaCha20-Poly1305) | Tidak ada pemanggilan AEAD pada runtime engine, penyimpanan lokal, mobile, maupun paket distribusi | Tidak ada pemanggilan fungsi cipher AEAD | Tidak ada library AEAD yang dipanggil | **NOT FOUND IN INSPECTED SCOPE** |
| **ALG-09** | **Key Derivation Function (PBKDF2 / Argon2 / Scrypt)** | KDF untuk derivasi kunci enkripsi atau private key passkey | Tidak ditemukan pemanggilan KDF untuk manajemen kunci (kunci privat disimpan langsung dalam format PKCS#8) | Tidak ada pemanggilan PBKDF2/Argon2/HKDF | Standar library tidak memanggil KDF modul | **NOT FOUND IN INSPECTED SCOPE** |
| **ALG-10** | **Key Agreement (ECDH / X25519)** | Pertukaran kunci rahasia (*Diffie-Hellman / Shared Secret*) | Tidak ditemukan protokol key agreement antar entitas Nexa | Tidak ada modul X25519 / ECDH | Tidak ada pemanggilan | **NOT FOUND IN INSPECTED SCOPE** |
| **ALG-11** | **Transport Security (TLS / HTTPS)** | Enkripsi transport komunikasi jaringan (REST API) | Marketplace ke Registry Service | [`marketplace/server.js:386`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L386) (`https://nxregistry.opticpro.my.id`), [`marketplace/server.js:216`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L216) | Node.js built-in `https` module | **CONFIG-VERIFIED** (Pengelolaan TLS dikelola OS / reverse proxy eksternal) |
| **ALG-12** | **X.509 Certificate Chain / PKI / Pinning** | Validasi sertifikat PKIX hirarkis tradisional, mutual TLS (mTLS), atau certificate pinning | Verifikasi kredensial Nexa tidak menggunakan X.509/ASN.1 certificate chain konvensional; sertifikat diformat sebagai JSON / RFC 8785 JCS assertions yang ditandatangani Ed25519 secara langsung | [`internal/engine/verification/verification.go:42`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L42) (`RegistryCert`), [`internal/engine/ownership/cert.go:15`](file:///opt/antigravity/projects/nexa/internal/engine/ownership/cert.go#L15) | Pemformatan mandiri JSON JCS; tidak ada parsing rantai ASN.1 X.509 | **NOT FOUND IN INSPECTED SCOPE** (X.509 PKIX chain tidak digunakan) |

---

## 3. Digital Signature — Ed25519

1. **Lokasi Fungsi Signing:**
   - **Go Core Engine:** [`internal/engine/crypto/crypto.go:173`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L173) (`Sign(privKey ed25519.PrivateKey, data []byte) []byte`), dibungkus oleh CLI forge [`internal/forge/forge.go:45`](file:///opt/antigravity/projects/nexa/internal/forge/forge.go#L45).
   - **Identity Lineage & Ownership:** [`internal/engine/ownership/cert.go:68`](file:///opt/antigravity/projects/nexa/internal/engine/ownership/cert.go#L68) (`crypto.Sign(creatorPrivKey, canonicalBytes)`).
   - **TypeScript SDK:** [`sdk/typescript/src/crypto.ts:11`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L11) (`sign(privateKey: crypto.KeyObject, data: Buffer): Buffer`).
   - **C Native SDK:** [`sdk/c/secure_key.c:54`](file:///opt/antigravity/projects/nexa/sdk/c/secure_key.c#L54) (`nexa_secure_key_sign`).
2. **Lokasi Fungsi Verification:**
   - **Go Core Engine:** [`internal/engine/crypto/crypto.go:178`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L178) (`Verify(pubKey ed25519.PublicKey, data []byte, sig []byte) bool`), dipanggil pada [`internal/engine/verification/verification.go:146`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L146) via package `evidence`.
   - **TypeScript SDK:** [`sdk/typescript/src/crypto.ts:15`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L15) (`verify(publicKey: crypto.KeyObject, data: Buffer, signature: Buffer): boolean`).
   - **Marketplace Server:** [`marketplace/server.js:593`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L593) (`crypto.verify(null, Buffer.from(canonStr, 'utf8'), pubKeyObj, sigBytes)`).
3. **Komponen Pembuat Signature:**
   - Nexa CLI (`cmd/nexa forge`)
   - Studio Desktop (`studio-desktop/`)
   - Registry Service (`cmd/registry`)
   - Licensing Authority (`cmd/licensing`)
   - Ownership Certificate Issuer
4. **Komponen Pemeriksa/Verifikasi Signature:**
   - Nexa CLI (`cmd/nexa verify`)
   - Verify Desktop (`verify-desktop/`)
   - Player Desktop (`player-desktop/`)
   - Marketplace Ingestion Server (`marketplace/server.js`)
   - C Native Mobile Bindings (`sdk/c/nexa_mobile_cbindings.go`)
   - Mobile Expo App (`mobile/packages/expo-nexa-core/`)
5. **Struktur Payload yang Ditandatangani:**
   - **Kontainer `.nx`:** Seluruh byte representasi JSON dari `Manifest` model (`asset_name`, `asset_size`, `asset_hash`, `creator`, `issuer`, `created_at`, `payload_format`, `usage_opt_in`, `publisher_opt_in_proof`).
   - **Registry Certificate:** String kanonikal JCS berisikan 6 field: `{"certificate_id":...,"creator_public_key":...,"issued_at":...,"issuer":...,"status":...,"valid_until":...}`.
   - **Genesis Ownership Certificate:** String kanonikal RFC 8785 JCS memuat: `asset_id`, `creator_public_key`, `effective_at`, `issued_at`, `issuer_id`, `previous_cert_ref`, `subject_id`, `underlying_cert_id`.
   - **Active Key Assertion:** Representasi JCS `ActiveKeyAuthorizationAssertion` (diotorisasi oleh Root Key).
   - **Delegation Assertion:** Representasi JCS `DelegationAssertion` (diotorisasi oleh Parent Public Key).
6. **Penyiapan Payload Sebelum Signing:**
   - Payload JSON diserialisasikan secara deterministik menggunakan pengurutan kunci leksikografis RFC 8785 (UTF-16 code units), string tanpa escape HTML (`SetEscapeHTML(false)`), dan timestamp berpresisi nanodetik UTC (`2006-01-02T15:04:05.000000000Z`).
7. **Format Penyimpanan Signature:**
   - Pada file kontainer `.nx`: Disimpan sebagai byte mentah biner (*raw binary*) berukuran tepat 64 byte di akhir segmen kontainer (offset setelah payload).
   - Pada JSON / REST API / Sidecar: Direpresentasikan sebagai string hex 128 karakter (`encoding/hex`).
8. **Format Public Key dan Private Key:**
   - **Penyimpanan Berkas Kunci:** Format PEM standar:
     - Private Key: PEM `BEGIN PRIVATE KEY` (PKCS#8 DER bytes via `x509.MarshalPKCS8PrivateKey`).
     - Public Key: PEM `BEGIN PUBLIC KEY` (PKIX DER bytes via `x509.MarshalPKIXPublicKey`).
   - **Dalam Memori / Payload JSON:** Raw bytes 32 byte atau representasi hex string 64 karakter (dengan DER SPKI prefix `302a300506032b6570032100` pada interoperabilitas Node.js).
9. **Hubungan Public Key dengan Identitas / Otoritas:**
   - **Creator Key:** Mewakili identitas pembuat/pemilik aset.
   - **Issuer / Registry Key:** Kunci otoritas pendaftaran (*nexa-local* atau *Registry Authority*).
   - **Root Key vs Active Key:** Model identitas multi-tier di mana Genesis Root Key mendelegasikan otoritas penandatanganan harian ke Active Public Key bertingkat dengan masa berlaku (*effective_at* s.d. *expires_at*).
10. **Mekanisme Key Rotation & Revocation:**
    - **Rotasi:** Didukung via `ActiveKeyAuthorizationAssertion` yang memiliki sequence number dan batasan waktu (`internal/engine/identity/active_key.go:15`).
    - **Pemulihan Kunci (Recovery):** Menggunakan protokol 2-step `RootRecoveryAssertion` terikat pada hash digest kunci pemulihan genesis (`genesis_recovery_key_digest`).
    - **Revokasi Sertifikat:** Ditangani oleh status Registry API (`status: "revoked"`) dan dicatat pada database registri.
11. **Dependency Library:**
    - Go Standard Library `crypto/ed25519`.
    - Node.js native `crypto` module (via OpenSSL bawaan Node runtime).

---

## 4. Hashing dan Asset Integrity

| Objek yang Di-hash | Algoritma Hash | Input Data | Output & Format Digest | Fungsi Pemanggil | Komponen Pengguna | Hubungan dengan Signature |
|:---|:---|:---|:---|:---|:---|:---|
| **Raw Asset Payload** | SHA-256 | Seluruh byte mentah berkas digital (audio WAV/MP3, video, dsb.) | Hex string 64-karakter | [`internal/forge/forge.go:27`](file:///opt/antigravity/projects/nexa/internal/forge/forge.go#L27) (`sha256.Sum256`) | Forge CLI, Verification Engine, C Mobile Bindings | Nilai hash dimasukkan ke dalam `Manifest.AssetHash`. Manifest tersebut kemudian ditandatangani Ed25519. Integritas aset terjamin secara tidak langsung (*hash-then-sign* via Manifest). |
| **Manifest Signature (Certificate ID Derivation)** | SHA-256 | 64 byte tanda tangan Ed25519 manifest | Hex string 64-karakter | [`internal/engine/verification/verification.go:154`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L154) (`sha256.Sum256(signature)`) | Core Verifier, Player, Verify Desktop | Hasil hash dari signature dijadikan pengenal unik deterministik sertifikat (`CertificateID`), mengikat registrasi registry langsung ke bukti signature. |
| **Streaming Container Payload** | SHA-256 | Aliran byte payload dibaca per blok 64 KB | Hex string 64-karakter | [`internal/engine/verification/verification.go:129`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L129) (`sha256.New()`) | Verifier CLI, Desktop Apps, Mobile Bindings | Dibandingkan terhadap `Manifest.AssetHash` untuk mendeteksi manipulasi payload tanpa memuat seluruh file ke RAM. |
| **Distribution Package (.nx container file)** | SHA-256 | Seluruh byte file `.nx` terpaket | Hex string 64-karakter (`package_sha256`) | [`marketplace/server.js:2644`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L2644), [`storage/internal/store/storage_engine.go:181`](file:///opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go#L181) | Marketplace, Storage Service | Memverifikasi integritas transmisi berkas saat upload/download antara Marketplace dan Storage node. |
| **Genesis Recovery Key** | SHA-256 | Raw bytes kunci publik recovery (32 byte) | Hex string 64-karakter | [`internal/engine/identity/lineage.go:47`](file:///opt/antigravity/projects/nexa/internal/engine/identity/lineage.go#L47) | Identity Lineage Verifier | Nilai digest dicocokkan dengan `genesis_recovery_key_digest` sebelum signature recovery assertion diverifikasi. |
| **API Request Body (HMAC)** | SHA-256 | Byte body payload HTTP request | Hex string 64-karakter | [`storage/internal/store/storage_engine.go:133`](file:///opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go#L133) | Storage Engine, Marketplace | Disematkan ke dalam string kanonikal HMAC untuk verifikasi integritas pesan REST API. |
| **Client Nonce Anti-Replay** | SHA-256 | String nonce yang dikirim klien | Byte array 32 byte (`sha256.Sum256`) | [`internal/handler/ecosystem_api_handler.go:580`](file:///opt/antigravity/projects/nexa/internal/handler/ecosystem_api_handler.go#L580) | Ecosystem API Handler | Mencegah replay attack pada telemetri dan audit usage record. |

---

## 5. JSON Canonicalization — RFC 8785

1. **Lokasi Fungsi Canonicalization:**
   - **Go Core Engine:** [`internal/engine/crypto/jcs.go:19`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/jcs.go#L19) (`CanonicalizeJCS(v interface{}) ([]byte, error)`).
   - **TypeScript SDK:** [`sdk/typescript/src/registry.ts:118`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L118) (`canonicalJcs`), [`sdk/typescript/src/ownership.ts:86`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/ownership.ts#L86) (`canonicalizeGenesisPayload`).
   - **Go Verification Module:** [`internal/engine/verification/verification.go:329`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L329) (`canonicalJSON`).
2. **Nama Fungsi dan Package:**
   - `crypto.CanonicalizeJCS` (`nexa/internal/engine/crypto`)
   - `ownership.CanonicalizeGenesisPayload` (`nexa/internal/engine/ownership`)
   - `NexaRegistry.canonicalJcs` (`nexa-sdk` TypeScript)
3. **Komponen Pemanggil:**
   - `internal/engine/identity/` (`lineage.go`, `active_key.go`, `delegation.go`, `verifier.go`)
   - `internal/handler/ecosystem_api_handler.go`
   - `pkg/nexa/identity.go`
   - `sdk/typescript/src/ownership.ts` & `sdk/typescript/src/federation.ts`
4. **Data atau Struktur JSON yang Diproses:**
   - `RootRecoveryAssertion`
   - `ActiveKeyAuthorizationAssertion`
   - `DelegationAssertion`
   - `OwnershipCertificate` (Genesis Claim)
   - `TransferEvent`
   - `RegistryCert`
5. **Cakupan Implementasi (Generik vs Terbatas):**
   - **Go Engine (`internal/engine/crypto/jcs.go`):** Bersifat **generik**. Menerima `interface{}`, melakukan validasi UTF-8 sebelum serialisasi, melakukan traversal rekursif terhadap `map[string]interface{}` dan `[]interface{}`, mengurutkan properti berdasarkan nilai UTF-16 code unit, memformat angka sesuai spesifikasi ECMAScript (aturan `-0 -> 0`, eksponensial tanpa *leading zero* pada eksponen).
   - **TypeScript SDK & Verifier Helper:** Bersifat **terbatas/struktural khusus**, memetakan field tertentu secara *hardcoded* dalam urutan alfabetis tetap untuk menghindari overhead parser penuh pada runtime klien.
6. **Hubungan Output Canonicalization dengan Hashing & Signing:**
   - Output byte kanonikal langsung menjadi input data yang di-hash atau ditandatangani:
     `Sign(privKey, canonicalBytes)` dan `Verify(pubKey, canonicalBytes, sigBytes)`.
7. **Library yang Digunakan:**
   - Ditulis secara mandiri (*in-house native Go & TypeScript*) tanpa menggunakan dependency external pihak ketiga seperti `go-jcs` atau `canonical-json`.

---

## 6. Authenticated Encryption dan Data Protection

- **Penyimpanan Lokal (Local Storage):** **NOT FOUND IN INSPECTED SCOPE.** File konfigurasi, berkas riwayat, dan counter penggunaan (`usage_counter.dat`) disimpan tanpa lapisan cipher enkripsi simetris.
- **Database:** **NOT FOUND IN INSPECTED SCOPE.** Database PostgreSQL (`marketplace/db/`, `migrations/`) menyimpan data relasional dalam bentuk teks dan byte ter-hash (password disimpan sebagai hash bcrypt; token sesi dan nonce disimpan dalam bentuk plain hex string). Tidak ditemukan pemanggilan modul enkripsi kolom seperti *pgcrypto* atau enkripsi level aplikasi.
- **File / Paket Distribusi (`.nx` container):** **NOT FOUND IN INSPECTED SCOPE.** Sesuai rancangan pada [`internal/engine/container/container.go`](file:///opt/antigravity/projects/nexa/internal/engine/container/container.go) dan dokumentasi proyek, payload disimpan dalam format *raw digital asset bytes* (hanya dibungkus header dan tanda tangan digital, bukan enkripsi cipher).
- **Komunikasi Antarkomponen:** Komunikasi internal antara Marketplace dan Storage Engine diamankan menggunakan tanda tangan **HMAC-SHA256** dan pemeriksaan nonce anti-replay, bukan melalui terowongan terenkripsi level aplikasi (enkripsi transport bergantung pada HTTPS jika dikonfigurasi).
- **Aplikasi Mobile & Desktop:** Tidak ditemukan implementasi cipher AEAD (AES-GCM / ChaCha20-Poly1305) pada layer aplikasi desktop maupun mobile.

---

## 7. Key Management

1. **Pembuatan Key Pair:**
   - Dibuat menggunakan fungsi `ed25519.GenerateKey(rand.Reader)` pada Go Core Engine ([`internal/engine/crypto/crypto.go:18`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L18)) dan `crypto.generateKeyPairSync("ed25519")` pada runtime Node.js/TypeScript.
2. **Penyimpanan Private Key:**
   - Disimpan di disk dalam format berkas teks PEM PKCS#8 DER terenkod Base64 dengan izin berkas ketat `0600` (`SavePrivateKey` pada [`internal/engine/crypto/crypto.go:42`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L42)).
   - Default path lokal: `keys/ed25519_key` atau path kustom melalui flag CLI `--key`.
3. **Penyimpanan Public Key:**
   - Disimpan di disk dalam format PEM PKIX DER dengan izin `0644` (`SavePublicKey` pada [`internal/engine/crypto/crypto.go:72`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go#L72)).
   - Dalam database Marketplace/Registry, kunci publik disimpan sebagai string heksadesimal 64 karakter.
4. **Environment Variables & Secret Store:**
   - Environment variables digunakan untuk menyimpan kunci dan secret operasional:
     - `NEXA_STORAGE_SERVICE_SECRET`: Kunci simetris bersama untuk HMAC Storage Engine.
     - `REGISTRY_AUTHORITY_URL`: Endpoint otoritas registri.
     - `ISSUER_PRIVATE_KEY` / `ISSUER_PUBLIC_KEY`: Kunci penandatangan otoritas penerbit pada microservice registry.
5. **OS Keystore / Secure Storage:**
   - **NOT FOUND IN INSPECTED SCOPE.** Tidak ditemukan integrasi dengan Android Keystore, iOS Keychain, macOS Keychain, maupun Windows Credential Manager pada source code desktop dan mobile.
6. **Hardware-Backed Key Storage (HSM / TPM / Secure Enclave):**
   - **NOT FOUND IN INSPECTED SCOPE.** Pada layer C SDK ([`sdk/c/secure_buffer.c`](file:///opt/antigravity/projects/nexa/sdk/c/secure_buffer.c)), implementasi `NexaSecureBuffer` mengandalkan alokasi memori fisik terkunci (*virtual memory page locking* via `mlock()`) dengan halaman pelindung (*guard pages* via `mprotect()`) serta pembersihan memori eksplisit (`volatile bzero`), namun bukan merupakan hardware HSM/TPM.
7. **Key Rotation & Revocation:**
   - Dikelola melalui arsitektur deklaratif identitas: `ActiveKeyAuthorizationAssertion` memungkinkan rotasi kunci aktif harian tanpa mengubah *Genesis Root Key*.
   - Revokasi kunci dicatat di Registry Authority dan dicek saat resolusi validitas identitas.
8. **Key Backup & Recovery:**
   - Protokol `RootRecoveryAssertion` terikat pada hash `genesis_recovery_key_digest` yang telah dideklarasikan di awal saat inisialisasi identitas.
9. **Pemisahan Kunci (Key Separation):**
   - Kunci tanda tangan digital (**Signing Keys**) terpisah berdasarkan perannya: *Genesis Root Key*, *Active Key*, *Delegation Key*, *Registry Authority Key*, dan *Creator Key*.
   - Kunci autentikasi API (**HMAC Secret**) terpisah sebagai *shared secret pre-shared key*.
   - Tidak ada kunci enkripsi data (*Encryption Keys*) yang terdeteksi aktif.

---

## 8. Cryptographic Dependencies

| Dependency / Package | Versi Manifest | Package Manager / Manifest File | Komponen Pengguna | Fungsi Kriptografi yang Dipakai | Status Ketergantungan |
|:---|:---|:---|:---|:---|:---|
| **`crypto/ed25519`** | Go 1.26.5 Standard Lib | `go.mod` (Go toolchain) | Core Engine, CLI, Registry, Verification, Licensing | Pembuatan keypair, penandatanganan, dan verifikasi Ed25519 | **Langsung (Direct / Built-in)** |
| **`crypto/sha256`** | Go 1.26.5 Standard Lib | `go.mod` (Go toolchain) | Core Engine, Verification, Storage, Registry | Hashing payload, integritas, dan token | **Langsung (Direct / Built-in)** |
| **`crypto/hmac`** | Go 1.26.5 Standard Lib | `go.mod` (Go toolchain) | Storage Service, Ecosystem API | Autentikasi pesan HMAC-SHA256 | **Langsung (Direct / Built-in)** |
| **`crypto/rand`** | Go 1.26.5 Standard Lib | `go.mod` (Go toolchain) | Core Engine, Handler, Storage | Sumber entropi acak kriptografis (CSPRNG) | **Langsung (Direct / Built-in)** |
| **`crypto/x509`** | Go 1.26.5 Standard Lib | `go.mod` (Go toolchain) | Core Engine Key Storage | Encoding/parsing format PKCS#8 dan PKIX DER untuk Ed25519 PEM | **Langsung (Direct / Built-in)** |
| **`crypto` (Node.js)** | Built-in Node.js runtime | Node.js engine | Marketplace, TS SDK, Desktop Apps | `createHash`, `createHmac`, `sign`, `verify`, `createPublicKey`, `createPrivateKey`, `randomBytes` | **Langsung (Direct / Built-in)** |
| **`bcryptjs`** | `^3.0.3` | `marketplace/package.json` | Marketplace Server | Hash dan verifikasi password akun pengguna | **Langsung (Direct / Third-party npm)** |
| **`electron`** | `^31.0.0` | `player-desktop/package.json`, dsb. | Desktop Apps | Runtime Chromium/Node.js pengeksekusi modul crypto desktop | **Direct Runtime** |

---

## 9. Transport Security

- **TLS Version:** Tidak ada konfigurasi versi TLS eksplisit (misal pembatasan spesifik TLS 1.2 / TLS 1.3) yang didefinisikan di dalam source code aplikasi Go maupun Node.js.
- **Lokasi Konfigurasi TLS:**
  - Kode program Nexa bertindak sebagai HTTP client dan server standar (`net/http` pada Go dan `http.createServer` / `express` pada Node.js).
  - Port layanan backend (`8080` untuk Registry, `8087` untuk Storage, `3000` untuk Marketplace) mendengarkan secara default pada HTTP biasa (*plaintext*).
  - Pada lingkungan produksi, konfigurasi merujuk ke endpoint HTTPS publik (seperti `https://nxregistry.opticpro.my.id`).
- **Certificate Validation:** Validasi sertifikat TLS server dilakukan oleh trust store default sistem operasi / Node.js runtime saat memanggil URL `https://`.
- **Certificate Pinning:** **NOT FOUND IN INSPECTED SCOPE.** Tidak ditemukan implementasi pinning hash public key atau pinning sertifikat pada kode client desktop maupun mobile.
- **Mutual TLS (mTLS):** **NOT FOUND IN INSPECTED SCOPE.** Tidak ditemukan konfigurasi otentikasi sertifikat klien dua arah pada kode server maupun client.
- **Kesimpulan Batasan:** Pengamanan TLS seutuhnya didelegasikan kepada layer infrastruktur eksternal (reverse proxy Nginx / Caddy / Cloudflare).

---

## 10. Component and Platform Mapping

| Komponen Nexa | Keberadaan di Repository | Penggunaan Kriptografi yang Terbukti pada Source Code |
|:---|:---|:---|
| **Nexa Core / SDK** | Terverifikasi ([`internal/engine/`](file:///opt/antigravity/projects/nexa/internal/engine/), [`pkg/`](file:///opt/antigravity/projects/nexa/pkg/), [`sdk/`](file:///opt/antigravity/projects/nexa/sdk/)) | Ed25519 (Keygen, Sign, Verify), SHA-256 (Payload Hash, CertID Hash), RFC 8785 Canonical JCS, CSPRNG. |
| **NX Studio Desktop** | Terverifikasi ([`studio-desktop/`](file:///opt/antigravity/projects/nexa/studio-desktop/)) | SHA-256 payload calculation, integrasi pembuatan kontainer via Nexa SDK / Core CLI, pemuatan private key penandatangan. |
| **Verify Desktop** | Terverifikasi ([`verify-desktop/`](file:///opt/antigravity/projects/nexa/verify-desktop/)) | Verifikasi kontainer `.nx`, streaming hash verification, verifikasi Ed25519 signature manifest dan sidecar `.nxcert`. |
| **Player Desktop** | Terverifikasi ([`player-desktop/`](file:///opt/antigravity/projects/nexa/player-desktop/)) | Pemeriksaan integritas payload aset via SHA-256, verifikasi status tanda tangan offline/online sebelum playback. |
| **Player Android/iOS** | Terverifikasi sebagian ([`mobile/apps/player/`](file:///opt/antigravity/projects/nexa/mobile/apps/player/), [`mobile/packages/expo-nexa-core/`](file:///opt/antigravity/projects/nexa/mobile/packages/expo-nexa-core/)) | Memanggil wrapper native CGO binding (`NexaMobileOpenContainer`, `verifyContainer`), verifikasi integritas hash dan signature. |
| **Verify Android/iOS** | Terverifikasi sebagian ([`mobile/apps/verify-lite/`](file:///opt/antigravity/projects/nexa/mobile/apps/verify-lite/)) | Memanggil fungsi verifikasi container pada library native C/CGO. |
| **Registry** | Terverifikasi ([`cmd/registry/`](file:///opt/antigravity/projects/nexa/cmd/registry/)) | Penandatanganan sertifikat registrasi aset dengan Ed25519, verifikasi kunci publik kreator, validasi kanonikal JCS. |
| **License Authority** | Terverifikasi ([`cmd/licensing/`](file:///opt/antigravity/projects/nexa/cmd/licensing/), [`internal/handler/licensing_handler.go`](file:///opt/antigravity/projects/nexa/internal/handler/licensing_handler.go)) | Penandatanganan lisensi bukti kepemilikan dan hak pakai menggunakan Ed25519. |
| **Usage** | Terverifikasi ([`cmd/usage/`](file:///opt/antigravity/projects/nexa/cmd/usage/), [`internal/engine/counter/`](file:///opt/antigravity/projects/nexa/internal/engine/counter/)) | Hashing agregat dan anti-replay audit penggunaan menggunakan SHA-256. |
| **Storage Engine** | Terverifikasi ([`storage/`](file:///opt/antigravity/projects/nexa/storage/)) | Validasi integritas upload/staging paket dengan SHA-256, autentikasi REST API dengan HMAC-SHA256, tracking nonce anti-replay. |
| **DistributionHub** | Terverifikasi (Dikelola dalam repositori via script build dist dan domain `nxdist.opticpro.my.id`) | Mengandalkan integritas file paket `.nx` berbasis hash SHA-256 dan verifikasi tanda tangan Ed25519. |
| **Marketplace** | Terverifikasi ([`marketplace/`](file:///opt/antigravity/projects/nexa/marketplace/)) | Otentikasi password bcrypt, komunikasi internal HMAC-SHA256, verifikasi signature Ed25519 kontainer yang diunggah. |

---

## 11. PQC (Post-Quantum Cryptography) Migration Dependencies

Bagian ini mengidentifikasi titik-titik keterikatan teknis (*technical coupling*) terhadap algoritma kriptografi kunci publik asimetris klasik (Ed25519) yang akan menjadi pertimbangan teknis pada perencanaan migrasi Post-Quantum Cryptography:

1. **Keterikatan Ukuran Tanda Tangan pada Binary Container Format (`.nx` v2.0):**
   - Header kontainer `.nx` memiliki field ukuran `sigLen` (uint32 BE), namun kode validasi di [`internal/engine/container/container.go:27`](file:///opt/antigravity/projects/nexa/internal/engine/container/container.go#L27) dan [`internal/engine/container/container.go:126`](file:///opt/antigravity/projects/nexa/internal/engine/container/container.go#L126) melakukan validasi *hardcoded*:
     ```go
     if len(signature) != 64 { return nil, fmt.Errorf("invalid signature size: expected 64 bytes...") }
     if manifestLen > ... || sigLen != 64 { return nil, errors.New("invalid section sizes...") }
     ```
   - *Dampak PQC:* Algoritma signature PQC (seperti ML-DSA / Dilithium atau Falcon) memiliki ukuran signature ribuan byte (misal 2.420 byte s.d. 3.293 byte). Kode deserialisasi container akan menolak (*fail-closed*) ukuran signature selain 64 byte.
2. **Keterikatan Ukuran Public Key dan Private Key:**
   - Pemeriksaan panjang raw public key 32 byte secara eksplisit di berbagai file:
     - [`internal/engine/identity/lineage.go:42`](file:///opt/antigravity/projects/nexa/internal/engine/identity/lineage.go#L42): `len(recPubKeyBytes) != 32`
     - [`internal/engine/identity/delegation.go:39`](file:///opt/antigravity/projects/nexa/internal/engine/identity/delegation.go#L39): `len(parentKeyBytes) != 32`
     - [`sdk/typescript/src/crypto.ts:41`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L41): `rawBytes.length === 32` (dengan injeksi DER SPKI prefix tetap untuk Ed25519 `302a300506032b6570032100`).
   - *Dampak PQC:* Kunci publik PQC memiliki ukuran jauh lebih besar (misal ML-DSA-44 berukuran 1.312 byte), sehingga parser raw key dan prefix DER SPKI akan gagal memproses format kunci PQC tanpa refaktorisasi.
3. **Keterikatan Field `signature_algorithm`:**
   - Field `signature_algorithm` di assertion JSON divalidasi kaku dengan string `"Ed25519"`:
     - [`internal/engine/identity/lineage.go:20`](file:///opt/antigravity/projects/nexa/internal/engine/identity/lineage.go#L20): `if assertion.SignatureAlgorithm != "Ed25519" { return error }`
     - [`internal/engine/identity/delegation.go:18`](file:///opt/antigravity/projects/nexa/internal/engine/identity/delegation.go#L18): `if assertion.SignatureAlgorithm != "Ed25519" { return error }`
4. **Keterikatan Derivasi Certificate ID:**
   - `CertificateID` diturunkan secara deterministik dari SHA-256 atas 64-byte Ed25519 signature ([`internal/engine/verification/verification.go:154`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go#L154)). Perubahan format atau skema signature akan mengubah pola pembentukan Certificate ID historis.
5. **Abstraksi Kriptografi Saat Ini:**
   - Nexa sudah memusatkan fungsi kriptografi dasar pada package [`internal/engine/crypto/`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/) (`crypto.go` dan `jcs.go`), yang memberikan titik awal modul apabila nantinya diperlukan enkapsulasi antarmuka multi-algoritma (*cryptographic agility*).

---

## 12. Evidence References

| ID | Kategori Bukti | Lokasi Berkas | Baris Referensi | Deskripsi Bukti Teknis |
|:---|:---|:---|:---|:---|
| **EVID-01** | Ed25519 Keygen & PEM | [`internal/engine/crypto/crypto.go`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go) | Baris 17–83 | Menunjukkan pembuatan pasangan kunci Ed25519 menggunakan `rand.Reader` dan penyimpanan format PEM PKCS#8 / PKIX. |
| **EVID-02** | Ed25519 Signing & Verify | [`internal/engine/crypto/crypto.go`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/crypto.go) | Baris 172–185 | Menunjukkan pemanggilan langsung fungsi standar Go `ed25519.Sign` dan `ed25519.Verify`. |
| **EVID-03** | Container Binary Layout | [`internal/engine/container/container.go`](file:///opt/antigravity/projects/nexa/internal/engine/container/container.go) | Baris 18–66 | Menunjukkan layout header 21 byte `.nx` v2.0, pengecekan panjang signature tetap 64 byte, dan penataan body segment. |
| **EVID-04** | SHA-256 Payload & Manifest | [`internal/forge/forge.go`](file:///opt/antigravity/projects/nexa/internal/forge/forge.go) | Baris 27–46 | Menunjukkan komputasi `sha256.Sum256(payload)`, penyusunan model `Manifest`, serialisasi JSON, dan signing Ed25519. |
| **EVID-05** | RFC 8785 Generic JCS | [`internal/engine/crypto/jcs.go`](file:///opt/antigravity/projects/nexa/internal/engine/crypto/jcs.go) | Baris 19–43, 184–197 | Menunjukkan implementasi mandiri RFC 8785 JCS dengan validasi UTF-8 sebelum marshaling dan pengurutan kunci berbasis UTF-16 code units. |
| **EVID-06** | Streaming Verification | [`internal/engine/verification/verification.go`](file:///opt/antigravity/projects/nexa/internal/engine/verification/verification.go) | Baris 128–156 | Menunjukkan streaming hash payload dengan buffer 64 KB, perbandingan hash, dan komputasi `CertificateID` via `sha256.Sum256(signature)`. |
| **EVID-07** | HMAC-SHA256 Auth & Nonce | [`storage/internal/store/storage_engine.go`](file:///opt/antigravity/projects/nexa/storage/internal/store/storage_engine.go) | Baris 88–161 | Menunjukkan mekanisme anti-replay nonce persistensi disk dan validasi signature `hmac.New(sha256.New, key)`. |
| **EVID-08** | TypeScript SDK Ed25519 | [`sdk/typescript/src/crypto.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts) | Baris 4–20, 42 | Menunjukkan rekonstruksi format SPKI DER Ed25519 prefix `302a300506032b6570032100` dan pemanggilan `crypto.sign` / `crypto.verify`. |
| **EVID-09** | Identity Lineage Recovery | [`internal/engine/identity/lineage.go`](file:///opt/antigravity/projects/nexa/internal/engine/identity/lineage.go) | Baris 20–85 | Menunjukkan verifikasi 2-step `RootRecoveryAssertion` mencakup pencocokan SHA-256 digest kunci recovery dan validasi tanda tangan Ed25519 atas JCS. |
| **EVID-10** | Memory-Locked Secure Buffer | [`sdk/c/secure_buffer.c`](file:///opt/antigravity/projects/nexa/sdk/c/secure_buffer.c) & [`sdk/c/secure_key.c`](file:///opt/antigravity/projects/nexa/sdk/c/secure_key.c) | Baris 34–89 | Menunjukkan alokasi buffer kunci terisolasi di RAM dengan page locking (`mlock`), guard pages, dan zeroing memori eksplisit. |

---

## 13. Informasi yang Belum Ditemukan atau Belum Dapat Diverifikasi

Sesuai aturan batas pemeriksaan fakta tanpa asumsi:

1. **Symmetric Encryption at-rest:** Tidak ditemukan bukti penggunaan algoritma enkripsi simetris (AES-CBC, AES-GCM, ChaCha20) pada penyimpanan lokal database, kontainer `.nx`, maupun berkas konfigurasi (**NOT FOUND IN INSPECTED SCOPE**).
2. **Authenticated Encryption (AEAD):** Tidak ditemukan bukti pemanggilan fungsi AEAD pada modul manapun di repositori (**NOT FOUND IN INSPECTED SCOPE**).
3. **Key Derivation Function (KDF):** Tidak ditemukan penggunaan modul derivasi kunci enkripsi seperti HKDF, PBKDF2, Argon2, atau Scrypt (selain `bcrypt` yang khusus digunakan untuk hash password akun web di Marketplace) (**NOT FOUND IN INSPECTED SCOPE**).
4. **Key Agreement (Diffie-Hellman / ECDH):** Tidak ditemukan mekanisme pembentukan shared secret kriptografis antar entitas (**NOT FOUND IN INSPECTED SCOPE**).
5. **Certificate Pinning & mTLS:** Tidak ditemukan konfigurasi pinning sertifikat ataupun otentikasi timbal balik (mTLS) di level kode aplikasi (**NOT FOUND IN INSPECTED SCOPE**).
6. **Hardware-Backed Key Storage (HSM/SE):** Tidak ditemukan driver atau integrasi perangkat keras keamanan (PKCS#11, TPM 2.0, Android Keystore hardware-backed, Apple Secure Enclave) (**NOT FOUND IN INSPECTED SCOPE**).
