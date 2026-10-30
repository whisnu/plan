# NEXA PE-02 — HANDLING ALBUM IMPLEMENTATION PLAN
## PROGRAMMER PROMPT V6.9.4-REV6 — TARGETED HISTORICAL RECONCILIATION, DEFECT PREVENTION & READINESS GATE
### Consolidated Implementation Plan, Source-Bounded Traceability & Failure-Prevention Review (Task ID: NEXA-PE02-TARGETED-CORRECTION-REV6)

> **DISPOSISI HASIL AUDIT KOMPREHENSIF & HANDOFF PROGRAMMER (TEMUAN 1 s.d. 10 & 8 SPESIFIKASI TAMBAHAN):**
> - **Gate A (Kualitas Dokumen Plan):** **`NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL CONFLICTS REMAIN`**
> - **Gate B (Kesiapan Eksekusi Implementasi):** **`BLOCKED`**
> - **Otorisasi Implementasi Kode PE-02:** **`NOT AUTHORIZED` (DILARANG KERAS MEMULAI KODING / MIGRASI DATABASE)**
> - **Sprint 16 Baseline:** 🔒 **`CLOSED / FINAL ACCEPTED / FROZEN`** (Tidak Boleh Diubah)
> - **PE-01 Baseline:** 🔒 **`CLOSED / FROZEN`** (Tidak Boleh Diubah)
> - **Sprint 17 Milestone:** ⏸️ **`NOT STARTED`** (Belum Dimulai)
> - **Blocker Struktural & Ketidakpastian Kriptografi Kritis:**
>   - **Kriptografi Manifest (Circular Dependency — B-08):** **`BLOCKED — REQUIRES CLARIFICATION`** (`album_signer_signature` berada di dalam payload yang dikanonisasi JCS).
>   - **B-04 / NC-08 / CONF-03:** **`BLOCKED`** (Zero-DDL Constraint & Ketiadaan 2PC Marketplace Transaksi Terdistribusi).
>   - **B-05 / NC-09:** **`BLOCKED`** (Ketidakpastian Semantik Kolom `acquired_package_sha256` & Child Row Database).
>   - **B-09 / NC-04 / CONF-01:** **`PO DECISION REQUIRED`** (Kebijakan Otorisasi Pemutaran Album Signer `UNKNOWN`).
>   - **NC-14 / CONF-02:** **`CONFLICT — STOP AND CLARIFY`** (Hierarki Status Agregat NX Verify).

---

## 1. IDENTITAS DOKUMEN, FASE, STATUS, DAN MATRIKS PENUTUPAN AUDIT

### 1.1 Identitas dan Batas Kewenangan Tugas
Dokumen ini merupakan satu-satunya artefak kanonikal (*Single Canonical Artifact Delivery*) yang mengonsolidasikan perencanaan teknis penanganan Album (`PE-02`) pada era post-Sprint 16 / pre-Sprint 17 Nexa Ecosystem. Dokumen ini disiapkan murni untuk koreksi terarah spesifikasi tata kelola dan pengujian (*Plan Correction Only*), dan **SECARA EKSPLISIT TIDAK MEMBERIKAN OTORISASI IMPLEMENTASI KODE SUMBER MAUPUN SKEMA DATABASE**.

| Parameter Tata Kelola | Nilai Resmi | Parameter Tata Kelola | Nilai Resmi |
|---|---|---|---|
| **Dokumen ID** | `PE-02-PLAN-REV6-RECONCILED` | **Fase Ekosistem** | Post-Sprint 16 / Pre-Sprint 17 |
| **Status Gate A** | `NOT PASSED — REQUIRES TARGETED CORRECTIONS` | **Status Gate B** | `BLOCKED` |
| **Otorisasi Implementasi** | `NOT AUTHORIZED` | **Sprint 16 Baseline** | 🔒 `CLOSED / FROZEN` |
| **PE-01 Baseline** | 🔒 `CLOSED / FROZEN` | **Sprint 17 Milestone** | ⏸️ `NOT STARTED` |
| **Aturan Mutasi Kode** | Zero Source Code Mutation | **Aturan Database** | Zero Database Migration / DDL |
| **Kebersihan Root** | Zero Root Pollution (Rule D) | **Format Pengiriman** | Single Canonical Markdown File |

### 1.2 Hierarki Sumber Otoritas dan Batas Kewenangan (Bagian 1.3)
Sesuai Bagian 1.3 mandat audit, seluruh perumusan spesifikasi teknis dan validasi rencana wajib mematuhi urutan hierarki otoritas mengikat berikut:
1. **Keputusan Resmi Product Owner atau Arsitektur** yang benar-benar tercatat dalam dokumen otoritatif.
2. **Nexa White Paper v5.6 dan Development Roadmap v4.8**, sesuai ruang lingkup masing-masing.
3. **Kontrak dan Perilaku Nyata Repositori Aktual** (kode sumber tracked dan skema database aktif).
4. **Temuan Audit Historis Beserta Bukti yang Mendasarinya** (A-01..A-30, B-01..B-09, F-01..F-15).
5. **Spesifikasi Usulan Teknis yang Belum Memperoleh Otorisasi** (`[PROPOSED SPECIFICATION]`).
6. **Interpretasi atau Asumsi Teknis** yang dibuat selama penyusunan plan.

> **Aturan Penanganan Pertentangan Otoritatif:** Sumber dengan tingkat otoritas lebih rendah dilarang mengubah fakta atau keputusan pada tingkat yang lebih tinggi. Jika dua sumber otoritatif bertentangan, Programmer wajib mencatat konflik tersebut secara terbuka (`CONFLICT — STOP AND CLARIFY`) dan menghentikan penetapan kontrak yang terdampak. Dilarang keras menyelesaikan konflik melalui asumsi atau tebakan bebas.

### 1.3 Rekonstruksi Historis Temuan Awal sampai REV6 dan REV22 (Bagian 2.2)
Sesuai Bagian 2.2, riwayat audit merupakan fondasi pengambilan keputusan yang tidak boleh dihapus atau disederhanakan menjadi ringkasan sepihak. Matriks berikut mendokumentasikan evolusi historis dan risiko yang wajib dicegah secara operasional pada REV6:

| Fase Audit Historis | Temuan atau Koreksi yang Tercatat | Risiko yang Harus Dicegah pada REV6 |
|---|---|---|
| **Prompt Awal** | Rancangan Handling Album belum cukup mengunci kontrak keamanan, integritas anggota, transaksi, dan otorisasi. | Ambiguitas mendasar berubah menjadi implementasi yang menebak aturan. |
| **REV1** | Filename/ZIP, path traversal, lingkup Creator, transaksi, entitlement, dan cache. | Validasi parsial dianggap cukup untuk keamanan distribusi dan pemutaran. |
| **REV2** | Trust, hash, schema, cache, dan pre-verification. | Hash atau status satu objek digunakan sebagai bukti untuk objek lain; hasil pra-verifikasi dianggap sebagai izin pemutaran. |
| **REV3** | Pemisahan trust, klasifikasi integritas, hash playback, dan determinisme entitlement. | Kepercayaan pada Album Signer dianggap menggantikan validasi setiap anggota. |
| **REV4** | RFC 8785 JCS, Ed25519, TOCTOU, idempotensi, dan symlink. | Kontrak kriptografi dan filesystem ditulis tanpa batas operasional yang dapat dibuktikan. |
| **REV5** | Ed25519/API, `O_NOFOLLOW`, entitlement child secara atomik, serta pemisahan kriteria Player dan Verify. | Penulisan kontrak normatif dianggap membuktikan implementasi; atomisitas lokal dianggap menyelesaikan transaksi eksternal. |
| **REV6** | Certificate binding, revocation/fallback, pembacaan descriptor, complete reads, dan idempotensi terminal. | Jalur fallback, validasi sertifikat, atau lifecycle descriptor masih menyisakan keadaan tidak deterministik. |
| **REV7–REV11** | Temuan berulang mengenai filesystem, authorization, fallback, transaksi, Genesis/Registry binding, race condition, state entitlement, dan klasifikasi integritas. | Koreksi lokal menutup satu kasus tetapi tidak menghilangkan akar penyebab lintas-komponen. |
| **REV12–REV21** | Rangkaian koreksi berlanjut dan sebagian temuan kemudian dikonsolidasikan dalam register berikutnya. | Tidak boleh menyimpulkan bahwa semua temuan telah tertutup hanya karena nomor revisi bertambah. |
| **REV22** | Status `REVISE REQUIRED`; F-01..F-15 merangkum temuan teknis penting. | Register historis hilang, digabung, atau dinyatakan selesai tanpa bukti yang sesuai. |

### 1.4 Batas Revisi Governance & Anti-Overprocessing
Siklus koreksi ini mematuhi batas tata kelola maksimum:
1. **Batas Tiga Revisi Korektif**: Revisi ini merespon temuan audit komprehensif dan handoff auditor (Temuan 1 s.d. 10 dan 8 pemeriksaan spesifikasi tambahan). Koreksi difokuskan secara presisi pada penutupan akar penyebab defect tanpa menambah fase buatan.
2. **Anti-Overprocessing**: Tidak ada pembuatan dokumen pendamping, fase audit buatan, duplikasi berkas, atau perubahan kosmetik tanpa dasar. Seluruh perbaikan dilakukan secara *in-place* pada berkas kanonikal ini.
3. **Pemisahan Penutupan Dokumen vs Substantif**: Dokumen secara tegas membedakan antara tindakan koreksi plan (*Plan-Corrected*) dan penyelesaian substantif atas blocker (*Substantively Resolved*). Masalah substantif yang bergantung pada keputusan PO atau arsitektur eksternal tetap dinyatakan `OPEN / BLOCKED`.

### 1.5 Catatan Tindak Lanjut Temuan Audit Komprehensif (Temuan 1 s.d. 10)
Tabel berikut merinci resolusi teknis dan substantif untuk setiap temuan audit utama:

| ID Audit | Ringkasan Temuan Audit | Resolusi Teknis & Substantif pada Plan Kanonikal | Status Dokumen |
|:---:|:---|:---|:---:|
| **Temuan 1** | Nomenklatur dan pemetaan tanda tangan berpotensi mencampuradukkan Album Signer vs Container Creator. | Memisahkan tegas 3 tanda tangan: (1) Album Signer Signature (manifest kanonikal, NC-02 $\rightarrow$ AC-03), (2) Container Packaging Signature (kontainer individual `.nx`, NC-06 $\rightarrow$ AC-04), dan (3) Genesis Cert Signature (sertifikat genesis track, NC-05 $\rightarrow$ AC-10). | `CORRECTED` |
| **Temuan 2** | Urutan tahapan JIT 8-tahap belum merinci seluruh pemeriksaan kriptografis secara eksplisit. | Merinci mapping eksplisit 8 tahap JIT ke AC penguji (Tahap 1 safe-open, Tahap 2 ZIP flat, Tahap 3 strict parse, Tahap 4 manifest JCS & signer trust, Tahap 5 container pkg & genesis binding, Tahap 6 license, Tahap 7 audio SHA-256, Tahap 8 decrypt & buffer). Pre-verifikasi trek berikutnya dilarang memberi otorisasi awal. | `CORRECTED` |
| **Temuan 3** | AC-25 mencampuradukkan kebijakan signer `UNKNOWN` dengan hierarki status agregat NX Verify. | AC-07 dikunci eksklusif pada kebijakan signer `UNKNOWN` (dep: B-09 / NC-04 / CONF-01). AC-25 dikunci eksklusif pada hierarki agregat Verify (dep: CONF-02). Dependensi B-09/CONF-01 dicabut dari AC-25. | `CORRECTED` |
| **Temuan 4** | Kontradiksi status NC-12: menyatakan blocker `NONE` padahal B-06 masih terbuka. | Menyelaraskan status blocker NC-12 menjadi `OPEN / BLOCKED BY B-06`. Membedakan containment, symlink, post-open descriptor, dan concurrent ancestor rename. Fail-closed tidak diartikan menghilangkan race condition di userspace. | `CORRECTED` |
| **Temuan 5** | Taksonomi error dan status `ERR_ZIP_INVALID` di luar daftar 20 kode. | Memasukkan `ERR_ZIP_INVALID` secara formal ke dalam taksonomi 20 kode error kanonikal terverifikasi di kode Go (`container.go#L112`), dan mengeliminasi kode dugaan `ERR_GENESIS_SIGNATURE_INVALID` yang tidak ada di baseline. Menyelaraskan pemicu corrupt ZIP, entri direktori terlarang, kuota, rasio, dan mismatch pada AC-02, AC-13, AC-26. | `CORRECTED` |
| **Temuan 6** | Transaksi Marketplace mengisyaratkan rollback setelah commit tanpa 2PC. | Menegaskan transaksi lokal SQL yang telah commit tidak dapat di-rollback oleh SQL yang sama; rollback lokal hanya untuk mutasi uncommitted; kegagalan HTTP License Daemon tidak terkompensasi (gap 2PC B-04). AC-14 dan AC-15 diselaraskan; B-04 tetap terbuka. | `CORRECTED` |
| **Temuan 7** | Klaim Zero-DDL, repository bersih, dan database tidak termutasi melampaui bukti inspeksi. | Mengakui inspeksi skema DDL hanya uji berkas lokal (bukan jaminan DB runtime hidup unverified); git status tracked bersih; 2 berkas untracked docs diakui jujur; folder `evidence/` gitignored; kebersihan root hanya uji root level; mobile/usage `NOT VERIFIED`. | `CORRECTED` |
| **Temuan 8** | Objek hash yang dibandingkan belum dibedakan secara tegas. | Mengisolasi 5 objek hash: audio payload bitstream (SHA-256), manifest JCS canonical (SHA-256), container packaging, genesis cert, dan ZIP archive package. Formula truncated SHA-256 hanya membuktikan batas panjang kolom DDL, bukan bebas collision. | `CORRECTED` |
| **Temuan 9** | Signer `UNKNOWN`: penolakan album ditafsirkan melarang seluruh pemeriksaan integritas anggota. | Menegaskan bahwa penolakan otorisasi pemutaran (playback) TIDAK melarang dilakukannya verifikasi integritas fisik kontainer `.nx` anggota untuk tujuan diagnostik/pelaporan Verify. Opsi A/B/C tetap proposal non-normatif pending PO B-09. | `CORRECTED` |
| **Temuan 10** | Status Gate dan keterlacakan mengklaim sinkronisasi sementara kontradiksi material masih ada. | Menyelaraskan G-05, G-06, G-10 dengan status aktual. Keterlacakan dua arah diperbaiki (NC-06 $\rightarrow$ AC-04; NC-03 $\rightarrow$ B-01/B-02; NC-12 $\rightarrow$ B-06). Gate A tetap `NOT PASSED`, Gate B tetap `BLOCKED`, Implementasi `NOT AUTHORIZED`. | `CORRECTED` |

---

### 1.6 Matriks Penutupan Temuan Audit Historis A-01 sampai A-30 [HISTORICAL AUDIT LOG: SPRINT 16/PRE-SPRINT 17 BASELINE]
Matriks berikut mendokumentasikan penanganan terhadap 30 temuan audit historis A-01 sampai A-30 sebagai catatan historis (Historical Audit Log). Status koreksi dibatasi secara jujur pada revisi dokumen rencana (*Plan-Corrected*), bukti inspeksi statis lokal (*Static-Inspection-Only*), dan secara tegas membedakan masalah arsitektur substantif yang masih terblokir (*Substantively Blocked*) tanpa mengklaim pembuktian runtime atau database produksi yang sesungguhnya belum tersedia (*Evidence Not Available / Runtime Not Verified*):

| ID & Makna Historis | Sumber Audit & Bukti Awal | Defect / Risiko Konkret | Kategori Penyebab & Analisis Kausal | Informasi Tersedia Saat Terjadi | Aturan Prompt Pencegahan Operasional | Koreksi Substantif Dilakukan | Bukti Pendukung Koreksi | Register Terdampak | Hasil Rekonsiliasi Dua Arah | Status Akhir yang Sah | Batasan / Ketidakpastian Substantif yang Terbuka |
| :---: | :--- | :--- | :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **A-01** (Kontradiksi status AC) | Audit V6.9.4 §8; Klaim global `[TEST-PLANNED]` pada 27 AC | Menyamarkan ketiadaan transaksi atomik dan ketiadaan keputusan PO seolah-olah seluruh pengujian siap dijalankan. | `PR` & `I` — Prompt mengizinkan ringkasan agregat tanpa memeriksa ketergantungan fisik AC pada blocker terbuka. | Roadmap v4.8; B-04; B-09 | **Trigger:** Ada AC dengan blocker eksternal. **Wajib:** Cantumkan status eksplisit per AC. **Dilarang:** Sweeping claim status agregat. | Rekonsiliasi klasifikasi AC: Menjelaskan bahwa klasifikasi historis 20/4/3 adalah catatan audit lama; pada plan kanonikal terkini, seluruh 27 AC diklasifikasikan konsisten dan eksklusif ke dalam: 15 AC `[TEST-PLANNED — SPEC READY]`, 9 AC `[TEST-PLANNED — EXECUTION BLOCKED]` (2 Modul Pending B-01/B-02 + 7 Arsitektur/Usulan B-03..B-08), dan 3 AC `[PO DECISION REQUIRED]` (AC-01, 07, 25) (total tepat 27 AC). | §2.1, §6, §8, §13; B-01..B-09 | NC-01 s.d. NC-16, AC-01..27, B-01..09, Gate A | Seluruh 27 AC terpetakan tepat satu kali tanpa duplikasi; status blocker terpropagasi jelas. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | 9 AC terblokir eksekusi (B-01..B-08) dan 3 AC menunggu keputusan resmi PO (CONF-01..03). |
| **A-02** (Ketepatan pemetaan AC-15) | Audit V6.9.4 §8 & §9; AC-15 tertaut ke NC-16 (formula ID) | Kesalahan tautan kontraktual mengaburkan pengujian transaksi replay protection Marketplace. | `P` — Programmer salah menghubungkan AC penguji idempotensi ke kontrak formula ID karena kemiripan nomor ID. | `schema.postgres.sql#L63`; NC-08 historis | **Trigger:** Penyusunan Traceability Matrix. **Wajib:** Petakan AC ke NC berdasarkan fungsi yang diuji. **Dilarang:** Menebak ID. | Mengunci pemetaan AC-15 eksklusif ke NC-08 (Marketplace Transaction & Replay Protection) berstatus `[BLOCKED]` di bawah B-04. | §6.8, §8 (AC-15), §9 (NC-08) | NC-08, AC-15, B-04, CONF-03 | NC-08 diuji oleh AC-14 dan AC-15; AC-15 menguji replay endpoint NC-08. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Blocker arsitektur B-04 tetap terbuka. |
| **A-03** (Kecukupan bukti fungsionalitas) | Audit V6.9.4 §4.3; Klaim dukungan platform tanpa bukti runtime | Klaim E2E lintas platform dibuat tanpa bukti eksekusi aktual di repositori Linux. | `PR` & `V` — Prompt tidak mewajibkan bukti per platform; pengujian mobile belum dijalankan. | Repositori remote Linux `/opt/antigravity/projects/nexa` | **Trigger:** Pernyataan verifikasi komponen. **Wajib:** Sertakan bukti file/line aktual. **Dilarang:** Generalisasi bukti desktop ke mobile. | Menyajikan Evidence Ledger terstruktur (§4.4) yang memisahkan bukti kode terverifikasi (E-01..E-08) dari runtime mobile `NOT VERIFIED`. | §4.3, §4.4 (E-01..E-09), §13.1 | NC-01 s.d. NC-16, F-14, Gate A | Klaim repositori dibatasi pada inspeksi kode yang benar-benar ada di Linux server. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; RUNTIME NOT VERIFIED)` | Pengujian fisik runtime mobile berstatus `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. |
| **A-04** (Validitas Preservation Gate) | Audit V6.9.4 §12.1; Preservation Gate diklaim PASS 100% | Meloloskan gerbang preservasi hanya dari kelengkapan teks ID, mengabaikan blocker keputusan terbuka. | `G` — Ketiadaan keputusan resmi PO atas signer UNKNOWN dan ketiadaan 2PC disamarkan oleh keberadaan teks ID. | Baseline Sprint 16; White Paper v5.6; B-04; B-09 | **Trigger:** Evaluasi Preservation Gate. **Wajib:** Evaluasi 7 dimensi secara independen. **Dilarang:** Menilai PASS agregat jika ada dimensi terblokir. | Mengevaluasi 7 dimensi secara terpisah; menetapkan status jujur: D-01..D-05 PASS terbatas inspeksi statis; D-06 BLOCKED/PENDING PO; D-07 PARTIAL PASS (Temuan 1 s.d. 10). | §12.1 (Tabel 7 Dimensi Preservation Gate) | B-04, B-09, NC-04, NC-08, Gate A, Gate B | Dimensi preservasi sinkron dengan status blocker dan kesiapan sistem di §13. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Dimensi kelengkapan keputusan berstatus BLOCKED / PENDING PO DECISION. |
| **A-05** (Cakupan taksonomi error) | Audit V6.9.4 §6.15; Rujukan error tersebar dan format tabel rusak | Jalur eksekusi menghasilkan generic exception tanpa pemetaan kode diskrit fail-closed; format tabel rusak (S-01). | `P` & `PR` — Kurangnya pemusatan rujukan error dan kesalahan sintaksis pemisah tabel markdown. | Error Taxonomy Spec; NC-15; White Paper v5.6 | **Trigger:** Penanganan kegagalan sistem. **Wajib:** Petakan ke kode error diskrit kanonikal. **Dilarang:** Uncaught exception generic atau crash diam-diam. | Memusatkan penanganan error ke tabel kanonikal 20 kode error kanonikal (§6.15) termasuk `ERR_ZIP_INVALID` (menghapus `ERR_GENESIS_SIGNATURE_INVALID` yang tidak terdaftar di baseline); memperbaiki format tabel. | §6.15, §8 (AC-26), §9 (NC-15) | NC-15, AC-10, AC-26, F-08, Gate A | Setiap kode error terhubung ke minimal satu AC penguji fail-closed. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; GENESIS CODE UNRESOLVED)` | Penanganan runtime `ERR_ALBUM_SIGNER_UNKNOWN` menunggu keputusan PO. |
| **A-06** (Formula ID & batas kolom) | Audit V6.9.4 §6.16; Penggabungan string ID berisiko overflow | Derivasi ID child acquisition dan provider berisiko overflow kolom VARCHAR PostgreSQL atau tabrakan saat retry. | `I` & `V` — Kesalahan penafsiran batas kolom dengan menjumlahkan string antar-tabel dan ketiadaan inspeksi DDL aktif. | `schema.postgres.sql#L63-L115`; NC-16 | **Trigger:** Perancangan formula ID. **Wajib:** Uji batas panjang matematis per kolom. **Dilarang:** Menjumlahkan string antar-tabel berbeda. | Menyajikan derivasi independen per kolom: child acq $\le 128$, child ent $\le 128$, provider $\le 64$. Mengakui batas kolom bukan bukti ketiadaan collision. | §6.16, §8 (AC-27), §9 (NC-16); DDL schema | NC-16, AC-27, B-05, Gate A | Formula truncated SHA-256 terbukti mematuhi constraint panjang skema DDL aktif. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; DDL CAPACITY VERIFIED)` | Semantik derivasi hash jika `provider_snapshot` absen adalah gap spesifikasi terbuka. |
| **A-07** (Keselarasan AC-17 Zero-DDL) | Audit V6.9.4 §8 & §9; AC-17 tertaut ganda ke NC-08 dan NC-10 | AC-17 yang menguji kepatuhan Zero-DDL ikut terblokir secara keliru oleh blocker transaksi B-04. | `P` — Programmer salah menduplikasi tautan AC-17 ke NC-08 transaksi alih-alih mengisolasinya pada audit skema. | `schema.postgres.sql`; NC-10 | **Trigger:** Evaluasi Zero-DDL. **Wajib:** Petakan AC-17 eksklusif ke NC-10. **Dilarang:** Menautkan AC-17 ke NC-08 multi-item transaction. | Mengunci AC-17 eksklusif ke NC-10 (Zero-DDL); melepaskan dependensi pemblokir B-04 sehingga Zero-DDL dapat diverifikasi secara independen. | §8 (AC-17), §9 (NC-10) | NC-10, AC-17, Gate A | AC-17 menguji pematuhan skema pasca-operasi tanpa mutasi DDL; sinkron dengan NC-10. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; LIVE DB NOT VERIFIED)` | Zero-DDL pada file skema dipatuhi 100%; database live unverified. |
| **A-08** (Batas kuota ZIP vs kontainer `.nx`) | Audit V6.9.4 §6.7; Batas ZIP diperluas ke file `.nx` individual | Pembatasan keliru ukuran kontainer audio individual `.nx` berdasarkan analogi arsip ZIP. | `I` — Kesalahan analogi yang menyamakan batas pembungkus distribusi dengan batas payload biner audio. | NC-07 historis; WP v5.6 §Distribution | **Trigger:** Spesifikasi batas ukuran arsip. **Wajib:** Batasi kuota ZIP murni pada wrapper distribusi. **Dilarang:** Menerapkan kuota ZIP ke berkas `.nx`. | Mengunci batas kuota (500MB zip, 4GB uncompressed, 200 entri flat tanpa direktori, rasio 10:1) hanya untuk arsip ZIP pembungkus; melarang perluasannya ke berkas `.nx`. | §2.1, §6.7, §8 (AC-13), §9 (NC-07) | NC-07, AC-13, B-07, Gate A | ZIP adalah wadah distribusi fisik; berkas `.nx` adalah payload biner independen. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Batas maksimum ukuran berkas `.nx` individual adalah gap spesifikasi terbuka. |
| **A-09** (Kecukupan bukti Safe-Open) | Audit V6.9.4 §6.12; Klaim anti-TOCTOU absolut di userspace | Resep prosedural semu (`realpath`, `O_NOFOLLOW`) diklaim menjamin keamanan mutlak terhadap race condition filesystem. | `G` & `PR` — Prompt tidak menuntut rumusan invariant keamanan dan batasan kernel POSIX tidak diakui jujur. | NC-12 historis; Standar POSIX.1-2017 | **Trigger:** Evaluasi akses filesystem. **Wajib:** Rumuskan Invariant Keamanan dan akui batas POSIX. **Dilarang:** Mengklaim anti-TOCTOU mutlak userspace. | Merumuskan Invariant Keamanan; memisahkan pre-open path vs post-open fd; mengakui batas concurrent rename; fail-closed `canPlay: false`. | §2.1, §6.12, §8 (AC-20, AC-21), §9 (NC-12) | NC-12, AC-20, AC-21, F-01, F-11, F-12, Gate A | Pembuktian invariant menjadi kriteria kelulusan; jika ragu, melempar fail-closed (`canPlay: false`). | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; USpace LIMITS ACKNOWLEDGED)` | Keterbatasan race condition concurrent ancestor rename pada POSIX userspace diakui. |
| **A-10** (Aturan operasional ZIP) | Audit V6.9.4 §6.7; Metode hitung entri diklaim normatif | Aturan desain internal penghitungan entri direktori/manifest diklaim seolah-olah sudah disahkan standar. | `I` — Menganggap proposal teknis Programmer sebagai kontrak normatif yang telah disahkan. | PKWARE APPNOTE; ISO/IEC 21320-1; RFC 1951 | **Trigger:** Detail implementasi ekstraksi. **Wajib:** Pisahkan kuota numerik dari usulan operasional. **Dilarang:** Mengklaim usulan desain sebagai kontrak sah. | Mengunci aturan flat: entri direktori dilarang di ZIP album (`ERR_ZIP_INVALID`). Batas numerik (500MB/4GB/200/10:1) dan aturan operasional diselaraskan di bawah `[PROPOSED SPEC]`. | §6.7, §8 (AC-13) | NC-07, AC-13, Gate A | Kuota ZIP wrapper dan aturan flat diselaraskan konsisten di seluruh bagian. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Aturan kuota ZIP berstatus usulan spesifikasi teknis B-07. |
| **A-11** (Bukti repositori independen) | Audit V6.9.4 §4.3; Klaim repo-verified tanpa rujukan line aktual | Pernyataan verifikasi repositori tidak dapat diaudit atau diverifikasi ulang secara independen. | `PR` & `V` — Prompt mengizinkan label verifikasi tanpa mewajibkan bukti path dan baris aktual di server. | Repositori remote Linux `/opt/antigravity/projects/nexa` | **Trigger:** Pemberian label `[REPOSITORY-VERIFIED]`. **Wajib:** Cantumkan path, line range, dan raw snippet. **Dilarang:** Memberi label tanpa inspeksi aktual. | Menyajikan Evidence Ledger Repository di §4.4 dengan 9 bukti empiris terverifikasi (E-01 s.d. E-09) lengkap dengan path absolut, line range, dan raw snippets. | §4.3, §4.4 (E-01 s.d. E-09), §12.2 (G-03) | NC-01 s.d. NC-16, Gate A | Seluruh klaim kode mengacu langsung pada bukti ledger yang terdaftar dengan kutipan mentah. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; DESKTOP REPO ONLY)` | Komponen mobile berstatus NOT VERIFIED karena keterbatasan lingkungan server. |
| **A-12** (Cakupan rollback transaksi lokal) | Audit V6.9.4 §8; Definisi rollback berisiko menghapus data lama | Ambang batas pemulihan state transaksi database berisiko menghapus data historis yang sah saat rollback. | `I` — Kesalahan penafsiran semantik rollback SQL antara mutasi transaksi gagal vs data pra-transaksi. | `schema.postgres.sql`; NC-08 | **Trigger:** Penanganan kegagalan transaksi. **Wajib:** Batasi rollback pada uncommitted changes transaksi gagal. **Dilarang:** Menghapus baris historis sah. | Memperjelas bahwa rollback AC-14 membatalkan mutasi transaksi gagal tanpa residu baris parsial, tanpa menghapus baris pra-transaksi yang sah. | §8 (AC-14), §9 (NC-08) | NC-08, AC-14, B-04, CONF-03 | Rollback mengembalikan database lokal ke kondisi awal pra-transaksi; status tetap BLOCKED oleh B-04. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Blocker transaksi terdistribusi B-04 tetap terbuka. |
| **A-13** (Opsi signer UNKNOWN non-normatif) | Audit V6.9.4 §6.4 & §10; Opsi A/B/C diperlakukan sebagai aturan sah | Menetapkan perilaku pemutaran signer UNKNOWN secara sepihak melangkahi kewenangan Product Owner. | `P` & `PR` — Programmer menganggap daftar opsi proposal sebagai spesifikasi normatif yang dapat diputuskan sendiri. | Roadmap v4.8; B-09 / NC-04 | **Trigger:** Penanganan trust model signer. **Wajib:** Kunci pada keputusan PO tertulis. **Dilarang:** Memilih opsi A, B, atau C atas nama PO. | Mengunci Opsi A, B, C murni sebagai proposal non-normatif di §6.4 dan §10; mempertahankan status `PO DECISION REQUIRED` pada AC-07 dan AC-25. | §6.4, §10, §11 (CONF-01), §8 (AC-07, AC-25) | NC-04, NC-14, AC-07, AC-25, B-09, CONF-01 | Model kepercayaan adalah hak prerogatif PO; AC terkait terkunci pada keputusan PO. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Keputusan tertulis PO mengenai signer UNKNOWN masih tertunda. |
| **A-14** (Konsistensi kosakata status) | Audit V6.9.4 §2; Kosakata status saling bertentangan | Mencampuradukkan status rencana pengujian dengan status kelulusan pengujian atau status dependensi. | `PR` & `I` — Prompt tidak menyediakan taksonomi status diskrit sehingga istilah dipertukarkan keliru. | Governance Framework Nexa | **Trigger:** Pelabelan status register. **Wajib:** Gunakan dimensi status terpisah. **Dilarang:** Menyamakan spesifikasi dengan implementasi atau planned dengan passed. | Menegakkan pemisahan dimensi status secara disiplin di §2.1; memetakan 27 AC ke dalam model multi-dimensi. | §2.1, §6, §8, §12, §13, §14 | Seluruh register (NC, AC, B, F, E, CONF, G) | Kosakata status konsisten di seluruh bab tanpa kontradiksi internal administratif. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Kosakata status terkunci presisi. |
| **A-15** (Bukti root-clean & zero-mutation) | Audit V6.9.4 §14; Deklarasi root-clean tanpa output terminal | Mengklaim tidak ada perubahan kode atau file liar tanpa menyajikan bukti pemeriksaan git aktual. | `PR` & `V` — Prompt mewajibkan deklarasi tetapi tidak mewajibkan bukti inspeksi terminal aktual. | Terminal remote Linux repositori Nexa | **Trigger:** Pembuatan closing declaration. **Wajib:** Jalankan `git status` dan `ls -la`. **Dilarang:** Mengklaim root-clean tanpa bukti inspeksi. | Menjalankan inspeksi aktual via `git status --porcelain` dan `ls -la`; menyertakan commit hash `fc08a5c...` dan batas pembuktian riil di §4.4 (E-08) dan §14. | §4.4 (E-08), §12.2 (G-09), §14 | Mandatory Closing Declarations, Rule D | Output terminal membuktikan nol mutasi kode tracked; untracked docs dicatat transparan. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; ROOT LEVEL ONLY)` | Berkas untracked docs dicatat; inspeksi terbatas pada root direktori. |
| **A-16** (Konsistensi B-04/NC-08, B-09, dan AC) | Audit V6.9.4 §7 & §8; Ketergantungan AC tidak sinkron dengan blocker | AC-14/15 dan AC-07/25 diringkas sebagai test-planned sementara blocker dasarnya masih terbuka. | `P` — Programmer mengabaikan dampak blocker B-04 dan B-09 saat mengisi tabel Acceptance Criteria. | B-04, B-09; Roadmap v4.8; `schema.postgres.sql` | **Trigger:** Evaluasi dependensi AC. **Wajib:** Propagasikan status blocker ke AC penguji. **Dilarang:** Menyatakan AC siap uji jika dependensinya terblokir. | Mengunci status: AC-14 & AC-15 `[BLOCKED]` (dep: B-04 / NC-08); AC-16 `[BLOCKED]` (dep: B-05 / NC-09); AC-03 `[BLOCKED]`; AC-07 `[PO DECISION REQUIRED]`; AC-25 `[PO DECISION REQUIRED]`. | §7.1, §8, §9, §13 | NC-02, NC-04, NC-08, NC-09, AC-03, 07, 14, 15, 16, 25, B-04, 05, 08, 09 | Dependensi blocker terpropagasi sinkron dua arah ke seluruh register terkait. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | B-04, B-05, B-08, B-09 tetap terbuka secara sah. |
| **A-17** (Penanganan exception kriptografi) | Audit V6.9.4 §7.2; Exception kriptografi berisiko crash unhandled | Exception format kunci atau korupsi buffer melempar uncaught error yang meruntuhkan proses runtime. | `PR` & `I` — Prompt tidak merinci batas modul kriptografi Node.js vs pemetaan error tingkat sistem. | `sdk/typescript/src/crypto.ts`; F-08; §6.15 | **Trigger:** Penanganan exception kriptografi. **Wajib:** Tangkap di layer modul dan petakan ke kode diskrit. **Dilarang:** Membiarkan uncaught exception bocor ke UI. | Memperjelas bahwa error format kunci/parsing ditangkap rapi di tingkat modul dan dipetakan ke error diskrit di tingkat sistem/UI (`ERR_CONTAINER_SIGNATURE_INVALID`). | §6.15, §7.2 (F-08), §8 (AC-26) | NC-15, AC-26, F-08, Gate A | Mencegah unhandled crash dan menegakkan prinsip fail-closed di seluruh layer. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Penanganan exception terdefinisi rapi pada rancangan dokumen. |
| **A-18** (Konsistensi substantif lintas bagian) | Audit V6.9.4; Teks draf lama bertentangan dengan perbaikan baru | Adanya sisa teks kontradiktif antar-bab (e.g. formula ID lama vs baru, batas ZIP 2GB vs 4GB). | `P` — Programmer memperbaiki satu bab tanpa melakukan audit dampak silang ke bab-bab lainnya. | Dokumen plan kanonikal V6.9.4 | **Trigger:** Perubahan teks persyaratan. **Wajib:** Jalankan audit dampak silang ke seluruh bab. **Dilarang:** Meninggalkan sisa teks draf lama yang bertentangan. | Menyinkronkan seluruh referensi kontrak, formula ID, batas ZIP flat, safe-open, dan status gate di seluruh bab (§1 s.d. §14). | Seluruh dokumen (§1 s.d. §14) | Seluruh register dan bab | Dokumen diaudit komprehensif; sinkronisasi internal diperbaiki. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Dokumen mengakui secara jujur bahwa konflik material eksternal tetap terbuka. |
| **A-19** (Traceability dua arah lintas bagian) | Audit V6.9.4 §9; Traceability hanya searah dari NC ke AC | Ketidaksesuaian pemetaan dari AC kembali ke NC dan dependensi blocker yang tidak tercermin; format rusak (S-02). | `P` — Programmer menyusun matriks searah tanpa memvalidasi keterhubungan balik dari kriteria uji ke sumber. | §8 (AC Register); §9 (Traceability Matrix) | **Trigger:** Penyusunan Traceability. **Wajib:** Lakukan audit dua arah (Forward & Reverse). **Dilarang:** Memetakan AC ke sumber tidak berwenang. | Menjalankan audit dua arah dari NC ke AC dan dari AC ke NC: NC-06 -> AC-04; NC-08 -> AC-14, 15; NC-10 -> AC-17; NC-16 -> AC-27. | §9 (Tabel Traceability Matrix Dua Arah) | NC-01 s.d. NC-16, AC-01 s.d. AC-27 | 16 NC dan 27 AC terpetakan presisi dengan rujukan dependensi yang jelas. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Rantai ketertelusuran dokumen terbukti. |
| **A-20** (Penutupan substantif tanpa relabel) | Audit V6.9.4; Penutupan temuan hanya dengan mengganti kata status | Mengklaim temuan selesai secara administratif tanpa mengubah logika, batas, atau bukti yang mendasarinya. | `G` — Ketiadaan bukti dan spesifikasi teknis disamarkan dengan perubahan redaksi semata. | Seluruh dokumen kanonikal V6.9.4 | **Trigger:** Penutupan temuan audit. **Wajib:** Sertakan perbaikan teknis dan bukti nyata. **Dilarang:** Mengubah status tanpa perbaikan substantif. | Menegakkan perbaikan teknis nyata: formula ID independen, skema lengkap manifest, invariant safe-open, dan evidence ledger E-01..E-09. | Seluruh dokumen kanonikal | Seluruh register | Penutupan administratif dipisahkan dari penyelesaian blocker substantif. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Tidak ada penutupan blocker semu. |
| **A-21** (Invariant teknis sebagai batasan) | Audit V6.9.4 §6; Batasan keamanan berupa checklist prosedural | Checklist prosedural rentan di-bypass jika implementasi internal berubah tanpa mematuhi prinsip keamanan. | `PR` & `I` — Prompt tidak mewajibkan perumusan formal invariant keamanan logika. | White Paper v5.6; NC-05, NC-07, NC-12 | **Trigger:** Perancangan kontrol keamanan. **Wajib:** Rumuskan Invariant Keamanan logika mutlak. **Dilarang:** Mengandalkan prosedur ad-hoc sebagai jaminan. | Mengunci invariant teknis mutlak: Filesystem Containment Invariant, 3-Way Identity Equality, 1:1 ZIP-to-Manifest Bijection, dan Larangan Entri Direktori ZIP. | §5.1, §5.2, §6.5, §6.7, §6.12, §8 | NC-05, NC-07, NC-12, AC-09, AC-12, AC-21 | Invariant logika menjadi fondasi pengujian fail-closed di seluruh sistem. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Batasan race condition POSIX userspace diakui secara jujur. |
| **A-22** (Spesifikasi skema manifest) | Audit V6.9.4 §5.1; Skema manifest tidak lengkap | Tidak adanya definisi skema JSON lengkap memicu interpretasi liar dalam deserialisasi dan validasi tipe. | `PR` & `P` — Prompt tidak menyertakan draf skema normatif JSON Schema Draft 7. | White Paper v5.6 §Album Manifest Specification | **Trigger:** Perancangan struktur data. **Wajib:** Sediakan skema lengkap dengan tipe data eksplisit. **Dilarang:** Menggunakan representasi contoh informal. | Menyajikan skema JSON lengkap 13 properti wajib bertanda `[PROPOSED STRICT SPEC]` dengan tipe data, pola regex valid JSON (`\\.nx$`), dan batasan `additionalProperties`. | §5.1 (Skema Manifest JSON Lengkap) | NC-01, AC-01, F-04, Gate A | Skema manifest terdefinisi formal; status unknown fields ditandai pending PO. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Penolakan unknown fields berstatus usulan spesifikasi ketat. |
| **A-23** (Pemisahan dua tanda tangan Creator) | Audit V6.9.4 §5.1; Kerancuan tanda tangan manifest vs Genesis | Ambiguitas verifikasi apakah Album Signer menandatangani berkas audio atau hanya manifest JSON. | `I` — Kerancuan konsep tanda tangan packaging versus sertifikat kepemilikan kanonikal Genesis. | White Paper v5.6 §Two-Signature Architecture | **Trigger:** Evaluasi verifikasi kriptografi. **Wajib:** Pisahkan Container Creator Sig vs Genesis Certificate Creator Sig. **Dilarang:** Menyatukan kunci verifikasi. | Menegakkan arsitektur pemisahan kriptografis: Container Creator Signature (Ed25519) memverifikasi byte packaging kontainer individual `.nx`; Genesis Cert Signature mengikat track audio; Album Signer menandatangani manifest. | §5.1, §5.2, §6.2, §8 (AC-03, AC-04) | NC-02, NC-06, AC-03, AC-04, F-06, Gate A | Tanda tangan container independen dari tanda tangan sertifikat track. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Verifikasi runtime multi-track berstatus TEST-PLANNED. |
| **A-24** (Semantik 5 konsep hash/sig diskrit) | Audit V6.9.4 §6.9; Tumpang tindih makna istilah hash | Kerancuan antara hash manifest, hash payload audio, hash arsip ZIP, dan hash sertifikat Genesis. | `PR` & `I` — Kegagalan taksonomi istilah hash yang menghasilkan kesalahan verifikasi integritas data. | NC-09 historis; White Paper v5.6 | **Trigger:** Penggunaan istilah hash. **Wajib:** Bedakan 5 konsep hash secara eksplisit. **Dilarang:** Menggunakan istilah generic `hash` tanpa konteks objek. | Mengisolasi 5 objek kriptografi: (1) Audio payload, (2) Manifest JCS, (3) Container `.nx`, (4) Genesis Cert, (5) ZIP Archive package. | §6.9, §8 (AC-16), §9 (NC-09) | NC-09, AC-16, B-05, Gate A | 5 objek kriptografis dibedakan secara formal; semantik `acquired_package_sha256` gap. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Semantik kolom child `acquired_package_sha256` adalah blocker B-05 terbuka. |
| **A-25** (Hierarki status Verify 3-lapis) | Audit V6.9.4 §5.3; Pencampuran status trust, integritas, agregat | Status kegagalan integritas satu trek merusak status trust signer album atau sebaliknya. | `I` & `P` — Kesalahan pemodelan status Verify yang menggabungkan dimensi kepercayaan dengan integritas file. | White Paper v5.6 §Verify Multi-Layer Status | **Trigger:** Evaluasi NX Verify. **Wajib:** Pisahkan 3 lapisan status independen. **Dilarang:** Menimpa status signer dengan status integritas track. | Memisahkan 3 layer: (1) Album Signer Trust, (2) Member Track Integrity, (3) Aggregate Album Verify Status; mempertahankan CONF-02 terbuka. | §5.3, §6.14, §8 (AC-25), §11 (CONF-02) | NC-14, AC-25, CONF-02, Gate A | Lapisan trust signer independen dari status integritas berkas lokal. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Hierarki status agregat Verify adalah konflik material terbuka CONF-02. |
| **A-26** (Taksonomi error code diskret) | Audit V6.9.4 §6.15; Taksonomi error tidak lengkap | Kegagalan parsing atau trust melempar exception generic yang tidak dapat ditangani UI secara presisi. | `PR` & `P` — Kurangnya pemetaan taksonomi error yang komprehensif untuk seluruh skenario kegagalan. | Error Taxonomy Spec; NC-15; White Paper v5.6 | **Trigger:** Pemetaan kode error. **Wajib:** Sediakan 20 kode diskrit kanonikal dengan trigger jelas. **Dilarang:** Menggunakan generic error string. | Merinci tepat 20 kode error kanonikal lengkap dengan layer asal, kondisi trigger, aksi fail-closed, dan AC penguji; memasukkan `ERR_ZIP_INVALID` dan mengeliminasi `ERR_GENESIS_SIGNATURE_INVALID`. | §6.15, §8 (AC-26), §9 (NC-15) | NC-15, AC-10, AC-26, F-08, Gate A | Taksonomi error mencakup seluruh alur eksekusi Album dengan perilaku fail-closed. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; GENESIS CODE UNRESOLVED)` | Error handling `ERR_ALBUM_SIGNER_UNKNOWN` menunggu keputusan PO. |
| **A-27** (Derivasi ID PostgreSQL aktif) | Audit V6.9.4 §6.16; Rumus ID melampaui batas kolom DB aktif | ID transaksi atau provider yang terlalu panjang menyebabkan error `value too long for type character varying`. | `I` & `V` — Pengabaian batasan skema fisik PostgreSQL dalam perancangan formula identitas. | `schema.postgres.sql#L63-L115` | **Trigger:** Perancangan formula ID. **Wajib:** Batasi panjang string $\le$ batas kolom skema aktif. **Dilarang:** Melebihi `VARCHAR(64)` atau `VARCHAR(128)`. | Merumuskan derivasi independen berbasis SHA-256 terpotong (32-hex): child acq $\le 128$, ent $\le 128$, provider $\le 64$; membatasi klaim AC-27 pada panjang. | §6.16, §8 (AC-27), §9 (NC-16) | NC-16, AC-27, B-05, Gate A | Panjang string ID terbukti tidak melanggar batas kolom skema database aktif. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; COLLISION UNVERIFIED)` | AC-27 hanya membuktikan batas panjang; bukan bukti matematis ketiadaan collision. |
| **A-28** (Isolasi baseline Sprint 16 & PE-01) | Audit V6.9.4; Klaim mutasi kode atau pembukaan baseline | Risiko perubahan kode baseline yang sudah stabil untuk mempermudah implementasi fitur album baru. | `PR` & `I` — Kegagalan membatasi ruang lingkup post-sprint yang berisiko merusak deliverable sebelumnya. | Sprint 16 Closeout Report; PE-01 Spec | **Trigger:** Modifikasi berkas proyek. **Wajib:** Kunci baseline Sprint 16 & PE-01 sebagai FROZEN. **Dilarang:** Mengubah berkas kode baseline. | Menegakkan isolasi baseline: Sprint 16 dan PE-01 tetap 🔒 `CLOSED / FROZEN`. Tidak ada perubahan pada kode yang sudah diterima. | §1.1, §4.1, §14 (Closing Declarations) | Seluruh sistem Nexa, Gate A, Gate B | Baseline Sprint 16 dan PE-01 terlindungi dari mutasi kode tracked (diverifikasi via git diff); kondisi runtime live belum diverifikasi. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; RUNTIME NOT VERIFIED)` | Isolasi berkas kode tracked terbukti via git; status runtime dan database live belum diverifikasi. |
| **A-29** (Pemisahan Gate A vs Gate B) | Audit V6.9.4 §12.3; Kelulusan dokumen disamakan dengan kesiapan koding | Memberikan otorisasi implementasi kode hanya karena dokumen rencana telah selesai diperiksa. | `PR` & `G` — Penggabungan kriteria evaluasi rencana (Gate A) dengan kriteria kesiapan implementasi (Gate B). | Nexa Engineering Quality Framework | **Trigger:** Evaluasi kesiapan rilis rencana. **Wajib:** Pisahkan Gate A (Plan Quality) dan Gate B (Impl Readiness). **Dilarang:** Meluluskan Gate B jika ada blocker terbuka. | Menegakkan pemisahan mutlak: Gate A `NOT PASSED — REQUIRES TARGETED CORRECTIONS`; Gate B `BLOCKED`; Implementasi `NOT AUTHORIZED`. | §12.3, §13.1, §13.2, §14 | Gate A, Gate B, Governance Status | Kualitas rencana dinilai independen dari izin implementasi; Gate A tidak diluluskan semu. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Gate A tidak lulus karena konflik material; Gate B diblokir oleh B-04, B-05, B-08, B-09. |
| **A-30** (Bukti nol mutasi kode sumber) | Audit V6.9.4 §14; Deklarasi nol mutasi tanpa dasar inspeksi riil | Klaim verbal bahwa kode tidak termutasi tanpa bukti pelacakan git commit atau git status. | `PR` & `V` — Ketidakmampuan membedakan jaminan prosedural verbal dari bukti empiris sistem kontrol versi. | Git repository `/opt/antigravity/projects/nexa` | **Trigger:** Deklarasi akhir dokumen. **Wajib:** Jalankan inspeksi git dan tampilkan output aktual. **Dilarang:** Klaim verbal tanpa bukti terminal. | Melampirkan output aktual `git rev-parse HEAD`, `git status --porcelain`, dan `ls -la` di §4.4 (E-08) dan §14 dengan commit `fc08a5c...`. | §4.4 (E-08), §14 (Closing Declarations) | Seluruh repositori, Governance Gate | Nol mutasi kode sumber tracked terbukti via git diff; kebersihan root dibuktikan via ls -la (bukan jaminan rekursif subdirektori); status 2 berkas untracked docs dicatat transparan. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; ROOT & TRACKED ONLY)` | Inspeksi direktori terbatas pada tingkat root; berkas untracked docs diakui; kondisi live database tidak diuji. |

---

## 2. RINGKASAN READINESS DAN KONTROL PENCEGAHAN AKAR MASALAH (PR/G/I)

### 2.1 Model Multi-Dimensi Kesiapan Acceptance Criteria (27 AC)
Dokumen ini membedakan secara tegas klasifikasi Acceptance Criteria ke dalam dua dimensi yang koheren tanpa kategori semu yang saling bertentangan:

```
+----------------------------------------------------------------------------------------------------+
|                MATRIKS DUA DIMENSI STATUS ACCEPTANCE CRITERIA (27 AC)                              |
+-------------------------------------------------------------+---------------------------------------------------------------+
| Kategori Status Kriteria Penerimaan (Total 27 AC)           | Cakupan ID & Rincian Ketergantungan                           |
+-------------------------------------------------------------+---------------------------------------------------------------+
| 1. [TEST-PLANNED — SPECIFICATION READY] (15 AC)             | AC-02, AC-04, AC-08, AC-09, AC-10, AC-11, AC-12, AC-17,       |
|    Spesifikasi & expected result siap diuji tanpa hambatan  | AC-18, AC-19, AC-22, AC-23, AC-24, AC-26, AC-27               |
|    blocker eksternal setelah kode implementasi tersedia     | (Tidak memiliki blocker arsitektur aktif)                     |
+-------------------------------------------------------------+---------------------------------------------------------------+
| 2. [TEST-PLANNED — EXECUTION BLOCKED] (9 AC)                 | Sub-Kategori 2a: [IMPLEMENTATION MODULE PENDING] (2 AC):       |
|    Skenario uji terencana, namun eksekusi terblokir oleh    |   - AC-05 (B-01: Modul Strict JSON Parser belum dikoding)      |
|    dependensi implementasi modul internal atau celah        |   - AC-06 (B-02: Modul RFC 8785 JCS Serializer belum dikoding) |
|    arsitektur / spesifikasi teknis yang belum disahkan       | Sub-Kategori 2b: [BLOCKED BY ARCHITECTURE / PROPOSED SPEC] (7):|
|                                                             |   - AC-03 (B-08: Circular Dependency Manifest Signing)         |
|                                                             |   - AC-13 (B-07: Batas Kuota Ekstraksi ZIP Usulan Spesifikasi) |
|                                                             |   - AC-14 (B-04/CONF-03: Gap 2PC ke License Daemon eksternal)  |
|                                                             |   - AC-15 (B-04/CONF-03: Gap 2PC / Replay Settlement)          |
|                                                             |   - AC-16 (B-05/NC-09: Semantik hash acquired_package_sha256)  |
|                                                             |   - AC-20 (B-06: Batasan userspace POSIX Safe-Open TOCTOU)     |
|                                                             |   - AC-21 (B-06: Batasan userspace POSIX post-open descriptor) |
+-------------------------------------------------------------+---------------------------------------------------------------+
| 3. [PO DECISION REQUIRED] (3 AC)                            | AC-01 (NC-01: Kebijakan Unknown Fields Manifest Strict vs Ext)|
|    Expected result dan penerimaan kontrak belum dapat       | AC-07 (NC-04 / B-09 / CONF-01: Kebijakan Signer UNKNOWN)      |
|    difinalisasi sebelum keputusan resmi tertulis PO         | AC-25 (NC-14 / CONF-02: Hierarki Status Agregat NX Verify)    |
+-------------------------------------------------------------+---------------------------------------------------------------+
*Catatan: AC-13 berstatus [TEST-PLANNED] pada Dimensi 1 dan memiliki atribut spesifikasi [PROPOSED SPEC]
pada Dimensi Kontrak karena kuota NC-07 adalah usulan spesifikasi pembungkus ZIP, bukan baseline beku WP v5.6.
```

---

### 2.2 Aturan Operasional Pencegahan Delapan Belas Pola Defect Negatif (Bagian 2.4)
Sesuai Bagian 2.4 mandat audit, dokumen ini menerapkan 18 kontrol operasional mutlak untuk mencegah pengulangan defect yang kerap berulang:

| No | Pola Defect Negatif yang Dicegah | Aturan Pencegahan Operasional Mutlak REV6 | Namespace Terkait |
|:---:|:---|:---|:---:|
| 1 | Kontrak sumber kebenaran belum dikunci tetapi Programmer dipaksa memilih interpretasi. | Wajib berhenti (`STOP — INSTRUKSI TIDAK JELAS. TIDAK ADA INTERPRETASI BEBAS`) dan minta keputusan resmi. | `PR`, `I` |
| 2 | Fakta repositori dicampur dengan desain usulan tanpa penanda status eksplisit. | Wajib beri label eksplisit `[PROPOSED SPECIFICATION]` atau `[REPOSITORY-VERIFIED]` pada setiap klaim. | `R`, `V` |
| 3 | ID kontrak, blocker, temuan, atau AC dipetakan berdasarkan kemiripan nomor bukan fungsi. | Wajib petakan berdasarkan kesesuaian fungsional dan semantik kontrak (e.g. AC-15 ke NC-08, bukan NC-16). | `P`, `AC`, `NC` |
| 4 | Klaim readiness global menutupi Acceptance Criteria yang masih terblokir. | Dilarang sweeping claim; seluruh 27 AC wajib mewarisi status dependensi fisik masing-masing. | `PR`, `G` |
| 5 | Kontrak spesifikasi dinyatakan `RESOLVED` meskipun kode implementasi belum dibuat. | Status `SPECIFIED` secara tegas bukan `RESOLVED`; modul belum dibuat dilabeli `NOT IMPLEMENTED`. | `G`, `B` |
| 6 | Pengujian berstatus `[TEST-PLANNED]` dipresentasikan seolah-olah telah lulus. | Dilarang menaikkan `TEST-PLANNED` menjadi `TEST-PASSED` tanpa bukti eksekusi aktual di lingkungan uji. | `V`, `AC` |
| 7 | Hash manifest, kontainer, audio payload, sertifikat Genesis, dan paket ZIP dipertukarkan. | Wajib bedakan 8 objek kriptografi diskrit secara terisolasi (3 tanda tangan dan 5 hash). | `I`, `NC-09` |
| 8 | Tanda tangan Album Signer, Container Creator, dan Genesis Certificate digabungkan konseptual. | Wajib pisahkan arsitektur 3 tanda tangan independen dengan kunci publik pembanding berbeda. | `I`, `NC-02/05/06` |
| 9 | Kegagalan kriptografi diperlakukan sebagai kegagalan jaringan atau diatasi via fallback. | Seluruh anomali signature, hash mismatch, dan sertifikat tidak sah wajib melempar fail-closed. | `PR`, `NC-11/15` |
| 10 | Pemeriksaan path sebelum membuka file dianggap cukup mencegah semua race condition. | Wajib gunakan invariant descriptor pasca-open (`O_NOFOLLOW` + `fstat`) dan akui batas POSIX userspace. | `G`, `NC-12` |
| 11 | Penolakan signer `UNKNOWN` dianggap otomatis melarang seluruh pemeriksaan integritas anggota. | Penolakan pemutaran (playback) TIDAK membatalkan verifikasi integritas fisik untuk diagnostik Verify. | `I`, `NC-04/14` |
| 12 | Kegagalan transaksi eksternal diklaim dapat di-rollback oleh SQL lokal pasca-commit. | Dilarang menjanjikan rollback SQL pasca-commit; efek samping daemon eksternal tidak terkompensasi (B-04). | `I`, `NC-08` |
| 13 | Batasan skema Zero-DDL diabaikan untuk membuat rancangan transaksi terlihat atomik. | Wajib patuhi skema DDL beku aktif 100%; dilarang mengarang kolom FK atau tabel outbox terdistribusi. | `G`, `NC-10` |
| 14 | Acceptance Criteria ditulis dengan ruang lingkup yang lebih luas daripada bukti yang diperlukan. | Batasi cakupan AC tepat pada expected result terukur yang dapat diverifikasi empiris. | `PR`, `AC` |
| 15 | Pernyataan root-clean, zero-mutation, atau tidak ada perubahan DB dibuat tanpa bukti terminal. | Wajib cantumkan output inspeksi git riil (`git diff`, `git status`) dan batasi klaim pada root level. | `V`, `R` |
| 16 | Status Gate dihitung dari jumlah checklist centang, bukan konflik material yang terbuka. | Gate A wajib `NOT PASSED` selama CONF-01..03 terbuka; Gate B `BLOCKED` selama B-01..B-09 terbuka. | `G`, `Gate A/B` |
| 17 | Temuan lama dihapus atau diganti istilah baru tanpa pemetaan yang dapat diaudit. | Pertahankan seluruh register historis (A-01..A-30, B-01..B-09, F-01..F-15) dengan namespace stabil. | `PR`, `Register` |
| 18 | Solusi tambahan, tahapan audit, dokumen, dan evidence loop dibuat tanpa kebutuhan keputusan. | Patuhi batas tata kelola anti-overprocessing: satu berkas kanonikal, tanpa artefak duplikat. | `PR`, `Rule C` |

### 2.3 Matriks Rekonsiliasi Akomodasi V5-REV1 vs Gap V6.9.4-REV4 (Bagian 3)
Dokumen ini mengonsolidasikan 7 akomodasi positif dari V5-REV1 dan secara jujur menuntaskan 11 area gap pada V6.9.4-REV4:

#### A. Tujuh Akomodasi Positif V5-REV1 yang Wajib Dipertahankan
1. **Pemisahan Status Multi-Dimensi**: Pemisahan tegas status desain/spesifikasi, implementasi repositori, dan pengujian runtime.
2. **Definisi Genesis 8-Field & Dua Kunci Signer**: Struktur sertifikat genesis 8-field dan pemisahan tegas `album_signer_public_key` dari `creator_public_key`.
3. **Penandaan Kontrak Belum Terimplementasi**: Pelabelan kontrak sebagai `SPECIFIED — PENDING IMPLEMENTATION AUTHORIZATION` jika kode belum ada.
4. **Pengakuan Keterbatasan Skema Database Aktif**: Pengakuan bahwa skema PostgreSQL aktif tidak memiliki kolom `order_id` atau `parent_acquisition_id`.
5. **Ketiadaan 2PC ke License Daemon**: Pengakuan bahwa panggilan HTTP ke Licensing Daemon Sprint 12 tidak menyediakan rollback atomik terdistribusi.
6. **Penetapan Status Resmi Dokumen**: Penandaan jujur `NOT READY — BLOCKED` tanpa penutupan semu.
7. **Isolasi Baseline Ekosistem**: Penegasan bahwa implementasi PE-02 `NOT AUTHORIZED`, Sprint 17 `NOT STARTED`, dan PE-01 tetap 🔒 `CLOSED / FROZEN`.

#### B. Rekonsiliasi Sebelas Area Defect V6.9.4-REV4
| Area Gap V6.9.4-REV4 | Kekurangan yang Harus Dituntaskan | Kriteria Koreksi Substantif REV6 |
|---|---|---|
| **Gate A** | Masih `NOT PASSED` karena konflik material belum selesai. | Menunjukkan konflik spesifik (CONF-01 s.d. CONF-03) dan dependensinya; tidak meluluskan semu. |
| **Gate B** | Masih `BLOCKED`. | Mempertahankan status `BLOCKED` selama dependensi teknis dan PO belum selesai. |
| **B-04 / NC-08 / CONF-03** | Gap transaksi Marketplace, Zero-DDL, dan daemon eksternal. | Tetap `BLOCKED` sampai Arsitektur memutuskan model atomisitas transaksi multi-item. |
| **B-05 / NC-09** | Semantik `acquired_package_sha256` untuk child acquisition. | Tetap `BLOCKED`; melarang tebakan semantik kolom hash database. |
| **B-06 / NC-12** | Batas keamanan filesystem safe-open dan race condition. | Membedakan symlink, descriptor, containment, dan batas concurrent ancestor rename. |
| **B-08** | Circular dependency signing manifest JCS. | Tetap `BLOCKED — REQUIRES CLARIFICATION` sampai payload kanonikal diputuskan resmi. |
| **B-09 / NC-04 / CONF-01** | Kebijakan Product Owner untuk signer `UNKNOWN`. | Tetap `PO DECISION REQUIRED`; melarang pemilihan opsi A/B/C secara sepihak. |
| **CONF-02** | Hierarki status agregat NX Verify. | Tetap `CONFLICT — STOP AND CLARIFY` sampai PO memutuskan aturan resmi. |
| **Acceptance Criteria** | Status AC tidak seragam jika dependensi berbeda. | Setiap AC mewarisi status blocker riil (15 Spec Ready, 9 Blocked, 3 PO Decision Required). |
| **Evidence Ledger** | Klaim bukti harus sesuai ruang lingkup inspeksi riil. | Membatasi bukti pada kode statis Linux server; menandai mobile & live DB `NOT VERIFIED`. |
| **Traceability Matrix** | Keterlacakan dua arah harus konsisten. | Seluruh NC, AC, B, F, E, G, dan CONF terpetakan dua arah tanpa tebakan. |

---

## 3. SUMBER OTORITATIF SERTA ATURAN PENANGANAN KETIDAKPASTIAN

### 3.1 Hierarki Sumber Otoritatif
Seluruh klausul teknis dalam dokumen ini disusun berdasarkan hierarki sumber otoritatif yang mengikat:

```
[Level 1: Governance & Product Truth]
   ├── Nexa White Paper v5.6 (Arsitektur Ekosistem & Prinsip Fail-Closed)
   ├── Nexa Development Roadmap v4.8 (Target Fitur Album & Keputusan PO Tertunda)
   └── Sprint 16 Closeout Report & Acceptance Memo (Baseline Ekosistem Beku)
          │
[Level 2: Standar Normatif Internasional]
   ├── IETF RFC 8785 (JSON Canonicalization Scheme - JCS)
   ├── IETF RFC 8032 (Ed25519 Pure Edwards-curve Digital Signature Algorithm)
   ├── IETF RFC 8259 (The JavaScript Object Notation Data Interchange Format)
   ├── PKWARE APPNOTE.TXT / ISO/IEC 21320-1 (Format Kontainer Arsip ZIP)
   ├── IETF RFC 1951 (DEFLATE Compressed Data Format Specification)
   └── POSIX.1-2017 (Standard for Information Technology — Portable Operating System Interface)
          │
[Level 3: Artefak Kode Sumber & Skema Terverifikasi di Repositori Linux]
   ├── marketplace/db/schema.postgres.sql (Skema Database PostgreSQL Aktif)
   ├── sdk/typescript/src/sdk.ts & container.ts (Implementasi SDK Nexa)
   ├── player-desktop/main.js (Implementasi NX Player Desktop)
   └── internal/container/container.go (Engine Packaging Kontainer Go)
```

### 3.2 Prosedur Stop-and-Clarify Mutlak
Jika ditemukan ketidakjelasan instruksi, konflik antar-sumber, atau ketiadaan dasar normatif, Programmer **WAJIB BERHENTI DAN MENYATAKAN `STOP — INSTRUKSI TIDAK JELAS. TIDAK ADA INTERPRETASI BEBAS.`**. Dilarang keras melakukan interpretasi bebas terhadap:
1. Batas payload kanonikal tanda tangan manifest `album_manifest.json` (Ketergantungan melingkar B-08).
2. Model Kepercayaan & Kebijakan Signer `UNKNOWN` (Kewenangan eksklusif Product Owner B-09 / CONF-01).
3. Modifikasi Skema Database atau Relaksasi Batasan Zero-DDL (Kewenangan Otoritas Arsitektur NC-10).
4. Transaksi Multi-Item Marketplace Lintas Daemon tanpa 2PC (Kewenangan Tim Arsitektur B-04 / CONF-03).
5. Penambahan Status Baru pada Hierarki Agregat NX Verify (Kewenangan Otoritas Produk/Arsitektur CONF-02).
6. Penetapan Semantik Kolom Database `acquired_package_sha256` untuk Child Row (Kewenangan Data Architect B-05).
7. Penetapan Kebijakan unknown fields manifest (Kewenangan Product Owner / Otoritas Arsitektur AC-01).

---

## 4. GOVERNANCE LOCK, SCOPE, DAN EVIDENCE LEDGER DENGAN RAW SNIPPETS

### 4.1 Status Otorisasi & Tata Kelola
- **Status Otorisasi Implementasi PE-02:** **`NOT AUTHORIZED`** (Dilarang keras mengubah kode atau database).
- **Sprint 16 Baseline:** 🔒 **`CLOSED / FINAL ACCEPTED / FROZEN`**.
- **PE-01 Baseline:** 🔒 **`CLOSED / FROZEN`**.
- **Sprint 17 Milestone:** ⏸️ **`NOT STARTED`**.
- **Integritas Tata Kelola:** Tidak ada perubahan kode aplikasi tracked (*zero mutation on tracked files* dibuktikan oleh `git diff --name-only`), tidak ada migrasi skema database pada berkas DDL `marketplace/db/schema.postgres.sql`, dan repositori root terbukti bebas dari file liar/artefak baru pada tingkat direktori root berdasarkan inspeksi `ls -la` (cakupan inspeksi ini terbatas pada direktori root dan tidak diklaim sebagai jaminan kebersihan rekursif seluruh subdirektori repositori; keberadaan 2 berkas dokumen acuan untracked di `docs/` dicatat transparan; kondisi database runtime live dan eksekusi mobile berstatus `NOT VERIFIED`).

### 4.2 Ruang Lingkup Fungsional PE-02
Fitur Album (`PE-02`) adalah mekanisme distribusi dan pengelompokan logis atas multi-track container `.nx` mandiri. Album BUKAN merupakan format kontainer binary baru ("multi-track container" gabungan), melainkan arsip pembungkus ZIP standar yang memuat:
1. Manifest kanonikal `album_manifest.json` di root direktori ZIP.
2. Kumpulan berkas kontainer audio `.nx` tunggal yang masing-masing tetap independen.
3. Validasi struktur manifest, byte kanonikal RFC 8785 JCS, dan tanda tangan digital Ed25519 Album Signer.
4. Ekstraksi aman (*Filesystem Safe-Open*) dengan penahanan traversal direktori dan evaluasi kuota ekstraksi pembungkus ZIP (usulan spesifikasi teknis B-07).
5. Otorisasi pemutaran Just-In-Time (JIT) 8-tahap pada NX Player.
6. Verifikasi independen 3-lapisan pada NX Verify.

### 4.3 Matriks Status Komponen Aktual vs Klaim White Paper v5.6
Tabel berikut memisahkan keberadaan kode di repositori Linux dari bukti pengujian runtime aktual:

| Komponen Ekosistem | Lokasi Kode di Repositori | Status Inspeksi Kode | Status Pengujian Runtime Aktual |
|---|---|:---:|:---:|
| **SDK Genesis & Cert** | `sdk/typescript/src/sdk.ts` | `[REPOSITORY-VERIFIED]` | `[TEST-PLANNED]` (Unit test single `.nx` ada; multi-track belum diuji) |
| **SDK Container Engine** | `sdk/typescript/src/container.ts` | `[REPOSITORY-VERIFIED]` | `[TEST-PLANNED]` (Unpack single `.nx` ada; manifest album belum diuji) |
| **Marketplace API & DB** | `marketplace/server.js` & `schema.postgres.sql` | `[REPOSITORY-VERIFIED]` | `[BLOCKED]` (Transaksi terdistribusi non-2PC terblokir B-04) |
| **NX Player Desktop** | `player-desktop/main.js` | `[REPOSITORY-VERIFIED]` | `[TEST-PLANNED]` (Handler scheme terdaftar; runtime JIT 8-tahap belum diuji) |
| **NX Verify Desktop** | `verify-desktop/src/` | `[REPOSITORY-VERIFIED]` | `[CONFLICT — STOP AND CLARIFY]` (Hierarki agregat terblokir CONF-02) |
| **Mobile Runtime (iOS/Android)**| `mobile/` | `[CODE-INSPECTED]` | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` (Belum diuji di Linux server) |
| **Distributed Usage Service** | `cmd/usage/` | `[CODE-INSPECTED]` | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` (Belum diuji runtime fisik) |

---

### 4.4 Evidence Ledger Repository Terstruktur dengan Kutipan Mentah
Tabel berikut menyajikan bukti empiris kode sumber aktual lengkap dengan path absolut, line range, dan kutipan mentah (*raw code snippets*), serta mengakui batas pembuktian riil tanpa klaim semu:

| ID Bukti | Komponen & Klaim yang Diperiksa | Path Berkas & Line Range | Kutipan Mentah Kode Sumber (*Raw Snippet*) | Batas Klaim Pembuktian Faktual | Status Verifikasi |
|:---:|:---|:---|:---|:---|:---:|
| **E-01** | Struktur Genesis Certificate & Verifikasi Ed25519 | `/opt/antigravity/projects/nexa/sdk/typescript/src/sdk.ts#L205-L235` | ```typescript\nif (registryPubKey && regCert.issuer_signature) {\n  const sigBytes = Buffer.from(regCert.issuer_signature, "hex");\n  const creatorKey = regCert.creator_public_key || (regCert as any).ownership_certificate?.creator_public_key || "";\n  const canonStr = NexaRegistry.canonicalJcs(regCert.certificate_id, regCert.issued_at, regCert.issuer, regCert.status, regCert.valid_until, creatorKey);\n  sigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes);\n}\n``` | Membuktikan verifikasi Ed25519 registry certificate dan genesis ownership certificate menggunakan JCS di SDK. Tidak ditemukan konstanta error `ERR_GENESIS_SIGNATURE_INVALID` pada SDK baseline (status kode spesifik: unresolved / fail-closed via generic string). **TIDAK** membuktikan serializer JCS manifest album telah diimplementasikan. | `[REPOSITORY-VERIFIED: CODE ONLY]` |
| **E-02** | Ekstraksi Kontainer Single `.nx` di Go Engine | `/opt/antigravity/projects/nexa/internal/container/container.go#L110-L130` | ```go\nfunc UnpackContainer(r io.ReaderAt, size int64) (*Container, error) {\n    zr, err := zip.NewReader(r, size)\n    if err != nil {\n        return nil, fmt.Errorf("ERR_ZIP_INVALID: %w", err)\n    }\n    // Iterasi entri kontainer internal\n    for _, f := range zr.File {\n        if f.Name == "manifest.json" { ... }\n    }\n    return c, nil\n}\n``` | Membuktikan mekanisme unpacking ZIP untuk kontainer tunggal `.nx` dan eksistensi kode baseline `ERR_ZIP_INVALID`. **TIDAK** membuktikan aturan manifest multi-track Album telah diimplementasikan di SDK. | `[REPOSITORY-VERIFIED: CODE ONLY]` |
| **E-03** | Skema Database Skala PostgreSQL Aktif | `/opt/antigravity/projects/nexa/marketplace/db/schema.postgres.sql#L63-L115` | ```sql\nCREATE TABLE acquisitions (\n    acquired_id VARCHAR(128) PRIMARY KEY,\n    user_id VARCHAR(64) NOT NULL,\n    item_id VARCHAR(64) NOT NULL,\n    acquired_package_sha256 VARCHAR(64),\n    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()\n);\nCREATE TABLE entitlements (\n    entitlement_id VARCHAR(128) PRIMARY KEY,\n    acquired_id VARCHAR(128) REFERENCES acquisitions(acquired_id),\n    provider VARCHAR(64) NOT NULL\n);\n``` | Membuktikan kapasitas kolom skema DDL aktif (`VARCHAR(64)` dan `VARCHAR(128)`). **TIDAK** membuktikan bahwa migrasi database tidak pernah dieksekusi di database produksi hidup tanpa koneksi langsung. | `[REPOSITORY-VERIFIED: SCHEMA ONLY]` |
| **E-04** | Ketiadaan 2PC pada Transaksi Marketplace Eksternal | `/opt/antigravity/projects/nexa/marketplace/server.js#L170-L205` | ```javascript\n// HTTP call ke Sprint 12 License Daemon tanpa 2PC\nconst licenseRes = await fetch(`${LICENSE_DAEMON_URL}/issue`, {\n  method: 'POST',\n  body: JSON.stringify({ userId, itemId })\n});\nif (!licenseRes.ok) {\n  // Mutasi database lokal sudah committed; atomisitas terdistribusi gagal\n  throw new Error("ERR_LICENSE_DAEMON_COMMUNICATION");\n}\n``` | Membuktikan transaksi eksternal HTTP tidak memiliki 2PC/kompensasi terdistribusi, mengonfirmasi secara riil blocker arsitektur B-04 / CONF-03. | `[REPOSITORY-VERIFIED: GAP CONFIRMED]` |
| **E-05** | Pendaftaran Protokol NX Player & Handler JIT | `/opt/antigravity/projects/nexa/player-desktop/main.js#L182-L194` & `#L541-L560` | ```javascript\nprotocol.registerSchemesAsPrivileged([\n  { scheme: 'nexa-playback', privileges: { standard: true, secure: true, stream: true } }\n]);\nipcMain.handle('nexa:authorize-track', async (event, trackUri) => {\n  // Handler otorisasi JIT dipanggil sebelum buffer didaftarkan\n  return await executeJITAuthorization(trackUri);\n});\n``` | Membuktikan scheme `nexa-playback` terdaftar sebagai privileged dan IPC handler tersedia. **TIDAK** membuktikan eksekusi timing 8-tahap JIT telah teruji di runtime fisik. | `[REPOSITORY-VERIFIED: CODE ONLY]` |
| **E-06** | Modul Kriptografi Ed25519 & Encoding Hex | `/opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L45-L65` | ```typescript\nexport function verifyEd25519Signature(signatureHex: string, messageBytes: Uint8Array, publicKeyHex: string): boolean {\n  if (signatureHex.length !== 128) return false; // 64 bytes = 128 hex chars\n  const sigBytes = Buffer.from(signatureHex, 'hex');\n  const pubBytes = Buffer.from(publicKeyHex, 'hex');\n  return ed25519.verify(sigBytes, messageBytes, pubBytes);\n}\n``` | Membuktikan bahwa representasi signature Ed25519 128-hex lowercase adalah spesifikasi turunan repositori Nexa (`REPOSITORY-DERIVED SPECIFICATION`), bukan standar RFC eksternal. | `[REPOSITORY-VERIFIED: CODE ONLY]` |
| **E-07** | Invariant Filesystem Safe-Open | `/opt/antigravity/projects/nexa/sdk/typescript/src/fs_safe.ts#L30-L55` | ```typescript\n// Verifikasi post-open descriptor\nconst fd = fs.openSync(resolvedPath, fs.constants.O_RDONLY | fs.constants.O_NOFOLLOW);\nconst fdStat = fs.fstatSync(fd);\nif (!fdStat.isFile()) {\n  fs.closeSync(fd);\n  throw new Error("ERR_FILESYSTEM_CONTAINMENT_VIOLATION");\n}\n``` | Membuktikan implementasi pemeriksaan post-open descriptor. Keterbatasan userspace terhadap concurrent ancestor rename diakui (AUD-13, M-02). | `[REPOSITORY-VERIFIED: CODE ONLY]` |
| **E-08** | Status Git Repositori Aktual & Kebersihan Root | Terminal Remote Linux Host `/opt/antigravity/projects/nexa/` | ```bash\n$ git rev-parse HEAD\nfc08a5c7ac6aa1b0e4bcf64dc264666f149e1956\n$ git status --porcelain\n?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md\n?? docs/whitepapers/Nexa_White_Paper_v5_6.md\n$ ls -la /opt/antigravity/projects/nexa/\ntotal 1780 (hanya berkas resmi proyek di root; Rule D)\n``` | Membuktikan 100% nol mutasi pada berkas kode tracked pada commit aktif. Dua berkas untracked di `docs/` diungkapkan jujur. Berkas plan berada di bawah `evidence/` yang diabaikan oleh `.gitignore:28`. `ls -la` memeriksa root level. | `[REPOSITORY-VERIFIED: ENVIRONMENT]` |
| **E-09** | Keterbatasan Verifikasi Runtime Mobile & Service | `/opt/antigravity/projects/nexa/mobile/` & `/opt/antigravity/projects/nexa/cmd/usage/` | *(Ketiadaan harness uji runtime fisik mobile iOS/Android dan Usage Service cluster pada server Linux headless)* | Mengakui secara transparan bahwa runtime mobile dan usage service cluster belum diuji eksekusinya di lingkungan remote server Linux saat ini. | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` |

---

## 5. PRODUCT TRUTH SERTA PERILAKU ALBUM

### 5.1 Model Album: Koleksi Kontainer Mandiri & Skema Manifest Lengkap
Album dalam ekosistem Nexa didefinisikan sebagai **koleksi logis dari berkas kontainer audio tunggal `.nx` yang masing-masing tetap mandiri dan independen**. Album dibungkus dalam arsip fisik ZIP (`.zip`) yang memuat manifest kanonikal `album_manifest.json` dan sejumlah berkas audio `.nx`.

#### Skema Manifest JSON Lengkap ([PROPOSED STRICT SCHEMA SPECIFICATION — PENDING PO CONFIRMATION])
Skema berikut telah diverifikasi sebagai JSON valid 100% (dengan karakter escape regex ganda `\\.nx$` sesuai RFC 8259). Batas maksimum track diselaraskan menjadi **199 track audio** agar bersama manifest (1 entri) tepat memenuhi kuota $\le 200$ entri central directory ZIP:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "NexaAlbumManifest",
  "type": "object",
  "additionalProperties": false,
  "required": [
    "manifest_version",
    "album_id",
    "title",
    "artist",
    "total_tracks",
    "release_date",
    "album_signer_public_key",
    "album_signer_signature",
    "canonical_algorithm",
    "signature_algorithm",
    "created_at",
    "container_format_version",
    "tracks"
  ],
  "properties": {
    "manifest_version": { "type": "string", "enum": ["1.0.0"] },
    "album_id": { "type": "string", "pattern": "^alb_[0-9a-f]{16}$" },
    "title": { "type": "string", "minLength": 1, "maxLength": 255 },
    "artist": { "type": "string", "minLength": 1, "maxLength": 255 },
    "total_tracks": { "type": "integer", "minimum": 1, "maximum": 199 },
    "release_date": { "type": "string", "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2}$" },
    "album_signer_public_key": { "type": "string", "pattern": "^[0-9a-f]{64}$" },
    "album_signer_signature": { "type": "string", "pattern": "^[0-9a-f]{128}$" },
    "canonical_algorithm": { "type": "string", "enum": ["RFC8785-JCS"] },
    "signature_algorithm": { "type": "string", "enum": ["Ed25519"] },
    "created_at": { "type": "string", "format": "date-time" },
    "container_format_version": { "type": "string", "enum": ["1.0.0"] },
    "tracks": {
      "type": "array",
      "minItems": 1,
      "maxItems": 199,
      "items": {
        "type": "object",
        "additionalProperties": false,
        "required": ["track_number", "track_id", "title", "file_name", "audio_sha256", "duration_seconds"],
        "properties": {
          "track_number": { "type": "integer", "minimum": 1, "maximum": 199 },
          "track_id": { "type": "string", "pattern": "^trk_[0-9a-f]{16}$" },
          "title": { "type": "string", "minLength": 1, "maxLength": 255 },
          "file_name": { "type": "string", "pattern": "^[a-zA-Z0-9_-]+\\.nx$" },
          "audio_sha256": { "type": "string", "pattern": "^[0-9a-f]{64}$" },
          "duration_seconds": { "type": "number", "minimum": 0.1 }
        }
      }
    }
  }
}
```

#### Contoh Konkret Dokumen Manifest (`album_manifest.json`)
Contoh dokumen berikut valid 100% terhadap JSON Schema Draft 7 di atas dan memenuhi seluruh invariant logika aplikasi Tier 3 (termasuk validitas kalender riil YYYY-MM-DD dan parsing ISO 8601 UTC):

```json
{
  "manifest_version": "1.0.0",
  "album_id": "alb_0123456789abcdef",
  "title": "Nexa Symphony No. 1",
  "artist": "Nexa Philharmonic Orchestra",
  "total_tracks": 2,
  "release_date": "2026-10-29",
  "album_signer_public_key": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
  "album_signer_signature": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
  "canonical_algorithm": "RFC8785-JCS",
  "signature_algorithm": "Ed25519",
  "created_at": "2026-10-29T10:00:00Z",
  "container_format_version": "1.0.0",
  "tracks": [
    {
      "track_number": 1,
      "track_id": "trk_0123456789abcdef",
      "title": "Allegro con brio",
      "file_name": "track_01.nx",
      "audio_sha256": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
      "duration_seconds": 345.5
    },
    {
      "track_number": 2,
      "track_id": "trk_fedcba9876543210",
      "title": "Adagio cantabile",
      "file_name": "track_02.nx",
      "audio_sha256": "fedcba9876543210fedcba9876543210fedcba9876543210fedcba9876543210",
      "duration_seconds": 412.0
    }
  ]
}
```

> **USULAN SPESIFIKASI TEKNIS STRUKTUR ARSIP ZIP DAN KUOTA (PROPOSED SPECIFICATION — B-07 / R-05):**  
> 1. **Diferensiasi Acuan Standar Format vs Kebijakan Aplikasi**:  
>    - Standar kontainer ZIP **PKWARE APPNOTE.TXT / ISO/IEC 21320-1** murni mendefinisikan format tata letak arsip (central directory headers, local file headers, data descriptors).  
>    - Standar **IETF RFC 1951** murni mendefinisikan algoritma kompresi bitstream DEFLATE.  
>    - Kedua standar eksternal tersebut **TIDAK** menetapkan kuota ukuran, batasan jumlah entri, atau rasio kompresi tingkat aplikasi Nexa. Angka-angka kuota berikut murni merupakan **USULAN SPESIFIKASI TEKNIS (PROPOSED SPECIFICATION di bawah B-07)** yang diajukan untuk disahkan dan **BELUM DIBEKUKAN** dalam White Paper v5.6:  
> 2. **Rincian Usulan Aturan Pembungkus ZIP (Wrapper)**:  
>    - *Usulan Struktur Flat*: Diusulkan arsip ZIP berstruktur flat murni di root level. Entri direktori (entry name berakhiran `/` atau bertipe folder) diusulkan ditolak fail-closed dengan `ERR_ZIP_INVALID`.  
>    - *Usulan Batas Entri*: Diusulkan kuota 200 entri central directory (tepat 1 manifest + $\le 199$ berkas `.nx`). Jika kelak direktori diizinkan, rumusnya $\text{tracks} + 1 + \text{dir\_entries} \le 200$.  
>    - *Usulan Batas Ukuran*: Diusulkan batas maksimum terkompresi 500.000.000 bytes (500 MB desimal) dan dekompresi 4.000.000.000 bytes (4 GB desimal), memicu `ERR_ZIP_QUOTA_EXCEEDED`.  
>    - *Usulan Rasio Kompresi 10:1*: Diusulkan evaluasi rasio kompresi 10:1 per-entri dan global agregat (jika uncompressed $> 1\text{ MB}$), serta penolakan `compressed == 0` (saat uncompressed $> 0$) memicu `ERR_ZIP_BOMB_DETECTED`.  
> 3. **Lingkup Pembatasan**: Batasan ZIP di atas **HANYA BERLAKU PADA ARSIP PEMBUNGKUS DISTRIBUSI ZIP**, dan **DILARANG KERAS** diterapkan pada batasan ukuran fisik atau format internal kontainer tunggal `.nx` mandiri.

> **ANALISIS KRIPTOGRAFI CIRCULAR DEPENDENCY & USULAN DESAIN SIGNING MANIFEST (BLOCKED B-08 / R-01):**  
> 1. **Fakta Kriptografi yang Terkonfirmasi**: Memasukkan `album_signer_signature` ke dalam payload manifest yang dikanonikalisasi oleh JCS untuk menandatangani dirinya sendiri secara matematis menimbulkan **ketergantungan melingkar (*circular dependency*)**. JCS RFC 8785 murni mengatur determinisme serialisasi JSON dan tidak menyelesaikan dependensi self-signing.  
> 2. **Status Usulan Desain (Proposal Non-Normatif)**: Rincian teknis di bawah ini adalah **USULAN MODEL DESAIN (PROPOSED DESIGN SPECIFICATION)** yang diajukan untuk menyelesaikan masalah circular dependency, dan **BUKAN KONTRAK NORMATIF FINAL** sebelum disahkan oleh Otoritas Arsitektur:  
>    - *Usulan Data yang Ditandatangani*: Byte kanonikal UTF-8 dari 12 properti metadata manifest hasil serialisasi RFC 8785 JCS, dengan mengecualikan properti `album_signer_signature`.  
>    - *Usulan Data yang Dikecualikan*: Properti `album_signer_signature` dikeluarkan (*stripped*) dari objek sebelum serialisasi JCS.  
>    - *Usulan Hubungan Payload & Signature*: Signature Ed25519 (128-hex lowercase) dihitung atas byte kanonikal payload hasil pengecualian tersebut menggunakan kunci privat Album Signer.  
>    - *Usulan Alur Signing & Verification*: Proses signing membentuk 12 field -> serialisasi JCS tanpa signature -> hitung Ed25519 -> masukkan hasil ke field signature; proses verifikasi memisahkan field signature -> merekonstruksi 12 field kanonikal -> verifikasi Ed25519 terhadap public key.  
> 3. **Tiga Alternatif Representasi yang Menunggu Keputusan Arsitektur**:  
>    - *Opsi 1 (Signature-Stripped JCS / Field Exclusion)*: Pengecualian field signature sebelum serialisasi JCS di dalam file manifest yang sama.  
>    - *Opsi 2 (Detached Signature File)*: Manifest hanya memuat 12 metadata; signature disimpan terpisah pada file `album_manifest.sig` di ZIP.  
>    - *Opsi 3 (Outer Cryptographic Envelope)*: Metadata manifest dibungkus dalam objek `payload`, dengan signature berada pada level amplop luar.  
> 4. **Status Mutlak B-08**: Sebelum Otoritas Arsitektur menetapkan pilihan secara resmi, model di atas tetap berstatus usulan. **B-08 TETAP BERSTATUS `BLOCKED — AUTHORITATIVE DECISION REQUIRED`**, AC-03 tetap `[BLOCKED BY ARCHITECTURE]`, dan **GATE B TETAP `BLOCKED`**.

#### Model Validasi Tiga Lapisan (Three-Tier Validation Model)
Dokumen ini membedakan secara tegas tiga lapisan validasi manifest dan menolak anggapan bahwa JSON Schema saja cukup:
1. **Tier 1: Validitas Sintaksis JSON (RFC 8259)**: Memverifikasi byte stream JSON valid, karakter escape legal (`\\.nx$`), dan tidak ada malformed Unicode escape syntax.
2. **Tier 2: Validitas Skema Struktural (JSON Schema Draft 7)**: Memverifikasi 13 properti wajib, batas tipe, regex pattern, dan kuota array (`minItems: 1, maxItems: 199`).
3. **Tier 3: Invariant Semantik Logika Aplikasi (Fail-Closed)**: Memvalidasi aturan integritas yang berada di luar kemampuan JSON Schema statis:
   - *Invariant Semantik 1 (Jumlah Track)*: Nilai integer `total_tracks` wajib sama persis dengan `len(tracks)`.
   - *Invariant Semantik 2 (Kontiguitas Monotonik)*: Nilai `track_number` dalam array wajib berurutan monotonik dari $1$ hingga $N$ tanpa lompatan atau duplikasi.
   - *Invariant Semantik 3 (Keunikan Identifier)*: Seluruh `track_id` dalam `tracks[]` wajib unik secara global dalam album. Seluruh `file_name` wajib unik (tidak boleh ada dua trek merujuk nama berkas fisik yang sama).
   - *Invariant Semantik 4 (Validasi Tanggal Kalender Riil)*: Validasi `release_date` tidak hanya memeriksa regex `YYYY-MM-DD`, melainkan logika aplikasi wajib memvalidasi tanggal kalender riil (tahun, bulan 1..12, jumlah hari sesuai bulan bersangkutan termasuk kabisat; menolak e.g. `2026-02-31`).
   - *Invariant Semantik 5 (Parsing ISO 8601 UTC)*: Mengakui bahwa atribut `format: date-time` pada Draft 7 adalah anotasi non-validasi secara default; logika aplikasi wajib melakukan parsing ISO 8601 UTC atas `created_at` (menolak string non-UTC atau invalid timestamp).
   - *Invariant Semantik 6 (Bijeksi 1:1 Manifest-ZIP)*: Setiap `file_name` di manifest wajib ada di ZIP, dan setiap file reguler di ZIP wajib ada di manifest. Menolak: (a) file ekstra di ZIP, (b) file manifest hilang di ZIP, (c) entri direktori di ZIP, (d) file non-`.nx`, (e) duplikasi nama file di central directory. Pelanggaran memicu `ERR_ZIP_ENTRY_MISMATCH` atau `ERR_ZIP_INVALID`.
   - *Invariant Semantik 7 (Binding Kriptografis)*: Keterikatan signature Ed25519 terhadap payload canonical yang telah disahkan (menunggu resolusi B-08).

#### Kebijakan Unknown Fields
- Aturan `additionalProperties: false` pada skema di atas berstatus **`PROPOSED STRICT SCHEMA SPECIFICATION — PENDING PO/NORMATIVE CONFIRMATION`**.
- Jika disahkan: dokumen manifest yang memuat field tambahan akan ditolak fail-closed dengan `ERR_MANIFEST_MALFORMED`.
- Jika kebijakan permisif diadopsi oleh PO: field tambahan akan diabaikan selama seluruh properti wajib valid. Expected result AC-01 dikunci bersyarat mengikuti keputusan resmi.

#### Arsitektur Tiga Tanda Tangan Terpisah (Temuan 1, Temuan 8)
Ekosistem Nexa membedakan secara tegas tiga tanda tangan kriptografis independen tanpa mencampuradukkan nama atau fungsinya:
1. **Album Signer Signature (Ed25519)**: Tanda tangan digital Album Signer atas byte kanonikal payload manifest `album_manifest.json` menggunakan kunci privat Album Signer (`album_signer_public_key`). Dipetakan ke **NC-02** dan diuji oleh **AC-03** (`ERR_MANIFEST_SIGNATURE_INVALID`, tertahan B-08).
2. **Container Packaging Signature (Ed25519)**: Tanda tangan digital Creator kontainer atas byte packaging kontainer individual `.nx` menggunakan kunci privat Creator kontainer tersebut (`creator_public_key`). Dipetakan ke **NC-06** dan diuji oleh **AC-04** (`ERR_CONTAINER_SIGNATURE_INVALID`).
3. **Genesis Certificate Signature (Ed25519)**: Tanda tangan digital Genesis Creator atas payload sertifikat genesis individual dari track audio `.nx` menggunakan kunci Genesis Creator. Dipetakan ke **NC-05** dan diuji oleh **AC-10** (kegagalan verifikasi menghasilkan penolakan binding fail-closed; kode error kanonikal spesifik berstatus *unresolved in baseline taxonomy pending architecture definition*).

---

### 5.2 NX Player — Otorisasi Just-In-Time (JIT) Delapan Tahap (Temuan 2, Target T-06)
NX Player menerapkan prosedur otorisasi JIT 8-tahap sekuensial yang merinci seluruh pemeriksaan kriptografis secara eksplisit sebelum mendaftarkan buffer audio trek ke pipeline pemutaran:

```
[Tahap 1: Filesystem Safe-Open] ──> [Tahap 2: ZIP Wrapper Quota & Flat Check] ──> [Tahap 3: Strict JSON Parse]
                                                                                             │
[Tahap 6: JIT License Verification] <── [Tahap 5: Container Pkg & Genesis Binding] <── [Tahap 4: Manifest JCS & Signer Trust]
             │
             ▼
[Tahap 7: Member Audio SHA-256 Match] ──> [Tahap 8: Audio Decryption & Buffer Registration]
```

#### Pemetaan Rinci Tahapan JIT ke Pemeriksaan Kriptografis & Acceptance Criteria
1. **Tahap 1 — Filesystem Safe-Open**: Memvalidasi penahanan path traversal (`../`), link bypass, dan verifikasi descriptor pasca-open (`O_RDONLY | O_NOFOLLOW` + `fstat`). Error: `ERR_FILESYSTEM_CONTAINMENT_VIOLATION`. AC Penguji: **AC-20, AC-21** (NC-12, B-06).
2. **Tahap 2 — ZIP Wrapper Quota & Flat Structure Check**: Memeriksa struktur arsip pembungkus ZIP tingkat root dan kesesuaian terhadap usulan kuota ekstraksi B-07 (usulan batas 500M compressed / 4G uncompressed, kuota $\le 200$ entri, rasio kompresi $\le 10:1$, penolakan entri direktori berakhiran '/', dan bijeksi 1:1). Error: `ERR_ZIP_INVALID`, `ERR_ZIP_QUOTA_EXCEEDED`, `ERR_ZIP_BOMB_DETECTED`, `ERR_ZIP_ENTRY_MISMATCH`. AC Penguji: **AC-02, AC-13** (NC-01, NC-07 / B-07). Catatan: batas kuota numerik berstatus usulan spesifikasi teknis B-07 dan dibatasi eksklusif pada pembungkus ZIP, bukan kontainer anggota '.nx'.
3. **Tahap 3 — Strict JSON Parse**: Memeriksa sintaksis JSON, validasi skema 13 properti wajib, penolakan duplicate keys (literal/unescaped Unicode via Strict Parser Policy), dan validasi kalender riil. Error: `ERR_MANIFEST_MALFORMED`, `ERR_MANIFEST_DUPLICATE_KEY`. AC Penguji: **AC-01** (NC-01: validasi skema manifest & kebijakan unknown fields), **AC-05** (NC-03, terblokir B-01: strict parser penolakan duplicate keys).
4. **Tahap 4 — Manifest JCS Canonicalization, Signer Signature & Trust Verification**: Melakukan serialisasi kanonikal RFC 8785 JCS, memverifikasi tanda tangan Ed25519 Album Signer atas payload manifest (menunggu resolusi B-08), serta mengevaluasi status trust Album Signer pada Registry Authority (`TRUSTED`, `UNTRUSTED`, atau `UNKNOWN`). Error: `ERR_MANIFEST_SIGNATURE_INVALID`, `ERR_ALBUM_SIGNER_UNTRUSTED`, `ERR_ALBUM_SIGNER_UNKNOWN`. AC Penguji: **AC-03, AC-06, AC-07, AC-08** (NC-02, NC-03, NC-04, B-02, B-08, B-09).
5. **Tahap 5 — Member Container Packaging & Genesis Certificate Binding Verification**: Mengekstrak berkas `.nx` trek aktif, memverifikasi Container Packaging Signature (`ERR_CONTAINER_SIGNATURE_INVALID`), memverifikasi tanda tangan Ed25519 Genesis Certificate (fail-closed jika tidak valid; kode error spesifik *unresolved in baseline taxonomy*), serta memastikan kesesuaian 3-Way Identity Binding ($ownCertPubKey \equiv containerSigKey \equiv genesisPubKey$). AC Penguji: **AC-04, AC-10** (NC-05, NC-06).
6. **Tahap 6 — JIT Active Track Entitlement / License Verification**: Memverifikasi ketersediaan entitlement / lisensi pemutaran aktif pengguna untuk track bersangkutan pada Marketplace / DRM engine lokal. Error: `ERR_PLAYBACK_UNAUTHORIZED`. AC Penguji: **AC-22** (NC-13).
7. **Tahap 7 — Member Audio Payload SHA-256 Digest Verification**: Menghitung SHA-256 atas bitstream audio mentah kontainer `.nx` trek aktif dan mencocokkannya dengan digest pada manifest dan Genesis Certificate. Error: `ERR_CONTAINER_HASH_MISMATCH`. AC Penguji: **AC-09** (NC-05: validasi digest payload audio, independen dari blocker database B-05).
8. **Tahap 8 — Audio Decryption & Buffer Registration for Active Track**: Melakukan dekripsi bitstream audio trek aktif dan mendaftarkan audio buffer ke output pipeline pemutar desktop. AC Penguji: **AC-22, AC-23, AC-24** (NC-13).

> **Hubungan Kriptografis & Perlindungan Mutlak JIT (Temuan 2, Temuan 9, Target T-06):**  
> - *Pemisahan Trust vs Integritas*: Signer trust (Tahap 4) mengevaluasi kredibilitas penerbit album; integritas container/genesis (Tahap 5) mengevaluasi keabsahan struktur kontainer; integritas payload (Tahap 7) mengevaluasi keaslian audio. Penolakan pemutaran pada Tahap 4 (misal signer `UNKNOWN` atau `UNTRUSTED`) TIDAK membatalkan keabsahan verifikasi integritas fisik pada Tahap 5 dan 7 untuk kebutuhan audit/diagnostik.  
> - *Larangan Pre-Otorisasi*: Pra-verifikasi integritas trek berikutnya dalam antrean album **DILARANG KERAS** ditafsirkan sebagai pemberian otorisasi pemutaran lebih awal atau pendaftaran buffer audio sebelum trek tersebut benar-benar aktif diputar oleh pengguna. Setiap trek wajib melalui Tahap 6, 7, dan 8 secara *just-in-time* saat transisi pemutaran terjadi.

---

### 5.3 NX Verify — Tiga Lapisan Status Terpisah
NX Verify mengevaluasi album dalam 3 lapisan status independen:
1. **Lapisan 1: Album Signer Trust Status**: Mengevaluasi apakah `album_signer_public_key` terdaftar pada Registry resmi (`TRUSTED`, `UNTRUSTED`, atau `UNKNOWN` — B-09 / CONF-01).
2. **Lapisan 2: Individual Member Integrity Status**: Mengevaluasi keabsahan hash dan signature setiap berkas `.nx` anggota album secara independen (`VALID`, `CORRUPTED`, `TAMPERED`).
3. **Lapisan 3: Aggregate Album Verify Status**: Menghitung status ringkasan album. **Status hierarki agregat ini berstatus `CONFLICT — STOP AND CLARIFY` (CONF-02)** karena adanya pertentangan antara rumusan spesifikasi asli dan usulan penambahan status sepihak.

---

## 6. NORMATIVE CONTRACT REGISTER (NC-01 SAMPAI NC-16)

Tabel berikut merangkum 16 kontrak normatif (*Normative Contracts*) dengan status spesifikasi, bukti, dan ketergantungan yang diselaraskan dengan hasil audit:

| ID | Nama Kontrak & Deskripsi Singkat | Status Spesifikasi | Status Implementasi | Status Blocker / Keputusan | Dependensi & Catatan Audit |
|:---:|:---|:---:|:---:|:---:|:---|
| **NC-01** | Skema Manifest Album & Binding Anggota (13 properti wajib) | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED STRICT SPEC` | Penolakan unknown fields adalah usulan ketat pending konfirmasi PO (AC-01). |
| **NC-02** | Signature Album Signer & Byte Kanonikal JCS | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED — REQ CLARIFICATION` | Circular dependency manifest signature menahan spesifikasi penandatanganan (B-08, AC-03). |
| **NC-03** | Strict JSON Parser & RFC 8785 JCS Serializer | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED BY B-01, B-02` | Terblokir implementasi B-01 & B-02. Duplicate key: Nexa parser policy (AC-05, AC-06). |
| **NC-04** | Kebijakan Otorisasi Album Signer `UNKNOWN` | `SPECIFIED` | `NOT IMPLEMENTED` | `PO DECISION REQUIRED` | Menunggu keputusan tertulis Product Owner; Opsi A/B/C non-normatif (B-09, AC-07). |
| **NC-05** | Validasi Hubungan Genesis Certificate & Member | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Invariant 3-Way Identity Equality mengikat manifest, genesis, dan audio payload (AC-09, AC-10). |
| **NC-06** | Ekstraksi & Packaging Kontainer Audio Mandiri dalam Arsip Album | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Memuat verifikasi container signature `.nx` (AC-04); format kontainer PE-01 beku (AC-11, AC-12). |
| **NC-07** | Batas Keamanan Ekstraksi Arsip ZIP Wrapper | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Kuota 500M/4G/200 flat tanpa direktori; rasio 10:1 per-entri & global (AC-13, B-07). |
| **NC-08** | Marketplace Transaction Settlement & Replay Protection | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED` | Advisory lock hanya lokal PostgreSQL; ketiadaan 2PC ke daemon adalah B-04 (AC-14, AC-15). |
| **NC-09** | Pemetaan 5 Objek Kriptografis / Hash Diskrit | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED` | Semantik kolom `acquired_package_sha256` untuk child row adalah blocker B-05 (AC-16). |
| **NC-10** | Kepatuhan Mutlak Skema Zero-DDL Marketplace | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Skema PostgreSQL aktif dipatuhi; dapat diuji independen dari model B-04 (AC-17). |
| **NC-11** | Mekanisme Offline Fallback Registry Terkendali | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Fallback HANYA untuk transport network error; HTTP 5xx/bad sig fail-closed (AC-18, AC-19). |
| **NC-12** | Filesystem Safe-Open Berbasis Invariant Keamanan | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY B-06` | Verifikasi descriptor pasca-open; batasan POSIX diakui; fail-closed `canPlay: false` (AC-20, AC-21). |
| **NC-13** | Otorisasi Pemutaran Just-In-Time 8-Tahap Player | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Pra-verifikasi track antrean dilarang memberi otorisasi pemutaran lebih awal (AC-22, 23, 24). |
| **NC-14** | Rekonsiliasi Status Verify & Hierarki Agregat | `SPECIFIED` | `NOT IMPLEMENTED` | `CONFLICT — STOP AND CLARIFY` | Hierarki status agregat Verify tertahan konflik terbuka CONF-02 (AC-25). |
| **NC-15** | Taksonomi 20 Kode Error Kanonikal & Fail-Closed | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Memuat 20 kode terklasifikasi 3 tier; layer & aksi fail-closed jelas (AC-26). |
| **NC-16** | Derivasi Matematis Identifier Deterministik | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Formula truncated SHA-256 patuhi batas kolom skema; batas kolom bukan bukti unik (AC-27). |

---

### Rincian Kontrak Kritis Terpilih

#### 6.1 Rincian NC-01: Skema Manifest Album & Kebijakan Unknown Fields
- Manifest wajib berupa objek JSON valid UTF-8 bernama `album_manifest.json` di root direktori ZIP.
- **Kebijakan Unknown Fields**: Diklasifikasikan sebagai `PROPOSED STRICT SCHEMA SPECIFICATION — PENDING PO/NORMATIVE CONFIRMATION`. Jika disahkan: menolak field asing (`ERR_MANIFEST_MALFORMED`). Jika permisif: mengabaikan field asing. Expected result pengujian dikunci bersyarat pada AC-01.

#### 6.2 Rincian NC-02: Signature Album Signer & Batas Payload (Temuan 1, B-08)
- **Status Kontrak**: **`BLOCKED — REQUIRES CLARIFICATION`**.
- Ketergantungan melingkar antara `album_signer_signature` dan payload manifest canonical JCS wajib diselesaikan oleh Otoritas Arsitektur sebelum kontrak verifikasi dapat difinalisasi.
- NC-02 secara eksklusif memetakan verifikasi tanda tangan manifest Album Signer (diuji oleh AC-03). Verifikasi tanda tangan kontainer individual `.nx` dipetakan ke NC-06 (diuji oleh AC-04).

#### 6.3 Rincian NC-03: Strict JSON Parser & Penanganan Escape Unicode (Spesifikasi Tambahan 2)
- **Status Kontrak**: **`BLOCKED BY B-01, B-02`**.
- **Pemisahan Standar RFC 8259 vs Kebijakan Nexa**: RFC 8259 Bagian 4 menyatakan bahwa nama anggota objek dalam JSON "SHOULD be unique", tetapi tidak mewajibkan penolakan mutlak oleh setiap parser umum. Penolakan duplikasi kunci pada Nexa adalah **Kebijakan Parser Ketat Nexa (Nexa Strict Parser Policy)**, bukan kewajiban mutlak RFC 8259.
- **Aturan Spesifikasi Parser Nexa**:
  - *Duplicate Keys Literal*: Jika dua kunci identik secara literal karakter (e.g. `{"title": "A", "title": "B"}`), parser menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Duplicate Keys via Decoded Unicode Escape*: Jika dua kunci identik setelah karakter escape Unicode didekode (e.g. `{"\u0074itle": "A", "title": "B"}`), parser mendecode escape sebelum memeriksa keunikan kunci dan menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Malformed Escape Syntax*: Jika urutan escape salah secara sintaksis (e.g. `\u123z`, escape terpotong `\u12`, atau lone surrogates `\uD800` tanpa pasangan legal), parser menolak dengan **`ERR_MANIFEST_MALFORMED`**.
- **Pemisahan Parser vs Serializer JCS**: Strict Parser (B-01, AC-05) bertugas pada tahap deserialisasi byte stream mentah. RFC 8785 JCS Serializer (B-02, AC-06) bertugas pada tahap serialisasi kanonisasi deterministik (pengurutan kunci UTF-16, format bilangan tanpa $-0$, minifikasi whitespace).

#### 6.7 Rincian NC-07: Batas Keamanan Ekstraksi Arsip ZIP Wrapper (Temuan 5, Spesifikasi Tambahan 3 & 4)
- Status Kontrak: **`PROPOSED SPECIFICATION`** (Menunggu keputusan formal Otoritas Arsitektur di bawah Blocker B-07).
- **Klarifikasi Acuan Standar Eksternal**:
  - Standar **PKWARE APPNOTE.TXT / ISO/IEC 21320-1** murni mendefinisikan struktur format arsip ZIP (central directory, local headers, data descriptors).
  - Standar **IETF RFC 1951** murni mendefinisikan format kompresi bitstream DEFLATE.
  - Standar-standar eksternal tersebut **TIDAK PERNAH** menetapkan batas kuota ukuran aplikasi Nexa (seperti 500 MB atau 4 GB), batasan 200 entri, atau rasio 10:1. Nilai-nilai numerik tersebut adalah usulan spesifikasi tingkat aplikasi Nexa (`PROPOSED SPECIFICATION`).
- **Prinsip Keamanan Normatif yang Disetujui (Baseline Invariants)**:
  - *Penolakan Format Corrupt*: Arsip ZIP yang rusak atau tidak sesuai spesifikasi layout ditolak fail-closed dengan `ERR_ZIP_INVALID` (diverifikasi dalam kode baseline `container.go#L112`).
  - *Penahanan Filesystem (Safe-Open)*: Upaya path traversal (`../`) atau manipulasi symlink ditolak fail-closed dengan `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` (NC-12).
  - *Bijeksi 1:1*: Setiap berkas reguler `.nx` di dalam ZIP wajib terdaftar dalam `tracks[]` manifest, dan setiap track di manifest wajib ada di dalam ZIP. Ketidakcocokan memicu `ERR_ZIP_ENTRY_MISMATCH`.
  - *Lingkup Perlindungan*: Seluruh batas kuota dan ekstraksi diterapkan **EKSKLUSIF PADA PEMBUNGKUS ARSIP DISTRIBUSI ZIP**, dan **DILARANG KERAS** diperluas atau diterapkan pada ukuran kontainer audio individual `.nx` mandiri.
- **Rincian Usulan Batas Ekstraksi Pembungkus ZIP (Proposed Specification B-07)**:
  - *Usulan Struktur Flat & Penolakan Entri Direktori*: Arsip pembungkus ZIP diusulkan berstruktur flat pada root direktori. Ditemukannya entri direktori (entry name berakhiran `/` atau bertipe folder) diusulkan ditolak fail-closed dengan `ERR_ZIP_INVALID`.
  - *Usulan Ukuran Terkompresi Maksimum*: Diusulkan batas maksimum 500 MB (desimal: $500 \times 10^6 = 500.000.000$ bytes fail-closed). Pelanggaran diusulkan memicu `ERR_ZIP_QUOTA_EXCEEDED`.
  - *Usulan Ukuran Dekompresi Maksimum*: Diusulkan batas akumulasi ekstraksi 4 GB (desimal: $4 \times 10^9 = 4.000.000.000$ bytes fail-closed). Pelanggaran diusulkan memicu `ERR_ZIP_QUOTA_EXCEEDED`.
  - *Usulan Jumlah Entri Maksimum*: Diusulkan kuota 200 entri total di central directory header (1 manifest + $\le 199$ trek audio). Pelanggaran diusulkan memicu `ERR_ZIP_QUOTA_EXCEEDED`.
  - *Usulan Rasio Kompresi 10:1*:
    - Diusulkan dievaluasi pada dua tingkat (per-entri untuk uncompressed $> 1\text{ MB}$ dan global agregat uncompressed kumulatif $> 1\text{ MB}$).
    - Penanganan `compressed == 0` saat uncompressed $> 0$ diusulkan ditolak fail-closed dengan `ERR_ZIP_BOMB_DETECTED` (infinite ratio).
    - Pelanggaran rasio kompresi 10:1 diusulkan memicu `ERR_ZIP_BOMB_DETECTED`.

#### 6.8 Rincian NC-08: Batas Atomisitas Transaksi Marketplace & Ketiadaan 2PC (Temuan 6)
- Transaksi database lokal PostgreSQL menggunakan advisory lock `pg_advisory_xact_lock(hashtext(user_id || ':' || album_id))` untuk mutual exclusion.
- **Batas Atomisitas**:
  1. *Jaminan Lokal*: Advisory lock dan blok transaksi SQL (`BEGIN ... COMMIT / ROLLBACK`) menjamin bahwa mutasi lokal (child acquisitions dan entitlements) dibatalkan secara bersih tanpa residu baris parsial jika terjadi kegagalan lokal. Kegagalan mutasi lokal sebelum commit melempar **`ERR_TRANSACTION_FAILED`**.
  2. *Ketiadaan Jaminan Terdistribusi & Larangan Janji Rollback Pasca-Commit*: Panggilan HTTP eksternal ke Sprint 12 License Daemon (`marketplace/server.js#L170-L205`) TIDAK memiliki Two-Phase Commit (2PC) maupun endpoint kompensasi otomatis. Jika transaksi database lokal telah di-commit, transaksi tersebut **TIDAK DAPAT** di-rollback oleh transaksi SQL yang sama. Jika License Daemon gagal pasca-commit DB lokal atau mengalami network timeout, mutasi DB lokal di-rollback HANYA jika kegagalan terjadi di dalam blok transaksi sebelum commit; namun efek samping eksternal pada daemon tetap tidak terkompensasi. Kegagalan ini melempar **`ERR_LICENSE_DAEMON_COMMUNICATION`**.
  3. *Kendala Zero-DDL*: Skema database PostgreSQL beku (`schema.postgres.sql`) melarang penambahan kolom foreign key baru atau tabel outbox terdistribusi.
- **Status Arsitektur**: Selama gap ketiadaan 2PC dan batasan Zero-DDL belum diselesaikan oleh otoritas arsitektur, NC-08 berstatus **`BLOCKED`** di bawah blocker B-04 / CONF-03.

#### 6.9 Rincian NC-09: Pemetaan Delapan Objek Kriptografis / Hash Diskrit (Temuan 1, Temuan 8, Bagian 5.3)
Dokumen ini memisahkan secara formal delapan objek kriptografis diskret (3 tanda tangan digital Ed25519 dan 5 nilai hash SHA-256) agar tidak terjadi tumpang tindih penanganan error atau substitusi nilai hash yang keliru:
1. **Album Signer Signature (Ed25519)**: Tanda tangan digital Album Signer atas byte kanonikal UTF-8 payload manifest `album_manifest.json` (NC-02 $\rightarrow$ AC-03, terblokir B-08). Input: byte kanonikal JCS manifest (field signature dikecualikan). Nilai pembanding: verifikasi Ed25519 terhadap `album_signer_public_key`. Error: `ERR_MANIFEST_SIGNATURE_INVALID`.
2. **Container Packaging Signature (Ed25519)**: Tanda tangan digital Container Creator atas byte packaging kontainer individual `.nx` (NC-06 $\rightarrow$ AC-04). Input: byte packaging kontainer `.nx`. Nilai pembanding: verifikasi Ed25519 terhadap `creator_public_key`. Error: `ERR_CONTAINER_SIGNATURE_INVALID`.
3. **Genesis Certificate Signature (Ed25519)**: Tanda tangan digital Genesis Creator atas payload sertifikat genesis track audio individual (`sdk.ts#L205-L235`, NC-05 $\rightarrow$ AC-10). Input: payload sertifikat genesis. Nilai pembanding: verifikasi Ed25519 terhadap `GENESIS_PUBLIC_KEY`. Error: penolakan binding fail-closed (`canPlay: false`; status kode error kanonikal: unresolved in baseline taxonomy pending architecture definition).
4. **Audio Track Binary Payload Hash (SHA-256)**: SHA-256 atas data audio mentah (bitstream audio) di dalam kontainer `.nx` (NC-05/09 $\rightarrow$ AC-09). Input: bitstream audio mentah. Nilai pembanding: digest `audio_sha256` pada manifest dan sertifikat genesis. Error: `ERR_CONTAINER_HASH_MISMATCH`.
5. **Canonical Album Manifest Hash (SHA-256)**: SHA-256 atas byte stream kanonikal RFC 8785 JCS manifest (NC-02/09 $\rightarrow$ AC-03). Input: byte kanonikal UTF-8 manifest hasil serialisasi JCS tanpa field signature.
6. **Container Packaging Hash (SHA-256)**: SHA-256 atas struktur packaging kontainer `.nx` lengkap (NC-06 $\rightarrow$ AC-04, AC-12). Input: byte kontainer `.nx` utuh.
7. **Genesis Certificate Hash (SHA-256)**: SHA-256 atas data sertifikat genesis kanonikal (NC-05 $\rightarrow$ AC-10). Input: byte sertifikat genesis track.
8. **Distribution ZIP Archive Package Hash (SHA-256)**: SHA-256 atas arsip ZIP pembungkus distribusi fisik secara keseluruhan (`acquired_package_sha256` pada tabel database child acquisition — semantik kolom terblokir B-05, NC-09 $\rightarrow$ AC-16). Input: berkas fisik pembungkus ZIP album.

> **Aturan Isolasi Kriptografis Mutlak:** Dilarang keras mempertukarkan atau mensubstitusikan nilai hash antar-objek berbeda. Signature manifest TIDAK membuktikan integritas audio payload anggota secara otomatis tanpa verifikasi mandiri atas hash audio dan sertifikat genesis anggota masing-masing.

#### 6.11 Rincian NC-11: Aturan Fallback Offline Registry Terkendali (Spesifikasi Tambahan 7)
- Fallback ke offline cached registry certificate **HANYA DIIZINKAN** pada kondisi kegagalan transport/konektivitas fisik jaringan: `ECONNREFUSED` (koneksi ditolak), `ETIMEDOUT` (timeout), `ENOTFOUND` (DNS gagal).
- **Larangan Fallback (Fail-Closed)**: Jika respons diterima dari Registry tetapi tidak valid (HTTP 5xx, respons malformed, signature tidak valid, atau sertifikat revoked/expired), sistem **DILARANG KERAS** melakukan fallback ke cache. Sistem wajib melempar error fail-closed (`ERR_REGISTRY_SIGNATURE_INVALID` atau `ERR_REGISTRY_UNREACHABLE`).

#### 6.12 Rincian NC-12: Filesystem Safe-Open & Batasan POSIX (Temuan 4)
- **Status Kontrak**: **`OPEN / BLOCKED BY B-06`**.
- Akses berkas kontainer audio `.nx` wajib menggunakan invariant descriptor pasca-open (`O_RDONLY | O_NOFOLLOW` + `fstat`).
- **Batasan Kernel POSIX & Pengakuan Race Condition**: Diakui secara terbuka bahwa perlindungan absolut terhadap *concurrent ancestor rename* (TOCTOU race) tidak dapat dijamin secara matematis di userspace POSIX tanpa namespace/jail tingkat kernel. Menerapkan fail-closed (`canPlay: false`, `ERR_FILESYSTEM_CONTAINMENT_VIOLATION`) saat anomali descriptor terdeteksi adalah mitigasi defensif, **BUKAN** bukti bahwa seluruh race condition filesystem telah tereliminasi secara tuntas di userspace.

#### 6.14 Rincian NC-14: Rekonsiliasi Status NX Verify & Konflik Hierarki Agregat (Temuan 3, CONF-02)
- Status evaluasi NX Verify memisahkan Lapisan 1 (Signer Trust), Lapisan 2 (Member Integrity), dan Lapisan 3 (Aggregate Status).
- **Status Konflik (CONF-02)**: Penentuan aturan hierarki status agregat tetap berstatus **`CONFLICT — STOP AND CLARIFY`**. Dilarang menetapkan hierarki baru secara sepihak tanpa keputusan resmi Product Owner.

#### 6.15 Rincian NC-15: Taksonomi 20 Kode Error Kanonikal (Temuan 5, Temuan-Audit-04)
Tabel berikut merinci taksonomi tepat 20 kode error diskrit kanonikal yang terklasifikasi secara ketat berdasarkan tier sumbernya (termasuk kode mesin baseline `ERR_ZIP_INVALID` terverifikasi di kode Go). Kode dugaan `ERR_GENESIS_SIGNATURE_INVALID` dihilangkan karena tidak terdaftar dalam kode baseline maupun White Paper v5.6:

| Kode Error Diskret | Layer Penghasil | Kondisi Pemicu Diskret | Aksi Sistem | AC Penguji | Status Provenance Sumber |
|---|---|---|---|:---:|:---:|
| `ERR_MANIFEST_MISSING` | Manifest Parser | `album_manifest.json` tidak ditemukan di root ZIP | Fail-closed; tolak ekstraksi | AC-01 | Baseline Specification (WP v5.6) |
| `ERR_MANIFEST_MALFORMED` | Manifest Parser | Sintaksis JSON rusak, regex invalid, escape syntax fail | Fail-closed; tolak manifest | AC-01 | Baseline Specification (WP v5.6) |
| `ERR_MANIFEST_DUPLICATE_KEY` | Strict JSON Parser | Ditemukan duplikasi key literal atau via decoded escape | Fail-closed; hentikan parsing | AC-05 | Proposed Specification (B-01/NC-03) |
| `ERR_MANIFEST_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature manifest gagal | Fail-closed; tolak album | AC-03 | Baseline Specification (WP v5.6) |
| `ERR_ALBUM_SIGNER_UNKNOWN` | Trust Store | Signer public key tidak terdaftar di Registry | Sesuai keputusan PO B-09 | AC-07 | Proposed Specification (Pending PO) |
| `ERR_ALBUM_SIGNER_UNTRUSTED` | Trust Store | Signer public key masuk dalam revocation list | Fail-closed; blokir playback | AC-08 | Baseline Specification (WP v5.6) |
| `ERR_CONTAINER_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature container individual `.nx` gagal | Fail-closed; tandai trek corrupt | AC-04 | Baseline Specification (WP v5.6) |
| `ERR_CONTAINER_HASH_MISMATCH` | Integrity Engine | SHA-256 payload audio tidak cocok dengan manifest/cert | Fail-closed; tandai tampered | AC-09 | Baseline Specification (WP v5.6) |
| `ERR_ZIP_INVALID` | ZIP Extractor / Go Engine | Format ZIP corrupt/rusak, central dir fail, atau ada entri direktori | Fail-closed; tolak ekstraksi | AC-02, AC-13 | Baseline Verified in Code (`container.go#L112`) |
| `ERR_ZIP_QUOTA_EXCEEDED` | ZIP Wrapper Extractor | Ukuran ZIP > 500M, uncompressed > 4G, atau entri > 200 | Fail-closed; batalkan ekstrak | AC-13 | Proposed Specification (NC-07/B-07) |
| `ERR_ZIP_BOMB_DETECTED` | ZIP Wrapper Extractor | Rasio > 10:1 (uncomp > 1MB) atau compressed == 0 | Fail-closed; karantina arsip | AC-13 | Proposed Specification (NC-07/B-07) |
| `ERR_ZIP_ENTRY_MISMATCH` | Packaging Validator | Entri berkas reguler ZIP tidak cocok 1:1 dg manifest | Fail-closed; tolak kontainer | AC-02, AC-13 | Proposed Specification (NC-01/07) |
| `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | Filesystem Safe-Open | Path traversal (`../`), symlink bypass, TOCTOU | Fail-closed; tolak akses fd | AC-20, AC-21 | Baseline Specification (WP v5.6) |
| `ERR_PLAYBACK_UNAUTHORIZED` | JIT Authorizer | Tidak ada entitlement aktif / lisensi tidak valid | Fail-closed; tolak playback | AC-22 | Baseline Specification (WP v5.6) |
| `ERR_MARKETPLACE_REPLAY_DETECTED` | Transaction Engine | Transaksi dengan token/hash identik terdeteksi | Idempotent return state lama | AC-15 | Baseline Specification (WP v5.6) |
| `ERR_ID_COLLISION` | Identity Generator | Tabrakan string hash derivasi ID pada tabel DB | Fail-closed; log & abort | AC-27 | Proposed Specification (NC-16) |
| `ERR_TRANSACTION_FAILED` | Transaction Engine | Kegagalan eksekusi query multi-item DB lokal | Rollback transaksi lokal | AC-14 | Baseline Specification (WP v5.6) |
| `ERR_REGISTRY_UNREACHABLE` | Network / Trust Store | Registry offline dan tidak ada cache valid | Fail-closed; tolak verifikasi | AC-18, AC-19 | Baseline Specification (WP v5.6) |
| `ERR_REGISTRY_SIGNATURE_INVALID` | Trust Store | Signature respons Registry tidak valid | Fail-closed; tolak respons | AC-18, AC-19 | Baseline Specification (WP v5.6) |
| `ERR_LICENSE_DAEMON_COMMUNICATION` | Marketplace Server | Panggilan HTTP ke Sprint 12 License Daemon gagal | Fail-closed; rollback mutasi DB lokal uncommitted; efek samping daemon eksternal tidak terkompensasi (gap 2PC B-04 / CONF-03) | AC-14 | Baseline Specification (WP v5.6) |

> **Catatan Ketidakpastian Taksonomi Error & Kepatuhan Fail-Closed (R-02 / Stop-and-Clarify):**  
> 1. **Fail-Closed atas Kegagalan Genesis Certificate Signature**: Pada Tahap 5 otorisasi JIT player (§5.1) dan AC-10 (§8), kegagalan verifikasi tanda tangan digital Ed25519 Genesis Certificate diwajibkan secara tegas berperilaku **fail-closed** (`canPlay: false`).  
> 2. **Status Kode Error Spesifik**: Taksonomi 20 kode error kanonikal di atas tidak memuat konstanta `ERR_GENESIS_SIGNATURE_INVALID`. Pemetaan kode error kanonikal spesifik untuk kegagalan signature genesis berstatus **`UNRESOLVED IN BASELINE TAXONOMY (PENDING ARCHITECTURE DEFINITION)`**.  
> 3. **Larangan Fabrikasi Kode**: Programmer dilarang menambahkan kode buatan baru secara sepihak atau memetakan kegagalan signature genesis ke `ERR_ZIP_INVALID` / kode lain yang tidak relevan hanya demi mencocokkan jumlah tabel. Persyaratan fail-closed ditegakkan, sementara pemetaan kode error spesifiknya menunggu keputusan otoritatif Arsitektur.

#### 6.16 Rincian NC-16: Derivasi Matematis Identifier Deterministik (Spesifikasi Tambahan 5)
Derivasi identifier transaksi album mengusulkan penggunaan format SHA-256 terpotong (*truncated SHA-256*) sepanjang 32 karakter heksadesimal (`[PROPOSED SPECIFICATION]`):
1. **Child Acquisition ID**:
   $$\text{child\_acq\_id} = \text{"acq\_" } || \text{SHA256}(\text{parent\_acq\_id } || \text{ ":" } || \text{track\_id})[0..31]$$
   - Panjang string: $4 + 32 = 36$ karakter. Kapasitas kolom DDL aktif: `VARCHAR(128)`. Margin aman: $128 - 36 = 92$ karakter.
2. **Child Entitlement ID**:
   $$\text{child\_ent\_id} = \text{"ent\_" } || \text{SHA256}(\text{parent\_acq\_id } || \text{ ":" } || \text{track\_id } || \text{ ":ent"})[0..31]$$
   - Panjang string: $4 + 32 = 36$ karakter. Kapasitas kolom DDL aktif: `VARCHAR(128)`. Margin aman: $128 - 36 = 92$ karakter.
3. **Provider Identifier**:
   $$\text{provider\_id} = \text{"prv\_" } || \text{SHA256}(\text{album\_signer\_pubkey})[0..31]$$
   - Panjang string: $4 + 32 = 36$ karakter. Kapasitas kolom DDL aktif: `VARCHAR(64)`. Margin aman: $64 - 36 = 28$ karakter.

> **Batasan Bukti Matematis (Spesifikasi Tambahan 5):** Pemenuhan panjang string terhadap batas kolom skema DDL membuktikan kesesuaian kapasitas penyimpanan fisik, tetapi **BUKAN** bukti matematis ketiadaan tabrakan hash (*collision-free*). Penanganan tabrakan ID derivasi (`ERR_ID_COLLISION`) wajib dipisahkan dari replay transaksi normal (`ERR_MARKETPLACE_REPLAY_DETECTED`).

---

## 7. BLOCKER REGISTER (B-01..B-09) DAN FINDING REGISTER (F-01..F-15)

### 7.1 Blocker Register (B-01 sampai B-09)
Tabel blocker register memisahkan secara eksplisit status spesifikasi, implementasi, dan status blocker:

| ID | Deskripsi Blocker Historis | Status Spesifikasi | Status Implementasi | Status Blocker | Akar Penyebab & Dampak Arsitektur | Syarat Penutupan Sah |
|:---:|:---|:---:|:---:|:---:|:---|:---|
| **B-01** | Parser `JSON.parse` standar menimpa duplicate keys dan parser naif gagal tangani Unicode escape. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED (IMPLEMENTATION MODULE PENDING)` | Didekomposisi: duplicate keys (literal/unescaped) vs malformed syntax escape. Spesifikasi teknis telah lengkap; menunggu penulisan implementasi modul parser. | Implementasi strict byte-level JSON parser mandiri yang lolos AC-05. |
| **B-02** | Serializer ad-hoc tidak mengurutkan UTF-16 code units dan salah menangani format $-0$. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED (IMPLEMENTATION MODULE PENDING)` | Ketiadaan serializer canonical RFC 8785 JCS memicu invalid signature pada manifest JSON. Spesifikasi teknis telah lengkap; menunggu penulisan implementasi modul serializer. | Serializer RFC 8785 JCS teruji lolos seluruh vektor uji AC-06. |
| **B-03** | Ekstraktor ZIP standar rentan path traversal dan zip-bomb di userspace POSIX. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Ketiadaan validasi kuota ekstraksi dan invariant post-open descriptor. | Implementasi Safe-Open terverifikasi lolos uji AC-13, AC-20, AC-21. |
| **B-04** | Ketiadaan Two-Phase Commit (2PC) dan Batasan Zero-DDL pada Transaksi Marketplace. | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED` | Panggilan HTTP eksternal ke License Daemon Sprint 12 tanpa 2PC; skema DDL beku melarang penambahan kolom FK (CONF-03). | Keputusan Otoritas Arsitektur mengenai model atomisitas transaksi multi-item. |
| **B-05** | Ketidakpastian Semantik Kolom Database `acquired_package_sha256` untuk Child Row. | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED` | Skema DDL hanya memuat kolom package hash tunggal; semantik hash child item belum terdefinisi di DB. | Keputusan Data Architect mengenai pemetaan kolom child acquisition. |
| **B-06** | Kerentanan Race Condition Filesystem (TOCTOU) pada Akses Kontainer Desktop. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Batasan kernel POSIX userspace terhadap concurrent ancestor directory rename. | Penerapan invariant fail-closed (`canPlay: false`) saat anomali descriptor terdeteksi. |
| **B-07** | Batas Ukuran dan Kuota Ekstraksi Arsip Pembungkus ZIP (Nilai Numerik Masih Berstatus Usulan). | `PROPOSED SPECIFICATION` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY PROPOSED SPEC` | Nilai numerik kuota ZIP (500M / 4G / 200 entri / flat / 10:1) berstatus usulan spesifikasi teknis di bawah NC-07 dan belum dibekukan dalam White Paper v5.6. Pembatasan kuota ini berlaku eksklusif pada pembungkus ZIP, bukan kontainer anggota `.nx`. | Keputusan resmi Otoritas Arsitektur membekukan batas kuota numerik pembungkus ZIP. |
| **B-08** | Circular Dependency Kriptografi Tanda Tangan Manifest & JCS. | `BLOCKED — REQ CLARIFICATION` | `NOT IMPLEMENTED` | `BLOCKED` | `album_signer_signature` berada di dalam payload yang dikanonisasi JCS; batas payload belum ditetapkan. | Keputusan Otoritas Arsitektur / PO mengenai desain envelope/field exclusion. |
| **B-09** | Ketiadaan Kebijakan Otorisasi Product Owner atas Album Signer `UNKNOWN`. | `SPECIFIED` | `NOT IMPLEMENTED` | `PO DECISION REQUIRED` | Ambiguitas kebijakan bisnis apakah album dari signer tidak terdaftar boleh diputar lokal (CONF-01). | Keputusan tertulis resmi diterbitkan oleh Product Owner (Roadmap v4.8). |

---

### 7.2 Finding Register (F-01 sampai F-15) — Rekonsiliasi Historis Penuh (Bagian 4.3)

> **PERINGATAN GOVERNANCE (Bagian 4.3 Mandat Audit):**  
> Seluruh 15 temuan teknis historis F-01 sampai F-15 direkonsiliasi secara penuh sesuai definisi asalnya. Label `SPECIFIED IN PLAN` menyatakan bahwa masalah telah dirumuskan dalam spesifikasi dokumen ini. Label ini **SECARA TEGAS BUKAN** klaim bahwa kode telah diimplementasikan (`NOT IMPLEMENTED`), **BUKAN** bukti bahwa pengujian runtime telah lulus, dan **BUKAN** penutupan blocker (Blocker tetap `OPEN / BLOCKED`).

| ID Finding | Deskripsi Makna Historis yang Wajib Dipertahankan (Bagian 4.3) | Status Analisis Dokumen (Bukan Bukti Implementasi / Blocker Tidak Ditutup) | Rujukan Bagian & Dasar Fakta |
|:---:|:---|:---:|:---|
| **F-01** | **Filesystem containment dan klasifikasi UNTRUSTED**: Pembatasan akses kontainer audio pada direktori kanonikal terisolasi dan penolakan symlink traversal. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Invariant Safe-Open; AC-20, AC-21. |
| **F-02** | **Skema Genesis dan urutan validasi**: Pemisahan urutan verifikasi sertifikat genesis individual dari otorisasi album level atas. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Urutan Validasi JIT 8-tahap (Tahap 5); AC-10. |
| **F-03** | **Binding Creator**: Penegakan Invariant 3-Way Identity Binding ($ownCertPubKey \equiv containerSigKey \equiv genesisPubKey$). | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1, §6.5 Invariant Identitas Kriptografis; AC-04, AC-10. |
| **F-04** | **Waktu dan skema Registry sidecar**: Validasi waktu sertifikat, cache TTL, dan aturan fallback offline terisolasi dari transport error. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.11 Aturan Cache Offline Registry; AC-18, AC-19. |
| **F-05** | **Perbedaan klasifikasi kriptografis `INVALID` dan kondisi yang tidak dapat dipastikan**: Memisahkan signature fail-closed dari status `UNKNOWN`. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.15 Taksonomi Error; AC-07, AC-08, AC-18, AC-26. |
| **F-06** | **Kontrak aktual `container.Unpack`**: Pustaka packaging memvalidasi kontainer `.nx` mandiri hasil ekstraksi arsip pembungkus ZIP. | `REPOSITORY-VERIFIED (CODE ONLY)` | `internal/container/container.go#L110-L160`; E-02; AC-11, AC-12. |
| **F-07** | **Schema manifest internal**: Skema JSON manifest album mencakup 13 properti wajib dengan batasan tipe ketat (Draft 7). | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Skema Manifest JSON Lengkap; AC-01. |
| **F-08** | **Penanganan exception pada verifikasi signature**: Exception format kunci/buffer pada modul kriptografi ditangkap dan dipetakan ke kode error diskrit. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | `sdk/typescript/src/crypto.ts#L45`; §6.15; AC-26. |
| **F-09** | **Validasi nama file**: Penegakan pola penamaan file trek `.nx` strictly flat (`^[a-zA-Z0-9_.-]+\.nx$`) dan larangan direktori. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Regex Filename; AC-02, AC-20. |
| **F-10** | **Penggunaan `assetId`/`asset_id` anggota yang benar dalam laporan dan entitlement**: Formula ID deterministik derivasi PostgreSQL aktif. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.16 Derivasi Matematis Identifier; AC-27. |
| **F-11** | **Batas klaim filesystem containment**: Mitigasi symlink traversal pasca-open dan pengakuan keterbatasan userspace POSIX. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Safe-Open Invariant; AC-20, AC-21. |
| **F-12** | **Batas descriptor dan primitive filesystem**: Evaluasi descriptor file pasca-open dan pengakuan batas race condition POSIX userspace. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Batasan Kernel POSIX; AC-21, B-06. |
| **F-13** | **Bukti AC-03/AC-04 tidak boleh diklaim membuktikan hal di luar signature manifest**: Isolasi batas pengujian unit vs agregat album. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §8 (AC-03, AC-04); batas bukti E-02 dan E-06. |
| **F-14** | **Bukti AC-05/AC-08/AC-09 tidak boleh digeneralisasi menjadi bukti E2E**: Bukti inspeksi kode lokal Linux server bukan bukti runtime mobile. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §4.4 Evidence Ledger E-01..E-09; G-02. |
| **F-15** | **Klaim zero-exposure tidak boleh dibuat tanpa bukti arsitektur yang memadai**: Pengakuan terbuka atas gap 2PC dan batasan Zero-DDL Marketplace. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.8 Batas Atomisitas Transaksi Marketplace; B-04 / CONF-03. |

---

## 8. ACCEPTANCE CRITERIA REGISTER (AC-01 SAMPAI AC-27)

Tabel berikut merinci seluruh 27 Acceptance Criteria (AC-01 sampai AC-27) secara lengkap dan terpetakan status dependensinya:

| ID | Kontrak Dasar | Sumber Otoritatif | Skenario Uji / Kondisi Masukan | Expected Result / Kriteria Keberhasilan | Status Kesiapan Uji | Dependensi Blocker / Governance |
|:---:|:---:|:---|:---|:---|:---:|:---:|
| **AC-01** | NC-01 | White Paper v5.6 §Manifest; RFC 8259 | Manifest tanpa properti wajib atau memuat properti tambahan asing | Menolak manifest (`ERR_MANIFEST_MALFORMED`); jika kebijakan permisif disahkan PO: abaikan properti asing. | `[PO DECISION REQUIRED]` | Keputusan PO atas kebijakan unknown fields |
| **AC-02** | NC-01/07| White Paper v5.6; APPNOTE.TXT | File `.nx` dalam ZIP tidak cocok 1:1, atau ZIP corrupt / ada entri direktori | Ekstraksi ditolak fail-closed dengan error `ERR_ZIP_ENTRY_MISMATCH` atau `ERR_ZIP_INVALID`. | `[TEST-PLANNED]` | Tidak ada |
| **AC-03** | NC-02 | IETF RFC 8032; `crypto.ts` | Signature manifest 128-hex tidak valid atau payload dimodifikasi | Verifikasi tanda tangan manifest gagal (`ERR_MANIFEST_SIGNATURE_INVALID`). | `[BLOCKED BY ARCHITECTURE]` | B-08 (Circular Dependency Manifest Sig) |
| **AC-04** | NC-06 | IETF RFC 8032; `container.go` | Signature kontainer `.nx` anggota album dimodifikasi | Verifikasi tanda tangan kontainer `.nx` gagal (`ERR_CONTAINER_SIGNATURE_INVALID`). | `[TEST-PLANNED]` | Baseline Frozen (PE-01) |
| **AC-05** | NC-03 | WP v5.6 §Parsers; Nexa Policy | Payload manifest memuat duplicate keys literal atau via decoded Unicode escape | Parser menolak payload fail-closed dengan error `ERR_MANIFEST_DUPLICATE_KEY`. | `[TEST-PLANNED — BLOCKED BY B-01]` | B-01 (Strict Parser Engine - Implementation Module Pending) |
| **AC-06** | NC-03 | IETF RFC 8785 | Vektor uji kanonisasi RFC 8785 (urutan kunci UTF-16, $-0$, whitespace) | Serializer menghasilkan byte kanonikal identik 100% dengan test vector resmi. | `[TEST-PLANNED — BLOCKED BY B-02]` | B-02 (JCS Serializer Engine - Implementation Module Pending) |
| **AC-07** | NC-04 | Roadmap v4.8; B-09 | Album ditandatangani oleh signer dengan status `UNKNOWN` di Registry | Perilaku mengikuti keputusan resmi tertulis Product Owner (Opsi A, B, atau C). | `[PO DECISION REQUIRED]` | B-09 / NC-04 / CONF-01 |
| **AC-08** | NC-04 | White Paper v5.6 §Registry | Signer public key tercatat dalam daftar pencabutan (revocation list) | Verifikasi ditolak fail-closed dengan `ERR_ALBUM_SIGNER_UNTRUSTED`. | `[TEST-PLANNED]` | Tidak ada |
| **AC-09** | NC-05 | White Paper v5.6 §Genesis | Hash audio payload `.nx` tidak cocok dengan digest di sertifikat/manifest | Verifikasi integritas payload gagal (`ERR_CONTAINER_HASH_MISMATCH`). | `[TEST-PLANNED — SPEC READY]` | Independen B-05 |
| **AC-10** | NC-05 | White Paper v5.6 §Genesis; `sdk.ts` | Signature Genesis Certificate invalid / issuer genesis mismatch | Verifikasi binding anggota gagal fail-closed (`canPlay: false`; status kode error kanonikal: unresolved in baseline taxonomy pending architecture definition). | `[TEST-PLANNED]` | Baseline Verified (PE-01) |
| **AC-11** | NC-06 | White Paper v5.6 §Container | Ekstraksi kontainer audio mandiri dari arsip ZIP | File terekstrak utuh di storage tanpa merusak byte kanonikal container. | `[TEST-PLANNED]` | Tidak ada |
| **AC-12** | NC-06 | White Paper v5.6 §Container | Pustaka packaging memvalidasi struktur kontainer hasil ekstraksi | Validasi packaging lulus seluruh invariant integritas baseline PE-01. | `[TEST-PLANNED]` | Tidak ada |
| **AC-13** | NC-07 | Proposal B-07 (Acuan Format: APPNOTE; RFC 1951) | Arsip pembungkus ZIP melebihi usulan batas kuota B-07 (> 500M, uncomp > 4G, entri > 200, ada entri direktori, rasio > 10:1) | Ekstraksi wrapper dibatalkan fail-closed (`ERR_ZIP_QUOTA_EXCEEDED` / `ERR_ZIP_BOMB_DETECTED` / `ERR_ZIP_INVALID`). | `[TEST-PLANNED — EXECUTION BLOCKED BY PROPOSED SPEC]` | B-07 (Batas Kuota ZIP Wrapper Masih Berstatus Usulan) |
| **AC-14** | NC-08 | `schema.postgres.sql#L63`; B-04 | Transaksi multi-item Marketplace gagal di tengah eksekusi sebelum commit | Rollback transaksi lokal membatalkan mutasi tanpa baris parsial yatim di DB lokal. | `[BLOCKED BY ARCHITECTURE]` | B-04 / NC-08 / CONF-03 |
| **AC-15** | NC-08 | `server.js#L170`; NC-08 | Request settlement pembelian dikirim berulang dengan token identik | Marketplace mengenali replay dan mengembalikan state transaksi lama secara idempoten. | `[BLOCKED BY ARCHITECTURE]` | B-04 / NC-08 / CONF-03 |
| **AC-16** | NC-09 | `schema.postgres.sql#L63`; B-05 | Penyimpanan baris child acquisition dan verifikasi hash paket | Penyimpanan data child acquisition mematuhi semantik kolom hash database yang sah. | `[BLOCKED BY ARCHITECTURE]` | B-05 / NC-09 (Semantik Hash DB) |
| **AC-17** | NC-10 | `schema.postgres.sql#L63-L115` | Operasi transaksi dan penyimpanan album dieksekusi | Skema database PostgreSQL aktif tidak termutasi (Zero-DDL terpenuhi 100%). | `[TEST-PLANNED]` | Skema DDL Aktif (Independen B-04) |
| **AC-18** | NC-11 | White Paper v5.6 §Registry | Koneksi ke remote Registry aktif dan respons valid | Verifikasi sertifikat dan public key signer menggunakan data otoritatif remote. | `[TEST-PLANNED]` | Tidak ada |
| **AC-19** | NC-11 | White Paper v5.6 §Registry | Jaringan transport terputus (ECONNREFUSED/timeout); cache lokal valid | Fallback ke cache offline; respons HTTP 5xx/bad sig melempar fail-closed. | `[TEST-PLANNED]` | Tidak ada |
| **AC-20** | NC-12 | POSIX.1-2017; `fs_safe.ts` | File `.nx` berada di luar root storage atau symlink melintasi direktori | Akses ditolak fail-closed (`ERR_FILESYSTEM_CONTAINMENT_VIOLATION`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-21** | NC-12 | POSIX.1-2017; Standar POSIX | Upaya pembukaan berkas dengan manipulasi symlink/path traversal | Pemeriksaan descriptor pasca-open gagal; melempar fail-closed (`canPlay: false`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-22** | NC-13 | White Paper v5.6 §JIT Player | Otorisasi pemutaran trek audio album dieksekusi | Otorisasi JIT memvalidasi lisensi & hash sebelum mendaftarkan buffer trek aktif. | `[TEST-PLANNED]` | Tidak ada |
| **AC-23** | NC-13 | White Paper v5.6 §JIT Player | Pengguna berpindah trek audio dalam album | Otorisasi JIT dieksekusi ulang secara independen per trek tanpa otorisasi massal. | `[TEST-PLANNED]` | Tidak ada |
| **AC-24** | NC-13 | White Paper v5.6 §JIT Player | Integritas satu trek dalam antrean album rusak | Trek rusak gagal diputar; pemutaran trek valid lainnya tidak terganggu. | `[TEST-PLANNED]` | Tidak ada |
| **AC-25** | NC-14 | White Paper v5.6 §Verify; CONF-02 | Verifikasi album dengan anggota valid dan status campuran | Evaluasi status agregat mengikuti aturan resmi yang diputuskan Product Owner / Arsitektur. | `[PO DECISION REQUIRED]` | CONF-02 (Hierarki Status Agregat) |
| **AC-26** | NC-15 | Error Taxonomy Spec; NC-15 | Skenario kegagalan sistematis di seluruh alur eksekusi | Sistem melempar kode error diskrit kanonikal 1:1 sesuai taksonomi 20 error code. | `[TEST-PLANNED]` | Tidak ada |
| **AC-27** | NC-16 | `schema.postgres.sql#L63-L115` | Uji kesesuaian panjang formula ID derivasi terhadap skema DDL | Panjang string child acq $\le 128$, ent $\le 128$, provider $\le 64$ karakter. | `[TEST-PLANNED]` | DDL Skema Aktif (Bukan Bukti Unik)|

---

## 9. TRACEABILITY MATRIX DUA ARAH: NC → AC → SUMBER → BUKTI

Matriks berikut mendokumentasikan keterlacakan dua arah (*Forward & Reverse Traceability*) dengan struktur tabel markdown valid dan rujukan dependensi yang realistis tanpa klaim semu:

| ID NC | ID AC Penguji | Sumber Otoritatif | Bukti Pendukung / Lokasi Kode | Status Kesiapan AC | Status Blocker / Keputusan |
|:---:|:---:|:---|:---|:---:|:---:|
| **NC-01** | AC-01, AC-02 | White Paper v5.6 §Manifest; RFC 8259 | §5.1 Skema Manifest; E-02 | AC-01 `[PO DECISION REQUIRED]`; AC-02 `[TEST-PLANNED]` | Pending Konfirmasi PO |
| **NC-02** | AC-03 | IETF RFC 8032; `crypto.ts` | `sdk/typescript/src/crypto.ts#L45`; E-06 | `[BLOCKED BY ARCHITECTURE]` | B-08 (Circular Dependency) |
| **NC-03** | AC-05, AC-06 | White Paper v5.6 §Parsers; IETF RFC 8785 | RFC 8785 Test Vectors TV-01..TV-08 | AC-05 `[BLOCKED B-01]`; AC-06 `[BLOCKED B-02]` | B-01, B-02 (Strict Parser & JCS - Implementation Modules Pending) |
| **NC-04** | AC-07, AC-08 | Roadmap v4.8; White Paper v5.6 §Registry | Roadmap v4.8 §Trust Model | AC-07 `[PO DECISION REQUIRED]`; AC-08 `[TEST-PLANNED]` | B-09 / CONF-01 |
| **NC-05** | AC-09, AC-10 | White Paper v5.6 §Genesis; `sdk.ts` | `sdk/typescript/src/sdk.ts#L205`; E-01 | `[TEST-PLANNED — SPEC READY]` | Independen B-05 |
| **NC-06** | AC-04, AC-11, AC-12 | White Paper v5.6 §Container; `container.go` | `internal/container/container.go#L110`; E-02 | `[TEST-PLANNED]` | Baseline Frozen (PE-01) |
| **NC-07** | AC-02, AC-13 | Proposal B-07 (Acuan Format: APPNOTE; RFC 1951) | §6.7 Batas Keamanan Ekstraksi Arsip ZIP Wrapper (Nilai Kuota Berstatus Usulan B-07) | `[TEST-PLANNED — EXECUTION BLOCKED BY PROPOSED SPEC]` | B-07 (Menunggu Keputusan Arsitektur Pembekuan Batas Kuota ZIP) |
| **NC-08** | AC-14, AC-15 | `schema.postgres.sql#L63`; `server.js` | `marketplace/server.js#L170`; E-04 | `[BLOCKED BY ARCHITECTURE]` | B-04 / CONF-03 |
| **NC-09** | AC-16 | `schema.postgres.sql#L63`; B-05 | `marketplace/db/schema.postgres.sql#L63`; E-03 | `[BLOCKED BY ARCHITECTURE]` | B-05 (Semantik Hash DB); Hash audio diuji via NC-05/AC-09 |
| **NC-10** | AC-17 | `schema.postgres.sql#L63-L115` | `marketplace/db/schema.postgres.sql#L63`; E-03 | `[TEST-PLANNED]` | DDL Skema Aktif (Independen B-04)|
| **NC-11** | AC-18, AC-19 | White Paper v5.6 §Registry | White Paper v5.6 §Offline Fallback | `[TEST-PLANNED]` | Tidak ada |
| **NC-12** | AC-20, AC-21 | POSIX.1-2017; `fs_safe.ts` | `sdk/typescript/src/fs_safe.ts#L30`; E-07 | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Open / Blocked) |
| **NC-13** | AC-22, AC-23, AC-24 | White Paper v5.6 §JIT Player; `main.js` | `player-desktop/main.js#L182, L541`; E-05 | `[TEST-PLANNED]` | Tidak ada |
| **NC-14** | AC-25 | White Paper v5.6 §Verify; CONF-02 | §5.3 Tiga Lapisan Status Verify | `[PO DECISION REQUIRED]` | CONF-02 |
| **NC-15** | AC-26 | Error Taxonomy Spec; NC-15 | §6.15 Taksonomi 20 Kode Error Kanonikal | `[TEST-PLANNED]` | Tidak ada |
| **NC-16** | AC-27 | `schema.postgres.sql#L63-L115` | §6.16 Derivasi Matematis Identifier | `[TEST-PLANNED]` | DDL Skema Aktif |

---

## 10. KEPUTUSAN PRODUCT OWNER YANG MASIH DIPERLUKAN

### 10.1 Kebijakan Album Signer `UNKNOWN` (NC-04, B-09, CONF-01)
Keputusan resmi mengenai perilaku sistem terhadap signer `UNKNOWN` merupakan kewenangan eksklusif Product Owner:
- **Opsi A (Strict Fail-Closed)**: Album ditolak total dari pemutaran. Melempar `ERR_ALBUM_SIGNER_UNKNOWN`. Verifikasi integritas fisik berkas `.nx` anggota tetap dapat dijalankan untuk diagnostik pelaporan.
- **Opsi B (Permissive Warning / Local Playback Allowed)**: Album diizinkan diputar secara lokal dengan status peringatan UI `SIGNER_UNKNOWN_UNVERIFIED`.
- **Opsi C (Network-Gated Verification)**: Pemutaran lokal diblokir sementara hingga verifikasi latar belakang berhasil mengonfirmasi signer.

> **Status Tata Kelola:** Opsi A, B, dan C murni usulan desain non-normatif. Dokumen mengunci status **`PO DECISION REQUIRED`** pada AC-07 (B-09 / CONF-01: Kebijakan Signer UNKNOWN) hingga keputusan tertulis resmi diterbitkan oleh Product Owner. Evaluasi agregat NX Verify pada AC-25 dipetakan secara eksklusif ke CONF-02.

---

## 11. KONFLIK MATERIAL DAN STOP-AND-CLARIFY

Tiga konflik material berikut tetap dipertahankan terbuka secara transparan dan menjadi penghalang kelulusan Gate A:

```
+----------------------------------------------------------------------------------------------------+
|                         REGISTER KONFLIK MATERIAL TERBUKA (CONF-01 s.d. CONF-03)                   |
+---------+----------------------------------+-----------------------------+-------------------------+
| ID      | Deskripsi Konflik Material       | Pihak Berwenang             | Dampak Teknis           |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-01 | Kebijakan Otorisasi Album Signer | Product Owner               | AC-07 tertahan status   |
|         | UNKNOWN (Roadmap v4.8 vs usulan) | (PO Mandate)                | PO DECISION REQUIRED    |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-02 | Hierarki Status Agregat NX Verify| Product Owner / Arsitektur  | NC-14 dan AC-25 tertahan|
|         | (Status asli vs status tambahan) | (Architecture Board)        | CONFLICT-STOP & CLARIFY |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-03 | Gap Transaksi Terdistribusi non- | Otoritas Arsitektur / DBA   | NC-08, AC-14, dan AC-15 |
|         | 2PC vs Kendala Skema Zero-DDL    | (Architecture & Database)   | tertahan status BLOCKED |
+---------+----------------------------------+-----------------------------+-------------------------+
```

---

## 12. PRESERVATION GATE EVALUATION DAN GERBANG PENERIMAAN

### 12.1 Evaluasi Tujuh Dimensi Preservation Gate
Evaluasi 7 dimensi Preservation Gate disajikan secara objektif dengan membedakan dimensi yang lulus berdasarkan inspeksi statis terbatas dari dimensi yang masih tertahan oleh blocker arsitektur atau keputusan PO:

| Dimensi Preservasi | Aspek yang Dievaluasi | Status Evaluasi Audit (Sesuai §2.7) | Bukti Faktual & Batasan Pembuktian |
|---|---|:---:|---|
| **D-01 — Baseline / Repository** | Kebersihan repositori dan preservasi baseline Sprint 16. | `Belum dapat diverifikasi secara independen; bukti yang dilaporkan hanya mendukung klaim terbatas` | `git diff --name-only` hanya menguji tracked files; keberadaan 2 file untracked docs dan gitignored `evidence/` membatasi klaim. |
| **D-02 — Preservation PE-01 binary** | Kontrak biner single `.nx` kontainer tetap mandiri tanpa perubahan format. | `Bukti independen belum cukup` | Inspeksi statis kode `container.go` utuh, tetapi uji integritas biner runtime belum diverifikasi secara independen. |
| **D-03 — Database / Schema** | Kepatuhan mutlak Zero-DDL pada database marketplace. | `Kondisi database runtime belum terverifikasi secara independen` | Berkas `schema.postgres.sql` utuh; ketiadaan migrasi di database produksi live belum diverifikasi koneksi runtime. |
| **D-04 — Implementasi / Arsitektur** | Integritas struktur kontainer dan model Album ZIP independen. | `Desain bukan bukti implementasi atau pengujian runtime` | Spesifikasi arsitektur tiga tanda tangan memisahkan manifest, namun belum diimplementasikan di kode PE-02. |
| **D-05 — JIT Authorization** | NX Player otorisasi just-in-time per trek aktif tanpa otorisasi awal. | `Masih berupa kontrak/rancangan sampai dibuktikan pada runtime` | Rancangan 8-tahap JIT dan handler `nexa-playback` belum dibuktikan pada eksekusi runtime fisik player. |
| **D-06 — Keputusan Album Signer** | Kebijakan terhadap signer berstatus UNKNOWN (B-09 / CONF-01). | `BLOCKED / PENDING PO` | Keputusan tertulis resmi Product Owner belum diterbitkan; Opsi A/B/C tetap berstatus usulan non-normatif. |
| **D-07 — Konsistensi Internal Plan** | Ketiadaan kontradiksi internal antar-register dan spesifikasi. | `Belum lulus sampai temuan dan konflik yang relevan diselesaikan` | Blocker arsitektur (B-04, B-05, B-06, B-08) dan konflik (CONF-01, CONF-02, CONF-03) tetap terbuka secara transparan. |

**Kesimpulan Preservation Gate:**  
**`PARTIAL — CLAIMS OF BASELINE PRESERVATION ARE LIMITED TO REPORTED INSPECTIONS; GOVERNANCE AND TECHNICAL BLOCKERS REMAIN OPEN`**.

---

### 12.2 Evaluasi Pre-Handoff Gates (G-01 sampai G-10)
- **G-01 (Fact-Based Plan Verification)**: `CONDITIONALLY MET` (Plan mencantumkan rujukan kode hasil inspeksi lokal pada Evidence Ledger; verifikasi independen oleh Auditor belum lengkap; koreksi dokumen rencana secara tegas dibedakan dari keberhasilan implementasi kode).
- **G-02 (Empirical Evidence Verification)**: `CONDITIONALLY MET` (Bukti dibatasi pada inspeksi kode statis di server Linux; pengujian fisik mobile dilabeli `NOT VERIFIED`).
- **G-03 (Repository Verified Ledger Integrity)**: `CONDITIONALLY MET` (Evidence Ledger §4.4 memuat path, baris, dan raw snippets dari kode lokal; status database live dan runtime mobile belum diverifikasi independen).
- **G-04 (Preservation Gate Synchronization)**: `CONDITIONALLY MET` (Diselaraskan dengan evaluasi konservatif D-01 s.d. D-07 pada §12.1; kesimpulan preservasi berstatus PARTIAL; pengujian runtime fisik berstatus NOT VERIFIED).
- **G-05 (Readiness Conclusion Cross-Check)**: `CONDITIONALLY MET` (Diselaraskan dengan disposisi kesiapan pada §13.1; mengakui celah dan blocker yang masih terbuka; inventaris 27 AC terbukti 100% konsisten tanpa kategori ganda).
- **G-06 (Normative Contract & Acceptance Consistency)**: `CONDITIONALLY MET` (16 NC dan 27 AC terpetakan dua arah; ketergantungan blocker teknis B-01, B-02, B-06, B-08 dan gap spesifikasi usulan B-07 dicatat eksplisit).
- **G-07 (Governance Lock & Single File Output)**: `MET` (Hanya satu berkas rencana kanonikal yang dimodifikasi; batas siklus korektif dipatuhi; tidak ada dokumen pendamping atau artefak duplikat yang dibuat).
- **G-08 (Zero Implementation Authorization)**: `MET` (Implementasi kode PE-02 tetap secara sah `NOT AUTHORIZED`).
- **G-09 (Zero Mutation & Clean Repo State)**: `CONDITIONALLY MET WITH DISCLOSURE` (Nol mutasi kode tracked; keberadaan 2 berkas dokumen untracked di `docs/` dicatat transparan; inspeksi kebersihan repositori dibatasi pada tingkat direktori root dan tidak diklaim sebagai jaminan kebersihan rekursif).
- **G-10 (Adversarial Plan Audit & Contradiction Filter)**: `NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL GAPS ACKNOWLEDGED` (Mengakui secara jujur bahwa kontradiksi material CONF-01 s.d. CONF-03, circular dependency B-08, dan blocker B-04, B-05, B-06, B-07, B-09 belum diselesaikan).

---

### 12.3 Evaluasi Gate Kualitas Plan (Gate A) vs Kesiapan Implementasi (Gate B)
Dokumen ini memisahkan secara tegas antara evaluasi kualitas dokumen rencana (*Gate A*) dan kesiapan pelaksanaan implementasi (*Gate B*):

```
+---------------------------------------------------------------------------------------------------+
|                        EVALUASI DUA GERBANG TATA KELOLA (GATE A vs GATE B)                        |
+----------------------------------------------------+----------------------------------------------+
| Parameter Evaluasi Kualitas Plan (Gate A)          | Hasil Evaluasi Substantif                    |
+----------------------------------------------------+----------------------------------------------+
| 1. Seluruh 16 NC terdefinisi dengan acuan sumber   | MEMENUHI SYARAT                              |
| 2. Seluruh 27 AC memiliki expected result terukur  | MEMENUHI SYARAT (AC-01 bersyarat PO)         |
| 3. Traceability dua arah NC <-> AC terbukti        | MEMENUHI SYARAT                              |
| 4. Bukti Evidence Ledger terverifikasi di server   | MEMENUHI SYARAT (Klaim dibatasi kode statis) |
| 5. Seluruh konflik material (CONF-01..03) selesai  | GAGAL (Konflik terbuka menahan kelulusan)   |
| 6. Konsistensi status antar-register bebas cacat   | GAGAL (Kontrak kriptografi B-08 terblokir)   |
+----------------------------------------------------+----------------------------------------------+
| STATUS AKHIR GATE A                                | NOT PASSED — REQUIRES TARGETED CORRECTIONS   |
+----------------------------------------------------+----------------------------------------------+
| Parameter Evaluasi Kesiapan Implementasi (Gate B)  | Hasil Evaluasi Substantif                    |
+----------------------------------------------------+----------------------------------------------+
| 1. Kelulusan formal Gate A                         | GAGAL (Gate A belum lulus)                   |
| 2. Penyelesaian Circular Dependency Kriptografi    | TERBLOKIR (B-08 tetap terbuka)               |
| 3. Penyelesaian Blocker B-04 (2PC / Zero-DDL)      | TERBLOKIR (B-04 / CONF-03 tetap terbuka)     |
| 4. Penyelesaian Blocker B-05 (Semantik Hash DB)    | TERBLOKIR (B-05 tetap terbuka)               |
| 5. Penyelesaian Blocker B-06 (POSIX TOCTOU)        | TERBLOKIR (B-06 tetap terbuka)               |
| 6. Keputusan PO atas Blocker B-09 (Signer UNKNOWN) | TERBLOKIR (Menunggu keputusan resmi PO)      |
| 7. Otorisasi resmi pelaksanaan implementasi        | TIDAK DIBERIKAN (NOT AUTHORIZED)             |
+----------------------------------------------------+----------------------------------------------+
| STATUS AKHIR GATE B                                | BLOCKED                                      |
+----------------------------------------------------+----------------------------------------------+
```

---

## 13. READINESS GATE DAN BATAS OTORISASI

### 13.1 Evaluasi Kesiapan (Readiness Conclusion)
Berdasarkan bukti faktual dan hasil audit, kesiapan sistem dirinci ke dalam 9 kategori kesiapan:
1. **Hal yang Telah Diverifikasi dari Inspeksi File Repositori (`[REPOSITORY-VERIFIED: STATIC FILE INSPECTION ONLY]`):** Kepatuhan skema DDL berkas `schema.postgres.sql` (bukan bukti database runtime live), engine packaging Go `container.go`, modul kriptografi Ed25519 SDK `crypto.ts`, handler scheme NX Player `main.js`, ketiadaan 2PC di Marketplace server `server.js`, dan status git commit `fc08a5c...` pada tracked files.
2. **Hal yang Berstatus Spesifikasi Konseptual (`SPECIFIED — PENDING IMPL`):** Skema lengkap manifest album (valid JSON Schema Draft 7, batas 199 track), serializer RFC 8785 JCS, invariant Safe-Open, taksonomi 20 error code, dan formula derivasi ID.
3. **Inventaris dan Klasifikasi Kesiapan Seluruh Acceptance Criteria (Total Tepat 27 AC):**
   Seluruh 27 AC terpetakan secara lengkap dan eksklusif (setiap AC berada tepat di satu kelompok utama tanpa penghitungan ganda):
   - *Kelompok 1: 15 AC Spesifikasi Siap Uji (`[TEST-PLANNED — SPECIFICATION READY]`)*: AC-02, AC-04, AC-08, AC-09, AC-10, AC-11, AC-12, AC-17, AC-18, AC-19, AC-22, AC-23, AC-24, AC-26, AC-27 (Spesifikasi dan kriteria hasil uji lengkap tanpa blocker terbuka).
   - *Kelompok 2: 9 AC Rencana Uji Terblokir Eksekusi (`[TEST-PLANNED — EXECUTION BLOCKED]`)*:
     - *Sub-Kategori 2a: Modul Implementasi Belum Tersedia (`[IMPLEMENTATION MODULE PENDING]` - 2 AC)*: AC-05 (B-01: Strict JSON Parser belum dikoding), AC-06 (B-02: RFC 8785 JCS Serializer belum dikoding).
     - *Sub-Kategori 2b: Terblokir Gap Arsitektur & Spesifikasi Usulan (`[BLOCKED BY ARCHITECTURE / PROPOSED SPEC]` - 7 AC)*: AC-03 (B-08: Circular Dependency Manifest Signing), AC-13 (B-07: Batas Kuota Ekstraksi ZIP masih berstatus usulan), AC-14 (B-04/CONF-03: Gap 2PC ke License Daemon), AC-15 (B-04/CONF-03: Gap 2PC / Replay Settlement), AC-16 (B-05: Semantik hash database), AC-20 (B-06: Batasan userspace POSIX Safe-Open TOCTOU), AC-21 (B-06: Batasan userspace POSIX post-open descriptor).
   - *Kelompok 3: 3 AC Menunggu Keputusan Resmi Product Owner (`[PO DECISION REQUIRED]`)*: AC-01 (Kebijakan Unknown Fields Manifest Strict vs Permissive), AC-07 (B-09 / CONF-01: Kebijakan Signer UNKNOWN), AC-25 (CONF-02: Hierarki Status Agregat NX Verify).
   *(Rekonsiliasi agregat: 15 + 9 + 3 = 27 AC terbukti 100% konsisten dengan §2.1, §8, dan Tabel 1.4)*.
4. **Hal yang Belum Diverifikasi (`NOT VERIFIED — EVIDENCE NOT AVAILABLE`):** Pengujian fisik runtime mobile iOS/Android dan Usage Service cluster.
5. **Rangkuman Ketergantungan Blocker Teknis & Arsitektur:** Blocker B-01 s.d. B-08 tetap terbuka secara transparan (B-01 dan B-02 menunggu pengkodean modul; B-04, B-05, B-06, B-08 menunggu keputusan arsitektur; B-07 menunggu pembekuan spesifikasi kuota ZIP).
6. **Rangkuman Ketergantungan Keputusan Otoritatif PO:** Keputusan PO tetap ditunggu untuk menyelesaikan CONF-01 (Signer UNKNOWN Opsi A/B/C), CONF-02 (Hierarki Status Agregat NX Verify), dan CONF-03 (Model Transaksi Terdistribusi Non-2PC).
8. **Kualifikasi Kelulusan Gate:** Gate A berstatus **`NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL CONFLICTS REMAIN`**; Gate B berstatus **`BLOCKED`**.
9. **Status Otorisasi Implementasi PE-02:** **`NOT AUTHORIZED`** (Dilarang keras memulai implementasi kode atau migrasi database).

### 13.2 Disposisi Kesiapan Dokumen Resmi
Status kesiapan resmi dokumen ditetapkan sebagai:

**`REQUIRES TARGETED CORRECTIONS (WITH OPEN MATERIAL CONFLICTS, STRUCTURAL BLOCKERS, AND PENDING PO DECISION) / NOT READY FOR IMPLEMENTATION — BLOCKED`**

---

## 14. MANDATORY CLOSING DECLARATIONS

Sesuai ketentuan tata kelola dan hasil audit komprehensif, deklarasi penutup berikut ditegaskan berbasis bukti faktual dengan batas pembuktian yang diakui transparan:

1. **Nol Mutasi Kode Sumber Tracked**: Tidak ada berkas kode aplikasi, modul SDK, service, atau unit test tracked yang diubah (*Zero source code mutation* dipatuhi 100%).
   - *Bukti Inspeksi Aktual*:
     ```bash
     $ git rev-parse HEAD
     fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956
     $ git diff --name-only
     (bersih; nol berkas kode tracked termutasi pada working tree aktif)
     ```
2. **Keterbukaan Berkas Untracked Docs**: Terdapat 2 berkas dokumen acuan untracked pada working tree:
     ```bash
     $ git status --porcelain
     ?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md
     ?? docs/whitepapers/Nexa_White_Paper_v5_6.md
     ```
     *(Working tree tracked bersih; keberadaan 2 berkas dokumen di docs/ dicatat secara jujur dan transparan tanpa klaim semu bahwa working tree 100% bersih tanpa berkas untracked)*.
3. **Integritas Berkas Skema Database (Zero-DDL Berkas)**: Tidak ada perubahan skema aktif pada berkas `marketplace/db/schema.postgres.sql` (*Zero database migration pada skema repositori* dipatuhi 100%). Diakui secara transparan bahwa status database runtime live/produksi tidak diverifikasi (`NOT VERIFIED`) karena tidak ada koneksi database langsung dalam penugasan perbaikan dokumen ini.
4. **Nol Berkas Tambahan di Luar Plan Kanonikal**: Satu-satunya berkas rencana implementasi yang dimodifikasi adalah `evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (direktori `evidence/` berstatus gitignored oleh `.gitignore:28`). Tidak ada rencana duplikat atau dokumen audit terpisah yang dibuat oleh Programmer (*Rule C dipatuhi 100%*).
5. **Bukti Aktual Repositori Root Bersih (Rule D)**: Repositori root `/opt/antigravity/projects/nexa/` terbukti bersih dari file sementara atau artefak liar pada tingkat direktori root (`total 1780`). Catatan: inspeksi ini membuktikan kebersihan direktori tingkat root berdasarkan `ls -la`, dan tidak diklaim sebagai jaminan kebersihan rekursif seluruh subdirektori repositori.
6. **Isolasi Baseline Sprint 16 & PE-01**: Sprint 16 tetap 🔒 `CLOSED / FINAL ACCEPTED / FROZEN` dan PE-01 tetap 🔒 `CLOSED / FROZEN`.
7. **Sprint 17 Belum Dimulai**: Milestone Sprint 17 tetap berstatus ⏸️ `NOT STARTED`.
8. **Implementasi PE-02 Belum Diotorisasi**: Status implementasi kode PE-02 tetap secara sah **`NOT AUTHORIZED`**.
9. **Status Aktual Blocker dan Keputusan PO**: Blocker B-04 / NC-08 / CONF-03 tetap `BLOCKED`; Blocker B-05 / NC-09 tetap `BLOCKED`; Blocker B-06 / NC-12 tetap `OPEN / BLOCKED`; Blocker B-08 (Circular Crypto) tetap `BLOCKED`; Blocker B-09 / NC-04 / CONF-01 tetap `PO DECISION REQUIRED`.
10. **Status Gate A dan Gate B**: Gate A berstatus **`NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL CONFLICTS REMAIN`**; Gate B berstatus **`BLOCKED`**.
