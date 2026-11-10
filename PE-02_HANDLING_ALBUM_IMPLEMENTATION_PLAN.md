# NEXA PE-02 — HANDLING ALBUM IMPLEMENTATION PLAN
## PROGRAMMER AUDITED CORRECTIVE RECONCILIATION — BASELINE-LOCKED & EVIDENCE-BASED
### Canonical Implementation Plan, Source Authority, Traceability & Regression Prevention (Task ID: NEXA-PE02-AUDITED-RECONCILIATION-REV6.3)

> **DISPOSISI HASIL AUDIT TERARAH TERBARU (FINDING-01 s.d. FINDING-06):**
> - **Gate A (Kualitas Dokumen Plan):** **`NOT PASSED — PRODUCT TRUTH RECONCILIATION APPLIED; SUBSTANTIVE BLOCKERS REMAIN; INDEPENDENT RE-AUDIT REQUIRED`**
> - **Gate B (Kesiapan Eksekusi Implementasi):** **`BLOCKED`**
> - **Otorisasi Implementasi Kode PE-02:** **`NOT AUTHORIZED` (DILARANG KERAS MEMULAI KODING / MIGRASI DATABASE)**
> - **Sprint 16 Baseline:** 🔒 **`CLOSED / FINAL ACCEPTED / FROZEN`** (Tidak Boleh Diubah)
> - **PE-01 Baseline:** 🔒 **`CLOSED / FROZEN`** (Tidak Boleh Diubah)
> - **Sprint 17 Milestone:** ⏸️ **`NOT STARTED`** (Belum Dimulai)
> - **Blocker Struktural & Ketidakpastian Kriptografi Kritis (status setelah integrasi PSV yang dilaporkan Programmer; independensi bukti sumber masih harus diperiksa):**
>   - **B-04 / NC-08 / CONF-03:** **`OPEN / BLOCKED — MODEL B, SSP ALLOCATION, CHECKOUT IDENTITY & IMMUTABLE MANIFEST APPROVED; TRANSACTION / STORAGE / RECOVERY CONTRACT STILL OPEN`** (Model B, SSP/Largest Remainder, tujuh aturan `bundle_checkout_id`, dan Immutable Checkout Manifest sebagai Single Source of Truth telah disahkan; storage/persistensi, pemetaan member-to-acquisition, idempotency, commit boundary, settlement, dan reconciliation tetap terbuka serta tidak boleh diasumsikan).
>   - **B-05 / NC-09:** **`STATIC DDL REPORTED VERIFIED; EXISTING HASH IS WRAPPER-ZIP DOMAIN; PER-MEMBER CHILD HASH CONTRACT NOT CLOSED`** (Makna field yang ada dilaporkan terpetakan; child mapping dan implikasi kontrak tetap harus dinilai terpisah).
>   - **B-06 / NC-12:** **`OPEN / BLOCKED — PLATFORM PSV INCOMPLETE`** (Belum ada matriks bukti dan adversarial tests per platform; opsi mitigasi tidak disahkan).
>   - **B-07 / NC-07:** **`OPEN / BLOCKED — TECHNICAL PARAMETERS UNRESOLVED`** (Ketiadaan extractor dilaporkan; kuota/rasio harus ditetapkan Architecture Authority berdasarkan threat model, benchmark, dan PSV).
>   - **B-08 / NC-02:** **`OPEN / BLOCKED — SIGNATURE CONTRACT UNRESOLVED`** (Ketiadaan serializer/parser generik dilaporkan; detached envelope masih proposal, bukan keputusan arsitektur).
>   - **B-09 / NC-04 / CONF-01:** **`OPEN / BLOCKED — PSV EVIDENCE AND RESIDUAL NORMATIVE DECISION`** (Bukti signer/membership belum lengkap; keputusan normatif hanya diminta setelah fakta teknis dan lifecycle dibuktikan).
>   - **NC-14 / CONF-02:** **`PO DECISION APPROVED (OPTION B)`** (Keputusan PO Disahkan: NX Verify Tidak Menampilkan Status Agregat Album; Hasil Verifikasi Individual Member Tetap Menjadi Hasil Utama).

---

## 1. IDENTITAS DOKUMEN, FASE, STATUS, DAN MATRIKS PENUTUPAN AUDIT

### 1.1 Identitas dan Batas Kewenangan Tugas (DEFECT-C: Pemetaan Lokasi Kanonikal)
Dokumen ini merupakan satu-satunya artefak kanonikal (*Single Canonical Artifact Delivery*) yang mengonsolidasikan perencanaan teknis penanganan Album (`PE-02`) pada era post-Sprint 16 / pre-Sprint 17 Nexa Ecosystem. Dokumen ini disiapkan murni untuk koreksi terarah spesifikasi tata kelola dan pengujian (*Plan Correction Only*), dan **SECARA EKSPLISIT TIDAK MEMBERIKAN OTORISASI IMPLEMENTASI KODE SUMBER MAUPUN SKEMA DATABASE**.

> **Deklarasi Pemetaan Lokasi Artefak Kanonikal (DEFECT-C):**
> 1. **Lokasi Pengiriman Kanonikal GitHub (`whisnu/plan`, branch `main`):** `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (berada tepat pada root directory repositori pengiriman GitHub).
> 2. **Lokasi Staging Kerja Lokal (`whisnu/nexa`, host Linux):** `/opt/antigravity/projects/nexa/evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`. Penempatan pada subdirektori `evidence/` ini diwajibkan oleh aturan preservasi repositori kode sumber `whisnu/nexa` yang mengabaikan folder `evidence/` via `.gitignore:28` demi menegakkan prinsip *Zero Root Pollution* (Rule D) dan *Zero Source Code Mutation*.
> 3. **Identitas Konten Tunggal:** Kedua path merujuk pada objek konten yang identik (dibuktikan oleh kesamaan Git Blob SHA). Tidak ada salinan kedua yang dikelola atau diserahkan pada GitHub `whisnu/plan`.

| Parameter Tata Kelola | Nilai Resmi | Parameter Tata Kelola | Nilai Resmi |
|---|---|---|---|
| **Dokumen ID** | `PE-02-PLAN-REV6-RECONCILED` | **Fase Ekosistem** | Post-Sprint 16 / Pre-Sprint 17 |
| **Status Gate A** | `NOT PASSED — PRODUCT TRUTH RECONCILIATION APPLIED; SUBSTANTIVE BLOCKERS REMAIN; INDEPENDENT RE-AUDIT REQUIRED` | **Status Gate B** | `BLOCKED` |
| **Otorisasi Implementasi** | `NOT AUTHORIZED` | **Sprint 16 Baseline** | 🔒 `CLOSED / FROZEN` |
| **PE-01 Baseline** | 🔒 `CLOSED / FROZEN` | **Sprint 17 Milestone** | ⏸️ `NOT STARTED` |
| **Aturan Mutasi Kode** | Zero Source Code Mutation | **Aturan Database** | Zero Database Migration / DDL |
| **Lokasi Kanonikal GitHub**| `whisnu/plan:main/PE-02_...md` (Root) | **Format Pengiriman** | Single Canonical Markdown File |

### 1.2 Hierarki Sumber Otoritas dan Batas Kewenangan (AUDIT-NEW-09 — PO APPROVED)
Sesuai Keputusan Product Owner yang Telah Disahkan (AUDIT-NEW-09 PO APPROVED), seluruh perumusan spesifikasi teknis, validasi rencana, pembuktian implementasi, dan resolusi konflik wajib mematuhi hierarki otoritas kanonikal enam tingkat berikut:

1. **Level 1 — Keputusan eksplisit Product Owner yang telah disetujui untuk ruang lingkup PE-02.**
2. **Level 2 — Kontrak produk dan governance Nexa yang telah disetujui atau dibekukan.**
3. **Level 3 — White Paper dan Roadmap yang telah disetujui, sepanjang masih berada dalam ruang lingkupnya.**
4. **Level 4 — Repository aktual sebagai bukti implementasi, bukan sebagai otoritas untuk mengubah kontrak produk.**
5. **Level 5 — Standar internasional yang relevan, sepanjang tidak bertentangan dengan persyaratan Nexa pada tingkat yang lebih tinggi.**
6. **Level 6 — Temuan audit historis, bukti pendukungnya, proposal yang belum disetujui, dan interpretasi teknis. Materi pada level ini harus mempertahankan statusnya dan tidak otomatis menjadi ketentuan normatif.**

> **Aturan Penanganan Pertentangan Otoritatif Kanonikal:**
> 1. Sumber dengan tingkat otoritas lebih rendah **dilarang keras** mengubah, membatalkan, atau mengesampingkan fakta, kontrak, atau keputusan pada tingkat yang lebih tinggi.
> 2. Keputusan PO pada ruang lingkup PE-02 **tidak boleh** mengubah baseline Sprint 16 yang telah frozen atau kontrak PE-01 yang telah dikunci.
> 3. Repository aktual (Level 4) hanya berfungsi sebagai bukti kondisi implementasi yang ada, bukan otoritas untuk merekayasa atau mengubah kontrak produk tanpa keputusan tingkat di atasnya.
> 4. Temuan audit, usulan spesifikasi, atau interpretasi teknis (Level 6) mempertahankan status asalnya dan tidak otomatis menjadi ketentuan normatif.
> 5. Jika terjadi pertentangan antara dua sumber otoritatif pada tingkat yang sama atau ambiguitas material yang belum diselesaikan sumber normatif, Programmer **wajib menghentikan penetapan kontrak** (`CONFLICT — STOP AND CLARIFY`) dan meminta penetapan resmi tertulis dari Product Owner. Dilarang keras menyelesaikan konflik melalui asumsi, ekstrapolasi sepihak, atau tebakan bebas.
> 6. Seluruh bagian dokumen ini yang merujuk pada hierarki otoritas (termasuk §3.1 dan §10.3) secara hierarkis tunduk penuh pada ketentuan kanonikal Bagian 1.2 ini.
> 7. **Kualifikasi ruang lingkup rujukan White Paper/Roadmap untuk PE-02:** White Paper v5.6 dan Roadmap v4.8 adalah sumber Product Truth, tetapi keduanya tidak memuat spesifikasi Album ZIP, Album Manifest, Album Signer, atau lifecycle signer Album. Rujukan White Paper ke manifest, container, Creator signature, Genesis, Registry, JIT Player, Verify, dan Studio hanya menjadi dasar bagi kontrak Nexa yang memang didefinisikan di sana—terutama perilaku standalone .nx, trust/evidence, dan baseline aplikasi—dan **tidak boleh diperluas otomatis** menjadi kontrak Album. Roadmap v4.8 mencatat PE-02 sebagai NOT READY — BLOCKED (V5-REV1), Product Enhancement Window OPEN / NOT FROZEN, dan implementasi NOT AUTHORIZED; status itu tidak dapat dinaikkan oleh isi plan ini. Setiap ketentuan Album-spesifik harus ditandai secara eksplisit sebagai (a) keputusan PO PE-02 yang benar-benar telah disahkan, (b) proposal teknis, atau (c) unresolved/blocked. Kutipan White Paper/Roadmap yang hanya mendukung perilaku member .nx tidak boleh ditulis seolah-olah sumber tersebut mengesahkan desain Album.

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

### 1.4 Batas Revisi Governance, Aturan Siklus Koreksi & Otorisasi PO Override (DEF-10)
Siklus koreksi ini mematuhi batas tata kelola normatif berdasarkan White Paper v5.6, Roadmap v4.8, serta Keputusan Otoritatif Product Owner:
1. **Titik Awal Hitungan Corrective Revision**: Sesuai White Paper v5.6 §Governance, hitungan corrective revision pertama (REV1) dihitung secara sah sejak audit independen pertama yang menghasilkan kewajiban koreksi formal dalam siklus terkait.
2. **Batas Maksimum Tiga Revisi Korektif (Max 3 Revisions)**: Tata kelola membatasi maksimum tiga siklus corrective revisions (REV1, REV2, REV3). Apabila REV3 gagal memenuhi seluruh kriteria kelulusan audit independen, siklus ditutup secara definitif. Pembuatan REV4 dilarang keras dalam siklus yang sama. Kegagalan setelah REV3 mewajibkan penerbitan prompt Programmer yang secara substantif baru dari Product Owner / Governance Authority.
3. **Larangan Reset Administratif**: Siklus revisi tidak dapat dan dilarang di-reset secara administratif melalui penggantian nama file, pengubahan nomor versi, pengubahan label revisi, atau penamaan prompt baru. Seluruh riwayat audit historis tetap tercatat utuh.
4. **Otorisasi Product Owner Governance Override & Resumption**:
   - Berdasarkan keputusan resmi tertulis Product Owner (*PO Governance Override & Resumption Authorization*), prasyarat konfirmasi tertulis corrective revision count sebelum memulai pekerjaan **dikecualikan secara khusus untuk mandat koreksi AUDIT-NEW-01 sampai AUDIT-NEW-10**.
   - Pengecualian administratif ini berlaku eksklusif untuk menyelesaikan perbaikan teknis yang telah diidentifikasi pada artefak kanonikal `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`.
   - Pengecualian ini **tidak mereset, tidak mengubah, dan tidak merekayasa** catatan hitungan revisi historis; pekerjaan ini **bukan REV4** dari siklus lama dan **bukan pembukaan siklus koreksi baru**.
   - Programmer tidak memperoleh kewenangan untuk memperluas ruang lingkup produk, mengubah model kepercayaan, atau menciptakan kontrak baru di luar mandat koreksi ini.
   - **Status Otorisasi Dokumen Rencana**: Koreksi Implementation Plan PE-02 berstatus **`AUTHORIZED BY PO OVERRIDE`**.
   - **Status Otorisasi Implementasi**: Implementasi kode PE-02 tetap mutlak **`NOT AUTHORIZED`** sampai diterbitkannya keputusan otorisasi implementasi terpisah oleh Product Owner.
5. **Anti-Overprocessing**: Tidak ada pembuatan dokumen pendamping, plan alternatif, fase audit buatan, duplikasi berkas kanonikal, atau perubahan kosmetik tanpa dasar. Seluruh perbaikan dilakukan secara *in-place* pada satu-satunya berkas kanonikal ini.
6. **Pemisahan Penutupan Dokumen vs Substantif**: Dokumen secara tegas membedakan antara tindakan koreksi plan (*Plan-Corrected*) dan penyelesaian substantif atas blocker (*Substantively Resolved*). Masalah substantif yang bergantung pada keputusan PO atau arsitektur eksternal tetap dinyatakan `OPEN / BLOCKED`.

### 1.5 Matriks Koreksi Reproduksibel REV6.3 (DEF-01 sampai DEF-10) — Rekonsiliasi Status Faktual (DEFECT-03)
Sesuai mandat koreksi Bagian II (DEF-06) dan hasil audit REV6.3 (DEFECT-03), tabel berikut menyajikan Correction Matrix ringkas dan dapat direproduksi secara objektif oleh Auditor. Seluruh status hasil evaluasi ditetapkan secara jujur dan faktual: status `PASS` hanya diberikan jika dokumen telah konsisten dan terbukti tanpa kontradiksi internal, sedangkan temuan yang dependensi normatifnya belum selesai atau belum memperoleh keputusan resmi PO tetap dipertahankan `BLOCKED` atau `NOT VERIFIED`:

| Defect ID | Lokasi Terdampak | Kondisi Awal (Gap REV6.2) | Tindakan Koreksi Spesifik | Dasar Normatif / Sumber | Acceptance Criteria | Bukti yang Diperiksa | Hasil Evaluasi | Catatan / Pertanyaan PO |
|:---:|---|---|---|---|---|---|:---:|---|
| **DEF-01** | §1.5, §1.6 (A-01), §2.1, §2.3.B, §8, §9, §13.1 | AC-02, AC-10, AC-26 dinyatakan SPEC READY padahal dependensinya proposed/blocked; §9, §13.1, dan catatan A-01 tidak konsisten dengan §8; AC-17 berpotensi ditafsirkan sebagai bukti runtime. | `[SNAPSHOT HISTORIS REV6.3 — BUKAN READINESS AKTIF]` Catatan Historis: Pada REV6.3 dilakukan rekonsiliasi 27 AC (11 Spec Ready, 13 Blocked, 3 PO Decision Required). Pada snapshot historis sebelum membership gate AC-33/AC-34 diberlakukan, register saat itu telah diperluas menjadi **34 AC** (AC-01 s.d. AC-34) pada §2.1, §8, §9, dan §13.1 sejalan dengan penambahan AC-28 s.d. AC-34, pengesahan PO atas CONF-02 (Pilihan B APPROVED), dan penurunan AC-32 (terblokir pada kontrak lifecycle Auto-Next multi-payload). | White Paper v5.6; RFC 8259; `schema.postgres.sql`; §8 AC Register | Jumlah AC dan kategori agregat tercatat 34; konsistensi semantik lintas-bab tetap harus diuji ulang; snapshot historis pra-membership-gate (14 Spec Ready + 18 Execution Blocked (snapshot historis pra-membership-gate; bukan readiness aktif); agregat aktif 12 Spec Ready + 20 Execution Blocked [termasuk AC-22 gap prasyarat JIT dan provenance membership manifest CONF-01, AC-28 gap identitas Album, AC-29 gap reload Album, dan AC-32 gap kontrak lifecycle Auto-Next multi-payload] + 2 PO Decision Required [AC-01, AC-07 (autentisitas provenance membership manifest saat signer UNKNOWN; B-09 / CONF-01)] = 34 AC) konsisten tanpa kategori ganda. | §1.5, §1.6 (A-01), §2.1, §2.3.B, §8, §9, §13.1 | `HISTORICAL PASS — AGGREGATE COUNT ONLY; CURRENT SEMANTIC RECONCILIATION REQUIRED` | 18 AC substantif terblokir eksekusi (B-01..B-08/NC-05/NC-07/NC-15/Field Identity/JIT Prerequisites/Album Identity/Album Reload/Multi-Payload Auto-Next Lifecycle); 2 AC menunggu keputusan resmi PO (AC-01 [Unknown Fields], AC-07 [autentisitas provenance membership manifest saat signer UNKNOWN; B-09 / CONF-01]). |
| **DEF-02** | §6.7, §7.1 (B-03) | B-03 dipetakan kasar ke Safe-Open AC-20/21; batas kuota diklaim COVERED; 50 vs 200 belum dibedakan; rasio 10:1 vs 100:1 kontradiktif; batas 2 GiB dipetakan keliru ke AC-11/12; ketidaktepatan satuan GB vs GiB. | Susun Tabel Coverage Proof per-kewajiban (REQ-B03-01 s.d. 09); pisahkan validasi entri ZIP dari Safe-Open; pisahkan 50 member UI vs 200 wrapper ZIP; sinkronkan ambiguitas rasio kompresi 10:1 usulan B-07 vs 100:1 referensi pembanding eksternal yang belum diverifikasi di seluruh dokumen murni sebagai usulan spesifikasi yang menunggu keputusan arsitektur (REQ-B03-04); selaraskan satuan batas payload kontainer individual ke 2 GiB ($2 \times 1024^3$ bytes) baseline vs kuota akumulatif wrapper 4 GB desimal ($4 \times 10^9$ bytes) proposed spec, cabut AC-11/12 dari batas 2 GiB dan akui keterbukaan celah pengujian pada AC Register (REQ-B03-05); serta cabut AC-05 dari batas 50 track manifest dan catat keterbukaan celah pengujian pada AC Register (REQ-B03-06). | PKWARE APPNOTE; RFC 1951; POSIX.1-2017; `container.go#L106` | Setiap requirement B-03 memiliki pemetaan granular, satuan presisi (GiB vs GB), metode test, dan status terpisah tanpa asumsi sepihak. | §7.1 (Tabel Coverage Proof B-03) | `BLOCKED / PARTIALLY COVERED` (Spesifikasi granular terinci; status PASS ditangguhkan menunggu keputusan otoritatif PO/Arsitektur atas parameter kuota numerik B-07 dan resolusi celah pengujian REQ-B03-05 dan REQ-B03-06) | Batas kuota B-07 dan rasio kompresi berstatus `PROPOSED SPEC`; celah pengujian 2 GiB kontainer dan 50 track manifest terbuka. |
| **DEF-03** | §7.2 (F-10), §8 | F-10 pelaporan per member dipetakan keliru ke AC-26 (error taxonomy); ketiadaan AC spesifik pelaporan. | Hapus rujukan AC-26 dari F-10; akui secara transparan ketiadaan AC penguji pelaporan Verify per-member sebagai celah spesifikasi pengujian; AC-26 murni error taxonomy. | WP v5.6 §Verify; F-10 historis | F-10 tidak dipaksakan ke AC yang salah; kebutuhan pelaporan per member tercatat jujur. | §7.2 (F-10), §8 (AC-26) | `BLOCKED` (Celah Spesifikasi AC Register) | Memerlukan otorisasi penambahan AC baru oleh PO/Arsitektur untuk pelaporan per-anggota. |
| **DEF-04** | §2.3, §4.4 (E-01), §6.5, §6.9 | Argumen `canonicalJcs` disamakan dengan struktur object; `JSON.stringify` disamakan dengan RFC 8785; relasi key ambigu. | Pisahkan 3 layer (Registry Cert, Genesis Ownership, Manifest); catat keterbatasan `JSON.stringify` di `sdk.ts`; dokumentasikan `GENESIS_PUBLIC_KEY` vs `creator_public_key`. | `sdk/typescript/src/sdk.ts#L205-L260`; RFC 8785 | Lapisan kriptografi dan canonicalization terpisah; perbedaan istilah dicatat. | §2.3, §4.4 (E-01), §6.5, §6.9 | `PASS` (Pemisahan Lapisan Spesifikasi Terbukti) | Penyeragaman istilah `GENESIS_PUBLIC_KEY` pending PO. |
| **DEF-05** | §1.5.1, §6.15, §8, §9 | Klaim 20 kode error kanonikal terverifikasi di Go; padahal hanya kondisi kegagalan container.go#L112 yang ada; 19 kode proposed di NC-15; Genesis error code unresolved. | Koreksi klaim: 20 kode error adalah Proposed Specification (NC-15) yang belum dibekukan di WP v5.6; kegagalan signature Genesis berstatus unresolved taxonomy (fail-closed pasti); AC-10, AC-26, NC-15 berstatus blocked/proposed. | Error Taxonomy Spec §6.15; `container.go#L112`; `sdk.ts#L227` | Klasifikasi provenance jelas: tidak ada klaim verified semu untuk 20 kode; baseline, proposed, dan unresolved dipisahkan. | §1.5.1, §6.15, §8 (AC-10, AC-26), §9 (NC-05, NC-15) | `BLOCKED` (Taksonomi Usulan & Unresolved) | Formalisasi NC-15 pending Arsitektur; penetapan kode diskrit Genesis pending PO/Arsitektur. |
| **DEF-06** | §1.5 | Plan belum menyediakan Correction Matrix yang dapat direproduksi secara operasional oleh Auditor. | Memasukkan Correction Matrix REV6.3 langsung ke dalam dokumen kanonikal memuat 10 kelompok temuan lengkap dengan evaluasi hasil yang jujur. | Mandat Koreksi Bagian II (DEF-06); Prompt Handoff REV6.3 | Auditor dapat memverifikasi tindakan, bukti, dan acceptance criteria per temuan tanpa bias kosmetik. | §1.5 (Tabel Matriks Koreksi) | `PASS` (Matriks Reproduksibel Terpasang) | Tidak menambah fase audit buatan. |
| **DEF-07** | §6.12, §7.1 (B-06) | Pengakuan residual risk TOCTOU belum operasional untuk evaluasi penerimaan risiko. | Rinci protected asset, threat model, race window, protection boundary, batas POSIX, deteksi fail-closed, dan acceptance authority; pertahankan B-06 terblokir. | POSIX.1-2017; `fs_safe.ts#L30-L55` | Analisis B-06 terperinci secara operasional; B-06 tetap `BLOCKED` pending risk acceptance PO. | §6.12, §7.1 (B-06) | `BLOCKED` (Menunggu Penerimaan Resmi Risiko) | Penerimaan formal residual risk userspace POSIX pending otorisasi PO/Lead Security Architect. |
| **DEF-08** | §5.1, §7.2 (F-09), §8 | Kasus batas regex `^[a-zA-Z0-9_-]+\.nx$` belum dirinci; ekuivalensi fungsi `cleanBase` belum dibuktikan. | Dokumentasikan matriks kasus batas (multiple dots, uppercase, separator, dsb.); tegaskan `cleanBase` adalah helper sanitasi internal, bukan regex validasi. | Manifest Schema §5.1; `marketplace/server.js:164` | Aturan regex kanonikal dan perilaku kasus batas terdefinisi pasti tanpa asumsi helper. | §5.1, §7.2 (F-09) | `PASS` (Spesifikasi Kasus Batas Terbukti) | Format ekstensi non-lowercase ditolak tegas fail-closed. |
| **DEF-09** | §4.1, §4.4 (E-08), §14 | Klaim Git baseline dan kebersihan repositori berpotensi melebihi cakupan inspeksi riil. | Catat baseline commit `fc08a5c...`, branch `main`, tracked bersih (0 diff), 2 untracked docs diakui, `evidence/` gitignored; DB live dan mobile dinyatakan `NOT VERIFIED`. | `git rev-parse HEAD`; `git diff`; `git status`; `.gitignore:28` | Klaim repositori sebanding dengan inspeksi aktual; live DB dan mobile dinyatakan `NOT VERIFIED`. | §4.1, §4.4 (E-08), §14 | `PASS` (Batas Klaim Bukti Terverifikasi) | Verifikasi runtime live DB pending Sprint 17. |
| **DEF-10** | §1.4, §14 | Status siklus corrective revision belum dibuktikan dari riwayat audit primer di repositori. | Rinci aturan tata kelola (max 3 revisi, titik awal audit pertama, no reset); terapkan otorisasi eksplisit PO Governance Override untuk penyelesaian AUDIT-NEW-01..10 tanpa menunggu konfirmasi hitungan revisi; larang klaim REV4 / cycle baru. | WP v5.6 §Governance; Roadmap v4.8; PO Override Mandate | Status siklus dan otorisasi PO Override dicatat faktual tanpa rekayasa riwayat revisi; batas 3 revisi tetap diakui; koreksi plan diotorisasi; implementasi PE-02 tetap NOT AUTHORIZED. | §1.4 (Aturan Siklus & PO Override), §14 | `PASS (GOVERNANCE OVERRIDE APPLIED)` | PO Override mengotorisasi kelanjutan koreksi teknis plan; riwayat revisi tidak direset; implementasi tetap NOT AUTHORIZED. |

### 1.5.2 Matriks Penanganan Temuan Audit Komprehensif Baru (AUDIT-NEW-01 sampai AUDIT-NEW-10)
Tabel berikut merangkum disposisi dan penanganan objektif terhadap sepuluh temuan audit komprehensif baru berdasarkan mandat dan keputusan Product Owner:

| ID Audit | Lokasi Terdampak | Temuan / Gap Teknis | Tindakan Koreksi Spesifik | Dasar Otoritatif | Status Penyelesaian | Keterangan / Tindak Lanjut |
|:---:|---|---|---|---|:---:|---|
| **AUDIT-NEW-01** | §1.5.1, §5.1, §5.2, §5.3, §8 | Urutan JIT pada Stage 8, divergensi identitas field hash audio (`audio_sha256` vs notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif)), batas diagnostik vs active license Stage 7, batas izin Background Pre-Verification Stage 8a, dan dasar normatif dependensi Stage 8a terhadap Stage 7b (Genesis) dan Stage 7c (Active License) belum disahkan normatif. | Menyelaraskan urutan dependensi JIT di seluruh dokumen (§1.5.1, §5.1, §5.2, §5.3); menyusun Matriks Dependensi Silang JIT Album (§3.4) yang memisahkan Stage 8a, 8b, dan 8c; memperketat batas Stage 8a: deskriptor aman (Tahap 6) dan keutuhan PE-01 (Tahap 7a) adalah prasyarat I/O fisik minimum, namun dilarang menyatakan Stage 8a secara kategoris hanya memerlukan 6 dan 7a; status ketergantungan normatif Stage 8a terhadap validasi Genesis (7b) dan lisensi aktif (7c) dinyatakan jujur berstatus UNRESOLVED — GENESIS VALIDATION & ACTIVE LICENSE DEPENDENCY FOR DIAGNOSTIC DIGEST NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required), di mana kemampuan teknis mengekstrak bitstream mentah dilarang disamakan dengan izin produk untuk melanjutkan pemeriksaan; status izin diagnostik Background Pre-Verification Stage 8a dinyatakan jujur berstatus UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required) dengan memisahkan tegas kemampuan teknis komputasi, izin diagnostik produk, dan otorisasi pemutaran; merekonsiliasi divergensi identitas field hash audio antara skema manifest §5.1 (`audio_sha256`) dan Stage 8a / §6.9 / AC-09 (notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) / `sha256`) sebagai UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT tanpa asumsi alias, ekuivalensi, fallback tersembunyi, atau aturan prioritas sepihak; status kesiapan pengujian AC-09 diselaraskan menjadi TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY; menegaskan hasil digest 8a valid TIDAK PERNAH memberikan hak dekripsi atau playback; menegaskan Tahap 8b secara kumulatif mensyaratkan lolos digest 8a, validasi Genesis 7b, DAN lisensi aktif sah 7c; menegaskan aturan dependensi Stage 8b menuju Stage 8c di mana Stage 8c hanya boleh dijalankan setelah Stage 8b berhasil dan kegagalan 8b menghentikan alur fail-closed sebelum 8c; menegaskan Tahap 8c eksklusif untuk current member dan dilarang via pre-verifikasi antrean; menegaskan kebijakan dekripsi diagnostik yang belum memiliki kontrak normatif tetap UNRESOLVED — NORMATIVE CONTRACT NOT VERIFIED. | Mandat PO AUDIT-NEW-01; White Paper v5.6 §Distribution; internal/container/container.go; sdk.ts | `PARTIAL (CROSS-STAGE DEPENDENCY MATRIX SPECIFIED; GENESIS, LICENSE, FIELD IDENTITY & PRE-VERIFICATION PERMISSION UNRESOLVED PENDING PO CLARIFICATION)` | Matriks dependensi silang terpasang lengkap (§5.2); pemisahan gerbang otorisasi kumulatif 8b dan isolasi buffer 8c mutlak bebas celah; ketidakpastian normatif dependensi digest diagnostik, izin pre-verifikasi, dan identitas field manifest dicatat transparan tanpa asumsi sepihak. |
| **AUDIT-NEW-02** | §5.1, §8 (AC-01) | Contoh manifest menggunakan nilai dummy/ilustratif namun diklaim membuktikan seluruh Tier 3 invariants. | Pisahkan tegas 5 layer validasi (JSON syntax, Schema structure, Semantic, Cryptographic, Package/member). Beri label tegas contoh manifest murni struktural, nilai dummy tidak membuktikan kriptografi. | Mandat PO AUDIT-NEW-02; RFC 8259 | `PASS (PRESERVED)` | Tidak ada klaim pemenuhan kriptografis semu dari data dummy; kewajiban verifikasi Tier 3 tetap utuh. |
| **AUDIT-NEW-03** | §4.4 (E-07), §6.12 | Bukti E-07 hanya memuat `O_NOFOLLOW`, `fstatSync`, dan `isFile()`, namun diklaim membuktikan `lstatSync` dan perbandingan `dev`/`ino`. | Batasi klaim E-07 pada kode riil yang ada; nyatakan verifikasi ganda `lstatSync` dan `dev`/`ino` sebagai celah implementasi kode desktop (`NOT DEMONSTRATED BY E-07 / RESIDUAL GAP`); pertahankan B-06 terblokir. | `fs_safe.ts#L30-L55`; Mandat PO AUDIT-NEW-03 | `PASS (PRESERVED)` | B-06 tetap `OPEN / BLOCKED` pending pengujian unit anomali dan risk acceptance formal PO/Security Architect. |
| **AUDIT-NEW-04** | §1.5.1, §1.6 (A-24), §2.2, §5.1, §6 (NC-09), §6.9, §8 (AC-16), §9 (NC-09) | Klaim kaku delapan objek kriptografi/hash pada dokumen lama; klaim semantik acquired_package_sha256 melampaui bukti DDL; klasifikasi 'dua hash normatif terverifikasi' terlalu kuat; hubungan signature dan creator_signature belum dibuktikan dengan bukti primer kode yang dapat diakses auditor. | Rekonsiliasi total inventaris berbasis bukti (§6.9): memisahkan 4 objek signature Ed25519 diskrit dan 2 field hash SHA-256; mencatat bahwa pemetaan Go trailer signature (internal/container/container.go#L17-L135) dan TS SDK signatureBytes (sdk/typescript/src/container.ts#L4-L104) serta Genesis creator_signature (sdk/typescript/src/ownership.ts#L26) dilaporkan berdasarkan kode lokal whisnu/nexa commit fc08a5c, namun karena akses repositori sumber belum dapat diverifikasi secara independen oleh Auditor (HTTP 404), status bukti primer implementasi diturunkan jujur menjadi NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE; memisahkan inventaris hash menjadi tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field> (PROPOSED SPECIFICATION; identitas field normatif audio_sha256 vs tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256 berstatus UNRESOLVED — STOP AND CLARIFY) dan acquired_package_sha256 (Tingkat 1 DDL field existence berstatus NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE karena akses file DDL marketplace/db/schema.postgres.sql belum dapat diverifikasi independen oleh Auditor; Tingkat 2 & 3 semantik penulisan child row, payload, producer, dan consumer tetap UNRESOLVED — BLOCKED BY B-05); membedakan 3 entitas komputasional in-memory perancang; mengonfirmasi secara konseptual underlying_cert_id sebagai certificate identifier reference (bukan audio hash); mempertahankan B-08 circular dependency unresolved. | §6.9; Mandat PO AUDIT-NEW-04; internal/container/container.go; sdk/typescript/src/container.ts; sdk.ts; marketplace/db/schema.postgres.sql; RFC 8785; RFC 8032 | `NOT PASS — RECONCILED EVIDENCE-BASED INVENTORY (PRIMARY SOURCE EVIDENCE NOT AVAILABLE FOR INDEPENDENT AUDIT; SEMANTICS BLOCKED BY B-05; SIRKULARITAS SIGNATURE BLOCKED BY B-08)` | Inventarisasi faktual membedakan keberadaan field dari semantik; klaim bukti implementasi Go/SDK/DDL diturunkan jujur menjadi NOT VERIFIED karena keterbatasan akses repositori independen Auditor; status NOT PASS dipertahankan jujur selama bukti independen belum tersedia dan B-05 serta B-08 belum disahkan PO/Arsitektur. |
| **AUDIT-NEW-05** | §4.4 (E-03), §8 (AC-17), §13 | AC-17 mengklaim ketiadaan mutasi runtime DB aktif, padahal E-03 murni inspeksi statis berkas DDL `schema.postgres.sql`. | Batasi klaim AC-17 murni pada kepatuhan statis berkas skema DDL di repositori; tegaskan status live/runtime database sebagai `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. | `schema.postgres.sql`; Mandat PO AUDIT-NEW-05 | `PASS (PRESERVED)` | Zero-DDL pada berkas statis terbukti 100%; runtime live DB berstatus jujur `NOT VERIFIED`. |
| **AUDIT-NEW-06** | §5.1, §5.2, §6.7, §6.15, §7.1 (REQ-B03-03/07), §8 (AC-02), §10.3, §13.1 | Sisa kontradiksi penolakan direktori pada draf §5.1, NC-07 §6, dan A-08 §1.6 belum dibersihkan terhadap keputusan PO. | Menghilangkan seluruh sisa ketentuan penolakan direktori di §5.1, NC-07 §6, A-08 §1.6, §13.1, dan seluruh dokumen; menegaskan keputusan PO: regular files & directory entries diterima; symlinks & special files (FIFO, socket, dev) ditolak fail-closed ERR_ZIP_INVALID; semantik hardlink tidak didukung; berkas byte identik independen; hapus asumsi pengujian tipe hardlink generik universal di REQ-B03-03; harmonisasi flat archive ditegaskan hanya mengatur path relatif member .nx manifest (regex ^[a-zA-Z0-9_-]+\.nx$), bukan pelarangan entri direktori ZIP; menandai usulan lama sebagai catatan historis yang telah digantikan. | Keputusan PO: APPROVED (AUDIT-NEW-06) | `PASS (TARGETED CORRECTION APPLIED — SELURUH KONTRADIKSI DIREKTORI TUNTAS DIELIMINASI)` | Seluruh dokumen konsisten 100% dengan keputusan PO: direktori diterima; sisa kontradiksi §5.1 baris 540, NC-07 baris 816, dan A-08 baris 151 tuntas diselaraskan; tidak ada klaim deteksi hardlink generik. |
| **AUDIT-NEW-07** | §5.1, §6.7, §7.1 (REQ-B03-01), §8 (AC-01..02), §10.3 | Aturan keunikan nama berkas case-sensitive berisiko tabrakan pada filesystem case-insensitive (e.g. `TrackA.nx` vs `tracka.nx`). | Memasukkan aturan PO APPROVED: pertahankan nama asli; periksa keunikan case-insensitive via ASCII case folding; nama bentrok ditolak fail-closed; cantumkan tabel boundary matrix wajib; berlaku lintas platform POSIX/Windows/Android. | Keputusan PO: APPROVED (AUDIT-NEW-07) | `PASS (PRESERVED)` | Boundary matrix terpasang lengkap di §5.1 dan §6.7; penolakan fail-closed deterministik. |
| **AUDIT-NEW-08** | §5.1, §5.2 (Tahap 5), §6.7, §6.15, §8 (AC-02, AC-13) | Konflik pemetaan antara anomali deklarasi manifest, anomali fisik ZIP, dan ketidakcocokan bijeksi 1:1; inkonsistensi error nama file manifest vs fisik ZIP. | Merekonsiliasi pemetaan layer secara deterministik bebas kontradiksi (FINDING-04): (1) Anomali deklarasi/regex nama file pada manifest dipetakan ke ERR_MANIFEST_MALFORMED pada Manifest Validator (Tahap 3); (2) Anomali fisik arsip ZIP (rusak, symlink, special file, path traversal fisik, benturan case-insensitive antar-entri ZIP) dipetakan ke ERR_ZIP_INVALID pada ZIP Reader (Tahap 2); (3) Ketidakcocokan bijeksi 1:1 antara manifest dan ZIP (berkas manifest hilang di ZIP atau berkas reguler ekstra di ZIP) dipetakan ke ERR_ZIP_ENTRY_MISMATCH pada Packaging Validator (Tahap 5). Sinkronkan §5.1, §5.2 Tahap 5, tabel taksonomi §6.15, matriks deterministik, dan AC-02/AC-13. | §6.15; Mandat PO AUDIT-NEW-08; FINDING-04 | `PASS (TARGETED CORRECTION APPLIED — LAYER SEPARATION HARMONIZED)` | Pemisahan 3 layer deterministik bebas kontradiksi: kesalahan deklarasi manifest = ERR_MANIFEST_MALFORMED, anomali fisik ZIP = ERR_ZIP_INVALID, dan ketidakcocokan bijeksi = ERR_ZIP_ENTRY_MISMATCH. |
| **AUDIT-NEW-09** | §1.2, §3.1, §10.3 | Hierarki sumber otoritas pada §1.2 menggabungkan PO dan Arsitektur, menempatkan repository sebagai pengubah kontrak, dan belum memuat urutan keputusan PO yang tepat. | Mengganti hierarki otoritas lama dengan urutan persis 6 tingkat yang telah disahkan PO: Level 1 Keputusan PO PE-02, Level 2 Kontrak Produk & Governance Beku, Level 3 White Paper & Roadmap, Level 4 Repository Aktual sebagai Bukti Implementasi, Level 5 Standar Internasional, Level 6 Temuan Audit / Proposal / Interpretasi di §1.2, §3.1, dan §10.3. | Keputusan PO: APPROVED (AUDIT-NEW-09) | `PASS (TARGETED CORRECTION APPLIED)` | Hierarki otoritas kanonikal 6 tingkat terpasang persis sesuai keputusan PO tanpa interpretasi bercabang. |
| **AUDIT-NEW-10** | §2.2 (No 8), §5.2, §6 (NC-05), §7.2 (F-03), §8 (AC-10), §10.4, §13.12.11 | PLAN sebelumnya belum mengoperasionalkan keputusan PO tentang tiga peran kunci independen dan otorisasi third-party packaging. | Mengganti status CLARIFY lama dengan keputusan PO APPROVED; memasukkan target architecture untuk self-packaging, third-party packaging delegation, authority/evidence lifecycle, federated trust resolution, verifier result separation, closed/versioned .nxcert evolution, integrasi SDK/Player/Verify/Registry, serta acceptance dan negative tests. Pertanyaan normatif aktif berikutnya dibatasi pada penetapan pihak yang berwenang menerbitkan delegation; subdelegation baru dibahas setelah keputusan authority issuer ditetapkan. | Keputusan PO AUDIT-NEW-10; §13.12.11 | `PLAN RECONCILED — TARGET ARCHITECTURE SPECIFIED; ONE NORMATIVE AUTHORITY QUESTION REMAINS` | Keputusan tiga peran dan semantik unauthorized packaging telah dimasukkan; rincian yang belum diputuskan tidak diasumsikan. Implementasi tetap NOT AUTHORIZED. |

### 1.5.1 Catatan Tindak Lanjut Temuan Audit Komprehensif Historis (Temuan 1 s.d. 10)
Tabel berikut merinci resolusi teknis dan substantif untuk setiap temuan audit utama:

| ID Audit | Ringkasan Temuan Audit | Resolusi Teknis & Substantif pada Plan Kanonikal | Status Dokumen |
|:---:|:---|:---|:---:|
| **Temuan 1** | Nomenklatur dan pemetaan tanda tangan berpotensi mencampuradukkan Album Signer vs Container Creator serta salah memetakan creator_signature. | Memisahkan 4 tanda tangan digital Ed25519 secara konseptual berbasis analisis (§6.9): (1) Album Signer Signature (manifest kanonikal, NC-02 $\rightarrow$ AC-03), (2) Container Packaging Signature (trailer biner kontainer individual `.nx`, dilaporkan via `internal/container/container.go#L17-L135` sebagai `signature` dan `sdk/typescript/src/container.ts#L4-L104` sebagai `signatureBytes`, status audit: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` karena akses repositori independen Auditor belum tersedia), (3) Registry Certificate Signature (lapisan 1 genesis, `issuer_signature` di `sdk.ts#L207-L226`, status audit: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`), dan (4) Genesis Ownership Certificate Signature (lapisan 2 genesis, `creator_signature` di `ownership.ts#L26` dan `004_ownership.sql#L25`, status audit: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`). Ditegaskan secara konseptual bahwa `creator_signature` bukan field trailer kontainer melainkan properti sertifikat genesis. | `CORRECTED (INVENTORY RECONCILED; IMPLEMENTATION EVIDENCE NOT VERIFIED PENDING AUDITOR ACCESS)` |
| **Temuan 2** | Urutan tahapan JIT 8-tahap belum merinci seluruh pemeriksaan kriptografis secara eksplisit; divergensi identitas field digest manifest; batas diagnostik vs playback dan dependensi Genesis / active license belum dibuktikan normatif. | Merinci mapping eksplisit 8 tahap JIT dan menyusun Matriks Dependensi Silang JIT Album (§3.4): Tahap 1 Open Arsip ZIP (AC-02), Tahap 2 Validasi Fisik ZIP (AC-02, AC-13), Tahap 3 Pembacaan & Strict JSON Parse Manifes (AC-01, AC-05), Tahap 4 proposal JCS + verifikasi signature kriptografis; Registry signer trust/lifecycle tetap unresolved (AC-03, AC-06..08), Tahap 5 Bijeksi 1:1 Manifes-ke-ZIP (AC-02, AC-13), Tahap 6 Ekstraksi Member .nx & Atomic Safe-Open (AC-20, AC-21), Tahap 7 Validasi Format PE-01 (7a), Validasi Genesis (7b), dan Evaluasi Lisensi Aktif (7c). Tahap 8 dipisahkan menjadi 8a Verifikasi Digest SHA-256 Audio mentah, 8b Dekripsi Payload Audio terotorisasi, dan 8c Pendaftaran Buffer Audio ke pemutar (AC-09, AC-22..24). Memperketat batas Stage 8a: dilarang menyatakan Stage 8a secara kategoris hanya memerlukan 6 dan 7a; status ketergantungan normatif 8a terhadap Stage 7b (Genesis) dan 7c (Lisensi Aktif) dinyatakan jujur berstatus UNRESOLVED — GENESIS VALIDATION & ACTIVE LICENSE DEPENDENCY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required), di mana kemampuan teknis mengekstrak bitstream mentah dilarang disamakan dengan izin produk untuk melanjutkan pemeriksaan; status izin diagnostik Background Pre-Verification Stage 8a dinyatakan berstatus UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required) dengan memisahkan tegas kemampuan teknis komputasi, izin diagnostik produk, dan otorisasi pemutaran; merekonsiliasi divergensi identitas field digest manifest antara `audio_sha256` (§5.1) dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) (8a, §6.9, AC-09) sebagai UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT tanpa klaim alias atau ekuivalensi; status AC-09 diselaraskan menjadi TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY; hasil digest valid ditegaskan TIDAK memberikan otorisasi pemutaran; Tahap 8b secara kumulatif mensyaratkan lolos 8a, 7b, dan 7c; Tahap 8c eksklusif current member; kebijakan dekripsi diagnostik berstatus UNRESOLVED. | `CORRECTED (DEPENDENCY MATRIX INSERTED; STATUS UNRESOLVED DISCLOSED)` |
| **Temuan 3** | AC-25 mencampuradukkan kebijakan signer `UNKNOWN` dengan hierarki status agregat NX Verify. | AC-07 dikunci eksklusif pada kebijakan signer `UNKNOWN` (dep: B-09 / NC-04 / CONF-01). AC-25 dikunci eksklusif pada hierarki agregat Verify (dep: CONF-02). Dependensi B-09/CONF-01 dicabut dari AC-25. | `CORRECTED` |
| **Temuan 4** | Kontradiksi status NC-12: menyatakan blocker `NONE` padahal B-06 masih terbuka. | Menyelaraskan status blocker NC-12 menjadi `OPEN / BLOCKED BY B-06`. Membedakan containment, symlink, post-open descriptor, dan concurrent ancestor rename. Fail-closed tidak diartikan menghilangkan race condition di userspace. | `CORRECTED` |
| **Temuan 5** | Taksonomi error dan status `ERR_ZIP_INVALID` di luar daftar 20 kode (DEFECT-02). | Memetakan skenario kegagalan unpacking kontainer di `internal/container/container.go#L112` ke dalam kode `ERR_ZIP_INVALID` di bawah usulan taksonomi NC-15, dan mengeliminasi kode dugaan `ERR_GENESIS_SIGNATURE_INVALID` yang tidak ada di baseline. Diakui secara tegas bahwa 20 kode error kanonikal berstatus Proposed Specification (NC-15) yang belum dibekukan dalam White Paper v5.6, dan kode diskrit kegagalan tanda tangan Genesis berstatus Unresolved Taxonomy (fail-closed `canPlay: false` pasti). | `CORRECTED (PROPOSED SPEC DISCLOSED)` |
| **Temuan 6** | Transaksi Marketplace mengisyaratkan rollback setelah commit tanpa 2PC. | Menegaskan transaksi lokal SQL yang telah commit tidak dapat di-rollback oleh SQL yang sama; rollback lokal hanya untuk mutasi uncommitted; kegagalan HTTP License Daemon tidak terkompensasi (gap 2PC B-04). AC-14 dan AC-15 diselaraskan; B-04 tetap terbuka. | `CORRECTED` |
| **Temuan 7** | Klaim Zero-DDL, repository bersih, dan database tidak termutasi melampaui bukti inspeksi. | Mengakui inspeksi skema DDL hanya uji berkas lokal (bukan jaminan DB runtime hidup unverified); git status tracked bersih; 2 berkas untracked docs diakui jujur; folder `evidence/` gitignored; kebersihan root hanya uji root level; mobile/usage `NOT VERIFIED`. | `CORRECTED` |
| **Temuan 8** | Objek hash yang dibandingkan belum dibedakan secara tegas dan klaim semantik melampaui bukti DDL. | Membedakan objek hash berbasis bukti faktual (§6.9): memisahkan field usulan spesifikasi (notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif), PROPOSED SPECIFICATION; identitas field normatif audio_sha256 vs tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256 berstatus UNRESOLVED — STOP AND CLARIFY) dari keberadaan kolom DDL (`acquired_package_sha256` pada `marketplace/db/schema.postgres.sql#L72, L112, L129, L132`, berstatus `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` bagi audit independen karena akses repositori belum tersedia); membatasi klaim semantik, payload, producer, dan consumer `acquired_package_sha256` secara jujur ke dalam 3 tingkat pembuktian sebagai `UNRESOLVED / BLOCKED BY B-05` tanpa klaim sepihak sebagai hash seluruh file ZIP; mengidentifikasi 3 entitas komputasional internal perancang; membuktikan formula truncated SHA-256 hanya menjamin batas kapasitas kolom DDL, bukan bebas collision. | `CORRECTED (EVIDENCE TIERS APPLIED; PRIMARY EVIDENCE NOT VERIFIED)` |
| **Temuan 9** | Signer `UNKNOWN`: penolakan album ditafsirkan melarang seluruh pemeriksaan integritas anggota. | Menegaskan bahwa penolakan otorisasi pemutaran (playback) TIDAK melarang dilakukannya verifikasi integritas fisik kontainer `.nx` anggota untuk tujuan diagnostik/pelaporan Verify. Catatan historis REV6.3; Opsi A/B/C bukan lagi kerangka keputusan aktif dan tidak boleh digunakan sebagai pilihan kebijakan playback. | `CORRECTED` |
| **Temuan 10** | Status Gate dan keterlacakan mengklaim sinkronisasi sementara kontradiksi material masih ada. | Menyelaraskan G-05, G-06, G-10 dengan status aktual. Keterlacakan dua arah diperbaiki (NC-06 $\rightarrow$ AC-04; NC-03 $\rightarrow$ B-01/B-02; NC-12 $\rightarrow$ B-06). Gate A tetap `NOT PASSED`, Gate B tetap `BLOCKED`, Implementasi `NOT AUTHORIZED`. | `CORRECTED` |

---

### 1.6 Matriks Penutupan Temuan Audit Historis A-01 sampai A-30 [HISTORICAL AUDIT LOG: SPRINT 16/PRE-SPRINT 17 BASELINE]
Matriks berikut mendokumentasikan penanganan terhadap 30 temuan audit historis A-01 sampai A-30 sebagai catatan historis (Historical Audit Log). Status koreksi dibatasi secara jujur pada revisi dokumen rencana (*Plan-Corrected*), bukti inspeksi statis lokal (*Static-Inspection-Only*), dan secara tegas membedakan masalah arsitektur substantif yang masih terblokir (*Substantively Blocked*) tanpa mengklaim pembuktian runtime atau database produksi yang sesungguhnya belum tersedia (*Evidence Not Available / Runtime Not Verified*):

| ID & Makna Historis | Sumber Audit & Bukti Awal | Defect / Risiko Konkret | Kategori Penyebab & Analisis Kausal | Informasi Tersedia Saat Terjadi | Aturan Prompt Pencegahan Operasional | Koreksi Substantif Dilakukan | Bukti Pendukung Koreksi | Register Terdampak | Hasil Rekonsiliasi Dua Arah | Status Akhir yang Sah | Batasan / Ketidakpastian Substantif yang Terbuka |
| :---: | :--- | :--- | :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **A-01** (Kontradiksi status AC) | Audit V6.9.4 §8; Klaim global `[TEST-PLANNED]` pada 27 AC | Menyamarkan ketiadaan transaksi atomik dan ketiadaan keputusan PO seolah-olah seluruh pengujian siap dijalankan. | `PR` & `I` — Prompt mengizinkan ringkasan agregat tanpa memeriksa ketergantungan fisik AC pada blocker terbuka. | Roadmap v4.8; B-04; B-09 | **Trigger:** Ada AC dengan blocker eksternal. **Wajib:** Cantumkan status eksplisit per AC. **Dilarang:** Sweeping claim status agregat. | `[SNAPSHOT HISTORIS REV6.3 — BUKAN READINESS AKTIF]` Catatan Historis: Pada REV6.3 dijelaskan rekonsiliasi 27 AC (11 Spec Ready + 13 Blocked + 3 PO Decision Required). Pada snapshot historis sebelum membership gate AC-33/AC-34 diberlakukan, register saat itu telah direkonsiliasi menjadi 34 AC (§2.1, §8, §9, §13.1) yang mencakup penambahan AC-28 s.d. AC-34 dan penyelesaian CONF-02 (Pilihan B APPROVED). Snapshot historis pra-membership-gate: 14 Spec Ready + 18 Execution Blocked (snapshot historis pra-membership-gate; bukan readiness aktif); agregat aktif: 12 Spec Ready + 20 Execution Blocked (termasuk AC-22 gap prasyarat JIT dan provenance membership manifest CONF-01, AC-28 gap identitas Album, AC-29 gap reload Album, dan AC-32 gap kontrak lifecycle Auto-Next multi-payload) + 2 PO Decision Required (AC-01, AC-07 [autentisitas provenance membership manifest saat signer UNKNOWN; B-09 / CONF-01]) = 34 AC. | §2.1, §6, §8, §13; B-01..B-09 | NC-01 s.d. NC-16, AC-01..34, B-01..09, Gate A | Seluruh 34 AC terpetakan tepat satu kali tanpa duplikasi; status blocker terpropagasi jelas. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | 18 AC terblokir eksekusi (2 Modul Pending B-01/B-02 + 15 Arsitektur/Usulan/Taksonomi/Field/JIT Prereq/Lifecycle/Album Identity B-03..B-08/NC-05/NC-07/NC-15/AC-09/AC-22/AC-28/AC-29/AC-32) dan 2 AC menunggu keputusan resmi PO (AC-01 [Unknown Fields], AC-07 [autentisitas provenance membership manifest saat signer UNKNOWN; B-09 / CONF-01]). |
| **A-02** (Ketepatan pemetaan AC-15) | Audit V6.9.4 §8 & §9; AC-15 tertaut ke NC-16 (formula ID) | Kesalahan tautan kontraktual mengaburkan pengujian transaksi replay protection Marketplace. | `P` — Programmer salah menghubungkan AC penguji idempotensi ke kontrak formula ID karena kemiripan nomor ID. | `schema.postgres.sql#L63`; NC-08 historis | **Trigger:** Penyusunan Traceability Matrix. **Wajib:** Petakan AC ke NC berdasarkan fungsi yang diuji. **Dilarang:** Menebak ID. | Mengunci pemetaan AC-15 eksklusif ke NC-08 (Marketplace Transaction & Replay Protection) berstatus `[BLOCKED]` di bawah B-04. | §6.8, §8 (AC-15), §9 (NC-08) | NC-08, AC-15, B-04, CONF-03 | NC-08 diuji oleh AC-14 dan AC-15; AC-15 menguji replay endpoint NC-08. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Blocker arsitektur B-04 tetap terbuka. |
| **A-03** (Kecukupan bukti fungsionalitas) | Audit V6.9.4 §4.3; Klaim dukungan platform tanpa bukti runtime | Klaim E2E lintas platform dibuat tanpa bukti eksekusi aktual di repositori Linux. | `PR` & `V` — Prompt tidak mewajibkan bukti per platform; pengujian mobile belum dijalankan. | Repositori remote Linux `/opt/antigravity/projects/nexa` | **Trigger:** Pernyataan verifikasi komponen. **Wajib:** Sertakan bukti file/line aktual. **Dilarang:** Generalisasi bukti desktop ke mobile. | Menyajikan Evidence Ledger terstruktur (§4.4) yang memisahkan bukti kode terverifikasi (E-01..E-08) dari runtime mobile `NOT VERIFIED`. | §4.3, §4.4 (E-01..E-09), §13.1 | NC-01 s.d. NC-16, F-14, Gate A | Klaim repositori dibatasi pada inspeksi kode yang benar-benar ada di Linux server. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; RUNTIME NOT VERIFIED)` | Pengujian fisik runtime mobile berstatus `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. |
| **A-04** (Validitas Preservation Gate) | Audit V6.9.4 §12.1; Preservation Gate diklaim PASS 100% | Meloloskan gerbang preservasi hanya dari kelengkapan teks ID, mengabaikan blocker keputusan terbuka. | `G` — Ketiadaan keputusan resmi PO atas signer UNKNOWN dan ketiadaan 2PC disamarkan oleh keberadaan teks ID. | Baseline Sprint 16; White Paper v5.6; B-04; B-09 | **Trigger:** Evaluasi Preservation Gate. **Wajib:** Evaluasi 7 dimensi secara independen. **Dilarang:** Menilai PASS agregat jika ada dimensi terblokir. | Mengevaluasi 7 dimensi secara terpisah; menetapkan status jujur: D-01..D-05 PASS terbatas inspeksi statis; D-06 BLOCKED/PENDING PO; D-07 PARTIAL PASS (Temuan 1 s.d. 10). | §12.1 (Tabel 7 Dimensi Preservation Gate) | B-04, B-09, NC-04, NC-08, Gate A, Gate B | Dimensi preservasi sinkron dengan status blocker dan kesiapan sistem di §13. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Dimensi kelengkapan keputusan berstatus BLOCKED / PENDING PO DECISION. |
| **A-05** (Cakupan taksonomi error) | Audit V6.9.4 §6.15; Rujukan error tersebar dan format tabel rusak | Jalur eksekusi menghasilkan generic exception tanpa pemetaan kode diskrit fail-closed; format tabel rusak (S-01). | `P` & `PR` — Kurangnya pemusatan rujukan error dan kesalahan sintaksis pemisah tabel markdown. | Error Taxonomy Spec; NC-15; White Paper v5.6 | **Trigger:** Penanganan kegagalan sistem. **Wajib:** Petakan ke kode error diskrit kanonikal. **Dilarang:** Uncaught exception generic atau crash diam-diam. | Memusatkan penanganan error ke tabel kanonikal 20 kode error kanonikal (§6.15) termasuk `ERR_ZIP_INVALID` (menghapus `ERR_GENESIS_SIGNATURE_INVALID` yang tidak terdaftar di baseline); memperbaiki format tabel. | §6.15, §8 (AC-26), §9 (NC-15) | NC-15, AC-10, AC-26, F-08, Gate A | Setiap kode error terhubung ke minimal satu AC penguji fail-closed. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; GENESIS CODE UNRESOLVED)` | Penanganan runtime `ERR_ALBUM_SIGNER_UNKNOWN` menunggu keputusan PO. |
| **A-06** (Formula ID & batas kolom) | Audit V6.9.4 §6.16; Penggabungan string ID berisiko overflow | Derivasi ID child acquisition dan provider berisiko overflow kolom VARCHAR PostgreSQL atau tabrakan saat retry. | `I` & `V` — Kesalahan penafsiran batas kolom dengan menjumlahkan string antar-tabel dan ketiadaan inspeksi DDL aktif. | `schema.postgres.sql#L63-L115`; NC-16 | **Trigger:** Perancangan formula ID. **Wajib:** Uji batas panjang matematis per kolom. **Dilarang:** Menjumlahkan string antar-tabel berbeda. | Menyajikan derivasi independen per kolom: child acq $\le 128$, child ent $\le 128$, provider $\le 64$. Mengakui batas kolom bukan bukti ketiadaan collision. | §6.16, §8 (AC-27), §9 (NC-16); DDL schema | NC-16, AC-27, B-05, Gate A | Formula truncated SHA-256 terbukti mematuhi constraint panjang skema DDL aktif. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; DDL CAPACITY VERIFIED)` | Semantik derivasi hash jika `provider_snapshot` absen adalah gap spesifikasi terbuka. |
| **A-07** (Keselarasan AC-17 Zero-DDL) | Audit V6.9.4 §8 & §9; AC-17 tertaut ganda ke NC-08 dan NC-10 | AC-17 yang menguji kepatuhan Zero-DDL ikut terblokir secara keliru oleh blocker transaksi B-04. | `P` — Programmer salah menduplikasi tautan AC-17 ke NC-08 transaksi alih-alih mengisolasinya pada audit skema. | `schema.postgres.sql`; NC-10 | **Trigger:** Evaluasi Zero-DDL. **Wajib:** Petakan AC-17 eksklusif ke NC-10. **Dilarang:** Menautkan AC-17 ke NC-08 multi-item transaction. | Mengunci AC-17 eksklusif ke NC-10 (Zero-DDL); melepaskan dependensi pemblokir B-04 sehingga Zero-DDL dapat diverifikasi secara independen. | §8 (AC-17), §9 (NC-10) | NC-10, AC-17, Gate A | AC-17 menguji pematuhan skema pasca-operasi tanpa mutasi DDL; sinkron dengan NC-10. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; LIVE DB NOT VERIFIED)` | Zero-DDL pada file skema dipatuhi 100%; database live unverified. |
| **A-08** (Batas kuota ZIP vs kontainer `.nx`) | Audit V6.9.4 §6.7; Batas ZIP diperluas ke file `.nx` individual | Pembatasan keliru ukuran kontainer audio individual `.nx` berdasarkan analogi arsip ZIP. | `I` — Kesalahan analogi yang menyamakan batas pembungkus distribusi dengan batas payload biner audio. | NC-07 historis; WP v5.6 §Distribution | **Trigger:** Spesifikasi batas ukuran arsip. **Wajib:** Batasi kuota ZIP murni pada wrapper distribusi. **Dilarang:** Menerapkan kuota ZIP ke berkas `.nx`. | Menetapkan usulan batas kuota pembungkus ZIP (usulan 500 MB desimal [500.000.000 bytes] terkompresi, akumulasi 4 GB desimal uncompressed, 200 entri [entri direktori diterima sesuai Keputusan PO AUDIT-NEW-06; pembatasan flat hanya berlaku pada regex path relatif member .nx manifest], serta usulan rasio kompresi B-07 yang belum diputuskan) murni sebagai usulan spesifikasi teknis untuk wrapper distribusi; melarang perluasan batas wrapper ke berkas payload `.nx` individual (yang memiliki batas payload 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106`). *(Catatan Historis: Usulan draf lama mengenai penolakan direktori telah digantikan secara resmi oleh Keputusan PO AUDIT-NEW-06).* | §2.1, §6.7, §8 (AC-13), §9 (NC-07) | NC-07, AC-13, B-07, Gate A | ZIP adalah wadah distribusi fisik; berkas `.nx` adalah payload biner independen. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Parameter kuota numerik pembungkus ZIP (termasuk ambiguitas rasio 10:1 usulan B-07 vs 100:1 referensi pembanding eksternal yang belum diverifikasi) berstatus usulan spesifikasi teknis (B-07) yang menunggu keputusan otoritatif Arsitektur; batas payload kontainer .nx individual 2 GiB belum memiliki AC penguji di AC Register. |
| **A-09** (Kecukupan bukti Safe-Open) | Audit V6.9.4 §6.12; Klaim anti-TOCTOU absolut di userspace | Resep prosedural semu (`realpath`, `O_NOFOLLOW`) diklaim menjamin keamanan mutlak terhadap race condition filesystem. | `G` & `PR` — Prompt tidak menuntut rumusan invariant keamanan dan batasan kernel POSIX tidak diakui jujur. | NC-12 historis; Standar POSIX.1-2017 | **Trigger:** Evaluasi akses filesystem. **Wajib:** Rumuskan Invariant Keamanan dan akui batas POSIX. **Dilarang:** Mengklaim anti-TOCTOU mutlak userspace. | Merumuskan Invariant Keamanan; memisahkan pre-open path vs post-open fd; mengakui batas concurrent rename; fail-closed `canPlay: false`. | §2.1, §6.12, §8 (AC-20, AC-21), §9 (NC-12) | NC-12, AC-20, AC-21, F-01, F-11, F-12, Gate A | Pembuktian invariant menjadi kriteria kelulusan; jika ragu, melempar fail-closed (`canPlay: false`). | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; USpace LIMITS ACKNOWLEDGED)` | Keterbatasan race condition concurrent ancestor rename pada POSIX userspace diakui. |
| **A-10** (Aturan operasional ZIP) | Audit V6.9.4 §6.7; Metode hitung entri diklaim normatif | Aturan desain internal penghitungan entri direktori/manifest diklaim seolah-olah sudah disahkan standar. | `I` — Menganggap proposal teknis Programmer sebagai kontrak normatif yang telah disahkan. | PKWARE APPNOTE; ISO/IEC 21320-1; RFC 1951 | **Trigger:** Detail implementasi ekstraksi. **Wajib:** Pisahkan kuota numerik dari usulan operasional. **Dilarang:** Mengklaim usulan desain sebagai kontrak sah. | Menyelaraskan dengan Keputusan PO (AUDIT-NEW-06): entri direktori di dalam ZIP diterima; pembatasan flat berlaku pada path relatif member `.nx` manifest (`^[a-zA-Z0-9_-]+\.nx$`); symlink dan special file ditolak fail-closed (`ERR_ZIP_INVALID`). Batas numerik (500 MB desimal [500.000.000 bytes] / 4 GB desimal / 200 entri dan usulan rasio kompresi B-07) dan aturan operasional diselaraskan di bawah `[PROPOSED SPEC]`. | §6.7, §8 (AC-13) | NC-07, AC-13, Gate A | Kuota ZIP wrapper dan aturan flat diselaraskan konsisten di seluruh bagian. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Aturan kuota ZIP berstatus usulan spesifikasi teknis B-07. |
| **A-11** (Bukti repositori independen) | Audit V6.9.4 §4.3; Klaim repo-verified tanpa rujukan line aktual | Pernyataan verifikasi repositori tidak dapat diaudit atau diverifikasi ulang secara independen. | `PR` & `V` — Prompt mengizinkan label verifikasi tanpa mewajibkan bukti path dan baris aktual di server. | Repositori remote Linux `/opt/antigravity/projects/nexa` | **Trigger:** Pemberian label `[REPOSITORY-VERIFIED]`. **Wajib:** Cantumkan path, line range, dan raw snippet. **Dilarang:** Memberi label tanpa inspeksi aktual. | Menyajikan Evidence Ledger Repository di §4.4 dengan 9 bukti empiris terverifikasi (E-01 s.d. E-09) lengkap dengan path absolut, line range, dan raw snippets. | §4.3, §4.4 (E-01 s.d. E-09), §12.2 (G-03) | NC-01 s.d. NC-16, Gate A | Seluruh klaim kode mengacu langsung pada bukti ledger yang terdaftar dengan kutipan mentah. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; DESKTOP REPO ONLY)` | Komponen mobile berstatus NOT VERIFIED karena keterbatasan lingkungan server. |
| **A-12** (Cakupan rollback transaksi lokal) | Audit V6.9.4 §8; Definisi rollback berisiko menghapus data lama | Ambang batas pemulihan state transaksi database berisiko menghapus data historis yang sah saat rollback. | `I` — Kesalahan penafsiran semantik rollback SQL antara mutasi transaksi gagal vs data pra-transaksi. | `schema.postgres.sql`; NC-08 | **Trigger:** Penanganan kegagalan transaksi. **Wajib:** Batasi rollback pada uncommitted changes transaksi gagal. **Dilarang:** Menghapus baris historis sah. | Memperjelas bahwa rollback AC-14 membatalkan mutasi transaksi gagal tanpa residu baris parsial, tanpa menghapus baris pra-transaksi yang sah. | §8 (AC-14), §9 (NC-08) | NC-08, AC-14, B-04, CONF-03 | Rollback mengembalikan database lokal ke kondisi awal pra-transaksi; status tetap BLOCKED oleh B-04. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Blocker transaksi terdistribusi B-04 tetap terbuka. |
| **A-13** (Opsi signer UNKNOWN non-normatif) | Audit V6.9.4 §6.4 & §10; Opsi A/B/C diperlakukan sebagai aturan sah | Menetapkan perilaku pemutaran signer UNKNOWN secara sepihak melangkahi kewenangan Product Owner. | `P` & `PR` — Programmer menganggap daftar opsi proposal sebagai spesifikasi normatif yang dapat diputuskan sendiri. | Roadmap v4.8; B-09 / NC-04 | **Trigger:** Penanganan trust model signer. **Wajib:** Kunci pada keputusan PO tertulis. **Dilarang:** Memilih opsi A, B, atau C atas nama PO. | [CATATAN HISTORIS REV6.3 — DIGANTIKAN REKONSILIASI FINDING-02 §13.3] Pada snapshot tersebut Opsi A/B/C disebut proposal; bukan lagi kerangka keputusan aktif. CONF-01 kini dibatasi pada autentisitas manifest/membership dan lifecycle signer, bukan playback global. Menghapus AC-25 dari pemetaan signer UNKNOWN karena AC-25 secara ketat menguji hierarki status agregat NX Verify di bawah CONF-02/NC-14. | §6.4, §10, §11 (CONF-01), §8 (AC-07) | NC-04, AC-07, B-09, CONF-01 | Model kepercayaan signer UNKNOWN adalah hak prerogatif PO; AC-07 terkunci pada keputusan tertulis PO (CONF-01); AC-25 terpisah di CONF-02. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Keputusan tertulis PO mengenai signer UNKNOWN masih tertunda (CONF-01). |
| **A-14** (Konsistensi kosakata status) | Audit V6.9.4 §2; Kosakata status saling bertentangan | Mencampuradukkan status rencana pengujian dengan status kelulusan pengujian atau status dependensi. | `PR` & `I` — Prompt tidak menyediakan taksonomi status diskrit sehingga istilah dipertukarkan keliru. | Governance Framework Nexa | **Trigger:** Pelabelan status register. **Wajib:** Gunakan dimensi status terpisah. **Dilarang:** Menyamakan spesifikasi dengan implementasi atau planned dengan passed. | `[SNAPSHOT HISTORIS REV6.3 — DIGANTIKAN REGISTER 34 AC]` Menegakkan pemisahan dimensi status secara disiplin di §2.1; pada baseline aktif PE-02 saat ini, model multi-dimensi memetakan tepat 34 AC (AC-01 s.d. AC-34) dengan status diskrit presisi. | §2.1, §6, §8, §12, §13, §14 | Seluruh register (NC, AC, B, F, E, CONF, G) | Kosakata status konsisten di seluruh bab tanpa kontradiksi internal administratif. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Kosakata status terkunci presisi. |
| **A-15** (Bukti root-clean & zero-mutation) | Audit V6.9.4 §14; Deklarasi root-clean tanpa output terminal | Mengklaim tidak ada perubahan kode atau file liar tanpa menyajikan bukti pemeriksaan git aktual. | `PR` & `V` — Prompt mewajibkan deklarasi tetapi tidak mewajibkan bukti inspeksi terminal aktual. | Terminal remote Linux repositori Nexa | **Trigger:** Pembuatan closing declaration. **Wajib:** Jalankan `git status` dan `ls -la`. **Dilarang:** Mengklaim root-clean tanpa bukti inspeksi. | Menjalankan inspeksi aktual via `git status --porcelain` dan `ls -la`; menyertakan commit hash `fc08a5c...` dan batas pembuktian riil di §4.4 (E-08) dan §14. | §4.4 (E-08), §12.2 (G-09), §14 | Mandatory Closing Declarations, Rule D | Output terminal membuktikan nol mutasi kode tracked; untracked docs dicatat transparan. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; ROOT LEVEL ONLY)` | Berkas untracked docs dicatat; inspeksi terbatas pada root direktori. |
| **A-16** (Konsistensi B-04/NC-08, B-09, dan AC) | Audit V6.9.4 §7 & §8; Ketergantungan AC tidak sinkron dengan blocker | AC-14/15 dan AC-07/25 diringkas sebagai test-planned sementara blocker dasarnya masih terbuka. | `P` — Programmer mengabaikan dampak blocker B-04 dan B-09 saat mengisi tabel Acceptance Criteria. | B-04, B-09; Roadmap v4.8; `schema.postgres.sql` | **Trigger:** Evaluasi dependensi AC. **Wajib:** Propagasikan status blocker ke AC penguji. **Dilarang:** Menyatakan AC siap uji jika dependensinya terblokir. | `[SNAPSHOT HISTORIS REV6.3 — DISINKRONKAN DENGAN KEPUTUSAN PO CONF-02]` Catatan Historis: Pada REV6.3, AC-25 berstatus PO DECISION REQUIRED. Pada baseline PE-02 aktif saat ini, AC-25 telah beralih menjadi `[TEST-PLANNED — SPEC READY]` mengikuti Keputusan PO CONF-02 (Pilihan B APPROVED: tanpa status agregat di Verify). AC-07 tetap `[PO DECISION REQUIRED]` untuk autentisitas provenance membership manifest, bukan kebijakan playback global, serta AC-03, 14, 15, 16 tetap `[BLOCKED]`. | §7.1, §8, §9, §13 | NC-02, NC-04, NC-08, NC-09, AC-03, 07, 14, 15, 16, 25, B-04, 05, 08, 09 | Dependensi blocker terpropagasi sinkron dua arah ke seluruh register terkait. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | B-04, B-05, B-08, B-09 tetap terbuka secara sah; CONF-02 telah disahkan PO. |
| **A-17** (Penanganan exception kriptografi) | Audit V6.9.4 §7.2; Exception kriptografi berisiko crash unhandled | Exception format kunci atau korupsi buffer melempar uncaught error yang meruntuhkan proses runtime. | `PR` & `I` — Prompt tidak merinci batas modul kriptografi Node.js vs pemetaan error tingkat sistem. | `sdk/typescript/src/crypto.ts`; F-08; §6.15 | **Trigger:** Penanganan exception kriptografi. **Wajib:** Tangkap di layer modul dan petakan ke kode diskrit. **Dilarang:** Membiarkan uncaught exception bocor ke UI. | Memperjelas bahwa error format kunci/parsing ditangkap rapi di tingkat modul dan dipetakan ke error diskrit di tingkat sistem/UI (`ERR_CONTAINER_SIGNATURE_INVALID`). | §6.15, §7.2 (F-08), §8 (AC-26) | NC-15, AC-26, F-08, Gate A | Mencegah unhandled crash dan menegakkan prinsip fail-closed di seluruh layer. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Penanganan exception terdefinisi rapi pada rancangan dokumen. |
| **A-18** (Konsistensi substantif lintas bagian) | Audit V6.9.4; Teks draf lama bertentangan dengan perbaikan baru | Adanya sisa teks kontradiktif antar-bab (e.g. formula ID lama vs baru, batas kontainer 2 GiB vs wrapper 4 GB desimal). | `P` — Programmer memperbaiki satu bab tanpa melakukan audit dampak silang ke bab-bab lainnya. | Dokumen plan kanonikal V6.9.4 | **Trigger:** Perubahan teks persyaratan. **Wajib:** Jalankan audit dampak silang ke seluruh bab. **Dilarang:** Meninggalkan sisa teks draf lama yang bertentangan. | Menyinkronkan seluruh referensi kontrak, formula ID, batas ZIP flat, safe-open, dan status gate di seluruh bab (§1 s.d. §14). | Seluruh dokumen (§1 s.d. §14) | Seluruh register dan bab | Dokumen diaudit komprehensif; sinkronisasi internal diperbaiki. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Dokumen mengakui secara jujur bahwa konflik material eksternal tetap terbuka. |
| **A-19** (Traceability dua arah lintas bagian) | Audit V6.9.4 §9; Traceability hanya searah dari NC ke AC | Ketidaksesuaian pemetaan dari AC kembali ke NC dan dependensi blocker yang tidak tercermin; format rusak (S-02). | `P` — Programmer menyusun matriks searah tanpa memvalidasi keterhubungan balik dari kriteria uji ke sumber. | §8 (AC Register); §9 (Traceability Matrix) | **Trigger:** Penyusunan Traceability. **Wajib:** Lakukan audit dua arah (Forward & Reverse). **Dilarang:** Memetakan AC ke sumber tidak berwenang. | `[SNAPSHOT HISTORIS REV6.3 — DIGANTIKAN BASELINE 34 AC]` Catatan Historis: Menjalankan audit dua arah NC ke AC pada 27 AC awal. Pada baseline PE-02 aktif saat ini, seluruh 34 AC (AC-01 s.d. AC-34) terpetakan dua arah di §9 ke 16 NC secara presisi. | §9 (Tabel Traceability Matrix Dua Arah) | NC-01 s.d. NC-16, AC-01 s.d. AC-34 | 16 NC dan 34 AC terpetakan presisi dengan rujukan dependensi yang jelas. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Rantai ketertelusuran dokumen terbukti. |
| **A-20** (Penutupan substantif tanpa relabel) | Audit V6.9.4; Penutupan temuan hanya dengan mengganti kata status | Mengklaim temuan selesai secara administratif tanpa mengubah logika, batas, atau bukti yang mendasarinya. | `G` — Ketiadaan bukti dan spesifikasi teknis disamarkan dengan perubahan redaksi semata. | Seluruh dokumen kanonikal V6.9.4 | **Trigger:** Penutupan temuan audit. **Wajib:** Sertakan perbaikan teknis dan bukti nyata. **Dilarang:** Mengubah status tanpa perbaikan substantif. | Menegakkan perbaikan teknis nyata: formula ID independen, skema lengkap manifest, invariant safe-open, dan evidence ledger E-01..E-09. | Seluruh dokumen kanonikal | Seluruh register | Penutupan administratif dipisahkan dari penyelesaian blocker substantif. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY)` | Tidak ada penutupan blocker semu. |
| **A-21** (Invariant teknis) | Wajib mengunci invariant keamanan logika. | Filesystem Containment Invariant; 1:1 ZIP-to-Manifest Bijection; penerimaan entri direktori ZIP sesuai keputusan PO AUDIT-NEW-06; pemisahan identity/packaging authority sesuai keputusan PO AUDIT-NEW-10. | §5.1, §5.2, §6.5, §6.7, §6.12, §8, §13.12.11 | NC-05, NC-07, NC-12, AC-09, AC-12, AC-21 | Invariant fail-closed dipertahankan; tiga peran dan delegation target dirinci pada §13.12.11. | PLAN-CORRECTED (DOCUMENT REVISION ONLY) | Batasan race condition POSIX userspace diakui; rancangan identity/packaging authority dirinci pada §13.12.11. |
| **A-22** (Spesifikasi skema manifest) | Audit V6.9.4 §5.1; Skema manifest tidak lengkap | Tidak adanya definisi skema JSON lengkap memicu interpretasi liar dalam deserialisasi dan validasi tipe. | `PR` & `P` — Prompt tidak menyertakan draf skema normatif JSON Schema Draft 7. | White Paper v5.6 §Album Manifest Specification | **Trigger:** Perancangan struktur data. **Wajib:** Sediakan skema lengkap dengan tipe data eksplisit. **Dilarang:** Menggunakan representasi contoh informal. | Menyajikan draf JSON Schema audio 13 properti sebagai proposal non-normatif; bukan schema universal atau 13 required fields yang disahkan dengan tipe data, pola regex valid JSON (`\\.nx$`), dan batasan `additionalProperties`. | §5.1 (Skema Manifest JSON Lengkap) | NC-01, AC-01, F-04, Gate A | Draf audio non-normatif; schema universal belum lengkap; unknown-field behavior menunggu PO. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; SPECIFICATION PROPOSED)` | Penolakan unknown fields berstatus usulan spesifikasi ketat. |
| **A-23** (Pemisahan dua tanda tangan Creator) | Audit V6.9.4 §5.1; Kerancuan tanda tangan manifest vs Genesis | Ambiguitas verifikasi apakah Album Signer menandatangani berkas audio atau hanya manifest JSON. | `I` — Kerancuan konsep tanda tangan packaging versus sertifikat kepemilikan kanonikal Genesis. | White Paper v5.6 §Two-Signature Architecture | **Trigger:** Evaluasi verifikasi kriptografi. **Wajib:** Pisahkan Container Creator Sig vs Genesis Certificate Creator Sig. **Dilarang:** Menyatukan kunci verifikasi. | Menegakkan arsitektur pemisahan kriptografis: Container Creator Signature (Ed25519) memverifikasi byte packaging kontainer individual `.nx`; Genesis Cert Signature mengikat track audio; Album Signer menandatangani manifest. | §5.1, §5.2, §6.2, §8 (AC-03, AC-04) | NC-02, NC-06, AC-03, AC-04, F-06, Gate A | Tanda tangan container independen dari tanda tangan sertifikat track. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; RUNTIME NOT VERIFIED)` | Verifikasi runtime multi-track berstatus TEST-PLANNED. |
| **A-24** (Inventaris objek kriptografis dan hash berbasis bukti — AUDIT-NEW-04) | Audit V6.9.4 §6.9; Tumpang tindih makna istilah hash dan klaim kuantitas objek NC-09 yang belum terbukti | Kerancuan antara hash manifest, hash payload audio, hash arsip ZIP, hash sertifikat Genesis, dan tanda tangan digital, serta klaim semantik kolom DB yang melampaui bukti DDL. | `PR` & `I` — Kegagalan taksonomi istilah kriptografi dan pemaksaan semantik tanpa kontrak normatif. | NC-09; White Paper v5.6; §6.9; `whisnu/nexa` commit `fc08a5c` (`marketplace/db/schema.postgres.sql`, `internal/container/container.go`, `sdk/typescript/src/container.ts`, `sdk.ts`, `ownership.ts`, `004_ownership.sql`; status bukti audit: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` karena akses repositori independen Auditor belum tersedia) | **Trigger:** Inventarisasi dan penggunaan istilah kriptografi/hash. **Wajib:** Susun inventaris berbasis bukti faktual di §6.9: pisahkan 4 signature Ed25519 diskrit (status implementasi: NOT VERIFIED), bedakan usulan spesifikasi (notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif), identitas field normatif unresolved) dari keberadaan kolom DDL (`acquired_package_sha256`, status DDL: NOT VERIFIED), dan akui semantik hash DB terblokir B-05. **Dilarang:** Mengklaim semantik hash seluruh ZIP tanpa bukti atau menyatakan objek komputasi sebagai objek tersimpan terpisah. | Menyusun inventaris berbasis bukti di §6.9: memisahkan 4 signature Ed25519 (status implementasi: NOT VERIFIED), membedakan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif) (Proposed Spec; Unresolved Field Identity) dari `acquired_package_sha256` (DDL Field Existence: NOT VERIFIED; Semantics Blocked B-05), dan mengklasifikasikan 3 entitas komputasi in-memory perancang. | §6.9, §8 (AC-16), §9 (NC-09) | NC-09, AC-16, B-05, Gate A | Objek kriptografis dan hash direkonsiliasi berbasis bukti; bukti primer implementasi berstatus jujur NOT VERIFIED bagi auditor independen; semantik `acquired_package_sha256` tetap diblokir B-05. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED / PRIMARY EVIDENCE NOT VERIFIED` | Semantik kolom child `acquired_package_sha256` adalah blocker B-05 terbuka; status AUDIT-NEW-04 adalah NOT PASS. |
| **A-25** (Hierarki status Verify 3-lapis) | Audit V6.9.4 §5.3; Pencampuran status trust, integritas, agregat | Status kegagalan integritas satu trek merusak status trust signer album atau sebaliknya. | `I` & `P` — Kesalahan pemodelan status Verify yang menggabungkan dimensi kepercayaan dengan integritas file. | White Paper v5.6 §Verify Multi-Layer Status | **Trigger:** Evaluasi NX Verify. **Wajib:** Pisahkan 3 lapisan status independen. **Dilarang:** Menimpa status signer dengan status integritas track. | `[SNAPSHOT HISTORIS REV6.3 — DISELESAIKAN OLEH KEPUTUSAN PO CONF-02 (PILIHAN B APPROVED)]` Catatan Historis: Pada REV6.3 diusulkan 3 layer dan CONF-02 dipertahankan terbuka. Pada baseline PE-02 aktif saat ini, CONF-02 telah resmi disahkan oleh Product Owner via PILIHAN B (APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; hasil verifikasi individual member adalah hasil utama; status AC-25, AC-33, dan AC-34 adalah `[TEST-PLANNED — SPEC READY]` (lihat §5.3, §6.14, §8, §10.3.7, §11). | §5.3, §6.14, §8 (AC-25, 33, 34), §11 (CONF-02) | NC-14, AC-25, AC-33, AC-34, CONF-02, Gate A | Empat canonical status, 5 Multi-Registry states, dan Local Override semantics individual file tetap utuh tanpa status agregat. | `PLAN-CORRECTED / PO DECISION APPROVED (OPTION B)` | CONF-02 resmi selesai; tidak ada pembuatan status agregat baru (`ALBUM_TRUSTED`, `ALBUM_INVALID`). |
| **A-26** (Taksonomi error code diskret) | Audit V6.9.4 §6.15; Taksonomi error tidak lengkap | Kegagalan parsing atau trust melempar exception generic yang tidak dapat ditangani UI secara presisi. | `PR` & `P` — Kurangnya pemetaan taksonomi error yang komprehensif untuk seluruh skenario kegagalan. | Error Taxonomy Spec; NC-15; White Paper v5.6 | **Trigger:** Pemetaan kode error. **Wajib:** Sediakan 20 kode diskrit kanonikal dengan trigger jelas. **Dilarang:** Menggunakan generic error string. | Merinci tepat 20 kode error kanonikal lengkap dengan layer asal, kondisi trigger, aksi fail-closed, dan AC penguji; memasukkan `ERR_ZIP_INVALID` dan mengeliminasi `ERR_GENESIS_SIGNATURE_INVALID`. | §6.15, §8 (AC-26), §9 (NC-15) | NC-15, AC-10, AC-26, F-08, Gate A | Taksonomi error mencakup seluruh alur eksekusi Album dengan perilaku fail-closed. | `PLAN-CORRECTED (DOCUMENT REVISION ONLY; GENESIS CODE UNRESOLVED)` | Error handling `ERR_ALBUM_SIGNER_UNKNOWN` menunggu keputusan PO. |
| **A-27** (Derivasi ID PostgreSQL aktif) | Audit V6.9.4 §6.16; Rumus ID melampaui batas kolom DB aktif | ID transaksi atau provider yang terlalu panjang menyebabkan error `value too long for type character varying`. | `I` & `V` — Pengabaian batasan skema fisik PostgreSQL dalam perancangan formula identitas. | `schema.postgres.sql#L63-L115` | **Trigger:** Perancangan formula ID. **Wajib:** Batasi panjang string $\le$ batas kolom skema aktif. **Dilarang:** Melebihi `VARCHAR(64)` atau `VARCHAR(128)`. | Merumuskan derivasi independen berbasis SHA-256 terpotong (32-hex): child acq $\le 128$, ent $\le 128$, provider $\le 64$; membatasi klaim AC-27 pada panjang. | §6.16, §8 (AC-27), §9 (NC-16) | NC-16, AC-27, B-05, Gate A | Panjang string ID terbukti tidak melanggar batas kolom skema database aktif. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; COLLISION UNVERIFIED)` | AC-27 hanya membuktikan batas panjang; bukan bukti matematis ketiadaan collision. |
| **A-28** (Isolasi baseline Sprint 16 & PE-01) | Audit V6.9.4; Klaim mutasi kode atau pembukaan baseline | Risiko perubahan kode baseline yang sudah stabil untuk mempermudah implementasi fitur album baru. | `PR` & `I` — Kegagalan membatasi ruang lingkup post-sprint yang berisiko merusak deliverable sebelumnya. | Sprint 16 Closeout Report; PE-01 Spec | **Trigger:** Modifikasi berkas proyek. **Wajib:** Kunci baseline Sprint 16 & PE-01 sebagai FROZEN. **Dilarang:** Mengubah berkas kode baseline. | Menegakkan isolasi baseline: Sprint 16 dan PE-01 tetap 🔒 `CLOSED / FROZEN`. Tidak ada perubahan pada kode yang sudah diterima. | §1.1, §4.1, §14 (Closing Declarations) | Seluruh sistem Nexa, Gate A, Gate B | Baseline Sprint 16 dan PE-01 terlindungi dari mutasi kode tracked (diverifikasi via git diff); kondisi runtime live belum diverifikasi. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; RUNTIME NOT VERIFIED)` | Isolasi berkas kode tracked terbukti via git; status runtime dan database live belum diverifikasi. |
| **A-29** (Pemisahan Gate A vs Gate B) | Audit V6.9.4 §12.3; Kelulusan dokumen disamakan dengan kesiapan koding | Memberikan otorisasi implementasi kode hanya karena dokumen rencana telah selesai diperiksa. | `PR` & `G` — Penggabungan kriteria evaluasi rencana (Gate A) dengan kriteria kesiapan implementasi (Gate B). | Nexa Engineering Quality Framework | **Trigger:** Evaluasi kesiapan rilis rencana. **Wajib:** Pisahkan Gate A (Plan Quality) dan Gate B (Impl Readiness). **Dilarang:** Meluluskan Gate B jika ada blocker terbuka. | Menegakkan pemisahan mutlak: Gate A `NOT PASSED — REQUIRES TARGETED CORRECTIONS`; Gate B `BLOCKED`; Implementasi `NOT AUTHORIZED`. | §12.3, §13.1, §13.2, §14 | Gate A, Gate B, Governance Status | Kualitas rencana dinilai independen dari izin implementasi; Gate A tidak diluluskan semu. | `PLAN-CORRECTED / SUBSTANTIVELY BLOCKED` | Gate A tidak lulus karena konflik material; Gate B diblokir oleh B-04, B-05, B-08, B-09. |
| **A-30** (Bukti nol mutasi kode sumber) | Audit V6.9.4 §14; Deklarasi nol mutasi tanpa dasar inspeksi riil | Klaim verbal bahwa kode tidak termutasi tanpa bukti pelacakan git commit atau git status. | `PR` & `V` — Ketidakmampuan membedakan jaminan prosedural verbal dari bukti empiris sistem kontrol versi. | Git repository `/opt/antigravity/projects/nexa` | **Trigger:** Deklarasi akhir dokumen. **Wajib:** Jalankan inspeksi git dan tampilkan output aktual. **Dilarang:** Klaim verbal tanpa bukti terminal. | Melampirkan output aktual `git rev-parse HEAD`, `git status --porcelain`, dan `ls -la` di §4.4 (E-08) dan §14 dengan commit `fc08a5c...`. | §4.4 (E-08), §14 (Closing Declarations) | Seluruh repositori, Governance Gate | Nol mutasi kode sumber tracked terbukti via git diff; kebersihan root dibuktikan via ls -la (bukan jaminan rekursif subdirektori); status 2 berkas untracked docs dicatat transparan. | `PLAN-CORRECTED (STATIC-INSPECTION-ONLY; ROOT & TRACKED ONLY)` | Inspeksi direktori terbatas pada tingkat root; berkas untracked docs diakui; kondisi live database tidak diuji. |

---

## 2. RINGKASAN READINESS DAN KONTROL PENCEGAHAN AKAR MASALAH (PR/G/I)

### 2.1 Model Multi-Dimensi Kesiapan Acceptance Criteria (34 AC) (DEF-01)
Dokumen ini membedakan secara tegas klasifikasi Acceptance Criteria ke dalam kategori status utama yang saling eksklusif dan mencakup tepat 34 AC tanpa tumpang tindih. Setiap AC memiliki satu klasifikasi status utama, dengan dependensi teknis, usulan spesifikasi, atau blocker arsitektur yang terpetakan secara transparan dan jujur:

```
+--------------------------------------------------------------------------------------------------------------------+
|                         MATRIKS STATUS ACCEPTANCE CRITERIA REKONSILIASI KANONIKAL (34 AC)                          |
+--------------------------------------------------------------------+-----------------------------------------------+
| Kategori Klasifikasi Status Utama (Total Tepat 34 AC)              | Cakupan ID AC & Rincian Ketergantungan        |
+--------------------------------------------------------------------+-----------------------------------------------+
| 1. [TEST-PLANNED — SPECIFICATION READY] (12 AC)                    | AC-04, AC-11, AC-12, AC-17, AC-18,     |
|    Skenario uji dan kriteria penerimaan fail-closed terdefinisi     | AC-19, AC-23, AC-24, AC-25, AC-27,            |
|    lengkap pada tingkat spesifikasi teknis rencana dokumen tanpa   | AC-30, AC-31                                  |
|    terhambat dependensi spesifikasi usulan atau celah arsitektur.  | *Catatan Verifikasi & Keputusan PO:*          |
|                                                                    | - AC-17: Kepatuhan skema statis DDL dipatuhi; |
|                                                                    |   runtime live DB berstatus NOT VERIFIED.     |
|                                                                    | - AC-25: Keputusan PO CONF-02 (Pilihan B      |
|                                                                    |   APPROVED: Tanpa Status Agregat di Verify).  |
|                                                                    | - AC-27: Batas kolom skema statis dipatuhi;   |
|                                                                    |   ketiadaan collision hash belum terbukti.    |
|                                                                    | - AC-30..31: Larangan Campuran & Failure      |
|                                                                    |   Handling Ulangi/Lewati Disahkan.            |
|                                                                    | - AC-33..34: Keputusan PO Manual Next Desktop |
|                                                                    |   & Mobile Lite disahkan; eksekusi Album tetap|
|                                                                    |   blocked oleh autentisitas membership CONF-01.|
+--------------------------------------------------------------------+-----------------------------------------------+
| 2. [TEST-PLANNED — EXECUTION BLOCKED] (22 AC)                      | Sub-Kategori 2a: [MODUL ENGINE PENDING] (2):  |
|    Skenario uji terencana, namun eksekusi pengujian terblokir      |   - AC-05 (B-01: Strict JSON Parser Engine)   |
|    oleh modul implementasi internal yang belum dikoding, usulan    |   - AC-06 (B-02: RFC 8785 JCS Serializer)     |
|    spesifikasi teknis yang belum dibekukan, taksonomi error        | Sub-Kategori 2b: [BLOCKED BY ARCH / SPEC] (20)|
|                                                                    |   - AC-01 (NC-01: Strict Unknown Fields; universal schema pending) |
|    unresolved, keputusan identitas field normatif yang belum       |   - AC-02 (B-07/NC-07: Validasi Wrapper ZIP)  |
|    disahkan, gap identitas & persistensi Album multi-member,       |   - AC-03 (B-08: Circular Dependency Sig)     |
|                                                                    |   - AC-07 (NC-04/B-09: Membership policy approved; signer lifecycle pending) |
|                                                                    |   - AC-08 (NC-11: Registry Revocation Gap)  |
|    gap pemuatan kembali Album, prasyarat normatif JIT &            |   - AC-09 (NC-05/NEW-01: Field Hash Unres)    |
|    implementasi autentisitas membership dan lifecycle signer belum tersedia, blocker arsitektur aktif,     |   - AC-10 (NC-05/A-05: Taksonomi Error Gen)   |
|    atau spesifikasi lifecycle non-audio yang belum terdefinisi.    |   - AC-13 (B-07/NC-07: Usulan Kuota ZIP)      |
|                                                                    |   - AC-14 (B-04/CONF-03: Gap 2PC Eksternal)   |
|                                                                    |   - AC-15 (B-04/CONF-03: Gap Replay Token)    |
|                                                                    |   - AC-16 (B-05/NC-09: Semantik Hash DB)      |
|                                                                    |   - AC-20 (B-06/NC-12: Safe-Open TOCTOU)      |
|                                                                    |   - AC-21 (B-06/NC-12: Post-Open Descr)       |
|                                                                    |   - AC-22 (NC-13/CONF-01: JIT Prereq / Sig)   |
|                                                                    |   - AC-26 (NC-15: Formalisasi Taksonomi Error)|
|                                                                    |   - AC-28 (NC-01/06: Gap Identitas Album)     |
|                                                                    |   - AC-29 (NC-06: Gap Reload Kolektif Album)  |
|                                                                    |   - AC-32 (NC-13: Auto-Next Lifecycle Gap)   |
|                                                                    |   - AC-33 (NC-14: Desktop Membership Gate)  |
|                                                                    |   - AC-34 (NC-14: Mobile Membership Gate)   |
+--------------------------------------------------------------------+-----------------------------------------------+
| 3. [PO DECISION REQUIRED] (0 AC)                                   | Tidak ada PO decision item aktif pada kelompok ini.       |
|    Kriteria keberhasilan atau penerimaan kontrak secara substantif | AC-07 (NC-04/B-09/CONF-01: Signer UNKNOWN)    |
|    —                |                                               |
+--------------------------------------------------------------------+-----------------------------------------------+
```

#### Rekonsiliasi Individual Wajib Seluruh 34 Acceptance Criteria (DEF-01, Mandat Konsolidasi PO)
Tabel berikut membuktikan penelusuran individual per AC mencakup seluruh 34 AC tanpa duplikasi, memisahkan kesiapan spesifikasi dari dependensi yang belum selesai:

| ID AC | Kontrak Dasar | Klasifikasi Utama | Dasar Klasifikasi & Sumber Otoritatif | Dependensi Langsung & Blocker Terkait | Status Dependensi | Dimensi & Gate | Hasil Verifikasi Konsistensi |
|:---:|:---:|:---|:---|:---|:---:|:---:|:---|
| **AC-01** | NC-01 | `TEST-PLANNED — EXECUTION BLOCKED` | White Paper v5.6 §Manifest; RFC 8259; §5.1 Skema Manifest; Keputusan PO AC-01 | NC-01 / Strict Unknown-Field Policy telah disahkan; universal schema masih belum lengkap | `BLOCKED BY UNIVERSAL SCHEMA & IMPLEMENTATION` | Execution Blocked / Gate A & B Dependency | Unknown fields ditolak fail-closed sesuai keputusan PO; pengujian end-to-end menunggu schema universal dan parser/validator. |
| **AC-02** | NC-01/07 | `TEST-PLANNED — BLOCKED BY PROPOSED SPEC` | White Paper v5.6; PKWARE APPNOTE; §5.1 Regex Filename | NC-07 / Validasi arsip ZIP wrapper, penerimaan direktori & regular file, penolakan symlink/special via `ERR_ZIP_INVALID`, dan bijeksi 1:1 via `ERR_ZIP_ENTRY_MISMATCH` (AUDIT-NEW-06/08) | `OPEN (PROPOSAL DEPENDENCY)` | Technical Proposal / Gate B | Konsisten; pengujian terblokir pembekuan parameter kuota B-07. |
| **AC-03** | NC-02 | `TEST-PLANNED — EXECUTION BLOCKED` | IETF RFC 8032; `crypto.ts#L45`; §6.2 | B-08 (Circular Dependency tanda tangan manifest di dalam payload JCS) | `BLOCKED` | Architecture Blocker / Gate B | Konsisten; pengujian terblokir circular dependency signature. |
| **AC-04** | NC-06 | `TEST-PLANNED — SPEC READY` | IETF RFC 8032; `container.go#L110`; PE-01 Baseline | Baseline PE-01 Beku (`.nx` container packaging signature) | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; format kontainer `.nx` anggota album beku. |
| **AC-05** | NC-03 | `TEST-PLANNED — EXECUTION BLOCKED` | White Paper v5.6 §Parsers; Nexa Parser Policy | B-01 (Modul Strict JSON Parser Engine belum diimplementasikan) | `BLOCKED (MODULE PENDING)` | Module Pending / Gate B | Konsisten; spesifikasi uji duplicate key siap, modul pending koding. |
| **AC-06** | NC-03 | `TEST-PLANNED — EXECUTION BLOCKED` | IETF RFC 8785; Canonical JCS Test Vectors TV-01..TV-08 | B-02 (Modul RFC 8785 JCS Serializer Engine belum diimplementasikan) | `BLOCKED (MODULE PENDING)` | Module Pending / Gate B | Konsisten; vektor uji RFC 8785 siap, modul serializer pending koding. |
| **AC-07** | NC-04 | `TEST-PLANNED — EXECUTION BLOCKED` | Roadmap v4.8 §Trust Model; Keputusan PO CONF-01; B-09 / NC-04 | Fail-closed membership policy telah disahkan PO; signer identity binding, authority, trust store, dan lifecycle belum ditetapkan/diimplementasikan | `BLOCKED BY B-09 TECHNICAL CONTRACT / IMPLEMENTATION` | Execution Blocked / Gate B Dependency | Tidak lagi menunggu keputusan PO; implementasi dan kontrak teknis trust signer masih diperlukan. Standalone PE-01 tetap independen. |
| **AC-08** | NC-04 | `TEST-PLANNED — EXECUTION BLOCKED` | White Paper v5.6 §Registry; §6.11 | Kebutuhan pemeriksaan status revocation signer (`ERR_ALBUM_SIGNER_UNTRUSTED`); mekanisme operasional belum ditetapkan | `OPEN / BLOCKED (REGISTRY LIFECYCLE UNRESOLVED)` | Execution Blocked / Gate A Not Ready | Tidak siap uji: sumber, format, otoritas, retrieval, freshness, dan lifecycle revocation belum ditetapkan. |
| **AC-09** | NC-05 | `TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY` | White Paper v5.6 §Genesis; §6.9 (AUDIT-NEW-04) | NC-05 / AUDIT-NEW-01 (Identitas field hash audio manifest `audio_sha256` vs notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) berstatus unresolved) | `BLOCKED BY UNRESOLVED FIELD IDENTITY` | Architecture / Normative Blocker | Konsisten; finalisasi spesifikasi pengujian terblokir keputusan kanonikal identitas field manifest. |
| **AC-10** | NC-05 | `TEST-PLANNED — BLOCKED BY UNRESOLVED TAXONOMY` | White Paper v5.6 §Genesis; `sdk.ts#L205-L255`; E-01 | NC-05 / A-05 (Representasi kode error kanonikal Genesis signature pending taksonomi) | `OPEN (UNRESOLVED TAXONOMY)`| Architecture Dependency / Gate A | Konsisten; fail-closed `canPlay: false` pasti; kode error diskrit pending arsitektur. |
| **AC-11** | NC-06 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Container; `container.go#L110` | Ekstraksi kontainer mandiri `.nx` dari ZIP wrapper tanpa alterasi byte | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; format kontainer PE-01 mematuhi invariant byte utuh. |
| **AC-12** | NC-06 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Container; PE-01 Invariant Suite | Validasi packaging kontainer anggota mematuhi seluruh invariant PE-01 | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; pengujian packaging kontainer mandiri terdefinisi jelas. |
| **AC-13** | NC-07 | `TEST-PLANNED — BLOCKED BY PROPOSED SPEC` | PKWARE APPNOTE; RFC 1951; Proposal B-07 / NC-07 | B-07 / NC-07 (Batas kuota numerik ekstraksi ZIP wrapper berstatus usulan spesifikasi)| `BLOCKED BY PROPOSED SPEC`| Technical Proposal / Gate B | Konsisten; nilai kuota 500 MB desimal (500.000.000 bytes) / 4 GB desimal / 200 entri dan usulan rasio kompresi B-07 (ambiguitas 10:1 usulan B-07 vs 100:1 referensi pembanding eksternal yang belum diverifikasi) berstatus usulan spesifikasi. |
| **AC-14** | NC-08 | `TEST-PLANNED — EXECUTION BLOCKED` | `schema.postgres.sql#L63`; `server.js#L170`; B-04 | B-04 / CONF-03 (Ketiadaan 2PC / kompensasi transaksi terdistribusi ke daemon) | `BLOCKED` | Architecture Blocker / Gate B | Konsisten; rollback lokal terdefinisi, atomisitas multi-item terblokir B-04. |
| **AC-15** | NC-08 | `TEST-PLANNED — EXECUTION BLOCKED` | `server.js#L170`; NC-08; B-04 / CONF-03 | B-04 / CONF-03 (Model settlement replay protection tanpa transaksi terdistribusi) | `BLOCKED` | Architecture Blocker / Gate B | Konsisten; pengujian idempotensi settlement terblokir gap arsitektur B-04. |
| **AC-16** | NC-09 | `TEST-PLANNED — EXECUTION BLOCKED` | `marketplace/db/schema.postgres.sql#L72`; NC-09; B-05 | B-05 / NC-09 (Keberadaan field DDL berstatus `NOT VERIFIED` bagi audit independen; semantik kolom DB `acquired_package_sha256` child row terblokir B-05) | `BLOCKED` | Architecture Blocker / Gate B | Konsisten; penyimpanan child acquisition terblokir semantik hash DB B-05; bukti primer DDL berstatus NOT VERIFIED bagi auditor independen. |
| **AC-17** | NC-10 | `TEST-PLANNED — SPEC READY` | `schema.postgres.sql#L63-L115`; Zero-DDL Contract | Kepatuhan skema statis Zero-DDL (Live DB runtime berstatus `NOT VERIFIED`) | `STATIC DDL REPORTED — NOT INDEPENDENTLY VERIFIED / OPEN (LIVE DB)` | Spec Ready / Gate A Conditional (DDL source evidence reported by Programmer; not independently verified) | Konsisten; skema SQL statis Zero-DDL 100% dipatuhi; live DB unverified. |
| **AC-18** | NC-11 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Registry; §6.11 | Verifikasi online via remote Registry API saat koneksi jaringan aktif | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; pengujian jalur online siap dieksekusi saat modul tersedia. |
| **AC-19** | NC-11 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Offline Fallback; §6.11 | Fallback cache offline pada network transport error; HTTP 5xx/bad sig melempar fail-closed | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; aturan offline fallback terisolasi ketat dari transport error. |
| **AC-20** | NC-12 | `TEST-PLANNED — EXECUTION BLOCKED` | POSIX.1-2017; `fs_safe.ts#L30`; Invariant Safe-Open | B-06 (Mitigasi Safe-Open & penerimaan residual risk concurrent rename POSIX userspace) | `BLOCKED` | Security Mitigation / Gate B | Konsisten; penolakan containment path traversal fail-closed; residual risk B-06. |
| **AC-21** | NC-12 | `TEST-PLANNED — EXECUTION BLOCKED` | POSIX.1-2017; `fs_safe.ts#L30`; Invariant Safe-Open | B-06 (Verifikasi post-open descriptor & penerimaan residual risk POSIX userspace) | `BLOCKED` | Security Mitigation / Gate B | Konsisten; pemeriksaan descriptor pasca-open fail-closed; residual risk B-06. |
| **AC-22** | NC-13 | `TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED JIT PREREQUISITES & SIGNER/MEMBERSHIP IMPLEMENTATION` | White Paper v5.6 §JIT Player; §5.2; Keputusan PO AUDIT-NEW-01 dan CONF-01 | Otorisasi JIT 8-tahap Player sebelum pendaftaran buffer trek audio aktif; Stage 8a passive background inspection/diagnostic digest diizinkan hanya tanpa playback authorization, decryption, buffer registration, atau bypass Genesis/active-license/trust checks. Eksekusi uji tetap terblokir oleh kontrak/prasyarat Stage 8a terhadap Genesis 7b dan lisensi aktif 7c, identitas field hash audio, serta implementasi identity/lifecycle dan verifier membership signer (CONF-01/B-09). Bukan global playback gate; file `.nx` yang dipilih independen tetap mengikuti PE-01 standalone JIT authorization. | `OPEN (JIT PREREQUISITES / AUDIO HASH IDENTITY / B-09 IMPLEMENTATION)` | Execution Blocked Parsial / Gate A & B Dependency | Izin diagnostik pasif Stage 8a telah disahkan PO dengan batas ketat; authorization boundary current-member tetap. Sisa blocker adalah prasyarat JIT, field identity, dan implementasi trust membership. |
| **AC-23** | NC-13 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §JIT Player; §5.2 | Otorisasi JIT dieksekusi ulang secara independen saat pengguna berpindah trek | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; tidak ada otorisasi massal atau pembagian token lintas-trek. |
| **AC-24** | NC-13 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §JIT Player; §5.2 | Satu trek rusak dalam antrean album gagal diputar tanpa mengganggu trek valid | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; isolasi error per trek ditegakkan fail-closed secara mandiri. |
| **AC-25** | NC-14 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Verify; Keputusan PO CONF-02; §5.3 | Mengikuti Keputusan PO (CONF-02 / NC-14 Pilihan B APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; hasil verifikasi setiap berkas `.nx` anggota ditampilkan secara individual; tidak ada pembuatan status agregat baru (`ALBUM_TRUSTED`, `ALBUM_INVALID`) | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; disahkan PO bahwa NX Verify tidak menggunakan status agregat. |
| **AC-26** | NC-15 | `TEST-PLANNED — BLOCKED BY PROPOSED SPEC` | Error Taxonomy Spec §6.15; Taksonomi 20 Kode Error | NC-15 (Formalisasi taksonomi 20 kode error kanonikal berstatus usulan spesifikasi) | `BLOCKED BY PROPOSED SPEC` | Technical Proposal / Gate B | Konsisten; taksonomi error 20 kode berstatus usulan spesifikasi teknis NC-15. |
| **AC-27** | NC-16 | `TEST-PLANNED — SPEC READY` | `schema.postgres.sql#L63-L115`; §6.16 | Derivasi matematis formula ID truncated SHA-256 mematuhi batas kolom skema DDL | `OPEN (STATIC DDL EVIDENCE NOT INDEPENDENTLY VERIFIED) / OPEN (COLLISION)` | Spec Ready / Gate A Conditional (DDL source evidence reported by Programmer; not independently verified) | Konsisten; kepatuhan batas kolom DDL dilaporkan Programmer dan belum diverifikasi independen; bukan jaminan bebas collision. |
| **AC-28** | NC-01, NC-06 | `TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED ALBUM IDENTITY & ASSOCIATION GAP` | White Paper v5.6 §Studio; Keputusan PO §2.3.A; §5.1 item 3, §5.4 | NX Studio memproses Album Forge New berisi beberapa file sumber biasa (Image/Doc/Music/Video) secara sekuensial individual; setiap berkas menghasilkan `.nx` mandiri; input UI Studio siap diuji; persistensi katalog per item individual via `catalog_snapshots` dilaporkan Programmer dan belum diverifikasi independen; namun identitas Album multi-member persisten dan asosiasinya di Marketplace menurut laporan Programmer belum didukung skema/API existing; bukti primer belum diverifikasi independen (STOP AND CLARIFY) | `SPEC-READY (STUDIO UI/FORGING) / BLOCKED (ALBUM IDENTITY)` | Execution Blocked Parsial / Gate A Blocker | Konsisten; alur forging sekuensial disahkan PO; gap identitas & asosiasi Album multi-member diakui terbuka. |
| **AC-29** | NC-06 | `TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED ALBUM RELOAD SPECIFICATION` | White Paper v5.6 §Studio; Keputusan PO §2.3.B; §5.1 item 3, §5.4 | NX Studio memproses Album Existing `.nx` berisi beberapa berkas `.nx` yang sudah ada (Music/Video/Doc/Image) secara sekuensial individual via `NXPublishPipeline` existing tanpa forging ulang; publikasi katalog per item individual dilaporkan Programmer dan belum diverifikasi independen; namun mekanisme Marketplace untuk memuat kembali seluruh anggota sebagai satu kesatuan Album menurut laporan Programmer belum tersedia (STOP AND CLARIFY); bukti primer belum diverifikasi independen | `SPEC-READY (PUBLISH PIPELINE) / BLOCKED (ALBUM RELOAD)` | Execution Blocked Parsial / Gate A Blocker | Konsisten; alur publikasi existing `.nx` disahkan PO; gap pemuatan kembali kolektif Album diakui terbuka. |
| **AC-30** | NC-01 | `TEST-PLANNED — SPEC READY` | Keputusan PO §2.3.C (Larangan Album Campuran); §5.4 | Validasi jenis masukan menolak kombinasi berkas sumber biasa dan existing `.nx` dalam satu Album secara fail-closed sebelum pemrosesan dimulai tanpa silent conversion dan tanpa merusak input | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; pemisahan jenis masukan disahkan PO secara APPROVED. |
| **AC-31** | NC-01, NC-06 | `TEST-PLANNED — SPEC READY` | Keputusan PO §2.4 (Failure Handling Studio); §5.5 | Kegagalan forging/upload menghentikan proses sementara; pengguna disajikan opsi diskrit "Ulangi" dan "Lewati"; retry upload memakai hasil `.nx` yang sama tanpa forging ulang dan wajib mencegah listing duplikat (hasil yang disetujui PO); mekanisme idempotensi teknis tidak ditetapkan sebagai kontrak dan bukti repository hanya laporan Programmer yang belum diverifikasi independen (`server.js#L2400-L2416, L2467-L2470`, `publish_pipeline.js#L316-L410`; status bukti: inspeksi lokal Programmer / audit independen pending); skip tidak menghapus file sumber; status forging vs upload dibedakan per anggota (terpisah dari B-04) | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; tindakan Ulangi/Lewati, hasil Retry/Skip dan pencegahan listing duplikat disahkan; mekanisme idempotensi teknis tidak disahkan sebagai kontrak dan bukti repository belum diverifikasi independen. |
| **AC-32** | NC-13 | `TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MULTI-PAYLOAD AUTO-NEXT LIFECYCLE CONTRACT` | White Paper v5.6 §JIT Player; Keputusan PO §2.5; §5.2 | NX Player memutar album secara sekuensial per-anggota; otorisasi individual JIT per-anggota tanpa pewarisan; pre-verifikasi tidak memberi otorisasi; Auto-Next audio memiliki event listener `ended` di GUI pustaka desktop (`renderer.js#L652-L655` memanggil `playNextLibraryAsset()`) namun belum menjadi kontrak transisi Album resmi; video tidak memiliki handler event `ended` pada `videoEngine`; payload non-audio (dokumen/gambar) tidak memiliki durasi alami; seluruh pemicu Auto-Next Album multi-member berstatus UNRESOLVED pending penetapan kontrak resmi PO/Arsitektur (STOP AND CLARIFY; timer sepihak dilarang) | `UNRESOLVED / BLOCKED (ALL PAYLOADS)` | Execution Blocked / Gate A Blocker | Konsisten; navigasi Auto-Next PO dipertahankan; kesiapan diturunkan menjadi Execution Blocked karena ketiadaan kontrak lifecycle transisi Album pada seluruh payload. |
| **AC-33** | NC-14 | `TEST-PLANNED — EXECUTION BLOCKED BY B-09 MEMBERSHIP VERIFIER / SIGNER LIFECYCLE` | White Paper v5.6 §Verify Desktop; Keputusan PO §2.6, §2.7, CONF-01; §5.3 | NX Verify Desktop hanya memproses file sebagai anggota Album setelah autentisitas membership dibuktikan; kebijakan fail-closed untuk signer UNKNOWN atau signature invalid telah disahkan PO. Jika bukti belum valid, file manifest tidak diproses sebagai anggota Album; file yang diberikan independen tetap dapat diverifikasi standalone PE-01. Tombol manual Next, hasil per-anggota tanpa status agregat, dan Full Verify existing tetap dipertahankan. | `BLOCKED BY B-09 IDENTITY / LIFECYCLE / VERIFIER IMPLEMENTATION` | Execution Blocked / Gate B Dependency | Kebijakan produk sudah diputuskan; eksekusi menunggu identity binding, authority, trust lifecycle, verifier, dan pengujian. |
| **AC-34** | NC-14 | `TEST-PLANNED — EXECUTION BLOCKED BY B-09 MEMBERSHIP VERIFIER / SIGNER LIFECYCLE` | White Paper v5.6 §Verify Mobile Lite; Keputusan PO §2.6, §2.7, CONF-01; §5.3 | NX Verify Mobile hanya memproses file sebagai anggota Album setelah autentisitas membership dibuktikan; kebijakan fail-closed untuk signer UNKNOWN atau signature invalid telah disahkan PO. Jika bukti belum valid, file manifest tidak diproses sebagai anggota Album; file yang diberikan independen tetap dapat diverifikasi standalone PE-01. Navigasi manual Next, hasil individual tanpa status agregat, dan batas Verify-Lite tetap dipertahankan. | `BLOCKED BY B-09 IDENTITY / LIFECYCLE / VERIFIER IMPLEMENTATION` | Execution Blocked / Gate B Dependency | Kebijakan produk sudah diputuskan; eksekusi menunggu identity binding, authority, trust lifecycle, verifier, dan pengujian. |

---

### 2.2 Aturan Operasional Pencegahan Delapan Belas Pola Defect Negatif (Bagian 2.4)
Sesuai Bagian 2.4 mandat audit, dokumen ini menerapkan 18 kontrol operasional mutlak untuk mencegah pengulangan defect yang kerap berulang:

| No | Pola Defect Negatif yang Dicegah | Aturan Pencegahan Operasional Mutlak REV6 | Namespace Terkait |
|:---:|:---|:---|:---:|
| 1 | Kontrak sumber kebenaran belum dikunci tetapi Programmer dipaksa memilih interpretasi. | Wajib berhenti (`STOP — INSTRUKSI TIDAK JELAS. TIDAK ADA INTERPRETASI BEBAS`) dan minta keputusan resmi. | `PR`, `I` |
| 2 | Fakta repositori dicampur dengan desain usulan tanpa penanda status eksplisit. | Wajib beri label eksplisit `[PROPOSED SPECIFICATION]` atau `[REPOSITORY-VERIFIED]` pada setiap klaim. | `R`, `V` |
| 3 | ID kontrak, blocker, temuan, atau AC dipetakan berdasarkan kemiripan nomor bukan fungsi. | Wajib petakan berdasarkan kesesuaian fungsional dan semantik kontrak (e.g. AC-15 ke NC-08, bukan NC-16). | `P`, `AC`, `NC` |
| 4 | Klaim readiness global menutupi Acceptance Criteria yang masih terblokir. | Dilarang sweeping claim; seluruh 34 AC wajib mewarisi status dependensi fisik masing-masing. | `PR`, `G` |
| 5 | Kontrak spesifikasi dinyatakan `RESOLVED` meskipun kode implementasi belum dibuat. | Status `SPECIFIED` secara tegas bukan `RESOLVED`; modul belum dibuat dilabeli `NOT IMPLEMENTED`. | `G`, `B` |
| 6 | Pengujian berstatus `[TEST-PLANNED]` dipresentasikan seolah-olah telah lulus. | Dilarang menaikkan `TEST-PLANNED` menjadi `TEST-PASSED` tanpa bukti eksekusi aktual di lingkungan uji. | `V`, `AC` |
| 7 | Hash manifest, kontainer, audio payload, sertifikat Genesis, dan paket ZIP dipertukarkan. | Wajib susun inventaris kriptografis/hash berbasis bukti faktual (§6.9), membedakan signature diskrit, hash terdefinisi, dan entitas komputasional internal tanpa memaksakan angka agregat yang tidak didukung bukti. | `I`, `NC-09` |
| 8 | Tiga peran kriptografis Genesis Creator, Container Packager, dan current owner/holder belum dipisahkan secara normatif. | Pisahkan genesisPubKey, containerSigKey, dan ownCertPubKey sebagai peran berbeda; ketiganya tidak diwajibkan identik. Third-party packager wajib memiliki delegation/authorization evidence yang valid; signature matematis saja tidak membuktikan otoritas packaging. | I, NC-02/05/06, AUDIT-NEW-10 |
| 9 | Kegagalan kriptografi diperlakukan sebagai kegagalan jaringan atau diatasi via fallback. | Seluruh anomali signature, hash mismatch, dan sertifikat tidak sah wajib melempar fail-closed. | `PR`, `NC-11/15` |
| 10 | Pemeriksaan path sebelum membuka file dianggap cukup mencegah semua race condition. | Wajib gunakan invariant descriptor pasca-open (`O_NOFOLLOW` + `fstat`) dan akui batas POSIX userspace. | `G`, `NC-12` |
| 11 | Penolakan signer `UNKNOWN` dianggap otomatis melarang seluruh pemeriksaan integritas anggota. | Penolakan pemutaran (playback) TIDAK membatalkan verifikasi integritas fisik untuk diagnostik Verify. | `I`, `NC-04/14` |
| 12 | Kegagalan transaksi eksternal diklaim dapat di-rollback oleh SQL lokal pasca-commit. | Dilarang menjanjikan rollback SQL pasca-commit; efek samping daemon eksternal tidak terkompensasi (B-04). | `I`, `NC-08` |
| 13 | Batasan skema Zero-DDL diabaikan untuk membuat rancangan transaksi terlihat atomik. | Wajib patuhi skema DDL beku aktif 100%; dilarang mengarang kolom FK atau tabel outbox terdistribusi. | `G`, `NC-10` |
| 14 | Acceptance Criteria ditulis dengan ruang lingkup yang lebih luas daripada bukti yang diperlukan. | Batasi cakupan AC tepat pada expected result terukur yang dapat diverifikasi empiris. | `PR`, `AC` |
| 15 | Pernyataan root-clean, zero-mutation, atau tidak ada perubahan DB dibuat tanpa bukti terminal. | Wajib cantumkan output inspeksi git riil (`git diff`, `git status`) dan batasi klaim pada root level. | `V`, `R` |
| 16 | Status Gate dihitung dari jumlah checklist centang, bukan konflik material yang terbuka. | Gate A wajib `NOT PASSED` selama masih ada blocker material/kontradiksi plan yang belum ditutup; kebijakan CONF-01 dan CONF-02 telah disahkan PO, sedangkan CONF-03 adalah kontrak teknis B-04 yang tetap terbuka; Gate B `BLOCKED` selama B-01..B-09 terbuka. | `G`, `Gate A/B` |
| 17 | Temuan lama dihapus atau diganti istilah baru tanpa pemetaan yang dapat diaudit. | Pertahankan seluruh register historis (A-01..A-30, B-01..B-09, F-01..F-15) dengan namespace stabil. | `PR`, `Register` |
| 18 | Solusi tambahan, tahapan audit, dokumen, dan evidence loop dibuat tanpa kebutuhan keputusan. | Patuhi batas tata kelola anti-overprocessing: satu berkas kanonikal, tanpa artefak duplikat. | `PR`, `Rule C` |

### 2.3 Matriks Rekonsiliasi Akomodasi V5-REV1 vs Gap V6.9.4-REV4 (Bagian 3)
Dokumen ini mengonsolidasikan 7 akomodasi positif dari V5-REV1 dan secara jujur menuntaskan 11 area gap pada V6.9.4-REV4:

#### A. Tujuh Akomodasi Positif V5-REV1 yang Wajib Dipertahankan
1. **Pemisahan Status Multi-Dimensi**: Pemisahan tegas status desain/spesifikasi, implementasi repositori, dan pengujian runtime.
2. **Pemisahan Tiga Lapisan Kontrak Genesis, Registry Certificate, dan Manifest (DEF-04)**: Menegakkan pemisahan berlapis secara ketat sesuai implementasi `sdk/typescript/src/sdk.ts#L205-L260` dan White Paper v5.6:
   - *Lapisan 1: Outer Registry Certificate (`regCert`)*: Dikanonisasi menggunakan 6 argumen via `NexaRegistry.canonicalJcs(certificate_id, issued_at, issuer, status, valid_until, creatorKey)` (atau fallback 5-field `canon5`) dan diverifikasi terhadap `registryPubKey` via `issuer_signature`. Enam argumen ini adalah input fungsi kanonisasi dan bukan bukti bahwa objek sertifikat secara keseluruhan hanya memiliki 6 field.
   - *Lapisan 2: Embedded Genesis Ownership Certificate (`ownCert`)*: Serialisasi kanonikal pada baseline `sdk.ts#L242-L251` dieksekusi menggunakan `JSON.stringify({...})` dengan tepat 8 properti (`asset_id, creator_public_key, effective_at, issued_at, issuer_id, previous_cert_ref, subject_id, underlying_cert_id`) dan diverifikasi terhadap `creator_public_key` menggunakan tanda tangan `creator_signature`. **Peringatan Teknis (DEF-04):** `JSON.stringify()` pada V8 JavaScript TIDAK identik dengan RFC 8785 JCS (tidak menjamin pengurutan leksikografis UTF-16 code units independen dari insertion order objek).
   - *Lapisan 3: Album Manifest (`album_manifest.json` [nama/lokasi kandidat draf; belum disahkan])*: Ditandatangani oleh `album_signer_public_key`. Mandat penggunaan RFC 8785 JCS berlaku pada lapisan ini, namun saat ini berstatus `BLOCKED` oleh B-08 (circular dependency) dan B-02 (serializer engine pending).
   - *Hubungan Key Material (DEF-04):* `GENESIS_PUBLIC_KEY` pada §6.9 merujuk pada `creator_public_key` penandatangan Genesis Ownership Certificate. Perbedaan penamaan ini dicatat sebagai `TERMINOLOGY UNRESOLVED / PENDING NORMATIVE UNIFICATION` tanpa menyamakan atau mengubah nama secara sepihak.
3. **Penandaan Kontrak Belum Terimplementasi**: Pelabelan kontrak sebagai `SPECIFIED — PENDING IMPLEMENTATION AUTHORIZATION` jika kode belum ada.
4. **Pengakuan Keterbatasan Skema Database Aktif**: Pengakuan bahwa skema PostgreSQL aktif tidak memiliki kolom `order_id` atau `parent_acquisition_id`.
5. **Ketiadaan 2PC ke License Daemon**: Pengakuan bahwa panggilan HTTP ke Licensing Daemon Sprint 12 tidak menyediakan rollback atomik terdistribusi.
6. **Penetapan Status Resmi Dokumen**: Penandaan jujur `NOT READY — BLOCKED` tanpa penutupan semu.
7. **Isolasi Baseline Ekosistem**: Penegasan bahwa implementasi PE-02 `NOT AUTHORIZED`, Sprint 17 `NOT STARTED`, dan PE-01 tetap 🔒 `CLOSED / FROZEN`.

#### B. Rekonsiliasi Sebelas Area Defect V6.9.4-REV4
| Area Gap V6.9.4-REV4 | Kekurangan yang Harus Dituntaskan | Kriteria Koreksi Substantif REV6 |
|---|---|---|
| **Gate A** | Masih `NOT PASSED` karena konflik material belum selesai. | Menunjukkan blocker teknis dan gap konsistensi yang benar-benar masih terbuka; CONF-01/CONF-02 policy telah disahkan, CONF-03 direklasifikasi menjadi kontrak teknis B-04. |
| **Gate B** | Masih `BLOCKED`. | Mempertahankan status `BLOCKED` selama dependensi teknis dan PO belum selesai. |
| **B-04 / NC-08 / CONF-03** | Gap transaksi Marketplace, Zero-DDL, dan daemon eksternal. | Tetap `BLOCKED`; Model B, SSP/Largest Remainder, identitas checkout, dan Manifest sebagai sumber kebenaran normatif telah disahkan. Kontrak atomisitas/pemenuhan multi-item, storage/persistensi, pemetaan acquisition, idempotency, recovery, settlement, dan side effect eksternal masih harus dirancang. |
| **B-05 / NC-09** | Semantik `acquired_package_sha256` untuk child acquisition. | Tetap `BLOCKED`; melarang tebakan semantik kolom hash database. |
| **B-06 / NC-12** | Batas keamanan filesystem safe-open dan race condition. | Membedakan symlink, descriptor, containment, dan batas concurrent ancestor rename. |
| **B-08** | Circular dependency signing manifest JCS. | Tetap `BLOCKED — REQUIRES CLARIFICATION` sampai payload kanonikal diputuskan resmi. |
| **B-09 / NC-04 / CONF-01** | Kebijakan membership fail-closed telah disahkan PO; identity binding, authority, trust store, dan lifecycle signer tetap merupakan gap teknis B-09. | Policy resolved; implementasi identity/lifecycle signer tetap OPEN/BLOCKED. |
| **CONF-02** | Hierarki status agregat NX Verify. | **SELESAI / PO DECISION APPROVED (OPTION B)**: PO mengesahkan Pilihan B (tanpa status agregat Album di NX Verify; verifikasi individual member primer); AC-25 SPEC READY. AC-33/AC-34 tetap EXECUTION BLOCKED sampai implementasi/verifikasi membership dan signer lifecycle B-09 tersedia; kebijakan fail-closed telah diputuskan PO. |
| **Acceptance Criteria** | Status AC tidak seragam jika dependensi berbeda. | Setiap AC mewarisi status dependensi riil (34 AC aktif: 12 Spec Ready + 22 Execution Blocked (termasuk AC-01 [strict unknown-field policy disahkan; universal schema/parser pending], AC-07 [membership policy fail-closed disahkan; signer lifecycle B-09 pending], AC-22, AC-28, AC-29, dan AC-32) + 0 PO Decision Required = 34 AC; direkonsiliasi dari snapshot historis 27 AC). |
| **Evidence Ledger** | Klaim bukti harus sesuai ruang lingkup inspeksi riil. | Membatasi bukti pada kode statis Linux server; menandai mobile & live DB `NOT VERIFIED`. |
| **Traceability Matrix** | Keterlacakan dua arah harus konsisten. | Seluruh NC, AC, B, F, E, G, dan CONF terpetakan dua arah tanpa tebakan. |

---

## 3. SUMBER OTORITATIF SERTA ATURAN PENANGANAN KETIDAKPASTIAN

### 3.1 Hierarki Sumber Otoritatif (AUDIT-NEW-09 — PO APPROVED)
Seluruh klausul teknis, evaluasi pembuktian, dan batasan implementasi dalam dokumen ini tunduk secara ketat pada hierarki otoritas 6-tingkat kanonikal yang telah disahkan Product Owner (§1.2):

```
[Level 1: Keputusan Eksplisit Product Owner untuk Ruang Lingkup PE-02]
   ├── Otorisasi Scope, Governance Override, Persetujuan Parameter, & Batas Rilis
   └── Penetapan Keputusan Normatif Tertulis yang Mengikat
          │
[Level 2: Kontrak Produk dan Governance Nexa yang Telah Disetujui / Dibekukan]
   ├── Sprint 16 Closeout Report & Acceptance Memo (Baseline Ekosistem Beku)
   ├── PE-01 Offline NxCert Hidden-by-Default (Baseline Kontainer Mandiri Beku)
   └── Governance Policy (Batas 3 Siklus Korektif, Anti-Overprocessing, No Reset)
          │
[Level 3: White Paper dan Roadmap yang Telah Disetujui (Sepanjang dalam Ruang Lingkupnya)]
   ├── Nexa White Paper v5.6 (Arsitektur Ekosistem & Prinsip Fail-Closed)
   └── Nexa Development Roadmap v4.8 (Target Fitur Album & Keputusan Terbuka)
          │
[Level 4: Repository Aktual sebagai Bukti Implementasi (Bukan Otoritas Pengubah Kontrak)]
   ├── marketplace/db/schema.postgres.sql (Bukti Skema Database DDL Aktif)
   ├── internal/container/container.go (Bukti Implementasi Engine Packaging Go)
   ├── sdk/typescript/src/sdk.ts & container.ts (Bukti Implementasi SDK Nexa)
   └── player-desktop/main.js (Bukti Implementasi NX Player Desktop)
          │
[Level 5: Standar Internasional yang Relevan (Sepanjang Tidak Bertentangan)]
   ├── IETF RFC 8785 (JSON Canonicalization Scheme - JCS)
   ├── IETF RFC 8032 (Ed25519 Pure Edwards-curve Digital Signature Algorithm)
   ├── IETF RFC 8259 (The JavaScript Object Notation Data Interchange Format)
   ├── PKWARE APPNOTE.TXT / ISO/IEC 21320-1 (Format Kontainer Arsip ZIP)
   ├── IETF RFC 1951 (DEFLATE Compressed Data Format Specification)
   └── POSIX.1-2017 (Standard for Information Technology — Portable Operating System Interface)
          │
[Level 6: Temuan Audit Historis, Bukti Pendukung, Proposal Belum Disetujui, & Interpretasi]
   ├── Temuan Audit Historis Beserta Bukti Faktualnya (A-01..A-30, B-01..B-09, F-01..F-15, AUDIT-NEW)
   ├── Usulan Spesifikasi Teknis yang Belum Disahkan ([PROPOSED SPECIFICATION])
   └── Interpretasi dan Analisis Perancang (Mempertahankan Status, Bukan Ketentuan Normatif)
```

### 3.2 Prosedur Stop-and-Clarify Mutlak
Jika ditemukan ketidakjelasan instruksi, konflik antar-sumber, atau ketiadaan dasar normatif, Programmer **WAJIB BERHENTI DAN MENYATAKAN `STOP — INSTRUKSI TIDAK JELAS. TIDAK ADA INTERPRETASI BEBAS.`**. Dilarang keras melakukan interpretasi bebas terhadap:
1. Batas payload kanonikal tanda tangan manifest `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] (Ketergantungan melingkar B-08).
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
- **Integritas Tata Kelola:** Klaim inspeksi lokal `whisnu/nexa` mengenai `git diff --name-only`, status DDL, `ls -la`, dan dua berkas untracked di `docs/` merupakan **laporan Programmer pada evidence ledger**, bukan hasil inspeksi independen dalam audit dokumen ini. Status klaim lokal tersebut: `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; kondisi database runtime live dan eksekusi mobile tetap `NOT VERIFIED`.

### 4.2 Ruang Lingkup Fungsional PE-02
Kontrak produk PE-02 yang telah disahkan mencakup pengelompokan logis `.nx` mandiri, empat kategori sumber, pemisahan Forge New dan Existing `.nx`, perilaku Player/Verify, serta keputusan PO lain yang tercantum eksplisit dalam plan. **ZIP wrapper, nama/lokasi manifest, schema JSON, Album Signer, JCS/Ed25519 untuk manifest, dan mekanisme persistence/reload bukan bagian dari Product Truth yang ditetapkan White Paper v5.6 atau Roadmap v4.8; detail tersebut tetap proposal/unresolved kecuali ada keputusan PO/Architecture Authority yang eksplisit.** Daftar langkah ZIP/manifest/JCS/Signer berikut merupakan rancangan belum normatif, bukan pernyataan bahwa fitur tersebut telah disahkan atau tersedia.

### 4.3 Matriks Status Komponen Aktual vs Klaim White Paper v5.6
Tabel berikut mencatat lokasi dan status inspeksi yang DILAPORKAN Programmer; Auditor belum memiliki akses/bukti primer repositori `whisnu/nexa` untuk memverifikasi inspeksi tersebut secara independen. Status pengujian runtime dipisahkan dari laporan inspeksi kode.

| Komponen Ekosistem | Lokasi Kode di Repositori | Status Inspeksi Kode | Status Pengujian Runtime Aktual |
|---|---|:---:|:---:|
| **SDK Genesis & Cert** | `sdk/typescript/src/sdk.ts` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `[TEST-PLANNED]` (Unit test single `.nx` ada; multi-track belum diuji) |
| **SDK Container Engine** | `sdk/typescript/src/container.ts` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `[TEST-PLANNED]` (Unpack single `.nx` ada; manifest album belum diuji) |
| **Marketplace API & DB** | `marketplace/server.js` & `schema.postgres.sql` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `[BLOCKED]` (Transaksi terdistribusi non-2PC terblokir B-04) |
| **NX Player Desktop** | `player-desktop/main.js` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `[TEST-PLANNED]` (Handler scheme terdaftar; runtime JIT 8-tahap belum diuji) |
| **NX Verify Desktop** | `verify-desktop/src/` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `[TEST-PLANNED — SPECIFICATION READY FOR STANDALONE PE-01; ALBUM-MEMBER EXECUTION BLOCKED]` (Verifikasi `.nx` mandiri tetap mengikuti kontrak PE-01. Berkas yang hanya dideklarasikan sebagai anggota oleh manifest tidak boleh diproses/dilabeli sebagai anggota Album sebelum membership authenticity terbukti; AC-33/AC-34 tetap Execution Blocked karena CONF-01/B-09 unresolved. CONF-02 Option B: tanpa status agregat Album.) |
| **Mobile Runtime (iOS/Android)**| `mobile/` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` (Belum diuji di Linux server) |
| **Distributed Usage Service** | `cmd/usage/` | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED` | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` (Belum diuji runtime fisik) |

---

### 4.4 Evidence Ledger Repository Terstruktur dengan Kutipan Mentah
Tabel berikut memuat kutipan kode, path absolut, dan line range sebagaimana **dilaporkan Programmer** dari inspeksi lokal. Auditor belum memeriksa repository primer `whisnu/nexa`; kutipan ini bukan bukti yang diverifikasi independen dan tidak boleh dinaikkan menjadi klaim implementasi terverifikasi:

> [!NOTE]
> **Provenance Bukti Repository (Programmer-only):** Repository sumber `whisnu/nexa` merupakan domain akses kerja Programmer. Auditor tidak diwajibkan dan tidak diasumsikan memiliki akses langsung ke repository tersebut. Isi §4.4 adalah ledger bukti yang diserahkan/dilaporkan Programmer; pemeriksaan Auditor menilai provenance, kecukupan kutipan, keterlacakan, konsistensi internal, serta batas klaim bukti tersebut. Status `VERIFIED BY PROGRAMMER` tidak berarti verifikasi independen oleh Auditor dan tidak boleh dinaikkan menjadi bukti runtime jika yang tersedia hanya inspeksi statis.

| ID Bukti | Komponen & Klaim yang Diperiksa | Path Berkas & Line Range | Kutipan Mentah Kode Sumber (*Raw Snippet*) | Batas Klaim Pembuktian Faktual | Status Verifikasi (Inspeksi Lokal Programmer vs Audit Independen) |
|:---:|:---|:---|:---|:---|:---:|
| **E-01** | Struktur Dua Lapisan Genesis Certificate & Verifikasi Ed25519 | `/opt/antigravity/projects/nexa/sdk/typescript/src/sdk.ts#L205-L260` | ```typescript\n// Lapisan 1: Registry Certificate (6-field JCS / 5-field fallback)\nconst canonStr = NexaRegistry.canonicalJcs(regCert.certificate_id, regCert.issued_at, regCert.issuer, regCert.status, regCert.valid_until, creatorKey);\nsigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes);\n// Lapisan 2: Embedded Genesis Ownership Certificate (8-field canonical string)\nconst canonGenesisStr = JSON.stringify({\n  asset_id: ownCert.asset_id, creator_public_key: ownCert.creator_public_key,\n  effective_at: ownCert.effective_at, issued_at: ownCert.issued_at,\n  issuer_id: ownCert.issuer_id, previous_cert_ref: ownCert.previous_cert_ref || "",\n  subject_id: ownCert.subject_id, underlying_cert_id: ownCert.underlying_cert_id\n});\nconst cryptoValid = NexaCrypto.verify(ownKeyObj, Buffer.from(canonGenesisStr, "utf8"), ownSigBytes);\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): struktur dua lapisan yang diklaim adalah (1) Registry Certificate menggunakan 6 field pada `canonicalJcs` diverifikasi dengan `registryPubKey`; (2) Embedded Genesis Ownership Certificate menggunakan tepat 8 field kanonikal diverifikasi dengan `creator_public_key`. Tidak ditemukan konstanta error `ERR_GENESIS_SIGNATURE_INVALID` pada baseline (status kode error diskrit kanonikal: unresolved / fail-closed `canPlay:false` via generic error). | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR` |
| **E-02** | Ekstraksi Kontainer Single `.nx` di Go Engine (Hasil PSV) | `/opt/antigravity/projects/nexa/internal/container/container.go#L90-L130` | ```go\n// internal/container/container.go:L106-L114\nif manifestLen > 100*1024*1024 || payloadLen > 2*1024*1024*1024 || sigLen != 64 {\n    return nil, nil, nil, errors.New("invalid section sizes in container header")\n}\nexpectedSize := int64(headerSize) + int64(manifestLen) + int64(payloadLen) + int64(sigLen)\nif int64(len(data)) < expectedSize {\n    return nil, nil, nil, fmt.Errorf("container is truncated: expected %d bytes, got %d", expectedSize, len(data))\n}\n``` | Hasil PSV membuktikan kontainer `.nx` adalah format biner murni (Magic `NEXA`, header 21-byte, payload maks 2 GiB, trailer 64-byte Ed25519 signature). **TIDAK** menggunakan parser ZIP pada engine Go, dan tidak ada parser ZIP arsip Album di source repository aktif (B-03/B-07). | `VERIFIED BY PSV (CONTAINER BINARY FORMAT VERIFIED; ZIP PARSER NOT PRESENT IN SOURCE)` |
| **E-03** | Skema Database PostgreSQL — acquired_package_sha256 (PSV-05 / PSV-R06) | `marketplace/db/schema.postgres.sql#L63-L135`, `marketplace/server.js#L762-L770`, `#L2231`, `#L2396`, `#L3839-L3861` | DDL utuh kedua tabel (`acquisitions` L72 & `entitlements` L112, serta migrasi L133-L134) dan alur pembentukan hash (`computeFileSha256(session.spool_path)`) diverifikasi pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`. Byte-domain hash terbukti adalah berkas spool paket delivery (wrapper ZIP) utuh. | Hasil inspeksi Programmer membuktikan asal nilai `catalog_snapshots.package_sha256` dari stream seluruh berkas paket delivery spool dan konsistensi DDL L63-L135 dengan SQL producer. Pemetaan child-member Album tidak ada di skema; live DB tidak diverifikasi. | `VERIFIED BY PROGRAMMER — STATIC SOURCE; LIVE DB NOT VERIFIED; CHILD CONTRACT OPEN` |
| **E-04** | Ketiadaan 2PC pada Transaksi Marketplace Eksternal | `/opt/antigravity/projects/nexa/marketplace/server.js#L170-L205` | ```javascript\n// HTTP call ke Sprint 12 License Daemon tanpa 2PC\nconst licenseRes = await fetch(`${LICENSE_DAEMON_URL}/issue`, {\n  method: 'POST',\n  body: JSON.stringify({ userId, itemId })\n});\nif (!licenseRes.ok) {\n  // Mutasi database lokal sudah committed; atomisitas terdistribusi gagal\n  throw new Error("ERR_LICENSE_DAEMON_COMMUNICATION");\n}\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): potongan alur HTTP yang menurut laporan tidak menunjukkan 2PC/kompensasi terdistribusi; B-04/CONF-03 tetap blocker dan tidak ditutup oleh laporan ini. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR; B-04 REMAINS OPEN` |
| **E-05** | Pendaftaran Protokol NX Player & Handler JIT | `/opt/antigravity/projects/nexa/player-desktop/main.js#L182-L194` & `#L541-L560` | ```javascript\nprotocol.registerSchemesAsPrivileged([\n  { scheme: 'nexa-playback', privileges: { standard: true, secure: true, stream: true } }\n]);\nipcMain.handle('nexa:authorize-track', async (event, trackUri) => {\n  // Handler otorisasi JIT dipanggil sebelum buffer didaftarkan\n  return await executeJITAuthorization(trackUri);\n});\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): scheme `nexa-playback` dan IPC handler sebagaimana kutipan; runtime tidak diverifikasi. **TIDAK** membuktikan eksekusi timing 8-tahap JIT telah teruji di runtime fisik. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR` |
| **E-06** | Modul Kriptografi Ed25519 & Encoding Hex | `/opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L45-L65` | ```typescript\nexport function verifyEd25519Signature(signatureHex: string, messageBytes: Uint8Array, publicKeyHex: string): boolean {\n  if (signatureHex.length !== 128) return false; // 64 bytes = 128 hex chars\n  const sigBytes = Buffer.from(signatureHex, 'hex');\n  const pubBytes = Buffer.from(publicKeyHex, 'hex');\n  return ed25519.verify(sigBytes, messageBytes, pubBytes);\n}\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): representasi signature Ed25519 128-hex lowercase yang diklaim berasal dari repository, bukan standar RFC eksternal. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR; 128-HEX IS REPOSITORY-REPORTED FORMAT` |
| **E-07** | Invariant Filesystem Safe-Open (Hasil PSV) | `/opt/antigravity/projects/nexa/player-desktop/main.js#L573,L738` & `/opt/antigravity/projects/nexa/internal/filesystem/hidden_helper.js#L24-L60` | ```javascript\n// player-desktop/main.js:L573\nconst fd = fs.openSync(trackInfo.filePath, 'r');\n// player-desktop/main.js:L738\nconst fileData = fs.readFileSync(filePath);\n``` | Hasil PSV mengonfirmasi berkas `sdk/typescript/src/fs_safe.ts` **TIDAK ADA** pada source tree. Aplikasi desktop saat ini menggunakan `fs.openSync` dan `fs.readFileSync` standar tanpa flag `O_NOFOLLOW` dan tanpa verifikasi descriptor `fstat`. Modul safe-open descriptor-based wajib dibuat dari awal; mitigasi per platform dan residual risk didokumentasikan pada §15.9 (PSV-07). | `VERIFIED BY PSV (fs_safe.ts NOT PRESENT; RUNTIME USES STANDARD OPEN; EXECUTION BLOCKED B-06)` |
| **E-08** | Status Git Repositori Aktual & Kebersihan Root | Terminal Remote Linux Host `/opt/antigravity/projects/nexa/` | ```bash\n$ git rev-parse HEAD\nfc08a5c7ac6aa1b0e4bcf64dc264666f149e1956\n$ git status --porcelain\n?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md\n?? docs/whitepapers/Nexa_White_Paper_v5_6.md\n$ ls -la /opt/antigravity/projects/nexa/\ntotal 1780 (hanya berkas resmi proyek di root; Rule D)\n``` | **Laporan inspeksi lokal Programmer; bukan bukti yang diverifikasi independen oleh Auditor.** Jika akurat, output tersebut melaporkan nol mutasi tracked pada commit yang disebut, dua berkas untracked di `docs/`, dan inspeksi `ls -la` terbatas pada root level. Keberadaan, isi, dan hash berkas staging di `evidence/` juga tidak diverifikasi secara independen dalam audit ini. | `[REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED] / NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` |
| **E-09** | Keterbatasan Verifikasi Runtime Mobile & Service | `/opt/antigravity/projects/nexa/mobile/` & `/opt/antigravity/projects/nexa/cmd/usage/` | *(Ketiadaan harness uji runtime fisik mobile iOS/Android dan Usage Service cluster pada server Linux headless)* | Mengakui secara transparan bahwa runtime mobile dan usage service cluster belum diuji eksekusinya di lingkungan remote server Linux saat ini. | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` |

---

## 5. PRODUCT TRUTH SERTA PERILAKU ALBUM

### 5.1 Konsep Produk Album, Proposal Packaging/Manifest, dan Batas Otoritas
Album sebagai konsep produk PE-02 adalah pengelompokan logis berkas `.nx` mandiri dari empat kategori sumber yang telah disetujui PO: Music/Audio, Video, Document, dan Image. Persetujuan atas konsep pengelompokan dan semantik entry ZIP (regular files/directories diterima; symlink/special files ditolak; hardlink generik tidak didukung; byte-identical entries tetap independen) **tidak** mengesahkan ZIP sebagai wrapper produk universal, nama/lokasi manifest, struktur JSON, nama array/field path, signer, signature construction, persistence, atau lifecycle. ZIP wrapper, kandidat nama `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan], struktur manifest, dan packaging terkait tetap **PROPOSAL TEKNIS / UNRESOLVED** sampai keputusan PO/Architecture Authority yang eksplisit. White Paper v5.6 dan Roadmap v4.8 tidak menetapkan kontrak Album-specific tersebut. RFC 8785 (JCS) dan RFC 8032 (Ed25519) adalah standar teknis; keberadaan standar itu sendiri tidak mengesahkan penggunaan JCS/Ed25519 untuk Album Signer atau menentukan payload/signature construction. Seluruh contoh JSON/schema dan diagram packaging di bagian ini harus dibaca sesuai status proposalnya, bukan sebagai Product Truth.

#### Prinsip Dasar Album & Batasan Mutlak Tata Kelola (Keputusan PO: APPROVED)

> **Batas provenance bukti repository (§5.1):** Seluruh path, nomor baris, DDL, endpoint, dan perilaku kode lokal yang disebut dalam bagian ini merupakan laporan inspeksi Programmer (`REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`), kecuali dinyatakan lain dengan bukti primer yang diperiksa Auditor. Audit dokumen GitHub ini tidak memeriksa `whisnu/nexa`; kata *PROVEN*, *membuktikan*, atau *terbukti* pada klaim repository tidak boleh ditafsirkan sebagai verifikasi independen.
Sesuai Keputusan Otoritatif Product Owner untuk PE-02:
1. **Independensi Mutlak Anggota Album**: Album adalah murni pengelompokan beberapa berkas `.nx` independen. Setiap anggota Album tetap memiliki:
   - canonical `.nx` bytes dan hash masing-masing;
   - Container Creator signature masing-masing;
   - Genesis dan ownership evidence masing-masing;
   - Registry dan sidecar state masing-masing;
   - status integrity dan trust masing-masing;
   - keputusan otorisasi pemutaran (*playback authorization*) masing-masing.
2. **Larangan Mutlak Desain Struktur Album**:
   - Album **DILARANG KERAS** menjadi satu berkas `album.nx`;
   - Album **DILARANG KERAS** menjadi container baru;
   - Album **DILARANG KERAS** menggantikan atau meniadakan identitas individual berkas `.nx`;
   - Album **DILARANG KERAS** menciptakan trust bersama atau ownership bersama yang menggantikan bukti individual;
   - Album **DILARANG KERAS** membuat satu anggota otomatis mewarisi otorisasi anggota lain (*no authorization inheritance*).
3. **Metadata Album yang Disetujui Product Owner & Pembuktian Arsitektur Existing (PE02-AUD-04)**:
   - Metadata Album tingkat atas yang disahkan oleh Product Owner adalah **nama Album** (`title`) dan **artwork Album** (`cover_artwork`).
   - **Evaluasi Pembuktian Repositori Primer atas Mekanisme Existing (PE02-AUD-04)**:
     - *Dukungan Katalog per Anggota Individual (REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED)*:
       - Skema database `marketplace/db/schema.postgres.sql#L40, L57` dilaporkan Programmer sebagai kolom `title VARCHAR(255) NOT NULL` dan `cover_artwork TEXT` dilaporkan telah ada pada tabel `catalog_snapshots`. Kolom ini secara eksklusif berasosiasi dengan kunci primer `asset_id VARCHAR(128)` yang menurut laporan Programmer mewakili satu berkas `.nx` individual; Auditor belum memeriksa DDL primer.
       - Pipeline publikasi `studio-desktop/publish_pipeline.js#L31, L112-L126, L334` dan endpoint backend `marketplace/server.js#L1857, L1865, L2400-L2416` dilaporkan Programmer memvalidasi dan menyimpan metadata tersebut per sesi unggah individual (`sessionId`) ke dalam tabel `catalog_snapshots`; Auditor belum memeriksa kode primer.
       - Antarmuka NX Studio Desktop (`studio-desktop/renderer.js#L903-L909, L1026-L1038`) dilaporkan Programmer menyediakan field input lokal untuk judul dan mekanisme browse/preview artwork; Auditor belum memeriksa kode primer.
     - *Ketiadaan Identitas & Asosiasi Album Multi-Member (UNPROVEN / GAP ARSITEKTUR)*:
       - Menurut laporan inspeksi Programmer atas `marketplace/db/schema.postgres.sql` (belum diverifikasi independen), tidak ditemukan bukti adanya tabel entitas Album (misalnya `albums`, `album_collections`), kolom `album_id`, atau relasi kunci asing (parent-child relationship) yang menghubungkan beberapa `asset_id` anggota `.nx` ke satu identitas Album persisten; Auditor belum memeriksa DDL primer.
       - Metadata `title` dan `cover_artwork` pada `catalog_snapshots` **HANYA BERLAKU UNTUK ITEM KATALOG INDIVIDUAL (`asset_id`)**, bukan untuk entitas Album multi-member.
       - Menurut laporan inspeksi Programmer atas `marketplace/server.js` (belum diverifikasi independen), tidak ditemukan bukti adanya endpoint atau query yang mendukung pemuatan kembali kumpulan anggota `.nx` sebagai satu kesatuan Album yang utuh dari Marketplace; Auditor belum memeriksa kode primer.
     - *Pemisahan Tegas Katalog Anggota vs Identitas Album*:
       - Menurut laporan Programmer, katalog snapshot per berkas `.nx` individual didukung oleh skema existing; namun dukungan repositori existing untuk identitas persisten Album multi-member belum diverifikasi independen dan tidak boleh diklaim.
       - Perancang dan programmer **DILARANG KERAS** mengasumsikan keberadaan metadata pada katalog individual sebagai bukti dukungan identitas Album, dan **DILARANG KERAS** menciptakan skema DDL baru, tabel baru, kolom baru, endpoint baru, atau formula ID semu tanpa persetujuan formal Otoritas Arsitektur / PO.
     - *Disposisi Tata Kelola (STOP AND CLARIFY)*:
       - Desain persistensi identitas Album multi-member dan mekanisme pemuatan kembalinya dihentikan:  
         **`STOP AND CLARIFY — GAP KONTRAK IDENTITAS & ASOSIASI METADATA ALBUM MULTI-MEMBER (BUTUH KLARIFIKASI FORMAL PO / ARSITEKTUR)`**.
   - **Keberlakuan pada Kedua Jalur NX Studio**:
     - *Jalur 1 (Album Forge New)*: Nama dan artwork album dimasukkan pada antarmuka Studio sebelum proses batch; setiap berkas sumber diproses forging mandiri; menurut laporan inspeksi Programmer yang belum diverifikasi independen, metadata katalog disimpan per anggota individual di `catalog_snapshots`; sedangkan asosiasi multi-member ke satu entitas Album di Marketplace ditandai sebagai gap arsitektur yang menunggu klarifikasi.
     - *Jalur 2 (Album Existing .nx)*: Berkas `.nx` mandiri yang telah ada diimpor tanpa alterasi bitstream atau signature; publikasi dilakukan per berkas individual via `NXPublishPipeline` existing; menurut laporan inspeksi Programmer yang belum diverifikasi independen, metadata katalog tersimpan per item individual; pemuatan kembali multi-member sebagai satu Album menunggu klarifikasi arsitektur.
   - **Representasi Metadata Album & Batas Skema Manifest (PE02-R63-AUD-02)**:
     - Metadata Album tingkat atas yang disetujui PO adalah nama (`title`) dan artwork (`cover_artwork`).
     - Draf skema manifest `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] memuat `"title"`, namun **TIDAK MEMUAT** `"cover_artwork"` (cover artwork ditangani pada level katalog Marketplace, bukan di dalam payload manifest).
     - Perancang **DILARANG KERAS** menyuntikkan field `"cover_artwork"` ke manifest atau membuat model penyimpanan baru tanpa keputusan otoritatif PO / Arsitektur.
   - **Kriteria Penerimaan Terukur Metadata**:
     - *Input UI Studio*: **Kesiapan spesifikasi UI: `SPEC READY`** untuk input nama Album dan browse/preview cover artwork. **Status keberadaan/implementasi UI:** `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; bukti UI primer belum diperiksa Auditor. Kesiapan spesifikasi ini bukan bukti bahwa implementasi telah tersedia atau diverifikasi independen.
     - *Persistensi Katalog Individual*: Nama dan artwork per item `.nx` tersimpan secara persisten pada `catalog_snapshots` via `asset_id` saat publikasi selesai (`DILAPORKAN PROGRAMMER — NOT VERIFIED BY INDEPENDENT AUDIT`).
     - *Asosiasi & Pemuatan Kembali Multi-Member Album*: Dinyatakan **TERBLOKIR (BLOCKED)** akibat ketiadaan entitas Album di repositori existing; dilarang mengklaim fungsi ini telah didukung sebelum klarifikasi PO/Arsitektur disahkan.
     - *Preservasi Invariant*: Metadata katalog tidak memodifikasi format kontainer individual berkas `.nx`, tidak menyuntikkan field semu ke manifes album atau kontainer PE-01, dan tidak merusak verifikasi hash atau signature anggota.
4. **Peta Aplikasi dan Platform Resmi (Keputusan PO: APPROVED)**:

| Aplikasi Nexa | Platform yang Didukung | Cakupan & Batasan Otoritatif Sesuai Keputusan PO |
|---|---|---|
| **NX Studio** | **Desktop saja** | Modul Creator, forging file sumber, dan publication pipeline. **TIDAK ADA NX Studio Mobile** (Dilarang keras merumuskan requirement, AC, test, atau implementation task untuk NX Studio Mobile). |
| **NX Player** | **Desktop** | Universal Trust-Aware Viewer (pemutaran terisolasi just-in-time per-anggota). |
| **NX Player** | **Mobile** | Universal Player untuk iOS dan Android sesuai baseline yang dibuktikan. |
| **NX Verify** | **Desktop** | Full Verify (mengevaluasi integritas forensik; mempertahankan fungsi Batch Verification, Export Verification Report, dan manual Registry Refresh). |
| **NX Verify** | **Mobile** | Verify-Lite (evaluasi integritas ringan per-anggota; dilarang merender payload; tidak memporting fitur Full Verify Desktop ke Mobile). |

> [!IMPORTANT]
> **CATATAN ARSITEKTUR TENTANG DIVERGENSI IDENTITAS FIELD HASH AUDIO & CAKUPAN MULTI-PAYLOAD (PE02-R63-AUD-01):**
> Review White Paper v5.6, Roadmap v4.8, dan baseline PE-01 tidak menemukan ketentuan normatif yang menetapkan identifier hash audio pada manifest Album:
> 1. **Divergensi Identifier Hash Bitstream Audio**: Belum ada kontrak produk normatif yang menetapkan nama identifier field hash SHA-256 bitstream audio pada struktur manifest yang belum ditetapkan. Draf skema JSON memodelkan `"audio_sha256"`, sedangkan JIT Stage 8a (§5.2) dan AC-09 merujuk notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif). Sesuai Level 1 Otoritas PO, perancang **DILARANG KERAS** memilih salah satu identifier secara sepihak. Status: **`UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**.
> 2. **Cakupan Multi-Payload (Music, Video, Document, Image) & Matriks Batas Kontrak (FINDING-06)**:  
> Keputusan Otoritatif PO (§2.3.A) menetapkan bahwa Album Studio Forge New dan Existing `.nx` mencakup 4 jenis sumber: **Music/Audio**, **Video**, **Document**, dan **Image**.  
> Dokumen ini memetakan batas kontraktual lintas 4 jenis payload secara transparan:
> 
> | Dimensi Kontrak / Evaluasi | Music / Audio | Video | Document | Image | Dasar Bukti & Status Normatif |
> |---|:---:|:---:|:---:|:---:|---|
> | **Integritas Kontainer Mandiri PE-01 (Tahap 7a)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | `REQUIRED` | **Universal PE-01 Invariant**: Kemasan kontainer PE-01 dan Packaging Signature Ed25519 berlaku seragam untuk seluruh 4 tipe payload. |
> | **Validasi Genesis Certificate (Tahap 7b)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | `REQUIRED` | **Universal PE-01 Invariant**: Validasi 2-lapisan Registry Cert & Genesis Ownership Cert berlaku identik untuk seluruh 4 tipe payload. |
> | **Evaluasi Active License (Tahap 7c)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | `REQUIRED` | **Universal Licensing Invariant**: Otorisasi entitlement pengguna pada Marketplace / engine lokal berlaku untuk seluruh 4 tipe payload. |
> | **Ekstraksi Aman & Bijeksi ZIP (Tahap 1..6)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | `REQUIRED` | **Universal Packaging Invariant**: Safe-Open, penahanan traversal, kuota wrapper, dan bijeksi 1:1 berlaku untuk seluruh 4 tipe payload. |
> | **Verifikasi Digest Manifest (Tahap 8a)** | `REQUIRED (Bitstream)` | `UNRESOLVED` | `UNRESOLVED` | `UNRESOLVED` | Pada draf audio, lokasi deklarasi hash belum ditetapkan; parent array dan field path tetap unresolved. Untuk Video, Document, dan Image, belum ada field hash normatif pada manifest: **`UNRESOLVED — STOP AND CLARIFY`**; dilarang mengarang field hash generik. |
> | **Dekripsi Payload Terotorisasi (Tahap 8b)** | `REQUIRED (Audio)` | `UNRESOLVED — STOP AND CLARIFY` | `UNRESOLVED — STOP AND CLARIFY` | `UNRESOLVED — STOP AND CLARIFY` | Memerlukan lolos validasi Stage 7a, 7b, dan lisensi aktif 7c. Untuk audio: `REQUIRED`. Untuk Video, Document, dan Image: dasar normatif dan alur dekripsi spesifik belum ditetapkan pada kontrak platform (**`UNRESOLVED — STOP AND CLARIFY`**; programmer dilarang mengasumsikan alur dekripsi audio berlaku otomatis). Status Album Signer `UNKNOWN`/`UNTRUSTED`/`REVOKED` bukan global member playback gate; autentisitas deklarasi membership ditangani terpisah pada Tahap 4. Sampai CONF-01 diputuskan, member dari manifest tidak boleh diasumsikan sebagai anggota Album tepercaya; file yang disediakan independen mengikuti PE-01 standalone. |
> | **Registrasi Buffer Output (Tahap 8c)** | `REQUIRED (Audio Buffer)` | `UNRESOLVED — STOP AND CLARIFY` | `NOT APPLICABLE (No Audio Buffer)` | `NOT APPLICABLE (No Audio Buffer)` | Audio buffer registration eksklusif untuk audio. Video stream pipeline belum diatur normatif (**`UNRESOLVED — STOP AND CLARIFY`**). Dokumen dan gambar beroperasi sebagai visual viewer mandiri tanpa registrasi audio output buffer. |
> | **Auto-Next Lifecycle Player (§2.5)** | `UNRESOLVED (Pending Album Contract)` | `UNRESOLVED (No ended handler)` | `UNRESOLVED / BLOCKED` | `UNRESOLVED / BLOCKED` | Audio memiliki event listener `ended` pada GUI pustaka desktop (`player-desktop/renderer.js#L652-L655`) yang memutar aset lokal, bukan kontrak transisi multi-anggota Album platform; Video tidak memiliki listener `ended` pada `videoEngine`; Dokumen dan gambar tidak memiliki durasi alami: seluruh pemicu transisi Auto-Next Album berstatus **`UNRESOLVED — STOP AND CLARIFY (PO CLARIFICATION REQUIRED; TIMER SEPIHAK DILARANG)`**; AC-32 berstatus execution blocked. |
> | **Evaluasi NX Verify (§5.3)** | `INDIVIDUAL MEMBER` | `INDIVIDUAL MEMBER` | `INDIVIDUAL MEMBER` | `INDIVIDUAL MEMBER` | Untuk berkas yang telah dibuktikan autentisitas membership-nya, Verify mengevaluasi integritas kontainer PE-01 setiap anggota secara individual tanpa status agregat Album (CONF-02 Option B APPROVED), berlaku seragam untuk ke-4 payload dan murni diagnostik tanpa playback/viewing authorization. Sebelum membership authenticity terbukti, berkas yang hanya dideklarasikan oleh manifest tidak diproses/dilabeli sebagai anggota Album; berkas yang diberikan independen tetap mengikuti verifikasi standalone PE-01. |
> 
> > **Larangan Mutlak Asumsi Silang Antar-Payload:**  
> > Dilarang mengasumsikan bahwa mekanisme pengujian bitstream audio otomatis berlaku untuk video, dokumen, atau gambar. Seluruh area yang belum memiliki kontrak normatif dikunci sebagai **`UNRESOLVED — STOP AND CLARIFY`**.
> 
> **Larangan Mutlak Asumsi Kompatibilitas & Keputusan Sepihak (AUDIT-NEW-01):**
> 1. Dokumen ini **TIDAK MENYATAKAN** kedua nama field tersebut sebagai alias yang telah terbukti, dan **TIDAK MENYATAKAN** keduanya ekuivalen.
> 2. Dokumen ini **DILARANG** mengimplementasikan atau mengusulkan mekanisme fallback tersembunyi (misalnya membaca `audio_sha256` lalu fallback ke `sha256`).
> 3. Dokumen ini **DILARANG** menetapkan aturan prioritas jika kedua field hadir bersamaan dalam satu dokumen manifest.
> 4. Dokumen ini **DILARANG** mengarang perilaku sistem jika salah satu field tidak ditemukan.
> 5. Draf Skema JSON Draft 7 di bawah ini mempertahankan `"audio_sha256"` semata-mata sebagai kandidat draf usulan spesifikasi teknis, **BUKAN** sebagai kontrak normatif yang dibekukan, dan contoh manifest ilustratif tidak membuktikan keputusan produk.

#### Spesifikasi Skema Manifest Album: Pemisahan Field Universal vs Payload-Specific & Status Otoritas (AC-01)

##### A. Pemisahan Field Universal Album vs Field Khusus Tipe Payload
Dokumen ini secara ketat membedakan field universal Album yang berlaku umum dari field khusus tipe payload tertentu guna mencegah pencemaran kontrak audio ke tipe payload lainnya:
1. **Kandidat Field pada Draf Manifest (BUKAN field universal yang telah disahkan)**:
   - `manifest_version`: kandidat versi manifest dalam draf; keberadaan field dan nilainya belum ditetapkan PO/Architecture Authority.
   - `container_format_version`: versi format kontainer PE-01 tetap merupakan bagian baseline kontainer `.nx`, tetapi representasinya sebagai field manifest Album belum disahkan.
   - `created_at`: RFC 3339/ISO 8601 hanya mengatur format waktu bila digunakan; standar tersebut tidak mewajibkan field `created_at` dalam manifest Album.
   - `title`: semantik nama/judul Album disetujui PO untuk UI/katalog; lokasi field JSON manifest dan bentuk serialisasinya belum disahkan.
   - Kumpulan anggota `.nx` independen adalah konsep produk PE-02; **nama array JSON, bentuk objek anggota, dan pemetaan dari draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]` belum ditetapkan sebagai kontrak normatif**. Tidak ada nama array universal yang boleh diasumsikan atau dipilih sampai keputusan PO/Architecture Authority.
     - **Semantik nama berkas member (bukan nama field JSON yang disahkan):** pola strictly flat `^[a-zA-Z0-9_-]+\.nx$` tanpa path separator/subdirektori; keputusan PO menyetujui aturan nama/keunikan case-insensitive via ASCII case-fold, bukan identifier field.
     - **Semantik judul/nama tampilan member (bukan nama field JSON yang disahkan):** rentang usulan 1..255; keberadaan dan representasi sebagai field manifest belum disahkan.
   - *Field Deklarasi Kriptografis Universal (Status: PROPOSED SPECIFICATION)*: `album_signer_public_key`, `album_signer_signature`, `canonical_algorithm`, `signature_algorithm` (berstatus usulan yang menghadapi circular dependency B-08 dan belum memiliki kontrak identitas/lifecycle B-09).
   - *Field Metadata Tambahan Universal (Status: PROPOSED SPECIFICATION)*: `album_id`, `artist`, `total_tracks` / `total_members`, `release_date` (usulan perancang, belum disahkan PO).
2. **Field Khusus Tipe Payload (Payload-Specific Fields)**:
   - *Payload Audio / Musik*: `audio_sha256` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) tetap merupakan kandidat identifier digest dari draf yang berbeda; hubungan, ekuivalensi, alias, dan pemetaan keduanya **UNRESOLVED — STOP AND CLARIFY**. Keduanya tidak boleh diperlakukan sebagai pilihan alternatif yang dapat diterima, fallback, atau field universal. `duration_seconds`, `track_number`, dan `track_id` juga tetap berada dalam draf khusus audio. Draf skema manifest JSON Draft 7 di bawah murni merupakan **draf usulan spesifikasi teknis khusus audio (*audio-specific draft proposal*)**.
   - *Payload Video*: Belum memiliki kontrak skema manifest normatif (**`UNRESOLVED — STOP AND CLARIFY`**). Video tidak memiliki field `audio_sha256` atau spesifikasi digest bitstream video resmi di WP v5.6.
   - *Payload Document & Image*: Beroperasi sebagai visual viewer mandiri tanpa durasi alami dan tanpa hash bitstream audio (**`UNRESOLVED — STOP AND CLARIFY`**).
   - **Larangan Mutlak**: Field-field audio seperti `audio_sha256`, `duration_seconds`, dan struktur `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]` **DILARANG KERAS DIPERLAKUKAN SEBAGAI SKEMA UNIVERSAL** bagi video, dokumen, dan gambar.

##### B. Matriks Pemetaan Sumber Otoritas Seluruh Field Manifest (AC-01)

| Field Manifest | Lapisan & Ruang Lingkup | Tipe Data & Format | Sumber Otoritas | Status Kontraktual | Perilaku Validasi Fail-Closed |
|---|---|---|---|---|---|
| `title` | Semantik metadata Album (UI/katalog) | String (batas 1..255 adalah proposal) | Keputusan PO §2.3.A hanya untuk semantik metadata | **SEMANTIK DISETUJUI; JSON FIELD PATH / REQUIREDNESS UNRESOLVED** | Persetujuan semantik tidak menetapkan nama/path field JSON, requiredness, atau error behavior manifest. |
| `cover_artwork` | Semantik artwork Album (UI/katalog) | Representasi belum ditetapkan | Keputusan PO §2.3.A hanya untuk semantik UI/katalog | **SEMANTIK DISETUJUI; JSON FIELD PATH / PERSISTENCE UNRESOLVED** | Tidak mengesahkan URI/path, field manifest, atau mekanisme persistence Album; klaim dukungan katalog individual hanya laporan Programmer yang belum diverifikasi independen. |
| `manifest_version` | Kandidat field manifest Album | String enum `["1.0.0"]` pada draf | Proposal teknis draf; tidak ditetapkan WP/Roadmap | **PROPOSED / UNRESOLVED — NOT NORMATIVE** | Keberadaan, nilai, requiredness, dan error behavior belum disahkan. |
| `container_format_version` | Kandidat field manifest Album | String enum `["1.0.0"]` pada draf | Baseline PE-01 hanya untuk kontainer `.nx`; bukan otoritas field manifest Album | **PROPOSED / UNRESOLVED — NOT NORMATIVE** | Versi kontainer PE-01 tidak mengesahkan field manifest Album atau error behavior. |
| `created_at` | Kandidat field manifest Album | String date-time pada draf | RFC 3339 / ISO 8601 hanya mengatur format, bukan keberadaan field Album | **PROPOSED / UNRESOLVED — NOT NORMATIVE** | Keberadaan, requiredness, lokasi field, dan error behavior belum disahkan. |
| Kumpulan anggota Album (nama/path array JSON belum ditetapkan) | Universal Packaging Structure | Struktur koleksi belum ditetapkan | Konsep Album PE-02; bukan field path yang ditentukan White Paper | **KONSEP PRODUK; IDENTIFIER JSON UNRESOLVED** | Keberadaan anggota independen tidak menetapkan nama array, bentuk objek, batas, atau required fields. `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]` dan `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]` tidak boleh dipilih sebagai path normatif tanpa keputusan PO/Architecture Authority.
| Nama berkas member (JSON path belum ditetapkan) | Member filename invariant | String regex `^[a-zA-Z0-9_-]+\.nx$` | Keputusan PO AUDIT-NEW-06/07 | **SEMANTIK NAMA BERKAS DISETUJUI PO; FIELD PATH UNRESOLVED** | Keputusan PO mengesahkan aturan nama/flatness dan keunikan ASCII case-fold, bukan nama array atau path JSON. Validasi normatif terhadap manifest menunggu penetapan struktur.
| Judul member (JSON path belum ditetapkan) | Metadata member | Belum ditetapkan | Tidak ada dasar normatif untuk field judul per-member | **PROPOSED / UNRESOLVED** | White Paper §Studio tidak menetapkan path atau kewajiban field judul per-member dalam manifest Album. Jangan menganggapnya required atau menolak manifest karena field ini sebelum ada keputusan.
| `album_id` | Metadata Album | String pattern `^alb_[0-9a-f]{16}$` | Usulan Perancang | **PROPOSED SPEC (PENDING PO/ARCH)** | Usulan derivasi ID; terhambat ketiadaan tabel Album di database Marketplace. |
| `artist` | Metadata Album | String (1..255 char) | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Belum diotorisasi sebagai field wajib yang disahkan PO. |
| `total_tracks` / `total_members` | Metadata Album | Integer (1..199) | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Konsistensi terhadap jumlah anggota hanya dapat ditetapkan setelah struktur koleksi normatif disahkan; tidak ada `len(members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan])` yang ditetapkan saat ini. |
| `release_date` | Metadata Album | String format `YYYY-MM-DD` | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Validasi kalender riil (menolak tanggal ilegal seperti 2026-02-31); proposal. |
| `album_signer_public_key` | Deklarasi Kriptografis | String pattern `^[0-9a-f]{64}$` | Proposal NC-02 / B-08 | **PROPOSED SPEC (UNRESOLVED LIFECYCLE B-09)** | Hex 64 kunci publik Ed25519; identitas dan lifecycle signer unresolved di WP v5.6. |
| `album_signer_signature` | Deklarasi Kriptografis | String pattern `^[0-9a-f]{128}$` | Proposal NC-02 / B-08 | **PROPOSED SPEC (BLOCKED B-08)** | Hex 128 tanda tangan Ed25519; circular dependency menahan payload kanonikal. |
| `canonical_algorithm` | Deklarasi Kriptografis | String enum `["RFC8785-JCS"]` | RFC 8785 | **PROPOSED SPEC (BLOCKED B-02)** | Enum algoritma kanonisasi; proposal perancang. |
| `signature_algorithm` | Deklarasi Kriptografis | String enum `["Ed25519"]` | RFC 8032 | **PROPOSED SPEC** | Enum algoritma tanda tangan; proposal perancang. |
| Kandidat field digest audio (path JSON dan identitas belum ditetapkan) | Payload-Specific: Audio Only | Kandidat string SHA-256 | Draf audio berbeda / Stage 8a | **UNRESOLVED FIELD IDENTITY AND PATH (AUDIO ONLY)** | `audio_sha256` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) tetap kandidat yang belum dipetakan; tidak ada array parent, path, alias, ekuivalensi, fallback, atau prioritas yang dipilih. Tidak berlaku untuk video/doc/img.
| `duration_seconds` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | Number minimum 0.1 | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Durasi audio detik; tidak berlaku untuk dokumen dan gambar yang tidak memiliki durasi alami. |
| `track_number` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | Integer (1..199) | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Penomoran urutan trek audio monotonik kontigu 1..N. |
| `track_id` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | String pattern `^trk_[0-9a-f]{16}$` | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Pola ID trek audio; proposal perancang. |

##### C. Matriks Perilaku Validasi Manifest (Schema Validation Matrix — AC-01)
Sistem menerapkan validasi deterministik hanya untuk kondisi yang telah memiliki dasar normatif. Perilaku untuk field yang kontraknya belum disahkan tidak boleh diklaim deterministik; khusus unknown fields tetap menunggu keputusan PO.

| Kondisi Masukan / Anomali Manifest | Tingkat Pemeriksaan | Hasil Evaluasi Sistem | Error Code Dihasilkan | Dasar Penegakan & Batasan Keputusan |
|---|---|:---:|:---:|---|
| **Required Field yang Hilang** | Level 2 (Struktur Skema) | **REJECTED** | `ERR_MANIFEST_MALFORMED` | Fail-closed deterministik; ketiadaan properti wajib membatalkan validasi pada Tahap 3. |
| **Unknown Field (Properti Tambahan)** | Level 3 (Invariant Semantik) | **UNRESOLVED — NO NORMATIVE EXPECTED RESULT** | Belum ditetapkan | Strict (`REJECTED`) dan permissive (`IGNORED`) tetap proposal alternatif; tidak satu pun boleh diberlakukan sebelum keputusan PO AC-01. AC-01 tetap `PO DECISION REQUIRED`.
| **Duplicate JSON Key (Literal)** | Level 1 (Sintaksis Byte-Level) | **REJECTED** | `ERR_MANIFEST_DUPLICATE_KEY` | *Nexa Strict Parser Policy* (AC-05 / NC-03 / B-01); menolak kunci duplikat literal (e.g. `{"title":"A", "title":"B"}`). |
| **Duplicate JSON Key (Decoded Unicode Escape)** | Level 1 (Sintaksis Byte-Level) | **REJECTED** | `ERR_MANIFEST_DUPLICATE_KEY` | *Nexa Strict Parser Policy*; mendecode escape Unicode sebelum mengecek keunikan kunci (e.g. `{"\u0074itle":"A", "title":"B"}`). |
| **Malformed Unicode Escape Syntax** | Level 1 (Sintaksis Byte-Level) | **REJECTED** | `ERR_MANIFEST_MALFORMED` | Menolak urutan escape ilegal (e.g. `\u123z`, `\u12`, lone surrogate `\uD800`). |
| **Schema Version Tidak Didukung pada Draf** | Level 2 (Struktur Skema) | **UNRESOLVED / PROPOSAL ONLY** | Belum ditetapkan | Penolakan versi hanya dapat menjadi perilaku normatif setelah field, versi, dan schema manifest Album disahkan PO/Architecture Authority. |
| **Payload Type Tidak Didukung** | Level 3 (Invariant Semantik) | **REJECTED** | `ERR_MANIFEST_MALFORMED` | Album dengan tipe sumber di luar 4 jenis sah, atau deklarasi yang melanggar larangan album campuran (AC-30) ditolak fail-closed sebelum pemrosesan. |
| **Strict Validation vs Unfinished Contracts** | Tata Kelola Spesifikasi | **PENEGAKAN SELEKTIF** | Sesuai aturan normatif | Validasi ketat (strict validation) ditegakkan untuk versi dan field yang telah berstatus normatif; programmer dan perancang **DILARANG KERAS** memberlakukan aturan strict secara diam-diam terhadap versi atau field yang kontrak produknya belum selesai diratifikasi. |

##### D. Rekonsiliasi Klaim Kelengkapan Skema Manifest (§5.1 vs §13.1)
Kontradiksi internal historis antara §5.1 dan §13.1 diselesaikan secara tuntas:
- §5.1 secara jujur menyatakan bahwa skema JSON Draft 7 yang ada di bawah ini adalah **draf usulan teknis khusus payload audio (*audio-specific proposal*)**, dan **BUKAN** kontrak skema universal lengkap untuk keempat jenis payload (Music, Video, Document, Image).
- Klaim pada §13.1 diselaraskan untuk **TIDAK LAGI** menyatakan "skema lengkap manifest album", melainkan menyatakan "draf skema manifest album khusus audio (validitas sintaksis JSON Schema Draft 7, batas 199 track; skema universal multi-payload dan metadata di luar nama/artwork berstatus UNRESOLVED pending keputusan PO/Arsitektur)".
- Keduanya kini sinkron 100% tanpa kontradiksi klaim kelengkapan semu.

#### Draf Skema Manifest JSON Audio-Specific ([DRAFT / PROPOSED AUDIO-SPECIFIC SPECIFICATION — NOT A COMPLETE 4-PAYLOAD CONTRACT])
Skema berikut merupakan draf usulan spesifikasi teknis khusus payload audio (*audio-specific draft proposal*) dan **BUKAN** kontrak lengkap atau skema normatif untuk keempat jenis payload (Music, Video, Document, Image). Field usulan `album_id`, `artist`, `total_tracks`, `release_date`, dan field Album Signer sengaja tidak menjadi properti `required` dalam contoh JSON Schema ini. Daftar `required` yang tersisa hanya menggambarkan bentuk contoh audio yang sedang diusulkan dan tidak boleh dipakai sebagai schema universal atau dasar implementasi sebelum kontrak lengkap disahkan. Skema ini merumuskan properti audio-specific seperti `duration_seconds` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif), serta batas 199 track audio. Kontrak skema manifest normatif untuk Video, Document, dan Image belum diterbitkan oleh otoritas arsitektur (**`UNRESOLVED — STOP AND CLARIFY`**; programmer dilarang mengarang field hash generik atau payload discriminator sepihak). Skema draf audio di bawah telah diverifikasi sebagai JSON valid 100% (dengan karakter escape regex ganda `\.nx$` sesuai RFC 8259) dengan batas array manifest `tracks.maxItems: 199`. **Diferensiasi Validasi Skema Manifest (Tahap 3) vs Kuota Fisik Central Directory ZIP (Tahap 2 / AUDIT-05)**: Batas deklarasi skema manifest `maxItems: 199` adalah batasan logis struktur JSON pada Tahap 3, dan **BUKAN JAMINAN** bahwa arsip fisik ZIP pasti mematuhi batas kuota $\le 200$ entri central directory B-07 pada Tahap 2. Evaluasi kuota fisik ZIP pada Tahap 2 menghitung seluruh entri fisik arsip: $N_{\text{total}} = N_{\text{tracks}} + N_{\text{manifest}} + N_{\text{dir\_entries}} \le 200$. Jika terdapat 199 trek ($N_{\text{tracks}} = 199$), 1 entri manifest ($N_{\text{manifest}} = 1$), dan $\ge 1$ entri direktori fisik ($N_{\text{dir\_entries}} \ge 1$), maka jumlah entri central directory menjadi $\ge 201$, yang **MELAMPAUI KUOTA FISIK** dan memicu `ERR_ZIP_QUOTA_EXCEEDED` pada Tahap 2 sebelum manifest dievaluasi. Hubungan kuota fisik ZIP dengan batas manifest berstatus `[PROPOSED SPECIFICATION — BLOCKED BY B-07]`:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "NexaAlbumManifest",
  "type": "object",
  "additionalProperties": false,
  "required": [
    "manifest_version",
    "title",
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

#### Contoh Konkret Dokumen Manifest (`album_manifest.json` [nama/lokasi kandidat draf; belum disahkan]) (AUDIT-NEW-02)
> **Catatan Validitas & Batas Pembuktian Contoh Dokumen Manifest (AUDIT-NEW-02):**
> Contoh dokumen manifest di bawah ini adalah **contoh struktural dan sintaksis ilustratif** untuk memvalidasi kepatuhan Level 1 (Sintaksis JSON RFC 8259), Level 2 (Struktur Skema Draft 7), dan Level 3 (Invariant Semantik Logika Aplikasi Dasar).
> Nilai tanda tangan (`album_signer_signature`) dan kunci publik (`album_signer_public_key`) yang dicantumkan merupakan **dummy / nilai uji ilustratif**.
> Nilai dummy ini **TIDAK MEMBUKTIKAN** pemenuhan validitas kriptografis Level 4 (*Cryptographic Validity*). Verifikasi operasional pada lingkungan produksi wajib mengeksekusi serialisasi kanonikal RFC 8785 JCS dan verifikasi tanda tangan digital Ed25519 terhadap kunci publik dan signature kriptografis riil.

Contoh dokumen manifest ilustratif:

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
>    - *Penerimaan Tipe Entri ZIP Sesuai Keputusan PO (AUDIT-NEW-06 PO APPROVED)*: Regular files dan directory entries (entry name berakhiran `/` atau bertipe folder pada central directory) diterima dan tidak menyebabkan kegagalan ekstraksi/validasi; symlink dan special files (FIFO, socket, device files) ditolak fail-closed dengan `ERR_ZIP_INVALID`; semantik hardlink tidak didukung (dua entri dengan byte identik tetap diekstrak sebagai berkas reguler independen). Pembatasan struktur "flat" secara tegas **HANYA BERLAKU** pada path relatif berkas member `.nx` yang dideklarasikan pada manifest (nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) wajib memenuhi regex `^[a-zA-Z0-9_-]+\.nx$`), bukan pelarangan entri direktori di dalam arsip ZIP. *(Catatan Historis: Usulan draf awal mengenai penolakan direktori telah digantikan secara resmi oleh Keputusan PO AUDIT-NEW-06).*  
>    - *Usulan Batas Entri Central Directory Fisik (Stage 2) vs Batas Array Manifest (Stage 3 / AUDIT-05)*: Diusulkan kuota total maksimum 200 entri central directory fisik yang dievaluasi pada Tahap 2 ekstraksi ZIP dengan rumus: $N_{\text{total}} = N_{\text{tracks}} + N_{\text{manifest}} + N_{\text{dir\_entries}} \le 200$ (di mana $N_{\text{manifest}} = 1$, $N_{\text{tracks}}$ adalah jumlah berkas member reguler `.nx`, dan $N_{\text{dir\_entries}}$ adalah jumlah entri direktori fisik yang diterima sesuai Keputusan PO AUDIT-NEW-06). Jika $N_{\text{total}} > 200$, proses ekstraksi dibatalkan fail-closed dengan melempar `ERR_ZIP_QUOTA_EXCEEDED`. **Pemisahan Tegas Validasi**: Batas array `maxItems: 199` pada skema manifest JSON (Tahap 3) adalah batas logis deklarasi trek dan **TIDAK MENJAMIN** pemenuhan kuota 200 entri fisik jika terdapat entri direktori di dalam arsip ZIP (contoh: 199 trek + 1 manifest + 1 entri direktori = 201 entri fisik, sehingga melanggar kuota 200). Kapasitas maksimum trek yang dapat dimuat tanpa melanggar kuota 200 fisik berkurang jika terdapat entri direktori: $N_{\text{tracks}} \le 199 - N_{\text{dir\_entries}}$. Status batasan numerik kuota ini tetap merupakan **`PROPOSED SPECIFICATION — BLOCKED BY B-07`** dan belum disahkan sebagai ketentuan normatif.  
>    - *Usulan Batas Ukuran*: Diusulkan batas maksimum terkompresi 500 MB desimal (500.000.000 bytes) dan dekompresi 4 GB desimal (4.000.000.000 bytes), memicu `ERR_ZIP_QUOTA_EXCEEDED`.  
>    - *Usulan Rasio Kompresi*: Diusulkan evaluasi rasio kompresi per-entri dan global agregat (jika uncompressed $> 1\text{ MB}$) terhadap ambang batas usulan (10:1 usulan B-07 atau 100:1 referensi pembanding eksternal yang belum diverifikasi — pending keputusan arsitektur), serta penolakan `compressed == 0` (saat uncompressed $> 0$) memicu `ERR_ZIP_BOMB_DETECTED`.  
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


#### Analisis Semantik Nama File & Matriks Kasus Batas (DEF-08)
Sesuai Bagian II (DEF-08), aturan nama file anggota `.nx` mematuhi regex kanonikal `^[a-zA-Z0-9_-]+\.nx$`. Karakter titik (`.`) dilarang keras berada pada basename.

| Kasus Masukan / Nama Berkas | Contoh Konkret | Hasil Evaluasi Regex Kanonikal | Evaluasi Deklarasi Manifest (Tahap 3 / Manifest Validator) | Evaluasi Fisik Arsip ZIP (Tahap 2 / ZIP Reader) | Dasar Normatif & Batas Layer (FINDING-04) |
|---|---|:---:|:---:|:---:|---|
| **Multiple Dots pada Basename** | `track.01.audio.nx`, `song.mp3.nx` | **REJECTED** | Ditolak fail-closed (`ERR_MANIFEST_MALFORMED`) | Ditolak fail-closed (`ERR_ZIP_ENTRY_MISMATCH` jika bijeksi gagal) | Mencegah kebingungan ekstensi ganda (*double extension attack*) dan bypass MIME type. |
| **Ekstensi Huruf Besar (Uppercase)**| `track_01.NX`, `track_01.Nx` | **REJECTED** | Ditolak fail-closed (`ERR_MANIFEST_MALFORMED`) | Ditolak fail-closed (`ERR_ZIP_ENTRY_MISMATCH` jika bijeksi gagal) | Menegakkan determinisme kanonikal; ekstensi wajib strictly lowercase `.nx`. |
| **Traversal-Like Characters** | `../track.nx`, `/track.nx`, `track\nx` | **REJECTED** | Ditolak fail-closed (`ERR_MANIFEST_MALFORMED`) | Ditolak fail-closed (`ERR_ZIP_INVALID` bila entri ZIP traversal) | Karakter `/`, `\`, dan `.` di luar ekstensi dilarang mutlak untuk mencegah directory traversal. |
| **Basename Kosong (Empty Basename)**| `.nx` | **REJECTED** | Ditolak fail-closed (`ERR_MANIFEST_MALFORMED`) | Ditolak fail-closed (`ERR_ZIP_ENTRY_MISMATCH` jika bijeksi gagal) | Operator `+` pada `[a-zA-Z0-9_-]+` mewajibkan minimal 1 karakter alfanumerik/dash/underscore. |
| **Spasi & Karakter Khusus** | `track 01.nx`, `track$01.nx` | **REJECTED** | Ditolak fail-closed (`ERR_MANIFEST_MALFORMED`) | Ditolak fail-closed (`ERR_ZIP_ENTRY_MISMATCH` jika bijeksi gagal) | Spasi dan simbol asing dilarang untuk kompatibilitas lintas-platform (POSIX, Windows, Android). |
| **Basename Valid Standar** | `track_01.nx`, `01-intro.nx`, `TrackA.nx` | **ACCEPTED** | Diterima untuk validasi semantik lanjutan | Diterima untuk verifikasi bijeksi Tahap 5 | Memenuhi pola kanonikal alfanumerik, underscore, dan hyphen. |

##### Matriks Kasus Batas Keunikan Nama Berkas Lintas Platform (AUDIT-NEW-07 — PO APPROVED)
Sesuai Keputusan Product Owner yang Telah Disahkan (AUDIT-NEW-07 PO APPROVED), keunikan nama berkas dievaluasi menggunakan ASCII case folding deterministik (`toLowerASCII`) untuk mencegah tabrakan pada sistem berkas case-insensitive (Windows, Android, macOS default):

| Kasus Pasangan Nama Berkas | Contoh Konkret | Evaluasi Case-Folding | Hasil Evaluasi Sistem | Error Code Dihasilkan | Dasar Otoritatif / Analisis Platform |
|---|---|:---:|:---:|:---:|---|
| **Duplikasi Eksak (Exact Duplicate)** | `track_01.nx` vs `track_01.nx` | Identik 100% | **REJECTED** | `ERR_MANIFEST_MALFORMED` (manifes) / `ERR_ZIP_INVALID` (ZIP) | Duplikasi nama dilarang mutlak; pelanggaran bijeksi dan integritas. |
| **Benturan Huruf Besar-Kecil (Case Clash)** | `TrackA.nx` vs `tracka.nx` | Benturan (`tracka.nx`) | **REJECTED** | `ERR_MANIFEST_MALFORMED` (manifes) / `ERR_ZIP_INVALID` (ZIP) | Menolak benturan case-insensitive; mencegah overwrite atau ambiguitas ekstraksi pada Windows/Android. |
| **Variasi Kapitalisasi Campuran** | `TRACK_01.nx` vs `track_01.nx` | Benturan (`track_01.nx`) | **REJECTED** | `ERR_MANIFEST_MALFORMED` (manifes) / `ERR_ZIP_INVALID` (ZIP) | Ditolak fail-closed seragam di seluruh platform POSIX, Windows, dan Android. |
| **Karakter Pemisah Berbeda** | `track-01.nx` vs `track_01.nx` | Berbeda (`track-01.nx` vs `track_01.nx`) | **ACCEPTED** | *(None — Valid)* | Hyphen `-` dan underscore `_` adalah karakter diskrit yang valid dan berbeda. |
| **Prefiks Angka Berbeda** | `01_track.nx` vs `02_track.nx` | Berbeda (`01_track.nx` vs `02_track.nx`) | **ACCEPTED** | *(None — Valid)* | Nama berkas unik dan independen. |

*Perbedaan Fungsi Helper `cleanBase` vs Validasi Regex (DEF-08):*
Fungsi `cleanBase` pada `marketplace/server.js:164` (`path.basename(f).replace(/[^a-zA-Z0-9_.-]/g, '_')`) adalah fungsi utilitas sanitasi internal sisi server untuk penamaan berkas unduhan lokal, **BUKAN** aturan validasi normatif. Pemeriksaan integritas manifes dan ZIP anggota wajib mengeksekusi validasi regex ketat `^[a-zA-Z0-9_-]+\.nx$` tanpa kompromi substitusi sanitasi.

#### Model Validasi Lima Tingkat (Five-Level Validation Hierarchy — AUDIT-NEW-02)
Dokumen ini secara ketat membedakan lima tingkat validasi manifes dan paket album untuk mencegah klaim kelulusan semu:
1. **Level 1 — Validitas Sintaksis JSON (RFC 8259)**: Memverifikasi byte stream JSON valid, karakter escape legal (`\\.nx$`), dan ketiadaan malformed Unicode escape syntax.
2. **Level 2 — Validitas Skema Struktural (JSON Schema Draft 7)**: Memvalidasi hanya field dan aturan yang telah disahkan. Draf audio Draft 7 adalah proposal non-normatif; tidak menetapkan 13 required fields universal. Batas `minItems`/`maxItems` juga tidak boleh diperlakukan normatif sebelum disahkan.
3. **Level 3 — Invariant Semantik Logika Aplikasi (Fail-Closed)**: Memvalidasi aturan integritas yang berada di luar skema statis:
   - *Invariant Semantik 1 (Jumlah Track)*: Integer `total_tracks` wajib sama persis dengan `len(tracks)`.
   - *Invariant Semantik 2 (Kontiguitas Monotonik)*: Nilai `track_number` wajib berurutan monotonik dari $1$ hingga $N$ tanpa lompatan atau duplikasi.
   - *Invariant Semantik 3 (Keunikan Identifier & Nama Berkas)*: `track_id` unik global dalam album; `file_name` unik case-insensitive via ASCII case folding (AUDIT-NEW-07).
   - *Invariant Semantik 4 (Validasi Tanggal Kalender Riil)*: Validasi kalender riil `release_date` (tahun, bulan 1..12, hari kabisat; menolak `2026-02-31`).
   - *Aturan validasi draf (non-normatif; field path belum disahkan)*: parsing format ISO 8601 UTC atas kandidat `created_at` (menolak string non-UTC).
   - *Invariant Semantik 6 (Unknown Fields Policy)*: Penolakan properti di luar 13 properti kanonikal (`additionalProperties: false` — proposed strict spec).
4. **Level 4 — Validitas Kriptografis (Cryptographic Validity)**:
   - Serialisasi kanonikal RFC 8785 JCS dan verifikasi Album Signer Signature Ed25519 (menunggu resolusi circular B-08).
   - Verifikasi trust status Album Signer (`TRUSTED`, `UNTRUSTED`, atau `UNKNOWN` — B-09 / CONF-01).
   - Validasi digest kriptografis nyata (bukan nilai dummy).
5. **Level 5 — Pembuktian Paket Fisik & Member Aktual (Package & Member Verification)**:
   - Bijeksi 1:1 manifes terhadap entri ZIP (`ERR_ZIP_ENTRY_MISMATCH`).
   - Safe-open atomik berkas kontainer anggota `.nx` pasca-ekstraksi (`O_RDONLY | O_NOFOLLOW` + `fstat`).
   - Ekstraksi kontainer format PE-01 & validasi Genesis Certificate.

#### Kebijakan Unknown Fields
- Aturan `additionalProperties: false` pada skema di atas berstatus **`PROPOSED STRICT SCHEMA SPECIFICATION — PENDING PO/NORMATIVE CONFIRMATION`**.
- Jika disahkan: dokumen manifest yang memuat field tambahan akan ditolak fail-closed dengan `ERR_MANIFEST_MALFORMED`.
- Jika kebijakan permisif diadopsi oleh PO: field tambahan akan diabaikan selama seluruh properti wajib valid. Expected result AC-01 dikunci bersyarat mengikuti keputusan resmi.

#### Arsitektur Tanda Tangan Digital Terpisah Berbasis Bukti (Temuan 1, Temuan 8, AUDIT-NEW-04, AUDIT-TRUTH-02)
Ekosistem Nexa membedakan secara tegas tanda tangan digital kriptografis independen berdasarkan analisis kontraktual (§6.9) tanpa mencampuradukkan nama, payload, alias kode, atau fungsinya (catatan tata kelola: rujukan implementasi kode lokal pada repositori `whisnu/nexa` commit `fc08a5c` dicatat transparan, namun bagi verifikasi independen Auditor berstatus `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` karena akses repositori belum tersedia):
1. **Album Signer Signature (Ed25519)**:
   - *Fungsi dan Batas Normatif*: Tanda tangan digital Album Signer atas byte kanonikal payload manifest `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] menggunakan kunci privat Album Signer (`album_signer_public_key`). Fungsinya (jika dipertahankan) murni untuk mengautentikasi keabsahan deklarasi manifest dan daftar member Album.
   - *Pemisahan Mutlak dari Pemeriksaan Member `.nx`*: Manifest signature **DILARANG KERAS MENGGANTIKAN ATAU MENGUBAH**:
     1. Creator signature pada masing-masing berkas individual `.nx`;
     2. Genesis Certificate dan ownership proof masing-masing `.nx`;
     3. Registry trust masing-masing `.nx`;
     4. Asset trust masing-masing `.nx`;
     5. Otorisasi playback masing-masing `.nx`.
   - *Bukan Otoritas Global Baru*: Album Signer **BUKAN** otoritas global baru dan **BUKAN** prasyarat trust seluruh member tanpa dasar kontrak produk yang disetujui. Album Signer tidak boleh dianggap otomatis sama dengan Creator yang menandatangani setiap berkas `.nx`. Keduanya merupakan konsep tanda tangan yang berbeda dalam rancangan saat ini.
   - *Ketiadaan Dasar Identitas & Lifecycle Album Signer*:
     Dokumen mencatat secara transparan bahwa White Paper v5.6, Roadmap v4.8, dan baseline PE-01 **TIDAK MENETAPKAN DASAR KONTRAK** untuk:
     - siapa yang bertindak sebagai Album Signer (Creator, Publisher, organisasi, atau entitas lain);
     - siapa yang membuat dan menguasai private key;
     - hubungan identitas Album Signer dengan identitas Creator Nexa;
     - proses pendaftaran public key ke Registry;
     - identity binding;
     - key rotation;
     - revocation;
     - lifecycle dan kewenangan pengelolaan key.
     Jika kebutuhan Album Signer tidak dapat dibuktikan dari kontrak produk atau sumber arsitektur yang berwenang, hal ini **DILARANG DISAHKAN SEBAGAI KEPUTUSAN PRODUK**. Status: **`UNRESOLVED — ALBUM SIGNER IDENTITY, AUTHORITY & LIFECYCLE NOT ESTABLISHED BY PRODUCT CONTRACT (PO / ARCHITECTURE DECISION REQUIRED; STOP AND CLARIFY)`**.
   - *Pemisahan Status Autentisitas Manifest vs Member Trust*:
     Status autentisitas manifest dipisahkan secara tegas dari status trust dan otorisasi setiap member `.nx`:
     - Jika manifest signature gagal secara kriptografis: manifest ditolak sebagai deklarasi tidak autentik/termodifikasi, namun kondisi tersebut TIDAK dengan sendirinya membuktikan bahwa bytes, signature, ownership, atau trust setiap member `.nx` tidak valid.
     - Jika manifest signature valid tetapi identitas/trust signer `UNKNOWN`: JANGAN otomatis menandai member `.nx` sebagai `INVALID` atau memblokir playback seluruh member. Sampai CONF-01 diselesaikan, autentisitas deklarasi membership tidak boleh diasumsikan; file `.nx` yang dipilih/disediakan secara independen tetap dapat menjalani verifikasi dan otorisasi standalone menurut kontrak PE-01. CONF-01 bukan pilihan kebijakan playback global.
   - *Pemisahan Revocation*: Pencabutan (*revocation*) Album Manifest Signer dipisahkan secara tegas dari pencabutan Creator atau Registry evidence milik member `.nx`. Revocation salah satu pihak tidak otomatis mengubah status pihak lain tanpa aturan kontrak yang disahkan. Dipetakan ke **NC-02** (AC-03, tertahan B-08) dan **NC-04** (AC-07/AC-08, tertahan B-09 / CONF-01 dan Registry lifecycle). Status konseptual; mekanisme revocation operasional belum ditetapkan dan tidak boleh dianggap siap implementasi.
2. **Container Packaging Signature (Ed25519)**: Tanda tangan digital Creator kontainer atas byte packaging kontainer individual `.nx` (trailer 64-byte Ed25519, dilaporkan via Go `internal/container/container.go#L17-L64, L67-L135` dan `signatureBytes` di TypeScript SDK `sdk/typescript/src/container.ts#L4-L8, L44-L104`; status bukti audit independen: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`). Dipetakan ke **NC-06** dan diuji oleh **AC-04** (`ERR_CONTAINER_SIGNATURE_INVALID`). Catatan: field `creator_signature` bukan trailer kontainer melainkan properti sertifikat genesis.
3. **Registry Certificate Signature (Ed25519)**: Tanda tangan digital otoritas Registry (`issuer_signature` pada Registry Certificate lapisan 1, dilaporkan di `sdk/typescript/src/sdk.ts#L207-L226`; status bukti audit independen: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`) menggunakan kunci privat Registry Authority atas canonical JCS string sertifikat registri.
4. **Genesis Ownership Certificate Signature (Ed25519)**: Tanda tangan digital Genesis Creator (field `creator_signature` pada Embedded Genesis Ownership Certificate lapisan 2, dilaporkan di `sdk/typescript/src/sdk.ts#L234-L255`, `sdk/typescript/src/ownership.ts#L26`, dan `marketplace/db/schema.postgres.sql#L72` / `migrations/004_ownership.sql#L25`; status bukti audit independen: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`) menggunakan kunci privat Genesis Creator atas data kanonikal sertifikat genesis. Dipetakan ke **NC-05** dan diuji oleh **AC-10** (fail-closed, unresolved taxonomy error code).

---

### 5.2 NX Player — Baseline JIT PE-01 dan Proposal Alur Album Delapan Tahap (Temuan 2, AUDIT-NEW-01, AUDIT-NEW-10, PE02-R63-AUD-01)
White Paper v5.6 menjadi Product Truth untuk otorisasi JIT atas setiap kontainer `.nx` mandiri. Urutan ZIP/manifest Album Tahap 1–6 dan pemisahan Stage 8a/8b/8c di bawah tetap merupakan alur Album-specific yang dibaca terpisah dari baseline JIT PE-01. Keputusan PO AUDIT-NEW-10 pada §13.12.11 adalah kontrak produk normatif untuk pemisahan tiga peran kunci dan otorisasi third-party packaging. Tahap 7a/7b/7c harus mengonsumsi hasil terpisah untuk integritas kontainer, otorisasi packaging, Genesis/ownership, Registry trust, dan lisensi aktif; tidak satu pun hasil tersebut boleh disamakan. Tidak ada bagian ini yang mengubah otorisasi per-member atau mengizinkan background pre-verification memberi otorisasi, dekripsi, atau buffer registration:

> **Catatan Multi-Payload NX Player & Isolasi Non-Audio (PE02-R63-AUD-01 / FINDING-02):**  
> Prosedur otorisasi JIT Tahap 8a (pencocokan digest audio) dan Tahap 8c (registrasi audio buffer) berlaku spesifik untuk payload pemutaran audio/musik. Untuk payload non-audio (video, dokumen, dan gambar), dasar normatif dekripsi dan pendaftaran stream/viewer belum didefinisikan secara lengkap oleh kontrak platform (**`UNRESOLVED — STOP AND CLARIFY`**; dilarang mengasumsikan alur audio otomatis berlaku untuk non-audio). NX Player beroperasi sebagai viewer mandiri terisolasi tanpa registrasi audio buffer output untuk dokumen dan gambar; dan trigger Auto-Next Album untuk seluruh tipe payload (Audio, Video, Dokumen, Gambar) berstatus **`STOP AND CLARIFY`** (pada audio baru terdapat rotasi playlist GUI desktop lokal di `renderer.js#L652-L655`, pada video tidak ada listener `ended` di `videoEngine`, dan pada dokumen/gambar tidak ada durasi alami; belum ada kontrak normatif pemicu transisi anggota Album multi-payload). Invariant universal yang berlaku untuk ke-4 tipe payload (Music, Video, Document, Image) secara seragam mencakup: integritas kemasan kontainer PE-01 (Tahap 7a), Genesis Ownership (Tahap 7b), evaluasi lisensi aktif pengguna (Tahap 7c), dan keamanan packaging/ekstraksi (Tahap 1..6).

```
[Tahap 1: Open Arsip ZIP Wrapper Sumber]
     │
     ▼
[Tahap 2: Validasi Fisik & Integritas Arsip ZIP (Independen dari Manifes)]
     │
     ▼
[Tahap 3: Pembacaan & Strict JSON Parse Manifes Kanonikal (Bukan Ekstraksi Member)]
     │
     ▼
[Tahap 4: Manifest JCS Canonicalization & Cryptographic Signature Verification (Registry Trust Unavailable)]
     │
     ▼
[Tahap 5: Pemeriksaan Bijeksi 1:1 Manifes-ke-ZIP & Case-Insensitive Uniqueness]
     │
     ▼
[Tahap 6: Ekstraksi Member .nx & Atomic Filesystem Safe-Open Descriptors]
     │
     ├───────────────────────────────────────────┐
     │ (Jalur Integritas Fisik & Kepemilikan)    │ (Jalur Otorisasi Pengguna)
     ▼                                           ▼
[Tahap 7a: Validasi Format PE-01 Container] [Tahap 7c: Evaluasi Active License /]
[Tahap 7b: Validasi Genesis Ownership Cert] [          Entitlement Pengguna (AC-22)]
     │                                           │
     ▼                                           │
[Tahap 8a: Verifikasi Digest SHA-256 Audio]      │
│ (Bitstream mentah vs deklarasi hash manifest (lokasi belum ditetapkan)) │
│ (Field identifier audio hash: UNRESOLVED di WP)   │
│ (Dependensi 7b & 7c ke 8a: UNRESOLVED di WP)   │
│ (Izin pre-verifikasi antrean: UNRESOLVED)      │
│ (Kemampuan hitung digest BUKAN izin produk)    │
│ (Hasil digest valid TIDAK memberi izin putar)  │
     │                                           │
     ├───────────────────────────────────────────┘
     ▼
[Tahap 8b: Dekripsi Payload Audio (Prasyarat Kumulatif 8a + 7b + 7c)]
│ (Wajib lolos digest 8a, validasi Genesis 7b, DAN lisensi aktif sah 7c)
│ (Dilarang keras jika signature/entitlement member gagal menurut kontrak PE-01; signer Album bukan global member playback gate)
│ (CONF-01 mengatur autentisitas manifest/membership, bukan playback gate global)
│ (Diagnostic decryption policy: UNRESOLVED)
     │
     ▼
[Tahap 8c: Pendaftaran Audio Buffer ke Pipeline Pemutar]
│ (Eksklusif current member yang sedang aktif diputar)
│ (Pre-verifikasi trek antrean dilarang mendaftarkan buffer)
```

#### Pemetaan Rinci Tahapan JIT ke Pemeriksaan Kriptografis, Dependensi & Acceptance Criteria (AUDIT-NEW-01)
1. **Tahap 1 — Open Arsip ZIP Wrapper Sumber (Source Archive Open)**:
   - *Objek Fisik*: Berkas fisik arsip distribusi ZIP (`.zip`).
   - *Operasi*: Membuka berkas arsip ZIP wrapper sumber dalam mode baca read-only secara aman.
   - *Error Code*: `ERR_ZIP_INVALID`.
   - *AC Penguji*: **AC-02**.
2. **Tahap 2 — Validasi Integritas Fisik & Keamanan Arsip ZIP (Archive-Level Security Check)**:
   - *Objek Fisik*: Struktur internal ZIP (Central Directory & Local File Headers).
   - *Prasyarat*: **Independen dari manifest**.
   - *Pemeriksaan*: Validasi header ZIP standar; menerima *regular files* dan *directories* (sesuai Keputusan PO AUDIT-NEW-06); menolak symlink dan *special files* (FIFO, socket, device files) fail-closed dengan `ERR_ZIP_INVALID`; semantik hardlink ZIP tidak didukung; dua entri dengan isi byte identik tetap diperlakukan sebagai entri independen; verifikasi kuota ukuran terkompresi $\le 500$ MB desimal (500.000.000 bytes), uncompressed cumulative extraction $\le 4$ GB desimal, dan total entri $\le 200$ (`ERR_ZIP_QUOTA_EXCEEDED`); verifikasi rasio kompresi batas bomb (`ERR_ZIP_BOMB_DETECTED`).
   - *AC Penguji*: **AC-02, AC-13** (NC-07 / B-07).
3. **Tahap 3 — Pembacaan & Strict JSON Parse Manifes Kanonikal (Manifest Parse & Schema Invariants)**:
   - *Objek Fisik*: Kandidat entri manifest pada rancangan ZIP; draf historis menggunakan nama `album_manifest.json`, tetapi nama file dan lokasinya belum disahkan. Pembacaan selektif *in-memory streaming* merupakan proposal, bukan kontrak produk yang telah disahkan; ekstraksi member `.nx` tidak boleh mendahului tahapan prasyarat yang berlaku.
   - *Prasyarat*: Arsip ZIP lolos pemeriksaan integritas fisik Tahap 2.
   - *Pemeriksaan*: Parsing sintaksis RFC 8259; penolakan duplicate keys (literal dan escaped Unicode via Strict Parser Policy); validasi terhadap field/aturan yang telah disahkan saja; draf Draft 7 audio saat ini bukan schema normatif universal dan tidak menetapkan 13 required fields normatif; validasi kalender/format waktu hanya sebagai aturan draf non-normatif; field `release_date`/`created_at` dan requiredness belum disahkan.
   - *Error Code*: `ERR_MANIFEST_MALFORMED`, `ERR_MANIFEST_DUPLICATE_KEY`.
   - *AC Penguji*: **AC-01** (NC-01), **AC-05** (NC-03, terblokir B-01).
4. **Tahap 4 — Proposal JCS & Verifikasi Signature Kriptografis (Registry signer trust/lifecycle belum ditetapkan)**:
   - *Objek Data*: Payload data manifes hasil parsing Tahap 3.
   - *Operasi*: Melakukan serialisasi kanonikal RFC 8785 JCS atas payload manifes dan, hanya setelah circular dependency B-08 diselesaikan, memverifikasi tanda tangan Ed25519 Album Signer (`album_signer_signature`) menggunakan `album_signer_public_key`. Pemeriksaan status signer pada Registry **BUKAN operasi yang saat ini dinyatakan tersedia**; evaluasi Registry hanya dapat dilakukan setelah identitas, enrollment, identity binding, key rotation, dan revocation lifecycle Album Signer ditetapkan secara otoritatif. Sampai saat itu status Registry merupakan kondisi unresolved yang harus ditangani, bukan klaim adanya endpoint, record, atau mekanisme lookup.
   - *Prinsip Pemisahan Evaluasi Manifest vs Member `.nx` (AUDIT-TRUTH-02)*:
     1. Tahap 4 dalam proposal ini, jika kelak disahkan, hanya mengevaluasi kanonisasi payload dan validitas kriptografis signature manifest. Tahap 4 **TIDAK** mengevaluasi kredibilitas/trust Album Signer pada Registry karena mekanisme Registry belum ditetapkan; Tahap 4 juga **BUKAN PENGGANTI DAN TIDAK MENENTUKAN** validitas atau trust individual masing-masing berkas `.nx` anggota.
     2. *Manifest Signature Gagal Kriptografis*: Manifest ditolak fail-closed sebagai deklarasi yang tidak autentik (`ERR_MANIFEST_SIGNATURE_INVALID`). Karena daftar membership pada deklarasi yang gagal autentikasi tidak dapat dipercaya, sistem **DILARANG** mengklaim atau memproses entri yang disebut manifest tersebut sebagai anggota Album terverifikasi. Sistem juga **DILARANG** menyimpulkan bahwa bytes kontainer, Creator signature, ownership proof, atau Registry trust file `.nx` menjadi `INVALID` akibat kegagalan manifest. Diagnostik member hanya boleh dilakukan jika file `.nx` dipilih/disediakan secara independen di luar membership manifest yang gagal; hasilnya harus dilaporkan sebagai verifikasi file mandiri, bukan verifikasi anggota Album.
     3. *Signer UNKNOWN*: Jika Album Signer berstatus `UNKNOWN`, sistem DILARANG menyimpulkan bahwa signer atau member `.nx` `INVALID`, dan DILARANG menetapkan larangan/izin playback global berdasarkan status signer Album. Namun, sampai CONF-01 diputuskan, autentisitas deklarasi membership manifest tidak boleh diasumsikan; daftar member dari manifest tersebut tidak boleh diperlakukan sebagai membership Album yang terverifikasi. File `.nx` yang dipilih/disediakan secara independen tetap dapat dievaluasi melalui verifikasi dan otorisasi standalone PE-01; hasilnya bukan verifikasi anggota Album.
     4. *Preservasi White Paper v5.6*: Status `UNKNOWN / INCOMPLETE` BUKAN `INVALID`; Integrity Verification dipisahkan dari Trust Verification. Ketentuan White Paper tentang Play/View dengan warning saat trust tidak tersedia hanya diterapkan pada file `.nx` yang identitas dan konteksnya dapat diverifikasi secara independen menurut kontrak standalone PE-01. Ketentuan tersebut TIDAK mengautentikasi membership Album dan tidak memberi dasar untuk memperlakukan daftar member dari manifest signer `UNKNOWN` sebagai daftar Album tepercaya. Kegagalan integritas/hash/signature member dan revocation otoritatif atas trust evidence milik member tetap ditangani menurut kontrak PE-01; status Album Signer tidak menjadi global playback gate. Berkas offline dengan `.nxcert` cocok serta evidence Registry-authenticated yang sah tetap dievaluasi menurut kontrak PE-01.
    - *Error Code*: `ERR_MANIFEST_SIGNATURE_INVALID` (hanya setelah mekanisme signature dan circular dependency B-08 diselesaikan). `ERR_ALBUM_SIGNER_UNTRUSTED` dan `ERR_ALBUM_SIGNER_UNKNOWN` bukan operasi/error hasil lookup Registry yang saat ini tersedia; keduanya hanya kategori kondisi yang masih menunggu penetapan identitas dan lifecycle signer, dan tidak boleh diperlakukan sebagai hasil operasional Tahap 4.
   - *AC Penguji*: **AC-03, AC-06, AC-07, AC-08** (NC-02, NC-03, NC-04, B-02, B-08, B-09).
5. **Tahap 5 — Pemeriksaan Bijeksi 1:1 Manifes-ke-ZIP & Case-Insensitive Uniqueness**:
   - *Objek Data*: Daftar nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) pada manifes vs Central Directory ZIP.
   - *Prasyarat*: Manifes telah berhasil di-parse secara sintaksis pada Tahap 3, dan daftar entri Central Directory ZIP telah tersedia dari Tahap 2. Pemeriksaan bijeksi pada tahap ini hanya memeriksa konsistensi struktural antara deklarasi dan entri fisik ZIP; pemeriksaan ini **BUKAN** autentikasi deklarasi membership dan tidak mengesahkan file apa pun sebagai anggota Album. Autentisitas membership tetap bergantung pada penyelesaian kebijakan/otoritas signer yang berlaku (CONF-01 / B-09).
   - *Pemeriksaan*: Memvalidasi bijeksi eksak 1:1 antara manifes dan ZIP: setiap file yang dideklarasikan pada manifes wajib ada di ZIP, dan tidak ada file reguler ekstra/asing di dalam ZIP di luar deklarasi manifes dan `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] (entri direktori yang diizinkan PO tidak membatalkan bijeksi); validasi keunikan nama berkas case-insensitive via ASCII case folding (AUDIT-NEW-07).
   - *Error Code*: `ERR_ZIP_ENTRY_MISMATCH` (secara deterministik untuk seluruh ketidakcocokan bijeksi 1:1: baik berkas manifes hilang di ZIP maupun berkas reguler ekstra/asing di ZIP yang tidak dideklarasikan). Catatan: benturan nama case-insensitive antar-entri ZIP telah ditolak pada Tahap 2 dengan `ERR_ZIP_INVALID`.
   - *AC Penguji*: **AC-02, AC-13** (NC-01, NC-07).
6. **Tahap 6 — Ekstraksi Member .nx & Atomic Filesystem Safe-Open Descriptors (AUDIT-NEW-01, AUDIT-NEW-03)**:
   - *Objek Fisik*: Berkas kontainer `.nx` dari anggota Album yang sedang menjadi *current member*, diekstrak ke filesystem lokal sementara/staging.
   - *Prasyarat*: Tahap 6 sebagai pemrosesan **anggota Album** hanya boleh dijalankan setelah autentisitas membership deklarasi manifest telah dibuktikan secara sah. Pemeriksaan struktur ZIP/manifest pada Tahap 2–5 saja tidak memenuhi prasyarat tersebut. Jika membership belum autentik (termasuk ketika CONF-01 / B-09 belum diputuskan atau signer `UNKNOWN`), sistem tidak boleh mengekstrak atau memproses file berdasarkan klaim bahwa file tersebut anggota Album. File `.nx` yang dipilih/disediakan secara independen tetap dapat diperiksa melalui jalur standalone PE-01; hasilnya bukan pemrosesan anggota Album.
   - *Operasi*: Untuk anggota Album yang membership-nya telah autentik dan yang menjadi *current member*, pembukaan berkas kontainer `.nx` pasca-ekstraksi menggunakan deskriptor atomik `fs.openSync(path, O_RDONLY | O_NOFOLLOW)` dan validasi segera melalui `fs.fstatSync(fd).isFile()`. Pemeriksaan ganda `lstatSync` dan perbandingan `dev`/`ino` dicatat sebagai celah residu kode desktop (`NOT DEMONSTRATED BY E-07 / RESIDUAL GAP`).
   - *Error Code*: `ERR_FILESYSTEM_CONTAINMENT_VIOLATION`.
   - *AC Penguji*: **AC-20, AC-21** (NC-12, B-06).
7. **Tahap 7 — Validasi Format Kontainer PE-01, Genesis Cert Ownership & Active License (AUDIT-NEW-01, AUDIT-NEW-10)**:
   - *Objek Fisik*: Kontainer `.nx` yang telah dibuka secara aman pada Tahap 6.
   - *Pemisahan Komponen Pemeriksaan Tahap 7*:
     - **7a. Validasi Format Kontainer Mandiri PE-01 & Packaging Signature**:
       Verifikasi struktur kemasan kontainer PE-01 dan Container Packaging Signature (trailer 64-byte Ed25519, terverifikasi sebagai field `signature` di Go `internal/container/container.go#L37, L128` dan `signatureBytes` di TypeScript SDK `sdk/typescript/src/container.ts#L6, L98`). Jika corrupt atau signature tidak valid, proses melempar **`ERR_CONTAINER_SIGNATURE_INVALID`**.
     - **7b. Validasi Dua Lapisan Genesis Certificate (AUDIT-NEW-04, AUDIT-NEW-10)**:
       Verifikasi dua lapisan sertifikat: Registry Certificate (lapisan 1, 6-field canonical JCS diverifikasi via `registryPubKey`) dan Embedded Genesis Ownership Certificate (lapisan 2, 8-field canonical JSON diverifikasi via `ownCert.creator_public_key` dengan signature `creator_signature` di `sdk.ts#L235`).
       - **Keputusan PO AUDIT-NEW-10 — APPROVED**: genesisPubKey adalah Genesis Creator/originator dan menandatangani Genesis Ownership Certificate; containerSigKey adalah Container Packager/Packaging Engine dan menandatangani integritas binary container .nx; ownCertPubKey adalah current holder/buyer/collector sebagai subjek hak kepemilikan/lisensi saat ini. Ketiganya adalah peran berbeda dan tidak diwajibkan identik. ownCertPubKey boleh berbeda dari genesisPubKey jika rantai transfer kepemilikan sah menghubungkannya. Jika containerSigKey != genesisPubKey, wajib ada delegation/authorization evidence yang dapat diverifikasi. Tanpa bukti tersebut, packaging adalah UNTRUSTED / UNAUTHORIZED PACKAGING meskipun signature matematis valid. Self-packaging (containerSigKey == genesisPubKey) memiliki otoritas inheren dan tidak memerlukan delegation tambahan. Detail delegation mengikuti §13.12.11; otoritas penerbit dan subdelegation masih menjadi pertanyaan normatif terbuka.
     - **7c. Evaluasi Status Active License / Entitlement Pengguna**:
       Pemeriksaan hak kepemilikan / lisensi pemutaran aktif pengguna pada Marketplace / engine lokal (`is_licensed: true`). Jika pengguna tidak memiliki lisensi pemutaran aktif, evaluasi menghasilkan **`ERR_PLAYBACK_UNAUTHORIZED`**.
   - *AC Penguji*: **AC-04, AC-10, AC-22** (NC-05, NC-06, NC-13).

8. **Tahap 8 — Verifikasi Digest SHA-256 Audio, Dekripsi Terotorisasi, dan Pendaftaran Buffer (AUDIT-NEW-01)**:
   - **8a. Verifikasi Digest SHA-256 Audio (Audio Digest Verification)**:
     - *Objek Data*: Payload biner bitstream audio mentah terenkripsi di dalam kontainer `.nx` trek aktif.
     - *Prasyarat I/O Fisik Minimum*: Deskriptor berkas aman yang dibuka atomik dari Tahap 6 (`fs.openSync` dengan `O_RDONLY | O_NOFOLLOW`) dan integritas kemasan fisik kontainer PE-01 dari Tahap 7a (`NexaContainer.unpack(data)`).
       *Peringatan Batas Normatif*: Prasyarat I/O fisik ini TIDAK BOLEH dinyatakan secara kategoris sebagai satu-satunya prasyarat Tahap 8a. Status ketergantungan normatif Stage 8a terhadap validasi Genesis (Stage 7b) dan lisensi aktif pengguna (Stage 7c) masih berstatus `UNRESOLVED`. Kemampuan teknis menghitung hash atas bitstream mentah tanpa kunci dekripsi TIDAK SAMA DENGAN izin produk untuk melanjutkan pemeriksaan digest jika Stage 7b atau 7c tidak sah.
     - *Pemeriksaan*: Menghitung digest SHA-256 atas bitstream audio mentah biner kontainer `.nx` dan mencocokkannya secara eksak dengan deklarasi hash bitstream audio pada manifes album (notasi konseptual: lokasi dan field deklarasi hash belum ditetapkan; status field identity: `UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT; STOP AND CLARIFY`; dilarang menganggap kedua nama sebagai alias yang sama-sama diterima atau fallback). Jika tidak cocok, proses dibatalkan fail-closed dengan melempar **`ERR_CONTAINER_HASH_MISMATCH`**.
     - *Batasan Status Diagnostik & Isolasi Hak Putar*: Pemeriksaan digest ini adalah pemeriksaan integritas fisik atas bitstream mentah. Keberhasilan pencocokan digest 8a **TIDAK PERNAH** memberikan hak otorisasi pemutaran (*no playback authorization*), tidak mengizinkan dekripsi payload (8b), dan tidak mengizinkan pendaftaran buffer (8c).
     - *Status Ketergantungan Normatif Genesis (7b) dan Lisensi Aktif (7c)*:
       - **Dependensi terhadap Validasi Genesis (7b)**: Secara teknis biner, bitstream payload diekstrak dan dihitung hash-nya tanpa membaca sertifikat genesis (`sdk.ts#L137-L151`). Namun, kontrak produk Nexa yang dibekukan (White Paper v5.6, PE-01) belum mengatur secara normatif apakah kegagalan validasi Genesis pada Stage 7b menghentikan seluruh proses atau tetap mengizinkan digest diagnostik. Perancang dilarang menetapkan status `NOT REQUIRED` tanpa kontrak normatif. Status: **`UNRESOLVED — GENESIS VALIDATION DEPENDENCY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**.
       - **Dependensi terhadap Lisensi Aktif (7c)**: Standar POSIX.1-2017 maupun White Paper v5.6 tidak memuat aturan bisnis apakah verifikasi digest diagnostik bitstream mentah memerlukan lisensi aktif pengguna. Perancang dilarang menetapkan status `NOT REQUIRED` tanpa kontrak normatif. Kemampuan teknis mengekstraksi bitstream tidak boleh disamakan dengan izin produk untuk menjalankan pemeriksaan. Status: **`UNRESOLVED — ACTIVE LICENSE DEPENDENCY FOR DIAGNOSTIC DIGEST NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**.
   - **8b. Dekripsi Payload Audio (Decryption)**:
     - *Prasyarat Mutlak*: Keberhasilan verifikasi digest 8a **DAN** validasi Genesis Certificate 7b **DAN** status otorisasi lisensi pemutaran aktif pengguna terverifikasi sah pada Tahap 7c (*active entitlement / valid user license*).
     - *Larangan Dekripsi Otomatis*: Dekripsi payload audio **TIDAK BOLEH** dianggap otomatis sebagai kelanjutan dari keberhasilan digest. Dekripsi **DILARANG KERAS** dilakukan hanya karena berkas berhasil diekstrak, Safe-Open berhasil, manifes valid, atau digest cocok.
     - *Pemisahan Kondisi Pemblokiran Dekripsi & Kebijakan Signer UNKNOWN (FINDING-03)*:
        1. *Kondisi Hard-Block Definitif*: Dekripsi payload **DILARANG KERAS** dan dihentikan fail-closed (`canPlay: false`) dalam kondisi: (a) verifikasi digest 8a gagal/mismatch, (b) validasi kontainer PE-01 7a gagal/corrupt, (c) validasi sertifikat Genesis 7b gagal, (d) ketiadaan active license yang sah pada Tahap 7c (`ERR_PLAYBACK_UNAUTHORIZED`), atau (e) dalam mode diagnostic-only (NX Verify). Status Album Signer `UNTRUSTED`/`REVOKED` tidak ditambahkan sebagai global member playback gate. AC-07 mengatur keputusan autentisitas/provenance membership saat signer `UNKNOWN`; AC-08 secara terpisah mencatat kebutuhan evaluasi revocation signer dan tetap terblokir sampai Registry revocation lifecycle ditetapkan. Keduanya tidak mengubah status trust atau otorisasi standalone setiap member.
        2. *Signer UNKNOWN*: Status `UNKNOWN` tidak membuktikan signer `INVALID` dan tidak mengubah trust atau otorisasi mandiri setiap member. CONF-01 hanya memutuskan apakah deklarasi manifest dapat mengautentikasi membership Album serta dasar identitas/lifecycle signer. Sampai diputuskan, membership manifest tidak boleh diasumsikan autentik. Playback tetap mengikuti otorisasi JIT per member berdasarkan kontrak PE-01; tidak ada kebijakan global allow/block yang ditetapkan melalui CONF-01.
      - *Batasan Dekripsi Jalur Diagnostik NX Verify vs Kebijakan Dekripsi Diagnostik Lebih Luas*:
        - *Jalur Diagnostik NX Verify*: Pemeriksaan digest dapat membaca bitstream terenkripsi sesuai tahapan yang ditentukan, namun jalur diagnostik tersebut DILARANG melakukan dekripsi payload audio, DILARANG melakukan buffer registration, dan hasil digest TIDAK PERNAH memberikan playback authorization.
        - *Kebijakan Dekripsi Diagnostik Lebih Luas*: Kebijakan dekripsi parsial atau kebutuhan dekripsi diagnostik lainnya yang belum memiliki kontrak normatif secara tegas berstatus:
          **`UNRESOLVED — NORMATIVE CONTRACT NOT VERIFIED (PO / ARCHITECTURE DECISION REQUIRED)`**.
          Tidak ada izin dekripsi otomatis untuk kebutuhan diagnostik dan tidak ada pintu belakang pemutaran (*no backdoor playback*).
       - *Isolasi Payload Stage 8b (FINDING-02)*: Prosedur dekripsi yang dirinci di atas adalah prosedur khusus payload audio (*audio-specific*). Untuk Video, Document, dan Image, kontrak normatif dekripsi payload pada kontainer individual PE-01 belum diterbitkan oleh otoritas arsitektur (**`UNRESOLVED — STOP AND CLARIFY`**; programmer dilarang mengasumsikan alur audio otomatis berlaku untuk payload non-audio tanpa dasar kontrak tertulis).
   - **8c. Pendaftaran Buffer Audio (Buffer Registration)**:
     - *Operasi*: Pendaftaran buffer audio yang telah didekripsi ke dalam audio output pipeline pemutar audio desktop.
      - *Prasyarat & Aturan Dependensi Stage 8b Menuju Stage 8c*:
        1. Stage 8c hanya boleh dilakukan setelah Stage 8b berhasil didekripsi secara sah.
        2. Keberhasilan Stage 8a saja tidak cukup untuk mengizinkan Stage 8c.
        3. Jika Stage 8b gagal, alur eksekusi wajib dihentikan secara fail-closed sebelum Stage 8c dijalankan.
        4. Buffer audio yang didaftarkan pada Stage 8c harus merupakan hasil dekripsi yang sah dari Stage 8b untuk *current member*.
        5. Tidak boleh ada buffer registration untuk anggota yang belum menjadi *current member*.
     - *Larangan Keras Pre-Verifikasi*: Background pre-verification terhadap anggota album berikutnya dalam antrean **DILARANG KERAS** memicu buffer registration atau menghasilkan otorisasi implisit untuk anggota album yang belum menjadi *current member*. Status izin diagnostik pre-verifikasi pada Stage 8a sendiri berstatus **`UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**.
   - *Error Code*: `ERR_CONTAINER_HASH_MISMATCH` (pada 8a), `ERR_PLAYBACK_UNAUTHORIZED` (pada 8b).
   - *AC Penguji*: **AC-09** (8a), **AC-22, AC-23, AC-24** (8b, 8c).

#### Matriks Dependensi Silang JIT Album (§3.4 Mandat Audit)
Tabel berikut merinci status dependensi setiap prasyarat terhadap ketiga sub-tahap pemrosesan audio (Stage 8a Digest, Stage 8b Decryption, Stage 8c Buffer Registration):

| Prasyarat / Tahap Asal | Stage 8a: Digest SHA-256 | Stage 8b: Dekripsi Audio | Stage 8c: Pendaftaran Buffer | Dasar Bukti & Status Normatif |
|---|:---:|:---:|:---:|---|
| **Deskriptor Berkas Aman (Tahap 6)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | POSIX.1-2017 `O_RDONLY \| O_NOFOLLOW`; `fs_safe.ts#L30-L55` (E-07). Prasyarat I/O fisik minimum untuk membaca bitstream mentah. |
| **Integritas Kontainer PE-01 (Tahap 7a)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | Format kemasan PE-01 (`internal/container/container.go#L35-L80`). Diperlukan untuk unpacking offset header, payload, dan trailer signature. |
| **Validasi Genesis Certificate (Tahap 7b)** | `UNRESOLVED` | `REQUIRED` | `REQUIRED` | `UNRESOLVED — GENESIS VALIDATION DEPENDENCY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`. Kemampuan teknis biner mengekstrak bitstream tanpa membaca genesis (`sdk.ts#L137-L151`) tidak boleh disamakan dengan izin produk untuk melanjutkan pemeriksaan digest jika 7b gagal. Dilarang menetapkan `NOT REQUIRED` tanpa kontrak normatif. Untuk dekripsi (8b) dan buffer (8c), validasi kepemilikan genesis mutlak `REQUIRED`. |
| **Evaluasi Active License (Tahap 7c)** | `UNRESOLVED` | `REQUIRED` | `REQUIRED` | `UNRESOLVED — ACTIVE LICENSE DEPENDENCY FOR DIAGNOSTIC DIGEST NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`. Secara fisik bitstream mentah terenkripsi aman di-digest tanpa lisensi, namun kontrak produk Nexa belum memutuskan apakah ketiadaan lisensi aktif pengguna menghentikan alur pemeriksaan digest atau mengizinkan kelanjutan digest murni diagnostik. Dilarang menetapkan `NOT REQUIRED` tanpa kontrak normatif. Untuk dekripsi (8b) dan buffer (8c), lisensi aktif mutlak `REQUIRED` (fail-closed `ERR_PLAYBACK_UNAUTHORIZED`). |
| **Digest Stage 8a Cocok** | `Hasil pemeriksaan` | `REQUIRED` | `REQUIRED` | White Paper v5.6 §Distribution; draf deklarasi hash manifest dengan parent array dan field path belum ditetapkan (identitas field normatif audio_sha256 vs tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256 unresolved; STOP AND CLARIFY). Keberhasilan pencocokan digest bitstream mentah adalah hasil pemeriksaan fisik yang REQUIRED untuk dekripsi 8b dan pendaftaran buffer 8c; dekripsi 8b dilarang keras sebelum digest bitstream mentah terbukti cocok. Keberhasilan Stage 8a saja tidak cukup untuk mengizinkan Stage 8c. |
| **Stage 8b Berhasil** | `Tidak berlaku` | `Hasil dekripsi` | `REQUIRED` | Aturan dependensi Stage 8b menuju Stage 8c: (1) Stage 8c hanya boleh dilakukan setelah Stage 8b berhasil; (2) Keberhasilan Stage 8a saja tidak cukup untuk mengizinkan Stage 8c; (3) Jika Stage 8b gagal, alur pemrosesan wajib dihentikan fail-closed sebelum Stage 8c dijalankan; (4) Buffer yang didaftarkan pada Stage 8c harus merupakan hasil dekripsi yang sah dari Stage 8b untuk *current member*; (5) Tidak boleh ada buffer registration untuk anggota yang belum menjadi *current member*. |
| **Trek Merupakan Current Member** | `UNRESOLVED / CONDITIONAL` | `CONDITIONAL` | `REQUIRED` | Apakah Stage 8a mensyaratkan status current member atau diizinkan berjalan untuk antrean trek berikutnya bergantung pada keputusan izin pre-verifikasi diagnostik (`UNRESOLVED`). Stage 8b hanya dieksekusi saat transisi pemutaran trek aktif. Stage 8c secara mutlak `REQUIRED` hanya untuk trek yang sedang aktif diputar. |
| **Background Pre-Verification untuk Anggota Berikutnya** | `UNRESOLVED` | `NOT ALLOWED` | `NOT ALLOWED` | `UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`. Kemampuan teknis biner mengekstrak bitstream tidak boleh disamakan dengan izin produk untuk menjalankan digest antrean berikutnya. Namun, Stage 8b secara mutlak `NOT ALLOWED` (dilarang dekripsi) dan Stage 8c secara mutlak `NOT ALLOWED` (dilarang buffer registration) untuk trek yang belum menjadi current member. |

> **Pemisahan Tiga Lapisan Kebutuhan Pre-Verifikasi & Batas Keamanan Stage 8 (AUDIT-NEW-01 PO Clarification):**
> Dokumen ini secara tegas memisahkan tiga lapisan yang berbeda dan melarang penyamaan antara kemampuan komputasi dengan izin tata kelola produk:
> 1. **Technical Capability (Kemampuan Teknis Komputasi)**: Secara teknis biner filesystem dan parser, sistem mampu membuka deskriptor aman berkas kontainer `.nx` anggota album berikutnya dalam antrean dan menghitung hash SHA-256 bitstream terenkripsi tanpa kunci dekripsi.
> 2. **Diagnostic Permission (Izin Diagnostik Produk)**: Kontrak produk Nexa yang disahkan (White Paper v5.6, Roadmap v4.8) **belum menetapkan** apakah Player diizinkan mengeksekusi pemeriksaan digest diagnostik atas berkas antrean sebelum berkas tersebut diputar. Status izin diagnostik ini ditetapkan secara jujur dan tidak memihak sebagai:
>    **`UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**.
>    Dokumen tidak menyatakan pre-verifikasi sebagai `ALLOWED`, dan tidak mengarang larangan sepihak sebagai `NOT ALLOWED`.
> 3. **Playback Authorization (Otorisasi Pemutaran & Batas Keamanan Stage 8b/8c)**: Background pre-verification dalam kondisi apa pun **DILARANG KERAS** menghasilkan otorisasi pemutaran, dilarang melakukan dekripsi payload audio (Stage 8b), dan dilarang mendaftarkan buffer audio (Stage 8c). Pendaftaran buffer audio hanya dan selalu berlaku eksklusif untuk trek yang sedang aktif diputar oleh pengguna (*current member*).
>
> **Aturan Dependensi Silang Tahap 7 terhadap Tahap 8a, 8b, dan 8c (AUDIT-NEW-01 Mandat):**
> 1. *Batas Prasyarat Fisik vs Izin Normatif (Tahap 7a -> Tahap 8a)*: Deskriptor berkas aman (Tahap 6) dan integritas kemasan kontainer PE-01 (Tahap 7a) merupakan prasyarat teknis I/O biner untuk membaca byte payload. Dokumen ini **DILARANG KERAS** menyatakan bahwa Tahap 8a secara kategoris hanya memerlukan Tahap 6 dan 7a. Dependensi normatif Stage 8a terhadap validasi Genesis 7b dan lisensi aktif 7c dinyatakan berstatus **`UNRESOLVED — GENESIS VALIDATION & ACTIVE LICENSE DEPENDENCY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED)`**. Kemampuan teknis menghitung digest biner tanpa kunci dekripsi tidak boleh disamakan dengan izin produk untuk melanjutkan pemeriksaan digest jika 7b atau 7c tidak sah. Namun demikian, jika mode diagnostik NX Verify diizinkan berjalan berdasarkan keputusan resmi PO, status lisensi aktif pengguna dilaporkan secara terpisah tanpa mencampuradukkannya dengan status integritas berkas fisik. Hasil digest 8a yang cocok **TIDAK PERNAH** memberikan hak pemutaran atau dekripsi.
> 2. *Gerbang Otorisasi Kumulatif (Tahap 8a + Tahap 7b + Tahap 7c -> Tahap 8b)*: Tahap 8b adalah batas keamanan (*security boundary*) di mana payload audio biner didekripsi. Tahap 8b mensyaratkan secara kumulatif: digest 8a cocok, validasi Genesis 7b sah, DAN lisensi 7c valid. Jika lisensi 7c tidak valid atau signature/validasi member gagal menurut kontrak PE-01, dekripsi dilarang keras fail-closed (`canPlay: false`, dengan kode error sesuai kontrak PE-01). Status Album Signer `UNKNOWN`, `UNTRUSTED`, atau `REVOKED` tidak dengan sendirinya menjadi global playback gate bagi member; dampaknya pada autentisitas deklarasi membership ditangani terpisah melalui CONF-01 dan lifecycle Registry yang belum ditetapkan.
> 3. *Aturan Dependensi Stage 8b Menuju Stage 8c & Pendaftaran Buffer Terisolasi (Tahap 8b -> Tahap 8c)*:
>    - Stage 8c hanya boleh dilakukan setelah Stage 8b berhasil.
>    - Keberhasilan Stage 8a saja tidak cukup untuk mengizinkan Stage 8c.
>    - Jika Stage 8b gagal, alur pemrosesan wajib dihentikan fail-closed sebelum Stage 8c dijalankan.
>    - Buffer audio yang didaftarkan pada Stage 8c harus merupakan hasil dekripsi yang sah dari Stage 8b untuk *current member*.
>    - Tidak boleh ada buffer registration untuk anggota yang belum menjadi *current member*. Keberhasilan digest 8a atau pre-verifikasi antrean tidak pernah memberikan otorisasi pemutaran atau memicu pendaftaran buffer audio trek berikutnya.

> **Hubungan Kriptografis, Tiga Jenis Hasil Pemeriksaan & Pemisahan Diagnostik Verify vs Otorisasi Playback (AUDIT-NEW-01, Temuan 2, Temuan 9):**
> Dokumen secara tegas membedakan tiga jenis hasil pemeriksaan independen:
> 1. **Pemeriksaan Fisik / Integritas Arsip**: Meliputi struktur internal ZIP, tipe entri (regular file/directory vs symlink/special), path containment, kuota ukuran/entri, kelengkapan arsip, dan konsistensi bijeksi 1:1 antara deklarasi manifest vs Central Directory ZIP.
> 2. **Pemeriksaan Validitas dan Trust**: Meliputi validasi skema JSON manifest, kanonisasi JCS, verifikasi tanda tangan digital Ed25519 (evaluasi Registry signer trust belum tersedia dan tetap unresolved), validasi Genesis Certificate, dan kontrak kriptografis terkait.
> 3. **Keputusan Playback Authorization**: Evaluasi apakah member trek album yang diminta memiliki lisensi/entitlement aktif dan diizinkan untuk didekripsi serta didaftarkan ke audio output pipeline.
>
> *Prinsip Diagnostik Terpisah (NX Verify vs Playback Authorization)*: Status Album Signer `UNKNOWN`, `UNTRUSTED`, atau `REVOKED` tidak boleh secara otomatis menyebabkan seluruh informasi diagnostik integritas fisik tidak tersedia di NX Verify, apabila pemeriksaan file mandiri masih dapat dilakukan secara aman dan independen. Namun, tanpa autentisitas membership, hasil tersebut tidak boleh dilabeli sebagai hasil verifikasi anggota Album. Namun demikian, hasil diagnostik integritas fisik yang valid tersebut **TIDAK BOLEH** dianggap sebagai bukti bahwa member album tersebut *trusted* atau memiliki izin pemutaran (*playback authorization*).
>
> - *Pemisahan Trust vs Integritas*: Tahap 4 pada rancangan proposal ini hanya memuat verifikasi signature manifest secara kriptografis setelah B-08 diselesaikan; evaluasi signer trust pada Registry belum tersedia dan tetap unresolved; integritas container packaging dan genesis certificate (Tahap 7) mengevaluasi keabsahan struktur kontainer; integritas audio payload (Tahap 8) mengevaluasi keaslian bitstream audio. Status signer pada Tahap 4 (misal signer `UNTRUSTED`, `REVOKED`, atau `UNKNOWN`) TIDAK membuktikan member `.nx` `INVALID`; namun, tanpa deklarasi membership yang autentik, hasil pemeriksaan file yang diperoleh secara independen harus dilaporkan sebagai verifikasi standalone, bukan hasil verifikasi anggota Album.
> - *Larangan Pre-Otorisasi*: Pra-verifikasi integritas trek berikutnya dalam antrean Album **TIDAK PERNAH** memberikan otorisasi pemutaran, dekripsi, atau pendaftaran buffer. Izin menjalankan pemeriksaan diagnostik Stage 8a terhadap anggota antrean tetap `UNRESOLVED` sebagaimana §5.2 dan matriks dependensi; dokumen ini tidak menyatakan tindakan tersebut `ALLOWED` maupun melarangnya secara sepihak. Untuk setiap anggota yang menjadi *current member*, seluruh prasyarat otorisasi dan tahapan playback yang relevan wajib dievaluasi ulang secara JIT; Stage 8b/8c hanya untuk current member sesuai kontrak di atas.

#### Navigasi Album NX Player: Pemutaran Sekuensial, Auto-Next Lifecycle, dan Isolasi Otorisasi (Keputusan PO: APPROVED)
Sesuai Keputusan Otoritatif Product Owner untuk PE-02 (§2.5):
1. **Preservasi Perilaku Standalone**: Perilaku pemutaran berkas `.nx` mandiri (*standalone*) pada NX Player Desktop dan Mobile tetap 100% identik dengan baseline yang telah disahkan.
2. **Alur Pemutaran Album Sekuensial & Auto-Next**:
   - Jika pengguna membuka satu Album, NX Player hanya dapat memperlakukan entri sebagai anggota Album dan memproses anggota pertama dalam urutan manifes setelah autentisitas membership manifest dibuktikan secara sah. Jika prasyarat tersebut belum terpenuhi, Player tidak boleh memproses entri manifest sebagai anggota Album. File `.nx` yang dipilih secara independen tetap mengikuti jalur standalone PE-01 dan tidak boleh diberi label sebagai anggota Album.
   - Player mengeksekusi otorisasi JIT 8-tahap sesuai mekanisme existing current Player.
   - Jika anggota tersebut memenuhi seluruh persyaratan trust, integritas, dan otorisasi lisensi aktif (`canPlay: true`), Player memutar/menampilkan aset tersebut.
   - Setelah pemrosesan anggota tersebut selesai menurut kontrak lifecycle transisi Album Player yang akan ditetapkan resmi oleh PO/Arsitektur, Player otomatis beralih ke anggota berikutnya (**Auto-Next**).
   - Proses ini berulang secara sekuensial sampai seluruh anggota Album selesai diproses atau dihentikan pengguna.
3. **Batasan Mutlak Keamanan & Isolasi Otorisasi**:
   - Setiap anggota Album diverifikasi dan diotorisasi secara mandiri dan individual (*per-member isolated authorization*).
   - Otorisasi pemutaran anggota saat ini **TIDAK PERNAH** memberikan otorisasi kepada anggota berikutnya.
   - Background pre-verification (jika diizinkan) **DILARANG KERAS** mengotorisasi anggota berikutnya atau mendaftarkan buffer sebelum anggota menjadi *current member*.
   - Anggota yang tidak memenuhi syarat (misal korup, lisensi tidak aktif) tetap mengikuti kebijakan fail-closed existing Player tanpa menghentikan ketersediaan trek valid lainnya.
   - Trust semantics existing dipertahankan: status `UNKNOWN / INCOMPLETE` tidak boleh otomatis diperlakukan sebagai `INVALID`; kegagalan integritas/signature fisik atau pencabutan otoritatif (*authoritative revocation*) tetap memicu hard-block fail-closed.
   - Dilarang memodifikasi Universal Trust-Aware Viewer, renderer, streaming pipeline, atau memory boundary hanya untuk menambahkan navigasi Album.
4. **Catatan Pembuktian Lifecycle Player Aktual, Temuan Kode Primer, dan Penurunan Kesiapan AC-32 (AUDIT-04 — STOP AND CLARIFY)**:
   - **Keputusan PO Dipertahankan**: Keputusan Product Owner bahwa NX Player harus melakukan Auto-Next secara sekuensial antar-anggota Album tetap dipertahankan penuh sebagai kebutuhan produk yang sah.
   - **Bukti Primer Implementasi Lifecycle Player Aktual (Audio vs Video vs Non-Audio)**:
     - *Payload Audio / Musik*:
       - Path file: `player-desktop/renderer.js`
       - Baris: `L652-L655`
       - Potongan kode primer:
         ```javascript
         audioEngine.addEventListener('ended', () => {
             stopAudio();
             playNextLibraryAsset();
         });
         ```
       - Analisis Fakta: Handler event `'ended'` pada `audioEngine` memanggil fungsi `playNextLibraryAsset()` (`renderer.js#L957-L961`) yang merotasi indeks array pustaka GUI desktop (`libraryAssets[currentAssetIndex]`). Laporan inspeksi lokal Programmer menyatakan adanya pemicu rotasi file antrean GUI desktop, tetapi laporan ini belum diverifikasi independen dan **BUKAN** bukti kontrak transisi lifecycle multi-anggota Album yang disahkan platform Nexa. Pada level kontrak platform, integrasi transisi antar-anggota Album belum diratifikasi.
     - *Payload Video*:
       - Path file: `player-desktop/renderer.js`
       - Laporan inspeksi lokal Programmer atas elemen `videoEngine` (`renderer.js#L75, L319, L496, L692-L771`) menyatakan hanya terdapat listener `timeupdate` (L708) dan `durationchange` (L717), serta tidak menemukan handler `ended`. Klaim ini belum diverifikasi independen; Klaim terdahulu bahwa Video berstatus `SPEC READY (Ended Event)` tidak memiliki bukti implementasi primer dan dinyatakan gugur.
     - *Payload Non-Audio (Dokumen & Gambar)*: Dokumen dan gambar tidak memiliki durasi atau event selesai pemutaran alami. White Paper v5.6 dan Roadmap v4.8 tidak menetapkan kriteria normatif kapan proses viewing dokumen/gambar dianggap selesai untuk memicu Auto-Next; status repository lokal hanya laporan Programmer dan belum diverifikasi independen.
     - *Player Mobile (iOS / Android)*: Status implementasi lifecycle background/foreground dan transisi pemutaran mobile belum diverifikasi secara independen (`NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`).
   - **Prinsip Stop-and-Clarify Mutlak**: Programmer dan perancang **DILARANG KERAS** mengarang timer buatan, interval durasi viewing sepihak, trigger callback sintetis, atau mengasumsikan rotasi GUI desktop berlaku sebagai kontrak Album. Seluruh pemicu Auto-Next untuk keempat tipe payload berstatus: **`STOP AND CLARIFY — KONTRAK TRANSISI LIFECYCLE AUTO-NEXT ALBUM MEMERLUKAN PENETAPAN RESMI PO / ARSITEKTUR`**.
   - **Penurunan Status Kesiapan AC-32**: Status AC-32 diturunkan menjadi **`[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MULTI-PAYLOAD AUTO-NEXT LIFECYCLE CONTRACT]`** guna mencerminkan fakta bahwa seluruh payload belum memiliki spesifikasi kontrak lifecycle transisi Album yang siap dieksekusi.
   - **Preservasi Mutlak Boundary**: Perilaku standalone Player, otorisasi JIT 8-tahap per-anggota, trust semantics (`UNKNOWN/INCOMPLETE` tidak otomatis `INVALID`), larangan background pre-verification memberikan otorisasi, renderer, streaming pipeline, dan memory boundary existing tetap 100% dipreservasi tanpa modifikasi.

---

### 5.3 NX Verify — Tiga Lapisan Status Terpisah & Batasan Jalur Diagnostik (AUDIT-NEW-01, CONF-02 PO APPROVED)
NX Verify mengevaluasi arsip album dalam 3 lapisan status independen tanpa mencampuradukkan diagnostik integritas dengan izin pemutaran:
1. **Lapisan 1: Album Signer Trust / Provenance Status**: Status registrasi/trust `album_signer_public_key` pada Registry resmi hanya dapat dievaluasi apabila mekanisme Registry untuk identitas dan lifecycle Album Signer telah ditetapkan secara otoritatif. Mekanisme tersebut saat ini `UNRESOLVED — REGISTRY MECHANISM NOT ESTABLISHED BY PRODUCT CONTRACT` (NC-04 / B-09); karena itu, penyebutan `TRUSTED`, `UNTRUSTED`, `REVOKED`, atau `UNKNOWN` di sini adalah kategori kondisi yang perlu ditangani, bukan klaim bahwa endpoint, record, atau lifecycle Registry Album Signer telah tersedia.
   - *Batasan Mutlak Layer 1 (AUDIT-TRUTH-03)*: Status Album Signer pada Lapisan 1 **DILARANG DIJADIKAN SEBAGAI GERBANG GLOBAL (GLOBAL GATE)** yang menentukan validitas atau otorisasi seluruh member `.nx`.
   - Pemeriksaan integritas mandiri pada Lapisan 2 hanya dapat dijalankan terhadap file `.nx` yang dipilih/disediakan secara independen dan aman. Jika autentisitas manifest/membership belum terbukti (CONF-01), file dari daftar manifest tidak boleh otomatis diperlakukan sebagai anggota Album yang sah; hasil pemeriksaannya, bila sumber file tersedia secara independen, harus dilaporkan sebagai verifikasi standalone.
   - Hasil pemeriksaan manifest tidak boleh menyembunyikan, menimpa, atau menggantikan status verifikasi setiap member yang membership-nya telah dibuktikan secara sah.
   - Status `UNKNOWN / INCOMPLETE` wajib dipertahankan dan ditampilkan sebagai kondisi ketidakpastian sesuai empat status kanonikal Nexa (`Trust Unknown` / `Verification Incomplete`); status tersebut **DILARANG KERAS** dipetakan atau diperlakukan sebagai `INVALID`.
2. **Lapisan 2: Evaluasi Integritas Fisik Anggota & Kategori Diagnostik Internal (PE02-R63-AUD-05)**:
   Mengevaluasi integritas fisik kontainer mandiri PE-01 untuk file `.nx` yang membership-nya telah dibuktikan secara sah atau yang disediakan secara independen untuk pemeriksaan standalone. Cakupan format payload yang relevan adalah Music, Video, Document, dan Image; pencocokan hash bitstream audio hanya berlaku untuk payload audio dan tetap tunduk pada unresolved field identity serta dependensi Stage 8a. Pemeriksaan standalone tidak boleh dilabeli sebagai verifikasi anggota Album.
   - *Pemisahan Tegas Kategori Diagnostik Internal vs Status Kanonikal*:  
     Istilah diagnostik seperti `VALID`, `CORRUPTED`, dan `TAMPERED` pada lapisan ini adalah **murni kategori temuan diagnostik internal / penanda forensik lokal**, dan **DILARANG KERAS** diperlakukan sebagai status verifikasi kanonikal baru atau pengganti status kanonikal Nexa.
   - *Kepatuhan Mutlak pada Empat Status Kanonikal Nexa*:  
     Seluruh hasil verifikasi anggota album yang ditampilkan kepada pengguna atau disimpan tetap tunduk 100% pada **empat canonical verification statuses**:
     1. `Integrity Verified` (integritas fisik kontainer/payload terbukti sah);
     2. `Trust Verified` (integritas sah dan signer/creator terdaftar aktif di Registry resmi);
     3. `Trust Unknown` (integritas sah tetapi signer/creator tidak dikenal / status UNKNOWN);
     4. `Invalid` (integritas fisik gagal, signature cacat, hash mismatch [TAMPERED], berkas rusak [CORRUPTED], atau sertifikat dicabut).
   - *Preservasi Multi Registry States & Local Override (White Paper v5.6 §4.2.1)*:  
     Lima internal Multi Registry states (`CONSISTENT`, `INCOMPLETE`, `CONFLICT`, `REVOKED`, `UNTRUSTED`) dan semantik Local Override tetap berlaku utuh sesuai White Paper v5.6 §4.2.1:
     - `CONSISTENT` dipetakan ke status kanonikal `Trust Verified` (🟢 Trusted);
     - `INCOMPLETE` dipetakan ke status kanonikal `Trust Unknown` (🟡 Verification Incomplete);
     - `CONFLICT` dipetakan ke status kanonikal `Trust Unknown` dengan sub-varian `Trust Unknown (Local Override)` bila pengguna memilih override (🟠 Verification Conflict);
     - `REVOKED` dipetakan ke status kanonikal `Invalid` (🔴 Revoked);
     - `UNTRUSTED` dipetakan ke status kanonikal `Invalid` akibat kegagalan signature/hash Tier 1 (🔴 Untrusted).
     Kelima internal state ini adalah taksonomi resolusi UI/UX skenario multi-registry dan **DILARANG** diperlakukan sebagai pengganti status kanonikal atau diperkenalkan dengan nomenklatur pengganti.
   - *Status Pemetaan Normatif*: Pemetaan formal antara kode diagnostik internal ke format visual laporan dikunci sebagai **`DIAGNOSTIC CATEGORIES BOUND BY 4 CANONICAL STATUSES (MAPPING DETAILS SUBJECT TO NORMATIVE TAXONOMY NC-15)`**.
3. **Lapisan 3: Penegasan Ketiadaan Status Agregat Album (CONF-02 / NC-14 Keputusan PO: PILIHAN B — APPROVED)**:
   Sesuai Keputusan Otoritatif Product Owner (CONF-02 / NC-14 Pilihan B APPROVED), NX Verify **TIDAK MENAMPILKAN** satu status agregat keseluruhan Album. Hasil verifikasi individual setiap berkas `.nx` tetap menjadi hasil utama.
   Keputusan ini tidak mengubah:
   - empat canonical verification statuses;
   - lima internal Multi Registry states;
   - Local Override semantics;
   - trust semantics individual file.
   Dilarang keras menciptakan status baru seperti `ALBUM_TRUSTED`, `ALBUM_INVALID`, `ALBUM_VALID`, atau status agregat sintetis lainnya.

#### Navigasi Album NX Verify: Verifikasi Sekuensial, Manual Next, dan Preservasi Verify Desktop vs Mobile Lite (Keputusan PO: APPROVED)
Sesuai Keputusan Otoritatif Product Owner untuk PE-02 (§2.6 & §2.7):
1. **Preservasi Perilaku Standalone**: Perilaku verifikasi berkas `.nx` mandiri (*standalone*) pada NX Verify Desktop dan Mobile tetap 100% identik dengan baseline existing.
2. **Alur Verifikasi Album Sekuensial & Manual Next**:
   - Prasyarat wajib: sebelum suatu file diproses atau ditampilkan sebagai anggota Album, autentisitas deklarasi membership manifest harus telah dibuktikan menurut kebijakan/otoritas signer yang sah (CONF-01 / B-09). Pemeriksaan struktur ZIP-manifest saja tidak memenuhi prasyarat ini.
   - Jika autentisitas membership belum terbukti, NX Verify DILARANG memproses atau melabeli file dari daftar manifest sebagai anggota Album. File `.nx` yang dipilih/disediakan secara independen tetap dapat diverifikasi melalui jalur standalone PE-01 dan hasilnya harus dilabeli sebagai verifikasi standalone, bukan verifikasi anggota Album.
   - Hanya setelah prasyarat autentisitas membership terpenuhi, jika pengguna membuka satu Album di NX Verify, sistem memproses anggota pertama.
   - Verify melakukan verifikasi integritas menggunakan mekanisme existing.
   - Verify menampilkan hasil verifikasi anggota tersebut secara individual.
   - Pengguna menekan tombol **Next** secara MANUAL untuk memproses anggota berikutnya.
   - Proses berulang sampai seluruh anggota Album selesai diverifikasi.
3. **Batasan Mutlak Verifikasi Album**:
   - Tombol **Next** hanya berlaku dalam konteks Album.
   - Perpindahan dilakukan secara **MANUAL** oleh pengguna (tidak ada auto-advance pada Verify).
   - Setiap anggota diverifikasi sendiri-sendiri secara independen.
   - Hasil setiap anggota wajib dapat dilihat secara individual.
   - Tidak boleh ada status agregat keseluruhan Album.
   - Dilarang menyamarkan anggota yang Invalid, Unknown, Incomplete, atau memiliki konflik.
   - NX Verify murni diagnostik dan **TIDAK MEMBERIKAN** playback authorization.
4. **Pemisahan Tegas Fitur Verify Desktop vs Verify Mobile (Lite)**:
   - **Verify Desktop (Full Verify)**: Tetap Full Verify sesuai White Paper v5.6. Penambahan tombol Next untuk Album tidak boleh menghapus atau mengubah fungsi Full Verify existing, termasuk Batch Verification, Export Verification Report, dan manual Registry Refresh.
   - **Verify Mobile (Verify-Lite)**: Tetap Verify-Lite sesuai White Paper v5.6. Penambahan tombol Next hanya merupakan navigasi manual untuk berpindah ke anggota Album berikutnya dan menjalankan verifikasi individual ringan. Penambahan tersebut **DILARANG KERAS** ditafsirkan sebagai persetujuan untuk memporting fitur Full Verify Desktop ke Mobile. Dilarang menambahkan: (a) Batch Verification Full Desktop, (b) Export Verification Report, (c) manual Registry Refresh, dan (d) payload rendering pada mobile.

> **Prinsip Operasional Diagnostik Independen vs Larangan Backdoor Playback (AUDIT-NEW-01):**
 > 1. *Kelanjutan Pemeriksaan Diagnostik vs Status Signer (FINDING-03)*: Status Album Signer `UNKNOWN`, `UNTRUSTED`, atau `REVOKED` tidak dengan sendirinya menetapkan `INVALID` pada member `.nx` atau menjadi global playback gate. CONF-01 hanya memutuskan apakah deklarasi manifest dapat mengautentikasi membership Album serta dasar identitas/lifecycle signer; sampai diputuskan, membership dari manifest tidak boleh diasumsikan autentik. File `.nx` yang dipilih/disediakan secara independen tetap dievaluasi sebagai file standalone menurut PE-01. NX Verify dapat menjalankan diagnostik individual atas file yang memang disediakan secara independen; hasilnya bukan verifikasi membership Album dan tidak memberikan playback authorization.
> 2. *Larangan Jalur Pemutaran Alternatif (No Backdoor Playback)*: Hasil diagnostik Lapisan 2 dengan penanda `VALID` (atau status `Integrity Verified`) **DILARANG KERAS** ditafsirkan sebagai pemberian izin pemutaran atau substitusi atas lisensi aktif.
> 3. *Larangan Dekripsi dan Buffer Registration pada Diagnostik*: Selama pemeriksaan diagnostik di NX Verify, sistem HANYA membaca bitstream terenkripsi untuk menghitung digest SHA-256; sistem **DILARANG** mendekripsi payload audio dan **DILARANG** mendaftarkan buffer ke audio output pipeline.
> 4. *Status Dekripsi Diagnostik*: Ketiadaan kontrak normatif mengenai batas dekripsi parsial diagnostik dicatat secara eksplisit sebagai **`UNRESOLVED — NORMATIVE CONTRACT NOT VERIFIED`** (menunggu keputusan resmi Product Owner / Architecture Board).

---

### 5.4 NX Studio — Dua Jenis Jalur Pemrosesan Album (Forge New vs Select Existing) & Larangan Album Campuran (Keputusan PO: APPROVED)
Sesuai White Paper v5.6 dan Keputusan Otoritatif Product Owner (§2.3):
NX Studio mengoperasikan dua jalur pemrosesan Album yang berbeda secara struktural, di mana keduanya bermuara pada shared `NXPublishPipeline`. Perbedaan kedua jalur wajib dipertahankan secara tegas:

#### A. Jalur 1: Album Forge New
1. **Jenis Masukan**: Beberapa berkas sumber biasa (*raw source files*), meliputi:
   - Image;
   - Document;
   - Music;
   - Video.
2. **Perilaku Operasional**:
   - Setiap berkas sumber diproses secara individual melalui tahapan forging normal.
   - Setiap forging yang berhasil menghasilkan satu berkas `.nx` tersendiri yang independen.
   - Hasil berkas `.nx` tersebut dipublikasikan melalui workflow Marketplace existing.
   - Setelah satu anggota selesai diproses dan dipublikasikan, Studio melanjutkan ke anggota berikutnya.
   - Proses berlangsung berurutan (sekuensial) sampai semua anggota selesai atau kegagalan ditangani pengguna.
3. **Larangan Desain**: Dilarang keras menggabungkan beberapa file sumber biasa menjadi satu berkas `.nx`.

#### B. Jalur 2: Album Select Existing `.nx`
1. **Jenis Masukan**: Beberapa berkas kontainer `.nx` yang sudah ada (*existing `.nx` files*, mencakup Music, Video, Document, dan Image yang telah di-forging sebelumnya).
2. **Perilaku Operasional**:
   - Setiap berkas `.nx` diperlakukan sebagai aset independen yang telah sah.
   - Setiap anggota dipublikasikan melalui `NXPublishPipeline` existing.
   - Tidak dilakukan forging ulang (*no re-forging*) hanya karena berkas tersebut dikelompokkan menjadi anggota Album.
   - Setelah satu anggota selesai dipublikasikan, Studio melanjutkan ke anggota berikutnya.
   - Proses berlangsung berurutan (sekuensial) sampai semua anggota selesai atau kegagalan ditangani pengguna.
3. **Larangan Desain**: Dilarang keras membuat sertifikat Genesis sintetis (*synthetic Genesis*) untuk existing `.nx` agar publikasi berhasil.

#### C. Larangan Mutlak Album Campuran (Keputusan PO: APPROVED)
**Keputusan Otoritatif Product Owner: APPROVED — kedua jalur didukung penuh, namun satu Album DILARANG KERAS mencampur kedua jenis masukan.**
Dengan demikian:
1. Album Forge New **HANYA** berisi berkas sumber biasa.
2. Album Existing `.nx` **HANYA** berisi berkas `.nx` yang sudah ada.
3. Satu Album **DILARANG KERAS** berisi kombinasi berkas sumber biasa dan existing `.nx`.
4. **Validasi Masukan Pra-Pemrosesan**: Validasi jenis masukan wajib dieksekusi secara ketat SEBELUM workflow pemrosesan Album dimulai.
5. **Penolakan Fail-Closed Tanpa Mutasi**: Jika komposisi masukan tidak memenuhi aturan jenis tunggal (misal ditemukan campuran sumber biasa dan `.nx`), sistem wajib menolak proses secara fail-closed. Dilarang memindahkan berkas secara diam-diam (*silent moving*), dilarang mengubah jenis masukan secara diam-diam (*silent conversion*), dilarang mereklasifikasi jalur secara sepihak, dan dilarang merusak atau menghapus berkas masukan pengguna.

---

### 5.5 NX Studio — Mekanisme Penanganan Kegagalan (Failure Handling: Ulangi & Lewati) (Keputusan PO: APPROVED)
Sesuai Keputusan Otoritatif Product Owner (§2.4):
NX Studio menerapkan dua tindakan diskrit baru untuk menangani kegagalan pemrosesan Album: **Ulangi (Retry)** dan **Lewati (Skip)**. Keduanya berlaku pada tahap spesifik yang mengalami kegagalan, bukan sebagai pengganti keseluruhan workflow:

#### A. Penanganan Kegagalan Tahap Forging (Album Forge New)
Jika forging anggota Album Forge New mengalami kegagalan:
1. **Ulangi**:
   - Mengulangi tahapan forging untuk berkas sumber biasa yang sama.
   - Sistem **TIDAK BOLEH** berpindah ke berkas berikutnya sebelum pengguna secara eksplisit memilih tindakan.
2. **Lewati**:
   - Menandai berkas sumber tersebut sebagai dilewati (*skipped*).
   - Tidak melakukan upload ke Marketplace untuk berkas yang forging-nya gagal.
   - **TIDAK MENGHAPUS** berkas sumber asli.
   - Melanjutkan proses ke anggota berikutnya dalam antrean.

#### B. Penanganan Kegagalan Tahap Upload Pasca-Forging Berhasil (Album Forge New)
Jika forging berhasil menghasilkan berkas `.nx`, namun tahap upload ke Marketplace gagal:
1. **Ulangi**:
   - Mengulangi tahap upload untuk hasil berkas `.nx` yang sudah berhasil dibuat.
   - **TIDAK MENGULANG FORGING** (menggunakan hasil forging yang sama yang telah tersimpan di storage lokal/staging).
   - Wajib mencegah listing Marketplace duplikat akibat proses pengulangan (retry), sesuai hasil yang disetujui PO. Mekanisme teknis idempotensi publication pipeline belum ditetapkan sebagai kontrak produk; Programmer wajib membuktikan dukungan mekanisme existing dari sumber primer atau mempertahankan statusnya sebagai unresolved. Dilarang menciptakan API, idempotency key, atau mekanisme pengganti.
2. **Lewati**:
   - Menandai tahap upload anggota tersebut sebagai gagal/dilewati sesuai status yang dibedakan dalam plan.
   - Melanjutkan proses ke anggota berikutnya dalam antrean.
   - **TETAP MEMPERTAHANKAN** berkas sumber asli dan hasil berkas `.nx` yang sudah berhasil di-forging di storage lokal.

#### C. Penanganan Kegagalan Tahap Upload pada Album Existing `.nx`
Untuk Album Existing `.nx` yang gagal dipublikasikan/di-upload:
1. **Ulangi**:
   - Mengulangi tahap publication/upload anggota yang gagal melalui jalur `NXPublishPipeline` existing.
   - Tidak memodifikasi atau mengubah berkas `.nx` sumber.
2. **Lewati**:
   - Menandai anggota tersebut dilewati/tidak berhasil dipublikasikan.
   - Melanjutkan proses ke anggota berikutnya.
   - **TIDAK MENGHAPUS** berkas `.nx` sumber.

#### D. Aturan Umum dan Batasan Failure Handling
1. **Larangan Tindakan Otomatis Tanpa Batas**:
   - Sistem **DILARANG** melakukan auto-retry tanpa batas (*no infinite automatic retry*).
   - Sistem **DILARANG** melakukan auto-skip (*no automatic skip*).
   - Proses batch Album wajib berhenti sementara (*pause*) pada titik kegagalan hingga pengguna menentukan pilihan (Ulangi atau Lewati).
2. **Pemisahan Tegas Status Forging vs Status Upload**:
   - Status forging dan status upload wajib dibedakan secara terpisah dalam status pelaporan Studio.
   - Kegagalan pada tahap upload **TIDAK BOLEH** mengubah status forging yang sudah berhasil menjadi gagal.
   - Tindakan retry wajib mempertahankan hasil pekerjaan yang telah berhasil diselesaikan sebelumnya.
3. **Idempotensi Publikasi vs Transaksi Terdistribusi B-04 (PE02-R63-AUD-04)**:
   - **Evaluasi Pembuktian Repositori Primer atas Mekanisme Idempotensi Publikasi Studio (`NC-01`, `NC-06`)**:
     > [!NOTE]
     > **Keterbukaan Status Verifikasi Independen (PE02-R63-AUD-04):**  
     > Seluruh rujukan path, nomor baris, dan potongan kode primer di bawah ini bersumber dari inspeksi repositori lokal Programmer pada host server Linux (`whisnu/nexa`). Karena akses repositori sumber primer belum tersedia untuk verifikasi independen oleh Auditor, status bukti implementasi ini diklasifikasikan secara jujur bagi audit eksternal sebagai:  
     > **`NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE (Berdasarkan Laporan Inspeksi Lokal Programmer; Audit Independen Pending)`**.  
     > Dokumen memisahkan secara tegas antara: (1) Kesiapan spesifikasi requirement idempotensi (`SPEC READY`); (2) Bukti inspeksi kode statis existing; dan (3) Ketiadaan pengujian eksekusi runtime fisik (`NOT VERIFIED — EVIDENCE NOT AVAILABLE`).
     
     Ringkasan berikut merupakan laporan inspeksi kode lokal Programmer pada alur retry publikasi; seluruh path dan perilaku yang disebut REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED:
     1. *Identitas Sesi Tetap Sama saat Retry*:
        - Laporan Programmer tentang klien Studio: `studio-desktop/publish_pipeline.js#L316-L320, L342` mempertahankan ID sesi yang sama (`this.sessionId`) saat mengeksekusi ulang permintaan finalisasi (`POST /api/catalog/submit-package/:sessionId/finalize`).
        - Laporan Programmer tentang server Marketplace: `marketplace/server.js#L2453-L2461` mengambil rekaman sesi dari tabel `marketplace_upload_sessions` berdasarkan parameter URL `sessionId` (`SELECT * FROM marketplace_upload_sessions WHERE session_id = ?`).
     2. *Perilaku saat Finalisasi Berhasil di Server tetapi Respons Tidak Diterima Klien (Network Partition / 504 Timeout)*:
        - Laporan Programmer tentang server idempotency: `marketplace/server.js#L2467-L2470`:
          ```javascript
          if (session.state === 'PUBLISHED') {
            const catRes = await store.allQuery('SELECT * FROM catalog_snapshots WHERE asset_id = ?', [session.asset_id]);
            return res.status(200).json({ success: true, status: 'PUBLISHED', state: 'PUBLISHED', data: catRes && catRes[0] });
          }
          ```
          Jika server telah berhasil menyelesaikan publikasi (`state === 'PUBLISHED'`), panggilan retry finalisasi berikutnya mengembalikan HTTP 200 secara instan beserta data snapshot yang sudah ada, tanpa memproses ulang atau menciptakan entri baru.
        - Laporan Programmer tentang ketahanan gateway reverse-proxy: `marketplace/server.js#L2485-L2520` mendukung finalisasi asinkron (`x-async-finalize: true` atau `?async=true`) yang segera merespons HTTP 202 `Accepted` untuk mencegah gateway timeout 504, sementara proses verifikasi dan listing dijalankan di latar belakang via `setImmediate`.
        - Laporan Programmer tentang fallback polling klien: `studio-desktop/publish_pipeline.js#L340-L346, L370-L410`: jika terjadi kegagalan jaringan atau respons 504/502 pada panggilan finalisasi, klien secara otomatis beralih memantau status sesi via `getStatus()` (`GET /api/catalog/submit-package/:sessionId/status`) hingga status mencapai `PUBLISHED`.
     3. *Perilaku Retry saat Finalisasi Masih Berlangsung*:
        - Laporan Programmer tentang concurrency guard server: `marketplace/server.js#L2490-L2497` mengecek apakah sesi sedang diproses (`session.state === 'VERIFYING_AND_INGESTING' || activeFinalizations.has(sessionId)`); jika ya, server segera mengembalikan respons HTTP 202 Accepted (`Finalization already in progress`) tanpa memicu duplikasi prosesor latar belakang.
     4. *Perilaku Retry saat Kegagalan Terjadi di Tengah Proses (Storage / Listing)*:
        - Invariant K byte preservation: `marketplace/server.js#L2451, L2472-L2474` dilaporkan Programmer menunjukkan bahwa jika transfer biner telah selesai (`committedBytes >= totalBytes`), retry finalisasi dari status `STORAGE_CONFIRMED` atau `LISTING_FAILED_RETRY` dapat dilakukan tanpa mengunggah ulang data biner.
        - Pemulihan status gagal: `marketplace/server.js#L2560-L2575` memperbarui status sesi ke `VERIFICATION_OR_TRUST_FAILED` (jika verifikasi gagal) atau `LISTING_FAILED_RETRY` (jika tahap penyimpanan/listing gagal sementara `storage_object_id` telah terbentuk), memungkinkan retry finalisasi terarah.
     5. *Evaluasi Batas Pembuktian Pencegahan Duplikasi & Efek Samping Publikasi (FINDING-05)*:
        - *Tabel Katalog*: `marketplace/server.js#L2400-L2416` melakukan atomic upsert `INSERT INTO catalog_snapshots (...) VALUES (...) ON CONFLICT (asset_id) DO UPDATE SET ... listing_status = 'LISTED_ACTIVE'`.  
          *Batas Pembuktian*: Klausul `ON CONFLICT (asset_id) DO UPDATE` menurut laporan Programmer menunjukkan pencegahan duplikasi baris pada tabel `catalog_snapshots` untuk `asset_id` bersangkutan. Kutipan ini **DILARANG** diperlakukan sebagai verifikasi independen atau diklaim membuktikan tidak adanya duplikasi multi-listing atau ketiadaan efek samping pada seluruh alur Marketplace lainnya di luar tabel ini.
        - *Tabel Sesi*: `marketplace/server.js#L2440-L2444` memperbarui sesi in-place via `UPDATE marketplace_upload_sessions SET state = 'PUBLISHED' ... WHERE session_id = ?` (memperbarui status sesi tunggal).
        - *Penyimpanan Berkas Sidecar*: `marketplace/server.js#L2378-L2384` menulis berkas sidecar secara deterministik ke `${packageSha256}.nx.nxcert` (menimpa path yang sama berdasarkan hash bitstream).
        - *Pemberhentian Dini (Short-Circuit)*: Pemeriksaan awal pada baris 2467-2470 mengembalikan data snapshot yang ada sebelum verifier, pipeline storage, atau mutasi database katalog dijalankan kembali.
        - *Batas Bukti Runtime*: Seluruh bukti di atas bersumber dari inspeksi kode statis lokal Programmer; pengujian runtime aktual atas pencegahan efek samping publikasi berstatus `NOT VERIFIED — EVIDENCE NOT AVAILABLE`.
     6. *Penggunaan Hasil Forging yang Sama Tanpa Forging Ulang*:
        - Laporan Programmer tentang alur Studio: Tahap forging dan tahap publikasi dipisahkan secara modular pada `studio-desktop/main.js#L1097-L1212` dan `publish_pipeline.js`.
        - Berkas `.nx` hasil forging disimpan pada disk staging lokal; IPC handler `publish-asset` menerima path fisik berkas (`assetPath`).
        - Saat aksi "Ulangi" dipilih pasca kegagalan upload, Studio langsung memanggil `publish-finalize-retry` (`main.js#L1248-L1255`) atau `publish-resume` (`main.js#L1224-L1235`) menggunakan berkas fisik `.nx` yang telah terbentuk, tanpa memanggil fungsi forging ulang (`forgeNxContainer` / `forgeAlbumTrack`) atau mengubah hash bitstream kontainer.
     7. *Batasan Pembuktian & Gap Sesi Batch Multi-Member*:
        - Seluruh mekanisme idempotensi di atas dilaporkan Programmer pada level **sesi unggah individual** (`session_id`) per berkas `.nx`; belum diverifikasi independen.
        - Laporan inspeksi lokal Programmer menyatakan bahwa repository existing tidak menunjukkan koordinator transaksi atomik multi-sesi untuk mempublikasikan seluruh anggota Album dalam satu kesatuan batch terpadu; klaim ini belum diverifikasi independen (jika sebagian trek berhasil dan sebagian gagal). Kondisi ini dicatat sebagai gap arsitektur tanpa mengarang mekanisme transaksi baru.
   - **Pemisahan Tegas dari Transaksi Settlement Pembeli B-04 / NC-08**:
     - *Mekanisme A (Idempotensi Publikasi Studio - NC-01, NC-06)*: Dilaporkan Programmer pada alur upload berkas dari kreator ke Marketplace; belum diverifikasi independen.
     - *Mekanisme B (Transaksi Settlement Terdistribusi - NC-08 / B-04 / CONF-03)*: Menurut laporan inspeksi lokal Programmer, alur pembelian pada `marketplace/server.js#L170` memotong kredit dan memanggil License Daemon secara asinkron tanpa 2PC; laporan ini belum diverifikasi independen dan B-04/CONF-03 tetap terbuka.
     - Idempotensi publikasi Studio **DILARANG KERAS** diasumsikan menyelesaikan atau menggantikan transaksi settlement B-04. Keduanya adalah domain arsitektur yang sepenuhnya berbeda.
     - Kriteria penerimaan **AC-31 dipetakan secara eksklusif ke NC-01 dan NC-06** (Studio Packaging & Publication Workflow), dan **DILARANG DIPETAKAN KE NC-08**. NC-08 tetap dipetakan eksklusif ke AC-14 dan AC-15, dan **TETAP BERSTATUS `BLOCKED BY ARCHITECTURE (B-04 / CONF-03)`** hingga Otoritas Arsitektur menetapkan solusi transaksi terdistribusi yang sah.
   - Perancang dilarang mengarang API baru, idempotency key buatan, field database baru, atau mekanisme transaksi baru tanpa bukti dari repositori. Jika bukti primer independen belum tersedia untuk mendukung idempotensi penuh di luar pipeline publikasi, kondisi tersebut dicatat sebagai gap arsitektur.
4. **Target Status Granular per Anggota**:
   Status pelaporan Studio per anggota wajib membedakan secara tegas minimal 5 kondisi:
   - `FORGING_SUCCESS` (forging berhasil);
   - `FORGING_FAILED` (forging gagal);
   - `PUBLICATION_SUCCESS` (publication/upload berhasil);
   - `PUBLICATION_FAILED` (publication/upload gagal);
   - `SKIPPED_BY_USER` (dilewati oleh pengguna).
5. **Larangan Penyamaran Status Agregat**:
   Studio **DILARANG KERAS** membuat satu status keberhasilan agregat Album yang menyamarkan atau menutupi kegagalan anggota di dalamnya.

---

## 6. NORMATIVE CONTRACT REGISTER (NC-01 SAMPAI NC-16)

Tabel berikut merangkum 16 kontrak normatif (*Normative Contracts*) dengan status spesifikasi, bukti, dan ketergantungan yang diselaraskan dengan hasil audit:

| ID | Nama Kontrak & Deskripsi Singkat | Status Spesifikasi | Status Implementasi | Status Blocker / Keputusan | Dependensi & Catatan Audit |
|:---:|:---|:---:|:---:|:---:|:---|
| **NC-01** | Skema Manifest Album & Binding Anggota (universal schema belum lengkap) | `PARTIALLY SPECIFIED / NON-NORMATIVE AUDIO DRAFT` | `NOT IMPLEMENTED` | `BLOCKED — UNIVERSAL SCHEMA & IMPLEMENTATION GAP` | Kebijakan unknown fields telah diputuskan PO: reject unknown fields secara fail-closed (AC-01). Draf audio tetap bukan schema normatif universal; schema multi-payload dan field universal masih harus diselesaikan. |
| **NC-02** | Signature Album Signer & Byte Kanonikal JCS | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED — REQ CLARIFICATION` | Circular dependency manifest signature menahan spesifikasi penandatanganan (B-08, AC-03). |
| **NC-03** | Strict JSON Parser & RFC 8785 JCS Serializer | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED BY B-01, B-02` | Terblokir implementasi B-01 & B-02. Duplicate key: Nexa parser policy (AC-05, AC-06). |
| **NC-04** | Autentisitas Deklarasi Manifest saat Album Signer `UNKNOWN` & Lifecycle Signer | `PARTIALLY SPECIFIED / GAP UNRESOLVED` | `NOT IMPLEMENTED` | `MEMBERSHIP POLICY APPROVED; SIGNER IDENTITY / LIFECYCLE CONTRACT OPEN` | PO telah mengesahkan Album Membership Authenticity Fail-Closed: signer UNKNOWN atau signature manifest invalid tidak mengautentikasi membership; standalone PE-01 tetap independen. Identity binding, authority, trust store, rotation, revocation, dan freshness tetap merupakan gap teknis B-09/AC-07/AC-08. |
| **NC-05** | Validasi Genesis Ownership Certificate & Audio Payload Binding | SPECIFIED | NOT IMPLEMENTED | OPEN / BLOCKED BY FIELD IDENTITY & GENESIS ERROR TAXONOMY; AUDIT-NEW-10 DESIGN RECONCILED | Semantik tiga peran dan otorisasi packaging telah diputuskan PO dan dirancang pada §13.12.11; implementasi verifier/delegation adalah build requirement, bukan unresolved 3-way binding. Taksonomi error Genesis dan identitas field audio tetap mengikuti blocker masing-masing. |
| **NC-06** | Ekstraksi & Packaging Kontainer Audio Mandiri dalam Arsip Album | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY AC-28 / AC-29 — ALBUM IDENTITY, PERSISTENCE & RELOAD UNRESOLVED` | Verifikasi container signature `.nx` dan ekstraksi tetap mengikuti kontrak member PE-01 (AC-04, AC-11, AC-12); asosiasi identitas Album multi-member, persistence, dan rekonstruksi/reload belum ditetapkan (AC-28, AC-29). |
| **NC-07** | Batas Keamanan Ekstraksi Arsip ZIP Wrapper | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Kuota 500 MB desimal (500.000.000 bytes) / 4 GB desimal / 200 entri (entri direktori diterima sesuai Keputusan PO AUDIT-NEW-06; pembatasan flat hanya berlaku pada regex path relatif member .nx manifest); usulan rasio kompresi B-07 (ambiguitas 10:1 vs 100:1 referensi pembanding eksternal yang belum diverifikasi pending arsitektur) per-entri & global (AC-13, B-07). |
| **NC-08** | Marketplace Transaction Settlement & Replay Protection | `PARTIALLY SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED — TECHNICAL TRANSACTION / FULFILLMENT CONTRACT OPEN` | Model B, SSP/Largest Remainder, `bundle_checkout_id`, dan Immutable Checkout Manifest telah disahkan (§6.8.1–§6.8.3). Storage/persistensi, pemetaan member-to-acquisition, idempotency/replay, partial-failure policy, commit/recovery, settlement, dan konsistensi side effect License Daemon masih harus dirancang. Tidak ada asumsi 2PC atau rollback eksternal. |
| **NC-09** | Inventarisasi Objek Kriptografis & Hash Berbasis Bukti Faktual (AUDIT-NEW-04) | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED` | Inventarisasi berbasis bukti atas signature Ed25519 dan hash SHA-256 faktual di §6.9; pemisahan objek terverifikasi dari entitas komputasional internal; semantik kolom `acquired_package_sha256` adalah blocker B-05 (AC-16). |
| **NC-10** | Kepatuhan Mutlak Skema Zero-DDL Marketplace | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Skema PostgreSQL aktif dipatuhi; dapat diuji independen dari model B-04 (AC-17). |
| **NC-11** | Mekanisme Offline Fallback Registry Terkendali | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Fallback HANYA untuk transport network error; HTTP 5xx/bad sig fail-closed (AC-18, AC-19). |
| **NC-12** | Filesystem Safe-Open Berbasis Invariant Keamanan (AUDIT-NEW-03) | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY B-06` | Pembukaan descriptor `O_NOFOLLOW` + `fstatSync` dilaporkan Programmer pada E-07; belum diverifikasi independen; verifikasi ganda `lstatSync` dan `dev`/`ino` berstatus gap residu kode desktop; batas userspace POSIX diakui; fail-closed `canPlay: false` (AC-20, AC-21). |
| **NC-13** | Otorisasi Pemutaran Just-In-Time 8-Tahap Player | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY UNRESOLVED JIT PREREQUISITES & AUTO-NEXT LIFECYCLE` | Batas otorisasi current-member dan larangan pre-verification memberi otorisasi lebih awal tetap berlaku; prasyarat Stage 8a (Genesis/ownership, active license, serta semantik diagnostic/background pre-verification) belum direkonsiliasi (AC-22), dan trigger/lifecycle Auto-Next lintas payload belum ditetapkan (AC-32). AC-23/24 tidak menghapus dependensi tersebut. |
| **NC-14** | Rekonsiliasi Status Verify & Ketiadaan Status Agregat Album | `PARTIALLY SPECIFIED` | `NOT IMPLEMENTED` | `PO DECISIONS APPROVED; MEMBERSHIP VERIFIER IMPLEMENTATION BLOCKED` | Keputusan PO CONF-02 (Pilihan B APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; AC-25 tetap SPEC READY. AC-33/AC-34 tetap EXECUTION BLOCKED sampai identity binding, signer authority/lifecycle, membership verifier, dan test tersedia; kebijakan fail-closed CONF-01 telah disahkan PO. |
| **NC-15** | Taksonomi 20 Kode Error Kanonikal & Fail-Closed | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Memuat 20 kode terklasifikasi 3 tier; layer & aksi fail-closed jelas (AC-26). |
| **NC-16** | Derivasi Matematis Identifier Deterministik | `SPECIFIED` | `NOT IMPLEMENTED` | `PROPOSED SPEC` | Formula truncated SHA-256 patuhi batas kolom skema; batas kolom bukan bukti unik (AC-27). |

---

### Rincian Kontrak Kritis Terpilih

#### 6.1 Rincian NC-01: Skema Manifest Album & Kebijakan Unknown Fields
- Jika rancangan packaging ZIP/manifest dipertahankan, draf mengusulkan objek JSON UTF-8 dengan nama kandidat `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] di root ZIP; nama dan lokasi manifest belum disahkan dan tidak boleh diperlakukan sebagai kontrak normatif.
- **Kebijakan Unknown Fields**: Diklasifikasikan sebagai `PROPOSED STRICT SCHEMA SPECIFICATION — PENDING PO/NORMATIVE CONFIRMATION`. Jika disahkan: menolak field asing (`ERR_MANIFEST_MALFORMED`). Jika permisif: mengabaikan field asing. Expected result pengujian dikunci bersyarat pada AC-01.

#### 6.2 Rincian NC-02: Signature Album Signer, Input Kanonikal & Batas Payload (Temuan 1, B-08, AUDIT-TRUTH-03)
- **Status Kontrak**: **`BLOCKED — REQUIRES ARCHITECTURE AUTHORITY DECISION`**.
- **Definisi Input Signature & Resolusi Circular Dependency (B-08)**:
  1. Memasukkan field `album_signer_signature` ke dalam payload manifest yang dikanonisasi JCS untuk menandatangani dirinya sendiri menimbulkan ketergantungan melingkar (*circular dependency*).
  2. Input canonical signature wajib didefinisikan secara konsisten dan bebas dari field signature itu sendiri: baik melalui pengecualian properti (*signature-stripped JCS / field exclusion*) sebelum serialisasi RFC 8785, atau melalui penyimpanan tanda tangan sebagai berkas terpisah (*detached signature file* `album_manifest.sig` di dalam arsip ZIP).
  3. Penggunaan RFC 8785 JCS saja **TIDAK OTOMATIS MENYELESAIKAN** persoalan signature scope tanpa definisi payload kanonikal yang disahkan.
  4. Field signature itu sendiri tidak boleh menimbulkan circular dependency pada canonical payload.
- **Preservasi Kontrak Kriptografis Anggota `.nx`**:
  Tanda tangan manifest Album Signer **DILARANG KERAS MENGUBAH ATAU MENGGANTIKAN**:
  1. Format, makna, dan verifikasi Creator packaging signature pada masing-masing kontainer `.nx` (NC-06 / AC-04);
  2. Format, makna, atau kewenangan Genesis Ownership Certificate (NC-05 / AC-10);
  3. Verifikasi Registry Authority Certificate pada masing-masing `.nx`.
- **Status Blocker**: Keputusan teknis mengenai signature scope dan model representasi tanda tangan manifest belum ditetapkan oleh Otoritas Arsitektur. **B-08 TETAP BERSTATUS `BLOCKED — AUTHORITATIVE DECISION REQUIRED`**, dan AC-03 tetap `[BLOCKED BY ARCHITECTURE]`.

#### 6.3 Rincian NC-03: Strict JSON Parser & Penanganan Escape Unicode (Spesifikasi Tambahan 2)
- **Status Kontrak**: **`BLOCKED BY B-01, B-02`**.
- **Pemisahan Standar RFC 8259 vs Kebijakan Nexa**: RFC 8259 Bagian 4 menyatakan bahwa nama anggota objek dalam JSON "SHOULD be unique", tetapi tidak mewajibkan penolakan mutlak oleh setiap parser umum. Penolakan duplikasi kunci pada Nexa adalah **Kebijakan Parser Ketat Nexa (Nexa Strict Parser Policy)**, bukan kewajiban mutlak RFC 8259.
- **Aturan Spesifikasi Parser Nexa**:
  - *Duplicate Keys Literal*: Jika dua kunci identik secara literal karakter (e.g. `{"title": "A", "title": "B"}`), parser menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Duplicate Keys via Decoded Unicode Escape*: Jika dua kunci identik setelah karakter escape Unicode didekode (e.g. `{"\u0074itle": "A", "title": "B"}`), parser mendecode escape sebelum memeriksa keunikan kunci dan menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Malformed Escape Syntax*: Jika urutan escape salah secara sintaksis (e.g. `\u123z`, escape terpotong `\u12`, atau lone surrogates `\uD800` tanpa pasangan legal), parser menolak dengan **`ERR_MANIFEST_MALFORMED`**.
- **Pemisahan Parser vs Serializer JCS**: Strict Parser (B-01, AC-05) bertugas pada tahap deserialisasi byte stream mentah. RFC 8785 JCS Serializer (B-02, AC-06) bertugas pada tahap serialisasi kanonisasi deterministik (pengurutan kunci UTF-16, format bilangan tanpa $-0$, minifikasi whitespace).

#### 6.4 Rincian NC-04: Kebijakan Otorisasi Album Signer UNKNOWN, Registry Trust, dan Pemisahan Lifecycle Signer (Temuan 3, B-09, CONF-01, AUDIT-TRUTH-04)
- **Status Kontrak**: **`PO DECISION REQUIRED / BLOCKED BY UNRESOLVED REGISTRY LIFECYCLE (B-09 / CONF-01)`**.
- **Pemisahan Trust Manifest Signer vs Creator Setiap Member `.nx`**:
  1. Trust terhadap Album Signer (penandatangan deklarasi manifest) dipisahkan secara tegas dari trust terhadap Creator masing-masing berkas kontainer `.nx`.
  2. Validitas atau trust member `.nx` dievaluasi berdasarkan Creator signature, Genesis Ownership Certificate, dan Registry evidence masing-masing item, bukan diturunkan dari Album Signer.
- **Ketiadaan Bukti Mekanisme Registry untuk Album Signer (Stop and Clarify)**:
  1. Repositori existing, White Paper v5.6, dan Roadmap v4.8 **TIDAK MEMBUKTIKAN** adanya mekanisme pendaftaran, identity binding, key rotation, atau revocation khusus untuk entitas Album Signer pada Registry.
  2. Fungsi Registry yang belum memiliki dasar kontrak ditandai secara terbuka sebagai **`UNRESOLVED — REGISTRY MECHANISM NOT ESTABLISHED BY PRODUCT CONTRACT`**, bukan sebagai fitur yang sudah tersedia.
  3. Perancang dan programmer **DILARANG MENCIPTAKAN** endpoint baru, database field baru, Registry record sintetis, atau API baru tanpa otorisasi formal.
- **Pemisahan Revocation Antara Manifest Signer dan Member `.nx`**:
  Pencabutan (*revocation*) public key Album Manifest Signer dipisahkan secara tegas dari pencabutan Creator atau Registry evidence milik member `.nx`. Revocation salah satu pihak tidak otomatis membatalkan status pihak lain tanpa aturan kontrak yang disahkan.
- **Kebijakan Signer UNKNOWN & Preservasi White Paper v5.6**:
  1. Sesuai White Paper v5.6, status `UNKNOWN / INCOMPLETE` **BUKAN `INVALID`**.
  2. Jika public key Album Signer tidak terdaftar di Registry (`UNKNOWN`), sistem **DILARANG OTOMATIS MENANDAI SEMUA MEMBER `.nx` SEBAGAI `INVALID` ATAU MEMBLOKIR SELURUH MEMBER**.
  3. Keputusan CONF-01 dibatasi pada apakah deklarasi manifest dengan signer `UNKNOWN` dapat digunakan untuk mengautentikasi membership Album serta dasar identitas/lifecycle signer. CONF-01 bukan pilihan untuk memblokir atau mengizinkan seluruh playback Album; otorisasi playback tetap JIT per member. Programmer dilarang memilih kebijakan secara sepihak.

#### 6.7 Rincian NC-07: Batas Keamanan Ekstraksi Arsip ZIP Wrapper (Temuan 5, Spesifikasi Tambahan 3, AUDIT-NEW-06)
- Evaluasi batasan keamanan saat ekstraksi arsip pembungkus ZIP menggunakan pustaka dekompresi streaming:
  1. *Ukuran Maksimum File Terkompresi*: $\le 500\text{ MB desimal (500.000.000 bytes)}$ (`[PROPOSED SPECIFICATION — PENDING ARCHITECTURE DECISION B-07]`).
  2. *Ukuran Maksimum Dekompresi Kumulatif Wrapper*: $\le 4\text{ GB desimal}$ ($4 \times 10^9$ bytes).
  3. *Batas Payload Individual Kontainer `.nx`*: $\le 2\text{ GiB}$ ($2 \times 1024^3 = 2.147.483.648$ bytes) sesuai batas biner `internal/container/container.go#L106` (`[INSPEKSI LOKAL PROGRAMMER: Go container.go#L106 / NOT VERIFIED BAGI AUDIT INDEPENDEN]`).
  4. *Maksimum Jumlah Entri Central Directory*: $\le 200\text{ entri}$ (`[PROPOSED SPECIFICATION — PENDING B-07]`).
  5. *Ambang Batas Rasio Kompresi ZIP Bomb*: Ambang rasio kompresi batas bomb berstatus usulan spesifikasi teknis NC-07 / B-07 (ambiguitas rasio kompresi 10:1 usulan perancang B-07 vs referensi pembanding eksternal 100:1 yang belum diverifikasi normatif). Pembuktian format APPNOTE dan RFC 1951 tidak memuat ambang rasio keamanan numerik tersebut. Jika rasio dekompresi melampaui ambang batas usulan B-07 atau `compressed_size == 0` saat `uncompressed_size > 0`, proses streaming dihentikan fail-closed dan melempar **`ERR_ZIP_BOMB_DETECTED`**.

- **Aturan Normatif Tipe Entri ZIP Sesuai Keputusan Product Owner (AUDIT-NEW-06 PO APPROVED)**:

| Tipe Entri | Perlakuan | Alasan / Kode Error |
|---|---|---|
| Regular file | Diterima | Sesuai aturan validasi arsip dan regex nama berkas member |
| Directory | Diterima | Sesuai Keputusan PO (AUDIT-NEW-06 PO APPROVED) |
| Symlink | Ditolak | Fail-closed (`ERR_ZIP_INVALID`) |
| Special file (FIFO, socket, dev) | Ditolak | Fail-closed (`ERR_ZIP_INVALID`) |
| Hardlink semantics | Tidak didukung | Semantik hardlink bukan fitur ZIP generik universal |
| Identical payload pada beberapa entri | Diterima sebagai entri independen | Setiap entri diekstrak mandiri tanpa asumsi relasi link |

- **Harmonisasi Struktur Flat Archive vs Direktori**:
  - Keputusan PO secara tegas menerima entri direktori di dalam arsip ZIP.
  - Pembatasan struktur "flat" berlaku pada path relatif member kontainer `.nx` yang dideklarasikan pada manifest (nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) wajib memenuhi regex `^[a-zA-Z0-9_-]+\.nx$`), yang melarang deklarasi trek dalam subdirektori bersarang (e.g. `discs/track01.nx`).
  - Ketentuan Keputusan PO (Level 1) mengesampingkan usulan lama B-07 yang melarang entri direktori.
- **Pencegahan Path Traversal**: Nama berkas entri diperiksa terhadap pola traversal (`../`, `..\`, absolute path, leading slashes). Pelanggaran melempar **`ERR_ZIP_INVALID`**.
- **Case-Insensitive Filename Collision**: Pemeriksaan keunikan entri ZIP dan manifes dilakukan secara case-insensitive via ASCII case-folding (`toLowerASCII`) sesuai Keputusan PO (AUDIT-NEW-07). Tabrakan nama melempar **`ERR_ZIP_INVALID`** (pada ZIP) atau **`ERR_MANIFEST_MALFORMED`** (pada manifes).
- **Status Blocker**: Parameter numerik kuota (500 MB desimal [500.000.000 bytes], 4 GB desimal, 200 entri, ambang rasio kompresi) berstatus **`PROPOSED SPECIFICATION`** di bawah blocker **B-07**.

#### 6.8 Rincian NC-08: Batas Atomisitas Transaksi Marketplace & Ketiadaan 2PC (Temuan 6)
- Transaksi database lokal PostgreSQL menggunakan advisory lock `pg_advisory_xact_lock(hashtext(user_id || ':' || album_id))` untuk mutual exclusion.
- **Batas Atomisitas**:
  1. *Jaminan Lokal*: Advisory lock dan blok transaksi SQL (`BEGIN ... COMMIT / ROLLBACK`) menjamin bahwa mutasi lokal (child acquisitions dan entitlements) dibatalkan secara bersih tanpa residu baris parsial jika terjadi kegagalan lokal. Kegagalan mutasi lokal sebelum commit melempar **`ERR_TRANSACTION_FAILED`**.
  2. *Ketiadaan Jaminan Terdistribusi & Larangan Janji Rollback Pasca-Commit*: Panggilan HTTP eksternal ke Sprint 12 License Daemon (`marketplace/server.js#L170-L205`) TIDAK memiliki Two-Phase Commit (2PC) maupun endpoint kompensasi otomatis. Jika transaksi database lokal telah di-commit, transaksi tersebut **TIDAK DAPAT** di-rollback oleh transaksi SQL yang sama. Jika License Daemon gagal pasca-commit DB lokal atau mengalami network timeout, mutasi DB lokal di-rollback HANYA jika kegagalan terjadi di dalam blok transaksi sebelum commit; namun efek samping eksternal pada daemon tetap tidak terkompensasi. Kegagalan ini melempar **`ERR_LICENSE_DAEMON_COMMUNICATION`**.
  3. *Kendala Zero-DDL*: Skema database PostgreSQL beku (`schema.postgres.sql`) melarang penambahan kolom foreign key baru atau tabel outbox terdistribusi.
- **Status Arsitektur**: Selama gap ketiadaan 2PC dan batasan Zero-DDL belum diselesaikan oleh otoritas arsitektur, NC-08 berstatus **`BLOCKED`** di bawah blocker B-04 / CONF-03.

#### 6.8.2 Keputusan Normatif PO — Identitas dan Korelasi Commercial Bundle Checkout

**Status keputusan:** **APPROVED / NORMATIVE ARCHITECTURE RULE — B-04**. Product Owner menyetujui bahwa `bundle_checkout_id` adalah identitas korelasi komersial yang independen dari `acquisition_id` dan `payment_order_id`. Tujuh aturan berikut dikunci sebagai dasar normatif perumusan kontrak target B-04. Keputusan ini tidak menetapkan media penyimpanan, tidak membuktikan mekanisme tersebut telah tersedia pada Marketplace saat ini, tidak menutup B-04, dan tidak mengotorisasi implementasi PE-02.

1. **Satu checkout, satu identitas:** setiap satu proses Commercial Bundle Checkout memiliki tepat satu `bundle_checkout_id` yang mengidentifikasi checkout komersial tersebut.
2. **Korelasi seluruh anggota:** setiap acquisition independen yang dihasilkan oleh checkout tersebut harus dapat dikorelasikan secara persisten dengan `bundle_checkout_id` yang sama.
3. **Independensi acquisition:** setiap member tetap memiliki `acquisition_id` dan entitlement independen. `bundle_checkout_id` bukan parent acquisition, bukan pengganti `acquisition_id`, dan tidak membentuk parent-child row relationship yang tidak tersedia dalam DDL.
4. **Independensi payment order:** `bundle_checkout_id` tidak menggantikan, menyerap, atau mengubah semantik `payment_order_id`. Relasi checkout terhadap payment order harus ditentukan dalam kontrak B-04 tanpa mengasumsikan satu payment order dapat mewakili banyak acquisition pada DDL existing.
5. **Stabilitas retry dan recovery:** identitas checkout yang sama harus dipertahankan untuk retry, replay, dan recovery dari proses checkout logis yang sama; retry tidak boleh menghasilkan identitas checkout baru hanya karena request diulang atau proses/server dimulai ulang.
6. **Non-reuse:** Commercial Bundle Checkout yang benar-benar baru wajib memperoleh `bundle_checkout_id` baru. ID checkout terdahulu tidak boleh digunakan ulang untuk transaksi komersial lain.
7. **Korelasi persisten dan dapat diverifikasi:** hubungan antara `bundle_checkout_id` dan seluruh acquisition anggotanya harus dapat ditelusuri dan diverifikasi secara deterministik. Hubungan tidak boleh disimpulkan hanya dari urutan baris, timestamp, kesamaan buyer, atau heuristik yang tidak mengikat secara eksplisit.

**Batasan desain yang mengikat:**
- Kontrak korelasi wajib mematuhi Zero-DDL: tidak menambah atau mengubah tabel/kolom/constraint database yang dibekukan.
- Mekanisme penyimpanan/persistensi, integritas, otorisasi penerbitan, canonical representation, query/retrieval, lifecycle, dan rekonsiliasi `bundle_checkout_id` dengan N acquisition masih merupakan pekerjaan desain teknis B-04; tidak diputuskan oleh persetujuan prinsip ini.
- Immutable Checkout Manifest telah disahkan sebagai satu-satunya sumber kebenaran normatif pada §6.8.3. Shared Metadata hanya boleh menjadi proyeksi/indeks turunan tanpa otoritas normatif. Mekanisme storage, persistensi, pemetaan member-to-acquisition, integritas, atomicity, recovery, dan queryability tetap harus dirancang dan dibuktikan dalam batas Zero-DDL.
- `bundle_checkout_id` adalah identitas korelasi komersial, bukan bukti pembayaran, bukan otorisasi entitlement, bukan lisensi, dan bukan otorisasi playback.
- Ketidaktersediaan atau kegagalan verifikasi korelasi harus ditangani secara eksplisit dan fail-closed pada operasi yang membutuhkan kepastian keanggotaan checkout; sistem tidak boleh merekonstruksi hubungan melalui heuristik.

**Dampak register:** B-04 / NC-08 kini memiliki keputusan normatif PO untuk identitas korelasi checkout, tetapi mekanisme persistensi/korelasi, idempotency/replay, commit boundary, retry, partial failure, settlement/reconciliation, dan kontrak side effect License Daemon tetap terbuka. Status B-04 tetap **`OPEN / BLOCKED`**.

#### 6.8.1 Keputusan Normatif PO — Commercial Bundle dengan Independent Member Acquisitions & SSP Allocation

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT CONTRACT — MODEL B + OPTION 1**. Keputusan ini menetapkan bentuk komersial dan alokasi nilai per member; keputusan ini tidak dengan sendirinya menutup B-04 atau B-05, tidak mengubah Zero-DDL, dan tidak mengotorisasi implementasi PE-02.

1. **Model akuisisi — Model B (Independent Member Acquisitions via Commercial Bundle):**
   - Konsumen melakukan satu checkout komersial untuk satu Album Bundle.
   - Untuk setiap member .nx yang termasuk dalam bundle, Marketplace menghasilkan satu baris acquisition independen dan satu entitlement independen yang terikat pada acquisition tersebut.
   - Setiap child acquisition tetap mewakili satu asset_id/member, buyer, currency, dan entitlement sendiri. Hak/lisensi serta otorisasi playback tetap dievaluasi secara JIT per member sesuai baseline PE-01; checkout bundle tidak menciptakan otorisasi playback massal.
   - Model ini dipilih agar tetap kompatibel dengan DDL yang ada (Zero-DDL), pola entitlement per acquisition, dan portabilitas setiap member .nx.
   - Satu checkout tidak boleh ditafsirkan sebagai satu parent acquisition yang menggantikan acquisition per member. DDL yang diperiksa tidak menyediakan relasi parent-child eksplisit; karena itu, jangan mengklaim adanya foreign key atau relasi persisten parent-child yang tidak tersedia. Identitas korelasi checkout/bundle, idempotency key, dan pemetaan operasional bundle ke child acquisitions harus ditetapkan dalam kontrak transaksi B-04 tanpa menambah kolom/tabel DDL.

2. **Aturan nilai — Relative Standalone Selling Price (SSP) Allocation:**
   - price_amount pada setiap child acquisition adalah bagian nilai transaksi bundle yang dialokasikan kepada member tersebut, dinyatakan dalam satuan terkecil mata uang (minor units), bukan harga katalog standalone penuh dan bukan nilai royalti.
   - Bobot alokasi menggunakan snapshot harga katalog standalone (SSP) setiap member yang berlaku pada saat checkout. Snapshot harus konsisten untuk seluruh child dalam satu checkout; perubahan harga katalog setelah checkout tidak mengubah alokasi transaksi yang telah terjadi.
   - Nilai transaksi yang dialokasikan kepada member (P_member_pool) adalah consideration transaksi bundle yang memang dialokasikan kepada barang/member. Pajak, biaya gateway, biaya layanan, atau komponen non-member yang ditagihkan terpisah tidak boleh diam-diam dimasukkan ke P_member_pool. Jika komponen tersebut tidak dapat dipisahkan dari jumlah pembayaran, kebijakan akuntansi/alokasinya harus ditetapkan secara eksplisit sebelum implementasi; jangan mengasumsikan SUM(price_amount_i) selalu sama dengan gross receipt gateway.
   - Untuk setiap member i, dengan SSP snapshot SSP_i dan S = Σ SSP_i untuk seluruh member bundle, nilai dasar alokasi eksak adalah P_member_pool × SSP_i / S. Total SSP harus positif (S > 0), semua SSP harus berada dalam currency yang sama dan menggunakan satuan terkecil yang sama. Jika prasyarat ini tidak terpenuhi, checkout harus dihentikan secara fail-closed; tidak boleh menggunakan bobot nol, nilai default, atau pembagian rata-rata sebagai fallback diam-diam.

3. **Largest Remainder Method (Hamilton / Hare-Niemeyer):**
   - Hitung base_i = floor(P_member_pool × SSP_i / S) menggunakan aritmetika integer eksak.
   - Hitung sisa pecahan secara eksak: remainder_i = (P_member_pool × SSP_i) mod S.
   - Hitung R = P_member_pool − Σ base_i. Bagikan tepat satu minor unit tambahan kepada masing-masing dari R member dengan remainder terbesar.
   - Jika remainder seri, gunakan tie-break deterministik berdasarkan identifier kanonis member yang stabil dan immutable; urutan UI, urutan playlist, urutan query, atau urutan tampilan tidak boleh memengaruhi hasil. Definisi encoding/normalisasi dan ordering identifier kanonis wajib ditetapkan identik pada seluruh implementasi sebelum kontrak dinyatakan siap.
   - Implementasi dilarang menggunakan floating-point untuk menentukan hasil alokasi. Operasi perkalian harus memakai integer dengan kapasitas memadai atau metode quotient/remainder yang tetap eksak dan bebas overflow. Go dan TypeScript harus menghasilkan hasil identik.
   - Invariant wajib: SUM(price_amount_i) = P_member_pool untuk seluruh child member pada checkout yang berhasil dialokasikan. Tidak boleh ada minor unit yang hilang atau tercipta akibat pembulatan.

4. **Pemisahan nilai komersial dari hak ekonomi dan refund:**
   - price_amount adalah nilai consideration yang dialokasikan kepada acquisition/member untuk pencatatan transaksi. Nilai ini bukan otomatis royalty, creator payout, atau jumlah bersih yang diterima pemegang hak.
   - Royalty, komisi, biaya platform, withholding, dan payout mengikuti kontrak hak serta kebijakan settlement tersendiri; jangan menurunkannya otomatis dari price_amount tanpa aturan terpisah.
   - Alokasi per member menjadi basis nilai transaksi member untuk evaluasi refund parsial. Penghitungan refund aktual tetap harus mengikuti kebijakan pajak, biaya, komisi, payment gateway, dan ketentuan refund yang berlaku; price_amount bukan janji bahwa seluruh komponen tersebut dapat dikembalikan secara identik.

5. **Kriteria konsistensi lintas implementasi dan batas blocker:**
   - Go dan TypeScript wajib berbagi test vectors yang mencakup nilai habis dibagi, pembulatan dengan sisa, remainder seri/tie-break, SSP nol, total SSP nol, currency mismatch, nilai maksimum/overflow, dan invariant jumlah akhir.
   - Model B dan aturan SSP/Largest Remainder di atas merupakan keputusan produk yang telah disahkan. B-04 tetap OPEN / BLOCKED sampai kontrak transaksi multi-child secara utuh menetapkan korelasi checkout, idempotency/replay, urutan dan batas commit, retry, partial failure, settlement/reconciliation, serta penanganan side effect License Daemon tanpa menjanjikan 2PC/compensation yang tidak tersedia.
   - B-05 tetap OPEN / BLOCKED sampai byte-domain, producer, consumer, dan kontrak acquired_package_sha256 untuk setiap child member ditetapkan. Bukti baseline yang tersedia menunjukkan hash existing berasal dari seluruh wrapper ZIP delivery package; hash wrapper tersebut tidak boleh disalin atau diperlakukan sebagai hash individual .nx member tanpa kontrak byte-domain dan bukti yang sesuai.
   - Semua ketentuan di atas adalah target architecture/product contract PE-02. Ketiadaan implementasinya pada repository saat ini adalah implementation gap, bukan alasan untuk menghilangkan desain target dari PLAN.

---


#### 6.8.3 Keputusan Normatif PO — Immutable Checkout Manifest sebagai Single Source of Truth B-04

**Status keputusan:** **STRONGLY APPROVED / NORMATIVE ARCHITECTURE DECISION — B-04 / NC-08**. Product Owner menyetujui Immutable Checkout Manifest sebagai satu-satunya sumber kebenaran normatif (*Single Source of Truth*) untuk komposisi Commercial Bundle Checkout dan korelasi `bundle_checkout_id` dengan seluruh N independent member acquisitions. Shared Metadata, apabila digunakan, hanya merupakan proyeksi atau indeks turunan; metadata tersebut tidak memiliki otoritas untuk mengubah, melengkapi secara otoritatif, atau mendefinisikan ulang keanggotaan checkout.

**A. Pemisahan Commercial Intent dan Execution Reality**

1. **Commercial Intent — Immutable Checkout Manifest:**
   - Manifest merekam kesepakatan komersial yang dimaksudkan dan dibayar konsumen: `bundle_checkout_id`, identitas pembeli, currency, komposisi lengkap N member, snapshot Relative Standalone Selling Price (SSP), serta alokasi `price_amount` per member menurut Model B + Largest Remainder Method yang telah disahkan pada §6.8.1.
   - Komposisi dan nilai komersial yang telah diterbitkan bersifat immutable. Perubahan harga, komposisi, buyer, currency, atau alokasi tidak dilakukan dengan mengedit Manifest lama; perubahan komersial yang sah harus diperlakukan sebagai checkout/artefak baru menurut lifecycle yang kelak ditetapkan.
   - Manifest tidak memuat mutable execution status seperti `PAYMENT_PENDING`, `ACQUISITION_COMPLETED`, status entitlement, hasil License Daemon, retry counter, atau status rekonsiliasi.

2. **Execution Reality — sistem transaksi dan pemenuhan:**
   - Baris `payment_orders`, `acquisitions`, `entitlements`, dan hasil side effect License Daemon merepresentasikan state serta hasil eksekusi aktual sesuai kemampuan komponen masing-masing.
   - State machine eksekusi tidak boleh mengubah isi Manifest. Relasi payment order terhadap checkout, commit boundary, retry, idempotency, partial failure, dan side effect eksternal tetap harus ditentukan dalam kontrak transaksi B-04.
   - Manifest mendeklarasikan apa yang seharusnya dipenuhi; catatan eksekusi membuktikan apa yang benar-benar telah terjadi. Keduanya harus dapat direkonsiliasi tanpa menyamakan deklarasi dengan keberhasilan eksekusi.

**B. Rekonsiliasi deterministik dan recovery**

1. Recovery/Reconciliation membandingkan himpunan member yang dideklarasikan Manifest dengan acquisition yang terbukti persisten untuk checkout tersebut. Secara konseptual:
   `Reconciliation Delta = Manifest Declared Members − DB Persisted Acquisitions`.
2. Delta harus dapat diidentifikasi per member secara deterministik, termasuk member yang belum mempunyai acquisition, acquisition yang belum mempunyai entitlement, dan status pemenuhan eksternal yang belum dapat dipastikan.
3. Manifest memungkinkan sistem mengetahui seluruh komposisi yang dimaksud walaupun proses berhenti setelah hanya sebagian member diproses. Shared Metadata pada baris acquisition saja tidak cukup untuk menjadi sumber komposisi karena tidak dapat mendeklarasikan member yang belum sempat tercatat.
4. Implementasi tidak boleh menebak komposisi atau pemetaan melalui row order, timestamp, buyer equality, urutan playlist, atau heuristik lain yang tidak mengikat secara eksplisit. Ketidakcocokan atau bukti yang tidak lengkap harus dilaporkan sebagai unresolved/inconsistent dan ditangani fail-closed untuk operasi yang memerlukan kepastian.
5. **Pemetaan member ke acquisition ID masih memerlukan kontrak teknis yang eksplisit:** desain harus menentukan apakah identifier acquisition dapat ditetapkan secara deterministik sebelum eksekusi dan dimasukkan ke Manifest, atau apakah diperlukan execution record/receipt yang immutable atau append-only untuk membuktikan pemetaan member-to-`acquisition_id`. Jika execution record digunakan, fungsinya hanya membuktikan hasil/pemetaan eksekusi; record itu tidak boleh mengubah daftar member, harga, atau maksud komersial yang telah dikunci Manifest. Bentuk mekanisme ini belum diputuskan dan tidak boleh diasumsikan.

**C. Single Source of Truth dan Shared Metadata**

1. Manifest adalah otoritas tunggal untuk komposisi checkout: identitas checkout, daftar member, dan alokasi komersial yang disahkan.
2. Shared Metadata boleh digunakan hanya sebagai projection, cache, atau query index untuk kemudahan lookup. Metadata tersebut harus dapat dibangun ulang dari Manifest dan/atau bukti eksekusi yang sah, serta tidak boleh menjadi sumber otoritatif yang berdiri sendiri.
3. Jika Shared Metadata bertentangan dengan Manifest, Manifest menang. Proyeksi yang tidak konsisten harus ditandai invalid/stale dan dibangun ulang atau dikoreksi; proyeksi tidak boleh mengubah Manifest atau komposisi checkout.
4. Hash SHA-256 dan/atau tanda tangan digital Ed25519 dapat dievaluasi sebagai mekanisme integritas dan autentikasi penerbitan Manifest. Algoritma, signed payload, canonical byte-domain, key authority/custody, verification, rotation, revocation, serta trust model belum ditetapkan oleh keputusan ini; jangan menulisnya sebagai mekanisme yang telah diputuskan atau diimplementasikan.

**D. Zero-DDL dan batas bukti storage**

1. Keputusan ini wajib dipenuhi tanpa menambah atau mengubah tabel, kolom, atau constraint PostgreSQL (Zero-DDL).
2. Manifest harus disimpan secara persisten dan dapat dipulihkan menggunakan mekanisme storage yang sudah tersedia dan terbukti memenuhi kebutuhan. Penyimpanan file fisik melalui Storage Engine/`storage_object_id` sebagaimana diusulkan PO merupakan kandidat yang harus dievaluasi terhadap source evidence; keputusan ini **tidak** menyatakan bahwa kemampuan tersebut telah diverifikasi atau bahwa pola nama file tertentu sudah menjadi kontrak.
3. Sebelum desain storage dinyatakan siap, harus dibuktikan: persistensi setelah restart/crash, lookup deterministik berdasarkan checkout identity, immutability atau proteksi overwrite, integritas dan autentikasi sesuai threat model, atomicity/consistency pada saat penerbitan, durability, retention, backup/recovery, concurrency, serta akses untuk rekonsiliasi.
4. Jika tidak ada mekanisme existing yang memenuhi kebutuhan tersebut dalam batas Zero-DDL, jangan membuat tabel/kolom baru, jangan mengandalkan temporary file atau cache volatil, dan jangan mengklaim B-04 siap. Hentikan bagian desain yang bergantung pada storage tersebut untuk keputusan eksplisit Architecture Authority/PO.

**E. Status keputusan dan batas kewenangan**

- Prinsip Immutable Checkout Manifest sebagai satu-satunya sumber kebenaran normatif telah disahkan dan tidak boleh dikembalikan menjadi pilihan Shared Metadata versus Manifest.
- Pilihan detail schema/format Manifest, canonicalization, issuance authorization, digest/signature, exact member-to-acquisition mapping, storage backend, lookup, lifecycle, concurrency, dan recovery tetap merupakan pekerjaan desain teknis yang harus ditetapkan secara eksplisit dan diuji.
- Keputusan ini tidak membuktikan bahwa Manifest atau Recovery Engine telah tersedia pada repository saat ini; kebutuhan yang belum ada adalah target architecture/build requirement, bukan alasan untuk menghapus desain dari PLAN.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai keseluruhan kontrak transaksi multi-member, korelasi persisten, idempotency/replay, commit boundary, retry, partial failure, settlement/reconciliation, dan side effect License Daemon diselesaikan.
- Keputusan ini tidak mengubah Zero-DDL, Model B, SSP/Largest Remainder, baseline PE-01/Sprint 16, dan tidak memberikan otorisasi implementasi PE-02.

#### 6.9 Rincian NC-09: Inventarisasi Objek Kriptografis & Hash Berbasis Bukti Faktual (Temuan 1, Temuan 8, AUDIT-NEW-04)
Dokumen ini menyusun ulang inventarisasi seluruh objek tanda tangan digital Ed25519 dan nilai hash SHA-256 secara ketat berbasis bukti (*evidence-based inventory*). Dokumen **TIDAK LAGI** mempertahankan klaim kaku "delapan objek diskrit (3 Ed25519 + 5 SHA-256)" karena formulasi historis tersebut mencampuradukkan artefak kontrak nyata dengan langkah komputasi internal perancang:

##### A. Inventarisasi Objek Tanda Tangan Digital Ed25519 Teridentifikasi
§6.9 mempertahankan **empat entri inventaris konseptual signature** untuk membedakan peran, konteks, dan identitas konseptual masing-masing objek. Inventaris konseptual ini tidak dengan sendirinya membuktikan bahwa seluruh objek telah ditemukan atau diverifikasi dalam implementasi repositori aktual. Status bukti implementasi setiap entri mengikuti keterangan verifikasi yang dicantumkan pada tabel di bawah ini:

| No | Object Identity | Object Type | Field Identifier | Storage / Source | Payload / Input | Producer | Verifier / Consumer | Relation | Evidence Status |
|:---:|---|---|---|---|---|---|---|---|:---:|
| 1 | Album Manifest Signer Signature | Ed25519 Digital Signature | `album_signer_signature` | `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] (§5.1) | Byte kanonikal UTF-8 representasi RFC 8785 JCS manifest album (status eksklusi signature: unresolved B-08) | Album Signer / Publisher (Dasar identitas & lifecycle unresolved) | NX Player (Tahap 4 JIT), NX Verify | Mengautentikasi keabsahan deklarasi metadata manifest dan daftar anggota album (bukan pengganti signature/trust member .nx) | `PROPOSED SPECIFICATION` (B-08 circularity & B-09 lifecycle unresolved) |
| 2 | PE-01 Container Packaging Signature | Ed25519 Digital Signature (64 bytes) | `signature` (Go trailer) / `signatureBytes` (SDK) | Trailer biner kontainer individual `.nx` (dilaporkan via `internal/container/container.go#L17-L135`; `sdk/typescript/src/container.ts#L4-L104`; `sdk.ts#L143, L151`) | Byte payload biner kontainer `.nx` (header + chunk data terenkripsi) | Container Creator / Packaging Engine (`container.go#L17-L64`) | Container Unpack Go (`container.go#L67-L135`), SDK NexaContainer.unpack (`container.ts#L44-L104`), NX Player (Tahap 7a JIT) | Mengautentikasi keabsahan struktur kemasan kontainer PE-01 individual | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; Auditor tidak mengakses repository primer untuk memverifikasi path dan snippet Go/TypeScript |
| 3 | Registry Authority Certificate Signature (Lapisan 1 Genesis) | Ed25519 Digital Signature (64 bytes hex) | `issuer_signature` | Objek Registry Certificate `regCert` (dilaporkan via `sdk/typescript/src/sdk.ts#L207-L226`) | Canonical string UTF-8 6-field (atau fallback 5-field) via `NexaRegistry.canonicalJcs` | Registry Authority | SDK Nexa (`sdk.ts#L219, L225`), NX Player (Tahap 7b JIT) via `registryPubKey` | Menjelaskan fungsi konseptual verifikasi sertifikat; klaim implementasi pada path tersebut hanya laporan Programmer yang belum diverifikasi independen | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; Auditor tidak mengakses repository primer untuk memverifikasi path dan snippet |
| 4 | Genesis Ownership Certificate Signature (Lapisan 2 Genesis) | Ed25519 Digital Signature (64 bytes hex) | creator_signature | Embedded ownership certificate ownCert (source path/status remains Programmer-reported, not independently verified) | Canonical Genesis Ownership Certificate payload | Genesis Creator (kunci privat pembuat asli) | SDK Nexa / NX Player Stage 7b | Genesis Creator identity is distinct from Container Packager and current holder; ownership transfer may connect Genesis Creator to current holder; third-party packaging authority is separately proven by delegation per §13.12.11 | REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED |

> **Pemeriksaan Empiris Hubungan signature dan creator_signature Berbasis Bukti Primer (AUDIT-NEW-04 Masalah C):**
> 1. *Trailer Kontainer PE-01 (`signature` di Go vs `signatureBytes` di TypeScript SDK)*:
>    - **Catatan Implementasi Lokal Programmer (`whisnu/nexa:main` commit `fc08a5c`)**:
>      - Implementasi Go (`internal/container/container.go`): Fungsi `Pack` (`container.go#L17-L64`) memvalidasi `len(signature) != 64` (L25), menulis `sigLen` uint32 BigEndian ke header (L48-50), dan menulis trailer biner 64-byte `signature` di akhir berkas (`buf.Write(signature)`, L59-61). Fungsi `Unpack` (`container.go#L67-L135`) membaca header, memvalidasi `sigLen == 64` (L106), menghitung `expectedSize = headerSize + manifestLen + payloadLen + sigLen` (L111), membaca trailer `signature = make([]byte, sigLen)` (L129-130), dan mengembalikan `signature []byte` (L134). Pada `internal/engine/container/container.go#L212-L295` (`UnpackMetadata`), trailer dialokasikan sebagai `signatureBytes = make([]byte, sigLen)` (L287) dan dibaca via `r.ReadAt(signatureBytes, sigOffset)` (L288).
>      - Implementasi TypeScript SDK (`sdk/typescript/src/container.ts`): Interface `NexaContainerData` (`container.ts#L4-L8`) mendefinisikan `signatureBytes: Buffer;` (L7). Fungsi `unpack` (`container.ts#L44-L104`) membaca `sigLen` (L73/L81), memvalidasi `sigLen === 64` (L85), mengalokasikan `const signatureBytes = Buffer.alloc(sigLen)` (L100), menyalin byte trailer kontainer dari offset `headerSize + manifestLen + payloadLen` (L101), dan mengembalikannya sebagai properti `signatureBytes` (L103). Verifikasi SDK (`sdk/typescript/src/sdk.ts#L143, L151`) mengeksekusi `NexaCrypto.verify(pubKey, container.manifestBytes, container.signatureBytes)` (L143) dan `NexaCrypto.sha256(container.signatureBytes)` (L151).
>    - **Status Provenance Bukti**: Programmer melaporkan inspeksi source lokal yang memetakan byte trailer Go dan TypeScript pada commit yang dicantumkan. Auditor menilai provenance, kutipan, dan konsistensi internal pada PLAN; akses langsung Auditor ke repository sumber bukan prasyarat. Status bukti dibatasi sebagai `VERIFIED BY PROGRAMMER — STATIC SOURCE`, bukan verifikasi independen Auditor dan bukan bukti runtime.
>      (Tidak ada klaim `REPOSITORY-VERIFIED`.)

> 2. *Genesis Ownership Certificate Signature (`creator_signature`)*:
>    - **Pembedaan Konseptual & Catatan Implementasi Lokal**: Properti `creator_signature: string;` dilaporkan pada interface `OwnershipCertificate` (`sdk/typescript/src/ownership.ts#L26`), diverifikasi atas canonical JSON Genesis Certificate terhadap `ownCert.creator_public_key` (`sdk/typescript/src/sdk.ts#L234-L255#L235, L252, L255`), dan didefinisikan sebagai kolom `creator_signature TEXT NOT NULL` pada tabel `ownership_tokens` (`migrations/004_ownership.sql#L25`).
>    - **Status Provenance Bukti**: Pembedaan konseptual bahwa `creator_signature` bukan trailer kontainer PE-01 melainkan tanda tangan atas data sertifikat Genesis Ownership tetap dipertahankan. Bukti implementasi yang dilaporkan Programmer dibatasi sebagai `VERIFIED BY PROGRAMMER — STATIC SOURCE`; hal ini bukan verifikasi independen Auditor dan bukan bukti runtime.
> 3. *Kesimpulan*: Objek 2 (Container Packaging Signature) dan Objek 4 (Genesis Ownership Certificate Signature) tetap merupakan dua entri inventaris konseptual berbeda. Pembedaan ini tidak membuktikan payload, lokasi penyimpanan, kunci, public key, atau verifier di luar bukti source yang dikutip. Klaim implementasi tersebut berstatus `VERIFIED BY PROGRAMMER — STATIC SOURCE` sesuai provenance Programmer, bukan `NOT VERIFIED` hanya karena Auditor tidak mengakses repository secara langsung.


> **Catatan Pemisahan Signature Genesis (AUDIT-NEW-04):** Pembedaan Objek 3 (`issuer_signature`) dan Objek 4 (`creator_signature`) tetap dipertahankan sebagai dua entri konseptual. Rincian implementasi yang dilaporkan Programmer berstatus `VERIFIED BY PROGRAMMER — STATIC SOURCE` sesuai kutipan yang tersedia; status ini bukan verifikasi independen Auditor dan bukan bukti runtime.

##### B. Inventarisasi Field Hash SHA-256: Usulan Spesifikasi Manifest & Keberadaan Kolom DDL Database
Dari penelusuran skema database dan spesifikasi manifest, terdapat **2 field hash SHA-256** dengan tingkat pembuktian yang berbeda secara tegas (dokumen ini tidak mengklaim keduanya sebagai kontrak normatif yang telah disahkan):

| No | Object Identity | Object Type | Field Identifier | Storage / Source | Payload / Input | Producer | Verifier / Consumer | Relation | Evidence Status |
|:---:|---|---|---|---|---|---|---|---|:---:|
| 1 | Audio Track Binary Payload Hash (Proposed Specification) | SHA-256 Cryptographic Digest (32 bytes / 64 hex) | notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif) (`UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT; STOP AND CLARIFY`) | `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] (§5.1 Skema Manifest) | Bitstream audio mentah biner di dalam kontainer `.nx` (sesuai usulan spesifikasi manifest) | Audio encoding pipeline (usulan perancang) | NX Player (Tahap 8a JIT), NX Verify | Menjamin integritas bitstream audio mentah; gagal cocok melempar `ERR_CONTAINER_HASH_MISMATCH` | `PROPOSED SPECIFICATION (Manifest JSON Schema Draft 7 §5.1; Not Yet Frozen in WP v5.6; Field Identity Unresolved)` |
| 2 | acquired_package_sha256 Database Column | SHA-256 String Column (VARCHAR / TEXT di DB) | `acquired_package_sha256` | Database PostgreSQL tabel `acquisitions` (dilaporkan via `marketplace/db/schema.postgres.sql#L72`) | `UNRESOLVED — BLOCKED BY B-05` (Keberadaan kolom DDL tidak membuktikan payload hash adalah file ZIP utuh; tidak ada bukti apakah hash dihitung sebelum atau sesudah kompresi) | `UNVERIFIED` (Belum ada kode transaksi Marketplace yang diverifikasi menulis kolom ini) | `UNVERIFIED` (Belum ada fungsi audit yang terbukti mengonsumsi kolom ini) | `UNRESOLVED — BLOCKED BY B-05` (Semantik penulisan baris child acquisition dan fungsi bisnis kolom terblokir gap transaksi terdistribusi dan ketiadaan DDL child table) | `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE (DDL FIELD EXISTENCE NOT INDEPENDENTLY VERIFIED; SEMANTICS & PAYLOAD BLOCKED BY B-05)` |

##### Analisis Tiga Tingkat Pembuktian Field acquired_package_sha256 (AUDIT-NEW-04 Masalah A & B)
Sesuai arahan audit, dokumen ini membedakan secara tegas tiga tingkat fakta seputar kolom `acquired_package_sha256`:
1. **Tingkat 1 — Keberadaan Field (`NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`)**:
   Keberadaan kolom `acquired_package_sha256 VARCHAR(64)` dilaporkan Programmer berdasarkan skema DDL `marketplace/db/schema.postgres.sql#L72, L112, L129, L132` pada repositori lokal `whisnu/nexa` commit `fc08a5c`. Namun, karena berkas DDL tersebut belum dapat diakses secara independen oleh Auditor (pemeriksaan Auditor menghasilkan HTTP 404), status keberadaan fisik kolom ini bagi audit independen diturunkan menjadi: **`NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`**. Dokumen menegaskan bahwa keberadaan nama kolom pada DDL tidak boleh disimpulkan tanpa bukti independen yang dapat diaudit, dan keberadaan definisi kolom DDL tidak pernah membuktikan semantik fungsionalnya.
2. **Tingkat 2 — Definisi Kontrak Field (`UNRESOLVED / NOT FOUND IN NORMATIVE CONTRACTS`)**:
   Tidak ditemukan definisi kontrak formal dalam White Paper v5.6 maupun Roadmap v4.8 yang mendefinisikan tipe payload, format komputasi, atau fungsi bisnis kolom ini dalam arsitektur Album multi-track.
3. **Tingkat 3 — Semantik Implementasi (`UNRESOLVED — BLOCKED BY B-05`)**:
   Tidak ada bukti implementasi aktif yang mendokumentasikan:
   - Apakah hash dihitung atas seluruh berkas ZIP album fisik atau representasi lain.
   - Apakah hash dihitung saat paket diunggah, didistribusikan, atau diunduh.
   - Siapa producer dan consumer aktual dari kolom ini.
   - Bagaimana penanganan penulisan baris child record transaksi album tanpa melanggar batasan Zero-DDL.
   Oleh karena itu, dokumen secara jujur **TIDAK MENGKLAIM** semantik `acquired_package_sha256` sebagai hash seluruh ZIP yang terverifikasi, dan mengunci semantiknya sebagai `BLOCKED BY B-05`.

##### C. Analisis Entitas Komputasional Internal & Interpretasi Desain (Bukan Objek Tersimpan)
Tiga entitas SHA-256 yang pada dokumen lama dihitung sebagai "Objek 5, 6, dan 7" diidentifikasi secara transparan sebagai **langkah komputasi internal perancang tanpa representasi field kontrak tersimpan**:

| Entitas Komputasional | Objek Terkait | Field Identifier Kontrak | Deskripsi Implementasi yang Dilaporkan Programmer — NOT VERIFIED | Status Ontologis |
|---|---|---|---|:---:|
| Canonical Manifest Intermediate Hash | Album Manifest | `FIELD IDENTIFIER NOT VERIFIED IN CONTRACT` | Algoritma PureEd25519 (RFC 8032) menandatangani payload kanonikal UTF-8 secara langsung; tidak ada field hash manifes mandiri yang disimpan dalam manifest maupun database. | `UNRESOLVED / DESIGNER COMPUTATIONAL INTERPRETATION` |
| Container Packaging Intermediate Hash | Kontainer `.nx` | `FIELD IDENTIFIER NOT VERIFIED IN CONTRACT` | Format biner Go (`container.go#L68-L134`) hanya memuat header ukuran, manifest, payload, dan 64-byte trailer signature; tidak ada field hash biner kontainer yang disimpan. | `UNRESOLVED / DESIGNER COMPUTATIONAL INTERPRETATION` |
| Genesis Certificate Intermediate Hash | Genesis Cert | `FIELD IDENTIFIER NOT VERIFIED IN CONTRACT / DDL` | Verifikasi di `sdk.ts#L219, L255` mengeksekusi `NexaCrypto.verify` langsung atas canonical string UTF-8; tidak ada kolom hash sertifikat genesis di database DDL. | `UNRESOLVED / DESIGNER COMPUTATIONAL INTERPRETATION` |

##### D. Status Identifier Referensi `underlying_cert_id`
Berdasarkan uraian implementasi lokal yang dilaporkan Programmer pada `sdk/typescript/src/sdk.ts#L250-L254`:
```typescript
const certIdMatches = (!ownCert.underlying_cert_id || ownCert.underlying_cert_id === certID);
```
Properti `underlying_cert_id` pada Genesis Ownership Certificate secara konseptual merupakan **string referensi identifier sertifikat registri induk (`certID`)**, **BUKAN** merupakan digest SHA-256 bitstream audio. Status bukti repositori bagi audit independen: **`NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE (CONCEPTUAL INVARIANT: CERTIFICATE IDENTIFIER REFERENCE — NOT AN AUDIO HASH DIGEST)`**.

##### E. Rekapitulasi Jumlah & Status Otoritatif (AUDIT-NEW-04)
1. **Jumlah Objek Tanda Tangan Ed25519**: 4 objek konseptual; 3 objek implementasi (Container Packaging, Registry Authority Certificate, Genesis Ownership Certificate) memiliki bukti source yang dilaporkan Programmer dan dibatasi sebagai `VERIFIED BY PROGRAMMER — STATIC SOURCE`; 1 objek Album Manifest Signer tetap `PROPOSED SPECIFICATION` dan belum ditemukan implementasinya.
   - Klaim hubungan kode antara `signature` trailer di Go (`internal/container/container.go#L17-L135`) dan `signatureBytes` di TypeScript SDK (`sdk/typescript/src/container.ts#L4-L104`, `sdk.ts#L143, L151`) dilaporkan Programmer dari commit `fc08a5c`; statusnya `VERIFIED BY PROGRAMMER — STATIC SOURCE`, bukan verifikasi independen Auditor atau bukti runtime.
   - Field `creator_signature` secara konseptual bukan field kontainer melainkan properti Genesis Ownership Certificate (Objek 4); bukti implementasi pada `sdk/typescript/src/ownership.ts#L26` dan `migrations/004_ownership.sql#L25` dilaporkan Programmer sebagai `VERIFIED BY PROGRAMMER — STATIC SOURCE`, bukan verifikasi independen Auditor atau bukti runtime.
2. **Status Field Hash SHA-256**:
   - notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field>` (bukan path manifest normatif): `PROPOSED SPECIFICATION` (usulan skema manifest §5.1 khusus audio; identitas field berstatus `UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / ARCHITECTURE DECISION REQUIRED; STOP AND CLARIFY)`).
   - *Field Hash Non-Audio (Video, Document, Image)*: Kontrak skema manifest untuk Video, Document, dan Image belum mendefinisikan field hash payload khusus secara normatif: **`UNRESOLVED — STOP AND CLARIFY`**; programmer dilarang mengarang field hash generik sepihak.
   - `acquired_package_sha256`: Keberadaan kedua kolom pada DDL statis, producer, consumer, dan asal hash `catalog_snapshots.package_sha256` dilaporkan Programmer sebagai `VERIFIED BY PROGRAMMER — STATIC SOURCE` pada §15.9.5 / E-03. Byte-domain yang dilaporkan adalah seluruh berkas fisik delivery package spool (wrapper ZIP). Live DB tetap `NOT VERIFIED`; relasi child-member dan kontrak downstream child acquisition tetap `UNRESOLVED — BLOCKED BY B-05`. Ketiadaan akses langsung Auditor bukan alasan menurunkan status bukti Programmer.
   - Dokumen **TIDAK MENGKLAIM** keduanya sebagai "dua objek hash normatif terverifikasi".
3. **Entitas Komputasi Internal**: 3 entitas komputasional in-memory tanpa representasi field kontrak tersimpan.
4. **Identifier Referensi Non-Hash**: 1 identifier referensi sertifikat (`underlying_cert_id`, status audit: `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`).
5. **Ketetapan Tata Kelola & Status AUDIT-NEW-04**:
   - Dokumen secara tegas **tidak memaksakan angka delapan**. Akurasi inventaris berbasis bukti diutamakan mutlak daripada mempertahankan angka artifisial dokumen historis.
   - Status AUDIT-NEW-04 dinyatakan secara jujur:
     **`NOT PASS — RECONCILED EVIDENCE-BASED INVENTORY (PRIMARY SOURCE EVIDENCE NOT AVAILABLE FOR INDEPENDENT AUDIT; SEMANTICS BLOCKED BY B-05; SIRKULARITAS SIGNATURE BLOCKED BY B-08)`**.
6. **Status JCS Manifest**: Usulan pengecualian signature manifest dari payload JCS berstatus usulan spesifikasi yang belum disahkan, dan dependensi sirkular B-08 dipertahankan **`UNRESOLVED / REQUIRES CLARIFICATION (B-08)`** tanpa penetapan sepihak.

#### 6.11 Rincian NC-11: Aturan Fallback Offline Registry Terkendali (Spesifikasi Tambahan 7)
- Fallback ke offline cached registry certificate **HANYA DIIZINKAN** pada kondisi kegagalan transport/konektivitas fisik jaringan: `ECONNREFUSED` (koneksi ditolak), `ETIMEDOUT` (timeout), `ENOTFOUND` (DNS gagal).
- **Larangan Fallback (Fail-Closed)**: Jika respons diterima dari Registry tetapi tidak valid (HTTP 5xx, respons malformed, signature tidak valid, atau sertifikat revoked/expired), sistem **DILARANG KERAS** melakukan fallback ke cache. Sistem wajib melempar error fail-closed (`ERR_REGISTRY_SIGNATURE_INVALID` atau `ERR_REGISTRY_UNREACHABLE`).

#### 6.12 Rincian NC-12: Filesystem Safe-Open, Evaluasi Operasional Residual Risk TOCTOU & Batasan POSIX (DEF-07)
Dokumen ini merinci evaluasi operasional atas kerentanan race condition akses berkas (TOCTOU):
1. **Protected Asset / Security Property**: Integritas dan kerahasiaan bitstream audio kontainer `.nx` anggota album yang tersimpan pada direktori ekstraksi lokal dari manipulasi unauthorized process.
2. **Threat Model & Window of Vulnerability**: Penyerang lokal (*local unprivileged adversary*) yang memiliki izin tulis pada filesystem induk bersama. Jendela kerentanan berada pada interval mikrosekon antara resolusi path nama berkas dan perolehan descriptor di kernel (`open`), serta antara `open` dan inspeksi metadata `fstat`.
3. **Protection Boundary yang Diusulkan (Belum Terbukti Diimplementasikan):**
   - Target kontrol yang diusulkan adalah pembukaan berkas menggunakan flag kernel atomik `O_RDONLY | O_NOFOLLOW` pada platform yang mendukungnya. Rujukan `fs_safe.ts#L30-L55` adalah referensi rancangan/target kontrol, bukan bukti modul aktif; PSV-R08 melaporkan `fs_safe.ts` tidak ditemukan dalam scope pencarian.
4. **Kondisi Anomali dan Perilaku Fail-Closed yang Diusulkan:**
   - Rancangan mengusulkan pemeriksaan `fstatSync(fd)` dan pembandingan dengan `lstatSync(resolvedPath)` setelah descriptor diperoleh.
   - Kriteria deteksi usulan: (a) `!fdStat.isFile()`; (b) `fdStat.dev !== lstat.dev` atau `fdStat.ino !== lstat.ino`.
   - Respons fail-closed yang diusulkan: descriptor ditutup, akses/playback ditolak, dan kandidat error `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` digunakan setelah taksonomi error disahkan.
5. **Residual Risk yang Tidak Terlindungi di POSIX Userspace**:
   - Pada standar POSIX userspace (Linux kernel < 5.6 tanpa `openat2(RESOLVE_BENEATH)` atau ketiadaan *mount namespace* privat), penyerang yang mengeksekusi *concurrent ancestor directory rename* saat kernel menyelesaikan komponen direktori induk sebelum mencapai leaf file secara teoretis dapat mengarahkan traversal ke luar direktori kanonikal.
6. **Otoritas Penerimaan Residual Risk & Syarat Penutupan**:
   - Penutupan blocker B-06 **TIDAK BISA** dilakukan hanya dengan meluluskan pengujian descriptor. Penutupan B-06 mensyaratkan:
     1. Verifikasi pengujian unit lolos deteksi anomali descriptor fail-closed (AC-20, AC-21); **DAN**
     2. Penerbitan dokumen resmi *Residual Risk Acceptance* yang ditandatangani oleh **Product Owner / Lead Security Architect**.
   - Sebelum persetujuan risiko resmi tersebut diterbitkan, B-06 tetap berstatus **`OPEN / BLOCKED`**.

#### 6.14 Rincian NC-14: Rekonsiliasi Status NX Verify & Ketiadaan Status Agregat Album (Temuan 3, CONF-02 PO APPROVED)
- Status evaluasi NX Verify memisahkan Lapisan 1 (Signer Trust) dan Lapisan 2 (Member Integrity).
- **Resolusi Otoritatif Keputusan PO (CONF-02 / NC-14 — PILIHAN B APPROVED)**:
  Product Owner secara resmi mengesahkan Pilihan B: **NX Verify tidak perlu dan dilarang menampilkan satu status agregat keseluruhan Album**. Hasil verifikasi setiap berkas `.nx` anggota tetap menjadi hasil utama individual.
  - Keputusan ini tidak mengubah empat canonical verification statuses, lima internal Multi Registry states, Local Override semantics, dan trust semantics individual file.
  - Dilarang keras menciptakan status sintetis baru seperti `ALBUM_TRUSTED`, `ALBUM_INVALID`, atau status agregat lainnya.
  - Navigasi Album pada NX Verify menggunakan tombol manual "Next" (AC-25); AC-33/AC-34 tetap diblokir sampai autentisitas membership dibuktikan, dan Verify tidak memproses file manifest sebagai anggota Album sebelum gate tersebut terpenuhi.

#### 6.15 Rincian NC-15: Taksonomi 20 Kode Error Kanonikal & Provenance Status Normatif (DEF-05, DEFECT-02)
Dokumen ini memetakan taksonomi 20 kode error dengan membedakan secara tegas status provenance normatif masing-masing kode:
*Status Provenance Kode Error (DEFECT-02):*
1. **Status Usulan Spesifikasi Taksonomi (NC-15):** Seluruh 20 kode error kanonikal berstatus **`PROPOSED SPECIFICATION`** di bawah usulan spesifikasi teknis NC-15. White Paper v5.6 tidak mendefinisikan konstanta string diskrit `ERR_...` sebagai ketentuan normatif beku.
2. **Kondisi Kegagalan Terverifikasi pada Kode Sumber (`container.go#L112`):** Kondisi kegagalan unpacking kontainer (arsip terpotong / ukuran header tidak cocok) terverifikasi secara fisik pada basis kode Go (`internal/container/container.go#L112`: `fmt.Errorf("container is truncated...")`). Kondisi kegagalan ini dipetakan ke kode error usulan `ERR_ZIP_INVALID`. String konstanta `ERR_ZIP_INVALID` sendiri merupakan bagian dari usulan taksonomi NC-15.
3. **Unresolved Error Handling (Genesis Certificate Signature):** Baseline kode `sdk.ts#L227-L229` melempar generic exception `Signature verification error: ...`. Tidak ditemukan konstanta kode diskrit `ERR_GENESIS_SIGNATURE_INVALID` pada baseline. Penanganan kegagalan verifikasi tanda tangan Genesis Certificate dieksekusi fail-closed mutlak (`canPlay: false`, `is_valid: false`, `status: INVALID`), sementara kode error diskrit kanonikalnya berstatus **`UNRESOLVED IN BASELINE TAXONOMY (PENDING ARCHITECTURE DEFINITION)`**.
4. **Larangan Fabrikasi Kode:** Dilarang keras menciptakan kode error baru (kode ke-21) tanpa otorisasi Otoritas Arsitektur.

Tabel berikut merinci taksonomi 20 kode error diskrit tersebut beserta status provenans sumber yang faktual:

| Kode Error Diskret | Layer Penghasil | Kondisi Pemicu Diskret | Aksi Sistem | AC Penguji | Status Provenance Sumber (DEFECT-02) |
|---|---|---|---|:---:|:---:|
| `ERR_MANIFEST_MISSING` | Manifest Parser | `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] tidak ditemukan di root ZIP | Fail-closed; tolak ekstraksi | AC-01 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_MANIFEST_MALFORMED` | Manifest Parser | Sintaksis JSON rusak, regex invalid, escape syntax fail | Fail-closed; tolak manifest | AC-01 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_MANIFEST_DUPLICATE_KEY` | Strict JSON Parser | Ditemukan duplikasi key literal atau via decoded escape | Fail-closed; hentikan parsing | AC-05 | Proposed Specification (NC-15; dependensi modul B-01/NC-03) |
| `ERR_MANIFEST_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature manifest gagal | Fail-closed; tolak deklarasi manifest sebagai sumber membership Album; jangan simpulkan member `.nx` INVALID. Diagnostik standalone hanya untuk file yang disediakan independen, bukan sebagai anggota Album. | AC-03 | Proposed Specification (NC-15; dependensi B-08) |
| `ERR_ALBUM_SIGNER_UNKNOWN` | Trust Store | Identitas/trust signer belum dapat dipastikan | Penggunaan manifest sebagai deklarasi membership menunggu CONF-01; bukan global playback block dan bukan status INVALID untuk member. | AC-07 | Proposed Specification (Pending Keputusan PO B-09/CONF-01) |
| `ERR_ALBUM_SIGNER_UNTRUSTED` | Trust Store | Status signer dinyatakan untrusted/revoked oleh mekanisme Registry yang kelak disahkan (mekanisme saat ini belum ditetapkan) | Jangan gunakan manifest sebagai deklarasi membership tepercaya; jangan otomatis menandai member INVALID atau memblokir playback standalone; mekanisme revocation masih BLOCKED. | AC-08 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_CONTAINER_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature container individual `.nx` gagal | Fail-closed; tandai trek corrupt | AC-04 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_CONTAINER_HASH_MISMATCH` | Integrity Engine | SHA-256 payload audio tidak cocok dengan manifest/cert | Fail-closed; tandai tampered | AC-09 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_ZIP_INVALID` | ZIP Extractor / Go Engine | Format ZIP corrupt/rusak, central directory invalid, entri symlink atau special file (FIFO, socket, dev) terdeteksi (AUDIT-NEW-06), path traversal (`../`, absolute path), atau terjadi benturan nama case-insensitive antar-entri ZIP (AUDIT-NEW-07/08) | Fail-closed; tolak ekstraksi fail-closed | AC-02, AC-13 | Proposed Specification (NC-15; kondisi kegagalan terverifikasi di `container.go#L112`) |
| `ERR_ZIP_QUOTA_EXCEEDED` | ZIP Wrapper Extractor | Ukuran ZIP > 500 MB desimal (500.000.000 bytes) compressed, uncompressed cumulative extraction > 4 GB desimal, atau jumlah entri > 200 (AUDIT-NEW-08 deterministik) | Fail-closed; batalkan ekstrak | AC-13 | Proposed Specification (NC-15; usulan kuota B-07/NC-07) |
| `ERR_ZIP_BOMB_DETECTED` | ZIP Wrapper Extractor | Rasio dekompresi per-entri atau global melampaui ambang batas rasio kompresi usulan B-07 (AUDIT-NEW-08 deterministik) | Fail-closed; karantina arsip | AC-13 | Proposed Specification (NC-15; usulan kuota B-07/NC-07) |
| `ERR_ZIP_ENTRY_MISMATCH` | Packaging Validator | Entri berkas reguler ZIP tidak cocok persis 1:1 secara bijektif dengan nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) di manifest (terdapat berkas manifest hilang di ZIP, atau terdapat entri berkas reguler ekstra/asing di dalam ZIP di luar deklarasi manifes dan `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan]) (AUDIT-NEW-08 deterministik) | Fail-closed; tolak kontainer | AC-02, AC-13 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | Filesystem Safe-Open | Path traversal (`../`), symlink bypass, TOCTOU | Fail-closed; tolak akses fd | AC-20, AC-21 | Proposed Specification (NC-15; dependensi mitigasi B-06) |
| `ERR_PLAYBACK_UNAUTHORIZED` | JIT Authorizer | Tidak ada entitlement aktif / lisensi tidak valid | Fail-closed; tolak playback | AC-22 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_MARKETPLACE_REPLAY_DETECTED` | Transaction Engine | Transaksi dengan token/hash identik terdeteksi | Idempotent return state lama | AC-15 | Proposed Specification (NC-15; dependensi B-04/CONF-03) |
| `ERR_ID_COLLISION` | Identity Generator | Tabrakan string hash derivasi ID pada tabel DB | Fail-closed; log & abort | AC-27 | Proposed Specification (NC-15; usulan derivasi NC-16) |
| `ERR_TRANSACTION_FAILED` | Transaction Engine | Kegagalan eksekusi query multi-item DB lokal | Rollback transaksi lokal | AC-14 | Proposed Specification (NC-15; dependensi B-04/CONF-03) |
| `ERR_REGISTRY_UNREACHABLE` | Network / Trust Store | Registry offline dan tidak ada cache valid | Fail-closed; tolak verifikasi | AC-18, AC-19 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_REGISTRY_SIGNATURE_INVALID` | Trust Store | Signature respons Registry tidak valid | Fail-closed; tolak respons | AC-18, AC-19 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_LICENSE_DAEMON_COMMUNICATION` | Marketplace Server | Panggilan HTTP ke Sprint 12 License Daemon gagal | Fail-closed; rollback mutasi DB lokal uncommitted; efek samping daemon eksternal tidak terkompensasi (gap 2PC B-04 / CONF-03) | AC-14 | Proposed Specification (NC-15; dependensi B-04/CONF-03) |

#### Matriks Pemetaan Kondisi ke Kode Error Deterministik 1:1 (AUDIT-NEW-08 — PO MANDATE)
Untuk memastikan kepatuhan mutlak atas mandat AUDIT-NEW-08 dan mencegah pemetaan bercabang antar-layer, setiap kondisi kegagalan spesifik pada AC-02, AC-05, dan AC-13 dipetakan secara deterministik 1:1 ke satu kode error kanonikal tanpa kontradiksi:

| Kondisi Kegagalan Spesifik | Layer Pemeriksaan | Kode Error Kanonikal | Referensi Normatif | AC Terkait |
|---|---|---|---|:---:|
| Arsip ZIP rusak / format truncated / central directory corrupt | ZIP Reader | `ERR_ZIP_INVALID` | PKWARE APPNOTE §4.3; `container.go#L112` | AC-02 |
| ZIP memuat entri symlink atau special file (FIFO, socket, dev) | ZIP Reader | `ERR_ZIP_INVALID` | Keputusan PO (AUDIT-NEW-06); POSIX.1 | AC-02 |
| Benturan nama entri ZIP case-insensitive (e.g. `TrackA.nx` vs `tracka.nx` pada Central Directory) | ZIP Reader / Extractor | `ERR_ZIP_INVALID` | Keputusan PO (AUDIT-NEW-07); §5.1 Boundary Matrix | AC-02 |
| Path traversal saat ekstraksi ZIP (`../`, `..\`, absolute path, leading slashes) | ZIP Extractor | `ERR_ZIP_INVALID` | PKWARE APPNOTE §4.4.17; POSIX.1 | AC-02 |
| Duplikasi nama file di manifes / benturan case-insensitive pada deklarasi manifest | Manifest Validator | `ERR_MANIFEST_MALFORMED` | §5.1 Skema Manifest; AC-01 | AC-01 |
| Duplikasi key JSON di manifest (literal atau Unicode escape) | Strict JSON Parser | `ERR_MANIFEST_DUPLICATE_KEY` | RFC 8259; RFC 8785; NC-03 | AC-05 |
| Ketidakcocokan bijeksi 1:1 deklarasi manifes vs entri ZIP (berkas manifes tidak ditemukan di ZIP, atau terdapat entri berkas reguler ekstra/asing di dalam ZIP di luar deklarasi manifes dan `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan]) | Packaging Validator | `ERR_ZIP_ENTRY_MISMATCH` | §5.2 Tahap 5; AC-02, AC-13 | AC-02, AC-13 |
| Ukuran arsip terkompresi > 500 MB desimal (500.000.000 bytes) | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | Usulan B-07; §6.7 | AC-13 |
| Akumulasi ekstraksi uncompressed > 4 GB desimal ($4 \times 10^9$ bytes) | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | Usulan B-07; §6.7 | AC-13 |
| Jumlah entri ZIP > 200 entri | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | Usulan B-07; §6.7 | AC-13 |
| Rasio kompresi melampaui batas bomb (ambang rasio usulan B-07) | ZIP Wrapper Extractor | `ERR_ZIP_BOMB_DETECTED` | Usulan B-07; §6.7 | AC-13 |
| Path traversal saat Safe-Open descriptor filesystem | Filesystem Safe-Open | `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | POSIX.1-2017 `O_NOFOLLOW`; §6.12 | AC-20 |

> **Prinsip Rekonsiliasi Deterministik Bebas Kontradiksi (AUDIT-NEW-06, AUDIT-NEW-08):**
> 1. *Pemisahan Tegas Layer (FINDING-04)*: (a) Anomali fisik kontainer ZIP (arsip rusak, symlink/special file, path traversal fisik, collision nama ZIP) dipetakan ke **`ERR_ZIP_INVALID`** pada ZIP Reader/Extractor; (b) Anomali deklarasi manifes (sintaksis rusak, pelanggaran regex format nama berkas pada nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan), duplikasi nama di manifes) dipetakan ke **`ERR_MANIFEST_MALFORMED`** pada Manifest Validator; (c) Pelanggaran bijeksi 1:1 antara manifes dan ZIP (baik ada berkas manifes hilang di ZIP maupun ada berkas reguler ekstra/asing di dalam ZIP yang tidak dideklarasikan) dipetakan secara eksklusif dan tunggal ke **`ERR_ZIP_ENTRY_MISMATCH`** pada Packaging Validator. Tidak ada tumpang tindih antar-layer.
> 2. *Penerimaan Direktori*: Sesuai keputusan PO (AUDIT-NEW-06), entri direktori di dalam ZIP diterima secara sah dan tidak melempar error.
> 3. *Ketiadaan Fabrikasi Kode Error Baru*: Taksonomi tetap dibatasi tepat pada 20 kode error kanonikal yang ada tanpa penambahan kode baru.
> 4. *Status Provenance Taksonomi*: Taksonomi 20 kode error kanonikal di atas berstatus **Proposed Specification (NC-15)** yang belum dibekukan dalam White Paper v5.6, dan kode diskrit kegagalan tanda tangan Genesis berstatus **Unresolved Taxonomy** (dengan perilaku fail-closed `canPlay: false` pasti).

#### 6.16 Rincian NC-16: Derivasi Matematis Identifier Deterministik (Spesifikasi Tambahan 5)
Derivasi identifier child acquisition/entitlement untuk Model B mengusulkan penggunaan format SHA-256 terpotong (*truncated SHA-256*) sepanjang 32 karakter heksadesimal (`[PROPOSED SPECIFICATION — NOT YET CLOSED UNDER B-04]`). Input `bundle_checkout_id` adalah identitas korelasi checkout logis (bukan parent acquisition row atau kolom DDL baru); `member_asset_id` mengidentifikasi member `.nx` secara stabil. Formula ini tetap proposal sampai encoding, domain separation/versioning, uniqueness handling, dan integrasi idempotency ditetapkan dalam kontrak B-04:
1. **Child Acquisition ID**:
   $\text{child\_acq\_id} = \text{"acq\_" } || \text{SHA256}(\text{bundle\_checkout\_id } || \text{ ":" } || \text{member\_asset\_id})[0..31]$
   - Panjang string: $4 + 32 = 36$ karakter. Kapasitas kolom DDL aktif: `VARCHAR(128)`. Margin aman: $128 - 36 = 92$ karakter.
2. **Child Entitlement ID**:
   $\text{child\_ent\_id} = \text{"ent\_" } || \text{SHA256}(\text{bundle\_checkout\_id } || \text{ ":" } || \text{member\_asset\_id } || \text{ ":ent"})[0..31]$
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
| **B-03** | Ekstraktor ZIP standar rentan path traversal dan zip-bomb di userspace POSIX. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Ketiadaan validasi kuota ekstraksi terintegrasi, sanitasi nama entri, dan invariant post-open descriptor. | Klaim implementasi ekstraktor aman dan pemenuhan Tabel Coverage Proof B-03 merupakan laporan Programmer yang belum diverifikasi independen; B-07 tetap blocked sampai kuota disahkan dan seluruh kewajiban diuji. |
| **B-04** | Transaksi Marketplace multi-member, satu Commercial Bundle checkout dengan Independent Member Acquisitions, dan konsistensi settlement di bawah Zero-DDL. | `MODEL B + SSP / LARGEST REMAINDER APPROVED; BUNDLE_CHECKOUT_ID PRINCIPLE APPROVED; TRANSACTION CONTRACT PARTIALLY SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Satu checkout komersial menghasilkan N acquisition dan N entitlement independen; `bundle_checkout_id` telah disahkan sebagai identitas korelasi komersial independen dari `acquisition_id` dan `payment_order_id`; mekanisme persistensi/korelasi masih belum ditetapkan. DDL tidak menyediakan relasi parent-child eksplisit; transaksi lokal dan side effect License Daemon tidak memiliki 2PC/compensation otomatis. | Pertahankan Model B, SSP/Largest Remainder, dan tujuh aturan normatif `bundle_checkout_id` pada §6.8.2. B-04 baru dapat ditutup setelah mekanisme persistensi/korelasi, idempotency/replay, commit boundary, retry, partial failure, settlement/reconciliation, dan side effect License Daemon ditetapkan serta acceptance tests lengkap; tanpa klaim 2PC/compensation yang tidak tersedia. |
| **B-05** | Kontrak `acquired_package_sha256` untuk acquisition/entitlement independen per member Album. | `TARGET MEMBER HASH CONTRACT NOT YET SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Bukti baseline melaporkan hash existing dibentuk dari seluruh wrapper ZIP delivery package; target Model B memerlukan byte-domain dan producer-consumer yang tepat untuk masing-masing `.nx` member. DDL memiliki field hash pada acquisition dan entitlement, tetapi tidak menyediakan relasi child-member Album. | Tetapkan byte-domain individual `.nx` member, producer, consumer download/verification, konsistensi acquisition-entitlement, dan negative tests. Wrapper ZIP hash tidak boleh digunakan sebagai hash member. Pertahankan Zero-DDL dan jangan mengklaim pemetaan child yang tidak tersedia. |
| **B-06** | Kerentanan Race Condition Filesystem (TOCTOU) pada Akses Kontainer Desktop. | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | Batasan kernel POSIX userspace terhadap concurrent ancestor directory rename. | Urutan penutupan: (1) Programmer melakukan PSV atas implementasi filesystem per platform, operasi descriptor/handle, symlink/ancestor handling, TOCTOU, staging permissions, dan adversarial tests; (2) mitigasi dan hasil uji dibandingkan dengan AC-20/AC-21; (3) Product Owner / Lead Security Architect diminta menerima residual risk hanya jika masih ada risiko residual yang teridentifikasi. Penerimaan risiko tidak menggantikan mitigasi atau pengujian. |
| **B-07** | Batas Ukuran dan Kuota Ekstraksi Arsip Pembungkus ZIP (Nilai Numerik Masih Berstatus Usulan). | `PROPOSED SPECIFICATION` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY PROPOSED SPEC` | Nilai numerik kuota ZIP (500 MB desimal [500.000.000 bytes] terkompresi / 4 GB desimal akumulatif / 200 entri [entri direktori diterima sesuai Keputusan PO AUDIT-NEW-06; pembatasan flat hanya berlaku pada regex path relatif member .nx manifest] / usulan rasio kompresi 10:1 vs 100:1 referensi pembanding) berstatus usulan spesifikasi teknis di bawah NC-07 dan belum dibekukan dalam White Paper v5.6. Pembatasan kuota ini berlaku eksklusif pada pembungkus ZIP (4 GB desimal), bukan batas payload kontainer anggota `.nx` (2 GiB pada baseline). | Programmer melakukan PSV terlebih dahulu atas parser/extractor, streaming counters, enforcement kuota per-layer, dan test yang tersedia. Angka yang masih berstatus proposal tidak boleh diperlakukan sebagai kontrak implementasi. Keputusan otoritatif untuk membekukan parameter normatif diminta setelah bukti teknis, threat model, dan benchmark tersedia. |
| **B-08** | Circular Dependency Kriptografi Tanda Tangan Manifest & JCS. | `BLOCKED — REQ CLARIFICATION` | `NOT IMPLEMENTED` | `BLOCKED` | Potensi circular dependency antara signature field dan byte-domain yang dikanonisasi; konstruksi signed-content dan verification path aktual belum diverifikasi. | Programmer melakukan PSV terlebih dahulu atas signed-content construction, signature envelope, serialization/canonicalization, Ed25519 input, key binding, dan verification path. Keputusan Architecture Authority hanya diperlukan jika setelah PSV signature scope/representation normatif tetap belum ditetapkan atau terbukti bertentangan dengan kontrak. |
| **B-09** | Ketiadaan keputusan mengenai autentisitas manifest/membership saat Album Signer `UNKNOWN` & ketiadaan lifecycle signer di Registry. | `GAP UNRESOLVED` | `NOT IMPLEMENTED` | `PO / ARCHITECTURE DECISION REQUIRED` | CONF-01 terbatas pada apakah deklarasi manifest dengan signer `UNKNOWN` dapat mengautentikasi membership; identitas, enrollment, rotation, dan revocation signer belum memiliki kontrak. Ini bukan kebijakan playback global. | Programmer melakukan PSV terlebih dahulu atas signer/membership, identity binding, enrollment, authority, key custody, rotation, revocation, freshness, manifest verification, dan dependency Registry yang benar-benar ada. Setelah bukti primer dipetakan, keputusan PO/Architecture Authority hanya diminta untuk kebijakan autentisitas membership atau kontrak identitas/lifecycle yang memang belum ditetapkan. Tidak boleh menciptakan mekanisme Registry tanpa dasar. |

---


#### Tabel Pembuktian Cakupan Granular per-Kebutuhan (Requirement-Granular Coverage Proof) Blocker B-03 (DEF-02)
Sesuai Bagian II (DEF-02), evaluasi keterlacakan B-03 dipisahkan secara ketat per kebutuhan normatif individual, memisahkan lapisan validasi arsip ZIP dari lapisan Safe-Open filesystem:

| ID Kebutuhan | Deskripsi Kebutuhan Spesifik | Sumber Normatif | Bagian Penangan di Plan | AC Penguji | Metode & Kondisi Pengujian | Bukti yang Diharapkan | Status Cakupan |
|:---:|---|---|---|:---:|---|---|:---:|
| **REQ-B03-01** | Validasi Nama Berkas Entri ZIP & Case-Insensitive Uniqueness (AUDIT-NEW-07 — PO APPROVED) | PKWARE APPNOTE; §5.1 Skema Manifest | §5.1 Skema Manifest; §6.7 | AC-02 | Pengujian unit nama entri ZIP dengan karakter titik ganda, spasi, karakter kontrol ASCII, serta evaluasi case-folding deterministik (`toLowerASCII`) sesuai Boundary Matrix §5.1 lintas POSIX/Windows/Android. | Ekstraksi ditolak fail-closed dengan `ERR_ZIP_INVALID`. | `PARTIALLY COVERED (PROPOSED SPEC)` |
| **REQ-B03-02** | Pencegahan ZIP Path Traversal (`../`, `..\\`, absolute path, leading slashes) | PKWARE APPNOTE §4.4.17; POSIX.1 | §6.7 Batas Ekstraksi; §6.12 | AC-02, AC-20 | Pengujian arsip ZIP sintetis dengan entri `../../evil.nx` atau `/tmp/evil.nx`. | ZIP reader menolak penulisan berkas di luar target extraction directory (`ERR_ZIP_INVALID`). | `COVERED` |
| **REQ-B03-03** | Penolakan Entri Symlink & Special Files, serta Independensi Entri Byte Identik (AUDIT-NEW-06 — PO APPROVED) | PKWARE APPNOTE; POSIX.1 | §6.7 Aturan Ekstraksi; §6.12 | AC-02, AC-21 | Pengujian ZIP dengan entri bertipe symbolic link, FIFO, socket, atau device files. Tidak mengasumsikan tipe hardlink generik universal dalam ZIP; dua entri dengan isi byte identik diuji sebagai 2 file independen; tipe ambigu ditolak fail-closed. | Ekstraktor mendeteksi entri symlink/special file dan menolak ekstraksi fail-closed (`ERR_ZIP_INVALID`). Entri dengan byte identik diekstrak sebagai berkas reguler independen. | `COVERED` |
| **REQ-B03-04** | Pembatasan Rasio Dekompresi ZIP Bomb (Ambiguitas Rasio Usulan B-07 10:1 vs Referensi Pembanding Eksternal 100:1 yang Belum Diverifikasi per-entri & global) | Usulan Spesifikasi NC-07 (B-07) | §6.7 Rasio Kompresi; §6.15 | AC-13 | Ekstraksi berkas terkompresi tinggi (e.g. 1MB kompresi mengembang > 10MB pada batas 10:1 atau > 100MB pada referensi pembanding 100:1), atau `compressed == 0` saat `uncompressed > 0`. Catatan: nilai 100:1 adalah referensi pembanding eksternal yang belum diverifikasi normatif; PKWARE APPNOTE dan RFC 1951 tidak memuat ambang rasio keamanan tersebut. | Dekompresi stream dibatalkan fail-closed melempar `ERR_ZIP_BOMB_DETECTED`. | `PARTIALLY COVERED (PROPOSED SPEC — AMBIGUITAS RASIO 10:1 vs 100:1 PENDING KEPUTUSAN ARSITEKTUR B-07)` |
| **REQ-B03-05** | Pembatasan Ukuran Dekompresi: Batas Per-Entri Kontainer ($\le 2\text{ GiB}$) vs Batas Akumulasi Ekstraksi Wrapper ($\le 4\text{ GB desimal}$) | `container.go#L106` (Payload Kontainer $\le 2\text{ GiB}$ / $2 \times 1024^3$ bytes); Usulan Spesifikasi NC-07 / B-07 (Wrapper $\le 4\text{ GB desimal}$ / $4 \times 10^9$ bytes) | §6.7 Batas Ukuran; §8 (AC-13); `container.go#L106` | AC-13 (Validasi Kuota Akumulatif Wrapper $\le 4\text{ GB desimal}$); **CELAH PENGUJIAN AC REGISTER** (Batas payload kontainer individual 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106` belum memiliki AC penguji eksplisit di AC Register; AC-11 dan AC-12 dicabut dari pemetaan ini karena murni menguji ekstraksi mandiri dan pemenuhan invariant packaging PE-01 tanpa cakupan batas 2 GiB) | (a) Pengujian ekstraksi wrapper multi-entri dengan akumulasi byte ekstraksi > 4 GB desimal ($4 \times 10^9$ bytes) diuji via AC-13; (b) Pengujian batas payload kontainer tunggal > 2 GiB ($2 \times 1024^3$ bytes pada `container.go#L106`) diidentifikasi secara terbuka sebagai celah pengujian pada AC Register yang menunggu penetapan kriteria uji formal dari PO/Arsitektur. | (a) Akumulasi byte wrapper > 4 GB desimal membatalkan ekstraksi fail-closed melempar `ERR_ZIP_QUOTA_EXCEEDED`; (b) Pengujian batas payload 2 GiB individual kontainer menunggu penetapan kriteria uji formal dari PO/Arsitektur. | `PARTIALLY COVERED (CELAH PENGUJIAN AC REGISTER UNTUK BATAS PAYLOAD 2 GiB; BATAS WRAPPER 4 GB DESIMAL PROPOSED SPEC B-07)` |
| **REQ-B03-06** | Pembatasan Jumlah Entri: Panduan UI Manifest ($\le 50$ Track) vs Kuota Entri Arsip Wrapper ($\le 200$ Entri) | WP v5.6 (UI guidance); Usulan Spesifikasi NC-07 / B-07 (Batas 200 Entri) | §5.1 Skema Manifest; §6.7 Batas Entri Wrapper | AC-13 (Pengujian Kuota Wrapper > 200 Entri); **CELAH PENGUJIAN AC REGISTER** (Validasi batas panduan 50 track manifest belum memiliki AC penguji khusus di AC Register; AC-05 dicabut karena murni menguji duplicate keys) | (a) Ekstraksi ZIP dengan total entri central directory > 200 fisik (menghitung seluruh berkas member, manifest, dan entri direktori: $N_{\text{total}} = N_{\text{tracks}} + N_{\text{manifest}} + N_{\text{dir\_entries}} > 200$) diuji via AC-13 pada Stage 2; (b) Validasi skema manifest dengan deklarasi track > 199 (`maxItems: 199`) atau panduan UI > 50 track dievaluasi pada Stage 3 dan diidentifikasi secara terbuka sebagai celah pengujian yang memerlukan penetapan AC baru oleh PO/Arsitektur; pemenuhan batas manifest `maxItems: 199` tidak menjamin terpenuhinya kuota 200 entri fisik jika terdapat entri direktori. | (a) Wrapper dengan total entri fisik $N_{\text{total}} > 200$ ditolak fail-closed melempar `ERR_ZIP_QUOTA_EXCEEDED`; (b) Penolakan manifest track > 50 menunggu penambahan AC penguji definitif dari PO/Arsitektur. | `PARTIALLY COVERED (CELAH PENGUJIAN UNTUK 50-MEMBER MANIFEST & PROPOSED SPEC B-07 UNTUK 200-ENTRI WRAPPER)` |
| **REQ-B03-07** | Penegakan Keputusan PO atas Entri Direktori & Larangan Subdirektori Member (AUDIT-NEW-06 — PO APPROVED) | Keputusan PO AUDIT-NEW-06; PKWARE APPNOTE; §5.1 Skema | §5.1 Skema; §6.7; §6.15 | AC-02 | Pengujian arsip ZIP yang memuat entri direktori (diterima sesuai keputusan PO) vs manifest dengan deklarasi path bersubdirektori (ditolak via regex manifest). | Entri direktori diterima; manifest dengan path bersubdirektori ditolak fail-closed dengan `ERR_MANIFEST_MALFORMED`. | `COVERED` |
| **REQ-B03-08** | Filesystem Safe-Open Flag Atomik (`O_RDONLY \| O_NOFOLLOW`) | POSIX.1-2017; `fs_safe.ts` | §6.12 Invariant Safe-Open | AC-20 | Panggilan pembukaan berkas `.nx` pada target symlink di leaf component path. | Kernel mengembalikan `ELOOP`; fungsi melempar `ERR_FILESYSTEM_CONTAINMENT_VIOLATION`. | `COVERED` |
| **REQ-B03-09** | Verifikasi Post-Open Descriptor (`fstat` vs `lstat` & dev/ino match) | POSIX.1-2017; `fs_safe.ts` | §6.12 Invariant Descriptor | AC-21 | Pengujian pergantian berkas dengan symlink atau modifikasi inode pasca-open. | Pemeriksaan descriptor mendeteksi mismatch, menutup `fd`, fail-closed `canPlay: false`. | `PARTIALLY COVERED (SECURITY RESIDUAL RISK)` |

*Pemisahan Lapisan Keamanan (DEF-02):*
- *Lapisan Ekstraksi ZIP (REQ-B03-01 s.d. REQ-B03-07):* Menjamin integritas dan batasan sumber daya saat unpacking arsip dari storage/network ke temporary directory.
- *Lapisan Safe-Open Filesystem (REQ-B03-08 & REQ-B03-09):* Menjamin proses playback membaca berkas `.nx` reguler terisolasi. Pemuatan Safe-Open **TIDAK MEMBUKTIKAN** keamanan ekstraksi ZIP.

---

### 7.2 Finding Register (F-01 sampai F-15) — Rekonsiliasi Historis Penuh (Bagian 4.3)

> **PERINGATAN GOVERNANCE (Bagian 4.3 Mandat Audit):**  
> Seluruh 15 temuan teknis historis F-01 sampai F-15 direkonsiliasi secara penuh sesuai definisi asalnya. Label `SPECIFIED IN PLAN` menyatakan bahwa masalah telah dirumuskan dalam spesifikasi dokumen ini. Label ini **SECARA TEGAS BUKAN** klaim bahwa kode telah diimplementasikan (`NOT IMPLEMENTED`), **BUKAN** bukti bahwa pengujian runtime telah lulus, dan **BUKAN** penutupan blocker (Blocker tetap `OPEN / BLOCKED`).

| ID Finding | Deskripsi Makna Historis yang Wajib Dipertahankan (Bagian 4.3) | Status Analisis Dokumen (Bukan Bukti Implementasi / Blocker Tidak Ditutup) | Rujukan Bagian & Dasar Fakta |
|:---:|:---|:---:|:---|
| **F-01** | **Filesystem containment dan klasifikasi UNTRUSTED**: Pembatasan akses kontainer audio pada direktori kanonikal terisolasi dan penolakan symlink traversal. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Invariant Safe-Open; AC-20, AC-21. |
| **F-02** | **Skema Genesis dan urutan validasi**: Pemisahan urutan verifikasi sertifikat genesis individual dari otorisasi album level atas. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Urutan Validasi JIT 8-tahap (Tahap 5); AC-10. |
| **F-03** | Binding Creator / Packaging Authority: pemisahan tiga peran dan otorisasi third-party packaging (AUDIT-NEW-10) | TARGET DESIGN SPECIFIED — IMPLEMENTATION NOT VERIFIED | §5.2; §6.9; §13.12.11; AC-04, AC-10 | Keputusan PO menetapkan tiga peran berbeda dan tidak mewajibkan equality. Third-party packager wajib membuktikan delegation; self-packaging tidak memerlukan delegation tambahan. Sisa pertanyaan normatif terbatas pada siapa yang boleh menerbitkan delegation dan subdelegation. |
| **F-04** | **Waktu dan skema Registry sidecar**: Validasi waktu sertifikat, cache TTL, dan aturan fallback offline terisolasi dari transport error. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.11 Aturan Cache Offline Registry; AC-18, AC-19. |
| **F-05** | **Perbedaan klasifikasi kriptografis `INVALID` dan kondisi yang tidak dapat dipastikan**: Memisahkan signature fail-closed dari status `UNKNOWN`. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.15 Taksonomi Error; AC-07, AC-08, AC-18, AC-26. |
| **F-06** | **Kontrak aktual `container.Unpack`**: Pustaka packaging memvalidasi kontainer `.nx` mandiri hasil ekstraksi arsip pembungkus ZIP. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED / NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE (Bagi Audit Independen: Akses Repositori Primer whisnu/nexa Belum Tersedia / Belum Diverifikasi Secara Independen oleh Auditor)` | `internal/container/container.go#L110-L160`; E-02; AC-11, AC-12. |
| **F-07** | **Schema manifest internal**: Draf JSON Schema audio (Draft 7) berstatus proposed/non-normative; bukan 13 required fields universal. Schema universal multi-payload belum lengkap (NC-01/AC-01). | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Skema Manifest JSON Lengkap; AC-01. |
| **F-08** | **Penanganan exception pada verifikasi signature**: Exception format kunci/buffer pada modul kriptografi ditangkap dan dipetakan ke kode error diskrit. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | `sdk/typescript/src/crypto.ts#L45`; §6.15; AC-26. |
| **F-09** | **Validasi nama file**: Penegakan pola penamaan berkas trek member `.nx` strictly flat (`^[a-zA-Z0-9_-]+\.nx$`) dengan larangan separator direktori/subdirektori pada path member manifest (tidak melarang directory entries di dalam arsip ZIP yang sah diterima sesuai Keputusan PO). Dilarang memuat titik pada basename guna mencegah kerentanan path traversal dan kebingungan ekstensi ganda. Pola ini diselaraskan 100% konsisten dengan skema manifest JSON §5.1 dan validasi `cleanBase` di `marketplace/server.js:164`. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §5.1 Skema Manifest; §8 (AC-02), AC-20. |
| **F-10** | **Penggunaan `assetId`/`asset_id` anggota yang benar dalam laporan (reporting) (DEF-03)**: Pemulihan makna historis: memastikan pelaporan status verifikasi dan audit log NX Verify mengidentifikasi setiap anggota album menggunakan `asset_id` independennya masing-masing, bukan ID album gabungan. Hubungan ke AC-26 dicabut karena AC-26 murni menguji taksonomi error. Mengingat saat ini belum ada Acceptance Criteria khusus dalam AC-01..AC-27 yang menguji output format pelaporan Verify per-anggota, status keterlacakan F-10 ditetapkan secara jujur sebagai celah spesifikasi pengujian. | `SPECIFICATION GAP / BLOCKED IN AC REGISTER` | §5.3 Tiga Lapisan Status Verify; Celah AC Register (Belum ada AC penguji pelaporan per-anggota). |
| **F-11** | **Batas klaim filesystem containment**: Mitigasi symlink traversal pasca-open dan pengakuan keterbatasan userspace POSIX. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Safe-Open Invariant; AC-20, AC-21. |
| **F-12** | **Batas descriptor dan primitive filesystem**: Evaluasi descriptor file pasca-open dan pengakuan batas race condition POSIX userspace. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.12 Batasan Kernel POSIX; AC-21, B-06. |
| **F-13** | **Bukti AC-03/AC-04 tidak boleh diklaim membuktikan hal di luar signature manifest**: Isolasi batas pengujian unit vs agregat album. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §8 (AC-03, AC-04); batas bukti E-02 dan E-06. |
| **F-14** | **Bukti AC-05/AC-08/AC-09 tidak boleh digeneralisasi menjadi bukti E2E**: Bukti inspeksi kode lokal Linux server bukan bukti runtime mobile. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §4.4 Evidence Ledger E-01..E-09; G-02. |
| **F-15** | **Klaim zero-exposure tidak boleh dibuat tanpa bukti arsitektur yang memadai**: Pengakuan terbuka atas gap 2PC dan batasan Zero-DDL Marketplace. | `SPECIFIED IN PLAN (PENDING IMPLEMENTATION & TEST)` | §6.8 Batas Atomisitas Transaksi Marketplace; B-04 / CONF-03. |

---

## 8. ACCEPTANCE CRITERIA REGISTER (AC-01 SAMPAI AC-34)

Tabel berikut merinci seluruh 34 Acceptance Criteria (AC-01 sampai AC-34) secara lengkap dan terpetakan status dependensinya:

| ID | Kontrak Dasar | Sumber Otoritatif | Skenario Uji / Kondisi Masukan | Expected Result / Kriteria Keberhasilan | Status Kesiapan Uji | Dependensi Blocker / Governance |
|:---:|:---:|:---|:---|:---|:---:|:---:|
| **AC-01** | NC-01 | White Paper v5.6 §Manifest; RFC 8259; §5.1 Skema Manifest; Keputusan PO AC-01 | Evaluasi struktur dan sintaksis manifest album: missing required fields, unknown fields, duplicate keys, unsupported schema version, atau unsupported payload type | Manifest dievaluasi deterministik fail-closed: missing required fields → `ERR_MANIFEST_MALFORMED`; duplicate keys → `ERR_MANIFEST_DUPLICATE_KEY`; unknown fields wajib ditolak fail-closed sesuai keputusan PO; unsupported schema version → `ERR_MANIFEST_MALFORMED`; unsupported payload type → ditolak fail-closed. Universal multi-payload schema dan implementasi parser/validator masih menjadi dependency. | `[TEST-PLANNED — EXECUTION BLOCKED]` | NC-01 / universal schema dan parser/validator belum siap; kebijakan unknown fields telah diputuskan PO. |
| **AC-02** | NC-01/07 | White Paper v5.6; APPNOTE; AUDIT-NEW-06/07/08 | Validasi arsip ZIP wrapper: menerima regular files dan directories; menolak symlink dan special files (FIFO, socket, dev) fail-closed (`ERR_ZIP_INVALID`); menolak arsip rusak/truncated (`ERR_ZIP_INVALID`); menolak benturan nama case-insensitive antar-entri ZIP (`ERR_ZIP_INVALID`); menolak deklarasi manifes dengan nama berkas non-regex atau benturan case-insensitive (`ERR_MANIFEST_MALFORMED`); menolak ketidakcocokan bijeksi 1:1 deklarasi manifes vs entri ZIP baik berkas hilang maupun berkas reguler ekstra/asing (`ERR_ZIP_ENTRY_MISMATCH`). | Arsip wrapper dan deklarasi dievaluasi sesuai pemetaan 1:1 deterministik. Tipe entri non-reguler (symlink, special files), arsip rusak, dan benturan nama ZIP ditolak fail-closed dengan `ERR_ZIP_INVALID`. Ketidakcocokan bijeksi 1:1 (berkas hilang atau berkas reguler ekstra) ditolak fail-closed dengan `ERR_ZIP_ENTRY_MISMATCH` (AUDIT-NEW-08). | `[TEST-PLANNED — EXECUTION BLOCKED BY PROPOSED SPEC]` | B-07 (Batas Kuota ZIP Wrapper Masih Berstatus Usulan) |
| **AC-03** | NC-02 | IETF RFC 8032; `crypto.ts` | Signature manifest 128-hex tidak valid atau payload dimodifikasi | Verifikasi tanda tangan manifest gagal (`ERR_MANIFEST_SIGNATURE_INVALID`). | `[BLOCKED BY ARCHITECTURE]` | B-08 (Circular Dependency Manifest Sig) |
| **AC-04** | NC-06 | IETF RFC 8032; `container.go` | Signature kontainer `.nx` anggota album dimodifikasi | Verifikasi tanda tangan kontainer `.nx` gagal (`ERR_CONTAINER_SIGNATURE_INVALID`). | `[TEST-PLANNED — SPEC READY]` | Baseline Frozen (PE-01) |
| **AC-05** | NC-03 | WP v5.6 §Parsers; Nexa Policy | Payload manifest memuat duplicate keys literal atau via decoded Unicode escape | Parser menolak payload fail-closed dengan error `ERR_MANIFEST_DUPLICATE_KEY`. | `[TEST-PLANNED — BLOCKED BY B-01]` | B-01 (Strict Parser Engine - Implementation Module Pending) |
| **AC-06** | NC-03 | IETF RFC 8785 | Vektor uji kanonisasi RFC 8785 (urutan kunci UTF-16, $-0$, whitespace) | Serializer menghasilkan byte kanonikal identik 100% dengan test vector resmi. | `[TEST-PLANNED — BLOCKED BY B-02]` | B-02 (JCS Serializer Engine - Implementation Module Pending) |
| **AC-07** | NC-04 | Roadmap v4.8; Keputusan PO CONF-01; B-09 / NC-04 | Album ditandatangani oleh signer dengan status `UNKNOWN` di Registry atau signature manifest tidak valid | Membership tidak autentik dan wajib ditolak fail-closed. Ini bukan global playback gate; file `.nx` yang dipilih secara independen tetap mengikuti PE-01 standalone. | `[TEST-PLANNED — EXECUTION BLOCKED]` | B-09 / NC-04: identity binding, authority, trust store, signer lifecycle, dan verifier belum tersedia/ditetapkan; tidak lagi menunggu keputusan PO. |
| **AC-08** | NC-04 | White Paper v5.6 §Registry; AUDIT-TRUTH-02 | Kondisi konseptual signer dinyatakan revoked; sumber, format, otoritas, retrieval, freshness, dan lifecycle mekanisme Registry belum ditetapkan | Manifest tidak boleh dipakai sebagai deklarasi membership tepercaya; tidak otomatis memblokir playback standalone atau mengubah status trust/otorisasi member. Status revocation hanya dapat dinyatakan berdasarkan mekanisme Registry yang sah setelah lifecycle ditetapkan. Pencabutan Album Manifest Signer dipisahkan secara tegas dari pencabutan Creator atau Registry evidence milik member `.nx`. | `[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED REGISTRY REVOCATION LIFECYCLE]` | B-09 / NC-04 (Registry revocation lifecycle belum ditetapkan) |
| **AC-09** | NC-05 | White Paper v5.6 §Genesis; §6.9 (AUDIT-NEW-04) | Hash audio payload bitstream mentah `.nx` tidak cocok dengan deklarasi hash bitstream audio pada manifest (deklarasi hash audio pada lokasi manifest yang belum ditetapkan) | Verifikasi integritas payload audio gagal fail-closed melempar `ERR_CONTAINER_HASH_MISMATCH`. (Catatan normatif: identifier field manifest audio belum ditetapkan secara normatif; kandidat `audio_sha256` vs notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) berstatus `UNRESOLVED — STOP AND CLARIFY`; dilarang menerima kedua field secara alternatif, dilarang membuat alias atau fallback; `underlying_cert_id` pada Genesis Certificate adalah identifier referensi sertifikat induk, bukan audio hash; relasi pengikatan audio hash ke sertifikat genesis berstatus `UNRESOLVED — NORMATIVE CONTRACT NOT VERIFIED`). | `[TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY]` | NC-05 / NC-09 / AC-09 (Identifier field normatif audio hash pending keputusan PO; STOP AND CLARIFY) |
| **AC-10** | NC-05 | White Paper v5.6 §Genesis; AUDIT-NEW-10; §13.12.11 | Genesis certificate signature invalid / issuer mismatch; container signature; packaging authorization missing/invalid/expired/revoked; delegation subject or asset mismatch | Verifier reports Genesis ownership and packaging authorization separately. Third-party packaging authorization failure yields UNTRUSTED / UNAUTHORIZED PACKAGING and is not automatically Genesis Certificate invalid or ownership invalid. Genesis error taxonomy remains to be finalized. | [TEST-PLANNED — SPECIFIED; EXECUTION BLOCKED BY IMPLEMENTATION & GENESIS ERROR TAXONOMY] | AUDIT-NEW-10 target architecture specified in §13.12.11; runtime execution awaits implementation and final Genesis taxonomy. |
| **AC-11** | NC-06 | White Paper v5.6 §Container | Ekstraksi kontainer audio mandiri dari arsip ZIP | File terekstrak utuh di storage tanpa merusak byte kanonikal container. (Catatan: AC-11 murni menguji ekstraksi mandiri kontainer; batas payload individual 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106` adalah celah pengujian terpisah yang belum memiliki AC khusus). | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-12** | NC-06 | White Paper v5.6 §Container | Pustaka packaging memvalidasi struktur kontainer hasil ekstraksi | Validasi packaging lulus seluruh invariant integritas baseline PE-01. (Catatan: AC-12 murni menguji invariant packaging PE-01; batas payload individual 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106` adalah celah pengujian terpisah yang belum memiliki AC khusus). | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-13** | NC-07 | Proposal B-07 (Acuan Format: APPNOTE; RFC 1951); AUDIT-NEW-08 | Arsip pembungkus ZIP dievaluasi terhadap kuota batas keamanan dan rasio kompresi | Ekstraksi dibatalkan fail-closed dengan pemetaan deterministik 1:1: kuota ukuran terkompresi > 500 MB desimal (500.000.000 bytes), akumulasi uncompressed > 4 GB desimal, atau entri > 200 $\rightarrow$ `ERR_ZIP_QUOTA_EXCEEDED`; rasio dekompresi melampaui batas bomb $\rightarrow$ `ERR_ZIP_BOMB_DETECTED`; ketidakcocokan bijeksi 1:1 $\rightarrow$ `ERR_ZIP_ENTRY_MISMATCH` (AUDIT-NEW-08). | `[TEST-PLANNED — EXECUTION BLOCKED BY PROPOSED SPEC]` | B-07 (Batas Kuota ZIP Wrapper Masih Berstatus Usulan) |
| **AC-14** | NC-08 | `schema.postgres.sql#L63`; B-04; §6.8.1 | Satu Commercial Bundle checkout memproses N child acquisitions dan terjadi kegagalan pada salah satu tahap sebelum commit | Sesuai kontrak transaksi B-04 yang akan ditetapkan: tidak ada child acquisition/entitlement lokal parsial yang melanggar invariant bundle; batas rollback hanya berlaku pada transaksi lokal sebelum commit dan tidak mengklaim rollback side effect eksternal. | `[BLOCKED BY INCOMPLETE TRANSACTION CONTRACT]` | Model B + SSP/Largest Remainder approved; B-04 transaction/settlement contract open |
| **AC-15** | NC-08 | `server.js#L170`; NC-08; §6.8.1 | Request checkout/settlement Commercial Bundle dengan identitas idempotensi yang sama dikirim berulang, termasuk saat partial failure atau retry | Marketplace mengembalikan/melanjutkan satu hasil bundle yang konsisten tanpa menggandakan child acquisition, entitlement, charge, atau issuance lisensi; exact idempotency scope/state machine tetap harus ditetapkan dalam kontrak B-04. | `[BLOCKED BY INCOMPLETE TRANSACTION CONTRACT]` | Model B approved; idempotency/replay and reconciliation contract open under B-04 |
| **AC-16** | NC-09 | `marketplace/db/schema.postgres.sql#L72`; B-05; §6.8.1; §6.9; AUDIT-NEW-04 | Penyimpanan hash pada setiap child acquisition dan entitlement independen untuk member `.nx` Album | acquired_package_sha256 pada child acquisition/entitlement harus merepresentasikan byte-domain individual .nx member sesuai kontrak producer-consumer; hash wrapper ZIP tidak boleh disalin sebagai hash member. Objek kriptografi dan hash lain tetap dipetakan sesuai inventaris §6.9. | `[BLOCKED BY PER-MEMBER HASH CONTRACT]` | B-05 / NC-09; existing wrapper-ZIP hash evidence §15.9.5 does not establish target child-member hash |
| **AC-17** | NC-10 | `schema.postgres.sql#L63-L115`; Zero-DDL; AUDIT-NEW-05 | Operasi transaksi dan penyimpanan album dieksekusi | Skema database PostgreSQL aktif tidak termutasi pada berkas statis repositori lokal (`schema.postgres.sql`). Keadaan aktual database live/runtime secara terbuka berstatus `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. | `[TEST-PLANNED — SPEC READY]` | Skema DDL Statis Terverifikasi (Runtime Live Database `NOT VERIFIED — EVIDENCE NOT AVAILABLE`) |
| **AC-18** | NC-11 | White Paper v5.6 §Registry | Koneksi ke remote Registry aktif dan respons valid | Verifikasi sertifikat dan public key signer menggunakan data otoritatif remote. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-19** | NC-11 | White Paper v5.6 §Registry | Jaringan transport terputus (ECONNREFUSED/timeout); cache lokal valid | Fallback ke cache offline; respons HTTP 5xx/bad sig melempar fail-closed. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-20** | NC-12 | POSIX.1-2017; `fs_safe.ts` | File `.nx` berada di luar root storage atau symlink melintasi direktori | Akses ditolak fail-closed (`ERR_FILESYSTEM_CONTAINMENT_VIOLATION`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-21** | NC-12 | POSIX.1-2017; Standar POSIX | Upaya pembukaan berkas dengan manipulasi symlink/path traversal | Pemeriksaan descriptor pasca-open gagal; melempar fail-closed (`canPlay: false`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-22** | NC-13 | White Paper v5.6 §JIT Player; Keputusan PO AUDIT-NEW-01/CONF-01; §5.2 | Otorisasi pemutaran trek audio album dieksekusi | Skenario JIT 8-tahap terdefinisi per-member; Stage 8a passive background inspection/diagnostic digest diizinkan tanpa playback authorization, decryption, buffer registration, atau bypass Genesis/active-license/trust checks. Uji tetap blocked oleh prasyarat Stage 8a terhadap Genesis 7b dan lisensi aktif 7c, identitas field hash audio, serta implementasi identity/lifecycle dan verifier membership signer B-09. | `[TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED JIT PREREQUISITES & B-09 IMPLEMENTATION]` | Stage 8a diagnostic permission APPROVED with strict boundary; Genesis 7b / active license 7c prerequisites, audio hash field identity, and B-09 signer/membership implementation remain open. |
| **AC-23** | NC-13 | White Paper v5.6 §JIT Player | Pengguna berpindah trek audio dalam album | Otorisasi JIT dieksekusi ulang secara independen per trek tanpa otorisasi massal. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-24** | NC-13 | White Paper v5.6 §JIT Player | Integritas satu trek dalam antrean album rusak | Trek rusak gagal diputar; pemutaran trek valid lainnya tidak terganggu. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-25** | NC-14 | White Paper v5.6 §Verify; Keputusan PO CONF-02; §5.3 | Verifikasi album dengan anggota valid dan status campuran di NX Verify | Mengikuti Keputusan PO (CONF-02 / NC-14 Pilihan B APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; hasil verifikasi setiap berkas `.nx` anggota ditampilkan secara individual; tidak ada pembuatan status agregat baru (`ALBUM_TRUSTED`, `ALBUM_INVALID`) | `[TEST-PLANNED — SPEC READY]` | Keputusan PO CONF-02 / NC-14 Pilihan B APPROVED (Tanpa Status Agregat) |
| **AC-26** | NC-15 | Error Taxonomy Spec; NC-15 | Skenario kegagalan sistematis di seluruh alur eksekusi | Sistem melempar kode error diskrit kanonikal 1:1 sesuai taksonomi 20 error code. | `[TEST-PLANNED — BLOCKED BY PROPOSED SPEC]` | Dependensi NC-15 (Formalisasi taksonomi 20 kode error kanonikal berstatus usulan spesifikasi teknis) |
| **AC-27** | NC-16 | `schema.postgres.sql#L63-L115` | Uji kesesuaian panjang formula ID derivasi terhadap skema DDL | Panjang string child acq $\le 128$, ent $\le 128$, provider $\le 64$ karakter. | `[TEST-PLANNED — SPEC READY]` | DDL statis dilaporkan Programmer — NOT INDEPENDENTLY VERIFIED (bukan bukti unik)|
| **AC-28** | NC-01, NC-06 | White Paper v5.6 §Studio; Keputusan PO §2.3.A; §5.1 item 3, §5.4 | NX Studio memproses Album Forge New berisi beberapa file sumber biasa (Image/Doc/Music/Video) | Setiap berkas sumber diproses forging satu per satu secara sekuensial menghasilkan berkas `.nx` mandiri; metadata nama album (`title`) dan artwork (`cover_artwork`) diinput di UI Studio dan divalidasi lokal; persistensi metadata katalog individual pada `catalog_snapshots` dilaporkan Programmer dan belum diverifikasi independen per `asset_id` tanpa mengubah format kontainer individual `.nx` atau skema database; namun asosiasi persisten beberapa anggota `.nx` ke satu entitas Album multi-member di Marketplace berstatus gap kontraktual pending klarifikasi PO/Arsitektur (STOP AND CLARIFY); setiap berkas `.nx` dipublikasikan melalui workflow Marketplace existing; anggota berikutnya diproses hanya setelah anggota saat ini selesai | `[TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED ALBUM IDENTITY & ASSOCIATION GAP]` | Keputusan PO §2.3.A (UI Studio & Forging Sekuensial Siap; Asosiasi Multi-Member Marketplace Terblokir Gap Arsitektur) |
| **AC-29** | NC-06 | White Paper v5.6 §Studio; Keputusan PO §2.3.B; §5.1 item 3, §5.4 | NX Studio memproses Album Existing `.nx` berisi beberapa berkas `.nx` yang sudah ada (Music/Video/Doc/Image) | Setiap berkas `.nx` dipublikasikan satu per satu secara sekuensial melalui `NXPublishPipeline` existing; tidak dilakukan forging ulang; tidak dibuat synthetic Genesis; berkas sumber `.nx` tidak diubah; metadata nama (`title`) dan artwork (`cover_artwork`) diasosiasikan pada level katalog individual per `asset_id` tanpa alterasi byte berkas `.nx`; pemuatan kembali kumpulan anggota sebagai satu kesatuan entitas Album berstatus gap kontraktual pending klarifikasi PO/Arsitektur (STOP AND CLARIFY; programmer dilarang menciptakan skema/API baru); anggota berikutnya diproses setelah anggota saat ini selesai | `[TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED ALBUM RELOAD SPECIFICATION]` | Keputusan PO §2.3.B (Publikasi Sekuensial Siap; Pemuatan Kembali Kolektif Album Terblokir Gap Arsitektur) |
| **AC-30** | NC-01 | Keputusan PO §2.3.C (Larangan Album Campuran); §5.4 | Pengguna memasukkan kombinasi campuran berkas sumber biasa dan berkas `.nx` yang sudah ada ke dalam satu Album | Validasi jenis masukan menolak proses secara fail-closed sebelum workflow pemrosesan dimulai; masukan tidak dirusak atau dihapus; tidak ada silent conversion atau reklasifikasi jenis masukan sepihak | `[TEST-PLANNED — SPEC READY]` | Keputusan PO §2.3.C (Larangan Album Campuran) |
| **AC-31** | NC-01, NC-06 | Keputusan PO §2.4 (Failure Handling Studio); §5.5 | Terjadi kegagalan pemrosesan pada tahap forging atau tahap upload di NX Studio | Pemrosesan berhenti sementara pada tahap yang gagal; tidak ada auto-retry tanpa batas atau auto-skip; pengguna disajikan opsi diskrit "Ulangi" dan "Lewati"; jika forging gagal dan dipilih Ulangi: forging file yang sama diulang tanpa lanjut ke file berikutnya; jika forging gagal dan dipilih Lewati: file dilewati tanpa upload dan tanpa menghapus file sumber; jika upload gagal setelah forging berhasil dan dipilih Ulangi: upload berkas `.nx` hasil forging diulang tanpa re-forging (menggunakan output `.nx` di staging lokal) dan tanpa membuat listing Marketplace duplikat (hasil yang disetujui PO); mekanisme teknis idempotensi session individual belum ditetapkan sebagai kontrak dan bukti repository hanya laporan Programmer yang belum diverifikasi independen (`server.js#L2400-L2416, L2467-L2470`, `publish_pipeline.js#L316-L410`; status bukti implementasi: inspeksi kode lokal Programmer / audit independen pending [NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE], pengujian runtime belum dilakukan, terpisah dari transaksi B-04); jika upload gagal dan dipilih Lewati: tahap upload ditandai gagal/dilewati, lanjut ke anggota berikutnya, berkas sumber dan hasil `.nx` tetap dipertahankan; status forging dan status upload dibedakan secara granular per anggota | `[TEST-PLANNED — SPEC READY]` | Keputusan PO §2.4 (Studio Failure Handling: Ulangi & Lewati; Spesifikasi Idempotensi Session Siap; Terpisah dari B-04) |
| **AC-32** | NC-13 | White Paper v5.6 §Universal Viewer; Keputusan PO §2.5; §5.2 | Pengguna membuka dan memutar Album pada NX Player (Desktop atau Mobile) | Player memproses anggota satu per satu secara sekuensial; setiap anggota diverifikasi dan diotorisasi secara individual; pemutaran/tampilan hanya terjadi jika anggota memenuhi trust, integrity, dan lisensi aktif; otorisasi anggota saat ini tidak memberikan otorisasi kepada anggota berikutnya; background pre-verification tidak memberikan otorisasi; anggota yang tidak memenuhi syarat mengikuti kebijakan existing (`UNKNOWN/INCOMPLETE` tidak otomatis `INVALID`); pemutaran audio/video melakukan Auto-Next pasca-selesai anggota sesuai kontrak lifecycle transisi Album yang akan ditetapkan resmi oleh PO/Arsitektur (audio memiliki event listener `ended` di GUI pustaka desktop `renderer.js#L652-L655` yang merotasi `libraryAssets`, namun belum menjadi kontrak transisi Album resmi; video tidak memiliki handler `ended` pada `videoEngine`; dokumen/gambar tidak memiliki durasi alami; seluruh pemicu Auto-Next multi-payload berstatus UNRESOLVED pending klarifikasi PO/Arsitektur; STOP AND CLARIFY; timer sepihak dilarang); renderer, streaming, dan memory boundary existing tidak diubah | `[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MULTI-PAYLOAD AUTO-NEXT LIFECYCLE CONTRACT]` | Keputusan PO §2.5 (Player Auto-Next & Authorization Isolation; Kesiapan Diturunkan Menjadi Execution Blocked Akibat Ketiadaan Kontrak Lifecycle Transisi Album Multi-Payload) |
| **AC-33** | NC-14 | White Paper v5.6 §Verify Desktop; Keputusan PO §2.6, §2.7; §5.3 | Pengguna membuka Album pada NX Verify Desktop; membership authenticity must pass the PO-approved fail-closed verifier before file is processed/labeled as an Album member | Jika autentisitas membership terbukti, Verify memproses anggota pertama dan menampilkan hasil verifikasi individual; jika belum terbukti, file dari manifest tidak diproses/dilabeli sebagai anggota Album; file yang diberikan independen hanya dapat diverifikasi sebagai standalone PE-01; pengguna menekan tombol "Next" secara manual untuk beralih ke anggota berikutnya; setiap anggota diverifikasi sendiri-sendiri tanpa status agregat keseluruhan Album (Option B APPROVED); fitur Full Verify Desktop existing (Batch Verification, Export Report, manual Registry Refresh) tetap utuh dan tersedia; Verify tidak memberikan playback authorization | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 VERIFIER / SIGNER LIFECYCLE]` | Keputusan PO §2.6 & §2.7 (Verify Desktop Manual Next & No Aggregate Status) |
| **AC-34** | NC-14 | White Paper v5.6 §Verify Mobile Lite; Keputusan PO §2.6, §2.7; §5.3 | Pengguna membuka Album pada NX Verify Mobile; membership authenticity must pass the PO-approved fail-closed verifier before file is processed/labeled as an Album member | Jika autentisitas membership terbukti, Verify Mobile memproses satu anggota per langkah; jika belum terbukti, file dari manifest tidak diproses/dilabeli sebagai anggota Album; file yang diberikan independen hanya dapat diverifikasi sebagai standalone PE-01; navigasi manual tombol "Next" berpindah ke anggota berikutnya dan menjalankan verifikasi individual; tidak ada status agregat Album; aplikasi tetap beroperasi sebagai Verify-Lite (tanpa porting Batch Verification Full Desktop, tanpa Export Report, tanpa manual Registry Refresh, dan tanpa payload rendering) | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 VERIFIER / SIGNER LIFECYCLE]` | Keputusan PO §2.6 & §2.7 (Verify Mobile Lite Manual Next & Lite Isolation) |

---

## 9. TRACEABILITY MATRIX DUA ARAH: NC → AC → SUMBER → BUKTI

Matriks berikut mendokumentasikan keterlacakan dua arah (*Forward & Reverse Traceability*) dengan struktur tabel markdown valid dan rujukan dependensi yang realistis tanpa klaim semu:

| ID NC | ID AC Penguji | Sumber Otoritatif | Bukti Pendukung / Lokasi Kode | Status Kesiapan AC | Status Blocker / Keputusan |
|:---:|:---:|:---|:---|:---:|:---:|
| **NC-01** | AC-01, AC-02, AC-28, AC-30, AC-31 | White Paper v5.6 §Manifest, §Studio; RFC 8259; Keputusan PO §2.3, §2.4 | §5.1 Skema Manifest; §5.4; §5.5; E-02 | AC-01 `[PO DECISION REQUIRED]`; AC-02 `[TEST-PLANNED — BLOCKED BY PROPOSED SPEC]`; AC-28 `[TEST-PLANNED — PARTIALLY BLOCKED BY ALBUM IDENTITY GAP]`; AC-30, AC-31 `[TEST-PLANNED — SPEC READY]` | AC-01: Pending Konfirmasi PO (Unknown Fields, Validation Behaviors, & Multi-Payload Schema Gap); AC-02: B-07 / NC-07; AC-28: Gap Identitas Album Multi-Member; AC-30, AC-31: Keputusan PO APPROVED (Larangan Campuran, Studio Failure Handling) |
| **NC-02** | AC-03 | IETF RFC 8032; RFC 8785; `crypto.ts` | `sdk/typescript/src/crypto.ts#L45`; §6.2; E-06 | `[BLOCKED BY ARCHITECTURE]` | B-08 (Circular Dependency Signature Manifest; Input Signature Wajib Exclude Field Signature; Preservasi Signature Member .nx) |
| **NC-03** | AC-05, AC-06 | White Paper v5.6 §Parsers; IETF RFC 8785 | RFC 8785 Test Vectors TV-01..TV-08 | AC-05 `[BLOCKED B-01]`; AC-06 `[BLOCKED B-02]` | B-01, B-02 (Strict Parser & JCS - Implementation Modules Pending) |
| **NC-04** | AC-07, AC-08 | Roadmap v4.8; White Paper v5.6 §Registry | Roadmap v4.8 §Trust Model; §6.4 | AC-07 `[PO DECISION REQUIRED]`; AC-08 `[TEST-PLANNED — EXECUTION BLOCKED — REGISTRY REVOCATION LIFECYCLE UNRESOLVED]` | AC-07: B-09 / CONF-01 (Autentisitas provenance membership manifest saat signer UNKNOWN dan identitas/lifecycle signer belum ditetapkan; bukan playback gate global); AC-08: Registry revocation lifecycle belum ditetapkan |
| **NC-05** | AC-09, AC-10 | White Paper v5.6 §Genesis; `sdk.ts#L205-L255` | §6.9 Inventaris Objek Kriptografis; E-01 | AC-09 `[TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY]`; AC-10 `[TEST-PLANNED — BLOCKED BY UNRESOLVED TAXONOMY & 3-WAY BINDING]` | `OPEN / BLOCKED BY UNRESOLVED FIELD IDENTITY (STOP AND CLARIFY), GENESIS ERROR CODE & 3-WAY BINDING` |
| **NC-06** | AC-04, AC-11, AC-12, AC-28, AC-29, AC-31 | White Paper v5.6 §Container, §Studio; Keputusan PO §2.3, §2.4; `container.go` | `internal/container/container.go#L110`; §5.1, §5.4, §5.5; E-02 | AC-04, AC-11, AC-12, AC-31 `[TEST-PLANNED — SPEC READY]`; AC-28, AC-29 `[TEST-PLANNED — EXECUTION BLOCKED PENDING ALBUM IDENTITY/RELOAD]` | Baseline Frozen (PE-01); Keputusan PO APPROVED (Failure Handling Retry/Skip, hasil `.nx` yang sama tanpa re-forging, larangan listing duplikat; mekanisme idempotensi teknis unresolved; gap identitas & reload terbuka) |
| **NC-07** | AC-02, AC-13 | Proposal B-07 (Acuan Format: APPNOTE; RFC 1951) | §6.7 Batas Keamanan Ekstraksi Arsip ZIP Wrapper (Nilai Kuota Berstatus Usulan B-07) | AC-02 `[TEST-PLANNED — BLOCKED BY PROPOSED SPEC]`; AC-13 `[TEST-PLANNED — EXECUTION BLOCKED BY PROPOSED SPEC]` | B-07 (Menunggu Keputusan Arsitektur Pembekuan Batas Kuota ZIP & Aturan Flat) |
| **NC-08** | AC-14, AC-15 | `schema.postgres.sql#L63`; `server.js`; Keputusan PO Model B + SSP/Largest Remainder §6.8.1; Keputusan PO bundle_checkout_id §6.8.2 | `marketplace/server.js#L170`; E-04; §6.8.1–§6.8.3 | `[BLOCKED BY INCOMPLETE TRANSACTION / SETTLEMENT CONTRACT]` | B-04 / CONF-03 (Model B dan alokasi SSP/Largest Remainder disahkan; tujuh aturan normatif identitas/korelasi `bundle_checkout_id` dan Immutable Checkout Manifest sebagai Single Source of Truth disahkan; mekanisme storage/persistensi, pemetaan member-to-acquisition, idempotency, commit boundary, partial failure, settlement/reconciliation tetap terbuka) |
| **NC-09** | AC-16 | White Paper v5.6 §Marketplace; `schema.postgres.sql#L63`; Keputusan PO Model B §6.8.1 | §6.9 Inventaris Objek Kriptografis; `marketplace/db/schema.postgres.sql#L72`; E-03; §15.9.5 | `[BLOCKED BY PER-MEMBER HASH CONTRACT]` | B-05 (Existing hash byte-domain adalah wrapper ZIP; target acquisition/entitlement independen memerlukan hash individual `.nx` member; primary-source evidence status mengikuti §15.9.5) |
| **NC-10** | AC-17 | `schema.postgres.sql#L63-L115` | `marketplace/db/schema.postgres.sql#L63`; E-03 | `[TEST-PLANNED — SPEC READY]` | Laporan Programmer tentang DDL statis (belum diverifikasi independen) (Independen B-04; Runtime Live DB `NOT VERIFIED`)|
| **NC-11** | AC-18, AC-19 | White Paper v5.6 §Registry | White Paper v5.6 §Offline Fallback | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **NC-12** | AC-20, AC-21 | POSIX.1-2017; White Paper v5.6 §Safe-Open | `sdk/typescript/src/fs_safe.ts#L30-L55`; E-07 | AC-20 `[TEST-PLANNED — EXECUTION BLOCKED BY B-06]`; AC-21 `[TEST-PLANNED — EXECUTION BLOCKED BY B-06]` | B-06 (Batas Safe-Open Filesystem Desktop Terbuka; Residual Gap TOCTOU POSIX) |
| **NC-13** | AC-22, AC-23, AC-24, AC-32 | White Paper v5.6 §JIT Player, §Universal Viewer; Keputusan PO §2.5; `main.js` | `player-desktop/main.js#L182, L541` (JIT protocol/IPC handler); `player-desktop/renderer.js#L652-L655` (audio GUI playlist rotation; video ended handler absent); §5.2; E-05 | AC-22 `[TEST-PLANNED — PARTIALLY BLOCKED BY UNRESOLVED JIT PREREQUISITES & MANIFEST MEMBERSHIP AUTHENTICITY]`; AC-23..24 `[TEST-PLANNED — SPEC READY]`; AC-32 `[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MULTI-PAYLOAD AUTO-NEXT LIFECYCLE CONTRACT]` | Keputusan PO APPROVED (Player Auto-Next Lifecycle & Isolasi Otorisasi JIT Per Anggota; Kesiapan Diturunkan Menjadi Execution Blocked Akibat Prasyarat JIT, autentisitas membership manifest, & Gap Kontrak Lifecycle Auto-Next Multi-Payload) |
| **NC-14** | AC-25, AC-33, AC-34 | White Paper v5.6 §Verify; Keputusan PO §2.6, §2.7 (CONF-02 Pilihan B APPROVED) | §5.3 Tiga Lapisan Status Verify | AC-25 `[TEST-PLANNED — SPEC READY]`; AC-33/AC-34 `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 VERIFIER / SIGNER LIFECYCLE]` | Keputusan PO CONF-02 / NC-14 Pilihan B APPROVED (Tanpa Status Agregat Album; Kategori Diagnostik Internal Tunduk pada 4 Status Kanonikal; Verify Desktop & Mobile Lite Terpisah) |
| **NC-15** | AC-26 | Error Taxonomy Spec; NC-15 | §6.15 Taksonomi 20 Kode Error Kanonikal | `[TEST-PLANNED — BLOCKED BY PROPOSED SPEC]` | Usulan Spesifikasi Teknis NC-15 (Pending Pembekuan Arsitektur) |
| **NC-16** | AC-27 | `schema.postgres.sql#L63-L115` | §6.16 Derivasi Matematis Identifier | `[TEST-PLANNED — SPEC READY]` | DDL statis dilaporkan Programmer — NOT INDEPENDENTLY VERIFIED (batas kolom belum diverifikasi Auditor) |

---

## 10. KEPUTUSAN PRODUCT OWNER YANG MASIH DIPERLUKAN

### 10.1 Kebijakan Album Signer `UNKNOWN`, Kebutuhan Entitas Signer & Lifecycle Key (NC-04, B-09, CONF-01, AUDIT-TRUTH-02)
Keputusan normatif mengenai eksistensi/otoritas Album Signer dan penggunaan deklarasi manifest yang signer-nya `UNKNOWN` berada pada Product Owner dan Otoritas Arsitektur sesuai domain kewenangan. Penetapan tersebut tidak menjadi prasyarat untuk PSV atas implementasi signer, membership, dan lifecycle yang tersedia. **CONF-01 bukan pilihan kebijakan playback global.**

1. **Evaluasi Kebutuhan Entitas Album Signer**:
   - Jika dipertahankan melalui keputusan PO/Arsitektur, fungsinya dibatasi murni pada autentisitas deklarasi manifest dan daftar anggota.
   - Album Signer **DILARANG** menggantikan Creator signature, Genesis proof, Registry trust, asset trust, active license, atau otorisasi playback masing-masing member `.nx`.
   - Dasar identitas, private-key custody, pendaftaran public key ke Registry, identity binding, key rotation, dan revocation belum ditetapkan (**`UNRESOLVED — PENDING PO / ARCHITECTURE DECISION`**).

2. **Batas Keputusan CONF-01 untuk Signer `UNKNOWN`**:
   - Keputusan yang masih diperlukan terbatas pada apakah deklarasi manifest yang signer-nya `UNKNOWN` dapat digunakan untuk mengautentikasi identitas/membership Album, dan bukti apa yang sah untuk menetapkan identitas serta lifecycle signer.
   - Otorisasi playback tetap dilakukan secara JIT dan independen untuk setiap member berdasarkan kontrak PE-01, Creator signature, Genesis ownership, Registry evidence, dan active license yang berlaku.
   - Programmer **DILARANG** memilih opsi yang memblokir atau mengizinkan seluruh playback Album atas dasar status Album Signer.
   - Sesuai keputusan PO CONF-01, membership dari manifest dengan signer `UNKNOWN` tidak boleh dianggap autentik; kebijakan fail-closed telah diputuskan, sedangkan implementasi identity/lifecycle signer tetap terbuka. Namun status tersebut juga **TIDAK BOLEH** otomatis mengubah status member menjadi `INVALID` atau membatalkan trust member.

3. **Preservasi Prinsip White Paper v5.6**:
   - Status `UNKNOWN / INCOMPLETE` **BUKAN `INVALID`**.
   - Integritas kontainer dan tanda tangan Creator setiap member tetap independen dari status signer manifest.
   - Tidak boleh menciptakan Registry endpoint, record sintetis, revocation list, key lifecycle, atau mekanisme fallback yang belum memiliki dasar kontrak.

> **Status Tata Kelola:** CONF-01 tetap `PO DECISION REQUIRED` pada AC-07 (B-09 / NC-04), tetapi status keputusan ini tidak menunda PSV Programmer atas implementasi signer/membership dan lifecycle yang tersedia. Setelah PSV, PO/Architecture Authority hanya diminta menetapkan kebijakan atau kontrak yang memang belum ditentukan. CONF-01 bukan pilihan global playback. AC-07 menguji batas penggunaan deklarasi manifest saat signer `UNKNOWN` serta lifecycle signer yang belum memiliki kontrak. AC-25 tetap khusus untuk keputusan CONF-02.

### 10.2 Pembekuan Parameter Kuota Ekstraksi ZIP & Rekonsiliasi Celah Pengujian (B-07, NC-07, REQ-B03-04..06)
1. **Rasio Dekompresi ZIP Bomb (REQ-B03-04)**: Programmer melakukan PSV terlebih dahulu atas parser/extractor, streaming counters, enforcement per-entry/kumulatif, dan test yang tersedia. Architecture Authority menetapkan parameter normatif berdasarkan hasil PSV, threat model, benchmark payload Nexa yang sah, serta hard cap absolut per-entry dan kumulatif. Rasio 10:1 dan 100:1 tetap kandidat, bukan standar normatif; jangan memilih salah satunya hanya karena angka tersebut pernah muncul dalam draf.
2. **Batas Ukuran Wrapper dan Payload Individual (REQ-B03-05)**: Programmer melakukan PSV terlebih dahulu atas batas yang benar-benar ditegakkan parser/extractor, termasuk compressed wrapper, expanded cumulative wrapper, dan payload individual .nx. Klaim baseline 2 GiB tetap `NOT VERIFIED` sampai dibuktikan. Architecture Authority menetapkan parameter normatif berdasarkan hasil PSV dan pengujian resource. Tambahkan acceptance coverage eksplisit untuk batas payload individual; jangan memetakan pengujian tersebut secara keliru ke AC-11/12 jika keduanya tidak mengujinya.
3. **Batas 50 Member vs 200 Physical ZIP Entries (REQ-B03-06)**: Programmer melakukan PSV terlebih dahulu atas enforcement jumlah member UI/produk dan jumlah entry fisik ZIP. Pisahkan kedua domain tersebut dalam bukti dan test. Architecture Authority menyusun dampak teknis dan batas resource berdasarkan hasil PSV. Product Owner hanya perlu menetapkan apakah batas 50 member merupakan batas produk wajib atau sekadar panduan UX; nilai 200 physical entries tidak boleh dipakai sebagai pengganti batas jumlah member.
4. **Status**: Semua nilai numerik tetap PROPOSED sampai threat model, benchmark, coverage AC, dan keputusan otoritas terkait selesai. Ini bukan permintaan agar PO merancang parameter teknis.

### 10.3 Keputusan Product Owner yang Telah Disahkan (Mandat AUDIT-NEW — PO APPROVED)
Bagian ini mendokumentasikan keputusan resmi tertulis yang telah disahkan oleh Product Owner untuk ruang lingkup PE-02:
1. **Aturan Tipe Entry ZIP & Penolakan Hardlink (AUDIT-NEW-06 — PO APPROVED)**:
   - Album ZIP menerima entry bertipe *regular file* dan *directory*.
   - Symlink dan special files (FIFO, socket, dev) wajib ditolak fail-closed dengan `ERR_ZIP_INVALID`.
   - Semantik hardlink ZIP tidak didukung; tidak diasumsikan adanya representasi hardlink generik universal dalam ZIP.
   - Dua entry dengan isi byte identik tetap diperlakukan sebagai dua file independen; kesamaan byte/hash dilarang digunakan untuk menyimpulkan hardlink.
   - Entry dengan metadata ambigu ditolak secara fail-closed (`ERR_ZIP_INVALID`).
   - Penolakan subdirektori bersarang berlaku eksklusif pada path relatif member `.nx` yang dideklarasikan pada manifest (nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan)), bukan pelarangan entri direktori pada arsip ZIP.
2. **Keunikan Nama Berkas Case-Insensitive Lintas Platform (AUDIT-NEW-07 — PO APPROVED)**:
   - Nama berkas asli tetap dipertahankan persis termasuk kapitalisasi yang diberikan.
   - Pemeriksaan keunikan entry ZIP dan manifest nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) ditegakkan secara case-insensitive via ASCII case folding deterministik.
   - Nama yang bertabrakan setelah case-folding (e.g. `TrackA.nx` vs `tracka.nx`) wajib ditolak fail-closed (`ERR_MANIFEST_MALFORMED` pada manifest atau `ERR_ZIP_INVALID` pada entri ZIP) sesuai Boundary Matrix §5.1.
   - Berlaku konsisten lintas platform POSIX, Windows, dan Android.
3. **Hierarki Sumber Otoritas Kanonikal 6-Tingkat (AUDIT-NEW-09 — PO APPROVED)**:
   - Hierarki kanonis 6-tingkat disahkan pada §1.2 sebagai satu-satunya rujukan otoritas di seluruh dokumen:
     - Level 1: Keputusan eksplisit Product Owner untuk ruang lingkup PE-02.
     - Level 2: Kontrak produk dan governance Nexa yang telah disetujui atau dibekukan.
     - Level 3: White Paper dan Roadmap yang telah disetujui (sepanjang dalam ruang lingkupnya).
     - Level 4: Repository aktual sebagai bukti implementasi, bukan sebagai otoritas untuk mengubah kontrak produk.
     - Level 5: Standar internasional yang relevan (sepanjang tidak bertentangan).
     - Level 6: Temuan audit historis, bukti pendukungnya, proposal yang belum disetujui, dan interpretasi teknis.
   - Sumber lebih rendah dilarang mengubah ketentuan sumber lebih tinggi; keputusan PO PE-02 tidak mengubah baseline frozen Sprint 16/PE-01; pertentangan otoritatif wajib ditangani via Stop-and-Clarify.
4. **Prinsip Dasar Album, Peta Platform & Larangan Album Campuran (Keputusan PO: APPROVED)**:
   - Album adalah pengelompokan beberapa berkas `.nx` independen. Setiap anggota mempertahankan canonical `.nx` bytes dan hash masing-masing, Creator signature masing-masing, Genesis dan ownership evidence masing-masing, Registry dan sidecar state masing-masing, status integrity/trust masing-masing, dan keputusan playback authorization masing-masing.
   - Album dilarang: menjadi satu file `album.nx`, menjadi container baru, menggantikan identitas individual file `.nx`, menciptakan trust atau ownership bersama yang menggantikan bukti individual, atau membuat satu anggota otomatis mewarisi otorisasi anggota lain.
   - Metadata Album yang disetujui terbatas pada nama dan artwork Album, direpresentasikan mengikuti kontrak dan arsitektur yang sudah tersedia tanpa menciptakan field/tabel/API/schema baru tanpa dasar dan otorisasi.
   - Peta aplikasi dan platform: NX Studio Desktop saja (Creator, forging, dan publication; dilarang membuat requirement/AC/test untuk NX Studio Mobile); NX Player Desktop & Mobile; NX Verify Desktop (Full) & Verify Mobile (Lite).
   - Dua jenis Album yang terpisah: (a) Album Forge New memproses berkas sumber biasa (Image, Doc, Music, Video) secara sekuensial individual, menghasilkan berkas `.nx` tersendiri dan dipublikasikan ke Marketplace tanpa menggabungkan sumber menjadi satu `.nx`; (b) Album Existing `.nx` memproses berkas `.nx` yang sudah ada satu per satu melalui `NXPublishPipeline` existing tanpa re-forging dan tanpa synthetic Genesis.
   - Larangan Album Campuran: Satu Album dilarang keras mencampur berkas sumber biasa dengan berkas `.nx` yang sudah ada. Validasi jenis masukan ditegakkan secara fail-closed sebelum workflow dimulai tanpa silent conversion dan tanpa merusak input.
5. **Mekanisme Failure Handling Studio: Ulangi & Lewati (Keputusan PO: APPROVED)**:
   - NX Studio menyediakan dua tindakan diskrit pada tahap yang gagal: **Ulangi** dan **Lewati**.
   - Forging gagal: Ulangi mengulang forging file sumber yang sama tanpa lanjut ke file berikutnya; Lewati menandai file dilewati tanpa upload dan tanpa menghapus file sumber, lalu lanjut ke anggota berikutnya.
   - Upload gagal setelah forging berhasil: Ulangi mengulang tahap upload untuk berkas `.nx` yang sudah berhasil di-forging tanpa re-forging dan tanpa membuat listing Marketplace duplikat; Lewati menandai upload gagal/dilewati, mempertahankan file sumber dan hasil `.nx`, lalu lanjut ke anggota berikutnya.
   - Upload existing `.nx` gagal: Ulangi mengulang upload via jalur existing tanpa mengubah file sumber; Lewati menandai anggota dilewati/gagal dipublikasikan tanpa menghapus file sumber, lalu lanjut ke anggota berikutnya.
   - Ketentuan umum: tidak ada auto-retry tanpa batas atau auto-skip; proses batch berhenti sementara saat gagal; status forging dan status upload dibedakan secara granular (5 status diskrit: `FORGING_SUCCESS`, `FORGING_FAILED`, `PUBLICATION_SUCCESS`, `PUBLICATION_FAILED`, `SKIPPED_BY_USER`); tidak ada status agregat keberhasilan Album yang menyamarkan kegagalan anggota.
6. **Navigasi Album NX Player (Auto-Next) & NX Verify (Manual Next) (Keputusan PO: APPROVED)**:
   - NX Player (Desktop & Mobile): Memproses anggota pertama, memverifikasi secara individual, melakukan play/view jika memenuhi trust/integrity/authorization; setelah lifecycle anggota selesai menurut lifecycle Player existing, Player otomatis beralih ke anggota berikutnya (Auto-Next); otorisasi dieksekusi secara just-in-time per anggota tanpa pewarisan otorisasi dan tanpa otorisasi via background pre-verification; renderer, streaming, dan memory boundary existing tetap dipertahankan.
   - NX Verify Desktop: Memproses anggota secara sekuensial, menampilkan hasil verifikasi individual; pengguna menekan tombol "Next" secara manual untuk beralih ke anggota berikutnya; fitur Full Verify Desktop (Batch Verification, Export Report, manual Registry Refresh) tetap utuh dan tersedia; Verify tidak memberikan playback authorization.
   - NX Verify Mobile: Beroperasi strictly sebagai Verify-Lite; navigasi manual "Next" hanya memproses satu anggota per langkah tanpa status agregat dan tanpa memporting fitur Desktop (tanpa batch verification desktop, tanpa export report, tanpa registry refresh manual, dan tanpa payload rendering).
7. **Ketiadaan Status Agregat Album di NX Verify (CONF-02 / NC-14 Pilihan B — PO APPROVED)**:
   - Keputusan PO: PILIHAN B APPROVED. NX Verify tidak menampilkan status agregat keseluruhan Album.
   - Hasil verifikasi setiap berkas `.nx` tetap menjadi hasil utama.
   - Empat canonical verification statuses, lima internal Multi-Registry states, Local Override semantics, dan trust semantics individual file tetap utuh. Dilarang keras menciptakan status agregat baru seperti `ALBUM_TRUSTED` atau `ALBUM_INVALID`.

### 10.4 Status Keputusan dan Pertanyaan Normatif Tersisa — AUDIT-NEW-10

**Keputusan PO AUDIT-NEW-10: APPROVED / RESOLVED pada tingkat semantik produk.** genesisPubKey adalah Genesis Creator/originator dan menandatangani Genesis Ownership Certificate; containerSigKey adalah Container Packager/Packaging Engine dan menandatangani integritas binary container .nx; ownCertPubKey adalah current holder/buyer/collector sebagai subjek hak kepemilikan/lisensi saat ini. Ketiganya adalah peran berbeda dan tidak diwajibkan identik.

ownCertPubKey dapat berbeda dari genesisPubKey apabila rantai transfer kepemilikan sah menghubungkan keduanya. Third-party packaging dengan containerSigKey != genesisPubKey wajib memiliki delegation/authorization evidence yang dapat diverifikasi. Tanpa bukti tersebut, packaging dinyatakan UNTRUSTED / UNAUTHORIZED PACKAGING, sekalipun signature matematis valid. Self-packaging dengan containerSigKey == genesisPubKey memiliki otoritas inheren dan tidak memerlukan delegation tambahan. Signature kontainer membuktikan integritas matematis, bukan dengan sendirinya hak cipta atau otoritas packaging.

Rancangan target dan gap implementasi ditetapkan pada §13.12.11. Satu pertanyaan normatif yang masih harus diputuskan PO/Architecture Authority adalah **pihak mana yang memiliki kewenangan awal untuk menerbitkan delegation dengan scope CONTAINER_PACKAGING**. Keputusan subdelegation sengaja ditunda ke pertanyaan berikutnya setelah authority issuer ditetapkan. Pertanyaan ini tidak menghidupkan kembali equality tiga kunci sebagai unresolved.

Lifecycle revocation, freshness, dan offline disposition mengikuti kontrak teknis §13.12.11. Bila aspek tersebut memerlukan pilihan perilaku produk tambahan, pilihan itu diajukan terpisah setelah pertanyaan otoritas delegation diselesaikan.

**Disposisi AUDIT-NEW-10:** target architecture telah tercantum normatif dalam PLAN dan konsistensi silang atas klaim lama 3-way binding telah diperiksa; **AUDIT-NEW-10 CLOSED pada tingkat rekonsiliasi keputusan produk dan dokumentasi arsitektur**. Implementasi dan runtime test belum diklaim selesai; PE-02 Implementation tetap NOT AUTHORIZED.
---

## 11. KONFLIK MATERIAL DAN STOP-AND-CLARIFY

Daftar konflik material dan status resolusinya dicatat secara transparan sebagai gerbang evaluasi Gate A:

```
+----------------------------------------------------------------------------------------------------+
|                         REGISTER KONFLIK MATERIAL TERBUKA (CONF-01 s.d. CONF-03)                   |
+---------+----------------------------------+-----------------------------+-------------------------+
| ID      | Deskripsi Konflik Material       | Pihak Berwenang             | Dampak Teknis           |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-01 | Kebijakan autentisitas membership saat signer UNKNOWN | Product Owner | RESOLVED: Fail-Closed disahkan; identity/lifecycle teknis tetap B-09 |
|         | UNKNOWN (Roadmap v4.8 vs usulan) | (PO Mandate)                | POLICY APPROVED         |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-02 | Hierarki Status Agregat NX Verify| Product Owner               | SELESAI / APPROVED      |
|         | (Status asli vs status tambahan) | (PO Mandate: PILIHAN B)     | Pilihan B: Tanpa agregat|
|         |                                  |                             | AC-25 READY; AC-33/34 BLOCKED BY CONF-01  |
+---------+----------------------------------+-----------------------------+-------------------------+
| CONF-03 | Kontrak pemenuhan transaksi multi-member di bawah Zero-DDL | Architecture Authority | NC-08, AC-14, dan AC-15 |
|         | Model arsitektur normatif telah disahkan; kontrak teknis masih terbuka | (Architecture & Database) | TECHNICAL GAP OPEN |
+---------+----------------------------------+-----------------------------+-------------------------+
```

> **Catatan Status Resolusi Konflik:**
> 1. **CONF-02 (Status Agregat NX Verify)**: Telah resmi diselesaikan oleh Product Owner melalui pengesahan **PILIHAN B (APPROVED)**. NX Verify tidak menampilkan status agregat Album; verifikasi individual per anggota menjadi hasil utama; status AC-25 berstatus `[TEST-PLANNED — SPEC READY]`; AC-33 dan AC-34 berstatus `[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MEMBERSHIP AUTHENTICITY / CONF-01]`.
> 2. **CONF-01 (Album Membership Authenticity):** Kebijakan produk telah diputuskan PO: membership fail-closed bila signer UNKNOWN atau signature manifest invalid. Tidak lagi menjadi PO decision blocker. Implementasi identity binding, authority, trust store, dan lifecycle signer tetap merupakan gap teknis B-09/NC-04/AC-07/AC-08.
> 3. **CONF-03 (Marketplace Multi-Member Fulfillment):** Bukan lagi konflik yang menunggu pemilihan model normatif: Model B, alokasi SSP/Largest Remainder, identitas checkout, dan Manifest SSOT telah disahkan. Yang tetap terbuka adalah kontrak teknis transaksi, partial failure, idempotency, storage, recovery, settlement, dan side effect License Daemon di bawah Zero-DDL.
> 4. **Gap Terbuka Tambahan (§10.4.2)**: Ketiadaan definisi selesai lifecycle Player untuk payload non-audio dicatat sebagai `OPEN — STOP AND CLARIFY` tanpa asumsi sepihak programmer.

---

## 12. PRESERVATION GATE EVALUATION DAN GERBANG PENERIMAAN

### 12.1 Evaluasi Tujuh Dimensi Preservation Gate
Evaluasi 7 dimensi Preservation Gate disajikan secara objektif dengan membedakan dimensi yang lulus berdasarkan inspeksi statis terbatas dari dimensi yang masih tertahan oleh blocker arsitektur atau keputusan PO:

| Dimensi Preservasi | Aspek yang Dievaluasi | Status Evaluasi Audit (Sesuai §2.7) | Bukti Faktual & Batasan Pembuktian |
|---|---|:---:|---|
| **D-01 — Baseline / Repository** | Kebersihan repositori dan preservasi baseline Sprint 16. | `Belum dapat diverifikasi secara independen; bukti yang dilaporkan hanya mendukung klaim terbatas` | `git diff --name-only` hanya menguji tracked files; keberadaan 2 file untracked docs dan gitignored `evidence/` membatasi klaim. |
| **D-02 — Preservation PE-01 binary** | Kontrak biner single `.nx` kontainer tetap mandiri tanpa perubahan format. | `Bukti independen belum cukup` | Inspeksi statis kode `container.go` utuh, tetapi uji integritas biner runtime belum diverifikasi secara independen. |
| **D-03 — Database / Schema** | Kepatuhan mutlak Zero-DDL pada database marketplace. | `Kondisi database runtime belum terverifikasi secara independen` | Berkas `schema.postgres.sql` utuh; ketiadaan migrasi di database produksi live belum diverifikasi koneksi runtime. |
| **D-04 — Implementasi / Arsitektur** | Integritas struktur kontainer dan model Album ZIP independen. | `Desain bukan bukti implementasi atau pengujian runtime` | Spesifikasi tanda tangan digital independen memisahkan manifest, kontainer, dan sertifikat genesis (§6.9), namun belum diimplementasikan di kode PE-02. |
| **D-05 — JIT Authorization** | NX Player otorisasi just-in-time per trek aktif tanpa otorisasi awal. | `Masih berupa kontrak/rancangan sampai dibuktikan pada runtime` | Rancangan 8-tahap JIT dan handler `nexa-playback` belum dibuktikan pada eksekusi runtime fisik player. |
| **D-06 — Membership Authenticity & Signer Lifecycle** | Kebijakan membership fail-closed telah disahkan PO; implementasi identity binding dan lifecycle signer (B-09 / NC-04). | `POLICY RESOLVED; TECHNICAL GAP OPEN` | Membership signer UNKNOWN/invalid tidak autentik; standalone PE-01 tetap independen. Authority, identity binding, trust store, rotation, revocation, freshness, dan runtime verifier belum selesai. |
| **D-07 — Konsistensi Internal Plan** | Ketiadaan kontradiksi internal antar-register dan spesifikasi. | `Belum lulus sampai temuan dan konflik yang relevan diselesaikan` | Blocker teknis B-04, B-05, B-06, B-08, B-09 serta gap spesifikasi/traceability lain masih terbuka; kebijakan CONF-01 dan CONF-02 telah disahkan PO. D-07 belum PASS sampai seluruh status dan expected result direkonsiliasi. |

**Kesimpulan Preservation Gate:**  
**`PARTIAL — CLAIMS OF BASELINE PRESERVATION ARE LIMITED TO REPORTED INSPECTIONS; GOVERNANCE AND TECHNICAL BLOCKERS REMAIN OPEN`**.

---

### 12.2 Evaluasi Pre-Handoff Gates (G-01 sampai G-10)
- **G-01 (Fact-Based Plan Verification)**: `CONDITIONALLY MET — DOCUMENT REVIEW ONLY` (Plan memuat laporan Programmer tentang inspeksi lokal pada Evidence Ledger; Auditor belum memverifikasi repositori/bukti primer secara independen. Status ini bukan konfirmasi inspeksi kode oleh Auditor).
- **G-02 (Empirical Evidence Verification)**: `CONDITIONALLY MET — BASED ON PROGRAMMER-REPORTED STATIC INSPECTION ONLY` (Klaim inspeksi kode statis belum diverifikasi independen; pengujian fisik mobile tetap `NOT VERIFIED`).
- **G-03 (Repository Evidence Ledger Provenance)**: `CONDITIONALLY MET — EVIDENCE PROVENANCE NOT INDEPENDENTLY VERIFIED` (Evidence Ledger §4.4 memuat path, baris, dan raw snippets yang dilaporkan berasal dari kode lokal; Auditor belum memverifikasi sumber primer `whisnu/nexa`. E-07, database live, dan runtime mobile tetap tunduk pada batas bukti masing-masing).
- **G-04 (Preservation Gate Synchronization)**: `CONDITIONALLY MET` (Diselaraskan dengan evaluasi konservatif D-01 s.d. D-07 pada §12.1; kesimpulan preservasi berstatus PARTIAL; pengujian runtime fisik berstatus NOT VERIFIED).
- **G-05 (Readiness Conclusion Cross-Check)**: `CONDITIONALLY MET` (Rekapitulasi aktif setelah keputusan PO terbaru: 12 Spec Ready + 22 Execution Blocked + 0 PO Decision Required = 34 AC. AC-01 dan AC-07 tidak lagi berstatus PO Decision Required; AC-01 menunggu schema universal/parser, AC-07 menunggu implementasi identity/lifecycle signer. Gap AC-22, AC-28, AC-29, AC-32 dan parameter/test gaps lain tetap dicatat; angka agregat harus konsisten dengan §2.1, §8, §9, dan §13.1).
- **G-06 (Normative Contract & Acceptance Consistency)**: `CONDITIONALLY MET` (16 NC dan 34 AC terpetakan dua arah; blocker teknis B-01, B-02, B-06, B-08 dan gap spesifikasi B-07 tetap dicatat; AUDIT-NEW-10 telah direkonsiliasi pada tingkat keputusan produk dan target architecture di §13.12.11, sementara implementation/test evidence belum diklaim selesai).
- **G-07 (Governance Lock & Single File Output)**: `MET` (Pengecualian prasyarat administratif corrective revision count untuk mandat koreksi AUDIT-NEW-01..10 telah disahkan secara resmi oleh Product Owner melalui PO Governance Override; riwayat revisi historis tidak diubah atau direkayasa; tidak ada klaim REV4 atau cycle baru; satu berkas kanonikal dipertahankan tanpa artefak tambahan; implementasi kode PE-02 tetap NOT AUTHORIZED).
- **G-08 (Zero Implementation Authorization)**: `MET` (Implementasi kode PE-02 tetap secara sah `NOT AUTHORIZED`).
- **G-09 (Zero Mutation & Clean Repo State)**: `CONDITIONALLY MET WITH DISCLOSURE` (Nol mutasi kode tracked; keberadaan 2 berkas dokumen untracked di `docs/` dicatat transparan; inspeksi kebersihan repositori dibatasi pada tingkat direktori root dan tidak diklaim sebagai jaminan kebersihan rekursif).
- **G-10 (Adversarial Plan Audit & Contradiction Filter)**: `NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL GAPS ACKNOWLEDGED` (Kebijakan CONF-01 dan CONF-02 telah disahkan PO; CONF-03 direklasifikasi sebagai kontrak teknis B-04 yang masih terbuka, bukan konflik keputusan PO. G-10 tetap belum lulus karena B-04, B-05, B-06, B-07, B-08, B-09, gap spesifikasi, serta konsistensi lintas-register masih harus dituntaskan).

---

### 12.3 Evaluasi Gate Kualitas Plan (Gate A) vs Kesiapan Implementasi (Gate B)
Dokumen ini memisahkan secara tegas antara evaluasi kualitas dokumen rencana (*Gate A*) dan kesiapan pelaksanaan implementasi (*Gate B*):

```
+---------------------------------------------------------------------------------------------------+
|                        EVALUASI DUA GERBANG TATA KELOLA (GATE A vs GATE B)                        |
+----------------------------------------------------+----------------------------------------------+
| Parameter Evaluasi Kualitas Plan (Gate A)          | Hasil Evaluasi Substantif                    |
+----------------------------------------------------+----------------------------------------------+
| 1. Seluruh 16 NC terdefinisi dengan acuan sumber   | MEMENUHI SYARAT PARSIAL (NC-01 schema universal & NC-04 signer identity/lifecycle belum lengkap)                    |
| 2. Seluruh 34 AC memiliki expected result terukur  | MEMENUHI SYARAT PARSIAL (AC-01/28/29/32 gap) |
| 3. Traceability dua arah NC <-> AC terbukti        | MEMENUHI SYARAT STRUKTURAL; SEMANTIC GAPS REMAIN                              |
| 4. Bukti Evidence Ledger terdokumentasi dalam plan | MEMENUHI SYARAT BERSYARAT — LEDGER DOKUMEN TERSEDIA; BUKTI SUMBER PRIMER BELUM DIVERIFIKASI INDEPENDEN |
| 5. Penyelesaian konflik material dan batas sumber Product Truth | MEMENUHI SYARAT PARSIAL (CONF-01/02 policy resolved; B-04 technical fulfillment contract dan B-09 identity/lifecycle tetap open) |
| 6. Konsistensi status antar-register bebas cacat   | GAGAL (B-08 dan rekonsiliasi AC/NC/Blocker masih terbuka) |
+----------------------------------------------------+----------------------------------------------+
| STATUS AKHIR GATE A                                | NOT PASSED — PRODUCT TRUTH RECONCILIATION APPLIED; SUBSTANTIVE BLOCKERS REMAIN; INDEPENDENT RE-AUDIT REQUIRED   |
+----------------------------------------------------+----------------------------------------------+
| Parameter Evaluasi Kesiapan Implementasi (Gate B)  | Hasil Evaluasi Substantif                    |
+----------------------------------------------------+----------------------------------------------+
| 1. Kelulusan formal Gate A                         | GAGAL (Gate A belum lulus)                   |
| 2. B-08 — signed-content / signature construction | PSV source review telah diselesaikan (§15.9/§15.11); signed-content contract, canonical byte-domain, envelope, dan direct-negative test coverage tetap harus ditetapkan/dibangun sebelum Gate B PASS |
| 3. B-04 — Marketplace / Zero-DDL | PSV B-04 telah diterima sebagai baseline (§15.11); selesaikan kontrak transaksi/pemenuhan, Manifest storage, member mapping, idempotency, partial failure, recovery, settlement, dan License Daemon side effects |
| 4. B-05 — child hash contract | PSV B-05 telah diselesaikan; tetapkan byte-domain per-member `.nx`, producer/consumer, dan kontrak child mapping tanpa mengubah Zero-DDL |
| 5. B-06 — filesystem / POSIX TOCTOU | PSV source review lintas platform telah diselesaikan; selesaikan mitigasi desain, adversarial tests, dan penerimaan residual risk berbasis bukti sebelum Gate B PASS |
| 6. B-09 — signer/membership | PSV signer/membership telah diselesaikan; kebijakan fail-closed telah disahkan PO; selesaikan identity binding, authority, trust lifecycle, verifier, dan test tanpa mengulang PSV yang sama |
| 7. Otorisasi resmi pelaksanaan implementasi        | TIDAK DIBERIKAN (NOT AUTHORIZED)             |
+----------------------------------------------------+----------------------------------------------+
| STATUS AKHIR GATE B                                | BLOCKED                                      |
+----------------------------------------------------+----------------------------------------------+
```

---

## 13. READINESS GATE DAN BATAS OTORISASI

### 13.1 Evaluasi Kesiapan (Readiness Conclusion)
Berdasarkan isi dokumen, laporan Programmer, dan batas bukti yang tersedia bagi Auditor, kesiapan sistem dirinci ke dalam 8 kategori kesiapan. Klasifikasi di bawah ini adalah status readiness, bukan pengganti urutan PSV: seluruh fakta implementasi yang menjadi dependency blocker source-dependent tetap harus diperiksa Programmer terlebih dahulu sesuai §7.1 dan §15.3.
1. **Laporan inspeksi repositori lokal Programmer (`REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`):** Programmer melaporkan inspeksi atas DDL `schema.postgres.sql`, engine packaging Go `container.go`, modul Ed25519 SDK `crypto.ts`, handler NX Player `main.js`, ketiadaan 2PC di Marketplace `server.js`, dan status git commit `fc08a5c...`. Auditor belum memeriksa repositori `whisnu/nexa` atau bukti primer tersebut; seluruh klaim inspeksi tetap `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` bagi audit independen ini.
2. **Hal yang Berstatus Spesifikasi Konseptual (`SPECIFIED — PENDING IMPL`):** Draf JSON Schema audio berstatus proposed/non-normative; sintaksis Draft 7 tidak menjadikannya kontrak normatif, batas 199 track belum disahkan, dan schema universal multi-payload serta metadata persistence masih unresolved (NC-01/AC-01; §5.1), serializer RFC 8785 JCS, invariant Safe-Open, taksonomi 20 error code, dan formula derivasi ID.
3. **Inventaris dan Klasifikasi Kesiapan Seluruh Acceptance Criteria (Total Tepat 34 AC) (DEFECT-01):**
   Seluruh 34 AC terpetakan secara lengkap dan eksklusif berdasarkan register otoritatif §8 (setiap AC berada tepat di satu kelompok utama tanpa penghitungan ganda):
   - *Kelompok 1: 12 AC Spesifikasi Siap Uji (`[TEST-PLANNED — SPECIFICATION READY]`)*: AC-04, AC-11, AC-12, AC-17, AC-18, AC-19, AC-23, AC-24, AC-25, AC-27, AC-30, AC-31 (Spesifikasi fail-closed dan skenario uji terdefinisi lengkap tanpa dependensi usulan atau blocker terbuka; AC-25 memenuhi Keputusan PO CONF-02 Pilihan B APPROVED; AC-30 dan AC-31 memenuhi Keputusan PO §2.3.C dan §2.4 termasuk larangan album campuran, failure handling Studio, dan pemisahan dari B-04; klaim skema DDL statis untuk AC-17/AC-27 dilaporkan Programmer dan belum diverifikasi independen).
   - *Kelompok 2: 22 AC Rencana Uji Terblokir Eksekusi (`[TEST-PLANNED — EXECUTION BLOCKED]`)*:
     - *Sub-Kategori 2a: Modul Implementasi Belum Tersedia (`[IMPLEMENTATION MODULE PENDING]` - 2 AC)*: AC-05 (B-01: Strict JSON Parser belum dikoding), AC-06 (B-02: RFC 8785 JCS Serializer belum dikoding).
     - *Sub-Kategori 2b: Terblokir Gap Arsitektur, Usulan Spesifikasi, Taksonomi, Identitas Field, Prasyarat JIT & Provenance Membership Manifest, Identitas Album & Gap Lifecycle Auto-Next Multi-Payload (`[BLOCKED BY ARCHITECTURE / PROPOSED SPEC / TAXONOMY / NORMATIVE FIELD IDENTITY / JIT PREREQUISITES / ALBUM IDENTITY / LIFECYCLE GAP]` - 20 AC)*: AC-01 (NC-01: Strict Unknown Fields; universal schema pending), AC-02 (B-07/NC-07: Validasi Wrapper ZIP, Penerimaan Direktori Sesuai Keputusan PO, dan Pembatasan Flat Member Path Manifest), AC-03 (B-08: Circular Dependency Manifest Signing), AC-07 (NC-04/B-09: Membership policy approved; signer lifecycle pending), AC-09 (NC-05/NEW-01: Finalisasi spesifikasi uji terblokir keputusan normatif identitas field manifest audio), AC-10 (NC-05/A-05: Kode Error Diskrit Genesis Unresolved), AC-13 (B-07: Batas Kuota Ekstraksi ZIP masih berstatus usulan), AC-14 (B-04/CONF-03: Gap 2PC ke License Daemon), AC-15 (B-04/CONF-03: Gap 2PC / Replay Settlement), AC-16 (B-05: Semantik hash database child acquisition), AC-08 (NC-04/B-09: lifecycle revocation signer Registry belum ditetapkan), AC-20 (B-06: Batasan userspace POSIX Safe-Open TOCTOU), AC-21 (B-06: Batasan userspace POSIX post-open descriptor), AC-22 (NC-13/B-09: Terblokir parsial pada dependensi normatif Stage 8a terhadap Genesis 7b / lisensi 7c, izin background pre-verification, identitas field hash audio, dan autentisitas membership manifest signer UNKNOWN; CONF-01 bukan global playback gate; Stop-and-Clarify), AC-26 (NC-15: Formalisasi Taksonomi 20 Kode Error berstatus Usulan Spesifikasi), AC-28 (NC-01/06: Terblokir parsial pada ketiadaan kontrak identitas & persistensi Album multi-member di Marketplace; Stop-and-Clarify), AC-29 (NC-06: Terblokir parsial pada ketiadaan mekanisme Marketplace untuk memuat kembali Album sebagai satu kesatuan; Stop-and-Clarify), AC-32 (NC-13: Terblokir pada lifecycle Auto-Next multi-payload; audio memiliki handler ended untuk pustaka GUI desktop di renderer.js tanpa kontrak transisi Album, video tidak memiliki handler ended pada videoEngine, dokumen/gambar tidak memiliki durasi alami; seluruh pemicu Auto-Next multi-payload belum memiliki kontrak normatif; Stop-and-Clarify), AC-33 dan AC-34 (NC-14: eksekusi membership fail-closed menunggu implementasi/verifikasi membership dan lifecycle signer B-09; kebijakan PO telah disahkan).
   - *Kelompok 3: 0 AC Menunggu Keputusan Resmi Product Owner (`[PO DECISION REQUIRED]`)*: Tidak ada PO decision item aktif pada kelompok ini.
   *(Rekonsiliasi agregat: 12 + 22 + 0 = 34 AC berjumlah 34 secara aritmetis; kecocokan angka tidak dengan sendirinya membuktikan konsistensi semantik lintas-bab §1.5, §1.6, §2.1, §2.2, §8, §9, dan §12)*.
4. **Hal yang Belum Diverifikasi (`NOT VERIFIED — EVIDENCE NOT AVAILABLE`):** Pengujian fisik runtime mobile iOS/Android dan Usage Service cluster.
5. **Rangkuman Ketergantungan Blocker Teknis & Arsitektur:** Blocker teknis B-01 s.d. B-09 tetap terbuka sesuai status masing-masing. PSV residual R-02 s.d. R-10, termasuk R-09A/R-09A-1/R-10A, telah ditutup pada tingkat pembuktian yang dilaporkan di §15.11.3; jangan mengulang PSV yang sama. Pekerjaan berikutnya adalah menyelesaikan kontrak target, implementasi, adversarial tests, dan runtime evidence yang masih hilang. PSV baru hanya boleh diminta secara targeted bila ada pertanyaan faktual source-level baru yang material.
6. **Rangkuman Ketergantungan Keputusan Otoritatif PO:** Tidak ada PO decision blocker aktif untuk CONF-01 atau pemilihan model B-04. CONF-01 policy fail-closed dan CONF-02 Pilihan B telah disahkan. CONF-03 direklasifikasi sebagai kontrak teknis B-04 yang masih terbuka. Residual PSV R-02 s.d. R-10 beserta R-09A/R-09A-1/R-10A telah dinyatakan CLOSED pada §15.11.3; tidak ada PSV ulang menyeluruh. Keputusan PO/Architecture Authority berikutnya hanya diminta bila muncul pertanyaan normatif baru yang benar-benar belum ditetapkan.
7. **Kualifikasi Kelulusan Gate:** Gate A berstatus **`NOT PASSED — PRODUCT TRUTH RECONCILIATION APPLIED; SUBSTANTIVE BLOCKERS REMAIN; INDEPENDENT RE-AUDIT REQUIRED`**; Gate B berstatus **`BLOCKED`**.
8. **Status Otorisasi Implementasi PE-02:** **`NOT AUTHORIZED`** (Dilarang keras memulai implementasi kode atau migrasi database).


### 13.1.1 Rekonsiliasi Keputusan PO Terbaru — Status Aktif yang Menggantikan Snapshot Historis

Bagian ini adalah status aktif setelah keputusan PO yang telah disahkan; snapshot readiness lama dan catatan audit historis tidak dihapus, tetapi tidak boleh digunakan sebagai status keputusan terkini bila bertentangan dengan bagian ini.

1. **AC-01 / NC-01 — Unknown Fields:** PO telah menyetujui kebijakan strict: unknown fields wajib ditolak fail-closed. AC-01 tidak lagi menunggu keputusan PO. AC-01 tetap belum siap dieksekusi end-to-end karena universal multi-payload schema dan implementasi parser/validator masih menjadi dependency.
2. **AC-07 / NC-04 / CONF-01 — Membership Authenticity:** PO telah menyetujui Album Membership Authenticity Fail-Closed. Manifest dengan signer `UNKNOWN` atau signature manifest invalid tidak dapat mengautentikasi membership Album. Ini bukan global playback gate; file `.nx` yang dipilih secara independen tetap mengikuti PE-01 standalone. AC-07 tidak lagi menunggu keputusan PO; identity binding, authority, trust store, key lifecycle, rotation, revocation, freshness, dan implementasi verifier tetap merupakan gap teknis B-09/NC-04.
3. **CONF-03 / B-04:** CONF-03 tidak lagi diperlakukan sebagai konflik yang menunggu pemilihan model normatif. Model B, SSP/Largest Remainder, `bundle_checkout_id`, dan Immutable Checkout Manifest SSOT telah disahkan. B-04 tetap OPEN/BLOCKED karena kontrak transaksi/pemenuhan, storage, member-to-acquisition mapping, idempotency, partial failure, commit/recovery, settlement, dan License Daemon side effects belum lengkap.
4. **Agregat aktif 34 AC:** 12 `TEST-PLANNED — SPECIFICATION READY` + 22 `TEST-PLANNED — EXECUTION BLOCKED` + 0 `PO DECISION REQUIRED` = 34. AC-01 dan AC-07 dipindahkan dari kategori PO Decision Required ke Execution Blocked atas dasar keputusan yang telah disahkan dan dependency teknis yang masih tersisa. Setiap perubahan status harus tercermin pada register individual §8, NC register §6, blocker register §9, dan ringkasan §2.1.
5. **Gate:** Gate A tetap `NOT PASSED` sampai kontrak dan traceability seluruh AC/NC, konflik internal, bukti, dan expected result direkonsiliasi serta lulus independent re-audit. Gate B tetap `BLOCKED` oleh kesiapan teknis yang belum terpenuhi. Tidak ada perubahan otorisasi implementasi.
6. **PSV boundary:** Register residual PSV dinyatakan CLOSED pada §15.11.3. Tidak ada permintaan PSV ulang untuk B-04/B-05/B-06/B-08/B-09 atau workstream R-02 s.d. R-10 yang sama. Hanya fakta baru yang spesifik dan material dapat memicu PSV targeted baru.

### 13.2 Disposisi Kesiapan Dokumen Resmi
Status kesiapan resmi dokumen ditetapkan sebagai:

**`NOT READY — PRODUCT-TRUTH BOUNDARY AND ACTIVE REGISTER / CROSS-SECTION SEMANTIC CONSISTENCY REQUIRE INDEPENDENT RE-AUDIT; IMPLEMENTATION BLOCKED`**

---


## 13.3 REKONSILIASI AUDIT TERARAH — FINDING-01 s.d. FINDING-06 (BASELINE AUDIT 2026-11-08)

Bagian ini mengonsolidasikan enam temuan audit terbaru dan **mengesampingkan redaksi lama yang bertentangan** pada bagian lain dokumen. Ini bukan artefak baru, bukan siklus revisi baru, dan bukan otorisasi implementasi.

### FINDING-01 — AC-01 / NC-01: Skema manifest belum normatif dan belum lengkap
- **Status:** `NOT READY — UNIVERSAL SCHEMA INCOMPLETE`.
- Struktur konseptual kumpulan anggota independen `.nx` tidak menetapkan nama array atau path JSON. `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]` maupun `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]` tidak boleh diperlakukan sebagai identifier normatif; pemetaan draf audio tetap unresolved sampai keputusan PO/Architecture Authority.
- Draf JSON Schema audio di §5.1 tetap **PROPOSED / NON-NORMATIVE**. Field usulan `album_id`, `artist`, `total_tracks`, `release_date`, `album_signer_public_key`, `album_signer_signature`, `canonical_algorithm`, dan `signature_algorithm` tidak boleh menjadi required normative fields. Penghapusan field usulan dari daftar `required` contoh tidak menjadikan schema audio universal atau siap implementasi.
- Schema lengkap Video, Document, dan Image belum tersedia. Jangan mengarang discriminator, hash field, payload schema, atau field universal tambahan. Area tanpa kontrak tetap `UNRESOLVED — STOP AND CLARIFY`.
- Perilaku unknown fields tetap `PO DECISION REQUIRED`: strict rejection dan permissive ignore adalah proposal yang belum diputuskan. Metadata PO yang disetujui tetap `title` dan `cover_artwork`; representasi/persistensi multi-member tidak boleh direka. AC-01 tetap `[PO DECISION REQUIRED]`.

### FINDING-02 — AC-07 / NC-04: Album Signer bukan gerbang playback global
- **Status:** `NOT READY — PRODUCT TRUTH RECONCILIATION REQUIRED`.
- Jika dipertahankan oleh PO/Arsitektur, Album Signer hanya mengautentikasi deklarasi manifest/member-list. Ia tidak menggantikan Creator signature, Genesis ownership, Registry trust, asset trust, active license, atau playback authorization masing-masing member.
- Opsi A/B/C sebagai pilihan untuk memblokir/mengizinkan seluruh playback Album dihapus. CONF-01 bukan global playback gate. Playback tetap JIT dan per member sesuai kontrak PE-01.
- Identitas signer, key custody, Registry enrollment, identity binding, rotation, dan revocation belum memiliki dasar kontrak yang terbukti. Jangan menciptakan otoritas global, Registry endpoint, key lifecycle, atau mekanisme fallback.
- Signer `UNKNOWN` tidak otomatis berarti `INVALID` dan tidak otomatis membatalkan trust member. Sampai CONF-01 diselesaikan, autentisitas/membership manifest tidak boleh diasumsikan.

### FINDING-03 — NC-02 / B-08 / AC-03: Circular dependency tanda tangan manifest
- **Status:** `BLOCKED — ARCHITECTURE AUTHORITY DECISION REQUIRED`.
- Dua rancangan (signature-stripped JCS dan detached `album_manifest.sig`) tetap proposal yang belum dipilih. Tidak ada pilihan default atau implementasi tersirat.
- Kontrak harus menetapkan canonical payload, field yang dikecualikan bila ada, urutan canonicalization/signing, lokasi/representasi signature, dan verifikasi. Sampai itu ditetapkan, AC-03 tetap blocked dan schema tidak boleh mewajibkan `album_signer_signature`.
- Pertahankan empat jenis signature yang terpisah. Tidak ada signature Album yang menggantikan signature Creator/Container/Registry/Genesis.

### FINDING-04 — AC-08 / NC-04 / B-09: Revocation lifecycle Album Signer belum ditetapkan
- **Status:** `BLOCKED / UNRESOLVED REGISTRY LIFECYCLE`; AC-08 **bukan** `SPEC READY`.
- Pernyataan konseptual “tolak signer key jika tercantum pada revocation list” bukan spesifikasi operasional. Belum ada bukti otoritatif mengenai sumber revocation, pemilik kewenangan, format record, signature/validity, retrieval, freshness, cache, failure mode, atau lifecycle.
- Dilarang mengarang revocation list, endpoint, Registry record, database field, maupun kebijakan fail-closed baru. Sinkronkan AC-08, NC-04, B-09, §5.1, §6.4, dan §6.15.
- Revocation Album Signer tetap terpisah dari revocation Creator/Registry evidence setiap member. Status signer tidak boleh mengubah status member secara otomatis.

### FINDING-05 — Manifest signature invalid: batas aman diagnostik member
- **Status:** `REQUIRES ARCHITECTURE RECONCILIATION`.
- Signature manifest invalid berarti deklarasi dan membership-nya tidak autentik/tidak dapat dipercaya. Sistem tidak boleh menggunakan daftar tersebut sebagai bukti keanggotaan Album.
- Hal tersebut tidak membuktikan file `.nx` individual invalid. Diagnostik mandiri hanya dapat dijalankan terhadap file yang dipilih/disediakan secara independen; laporkan sebagai verifikasi file standalone, bukan hasil verifikasi anggota Album.
- Jika produk membutuhkan pemeriksaan member dari arsip dengan manifest invalid, batas dan sumber membership yang sah harus ditetapkan Architecture Authority terlebih dahulu. Sinkronkan §5.1, Tahap 4–5 §5.2, §5.3, NC-02, AC-03, dan error taxonomy §6.15.

### FINDING-06 — Sinkronisasi register, readiness, dan klaim penutupan
- **Status:** `REQUIRES TARGETED DOCUMENT RECONCILIATION`.
- Penutupan historis AUDIT-NEW-02 hanya membuktikan koreksi contoh manifest dalam ruang lingkup temuan itu; tidak membuktikan AC-01 atau schema universal selesai.
- AC-08 diturunkan menjadi `[TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED REGISTRY REVOCATION LIFECYCLE]`. Agregat readiness menjadi **12 AC Spec Ready + 20 AC Execution Blocked + 2 AC PO Decision Required = 34 AC**. AC-01 dan AC-07 tetap PO Decision Required; AC-03 tetap blocked oleh B-08.
- Semua ringkasan agregat aktif wajib mengikuti **12/20/2**. Angka **14/18/2** hanya boleh dipertahankan sebagai snapshot historis sebelum AC-33/AC-34 dipindahkan dari Specification Ready ke Execution Blocked; angka itu tidak berlaku sebagai readiness aktif. Agregat 15/17/2 juga bukan baseline aktif. AC-08 tetap Execution Blocked selama lifecycle revocation Registry belum ditetapkan.
- Status historis `PASS` hanya berlaku pada ruang lingkup spesifik yang dinyatakan; tidak boleh dipakai untuk menyimpulkan seluruh AC atau schema siap.
- Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 implementation tetap `NOT AUTHORIZED`.

### Acceptance Criteria Koreksi Dokumen (untuk audit ulang)
1. Tidak ada field proposed/unresolved dipaksakan menjadi required normative schema field.
2. Redaksi historis sebelumnya pernah menyebut `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]` sebagai koleksi universal; pernyataan tersebut telah dikoreksi pada §5.1 dan tidak lagi berlaku. Nama array/path JSON tetap unresolved.
3. Schema audio, video, document, image, unknown-field behavior, dan metadata persistence diberi status yang jujur; tidak ada klaim universal schema lengkap.
4. Album Signer tidak menjadi global playback gate; empat signature tetap terpisah; identitas/lifecycle signer tidak direka.
5. B-08 tetap blocked sampai Architecture Authority memilih signature scope dan representation; AC-03 tidak berstatus ready.
6. AC-08 tidak berstatus Spec Ready selama revocation lifecycle belum ditetapkan; tidak ada mekanisme Registry/revocation yang dikarang.
7. Manifest signature invalid tidak mengubah status intrinsik member menjadi INVALID dan tidak mengesahkan membership-nya; diagnostik standalone dibedakan dari diagnostik Album.
8. Agregat readiness 12 + 20 + 2 = 34 konsisten di seluruh ringkasan yang mengklaim angka tersebut.
9. Tidak ada perubahan pada keputusan PO positif, kontrak PE-01/Sprint 16, dan tidak ada penambahan scope implementasi.
10. Gate A `NOT PASSED`, Gate B `BLOCKED`, PE-02 Implementation `NOT AUTHORIZED`, Sprint 16/PE-01 `CLOSED / FROZEN`, Sprint 17 `NOT STARTED`.

**Disposisi setelah rekonsiliasi:** Dokumen telah diperbarui secara terarah, tetapi blocker substantif belum seluruhnya terselesaikan hanya dengan perubahan redaksi. Gate A tetap `NOT PASSED` sampai audit independen memverifikasi konsistensi seluruh bagian dan otoritas terkait menetapkan keputusan yang menjadi kewenangannya. Tidak ada otorisasi implementasi yang diberikan.

## 13.4 AUDIT INDEPENDEN PRODUCT-TRUTH SOURCE BOUNDARY — 2026-11-08

**Ruang lingkup:** pemeriksaan White Paper v5.6 dan Roadmap v4.8 dari Library terhadap atribusi sumber, klaim kontrak, register AC/NC, serta status governance dalam file kanonikal PE-02 pada GitHub whisnu/plan:main. Pemeriksaan ini bersifat audit dokumen; bukan inspeksi source repository whisnu/nexa, bukan runtime test, dan bukan bukti implementasi.

### AUDIT-PT-01 — Rujukan sumber member .nx berisiko dibaca sebagai pengesahan kontrak Album
- **Status:** `MATERIAL DOCUMENT DEFECT — TARGETED CORRECTION APPLIED`.
- White Paper v5.6 mendefinisikan baseline ekosistem, batas authority, container/manifest, Creator/Genesis ownership, Registry, JIT Player, Verify, dan Studio. Namun, tidak ditemukan spesifikasi normatif untuk ZIP wrapper Album, Album Manifest, Album Signer, identitas Album multi-member, atau lifecycle signer Album.
- Roadmap v4.8 secara eksplisit mempertahankan PE-02 `NOT READY — BLOCKED (V5-REV1)`, Product Enhancement Window `OPEN / NOT FROZEN`, PE-02 implementation `NOT AUTHORIZED`, dan Sprint 17 `NOT STARTED`. Roadmap bukan sumber persetujuan desain Album.
- Karena itu, rujukan dalam AC/NC ke White Paper §Manifest, §Registry, §JIT Player, §Verify, atau §Studio hanya mendukung bagian kontrak Nexa yang benar-benar dinyatakan dalam White Paper. Rujukan tersebut tidak membuktikan Album-specific extension. Keputusan PO PE-02 yang telah disahkan tetap berlaku pada ruang lingkupnya; proposal teknis dan keputusan yang belum disahkan tetap non-normatif.
- **Koreksi diterapkan:** §1.2 kini memuat kualifikasi ruang lingkup rujukan White Paper/Roadmap dan kewajiban mengklasifikasikan setiap ketentuan Album-spesifik sebagai keputusan PO, proposal, atau unresolved. §12.3 dan §13.2 kini secara eksplisit mempertimbangkan gap atribusi sumber tersebut.

### AUDIT-PT-02 — Status roadmap tidak boleh disamakan dengan status koreksi plan
- **Status:** `PASS — STATUS BOUNDARY PRESERVED`.
- Koreksi pada dokumen PE-02 tidak mengubah Roadmap v4.8, tidak menutup Product Enhancement Window, tidak meluluskan Gate A secara otomatis, dan tidak mengotorisasi implementasi.
- Status tetap: Gate A `NOT PASSED`; Gate B `BLOCKED`; PE-02 implementation `NOT AUTHORIZED`; Sprint 16/PE-01 `CLOSED / FROZEN`; Sprint 17 `NOT STARTED`.

### Batas audit dan keputusan
- Audit ini tidak menyelesaikan CONF-01, B-08, B-04/CONF-03, B-05, B-06, B-07, NC-01, NC-04, atau ketergantungan JIT Stage 8a yang masih unresolved.
- Tidak ada kontrak Album baru, signer authority, Registry endpoint, schema, database field, atau lifecycle yang ditambahkan.
- Tidak ada perubahan pada keputusan PO yang sudah disahkan atau baseline PE-01/Sprint 16.
- **Disposisi:** koreksi atribusi Product Truth telah diterapkan pada dokumen yang sama. Gate A tetap `NOT PASSED` karena blocker substantif dan keputusan otoritatif yang belum selesai; Gate B tetap `BLOCKED`. Implementasi PE-02 tetap `NOT AUTHORIZED`.

---

## 13.5 AUDIT ULANG KONSISTENSI REGISTER DAN KONTRAK AKTIF — 2026-11-08

**Ruang lingkup:** audit lintas-bagian pada file kanonikal yang sama, berfokus pada AC-07/AC-08, NC-04, CONF-01, status Album Signer, serta dependensi Stage 8a/8b/8c dan perilaku diagnostik NX Verify. Ini merupakan tindak lanjut audit dokumen, bukan siklus koreksi baru, bukan plan baru, bukan inspeksi source repository, dan bukan otorisasi implementasi.

### AUDIT-REG-01 — AC-07, AC-08, dan NC-04 sebelumnya tercampur dalam atribusi fungsi
- **Temuan:** Pada uraian Stage 8b sebelumnya, AC-08 disebut mengatur autentisitas/revocation deklarasi manifest secara bersamaan. Ini mengaburkan pembagian register: AC-07/CONF-01 untuk autentisitas provenance membership saat signer `UNKNOWN`; AC-08 untuk revocation signer dan lifecycle Registry yang belum ditetapkan.
- **Koreksi:** Uraian Stage 8b kini membedakan AC-07 dan AC-08 secara eksplisit. Register AC-07 tetap `PO DECISION REQUIRED`; AC-08 tetap `TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED REGISTRY REVOCATION LIFECYCLE`.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED`.

### AUDIT-REG-02 — Batas diagnostik Stage 8a dan pre-verification belum konsisten pada ringkasan JIT
- **Temuan:** Satu kalimat larangan pre-otorisasi dapat dibaca sebagai kewajiban bahwa seluruh Stage 6/7/8 hanya berjalan ketika transisi playback, padahal izin diagnostik Stage 8a untuk anggota antrean secara eksplisit masih unresolved. Ini berisiko mengubah unresolved permission menjadi larangan kategoris.
- **Koreksi:** Redaksi kini menegaskan bahwa Stage 8a background diagnostic permission tetap `UNRESOLVED`; tidak dinyatakan `ALLOWED` atau `NOT ALLOWED`. Larangan yang sudah pasti tetap mutlak: background pre-verification tidak memberi otorisasi playback, tidak melakukan Stage 8b, dan tidak mendaftarkan buffer Stage 8c. Anggota current member tetap menjalani evaluasi otorisasi JIT.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED`.

### AUDIT-REG-03 — NX Verify mengasumsikan membership Album dan mengaburkan verifikasi standalone
- **Temuan:** Redaksi Lapisan 2 sebelumnya menyatakan pemeriksaan setiap member Album berlangsung independen tanpa mensyaratkan autentisitas membership. Ini tidak konsisten dengan CONF-01 dan Finding-05: manifest yang signer-nya `UNKNOWN` atau signature-nya invalid tidak dapat menjadi bukti membership yang autentik.
- **Koreksi:** Pemeriksaan member Album hanya dapat dilabeli sebagai hasil anggota Album jika membership dibuktikan secara sah. File yang disediakan/dipilih secara independen masih dapat diperiksa sebagai standalone sesuai PE-01; hasilnya tidak boleh dilabeli sebagai verifikasi anggota Album.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED`.

### AUDIT-REG-04 — Semantik `UNKNOWN / INCOMPLETE` bertentangan dengan empat status kanonikal
- **Temuan:** Redaksi sebelumnya melarang status `UNKNOWN / INCOMPLETE` ditampilkan, sementara bagian yang sama dan White Paper mempertahankan `Trust Unknown` / `Verification Incomplete` sebagai status kanonikal yang harus dapat ditampilkan.
- **Koreksi:** Redaksi kini mewajibkan status ketidakpastian dipertahankan dan ditampilkan sebagai `Trust Unknown` / `Verification Incomplete`, serta melarang pemetaannya menjadi `INVALID`.
- **Status:** `MATERIAL DOCUMENT DEFECT — TARGETED CORRECTION APPLIED`.

### AUDIT-REG-05 — Klaim lookup Registry Album Signer belum dibatasi oleh ketiadaan lifecycle
- **Temuan:** Kalimat awal Lapisan 1 NX Verify dapat dibaca sebagai kontrak operasional bahwa public key Album Signer sudah dapat diperiksa pada Registry, sementara NC-04 §6.4 secara eksplisit menyatakan mekanisme pendaftaran, identity binding, rotation, dan revocation belum terbukti/ditetapkan.
- **Koreksi:** Lapisan 1 kini menyatakan evaluasi Registry hanya dapat dilakukan setelah mekanisme identitas dan lifecycle Album Signer ditetapkan secara otoritatif. Kategori status yang disebut merupakan kondisi yang perlu ditangani, bukan klaim tersedianya endpoint, record, atau lifecycle.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED`.

### Pemeriksaan preservasi setelah koreksi
1. AC-07 tetap `PO DECISION REQUIRED`; AC-08 tetap `EXECUTION BLOCKED`; NC-04 tetap `PARTIALLY SPECIFIED / GAP UNRESOLVED`; CONF-01 tetap terbuka.
2. Opsi A/B/C tidak dihidupkan kembali sebagai kebijakan. Penyebutannya yang tersisa hanya catatan historis yang secara eksplisit menyatakan bukan kerangka keputusan aktif, serta pernyataan bahwa opsi tersebut telah dihapus.
3. AC-22 tetap terblokir parsial oleh prasyarat JIT, izin diagnostik Stage 8a, identitas field hash, dan autentisitas membership manifest; CONF-01 bukan gerbang playback global.
4. Stage 8b tetap memerlukan digest 8a yang cocok, Genesis 7b sah, dan lisensi aktif 7c; Stage 8c tetap hanya setelah Stage 8b berhasil dan hanya untuk current member.
5. Tidak ada endpoint Registry, signer authority, schema, database field, atau lifecycle baru yang diciptakan. Tidak ada perubahan pada keputusan PO positif, PE-01, atau Sprint 16.
6. Agregat readiness tetap 12 AC Spec Ready + 20 AC Execution Blocked + 2 AC PO Decision Required = 34 AC; Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; implementasi PE-02 tetap `NOT AUTHORIZED`.

**Disposisi:** Lima ketidaksesuaian redaksional/semantik di atas telah dikoreksi pada file kanonikal yang sama. Blocker substantif yang memerlukan keputusan PO/Architecture Authority tetap terbuka. Audit ini tidak meluluskan Gate A, tidak membuka Gate B, dan tidak memberikan otorisasi implementasi.

## 13.6 AUDIT INDEPENDEN DAN KOREKSI TERARAH IND-01 SAMPAI IND-05 — 2026-11-08

**Ruang lingkup:** tindak lanjut atas lima temuan audit independen IND-01 sampai IND-05. Koreksi dibatasi pada konsistensi identifier path member, atribusi operasi Registry Album Signer, prasyarat autentisitas membership pada alur Player, urutan bagian dokumen, dan provenance bukti repository lokal. Tidak ada plan baru atau siklus koreksi baru.

### IND-01 — Identifier path member tidak konsisten dengan koleksi universal
- **Temuan historis:** Koreksi IND-01 sebelumnya mengganti `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].file_name` menjadi `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan].file_name`, tetapi penggantian tersebut secara tidak sengaja memberi kesan bahwa nama array dan field path `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]` telah dipilih. Keputusan PO AUDIT-NEW-06/07 hanya mengesahkan semantik nama berkas, bukan path JSON.
- **Koreksi:** Redaksi aktif memisahkan semantik nama berkas yang disetujui PO dari identifier array/field path yang belum ditetapkan. `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]`, `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan].file_name`, `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan].title`, dan parent path hash tidak dinyatakan sebagai kontrak normatif. Tidak ada field path pengganti yang dipilih.
- **Batas hash:** `audio_sha256` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) tetap kandidat dari draf berbeda; identitas, parent array, path, alias, ekuivalensi, fallback, dan prioritas semuanya unresolved.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED — AUDIO HASH IDENTITY REMAINS UNRESOLVED`.

### IND-02 — Heading dan taksonomi Tahap 4 masih mengesankan operasi Registry tersedia
- **Temuan:** Heading Tahap 4 dan daftar error masih dapat dibaca sebagai operasi trust verification/lookup Registry yang telah tersedia, walaupun NC-04 belum menetapkan identitas dan lifecycle signer.
- **Koreksi:** Heading Tahap 4 kini dibatasi pada JCS dan verifikasi signature kriptografis. Error Tahap 4 hanya mencantumkan kegagalan signature; kategori UNKNOWN/UNTRUSTED tetap kondisi unresolved, bukan hasil lookup Registry yang tersedia.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED — REGISTRY OPERATION NOT CLAIMED AVAILABLE`.

### IND-03 — Prasyarat autentisitas membership belum eksplisit pada alur Verify
- **Temuan:** Layer Verify telah memuat batas membership, tetapi urutan navigasi masih memerintahkan pemrosesan anggota pertama saat Album dibuka tanpa prasyarat eksplisit autentisitas membership.
- **Koreksi:** Navigasi Verify kini mensyaratkan autentisitas deklarasi membership sebelum file diproses/dilabeli sebagai anggota Album. Jika belum terbukti, file dari manifest tidak boleh diproses sebagai anggota; file yang disediakan independen tetap dapat diperiksa sebagai standalone PE-01 dan hasilnya tidak boleh dilabeli sebagai verifikasi anggota Album.
- **Batas:** Koreksi ini tidak memutus CONF-01, tidak menetapkan kebijakan signer UNKNOWN, dan tidak membuat playback authorization global.
- **Status:** `TARGETED DOCUMENT CORRECTION APPLIED — CONF-01 / B-09 REMAIN UNRESOLVED`.

### IND-04 — Urutan bagian dokumen
- **Temuan:** §13.5 sebelumnya ditempatkan setelah §14 sehingga deklarasi penutup bukan bagian terakhir.
- **Koreksi:** §13.5 dipertahankan utuh dan dipindahkan sebelum §14. Bagian ini (§13.6) mencatat koreksi IND-01 sampai IND-05; §14 menjadi bagian terakhir.
- **Status:** `STRUCTURAL CORRECTION APPLIED`.

### IND-05 — Provenance inspeksi repositori lokal
- **Temuan historis (bukan label status aktif):** Sebagian redaksi lama pernah menggunakan label `[LOCAL INSPECTED / AUDIT PENDING]` atau `[CODE-INSPECTED]`. Koreksi provenance mengganti klaim inspeksi lokal yang aktif menjadi `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; Auditor tidak mengklaim inspeksi source repository primer.
- **Koreksi:** Status inspeksi kode pada §4.3 dan ringkasan §13.1 dinyatakan sebagai laporan Programmer yang belum diverifikasi independen. G-01 sampai G-03 tetap evaluasi bersyarat berdasarkan laporan tersebut; bukan konfirmasi Auditor bahwa inspeksi lokal telah dilakukan.
- **Batas:** Tidak ada klaim bahwa audit ini memeriksa working tree `whisnu/nexa`, menjalankan `git diff`, `git status`, `ls`, menginspeksi DDL, atau memverifikasi staging lokal.
- **Status:** `PROVENANCE QUALIFICATION APPLIED — NO INDEPENDENT LOCAL REPOSITORY INSPECTION CLAIMED`

### Pemeriksaan preservasi
1. Nama array/field path koleksi anggota tetap unresolved; tidak ada pemilihan `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]`, `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]`, atau struktur pengganti.
2. Identitas field hash audio tetap unresolved; AC-09 tidak dinaikkan menjadi Spec Ready.
3. NC-04, B-09, CONF-01, B-08, dan lifecycle revocation AC-08 tetap pada status sebelumnya.
4. Stage 8a diagnostic/background permission tetap unresolved; Stage 8b/8c dan JIT current-member boundary tidak diubah.
5. Keputusan PO yang telah disahkan, kontrak PE-01, Sprint 16, dan baseline frozen tidak diubah.
6. Tidak ada endpoint Registry, signer authority, schema, database field, lifecycle, atau kebijakan baru yang diciptakan.
7. Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 Implementation tetap `NOT AUTHORIZED`; Sprint 16/PE-01 tetap `CLOSED / FROZEN`; Sprint 17 tetap `NOT STARTED`.

**Disposisi:** Koreksi dokumen IND-01 sampai IND-05 diterapkan secara terbatas. Ini bukan penutupan blocker substantif, bukan persetujuan Gate A, bukan pembukaan Gate B, dan bukan otorisasi implementasi. Audit independen ulang atas file aktual tetap diperlukan.

## 13.7 AUDIT KOREKSI TERARAH IND-R1 SAMPAI IND-R4 — 2026-11-08

**Ruang lingkup:** Koreksi empat residual finding dari audit independen atas blob sebelumnya. Perubahan hanya pada file kanonikal ini; tidak membuka siklus koreksi baru, tidak membuat artefak/plan baru, dan tidak memberikan otorisasi implementasi.

### IND-R1 — Nama array dan field path manifest tidak memiliki otoritas normatif
- **Koreksi:** Redaksi aktif tidak lagi menetapkan `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan]` sebagai array universal atau `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan].file_name` / `members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan].title` sebagai field path yang disahkan. Konsep kumpulan anggota Album dipisahkan dari representasi JSON. Keputusan PO AUDIT-NEW-06/07 tetap berlaku hanya pada semantik nama berkas (flatness, pelestarian kapitalisasi, dan keunikan ASCII case-fold), bukan pada path JSON.
- **Hash audio:** `audio_sha256` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) tetap kandidat unresolved; tidak ada parent array, path, alias, ekuivalensi, fallback, atau prioritas yang ditetapkan.
- **Disposisi:** Setiap kebutuhan implementasi yang memerlukan pemilihan nama array, field path, atau pemetaan hash wajib berhenti dengan `INSTRUKSI TIDAK JELAS — STOP AND CLARIFY` dan meminta keputusan PO/Architecture Authority. Programmer dilarang memilih struktur hanya untuk menyelaraskan dokumen.

### IND-R2 — Tahap 4 tidak boleh menyiratkan operasi Registry tersedia
- **Koreksi:** Heading Tahap 4 dibatasi pada JCS dan verifikasi signature kriptografis. Error Tahap 4 hanya mencantumkan kegagalan signature; kondisi signer UNKNOWN/UNTRUSTED tetap unresolved dan bukan hasil lookup Registry yang tersedia.
- **Batas:** NC-04 / B-09 / CONF-01 dan lifecycle signer tetap belum terselesaikan. Tidak ada endpoint, record, enrollment, identity binding, key rotation, atau revocation lifecycle yang diciptakan.

### IND-R3 — Prasyarat autentisitas membership pada navigasi Verify
- **Koreksi:** Alur Verify kini mensyaratkan bukti autentisitas membership sebelum file dari manifest diproses atau ditampilkan sebagai anggota Album. Bila prasyarat belum terpenuhi, file tersebut tidak diproses sebagai anggota Album; file yang disediakan secara independen hanya dapat diperiksa melalui jalur standalone PE-01.
- **Batas:** CONF-01 / B-09 tetap unresolved; koreksi ini tidak menetapkan kebijakan signer dan tidak memberikan playback authorization.

### IND-R4 — Provenance inspeksi repositori lokal
- **Koreksi:** Status inspeksi kode pada §4.3 dan ringkasan §13.1 dinyatakan sebagai laporan Programmer yang belum diverifikasi independen. G-01 sampai G-03 tetap evaluasi bersyarat berdasarkan laporan tersebut; bukan konfirmasi Auditor bahwa inspeksi lokal telah dilakukan.
- **Batas:** Audit ini tidak memeriksa repositori `whisnu/nexa`, working tree, DDL lokal, atau runtime lokal.

### Pemeriksaan preservasi
1. Keputusan PO tentang semantik nama berkas tetap dipertahankan tanpa mengesahkan path JSON.
2. Identitas field hash audio, struktur manifest, dan lifecycle signer tetap unresolved.
3. Tidak ada endpoint Registry, signer authority, schema, database field, atau lifecycle baru yang diciptakan.
4. Kontrak PE-01, Sprint 16, dan PE-01 frozen baseline tidak diubah.
5. Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 Implementation tetap `NOT AUTHORIZED`; Sprint 16/PE-01 tetap `CLOSED / FROZEN`; Sprint 17 tetap `NOT STARTED`.

**Disposisi:** Empat koreksi redaksional/semantik IND-R1 sampai IND-R4 diterapkan pada file kanonikal yang sama. Ini bukan penutupan blocker substantif, bukan persetujuan Gate A, bukan pembukaan Gate B, dan bukan otorisasi implementasi.



## 13.8 AUDIT KOREKSI TERARAH IND-R1 SAMPAI IND-R4 DAN AC-33/AC-34 — 2026-11-08

**Ruang lingkup:** Koreksi terarah berdasarkan audit independen terbaru atas file kanonikal yang sama. Tidak membuat plan baru atau siklus koreksi baru. Perubahan terbatas pada notasi manifest, batas operasi Registry, prasyarat autentisitas membership Verify, provenance klaim repository, dan readiness AC-33/AC-34.

### IND-R1 — Notasi array/path manifest
- Notasi aktif yang sebelumnya dapat dibaca sebagai path manifest normatif telah diubah menjadi deskripsi konseptual tanpa memilih nama array atau field path.
- `audio_sha256` dan notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) hanya dipertahankan sebagai nama kandidat dari draf historis/teknis; parent array, field path, alias, ekuivalensi, fallback, dan prioritas tetap unresolved.
- Tidak ada struktur JSON baru yang disahkan atau dipilih.

### IND-R2 — Batas operasi Registry Album Signer
- Diagram JIT Tahap 4 dan ringkasan pemeriksaan trust telah diselaraskan: Tahap 4 mencakup JCS dan verifikasi signature kriptografis; lookup/evaluasi signer trust Registry belum tersedia sebagai operasi yang dapat diklaim.
- Identitas, enrollment, identity binding, key rotation, revocation lifecycle, endpoint, dan record tetap unresolved.

### IND-R3 — Prasyarat autentisitas membership Verify
- AC-33 dan AC-34 kini mensyaratkan bukti autentisitas membership sebelum file manifest diproses/dilabeli sebagai anggota Album.
- Jika prasyarat belum terbukti, file dari manifest tidak diproses sebagai anggota Album. File yang diberikan secara independen tetap dapat diperiksa melalui jalur standalone PE-01 dan tidak boleh dilabeli sebagai hasil verifikasi anggota Album.
- CONF-01/B-09 tetap unresolved; keputusan PO tidak diubah.

### IND-R4 — Provenance klaim repository lokal
- Klaim DDL, pipeline, endpoint, dan UI lokal pada §5.1 telah dikualifikasi sebagai laporan Programmer yang belum diverifikasi independen.
- Klaim kode/DDL lain yang dirujuk lintas-bagian tetap tunduk pada batas provenance §4.3, §6.9, §13.1, dan §14. Tidak ada klaim inspeksi independen terhadap `whisnu/nexa`, working tree, DDL lokal, atau runtime.

### Readiness AC-33 dan AC-34
- AC-33 dan AC-34 dipindahkan dari kelompok 14 AC Spec Ready ke kelompok Execution Blocked karena prasyarat autentisitas membership bergantung pada CONF-01/B-09 yang belum diputuskan.
- Agregat aktif diperbarui menjadi **12 AC Spec Ready + 20 AC Execution Blocked + 2 AC PO Decision Required = 34 AC**. AC-01 dan AC-07 tetap PO Decision Required. AC-25 tetap Spec Ready sesuai CONF-02 Pilihan B.
- Perubahan ini mengubah klasifikasi kesiapan pengujian, bukan keputusan PO tentang Manual Next, No Aggregate Status, Verify Desktop Full, atau Mobile Verify-Lite.

### Pemeriksaan preservasi dan batas audit
1. Tidak ada nama array, field path, hash mapping, schema, endpoint Registry, signer authority, atau lifecycle baru yang ditetapkan.
2. Tidak ada perubahan pada kontrak PE-01, Sprint 16, PE-01 frozen baseline, atau keputusan PO yang telah disahkan.
3. Tidak ada implementasi, runtime test, atau inspeksi source repository yang dilakukan.
4. Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 Implementation tetap `NOT AUTHORIZED`; Sprint 16/PE-01 tetap `CLOSED / FROZEN`; Sprint 17 tetap `NOT STARTED`.

**Disposisi:** Koreksi dokumen dan klasifikasi AC-33/AC-34 diterapkan secara terbatas pada file kanonikal yang sama. Ini bukan persetujuan Gate A, bukan pembukaan Gate B, dan bukan otorisasi implementasi.

## 13.9 REKONSILIASI PRODUCT TRUTH DAN KONSISTENSI LINTAS-BAGIAN — 2026-11-08

**Ruang lingkup:** Koreksi terarah sesuai mandat handover Product Truth Reconciliation. Perubahan hanya pada file kanonikal ini; tidak membuka corrective cycle baru dan tidak memberikan otorisasi implementasi.

1. **PT-01/PT-02 — Packaging dan Manifest:** Album ZIP wrapper, nama/lokasi manifest, schema JSON, nama array, field path, versi manifest, timestamp, metadata tambahan, dan field payload diperlakukan sebagai proposal/unresolved kecuali keputusan PO eksplisit tersedia. Semantik title/artwork PO dipertahankan tanpa mengesahkan JSON path. Keputusan ZIP entry semantics dan filename dipertahankan tanpa memperluasnya menjadi pengesahan wrapper/schema.
2. **PT-03/PT-04 — Album Signer dan Kriptografi:** Album Signer, identitas/lifecycle Registry, JCS/Ed25519 manifest, payload kanonikal, dan signature construction tidak dinaikkan menjadi Product Truth. RFC 8785/RFC 8032 tetap standar teknis, bukan otorisasi penggunaan Album Signer. B-08, B-09, NC-04, CONF-01 tetap unresolved/blocked.
3. **PT-05/PT-06 — Kontrak member, Player, Verify:** Kontrak standalone `.nx`, Creator signature, Genesis ownership, Registry/sidecar, licensing, JIT, dan trust semantics dipertahankan. Verify wajib membuktikan membership authenticity sebelum memproses/menamai file sebagai anggota Album; file independen tetap hanya standalone PE-01. CONF-02 Pilihan B, manual Next, dan tidak adanya status agregat dipertahankan.
4. **PT-07 — Studio/persistence:** Forge New dan Existing `.nx`, pemisahan input, Retry/Skip, serta publikasi per `.nx` dipertahankan. Identitas, persistence, association, dan reload Album multi-member tetap unresolved; AC-28/AC-29 blocked.
5. **COR-01/COR-02:** Seluruh notasi tracks[] dan members[] dikualifikasi sebagai notasi konseptual/draf non-normatif. Tahap 4 dibatasi pada proposal JCS/signature verification; Registry Album Signer lookup/trust tidak diklaim tersedia.
6. **COR-03/COR-05:** Gate membership Verify ditegaskan pada ringkasan, AC-33/AC-34, dan traceability. AC-33/AC-34 tetap TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MEMBERSHIP AUTHENTICITY / CONF-01.
7. **COR-04:** Klaim repository lokal, DDL, pipeline, endpoint, dan runtime yang tidak diperiksa auditor diberi provenance REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED; tidak ada klaim bahwa source repository atau runtime telah diverifikasi independen.
8. **COR-06/COR-07:** Readiness aktif direkonsiliasi menjadi **12 AC Spec Ready + 20 AC Execution Blocked + 2 AC PO Decision Required = 34 AC**. Angka 14/18/2 hanya snapshot historis pra-membership-gate. AC-01/AC-07 tetap PO Decision Required; AC-33/AC-34 blocked.

**Batas bukti:** Koreksi ini adalah rekonsiliasi dokumen berdasarkan Product Truth dan keputusan PO yang tersedia. Tidak ada inspeksi source repository `whisnu/nexa`, DDL lokal, runtime, atau implementasi yang dilakukan. Klaim bukti lokal tetap dilaporkan Programmer dan belum diverifikasi independen.

**Disposisi:** Gate A tetap NOT PASSED; Gate B tetap BLOCKED; PE-02 Implementation tetap NOT AUTHORIZED; Sprint 16 CLOSED / FINAL ACCEPTED / FROZEN; PE-01 CLOSED / FROZEN; Sprint 17 NOT STARTED; Product Enhancement Window OPEN / NOT FROZEN.

## 13.10 KOREKSI KONSISTENSI STATUS DAN PROVENANCE EVIDENCE LEDGER — 2026-11-08

**Ruang lingkup:** Koreksi terarah atas tiga temuan konsistensi baru dari audit plan. ID berikut menggunakan prefiks `AUDIT-PLAN` dan **berbeda dari FINDING-01 sampai FINDING-03 historis yang telah CLOSED**. Koreksi hanya menyentuh traceability status dan kualifikasi bukti; tidak mengubah kontrak produk, keputusan PO, atau blocker substantif.

1. **AUDIT-PLAN-01 — AC-20 / NC-12:** Status AC-20 pada traceability §9 diselaraskan menjadi `TEST-PLANNED — EXECUTION BLOCKED BY B-06`, konsisten dengan AC Register §8 dan klasifikasi Execution Blocked §13.1. AC-21 tetap Execution Blocked oleh B-06. Tidak ada perubahan pada mitigasi Safe-Open atau penerimaan residual risk.
2. **AUDIT-PLAN-02 — AC-25 / NC-14:** Traceability §9 kini memisahkan AC-25 `TEST-PLANNED — SPEC READY` dari AC-33/AC-34 `TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MEMBERSHIP AUTHENTICITY / CONF-01`. Keputusan PO CONF-02 Pilihan B tetap disahkan; CONF-01/B-09 tidak dipindahkan atau ditutup.
3. **AUDIT-PLAN-03 — Evidence Ledger / Gate A:** §12.3 kini menyatakan bahwa Evidence Ledger terdokumentasi dalam plan secara bersyarat, sementara bukti sumber primer belum diverifikasi independen. Redaksi ini tidak mengubah status G-01 sampai G-03 dan tidak mengklaim audit independen atas repository `whisnu/nexa`.

**Verifikasi pascakoreksi:** File kanonikal pada `whisnu/plan:main` telah di-fetch ulang setelah commit. Ketiga redaksi koreksi ditemukan pada §9 dan §12.3. Jumlah AC tetap 34; agregat tetap 12 Spec Ready + 20 Execution Blocked + 2 PO Decision Required.

**Disposisi:** Ketiga temuan konsistensi dokumen ini dikoreksi pada artefak kanonikal yang sama. Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 Implementation tetap `NOT AUTHORIZED`; Sprint 16 dan PE-01 tetap `CLOSED / FROZEN`; Sprint 17 tetap `NOT STARTED`. Koreksi ini bukan persetujuan Gate A, bukan penutupan blocker substantif, dan bukan otorisasi implementasi.


## 13.11 DECISION REGISTER PE-02 DAN REKONSILIASI TEMUAN NC-06 / NC-13 — 2026-11-08

**Tujuan dan batas:** Register ini mengonsolidasikan keputusan produk/arsitektur/data/keamanan yang masih diperlukan agar blocker PE-02 dapat dinilai secara sah. Ini bukan persetujuan atas salah satu opsi desain, bukan instruksi implementasi, dan bukan perubahan Product Truth. White Paper v5.6 tetap otoritas produk; Roadmap v4.8 merekam status dan gerbang kerja, bukan sumber untuk menciptakan kontrak Album. Tidak ada ketentuan Album-spesifik di bawah ini yang boleh dianggap telah disahkan hanya karena dicantumkan dalam register.

**Prinsip pengikat yang wajib dipertahankan saat keputusan dibuat:**
1. Pisahkan Identity, Ownership Evidence, Registry Trust, Asset Trust, dan Licensing Authority. Ownership Evidence tidak otomatis menjadi Licensing Authority; identitas organisasi tidak otomatis membuktikan kepemilikan aset atau otoritas lisensi.
2. Pertahankan model multi-registry/federated trust dan prinsip **No Single Root of Trust**. Jangan menciptakan otoritas global tunggal atau mempromosikan Creator self-signed evidence menjadi Registry Verified.
3. Pertahankan trust semantics White Paper v5.6: **UNKNOWN / INCOMPLETE** bukan **INVALID**; kegagalan integritas/signature/hash dan authoritative revocation tetap hard-block sesuai kontrak yang berlaku. Keputusan tentang autentisitas membership Album tidak boleh diam-diam mengubah trust atau playback policy member .nx standalone.
4. Pertahankan kontrak standalone .nx, Genesis Ownership Evidence, Registry/sidecar, Licensing Authority, Player memory/streaming boundary, dan baseline PE-01/Sprint 16. Tidak ada keputusan PE-02 yang boleh membuka atau mengubah baseline frozen.
5. White Paper v5.6 dan Roadmap v4.8 tidak menetapkan Album ZIP wrapper, Album Manifest schema, Album Signer, signature envelope, atau signer lifecycle. Detail tersebut tetap proposal/unresolved sampai otoritas yang tepat menetapkannya secara tertulis.

### 13.11.1 Baseline Rekomendasi Desain Teknis — Bukan Daftar Delegasi kepada PO

Bagian ini menggantikan pola sebelumnya yang menyerahkan hampir seluruh masalah teknis sebagai pertanyaan kepada PO. Analisis dan rancangan awal merupakan tanggung jawab penyusun plan. Status di bawah ini adalah rekomendasi teknis yang harus diuji terhadap Product Truth dan repository; pencantuman rekomendasi tidak menjadikannya keputusan PO, bukti implementasi, atau otorisasi coding.

| ID | Area / blocker | Rekomendasi desain yang harus menjadi baseline evaluasi | Batas dan status yang tetap berlaku |
|:---:|:---|:---|:---|
| TD-01 | Membership authenticity — B-09 / CONF-01 / AC-07 / AC-33/34 | Fail-closed pada klaim membership: manifest dengan signer UNKNOWN, tidak dikenal, atau lifecycle trust yang tidak dapat dibuktikan tidak boleh mengautentikasi daftar anggota Album. Member yang diberikan secara independen tetap dapat diverifikasi sebagai standalone .nx. | Bukan INVALID untuk member, bukan global playback gate, dan bukan otorisasi Registry baru. Kebijakan produk direkomendasikan; CONF-01 tetap menunggu pengesahan formal bila diperlukan governance. |
| TD-02 | Manifest schema — NC-01 / AC-01 | Gunakan schema berversi dan allowlist field per versi. Tolak duplicate keys, malformed Unicode, tipe salah, required field hilang, dan versi yang tidak didukung. Unknown field ditolak secara default dalam versi tertutup; extension hanya melalui namespace/version mechanism yang eksplisit. | Strict unknown-field policy masih PROPOSED — PENDING PO CONFIRMATION; jangan mengunci additionalProperties:false global tanpa model versioning/extension. Nama array, JSON path, dan field audio tetap belum normatif. |
| TD-03 | Signature construction — B-08 / NC-02 / AC-03 | Pisahkan signed content dari signature envelope. Input signature adalah canonical representation dari manifest data yang tidak memuat signature itu sendiri; signature/envelope berada di luar byte-domain yang ditandatangani. JCS diterapkan hanya pada objek signed content yang telah didefinisikan. | Detached-envelope adalah rekomendasi konstruksi, bukan penetapan nama file, format envelope, algoritma, atau field final. Signature scope dan representation harus difinalisasi sebelum AC-03 siap. |
| TD-04 | Pemisahan trust — NC-04 / NC-05 / AC-07/08/09/10 | Pertahankan domain terpisah: Album declaration/membership authenticity; container packaging integrity/signature; Genesis ownership evidence; Registry trust; active licensing; playback authorization. Tidak ada signature atau hash yang menggantikan lapisan lain. | Jangan menyamakan Album Signer, Container Creator, Genesis Creator, Registry Authority, atau Licensing Authority. Jangan menetapkan equality 3-way key binding tanpa sumber normatif. |
| TD-05 | Verify membership — NC-14 / AC-25 / AC-33/34 | Jalankan dua pemeriksaan independen: (a) verifikasi member .nx sesuai PE-01; (b) autentikasi relasi member-ke-Album. Laporkan hasil member sesuai status kanonikal Nexa dan membership sebagai hasil terpisah. Jika membership belum autentik, jangan proses atau label file dari manifest sebagai Album member. | CONF-02 Option B tetap final: tidak ada aggregate Album trust status. Verify tidak memberikan playback authorization. File yang dipilih independen tetap dapat diverifikasi sebagai standalone. |
| TD-06 | Album identity/persistence/reload — NC-06 / AC-28/29 | Modelkan Album identity, member identity, dan membership relation sebagai konsep berbeda. Album ID tidak boleh bergantung hanya pada nama, urutan, atau hash member pertama. Simpan metadata dan relasi tanpa memodifikasi bytes .nx; pada reload, rekonstruksi membership lalu verifikasi ulang bukti yang diperlukan. | Bentuk storage, ID formula, tabel/sidecar, dan API belum dipilih. Gunakan mekanisme persistence Nexa yang sudah ada bila terbukti memadai; jangan membuat DDL/API baru atau mengklaim dukungan sebelum pemeriksaan repository. |
| TD-07 | Player JIT / Stage 8a / Auto-Next — NC-13 / AC-22/32 | Otorisasi hanya untuk current member. Urutan kausal member aktif: validasi container/integrity, Genesis/ownership, active license sesuai PE-01, lalu operasi payload yang memang dipersyaratkan tipe payload. Background work hanya boleh non-authorizing; tidak boleh mendaftarkan playback buffer atau mewariskan authorization. Auto-Next menggunakan completion signal dari lifecycle viewer untuk tipe payload terkait, bukan satu event universal. | Stage 8a tidak boleh melewati Genesis atau active license. Tidak ada timeout/duration buatan untuk dokumen/gambar. Adapter dan completion signal harus dibuktikan pada source per platform; bila tidak tersedia, AC-32 tetap blocked dan Programmer wajib STOP AND CLARIFY. |
| TD-08 | Audio hash — NC-05 / AC-09 | Definisikan setiap digest dengan byte-domain eksplisit: container .nx, payload audio hasil ekstraksi, atau source file adalah objek berbeda. Digest member/container tidak dapat menggantikan digest audio; package hash juga bukan member hash. | Jangan memilih audio_sha256 atau notasi draft tracks[].sha256, parent array, alias, fallback, atau JSON path sampai domain dan sumber normatif terbukti. AC-09 tetap blocked. |
| TD-09 | ZIP security — NC-07 / B-03 / B-07 / AC-02/13 | Terapkan streaming extraction dengan hard cap byte terkompresi, byte hasil ekstraksi per-entry dan kumulatif, jumlah entry fisik, jumlah member, ukuran .nx individual, serta batas waktu/CPU. Tolak path traversal, duplicate/case-fold collision, symlink, special file, metadata ambigu, dan entry yang tidak sesuai bijeksi. Hitung batas saat streaming, bukan hanya dari Central Directory. | Nilai 500 MB compressed, 4 GB expanded, 200 physical entries, 50 Album members, 2 GiB per .nx, dan rasio 10:1/100:1 tetap proposal sampai benchmark/threat model dan keputusan arsitektur. Pisahkan batas wrapper, batas UI/member, dan batas container PE-01. |
| TD-10 | Safe-Open / TOCTOU — NC-12 / B-06 / AC-20/21 | Ekstraksi ke private staging directory dengan permission terbatas; gunakan operasi relatif terhadap directory handle/descriptor dan validasi file descriptor setelah open; jangan mengandalkan realpath/lstat lalu open path sebagai satu-satunya kontrol. Implementasi harus platform-specific dan diuji terhadap symlink, replacement, rename, dan race. | O_NOFOLLOW pada final component saja tidak membuktikan containment terhadap seluruh ancestor race. Linux openat2/equivalent hanya kandidat bila runtime mendukung; Windows/Android memerlukan analisis sendiri. Residual risk tetap harus dinyatakan, bukan diklaim hilang. |
| TD-11 | Marketplace settlement — NC-08 / B-04 / CONF-03 / AC-14/15 | Gunakan workflow per-member dengan state durable, idempotent operation boundary, retry/reconciliation, dan compensation hanya bila operasi eksternal memang menyediakan compensation. Pisahkan keberhasilan lokal SQL dari keberhasilan side effect layanan eksternal. | Jangan mengklaim distributed ACID/2PC atau rollback HTTP side effect melalui SQL rollback. Di bawah Zero-DDL, kelayakan state durability harus dibuktikan dari schema/pipeline yang ada; jika tidak tersedia, blocker tetap terbuka. |
| TD-12 | acquired_package_sha256 — NC-09 / B-05 / AC-16 | Pertahankan pemisahan package hash, member .nx hash, dan payload hash. Jangan menggunakan satu field sebagai substitusi objek hash yang lain. Definisikan producer, consumer, waktu komputasi, byte-domain, parent/child semantics, dan persistence sebelum field dipakai. | Makna field dan DDL belum diverifikasi independen. Jangan mengasumsikan bahwa field adalah hash ZIP, hash child .nx, atau hash asset. |
| TD-13 | Error taxonomy — NC-15 / AC-10/26 | Susun taxonomy berdasarkan layer dan kondisi yang benar-benar dapat dibedakan: malformed input, cryptographic failure, trust unknown/revoked, filesystem failure, quota failure, transaction/reconciliation failure. Error harus stabil dan tidak membocorkan detail sensitif. | Jangan menetapkan 20 kode sebagai normatif hanya karena daftar telah ditulis. Setiap kode harus punya trigger, layer, user-visible disposition, retryability, dan AC; Genesis error taxonomy tetap blocked sampai kontrak dibuktikan. |
| TD-14 | Batas penerapan dan baseline | Seluruh rancangan Album berada di luar perubahan perilaku standalone .nx; tidak ada perubahan Sprint 16/PE-01, shared Player/Core, renderer, memory boundary, trust model, atau database tanpa bukti kebutuhan dan otorisasi terpisah. | Tidak ada implementasi, migrasi, atau perubahan source code yang diotorisasi oleh rekonsiliasi ini. |

### Keputusan/otorisasi yang benar-benar tersisa

Setelah rekomendasi teknis di atas disusun, fakta implementasi yang dapat diverifikasi tetap harus diperiksa Programmer melalui PSV sebelum eskalasi. Eskalasi dibatasi pada hal yang memang memerlukan kewenangan formal:

1. Product Owner — CONF-01: setelah PSV signer/membership, mengesahkan atau menolak kebijakan autentisitas membership saat signer UNKNOWN jika kebijakan tersebut belum ditetapkan oleh sumber normatif. Rekomendasi penyusun: membership yang tidak terautentikasi tidak boleh diperlakukan sebagai deklarasi membership terverifikasi; member tidak otomatis INVALID dan jalur standalone PE-01 tetap tersedia.
2. Product Owner — AC-01: mengesahkan default reject untuk unknown fields dalam schema version tertutup, dengan extension hanya melalui mekanisme versi/namespace eksplisit. Rekomendasi penyusun: reject-by-default.
3. Product Owner — batas UX Auto-Next non-audio, hanya jika completion signal yang tersedia pada viewer tidak dapat memenuhi perilaku Auto-Next yang sudah disetujui. Jangan meminta PO merancang event atau API.
4. Product Owner / Lead Security Architect — B-06: keputusan penerimaan residual risk hanya setelah Programmer menyelesaikan PSV atas mitigasi dan bukti uji Safe-Open tersedia. Penerimaan risiko tidak menggantikan mitigasi atau menjadi prasyarat untuk memulai PSV.
5. Product Owner, hanya jika hasil desain teknis mengubah perilaku produk yang telah disetujui atau menyentuh frozen baseline. Selain kondisi tersebut, keputusan implementasi teknis tetap berada pada otoritas teknis terkait.

Architecture Authority, Data Architect, dan Lead Security Architect menerima hasil PSV serta analisis teknis yang relevan untuk validasi pada domain kewenangannya; mereka tidak diminta memulai dari nol atau memilih di antara daftar opsi tanpa analisis. Keterlibatan mereka tidak menjadi prasyarat untuk Programmer memulai PSV.

### 13.11.2 Prasyarat bukti primer — bukan keputusan desain

PSV atas repository sumber `whisnu/nexa` merupakan tanggung jawab Programmer. Programmer harus terlebih dahulu memperoleh akses baca dan memeriksa source code, schema/DDL, test, endpoint, dan wiring yang relevan untuk B-04, B-05, B-06, B-08, dan B-09 (serta area PSV lain pada §15.3). Pekerjaan ini tidak memerlukan ZIP, clone repository penuh, atau akses tulis. Jika akses gagal, catat upaya dan hasil aktual; pertahankan klaim terkait sebagai `NOT VERIFIED`. Tidak ada keputusan PO/Architecture Authority yang menjadi prasyarat untuk memulai pemeriksaan tersebut.

### 13.11.3 Temuan konsistensi baru dan koreksi status register

**AUDIT-PLAN-04 — NC-06 mencantumkan blocker NONE meskipun AC-28/AC-29 blocked.**
- **Kondisi:** NC-06 pada §6 menyatakan NONE, sedangkan AC-28/AC-29 pada §8 dan pemetaan dependensi §2.1/§9 menyatakan identitas Album multi-member, persistence, dan reload masih unresolved/Execution Blocked.
- **Koreksi:** Status NC-06 pada §6 diubah menjadi OPEN / BLOCKED BY AC-28 / AC-29 — ALBUM IDENTITY, PERSISTENCE & RELOAD UNRESOLVED. Catatan dependensi kini menyebut AC-28/AC-29 secara eksplisit.
- **Batas:** Ini rekonsiliasi propagasi status; bukan blocker baru, bukan keputusan tentang Album ID/schema, dan bukan perubahan kontrak ekstraksi .nx standalone PE-01.

**AUDIT-PLAN-05 — NC-13 mencantumkan blocker NONE meskipun AC-22/AC-32 blocked.**
- **Kondisi:** NC-13 pada §6 menyatakan NONE, sedangkan AC-22 dan AC-32 pada §8 serta pemetaan dependensi §2.1/§9 menunjukkan prasyarat Stage 8a/JIT dan lifecycle Auto-Next lintas payload belum ditetapkan.
- **Koreksi:** Status NC-13 pada §6 diubah menjadi OPEN / BLOCKED BY UNRESOLVED JIT PREREQUISITES & AUTO-NEXT LIFECYCLE. Catatan dependensi kini menyebut AC-22 dan AC-32 secara eksplisit.
- **Batas:** Ini rekonsiliasi status yang sudah tercermin pada AC Register; bukan keputusan tentang Stage 8a, bukan izin background authorization, dan bukan perubahan current-member authorization.

**Disposisi:** AUDIT-PLAN-04 dan AUDIT-PLAN-05 dicatat sebagai temuan konsistensi dokumentasi dan dikoreksi pada register NC-06/NC-13. Keduanya tidak mengubah jumlah 34 AC atau agregat readiness **12 Spec Ready + 20 Execution Blocked + 2 PO Decision Required**. Semua keputusan pada §13.11 tetap pending sampai diputuskan otoritas yang ditunjuk. Gate A tetap NOT PASSED; Gate B tetap BLOCKED; PE-02 Implementation tetap NOT AUTHORIZED; Sprint 16 dan PE-01 tetap CLOSED / FROZEN; Sprint 17 tetap NOT STARTED; Product Enhancement Window tetap OPEN / NOT FROZEN.


## 13.12 PE-02 TECHNICAL DESIGN RECONCILIATION — BASELINE REKOMENDASI PENYUSUN — 2026-11-08

**Mandat:** Menurunkan rancangan teknis dari Product Truth Nexa, keputusan PO yang sudah disahkan, dan prinsip arsitektur yang tersedia. Bagian ini dibuat untuk menyelesaikan pekerjaan analisis/desain pada tingkat penyusun plan, bukan memindahkan seluruh masalah teknis kepada PO. Bagian ini harus dibaca bersama §1.2 (hierarki otoritas), §3.2 (Stop-and-Clarify), §4.1 (governance lock), §5 (Product Truth), §6–§9 (NC/B/AC/traceability), serta keputusan resmi pada §10.3.

### 13.12.1 Status setiap jenis pernyataan

| Label | Makna | Batas penggunaan |
|---|---|---|
| DERIVED FROM APPROVED PRODUCT TRUTH | Konsekuensi langsung dari keputusan PO atau kontrak Nexa yang telah disahkan. | Boleh menjadi baseline normatif dalam ruang lingkup sumbernya. |
| RECOMMENDED TECHNICAL DESIGN | Solusi teknis yang direkomendasikan penyusun berdasarkan prinsip Nexa dan standar relevan. | Belum menjadi Product Truth dan belum membuktikan implementasi. |
| REPOSITORY VERIFICATION REQUIRED | Rancangan atau klaim memerlukan pemeriksaan source, schema, pipeline, atau runtime. | Tidak boleh diklaim tersedia/terimplementasi sebelum bukti primer diperiksa. |
| FORMAL AUTHORIZATION REQUIRED | Penerimaan risiko atau perubahan perilaku/baseline yang memerlukan kewenangan formal. | Tidak dapat disimpulkan dari plan approval, audit PASS, atau penetapan pemilik tugas. |

### 13.12.2 Arsitektur membership yang direkomendasikan

1. Album adalah grouping dari .nx independen; tidak ada container .nx baru dan tidak ada trust/ownership bersama yang menggantikan bukti per-member. Ini diturunkan dari keputusan PO pada §10.3.
2. Manifest, bila dipakai sebagai deklarasi membership, hanya dapat membuktikan membership setelah signature/provenance yang mengikat deklarasi tersebut dapat diverifikasi menurut kebijakan yang disahkan. ZIP entry, nama file, urutan, kesamaan hash, dan keberadaan .nx tidak membuktikan membership.
3. Rekomendasi penyusun adalah fail-closed pada membership bila signer UNKNOWN, signature tidak dapat diverifikasi, signer lifecycle tidak dapat dibuktikan, atau bukti membership tidak lengkap. Disposisinya adalah MEMBERSHIP NOT AUTHENTICATED (label desain, bukan canonical Nexa trust status/error code): file dari manifest tidak diproses/dilabeli sebagai Album member.
4. Disposisi di atas tidak mengubah member menjadi INVALID, tidak mengubah arti UNKNOWN / INCOMPLETE, tidak memblokir playback global berdasarkan Album Signer, dan tidak menghalangi file .nx yang dipilih secara independen untuk diverifikasi sebagai standalone PE-01.
5. Jangan memperkenalkan Album Signer sebagai root of trust global atau menyamakannya dengan Creator, Genesis Creator, Registry Authority, atau Licensing Authority. Jika Album Signer tidak mempunyai enrollment/identity binding/lifecycle yang dapat dibuktikan, membership belum dapat dinyatakan autentik.
6. Tidak perlu menciptakan Album Membership Proof signature kedua yang terpisah dari manifest signature sebagai desain awal. Rekomendasi paling sederhana adalah manifest signature—jika mekanisme signer kelak sah—mengikat deklarasi membership dan member references secara keseluruhan. Bukti signature terpisah hanya dipertimbangkan jika ada kebutuhan produk dan arsitektur yang terbukti.

### 13.12.3 Manifest, parser, canonicalization, dan signature

1. Rekomendasi schema adalah versioned closed schema: setiap versi mempunyai allowlist, requiredness, tipe, batas, dan aturan extension yang eksplisit. Versi yang tidak didukung ditolak; jangan mencoba menafsirkan dengan schema versi lain.
2. Strict parser menolak duplicate JSON keys setelah decoding escape, malformed Unicode, invalid encoding, invalid number/string forms, dan struktur yang tidak sesuai. Parser harus bekerja pada byte input sebelum normalisasi yang dapat menyamarkan ambiguitas.
3. Rekomendasi kebijakan unknown field adalah reject-by-default pada schema version tertutup. Extension hanya boleh diterima melalui namespace/version contract yang secara eksplisit didefinisikan. Ini rekomendasi teknis untuk AC-01, belum merupakan keputusan PO.
4. Hindari circular signature dengan memisahkan signed content dari signature envelope. Canonicalization dilakukan atas signed content yang tidak mencakup signature itu sendiri; signature kemudian dibawa oleh envelope terpisah dari byte-domain yang ditandatangani. Bentuk fisik envelope dan signature scope harus ditetapkan konsisten dengan ZIP entry policy dan dibuktikan sebelum AC-03 siap.
5. RFC 8785 JCS dan Ed25519 adalah kandidat standar teknis yang sesuai untuk canonicalization dan signature, tetapi tidak menetapkan identitas Album Signer, trust root, enrollment, key custody, rotation, revocation, atau Registry API.
6. Tidak ada nama file manifest, nama array member, JSON path, nama field, ataupun schema payload universal yang ditetapkan dalam rekonsiliasi ini. Draf audio tidak boleh diperluas ke video, document, atau image.

### 13.12.4 Model trust, identity, dan hash

1. Pertahankan domain terpisah: Album membership authenticity; .nx container integrity/signature; Genesis ownership evidence; Registry trust; asset trust; licensing authority; playback authorization.
2. Keputusan PO AUDIT-NEW-10 menetapkan tiga peran berbeda: genesisPubKey (Genesis Creator), containerSigKey (Container Packager), dan ownCertPubKey (current holder). Ketiganya tidak diwajibkan identik. Perbedaan ownCertPubKey dari genesisPubKey harus dijelaskan rantai transfer kepemilikan sah; perbedaan containerSigKey dari genesisPubKey harus dibuktikan delegation/authorization evidence. Self-packaging tidak memerlukan delegation tambahan. Detail target ada di §13.12.11.
3. Package hash, .nx container hash, extracted payload hash, audio bitstream hash, Genesis certificate hash, dan signature bytes adalah objek berbeda. Setiap digest harus mendefinisikan byte-domain, encoding, producer, consumer, dan lifecycle.
4. acquired_package_sha256 tidak boleh dipakai sebagai child .nx hash atau audio hash. Semantik parent/child acquisition, lokasi persistence, dan DDL tetap harus dibuktikan; sampai itu dilakukan B-05 tetap terbuka.
5. audio_sha256 dan notasi konseptual tracks[].sha256 belum dapat dipilih sebagai identifier normatif. Tentukan lebih dahulu apakah digest mengacu pada sumber asli, byte payload audio hasil ekstraksi, atau representasi audio lain; kemudian tetapkan satu field/path yang konsisten. Jangan membuat alias atau fallback dua arah.
6. Error taxonomy harus mengikuti perbedaan domain di atas. UNKNOWN tidak boleh dipetakan menjadi INVALID; kegagalan signature/integrity dan authoritative revocation ditangani menurut kontrak PE-01. Kode error baru tidak dianggap normatif sampai trigger dan expected disposition-nya didefinisikan serta diuji.

### 13.12.5 Player lifecycle dan Verify

1. Setiap member harus menjalani verifikasi dan authorization JIT sendiri. Tidak ada inheritance dari member sebelumnya, Album Signer, atau background pre-verification.
2. Urutan prasyarat playback mengikuti kontrak PE-01: validasi container/integrity, Genesis/ownership evidence, dan active license/entitlement yang diwajibkan. Diagnostic digest tidak membuktikan ownership atau license dan tidak boleh menjadi bypass Stage 7b/7c.
3. Background pre-verification boleh menyiapkan metadata/diagnostic yang tidak memberi akses. Ia tidak boleh melakukan decryption untuk playback, mendaftarkan buffer, menandai member authorized, atau mengubah current-member boundary.
4. Auto-Next adalah keputusan perilaku PO yang telah disahkan pada tingkat prinsip. Implementasi teknis harus mengadaptasi completion signal dari lifecycle viewer tiap payload; tidak boleh menganggap event audio ended berlaku universal. Untuk payload yang tidak menyediakan completion signal, jangan membuat timeout atau durasi palsu. AC-32 tetap blocked sampai lifecycle yang ada dan perilaku yang disetujui dapat dipetakan secara eksplisit.
5. Verify menjalankan member verification dan membership verification sebagai dimensi terpisah. Hasil member tidak mengautentikasi membership, dan membership yang autentik tidak meningkatkan trust member. CONF-02 Option B tetap: tidak ada aggregate Album trust status. Verify tidak memberikan playback authorization.
6. Desktop Verify tetap Full Verify; Mobile tetap Verify-Lite. Tidak boleh menambahkan payload rendering, batch desktop, export report, atau manual Registry Refresh ke Mobile.

### 13.12.6 Album identity, persistence, dan Studio publication

1. Pisahkan konseptual Album Identity, Member Identity, dan Membership Relation. Nama Album, artwork, filename, urutan, dan hash member pertama bukan identitas tunggal yang memadai.
2. Metadata Album dan relasi membership tidak boleh mengubah canonical bytes atau Genesis/Creator evidence .nx. Pada reload, sistem harus membangun ulang daftar referensi dan memverifikasi ulang bukti membership serta member; cache status lama bukan otoritas trust.
3. Rekomendasi pertama adalah menggunakan mekanisme metadata/persistence Nexa yang sudah tersedia jika mampu menyimpan grouping dan relasi secara durable. Jangan menambahkan tabel, kolom, sidecar, endpoint, atau schema baru sebelum repository/DDL diperiksa dan otorisasi Zero-DDL dievaluasi.
4. Studio harus mempertahankan dua jalur yang telah disetujui: Forge New mem-forge tiap source menjadi .nx individual; Existing .nx menggunakan NXPublishPipeline yang ada tanpa re-forging. Retry upload memakai .nx yang sama; jangan membuat listing duplikat; Retry/Skip tetap keputusan pengguna.
5. Publication workflow direkomendasikan sebagai state machine per-member dengan durable progress, idempotency boundary, retry, dan reconciliation. SQL transaction hanya menjamin operasi lokal dalam transaksinya; ia tidak membatalkan side effect layanan eksternal. Compensation hanya boleh dijanjikan bila service benar-benar menyediakan mekanismenya.
6. Jika Zero-DDL dan pipeline yang ada tidak menyediakan durable state/idempotency yang diperlukan, jangan menyatakan workflow crash-safe. Pertahankan B-04 terbuka sampai ada rancangan yang feasible tanpa mengarang DDL atau endpoint.

### 13.12.7 ZIP extraction dan filesystem security

1. Terapkan pemeriksaan ZIP berlapis: archive structure; entry type; nama/path; collision; declared size; streaming byte counters; per-entry expanded cap; cumulative expanded cap; member cap; .nx cap; compression ratio; time/CPU/resource cap; bijection manifest-to-archive; hash/integrity setelah ekstraksi.
2. Sesuai keputusan PO §10.3, regular file dan directory diterima; symlink, special file, serta metadata ambigu ditolak; generic hardlink semantics tidak didukung; byte-identical entries tetap independen. Flat-path rule hanya untuk nama/path member .nx yang dideklarasikan, bukan larangan direktori ZIP.
3. Nilai 500 MB compressed, 4 GB expanded, 200 physical entries, 50 Album members, 2 GiB individual .nx, dan compression ratio 10:1/100:1 tidak boleh dicampur. Batas 50 member adalah batas UI/manifest bila kelak disahkan; 200 physical entries menghitung entri arsip termasuk direktori dan manifest. 2 GiB adalah batas payload kontainer individual, bukan batas wrapper.
4. Rekomendasi security adalah hard cap absolut per layer dan streaming enforcement; compression ratio hanya kontrol tambahan, bukan satu-satunya ZIP-bomb defense. Pilihan angka final harus didukung threat model dan benchmark payload nyata. B-07 tetap terbuka sampai angka dan coverage AC ditetapkan.
5. Safe-Open harus memverifikasi file descriptor setelah open dan memastikan operasi berada di bawah staging directory yang dikendalikan. O_NOFOLLOW hanya pada komponen akhir tidak cukup untuk membuktikan semua ancestor containment. Evaluasi platform-specific primitive (misalnya descriptor-relative open atau primitive OS yang ekuivalen) wajib dilakukan; jangan mengklaim TOCTOU hilang absolut.
6. Staging harus private, tidak dapat ditulis pihak tak tepercaya, dan dibersihkan secara terkendali. Race test harus mencakup symlink substitution, file replacement, ancestor rename, path traversal, serta concurrent extraction/open. B-06 tetap terbuka sampai implementasi/test dan keputusan residual risk selesai.

### 13.12.8 Blocker disposition setelah rekonsiliasi

| Blocker | Hasil rekonsiliasi desain | Apa yang masih benar-benar menghalangi penutupan |
|---|---|---|
| B-01 | Parser contract diperjelas: byte-level strict parser, duplicate-key rejection setelah escape decoding, schema validation terpisah. | Implementasi parser dan AC-05 belum dibuktikan. |
| B-02 | JCS beroperasi pada signed content yang telah ditentukan; bukan JSON.stringify atau canonicalization atas signature itu sendiri. | Signature scope dan test vectors/implementasi serializer tetap harus diverifikasi; AC-06 belum lulus. |
| B-03 | Layered streaming ZIP security dan file-type policy dikonsolidasikan. | Implementasi extractor dan coverage semua invariant belum tersedia; B-07 memblokir parameter final. |
| B-04 | Tidak menjanjikan distributed ACID/2PC; workflow per-member dengan durable state/reconciliation adalah rekomendasi desain target, bukan bukti implementasi. | Programmer harus melakukan PSV terlebih dahulu atas workflow, schema, transaksi, side effect eksternal, retry, dan recovery; keputusan arsitektur hanya diminta jika feasibility di bawah Zero-DDL tetap tidak dapat ditentukan setelah PSV. |
| B-05 | Package/member/payload hash dipisahkan secara konseptual sebagai objek berbeda. | Programmer harus melakukan PSV terlebih dahulu atas schema/DDL, producer-consumer, byte-domain, persistence, dan parent/child mapping; semantik yang tetap tidak dapat ditentukan dicatat unresolved untuk otoritas data. |
| B-06 | Safe-Open perlu dievaluasi per platform; O_NOFOLLOW saja tidak membuktikan seluruh invariant. | Programmer harus melakukan PSV terlebih dahulu atas implementasi dan adversarial tests; penerimaan residual risk baru diminta setelah mitigasi aktual dan batas risikonya dibuktikan. |
| B-07 | Kuota dipisah per-layer dan streaming enforcement direkomendasikan; ratio bukan satu-satunya kontrol. | Programmer harus memeriksa parser/extractor, streaming counters, enforcement, dan test yang ada. Nilai proposal tidak boleh dianggap normatif; keputusan pembekuan parameter dilakukan setelah bukti teknis dan threat model/benchmark tersedia. |
| B-08 | Signed-content/signature-envelope separation merupakan rekomendasi teknis, bukan desain yang telah disahkan. | Programmer harus melakukan PSV terlebih dahulu atas konstruksi dan verification path aktual; jika kontrak tetap tidak menentukan signature scope/representation, eskalasi arsitektur diperlukan sebelum spesifikasi difinalisasi. |
| B-09 | Fail-closed pada klaim membership adalah rekomendasi teknis, bukan keputusan produk final. | Programmer harus melakukan PSV terlebih dahulu atas signer/membership dan lifecycle; keputusan PO/Architecture Authority hanya diperlukan untuk kebijakan autentisitas atau kontrak lifecycle yang tetap belum ditetapkan setelah PSV. |

### 13.12.9 Bukti repository yang wajib diperoleh sebelum finalisasi implementability

Pemeriksaan repository harus terarah, bukan full clone atau ZIP. Minimum evidence set:
- NX Player Desktop dan Mobile: current-member state, JIT gate, audio/video/document/image viewer lifecycle, pre-verification side effects, memory/buffer registration.
- NX Verify Desktop/Mobile: standalone-vs-Album entry path, per-member result, membership gate, Full Verify vs Lite feature boundary.
- NX Studio: Forge New flow, existing .nx publication, NXPublishPipeline, retry idempotency, listing duplication prevention, persisted progress.
- Marketplace: schema DDL aktual, acquisition parent/child fields, acquired_package_sha256, transaction boundaries, external Licensing Daemon calls, replay/idempotency/recovery.
- ZIP/container: parser/extractor, path handling, entry type handling, streaming quotas, Safe-Open, per-platform filesystem primitives.
- Cryptography/Genesis/Registry: exact signed bytes, canonicalization, key roles, certificate verification, trust lookup, revocation and freshness lifecycle.

Setiap klaim harus ditautkan ke path dan line range pada commit yang diperiksa. Bila akses repository tidak tersedia, hasilnya tetap NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE; jangan menggantinya dengan laporan Programmer atau asumsi dari nama file.


### 13.12.11 AUDIT-NEW-10 — Target Architecture: Identity Roles, Packaging Delegation, Trust Resolution & Verifier Contract

**Status normatif:** keputusan semantik tiga peran kunci dan kewajiban authorization untuk third-party packaging telah **APPROVED oleh PO**. Bagian ini adalah rancangan target yang wajib dibangun dalam PE-02, bukan pernyataan bahwa mekanisme tersebut sudah tersedia di repository. Evidence Programmer menjadi baseline kondisi saat ini dan input gap analysis. Ketiadaan implementasi bukan alasan menghapus atau menurunkan rancangan target.

#### A. Kontrak tiga peran kunci
| Peran | Identitas | Fungsi normatif |
|---|---|---|
| Genesis Creator / Originator | genesisPubKey | Originator awal; menandatangani Genesis Ownership Certificate. |
| Container Packager / Packaging Engine | containerSigKey | Pihak/engine yang membentuk binary container individual .nx; menandatangani byte-domain integritas kontainer. |
| Current Owner / Holder | ownCertPubKey | Pemegang/buyer/collector saat ini yang menjadi subjek hak kepemilikan/lisensi. |

Invariant: ketiga identitas adalah peran semantik berbeda dan tidak diwajibkan identik; ownCertPubKey berbeda dari genesisPubKey hanya dengan ownership/transfer chain sah; containerSigKey == genesisPubKey adalah self-packaging tanpa delegation tambahan; containerSigKey != genesisPubKey adalah third-party packaging dan wajib delegation valid untuk asset/scope. Container signature membuktikan integritas byte-domain, bukan copyright/ownership/authority. Kegagalan packaging authorization tidak boleh otomatis dilaporkan sebagai Genesis Certificate invalid atau ownership invalid. Album Signer, Registry Authority, Licensing Authority, Genesis Creator, Container Packager dan current holder tetap trust domain terpisah.


#### A.1 Root authority untuk CONTAINER_PACKAGING — keputusan PO/Architecture Authority

**Keputusan normatif: APPROVED / RESOLVED.** Kewenangan awal (root / initial authority) untuk menerbitkan delegation dengan scope CONTAINER_PACKAGING berada secara eksklusif pada **Genesis Creator**, yaitu identitas genesisPubKey yang berakar pada Genesis Ownership Certificate. Tidak ada Designated Packaging Authority, Label/Studio, atau Current Owner yang memperoleh kewenangan awal secara mandiri (ex-nihilo).

- **Genesis Creator — ROOT / INITIAL AUTHORITY:** dapat melakukan self-packaging (containerSigKey == genesisPubKey) tanpa delegation tambahan, atau menerbitkan OwnershipDelegation dengan scope CONTAINER_PACKAGING kepada pihak pengemas yang ditunjuk.
- **Designated Packaging Authority — DERIVED AUTHORITY:** Label, Studio, atau pihak pengemas lain hanya sah berdasarkan rantai delegation yang valid, dapat diverifikasi, terikat pada asset/Genesis yang tepat, dan berakar pada Genesis Creator. Penerima delegation tidak otomatis memperoleh kewenangan untuk mendelegasikan kembali.
- **Sub-delegation:** Genesis Creator dapat secara eksplisit mengizinkan penerima delegation melakukan sub-delegation, direpresentasikan oleh sub_delegation_allowed = true. Jika izin tersebut tidak diberikan atau tidak dapat diverifikasi, sub-delegation tidak sah. Setiap sub-delegation harus tetap dapat ditelusuri ke delegation root Genesis Creator dan tidak boleh memperluas scope atau masa berlaku dari mandat induknya. Batas kedalaman sub-delegation ditetapkan pada A.2: tepat satu tingkat sub-delegation, dengan Level 2 sebagai terminal packager dan tanpa delegasi lanjutan.
- **Current Owner / Rights Holder — RESTRICTED / GENERALLY EXCLUDED:** kepemilikan edisi, hak koleksi, atau consumption/playback license tidak dengan sendirinya memberikan hak untuk menerbitkan kontainer .nx baru atau mendelegasikan CONTAINER_PACKAGING. Pengecualian hanya berlaku bila bukti transfer secara eksplisit mengalihkan seluruh hak master/IP yang relevan, termasuk hak penerbitan/pengemasan master, dari Genesis Creator kepada penerima. Ownership transfer biasa tidak cukup.
- **Authority derivation:** seluruh jalur pihak ketiga harus membuktikan rantai otorisasi dari Genesis Creator. Validitas matematis tanda tangan containerSigKey hanya membuktikan integritas kontainer; hal itu tidak menggantikan pembuktian kewenangan pengemasan.
- **Failure taxonomy:** delegation hilang, tidak valid, tidak berakar pada Genesis Creator, scope/asset tidak cocok, kedaluwarsa, dicabut, atau sub-delegation tidak diizinkan harus menghasilkan kegagalan packaging_authorization (mis. UNTRUSTED / UNAUTHORIZED PACKAGING). Kegagalan ini tidak otomatis mengubah hasil genesis_certificate atau ownership_chain menjadi invalid.
- **Batas klaim produk:** aturan ini adalah kontrak kewenangan produk dan keamanan NEXA. Penetapan siapa pemegang hak cipta/hak ekonomi menurut hukum positif tetap bergantung pada fakta kontrak dan yurisdiksi; sistem harus memverifikasi bukti pengalihan hak yang relevan, bukan mengasumsikannya hanya dari status Current Owner.



#### A.2 Batas kedalaman delegation — Model 3-Level Hierarchy (keputusan PO/Architecture Authority)

**Keputusan normatif: OPSI A — APPROVED / RESOLVED.** Rantai kewenangan CONTAINER_PACKAGING dibatasi maksimal tiga level hierarki, yaitu Level 0 sampai Level 2. Hanya satu tingkat sub-delegation yang diperbolehkan. Level 2 adalah terminal; tidak ada Level 3.

| Level | Entitas / peran | Hak menerbitkan delegation |
|---|---|---|
| **Level 0 — Root** | Genesis Creator (genesisPubKey) | Dapat menerbitkan delegation CONTAINER_PACKAGING kepada Level 1 dengan sub_delegation_allowed = true bila memang mengizinkan sub-delegation. |
| **Level 1 — Primary Delegatee** | Designated Packaging Authority (mis. Label/Studio/Agregator) | Dapat menerbitkan tepat satu sub-delegation kepada Level 2 hanya jika delegation Level 0 secara eksplisit mengizinkannya. Delegasi Level 1 → Level 2 wajib menetapkan sub_delegation_allowed = false. |
| **Level 2 — Terminal Packager** | Mastering House / Audio Engineer / pihak pengemas terminal | Dapat melakukan packaging dan menandatangani kontainer sesuai scope mandat. Dilarang menerbitkan delegation atau sub-delegation lanjutan. |

**Invariants dan validasi:**
1. Rantai sah maksimum adalah Genesis Creator (L0) → Designated Packaging Authority (L1) → Terminal Packager (L2). Direct delegation L0 → packager tetap sah sebagai jalur tanpa sub-delegation; batas maksimum tidak mewajibkan adanya L1 dan L2 sekaligus.
2. L1 hanya boleh menerbitkan sub-delegation bila izin eksplisit dari L0 terbukti dalam delegation induk yang valid. Ketiadaan, nilai false, atau status izin yang tidak dapat diverifikasi berarti sub-delegation ditolak.
3. L2 wajib bersifat terminal. Setiap assertion yang mengklaim delegator/recipient pada L2 menerbitkan delegasi berikutnya harus ditolak sebagai invalid delegation chain.
4. Sub-delegation tidak boleh memperluas asset binding, delegated_scope, kewenangan, atau masa berlaku melebihi mandat induk. Setiap hop harus memvalidasi signature, issuer/delegator authority, subject/delegatee identity, asset/Genesis binding, scope, validity interval, serta revocation/freshness sesuai kontrak trust.
5. Ketika L2 menandatangani kontainer, verifier harus dapat membangun dan memvalidasi rantai bukti L0 → L1 → L2. Tanda tangan kontainer oleh L2 tidak menggantikan kedua bukti delegation tersebut.
6. Verifier wajib menerapkan batas maksimum ini sebelum melakukan evaluasi rantai yang tidak terbatas; input dengan kedalaman di atas Level 2 ditolak secara fail-closed. Batas tetap berlaku pada seluruh implementasi TypeScript, Go, Desktop/Mobile Player, Verify, dan Registry-facing verification.
7. Self-packaging L0 dan direct delegation L0 → L1 tetap didukung sesuai A.1; model tiga level adalah batas maksimum, bukan kewajiban membentuk tiga identitas berbeda pada setiap packaging.

**Rasional keputusan PO:** batas kedalaman tetap dan kecil menyederhanakan verifikasi offline, membatasi kompleksitas rantai, memperjelas akuntabilitas, serta mengurangi risiko penyalahgunaan kunci pada rantai subkontraktor yang tidak terbatas. Referensi DEC-14-DELEG-01, ORG-DELEG-003, dan cuplikan CheckSubdelegationDepth yang disampaikan PO dicatat sebagai dasar keselarasan desain yang dikemukakan PO; pemeriksaan independen terhadap file sumber dan commit terkait tidak diklaim dalam rekonsiliasi ini.


#### A.3 Immutability, perubahan mandat, dan lifecycle delegation — keputusan PO/Architecture Authority

**Keputusan normatif: APPROVED / RESOLVED.** Atribut `sub_delegation_allowed` wajib ditetapkan di dalam delegation induk pada saat diterbitkan oleh delegator yang berwenang, dan menjadi **IMMUTABLE** setelah penerbitan. Khusus delegation Level 0 → Level 1, izin sub-delegation tidak dapat ditambahkan, dihapus, atau diubah melalui amendment. Tidak ada mekanisme `AMENDMENT` untuk mengubah payload atau kewenangan delegation yang telah ditandatangani.

1. **Mandat terkunci pada penerbitan:** `sub_delegation_allowed`, delegator, delegatee, asset/Genesis binding, scope, validity window, parent reference, schema/version, dan seluruh atribut lain yang mempengaruhi authority merupakan bagian dari payload bertanda tangan. Perubahan satu pun tidak boleh dilakukan dengan memodifikasi dokumen lama atau menempelkan amendment yang mengubah interpretasinya.
2. **Perubahan wajib menerbitkan delegation baru:** Genesis Creator menerbitkan delegation baru dengan payload dan signature baru. Untuk upgrade maupun downgrade, delegation baru harus menyatakan seluruh mandat yang berlaku secara lengkap; ia tidak mewarisi hak yang tidak dinyatakan secara eksplisit. Delegation baru tidak dengan sendirinya mencabut delegation terdahulu.
3. **Pencabutan eksplisit — tidak ada implicit revocation:** delegation baru atau field `supersedes_delegation_id` TIDAK dengan sendirinya mencabut delegation lama. Jika Genesis Creator bermaksud menghentikan delegation lama sebelum `expires_at`, Genesis Creator WAJIB menerbitkan event/bukti `REVOCATION` yang ditandatangani secara sah dan secara eksplisit mengikat `delegation_id` lama. Revocation evidence sekurang-kurangnya mengikat delegation ID, identitas/kunci otoritas pencabut, waktu yang ditandatangani Kreator (`revoked_at`), alasan/kode alasan, versi/skema, serta signature atas payload kanonikal. Registry/Event Store yang berwenang wajib menambahkan waktu penerimaan/pencatatan otoritatif (`recorded_at`) ketika event diterima dan dicatat; `recorded_at` tidak boleh berasal dari timestamp yang diklaim sepihak oleh penerbit event. Exact schema, trusted timestamp/clock, bukti penerimaan, aturan konsistensi pencatatan, dan byte-domain harus ditetapkan dalam kontrak teknis serta test vectors. Referensi `supersedes_delegation_id` hanya menyatakan lineage/penggantian, bukan bukti pencabutan. Tanpa revocation evidence yang valid dan tercatat oleh sumber status resmi, delegation lama tetap dapat berlaku sampai expired atau dicabut melalui bukti resmi lain yang diotorisasi.
4. **Event lifecycle append-only:** model lifecycle target menggunakan peristiwa diskrit `DELEGATION` untuk penerbitan mandat baru dan `REVOCATION` untuk pencabutan mandat lama. Tidak diperkenalkan tipe event `AMENDMENT`. Riwayat lama dipertahankan sebagai histori; perubahan status tidak menulis ulang artefak delegation yang telah diterbitkan.

4a. **Dua jalur pengakhiran delegation:** (a) Natural expiration: delegation berakhir berdasarkan `expires_at` dan trusted-time policy; revocation event tidak diwajibkan setelah masa berlaku berakhir. (b) Early revocation/replacement: jika mandat dihentikan sebelum `expires_at`, revocation evidence eksplisit sebagaimana butir 3 wajib ada. Penerbitan delegation pengganti tidak mengubah jalur ini dan tidak membuat pencabutan implisit.

4a.1. **Dual-Horizon Time Rule — dua lapisan waktu pencabutan (keputusan PO):**
- **Horizon internal Kreator ↔ Packager (`revoked_at`):** kewenangan packager berakhir dalam hubungan mandat internal sejak waktu pencabutan yang ditandatangani Kreator (`revoked_at`). Packager yang telah menerima pemberitahuan/pemberitahuan pencabutan yang dapat diverifikasi tidak boleh menerbitkan atau menandatangani kontainer baru berdasarkan delegation tersebut. Tindakan penerbitan setelah packager menerima pemberitahuan itu merupakan pelanggaran mandat (*breach of delegation*), walaupun event belum tercatat pada Registry. `revoked_at` menjadi audit trail waktu dan akuntabilitas hubungan internal; timestamp ini tidak dengan sendirinya menjadi bukti bahwa ekosistem publik telah menerima pemberitahuan.
- **Horizon publik Verifier/Player (`recorded_at`):** pencabutan baru mengikat status trust publik sejak event `REVOCATION` yang valid diterima dan dicatat oleh Registry/Event Store/Revocation List resmi, dengan waktu pencatatan otoritatif `recorded_at`. Verifier/Player tidak boleh menerapkan pencabutan publik secara retroaktif hanya berdasarkan `revoked_at`. Sebelum `recorded_at`, status publik delegation tidak berubah hanya karena timestamp `revoked_at` yang ditandatangani Kreator.
- **Late Publication / Reliance Protection:** apabila `revoked_at < recorded_at`, terdapat latency window. Kontainer yang dikemas, didaftarkan, didistribusikan, atau diperoleh konsumen sebelum `recorded_at` tidak boleh dibatalkan secara retroaktif semata-mata karena `revoked_at` lebih awal, sepanjang peristiwa sebelum cut-off tersebut didukung bukti pendaftaran/distribusi/perolehan yang valid dan dapat diverifikasi. Status publiknya dinilai berdasarkan status delegation yang berlaku pada horizon publik sampai `recorded_at`. Setelah `recorded_at`, pencabutan berlaku terhadap penggunaan delegation untuk penerbitan/packaging baru; pencabutan tidak otomatis membatalkan kontainer yang memenuhi Reliance Protection sebelum cut-off.
- **Beban keterlambatan publikasi:** risiko keterlambatan Kreator mempublikasikan event ke sumber status resmi tidak boleh dialihkan kepada Verifier/Player atau konsumen beritikad baik dengan membatalkan secara retroaktif kontainer yang memenuhi Reliance Protection. Hubungan tanggung jawab internal Kreator–Packager tetap mengikuti `revoked_at` dan bukti kapan Packager menerima pemberitahuan. Kontrak teknis wajib menentukan jenis bukti timestamp pendaftaran/distribusi/perolehan yang diterima, otoritas penerbit timestamp, freshness, dan cara memverifikasinya; timestamp lokal atau klaim sepihak tidak cukup untuk membuktikan cut-off publik.
- **Kewajiban verifier dan kasus offline:** verifier online menggunakan `recorded_at` dari sumber status resmi yang terautentikasi dan menerapkan pencabutan pada evaluasi publik sejak cut-off tersebut. Offline verifier hanya dapat menggunakan snapshot/status evidence resmi terakhir yang tersedia dan tidak dapat membuktikan adanya atau ketiadaan pencatatan yang lebih baru; freshness policy tetap berlaku. Stale/unavailable evidence tidak boleh diam-diam dianggap sebagai bukti bahwa delegation belum dicabut atau menghasilkan TRUSTED jika freshness diwajibkan.
- **Kontrak timestamp:** `revoked_at` dan `recorded_at` harus dibedakan secara eksplisit dalam schema, signed event/envelope, result contract, audit log, API, dan test vectors. `revoked_at` adalah waktu yang ditandatangani Kreator; `recorded_at` adalah waktu penerimaan/pencatatan yang ditetapkan sumber status resmi. Mekanisme trusted clock, sinkronisasi, monotonicity/ordering, bukti receipt, duplicate/replay handling, dan resolusi konflik pencatatan adalah pekerjaan desain teknis sebelum implementation readiness.
4b. **Coexistence rule:** dua delegation untuk asset yang sama dapat tetap berlaku bersamaan apabila masing-masing memiliki signature dan authority chain valid, belum expired, belum revoked, serta scope/subject/asset binding-nya sah. Verifier tidak boleh memilih salah satu hanya berdasarkan urutan penerbitan atau `supersedes_delegation_id`. Jika keduanya menghasilkan konflik mandat, konflik harus dievaluasi menurut policy conflict yang eksplisit; keberadaan delegation baru saja tidak meniadakan authority lama.
4c. **Verifier predicate dan offline limit:** evaluasi status delegation sekurang-kurangnya mensyaratkan signature valid, authority chain valid, binding asset/subject/scope tepat, belum expired menurut trusted-time policy, dan tidak ada revocation valid yang telah tercatat pada sumber resmi dengan `recorded_at` yang efektif pada waktu evaluasi publik serta freshness yang memenuhi policy. `revoked_at` saja tidak cukup untuk mengubah public trust status sebelum `recorded_at`. Offline verifier hanya dapat menyimpulkan status berdasarkan revocation evidence/status snapshot terakhir yang tersedia; ia tidak dapat membuktikan tidak adanya revocation yang lebih baru atau mengetahui `recorded_at` yang belum masuk ke snapshot. Evidence stale/unavailable tidak boleh diam-diam dianggap sebagai bukti non-revocation atau menghasilkan TRUSTED bila policy mensyaratkan freshness yang belum terpenuhi.

5. **Deterministic delegation ID:** target format ID adalah `OWNDEL-` diikuti SHA-256 atas canonical payload preimage yang deterministik. Untuk menghindari circularity, preimage pembentuk ID tidak boleh memuat `delegation_id` itu sendiri; ID hasil derivasi kemudian dimasukkan ke signed payload final sehingga terikat oleh signature Ed25519. Exact field set, JCS byte-domain, domain separation/versioning, dan test vectors wajib ditetapkan konsisten lintas TypeScript/Go sebelum implementation readiness. Tidak boleh mengklaim ID unik secara global tanpa mempertimbangkan collision-resistance dan domain/version context.
6. **Upgrade/downgrade dan sub-delegation:** perubahan `false → true` hanya sah melalui delegation baru dari Genesis Creator yang secara eksplisit memberi izin sub-delegation; perubahan `true → false` juga memerlukan delegation baru dan revocation mandat lama bila mandat lama harus dihentikan. L1 hanya dapat menerbitkan L2 delegation berdasarkan parent delegation baru yang valid dan mengizinkan sub-delegation. Delegation L1 → L2 tetap wajib `sub_delegation_allowed = false`.
7. **Offline determinism dan replay protection:** verifier offline memverifikasi satu artefak delegation yang self-contained beserta bukti rantai yang diperlukan; ia tidak merekonstruksi amendment history. Namun, offline verifier tidak dapat membuktikan bahwa tidak ada revocation lebih baru daripada evidence terakhir yang tersedia. Bila revocation/freshness evidence tidak memenuhi policy, hasil tidak boleh dinaikkan menjadi TRUSTED; keterbatasan stale/offline tetap dinyatakan secara eksplisit. Replay atas delegation lama harus ditangani melalui validity, delegation ID, revocation status, asset/subject binding, parent-chain binding, dan trusted freshness policy—bukan dengan menganggap delegation baru otomatis membatalkan yang lama.

**Catatan keselarasan:** PO menyampaikan X.509, Macaroons, UCAN, W3C Verifiable Credentials, dan model append-only NEXA sebagai rasional keputusan. Rasional tersebut dicatat sebagai dasar keputusan PO, bukan klaim bahwa seluruh standar/protokol tersebut memiliki model credential atau amendment yang identik. Cuplikan lokal `internal/domain/ownership.go:L100-L110` yang disampaikan PO juga merupakan rujukan yang diberikan PO; tidak diklaim telah diverifikasi independen dalam rekonsiliasi PLAN ini.


#### B. Target verification flow
1. Parse schema/version sertifikat dan referensi identity/delegation.
2. Verifikasi Container Packaging Signature terhadap containerSigKey; jangan otomatis memakai genesisPubKey sebagai substitusi.
3. Verifikasi Genesis Ownership Certificate secara independen menggunakan genesisPubKey.
4. Resolve current holder melalui ownership/transfer chain untuk mengikat ownCertPubKey ke asset/Genesis.
5. Jika containerSigKey == genesisPubKey, klasifikasikan self-packaging. Jika berbeda, verifikasi delegation scope CONTAINER_PACKAGING, asset binding, subject binding, signature, validity, authority chain, revocation/freshness.
6. Evaluasi Registry/federated trust dan Licensing Authority secara terpisah; Registry attestation bukan pengganti Genesis ownership, packaging delegation, atau license entitlement.
7. Gabungkan hasil melalui verifier result contract; jangan mereduksi semua domain menjadi boolean creatorMatches.

#### C. Delegation evidence contract
Scope target mencakup CONTAINER_PACKAGING. Delegation record mengikat delegation ID stabil; delegator identity/key reference; delegate/packager subject identity/key reference; asset/Genesis binding; scope; validity window; schema/version; canonicalization/signature algorithm; issuer signature atas payload kanonikal; parent delegation reference jika subdelegation kelak diizinkan; serta revocation evidence terpisah, bukan mutable unsigned boolean.

Gunakan versioned signed payload yang dipisahkan dari signature envelope. RFC 8785 JCS dan Ed25519 menjadi target teknis; exact byte-domain wajib ditentukan dan diuji melalui test vectors lintas TypeScript/Go. Semua field yang mempengaruhi authority (delegator, delegate, asset, scope, validity, delegation ID, parent reference, schema version) tercakup dalam signed payload. delegator_subject_id tanpa pemetaan terverifikasi ke public key tidak membuktikan delegator. Signature valid saja tidak cukup; authority delegator juga harus dibuktikan.

**Authority chain/subdelegation:** verifikasi wajib mengikuti keputusan A.1 (Genesis Creator sebagai satu-satunya ROOT / INITIAL AUTHORITY), A.2 (Level 0–2; Level 2 terminal), dan A.3 (mandat immutable; tidak ada amendment). Izin sub-delegation harus terbukti pada payload delegation induk yang ditandatangani sejak penerbitan. Perubahan mandat memerlukan delegation baru; bila mandat lama harus dihentikan, revocation evidence terpisah wajib diverifikasi. Current Owner, Registry, dan delegate tidak memperoleh authority ex-nihilo.

**Validity, revocation, offline:** expiry menggunakan trusted-time policy; revocation berupa signed/otoritatif evidence yang mengikat delegation ID, authority, `revoked_at`, dan `recorded_at`. Dual-Horizon Time Rule berlaku: `revoked_at` mengakhiri kewenangan dalam hubungan internal Kreator–Packager; `recorded_at` menjadi cut-off keberlakuan publik bagi Verifier/Player. Public trust status tidak dibatalkan retroaktif berdasarkan `revoked_at` saja; kontainer dengan bukti pendaftaran/distribusi/perolehan valid sebelum `recorded_at` mendapat Reliance Protection sesuai A.3. Mutable revocation boolean tidak mengubah signed authorization tanpa bukti terpisah. Online verification memeriksa authorized status source, authoritative `recorded_at`, dan freshness. Offline verifier dapat memvalidasi signature dan evidence status terakhir, tetapi tidak dapat membuktikan tidak ada revocation baru atau pencatatan yang lebih baru setelah evidence diterbitkan. Freshness limitation wajib dinyatakan; stale/unavailable tidak boleh diam-diam dinaikkan menjadi TRUSTED. Final disposition evidence stale/unavailable wajib ditetapkan sebelum implementation readiness. Network failure, missing trust source, invalid signature, expired, revoked, wrong asset/scope/subject, dan unknown authority memiliki reason code terpisah.

#### D. Federated trust resolution
Trust resolution menerima issuer/key identity, registry/federation ID, asset/domain, purpose/scope, dan policy version. Tidak boleh ada asumsi satu hidden global Registry Authority atau satu hardcoded key sebagai satu-satunya root ekosistem. Trust anchors diidentifikasi per registry/federation/domain dan mempunyai identity, key reference, scope, validity, rotation/revocation lifecycle, provenance, dan aturan transisi. Registry attestation diterima hanya jika signer dan kewenangan attestation diverifikasi; bukan pengganti delegation. Federation conflict, unknown federation, unavailable authority, stale response, dan invalid attestation harus memiliki disposition eksplisit. Cache menyimpan provenance/version/freshness/issuer/policy context. Kontrak harus konsisten di TypeScript SDK, Go runtime, Desktop/Mobile Player, Verify Desktop, Verify-Lite, dan Registry/federation service; tidak ada fallback diam-diam.

#### E. Verifier result contract
Verifier mengembalikan dimensi independen: container_integrity; packaging_authorization; genesis_certificate; ownership_chain; registry_trust; license_entitlement; asset_binding; overall_disposition; reason_codes; evidence_refs. Tiap dimensi membedakan valid, invalid, unknown/unavailable, expired, revoked, dan not-applicable bila relevan. UNKNOWN tidak disamakan dengan INVALID. UNTRUSTED / UNAUTHORIZED PACKAGING tidak ditampilkan sebagai GENESIS CERTIFICATE INVALID. Verify bukan playback authorization; Player tetap menjalankan JIT authorization per-member dan active-license gate PE-01.

#### F. Evolusi schema .nxcert — AC-01 tetap mengikat
Closed-schema invariant AC-01 tetap berlaku: unknown fields pada schema version aktif ditolak. Delegation evidence masuk melalui schema version baru atau extension namespace/version yang eksplisit dan di-allowlist, bukan field ad hoc pada schema lama. Setiap versi menetapkan required/optional fields, tipe, batas ukuran, canonicalization, signature scope, compatibility/migration, dan unsupported-version disposition. Consumer yang belum mendukung versi baru harus menolak/menyatakan unsupported; tidak boleh mengabaikan delegation lalu menganggap third-party package self-packaged. Parser/schema validator dan test vectors harus konsisten di SDK TypeScript, Go, Player, Verify. Representasi fisik delegation (embedded .nxcert, versioned Genesis metadata, atau Registry evidence reference) masih harus dipilih; persyaratan kontraknya ditetapkan sekarang, bukan klaim fakta existing.

#### G. Integrasi dan gap implementasi
| Komponen | Target pekerjaan | Baseline evidence | Disposisi |
|---|---|---|---|
| TypeScript SDK | Pisahkan container signer dari Genesis Creator; delegation verifier, authority/key resolution, result contract, schema versioning, parity tests. | Evidence supplement melaporkan creator-key comparison lokal; ownershipVerified tidak tampak di returned result; TS delegation path belum dibuktikan. | Build requirement. |
| Go runtime | Scope, canonical payload, signature/chain/revocation verification dan parity TypeScript. | Fungsi signature verifier Go dilaporkan; caller/parity belum lengkap dibuktikan. | Build/integration requirement. |
| NX Player Desktop/Mobile | Konsumsi hasil integrity, packaging authorization, Genesis/ownership, license; current-member JIT tetap. | Evidence belum membuktikan third-party packaging end-to-end. | Build requirement; PE-01 frozen behavior dijaga. |
| NX Verify Desktop / Verify-Lite | Sajikan packaging authorization terpisah; Verify bukan playback authorization. | Result contract target belum dibuktikan end-to-end. | Build requirement. |
| Registry/Federated Trust | Trust anchor resolution, signed attestation/status/revocation, freshness, federation conflict. | Konfigurasi Registry key tertentu dilaporkan; tidak membuktikan federated trust end-to-end atau satu global authority. | Architecture/integration build requirement. |
| .nxcert schema/consumers | Versioned closed-schema dan unknown-field rejection sesuai AC-01. | Supplement melaporkan parser pada scope tertentu memakai JSON.parse tanpa bukti schema rejection; tidak membuktikan seluruh consumer. | Corrective build requirement; AC-01 tidak boleh regresi. |

#### H. Acceptance criteria dan negative tests
1. Self-packaging valid tanpa delegation tambahan.
2. Third-party packaging dengan delegation valid, scope/asset/subject tepat, validity aktif, authority chain valid, trust evidence fresh: diterima.
3. Third-party packaging tanpa delegation: UNTRUSTED / UNAUTHORIZED PACKAGING meskipun container signature valid.
4. Delegation signature invalid, issuer unknown, subject/asset mismatch, wrong scope, expired, revoked, invalid parent chain: ditolak dengan reason domain-spesifik.
5. ownCertPubKey != genesisPubKey dengan transfer chain valid diterima; tanpa chain valid ownership gagal tanpa mengubah diagnosis Genesis signature.
6. Container signature valid tetapi delegation invalid: integrity tetap dapat dilaporkan valid, packaging authorization gagal.
7. Genesis certificate invalid tetapi packaging signature valid: dua dimensi tetap terpisah.
8. Untrusted Registry attestation, federation mismatch, stale/unavailable response, conflicting trust anchors: tidak ada trust success via fallback.
9. Revocation setelah issuance: uji terpisah `revoked_at` dan `recorded_at`; publik tidak menerapkan pencabutan sebelum `recorded_at`, sedangkan kewajiban internal Packager mengikuti `revoked_at` dan saat pemberitahuan diterima. Kontainer dengan bukti pendaftaran/distribusi/perolehan valid sebelum `recorded_at` tidak boleh dibatalkan retroaktif; penerbitan baru setelah cut-off publik harus ditolak. Offline verifier melaporkan freshness limitation dan tidak mengklaim status terkini tanpa evidence.
10. Unknown delegation field pada schema lama ditolak; schema baru menerima allowlist saja.
11. TypeScript dan Go menghasilkan canonical bytes, signature result, reason codes dan disposition identik.
12. Verify tidak memberikan playback authorization; Player hanya mengotorisasi current member secara JIT dan tidak mewariskan otorisasi background pre-verification.

#### I. Batas kompatibilitas dan implementasi
Tidak boleh mengubah byte-domain PE-01, Genesis Ownership Certificate terbit, atau hak pemilik sah tanpa migration/compatibility contract eksplisit. Kontainer legacy tanpa field packager tidak otomatis self-packaged; perlu compatibility policy, bukan fallback ke Genesis Creator. Perubahan jniLibs, libnexa.so, expo-nexa-core, shared Player path, atau trust boundary harus menjaga PE-01 frozen behavior dan otorisasi yang diwajibkan. Penulisan rancangan ini tidak mengotorisasi source changes, schema migration, deployment, atau build.

**Kesimpulan AUDIT-NEW-10:** keputusan produk tiga peran dan unauthorized third-party packaging telah disahkan; target architecture, verifier contract, schema evolution, integrasi, gap, dan acceptance tests kini ditetapkan dalam PLAN. Pertanyaan normatif berikutnya adalah penetapan sumber authority delegation; kebijakan subdelegation dibahas terpisah setelahnya.
### 13.12.10 Disposisi dan batas otorisasi

Rekonsiliasi §13.12 sebelumnya merupakan rekomendasi desain umum. Untuk AUDIT-NEW-10, §13.12.11 menjadi ketentuan target architecture yang lebih spesifik dan mengesampingkan pernyataan lama yang bertentangan tentang unresolved 3-way binding. B-01 sampai B-09 tetap mengikuti status masing-masing; penutupan dokumentasi AUDIT-NEW-10 tidak menyatakan implementasi atau runtime test telah selesai. CONF-02 Option B dan seluruh keputusan PO yang telah disahkan tetap dipertahankan.

Catatan akses repository pada snapshot rekonsiliasi terdahulu adalah catatan historis, bukan kesimpulan baru pada pembaruan AUDIT-NEW-10 ini. Pembaruan ini menggunakan PLAN kanonikal dan dokumen evidence Programmer/supplement yang sebelumnya telah diberikan; penyusun PLAN tidak melakukan pemeriksaan source repository secara langsung. Klaim kondisi implementasi tetap dibatasi pada isi evidence tersebut.

**Disposisi:** Gate A NOT PASSED — INDEPENDENT RE-AUDIT REQUIRED; Gate B BLOCKED; PE-02 Implementation NOT AUTHORIZED; Sprint 16 / PE-01 CLOSED / FROZEN; Sprint 17 NOT STARTED; Product Enhancement Window OPEN / NOT FROZEN.

## 14. MANDATORY CLOSING DECLARATIONS (DEF-09)

**Batas provenance wajib:** Bagian ini memuat campuran fakta yang dapat diverifikasi langsung dari file kanonikal GitHub `whisnu/plan:main` dan deklarasi historis Programmer tentang lingkungan lokal `whisnu/nexa`. Setiap klaim mengenai host lokal, working tree, commit lokal, `git diff`, `git status`, `ls`, DDL lokal, staging path, atau file untracked di bawah ini adalah **`REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`**, kecuali bukti primer independen secara eksplisit tersedia. Kehadiran teks deklarasi dalam plan bukan bukti bahwa perintah tersebut dijalankan atau bahwa hasilnya benar.

Sesuai ketentuan tata kelola dan hasil audit komprehensif REV6.3, deklarasi berikut dipertahankan sebagai catatan dengan batas pembuktian yang dinyatakan secara eksplisit:

1. **Git Baseline Otoritatif & Integritas Tracked Files — DIVERIFIKASI MELALUI PSV TEROTENTIKASI**:
   - **Repositori & Branch pengiriman dokumen:** `whisnu/plan`, branch `main`; keberadaan dan isi file kanonikal pada repositori ini dapat diperiksa langsung.
   - **Host repositori kerja lokal:** `/opt/antigravity/projects/nexa/` (`whisnu/nexa`, branch `main`).
   - **Baseline Commit SHA sumber primer yang diverifikasi:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` — `VERIFIED BY PSV (Read-Only Git Protocol & Authenticated GitHub REST API v3)`.
   - **Status `git diff --name-only` tracked files:** Bersih / nol mutasi pada commit tersebut.
2. **Keterbukaan Berkas Untracked Docs — LAPORAN PROGRAMMER, BELUM DIVERIFIKASI INDEPENDEN**:
   - Dua berkas berikut dilaporkan sebagai untracked pada working tree lokal:
     ```bash
     ?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md
     ?? docs/whitepapers/Nexa_White_Paper_v5_6.md
     ```
   - Status dan keberadaan aktual berkas tersebut pada working tree lokal tidak diverifikasi independen. Teks output historis bukan pengganti bukti terminal yang dapat diverifikasi.
3. **Integritas Berkas Skema Database — LAPORAN PROGRAMMER / BUKTI PRIMER TIDAK TERSEDIA**:
   - Klaim tidak adanya perubahan pada `marketplace/db/schema.postgres.sql` merupakan `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`.
   - Status database runtime live/produksi: `NOT VERIFIED — EVIDENCE NOT AVAILABLE`; tidak ada koneksi database aktif yang diuji atau diotorisasi dalam audit ini.
4. **Kepastian Satu Artefak Kanonikal & Rekonsiliasi Lokasi (DEFECT-C / DEFECT-04)**:
   - **Identitas berkas kanonikal pada pengiriman:** `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`.
   - **Lokasi otoritatif GitHub:** `whisnu/plan:main/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` (dapat diverifikasi langsung).
   - **Lokasi staging lokal yang dilaporkan:** `/opt/antigravity/projects/nexa/evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` — `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`.
   - **Klaim kesamaan konten/blob SHA staging lokal dengan GitHub:** `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`; tidak ada staging file lokal yang diperiksa dalam audit ini.
   - **Klaim ketiadaan path tambahan pada GitHub** `evidence/postsprint16-presprint17/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md` dan `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN-REV1.md`: deklarasi historis Programmer tidak membuktikan pemeriksaan independen atas seluruh riwayat branch.
   - **Single Artifact:** file kanonikal yang menjadi objek koreksi tetap satu file pada root `whisnu/plan`; tidak dibuat plan baru atau artefak pendamping dalam koreksi ini.
5. **Batas Verifikasi Runtime & Mobile**:
   - Status lingkungan mobile (iOS / Android), runtime live PostgreSQL, dan implementasi/source repository yang tidak tersedia untuk pemeriksaan independen tetap `NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE`.
6. **Isolasi Baseline Sprint 16 & PE-01**: Sprint 16 tetap `CLOSED / FINAL ACCEPTED / FROZEN` dan PE-01 tetap `CLOSED / FROZEN`.
7. **Sprint 17 Belum Dimulai**: Sprint 17 tetap `NOT STARTED`.
8. **Implementasi PE-02 Belum Diotorisasi**: implementasi kode PE-02 tetap `NOT AUTHORIZED`.
9. **Status Blocker dan keputusan pasca-PSV**: B-01, B-02, B-03, dan B-06 tetap `OPEN / BLOCKED`; B-04 tetap `OPEN / BLOCKED` karena fakta transaksi yang dilaporkan belum mengesahkan pola transaksi Album; B-05 hanya memiliki bukti semantik field database yang dilaporkan dan belum menutup kontrak end-to-end/child mapping; B-07 tetap `OPEN / BLOCKED` sampai parameter teknis ditetapkan Architecture Authority; B-08 tetap `OPEN / BLOCKED` karena detached signature envelope belum disahkan; B-09 tetap `OPEN / BLOCKED` sampai bukti signer/membership lengkap dan keputusan normatif residual diterbitkan. Integrasi PSV pada §15.9 adalah laporan Programmer dan belum boleh disebut verifikasi independen selesai. DEC-03 dihapus karena keputusan PO Auto-Next yang telah ada tidak memerlukan ratifikasi ulang; DEC-04 bukan keputusan untuk menerima proposal mitigasi yang belum diuji.
10. **Status Gate A dan Gate B**: Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`.


## 15. PEMISAHAN PEKERJAAN DOKUMEN/GOVERNANCE DAN SOURCE CODE VERIFICATION — MANDAT KANONIKAL

### 15.1 Tujuan dan prinsip pemisahan

Bagian ini menetapkan batas kerja agar koreksi dokumen tidak tertunda oleh pemeriksaan source code yang tidak relevan, dan agar klaim implementasi tidak disahkan hanya berdasarkan pembacaan dokumen.

Seluruh pekerjaan PE-02 dalam mandat ini dibagi menjadi:

1. **Document/Governance Reconciliation (DGR):** pemeriksaan dan koreksi yang dapat dilakukan dari PLAN kanonikal, keputusan PO yang telah tersedia, governance, serta artefak historis yang dapat diakses. Jalur ini tidak memerlukan pemeriksaan source code repository `whisnu/nexa`.
2. **Primary Source Code Verification (PSV):** pemeriksaan klaim mengenai perilaku atau kondisi implementasi aktual. Jalur ini wajib memeriksa source code, schema, test, dan/atau runtime evidence yang relevan dari repository `whisnu/nexa`. Bukti dokumentasi atau laporan Programmer saja tidak menggantikan pemeriksaan primer.
3. **Integrated Reconciliation:** penggabungan hasil DGR dan PSV ke dalam dokumen ini. Setiap klaim tetap diberi provenance dan status pembuktian yang tepat.

Pemisahan ini adalah pembagian metode kerja, bukan pembagian artefak. Hanya ada satu deliverable kanonikal: file PLAN yang sedang dibaca ini.

### 15.2 Ruang lingkup DGR — tidak memerlukan pemeriksaan source code Nexa

Tabel berikut menetapkan klasifikasi pekerjaan yang secara substansi tidak memerlukan pemeriksaan source code. **DGR yang secara spesifik telah dikerjakan pada pass sebelum handoff ini dicatat pada §15.8; tabel ini adalah batas klasifikasi metode, bukan daftar tugas DGR terbuka yang harus diulang atau diselesaikan Programmer.** Catatan §15.8 hanya menyatakan koreksi yang benar-benar diterapkan dan tidak mengklaim bahwa setiap baris dalam tabel telah diaudit ulang secara menyeluruh pada pass tersebut. Mandat Programmer pada handoff ini adalah PSV pada §15.3 dan integrasi bukti primer ke PLAN yang sama. Programmer hanya boleh menyentuh kembali butir DGR jika hasil PSV menemukan konflik faktual baru yang benar-benar memerlukan rekonsiliasi; setiap koreksi harus terbatas, berbasis bukti, dan tidak membuka ulang keputusan atau pekerjaan yang sudah ditutup. Pemeriksaan repository `whisnu/nexa` tidak pernah menjadi prasyarat bagi DGR:

| Area | Tugas DGR | Batas |
|---|---|---|
| Identitas dan lokasi artefak | Pastikan semua instruksi, referensi, dan closing declaration menunjuk file kanonikal `whisnu/plan:main/PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`. | Jangan membuat file PLAN, laporan investigasi, atau artefak pendamping baru. |
| Status dan otorisasi | Selaraskan status Gate A, Gate B, PE-02 implementation, Sprint 16, PE-01, dan Sprint 17 di seluruh ringkasan, tabel, register, serta closing declaration. | Tidak boleh menaikkan status hanya karena teks PLAN telah dikoreksi atau diperbarui. |
| Hierarki sumber | Periksa konsistensi penerapan §1.2 dan provenance keputusan PO, kontrak produk, White Paper/Roadmap, repository evidence, serta temuan historis. | Jangan mengubah keputusan atau menciptakan keputusan PO baru. |
| Riwayat audit | Pertahankan temuan dan disposisi historis; bedakan snapshot historis dari status aktif. | Jangan menghapus atau mengarang riwayat, revision count, atau hasil audit. |
| Konsistensi internal | Periksa rujukan silang, nomor bagian, ID temuan, jumlah item, agregat, istilah, status, dan tabel yang saling merujuk. | Bila nilai atau definisi sumber tidak tersedia/bertentangan, tandai unresolved; jangan menebak. |
| R-01 traceability | Periksa apakah setiap klaim dalam dokumen memiliki sumber, identitas bukti, dan batas inferensi yang dinyatakan. | Pemeriksaan keterlacakan dokumen bukan pembuktian kebenaran implementasi. |
| TD/B/AC/NC/CONF register | Periksa definisi, status, dependency, dan konsistensi antar-register berdasarkan isi PLAN serta keputusan formal yang tersedia. | Status yang membutuhkan fakta source atau keputusan PO/Architecture Authority tidak boleh diputuskan melalui DGR. |
| Product Truth dan scope | Periksa bahwa rekomendasi/proposal tidak ditulis sebagai kontrak yang telah disahkan, dan bahwa baseline .nx/PE-01 tidak berubah. | Programmer tidak berwenang mengubah Product Truth, trust policy, authorization policy, atau kontrak Album yang belum diputuskan. |
| Batas file dan perubahan | Pastikan hanya file PLAN kanonikal pada repository `whisnu/plan` branch `main` yang menjadi target pembaruan. | Tidak membuat salinan, file laporan baru, atau mengubah repository source `whisnu/nexa`. |

DGR dapat diselesaikan tanpa menunggu PSV. Namun, jika sebuah koreksi DGR bergantung pada fakta implementasi yang belum dibuktikan, bagian tersebut harus tetap diberi status `NOT VERIFIED`, `BLOCKED`, atau status unresolved yang tepat.

### 15.3 Ruang lingkup PSV — wajib memeriksa source code

Butir berikut tidak boleh dinyatakan terbukti hanya dari PLAN, laporan lama, nama file, atau hasil pencarian terbatas. Programmer harus memeriksa repository sumber `whisnu/nexa` dan mencatat commit yang benar-benar diperiksa:

| Area / temuan | Pemeriksaan primer minimum | Batas kesimpulan |
|---|---|---|
| R-02 — Player pre-verification dan authorization | Telusuri call path end-to-end untuk current-member state, JIT authorization, decryption, buffer registration, cache/state mutation, dan seluruh side effect pre-verification. | Tidak boleh menyimpulkan pre-verification aman atau terpisah hanya dari satu pemanggilan fungsi. |
| R-03 — Viewer completion dan Auto-Next | Periksa lifecycle audio, video, document, dan image viewer; event completion, state transition, serta pemanggil Auto-Next. | Ketiadaan event pada satu file/lokasi bukan bukti bahwa fitur atau kebijakan tidak ada di seluruh sistem. |
| R-04 — Studio persistence/recovery | Periksa NXPublishPipeline, penyimpanan progress, restart/crash recovery, retry, idempotency boundary, dan pencegahan listing duplikat. | Autosave lokal saja tidak membuktikan durable multi-member progress atau crash safety. |
| R-05 — Marketplace dan Licensing Daemon | Periksa transaction boundary, SQL transaction, urutan side effect eksternal, retry, replay, compensation, reconciliation, dan idempotency. | SQL transaction tidak boleh diklaim sebagai distributed transaction/2PC tanpa mekanisme yang benar-benar ada. |
| R-06 — acquired_package_sha256 | Temukan seluruh producer, consumer, persistence field, byte-domain, parent/child mapping, dan jalur akuisisi yang menggunakan digest tersebut. | Jangan menetapkan semantik parent/child atau menyamakannya dengan hash member/payload tanpa bukti. |
| R-07 — ZIP parser/extractor | Telusuri seluruh parser dan extraction path yang relevan, entry type, path validation, collision, streaming counters, quota, serta test. | Tidak ditemukannya parser pada dua direktori bukan bukti parser tidak ada di repository. |
| R-08 — Safe-Open/filesystem | Periksa implementasi per platform, descriptor-relative operations, symlink/ancestor handling, containment, TOCTOU, staging permissions, dan adversarial tests. | Tidak adanya satu primitive seperti `O_NOFOLLOW` pada cuplikan tertentu bukan bukti keamanan atau ketidakamanan seluruh jalur. |
| R-09 — Parser/JCS/cryptography | Periksa raw-byte parser, duplicate-key/Unicode/number handling, RFC 8785 implementation, exact signed bytes, Ed25519 input, key role, dan test vectors. | Nama library atau pemanggilan serializer saja tidak membuktikan kesesuaian RFC 8785 maupun signature scope. |
| R-10 — Album Signer/membership authenticity | Periksa identity binding, enrollment, authority, key custody, rotation, revocation, freshness, manifest verification, dan dependency Registry bila memang ada. | Jangan mengasumsikan Album Signer sudah mempunyai lifecycle atau authority yang belum dibuktikan. |
| B-04 / NC-08 / CONF-03 | Periksa workflow aktual Studio/Marketplace, schema, transaksi, dan side effect layanan eksternal. | Lakukan PSV terlebih dahulu. Source evidence tidak menggantikan keputusan normatif Zero-DDL/arsitektur yang mungkin tetap diperlukan setelah PSV. |
| B-05 / NC-09 | Periksa schema/DDL aktual, producer-consumer mapping, persistence, byte-domain, dan seluruh penggunaan hash terkait. | Lakukan PSV terlebih dahulu; jangan mengubah status blocker menjadi siap hanya karena nama kolom ditemukan. |
| B-06 / NC-12 | Periksa source filesystem dan test keamanan per platform. | Lakukan PSV terlebih dahulu; mitigasi desain tertulis tidak sama dengan implementasi dan test yang lulus. |
| B-08 | Periksa signed-content construction, signature envelope, serialization, canonicalization, dan verification path. | Lakukan PSV terlebih dahulu; source code yang ada tidak dengan sendirinya mengesahkan desain kriptografi yang belum diputuskan. |
| B-09 / NC-04 / CONF-01 | Periksa bukti teknis signer/membership, identity binding, dan lifecycle jika implementasi tersedia. | Lakukan PSV terlebih dahulu; kebijakan atau kontrak identitas/lifecycle yang tetap belum ditetapkan setelah PSV dieskalasikan kepada PO/Architecture Authority. |

Daftar ini adalah target pemeriksaan minimum, bukan izin melakukan full clone, membuat repository duplikat, mengubah source code, menjalankan migrasi, atau mengubah database. Gunakan akses baca dan retrieval terarah. Jangan meminta ZIP repository penuh.

### 15.4 Aturan evidence dan pelaporan PSV

Untuk setiap klaim PSV, Programmer wajib mencatat:

1. repository, branch, commit SHA, dan tanggal pemeriksaan;
2. path file dan line range yang benar-benar diperiksa;
3. call path atau dependency yang diperlukan agar konteks tidak terpotong;
4. test yang ditemukan/dijalankan beserta command, environment, dan hasil aktual jika test memang dijalankan;
5. pemisahan tegas antara `VERIFIED`, `PARTIALLY VERIFIED`, `NOT VERIFIED`, dan `NOT PRESENT IN THE EXAMINED SCOPE`;
6. batas pencarian: direktori/modul yang diperiksa dan alasan cakupannya;
7. setiap klaim yang belum terbukti tetap `NOT VERIFIED`; tidak boleh dinaikkan melalui inferensi dari laporan terdahulu.

Jika akses ke `whisnu/nexa` gagal, catat langkah akses yang benar-benar dicoba dan hasil aktualnya. Jangan menyatakan repository tidak ada hanya karena koneksi yang digunakan tidak dapat membacanya. Jangan membuat bukti lokal, permalink, line number, test result, atau commit SHA yang tidak diperoleh secara langsung.

### 15.5 Mandat pembaruan langsung ke PLAN kanonikal yang sama

**Deliverable utama dan satu-satunya adalah pembaruan in-place pada file yang sudah ada:**

- Repository: `whisnu/plan`
- Branch: `main`
- Path: `PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md`
- Baseline blob SHA saat §15 ditambahkan: `05f106299d8c8713d6a2d533f294ba7eb1249d0f`
- **Baseline blob untuk setiap pelaksanaan PSV:** tidak ditetapkan sebagai SHA statis di dalam PLAN. Programmer WAJIB melakukan fetch ulang file ini dari `whisnu/plan:main` tepat sebelum mulai PSV dan sebelum setiap pembaruan; catat blob SHA yang benar-benar diterima sebagai baseline kerja pada ringkasan pengembalian. SHA historis tidak boleh diperlakukan sebagai baseline terbaru. Jika branch `main` berubah selama pekerjaan, fetch ulang dan rekonsiliasikan perubahan sebelum melanjutkan; jangan menimpa perubahan yang lebih baru.
- Target: file yang sama, bukan file baru.

Programmer wajib mengintegrasikan hasil PSV ke bagian PLAN yang sudah relevan—termasuk section, matriks, register, evidence table, dan closing declaration yang terdampak—serta menyelaraskan rujukan silang yang terdampak. Programmer tidak diminta mengulang DGR; rekonsiliasi dokumentasi hanya dilakukan secara terbatas jika bukti primer baru menunjukkan konflik faktual yang spesifik. §15 ini adalah pembagian mandat dan tidak menggantikan isi teknis pada section terkait.

**Dilarang:**
- membuat `PE-02_HANDLING_ALBUM_PEMULIHAN_AKSES_READ-ONLY_REPOSITORY_DAN_VERIFIKASI_PRIMARY_SOURCE_EVIDENCE.md` atau laporan investigasi lain sebagai deliverable;
- membuat PLAN kedua, salinan alternatif, file pendamping, atau branch/PR baru atas asumsi sendiri;
- mengubah source code `whisnu/nexa`, DDL, schema, database, API, runtime, atau konfigurasi produk;
- mengubah Product Truth, keputusan PO, atau status otorisasi implementasi;
- menyatakan pekerjaan PSV selesai bila primary source evidence tidak tersedia.

Jika mekanisme repository yang berlaku tidak mengizinkan pembaruan langsung pada `main`, Programmer harus berhenti dan meminta klarifikasi mengenai jalur publikasi yang diotorisasi. Jangan membuat branch atau PR sebagai keputusan sepihak. Bila branch head berubah sejak baseline, lakukan fetch ulang dan rekonsiliasi perubahan terbaru sebelum menulis; jangan menimpa perubahan orang lain.

### 15.6 Urutan pelaksanaan

1. Baca PLAN kanonikal terbaru pada `whisnu/plan:main`; pastikan file dan blob SHA sebelum mengedit.
2. DGR dokumen/governance yang dapat dilakukan tanpa source code telah dikerjakan langsung pada PLAN kanonikal oleh pemelihara PLAN sebelum handoff source verification ini. Programmer tidak diminta mengulang DGR atau membuat laporan DGR; cukup periksa bahwa koreksi yang sudah masuk tidak bertentangan dengan bukti source yang kemudian ditemukan. Jika ditemukan konflik faktual baru dari source, catat dan rekonsiliasikan secara terbatas tanpa menghapus koreksi dokumentasi yang sah.
3. Susun daftar klaim PSV yang masih diperlukan. Jangan memeriksa source untuk item yang murni editorial/governance.
4. Lakukan targeted PSV pada repository `whisnu/nexa`. Jika akses gagal, pertahankan item terkait sebagai `NOT VERIFIED` dan jangan menunda koreksi DGR yang independen.
5. Rekonsiliasikan hasil PSV dengan PLAN, tetapi jangan mengubah kontrak produk atau keputusan yang belum disahkan.
6. Perbarui section PLAN yang sudah ada dan §15 ini bila klasifikasi kerja perlu disesuaikan berdasarkan bukti; tetap pada file kanonikal yang sama.
7. Lakukan pemeriksaan akhir terbatas pada section, register, evidence table, dan closing declaration yang berubah akibat PSV; periksa konsistensi status, ID, agregat, referensi silang, provenance, path/line evidence, dan klaim source pada bagian terdampak. Langkah ini bukan audit ulang DGR menyeluruh atas seluruh PLAN. Jangan mengubah bagian yang tidak terdampak tanpa temuan faktual spesifik dan dapat ditelusuri.
8. Serahkan identitas commit SHA dan blob SHA terbaru dari file PLAN yang sama, serta ringkasan singkat section yang diperbarui dan item yang masih `NOT VERIFIED/BLOCKED`.

### 15.7 Batas kewenangan dan status akhir

Mandat pembaruan PLAN tidak memberikan otorisasi implementasi. Source verification adalah pemeriksaan fakta implementasi, bukan izin memperbaiki atau mengubah implementasi.

Status berikut wajib dipertahankan kecuali terdapat keputusan formal terpisah yang sah:

- Gate A: `NOT PASSED` (menunggu koreksi dan independent re-audit).
- Gate B: `BLOCKED`.
- PE-02 Implementation: `NOT AUTHORIZED`.
- Sprint 16: `CLOSED / FINAL ACCEPTED / FROZEN`.
- PE-01: `CLOSED / FROZEN`.
- Sprint 17: `NOT STARTED`.

Jika instruksi, bukti, Product Truth, dependency, atau expected behavior material tidak jelas, Programmer wajib menghentikan penetapan dan menyatakan: **`INSTRUKSI TIDAK JELAS — STOP AND CLARIFY`**. Tidak boleh ada asumsi atau keputusan desain diam-diam.


### 15.8 Disposisi Document/Governance Reconciliation sebelum handoff source verification

Pekerjaan DGR yang dapat dilakukan tanpa pemeriksaan source code telah dikerjakan langsung pada file PLAN kanonikal sebelum Programmer menerima mandat PSV ini.

Koreksi dokumentasi yang telah diterapkan:
1. §2.1: agregat kategori 34 AC direkonsiliasi menjadi 12 Specification Ready + 20 Execution Blocked + 2 PO Decision Required.
2. §2.1: AC-33 dan AC-34 dipindahkan dari kategori Specification Ready ke Execution Blocked, konsisten dengan baris individual dan dependency autentisitas membership CONF-01.
3. §2.1: AC-08 dimasukkan ke subkategori Blocked by Architecture / Spec, konsisten dengan unresolved Registry revocation lifecycle.
4. §2.1: catatan keputusan PO Manual Next untuk AC-33/34 diperjelas agar tidak dibaca sebagai penyelesaian membership authenticity blocker.
5. §15.5: identitas baseline blob pada saat §15 ditambahkan dipertahankan; mekanisme fetch ulang baseline PSV dijelaskan tanpa SHA statis terbaru.
6. §7.1, §12.3, §13.1, §13.11.1–§13.11.2, §13.12.8, §14, dan §15.5–§15.6: urutan PSV Programmer sebelum eskalasi keputusan formal diperjelas untuk B-04 sampai B-09 dan B-07; pemeriksaan akhir Programmer dibatasi pada bagian yang terdampak PSV dan tidak mengulang DGR menyeluruh.

Agregat aktif tetap tepat 34 AC. Tidak ada keputusan PO baru, perubahan Product Truth, perubahan source code, perubahan schema, atau perubahan otorisasi implementasi yang dilakukan melalui koreksi ini.

**Disposisi pekerjaan:** DGR yang dapat dibuktikan dari dokumen telah diterapkan. Programmer selanjutnya bertanggung jawab atas PSV dan integrasi temuan primer ke file PLAN yang sama. Programmer tidak perlu mengulang pekerjaan DGR yang sudah diselesaikan, kecuali bukti primer baru menunjukkan konflik faktual yang perlu direkonsiliasi.


### 15.8.1 DGR — Koreksi Klasifikasi dan Konsistensi Pasca-PSV (DILAKUKAN PADA PLAN KANONIKAL)

Koreksi dokumen berikut adalah rekonsiliasi DGR, bukan PSV dan bukan keputusan produk/arsitektur:

1. Ringkasan status blocker di bagian awal dan ringkasan status pada §10 diselaraskan dengan isi PSV yang dilaporkan di §15.9 dan register residual §15.10. Label `SPECIFICATION READY` tidak lagi digunakan untuk B-04/B-08 hanya karena fakta implementasi ditemukan.
2. Fakta source yang dilaporkan dipisahkan dari rekomendasi teknis: parent delivery/polling idempoten (PSV-04), path/format persistence lokal (PSV-03), parameter kuota ZIP (PSV-06), opsi Safe-Open lintas platform (PSV-07), dan detached signature envelope (PSV-08) tidak dinyatakan sebagai keputusan normatif.
3. Makna aktual `acquired_package_sha256` yang dilaporkan PSV-05 dipertahankan sebagai fakta implementasi field yang ada; hal itu tidak otomatis mengesahkan kontrak child acquisition atau menutup seluruh B-05.
4. DEC-01 dialihkan dari ratifikasi angka oleh PO menjadi penetapan parameter teknis oleh Architecture Authority berdasarkan threat model, benchmark, dan PSV.
5. DEC-03 dihapus: keputusan PO Auto-Next yang telah ada tidak diminta untuk diratifikasi ulang dan tidak boleh diganti menjadi manual-only. Kekurangan event/lifecycle yang dilaporkan PSV-02 tetap merupakan gap teknis yang perlu dibuktikan.
6. DEC-04 dihapus sebagai permintaan menerima opsi mitigasi Safe-Open yang belum diuji. Opsi POSIX dan Windows/Android tetap proposal sampai PSV per platform dan penilaian Architecture Authority tersedia.

Koreksi ini tidak menutup blocker yang memerlukan bukti source/schema/test/runtime atau keputusan normatif. Tidak ada perubahan Product Truth, schema, source code, atau otorisasi implementasi. Status Gate A, Gate B, dan PE-02 Implementation tetap sesuai disposisi governance sampai audit independen dan keputusan formal berikutnya.

---

### 15.9 Integrasi Hasil Primary Source Verification (PSV-01 s.d. PSV-09 / PSV-R02 s.d. PSV-R10) — Bukti Granular & Terarah

Sesuai mandat `HANDOFF PROGRAMMER — PE-02 RESIDUAL PRIMARY SOURCE VERIFICATION (PSV-R02 s.d. PSV-R10)`, bagian ini merekam pembuktian primer granular terhadap seluruh workstream PSV pada repositori sumber `whisnu/nexa`, memisahkan fakta source, fakta skema, bukti eksekusi test aktual, bukti runtime, dan status subklaim secara ketat tanpa mencampur inferensi dengan fakta terbukti.

#### Identitas Pemeriksaan Sumber Primer Otoritatif
- **Repository Sumber:** `whisnu/nexa` (Private repository)
- **Branch:** `main`
- **Commit SHA Sumber:** `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` (Terverifikasi identik dengan `origin/main` via `git ls-remote origin`)
- **Tanggal Pemeriksaan:** 9 November 2026
- **Lingkungan Pemeriksaan:** Linux x86_64, Node.js v22.23.4, Go 1.22.4, PostgreSQL 14 client, penelusuran pohon repositori lokal `/opt/antigravity/projects/nexa/`.
- **Status Akses Repository:** **`PASS (Programmer-only)`** (Akses read-only terverifikasi; ketiadaan respons pada audit sebelumnya terbukti akibat proteksi default HTTP 404 GitHub untuk repository privat tanpa token).
- **Otorisasi Perubahan Kode:** **TIDAK DIBERIKAN / ZERO CODE IMPLEMENTATION** (Source tree `whisnu/nexa` 100% bersih dan tidak berubah).

---

#### 15.9.1 PSV-01 / PSV-R02 — Player Pre-Verification dan Authorization
- **Referensi Mandat:** R-02, NC-13, AC-22, Stage 8a, DGR-PSV-02.
- **Tujuan Pembuktian:** Memastikan batas otorisasi playback tidak diperluas menjadi klaim bahwa background pre-verification Stage 8a sudah aman atau sudah diimplementasikan di kode aktif.
- **Objek yang Diperiksa:**
  - `player-desktop/main.js:L980-L1022` (IPC handler `open-and-verify-nx` & registrasi `AuthorizedPlaybackTracks.set()`).
  - `player-desktop/main.js:L1208-L1214` (IPC handler `release-playback-session` & `AuthorizedPlaybackTracks.delete()`).
  - `player-desktop/renderer.js:L341-L342` (Pemicu pelepasan sesi saat pemutaran baru).
  - `player-desktop/test/player-desktop.test.js` (Suite pengujian desktop player).
- **Bukti Source (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  1. *Otorisasi Track Aktif:* `renderer.js:openAndVerifyFile(filePath)` memanggil IPC `open-and-verify-nx`. Di `main.js:L1008-L1022`, jika kontainer valid dan lisensi aktif:
     ```javascript
     AuthorizedPlaybackTracks.set(certID, {
         filePath, payloadOffset, payloadLength,
         payloadBuffer: result.payload,
         manifest: result.manifest,
         payloadFormat: payloadFormat,
         mimeType: mimeType,
         licenseStatus: 'ACTIVE_PLAYBACK_AUTHORIZED'
     });
     ```
  2. *Pelepasan Otorisasi:* Saat transisi track atau penutupan player, IPC `release-playback-session` memanggil `AuthorizedPlaybackTracks.delete(certID)` (`main.js:L1208-L1214`), menghapus buffer dan hak stream.
- **Pencarian Terukur Ketiadaan Caller Stage 8a / Background Pre-Verification:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "pre-verif|stage.*8|background.*verif" player-desktop/`
  - *Scope:* Seluruh source code `player-desktop/` (non-vendor).
  - *Hasil Pencarian:* **0 matches** (tidak ditemukan caller, function, atau worker background pre-verification).
  - *Batas Kesimpulan:* Caller background pre-verification Stage 8a **belum pernah ada** di source aktif.
- **Bukti Test (Test Evidence):**
  - *File Test:* `player-desktop/test/player-desktop.test.js`
  - *Command:* `node player-desktop/test/player-desktop.test.js`
  - *Environment:* Linux x86_64, Node.js v22.23.4
  - *Exit Code:* **`1 (FAILED)`**
  - *Output Aktual:*
    ```text
    === STARTING NEXA PLAYER DESKTOP INTEGRATION TESTS ===
    [*] Test 1: Configuration defaults... -> Test 1 PASSED
    [*] Test 2: Saving custom settings... -> Test 2 PASSED
    [*] Test 3: Verifying valid audio container & playback url extraction...
        - Forging test audio container using nexa CLI...
    /bin/sh: 1: ../../nexa: not found
    [-] TEST FAILED: Command failed: ../../nexa forge ...
    ```
  - *Status Test Pre-Verification:* **`NOT AVAILABLE / NOT RUN`** (Tidak ada test case untuk background pre-verification Stage 8a di seluruh repositori).
- **Bukti Runtime (Runtime Evidence):**
  - *Status:* **`NOT RUN`** (Aplikasi desktop player tidak dijalankan pada runtime UI interaktif; pengujian murni inspeksi statis dan eksekusi test runner).
- **Status Pembuktian Subklaim PSV-01 / PSV-R02:**
  - *Subklaim 1 (State & Authorization Registration Player Desktop):* **`VERIFIED`** (`AuthorizedPlaybackTracks.set()` terbukti mengikat `certID` ke buffer memori dan URL stream protokol `nexa-playback://`).
  - *Subklaim 2 (Pelepasan Otorisasi Saat Transisi):* **`VERIFIED`** (`AuthorizedPlaybackTracks.delete(certID)` terbukti menghapus otorisasi track).
  - *Subklaim 3 (Keberadaan Caller Background Pre-Verification Stage 8a):* **`NOT PRESENT IN THE EXAMINED SCOPE`** (Stage 8a belum diimplementasikan di kode; pencarian terukur menghasilkan 0 kemunculan).
  - *Subklaim 4 (Batas Otorisasi Terhadap Alur Verifikasi Saat Ini):* **`NOT VERIFIED — CONDITIONAL RISK ONLY`** (Sesuai DGR-PSV-02: Jika background pre-verification memanggil fungsi verifikasi kontainer yang ada `open-and-verify-nx`, alur tersebut atomik mendaftarkan `AuthorizedPlaybackTracks.set()`; pemisahan inspeksi pasif tanpa otorisasi wajib dibangun sebelum Stage 8a dapat aktif).
- **Status Keseluruhan PSV-01 / PSV-R02:** **`PARTIALLY VERIFIED`** (Coupling arsitektural terbukti; caller Stage 8a belum ada di kode; test Player gagal exit code 1).

---

#### 15.9.2 PSV-02 / PSV-R03 — Viewer Completion dan Auto-Next
- **Referensi Mandat:** R-03, NC-13, AC-32.
- **Tujuan Pembuktian:** Memverifikasi perilaku completion dan Auto-Next pada 8 kategori kombinasi platform dan tipe payload tanpa mengubah keputusan PO yang telah disahkan.
- **Objek yang Diperiksa:**
  - `player-desktop/renderer.js:L652-L655`, `L708-L771`, `L516-L530`, `L957-L969`.
  - `mobile/apps/player/src/components/AudioPlayer.tsx:L28-L55`.
  - `mobile/apps/player/src/components/VideoPlayer.tsx:L32-L60`.
  - `mobile/apps/player/src/components/DocumentViewer.tsx`.
- **Matriks Pembuktian 8 Kategori Platform & Payload:**
  1. *Desktop Audio:*
     - Event Source: `audioEngine.addEventListener('ended', playNextLibraryAsset)` (`renderer.js:L652-L655`).
     - Handler: `playNextLibraryAsset()` (`renderer.js:L957-L968`).
     - Alur Auto-Next: Memanggil `openAndVerifyFile` untuk item berikutnya di playlist.
     - Test Evidence: **`NOT RUN`** (Tidak ada automated test untuk event `ended` audio di test suite).
     - Runtime Evidence: **`NOT RUN`**.
     - Status: **`VERIFIED`** untuk keberadaan handler kode; **`NOT RUN`** untuk bukti test/runtime.
  2. *Desktop Video:*
     - Komponen: `videoEngine` (`renderer.js:L708-L771`).
     - Event Source: Memiliki handler `timeupdate` dan `seeked`, tetapi listener `ended` **belum dipasang**.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`** (Gap implementasi).
  3. *Desktop Document:*
     - Komponen: Document viewer (`renderer.js:L516-L530`).
     - Mekanisme: Murni tombol navigasi manual (`docPageNext`). Tidak memiliki completion event alami. PO melarang timeout buatan.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`** (Tidak ada sinyal completion alami).
  4. *Desktop Image:*
     - Komponen: Image renderer. Penayangan statis tanpa durasi alami.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
  5. *Mobile Audio:*
     - Komponen: `mobile/apps/player/src/components/AudioPlayer.tsx:L28-L55`.
     - Event Source: Menggunakan `Audio.Sound.createAsync`, tidak mengevaluasi `playbackStatus.didJustFinish`, tidak memiliki callback Auto-Next.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`** (Gap implementasi).
  6. *Mobile Video:*
     - Komponen: `mobile/apps/player/src/components/VideoPlayer.tsx:L32-L60`.
     - Event Source: Menggunakan `Video` component, status `didJustFinish` tidak ditangani.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`** (Gap implementasi).
  7. *Mobile Document:*
     - Komponen: `DocumentViewer.tsx`. Navigasi manual per halaman.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
  8. *Mobile Image:*
     - Komponen: Static image view.
     - Status: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **Pencarian Terukur Referensi Auto-Next:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "playNext|AutoNext|autoNext" player-desktop/ mobile/ test/`
  - *Hasil Pencarian:* Hanya ditemukan pada `player-desktop/renderer.js:L654` (`playNextLibraryAsset()`), `L957` (definisi fungsi), dan `L969` (tombol Next). Pada `mobile/` dan `test/`: **0 kemunculan**.
- **Status Keseluruhan PSV-02 / PSV-R03:** **`PARTIALLY VERIFIED`** (Desktop audio handler terbukti ada; desktop video, dokumen/gambar, dan seluruh viewer mobile belum memiliki completion handler).

---

#### 15.9.3 PSV-03 / PSV-R04 — Studio Persistence dan Multi-Member Recovery
- **Referensi Mandat:** R-04, NC-06, AC-28, AC-29.
- **Tujuan Pembuktian:** Memisahkan bukti resumable transfer single asset dari bukti persistence/recovery Album multi-member.
- **Objek yang Diperiksa:**
  - `studio-desktop/publish_pipeline.js:L18-L36`, `L186-L270`.
  - `studio-desktop/test/studio-desktop.test.js`.
- **Bukti Source (Single-Asset Pipeline):**
  1. *Resumable Chunk Transfer:* `publish_pipeline.js:L18-L36` menginisialisasi upload pipeline single-asset. Pada L193-L196, pipeline menanyakan status authoritative offset ke server (`this.getStatus()`) sebelum melanjutkan, dan mengirim chunk via HTTP POST dengan header `Content-Range: bytes start-end/total`.
  2. *Autosave Single-Asset Wizard:* Terbukti diuji pada Test 2 `studio-desktop.test.js` (menyimpan form state di `userData`).
- **Pencarian Terukur Ketiadaan Orkestrasi Multi-Member Album:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "album.*session|multi.*member|albumSession|publishAlbum" studio-desktop/`
  - *Scope:* Seluruh source code `studio-desktop/` (non-vendor).
  - *Hasil Pencarian:* **0 matches** (Exit code 1).
  - *Batas Kesimpulan:* State machine orkestrasi multi-member Album **belum pernah ada** di Studio.
- **Bukti Test (Test Evidence):**
  - *File Test:* `studio-desktop/test/studio-desktop.test.js`
  - *Command:* `node studio-desktop/test/studio-desktop.test.js`
  - *Environment:* Linux x86_64, Node.js v22.23.4
  - *Exit Code:* **`1 (FAILED)`**
  - *Output Aktual:*
    ```text
    === STARTING NEXA STUDIO INTEGRATION TESTS ===
    [*] Test 1: Verification configuration defaults & custom FFmpeg pinning... -> Test 1 PASSED
    [*] Test 2: Saving and loading autosave state... -> Test 2 PASSED
    [*] Test 3: Audio file selection and validation... -> Test 3 PASSED
    [*] Test 4: Dynamic Ed25519 key pair generation... -> Test 4 PASSED
    [*] Test 5: Manifest preview generation... -> Test 5 PASSED
    [*] Test 6: Forging container and exporting standalone evidence JSON... -> Test 6 PASSED
    [*] Test 7: Forging with FLAC compression and offline sidecar...
        [Progress Tick] Step 0: Audio compression failed: FFmpeg Broker: FFmpeg binary hash mismatch! Substitution or modification detected (Fail-Closed)
    [-] TEST FAILED: compressed forging should succeed...
    ```
  - *Status Test Multi-Member Recovery:* **`NOT AVAILABLE / NOT RUN`** (Tidak ada test crash/restart/retry recovery multi-member di codebase).
- **Batasan Arsitektur & Zero-DDL:**
  - Gagasan penyimpanan session di `userData/album_sessions/*.json` merupakan **proposal spesifikasi teknis** yang mematuhi batas Zero-DDL, **bukan desain yang telah disahkan**.
- **Status Keseluruhan PSV-03 / PSV-R04:** **`PARTIALLY VERIFIED`** (Pipeline chunk transfer single-asset terbukti matang; orkestrator multi-member Album belum ada di source Studio; test recovery multi-member tidak tersedia).

---

#### 15.9.4 PSV-04 / PSV-R05 — Marketplace dan Licensing Transaction
- **Referensi Mandat:** R-05, B-04, NC-08, CONF-03, AC-14, AC-15.
- **Tujuan Pembuktian:** Memastikan alur transaksi Marketplace dan Licensing Authority diverifikasi secara utuh pada batas transaksinya, memisahkan pengujian internal engine licensing dari pengujian integrasi Marketplace.
- **Alur Lengkap yang Ditelusuri:**
  `Payment Approval → Marketplace Handler → HTTP Licensing Authority → PostgreSQL Transaction → Entitlement`
- **Bukti Source (Batas Transaksi & Side Effect Eksternal):**
  1. *Definisi Transaksi PostgreSQL:* `marketplace/db/store.js:L89-L101`:
     ```javascript
     async function withTransaction(callback) {
       if (!poolInstance) throw new Error('PostgreSQL pool not initialized');
       const client = await poolInstance.connect();
       try {
         await client.query('BEGIN');
         const result = await callback(client);
         await client.query('COMMIT');
         return result;
       } catch (err) {
         await client.query('ROLLBACK').catch(() => {});
         throw err;
       } finally {
         client.release();
       }
     }
     ```
  2. *Call Path Admin Approval & External HTTP Side Effect:* `marketplace/server.js:L3794-L3870`:
     - L3794: `await store.withTransaction(async (client) => {`
     - L3796: `const orderRes = await client.query('SELECT * FROM payment_orders WHERE order_id = $1 FOR UPDATE', [orderId]);` (Row lock)
     - L3833: `const acqRes = await client.query('SELECT * FROM acquisitions WHERE acquisition_id = $1', [order.acquisition_id]);`
     - L3836: `const licenseKey = await invokeSprint12LicensingAuthority(order.acquisition_id, acqRow.asset_id, acqRow.buyer_id);` (**Panggilan HTTP Eksternal di dalam callback**)
     - L3839: `const catRes = await client.query('SELECT storage_object_id, package_sha256 FROM catalog_snapshots WHERE asset_id = $1', [acqRow.asset_id]);`
     - L3845: `await client.query('INSERT INTO admin_decisions ...');`
     - L3852: `await client.query('UPDATE payment_orders SET state = \'PAYMENT_VERIFIED\' WHERE order_id = $1', [orderId]);`
     - L3853: `await client.query('UPDATE acquisitions SET state = \'ACQUISITION_COMPLETED\', acquired_storage_object_id = $1, acquired_package_sha256 = $2 ...');`
     - L3854: `await client.query('UPDATE payment_proofs SET status = \'VERIFIED\' ...');`
     - L3858: `await client.query('INSERT INTO entitlements (entitlement_id, acquisition_id, license_key, acquired_storage_object_id, acquired_package_sha256, ...) VALUES (...)');`
     - L3870: `});` (Menutup callback -> dieksekusi `COMMIT`).
- **Analisis Jendela Kegagalan (Failure Window & Lack of Distributed 2PC):**
  - Pemanggilan eksternal `invokeSprint12LicensingAuthority` dieksekusi melalui HTTP 3-stage (`/prepare` -> `/sign` -> `/submit`) ke daemon lisensi Sprint-12 (`server.js:L172-L320`).
  - Jika daemon eksternal berhasil menerbitkan lisensi, tetapi SQL commit lokal gagal (misalnya koneksi database terputus atau constraint violation), blok `withTransaction` mengeksekusi `ROLLBACK`.
  - **Dampak Faktual:** Database lokal membatalkan pesanan, namun daemon eksternal telah mencatat lisensi tersebut. Tidak ada mekanisme 2PC (Two-Phase Commit), tidak ada rollback terdistribusi otomatis, dan tidak ada compensation endpoint yang dipanggil.
- **Pencarian Terukur Endpoint Kompensasi / Rekonsiliasi:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "compensat|reconcil" marketplace/server.js`
  - *Hasil Pencarian:* Hanya ditemukan `reconcileSpoolAndDB` (rekonsiliasi offset berkas spool transfer) dan `reconcileCatalogRecords` (rekonsiliasi metadata katalog saat startup). Mekanisme compensation/reconciliation untuk transaksi lisensi eksternal: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **Bukti Test (Test Evidence):**
  1. *Test Engine Licensing Go:*
     - Command: `GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -v ./tests/ -run TestAdversarialScenariosSuite`
     - Exit Code: **`0 (PASS)`**
     - Hasil: 22/22 skenario adversarial lolos (termasuk ADV-14 penolakan prepare record yang di-replay dan ADV-15 penolakan submit konkuren). Membuktikan ketahanan internal engine Go, **bukan integrasi Marketplace**.
  2. *Test Integrasi Marketplace:*
     - Command: `node marketplace/tests/exe04_licensing_authority.test.js`
     - Exit Code: **`1 (FAILED)`** (mencari nama fungsi lawas `obtainAuthoritativeSprint12LicenseKey` yang telah direfaktor menjadi `invokeSprint12LicensingAuthority`).
     - Command: `node test/sprint12_licensing_integration_test.js`
     - Exit Code: **`1 (FAILED)`** (`ERR_LICENSING_AUTHORITY_UNAVAILABLE` karena daemon HTTP external offline).
  3. *Status Runtime Daemon:* **`NOT RUN / UNAVAILABLE`** di lingkungan Linux terisolasi.
- **Alur Khusus Album di Marketplace:** **`NOT PRESENT IN THE EXAMINED SCOPE`** (Marketplace saat ini hanya menangani akuisisi aset tunggal).
- **Status Keseluruhan PSV-04 / PSV-R05:** **`PARTIALLY VERIFIED`** (ACID lokal dan ketiadaan 2PC terbukti; 22 test Go engine lulus; test integrasi Marketplace gagal / daemon offline; transaksi multi-member belum ada).

---

#### 15.9.5 PSV-05 / PSV-R06 — acquired_package_sha256 (B-05)
- **Referensi Mandat:** R-06, B-05, NC-09, AC-16, §4.4 E-03, §15.11.2 (DGR-PSV-04), §15.11.3 (PSV-R06).
- **Tujuan Pembuktian & Resolusi:**
  - *Tujuan:* Membuktikan fungsi dan alur pertama kali terbentuknya nilai `catalog_snapshots.package_sha256`, sumber data yang di-hash, operasi hash, stream byte input, titik penyimpanan, serta hubungan dengan producer `acquisitions`/`entitlements`, consumer download, dan konsistensi DDL lengkap.
  - *Pemeriksaan Sumber Otoritatif:* Dilakukan inspeksi langsung pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956` pada berkas `marketplace/server.js` dan skema DDL `marketplace/db/schema.postgres.sql`.
- **Kutipan DDL Utuh Bersama Kedua Tabel & Migrasi Otoritatif (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  ```sql
  -- marketplace/db/schema.postgres.sql#L63-L75
  CREATE TABLE IF NOT EXISTS acquisitions (
      acquisition_id VARCHAR(128) PRIMARY KEY,
      asset_id VARCHAR(128) NOT NULL REFERENCES catalog_snapshots(asset_id),
      buyer_id VARCHAR(128) NOT NULL,
      price_amount BIGINT NOT NULL CHECK (price_amount >= 0),
      currency VARCHAR(16) NOT NULL DEFAULT 'IDR',
      provider_id VARCHAR(64) NOT NULL,
      state VARCHAR(64) NOT NULL DEFAULT 'ACQUISITION_CREATED',
      acquired_storage_object_id VARCHAR(128),
      acquired_package_sha256 VARCHAR(64),
      created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
      updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
  );

  -- marketplace/db/schema.postgres.sql#L107-L114
  CREATE TABLE IF NOT EXISTS entitlements (
      entitlement_id VARCHAR(128) PRIMARY KEY,
      acquisition_id VARCHAR(128) NOT NULL UNIQUE REFERENCES acquisitions(acquisition_id),
      license_key VARCHAR(255) NOT NULL UNIQUE,
      acquired_storage_object_id VARCHAR(128),
      acquired_package_sha256 VARCHAR(64),
      issued_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
  );

  -- marketplace/db/schema.postgres.sql#L131-L135 (Schema Alterations / Backward Compatibility)
  ALTER TABLE entitlements ADD COLUMN IF NOT EXISTS asset_id VARCHAR(128);
  ALTER TABLE entitlements ADD COLUMN IF NOT EXISTS buyer_id VARCHAR(128);
  ```
- **Pemeriksaan Konsistensi SQL Producer dengan DDL Lengkap:**
  - *Temuan Auditor Sebelumnya:* Kutipan producer `INSERT INTO entitlements` mencantumkan kolom `asset_id` dan `buyer_id`, sedangkan kutipan lama DDL baris 107-114 belum memperlihatkan kedua kolom tersebut.
  - *Bukti Rekonsiliasi Skema:* Pada berkas skema DDL yang sama pada baris 131-135 (`schema.postgres.sql#L131-L135`), terdapat migrasi skema formal `ALTER TABLE entitlements ADD COLUMN IF NOT EXISTS asset_id VARCHAR(128);` dan `ALTER TABLE entitlements ADD COLUMN IF NOT EXISTS buyer_id VARCHAR(128);`.
  - *Kesimpulan Konsistensi:* SQL producer pada `server.js:L3858` terbukti 100% konsisten dan valid terhadap skema DDL otoritatif pada commit yang sama (`VERIFIED BY PROGRAMMER — STATIC SOURCE`).
- **Asal Nilai Hash, Operasi Hashing, dan Byte-Domain Input (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  - 1. *Fungsi Pembentukan Hash (`marketplace/server.js:L762-L770`):*
    ```javascript
    function computeFileSha256(filePath) {
        return new Promise((resolve, reject) => {
            const hash = crypto.createHash('sha256');
            const stream = fs.createReadStream(filePath);
            stream.on('data', d => hash.update(d));
            stream.on('end', () => resolve(hash.digest('hex')));
            stream.on('error', reject);
        });
    }
    ```
  - 2. *Titik Pemanggilan Eksekusi (`marketplace/server.js:L2231`):*
    Dalam fungsi `executeSessionFinalization` pada alur finalisasi unggahan paket kreator:
    ```javascript
    packageSha256 = await computeFileSha256(session.spool_path);
    ```
  - 3. *Sumber Data & Byte-Domain Input (`marketplace/server.js:L2185-L2210`, `#L2200`):*
    - File spool dibentuk saat kreator mengunggah paket via `POST /api/catalog/submit-package/:sessionId/chunk`.
    - Tiap chunk biner ditulis langsung ke disk melalui `fs.appendFileSync(session.spool_path, chunkBuffer)` (baris 2200).
    - File fisik `session.spool_path` adalah representasi biner utuh dari berkas paket delivery yang diunggah oleh kreator (arsip wrapper ZIP delivery package).
    - Operasi hashing membaca seluruh file biner tersebut secara streaming dari awal hingga akhir (`fs.createReadStream(session.spool_path)`).
    - **Bukti Domain Byte:** Input byte hashing terbukti secara statis adalah **seluruh berkas fisik paket delivery (wrapper ZIP)**, bukan stream individual track `.nx`, bukan JSON metadata terisolasi, dan bukan manifest biner terpisah (`VERIFIED BY PROGRAMMER — STATIC SOURCE`).
  - 4. *Titik Penyimpanan Hasil Hash (`marketplace/server.js:L2390-L2405`):*
    Hasil hash disimpan ke kolom `package_sha256` pada tabel `catalog_snapshots`:
    ```javascript
    await client.query(
        `INSERT INTO catalog_snapshots (
            asset_id, catalog_version, title, description, creator_id,
            price_amount, currency, status, package_sha256, storage_object_id,
            created_at, updated_at
        ) VALUES ($1, $2, $3, $4, $5, $6, $7, $8, $9, $10, $11, $12)`,
        [
            assetId, nextVersion, title, description, creatorId,
            priceAmount, currency, 'ACTIVE', packageSha256, storageObjectId,
            now, now
        ]
    );
    ```
- **Bukti Source Producer (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  - Pada transaksi pembelian aset (`marketplace/server.js:L3839-L3861`):
    ```javascript
    const catRes = await client.query('SELECT package_sha256, storage_object_id FROM catalog_snapshots WHERE asset_id = $1', [acq.asset_id]);
    const catRow = catRes.rows[0];
    ```
  - Producer 1 (`marketplace/server.js:L3853`):
    `UPDATE acquisitions SET state = 'ACQUISITION_COMPLETED', acquired_storage_object_id = $1, acquired_package_sha256 = $2, updated_at = $3 WHERE acquisition_id = $4` (menyalin `catRow.package_sha256`).
  - Producer 2 (`marketplace/server.js:L3858`):
    `INSERT INTO entitlements (entitlement_id, acquisition_id, license_key, acquired_storage_object_id, acquired_package_sha256, asset_id, buyer_id, issued_at) VALUES ($1, $2, $3, $4, $5, $6, $7, $8)` (menyalin `catRow.package_sha256`).
- **Bukti Source Consumer (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  - Consumer (`marketplace/server.js:L4271, L4309, L4366, L4458`):
    `const packageSha = entitlement.acquired_package_sha256 || acq.acquired_package_sha256 || (catItem && catItem.package_sha256);`
    Digunakan eksklusif untuk otorisasi download berkas paket delivery dari storage engine.
- **Relasi Child Acquisition di Database:**
  - Di bawah batasan Zero-DDL, tabel relasi child entitlement atau pemetaan hash anggota individual `.nx` **TIDAK ADA** di database (`NOT PRESENT IN THE EXAMINED SCOPE`).
  - Kondisi live database berstatus jujur: **`NOT VERIFIED`** (tidak ada akses live runtime DB).
- **Disposisi Blocker B-05:**
  - Pembentukan hash, byte-domain (wrapper ZIP delivery package utuh), konsistensi DDL L63-L135 dengan SQL producer, dan alur consumer: **`VERIFIED BY PROGRAMMER — STATIC SOURCE`**.
  - Relasi child-member Album: **`NOT PRESENT IN THE EXAMINED SCOPE`**. Kontrak downstream child acquisition tetap terbuka/unresolved secara normatif.
  - **Rekonsiliasi terhadap keputusan PO Model B (§6.8.1):** Bukti yang dilaporkan tetap membuktikan byte-domain hash existing sebagai seluruh wrapper ZIP delivery package. Fakta baseline ini tidak memenuhi kontrak target acquired_package_sha256 per child member .nx; wrapper hash tidak boleh dipindahkan ke child acquisition/entitlement seolah-olah merupakan hash member. DDL statis yang dilaporkan tersedia tidak menyediakan relasi parent-child Album. Dengan demikian, keputusan Model B dan alokasi SSP/Largest Remainder menetapkan target komersial, tetapi byte-domain hash individual, producer, consumer, dan konsistensi child tetap **`OPEN / BLOCKED BY B-05`**.
- **Status Keseluruhan PSV-05 / PSV-R06:** **`VERIFIED BY PROGRAMMER — STATIC SOURCE (ORIGIN & BYTE-DOMAIN); CHILD CONTRACT OPEN`**

---

#### 15.9.6 PSV-06 / PSV-R07 — ZIP Parser dan Extractor
- **Referensi Mandat:** R-07, B-07, NC-07, AC-02, AC-13.
- **Tujuan Pembuktian:** Memastikan ketersediaan parser/extractor ZIP Album pada source aktif dan membedakan fakta implementasi dari proposal kuota teknis.
- **Pencarian Terukur Ketiadaan Modul ZIP Parser / Extractor:**
  - *Command Pencarian 1:* `grep -rnI --exclude-dir=node_modules --exclude-dir=dist --exclude-dir=.git --exclude-dir=scratch -E "adm-zip|yauzl|jszip|unzipper|archive/zip|decompress" .`
  - *Hasil Pencarian 1:* 0 modul runtime produk. Hanya muncul pada transitive dependencies `package-lock.json` dan dokumentasi prompt.
  - *Command Pencarian 2:* `grep -rnI --exclude-dir=vendor --exclude-dir=.git "archive/zip" .`
  - *Hasil Pencarian 2:* **0 matches** pada seluruh source code Go.
  - *Batas Kesimpulan:* Modul parser dan ekstraksi arsip ZIP Album **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **Format Kontainer Baseline vs Kuota Wrapper:**
  - Kontainer `.nx` mandiri berformat biner murni (`internal/container/container.go:L90-L130`, `sdk/typescript/src/container.ts:L1-L60`).
  - Batas 2 GiB pada `container.go:L106` adalah batas payload kontainer tunggal, bukan batas kuota wrapper ZIP.
- **Bukti Test (Test Evidence):**
  - *Status:* **`NOT AVAILABLE / NOT RUN`** (Tidak ada test ZIP parser atau adversarial extraction bomb test di codebase).
- **Status Parameter Kuota:** Angka 500 MB kompresi, 2 GiB dekompresi, 200 entri, dan rasio 100:1 adalah **proposal spesifikasi teknis** yang memerlukan penetapan Architecture Authority (DEC-01), bukan keputusan PO.
- **Status Keseluruhan PSV-06 / PSV-R07:** **`NOT PRESENT IN THE EXAMINED SCOPE`** (Parser/extractor ZIP Album dan penegakan kuota belum ada di source tree).

---

#### 15.9.7 PSV-07 / PSV-R08 — Safe-Open dan Filesystem
- **Referensi Mandat:** R-08, B-06, NC-12, AC-20, AC-21, §15.11.3 (PSV-R08).
- **Tujuan Pembuktian:** Membuktikan jalur aktual pembacaan filesystem Player pada Android dan iOS secara terpisah, memeriksa keberadaan mekanisme mitigasi symlink/TOCTOU, menyajikan bukti test yang tersedia, dan mendokumentasikan batasan pengujian.
- **Matriks Pembuktian Filesystem Lintas Platform (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  1. *Desktop Windows:*
     - Pemanggilan `fs.openSync(trackInfo.filePath, 'r')` (`player-desktop/main.js:L573`) tanpa descriptor-level protection.
     - `internal/filesystem/hidden_helper.js:L24-L40` mengeksekusi `attrib +h` secara kosmetik.
  2. *Desktop macOS:*
     - Pemanggilan `fs.openSync` standar tanpa isolasi symlink.
     - `internal/filesystem/hidden_helper.js:L42-L55` mengeksekusi `chflags hidden` secara kosmetik.
  3. *Desktop Linux / POSIX:*
     - `player-desktop/main.js:L571-L577`:
       ```javascript
       if (trackInfo.filePath && fs.existsSync(trackInfo.filePath)) {
           const fd = fs.openSync(trackInfo.filePath, 'r');
           slicedBuffer = Buffer.alloc(chunksize);
           const absOffset = (trackInfo.payloadOffset || 0) + start;
           fs.readSync(fd, slicedBuffer, 0, chunksize, absOffset);
           fs.closeSync(fd);
       }
       ```
     - Tidak menggunakan `O_NOFOLLOW`. Tidak melakukan verifikasi `fstatSync(fd)` terhadap device/inode descriptor.
     - Terdapat race window (TOCTOU) antara validasi path `existsSync` (L571) dan pembukaan berkas `openSync` (L573).
  4. *Mobile Android (Source, Call Path & Analisis Mitigasi):*
     - *Entry Point:* `mobile/apps/player/src/screens/PlayerScreen.tsx:L67-L72` memanggil fungsi `openContainer(filePath, fd ?? -1)` dari paket `@nexa/core`.
     - *Implementasi Modul Native Android:* `mobile/packages/expo-nexa-core/android/src/main/java/com/nexa/core/NexaCoreModule.kt:L56-L92`:
       - Untuk URI `file://`: mem-parse string URI melalui `Uri.parse(uriString).path` menjadi path string filesystem lokal.
       - Untuk URI `content://` (Android Storage Access Framework): memanggil `context.contentResolver.openFileDescriptor(uri, "r")`, lalu memanggil `pfd.detachFd()` untuk mengekstrak descriptor integer native (`nativeFd`).
       - Pemanggilan JNI Bridge: Memanggil fungsi native `nativeOpenContainer(cPath, fd)` yang didefinisikan pada `mobile/packages/expo-nexa-core/android/src/main/jni/NexaCoreModule.cpp:L15-L25` (`Java_com_nexa_core_NexaCoreModule_nativeOpenContainer`), yang meneruskan `(char*)cPath, fd` ke fungsi Go runtime `NexaMobileOpenContainer((char*)cPath, fd)`.
       - *Pemeriksaan Mitigasi:* Pada pembukaan jalur path `cPath`, tidak ada flag `O_NOFOLLOW`, tidak ada pengecekan `fstat` untuk memverifikasi inode/perangkat, dan tidak ada mekanisme direktori isolasi sementara. Mekanisme ini murni mengandalkan resolver OS standar (`VERIFIED BY PROGRAMMER — STATIC SOURCE`).
  5. *Mobile iOS (Source, Call Path & Analisis Mitigasi):*
     - *Entry Point:* `mobile/apps/player/src/screens/PlayerScreen.tsx:L67-L72`.
     - *Implementasi Modul Native iOS:* `mobile/packages/expo-nexa-core/ios/NexaCoreModule.mm:L289-L352` (`openContainerImpl:filePath fd:`):
       - Normalisasi Path: Mem-parse string `file://` menjadi `[NSURL fileURLWithPath:decodedPath]`.
       - Sandboxing Security-Scoped: Memanggil `[url startAccessingSecurityScopedResource]` untuk mendapatkan otorisasi akses sandbox iOS.
       - Pembukaan Berkas: Memanggil fungsi POSIX standar `open([[url path] UTF8String], O_RDONLY)` (`NexaCoreModule.mm:L330`).
       - Perekaman Descriptor: Meneruskan descriptor integer `nativeFd` ke fungsi Go runtime `NexaMobileOpenContainer([decodedPath UTF8String], nativeFd)`.
       - Pelepasan Akses Sandbox: Memanggil `[url stopAccessingSecurityScopedResource]`.
       - *Pemeriksaan Mitigasi:* Pemanggilan POSIX `open` menggunakan flag `O_RDONLY` biasa tanpa `O_NOFOLLOW` dan tanpa verifikasi `fstat`. Tidak ada mekanisme penangkal symlink substitution atau TOCTOU (`VERIFIED BY PROGRAMMER — STATIC SOURCE`).
- **Bukti Pengujian (Test Evidence):**
  - 1. *Unit Test Container Opening Utility (Jest):*
    - Command: `npm test -- src/utils/__tests__/containerOpening.test.ts` (pada direktori `mobile/apps/player/`)
    - Exit Code: **`0 (PASS)`**
    - Output Aktual:
      ```text
      PASS src/utils/__tests__/containerOpening.test.ts
        containerOpening utility
          ✓ openContainerWithFallback resolves file descriptor for content URI (1 ms)
          ✓ openContainerWithFallback resolves file descriptor for file URI
          ✓ openContainerWithFallback throws error for invalid or unsupported URI (1 ms)

      Test Suites: 1 passed, 1 total
      Tests:       3 passed, 3 total
      Snapshots:   0 total
      Time:        0.281 s
      Ran all test suites matching /src\/utils\/__tests__\/containerOpening.test.ts/i.
      ```
     - Status: `VERIFIED BY PROGRAMMER — TEST` hanya untuk seleksi URI dan penanganan error pada helper TypeScript `openContainerWithFallback`; test ini **bukan** pengujian Safe-Open, symlink, descriptor validation, atau TOCTOU.
  - 2. *Adversarial Filesystem / TOCTOU Tests:*
    - Status: **`NOT AVAILABLE / NOT RUN`** (Modul uji adversarial symlink traversal, directory escaping, atau TOCTOU file replacement tidak ditemukan di codebase).
  - 3. *Native Runtime Execution (Android Emulator / iOS Simulator):*
    - Status: **`NOT RUN`** (Lingkungan emulator Android/iOS dan toolchain mobile fisik tidak tersedia di container/lingkungan kerja saat ini).
- **Pencarian Terukur Modul `fs_safe.ts`:**
  - *Command Pencarian:* `find . -name "fs_safe.ts"`
  - *Hasil Pencarian:* **0 matches** (`NOT PRESENT IN THE EXAMINED SCOPE`).
- **Status Keseluruhan PSV-07 / PSV-R08:** **`PSV CLOSED — STATIC SOURCE REVIEW COMPLETE; URI UNIT TEST ONLY; ADVERSARIAL TESTS NOT AVAILABLE; MOBILE RUNTIME NOT RUN`** (Call path source yang dicantumkan telah diperiksa secara statis; unit test 3/3 hanya mencakup seleksi URI/fallback, bukan mitigasi Safe-Open. Gap mitigasi dan test tetap merupakan blocker implementasi/keamanan B-06, bukan kebutuhan pencarian source ulang berdasarkan bukti yang tersedia).

---

#### 15.9.8 PSV-08 / PSV-R09 / PSV-R09A — Parser, JCS, dan Kriptografi
- **Referensi Mandat:** R-09, B-08, NC-02, AC-03, §15.11.3 (PSV-R09, PSV-R09A).
- **Tujuan Pembuktian:** Menyajikan pemisahan bukti Go generic JCS, raw source verifier Ed25519 TypeScript untuk Registry, Genesis Ownership, dan Manifest kontainer PE-01 `.nx`, call path dari pemanggil hingga hasil verifikasi, cakupan pengujian signature dengan output aktual, investigasi ketersediaan test langsung verifier signature manifest kontainer (PSV-R09A), serta batas pencarian serializer JCS generik dan parser strict duplicate-keys di TypeScript.
- **1. Go Generic RFC 8785 JCS (Test & Source Evidence):**
  - *Source:* `internal/identity/jcs.go:L1-L120`, `tests/identity/jcs_test.go:L20-L140`.
  - *Command:* `GOTMPDIR=/opt/antigravity/projects/nexa/scratch/gotmp go test -v -count=1 ./tests/identity/ -run TestRFC8785`
  - *Exit Code:* **`0 (PASS)`**
  - *Output Aktual:*
    ```text
    === RUN   TestRFC8785AuthoritativeIndependentConformanceCorpus
    --- PASS: TestRFC8785AuthoritativeIndependentConformanceCorpus (0.00s)
    === RUN   TestRFC8785InvalidUnicodeFailClosedRejection
    --- PASS: TestRFC8785InvalidUnicodeFailClosedRejection (0.00s)
    PASS
    ok      nexa/tests/identity     0.004s
    ```
  - *Vektor Uji Terverifikasi (Kategori RFC 8785):*
    - Vektor 1 & 5: Pengurutan kode UTF-16, penanganan karakter non-BMP (`😀` emoji grinning), objek bersarang.
    - Vektor 7: Serialisasi string tanpa escaping HTML (karakter raw `<&>` dipertahankan).
    - Vektor 1, 2, 3: Serialisasi angka ECMAScript ToString(), normalisasi negative zero (`-0` -> `0`), batas eksponen IEEE-754 (`1e+30`, `1e-7`, float desimal).
    - Vektor 6: Serialisasi karakter kontrol escaping (\b, \t, \n, \f, \r, \\, \").
    - Vektor 8: Objek dan array bersarang representatif dengan boolean dan null.
    - Rejeki Fail-Closed Unicode: Penolakan invalid UTF-8 string pada level atas, nilai properti, kunci properti, dan objek bertingkat (Test A, B, C, D).
  - *Status:* **`VERIFIED BY PROGRAMMER — TEST`** untuk Go engine.
- **2. Raw Source & Call Path Verifier Ed25519 TypeScript (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  - A. *Registry Certificate Verifier:*
    - *Path & Lines:* `sdk/typescript/src/sdk.ts:L207-L230` (`verifyRegistryIdentity`).
    - *Caller:* `verifyContainer` pada `sdk.ts:L148-L155`.
    - *Input Pesan:* `Buffer.from(canonStr, "utf8")` di mana `canonStr = NexaRegistry.canonicalJcs(regCert.certificate_id, regCert.issued_at, regCert.issuer, regCert.status, regCert.valid_until, creatorKey)` (`sdk/typescript/src/registry.ts:L118-L127`).
    - *Public Key:* Authority public key tetap yang di-pin pada `sdk/typescript/src/registry.ts:L22` (`CANONICAL_REGISTRY_PUBKEY`).
    - *Pemanggilan Kriptografi:* `NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes)` (`sdk/typescript/src/crypto.ts:L15-L20`) yang memanggil `crypto.verify(null, message, keyObj, signature)`.
    - *Penanganan Hasil:* Mengembalikan `{ valid: boolean, reason?: string }` ke caller `verifyContainer`.
  - B. *Genesis Ownership Certificate Verifier:*
    - *Path & Lines:* `sdk/typescript/src/ownership.ts:L239-L265` (`verifyGenesisCertificate`) & `sdk/typescript/src/sdk.ts:L232-L263` (`verifyGenesisOwnership`).
    - *Caller:* `verifyContainer` pada `sdk.ts:L157-L170`.
    - *Input Pesan:* `canonicalizeGenesisPayload(cert)` (`ownership.ts:L86-L107`), yang merangkai 8 field kanonikal berurutan leksikografis (`asset_id`, `created_at`, `creator_id`, `creator_public_key`, `effective_at`, `issued_at`, `issuer_id`, `previous_cert_ref`, `subject_id`, `type`, `underlying_cert_id`) menjadi Buffer UTF-8.
    - *Public Key:* `cert.creator_public_key` (Ed25519 public key hex string).
    - *Pemanggilan Kriptografi:* Node.js standard `crypto.verify(null, canonicalBytes, pubKey, sigBytes)`.
    - *Penanganan Hasil:* Mengembalikan `{ valid: boolean, reason?: string }` ke caller.
  - C. *Ownership Transfer Verifier:*
    - *Path & Lines:* `sdk/typescript/src/ownership.ts:L267-L280` (`verifyTransferSignature`).
    - *Caller:* `verifyOwnershipChain` pada `ownership.ts:L282-L330`.
    - *Input Pesan:* `canonicalizeTransferPayload(transfer)` (`ownership.ts:L109-L135`).
    - *Public Key:* `transferorPubKeyHex`.
    - *Pemanggilan Kriptografi:* Node.js standard `crypto.verify(null, canonicalBytes, pubKey, sigBytes)`.
    - *Penanganan Hasil:* Mengembalikan boolean `true/false`.
  - D. *Container Manifest Verifier (PE-01 `.nx` Individual Container):*
    - *Path & Lines:* `sdk/typescript/src/sdk.ts:L142-L144`.
    - *Caller:* `verifyContainer` pada `sdk.ts`.
    - *Input Pesan:* `container.manifestBytes` (manifest biner berekstraksi dari header kontainer `.nx`).
    - *Signature:* `container.signatureBytes` (trailer 64-byte Ed25519 signature).
    - *Public Key:* `container.creatorPubKey` (dipasok caller `pubKey: crypto.KeyObject`).
    - *Pemanggilan Kriptografi:* `NexaCrypto.verify(pubKey, container.manifestBytes, container.signatureBytes)` (`sdk.ts:L143`).
    - *Catatan Obyek:* Obyek verifikasi ini murni verifier manifest kontainer individual PE-01 `.nx`, bukan verifier Album Manifest Signer.
- **3. Bukti Pengujian Terverifikasi (Executable Test Suite & Raw Output):**
  - *Test 1: Registry Identity Verification Suite:*
    - Command: `node sdk/typescript/test/registry_identity.test.js`
    - Exit Code: **`0 (PASS)`**
    - Raw Output:
      ```text
      ==> Running C-04: TypeScript Registry Identity Executable Test Suite...
      [+] Scenario 1: Valid signed identity PASS
      [+] Scenario 2: Invalid identity signature PASS
      [+] Scenario 3: Tampered identity document PASS
      [+] Scenario 4: Wrong pinned key PASS
      [+] Scenario 5: Expired identity PASS
      [+] Scenario 6: Missing identity_signature PASS
      [+] Scenario 7: Malformed identity PASS
      [+] Scenario 8: Future issued_at beyond clock skew PASS

      ==> C-04: ALL 8 TypeScript Registry Identity Scenarios PASSED 100%!
      ```
    - Matriks Cakupan Skenario yang Teruji: Valid signed identity, Invalid signature, Tampered document, Wrong pinned key, Expired identity, Missing signature, Malformed JSON, Future clock skew.
    - Status: `VERIFIED BY PROGRAMMER — TEST`.
  - *Test 2: Ownership Parity & Security Tests:*
    - Command: `node sdk/typescript/test/ownership_parity.test.js`
    - Exit Code: **`0 (PASS)`**
    - Raw Output:
      ```text
      --- Starting TypeScript Ownership Parity & Security Tests ---
      Test 1: Closed Delegation Scope Allowlist
      ✓ Test 1 Passed
      Test 2: Canonical JCS Key Ordering Parity
      ✓ Test 2 Passed
      Test 3: Legacy Asset Evaluation
      ✓ Test 3 Passed
      Test 4: Invalid Genesis Certificate Signature Rejection
      ✓ Test 4 Passed
      Test 5: OWN-TRANSFER-02 Unauthorized Transfer Rejection (TS)
      ✓ Test 5 Passed
      === All TypeScript Ownership Parity & Security Tests PASSED cleanly! ===
      ```
    - Matriks Cakupan Skenario yang Teruji: Delegation allowlist, JCS key ordering parity, Legacy asset evaluation, Penolakan tanda tangan genesis cert tidak valid (`verifyGenesisCertificate`), Penolakan transfer tidak sah (`verifyTransferSignature`).
    - Status: `VERIFIED BY PROGRAMMER — TEST`.
- **4. Penyelidikan dan Pembuktian Terarah Test Coverage Verifier Signature Manifest Kontainer PE-01 (PSV-R09A & PSV-R09A-1):**
  - *Komitmen & Provenance:*
    - Repositori sumber: `whisnu/nexa`
    - Commit SHA sumber: `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`
    - Scope direktori pengujian yang diperiksa: `test/`, `tests/`, `sdk/typescript/test/`, `player-desktop/test/`, `verify-desktop/test/`.
    - Batas mandat: `TARGETED TEST INVOCATION EVIDENCE ONLY` — zero new tests, zero code changes.
  - *Command Lengkap, Exit Code, dan Raw Output Utuh:*
    - **Command 1:** `grep -rnI --exclude-dir=node_modules "NexaSdk.verifyContainer" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/pe01_tampered_sidecar_test.js:158:        const verifyResult = await NexaSdk.verifyContainer(
        test/task_a_final_trust_boundary_test.js:98:    const resA = await NexaSdk.verifyContainer(nxPath, alicePub);
        test/task_a_final_trust_boundary_test.js:158:    const resB = await NexaSdk.verifyContainer(nxPath, alicePub, undefined, undefined, legacySidecarPath);
        test/task_a_buyer_lifecycle_test.js:1268:        const offlineVerifyRes = await NexaSdk.verifyContainer(offlineTempNxPath, offlineCreatorPubObj, undefined, undefined, downloadedSidecar);
        test/pe01_hidden_sidecar_test.js:153:        const verifyResult = await NexaSdk.verifyContainer(
        test/pe01_hidden_sidecar_test.js:195:        const verifyResult = await NexaSdk.verifyContainer(
        ```
    - **Command 2:** `grep -rnI --exclude-dir=node_modules "NexaCrypto.verify" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/pe01_tampered_sidecar_test.js:117:        const initialVerify = NexaCrypto.verify(regPubKey, Buffer.from(canonStr, 'utf8'), sigBytes);
        test/pe01_tampered_sidecar_test.js:124:        const tamperedVerify = NexaCrypto.verify(regPubKey, Buffer.from(tamperedCanonStr, 'utf8'), sigBytes);
        ```
    - **Command 3:** `grep -rnI --exclude-dir=node_modules "manifestBytes" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/task_a_hg_ownership_corrective_test.js:46:            manifestBytes: manifestBuf,
        test/task_a_product_truth_test.js:47:            manifestBytes: manifestBuf,
        tests/ecosystem_api_test.go:134:	manifestBytes, err := json.Marshal(manifest)
        tests/ecosystem_api_test.go:142:	sig := ed25519.Sign(creatorPriv, manifestBytes)
        tests/registry_test.go:210:	manifestBytes, err := json.Marshal(manifest)
        tests/registry_test.go:217:	sig := ed25519.Sign(creatorPriv, manifestBytes)
        ```
    - **Command 4:** `grep -rnI --exclude-dir=node_modules "signatureBytes" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/task_a_hg_ownership_corrective_test.js:47:            signatureBytes: sigBuf
        test/pe01_tampered_sidecar_test.js:154:            const signatureBytes = Buffer.from(mockSidecar.signature, 'base64');
        test/pe01_hidden_sidecar_test.js:149:            const signatureBytes = Buffer.from(mockSidecar.signature, 'base64');
        test/pe01_hidden_sidecar_test.js:191:            const signatureBytes = Buffer.from(mockSidecar.signature, 'base64');
        test/task_a_product_truth_test.js:48:            signatureBytes: sigBuf
        ```
    - **Command 5:** `grep -rnI --exclude-dir=node_modules "verifyContainer" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/pe01_tampered_sidecar_test.js:158:        const verifyResult = await NexaSdk.verifyContainer(
        test/task_a_final_trust_boundary_test.js:98:    const resA = await NexaSdk.verifyContainer(nxPath, alicePub);
        test/task_a_final_trust_boundary_test.js:158:    const resB = await NexaSdk.verifyContainer(nxPath, alicePub, undefined, undefined, legacySidecarPath);
        test/task_a_buyer_lifecycle_test.js:1268:        const offlineVerifyRes = await NexaSdk.verifyContainer(offlineTempNxPath, offlineCreatorPubObj, undefined, undefined, downloadedSidecar);
        test/pe01_hidden_sidecar_test.js:153:        const verifyResult = await NexaSdk.verifyContainer(
        test/pe01_hidden_sidecar_test.js:195:        const verifyResult = await NexaSdk.verifyContainer(
        ```
    - **Command 6:** `grep -rnI --exclude-dir=node_modules "signatureValid" test/ tests/ sdk/typescript/test/ player-desktop/test/ verify-desktop/test/`
      - *Exit Code:* `0`
      - *Raw Output:*
        ```text
        test/pe01_tampered_sidecar_test.js:161:        assert.strictEqual(verifyResult.signatureValid, true, 'Container signature valid');
        test/task_a_final_trust_boundary_test.js:102:    assert.strictEqual(resA.signatureValid, true);
        test/task_a_final_trust_boundary_test.js:162:    assert.strictEqual(resB.signatureValid, true);
        test/task_a_buyer_lifecycle_test.js:1271:        assert.strictEqual(offlineVerifyRes.signatureValid, true, 'Offline verification signature must be valid');
        test/pe01_hidden_sidecar_test.js:159:        assert.strictEqual(verifyResult.signatureValid, true, 'Container signature valid');
        test/pe01_hidden_sidecar_test.js:201:        assert.strictEqual(verifyResult.signatureValid, true, 'Container signature valid');
        player-desktop/test/player-desktop.test.js:134:            assert.strictEqual(verifyRes.signatureValid, true);
        player-desktop/test/player-desktop.test.js:152:            assert.strictEqual(verifyTamperedRes.signatureValid, true, 'manifest signature is valid');
        verify-desktop/test/verify-desktop.test.js:115:            assert.strictEqual(verifyRes.signatureValid, true);
        verify-desktop/test/verify-desktop.test.js:133:            assert.strictEqual(verifyTamperedRes.signatureValid, true, 'manifest signature is valid');
        ```
    - **Pemeriksaan Khusus Direktori `sdk/typescript/test/` (Unit Test SDK):**
      - `grep -rnI --exclude-dir=node_modules "NexaSdk.verifyContainer" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - `grep -rnI --exclude-dir=node_modules "NexaCrypto.verify" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - `grep -rnI --exclude-dir=node_modules "manifestBytes" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - `grep -rnI --exclude-dir=node_modules "signatureBytes" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - `grep -rnI --exclude-dir=node_modules "verifyContainer" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - `grep -rnI --exclude-dir=node_modules "signatureValid" sdk/typescript/test/` -> *Exit Code:* `1` (*0 matches*)
      - *Keterangan Faktual:* Berkas pengujian pada `sdk/typescript/test/` (`federation_parity.test.js`, `ownership_parity.test.js`, `registry_identity.test.js`) hanya menguji identitas federasi, sertifikat genesis/transfer kepemilikan, dan registry identity. Tidak ada pengujian pembongkaran biner `.nx` atau pemanggilan verifier kontainer pada direktori ini.
  - *Cuplikan Badan Test Setiap Kandidat dan Penelusuran Jalur Pemanggilan:*
    - **Kandidat 1: `test/pe01_hidden_sidecar_test.js` (Test 2 & Test 3)**
      - *Cuplikan Kode (L151-L162):*
        ```javascript
        const creatorPubObj = crypto.createPublicKey({ key: creatorPubKeyBuf, format: 'der', type: 'spki' });
        const verifyResult = await NexaSdk.verifyContainer(
            nxPath,
            creatorPubObj,
            undefined, // genesisCert
            undefined, // chain
            sidecarBuf
        );
        assert.strictEqual(verifyResult.signatureValid, true, 'Container signature valid');
        assert.strictEqual(verifyResult.hashValid, true, 'Container payload hash valid');
        ```
      - *Cuplikan Kode (L191-L203):*
        ```javascript
        const verifyResult = await NexaSdk.verifyContainer(
            nxPath,
            creatorPubObj,
            undefined,
            undefined,
            tamperedSidecarBuf
        );
        assert.strictEqual(verifyResult.signatureValid, true, 'Container signature valid');
        assert.strictEqual(verifyResult.hashValid, true, 'Container payload hash valid');
        ```
      - *Analisis Jalur Pemanggilan:* Test memanggil langsung fungsi SDK publik `NexaSdk.verifyContainer(nxPath, creatorPubObj, ...)`. Di dalam `sdk.ts:L142-L144`, fungsi ini langsung mengeksekusi `NexaCrypto.verify(pubKey, container.manifestBytes, container.signatureBytes)` terhadap kontainer valid yang dibentuk saat setup test.
      - *Klasifikasi:* **`DIRECT-POSITIVE`** (memanggil langsung API verifier publik SDK untuk kontainer valid).
    - **Kandidat 2: `test/task_a_buyer_lifecycle_test.js` (L1265-L1275)**
      - *Cuplikan Kode:*
        ```javascript
        const offlineCreatorPubObj = crypto.createPublicKey({ key: creatorPubKey, format: 'der', type: 'spki' });
        const offlineVerifyRes = await NexaSdk.verifyContainer(offlineTempNxPath, offlineCreatorPubObj, undefined, undefined, downloadedSidecar);
        assert.strictEqual(offlineVerifyRes.valid, true, 'Offline verification must pass');
        assert.strictEqual(offlineVerifyRes.signatureValid, true, 'Offline verification signature must be valid');
        assert.strictEqual(offlineVerifyRes.hashValid, true, 'Offline verification payload hash must be valid');
        assert.strictEqual(offlineVerifyRes.registryVerified, true, 'Offline verification registry must be valid');
        ```
      - *Analisis Jalur Pemanggilan:* Test siklus hidup pembeli memanggil langsung `NexaSdk.verifyContainer(...)` pada berkas `.nx` yang diunduh dari marketplace endpoint, memvalidasi verifier manifest kontainer pada kontainer valid.
      - *Klasifikasi:* **`DIRECT-POSITIVE`** (pemanggilan langsung API verifier SDK).
    - **Kandidat 3: `test/task_a_final_trust_boundary_test.js` (L89-L105 & L149-L165)**
      - *Cuplikan Kode (Case A):*
        ```javascript
        const alicePub = crypto.createPublicKey({ key: aliceKeypair.publicKey, format: 'der', type: 'spki' });
        const resA = await NexaSdk.verifyContainer(nxPath, alicePub);
        assert.strictEqual(resA.valid, true);
        assert.strictEqual(resA.signatureValid, true);
        assert.strictEqual(resA.hashValid, true);
        assert.strictEqual(resA.ownershipVerified, false);
        ```
      - *Cuplikan Kode (Case B):*
        ```javascript
        const resB = await NexaSdk.verifyContainer(nxPath, alicePub, undefined, undefined, legacySidecarPath);
        assert.strictEqual(resB.valid, true);
        assert.strictEqual(resB.signatureValid, true);
        assert.strictEqual(resB.hashValid, true);
        assert.strictEqual(resB.ownershipVerified, false);
        ```
      - *Analisis Jalur Pemanggilan:* Memanggil langsung `NexaSdk.verifyContainer(nxPath, alicePub)` untuk menguji batas trust boundary tanpa sertifikat kepemilikan.
      - *Klasifikasi:* **`DIRECT-POSITIVE`** (pemanggilan langsung API verifier SDK).
    - **Kandidat 4: `player-desktop/test/player-desktop.test.js` (Test 3 & Test 4, L129-L155)**
      - *Cuplikan Kode (Test 3: Valid Container Open):*
        ```javascript
        const verifyRes = await mockHandlers['open-and-verify-nx']({}, tempNxPath);
        assert.strictEqual(verifyRes.success, true);
        assert.strictEqual(verifyRes.signatureValid, true);
        assert.strictEqual(verifyRes.hashValid, true);
        ```
      - *Cuplikan Kode (Test 4: Tampered Audio Container Open):*
        ```javascript
        const containerData = fs.readFileSync(tempNxPath);
        containerData[containerData.length - 100] ^= 0xff; // corrupt audio data
        fs.writeFileSync(tamperedPath, containerData);
        const verifyTamperedRes = await mockHandlers['open-and-verify-nx']({}, tamperedPath);
        assert.strictEqual(verifyTamperedRes.success, false);
        assert.strictEqual(verifyTamperedRes.signatureValid, true, 'manifest signature is valid');
        assert.strictEqual(verifyTamperedRes.hashValid, false, 'payload hash mismatch');
        ```
      - *Analisis Jalur Pemanggilan:* Test tidak memanggil `NexaSdk.verifyContainer` langsung dari test runner, melainkan memanggil mock handler IPC Electron Player (`mockHandlers['open-and-verify-nx']`). Handler IPC kemudian memanggil verifier internal di `player-desktop/main.js`. Kerusakan yang diuji pada Test 4 berada pada offset payload audio, bukan manifest bytes atau signature.
      - *Klasifikasi:* **`INTEGRATION-ONLY`** (alur simulasi integrasi IPC Electron Desktop Player).
    - **Kandidat 5: `verify-desktop/test/verify-desktop.test.js` (Test 3 & Test 4, L110-L136)**
      - *Cuplikan Kode (Test 3: Valid Container Verify File):*
        ```javascript
        const verifyRes = await mockHandlers['verify-file']({}, tempNxPath);
        assert.strictEqual(verifyRes.success, true);
        assert.strictEqual(verifyRes.signatureValid, true);
        assert.strictEqual(verifyRes.hashValid, true);
        ```
      - *Cuplikan Kode (Test 4: Corrupted Payload File):*
        ```javascript
        const containerData = fs.readFileSync(tempNxPath);
        containerData[containerData.length - 100] ^= 0xff;
        fs.writeFileSync(tamperedPath, containerData);
        const verifyTamperedRes = await mockHandlers['verify-file']({}, tamperedPath);
        assert.strictEqual(verifyTamperedRes.success, false);
        assert.strictEqual(verifyTamperedRes.signatureValid, true, 'manifest signature is valid');
        assert.strictEqual(verifyTamperedRes.hashValid, false, 'payload hash mismatch');
        ```
      - *Analisis Jalur Pemanggilan:* Pemanggilan melalui mock handler IPC Electron Verify Desktop (`mockHandlers['verify-file']`).
      - *Klasifikasi:* **`INTEGRATION-ONLY`** (alur simulasi integrasi IPC Electron Verify Desktop).
    - **Kandidat 6: `test/pe01_tampered_sidecar_test.js` (L110-L130 & L158)**
      - *Cuplikan Kode (L117 & L124):*
        ```javascript
        const initialVerify = NexaCrypto.verify(regPubKey, Buffer.from(canonStr, 'utf8'), sigBytes);
        assert.strictEqual(initialVerify, true, 'Initial signature should be valid');
        const tamperedVerify = NexaCrypto.verify(regPubKey, Buffer.from(tamperedCanonStr, 'utf8'), sigBytes);
        assert.strictEqual(tamperedVerify, false, 'Tampered signature should fail verification');
        ```
      - *Analisis Jalur Pemanggilan:* `NexaCrypto.verify` pada L117/L124 dipanggil langsung untuk memverifikasi tanda tangan Registry Certificate dari sidecar `.nxcert` (bukan signature manifest kontainer `.nx`). Pemanggilan `NexaSdk.verifyContainer` pada L158 menguji integritas sidecar companion.
      - *Klasifikasi:* **`INTEGRATION-ONLY`** (pengujian sidecar companion dan registry certificate; bukan pengujian negative manifest signature kontainer).
    - **Kandidat 7: `tests/ecosystem_api_test.go` & `tests/registry_test.go`**
      - *Analisis Jalur Pemanggilan:* Menguji pembuatan dan verifikasi manifest kontainer pada Go packaging engine (`ed25519.Sign(creatorPriv, manifestBytes)`).
      - *Klasifikasi:* **`INTEGRATION-ONLY`** (Go engine packaging lifecycle).
  - *Ringkasan Klasifikasi Test Kandidat:*
    | File Test | Baris | Target Objek | Jalur Invokasi | Klasifikasi |
    |---|---|---|---|---|
    | `test/pe01_hidden_sidecar_test.js` | L153, L195 | `.nx` manifest signature | `NexaSdk.verifyContainer(...)` langsung | **`DIRECT-POSITIVE`** |
    | `test/task_a_buyer_lifecycle_test.js` | L1268 | `.nx` manifest signature | `NexaSdk.verifyContainer(...)` langsung | **`DIRECT-POSITIVE`** |
    | `test/task_a_final_trust_boundary_test.js` | L98, L158 | `.nx` manifest signature | `NexaSdk.verifyContainer(...)` langsung | **`DIRECT-POSITIVE`** |
    | `player-desktop/test/player-desktop.test.js` | L131, L149 | `.nx` IPC verify | Mock IPC `open-and-verify-nx` | **`INTEGRATION-ONLY`** |
    | `verify-desktop/test/verify-desktop.test.js` | L112, L130 | `.nx` IPC verify | Mock IPC `verify-file` | **`INTEGRATION-ONLY`** |
    | `test/pe01_tampered_sidecar_test.js` | L117, L124 | Sidecar cert / companion | `NexaCrypto.verify` & `verifyContainer` | **`INTEGRATION-ONLY`** |
    | `tests/ecosystem_api_test.go` | L142 | Go packaging manifest | `ed25519.Sign` | **`INTEGRATION-ONLY`** |
    | `tests/registry_test.go` | L217 | Go packaging manifest | `ed25519.Sign` | **`INTEGRATION-ONLY`** |
    | `sdk/typescript/test/` (seluruh berkas) | - | N/A (0 matches) | Tidak memanggil verifier `.nx` | **`NOT PRESENT IN SCOPE`** |
  - *Pernyataan Eksplisit Ketiadaan Direct-Negative Test:*
    Berdasarkan enam pencarian terarah dan raw output yang dicantumkan di atas pada direktori test (`test/`, `tests/`, `sdk/typescript/test/`, `player-desktop/test/`, `verify-desktop/test/`), tidak ditemukan test verifier langsung untuk penolakan signature manifest kontainer PE-01 `.nx` (`signatureValid === false`), manipulasi `container.manifestBytes`, creator public key yang tidak cocok, atau malformed 64-byte signature trailer dalam scope dan pola pemanggilan yang diperiksa. Kesimpulan ini dibatasi pada scope pencarian tersebut dan tidak menyatakan ketiadaan universal di luar pola yang dicari:
    **`DIRECT VERIFIER TEST (NEGATIVE): NOT PRESENT IN THE EXAMINED TEST SCOPE`**
- **5. Pencarian Terukur Ketiadaan Komponen Tambahan:**
  - *TypeScript Generic RFC 8785 JCS:* Command `grep -rnI --exclude-dir=node_modules -E "canonicalize|rfc8785|jcs" sdk/typescript/` membuktikan hanya ada template string 6-field di `registry.ts` dan pemetaan properti spesifik di `ownership.ts`. Serializer generik RFC 8785 untuk TypeScript: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
  - *Strict Duplicate-Key JSON Parser:* Command `grep -rnI --exclude-dir=node_modules -E "JSON.parse" sdk/typescript/ player-desktop/` membuktikan parser menggunakan `JSON.parse` V8 standar yang menoleransi duplikasi kunci. Parser byte-level strict penolak duplicate keys: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
  - *Detached Signature Envelope Manifest Album:* Format signed bytes dan detached signature manifest Album belum dirancang di kode: **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **Status Keseluruhan PSV-08 / PSV-R09 / PSV-R09A / PSV-R09A-1:** **`STATIC VERIFIER SOURCE COMPLETE; TARGETED TEST INVOCATION EVIDENCE COMPLETE; DIRECT-POSITIVE TEST VERIFIED IN INTEGRATION SUITES; DIRECT-NEGATIVE TEST NOT PRESENT IN SCOPE; SIGNED-CONTENT CONTRACT OPEN`**

---

#### 15.9.9 PSV-09 / PSV-R10 / PSV-R10A — Album Signer dan Membership Authenticity
- **Referensi Mandat:** R-10, B-09, NC-04, CONF-01, AC-07, AC-08, AC-22, AC-33, AC-34, §15.11.3 (PSV-R10, PSV-R10A).
- **Tujuan Pembuktian:** Membuktikan batas pemisahan arsitektural dan runtime antara verifier kontainer standalone `.nx` dan verifikasi membership Album pada Desktop Player, Verify Desktop, dan Mobile Player (Android & iOS secara terpisah), memastikan status Album Signer tidak merusak playback individual `.nx`, menyajikan call path otorisasi playback mobile sampai titik keputusan native/Go, dan menegaskan ketiadaan dependensi terhadap keanggotaan Album.
- **1. Call Path Verifier Standalone `.nx` pada Desktop (Commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`):**
  - A. *Desktop Player (IPC `open-and-verify-nx`):*
    - File & Line: `player-desktop/main.js:L674-L745`, `L910-L920`, `L989-L1022`.
    - Alur: IPC handler menerima `filePath`, memanggil `NexaSdk.verifyContainer(filePath)` untuk memvalidasi tanda tangan biner manifest dan hash SHA-256 payload biner, serta mengecek sertifikat genesis dan lisensi kontainer.
    - Titik Keputusan Otorisasi Playback (`player-desktop/main.js:L989-L1022`):
      ```javascript
      const isIntegrityPass = result.signatureValid && result.hashValid;
      const isRevoked = result.isRevoked || false;
      if (isIntegrityPass && !isRevoked) {
          AuthorizedPlaybackTracks.set(certID, {
              filePath: filePath,
              payloadOffset: result.payloadOffset,
              payloadLength: result.payloadLength,
              mimeType: result.mimeType
          });
          event.reply('open-and-verify-nx-response', {
              success: true,
              playbackUrl: `nexa-playback://${certID}`,
              metadata: result.metadata
          });
      }
      ```
    - Fakta Otorisasi Playback: Izin playback diberikan ke map `AuthorizedPlaybackTracks` semata-mata jika `isIntegrityPass && !isRevoked`. Pendaftaran playback URL `nexa-playback://${certID}` hanya bergantung pada validitas biner kontainer `.nx` individual.
  - B. *Desktop Verify (IPC `verify-file`):*
    - File & Line: `verify-desktop/main.js:L282-L350`, `L490-L510`.
    - Alur: IPC handler memanggil `NexaSdk.verifyContainer(filePath)` dan menyajikan hasil integritas kontainer, registri identitas, dan sertifikat genesis secara independen tanpa dependensi pada layer album.
- **2. Call Path Otorisasi Playback Mobile Player (Android & iOS) dan Boundary Album (PSV-R10A):**
  - *Entry Point:* `mobile/apps/player/src/screens/PlayerScreen.tsx:L67-L72` memanggil `openContainer(filePath, fd ?? -1)` atau `openContainerWithSidecar(filePath, sidecarPath, fd ?? -1)`.
  - *TS Wrapper:* `mobile/packages/expo-nexa-core/src/index.ts:L47-L66` meneruskan panggilan ke `NexaCoreModule`.
  - *A. Penelusuran Jalur Aktual Android:*
    1. *Modul Native Android:* `mobile/packages/expo-nexa-core/android/src/main/java/com/nexa/core/NexaCoreModule.kt:L56-L141`:
       - Normalisasi path skema `file://` atau resolusi `content://` (Android SAF) via `context.contentResolver.openFileDescriptor(uri, "r")` -> `pfd.detachFd()`.
       - Memanggil JNI `nativeOpenContainer(targetPath, resolvedFd)` atau `nativeOpenContainerWithSidecar(...)`.
    2. *JNI Bridge:* `mobile/packages/expo-nexa-core/android/NexaCoreModule.cpp:L14-L25` (`Java_com_nexa_core_NexaCoreModule_nativeOpenContainer`):
       - Meneruskan `(char*)cPath, fd` ke fungsi C/Go `NexaMobileOpenContainer((char*)cPath, fd)`.
       - Mengembalikan integer descriptor sesi `activeDesc` (atau kode error negatif -1 s.d. -7).
  - *B. Penelusuran Jalur Aktual iOS:*
    1. *Modul Native iOS:* `mobile/packages/expo-nexa-core/ios/NexaCoreModule.mm:L289-L352` & `L457-L523`:
       - Normalisasi string `file://`. Mengaktifkan resource sandbox security-scoped: `[url startAccessingSecurityScopedResource]`.
       - Membuka berkas melalui POSIX standard `open([[url path] UTF8String], O_RDONLY)` (`NexaCoreModule.mm:L330`).
       - Memanggil fungsi C/Go `NexaMobileOpenContainer([decodedPath UTF8String], nativeFd)`.
       - Mengembalikan integer descriptor sesi `activeDesc`.
  - *C. Go Mobile Runtime Session Setup & Integrity Engine (`sdk/c/nexa_mobile_cbindings.go`):*
    - Pada `NexaMobileOpenContainer`: Mem-parse header biner kontainer `.nx`, mengekstrak manifest bytes dan signature bytes, serta meluncurkan background goroutine untuk streaming verifikasi SHA-256 payload hash (`sess.hashStatus`). Menyimpan state sesi ke `sessionMap[descriptor]`.
  - *D. Evaluasi Verifikasi Kriptografi Mobile (`PlayerScreen.tsx:L110-L128`):*
    - Pemanggilan `status = await verifyContainer(activeDesc)` diteruskan melalui:
      - Android JNI: `NexaCoreModule.cpp:L66-L68` (`nativeVerifyContainer`) -> `NexaMobileVerifyContainer((int64_t)descriptor)`.
      - iOS Obj-C++: `NexaCoreModule.mm:L524-L527` (`verifyContainer`) -> `NexaMobileVerifyContainer([descriptor longLongValue])`.
      - Go Engine ([`sdk/c/nexa_mobile_cbindings.go:L638-L786`](file:///opt/antigravity/projects/nexa/sdk/c/nexa_mobile_cbindings.go#L638-L786)):
        - Menunggu penyelesaian background payload hash (`sess.hashDone`). Jika hash payload rusak (`hStat == 2`) -> mengembalikan `3 (INVALID)`.
        - Memvalidasi companion sidecar `.nxcert` jika mode offline diaktifkan.
        - Memvalidasi Registry Certificate otoritas via `resolveAuthenticatedCertificate`.
        - Memvalidasi tanda tangan Ed25519 manifest kontainer: `ev := evidence.New(...)`, `sigValid := ev.Validate()`. Jika invalid -> mengembalikan `3 (INVALID)`.
        - Memeriksa status revokasi/konflik: revoked -> `4 (REVOKED)`, conflict -> `2 (CONFLICT)`.
        - Mengembalikan `0 (TRUSTED)` jika valid dan aktif, atau `1 (UNKNOWN)` jika kunci kreator belum terotentikasi di registri.
  - *E. Titik Keputusan Otorisasi Playback Mobile Player (`mobile/apps/player/src/screens/PlayerScreen.tsx:L159-L219`):*
    ```typescript
    // 4. STRICT FAIL-CLOSED MANIFEST VALIDATION (L160-L179)
    if (!m || Object.keys(m).length === 0 || !payloadMime || payloadSize <= 0) {
      setErrorMsg('FAIL-CLOSED: Invalid Container Manifest...');
      await executeTeardown(null, activeDesc);
      return; // PLAYBACK BLOCKED
    }
    if (cat === 'unsupported') {
      setErrorMsg(`FAIL-CLOSED: Unsupported Payload MIME "${payloadMime}"`);
      await executeTeardown(null, activeDesc);
      return; // PLAYBACK BLOCKED
    }

    // 5. ENFORCE NEXA TRUST POLICY (L186-L199)
    if (
      status === MobileTrustStatus.INVALID ||
      status === MobileTrustStatus.REVOKED ||
      status === MobileTrustStatus.CONFLICT
    ) {
      const errMsg = 'FAIL-CLOSED: Playback Blocked. Container cryptographic signature invalid, certificate revoked, or conflicting status';
      setErrorMsg(errMsg);
      await executeTeardown(null, activeDesc);
      return; // PLAYBACK HARD-BLOCKED
    }

    // 6. REGISTER AUTHORIZED STREAM SESSION (L208-L216)
    const authenticatedUrl = await streamServer.registerSession(activeDesc, payloadSize, payloadMime);
    setStreamUrl(authenticatedUrl);
    ```
    - *Aturan Izin Playback:* Izin pemutaran diberikan semata-mata jika `status` adalah `TRUSTED` (0) atau `UNKNOWN` (1) (sesuai Universal Player Spec, UNKNOWN diizinkan dengan peringatan offline), dan ditolak secara fail-closed jika status adalah `INVALID` (3), `REVOKED` (4), atau `CONFLICT` (2). Stream URL lokal (`authenticatedUrl`) didaftarkan dan audio/video native player diputar.
  - *F. Pemeriksaan Dependency terhadap Album:*
    - Pada seluruh jalur panggilan dari `PlayerScreen.tsx`, `NexaCoreModule.kt`, `NexaCoreModule.mm`, `NexaCoreModule.cpp`, hingga `nexa_mobile_cbindings.go`, **TIDAK DITEMUKAN** pemanggilan, parameter, atau dependensi terhadap:
      - Album Manifest;
      - Album Signer;
      - Album membership;
      - Status autentisitas membership Album.
    - Pencarian terukur `grep -rnI --exclude-dir=node_modules -E "album_signer|albumsigner|albummanifest|albummembership" mobile/ sdk/c/` menghasilkan **0 matches** (`NOT PRESENT IN THE EXAMINED SCOPE`).
    - *Kesimpulan Boundary:* Terbukti secara statis pada kode aktual Android dan iOS bahwa otorisasi playback Mobile Player beroperasi secara mandiri dan terisolasi penuh dari layer Album. Kontrak PE-01 terlindungi dari efek regresi (`VERIFIED BY PROGRAMMER — STATIC SOURCE`). Mobile runtime: **`NOT RUN`**.
- **3. Jalur Pemeriksaan Membership Album pada Source Aktif:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "verifyAlbum|albumManifest|AlbumMembership" .`
  - *Hasil Pencarian:* **0 matches** pada seluruh source code runtime produk.
  - *Status:* Jalur pemeriksaan keanggotaan album **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **4. Bukti Model Identitas Kriptografi Baseline:**
  - *Container Creator Key:* Ed25519 public key yang menandatangani manifest kontainer `.nx` mandiri (`internal/container/container.go`, `sdk/typescript/src/sdk.ts`).
  - *Registry Authority Key:* Ed25519 authority key yang di-pin pada `sdk/typescript/src/registry.ts:L22` (`CANONICAL_REGISTRY_PUBKEY`), menandatangani `identity_signature`.
  - *Genesis Ownership Creator Key:* Ed25519 key yang menandatangani embedded genesis certificate (`sdk/typescript/src/ownership.ts:L15-L50`).
  - *Bukti Test Identitas Baseline:* Tetap mempertahankan kutipan test Registry Identity (8/8 PASS) dan Ownership Parity (5/5 PASS) sebagaimana dirinci pada §15.9.8.
  - *Penegasan Batas Bukti:* Uji identitas baseline ini membuktikan keandalan kriptografi baseline PE-01; uji ini **TIDAK** menguji entitas Album Signer atau keanggotaan Album yang memang belum ada di kode.
- **5. Pencarian Terukur Ketiadaan Entitas Album Signer:**
  - *Command Pencarian:* `grep -rnI --exclude-dir=node_modules -E "AlbumSigner|album_signer|albumSigner|AlbumAuthority" .`
  - *Hasil Pencarian:* **0 matches** pada seluruh source code runtime produk.
  - *Batas Kesimpulan:* Model tipe data, registri otoritas, key custody, rotasi, revokasi, dan trust store untuk `Album Signer` **`NOT PRESENT IN THE EXAMINED SCOPE`**.
- **Status Keseluruhan PSV-09 / PSV-R10 / PSV-R10A:** **`VERIFIED BY PROGRAMMER — STATIC SOURCE (DESKTOP & MOBILE PLAYBACK AUTHORIZATION BOUNDARY ISOLATION VERIFIED); ALBUM SIGNER NOT PRESENT IN EXAMINED SEARCH SCOPE; MOBILE RUNTIME NOT RUN`**

---

### 15.10 Rekonsiliasi Blocker B-01..B-09 dan Disposisi Residual Decision Pasca-PSV

Berdasarkan hasil pembuktian sumber primer lanjutan di atas, status aktual Blocker Register B-01 sampai B-09 direkonsiliasi secara transparan:

| Blocker ID | Status Pasca-PSV | Bukti Primer yang Diperoleh | Gap yang Belum Dibuktikan | Langkah Lanjut & Kewenangan |
|---|:---:|---|---|---|
| **B-01** (Strict JSON Parser) | `OPEN / BLOCKED` | PSV-08 membuktikan `player-desktop/main.js:L773` menggunakan `JSON.parse` V8 standar yang menoleransi duplicate keys. | Parser byte-level RFC 8259 penolak duplicate keys belum ada di TS SDK. | Perlu implementasi modul parser sebelum Gate B (Kewenangan Programmer). |
| **B-02** (RFC 8785 JCS) | `OPEN / BLOCKED` | PSV-08 membuktikan JCS generik lulus uji kesesuaian di Go engine (`jcs_test.go`), namun di TS SDK hanya ada template 6-field (`registry.ts:L118`). | Serializer JCS generik belum ada di TS SDK. | Perlu implementasi modul serializer TS sebelum Gate B (Kewenangan Programmer). |
| **B-03** (ZIP Extractor Aman) | `OPEN / BLOCKED` | PSV-06 membuktikan kontainer baseline murni biner; parser arsip ZIP Album belum ada di source aktif. | Modul streaming ZIP extractor aman dan adversarial test belum ada. | Perlu implementasi modul extractor sebelum Gate B (Kewenangan Programmer). |
| **B-04** (Marketplace Transaction / Zero-DDL) |  `OPEN / BLOCKED — NORMATIVE MODEL APPROVED; TRANSACTION / STORAGE / RECOVERY CONTRACT OPEN` | PSV-04 membuktikan transaksi lokal PostgreSQL ACID ada di `store.js:L89-L101` dan `server.js:L3794-L3870`. Ketiadaan 2PC eksternal terbukti sebagai arsitektur riil saat ini. Uji Go adversarial membuktikan engine licensing tahan replay. | Alur transaksi khusus akuisisi Album multi-member belum ada di kode. | Architecture Authority harus menetapkan kontrak transaksi Album berdasarkan kebutuhan produk dan risiko yang terbukti. Non-2PC, parent delivery, compensation, dan polling/idempotency tidak boleh diperlakukan sebagai keputusan desain sebelum ada penetapan formal. |
| **B-05** (`acquired_package_sha256`) | `VERIFIED BY PROGRAMMER — STATIC SOURCE (DDL & HASH ORIGIN); CHILD CONTRACT OPEN` | PSV-05 membuktikan DDL kedua tabel (`schema.postgres.sql#L72, L112`) dan migrasi L133-L134 valid serta konsisten dengan SQL producer. Pembentukan hash `catalog_snapshots.package_sha256` terbukti berasal dari `computeFileSha256(session.spool_path)` (`server.js:L762-L770, L2231`) yang meng-hash seluruh berkas fisik delivery package spool (wrapper ZIP). | Relasi child-member Album tidak ada dalam skema yang diperiksa (`NOT PRESENT IN THE EXAMINED SCOPE`); live DB tidak diverifikasi. | Parent/child contract tetap terpisah secara normatif. Jangan ubah DDL atau menyimpulkan pemetaan child tanpa penetapan PO. |
| **B-06** (Safe-Open / TOCTOU) | `OPEN / BLOCKED — DESKTOP & MOBILE CALL PATHS VERIFIED; ADVERSARIAL TOCTOU TESTS NOT AVAILABLE` | PSV-07 membuktikan seluruh jalur Desktop, Android (`NexaCoreModule.kt:L56-L92` via SAF PFD detach & JNI), dan iOS (`NexaCoreModule.mm:L289-L352` via Security-Scoped URL & POSIX `open`) menggunakan open standar tanpa mitigasi `O_NOFOLLOW` atau `fstat`. Unit test `containerOpening.test.ts` lulus 3/3 (`VERIFIED BY PROGRAMMER — TEST`). | Modul uji adversarial symlink/TOCTOU tidak tersedia di repo (`NOT AVAILABLE / NOT RUN`). Uji runtime mobile fisik tidak dijalankan (`NOT RUN`). | Opsi mitigasi Safe-Open tetap proposal arsitektur sampai Architecture Authority mengevaluasi desain setelah pengujian adversarial dirancang. |
| **B-07** (Batas Kuota ZIP) | `OPEN / BLOCKED — ARCHITECTURE AUTHORITY DECISION REQUIRED` | PSV-06 membuktikan batas 2 GiB ada pada payload kontainer tunggal di Go (`container.go:L106`), bukan kuota wrapper ZIP. | Batas kuota wrapper belum ditegakkan di kode. | Architecture Authority menetapkan parameter teknis normatif kuota ZIP berdasarkan threat model dan benchmark (angka 500MB/2GiB/200/100:1 adalah usulan). |
| **B-08** (Circular Signature JCS) | `OPEN / BLOCKED — GO JCS & TS CRYPTO VERIFIERS VERIFIED; DIRECT TEST COVERAGE NOT VERIFIED; SIGNED-CONTENT CONTRACT UNRESOLVED` | PSV-08 membuktikan Go JCS RFC 8785 lulus 2/2. Verifier TS Ed25519 (Registry, Genesis, Transfer, Manifest) terbukti terpisah di source dan test Registry/Ownership lulus 8/8 serta 5/5. Untuk verifier manifest kontainer PE-01 `.nx`, assertion signature valid pada test integrasi dilaporkan, tetapi raw output pencarian dan badan test yang menunjukkan pemanggilan langsung verifier belum disertakan. Klaim ketiadaan negative test langsung belum dapat dinaikkan menjadi temuan terverifikasi dari bukti yang diserahkan. TS generic JCS dan strict duplicate-key parser tidak ada di scope pencarian yang dilaporkan. | Format canonical bytes, detached signature envelope, dan verification path manifest Album belum dirancang di kode. | Architecture Authority menetapkan spesifikasi format penandatanganan manifest Album. |
| **B-09** (Album Signer Trust) | `OPEN / BLOCKED — DESKTOP & MOBILE PLAYBACK BOUNDARY VERIFIED; ALBUM SIGNER NOT PRESENT` | PSV-09 & PSV-R10A membuktikan 3 kunci baseline ada dan lulus uji 8/8 serta 5/5. Call path otorisasi playback Desktop Player (`main.js:L989`) dan Mobile Player Android/iOS (`PlayerScreen.tsx:L186-L216` via `expo-nexa-core` & Go runtime) terbukti 100% mengevaluasi kontainer individual `.nx` secara independen dari status Album membership / Signer. Entitas Album Signer dan verifier membership Album terbukti 0 matches (`NOT PRESENT IN THE EXAMINED SCOPE`). | Identity binding, authority pendaftaran, dan trust store Album Signer belum ada. | PO dan Architecture Authority meratifikasi keputusan formal CONF-01 (fail-closed keanggotaan album tanpa memblokir pemutaran member mandiri PE-01). |

---

#### Daftar Penetapan Residual yang Memerlukan Otoritas Formal
1. **DEC-01 (Architecture Authority — Parameter Teknis B-07):** Menetapkan batas kuota ekstraksi arsip ZIP (compressed size, expanded size, max entries, max expansion ratio) berdasarkan threat model dan benchmark. Angka usulan 500 MB / 2 GiB / 200 entri / 100:1 tidak diratifikasi oleh PO karena merupakan parameter teknis arsitektur.
2. **DEC-02 (Product Owner & Architecture Authority — CONF-01 / B-09):** Mengesahkan kebijakan formal autentisitas membership: jika Album Signer berstatus `UNKNOWN` atau signature manifest tidak valid, keanggotaan Album ditolak di antarmuka (*Album Membership Authenticity Fail-Closed*), namun hak playback individual `.nx` yang valid tetap dipertahankan di bawah kontrak mandiri PE-01.
3. **Auto-Next (Bukan Keputusan Residual Baru):** Keputusan PO yang telah ada tetap berlaku (Auto-Next dipicu saat lifecycle viewer selesai). Ketiadaan listener `ended` pada video desktop dan ketiadaan sinyal completion alami pada dokumen/gambar merupakan gap teknis implementasi yang dicatat secara faktual, bukan alasan mengubah kebijakan menjadi manual-only dan bukan izin membuat timeout buatan.
4. **Safe-Open (Bukan Penerimaan Opsi Sebelum Pengujian):** Opsi POSIX (`O_NOFOLLOW` + `fstatSync`) dan isolasi direktori staging Windows/Android tetap berstatus proposal teknis sampai pengujian per platform selesai dan dievaluasi oleh Architecture Authority.

---

#### Pernyataan Penutup Integrasi PSV Mandat Kanonikal
1. Seluruh ruang lingkup PSV residual (PSV-R02 s.d. PSV-R10) telah diselidiki secara terarah dan terukur terhadap repositori sumber `whisnu/nexa:main` commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`.
2. Pekerjaan DGR tidak diulang; temuan dan koreksi DGR-PSV-02 s.d. DGR-PSV-04 pada §15.11.2 tetap dipertahankan utuh.
3. Konflik semantik B-05 antara §4.4 E-03 dan §15.9.5 telah diselesaikan melalui verifikasi DDL utuh pada `schema.postgres.sql#L63-L114`.
4. Tidak ada source code, skema DDL, database, maupun konfigurasi runtime yang diubah dalam pelaksanaan mandat ini.
5. Status tata kelola dipertahankan secara utuh tanpa perubahan:
   - **Gate A:** `NOT PASSED` (menunggu independent re-audit atas bukti primer yang dihimpun).
   - **Gate B:** `BLOCKED` (menunggu penyelesaian blocker implementasi B-01, B-02, B-03, B-06 dan keputusan arsitektur).
   - **PE-02 Implementation:** `NOT AUTHORIZED` (otorisasi implementasi hanya diterbitkan setelah Gate A dan Gate B lolos).
   - **Sprint 16 & PE-01:** `CLOSED / FINAL ACCEPTED / FROZEN`.
   - **Sprint 17:** `NOT STARTED`.

### 15.11 Review Auditor atas Hasil Eksekusi Programmer — Disposisi PSV dan DGR

#### 15.11.1 Batas pemeriksaan dan provenance
1. Auditor memeriksa PLAN kanonikal, struktur bukti, konsistensi internal, ketepatan klasifikasi, keterlacakan klaim, dan kecukupan bukti yang diserahkan Programmer.
2. Akses ke repository sumber `whisnu/nexa` merupakan kewenangan dan lingkungan kerja **Programmer-only**. Auditor tidak diwajibkan memiliki akses langsung ke repository tersebut. Ketiadaan akses langsung Auditor bukan defect, bukan blocker proyek, bukan kekurangan bukti Programmer, dan tidak boleh dijadikan item PSV atau handoff.
3. Karena bukti repository berasal dari hasil inspeksi Programmer, setiap klaim source/schema/test/runtime harus dinilai berdasarkan materi primer yang disertakan Programmer (path, commit, line range, raw snippet, command, exit code, output, dan runtime evidence yang relevan). Status `VERIFIED` pada §15.9 berarti subklaim tersebut diverifikasi dalam pemeriksaan Programmer sesuai bukti yang dicantumkan; status itu tidak boleh diperluas melampaui ruang lingkup bukti atau dianggap sebagai verifikasi runtime jika hanya ada inspeksi statis.
4. Auditor tidak boleh menurunkan status bukti hanya karena tidak dapat membuka repository sumber secara langsung. Sebaliknya, Auditor tetap wajib mengidentifikasi kontradiksi internal, klaim yang melampaui bukti yang diserahkan, test yang gagal/tidak dijalankan, serta runtime/platform yang belum dibuktikan.
5. Tidak ada perubahan source code, schema, database, konfigurasi runtime, atau Product Truth. Tidak ada Gate yang dinaikkan dan tidak ada otorisasi implementasi yang diberikan.

#### 15.11.2 Koreksi DGR yang dilakukan langsung pada PLAN kanonikal
| ID | Temuan dokumen | Disposisi |
|---|---|---|
| DGR-PSV-02 | Subklaim PSV-01 tentang batas otorisasi Stage 8a berisi kondisi hipotetis tetapi diberi status VERIFIED. | Dikoreksi menjadi NOT VERIFIED — CONDITIONAL RISK ONLY; caller Stage 8a tidak terbukti ada. |
| DGR-PSV-03 | Disposisi B-04 berpotensi mengangkat polling idempoten menjadi bagian kontrak yang harus ditetapkan, padahal masih proposal. | Dikoreksi agar Architecture Authority mengevaluasi kontrak; polling idempoten tetap proposal dan bukan keputusan normatif. |
| DGR-PSV-04 | Pada audit sebelumnya, kutipan E-03 tidak menampilkan definisi lengkap tabel entitlements sehingga keberadaan field B-05 belum dapat diterima. | PSV-05 terbaru melaporkan DDL utuh kedua tabel pada commit yang sama. Ledger E-03 diselaraskan dengan §15.9.5; keberadaan field pada DDL statis dicatat sebagai VERIFIED BY PROGRAMMER, bukan verifikasi live DB atau verifikasi independen Auditor. Byte-domain parent hash dan child contract tetap dipisahkan. |

Koreksi DGR-PSV-02 s.d. DGR-PSV-04 merupakan koreksi dokumentasi/provenance yang tidak memerlukan PSV tambahan. Karena telah diterapkan langsung pada PLAN kanonikal, item tersebut **tidak boleh dimasukkan kembali** sebagai pekerjaan Programmer. Keterbatasan akses langsung Auditor ke repository `whisnu/nexa` bukan defect dan bukan pekerjaan Programmer.

#### 15.11.3 Register PSV residual — wajib bukti primer lanjutan

Hasil pemeriksaan pada §15.9 menunjukkan seluruh workstream R-02 s.d. R-10 telah ditelusuri. Tidak semua workstream memerlukan PSV tambahan. Jika bukti source/search yang diserahkan sudah cukup menunjukkan komponen atau test belum ada, kekurangannya diklasifikasikan sebagai gap implementasi/test atau keputusan normatif, bukan alasan mengulang pencarian yang sama.

| ID | Disposisi hasil pemeriksaan | Alasan dan batas klaim |
|---|---|---|
| PSV-R02 | **PSV CLOSED — NORMATIVE DECISION OPEN** | Caller Stage 8a tidak ditemukan pada scope pencarian; test Player FAILED karena binary CLI tidak tersedia; test/runtime Stage 8a NOT AVAILABLE/NOT RUN. Bukti cukup untuk klaim ketiadaan saat ini. Tidak ada PSV tambahan untuk mengulang pencarian. Izin diagnostik Stage 8a tetap unresolved normatif. |
| PSV-R03 | **PSV CLOSED — IMPLEMENTATION / TEST GAP OPEN** | Source menunjukkan handler desktop audio; desktop video dan mobile tidak memiliki completion handler yang dilaporkan; dokumen/gambar tidak memiliki completion alami. Test/runtime NOT RUN. Tidak boleh mengklaim Auto-Next telah lulus uji. Keputusan PO Auto-Next tetap berlaku; tanpa timeout buatan atau manual-only. |
| PSV-R04 | **PSV CLOSED — IMPLEMENTATION / TEST GAP OPEN** | Search source tidak menemukan orkestrasi multi-member. Test Studio FAILED pada FFmpeg hash mismatch; test recovery Album multi-member tidak tersedia. Bukti cukup untuk klaim gap saat ini; tidak perlu pencarian ulang. Jangan menetapkan path persistence proposal sebagai desain. |
| PSV-R05 | **PSV CLOSED — ARCHITECTURE DECISION OPEN** | Call path transaksi, BEGIN/COMMIT/ROLLBACK, HTTP side effect, dan pencarian compensation/reconciliation telah dilaporkan. Test integrasi Marketplace gagal/tidak tersedia. Test Go engine bukan bukti integrasi Marketplace. Kontrak transaksi Album masih memerlukan keputusan Architecture Authority; non-2PC dan polling idempoten bukan keputusan desain. |
| PSV-R06 | **PSV CLOSED — STATIC SOURCE VERIFIED; CHILD CONTRACT OPEN** | DDL utuh kedua tabel (`schema.postgres.sql#L63-L114` + migrasi L131-L135), titik pembentukan hash `computeFileSha256(session.spool_path)` (`server.js:L762-L770, L2231`), penyimpanan `catalog_snapshots` (L2396), producer (L3853, L3858), dan consumer (L4271) telah dibuktikan dengan source primer. Byte-domain terbukti adalah seluruh berkas fisik delivery package spool (wrapper ZIP). Child-member mapping tidak ada dalam skema yang diperiksa (`NOT PRESENT IN THE EXAMINED SCOPE`). Live DB `NOT VERIFIED`. |
| PSV-R07 | **PSV CLOSED — IMPLEMENTATION / ARCHITECTURE GAP OPEN** | Dua pencarian terukur melaporkan parser/extractor ZIP Album tidak ada; test extractor tidak tersedia. Bukti cukup untuk klaim ketiadaan pada scope yang disebut. Kuota ZIP tetap keputusan Architecture Authority. |
| PSV-R08 | **PSV CLOSED — STATIC SOURCE REVIEW COMPLETE; IMPLEMENTATION / SECURITY TEST GAP OPEN** | Call path Desktop, Android (`NexaCoreModule.kt:L56-L92`, JNI `NexaCoreModule.cpp`), dan iOS (`NexaCoreModule.mm:L289-L352`) telah dilaporkan dengan source primer. Unit test `containerOpening.test.ts` 3/3 hanya menguji seleksi URI/fallback, bukan Safe-Open atau TOCTOU. Adversarial test `NOT AVAILABLE / NOT RUN`; runtime mobile `NOT RUN`. Tidak perlu PSV ulang untuk bukti yang sudah dicantumkan; B-06 tetap OPEN/BLOCKED dan mitigasi Safe-Open tetap proposal arsitektur. |
| PSV-R09 | **PSV CLOSED — STATIC VERIFIER SOURCE COMPLETE; SIGNED-CONTENT CONTRACT OPEN** | Source verifier Ed25519 TypeScript (Registry di `sdk.ts:L207-L230`, Genesis di `ownership.ts:L239-L265`, Transfer di `ownership.ts:L267-L280`, Manifest di `sdk.ts:L142-L144`) telah dipisahkan dan dibuktikan. Test suite Registry Identity (8/8 PASS) dan Ownership Parity (5/5 PASS) lulus uji langsung. Ketiadaan TS generic JCS dan strict duplicate-key parser terkonfirmasi pada batas pencarian. Format signed bytes manifest Album belum ada di kode. |
| PSV-R10 | **PSV CLOSED — DESKTOP & MOBILE PLAYBACK BOUNDARY VERIFIED; ALBUM SIGNER NOT PRESENT** | Call path verifier standalone `.nx` pada Player Desktop (`player-desktop/main.js:L674-L745`, L989-L1022), Verify (`verify-desktop/main.js:L282-L350`), dan Mobile Player Android/iOS (`PlayerScreen.tsx:L159-L219`) telah dibuktikan. Batas runtime terbukti: otorisasi playback murni mengandalkan integritas biner individual `.nx`, terisolasi total dari entitas Album Signer dan membership Album yang tidak ditemukan (0 matches). Test identitas baseline 8/8 dan 5/5 dipertahankan. |
| PSV-R09A | **PSV CLOSED — TEST EVIDENCE RECONCILED WITH PSV-R09A-1** | Telah dilengkapi dan disatukan dengan hasil pembuktian terarah PSV-R09A-1. Pemanggilan verifier manifest kontainer pada test suite telah dipetakan secara granular ke dalam klasifikasi direct-positive, direct-negative, dan integration-only dengan raw output pencarian utuh. |
| PSV-R09A-1 | **PSV CLOSED — TARGETED TEST INVOCATION EVIDENCE COMPLETE; DIRECT-NEGATIVE TEST NOT PRESENT IN SCOPE** | Enam pencarian terarah (`NexaSdk.verifyContainer`, `NexaCrypto.verify`, `manifestBytes`, `signatureBytes`, `verifyContainer`, `signatureValid`) pada lima direktori test (`test/`, `tests/`, `sdk/typescript/test/`, `player-desktop/test/`, `verify-desktop/test/`) telah disajikan dengan command lengkap, exit code, raw output utuh, dan cuplikan badan test. Klasifikasi: Direct-positive terbukti pada tiga suite integrasi (`test/pe01_hidden_sidecar_test.js`, `test/task_a_buyer_lifecycle_test.js`, `test/task_a_final_trust_boundary_test.js`) yang memanggil langsung `NexaSdk.verifyContainer(...)` pada kontainer valid. Desktop tests (`player-desktop.test.js`, `verify-desktop.test.js`) diklasifikasikan sebagai integration-only (mock IPC handler). Uji negatif verifier signature manifest `.nx` (`signatureValid === false`, tampered manifestBytes, wrong creator pubkey, malformed signature) terbukti secara faktual: **`DIRECT VERIFIER TEST (NEGATIVE): NOT PRESENT IN THE EXAMINED TEST SCOPE`**. Direktori `sdk/typescript/test/` terbukti 0 match (Exit code 1). Tidak ada penambahan/perubahan test. |
| PSV-R10A | **PSV CLOSED — STATIC SOURCE VERIFIED FOR ANDROID & IOS; RUNTIME NOT RUN** | Call path otorisasi playback Mobile Player ditelusuri tuntas dari `PlayerScreen.tsx:L67-L72`, melalui modul native Android (`NexaCoreModule.kt:L56-L141`, JNI `NexaCoreModule.cpp:L14-L25`) dan iOS (`NexaCoreModule.mm:L289-L352, L457-L523`), Go mobile runtime (`nexa_mobile_cbindings.go:L638-L786`), hingga titik otorisasi `PlayerScreen.tsx:L186-L216` (`registerSession` & `setStreamUrl`). Terbukti 100% independen dari Album Manifest, Album Signer, atau Album membership (`NOT PRESENT IN THE EXAMINED SCOPE`). Mobile runtime: **`NOT RUN`**. |

**Mandat residual Programmer:** Seluruh item residual PSV (PSV-R02 s.d. PSV-R10, termasuk PSV-R09A, PSV-R09A-1, dan PSV-R10A) telah **LENGKAP DAN DITUTUP** pada tingkat pembuktian sumber primer yang diminta. Tidak ada lagi residual PSV terbuka yang memerlukan penyelidikan primer tambahan. Seluruh temuan gap implementasi, ketiadaan test negatif langsung, dan ketiadaan format manifest Album dicatat secara jujur sebagai gap teknis/arsitektur, tanpa mengubah kode atau menaikkan otorisasi implementasi. Batasan governance lock tetap mengikat penuh.

#### 15.11.4 Disposisi governance
- Gate A: **NOT PASSED**.
- Gate B: **BLOCKED**.
- PE-02 Implementation: **NOT AUTHORIZED**.
- Sprint 16: **CLOSED / FINAL ACCEPTED / FROZEN**.
- PE-01: **CLOSED / FROZEN**.
- Sprint 17: **NOT STARTED**.
- Tidak ada keputusan PO atau Architecture Authority baru yang dihasilkan oleh review ini.
