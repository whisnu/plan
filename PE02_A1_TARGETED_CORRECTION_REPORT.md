# NEXA PE-02 A1 — TARGETED CORRECTION REPORT
## RECONCILIATION OF DOCUMENTATION & TECHNICAL EVIDENCE RESIDUALS (FINAL RETURN)

- **Repository Target:** `whisnu/plan`
- **Branch Target:** `main`
- **Canonical PLAN:** `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (mirrored locally at `evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`)
- **Source Repository:** `whisnu/nexa`
- **Source Branch:** `main`
- **Reported Source Revision:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (reported in Programmer evidence; not independently verified by AA)
- **Working-Tree Classification:** `DIRTY — UNTRACKED FILES` (Zero tracked modifications; 2 pre-existing untracked documentation files: `docs/roadmaps/Nexa_Development_Roadmap_v4_8.md` and `docs/whitepapers/Nexa_White_Paper_v5_6.md`)
- **Date:** 2026-11-10
- **Assigned Role:** Programmer
- **Reviewing Authority:** Architecture Authority (AA)
- **Implementation Authorization Status:** PE-02 Implementation NOT AUTHORIZED

---

## 1. RESIDUAL CORRECTION MATRIX

| Residual | Hasil Akhir & Pembatasan Scope | Dokumen Terdampak | Evidence / Referensi Utama | Status |
| :--- | :--- | :--- | :--- | :--- |
| **B-SUP-02** | `ResolveActiveSigningAuthorityAt` tidak menerima atau mengevaluasi `subject_type`. `ActiveKeyAuthorizationAssertion` tidak memuat `subject_type` dan mengikat URN `SubjectID`. `IdentityVerifier.ExecutePipeline` memanggil resolver yang sama untuk Individual dan Organization. Test pipeline assertion yang ada (`TestVerificationPipelineVerified`) secara eksplisit menggunakan fixture `SubjectTypeOrganization`; test primitive (JCS, Ed25519, Subject ID derivation) dan rule algoritma bersifat subject-agnostic. Dedicated end-to-end Individual Creator pipeline test tidak ditemukan dalam cakupan evidence yang tersedia. Temuan ini tidak membuktikan keberhasilan end-to-end Individual Creator dan tidak mengindikasikan adanya pemblokiran oleh resolver. | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md`<br>`PE02_A1_TEST_RECONCILIATION.md` | `active_key.go:L93-L154`<br>`verifier.go:L77-L81, L156`<br>`domain/identity.go:L99-L114` | `CLOSED (DOCUMENTATION RECONCILED)` |
| **C-SUP-02** | Pencarian dibatasi secara eksplisit pada 11 direktori kode yang terdokumentasi: `cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/` pada revision `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (sebagaimana dilaporkan dalam evidence Programmer, bukan verifikasi independen AA). Tidak ditemukan struktur kepemilikan multi-aset, agregasi Album, hak kompilasi, atau publisher-origin authority. Klaim negatif dibatasi menjadi `NOT FOUND IN EXAMINED CODE DIRECTORIES` dan tidak menyatakan ketiadaan di seluruh repositori. | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md` | `domain/ownership.go:L53-L68`<br>`cert.go:L15-L24`<br>Grep regex pada 11 direktori kode | `CLOSED (BOUNDED SCOPE RECONCILED)` |
| **E-SUP-02** | `GetRegistryKeyRevocations` menandatangani string `canonStr` yang HANYA memuat `registry_id` dan `updated_at`. Field `RevokedKeys` sepenuhnya dikecualikan dari preimage tanda tangan. Private key yang digunakan adalah `s.cfg.IssuerPrivateKey` (dari `ISSUER_PRIVATE_KEY_HEX`) dengan public key counterpart `s.cfg.IssuerPublicKey` (dari `ISSUER_PUBLIC_KEY_HEX`). Hubungan otoritas key, distribusi public key ke verifier, dan trust relationship berstatus `NOT VERIFIED FROM AVAILABLE EVIDENCE`. Verifier untuk `ListSignature` berstatus `NOT FOUND IN EXAMINED SEARCH SCOPE` (pencarian di `internal/`, `pkg/`, `apps/`). Tidak ditemukan mekanisme autentikasi alternatif dalam cakupan yang diperiksa. | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md` | `service.go:L75-L88`<br>`registry_identity.go:L24-L29`<br>`config.go:L140-L158` | `CLOSED / NOT VERIFIED PER ELEMENT` |
| **Test Reconciliation** | Total test dinormalisasi menjadi **39 top-level tests + 19 nested subtests = 58 total test invocations** (seluruhnya PASS). Angka 43 adalah hasil penjumlahan unnormalized dari pelaporan awal dan tidak dipertahankan. Klasifikasi test disinkronkan: dibedakan antara test yang secara eksplisit menggunakan Organization assertion, test primitive matematika/kriptografi subject-agnostic, test rule algoritma subject-agnostic, test level aset, test level federasi, dan test regresi yang tidak diklasifikasikan (`NOT CLASSIFIED`). | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md`<br>`PE02_A1_TEST_RECONCILIATION.md` | Raw output `go test` pada 4 suite:<br>`tests/identity`<br>`tests/audit/sprint14`<br>`ownership`<br>`federation` | `CLOSED (INVENTORY & CLASSIFICATION RECONCILED)` |
| **D-SUP-01** | `SupportedFeatures` ada di struct `RegistryIdentity`, namun fungsi `CanonicalJCS()` mengecualikannya dari signature preimage. `service.go:L69` menandatangani `CanonicalJCS()`, dan `VerifySignature()` memverifikasi `CanonicalJCS()`. Field ini tidak diautentikasi oleh `IdentitySignature`. Konsumen tidak boleh menganggap field ini terautentikasi oleh `VerifySignature()`. Kesimpulan dibatasi pada examined scope. | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md` | `registry_identity.go:L13-L63`<br>`service.go:L62-L71` | `PRESERVED` |
| **E-SUP-01** | `FreshnessOnlineFresh` diset di `verifier.go:L34-L37` murni berdasarkan argumen boolean input `!isOffline`. Tidak ada query jaringan, validasi timestamp, TTL cache, atau pengecekan respons Registry. Klasifikasi dipertahankan sebagai: `ONLINE_CLASSIFICATION — ONLINE FRESHNESS NOT ESTABLISHED`. | `PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`<br>`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md` | `domain/identity.go:L158-L165`<br>`verifier.go:L34-L42` | `PRESERVED` |

---

## 2. DOKUMEN YANG DISELARASKAN & RINGKASAN PERUBAHAN

Kelima dokumen paket A1 telah diperbarui dan diselaraskan secara konsisten tanpa ada kontradiksi silang:

1. **`PE02_A1_EVIDENCE_INDEX_SUPPLEMENT.md`**
   - **Perubahan B-SUP-02:** Menghilangkan klaim overbroad bahwa seluruh test di identity dan audit adalah Organization-specific; menegaskan sifat generik resolver dan bahwa fixture pipeline menggunakan Organization sementara test primitive bersifat subject-agnostic.
   - **Perubahan C-SUP-02:** Membatasi status menjadi `NOT FOUND IN EXAMINED CODE DIRECTORIES` dengan menyebutkan ke-11 direktori kode dan revision yang dilaporkan (`fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`).
   - **Perubahan E-SUP-02:** Mencantumkan hubungan signing key (`IssuerPrivateKey`) dan public key (`IssuerPublicKey`) dari konfigurasi lokal, menyatakan trust/distribusi sebagai `NOT VERIFIED FROM AVAILABLE EVIDENCE`, dan verifier sebagai `NOT FOUND IN EXAMINED SEARCH SCOPE`.
   - **Sinkronisasi E-SUP-01 & D-SUP-01:** Mempertahankan `ONLINE_CLASSIFICATION — ONLINE FRESHNESS NOT ESTABLISHED` dan eksklusi `SupportedFeatures` dari preimage.

2. **`PE02_A1_SEARCH_SCOPE_SUPPLEMENT.md`**
   - **Perubahan Group B:** Menjelaskan secara presisi bahwa resolver dan assertion struct tidak memeriksa `subject_type`, pipeline memanggil resolver untuk kedua tipe, fixture assertion pipeline menggunakan Organization, primitive JCS/Ed25519/Subject ID adalah subject-agnostic, dan 0 test end-to-end Individual Creator ditemukan.
   - **Perubahan Group C:** Menegaskan batas pencarian pada 11 direktori kode (`cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`). Menghapus klaim repository-wide.
   - **Perubahan Group E:** Menjelaskan detail konfigurasi `IssuerPrivateKey` dan `IssuerPublicKey`, eksklusi `RevokedKeys` dari preimage `canonStr`, batasan pencarian verifier di `internal/`, `pkg/`, `apps/` (`NOT FOUND IN EXAMINED SEARCH SCOPE`), dan status unverified trust.
   - **Perubahan Batas & Limitasi:** Menulis ulang Bab 2 untuk menyatakan batas pencarian secara jujur, status revision yang dilaporkan, dan bahwa ketiadaan bukti di luar direktori kode tidak diubah menjadi asumsi ketiadaan repository-wide.

3. **`PE02_A1_SOURCE_EVIDENCE_SUPPLEMENT.md`**
   - **Perubahan B-SUP-02:** Memperjelas kutipan source `active_key.go`, `verifier.go`, dan `domain/identity.go`. Menyusun kesimpulan rekonsiliasi yang membedakan ketiadaan pemeriksaan `subject_type` pada resolver, pemanggilan identik pada pipeline, dan ketiadaan dedicated end-to-end test untuk Individual Creator.
   - **Perubahan C-SUP-02:** Mengubah judul dan kesimpulan temuan C-SUP-02 menjadi `NOT FOUND IN EXAMINED CODE DIRECTORIES`.
   - **Perubahan E-SUP-02:** Menjelaskan asal signing key dari `ISSUER_PRIVATE_KEY_HEX`, keberadaan counterpart `IssuerPublicKey`, status unverified untuk otoritas dan distribusi public key, pernyataan eksplisit bahwa `RevokedKeys` tidak masuk signature preimage, dan ketiadaan verifier di examined search scope.
   - **Perubahan Rekonsiliasi Test:** Memperbarui ringkasan test execution menjadi 39 top-level + 19 nested = 58 invocations, dengan klasifikasi subjek yang konsisten.

4. **`PE02_A1_TEST_RECONCILIATION.md`**
   - **Inventaris Test:** Menetapkan dan mempertahankan 39 top-level tests + 19 nested subtests = 58 invocations (seluruhnya PASS). Menjelaskan secara matematis asal angka 43 unnormalized dan menegaskan angka tersebut tidak lagi digunakan.
   - **Klasifikasi Per Test Case:** Memberikan label klasifikasi eksplisit pada setiap test: `[ORGANIZATION EXPLICIT]`, `[SUBJECT-AGNOSTIC PRIMITIVE]`, `[SUBJECT-AGNOSTIC MECHANISM]`, `[ASSET-LEVEL]`, `[FEDERATION-LEVEL]`, dan `[NOT CLASSIFIED]`.
   - **Penegasan Batas:** Menghapus klaim bahwa seluruh test identity/audit menguji Organization; menetapkan bahwa primitive matematika dan rule algoritma bersifat subject-agnostic, fixture assertion pipeline menggunakan Organization, dan ketiadaan test Individual Creator tidak disimpulkan sebagai keberhasilan maupun penolakan.

5. **`PE02_A1_TARGETED_CORRECTION_REPORT.md` (Dokumen ini)**
   - Menjadi laporan sintesis final satu kali yang mencerminkan seluruh hasil rekonsiliasi, matriks koreksi, daftar perubahan per dokumen, konfirmasi kepatuhan ruang lingkup, dan deklarasi residual yang belum terverifikasi.

---

## 3. DEKLARASI RESIDUAL FINAL (UNVERIFIED ELEMENTS)

Sesuai aturan penanganan ketidakpastian (§6 handoff), elemen-elemen berikut secara jujur dicatat sebagai gap atau belum terverifikasi berdasarkan evidence yang tersedia, tanpa membuat asumsi atau investigasi baru:

1. **Otoritas & Distribusi Public Key CRL:** Evidence konfigurasi membuktikan adanya `s.cfg.IssuerPrivateKey` (`ISSUER_PRIVATE_KEY_HEX`) dan `s.cfg.IssuerPublicKey` (`ISSUER_PUBLIC_KEY_HEX`) pada instance registry node lokal. Namun, bagaimana public key tersebut diperoleh oleh verifier eksternal, siapa yang memiliki otoritas penerbitan CRL di tingkat jaringan, bagaimana key didistribusikan, dan apakah verifier mengevaluasinya berstatus:
   `NOT VERIFIED FROM AVAILABLE EVIDENCE`.
2. **Dedicated End-to-End Test Individual Creator:** Source code membuktikan resolver dan assertion struct bersifat generik serta dipanggil tanpa diskriminasi tipe subjek oleh pipeline. Namun, fixture test assertion pipeline yang ada hanya menggunakan `SubjectTypeOrganization`. Pembuktian aliran end-to-end Individual Creator di lingkungan produksi berstatus:
   `NOT FOUND IN EXAMINED SCOPE`.
3. **Cakupan Pencarian di Luar 11 Direktori Kode:** Ketiadaan representasi Album-wide ownership dan publisher-origin authority telah dibuktikan pada 11 direktori kode (`cmd/`, `internal/`, `pkg/`, `marketplace/`, `studio-desktop/`, `player-desktop/`, `verify-desktop/`, `mobile/`, `storage/`, `sdk/`, `migrations/`). Namun, keberadaan representasi di luar 11 direktori tersebut (misalnya direktori dokumentasi, test suites tambahan, atau format non-Go) berstatus:
   `NOT EXAMINED / UNVERIFIED`.
4. **Verifier CRL & Dual-Horizon Logic:** Tidak ditemukan fungsi verifikasi untuk `ListSignature` pada scope pencarian `internal/`, `pkg/`, `apps/`, dan tidak ditemukan perbandingan waktu `revoked_at` vs `recorded_at` pada verifier. Status:
   `NOT FOUND IN EXAMINED SEARCH SCOPE`.

---

## 4. KONFIRMASI KEPATUHAN RUANG LINGKUP (SCOPE CONFIRMATION)

Programmer memberikan konfirmasi eksplisit berikut:

- **Source code tidak diubah:** Zero source code modifications di seluruh repositori.
- **Schema, API, & konfigurasi tidak diubah:** Zero DDL, database migrations, endpoint definitions, atau configuration file changes.
- **Test code tidak diubah:** Zero modifications to existing test files.
- **Test suite tidak dijalankan ulang:** Rekonsiliasi didasarkan murni pada raw output test executions yang sudah lengkap dan terdokumentasi.
- **Tidak ada investigasi repository-wide baru:** Batas pencarian dibatasi sesuai data yang benar-benar tercatat dalam evidence.
- **Tidak ada keputusan arsitektur atau PO yang diubah:** Dokumen kanonis `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` tetap menjadi rujukan arsitektur tunggal; keputusan PO mengenai Opsi A1 tetap utuh.
- **Tidak ada otorisasi implementasi yang diterbitkan:** Rekonsiliasi ini murni pekerjaan dokumentasi dan bukti teknis A1.

---

## 5. STATUS TATA KELOLA (GOVERNANCE LOCK)

- **Sprint 16:** `CLOSED / FINAL ACCEPTED / FROZEN`
- **PE-01:** `CLOSED / FROZEN`
- **Sprint 17:** `NOT STARTED`
- **PE-02 Gate A:** `NOT PASSED` (menunggu penetapan AA)
- **PE-02 Gate B:** `BLOCKED` (menunggu penetapan AA)
- **PE-02 Implementation:** `NOT AUTHORIZED`
- **Tindak Lanjut:** Penugasan dokumentatif Programmer pada handoff ini telah **SELESAI**. Seluruh berkas diserahkan kepada Architecture Authority (AA) untuk evaluasi penutupan residual dan finalisasi Architecture Baseline A1 pada PLAN kanonis.
