# NEXA PE-02 A1 — TARGETED CORRECTION REPORT
## RECONCILIATION OF DOCUMENTATION & TECHNICAL EVIDENCE RESIDUALS

- **Repository Sumber:** `whisnu/nexa`
- **Branch Sumber:** `main`
- **Revision Acuan Sumber:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
- **Working-Tree Status:** `DIRTY — UNTRACKED FILES` (Zero tracked modifications; 2 pre-existing untracked documentation files)
- **Repository PLAN Kanonis:** `whisnu/plan` (branch `main`, mirror lokal di `evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`)
- **Tanggal:** 2026-11-10
- **Mode:** READ-ONLY terhadap source code

---

## 1. RESIDUAL CORRECTION MATRIX

| Residual | Hasil Pemeriksaan | Kesimpulan Akhir | Bukti Utama | Status |
| :--- | :--- | :--- | :--- | :--- |
| **B-SUP-02** | `ResolveActiveSigningAuthorityAt` tidak menerima atau memeriksa `subject_type`. `ActiveKeyAuthorizationAssertion` tidak memuat `subject_type` dan mengikat `SubjectID` URN (`urn:nexa:id:...`). `IdentityVerifier.ExecutePipeline` memanggil resolver yang sama untuk Individual dan Organization. | Source code mendukung active-key resolver generik untuk Individual dan Organization; tidak ada pembatasan konkret di source yang melarang Individual Creator. Namun, bukti test di `tests/identity/` dan `tests/audit/sprint14/` secara eksklusif hanya menguji skenario Organization. | `active_key.go:L93-L154`, `verifier.go:L77-L81, L156`, `domain/identity.go:L99-L114` | `CORRECTED` |
| **C-SUP-02** | Pencarian diperluas ke seluruh direktori kode repositori (`cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`). Semua struct ownership (`OwnershipCertificate`, dsb.) hanya menerima skalar `AssetID`. | Tidak ditemukan struktur kepemilikan multi-aset, agregasi Album, hak kompilasi, atau publisher-origin authority di seluruh repositori. | `domain/ownership.go:L53-L68`, `cert.go:L15-L24`, grep regex seluruh direktori kode | `CONFIRMED (REVISION-WIDE)` |
| **D-SUP-01** | `SupportedFeatures` ada di struct `RegistryIdentity`, namun fungsi `CanonicalJCS()` mengecualikannya dari string preimage. `service.go:L69` menandatangani `CanonicalJCS()`, dan `VerifySignature()` memverifikasi `CanonicalJCS()`. Field ini tidak pernah dibaca oleh evaluator. | `SupportedFeatures` **TIDAK TERIKAT** secara kriptografis pada signature `RegistryIdentity`. Perubahan nilai field ini tidak membatalkan signature. Konsumen tidak boleh menganggap field ini terautentikasi oleh `VerifySignature()`. | `registry_identity.go:L13-L63`, `service.go:L62-L71` | `CORRECTED` |
| **E-SUP-02** | `GetRegistryKeyRevocations` menandatangani string `canonStr` yang HANYA memuat `registry_id` dan `updated_at`. Field `RevokedKeys` sama sekali tidak masuk ke signature preimage. Signing key `s.cfg.IssuerPrivateKey` adalah private key instance node registry lokal. Tidak ada fungsi verifikasi `ListSignature` di repositori. | Signature tidak mengikat isi `RevokedKeys`. Keberhasilan verifikasi hanya membuktikan integritas field yang tercakup (`registry_id` dan `updated_at`), bukan daftar key yang dicabut. `NO ALTERNATIVE AUTHENTICATION MECHANISM FOUND IN EXAMINED SCOPE`. | `service.go:L75-L88`, `registry_identity.go:L24-L29`, `config.go:L140-L158` | `CORRECTED` |
| **E-SUP-01** | `FreshnessOnlineFresh` diset di `verifier.go:L34-L37` murni berdasarkan argumen boolean input `!isOffline`. Tidak ada query jaringan, validasi timestamp, TTL cache, atau pengecekan respons Registry. | `ONLINE_FRESH` bukan bukti kesegaran data aktual (*actual freshness*), melainkan sekadar **klasifikasi jalur online (`ONLINE_CLASSIFICATION`)**. Status kesegaran aktual adalah `ONLINE_FRESHNESS NOT ESTABLISHED`. | `domain/identity.go:L158-L165`, `verifier.go:L34-L42` | `CORRECTED` |
| **Test Reconciliation** | Angka "43" berasal dari penjumlahan unnormalized: 14 (`tests/identity` top-level) + 18 (historical audit assertion count) + 11 (`internal/engine/ownership` subtests) = 43, mengabaikan 8 test federation dan mencampur top-level dengan subtest. Klaim bahwa "seluruh test khusus menguji Organization" tidak tepat karena pengujian ownership, federation, JCS, dan Subject ID bersifat subject-agnostic. | Total pengujian aktual adalah **39 top-level tests + 19 nested subtests = 58 test invocations** (seluruhnya PASS). Pengujian assertion yang secara spesifik menggunakan `SubjectTypeOrganization` hanya berada pada identity assertion verification test cases. | Raw output test suites, `tests/identity/`, `tests/audit/sprint14/`, `ownership/`, `federation/` | `RECONCILED` |

---

## 2. REVISI & DAFTAR FILE YANG DIKOREKSI

- **Revision Sumber:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
- **Revision Repositori Dokumentasi:** Mengingat `whisnu/plan` merupakan remote repository terpisah yang tidak terklon sebagai working-tree lokal mandiri, deliverable dikembalikan sebagai berkas koreksi mandiri dan diarsipkan ke dalam zip supplement.
- **Daftar Berkas yang Dikoreksi:**
  1. `scratch/pe02_a1_supplement/PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md`
  2. `scratch/pe02_a1_supplement/PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`
  3. `scratch/pe02_a1_supplement/PE02_A1_TEST_RECONCILIATION.md`
  4. `scratch/pe02_a1_supplement/PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`
  5. `scratch/pe02_a1_supplement/PE02_A1_TARGETED_CORRECTION_REPORT.md` (berkas ini)

---

## 3. RINGKASAN PERUBAHAN DOKUMENTASI

1. **B-SUP-02 (Cakupan Active-Key Resolver):**  
   Dihapus klaim bahwa Individual Creator pasti tidak dapat diverifikasi. Diganti dengan bukti bahwa `ResolveActiveSigningAuthorityAt` dan `ActiveKeyAuthorizationAssertion` bersifat generik untuk kedua subject type, dengan catatan bahwa test suite existing hanya menyediakan test fixtures bertipe `ORGANIZATION`.
2. **C-SUP-02 (Cakupan Pencarian Album-wide Ownership):**  
   Pencarian diperluas ke seluruh direktori kode (`cmd/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`). Kesimpulan diperketat menjadi `NOT FOUND IN REPOSITORY AT REVISION fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`.
3. **D-SUP-01 (`SupportedFeatures` Preimage):**  
   Ditegaskan bahwa `SupportedFeatures` tidak masuk ke preimage `CanonicalJCS()` dan tidak diautentikasi oleh signature `RegistryIdentity`.
4. **E-SUP-02 (`RevokedKeys` Preimage & Signing Key):**  
   Ditegaskan bahwa `canonStr` hanya memuat `registry_id` dan `updated_at`, sedangkan `RevokedKeys` tidak masuk signature preimage. Dicantumkan kalimat wajib bahwa signature tidak mengikat isi `RevokedKeys`, pemilik key adalah node instance registry lokal (`s.cfg.IssuerPrivateKey`), dan tidak ada verifier untuk signature tersebut.
5. **E-SUP-01 (Makna `ONLINE_FRESH`):**  
   Ditegaskan bahwa `FreshnessOnlineFresh` murni klasifikasi jalur boolean (`isOffline == false`) tanpa pembuktian kesegaran jaringan/cache aktual (`ONLINE_FRESHNESS NOT ESTABLISHED`).
6. **Test Reconciliation:**  
   Direkonsiliasi secara matematis: 39 top-level tests + 19 nested subtests = 58 invocations. Dikoreksi klaim overbroad yang menyebut seluruh test menguji Organization; dipisahkan antara pengujian primitive/algoritmik (JCS, Subject ID), asset (ownership, federation), dan identity assertion verification (Organization).

---

## 4. KETERBATASAN BUKTI YANG MASIH TERSISA

1. **Jalur Penerbitan Assertion Individual Creator:** Belum ada fixture atau helper di repositori yang mendemonstrasikan penerbitan `ActiveKeyAuthorizationAssertion` oleh Individual Creator secara end-to-end.
2. **Integritas `RevokedKeys`:** Belum ada mekanisme native yang memberikan integritas kriptografis terhadap daftar key yang dicabut pada `RegistryKeyRevocationList`.
3. **Mekanisme Freshness Dinamis:** Belum ada verifier yang menghitung kesegaran waktu status pencabutan berdasarkan timestamp server resmi atau CRL TTL.

---

## 5. PERNYATAAN INTEGRITAS & DISIPLIN KERJA

- **Pernyataan Source Code:** Tidak ada source code, test code, schema, database, migration, API, atau konfigurasi aplikasi yang diubah selama penugasan ini.
- **Pernyataan Test Suite:** Tidak ada pengulangan eksekusi test suite yang dilakukan pada penugasan koreksi ini; seluruh rekonsiliasi didasarkan pada raw test output lengkap yang telah diperoleh pada pemeriksaan sebelumnya.
