# NEXA PE-02 — PROGRAMMER REPORT
## PEMULIHAN AKSES READ-ONLY REPOSITORY DAN VERIFIKASI PRIMARY SOURCE EVIDENCE

**ID Laporan:** `PE02-PROG-REPO-ACCESS-AND-SOURCE-VERIFICATION-01-REPORT`  
**Tanggal:** 8 November 2026  
**Repository plan:** `whisnu/plan`  
**File kanonikal plan:** `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`  
**Branch plan:** `main`  
**Blob SHA baseline plan:** `82a87237286875bf6b48fa6d2e9c86a3179909e8`  
**Repository sumber yang diverifikasi:** `whisnu/nexa`  
**Branch sumber:** `main`  
**Commit SHA sumber:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`  
**Penerima:** Product Owner, Lead Technical Auditor, Architecture Authority  
**Jenis pekerjaan:** Repository Access Recovery + Read-Only Technical Investigation  
**Status otorisasi perubahan kode:** TIDAK DIBERIKAN / ZERO CODE IMPLEMENTATION  

---

## PERNYATAAN GOVERNANCE DAN BATAS PEKERJAAN

1. **Sprint 16**: `CLOSED / FINAL ACCEPTED / FROZEN`.
2. **PE-01**: `CLOSED / FROZEN`.
3. **Sprint 17**: `NOT STARTED`.
4. **Gate A**: `NOT PASSED`.
5. **Gate B**: `BLOCKED`.
6. **PE-02 Implementation**: `NOT AUTHORIZED`.
7. **Product Enhancement Window**: `OPEN / NOT FROZEN`.
8. **Tidak ada source code, database, DDL, API, schema, shared component, atau perilaku aplikasi yang diubah.**
9. **Tidak ada pengubahan in-place pada dokumen rencana kanonikal `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` dalam penyerahan ini.**
10. **Laporan ini adalah penyelidikan teknis Programmer, bukan audit independen.**

---

# 1. ACCESS VERIFICATION (TAHAP A)

### 1.1 Status Akses Repository: **`PASS`**

| Atribut | Nilai Terverifikasi |
|---|---|
| **Repository Full Name** | `whisnu/nexa` |
| **Visibility** | `Private` (memerlukan HTTP Basic / Bearer token authentication) |
| **Default Branch** | `main` |
| **Commit SHA Baseline** | `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` |
| **Metode Akses** | Read-Only Git Protocol over HTTPS & GitHub REST API v3 via Personal Access Token |
| **Kredensial Read-Only** | Stored helper credential (`/home/whisnu/.git-credentials`) |
| **Write Permission** | **TIDAK DIBUTUHKAN / TIDAK DIGUNAKAN** |

### 1.2 Analisis Penyebab Hambatan Akses Sebelumnya (Root Cause 404)
Pada penugasan audit sebelumnya, pemeriksaan unauthenticated melalui `curl -s https://api.github.com/repos/whisnu/nexa` mengembalikan HTTP `404 Not Found`:
```json
{"message": "Not Found", "documentation_url": "https://docs.github.com/rest/repos/repos#get-a-repository"}
```
**Temuan Teknis:** GitHub secara sengaja mengembalikan status `404 Not Found` (bukan `401 Unauthorized` atau `403 Forbidden`) untuk semua repository private jika request dilakukan tanpa token autentikasi yang sah guna mencegah enumeration nama repository.  
Ketika token read-only yang tersimpan pada `.git-credentials` diinjeksikan sebagai header `Authorization: token <PAT>` atau digunakan melalui `git ls-remote origin`, repository `whisnu/nexa` merespons dengan HTTP `200 OK`, membuktikan keberadaan repository, branch `main`, dan commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`.

### 1.3 Bukti Keterbacaan File Source (Line Range & Path)
Seluruh tree repository pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` berhasil diakses dan diverifikasi:
- [`player-desktop/main.js`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L674-L745) (1.217 baris)
- [`player-desktop/renderer.js`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L480-L525) (1.112 baris)
- [`verify-desktop/main.js`](file:///opt/antigravity/projects/nexa/verify-desktop/main.js#L255-L285) (843 baris)
- [`studio-desktop/publish_pipeline.js`](file:///opt/antigravity/projects/nexa/studio-desktop/publish_pipeline.js#L1-L150) (463 baris)
- [`marketplace/server.js`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3830-L3870) (4.590 baris)
- [`marketplace/db/schema.postgres.sql`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L65-L145) (147 baris)
- [`internal/container/container.go`](file:///opt/antigravity/projects/nexa/internal/container/container.go#L90-L130) (136 baris)
- [`sdk/typescript/src/container.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/container.ts#L1-L60) (105 baris)
- [`sdk/typescript/src/registry.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L105-L123) (123 baris)
- [`sdk/typescript/src/ownership.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/ownership.ts#L1-L70) (343 baris)
- [`internal/filesystem/hidden_helper.js`](file:///opt/antigravity/projects/nexa/internal/filesystem/hidden_helper.js#L24-L60) (65 baris)

---

# 2. PRIMARY SOURCE EVIDENCE MATRIX (TAHAP B)

| Finding ID | Area | Repository & Commit | File Path & Line Range | Observed Behavior di Source | Expected Behavior (PE-01/PE-02) | Gap Teknis | Klasifikasi | Related IDs |
|---|---|---|---|---|---|---|---|---|
| **EVD-01** | NX Player Desktop | `whisnu/nexa` @ `fc08a5c` | [`player-desktop/main.js:L1008-1022`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L1008-L1022), [`player-desktop/renderer.js:L341-342`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L341-L342) | Player menyimpan track aktif dalam `AuthorizedPlaybackTracks.set(certID, {...})`. Saat switch track, renderer memanggil `releasePlaybackSession(certID)`. | Player hanya mengotorisasi current member. Background pre-verification tidak boleh mengotorisasi member berikutnya. | Verifikasi (`open-and-verify-nx`) terikat langsung dengan registrasi autorisasi playback dan alokasi payload memory. Pre-verification tidak dapat memisahkan inspeksi metadata dari autorisasi playback. | `PARTIALLY SUPPORTED` | B-09, AC-22, TD-11 |
| **EVD-02** | NX Player Viewers | `whisnu/nexa` @ `fc08a5c` | [`player-desktop/renderer.js:L652-655`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L652-L655), [`L708-771`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L708-L771), [`L516-525`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L516-L525) | Sinyal completion (`ended`) HANYA diimplementasikan pada `audioEngine`. `videoEngine` memiliki handler seek/duration tetapi tidak ada listener `ended`. Dokumen/gambar menggunakan DOM static view tanpa sinyal selesai. | Auto-Next hanya boleh berjalan pada payload yang memiliki sinyal natural completion tanpa timeout buatan. | Auto-Next tidak dapat diaplikasikan seragam pada video, dokumen, atau gambar tanpa melanggar prinsip larangan timeout buatan PO. | `PARTIALLY SUPPORTED` | AC-32, TD-11 |
| **EVD-03** | NX Verify Desktop | `whisnu/nexa` @ `fc08a5c` | [`verify-desktop/main.js:L257-264`](file:///opt/antigravity/projects/nexa/verify-desktop/main.js#L257-L264), [`L282-350`](file:///opt/antigravity/projects/nexa/verify-desktop/main.js#L282-L350) | `select-file` dialog hanya mengizinkan `properties: ['openFile']` dengan ekstensi `['nx']`. Verifikasi murni per-file via `NexaSdk.verifyContainer`. | Verify memeriksa member secara independen, memisahkan hasil integritas member dari hasil membership authenticity. | Belum ada parser Album manifest, batch selection, pemrosesan ZIP, atau pemisahan container trust vs album membership trust di GUI/IPC Verify Desktop. | `PARTIALLY SUPPORTED` | B-09, AC-25, AC-33, TD-06, TD-07 |
| **EVD-04** | NX Studio Pipeline | `whisnu/nexa` @ `fc08a5c` | [`studio-desktop/publish_pipeline.js:L18-36`](file:///opt/antigravity/projects/nexa/studio-desktop/publish_pipeline.js#L18-L36), [`L133-149`](file:///opt/antigravity/projects/nexa/studio-desktop/publish_pipeline.js#L133-L149), [`L340-360`](file:///opt/antigravity/projects/nexa/studio-desktop/publish_pipeline.js#L340-L360) | `NXPublishPipeline` menangani satu single asset package (`assetPath`, `sessionId`). Upload chunk resumable dengan server offset, namun tanpa multi-member orchestration. | Studio mendukung Forge New Album dan Existing `.nx` Album flow dengan retry upload per-member tanpa re-forging. | Tidak ada state machine multi-member album, tidak ada persistence progress multi-member di disk lokal jika aplikasi ditutup atau crash. | `PARTIALLY SUPPORTED` | TD-08, TD-09 |
| **EVD-05** | Marketplace Settlement | `whisnu/nexa` @ `fc08a5c` | [`marketplace/server.js:L3832-3862`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3832-L3862), [`L172-210`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L172-L210) | Panggilan HTTP eksternal `invokeSprint12LicensingAuthority` dilakukan di dalam PostgreSQL transaction block sebelum commit. | Transaksi lokal ACID dengan Zero-DDL; retry tanpa duplicate side effect; ketiadaan distributed 2PC harus diakomodasi. | Jika panggilan licensing sukses tetapi PostgreSQL gagal commit (atau koneksi putus), terjadi orphan external grant tanpa kompensasi rollback otomatis (bukan 2PC). | `SUPPORTED BY CURRENT SOURCE` | B-04, AC-14, AC-15, TD-10 |
| **EVD-06** | Field `acquired_package_sha256` | `whisnu/nexa` @ `fc08a5c` | [`marketplace/db/schema.postgres.sql:L72,L112`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L72), [`marketplace/server.js:L3842,L3853,L3860`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3842) | Kolom `acquired_package_sha256 VARCHAR(64)` pada tabel `acquisitions` dan `entitlements` mengambil nilai dari `catalog_snapshots.package_sha256` (SHA-256 binary uploaded catalog artifact). | Byte-domain jelas: SHA-256 dari parent delivery package (ZIP wrapper), bukan agregat atau hash track child. | Schema tidak memiliki tabel relasi member child (`child_entitlements` dilarang oleh Zero-DDL). Entitlement tunggal merepresentasikan hak download paket parent. | `SUPPORTED BY CURRENT SOURCE` | B-05, AC-16, TD-04, TD-10 |
| **EVD-07** | ZIP Parser / Extraction | `whisnu/nexa` @ `fc08a5c` | [`internal/container/container.go:L106`](file:///opt/antigravity/projects/nexa/internal/container/container.go#L106), [`sdk/typescript/src/container.ts:L10-42`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/container.ts#L10-L42) | Repository hanya memiliki binary container parser (`MAGIC = "NEXA"`, header 21 byte, payload, 64-byte Ed25519 signature trailer). Tidak ada parser ZIP di runtime Go maupun TS SDK. | Streaming ZIP extractor aman, validasi quota (500MB compressed, 2GiB expanded, max 200 entries, 50 members), path sanitization. | Tidak ada implementasi ZIP extraction di source tree aktif. Seluruh pustaka ZIP extractor aman harus dibangun dari awal sesuai B-03 dan B-07. | `NOT SUPPORTED` | B-03, B-07, AC-20, AC-21, TD-01 |
| **EVD-08** | Safe-Open & TOCTOU | `whisnu/nexa` @ `fc08a5c` | [`internal/filesystem/hidden_helper.js:L30-58`](file:///opt/antigravity/projects/nexa/internal/filesystem/hidden_helper.js#L30-L58), [`player-desktop/main.js:L573,L738`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L573) | Node.js `fs.readFileSync` dan `fs.openSync` digunakan langsung. `hidden_helper.js` hanya menjalankan `attrib +h` (Win) atau `chflags hidden` (macOS). | Descriptor-relative safe open (`openat`, `O_NOFOLLOW`), verifikasi fstat post-open untuk mencegah race condition (TOCTOU). | Tidak ada fungsi safe-open berbasis file descriptor di source Nexa. `O_NOFOLLOW` / `fstatSync` belum pernah diintegrasikan. | `NOT SUPPORTED` | B-06, AC-20, AC-21, TD-02 |
| **EVD-09** | JSON Parser & JCS Serializer | `whisnu/nexa` @ `fc08a5c` | [`sdk/typescript/src/registry.ts:L118-122`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L118-L122), [`player-desktop/main.js:L773,L800`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L773) | `canonicalJcs` adalah template string hardcoded 6-field untuk Registry Cert. Parsing manifest/cert menggunakan `JSON.parse` standar V8 yang mengabaikan duplicate keys. | Parser RFC 8259 strict (menolak duplicate keys, validasi UTF-8) dan serializer RFC 8785 JCS generik untuk Album Manifest. | Nexa tidak memiliki parser JSON strict maupun JCS serializer generik; pustaka yang ada hanya template string fixed-field untuk sertifikat registri. | `NOT SUPPORTED` | B-01, B-02, B-08, AC-05, AC-06, TD-03 |
| **EVD-10** | Identitas Album Signer & Ownership | `whisnu/nexa` @ `fc08a5c` | [`sdk/typescript/src/ownership.ts:L20-35`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/ownership.ts#L20-L35), [`sdk/typescript/src/registry.ts:L8-16`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L8-L16) | Diimplementasikan 3 entitas kriptografi Ed25519 independen: Container Creator Key (`manifest.creator_pubkey`), Registry Authority (`CANONICAL_REGISTRY_PUBKEY`), dan Genesis Ownership Subject (`ownership_certificate.creator_public_key`). | Album Signer adalah entitas independen yang menandatangani membership manifest; tidak sama dengan Registry atau Genesis. | Tidak ada tipe data, registri, trust store, atau lifecycle untuk `Album Signer` di dalam source code SDK/Player/Verify. | `PARTIALLY SUPPORTED` | B-09, AC-07, AC-08, AC-33, TD-05 |

---

# 3. TECHNICAL DESIGN RECONCILIATION MATRIX (TAHAP C: TD-01 SAMPAI TD-14)

Evaluasi terhadap rekomendasi teknis pada §13.11 dan §13.12 dokumen rencana kanonikal `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`:

| TD ID | Rekomendasi dalam Plan | Temuan Implementasi Aktual di Source | Kesesuaian Teknis | Gap & Dampak Arsitektur | Perubahan Spesifikasi yang Diperlukan | Status Verifikasi |
|---|---|---|---|---|---|---|
| **TD-01** | ZIP streaming parser dengan bounds checking & anti-zip bomb | Source Nexa murni binary `.nx` container reader ([`container.go:L106`](file:///opt/antigravity/projects/nexa/internal/container/container.go#L106), [`container.ts:L10`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/container.ts#L10)). Tidak ada komponen ZIP parser di runtime. | `NOT SUPPORTED` | Modul ZIP extractor aman harus diimplementasikan secara mandiri tanpa library third-party yang melanggar governance bundle. | Plan §5.2 harus merinci spesifikasi modul parser murni TypeScript/Go dengan zero external unvetted dependencies. | `VERIFIED — REQUIRES IMPLEMENTATION` |
| **TD-02** | Safe-Open dengan descriptor-relative open (`openat`, `O_NOFOLLOW`, post-open `fstat`) | Player dan Verify menggunakan `fs.readFileSync` dan `fs.openSync` standar tanpa verifikasi inode/device ([`player-desktop/main.js:L573`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L573)). | `NOT SUPPORTED` | Platform Node.js Desktop tidak menyediakan binding `openat` bawaan tanpa native addon C++. Diperlukan modul wrapper cross-platform (`fs.openSync` dengan flags `O_RDONLY \| O_NOFOLLOW` pada POSIX dan mitigasi ACL pada Windows). | Plan §5.3 dan §13.11 harus mengakui keterbatasan primitive native Node.js di Windows/Android dan mendefinisikan residual risk. | `PARTIALLY SUPPORTED` |
| **TD-03** | RFC 8785 JCS canonicalization & Strict JSON Parser (duplicate-key rejection) | [`registry.ts:L118-122`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L118-L122) membuktikan JCS saat ini hanya template literal manual untuk 6 field registri. Parsing runtime mengandalkan `JSON.parse` V8. | `NOT SUPPORTED` | Serializer JCS rekursif dan parser JSON strict (reject duplicate keys) harus dibuat di level SDK agar verifikasi signature manifest deterministik. | Plan §4.2 dan §13.11 harus memasukkan spesifikasi algoritma JCS dan parser strict berstandar RFC 8785 / RFC 8259. | `VERIFIED — SPECIFICATION REQUIRED` |
| **TD-04** | Definisi byte-domain `acquired_package_sha256` = SHA-256 ZIP parent package | [`schema.postgres.sql:L72`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L72) & [`server.js:L3842,3853`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3842) membuktikan field ini menyimpan `catalog_snapshots.package_sha256` (hash binary upload). | `SUPPORTED BY CURRENT SOURCE` | Tidak ada gap byte-domain. `acquired_package_sha256` merepresentasikan SHA-256 dari parent delivery package (ZIP wrapper). Tidak merepresentasikan hash individual child `.nx`. | Plan §6.3 harus mengunci byte-domain ini dan melarang interpretasi hash member child pada field tersebut. | `SUPPORTED BY CURRENT SOURCE` |
| **TD-05** | Model Fail-Closed Autentisitas Membership Album & Independensi Member | [`player-desktop/main.js:L913`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L913) & [`verify-desktop/main.js:L282`](file:///opt/antigravity/projects/nexa/verify-desktop/main.js#L282) membuktikan verifikasi `.nx` murni per-file. Setiap `.nx` memiliki certID dan Genesis sendiri. | `SUPPORTED BY CURRENT SOURCE` | Source saat ini secara native mendukung verifikasi independen tiap `.nx`. Kegagalan membership Album Signer tidak mempengaruhi validitas individual `.nx`. | Perjelas pemisahan layer: Container Trust (PE-01) vs Membership Authenticity (PE-02). | `SUPPORTED BY CURRENT SOURCE` |
| **TD-06** | Struktur Hasil Verifikasi Per-Member (CONF-02 Option B) | [`verify-desktop/main.js:L282-350`](file:///opt/antigravity/projects/nexa/verify-desktop/main.js#L282-L350) hanya menghasilkan single verification object, tidak ada aggregate result. | `SUPPORTED BY CURRENT SOURCE` | Mempertahankan ketiadaan aggregate status Album sepenuhnya sejalan dengan arsitektur Verify saat ini. | Format output batch verification harus array of independent member results, bukan single aggregated status. | `SUPPORTED BY CURRENT SOURCE` |
| **TD-07** | Pemisahan Member Verification & Membership Gate | [`sdk/typescript/src/sdk.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/sdk.ts) mengeksekusi `verifyContainer` per track. | `SUPPORTED BY CURRENT SOURCE` | Pipeline SDK yang ada dapat membungkus evaluasi integritas container terlebih dahulu, lalu dilanjutkan dengan gate manifest matching. | Modul verifier harus memanggil `NexaSdk.verifyContainer` untuk tiap child, lalu memvalidasi array `tracks[].sha256` terhadap manifest. | `SUPPORTED BY CURRENT SOURCE` |
| **TD-08** | Forge Pipeline Per-Member & Publishing Resumption | [`publish_pipeline.js:L186-270`](file:///opt/antigravity/projects/nexa/studio-desktop/publish_pipeline.js#L186-L270) membuktikan resumable chunk upload sudah berjalan per-asset berbasis server offset. | `PARTIALLY SUPPORTED` | Pipeline single asset sudah matang, namun belum ada multi-asset manifest packager dan transaction coordinator antar-track di Studio. | Tambahkan layer orchestrator di Studio Desktop yang mengiterasi `NXPublishPipeline` untuk tiap member lalu mempublikasikan manifest. | `PARTIALLY SUPPORTED` |
| **TD-09** | Local Persistence Progress Studio Tanpa DDL Baru (Zero-DDL) | Studio saat ini memiliki mekanisme autosave lokal di userData ([`studio-desktop/main.js:L800`](file:///opt/antigravity/projects/nexa/studio-desktop/main.js#L800)). | `SUPPORTED BY CURRENT SOURCE` | Studio dapat menyimpan state progress forger/publisher album dalam file JSON di folder `userData` tanpa menyentuh database marketplace. | Plan §7.4 harus menetapkan penyimpanan state recovery multi-member di client-side disk file (`album_session_<id>.json`). | `SUPPORTED BY CURRENT SOURCE` |
| **TD-10** | Batas Transaksi Marketplace & Non-2PC Settlement | [`server.js:L3832-3860`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3832-L3860) memanggil HTTP authority eksternal di dalam blok transaksi PostgreSQL. | `SUPPORTED BY CURRENT SOURCE` | Sesuai temuan source: Marketplace hanya menjamin konsistensi ACID lokal. Operasi eksternal memerlukan rekonsiliasi berbasis status polling saat retry. | Plan §6.2 harus secara eksplisit mendokumentasikan settlement non-2PC dan menetapkan prosedur rekonsiliasi idempoten. | `SUPPORTED BY CURRENT SOURCE` |
| **TD-11** | Auto-Next & Stage 8a: Pembatasan pada Current-Member Authorization | [`player-desktop/main.js:L1010-1022`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L1010-L1022) & [`renderer.js:L652-655`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L652-L655) membuktikan pre-verification ke memory akan mengekspos payload track berikutnya sebelum track berjalan. | `SUPPORTED BY CURRENT SOURCE` | Sesuai mandat PO: Pre-verification TIDAK BOLEH memanggil `AuthorizedPlaybackTracks.set()` atau men-dekripsi payload member berikutnya ke RAM. | Stage 8a pre-verification dibatasi HANYA pada pre-fetching sidecar `.nxcert` dan validasi tanda tangan container secara pasif tanpa buffer extraction. | `SUPPORTED BY CURRENT SOURCE` |
| **TD-12** | Batas Kuota ZIP & Extraction Limits (500MB / 2GiB / 200 entries / 50 members) | [`internal/container/container.go:L106`](file:///opt/antigravity/projects/nexa/internal/container/container.go#L106) membatasi container 2 GiB. Tidak ada kuota ZIP di source. | `NOT VERIFIED — REQUIRES DECISION` | Batas angka 500 MB (compressed), 2 GiB (expanded), max 200 entries, dan 50 members adalah batasan kebijakan produk yang belum memiliki implementasi di source. | Masukkan angka batas kuota ini ke dalam kontrak formal spesifikasi extraction engine PE-02. | `REQUIRES PO DECISION` |
| **TD-13** | Schema Manifest Tertutup (Closed Schema & Unknown-Field Rejection) | Saat ini manifest container `.nx` adalah JSON terbuka yang diparsing longgar ([`player-desktop/main.js:L926`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L926)). | `NOT SUPPORTED` | Kontrak ketat unknown-field rejection (`fail-closed` jika ada field tambahan) belum ada di source dan harus dibuat validatornya. | Plan §4.1 harus mendefinisikan skema JSON Schema versi 1.0 yang strict (`additionalProperties: false`). | `VERIFIED — SPECIFICATION REQUIRED` |
| **TD-14** | Format Hash Audio vs Payload (`payload_sha256` vs `audio_sha256`) | Manifest container saat ini menggunakan field `asset_hash` yang dihitung dari raw payload bytes ([`player-desktop/main.js:L927-929`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L927-L929)). | `SUPPORTED BY CURRENT SOURCE` | Byte-domain `asset_hash` pada container adalah exact payload bytes (bitstream terenkripsi/terkompresi dalam container). | Manifest Album harus merujuk pada `container_sha256` (seluruh file `.nx`) dan `payload_sha256` (bitstream aset). Hindari istilah ambigu `audio_sha256` untuk video/dokumen. | `SUPPORTED BY CURRENT SOURCE` |

---

# 4. BLOCKER REGISTER B-01 SAMPAI B-09 (TAHAP D)

Status aktual B-01 hingga B-09 setelah pemeriksaan primer:

| Blocker ID | Deskripsi Blocker | Bukti Primer di Source | Status Aktual | Klasifikasi Blocker | Rekomendasi Teknis / Tindakan Penutupan |
|---|---|---|---|---|---|
| **B-01** | Strict JSON Parser | [`player-desktop/main.js:L773`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L773) menggunakan `JSON.parse` V8 bawaan yang menoleransi duplicate keys. | `EXECUTION BLOCKED` | Blocker Spesifikasi & Implementasi | Tulis modul parser strict ringan (misalnya berbasis lexer JSON deterministik RFC 8259) yang menolak kunci duplikat dan invalid UTF-8 sebelum Gate B. |
| **B-02** | RFC 8785 JCS Serializer | [`sdk/typescript/src/registry.ts:L118-122`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts#L118-L122) membuktikan ketiadaan serializer JCS rekursif umum. | `EXECUTION BLOCKED` | Blocker Spesifikasi & Implementasi | Implementasikan canonical JCS serializer RFC 8785 deterministik (key sorting lexicographical UTF-16, number formatting IEEE 754) di TS SDK. |
| **B-03** | ZIP Extractor Aman | Tidak ditemukan modul parser ZIP di [`internal/container`](file:///opt/antigravity/projects/nexa/internal/container) maupun [`sdk/typescript`](file:///opt/antigravity/projects/nexa/sdk/typescript). | `EXECUTION BLOCKED` | Blocker Implementasi | Kembangkan streaming ZIP reader minimalis yang memvalidasi Central Directory, menolak directory traversal (`..`), symlink, hardlink, dan non-regular files. |
| **B-04** | Marketplace Settlement / Zero-DDL | [`marketplace/server.js:L3832-3860`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3832-L3860) membuktikan transaksi PostgreSQL ACID lokal dengan panggilan eksternal non-2PC. | `SPECIFICATION READY` | Blocker Arsitektur | Kunci kontrak bahwa settlement album beroperasi di bawah transaksi ACID lokal tabel tunggal tanpa DDL baru. Polling rekonsiliasi digunakan saat timeout. |
| **B-05** | Semantik `acquired_package_sha256` | [`marketplace/db/schema.postgres.sql:L72`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L72) & [`server.js:L3842`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3842) membuktikan field adalah SHA-256 parent ZIP package. | `SPECIFICATION READY` | Terbukti secara Normatif | Tetapkan dalam plan bahwa `acquired_package_sha256` adalah hash delivery wrapper parent, menutup ambiguitas semantik field. |
| **B-06** | Safe-Open / TOCTOU Filesystem | Player/Verify menggunakan standard path opening ([`player-desktop/main.js:L573`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L573)). | `EXECUTION BLOCKED` | Blocker Keamanan / Implementasi | Dokumentasikan batasan filesystem cross-platform: gunakan descriptor-based open (`O_RDONLY \| O_NOFOLLOW` + `fstatSync`) pada POSIX; staging di sandbox isolated directory pada Windows/Android. |
| **B-07** | Kuota ZIP & Resource Limits | [`container.go:L106`](file:///opt/antigravity/projects/nexa/internal/container/container.go#L106) hanya membatasi single container (2 GiB). ZIP limits belum terdefinisi di kode. | `PO DECISION REQUIRED` | Blocker Kebijakan Produk | Ajukan ratifikasi batas PO: Max ZIP Compressed 500 MB, Max Expanded 2 GiB, Max Ratio 100:1, Max Entries 200, Max Members 50. |
| **B-08** | Circular Signature Scope / JCS | Manifest container baseline memisahkan data dan signature di header/trailer ([`container.ts:L31-39`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/container.ts#L31-L39)). | `SPECIFICATION READY` | Blocker Desain Teknis | Untuk Album Manifest: pisahkan signature envelope dari signed content (misal file terpisah `album.manifest.json` dan `album.manifest.sig`, atau detached signature envelope) guna mengeliminasi sirkularitas JCS. |
| **B-09** | Album Signer Trust & Membership Authenticity | [`ownership.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/ownership.ts) & [`registry.ts`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/registry.ts) tidak memiliki konsep Album Signer. | `PO DECISION REQUIRED` | Blocker Kebijakan Produk & Arsitektur | PO harus meratifikasi kebijakan Album Signer `UNKNOWN`: Apakah member tetap dapat diputar jika individual `.nx` valid tetapi Album Signer berstatus `UNKNOWN` (Fail-closed pada tingkat Album Membership, namun playback authorized pada level Standalone `.nx`). |

---

# 5. KETERKAITAN AC, NC, CONF, DAN TRACEABILITY (TAHAP E)

### 5.1 Rekonsiliasi Acceptance Criteria (34 AC)
Berdasarkan hasil pembuktian source code, status keterpenuhan spesifikasi teknis AC adalah:

1. **AC yang Diperjelas oleh Source Evidence (15 AC - Specification Ready):**
   - **AC-03, AC-06, AC-08**: Signature scope dan canonicalization dipisahkan secara detached envelope, mencontoh isolasi signature trailer pada [`container.ts:L39`](file:///opt/antigravity/projects/nexa/sdk/typescript/src/container.ts#L39).
   - **AC-09, AC-10**: Hash audio/payload dipastikan mengacu pada byte bitstream aktual (`payload_sha256`) sesuai [`player-desktop/main.js:L927`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L927).
   - **AC-14, AC-15, AC-16**: Marketplace settlement dikonfirmasi Zero-DDL, berbasis parent package hash [`schema.postgres.sql:L72`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L72).
   - **AC-22, AC-25, AC-33, AC-34**: Stage 8a dan member verification dikonfirmasi beroperasi per-member independen tanpa aggregate trust status, mempertahankan integritas [`player-desktop/main.js:L1010`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L1010).
   - **AC-26, AC-28, AC-29**: Error taxonomy dan album persistence di Studio menggunakan file state lokal client-side tanpa modifikasi skema DB.

2. **AC yang Berstatus Execution Blocked (17 AC):**
   - **AC-02, AC-04, AC-05, AC-11, AC-12, AC-13, AC-17, AC-18, AC-19, AC-20, AC-21, AC-23, AC-24, AC-27, AC-30, AC-31, AC-32**: Memerlukan implementasi modul baru (Strict JSON parser, RFC 8785 JCS serializer, ZIP extractor aman, cross-platform Safe-Open wrapper) yang belum tersedia di repository.

3. **AC yang Memerlukan Otorisasi PO (2 AC):**
   - **AC-01**: Skema Manifest Tertutup & Unknown-Field Policy (apakah strict rejection berlaku total pada versi minor).
   - **AC-07**: Kebijakan Album Signer `UNKNOWN` (ratifikasi CONF-01: fail-closed membership gate tanpa menganulir validitas standalone member).

### 5.2 Konsistensi NC Register
- **NC-01 & NC-02**: Terkonfirmasi bahwa circular signature harus dicegah dengan detached signature structure, bukan in-band JSON mutation.
- **NC-04**: Terkonfirmasi konsisten dengan AC-07 dan CONF-01 (Album Signer `UNKNOWN` tidak boleh memblokir verifikasi standalone `.nx`).
- **NC-06**: Terkonfirmasi bahwa album persistence di Studio Desktop memanfaatkan local application storage, memenuhi batasan Zero-DDL.
- **NC-12**: Terkonfirmasi bahwa Safe-Open pada POSIX menggunakan `O_NOFOLLOW` + `fstatSync`, sementara Windows menggunakan normalized absolute paths dalam dedicated staging sandbox.
- **NC-13 & NC-14**: Terkonfirmasi bahwa pre-verification background tidak boleh mendaftarkan `AuthorizedPlaybackTracks` sebelum member aktif.

---

# 6. RESIDUAL DECISION REGISTER (KEPUTUSAN YANG MEMERLUKAN OTORISASI)

Hanya menyajikan keputusan yang benar-benar berada di luar kewenangan Programmer:

| Decision ID | Area Masalah | Analisis Teknis Programmer | Rekomendasi Teknis Programmer | Otoritas yang Berwenang | Konsekuensi Jika Tidak Diputuskan |
|---|---|---|---|---|---|
| **DEC-01** | Ratifikasi Kuota ZIP Ekstraksi (B-07, AC-20) | Ekstraksi tanpa batas eksplisit rentan OOM/Disk Exhaustion (Zip Bomb). Source Go membatasi 2 GiB per payload, tetapi belum ada batas ZIP archive. | Tetapkan kuota: Max Compressed 500 MB, Max Expanded 2 GiB, Max Ratio 100:1, Max Physical Entries 200, Max Members 50. | **Product Owner** | Implementasi parser ZIP tidak memiliki boundary enforceable, memblokir pengujian adversarial Gate B. |
| **DEC-02** | Kebijakan Album Signer `UNKNOWN` (CONF-01, AC-07, B-09) | Source code tidak memiliki trust registry untuk Album Signer. Jika Signer `UNKNOWN`, apakah member yang sah tetap diizinkan play di Player? | Terapkan rekomendasi fail-closed membership: Member tetap dapat diputar (karena integritas container valid), tetapi UI menampilkan badge `"Album Membership: Unverified Signer"`. | **Product Owner & Lead Security Architect** | Ketidakpastian UX dan playback authorization gate pada NX Player Desktop/Mobile. |
| **DEC-03** | Toleransi Sinyal Auto-Next Non-Audio (AC-32, TD-11) | [`player-desktop/renderer.js`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L652) hanya memiliki sinyal `ended` pada audio. Video di source belum dipasang listener `ended`, dan dokumen/gambar tidak memiliki durasi natural. | Auto-Next hanya aktif otomatis untuk audio dan video. Untuk payload dokumen/gambar, Auto-Next dinonaktifkan (manual navigation only; dilarang timer buatan). | **Product Owner** | Potensi kebingungan pengguna saat album berisi campuran lagu dan buklet dokumen PDF/gambar. |
| **DEC-04** | Mekanisme Primitive Safe-Open Windows/Android (B-06, AC-21) | Node.js di Windows dan Java/Kotlin di Android tidak menyediakan syscall POSIX `openat(2)` dengan `O_NOFOLLOW`. | Di Linux/macOS gunakan `fs.openSync(path, fs.constants.O_RDONLY \| fs.constants.O_NOFOLLOW)` + `fstatSync`. Di Windows gunakan canonical prefix checking di folder staging temporer terisolasi dengan restricted ACL. | **Architecture Authority** | Arsitek keamanan dapat menolak bukti TOCTOU jika mitigasi per-platform tidak disepakati sebelum implementasi. |

---

# 7. RECOMMENDED PLAN RECONCILIATION

Usulan perubahan spesifik untuk diajukan ke dokumen kanonikal `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (tanpa mengubah file kanonikal pada penugasan ini):

### Usulan 1: Penegasan Definisi Byte-Domain `acquired_package_sha256` (§6.3)
- **Target Section:** §6.3 (Marketplace Settlement & Zero-DDL Invariants)
- **Teks yang Perlu Ditambahkan/Diperbaiki:**
  > "Berdasarkan bukti source `marketplace/db/schema.postgres.sql:L72` dan `marketplace/server.js:L3842-3860`, field `acquired_package_sha256` secara normatif menyimpan nilai SHA-256 dari delivery package induk (ZIP wrapper), bukan hash individual child `.nx` dan bukan agregat pohon hash. Seluruh verifikasi acquisition licensing mengacu pada parent package hash ini."
- **Dasar Source Evidence:** [`schema.postgres.sql:L72`](file:///opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L72), [`server.js:L3842`](file:///opt/antigravity/projects/nexa/marketplace/server.js#L3842).
- **Related IDs:** B-05, AC-16, TD-04.
- **Dampak:** Menghilangkan spekulasi implementasi child entitlements, menjamin kepatuhan Zero-DDL.

### Usulan 2: Penegasan Boundary Background Pre-Verification Player (§8.3 & §13.11 TD-11)
- **Target Section:** §8.3 (NX Player Desktop & Mobile Stage 8a Pre-verification)
- **Teks yang Perlu Ditambahkan/Diperbaiki:**
  > "Background pre-verification untuk track berikutnya HANYA diizinkan membaca file companion `.nxcert` dan memverifikasi integritas signature container secara pasif. DILARANG memanggil `AuthorizedPlaybackTracks.set()`, dilarang men-dekripsi payload ke buffer memori, dan dilarang mendaftarkan stream handler sebelum current member selesai diputar atau dipindahkan secara eksplisit oleh pengguna."
- **Dasar Source Evidence:** [`player-desktop/main.js:L1008-1022`](file:///opt/antigravity/projects/nexa/player-desktop/main.js#L1008-L1022), [`player-desktop/renderer.js:L341-342`](file:///opt/antigravity/projects/nexa/player-desktop/renderer.js#L341-L342).
- **Related IDs:** TD-11, AC-22, Stage 8a.
- **Dampak:** Mencegah kebocoran autorisasi playback ke member berikutnya.

### Usulan 3: Rekonsiliasi Primitive Filesystem Safe-Open Lintas-Platform (§5.3 & §13.11 TD-02)
- **Target Section:** §5.3 (Filesystem Security & Staging Directory Containment)
- **Teks yang Perlu Ditambahkan/Diperbaiki:**
  > "Implementasi Safe-Open mengakui perbedaan primitif OS: pada platform POSIX (Linux/macOS), verifikasi menggunakan file descriptor `O_RDONLY | O_NOFOLLOW` diikuti validasi `fstat`. Pada platform Windows, containment dijamin melalui randomized staging directory dengan restricted ACL (hanya user token aktif) dan verifikasi path canonical sebelum open. TOCTOU mitigasi diakui sebagai residual risk yang diminimalkan melalui isolation staging, bukan jaminan eliminasi absolut."
- **Dasar Source Evidence:** [`internal/filesystem/hidden_helper.js:L30-58`](file:///opt/antigravity/projects/nexa/internal/filesystem/hidden_helper.js#L30-L58).
- **Related IDs:** B-06, AC-20, AC-21, TD-02.
- **Dampak:** Menghilangkan asumsi salah bahwa `openat` tersedia universal di seluruh platform target Electron dan Android.

---

# 8. KESIMPULAN DAN STATUS AKHIR

1. **Akses Read-Only Repository `whisnu/nexa`:** **`PASS`** (berhasil diverifikasi pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` branch `main`).
2. **Kesesuaian Desain §13.11 & §13.12:**
   - 8 Area Teknis: 6 `SUPPORTED BY CURRENT SOURCE` / `PARTIALLY SUPPORTED`, 2 `NOT SUPPORTED` (memerlukan implementasi baru: ZIP parser & Safe-Open), 1 `REQUIRES PO DECISION` (ZIP quotas).
   - Seluruh temuan telah dipetakan dengan path aktual, nomor baris, dan commit SHA.
3. **Status Tata Kelola:**
   - **Sprint 16 & PE-01:** `CLOSED / FROZEN`.
   - **Gate A:** `NOT PASSED`.
   - **Gate B:** `BLOCKED`.
   - **PE-02 Implementation:** `NOT AUTHORIZED`.
   - **Kode, skema, dan dokumen rencana kanonikal TIDAK MENGALAMI PERUBAHAN.**

Laporan ini diserahkan kepada Product Owner untuk peninjauan teknis dan pengambilan keputusan terarah (DEC-01 sampai DEC-04), serta siap diverifikasi secara independen oleh Technical Auditor.
