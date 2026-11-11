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
>   - **B-04 / NC-08 / CONF-03:** **`AA CONTRACT SPECIFIED; SOURCE-BACKED ZERO-DDL STORAGE FEASIBILITY REMAINS OPEN`** (Model B, Immutable Checkout Manifest SSOT, durable per-member execution receipt, idempotency, reconciliation, dan recovery contract telah ditetapkan AA; existing storage dan mapping source harus dibuktikan).
>   - **B-05 / NC-09:** **`CHILD .NX BYTE-DOMAIN SPECIFIED BY AA; EXISTING FIELD MAPPING / ZERO-DDL STORAGE PROOF PENDING`**.
>   - **B-06 / NC-12:** **`SAFE-OPEN / TOCTOU DESIGN SPECIFIED BY AA; PLATFORM TEST EXECUTION POST-AUTHORIZATION`**.
>   - **B-07 / NC-07:** **`AA BENCHMARK PROTOCOL SPECIFIED; NUMERIC RESOURCE LIMITS BLOCKED PENDING MEASURED CAPACITY EVIDENCE; PSV-R07 CLOSED`** (empat kelas payload, workload, metrik, boundary tests, dan format evidence ditetapkan pada §16.7 dan §16.14; tidak ada angka universal yang diasumsikan).
>   - **B-08 / NC-02:** **`SIGNATURE-STRIPPED JCS / SIGNED FIELD SET / ENVELOPE / VERIFIER CONTRACT SPECIFIED BY AA; IMPLEMENTATION AND TESTS POST-AUTHORIZATION`**.
>   - **B-09 / NC-04 / CONF-01:** **`PER-ALBUM MEMBERSHIP AUTHORITY APPROVED BY PO; AA CONTRACT SPECIFIED; IMPLEMENTATION GAP CONFIRMED BY PROGRAMMER EVIDENCE REPORT`** (Tier-1 explicit Album-wide Authority Designation binds exact `album_id` to `authority_subject_id` and must be proven through existing Identity and ownership/rights foundations; PO-approved Opsi A embeds the complete signed Album Genesis Origin Declaration inside the Manifest for offline self-contained verification, while online Registry/Federated status remains reconcilable under Dual-Horizon rules. Tier-2 complete signed Authority Evidence Carrier is also embedded in the Manifest and delegates only `ALBUM_MEMBERSHIP_SIGNING` to a separate Album Signer; Tier-3 Album Signer signs the complete canonical Manifest including both evidence objects. No member-ownership inference, global authority, new trust root, self-assertion, or `CONTAINER_PACKAGING` fallback. WP-04/WP-05 implementation and tests remain post-authorization.)
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
> 7. **Kualifikasi ruang lingkup rujukan White Paper/Roadmap untuk PE-02:** White Paper v5.6 dan Roadmap v4.8 tidak memuat spesifikasi Album ZIP, Album Manifest, Album Signer, atau lifecycle signer Album. Namun, fondasi Identity, Organization Identity, Registry evidence, dan Federated Trust yang memang didefinisikan Nexa dapat dipakai sebagai building blocks arsitektur B-09. Pemakaian tersebut **tidak** berarti White Paper/Roadmap telah menetapkan kontrak Album Signer; kontrak Album-spesifik tetap harus dirumuskan di PLAN ini, tidak boleh memperluas kewenangan Creator/Genesis/Registry/ownership/licensing secara otomatis, dan tidak boleh membentuk trust root baru. Roadmap v4.8 mencatat PE-02 sebagai NOT READY — BLOCKED (V5-REV1), Product Enhancement Window OPEN / NOT FROZEN, dan implementasi NOT AUTHORIZED; status itu tidak dapat dinaikkan oleh isi plan ini. Setiap ketentuan Album-spesifik harus ditandai secara eksplisit sebagai (a) keputusan PO PE-02 yang benar-benar telah disahkan, (b) proposal teknis, atau (c) unresolved/blocked. Kutipan White Paper/Roadmap yang hanya mendukung perilaku member .nx tidak boleh ditulis seolah-olah sumber tersebut mengesahkan desain Album.

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
| **AUDIT-NEW-01** | §1.5.1, §5.1, §5.2, §5.3, §8 | Historical finding: pada saat audit awal, izin background Stage 8a dan dependency diagnostik 7b/7c belum diputuskan. Keputusan PO 2026-11-10 kemudian menutup izin produk tersebut; sisa teknis adalah identitas/path payload hash dan sinkronisasi register. | Menyelaraskan urutan dependensi JIT di seluruh dokumen (§1.5.1, §5.1, §5.2, §5.3); menyusun Matriks Dependensi Silang JIT Album (§3.4) yang memisahkan Stage 8a, 8b, dan 8c; memperketat batas Stage 8a: deskriptor aman (Tahap 6) dan keutuhan PE-01 (Tahap 7a) adalah prasyarat I/O fisik minimum, namun dilarang menyatakan Stage 8a secara kategoris hanya memerlukan 6 dan 7a; status ketergantungan normatif Stage 8a terhadap validasi Genesis (7b) dan lisensi aktif (7c) dinyatakan jujur berstatus UNRESOLVED — GENESIS VALIDATION & ACTIVE LICENSE DEPENDENCY FOR DIAGNOSTIC DIGEST NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required), di mana kemampuan teknis mengekstrak bitstream mentah dilarang disamakan dengan izin produk untuk melanjutkan pemeriksaan; status izin diagnostik Background Pre-Verification Stage 8a dinyatakan jujur berstatus UNRESOLVED — BACKGROUND PRE-VERIFICATION PERMISSION NOT ESTABLISHED BY NORMATIVE CONTRACT (PO / Architecture Decision Required) dengan memisahkan tegas kemampuan teknis komputasi, izin diagnostik produk, dan otorisasi pemutaran; merekonsiliasi divergensi identitas field hash audio antara skema manifest §5.1 (`audio_sha256`) dan Stage 8a / §6.9 / AC-09 (notasi konseptual draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256` (bukan path manifest normatif) / `sha256`) sebagai UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT tanpa asumsi alias, ekuivalensi, fallback tersembunyi, atau aturan prioritas sepihak; status kesiapan pengujian AC-09 diselaraskan menjadi TEST-PLANNED — BLOCKED BY UNRESOLVED NORMATIVE FIELD IDENTITY; menegaskan hasil digest 8a valid TIDAK PERNAH memberikan hak dekripsi atau playback; menegaskan Tahap 8b secara kumulatif mensyaratkan lolos digest 8a, validasi Genesis 7b, DAN lisensi aktif sah 7c; menegaskan aturan dependensi Stage 8b menuju Stage 8c di mana Stage 8c hanya boleh dijalankan setelah Stage 8b berhasil dan kegagalan 8b menghentikan alur fail-closed sebelum 8c; menegaskan Tahap 8c eksklusif untuk current member dan dilarang via pre-verifikasi antrean; menegaskan kebijakan dekripsi diagnostik yang belum memiliki kontrak normatif tetap UNRESOLVED — NORMATIVE CONTRACT NOT VERIFIED. | Mandat PO AUDIT-NEW-01; White Paper v5.6 §Distribution; internal/container/container.go; sdk.ts | `PARTIAL (CROSS-STAGE DEPENDENCY MATRIX SPECIFIED; GENESIS, LICENSE, FIELD IDENTITY & PRE-VERIFICATION PERMISSION UNRESOLVED PENDING PO CLARIFICATION)` | Matriks dependensi silang terpasang lengkap (§5.2); pemisahan gerbang otorisasi kumulatif 8b dan isolasi buffer 8c mutlak bebas celah; ketidakpastian normatif dependensi digest diagnostik, izin pre-verifikasi, dan identitas field manifest dicatat transparan tanpa asumsi sepihak. |
| **AUDIT-NEW-02** | §5.1, §8 (AC-01) | Contoh manifest menggunakan nilai dummy/ilustratif namun diklaim membuktikan seluruh Tier 3 invariants. | Pisahkan tegas 5 layer validasi (JSON syntax, Schema structure, Semantic, Cryptographic, Package/member). Beri label tegas contoh manifest murni struktural, nilai dummy tidak membuktikan kriptografi. | Mandat PO AUDIT-NEW-02; RFC 8259 | `PASS (PRESERVED)` | Tidak ada klaim pemenuhan kriptografis semu dari data dummy; kewajiban verifikasi Tier 3 tetap utuh. |
| **AUDIT-NEW-03** | §4.4 (E-07), §6.12 | Bukti E-07 hanya memuat `O_NOFOLLOW`, `fstatSync`, dan `isFile()`, namun diklaim membuktikan `lstatSync` dan perbandingan `dev`/`ino`. | Batasi klaim E-07 pada kode riil yang ada; nyatakan verifikasi ganda `lstatSync` dan `dev`/`ino` sebagai celah implementasi kode desktop (`NOT DEMONSTRATED BY E-07 / RESIDUAL GAP`); pertahankan B-06 terblokir. | `fs_safe.ts#L30-L55`; Mandat PO AUDIT-NEW-03 | `PASS (PRESERVED)` | B-06 tetap `OPEN / BLOCKED` pending pengujian unit anomali dan risk acceptance formal PO/Security Architect. |
| **AUDIT-NEW-04** | §1.5.1, §1.6 (A-24), §2.2, §5.1, §6 (NC-09), §6.9, §8 (AC-16), §9 (NC-09) | Klaim kaku delapan objek kriptografi/hash pada dokumen lama; klaim semantik acquired_package_sha256 melampaui bukti DDL; klasifikasi 'dua hash normatif terverifikasi' terlalu kuat; hubungan signature dan creator_signature belum dibuktikan dengan bukti primer kode yang dapat diakses auditor. | Rekonsiliasi total inventaris berbasis bukti (§6.9): memisahkan 4 objek signature Ed25519 diskrit dan 2 field hash SHA-256; mencatat bahwa pemetaan Go trailer signature (internal/container/container.go#L17-L135) dan TS SDK signatureBytes (sdk/typescript/src/container.ts#L4-L104) serta Genesis creator_signature (sdk/typescript/src/ownership.ts#L26) dilaporkan berdasarkan kode lokal whisnu/nexa commit fc08a5c, namun karena akses repositori sumber belum dapat diverifikasi secara independen oleh Auditor (HTTP 404), status bukti primer implementasi diturunkan jujur menjadi NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE; memisahkan inventaris hash menjadi tracks[] [notasi draf audio non-normatif; bukan path manifest universal].<unresolved_audio_hash_field> (PROPOSED SPECIFICATION; identitas field normatif audio_sha256 vs tracks[] [notasi draf audio non-normatif; bukan path manifest universal].sha256 berstatus UNRESOLVED — STOP AND CLARIFY) dan acquired_package_sha256 (Tingkat 1 DDL field existence berstatus NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE karena akses file DDL marketplace/db/schema.postgres.sql belum dapat diverifikasi independen oleh Auditor; Tingkat 2 & 3 semantik penulisan child row, payload, producer, dan consumer tetap UNRESOLVED — BLOCKED BY B-05); membedakan 3 entitas komputasional in-memory perancang; mengonfirmasi secara konseptual underlying_cert_id sebagai certificate identifier reference (bukan audio hash); mempertahankan B-08 model Signature-Stripped JCS telah diputuskan; exact signed-content/verifier contract masih unresolved. | §6.9; Mandat PO AUDIT-NEW-04; internal/container/container.go; sdk/typescript/src/container.ts; sdk.ts; marketplace/db/schema.postgres.sql; RFC 8785; RFC 8032 | `NOT PASS — RECONCILED EVIDENCE-BASED INVENTORY (PRIMARY SOURCE EVIDENCE NOT AVAILABLE FOR INDEPENDENT AUDIT; SEMANTICS BLOCKED BY B-05; SIRKULARITAS SIGNATURE BLOCKED BY B-08)` | Inventarisasi faktual membedakan keberadaan field dari semantik; klaim bukti implementasi Go/SDK/DDL diturunkan jujur menjadi NOT VERIFIED karena keterbatasan akses repositori independen Auditor; status NOT PASS dipertahankan jujur selama bukti independen belum tersedia dan B-05 serta B-08 belum disahkan PO/Arsitektur. |
| **AUDIT-NEW-05** | §4.4 (E-03), §8 (AC-17), §13 | AC-17 mengklaim ketiadaan mutasi runtime DB aktif, padahal E-03 murni inspeksi statis berkas DDL `schema.postgres.sql`. | Batasi klaim AC-17 murni pada kepatuhan statis berkas skema DDL di repositori; tegaskan status live/runtime database sebagai `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. | `schema.postgres.sql`; Mandat PO AUDIT-NEW-05 | `PASS (PRESERVED)` | Zero-DDL pada berkas statis terbukti 100%; runtime live DB berstatus jujur `NOT VERIFIED`. |
| **AUDIT-NEW-06** | §5.1, §5.2, §6.7, §6.15, §7.1 (REQ-B03-03/07), §8 (AC-02), §10.3, §13.1 | Sisa kontradiksi penolakan direktori pada draf §5.1, NC-07 §6, dan A-08 §1.6 belum dibersihkan terhadap keputusan PO. | Menghilangkan seluruh sisa ketentuan penolakan direktori di §5.1, NC-07 §6, A-08 §1.6, §13.1, dan seluruh dokumen; menegaskan keputusan PO: regular files & directory entries diterima; symlinks & special files (FIFO, socket, dev) ditolak fail-closed ERR_ZIP_INVALID; semantik hardlink tidak didukung; berkas byte identik independen; hapus asumsi pengujian tipe hardlink generik universal di REQ-B03-03; harmonisasi flat archive ditegaskan hanya mengatur path relatif member .nx manifest (regex ^[a-zA-Z0-9_-]+\.nx$), bukan pelarangan entri direktori ZIP; menandai usulan lama sebagai catatan historis yang telah digantikan. | Keputusan PO: APPROVED (AUDIT-NEW-06) | `PASS (TARGETED CORRECTION APPLIED — SELURUH KONTRADIKSI DIREKTORI TUNTAS DIELIMINASI)` | Seluruh dokumen konsisten 100% dengan keputusan PO: direktori diterima; sisa kontradiksi §5.1 baris 540, NC-07 baris 816, dan A-08 baris 151 tuntas diselaraskan; tidak ada klaim deteksi hardlink generik. |
| **AUDIT-NEW-07** | §5.1, §6.7, §7.1 (REQ-B03-01), §8 (AC-01..02), §10.3 | Aturan keunikan nama berkas case-sensitive berisiko tabrakan pada filesystem case-insensitive (e.g. `TrackA.nx` vs `tracka.nx`). | Memasukkan aturan PO APPROVED: pertahankan nama asli; periksa keunikan case-insensitive via ASCII case folding; nama bentrok ditolak fail-closed; cantumkan tabel boundary matrix wajib; berlaku lintas platform POSIX/Windows/Android. | Keputusan PO: APPROVED (AUDIT-NEW-07) | `PASS (PRESERVED)` | Boundary matrix terpasang lengkap di §5.1 dan §6.7; penolakan fail-closed deterministik. |
| **AUDIT-NEW-08** | §5.1, §5.2 (Tahap 5), §6.7, §6.15, §8 (AC-02, AC-13) | Konflik pemetaan antara anomali deklarasi manifest, anomali fisik ZIP, dan ketidakcocokan bijeksi 1:1; inkonsistensi error nama file manifest vs fisik ZIP. | Merekonsiliasi pemetaan layer secara deterministik bebas kontradiksi (FINDING-04): (1) Anomali deklarasi/regex nama file pada manifest dipetakan ke ERR_MANIFEST_MALFORMED pada Manifest Validator (Tahap 3); (2) Anomali fisik arsip ZIP (rusak, symlink, special file, path traversal fisik, benturan case-insensitive antar-entri ZIP) dipetakan ke ERR_ZIP_INVALID pada ZIP Reader (Tahap 2); (3) Ketidakcocokan bijeksi 1:1 antara manifest dan ZIP (berkas manifest hilang di ZIP atau berkas reguler ekstra di ZIP) dipetakan ke ERR_ZIP_ENTRY_MISMATCH pada Packaging Validator (Tahap 5). Sinkronkan §5.1, §5.2 Tahap 5, tabel taksonomi §6.15, matriks deterministik, dan AC-02/AC-13. | §6.15; Mandat PO AUDIT-NEW-08; FINDING-04 | `PASS (TARGETED CORRECTION APPLIED — LAYER SEPARATION HARMONIZED)` | Pemisahan 3 layer deterministik bebas kontradiksi: kesalahan deklarasi manifest = ERR_MANIFEST_MALFORMED, anomali fisik ZIP = ERR_ZIP_INVALID, dan ketidakcocokan bijeksi = ERR_ZIP_ENTRY_MISMATCH. |
| **AUDIT-NEW-09** | §1.2, §3.1, §10.3 | Hierarki sumber otoritas pada §1.2 menggabungkan PO dan Arsitektur, menempatkan repository sebagai pengubah kontrak, dan belum memuat urutan keputusan PO yang tepat. | Mengganti hierarki otoritas lama dengan urutan persis 6 tingkat yang telah disahkan PO: Level 1 Keputusan PO PE-02, Level 2 Kontrak Produk & Governance Beku, Level 3 White Paper & Roadmap, Level 4 Repository Aktual sebagai Bukti Implementasi, Level 5 Standar Internasional, Level 6 Temuan Audit / Proposal / Interpretasi di §1.2, §3.1, dan §10.3. | Keputusan PO: APPROVED (AUDIT-NEW-09) | `PASS (TARGETED CORRECTION APPLIED)` | Hierarki otoritas kanonikal 6 tingkat terpasang persis sesuai keputusan PO tanpa interpretasi bercabang. |
| **AUDIT-NEW-10** | §2.2 (No 8), §5.2, §6 (NC-05), §7.2 (F-03), §8 (AC-10), §10.4, §13.12.11 | PLAN sebelumnya belum mengoperasionalkan keputusan PO tentang tiga peran kunci independen dan otorisasi third-party packaging. | Mengganti status CLARIFY lama dengan keputusan PO APPROVED; memasukkan target architecture untuk self-packaging, third-party packaging delegation, authority/evidence lifecycle, federated trust resolution, verifier result separation, closed/versioned .nxcert evolution, integrasi SDK/Player/Verify/Registry, serta acceptance dan negative tests. Genesis Creator sebagai ROOT / INITIAL AUTHORITY dan batas subdelegation L0–L2 (Option A) telah diputuskan PO dan dirinci pada §10.4 serta §13.12.11. Tidak ada pertanyaan normatif PO yang tersisa tentang issuer atau subdelegation; sisa pekerjaan adalah kontrak teknis dan implementasi verifier/lifecycle. | Keputusan PO AUDIT-NEW-10; §13.12.11 | `CLOSED — PRODUCT DECISIONS AND TARGET ARCHITECTURE RECONCILED; TECHNICAL IMPLEMENTATION REMAINS OPEN UNDER NC-05 / AC-10` | Keputusan tiga peran, Genesis Creator sebagai root issuer, dan satu tingkat subdelegation telah disahkan serta direkonsiliasi. Rincian kontrak teknis/verifier tetap merupakan pekerjaan implementasi; tidak ada keputusan PO issuer/subdelegation yang tertunda. Implementasi PE-02 tetap NOT AUTHORIZED. |

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
Klasifikasi aktif 34 Acceptance Criteria mengikuti keputusan PO terbaru pada §13.1.1: 12 AC specification-ready, 22 AC execution-blocked, dan 0 AC menunggu keputusan PO. Status implementasi yang belum ada tidak boleh disamakan dengan ketidaklengkapan kontrak pra-coding.

| Kategori klasifikasi utama | Cakupan AC | Makna status |
|---|---|---|
| `TEST-PLANNED — SPECIFICATION READY` (12) | AC-04, AC-09, AC-11, AC-12, AC-17, AC-18, AC-19, AC-23, AC-24, AC-25, AC-30, AC-31 | Expected result dan test contract cukup ditetapkan; bukan klaim test sudah dijalankan atau runtime diverifikasi. AC-17 tetap membedakan DDL statis dari live DB NOT VERIFIED. |
| `TEST-PLANNED — EXECUTION BLOCKED` (22) | AC-01, AC-02, AC-03, AC-05, AC-06, AC-07, AC-08, AC-10, AC-13, AC-14, AC-15, AC-16, AC-20, AC-21, AC-22, AC-26, AC-27, AC-28, AC-29, AC-32, AC-33, AC-34 | Eksekusi menunggu implementasi pascaotorisasi, benchmark/evidence, atau residual spesifikasi/kompatibilitas pada baris AC individual. |
| `PO DECISION REQUIRED` (0) | — | Tidak ada keputusan PO aktif yang belum diputuskan. CONF-01, CONF-02, dan Model B/CONF-03 telah diselesaikan; residual teknis dicatat terpisah. |
| **TOTAL** | **34 AC** | **12 + 22 + 0 = 34** |

Subklasifikasi execution-blocked: AC-05 (B-01 strict parser module) dan AC-06 (B-02 JCS serializer module) adalah dua modul implementasi yang belum tersedia. Dua puluh AC lainnya menunggu dependency kontrak, integrasi, evidence, benchmark, atau implementasi yang dipetakan pada §8 dan §16.19. Tidak ada AC berstatus PO DECISION REQUIRED.

#### Rekonsiliasi Individual Wajib Seluruh 34 Acceptance Criteria (DEF-01, Mandat Konsolidasi PO)
Tabel berikut membuktikan penelusuran individual per AC mencakup seluruh 34 AC tanpa duplikasi, memisahkan kesiapan spesifikasi dari dependensi yang belum selesai:

| ID AC | Kontrak Dasar | Klasifikasi Utama | Dasar Klasifikasi & Sumber Otoritatif | Dependensi Langsung & Blocker Terkait | Status Dependensi | Dimensi & Gate | Hasil Verifikasi Konsistensi |
|:---:|:---:|:---|:---|:---|:---:|:---:|:---|
| **AC-01** | NC-01 | `TEST-PLANNED — EXECUTION BLOCKED` | White Paper v5.6 §Manifest; RFC 8259; §5.1 Skema Manifest; Keputusan PO AC-01 | NC-01 / Strict Unknown-Field Policy telah disahkan; universal schema masih belum lengkap | `BLOCKED BY UNIVERSAL SCHEMA & IMPLEMENTATION` | Execution Blocked / Gate A & B Dependency | Unknown fields ditolak fail-closed sesuai keputusan PO; pengujian end-to-end menunggu schema universal dan parser/validator. |
| **AC-02** | NC-01 | `TEST-PLANNED — EXECUTION BLOCKED BY UNIVERSAL MANIFEST CONTRACT` | White Paper v5.6; PKWARE APPNOTE; §5.1; Keputusan PO AUDIT-NEW-06/07/08 | Validasi ZIP entry types, archive integrity, path/case collision, filename rules, dan bijeksi deklarasi member-manifest vs regular-file entries | `BLOCKED BY NC-01 UNIVERSAL SCHEMA / MANIFEST NAME & MEMBER PATH CONTRACT` | NC-01 / Technical Contract Dependency | Structural ZIP rules yang telah diputuskan PO tetap dipertahankan; eksekusi AC-02 secara lengkap menunggu nama/lokasi manifest, member array/path, dan universal schema NC-01. Kuota resource B-07 diuji terpisah oleh AC-13.
| **AC-03** | NC-02 | RFC 8032; RFC 8785; AA §16.4 | Signed manifest mutation, malformed signature, wrong key, altered member order/name/hash/size, cross-language JCS mismatch | Signature-Stripped JCS and the embedded Ed25519 signature envelope verify the exact signed fields; mismatch fails with ERR_MANIFEST_SIGNATURE_INVALID | `[TEST-PLANNED — EXECUTION BLOCKED BY IMPLEMENTATION / CROSS-LANGUAGE TESTS]` | B-08 contract specified by AA; implementation and tests post-authorization |
| **AC-04** | NC-06 | `TEST-PLANNED — SPEC READY` | IETF RFC 8032; `container.go#L110`; PE-01 Baseline | Baseline PE-01 Beku (`.nx` container packaging signature) | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; format kontainer `.nx` anggota album beku. |
| **AC-05** | NC-03 | `TEST-PLANNED — EXECUTION BLOCKED` | White Paper v5.6 §Parsers; Nexa Parser Policy | B-01 (Modul Strict JSON Parser Engine belum diimplementasikan) | `BLOCKED (MODULE PENDING)` | Module Pending / Gate B | Konsisten; spesifikasi uji duplicate key siap, modul pending koding. |
| **AC-06** | NC-03 | `TEST-PLANNED — EXECUTION BLOCKED` | IETF RFC 8785; Canonical JCS Test Vectors TV-01..TV-08 | B-02 (Modul RFC 8785 JCS Serializer Engine belum diimplementasikan) | `BLOCKED (MODULE PENDING)` | Module Pending / Gate B | Konsisten; vektor uji RFC 8785 siap, modul serializer pending koding. |
| **AC-07** | NC-04 | White Paper Identity/Federated Trust; PO CONF-01; AA §16.5/§16.16.4A | Unknown signer, unbound key, missing/invalid per-Album authority carrier, album/signer/key/purpose mismatch, stale/conflicting federation evidence, or invalid manifest signature | Album Membership `UNAUTHENTICATED` / `INVALID` fail-closed; standalone PE-01 behavior remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER IMPLEMENTATION]` | PO issuer-authority decision resolved; WP-04/WP-05 implementation and tests post-authorization |
| **AC-08** | NC-04 | Roadmap v4.8 §5.5; White Paper v5.6 §19.6; AA §16.5/§16.15/§16.16.4A/B | Signer key revoked/expired/rotated, invalid recovery lineage, stale/unavailable lifecycle evidence | Membership NOT AUTHENTICATED when required evidence is absent/invalid/unknown; standalone PE-01 remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 LIFECYCLE / VERIFIER INTEGRATION]` | PO issuer-authority and subject-class decisions are resolved; remaining dependencies are source-compatibility elements bounded as NOT VERIFIED and WP-04/WP-05 implementation/tests post-authorization |
| **AC-09** | NC-05 | `TEST-PLANNED — SPECIFICATION READY` | White Paper v5.6 §Genesis; AA §16.12 | Untuk member payload_type MUSIC_AUDIO, digest bitstream audio terenkripsi dalam payload region PE-01 dibandingkan dengan members[].audio_payload_sha256 (64 lowercase hex); hash penuh child .nx dan ZIP wrapper tetap domain terpisah | Mismatch menghasilkan ERR_CONTAINER_HASH_MISMATCH; match hanya memenuhi pemeriksaan digest dan tidak memberikan authorization | `[TEST-PLANNED — SPEC READY]` | Kontrak field/path dan byte-domain AA §16.12; source mapping dan runtime test setelah otorisasi |
| **AC-10** | NC-05 | `TEST-PLANNED — SPECIFIED; IMPLEMENTATION / TEST PENDING AUTHORIZATION` | White Paper v5.6 §Genesis; `sdk.ts#L205-L255`; E-01; §16.21.6 | NC-05 / A-05 (`ERR_GENESIS_SIGNATURE_INVALID` PO-approved at E-01 boundary) | `CONTRACT CLOSED; IMPLEMENTATION / TEST PENDING` | Architecture Dependency / Post-authorization | Genesis signature failure has a dedicated approved reason code; fail-closed observable behavior remains unchanged. |
| **AC-11** | NC-06 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Container; `container.go#L110` | Ekstraksi kontainer mandiri `.nx` dari ZIP wrapper tanpa alterasi byte | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; format kontainer PE-01 mematuhi invariant byte utuh. |
| **AC-12** | NC-06 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Container; PE-01 Invariant Suite | Validasi packaging kontainer anggota mematuhi seluruh invariant PE-01 | `CLOSED (FROZEN BASELINE)` | Spec Ready / Gate A Ready | Konsisten; pengujian packaging kontainer mandiri terdefinisi jelas. |
| **AC-13** | NC-07 | PKWARE APPNOTE; RFC 1951; AA §16.14 | ZIP wrapper tested against measured per-dimension resource limits and adversarial boundaries | Streaming enforcement fails closed at each ratified limit; no universal numeric cap before deployment-representative benchmark | `[TEST-PLANNED — EXECUTION BLOCKED BY B-07 BENCHMARK EVIDENCE]` | Benchmark protocol specified; measured capacity envelope and numeric limit ratification pending |
| **AC-14** | NC-08 | PO commercial decisions; AA §16.8/§16.15 | Bundle checkout processes N child acquisitions with partial success, external timeout, daemon uncertainty, terminal failure and automatic refund | Member success preserved; unknown external result reconciled before retry; terminal refund idempotent; no assumed distributed rollback | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED ZERO-DDL FEASIBILITY]` | Transaction/recovery contract specified; durable receipt, mapping and existing-store proof pending B-04 |
| **AC-15** | NC-08 | PO commercial decisions; AA §16.8/§16.13/§16.15 | Repeat checkout/member operation after timeout, crash, callback replay or recovery using identical operation identity | Same operation returns same outcome without duplicate acquisition, entitlement, daemon grant or refund; stable idempotency key reused | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED ZERO-DDL FEASIBILITY]` | Idempotency preimage specified; durable receipt and daemon lookup/reconciliation proof pending B-04 |
| **AC-16** | NC-09 | White Paper v5.6 §Marketplace; AA §16.3/§16.15 | Persist/retrieve child hash per member acquisition/entitlement without changing wrapper hash semantics | member_sha256 is full physical child .nx SHA-256; acquired_package_sha256 remains wrapper-domain where source evidence says so; child hash uses existing Zero-DDL store only if proven | `[TEST-PLANNED — EXECUTION BLOCKED BY EXISTING STORAGE MAPPING PROOF]` | B-05 byte-domain specified; per-member persistence/acquisition mapping pending |
| **AC-17** | NC-10 | `TEST-PLANNED — SPEC READY` | `schema.postgres.sql#L63-L115`; Zero-DDL Contract | Kepatuhan skema statis Zero-DDL (Live DB runtime berstatus `NOT VERIFIED`) | `STATIC DDL REPORTED — NOT INDEPENDENTLY VERIFIED / OPEN (LIVE DB)` | Spec Ready / Gate A Conditional (DDL source evidence reported by Programmer; not independently verified) | Konsisten; skema SQL statis Zero-DDL 100% dipatuhi; live DB unverified. |
| **AC-18** | NC-11 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Registry; §6.11 | Verifikasi online via remote Registry API saat koneksi jaringan aktif | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; pengujian jalur online siap dieksekusi saat modul tersedia. |
| **AC-19** | NC-11 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Offline Fallback; §6.11 | Fallback cache offline pada network transport error; HTTP 5xx/bad sig melempar fail-closed | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; aturan offline fallback terisolasi ketat dari transport error. |
| **AC-20** | NC-12 | `TEST-PLANNED — EXECUTION BLOCKED` | POSIX.1-2017; `fs_safe.ts#L30`; Invariant Safe-Open | B-06 (Mitigasi Safe-Open & penerimaan residual risk concurrent rename POSIX userspace) | `BLOCKED` | Security Mitigation / Gate B | Konsisten; penolakan containment path traversal fail-closed; residual risk B-06. |
| **AC-21** | NC-12 | `TEST-PLANNED — EXECUTION BLOCKED` | POSIX.1-2017; `fs_safe.ts#L30`; Invariant Safe-Open | B-06 (Verifikasi post-open descriptor & penerimaan residual risk POSIX userspace) | `BLOCKED` | Security Mitigation / Gate B | Konsisten; pemeriksaan descriptor pasca-open fail-closed; residual risk B-06. |
| **AC-22** | NC-13 | White Paper JIT; PO decision; AA §16.1/§16.12/§16.15 | Current/queued Stage 8a digest diagnostics and current-member 8b/8c JIT | Stage 8a may run without 7b/7c for passive digest only; 8b requires 7b+7c+matching digest; 8c only current member after 8b | `[TEST-PLANNED — EXECUTION BLOCKED BY JIT / B-09 INTEGRATION]` | Stage 8a and digest field contract closed; B-09 source integration pending |
| **AC-23** | NC-13 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §JIT Player; §5.2 | Otorisasi JIT dieksekusi ulang secara independen saat pengguna berpindah trek | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; tidak ada otorisasi massal atau pembagian token lintas-trek. |
| **AC-24** | NC-13 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §JIT Player; §5.2 | Satu trek rusak dalam antrean album gagal diputar tanpa mengganggu trek valid | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; isolasi error per trek ditegakkan fail-closed secara mandiri. |
| **AC-25** | NC-14 | `TEST-PLANNED — SPEC READY` | White Paper v5.6 §Verify; Keputusan PO CONF-02; §5.3 | Mengikuti Keputusan PO (CONF-02 / NC-14 Pilihan B APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; hasil verifikasi setiap berkas `.nx` anggota ditampilkan secara individual; tidak ada pembuatan status agregat baru (`ALBUM_TRUSTED`, `ALBUM_INVALID`) | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; disahkan PO bahwa NX Verify tidak menggunakan status agregat. |
| **AC-26** | NC-15 | `TEST-PLANNED — SPECIFIED; IMPLEMENTATION / TEST PENDING AUTHORIZATION` | Error Taxonomy Spec §6.15; §16.21.6; 20 active emitted reason codes | NC-15 (AA/PO-approved deterministic reason-code contract) | `CONTRACT CLOSED; IMPLEMENTATION / TEST PENDING` | Technical implementation / post-authorization acceptance | All active reason codes have deterministic trigger/layer/disposition semantics specified; source implementation and runtime tests remain pending. |
| **AC-27** | NC-16 | AA §16.13; source/DDL evidence §16.15 | Recompute member_execution_key and operation idempotency key from exact JCS preimages; verify receipt maps to actual acquisition_id | Identical checkout/member/operation yields identical key; distinct members never overwrite; acquisition_id remains existing-system-issued; no new DDL assumed | `[TEST-PLANNED — EXECUTION BLOCKED BY RECEIPT / DDL COMPATIBILITY EVIDENCE]` | Formula specified by AA; durable receipt/storage proof remains B-04 dependency |
| **AC-28** | NC-01, NC-06 | White Paper Studio; PO §2.3.A; AA §16.2/§16.15 | Forge New Album sources sequentially and persist ordered member association | Canonical Album identity/member contract specified; existing store must preserve association, order, reload and recovery without DDL | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED PERSISTENCE FEASIBILITY]` | NC-06 source evidence pending; no schema/API invention |
| **AC-29** | NC-06 | White Paper Studio; PO §2.3.B; AA §16.2/§16.15 | Publish existing .nx files sequentially and reload as one Album entity | Existing pipeline and child .nx bytes unchanged; Album identity/member relation survives reload/recovery without DDL | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED RELOAD FEASIBILITY]` | NC-06 source evidence pending |
| **AC-30** | NC-01 | `TEST-PLANNED — SPEC READY` | Keputusan PO §2.3.C (Larangan Album Campuran); §5.4 | Validasi jenis masukan menolak kombinasi berkas sumber biasa dan existing `.nx` dalam satu Album secara fail-closed sebelum pemrosesan dimulai tanpa silent conversion dan tanpa merusak input | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; pemisahan jenis masukan disahkan PO secara APPROVED. |
| **AC-31** | NC-01, NC-06 | `TEST-PLANNED — SPEC READY` | Keputusan PO §2.4 (Failure Handling Studio); §5.5 | Kegagalan forging/upload menghentikan proses sementara; pengguna disajikan opsi diskrit "Ulangi" dan "Lewati"; retry upload memakai hasil `.nx` yang sama tanpa forging ulang dan wajib mencegah listing duplikat (hasil yang disetujui PO); mekanisme idempotensi teknis tidak ditetapkan sebagai kontrak dan bukti repository hanya laporan Programmer yang belum diverifikasi independen (`server.js#L2400-L2416, L2467-L2470`, `publish_pipeline.js#L316-L410`; status bukti: inspeksi lokal Programmer / audit independen pending); skip tidak menghapus file sumber; status forging vs upload dibedakan per anggota (terpisah dari B-04) | `CLOSED (SPEC READY)` | Spec Ready / Gate A Ready | Konsisten; tindakan Ulangi/Lewati, hasil Retry/Skip dan pencegahan listing duplikat disahkan; mekanisme idempotensi teknis tidak disahkan sebagai kontrak dan bukti repository belum diverifikasi independen. |
| **AC-32** | NC-13 | White Paper Universal Viewer; PO §2.5; AA §16.11/§16.15 | Player advances after current viewer emits definitive completion | Normalized VIEWER_COMPLETED, stale/duplicate rejection, resource release and fresh JIT specified; platform/payload source feasibility and parity tests remain required | `[TEST-PLANNED — EXECUTION BLOCKED BY VIEWER SOURCE FEASIBILITY / TESTS]` | AA lifecycle contract specified; source evidence and platform tests pending |
| **AC-33** | NC-14 | `TEST-PLANNED — EXECUTION BLOCKED BY B-09 MEMBERSHIP VERIFIER / SIGNER LIFECYCLE` | White Paper v5.6 §Verify Desktop; Keputusan PO §2.6, §2.7, CONF-01; §5.3 | NX Verify Desktop hanya memproses file sebagai anggota Album setelah autentisitas membership dibuktikan; kebijakan fail-closed untuk signer UNKNOWN atau signature invalid telah disahkan PO. Jika bukti belum valid, file manifest tidak diproses sebagai anggota Album; file yang diberikan independen tetap dapat diverifikasi standalone PE-01. Tombol manual Next, hasil per-anggota tanpa status agregat, dan Full Verify existing tetap dipertahankan. | `BLOCKED BY B-09 IDENTITY / LIFECYCLE / VERIFIER IMPLEMENTATION` | Execution Blocked / Gate B Dependency | Kebijakan produk sudah diputuskan; eksekusi menunggu identity binding, authority, trust lifecycle, verifier, dan pengujian. |
| **AC-34** | NC-14 | White Paper v5.6 §Verify Mobile Lite; PO §2.6/§2.7; §5.3 | NX Verify Mobile opens an Album; membership authenticity must pass before files are processed/labeled as Album members | If authenticated, Verify processes one member per step; otherwise manifest files are not processed as Album members. Independently supplied files remain standalone PE-01. Manual Next only; no aggregate Album status; Verify-Lite excludes Desktop batch verification, export, manual Registry refresh and payload rendering | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 ISSUER DECISION / VERIFIER / SIGNER LIFECYCLE]` | PO §2.6/§2.7 (Verify Mobile Lite Manual Next & Lite Isolation) |
---
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
   - *Lapisan 3: Album Manifest (`album_manifest.json` [nama/lokasi kandidat draf; belum disahkan])*: Ditandatangani oleh `album_signer_public_key`. Mandat penggunaan RFC 8785 JCS berlaku pada lapisan ini. Model Signature-Stripped JCS telah diputuskan; exact signed-content contract B-08 dan serializer implementation B-02 tetap menjadi dependensi readiness.
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
| **B-04 / NC-08 / CONF-03** | Gap transaksi Marketplace, Zero-DDL, dan daemon eksternal. | Tetap `BLOCKED`; Model B, SSP/Largest Remainder, identitas checkout, dan Manifest sebagai sumber kebenaran normatif telah disahkan. Kontrak atomisitas/pemenuhan multi-item, storage/persistensi, pemetaan acquisition, idempotency, recovery, settlement, side effect eksternal, serta exception resolution untuk refund tertahan masih harus dirancang. |
| **B-05 / NC-09** | Semantik `acquired_package_sha256` untuk child acquisition. | Tetap `BLOCKED`; melarang tebakan semantik kolom hash database. |
| **B-06 / NC-12** | Batas keamanan filesystem safe-open dan race condition. | Membedakan symlink, descriptor, containment, dan batas concurrent ancestor rename. |
| **B-08** | Signed-content construction dan verifier contract tanda tangan Album Manifest. | `SIGNATURE-STRIPPED JCS / EXACT SIGNED FIELD SET / EMBEDDED ED25519 SIGNATURE ENVELOPE SPECIFIED BY AA §16.4` | `NOT IMPLEMENTED` | `OPEN / POST-AUTHORIZATION IMPLEMENTATION / TESTS` | Signed content excludes only the embedded `signature` property; remaining manifest fields are bound by JCS UTF-8 bytes and Ed25519; negative and cross-language vectors specified §16.4. | After Gate B PASS and separate PO authorization, implement strict parser/JCS/verifier and execute vectors; no further design decision or PSV repeat. |
| **B-09 / NC-04 / CONF-01** | Kebijakan membership fail-closed telah disahkan PO; identity binding, authority, trust store, dan lifecycle signer tetap merupakan gap teknis B-09. | Policy resolved; implementasi identity/lifecycle signer tetap OPEN/BLOCKED. |
| **CONF-02** | Hierarki status agregat NX Verify. | **SELESAI / PO DECISION APPROVED (OPTION B)**: PO mengesahkan Pilihan B (tanpa status agregat Album di NX Verify; verifikasi individual member primer); AC-25 SPEC READY. AC-33/AC-34 tetap EXECUTION BLOCKED sampai implementasi/verifikasi membership dan signer lifecycle B-09 tersedia; kebijakan fail-closed telah diputuskan PO. |
| **Acceptance Criteria** | Status AC tidak seragam jika dependensi berbeda. | Setiap AC mewarisi status dependensi riil (34 AC aktif: 11 Spec Ready + 23 Execution Blocked, termasuk AC-01 [strict unknown-field policy disahkan; universal schema/parser pending], AC-07 [membership policy fail-closed disahkan; signer lifecycle B-09 pending], AC-22, AC-27, AC-28, AC-29, dan AC-32) + 0 PO Decision Required = 34 AC; direkonsiliasi dari snapshot historis 27 AC. |
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
Kontrak produk PE-02 yang telah disahkan mencakup pengelompokan logis `.nx` mandiri, empat kategori sumber, pemisahan Forge New dan Existing `.nx`, perilaku Player/Verify, serta keputusan PO lain yang tercantum eksplisit dalam plan. **Keputusan PO PE-02 yang dicatat pada §5.1 telah mengesahkan ZIP wrapper hanya sebagai transport/packaging envelope Album.** Persetujuan tersebut tidak berasal dari White Paper v5.6/Roadmap v4.8 dan tidak mengesahkan nama/lokasi manifest, schema JSON, nama array/field path, Album Signer, JCS/Ed25519, maupun mekanisme persistence/reload. Detail yang belum diputuskan tetap proposal/unresolved. Daftar langkah teknis berikut tidak menyatakan fitur telah tersedia atau terimplementasi.

### 4.3 Matriks Status Komponen Aktual vs Klaim White Paper v5.6
Tabel berikut mencatat lokasi dan status inspeksi yang DILAPORKAN Programmer; AA belum memiliki akses/bukti primer repositori `whisnu/nexa` untuk memverifikasi inspeksi tersebut secara independen. Status pengujian runtime dipisahkan dari laporan inspeksi kode.

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
Tabel berikut memuat kutipan kode, path absolut, dan line range sebagaimana **dilaporkan Programmer** dari inspeksi lokal. AA belum memeriksa repository primer `whisnu/nexa`; kutipan ini bukan bukti yang diverifikasi independen dan tidak boleh dinaikkan menjadi klaim implementasi terverifikasi:

> [!NOTE]
> **Provenance Bukti Repository (Programmer-only):** Repository sumber `whisnu/nexa` merupakan domain akses kerja Programmer. AA tidak diwajibkan dan tidak diasumsikan memiliki akses langsung ke repository tersebut. Isi §4.4 adalah ledger bukti yang diserahkan/dilaporkan Programmer; pemeriksaan AA menilai provenance, kecukupan kutipan, keterlacakan, konsistensi internal, serta batas klaim bukti tersebut. Status `VERIFIED BY PROGRAMMER` tidak berarti verifikasi independen oleh AA dan tidak boleh dinaikkan menjadi bukti runtime jika yang tersedia hanya inspeksi statis.

| ID Bukti | Komponen & Klaim yang Diperiksa | Path Berkas & Line Range | Kutipan Mentah Kode Sumber (*Raw Snippet*) | Batas Klaim Pembuktian Faktual | Status Verifikasi (Inspeksi Lokal Programmer vs Audit Independen) |
|:---:|:---|:---|:---|:---|:---:|
| **E-01** | Struktur Dua Lapisan Genesis Certificate & Verifikasi Ed25519 | `/opt/antigravity/projects/nexa/sdk/typescript/src/sdk.ts#L205-L260` | ```typescript\n// Lapisan 1: Registry Certificate (6-field JCS / 5-field fallback)\nconst canonStr = NexaRegistry.canonicalJcs(regCert.certificate_id, regCert.issued_at, regCert.issuer, regCert.status, regCert.valid_until, creatorKey);\nsigValid = NexaCrypto.verify(registryPubKey, Buffer.from(canonStr, "utf8"), sigBytes);\n// Lapisan 2: Embedded Genesis Ownership Certificate (8-field canonical string)\nconst canonGenesisStr = JSON.stringify({\n  asset_id: ownCert.asset_id, creator_public_key: ownCert.creator_public_key,\n  effective_at: ownCert.effective_at, issued_at: ownCert.issued_at,\n  issuer_id: ownCert.issuer_id, previous_cert_ref: ownCert.previous_cert_ref || "",\n  subject_id: ownCert.subject_id, underlying_cert_id: ownCert.underlying_cert_id\n});\nconst cryptoValid = NexaCrypto.verify(ownKeyObj, Buffer.from(canonGenesisStr, "utf8"), ownSigBytes);\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): struktur dua lapisan yang diklaim adalah (1) Registry Certificate menggunakan 6 field pada `canonicalJcs` diverifikasi dengan `registryPubKey`; (2) Embedded Genesis Ownership Certificate menggunakan tepat 8 field kanonikal diverifikasi dengan `creator_public_key`. Tidak ditemukan konstanta error `ERR_GENESIS_SIGNATURE_INVALID` pada baseline (status kode error diskrit kanonikal: unresolved / fail-closed `canPlay:false` via generic error). | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR` |
| **E-02** | Ekstraksi Kontainer Single `.nx` di Go Engine (Hasil PSV) | `/opt/antigravity/projects/nexa/internal/container/container.go#L90-L130` | ```go\n// internal/container/container.go:L106-L114\nif manifestLen > 100*1024*1024 || payloadLen > 2*1024*1024*1024 || sigLen != 64 {\n    return nil, nil, nil, errors.New("invalid section sizes in container header")\n}\nexpectedSize := int64(headerSize) + int64(manifestLen) + int64(payloadLen) + int64(sigLen)\nif int64(len(data)) < expectedSize {\n    return nil, nil, nil, fmt.Errorf("container is truncated: expected %d bytes, got %d", expectedSize, len(data))\n}\n``` | Hasil PSV membuktikan kontainer `.nx` adalah format biner murni (Magic `NEXA`, header 21-byte, payload maks 2 GiB, trailer 64-byte Ed25519 signature). **TIDAK** menggunakan parser ZIP pada engine Go, dan tidak ada parser ZIP arsip Album di source repository aktif (B-03/B-07). | `VERIFIED BY PSV (CONTAINER BINARY FORMAT VERIFIED; ZIP PARSER NOT PRESENT IN SOURCE)` |
| **E-03** | Skema Database PostgreSQL — acquired_package_sha256 (PSV-05 / PSV-R06) | `marketplace/db/schema.postgres.sql#L63-L135`, `marketplace/server.js#L762-L770`, `#L2231`, `#L2396`, `#L3839-L3861` | DDL utuh kedua tabel (`acquisitions` L72 & `entitlements` L112, serta migrasi L133-L134) dan alur pembentukan hash (`computeFileSha256(session.spool_path)`) diverifikasi pada commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`. Byte-domain hash terbukti adalah berkas spool paket delivery (wrapper ZIP) utuh. | Hasil inspeksi Programmer membuktikan asal nilai `catalog_snapshots.package_sha256` dari stream seluruh berkas paket delivery spool dan konsistensi DDL L63-L135 dengan SQL producer. Pemetaan child-member Album tidak ada di skema; live DB tidak diverifikasi. | `VERIFIED BY PROGRAMMER — STATIC SOURCE; LIVE DB NOT VERIFIED; CHILD CONTRACT OPEN` |
| **E-04** | Ketiadaan 2PC pada Transaksi Marketplace Eksternal | `/opt/antigravity/projects/nexa/marketplace/server.js#L170-L205` | ```javascript\n// HTTP call ke Sprint 12 License Daemon tanpa 2PC\nconst licenseRes = await fetch(`${LICENSE_DAEMON_URL}/issue`, {\n  method: 'POST',\n  body: JSON.stringify({ userId, itemId })\n});\nif (!licenseRes.ok) {\n  // Mutasi database lokal sudah committed; atomisitas terdistribusi gagal\n  throw new Error("ERR_LICENSE_DAEMON_COMMUNICATION");\n}\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): potongan alur HTTP yang menurut laporan tidak menunjukkan 2PC/kompensasi terdistribusi; B-04/CONF-03 tetap blocker dan tidak ditutup oleh laporan ini. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR; B-04 REMAINS OPEN` |
| **E-05** | Pendaftaran Protokol NX Player & Handler JIT | `/opt/antigravity/projects/nexa/player-desktop/main.js#L182-L194` & `#L541-L560` | ```javascript\nprotocol.registerSchemesAsPrivileged([\n  { scheme: 'nexa-playback', privileges: { standard: true, secure: true, stream: true } }\n]);\nipcMain.handle('nexa:authorize-track', async (event, trackUri) => {\n  // Handler otorisasi JIT dipanggil sebelum buffer didaftarkan\n  return await executeJITAuthorization(trackUri);\n});\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): scheme `nexa-playback` dan IPC handler sebagaimana kutipan; runtime tidak diverifikasi. **TIDAK** membuktikan eksekusi timing 8-tahap JIT telah teruji di runtime fisik. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR` |
| **E-06** | Modul Kriptografi Ed25519 & Encoding Hex | `/opt/antigravity/projects/nexa/sdk/typescript/src/crypto.ts#L45-L65` | ```typescript\nexport function verifyEd25519Signature(signatureHex: string, messageBytes: Uint8Array, publicKeyHex: string): boolean {\n  if (signatureHex.length !== 128) return false; // 64 bytes = 128 hex chars\n  const sigBytes = Buffer.from(signatureHex, 'hex');\n  const pubBytes = Buffer.from(publicKeyHex, 'hex');\n  return ed25519.verify(sigBytes, messageBytes, pubBytes);\n}\n``` | Dilaporkan Programmer sebagai hasil inspeksi lokal (belum diverifikasi independen): representasi signature Ed25519 128-hex lowercase yang diklaim berasal dari repository, bukan standar RFC eksternal. | `REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED BY AUDITOR; 128-HEX IS REPOSITORY-REPORTED FORMAT` |
| **E-07** | Invariant Filesystem Safe-Open (Hasil PSV) | `/opt/antigravity/projects/nexa/player-desktop/main.js#L573,L738` & `/opt/antigravity/projects/nexa/internal/filesystem/hidden_helper.js#L24-L60` | ```javascript\n// player-desktop/main.js:L573\nconst fd = fs.openSync(trackInfo.filePath, 'r');\n// player-desktop/main.js:L738\nconst fileData = fs.readFileSync(filePath);\n``` | Hasil PSV mengonfirmasi berkas `sdk/typescript/src/fs_safe.ts` **TIDAK ADA** pada source tree. Aplikasi desktop saat ini menggunakan `fs.openSync` dan `fs.readFileSync` standar tanpa flag `O_NOFOLLOW` dan tanpa verifikasi descriptor `fstat`. Modul safe-open descriptor-based wajib dibuat dari awal; mitigasi per platform dan residual risk didokumentasikan pada §15.9 (PSV-07). | `VERIFIED BY PSV (fs_safe.ts NOT PRESENT; RUNTIME USES STANDARD OPEN; EXECUTION BLOCKED B-06)` |
| **E-08** | Status Git Repositori Aktual & Kebersihan Root | Terminal Remote Linux Host `/opt/antigravity/projects/nexa/` | ```bash\n$ git rev-parse HEAD\nfc08a5c7ac6aa1b0e4bcf64dc264666f149e1956\n$ git status --porcelain\n?? docs/roadmaps/Nexa_Development_Roadmap_v4_8.md\n?? docs/whitepapers/Nexa_White_Paper_v5_6.md\n$ ls -la /opt/antigravity/projects/nexa/\ntotal 1780 (hanya berkas resmi proyek di root; Rule D)\n``` | **Laporan inspeksi lokal Programmer; bukan bukti yang diverifikasi independen oleh AA.** Jika akurat, output tersebut melaporkan nol mutasi tracked pada commit yang disebut, dua berkas untracked di `docs/`, dan inspeksi `ls -la` terbatas pada root level. Keberadaan, isi, dan hash berkas staging di `evidence/` juga tidak diverifikasi secara independen dalam audit ini. | `[REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED] / NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE` |
| **E-09** | Keterbatasan Verifikasi Runtime Mobile & Service | `/opt/antigravity/projects/nexa/mobile/` & `/opt/antigravity/projects/nexa/cmd/usage/` | *(Ketiadaan harness uji runtime fisik mobile iOS/Android dan Usage Service cluster pada server Linux headless)* | Mengakui secara transparan bahwa runtime mobile dan usage service cluster belum diuji eksekusinya di lingkungan remote server Linux saat ini. | `NOT VERIFIED — EVIDENCE NOT AVAILABLE` |

---

## 5. PRODUCT TRUTH SERTA PERILAKU ALBUM

### 5.1 Konsep Produk Album, Proposal Packaging/Manifest, dan Batas Otoritas
Album sebagai konsep produk PE-02 adalah pengelompokan logis berkas `.nx` mandiri dari empat kategori sumber yang telah disetujui PO: Music/Audio, Video, Document, dan Image. **Keputusan PO — ZIP Wrapper APPROVED:** ZIP wrapper disahkan sebagai transport/packaging envelope untuk distribusi Album, dengan ketentuan Album tetap logical grouping, setiap member tetap `.nx` independen, tidak ada `album.nx` atau perubahan format `.nx`, dan ZIP tidak menggantikan identitas, signature, ownership, maupun trust setiap member. Album Membership Manifest adalah deklarasi membership yang terpisah dari Immutable Checkout Manifest Marketplace. Persetujuan wrapper ini tidak menetapkan nama/lokasi manifest, struktur JSON, nama array/field path, signer, signature construction, persistence, atau lifecycle. Kandidat `album_manifest.json` dan struktur manifest tetap **PROPOSAL TEKNIS / UNRESOLVED**. White Paper v5.6 dan Roadmap v4.8 tidak menetapkan kontrak Album-specific tersebut; otorisasi ZIP wrapper berasal dari keputusan PO ini. RFC 8785 (JCS) dan RFC 8032 (Ed25519) adalah standar teknis; keberadaan standar itu sendiri tidak mengesahkan penggunaan JCS/Ed25519 untuk Album Signer atau menentukan payload/signature construction. Seluruh contoh JSON/schema dan diagram packaging di bagian ini harus dibaca sesuai status proposalnya, bukan sebagai Product Truth.

#### Prinsip Dasar Album & Batasan Mutlak Tata Kelola (Keputusan PO: APPROVED)

> **Batas provenance bukti repository (§5.1):** Seluruh path, nomor baris, DDL, endpoint, dan perilaku kode lokal yang disebut dalam bagian ini merupakan laporan inspeksi Programmer (`REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`), kecuali dinyatakan lain dengan bukti primer yang diperiksa AA. Audit dokumen GitHub ini tidak memeriksa `whisnu/nexa`; kata *PROVEN*, *membuktikan*, atau *terbukti* pada klaim repository tidak boleh ditafsirkan sebagai verifikasi independen.
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
> 1. **Divergensi Identifier Hash Bitstream Audio — DISPOSISI AA §16.12**: Byte-domain Stage 8a dan field/path kanonikal ditetapkan sebagai SHA-256 atas exact encrypted audio bitstream pada payload region child PE-01, dideklarasikan pada members[].audio_payload_sha256 untuk payload_type MUSIC_AUDIO. audio_sha256 dan notasi draf tracks[].sha256 bukan alias/fallback; keduanya superseded sebagai kandidat draf. AC-09 SPEC READY. Digest tidak menggantikan full child member_sha256 atau ZIP wrapper hash.
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
> | **Verifikasi Digest Manifest (Tahap 8a)** | `REQUIRED (members[].audio_payload_sha256)` | `UNRESOLVED — NON-AUDIO PAYLOAD CONTRACT` | `UNRESOLVED — NON-AUDIO PAYLOAD CONTRACT` | AA §16.12 menetapkan payload_type dan field audio-only. Digest audio membandingkan exact encrypted bitstream sebelum dekripsi; tidak menetapkan hash domain video/document/image. |
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
   - `manifest_version`: kandidat versi manifest dalam draf; keberadaan field, nilai, dan requiredness belum ditetapkan Architecture Authority.
   - `container_format_version`: versi format kontainer PE-01 tetap merupakan bagian baseline kontainer `.nx`, tetapi representasinya sebagai field manifest Album belum disahkan.
   - `created_at`: RFC 3339/ISO 8601 hanya mengatur format waktu bila digunakan; standar tersebut tidak mewajibkan field `created_at` dalam manifest Album.
   - `title`: semantik nama/judul Album disetujui PO untuk UI/katalog; lokasi field JSON manifest dan bentuk serialisasinya belum disahkan.
   - Kumpulan anggota `.nx` independen adalah konsep produk PE-02; **nama array JSON, bentuk objek anggota, dan pemetaan dari draf audio `tracks[] [notasi draf audio non-normatif; bukan path manifest universal]` belum ditetapkan sebagai kontrak normatif**. Architecture Authority menetapkan bentuk teknis yang memenuhi kontrak PO; PO hanya diminta kembali bila ada perubahan material pada perilaku/semantik produk yang telah disetujui.
     - **Semantik nama berkas member (bukan nama field JSON yang disahkan):** pola strictly flat `^[a-zA-Z0-9_-]+\.nx$` tanpa path separator/subdirektori; keputusan PO menyetujui aturan nama/keunikan case-insensitive via ASCII case-fold, bukan identifier field.
     - **Semantik judul/nama tampilan member (bukan nama field JSON yang disahkan):** rentang usulan 1..255; keberadaan dan representasi sebagai field manifest belum disahkan.
   - *Field Deklarasi Kriptografis Universal (Status: PROPOSED FIELD CONTRACT)*: `album_signer_public_key`, `album_signer_signature`, `canonical_algorithm`, `signature_algorithm` belum ditetapkan sebagai nama/field schema normatif. Model konstruksi Signature-Stripped JCS telah disetujui (B-08); exact signed field set, encoding, schema placement, dan identity/key lifecycle tetap belum lengkap (B-08/B-09). Circular dependency signature telah diselesaikan pada tingkat model.
   - *Field Metadata Tambahan Universal (Status: PROPOSED SPECIFICATION)*: `album_id`, `artist`, `total_tracks` / `total_members`, `release_date` (usulan perancang, belum disahkan PO).
2. **Field Khusus Tipe Payload (Payload-Specific Fields)**:
   - *Payload Audio / Musik*: Field normatif adalah members[].audio_payload_sha256 untuk payload_type MUSIC_AUDIO sesuai AA §16.12. Kandidat lama audio_sha256 dan notasi tracks[].sha256 telah superseded; bukan alias, fallback, atau compatibility alternative. duration_seconds, track_number, dan track_id tetap hanya contoh metadata audio non-normatif sampai kontrak field metadata disahkan. Draf JSON Schema Draft 7 di bawah tetap historical audio-specific proposal, bukan schema manifest aktif.
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
| members[] | Universal Packaging Structure | Ordered array of member objects | AA §16.2 | SPECIFIED BY AA | Exact full JSON Schema, filename/location and signer schema placement still require reconciliation |
| Nama berkas member (JSON path belum ditetapkan) | Member filename invariant | String regex `^[a-zA-Z0-9_-]+\.nx$` | Keputusan PO AUDIT-NEW-06/07 | **SEMANTIK NAMA BERKAS DISETUJUI PO; FIELD PATH UNRESOLVED** | Keputusan PO mengesahkan aturan nama/flatness dan keunikan ASCII case-fold, bukan nama array atau path JSON. Validasi normatif terhadap manifest menunggu penetapan struktur.
| Judul member (JSON path belum ditetapkan) | Metadata member | Belum ditetapkan | Tidak ada dasar normatif untuk field judul per-member | **PROPOSED / UNRESOLVED** | White Paper §Studio tidak menetapkan path atau kewajiban field judul per-member dalam manifest Album. Jangan menganggapnya required atau menolak manifest karena field ini sebelum ada keputusan.
| `album_id` | Metadata Album | String pattern `^alb_[0-9a-f]{16}$` | Usulan Perancang | **PROPOSED SPEC (PENDING PO/ARCH)** | Usulan derivasi ID; terhambat ketiadaan tabel Album di database Marketplace. |
| `artist` | Metadata Album | String (1..255 char) | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Belum diotorisasi sebagai field wajib yang disahkan PO. |
| `total_tracks` / `total_members` | Metadata Album | Integer (1..199) | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Konsistensi terhadap jumlah anggota hanya dapat ditetapkan setelah struktur koleksi normatif disahkan; tidak ada `len(members[] [contoh identifier koleksi non-normatif; bukan path manifest disahkan])` yang ditetapkan saat ini. |
| `release_date` | Metadata Album | String format `YYYY-MM-DD` | Usulan Perancang | **PROPOSED SPEC (PENDING PO)** | Validasi kalender riil (menolak tanggal ilegal seperti 2026-02-31); proposal. |
| `album_signer_public_key` | Deklarasi Kriptografis | String pattern `^[0-9a-f]{64}$` | Proposal NC-02 / B-08 | **PROPOSED SPEC (UNRESOLVED LIFECYCLE B-09)** | Hex 64 kunci publik Ed25519; identitas dan lifecycle signer unresolved di WP v5.6. |
| `album_signer_signature` | Deklarasi Kriptografis | String pattern `^[0-9a-f]{128}$` | Proposal NC-02 / B-08 | **PROPOSED SPEC (BLOCKED B-08)** | Hex 128 tanda tangan Ed25519 (format encoding masih perlu dikonfirmasi dalam kontrak final); Signature-Stripped JCS telah dipilih, tetapi exact signed-content contract B-08 masih terbuka. |
| `canonical_algorithm` | Deklarasi Kriptografis | String enum `["RFC8785-JCS"]` | RFC 8785 | **PROPOSED SPEC (BLOCKED B-02)** | Enum algoritma kanonisasi; proposal perancang. |
| `signature_algorithm` | Deklarasi Kriptografis | String enum `["Ed25519"]` | RFC 8032 | **PROPOSED SPEC** | Enum algoritma tanda tangan; proposal perancang. |
| members[].audio_payload_sha256 | Payload-Specific: MUSIC_AUDIO | String SHA-256 lowercase hex (64 chars) | AA §16.12 | SPECIFIED BY AA | Required only for MUSIC_AUDIO; not an alias/fallback and not applicable to non-audio payloads |
| `duration_seconds` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | Number minimum 0.1 | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Durasi audio detik; tidak berlaku untuk dokumen dan gambar yang tidak memiliki durasi alami. |
| `track_number` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | Integer (1..199) | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Penomoran urutan trek audio monotonik kontigu 1..N. |
| `track_id` (path JSON belum ditetapkan) | Payload-Specific: Audio Only | String pattern `^trk_[0-9a-f]{16}$` | Proposal §5.1 | **PROPOSED SPEC (AUDIO ONLY)** | Pola ID trek audio; proposal perancang. |

##### C. Matriks Perilaku Validasi Manifest (Schema Validation Matrix — AC-01)
Sistem menerapkan validasi deterministik sesuai keputusan PO dan AA yang telah disahkan. Strict unknown-field rejection tetap berlaku; payload_type memiliki enum tertutup; audio_payload_sha256 wajib hanya untuk MUSIC_AUDIO. Schema JSON lengkap, file envelope/name/location, schema-version release, dan signer schema placement masih memerlukan rekonsiliasi.

| Kondisi Masukan / Anomali Manifest | Tingkat Pemeriksaan | Hasil Evaluasi Sistem | Error Code Dihasilkan | Dasar Penegakan & Batasan Keputusan |
|---|---|:---:|:---:|---|
| **Required Field yang Hilang** | Level 2 (Struktur Skema) | **REJECTED** | `ERR_MANIFEST_MALFORMED` | Fail-closed deterministik; ketiadaan properti wajib membatalkan validasi pada Tahap 3. |
| **Unknown Field (Properti Tambahan)** | Level 3 (Invariant Semantik) | **REJECTED — PO DECISION APPROVED** | `ERR_MANIFEST_MALFORMED` | Unknown fields wajib ditolak fail-closed sesuai keputusan PO AC-01. Ini tidak menyelesaikan universal multi-payload schema, field/path JSON, atau implementasi parser/validator. |
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
- **Kebijakan unknown fields: PO APPROVED — STRICT REJECTION / FAIL-CLOSED.** Unknown fields pada schema version aktif wajib ditolak dengan `ERR_MANIFEST_MALFORMED`; permissive-ignore tidak berlaku.
- Jika disahkan: dokumen manifest yang memuat field tambahan akan ditolak fail-closed dengan `ERR_MANIFEST_MALFORMED`.
- Penetapan ini tidak mengesahkan schema universal multi-payload, nama array/path JSON, atau daftar field final. `additionalProperties: false` hanya boleh diterapkan pada schema version/objek yang memang telah didefinisikan lengkap; jangan mengklaim seluruh schema Album sudah normatif.

| **AC-08** | NC-04 | Roadmap v4.8 §5.5; White Paper v5.6 §19.6; AA §16.5/§16.15/§16.16.4A/B | Signer key revoked/expired/rotated, invalid recovery lineage, stale/unavailable lifecycle evidence | Membership NOT AUTHENTICATED when required evidence is absent/invalid/unknown; standalone PE-01 remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 LIFECYCLE / VERIFIER INTEGRATION]` | PO issuer-authority and subject-class decisions are resolved; remaining source-compatibility elements are bounded NOT VERIFIED and Album-specific implementation/tests are post-authorization |
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
   - *Operasi*: Melakukan serialisasi kanonikal RFC 8785 JCS atas payload manifes dan, setelah exact signed-content contract B-08 dan serializer B-02 siap, memverifikasi tanda tangan Ed25519 Album Signer (`album_signer_signature`) menggunakan `album_signer_public_key` atas canonical UTF-8 bytes dari signed content yang telah mengeluarkan field signature. Pemeriksaan status signer pada Registry **BUKAN operasi yang saat ini dinyatakan tersedia**; evaluasi Registry hanya dapat dilakukan setelah identitas, enrollment, identity binding, key rotation, dan revocation lifecycle Album Signer ditetapkan secara otoritatif. Sampai saat itu status Registry merupakan kondisi unresolved yang harus ditangani, bukan klaim adanya endpoint, record, atau mekanisme lookup.
| **AC-08** | NC-04 | Roadmap v4.8 §5.5; White Paper v5.6 §19.6; AA §16.5/§16.15/§16.16.4A/B | Signer key revoked/expired/rotated, invalid recovery lineage, stale/unavailable lifecycle evidence | Membership NOT AUTHENTICATED when required evidence is absent/invalid/unknown; standalone PE-01 remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 LIFECYCLE / VERIFIER INTEGRATION]` | PO issuer-authority and subject-class decisions are resolved; remaining source-compatibility elements are bounded NOT VERIFIED and Album-specific implementation/tests are post-authorization |
     1. Tahap 4 dalam proposal ini, jika kelak disahkan, hanya mengevaluasi kanonisasi payload dan validitas kriptografis signature manifest. Tahap 4 **TIDAK** mengevaluasi kredibilitas/trust Album Signer pada Registry karena mekanisme Registry belum ditetapkan; Tahap 4 juga **BUKAN PENGGANTI DAN TIDAK MENENTUKAN** validitas atau trust individual masing-masing berkas `.nx` anggota.
     2. *Manifest Signature Gagal Kriptografis*: Manifest ditolak fail-closed sebagai deklarasi yang tidak autentik (`ERR_MANIFEST_SIGNATURE_INVALID`). Karena daftar membership pada deklarasi yang gagal autentikasi tidak dapat dipercaya, sistem **DILARANG** mengklaim atau memproses entri yang disebut manifest tersebut sebagai anggota Album terverifikasi. Sistem juga **DILARANG** menyimpulkan bahwa bytes kontainer, Creator signature, ownership proof, atau Registry trust file `.nx` menjadi `INVALID` akibat kegagalan manifest. Diagnostik member hanya boleh dilakukan jika file `.nx` dipilih/disediakan secara independen di luar membership manifest yang gagal; hasilnya harus dilaporkan sebagai verifikasi file mandiri, bukan verifikasi anggota Album.
     3. *Signer UNKNOWN*: Jika Album Signer berstatus `UNKNOWN`, sistem DILARANG menyimpulkan bahwa signer atau member `.nx` `INVALID`, dan DILARANG menetapkan larangan/izin playback global berdasarkan status signer Album. Namun, sampai CONF-01 diputuskan, autentisitas deklarasi membership manifest tidak boleh diasumsikan; daftar member dari manifest tersebut tidak boleh diperlakukan sebagai membership Album yang terverifikasi. File `.nx` yang dipilih/disediakan secara independen tetap dapat dievaluasi melalui verifikasi dan otorisasi standalone PE-01; hasilnya bukan verifikasi anggota Album.
     4. *Preservasi White Paper v5.6*: Status `UNKNOWN / INCOMPLETE` BUKAN `INVALID`; Integrity Verification dipisahkan dari Trust Verification. Ketentuan White Paper tentang Play/View dengan warning saat trust tidak tersedia hanya diterapkan pada file `.nx` yang identitas dan konteksnya dapat diverifikasi secara independen menurut kontrak standalone PE-01. Ketentuan tersebut TIDAK mengautentikasi membership Album dan tidak memberi dasar untuk memperlakukan daftar member dari manifest signer `UNKNOWN` sebagai daftar Album tepercaya. Kegagalan integritas/hash/signature member dan revocation otoritatif atas trust evidence milik member tetap ditangani menurut kontrak PE-01; status Album Signer tidak menjadi global playback gate. Berkas offline dengan `.nxcert` cocok serta evidence Registry-authenticated yang sah tetap dievaluasi menurut kontrak PE-01.
    - *Error Code*: `ERR_MANIFEST_SIGNATURE_INVALID` (setelah exact signed-content/verifier contract B-08 dan serializer B-02 siap). `ERR_ALBUM_SIGNER_UNTRUSTED` dan `ERR_ALBUM_SIGNER_UNKNOWN` bukan operasi/error hasil lookup Registry yang saat ini tersedia; keduanya hanya kategori kondisi yang masih menunggu penetapan identitas dan lifecycle signer, dan tidak boleh diperlakukan sebagai hasil operasional Tahap 4.
   - *AC Penguji*: **AC-03, AC-06, AC-07, AC-08** (NC-02, NC-03, NC-04, B-02, B-08, B-09).
5. **Tahap 5 — Pemeriksaan Bijeksi 1:1 Manifes-ke-ZIP & Case-Insensitive Uniqueness**:
   - *Objek Data*: Daftar nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan) pada manifes vs Central Directory ZIP.
   - *Prasyarat*: Manifes telah berhasil di-parse secara sintaksis pada Tahap 3, dan daftar entri Central Directory ZIP telah tersedia dari Tahap 2. Pemeriksaan bijeksi pada tahap ini hanya memeriksa konsistensi struktural antara deklarasi dan entri fisik ZIP; pemeriksaan ini **BUKAN** autentikasi deklarasi membership dan tidak mengesahkan file apa pun sebagai anggota Album. Autentisitas membership tetap bergantung pada penyelesaian kebijakan/otoritas signer yang berlaku (CONF-01 / B-09).
   - *Pemeriksaan*: Memvalidasi bijeksi eksak 1:1 antara manifes dan ZIP: setiap file yang dideklarasikan pada manifes wajib ada di ZIP, dan tidak ada file reguler ekstra/asing di dalam ZIP di luar deklarasi manifes dan `album_manifest.json` [nama/lokasi kandidat draf; belum disahkan] (entri direktori yang diizinkan PO tidak membatalkan bijeksi); validasi keunikan nama berkas case-insensitive via ASCII case folding (AUDIT-NEW-07).
   - *Error Code*: `ERR_ZIP_ENTRY_MISMATCH` (secara deterministik untuk seluruh ketidakcocokan bijeksi 1:1: baik berkas manifes hilang di ZIP maupun berkas reguler ekstra/asing di ZIP yang tidak dideklarasikan). Catatan: benturan nama case-insensitive antar-entri ZIP telah ditolak pada Tahap 2 dengan `ERR_ZIP_INVALID`.
   - *AC Penguji*: **AC-02, AC-13** (NC-01, NC-07).
6. **Tahap 6 — Ekstraksi Member .nx & Atomic Filesystem Safe-Open Descriptors (AUDIT-NEW-01, AUDIT-NEW-03)**:
   - *Objek Fisik*: Berkas kontainer `.nx` dari anggota Album yang sedang menjadi *current member*, diekstrak ke filesystem lokal sementara/staging.
   - *Prasyarat*: Tahap 6 sebagai pemrosesan **anggota Album** hanya boleh dijalankan setelah autentisitas membership deklarasi manifest telah dibuktikan secara sah. Pemeriksaan struktur ZIP/manifest pada Tahap 2–5 saja tidak memenuhi prasyarat tersebut. Jika membership belum autentik—misalnya signer `UNKNOWN`, signature manifest invalid, atau bukti identity/authority/lifecycle belum dapat diverifikasi karena kontrak/verifier B-09 belum tersedia—sistem tidak boleh mengekstrak atau memproses file berdasarkan klaim bahwa file tersebut anggota Album. CONF-01 telah disahkan PO; yang masih terbuka adalah realisasi teknis B-09, bukan keputusan kebijakan CONF-01. File `.nx` yang dipilih/disediakan secara independen tetap dapat diperiksa melalui jalur standalone PE-01; hasilnya bukan pemrosesan anggota Album.
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
       - **Keputusan PO AUDIT-NEW-10 — APPROVED**: genesisPubKey adalah Genesis Creator/originator dan menandatangani Genesis Ownership Certificate; containerSigKey adalah Container Packager/Packaging Engine dan menandatangani integritas binary container .nx; ownCertPubKey adalah current holder/buyer/collector sebagai subjek hak kepemilikan/lisensi saat ini. Ketiganya adalah peran berbeda dan tidak diwajibkan identik. ownCertPubKey boleh berbeda dari genesisPubKey jika rantai transfer kepemilikan sah menghubungkannya. Jika containerSigKey != genesisPubKey, wajib ada delegation/authorization evidence yang dapat diverifikasi. Tanpa bukti tersebut, packaging adalah UNTRUSTED / UNAUTHORIZED PACKAGING meskipun signature matematis valid. Self-packaging (containerSigKey == genesisPubKey) memiliki otoritas inheren dan tidak memerlukan delegation tambahan. Detail delegation mengikuti §13.12.11. Genesis Creator sebagai ROOT / INITIAL AUTHORITY dan batas satu tingkat subdelegation (L0–L2, Option A) telah diputuskan PO; tidak ada pertanyaan normatif issuer/subdelegation yang tersisa.
     - **7c. Evaluasi Status Active License / Entitlement Pengguna**:
       Pemeriksaan hak kepemilikan / lisensi pemutaran aktif pengguna pada Marketplace / engine lokal (`is_licensed: true`). Jika pengguna tidak memiliki lisensi pemutaran aktif, evaluasi menghasilkan **`ERR_PLAYBACK_UNAUTHORIZED`**.
   - *AC Penguji*: **AC-04, AC-10, AC-22** (NC-05, NC-06, NC-13).

8. **Tahap 8 — Verifikasi Digest SHA-256 Audio, Dekripsi Terotorisasi, dan Pendaftaran Buffer (AUDIT-NEW-01)**:
   - **8a. Verifikasi Digest SHA-256 Audio (Audio Digest Verification)**:
     - *Objek Data*: Payload biner bitstream audio mentah terenkripsi di dalam kontainer `.nx` trek aktif.
     - *Prasyarat I/O Fisik Minimum*: Deskriptor berkas aman yang dibuka atomik dari Tahap 6 (`fs.openSync` dengan `O_RDONLY | O_NOFOLLOW`) dan integritas kemasan fisik kontainer PE-01 dari Tahap 7a (`NexaContainer.unpack(data)`).
        *Peringatan Batas Normatif*: Stage 8a telah disetujui PO pada 2026-11-10 sebagai pemeriksaan diagnostik pasif. Deskriptor aman Tahap 6 dan integritas kontainer PE-01 Tahap 7a diperlukan untuk membaca byte payload. Stage 8a boleh menghitung digest tanpa menunggu Genesis 7b atau active license 7c; ini bukan bypass karena hasil digest tidak mengotorisasi dekripsi atau playback.
     - *Pemeriksaan*: Menghitung digest SHA-256 atas bitstream audio mentah biner kontainer `.nx` dan mencocokkannya secara eksak dengan deklarasi hash bitstream audio pada manifes album (notasi konseptual: lokasi dan field deklarasi hash belum ditetapkan; status field identity: `UNRESOLVED — FIELD IDENTITY NOT ESTABLISHED BY NORMATIVE CONTRACT; STOP AND CLARIFY`; dilarang menganggap kedua nama sebagai alias yang sama-sama diterima atau fallback). Jika tidak cocok, proses dibatalkan fail-closed dengan melempar **`ERR_CONTAINER_HASH_MISMATCH`**.
     - *Batasan Status Diagnostik & Isolasi Hak Putar*: Pemeriksaan digest ini adalah pemeriksaan integritas fisik atas bitstream mentah. Keberhasilan pencocokan digest 8a **TIDAK PERNAH** memberikan hak otorisasi pemutaran (*no playback authorization*), tidak mengizinkan dekripsi payload (8b), dan tidak mengizinkan pendaftaran buffer (8c).
     - *Status Ketergantungan Normatif Genesis (7b) dan Lisensi Aktif (7c)*:
        - **Dependensi terhadap Validasi Genesis (7b)**: Genesis 7b bukan prasyarat komputasi digest diagnostik pasif Stage 8a. Stage 8a tidak menyimpulkan Genesis valid atau invalid. Genesis/ownership validation yang sah tetap wajib secara kumulatif untuk Stage 8b dan Stage 8c. Status: **`PO-APPROVED — DIAGNOSTIC-ONLY`**.
        - **Dependensi terhadap Lisensi Aktif (7c)**: Active license 7c bukan prasyarat komputasi digest diagnostik pasif Stage 8a. Hasil Stage 8a tidak membuktikan entitlement atau playback permission. Active license yang sah tetap wajib untuk Stage 8b/8c. Status: **`PO-APPROVED — DIAGNOSTIC-ONLY`**.
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
     - *Larangan Keras Pre-Verifikasi*: Background pre-verification terhadap anggota album berikutnya dalam antrean **DILARANG KERAS** memicu buffer registration atau menghasilkan otorisasi implisit untuk anggota album yang belum menjadi *current member*. Status izin diagnostik pre-verifikasi pada Stage 8a sendiri berstatus **`PO-APPROVED — PASSIVE DIAGNOSTIC BACKGROUND PRE-VERIFICATION ALLOWED; NO DECRYPTION / BUFFER REGISTRATION / PLAYBACK AUTHORIZATION`**.
   - *Error Code*: `ERR_CONTAINER_HASH_MISMATCH` (pada 8a), `ERR_PLAYBACK_UNAUTHORIZED` (pada 8b).
   - *AC Penguji*: **AC-09** (8a), **AC-22, AC-23, AC-24** (8b, 8c).

#### Matriks Dependensi Silang JIT Album (§3.4 Mandat Audit)
Tabel berikut merinci status dependensi setiap prasyarat terhadap ketiga sub-tahap pemrosesan audio (Stage 8a Digest, Stage 8b Decryption, Stage 8c Buffer Registration):

| Prasyarat / Tahap Asal | Stage 8a: Digest SHA-256 | Stage 8b: Dekripsi Audio | Stage 8c: Pendaftaran Buffer | Dasar Bukti & Status Normatif |
|---|:---:|:---:|:---:|---|
| **Deskriptor Berkas Aman (Tahap 6)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | POSIX.1-2017 `O_RDONLY \| O_NOFOLLOW`; `fs_safe.ts#L30-L55` (E-07). Prasyarat I/O fisik minimum untuk membaca bitstream mentah. |
| **Integritas Kontainer PE-01 (Tahap 7a)** | `REQUIRED` | `REQUIRED` | `REQUIRED` | Format kemasan PE-01 (`internal/container/container.go#L35-L80`). Diperlukan untuk unpacking offset header, payload, dan trailer signature. |
| **Validasi Genesis Certificate (Tahap 7b)** | `NOT REQUIRED — DIAGNOSTIC ONLY` | `REQUIRED` | `REQUIRED` | Stage 8a tidak menyimpulkan validitas Genesis; Genesis/ownership tetap wajib untuk dekripsi Stage 8b dan buffer Stage 8c. |
| **Evaluasi Active License (Tahap 7c)** | `NOT REQUIRED — DIAGNOSTIC ONLY` | `REQUIRED` | `REQUIRED` | Stage 8a tidak menyimpulkan entitlement; active license tetap wajib untuk Stage 8b/8c (`ERR_PLAYBACK_UNAUTHORIZED` bila tidak sah). |
| **Digest Stage 8a Cocok** | `Hasil pemeriksaan` | `REQUIRED` | `REQUIRED` | Digest wajib cocok dengan members[].audio_payload_sha256 untuk MUSIC_AUDIO sesuai AA §16.12; exact encrypted audio bitstream byte-domain. Ini syarat 8b/8c tetapi bukan authorization tersendiri. |
| **Stage 8b Berhasil** | `Tidak berlaku` | `Hasil dekripsi` | `REQUIRED` | Aturan dependensi Stage 8b menuju Stage 8c: (1) Stage 8c hanya boleh dilakukan setelah Stage 8b berhasil; (2) Keberhasilan Stage 8a saja tidak cukup untuk mengizinkan Stage 8c; (3) Jika Stage 8b gagal, alur pemrosesan wajib dihentikan fail-closed sebelum Stage 8c dijalankan; (4) Buffer yang didaftarkan pada Stage 8c harus merupakan hasil dekripsi yang sah dari Stage 8b untuk *current member*; (5) Tidak boleh ada buffer registration untuk anggota yang belum menjadi *current member*. |
| **Trek Merupakan Current Member** | `CURRENT OR QUEUED — DIAGNOSTIC ONLY` | `CURRENT MEMBER ONLY` | `CURRENT MEMBER ONLY` | Stage 8a boleh berjalan untuk current/queued member secara diagnostik; Stage 8b hanya pada current-member playback; Stage 8c hanya setelah 8b berhasil dan untuk current member. |
| **Background Pre-Verification untuk Anggota Berikutnya** | `ALLOWED — PASSIVE DIAGNOSTIC ONLY` | `NOT ALLOWED` | `NOT ALLOWED` | PO-approved: background digest only; no decryption, buffer registration, playback authorization, or implicit auth-state change. |

> **Pemisahan Tiga Lapisan Kebutuhan Pre-Verifikasi & Batas Keamanan Stage 8 (AUDIT-NEW-01 PO Clarification):**
> Dokumen ini secara tegas memisahkan tiga lapisan yang berbeda dan melarang penyamaan antara kemampuan komputasi dengan izin tata kelola produk:
> 1. **Technical Capability (Kemampuan Teknis Komputasi)**: Secara teknis biner filesystem dan parser, sistem mampu membuka deskriptor aman berkas kontainer `.nx` anggota album berikutnya dalam antrean dan menghitung hash SHA-256 bitstream terenkripsi tanpa kunci dekripsi.
> 2. **Diagnostic Permission (Izin Diagnostik Produk)**: Kontrak produk Nexa yang disahkan (White Paper v5.6, Roadmap v4.8) **belum menetapkan** apakah Player diizinkan mengeksekusi pemeriksaan digest diagnostik atas berkas antrean sebelum berkas tersebut diputar. Status izin diagnostik ini ditetapkan secara jujur dan tidak memihak sebagai:
>    **`PO-APPROVED — PASSIVE DIAGNOSTIC BACKGROUND PRE-VERIFICATION ALLOWED; NO DECRYPTION / BUFFER REGISTRATION / PLAYBACK AUTHORIZATION`**.
>    Dokumen tidak menyatakan pre-verifikasi sebagai `ALLOWED`, dan tidak mengarang larangan sepihak sebagai `NOT ALLOWED`.
> 3. **Playback Authorization (Otorisasi Pemutaran & Batas Keamanan Stage 8b/8c)**: Background pre-verification dalam kondisi apa pun **DILARANG KERAS** menghasilkan otorisasi pemutaran, dilarang melakukan dekripsi payload audio (Stage 8b), dan dilarang mendaftarkan buffer audio (Stage 8c). Pendaftaran buffer audio hanya dan selalu berlaku eksklusif untuk trek yang sedang aktif diputar oleh pengguna (*current member*).
>
> **Aturan Dependensi Silang Tahap 7 terhadap Tahap 8a, 8b, dan 8c (AUDIT-NEW-01 Mandat):**
 > 1. *Batas Prasyarat Fisik vs Izin Diagnostik (Tahap 7a -> Tahap 8a)*: Descriptor aman Tahap 6 dan integritas PE-01 Tahap 7a merupakan prasyarat I/O untuk membaca byte payload. Keputusan PO 2026-11-10 mengizinkan digest diagnostik pasif tanpa menunggu Genesis 7b atau active license 7c. Hasil 8a tidak menyatakan 7b/7c lulus dan tidak memberi hak dekripsi/pemutaran.
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
 > - *Larangan Pre-Otorisasi*: Pre-verifikasi diagnostik Stage 8a untuk anggota berikutnya di antrean Album diizinkan berdasarkan keputusan PO 2026-11-10. Izin tersebut hanya mencakup pembacaan/hash pasif; tidak memberikan playback authorization, tidak melakukan Stage 8b, tidak mendaftarkan buffer Stage 8c, dan tidak mengubah authorization state. Current member tetap menjalani seluruh pemeriksaan JIT secara independen.

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
| **NC-01** | Canonical Album Manifest, ordered member binding, payload discriminator | `TOP-LEVEL / COMMON-MEMBER / AUDIO-DIGEST / TIER-1/TIER-2 CONTRACT SPECIFIED; COMPLETE SCHEMA & ZIP ENTRY PLACEMENT OPEN` | `NOT IMPLEMENTED` | `OPEN — AC-01/02 CONTRACT COMPLETION + IMPLEMENTATION` | §16.2, §16.12, §16.16.4A/B menetapkan field top-level, common member, order, payload_type, audio digest, dan evidence structures. Complete nested machine-validatable schema/version rules serta exact ZIP Manifest entry name/location masih terbuka. Audio example §5.1 tetap non-normatif. |
| **NC-02** | Manifest signature and verifier construction | `SIGNATURE-STRIPPED JCS / EXACT SIGNED FIELD SET / EMBEDDED ED25519 ENVELOPE SPECIFIED` | `NOT IMPLEMENTED` | `OPEN — B-08 IMPLEMENTATION / CROSS-LANGUAGE TESTS POST-AUTHORIZATION` | AC-03; §16.4 defines exact signed-content set, removal of only top-level signature, RFC 8785 JCS UTF-8 byte domain, embedded Ed25519 envelope and verifier sequence. Detached signature and outer envelope are not selected. |
| **NC-03** | Strict JSON Parser & RFC 8785 JCS Serializer | `SPECIFIED` | `NOT IMPLEMENTED` | `BLOCKED BY B-01, B-02` | Terblokir implementasi B-01 & B-02. Duplicate key: Nexa parser policy (AC-05, AC-06). |
| **NC-04** | Identity, per-Album Membership Authority, Album Signer lifecycle and verifier (AC-07/08) | `PO POLICY APPROVED; AA SEMANTIC / CARRIER / OFFLINE CLOSURE CONTRACT SPECIFIED` | `ALBUM-SPECIFIC CAPABILITY / VERIFIER NOT IMPLEMENTED` | `OPEN — WP-04 / WP-05 POST-AUTHORIZATION; SOURCE COMPATIBILITY ELEMENTS NOT VERIFIED` | Individual Creator and Organization are approved subject classes. Explicit `ALBUM_MEMBERSHIP_SIGNING`, exact `album_id`, Tier-1 designation, Tier-2 carrier, existing trust-anchor termination, lifecycle and Dual-Horizon semantics are specified in §16.5/§16.16.4A/B. Individual Creator lifecycle and some native proof serialization/verifier details remain bounded NOT VERIFIED; no PO issuer-authority decision is pending. |
| **NC-05** | AC-09, AC-10 | White Paper v5.6 §Genesis; AA §16.12; AUDIT-NEW-10 | §6.9; §16.9/§16.12; E-01 | AC-09 `[TEST-PLANNED — SPEC READY]`; AC-10 `[TEST-PLANNED — EXECUTION BLOCKED BY GENESIS ERROR TAXONOMY / IMPLEMENTATION]` | Audio digest field/path and byte-domain specified by AA; Genesis error taxonomy remains separate residual |
| **NC-06** | AC-04, AC-11, AC-12, AC-28, AC-29, AC-31 | White Paper v5.6 §Container/Studio; PO §2.3/§2.4; AA §16.2/§16.15 | §5.4/§5.5; E-02; §16.15 | AC-04/11/12/31 `[TEST-PLANNED — SPEC READY]`; AC-28/29 `[TEST-PLANNED — SOURCE FEASIBILITY BLOCKED]` | Album identity/member manifest contract specified by AA; existing persistence, association, reload and recovery must be proven without DDL |
| **NC-07** | Batas Keamanan Ekstraksi Arsip ZIP Wrapper | `PARTIALLY SPECIFIED — ENTRY/PATH/TYPE POLICY SET; RESOURCE QUOTAS BENCHMARK-GATED` | `NOT IMPLEMENTED` | `PROPOSED SPEC — BENCHMARK-GATED; NO HARD CAP RATIFIED` | Kandidat awal 500 MB compressed / 4 GB expanded / 200 physical entries dan rasio 10:1 atau 100:1 hanya input benchmark, bukan hard cap normatif. Benchmark envelope empat payload, threat model, adversarial tests, dan capacity evidence harus dievaluasi Architecture Authority sebelum hard caps per-layer/per-entry/cumulative ditetapkan. |
| **NC-08** | AC-14, AC-15 | PO commercial decisions; AA §16.8/§16.13/§16.15 | `marketplace/server.js` reported; source/DDL proof required | `[AA CONTRACT SPECIFIED — SOURCE-BACKED ZERO-DDL FEASIBILITY BLOCKED]` | Checkout/member execution state, idempotency, receipts, reconciliation and recovery specified; durable store and actual acquisition mapping must be proven under §16.15 |
| **NC-09** | AC-16 | White Paper v5.6 §Marketplace; AA §16.3/§16.15 | §6.9; E-03; §15.9.5 | `[CHILD HASH CONTRACT SPECIFIED — EXISTING STORAGE MAPPING BLOCKED]` | Child .nx byte-domain specified; acquired_package_sha256 remains wrapper-domain where evidence says so; Zero-DDL child hash persistence proof required |
| **NC-10** | Kepatuhan Mutlak Skema Zero-DDL Marketplace | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Skema PostgreSQL aktif dipatuhi; dapat diuji independen dari model B-04 (AC-17). |
| **NC-11** | Mekanisme Offline Fallback Registry Terkendali | `SPECIFIED` | `NOT IMPLEMENTED` | `NONE` | Fallback HANYA untuk transport network error; HTTP 5xx/bad sig fail-closed (AC-18, AC-19). |
| **NC-12** | Filesystem Safe-Open Berbasis Invariant Keamanan (AUDIT-NEW-03) | `SPECIFIED` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY B-06` | Pembukaan descriptor `O_NOFOLLOW` + `fstatSync` dilaporkan Programmer pada E-07; belum diverifikasi independen; verifikasi ganda `lstatSync` dan `dev`/`ino` berstatus gap residu kode desktop; batas userspace POSIX diakui; fail-closed `canPlay: false` (AC-20, AC-21). |
| **NC-13** | AC-22, AC-23, AC-24, AC-32 | White Paper v5.6 §JIT/Universal Viewer; PO §2.5; AA §16.1/§16.11/§16.15 | §5.2; E-05; §16.15 | AC-22 `[TEST-PLANNED — JIT / B-09 INTEGRATION BLOCKED]`; AC-23/24 `[TEST-PLANNED — SPEC READY]`; AC-32 `[TEST-PLANNED — VIEWER SOURCE FEASIBILITY BLOCKED]` | Stage 8a permission and Auto-Next event semantics specified; B-09 integration and definitive per-platform/payload completion source remain to be evidenced |
| **NC-14** | Verify per-member behavior and exclusion of aggregate Album trust status | `PO DECISION APPROVED; AA BEHAVIOR CONTRACT SPECIFIED` | `ALBUM MEMBERSHIP VERIFIER NOT IMPLEMENTED` | `OPEN — B-09 MEMBERSHIP VERIFIER / LIFECYCLE INTEGRATION POST-AUTHORIZATION` | CONF-02 Option B is active: no aggregate Album trust status; AC-25 is specification-ready. AC-33/AC-34 remain execution-blocked on B-09 authority carrier, verifier and lifecycle integration. CONF-01 membership fail-closed is approved; Verify output is not playback authorization. |
| **NC-15** | Error taxonomy dimensions and stable reason-code registry (AC-26) | `SEMANTIC CONTRACT CLOSED; 20 ACTIVE REASON CODES SPECIFIED (19 legacy active + 1 PO-approved Genesis); replay label deprecated` | `NOT IMPLEMENTED` | `PLAN CONTRACT CLOSED — IMPLEMENTATION / TEST PENDING AUTHORIZATION` | §6.15 and §16.21.6 define deterministic triggers, producer layers, dispositions, retryability, affected object, evidence/provenance boundary and AC mapping. `ERR_GENESIS_SIGNATURE_INVALID` is PO-approved for E-01 only; PE-01 observable behavior is unchanged. `ERR_MARKETPLACE_REPLAY_DETECTED` is deprecated and not emitted. |
| **NC-16** | AC-27 | AA §16.13; DDL/source evidence §16.15 | §16.13 | `[FORMULA SPECIFIED BY AA — RECEIPT / DDL COMPATIBILITY BLOCKED]` | member_execution_key and operation idempotency JCS preimages specified; no acquisition_id replacement or new DDL; actual durable receipt mapping remains B-04 evidence dependency |

---

### Rincian Kontrak Kritis Terpilih

#### 6.1 Rincian NC-01: Skema Manifest Album & Kebijakan Unknown Fields
- **ZIP Wrapper — PO APPROVED:** ZIP adalah transport/packaging envelope distribusi Album, bukan format kontainer Nexa baru. Album tetap logical grouping dan setiap member tetap `.nx` mandiri; tidak ada `album.nx` atau perubahan format `.nx`. ZIP tidak menggantikan identitas, Creator signature, Genesis/ownership, Registry, license authority, atau trust setiap member. **Album Membership Manifest** mendeklarasikan membership Album dan terpisah secara dokumen, namespace, authority, serta trust domain dari **Immutable Checkout Manifest** Marketplace. Draf masih mengusulkan objek JSON UTF-8 bernama `album_manifest.json` di root ZIP; nama/lokasi tersebut belum disahkan.
- **Kebijakan Unknown Fields — PO APPROVED:** Unknown fields wajib ditolak fail-closed dengan `ERR_MANIFEST_MALFORMED`. Kebijakan permissive-ignore tidak berlaku. Keputusan ini tidak melengkapi schema universal multi-payload atau menetapkan nama array/path JSON yang masih unresolved.

#### 6.2 Rincian NC-02: Signature Album Signer, Input Kanonikal & Batas Payload (Temuan 1, B-08, AUDIT-TRUTH-03)
- **Status Kontrak**: **`SIGNATURE-STRIPPED JCS / EXACT SIGNED-CONTENT / VERIFIER CONTRACT SPECIFIED BY AA §16.4`**.
- **Definisi Input Signature & Resolusi Circular Dependency (B-08)**:
  1. Memasukkan field `album_signer_signature` ke dalam payload manifest yang dikanonisasi JCS untuk menandatangani dirinya sendiri menimbulkan ketergantungan melingkar (*circular dependency*).
  2. **Keputusan PO/Architecture Authority:** gunakan Signature-Stripped JCS. `album_signer_signature` dikeluarkan dari objek sebelum serialisasi RFC 8785. Detached signature file tidak dipilih.
  3. Penggunaan RFC 8785 JCS saja **TIDAK OTOMATIS MENYELESAIKAN** persoalan signature scope tanpa definisi payload kanonikal yang disahkan.
  4. Field signature itu sendiri tidak boleh menimbulkan circular dependency pada canonical payload.
- **Preservasi Kontrak Kriptografis Anggota `.nx`**:
  Tanda tangan manifest Album Signer **DILARANG KERAS MENGUBAH ATAU MENGGANTIKAN**:
  1. Format, makna, dan verifikasi Creator packaging signature pada masing-masing kontainer `.nx` (NC-06 / AC-04);
  2. Format, makna, atau kewenangan Genesis Ownership Certificate (NC-05 / AC-10);
  3. Verifikasi Registry Authority Certificate pada masing-masing `.nx`.
- **Status Blocker**: Exact signed field set, canonical byte-domain, embedded signature envelope, and verifier sequence are specified by AA §16.4. B-08 remains open only for post-authorization engine implementation and cross-language/negative/adversarial test execution; AC-03 remains execution-blocked for those implementation/test deliverables, not for an unresolved PO choice or missing AA signature-scope decision.



#### Keputusan PO/Architecture Authority — B-08 Signature Construction (APPROVED)

1. Model konstruksi tanda tangan Album Manifest adalah **Signature-Stripped JCS**.
2. `album_signer_signature` tidak menjadi bagian dari signed content dan wajib dikeluarkan dari objek manifest sebelum canonicalization.
3. Signed content yang tersisa diserialisasi menggunakan RFC 8785 JCS; byte UTF-8 hasil canonicalization menjadi input Ed25519 untuk signing dan verification.
4. Signature tetap direpresentasikan pada manifest yang sama. Detached signature file (`album_manifest.sig`) dan outer cryptographic envelope bukan model yang dipilih.
5. Keputusan ini hanya menyelesaikan pilihan model dan circular dependency. Exact signed field set, schema version/field contract, canonical byte-domain details, serialization conformance, signer-key binding/lifecycle (B-09), verifier behavior, serta negative/adversarial tests tetap harus diselesaikan sebelum B-08/AC-03 dapat dinyatakan ready.
6. Album Signer signature tidak menggantikan atau mengubah Container Packaging Signature, Registry Certificate Signature, maupun Genesis Ownership Certificate Signature pada setiap `.nx`.

#### 6.3 Rincian NC-03: Strict JSON Parser & Penanganan Escape Unicode (Spesifikasi Tambahan 2)
- **Status Kontrak**: **`BLOCKED BY B-01, B-02`**.
- **Pemisahan Standar RFC 8259 vs Kebijakan Nexa**: RFC 8259 Bagian 4 menyatakan bahwa nama anggota objek dalam JSON "SHOULD be unique", tetapi tidak mewajibkan penolakan mutlak oleh setiap parser umum. Penolakan duplikasi kunci pada Nexa adalah **Kebijakan Parser Ketat Nexa (Nexa Strict Parser Policy)**, bukan kewajiban mutlak RFC 8259.
- **Aturan Spesifikasi Parser Nexa**:
  - *Duplicate Keys Literal*: Jika dua kunci identik secara literal karakter (e.g. `{"title": "A", "title": "B"}`), parser menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Duplicate Keys via Decoded Unicode Escape*: Jika dua kunci identik setelah karakter escape Unicode didekode (e.g. `{"\u0074itle": "A", "title": "B"}`), parser mendecode escape sebelum memeriksa keunikan kunci dan menolak dengan **`ERR_MANIFEST_DUPLICATE_KEY`**.
  - *Malformed Escape Syntax*: Jika urutan escape salah secara sintaksis (e.g. `\u123z`, escape terpotong `\u12`, atau lone surrogates `\uD800` tanpa pasangan legal), parser menolak dengan **`ERR_MANIFEST_MALFORMED`**.
- **Pemisahan Parser vs Serializer JCS**: Strict Parser (B-01, AC-05) bertugas pada tahap deserialisasi byte stream mentah. RFC 8785 JCS Serializer (B-02, AC-06) bertugas pada tahap serialisasi kanonisasi deterministik (pengurutan kunci UTF-16, format bilangan tanpa $-0$, minifikasi whitespace).

#### 6.4 Rincian NC-04: Identitas, Federated Trust, dan Lifecycle Album Signer (B-09, CONF-01, AUDIT-TRUTH-04)

- **Status Kontrak**: **`ALBUM SIGNER ARCHITECTURE MODEL B APPROVED / ARCHITECTURE DIRECTION SET / DETAILED IDENTITY & LIFECYCLE CONTRACT OPEN`**. PO/Architecture Authority menyetujui **Album Signer Architecture Model B**: Album Signer merupakan otoritas penandatanganan deklarasi membership Album yang identitas dan kewenangannya diverifikasi melalui fondasi Identity dan Federated Trust Nexa yang sudah ada. Otoritas membership ini independen dari `CONTAINER_PACKAGING`; bukan trust root baru dan bukan pengganti Registry, Genesis, ownership, atau licensing tiap member. CONF-01 tetap disahkan dan tidak dibuka kembali. PSV-R10/R10A tetap CLOSED sesuai batas bukti §15.11.3.

- **Pemisahan Domain Otoritas**:
  1. Album Signer menandatangani deklarasi membership Album saja. Keberhasilan signature dan trust Album Signer tidak membuktikan bahwa setiap member `.nx` valid, dimiliki secara sah, memiliki lisensi aktif, atau diizinkan diputar.
  2. Album Signer bukan `genesisPubKey`, `containerSigKey`, `ownCertPubKey`, Registry issuer key, maupun Licensing Authority. Kesamaan key/subject tidak boleh diasumsikan dan tidak menggabungkan kewenangan domain-domain tersebut.
  3. Hak `CONTAINER_PACKAGING` yang diatur §13.12.11 tidak otomatis memberikan hak menandatangani Album membership; sebaliknya, kewenangan Album Signer tidak memberikan hak membuat atau mengemas kontainer `.nx`.
  4. Identity menyatakan siapa subject yang terikat pada key; authority menyatakan apakah subject tersebut berwenang menandatangani deklarasi membership Album. Keduanya wajib diverifikasi terpisah.

- **Model Identity dan Federated Trust (Architecture Direction)**:
  1. Subject Album Signer harus diikat ke identitas Nexa yang dapat diverifikasi melalui fondasi Identity yang ada, bukan dipercaya hanya karena public key tercantum di manifest atau karena manifest memiliki signature Ed25519 yang matematis valid.
  2. Penilaian trust menggunakan mekanisme Federated Trust Nexa: evidence dari Registry atau trust/evidence provider yang relevan dinilai berdasarkan identitas issuer, validitas evidence, scope, freshness, dan hasil verifikasi kriptografis. Registry tetap merupakan evidence provider/authority sesuai domainnya, bukan hidden global winner atau satu-satunya root untuk semua trust.
  3. Tidak boleh menciptakan global root, central signer authority, atau trust override implisit. Konflik antar-evidence harus tetap terlihat dan ditangani sesuai prinsip federasi Nexa; tidak boleh diselesaikan dengan memilih satu Registry secara diam-diam.
  4. Model Organization Identity Sprint 14 dan Creator identity trust chain merupakan building blocks yang relevan, tetapi bukan bukti bahwa setiap detail kontrak organisasi atau Creator otomatis menjadi kontrak Album Signer.
  5. **Subject-class decision — PO APPROVED (2026-11-10):** Album Signer dapat menggunakan kedua kelas Identity Subject yang telah ada di Nexa, yaitu Individual Creator maupun Organization. Keputusan ini menetapkan kelayakan kelas subjek, bukan pemberian kewenangan otomatis kepada setiap Creator atau Organization. Untuk setiap signer, authority Album Membership Signing harus dinyatakan secara eksplisit dan diverifikasi melalui Identity/Federated Trust Nexa. Tidak ada lagi PO decision yang diperlukan untuk memilih kelas subject; pemetaan teknis ke kontrak Identity existing tetap menjadi pekerjaan Architecture Authority.

- **Key Binding dan Lifecycle — Required Technical Contract**:
  1. Verifier harus dapat membuktikan binding antara Album Signer subject, public key yang digunakan menandatangani manifest, dan authority untuk scope deklarasi membership Album. Public key yang hanya disisipkan oleh pembuat manifest tanpa evidence binding tidak cukup.
  2. Kontrak teknis harus mencakup enrollment/issuance atau pengakuan key melalui mekanisme Identity/Federated Trust existing yang terbukti sesuai; key custody; activation; validity interval; rotation; recovery; revocation; issuer/subject binding; scope; dan freshness/offline evidence.
  3. Rotation atau recovery tidak boleh diam-diam membuat key lama tetap berwenang. Verifier harus dapat membedakan key aktif, key historis yang masih valid untuk waktu tertentu, key revoked, key expired, key unknown, dan evidence yang tidak cukup/fresh.
  4. Revocation Album Signer hanya memengaruhi autentisitas deklarasi membership sesuai lifecycle Album Signer. Revocation tersebut tidak otomatis mencabut Creator signature, Genesis Ownership Certificate, Registry evidence, ownership, atau licensing member `.nx`. Revocation member-level juga tidak otomatis mencabut Album Signer.
  5. Timestamp, trusted-time source, event ordering, offline snapshot, freshness window, dan perilaku saat bukti lifecycle tidak tersedia harus ditetapkan secara eksplisit. Jangan memakai timestamp lokal yang tidak terautentikasi sebagai bukti revocation/validity.

- **Membership Verifier dan CONF-01**:
  1. Verifier memeriksa signature manifest menggunakan Signature-Stripped JCS sesuai §6.2, kemudian memvalidasi key-to-subject binding, authority, dan lifecycle melalui Federated Trust.
  2. Signature matematis valid tanpa identity/authority evidence yang dapat diverifikasi tidak mengautentikasi membership.
  3. Status signer `UNKNOWN`, evidence tidak cukup/fresh, konflik yang belum terselesaikan, signature invalid, revoked, atau expired menghasilkan membership yang tidak terautentikasi/fail-closed sesuai CONF-01. Status `UNKNOWN / INCOMPLETE` tetap bukan sinonim global `INVALID`; hasil tersebut tidak boleh mengubah standalone verification atau JIT playback authorization member `.nx`.
  4. Album membership verifier tidak menggantikan verifier standalone PE-01. Player tetap mengotorisasi current member secara JIT; pre-verification Album tidak memberikan playback authorization.

- **Batas Implementasi dan Larangan Asumsi**:
  1. Tidak ada bukti dalam sumber yang ditinjau bahwa endpoint, Registry record type, database field, certificate format, API, atau storage khusus Album Signer telah tersedia. Status ketersediaan setiap mekanisme tersebut adalah **`NOT VERIFIED`** sampai ada bukti primer.
  2. Adaptasi harus terlebih dahulu memetakan kontrak dan primitive Identity/Federated Trust existing. Dilarang membuat endpoint, schema, Registry record sintetis, global trust root, atau jalur otorisasi baru hanya untuk mengisi gap B-09 tanpa dasar kontrak dan pembuktian Zero-DDL/kompatibilitas yang relevan.
  3. Tidak ada asumsi bahwa Registry public key dapat dipakai untuk memverifikasi Creator signature. Binding dan issuer verification harus tetap mengikuti domain identitas yang tepat.
  4. Tidak ada perubahan source code, schema, database, atau runtime pada tahap plan correction ini.

- **Required Acceptance / Negative Test Design sebelum Gate B**:
  1. Signature valid + subject/key binding valid + authority valid + lifecycle fresh → membership dapat diautentikasi.
  2. Signature valid tetapi key tidak terikat pada subject → membership tidak terautentikasi.
  3. Subject dikenal tetapi tidak memiliki authority membership Album → membership tidak terautentikasi.
  4. Signer/key unknown, evidence missing/stale, issuer tidak dipercaya, atau federated conflict unresolved → membership fail-closed; tidak mengubah hasil standalone `.nx`.
  5. Key revoked/expired sebelum waktu evaluasi → membership tidak terautentikasi menurut aturan waktu/lifecycle yang ditetapkan.
  6. Key rotation/recovery: key baru hanya berlaku dengan evidence lifecycle sah; key lama mengikuti interval dan revocation evidence yang dapat diverifikasi.
  7. Revocation Album Signer tidak membatalkan trust/ownership/license member `.nx`; revocation member tidak mencabut Album Signer.
  8. Tampered manifest, wrong key, malformed signature, wrong subject, wrong scope, issuer substitution, replayed/stale evidence, dan conflicting registry evidence harus memiliki expected result deterministik.
  9. Album membership failure tidak menjadi global playback gate; standalone member playback tetap tunduk pada PE-01 JIT.

- **Status Blocker**: Album Signer Architecture Model B dan pemisahan otoritas telah diputuskan. Kedua kelas subject—Individual Creator dan Organization—telah **`PO APPROVED`** pada 2026-11-10. B-09 tetap **`OPEN / BLOCKED`** hanya untuk concrete identity/key binding, explicit Album Membership Signing authority, Federated Trust resolution/conflict, key custody/lifecycle/freshness, membership verifier, dan negative/adversarial test specification. Implementasi dan test execution tetap menunggu otorisasi implementasi terpisah.


#### 6.7 Rincian NC-07: Batas Keamanan Ekstraksi Arsip ZIP Wrapper (Temuan 5, Spesifikasi Tambahan 3, AUDIT-NEW-06)
- Evaluasi batasan keamanan saat ekstraksi arsip pembungkus ZIP menggunakan pustaka dekompresi streaming:
  1. *Kandidat benchmark ukuran terkompresi* — 500 MB desimal (500.000.000 bytes) adalah input benchmark awal, **bukan hard cap normatif** dan bukan batas yang boleh ditegakkan sebelum evidence B-07 lengkap.
  2. *Kandidat benchmark dekompresi kumulatif wrapper* — 4 GB desimal ($4 \times 10^9$ bytes) adalah input benchmark awal, **bukan hard cap normatif**.
  3. *Batas Payload Individual Kontainer `.nx`*: $\le 2\text{ GiB}$ ($2 \times 1024^3 = 2.147.483.648$ bytes) sesuai batas biner `internal/container/container.go#L106` (`[INSPEKSI LOKAL PROGRAMMER: Go container.go#L106 / NOT VERIFIED BAGI AUDIT INDEPENDEN]`).
  4. *Kandidat benchmark jumlah entri Central Directory* — 200 physical entries adalah input benchmark awal, **bukan hard cap normatif**.
  5. *Rasio kompresi / ZIP-bomb threshold* — 10:1 dan 100:1 tetap kandidat pembanding yang belum diratifikasi. APPNOTE dan RFC 1951 tidak menetapkan ambang keamanan numerik tersebut; tidak satu pun boleh diperlakukan sebagai hard cap sampai metodologi benchmark B-07 menghasilkan evidence yang memadai. Implementasi kelak wajib menghentikan ekstraksi secara fail-closed ketika hard cap yang telah disahkan terlampaui atau ketika `compressed_size == 0` saat `uncompressed_size > 0`, dengan **`ERR_ZIP_BOMB_DETECTED`**.

- **Metodologi B-07 yang telah disetujui PO:** Architecture Authority wajib menyusun dan mengevaluasi benchmark envelope untuk empat kelas payload (Music, Video, Document, Image), threat model, metrik/hasil benchmark, adversarial tests, dan bukti kapasitas sistem. Hard caps per-layer, per-entry, dan cumulative baru ditetapkan setelah seluruh evidence tersebut tersedia. Batas payload individual `.nx` sebesar 2 GiB pada butir 3 tetap domain PE-01 yang terpisah dan tidak boleh disamakan dengan batas ZIP wrapper.

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

1. **Model akuisisi — Commercial Bundle Model B (Independent Member Acquisitions via Commercial Bundle):**
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

**Batas terminologi wajib:** Immutable Checkout Manifest pada NC-08 adalah artefak **Commercial Intent / checkout correlation**. Ia berbeda dari Album Membership Manifest pada NC-01/NC-02/NC-04 yang mendeklarasikan relasi member-to-Album dan ditandatangani Album Signer. Keduanya bukan satu dokumen, bukan satu namespace identitas, bukan satu signature/trust domain, dan tidak saling menggantikan. Bukti atau status salah satunya tidak membuktikan keabsahan yang lain.

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

#### 6.8.4 Keputusan Normatif PO — Partial Fulfillment with Member-Level Recovery untuk Commercial Bundle Checkout

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT POLICY — B-04 / NC-08 / MODEL B**. Product Owner menyetujui Opsi A — **Partial Fulfillment with Member-Level Recovery**. Setiap member dalam satu Commercial Bundle Checkout tetap merupakan unit acquisition dan entitlement yang independen. Kegagalan pemenuhan satu atau beberapa member tidak membatalkan secara otomatis member lain yang telah berhasil dipenuhi.

**A. Prinsip pemenuhan per member**

1. Setiap member yang berhasil dipenuhi mempertahankan acquisition dan entitlement independennya. Sistem tidak boleh menghapus, membatalkan, atau menganggap gagal member yang telah berhasil hanya karena member lain dalam checkout yang sama gagal.
2. Untuk checkout berisi N member, keberhasilan sebagian member adalah **partial fulfillment**, bukan keberhasilan penuh maupun kegagalan total. Contoh: tujuh dari sepuluh member berhasil berarti tujuh member tetap berhasil dan tiga member masih belum terpenuhi/berstatus unresolved sesuai fakta eksekusi.
3. Checkout tidak boleh dinyatakan `FULLY_FULFILLED` sampai seluruh N member dalam Immutable Checkout Manifest terbukti memiliki hasil pemenuhan yang diwajibkan, termasuk acquisition dan entitlement serta status side effect eksternal yang relevan.
4. Manifest tetap immutable dan menjadi SSOT komposisi serta alokasi komersial. Mutable fulfillment status, retry, daemon result, dan reconciliation state dicatat di **durable execution state/receipt per-member** yang terpisah dari Immutable Checkout Manifest; tidak ditulis kembali ke Manifest. Ini konsekuensi keputusan PO mengenai independent member recovery serta durable terminal/refund/exception evidence, bukan keputusan baru yang menunggu approval.
5. Status checkout agregat harus diturunkan dari hasil per-member yang dapat dibuktikan, bukan dari keberhasilan satu payment order, jumlah row yang kebetulan tercatat, atau asumsi bahwa satu transaksi lokal mewakili semua side effect eksternal.

**B. Retry, recovery, dan idempotency**

1. Member yang gagal atau belum dapat dipastikan hasilnya harus dapat diproses melalui retry/recovery pada tingkat member dengan identitas operasi yang stabil dan idempotent. Retry atas satu member tidak boleh membuat acquisition, entitlement, atau grant License Daemon duplikat.
2. Member yang telah terbukti berhasil tidak boleh diproses ulang sebagai operasi baru, diduplikasi, atau di-rollback semata-mata karena member lain gagal.
3. Jika hasil panggilan License Daemon tidak diketahui (misalnya timeout setelah request dikirim), sistem wajib melakukan status lookup/reconciliation menggunakan bukti dan mekanisme yang kelak ditetapkan sebelum mengirim ulang operasi yang berpotensi menggandakan grant. Jangan mengasumsikan timeout berarti operasi eksternal gagal.
4. Kegagalan lokal yang belum commit dapat di-rollback dalam batas transaksi PostgreSQL lokal. Commit lokal tidak dapat di-rollback oleh transaksi SQL yang sama; side effect License Daemon atau payment provider tidak otomatis dibatalkan oleh rollback PostgreSQL. Workflow harus menggunakan durable state, idempotency, retry, dan reconciliation; compensation hanya boleh dilakukan bila operasi eksternal memang menyediakan mekanisme compensation yang terbukti.
5. Ketidakpastian hasil, correlation gap, atau bukti eksekusi yang tidak konsisten harus ditandai eksplisit sebagai unresolved/inconsistent dan tidak boleh dipromosikan menjadi sukses.

**C. Kegagalan permanen dan penyelesaian komersial per member**

1. Jika suatu member terbukti tidak dapat dipenuhi secara permanen setelah recovery yang ditetapkan, penyelesaian komersial dilakukan pada tingkat member yang gagal; keberhasilan member lain tetap dipertahankan.
2. Alokasi `price_amount` member berdasarkan SSP/Largest Remainder pada §6.8.1 menjadi dasar nilai alokasi member untuk perhitungan penyelesaian/refund. Nilai tersebut bukan otomatis jumlah bruto yang diterima gateway apabila pajak, biaya, atau komponen lain dipisahkan.
3. Refund aktual hanya boleh dijanjikan atau ditandai selesai apabila payment provider dan payment flow terbukti mendukung mekanisme refund yang relevan. Dukungan partial refund, batas waktu, fee/tax treatment, serta prosedur kegagalan refund harus ditetapkan dalam kontrak teknis/komersial; belum dianggap tersedia hanya karena kebijakan partial fulfillment disetujui.
4. Jika partial refund tidak didukung, sistem tidak boleh mengarang kemampuan provider atau menyatakan refund telah terjadi. Kasus tersebut harus masuk jalur penyelesaian komersial/manual yang eksplisit dan tercatat, untuk keputusan kebijakan lanjutan bila diperlukan.
5. Keputusan ini tidak menetapkan royalty, payout, tax allocation, atau hak pihak ketiga. Perhitungan tersebut tetap tunduk pada kontrak terpisah; `price_amount` adalah alokasi nilai transaksi per member sebagaimana telah didefinisikan pada §6.8.1.

**D. Kontrak teknis yang masih wajib dirancang dan dibuktikan**

- State machine checkout dan per-member, termasuk state partial, retryable, unresolved, permanently failed, fulfilled, dan commercial resolution/refund; nama enum final belum diputuskan.
- Batas commit lokal, durable execution receipt, relasi payment order, deterministic member-to-acquisition mapping, dan korelasi terhadap Immutable Checkout Manifest.
- Idempotency key/scope untuk checkout, setiap child acquisition, entitlement, payment callback, dan License Daemon operation; replay/restart harus mempertahankan identitas operasi yang sama.
- Reconciliation atas hasil daemon yang diketahui, gagal, atau tidak diketahui; deduplication dan pencegahan double-grant.
- Kriteria kapan kegagalan dapat dinyatakan permanen, batas retry/backoff, operator intervention, serta transisi menuju penyelesaian komersial.
- Kemampuan payment provider untuk partial refund, settlement finality, fee/tax treatment, serta bukti refund dan recovery bila refund gagal.
- Semua mekanisme wajib mematuhi Zero-DDL dan tidak boleh mengasumsikan distributed ACID/2PC atau rollback otomatis atas side effect eksternal.

**E. Dampak dan batas keputusan**

- Kebijakan produk partial fulfillment per member dan recovery member-level telah diputuskan; tidak perlu diajukan ulang sebagai pertanyaan normatif.
- Kontrak teknis yang tercantum pada Bagian D tetap merupakan pekerjaan desain B-04/NC-08 dan harus mempunyai acceptance criteria serta adversarial tests.
- Keputusan ini tidak menyatakan bahwa partial refund, daemon compensation, idempotency, recovery engine, atau state machine tersebut sudah tersedia/terimplementasi.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai kontrak teknis dan bukti implementasinya memenuhi kebijakan ini. Keputusan ini tidak mengubah Zero-DDL, Model B, SSP/Largest Remainder, Immutable Checkout Manifest, baseline Sprint 16/PE-01, atau status **PE-02 Implementation NOT AUTHORIZED**.


#### 6.8.5 Keputusan Normatif PO — Refund sebagai Kewajiban Default untuk Member Permanently Unfulfillable

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT POLICY — B-04 / NC-08 / MODEL B**. Product Owner menyetujui Opsi A: apabila satu member terbukti **permanently unfulfillable** setelah proses recovery yang ditetapkan, NEXA wajib menyelesaikan pengembalian nilai alokasi member tersebut kepada pembeli. Kegagalan pemenuhan member tidak boleh dialihkan menjadi kerugian pembeli hanya karena payment provider tidak menyediakan partial refund otomatis.

**A. Kewajiban penyelesaian**

1. Kewajiban refund berlaku pada tingkat member yang gagal permanen; acquisition dan entitlement member lain yang telah berhasil tetap dipertahankan sesuai §6.8.4.
2. Nilai alokasi `price_amount` member berdasarkan SSP/Largest Remainder (§6.8.1) menjadi dasar nilai refund member. Perhitungan final wajib memperhitungkan perlakuan pajak, biaya, komisi, dan komponen transaksi lain sesuai kontrak komersial serta ketentuan yang berlaku; `price_amount` tidak otomatis sama dengan nilai bruto gateway.
3. Jika payment provider/payment flow mendukung partial refund yang relevan, NEXA harus menggunakan jalur tersebut dan menyimpan bukti hasil refund.
4. Jika partial refund tidak didukung, kewajiban penyelesaian tidak gugur. NEXA wajib menyediakan jalur penyelesaian manual atau mekanisme komersial lain yang sah, eksplisit, dapat diaudit, dan ditelusuri sampai selesai. Sistem tidak boleh mengklaim refund telah terjadi sebelum ada bukti penerimaan/penyelesaian yang memadai.
5. Store credit, saldo internal, voucher, penggantian member, atau bentuk kompensasi non-tunai tidak boleh dipaksakan sebagai pengganti refund. Bentuk tersebut hanya dapat digunakan apabila pembeli secara eksplisit menyetujuinya.
6. Kasus tidak boleh ditandai selesai hanya karena refund diminta atau proses dimulai. Status penyelesaian harus mencerminkan bukti hasil aktual; kegagalan atau ketidakpastian refund tetap menjadi kasus terbuka untuk rekonsiliasi/intervensi.

**B. Batas keputusan dan pekerjaan teknis**

- Keputusan ini menetapkan kewajiban produk NEXA untuk menyelesaikan nilai member yang gagal permanen; keputusan ini tidak membuktikan kemampuan partial refund provider tertentu, tidak menetapkan API/provider, dan tidak mengubah kontrak payment yang sudah ada.
- Desain B-04/NC-08 masih harus menetapkan sumber dana dan jalur pembayaran penyelesaian, otorisasi dan persetujuan pembeli untuk alternatif non-tunai, status serta bukti refund, idempotency, retry/reconciliation refund, perlakuan fee/tax/commission, kegagalan atau timeout provider, dan audit trail.
- Tidak boleh mengasumsikan refund eksternal dapat di-rollback, diduplikasi dengan aman tanpa idempotency, atau selesai hanya berdasarkan timeout/HTTP response yang belum diverifikasi.
- Kewajiban refund ini tidak menghapus kebutuhan untuk menetapkan kriteria permanen gagal, member-level recovery, dan operator intervention pada §6.8.4.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai kontrak teknis/komersial, Zero-DDL persistence, settlement/reconciliation, acceptance criteria, dan adversarial tests ditetapkan serta dibuktikan. Keputusan ini tidak mengubah Model B, SSP/Largest Remainder, Immutable Checkout Manifest, kebijakan Partial Fulfillment, baseline Sprint 16/PE-01, atau status **PE-02 Implementation NOT AUTHORIZED**.


#### 6.8.6 Keputusan Normatif PO — Kriteria Objektif Status PERMANENTLY_UNFULFILLABLE

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT POLICY — B-04 / NC-08 / MODEL B**. Product Owner menyetujui Opsi A: status `PERMANENTLY_UNFULFILLABLE` hanya boleh ditetapkan berdasarkan kondisi terminal yang objektif, dapat diuji, didukung bukti, dan dapat diaudit. Status tersebut bukan keputusan diskresioner operator.

**A. Prasyarat penetapan status terminal**

1. Sistem harus memiliki kriteria terminal yang eksplisit dan dapat diuji untuk jenis kegagalan yang relevan. Kriteria tersebut harus membedakan kegagalan definitif yang tidak dapat dipulihkan dari kegagalan sementara, retryable, dan unresolved.
2. Jalur recovery yang diwajibkan untuk member tersebut harus telah dijalankan sampai batas yang ditetapkan kontrak teknis, atau bukti objektif menunjukkan bahwa jalur recovery terkait memang tidak tersedia/tidak dapat diterapkan. Jumlah retry, backoff, dan kondisi penghentian harus ditentukan dalam desain teknis berdasarkan karakteristik operasi; keputusan PO ini tidak menetapkan angka retry tertentu.
3. Hasil side effect eksternal yang tidak diketahui, termasuk timeout atau koneksi terputus setelah request, wajib direkonsiliasi melalui mekanisme status/evidence yang sah sebelum member dapat dinyatakan gagal permanen. Ketidakpastian bukan bukti kegagalan.
4. Kegagalan sementara, timeout tanpa rekonsiliasi, provider/daemon yang belum merespons, antrean tertunda, atau retry yang belum mencapai kriteria penghentian tidak memenuhi syarat status permanen.
5. Penetapan terminal wajib didukung durable execution evidence/receipt yang mencatat sekurang-kurangnya identitas checkout dan member, tahap operasi, kategori serta kode kegagalan, hasil recovery yang telah dicoba, hasil rekonsiliasi side effect eksternal yang relevan, waktu dan sumber bukti, serta dasar pemenuhan kriteria terminal. Format dan mekanisme persistensinya tetap pekerjaan desain teknis B-04/NC-08 dalam batas Zero-DDL.
6. Jika bukti tidak lengkap, bertentangan, kedaluwarsa ketika freshness diperlukan, atau hasil eksternal masih tidak diketahui, status harus tetap `UNRESOLVED`/status non-terminal yang sesuai; sistem tidak boleh mengubahnya menjadi `PERMANENTLY_UNFULFILLABLE` demi menutup checkout atau memicu refund.

**B. Batas kewenangan operator**

1. Operator boleh memantau, menginvestigasi, memulai recovery yang diizinkan, meminta rekonsiliasi, mengoreksi data operasional melalui prosedur terotorisasi, dan mengeskalasi kasus.
2. Operator tidak boleh melewati, menurunkan, atau menggantikan prasyarat terminal objektif dengan keputusan manual, tekanan waktu, jumlah retry yang belum terpenuhi, atau alasan administratif.
3. Jika operator menemukan bukti baru, sistem harus memproses bukti tersebut melalui jalur validasi/reconciliation yang ditetapkan. Perubahan status hanya terjadi setelah kriteria terminal dievaluasi ulang dan terbukti terpenuhi; bukan melalui override status tanpa bukti.
4. Setiap tindakan operator harus terotorisasi dan memiliki audit trail. Audit trail tidak dengan sendirinya membuat keputusan yang melanggar kriteria menjadi sah.

**C. Hubungan dengan kewajiban refund dan pekerjaan teknis**

- Kewajiban refund default pada §6.8.5 baru dipicu setelah status `PERMANENTLY_UNFULFILLABLE` ditetapkan secara sah berdasarkan kriteria bagian A. Status `UNRESOLVED` tidak boleh memicu penutupan kasus sebagai kegagalan permanen.
- Setelah status permanen sah, kewajiban penyelesaian/refund per member tetap berlaku; operator tidak memiliki diskresi untuk menghapus kewajiban tersebut.
- Desain teknis B-04/NC-08 masih harus menetapkan taksonomi kegagalan, state machine, kriteria retry/backoff dan terminal per kategori, bukti durable, sumber status eksternal, aturan freshness, prosedur rekonsiliasi, kontrol akses operator, audit trail, serta acceptance/adversarial tests.
- Keputusan ini tidak menetapkan angka retry, SLA, nama enum final selain status normatif yang dirujuk, ataupun mekanisme storage tertentu; hal tersebut harus dirancang dan diuji tanpa melanggar Zero-DDL.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai kontrak teknis dan bukti implementasinya memenuhi keputusan ini serta §6.8.1–§6.8.5. Tidak ada perubahan pada baseline Sprint 16/PE-01 atau status **PE-02 Implementation NOT AUTHORIZED**.


#### 6.8.7 Keputusan Normatif PO — Automatic Refund Execution setelah Kriteria Terminal Terpenuhi

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT POLICY — B-04 / NC-08 / MODEL B**. Product Owner menyetujui Opsi A: setelah status `PERMANENTLY_UNFULFILLABLE` ditetapkan secara sah berdasarkan §6.8.6 dan seluruh bukti terminal yang diwajibkan tersedia, sistem NEXA harus secara otomatis memulai proses refund per-member tanpa memerlukan persetujuan manual operator untuk setiap kasus.

**A. Aturan eksekusi otomatis**

1. Pemicu otomatis hanya boleh terjadi setelah validasi status terminal dan bukti durable berhasil; `UNRESOLVED`, timeout yang belum direkonsiliasi, atau bukti yang tidak lengkap tidak boleh memicu refund.
2. Refund dijalankan pada tingkat member yang gagal permanen, berdasarkan kewajiban dan dasar alokasi pada §6.8.5. Keberhasilan member lain tetap dipertahankan sesuai §6.8.4.
3. Eksekusi harus idempotent. Retry, replay, crash recovery, atau pengiriman ulang event tidak boleh menghasilkan refund ganda untuk kewajiban refund yang sama.
4. Jika hasil request refund tidak diketahui, sistem wajib melakukan status lookup/reconciliation melalui sumber pembayaran yang sah sebelum mengirim ulang request. Timeout bukan bukti refund gagal maupun berhasil.
5. Sistem harus menyimpan durable evidence untuk pemicu, otorisasi, request, response/receipt, status akhir, dan setiap upaya rekonsiliasi. Status `REFUND_COMPLETED` hanya boleh digunakan setelah ada bukti penyelesaian aktual yang memadai; request terkirim atau HTTP success saja tidak otomatis membuktikan dana telah diterima pembeli.
6. Jika refund gagal, tertunda, atau hasilnya tidak dapat dipastikan, kasus tetap terbuka dalam status non-terminal yang sesuai dan masuk retry/reconciliation atau eskalasi operasional; kewajiban refund tidak gugur.
7. Operator menangani pengecualian, anomali, kegagalan, dan rekonsiliasi; persetujuan manual operator per kasus bukan prasyarat rutin untuk memulai refund otomatis.

**B. Kontrol dan batas kewenangan**

- Jalur otomatis wajib dibatasi oleh konfigurasi dan otorisasi yang terkontrol, pembatasan nominal/limit yang ditetapkan melalui desain dan kebijakan komersial, pemisahan hak akses, audit trail, serta mekanisme deteksi dan penanganan anomali.
- Perubahan konfigurasi refund, batas nominal, credential/provider, atau kebijakan eksekusi harus melalui otorisasi yang sesuai dan tercatat. Operator tidak boleh mengubah status terminal atau melewati kriteria §6.8.6 untuk memicu refund.
- Jika suatu kasus melampaui limit, melanggar kontrol, atau terdeteksi anomali, sistem harus menahan eksekusi otomatis untuk kasus tersebut dan mengeskalasinya melalui jalur pengecualian yang terotorisasi. Penahanan karena kontrol/anomali tidak menghapus kewajiban refund dan harus memiliki jalur penyelesaian serta audit trail.

**C. Batas keputusan dan pekerjaan teknis**

- Keputusan ini menetapkan automatic initiation/execution sebagai perilaku produk normatif; keputusan ini tidak membuktikan bahwa provider/payment flow saat ini mendukung partial refund, tidak memilih provider/API, dan tidak menetapkan nilai limit atau SLA.
- Desain B-04/NC-08 masih harus menentukan refund state machine, sumber otorisasi dana, provider capability contract, idempotency key/scope, request identity, status lookup, retry/backoff, timeout/unknown-outcome reconciliation, bukti final settlement/refund, penanganan partial/failed refund, limit dan approval konfigurasi, segregation of duties, audit log, serta jalur manual yang sah bila provider tidak mendukung partial refund otomatis.
- Apabila provider tidak mendukung partial refund, kewajiban penyelesaian pada §6.8.5 tetap berlaku melalui jalur manual atau mekanisme komersial sah; sistem tidak boleh mengklaim kemampuan provider yang belum dibuktikan.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai seluruh kontrak teknis, Zero-DDL persistence, acceptance criteria, dan adversarial tests dirancang dan dibuktikan. Keputusan ini tidak mengubah Model B, SSP/Largest Remainder, Immutable Checkout Manifest, §6.8.4–§6.8.6, baseline Sprint 16/PE-01, atau status **PE-02 Implementation NOT AUTHORIZED**.


#### 6.8.8 Keputusan Normatif PO — Mandatory Exception Resolution untuk Refund yang Tertahan

**Status keputusan:** **APPROVED / NORMATIVE PRODUCT POLICY — B-04 / NC-08 / MODEL B**. Product Owner menyetujui Opsi A: setiap refund yang seharusnya dijalankan berdasarkan §6.8.5–§6.8.7 tetapi tertahan oleh limit, kontrol keamanan, anomali, atau kegagalan jalur otomatis wajib menjadi kasus pengecualian yang harus diselesaikan. Penahanan eksekusi bukan pembatalan kewajiban refund.

**A. Pembentukan dan pengelolaan kasus pengecualian**

1. Setiap refund yang tertahan otomatis wajib menghasilkan kasus pengecualian yang durable dan dapat ditelusuri; kasus sekurang-kurangnya mengikat checkout/member, kewajiban refund, alasan/kode penahanan, waktu dan sumber deteksi, status terakhir, serta referensi bukti terkait.
2. Kasus harus masuk antrean penyelesaian yang terpantau dan memiliki pemilik tanggung jawab (assigned owner/role), jalur eskalasi, serta audit trail untuk setiap perubahan status dan tindakan.
3. Kasus tetap terbuka sampai kewajiban refund benar-benar diselesaikan dan hasilnya didukung bukti yang memadai, atau penyelesaian alternatif yang sah telah disetujui secara eksplisit oleh pembeli dan dilaksanakan serta dibuktikan.
4. Kasus tidak boleh ditutup, dihapus, dianggap selesai, atau kehilangan kewajiban hanya karena melewati SLA/tenggat, dipindahkan antrean, berganti pemilik, atau mengalami pergantian operator.
5. Perubahan owner, antrean, prioritas, atau eskalasi tidak boleh mengubah nilai kewajiban, dasar refund, status terminal member, maupun hak pembeli.

**B. Batas kewenangan operator**

- Operator berwenang melakukan investigasi, meminta/melakukan rekonsiliasi, memperbaiki data operasional melalui prosedur terotorisasi, mengeskalasi, dan menjalankan tindakan penyelesaian yang memang diizinkan oleh kontrol akses.
- Operator tidak berwenang menghapus kewajiban refund, menutup kasus tanpa bukti penyelesaian, melewati kriteria terminal §6.8.6, atau mengganti refund dengan store credit, saldo internal, voucher, replacement member, maupun kompensasi non-tunai lain secara sepihak.
- Setiap penyelesaian selain refund uang hanya dapat dilakukan dengan persetujuan eksplisit pembeli yang tercatat dan dapat dibuktikan. Persetujuan tersebut tidak boleh diasumsikan dari diamnya pembeli atau tindakan operator.
- Jika kontrol keamanan atau limit belum dapat dipenuhi, kasus harus tetap tertahan dan dieskalasi melalui jalur yang sah; operator tidak boleh melakukan bypass informal. Kewajiban refund tetap aktif.

**C. Batas keputusan dan pekerjaan teknis**

- Keputusan ini menetapkan kewajiban exception resolution sebagai kebijakan produk; tidak menetapkan SLA numerik, nama status final, struktur antrean, jabatan/role spesifik, atau mekanisme storage tertentu.
- Desain teknis B-04/NC-08 harus menentukan exception state machine, durable case/receipt, ownership dan reassignment, antrean dan prioritas, SLA serta eskalasi, access control/segregation of duties, alasan penahanan dan taxonomy, audit trail, rekonsiliasi, kriteria penutupan, bukti penyelesaian, dan acceptance/adversarial tests di bawah Zero-DDL.
- Penahanan otomatis tidak mengubah status member dari \`PERMANENTLY_UNFULFILLABLE\` dan tidak meniadakan kewajiban refund yang telah dipicu sesuai §6.8.5–§6.8.7. Exception case adalah pengelolaan penyelesaian kewajiban, bukan mekanisme untuk mengubah keputusan produk.
- B-04 / NC-08 tetap **OPEN / BLOCKED** sampai kontrak teknis dan bukti implementasinya lengkap. Tidak ada perubahan pada baseline Sprint 16/PE-01 atau status **PE-02 Implementation NOT AUTHORIZED**.


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

#### 6.15 Rincian NC-15: Taksonomi Reason Code Kanonikal & Provenance Status Normatif (20 kode aktif + 1 label historis deprecated; DEF-05, DEFECT-02)
Dokumen ini memetakan 20 reason code aktif setelah keputusan PO pada §16.21.6: 19 kode dari daftar usulan awal tetap aktif, satu label replay dipertahankan hanya untuk histori (deprecated, tidak diemisi), dan satu kode khusus Genesis ditambahkan berdasarkan persetujuan PO. Tabel memuat 21 label historis/aktif, tetapi tepat 20 reason code aktif. Status provenance setiap kode dibedakan secara tegas:
*Status Provenance Kode Error (DEFECT-02):*
1. **Status provenance:** Reason code Album/PE-02 dalam NC-15 merupakan kontrak spesifikasi AA/PO, bukan klaim bahwa konstanta tersebut sudah ada atau terverifikasi di source. White Paper v5.6 tidak mendefinisikan konstanta string diskrit `ERR_...` sebagai ketentuan normatif beku.
2. **Batas provenance `ERR_ZIP_INVALID`:** Bukti `container.go#L112` yang dicatat pada PSV-06 berkaitan dengan penolakan/truncation kontainer `.nx` individual, bukan bukti adanya ZIP-wrapper reader/extractor. Karena PSV-R07 menyatakan parser/extractor Album tidak ditemukan pada scope, `ERR_ZIP_INVALID` tetap kode usulan NC-15 dan tidak boleh diklaim sebagai error ZIP wrapper yang sudah terverifikasi di source.
3. **Genesis Certificate signature failure — PO APPROVED:** Baseline `sdk.ts#L227-L229` melaporkan generic exception `Signature verification error: ...` dan fail-closed (`canPlay: false`, `is_valid: false`, `status: INVALID`). PO telah menyetujui reason code kontraktual `ERR_GENESIS_SIGNATURE_INVALID` pada boundary verifikasi Genesis Certificate (E-01). Ini keputusan spesifikasi, bukan klaim bahwa konstanta tersebut sudah ada di baseline source. Kode ini dilarang dipetakan ke `ERR_CONTAINER_SIGNATURE_INVALID`, `ERR_MANIFEST_SIGNATURE_INVALID`, atau `ERR_REGISTRY_SIGNATURE_INVALID`.
4. **Preservasi PE-01:** Penambahan reason code tidak mengubah perilaku observable PE-01. Baseline tetap fail-closed mutlak (`canPlay: false`, `is_valid: false`, `status: INVALID`); tidak ada perubahan pemanggil/ekosistem PE-01 yang dibenarkan.

Tabel berikut memuat 20 reason code aktif serta satu label replay historis yang deprecated. Reason code Genesis baru berstatus PO-APPROVED SPECIFICATION; status implementasi/provenance source tetap dibedakan secara faktual:

| Kode Error Diskret | Layer Penghasil | Kondisi Pemicu Diskret | Aksi Sistem | AC Penguji | Status Provenance Sumber (DEFECT-02) |
|---|---|---|---|:---:|:---:|
| `ERR_MANIFEST_MISSING` | Manifest Parser | Manifest entry yang diwajibkan oleh schema/version Album yang kelak disahkan tidak ditemukan; nama file dan lokasi manifest belum ditetapkan normatif | Fail-closed; tolak deklarasi Album | AC-01 | Proposed Specification (NC-15; nama/lokasi manifest masih terbuka pada NC-01) |
| `ERR_MANIFEST_MALFORMED` | Manifest Parser | Sintaksis JSON rusak, regex invalid, escape syntax fail | Fail-closed; tolak manifest | AC-01 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_MANIFEST_DUPLICATE_KEY` | Strict JSON Parser | Ditemukan duplikasi key literal atau via decoded escape | Fail-closed; hentikan parsing | AC-05 | Proposed Specification (NC-15; dependensi modul B-01/NC-03) |
| `ERR_MANIFEST_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature manifest gagal | Fail-closed; tolak deklarasi manifest sebagai sumber membership Album; jangan simpulkan member `.nx` INVALID. Diagnostik standalone hanya untuk file yang disediakan independen, bukan sebagai anggota Album. | AC-03 | Proposed Specification (NC-15; dependensi B-08) |
| `ERR_ALBUM_SIGNER_UNKNOWN` | Trust Store | Identitas/trust signer belum dapat dipastikan | Fail-closed untuk autentisitas membership sesuai CONF-01 yang telah disahkan; bukan global playback block dan bukan status INVALID untuk member standalone. | AC-07 | Proposed Specification (NC-15; membership policy approved, signer lifecycle teknis B-09 masih open) |
| `ERR_ALBUM_SIGNER_UNTRUSTED` | Trust Store | Status signer dinyatakan untrusted/revoked oleh mekanisme Registry yang kelak disahkan (mekanisme saat ini belum ditetapkan) | Jangan gunakan manifest sebagai deklarasi membership tepercaya; jangan otomatis menandai member INVALID atau memblokir playback standalone; mekanisme revocation masih BLOCKED. | AC-08 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_CONTAINER_SIGNATURE_INVALID` | Crypto Engine | Verifikasi Ed25519 signature container individual `.nx` gagal | Fail-closed; tandai trek corrupt | AC-04 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_GENESIS_SIGNATURE_INVALID` | Genesis Certificate verifier (E-01 only) | Verifikasi tanda tangan Genesis Certificate gagal secara definitif pada boundary Genesis; bukan kegagalan signature kontainer, Manifest, atau Registry | Fail-closed; pertahankan `canPlay: false`, `is_valid: false`, `status: INVALID`; jangan mengubah perilaku observable PE-01 | AC-10, AC-26 | PO-APPROVED SPECIFICATION (§16.21.6); not present/verified as a discrete source constant in baseline |
| `ERR_CONTAINER_HASH_MISMATCH` | Integrity Engine | Exact encrypted audio bitstream digest differs from members[].audio_payload_sha256 for a MUSIC_AUDIO member | Fail-closed; laporkan kegagalan digest domain yang tepat; jangan menyamakan dengan Genesis signature failure | AC-09 | NC-05 / §16.12 |
| `ERR_ZIP_INVALID` | ZIP Wrapper Reader / Extractor | Format ZIP corrupt/rusak, central directory invalid, symlink/special file, path traversal, atau benturan nama case-insensitive antar-entri ZIP | Fail-closed; tolak ekstraksi | AC-02, AC-13 | Proposed Specification (NC-15; keberadaan error dengan nama ini pada pemeriksaan `.nx` existing tidak membuktikan adanya ZIP-wrapper extractor Album; PSV-R07 menyatakan parser/extractor Album tidak ditemukan pada scope) |
| `ERR_ZIP_QUOTA_EXCEEDED` | ZIP Wrapper Extractor | Salah satu hard cap archive-level yang telah diratifikasi Architecture Authority terlampaui (compressed bytes, expanded per-entry/cumulative bytes, physical entries, member count, atau CPU/time/memory limit); batas payload `.nx` individual PE-01 dievaluasi terpisah dan tidak otomatis dipetakan ke kode ini | Fail-closed; batalkan ekstrak | AC-13 | Proposed Specification (NC-15; trigger numerik menunggu ratifikasi B-07) |
| `ERR_ZIP_BOMB_DETECTED` | ZIP Wrapper Extractor | Indikator ZIP-bomb yang ditetapkan dalam kontrak B-07 terdeteksi, termasuk rasio per-entry/global yang melampaui threshold yang kelak diratifikasi atau `compressed_size == 0` saat `uncompressed_size > 0` | Fail-closed; batalkan ekstraksi; tindakan karantina hanya jika kelak ditetapkan dalam security handling contract | AC-13 | Proposed Specification (NC-15; threshold rasio menunggu benchmark/ratifikasi B-07) |
| `ERR_ZIP_ENTRY_MISMATCH` | Packaging Validator | Entri berkas reguler ZIP tidak cocok secara bijektif 1:1 dengan deklarasi member dalam manifest (nama manifest, array, dan JSON path belum ditetapkan secara normatif) | Fail-closed; tolak kontainer | AC-02, AC-13 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | Filesystem Safe-Open | Path traversal (`../`), symlink bypass, TOCTOU | Fail-closed; tolak akses fd | AC-20, AC-21 | Proposed Specification (NC-15; dependensi mitigasi B-06) |
| `ERR_PLAYBACK_UNAUTHORIZED` | JIT Authorizer | Tidak ada entitlement aktif / lisensi tidak valid | Fail-closed; tolak playback | AC-22 | Proposed Specification (NC-15 / Error Taxonomy Spec) |
| `ERR_MARKETPLACE_REPLAY_DETECTED` | Transaction Engine | Transaksi dengan idempotency/correlation identity dan immutable request tuple yang sama diajukan kembali | Deprecated historical label; jangan emit sebagai error. Return/reconcile authoritative state dan receipt yang sama secara idempotent | AC-15 | DEPRECATED — retained for historical traceability; not an active emitted reason code |
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
| Ketidakcocokan bijeksi 1:1 deklarasi manifest vs entri ZIP (berkas member yang dideklarasikan tidak ditemukan, atau terdapat entri berkas reguler ekstra/asing yang tidak dideklarasikan) | Packaging Validator | `ERR_ZIP_ENTRY_MISMATCH` | §5.2 Tahap 5; AC-02, AC-13 | AC-02, AC-13 |
| Hard cap compressed-size ZIP wrapper yang telah diratifikasi terlampaui | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | B-07 ratified resource quota; §6.7 | AC-13 |
| Hard cap expanded bytes per-entry atau kumulatif yang telah diratifikasi terlampaui | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | B-07 ratified resource quota; §6.7 | AC-13 |
| Hard cap physical-entry/member count yang telah diratifikasi terlampaui | ZIP Wrapper Extractor | `ERR_ZIP_QUOTA_EXCEEDED` | B-07 ratified resource quota; §6.7 | AC-13 |
| Indikator ZIP-bomb yang ditetapkan B-07 terdeteksi (termasuk compressed-size nol dengan uncompressed-size positif) | ZIP Wrapper Extractor | `ERR_ZIP_BOMB_DETECTED` | B-07 ratified ZIP-bomb detection contract; §6.7 | AC-13 |
| Path traversal saat Safe-Open descriptor filesystem | Filesystem Safe-Open | `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | POSIX.1-2017 `O_NOFOLLOW`; §6.12 | AC-20 |

> **Prinsip Rekonsiliasi Deterministik Bebas Kontradiksi (AUDIT-NEW-06, AUDIT-NEW-08):**
> 1. *Pemisahan Tegas Layer (FINDING-04)*: (a) Anomali fisik kontainer ZIP (arsip rusak, symlink/special file, path traversal fisik, collision nama ZIP) dipetakan ke **`ERR_ZIP_INVALID`** pada ZIP Reader/Extractor; (b) Anomali deklarasi manifes (sintaksis rusak, pelanggaran regex format nama berkas pada nama berkas member yang dideklarasikan pada manifest (path JSON belum ditetapkan), duplikasi nama di manifes) dipetakan ke **`ERR_MANIFEST_MALFORMED`** pada Manifest Validator; (c) Pelanggaran bijeksi 1:1 antara manifes dan ZIP (baik ada berkas manifes hilang di ZIP maupun ada berkas reguler ekstra/asing di dalam ZIP yang tidak dideklarasikan) dipetakan secara eksklusif dan tunggal ke **`ERR_ZIP_ENTRY_MISMATCH`** pada Packaging Validator. Tidak ada tumpang tindih antar-layer.
> 2. *Penerimaan Direktori*: Sesuai keputusan PO (AUDIT-NEW-06), entri direktori di dalam ZIP diterima secara sah dan tidak melempar error.
> 3. *Ketiadaan Fabrikasi Kode Error Baru*: Taksonomi tetap dibatasi tepat pada 20 kode error kanonikal yang ada tanpa penambahan kode baru.
> 4. *Status Provenance Taksonomi*: Taksonomi 20 kode error kanonikal di atas berstatus **Proposed Specification (NC-15)** yang belum dibekukan dalam White Paper v5.6, dan kode diskrit kegagalan tanda tangan Genesis berstatus **Unresolved Taxonomy** (dengan perilaku fail-closed `canPlay: false` pasti).

#### 6.16 NC-16 — status historis formula identifier

Formula child acquisition/entitlement dan provider ID yang pernah dicantumkan pada revisi terdahulu adalah proposal historis dan **bukan kontrak aktif**. Formula yang menggunakan delimiter string, pemotongan digest, atau Album Signer key tidak boleh dipakai sebagai implementasi normatif.

Kontrak aktif NC-16 adalah AA §16.13: member_execution_key dan operation idempotency key menggunakan preimage RFC 8785 JCS yang domain-separated, SHA-256 lowercase hex 64 karakter, dan tidak menggantikan acquisition_id yang diterbitkan existing system. Provider identity tetap domain terpisah; provider_id tidak diturunkan dari Album Signer.

AC-27 hanya menguji formula correlation/idempotency dan receipt mapping. Tidak ada klaim DDL capacity atau collision-free database sebelum source evidence §16.15 membuktikan existing durable receipt/store dan constraint yang relevan.

---

## 7. BLOCKER REGISTER (B-01..B-09) DAN FINDING REGISTER (F-01..F-15)

### 7.1 Blocker Register (B-01 sampai B-09)
Tabel blocker register memisahkan secara eksplisit status spesifikasi, implementasi, dan status blocker:

| ID | Deskripsi Blocker Historis | Status Spesifikasi | Status Implementasi | Status Blocker | Akar Penyebab & Dampak Arsitektur | Syarat Penutupan Sah |
|:---:|:---|:---:|:---:|:---:|:---|:---|
| **B-01** | Parser `JSON.parse` standar menimpa duplicate keys dan parser naif gagal tangani Unicode escape. | `SPECIFIED — AC-01 POLICY / AC-05 TEST CONTRACT READY` | `NOT IMPLEMENTED` | `OPEN / POST-AUTHORIZATION IMPLEMENTATION PENDING` | Strict byte-level parser contract dan duplicate-key/Unicode rejection telah ditetapkan; TypeScript module belum dibangun. Ini build requirement, bukan syarat menyelesaikan source PSV sebelum Gate B. | Setelah Gate B PASS dan otorisasi eksplisit PO, Programmer mengimplementasikan strict byte-level JSON parser mandiri dan menjalankan AC-05/negative vectors. |
| **B-02** | Serializer ad-hoc tidak mengurutkan UTF-16 code units dan salah menangani format $-0$. | `SPECIFIED — RFC 8785 JCS TARGET / AC-06 TEST CONTRACT READY` | `NOT IMPLEMENTED` | `OPEN / POST-AUTHORIZATION IMPLEMENTATION PENDING` | Target RFC 8785 JCS generik telah ditetapkan; TypeScript serializer belum dibangun. Go baseline dan test evidence yang tersedia tidak menggantikan kebutuhan TS parity. Ini build requirement, bukan blocker untuk memulai coding setelah otorisasi. | Setelah Gate B PASS dan otorisasi eksplisit PO, Programmer mengimplementasikan serializer RFC 8785 JCS TypeScript dan menjalankan AC-06/cross-language vectors. |
| **B-03** | Ekstraktor ZIP standar rentan path traversal dan zip-bomb di userspace POSIX. | `AA DESIGN SPECIFIED; B-07 RESOURCE LIMITS PENDING` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY B-07; IMPLEMENTATION POST-AUTHORIZATION` | Streaming extraction, archive validation, staging, descriptor-relative no-follow, post-open validation, atomic promotion, cleanup, and adversarial test design ditetapkan AA §16.6; numeric caps mengikuti benchmark §16.14. | Setelah B-07 capacity evidence tersedia dan Gate B PASS + otorisasi PO terpisah, implementasi dan adversarial tests; tidak perlu PSV ulang atas scope tertutup. |
| **B-04** | Transaksi Marketplace multi-member, satu Commercial Bundle checkout dengan Independent Member Acquisitions, dan konsistensi settlement di bawah Zero-DDL. | `AA TRANSACTION / RECOVERY CONTRACT SPECIFIED; SOURCE-BACKED ZERO-DDL FEASIBILITY OPEN` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY EXISTING STORAGE / RECEIPT PROOF` | Manifest SSOT, per-member durable receipt, member_execution_key/idempotency, state transitions, daemon reconciliation, partial fulfillment, settlement and recovery specified §16.8/§16.13. Existing store, lookup, immutability, concurrency, retention and recovery remain unproven. | Close only when evidence §16.15 proves checkout→member→actual acquisition/entitlement receipt mapping, durability, idempotency, reconciliation and recovery without DDL. No 2PC assumption or new schema. |
| **B-05** | Kontrak acquired_package_sha256 dan child member hash per acquisition/entitlement. | `CHILD .NX BYTE-DOMAIN SPECIFIED BY AA; EXISTING ZERO-DDL FIELD / RECEIPT MAPPING OPEN` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY EXISTING STORAGE MAPPING` | Existing acquired_package_sha256 remains wrapper ZIP hash where source evidence identifies it; AA defines member_sha256 as full physical child .nx SHA-256 §16.3. No field semantic is repurposed. | Prove existing Zero-DDL store can persist/retrieve child hash per member and map it to acquisition/entitlement under §16.15; no PSV repeat. |
| **B-06** | Kerentanan Race Condition Filesystem (TOCTOU) pada akses kontainer Desktop dan Mobile. | `SOURCE PSV CLOSED; MITIGATION / ADVERSARIAL TEST DESIGN OPEN` | `NOT IMPLEMENTED` | `OPEN / BLOCKED` | PSV-R08 telah memetakan call paths Desktop, Android, dan iOS serta menemukan open standar tanpa mitigasi Safe-Open yang memadai pada scope yang diperiksa. Adversarial symlink/TOCTOU tests belum tersedia/tidak dijalankan; mobile runtime fisik belum dijalankan. | Architecture Authority menetapkan mitigasi platform-specific, staging/descriptor containment, threat model, residual-risk statement, serta adversarial test plan/expected results sebelum Gate B PASS. Implementasi dan eksekusi adversarial/runtime tests dilakukan setelah otorisasi. Evaluasi residual risk dilakukan setelah hasil uji; jangan mengulang PSV source review yang sama. |
| **B-07** | Batas ukuran dan kuota ekstraksi arsip pembungkus ZIP. | `BENCHMARK PROTOCOL SPECIFIED BY AA; NUMERIC LIMITS REQUIRE MEASURED EVIDENCE` | `NOT IMPLEMENTED` | `OPEN / BLOCKED BY BENCHMARK / CAPACITY EVIDENCE` | Four-payload dataset, deployment-representative environment, repeatability, metrics, boundary/adversarial suite and evidence format specified §16.14. No numeric cap is normative. | Supply raw benchmark evidence and capacity rationale per dimension under §16.14; then AA ratifies numeric resource envelope. 50 members remains UX guidance only. |
| **B-08** | Manifest signature, canonical signed bytes, and verifier construction | `SPECIFIED — SIGNATURE-STRIPPED JCS / EMBEDDED ED25519 SIGNATURE ENVELOPE` | `NOT IMPLEMENTED` | `OPEN / POST-AUTHORIZATION IMPLEMENTATION & CROSS-LANGUAGE TESTS PENDING` | The manifest JSON contains its `signature` envelope as a property; only that property is excluded when reconstructing RFC 8785 JCS UTF-8 signed bytes. All other schema-approved manifest fields, including signer identity/key reference and ordered members, are signed. The verifier checks strict parsing/schema, reconstructs the exact signed bytes, verifies Ed25519, then resolves signer authority/lifecycle via B-09. Detached signature files and an outer cryptographic envelope are not selected. | After Gate B PASS and explicit PO authorization, implement the embedded envelope verifier and cross-language vectors per §16.4; no implementation completion is required before authorization. |
| **B-09** | Implementasi autentisitas membership Manifest melalui Identity dan Federated Trust Nexa serta lifecycle Album Signer. | `PO-APPROVED PER-ALBUM MEMBERSHIP AUTHORITY; AA SEMANTIC / CARRIER / VERIFIER CONTRACT SPECIFIED; IMPLEMENTATION POST-AUTHORIZATION` | `NOT IMPLEMENTED` | `OPEN / IMPLEMENTATION WORKSTREAM SPECIFIED; POST-AUTHORIZATION WP-04 / WP-05` | Organization Subject ID and root/key lifecycle must preserve WP v5.6 §19.6 / Roadmap v4.8 §5.5. Explicit ALBUM_MEMBERSHIP_SIGNING capability and fail-closed verifier specified §16.5. | Prove existing subject/key binding, issuer/capability evidence, current key/recovery/revocation and federated caller path under §16.15. No new root, endpoint, Registry record, or schema by assumption. |

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
| **REQ-B03-06** | Pemisahan Panduan UX Jumlah Member vs Kuota Entri Fisik ZIP Wrapper | WP v5.6 (50 track sebagai UX guidance); Usulan Spesifikasi NC-07 / B-07 (200 physical entries) | §5.1 Skema Manifest; §6.7 Batas Entri Wrapper | AC-13 (Pengujian kuota wrapper > 200 entri); tidak ada AC untuk menegakkan angka 50 karena angka 50 bukan batas produk | (a) Total entri central directory > 200 fisik dihitung mencakup berkas member, manifest, dan entri direktori: $N_{\text{total}} = N_{\text{tracks}} + N_{\text{manifest}} + N_{\text{dir\_entries}} > 200$; (b) angka 50 hanya memandu UI dan tidak memicu validasi penolakan; (c) nilai 200 tetap usulan teknis sampai ditetapkan Architecture Authority berdasarkan threat model, benchmark, dan kapasitas sistem | (a) Jika batas teknis 200 physical entries kelak ditetapkan dan dilampaui, wrapper ditolak fail-closed dengan `ERR_ZIP_QUOTA_EXCEEDED`; (b) Album dengan lebih dari 50 member tidak boleh ditolak semata-mata karena melewati panduan UX tersebut | `PARTIALLY COVERED — UX GUIDANCE NOT AN ENFORCED LIMIT; TECHNICAL ZIP QUOTA PROPOSED / B-07 BLOCKED` |
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
| **F-03** | Binding Creator / Packaging Authority: pemisahan tiga peran dan otorisasi third-party packaging (AUDIT-NEW-10) | TARGET DESIGN SPECIFIED — IMPLEMENTATION NOT VERIFIED | §5.2; §6.9; §13.12.11; AC-04, AC-10 | Keputusan PO menetapkan tiga peran berbeda dan tidak mewajibkan equality; Genesis Creator adalah ROOT / INITIAL AUTHORITY untuk delegation CONTAINER_PACKAGING dengan satu tingkat subdelegation (L0–L2, Option A). Third-party packager wajib membuktikan delegation; self-packaging tidak memerlukan delegation tambahan. Issuer dan subdelegation telah diputuskan; sisa pekerjaan adalah kontrak teknis, verifier, lifecycle, trusted-time/freshness, dan pengujian. |
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
| **AC-02** | NC-01 | White Paper v5.6; PKWARE APPNOTE; Keputusan PO AUDIT-NEW-06/07/08; NC-01 | Validasi arsip ZIP wrapper: menerima regular files dan directories; menolak symlink dan special files (FIFO, socket, dev) fail-closed (`ERR_ZIP_INVALID`); menolak arsip rusak/truncated (`ERR_ZIP_INVALID`); menolak benturan nama case-insensitive antar-entri ZIP (`ERR_ZIP_INVALID`); menolak deklarasi member dengan nama berkas non-regex atau benturan case-insensitive (`ERR_MANIFEST_MALFORMED`); menolak ketidakcocokan bijeksi 1:1 deklarasi member vs entri ZIP baik berkas hilang maupun berkas reguler ekstra/asing (`ERR_ZIP_ENTRY_MISMATCH`). | Arsip wrapper dan deklarasi dievaluasi sesuai pemetaan 1:1 deterministik. Tipe entri non-reguler (symlink, special files), arsip rusak, dan benturan nama ZIP ditolak fail-closed dengan `ERR_ZIP_INVALID`. Ketidakcocokan bijeksi 1:1 (berkas hilang atau berkas reguler ekstra) ditolak fail-closed dengan `ERR_ZIP_ENTRY_MISMATCH` (AUDIT-NEW-08). | `[TEST-PLANNED — EXECUTION BLOCKED BY NC-01 UNIVERSAL SCHEMA / MANIFEST CONTRACT]` | NC-01 (manifest name/location, member array/path, and universal schema unresolved); B-07 resource quotas are separate under AC-13.
| **AC-03** | NC-02 | IETF RFC 8032; RFC 8785; AA §16.4 | Signed manifest mutation, malformed signature, wrong key, altered member order/name/hash/size, or cross-language JCS mismatch | Signature-Stripped JCS and the embedded Ed25519 signature envelope verify the exact signed fields; mismatch fails with ERR_MANIFEST_SIGNATURE_INVALID | `[TEST-PLANNED — EXECUTION BLOCKED BY IMPLEMENTATION / CROSS-LANGUAGE TESTS]` | B-08 contract specified by AA; implementation and tests post-authorization |
| **AC-04** | NC-06 | IETF RFC 8032; `container.go` | Signature kontainer `.nx` anggota album dimodifikasi | Verifikasi tanda tangan kontainer `.nx` gagal (`ERR_CONTAINER_SIGNATURE_INVALID`). | `[TEST-PLANNED — SPEC READY]` | Baseline Frozen (PE-01) |
| **AC-05** | NC-03 | WP v5.6 §Parsers; Nexa Policy | Payload manifest memuat duplicate keys literal atau via decoded Unicode escape | Parser menolak payload fail-closed dengan error `ERR_MANIFEST_DUPLICATE_KEY`. | `[TEST-PLANNED — BLOCKED BY B-01]` | B-01 (Strict Parser Engine - Implementation Module Pending) |
| **AC-06** | NC-03 | IETF RFC 8785 | Vektor uji kanonisasi RFC 8785 (urutan kunci UTF-16, $-0$, whitespace) | Serializer menghasilkan byte kanonikal identik 100% dengan test vector resmi. | `[TEST-PLANNED — BLOCKED BY B-02]` | B-02 (JCS Serializer Engine - Implementation Module Pending) |
| **AC-07** | NC-04 | White Paper Identity/Federated Trust; PO CONF-01; AA §16.5/§16.16.4A | Unknown signer, unbound key, missing/invalid per-Album authority carrier, album/signer/key/purpose mismatch, stale/conflicting federation evidence, or invalid manifest signature | Album Membership `UNAUTHENTICATED` / `INVALID` fail-closed; standalone PE-01 behavior remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER IMPLEMENTATION]` | PO issuer-authority decision resolved; WP-04/WP-05 implementation and tests post-authorization |
| **AC-08** | NC-04 | Roadmap v4.8 §5.5; White Paper v5.6 §19.6; AA §16.5/§16.15/§16.16.4A/B | Signer key revoked/expired/rotated, invalid recovery lineage, stale/unavailable lifecycle evidence | Membership NOT AUTHENTICATED when required evidence is absent/invalid/unknown; standalone PE-01 remains independent | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 LIFECYCLE / VERIFIER INTEGRATION]` | PO issuer-authority and subject-class decisions are resolved; remaining source-compatibility elements are bounded NOT VERIFIED and Album-specific implementation/tests are post-authorization |
| **AC-09** | NC-05 | White Paper v5.6 §Genesis; AA §16.12 | For each MUSIC_AUDIO member, recompute SHA-256 of exact encrypted audio bitstream from PE-01 payload region and compare with members[].audio_payload_sha256 | Mismatch fails closed with ERR_CONTAINER_HASH_MISMATCH; match only satisfies digest check and grants no playback authorization | `[TEST-PLANNED — SPEC READY]` | Canonical field/path and byte-domain specified AA §16.12; source mapping and runtime tests post-authorization |
| **AC-10** | NC-05 | White Paper v5.6 §Genesis; AUDIT-NEW-10; §13.12.11 | Genesis certificate signature invalid / issuer mismatch; container signature; packaging authorization missing/invalid/expired/revoked; delegation subject or asset mismatch | Verifier reports Genesis ownership and packaging authorization separately. Third-party packaging authorization failure yields UNTRUSTED / UNAUTHORIZED PACKAGING and is not automatically Genesis Certificate invalid or ownership invalid. Genesis error taxonomy remains to be finalized. | [TEST-PLANNED — SPECIFIED; EXECUTION BLOCKED BY IMPLEMENTATION & GENESIS ERROR TAXONOMY] | AUDIT-NEW-10 target architecture specified in §13.12.11; runtime execution awaits implementation and final Genesis taxonomy. |
| **AC-11** | NC-06 | White Paper v5.6 §Container | Ekstraksi kontainer audio mandiri dari arsip ZIP | File terekstrak utuh di storage tanpa merusak byte kanonikal container. (Catatan: AC-11 murni menguji ekstraksi mandiri kontainer; batas payload individual 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106` adalah celah pengujian terpisah yang belum memiliki AC khusus). | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-12** | NC-06 | White Paper v5.6 §Container | Pustaka packaging memvalidasi struktur kontainer hasil ekstraksi | Validasi packaging lulus seluruh invariant integritas baseline PE-01. (Catatan: AC-12 murni menguji invariant packaging PE-01; batas payload individual 2 GiB [$2 \times 1024^3 = 2.147.483.648$ bytes] pada `container.go#L106` adalah celah pengujian terpisah yang belum memiliki AC khusus). | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-13** | NC-07 | PKWARE APPNOTE; RFC 1951; metodologi benchmark B-07 | Arsip ZIP wrapper dievaluasi terhadap hard caps yang telah ditetapkan Architecture Authority setelah benchmark envelope empat kelas payload, threat model, adversarial tests, dan capacity evidence selesai | Ekstraksi dihentikan fail-closed jika compressed-size, expanded per-entry/cumulative, physical-entry, member-count, CPU/time/memory, atau hard cap archive-level lain yang telah diratifikasi terlampaui; batas payload kontainer `.nx` individual tetap diuji terpisah sesuai PE-01; pelanggaran rasio/struktur ZIP yang diklasifikasikan sebagai ZIP-bomb ditolak dengan `ERR_ZIP_BOMB_DETECTED`; kuota yang disahkan terlampaui menghasilkan `ERR_ZIP_QUOTA_EXCEEDED`; ketidakcocokan bijeksi manifest–archive menghasilkan `ERR_ZIP_ENTRY_MISMATCH`. Tidak ada angka hard cap yang ditetapkan oleh AC ini sebelum evidence B-07 disetujui. | `[TEST-PLANNED — SPECIFICATION DEPENDS ON B-07 BENCHMARK / ARCHITECTURE RATIFICATION]` | B-07 (benchmark envelope empat payload, threat model, adversarial tests, dan capacity evidence belum selesai) |
| **AC-14** | NC-08 | PO commercial decisions; AA §16.8/§16.15 | Bundle checkout processes N child acquisitions with partial success, external timeout, daemon uncertainty, terminal failure and automatic refund | Member success preserved; unknown external result reconciled before retry; terminal refund idempotent; no assumed distributed rollback | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED ZERO-DDL FEASIBILITY]` | Transaction/recovery contract specified; durable receipt, mapping and existing-store proof pending B-04 |
| **AC-15** | NC-08 | PO commercial decisions; AA §16.8/§16.13/§16.15 | Repeat checkout/member operation after timeout, crash, callback replay or recovery using identical operation identity | Same operation returns same outcome without duplicate acquisition, entitlement, daemon grant or refund; stable idempotency key reused | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED ZERO-DDL FEASIBILITY]` | Idempotency preimage specified; durable receipt and daemon lookup/reconciliation proof pending B-04 |
| **AC-16** | NC-09 | White Paper v5.6 §Marketplace; AA §16.3/§16.15 | Persist/retrieve child hash per member acquisition/entitlement without changing wrapper hash semantics | member_sha256 is full physical child .nx SHA-256; acquired_package_sha256 remains wrapper-domain where source evidence says so; child hash uses existing Zero-DDL store only if proven | `[TEST-PLANNED — EXECUTION BLOCKED BY EXISTING STORAGE MAPPING PROOF]` | B-05 byte-domain specified; per-member persistence/acquisition mapping pending |
| **AC-17** | NC-10 | `schema.postgres.sql#L63-L115`; Zero-DDL; AUDIT-NEW-05 | Operasi transaksi dan penyimpanan album dieksekusi | Skema database PostgreSQL aktif tidak termutasi pada berkas statis repositori lokal (`schema.postgres.sql`). Keadaan aktual database live/runtime secara terbuka berstatus `NOT VERIFIED — EVIDENCE NOT AVAILABLE`. | `[TEST-PLANNED — SPEC READY]` | Skema DDL Statis Terverifikasi (Runtime Live Database `NOT VERIFIED — EVIDENCE NOT AVAILABLE`) |
| **AC-18** | NC-11 | White Paper v5.6 §Registry | Koneksi ke remote Registry aktif dan respons valid | Verifikasi sertifikat dan public key signer menggunakan data otoritatif remote. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-19** | NC-11 | White Paper v5.6 §Registry | Jaringan transport terputus (ECONNREFUSED/timeout); cache lokal valid | Fallback ke cache offline; respons HTTP 5xx/bad sig melempar fail-closed. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-20** | NC-12 | POSIX.1-2017; `fs_safe.ts` | File `.nx` berada di luar root storage atau symlink melintasi direktori | Akses ditolak fail-closed (`ERR_FILESYSTEM_CONTAINMENT_VIOLATION`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-21** | NC-12 | POSIX.1-2017; Standar POSIX | Upaya pembukaan berkas dengan manipulasi symlink/path traversal | Pemeriksaan descriptor pasca-open gagal; melempar fail-closed (`canPlay: false`). | `[TEST-PLANNED — BLOCKED BY B-06]` | B-06 (Safe-Open POSIX) |
| **AC-22** | NC-13 | White Paper JIT; PO decision; AA §16.1/§16.12/§16.15 | Current/queued Stage 8a digest diagnostics and current-member 8b/8c JIT | Stage 8a may run without 7b/7c for passive digest only; 8b requires 7b+7c+matching digest; 8c only current member after 8b | `[TEST-PLANNED — EXECUTION BLOCKED BY JIT / B-09 INTEGRATION]` | Stage 8a and digest field contract closed; B-09 source integration pending |
| **AC-23** | NC-13 | White Paper v5.6 §JIT Player | Pengguna berpindah trek audio dalam album | Otorisasi JIT dieksekusi ulang secara independen per trek tanpa otorisasi massal. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-24** | NC-13 | White Paper v5.6 §JIT Player | Integritas satu trek dalam antrean album rusak | Trek rusak gagal diputar; pemutaran trek valid lainnya tidak terganggu. | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **AC-25** | NC-14 | White Paper v5.6 §Verify; Keputusan PO CONF-02; §5.3 | Verifikasi album dengan anggota valid dan status campuran di NX Verify | Mengikuti Keputusan PO (CONF-02 / NC-14 Pilihan B APPROVED): NX Verify tidak menampilkan status agregat keseluruhan Album; hasil verifikasi setiap berkas `.nx` anggota ditampilkan secara individual; tidak ada pembuatan status agregat baru (`ALBUM_TRUSTED`, `ALBUM_INVALID`) | `[TEST-PLANNED — SPEC READY]` | Keputusan PO CONF-02 / NC-14 Pilihan B APPROVED (Tanpa Status Agregat) |
| **AC-26** | NC-15 | Error Taxonomy Spec; NC-15; §16.21.6 | Skenario kegagalan sistematis di seluruh alur eksekusi | Setiap kondisi menghasilkan reason code aktif sesuai trigger dan producer layer deterministik; replay idempotent mengembalikan receipt/state, bukan error. | `[TEST-PLANNED — SPECIFIED; IMPLEMENTATION / TEST PENDING AUTHORIZATION]` | NC-15 contract closed; source implementation and runtime test pending. |
| **AC-27** | NC-16 | AA §16.13; source/DDL evidence §16.15 | Recompute member_execution_key and operation idempotency key from exact JCS preimages; verify receipt maps to actual acquisition_id | Identical checkout/member/operation yields identical key; distinct members never overwrite; acquisition_id remains existing-system-issued; no new DDL assumed | `[TEST-PLANNED — EXECUTION BLOCKED BY RECEIPT / DDL COMPATIBILITY EVIDENCE]` | Formula specified by AA; durable receipt/storage proof remains B-04 dependency |
| **AC-28** | NC-01, NC-06 | White Paper Studio; PO §2.3.A; AA §16.2/§16.15 | Forge New Album sources sequentially and persist ordered member association | Canonical Album identity/member contract specified; existing store must preserve association, order, reload and recovery without DDL | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED PERSISTENCE FEASIBILITY]` | NC-06 source evidence pending; no schema/API invention |
| **AC-29** | NC-06 | White Paper Studio; PO §2.3.B; AA §16.2/§16.15 | Publish existing .nx files sequentially and reload as one Album entity | Existing pipeline and child .nx bytes unchanged; Album identity/member relation survives reload/recovery without DDL | `[TEST-PLANNED — EXECUTION BLOCKED BY SOURCE-BACKED RELOAD FEASIBILITY]` | NC-06 source evidence pending |
| **AC-30** | NC-01 | Keputusan PO §2.3.C (Larangan Album Campuran); §5.4 | Pengguna memasukkan kombinasi campuran berkas sumber biasa dan berkas `.nx` yang sudah ada ke dalam satu Album | Validasi jenis masukan menolak proses secara fail-closed sebelum workflow pemrosesan dimulai; masukan tidak dirusak atau dihapus; tidak ada silent conversion atau reklasifikasi jenis masukan sepihak | `[TEST-PLANNED — SPEC READY]` | Keputusan PO §2.3.C (Larangan Album Campuran) |
| **AC-31** | NC-01, NC-06 | Keputusan PO §2.4 (Failure Handling Studio); §5.5 | Terjadi kegagalan pemrosesan pada tahap forging atau tahap upload di NX Studio | Pemrosesan berhenti sementara pada tahap yang gagal; tidak ada auto-retry tanpa batas atau auto-skip; pengguna disajikan opsi diskrit "Ulangi" dan "Lewati"; jika forging gagal dan dipilih Ulangi: forging file yang sama diulang tanpa lanjut ke file berikutnya; jika forging gagal dan dipilih Lewati: file dilewati tanpa upload dan tanpa menghapus file sumber; jika upload gagal setelah forging berhasil dan dipilih Ulangi: upload berkas `.nx` hasil forging diulang tanpa re-forging (menggunakan output `.nx` di staging lokal) dan tanpa membuat listing Marketplace duplikat (hasil yang disetujui PO); mekanisme teknis idempotensi session individual belum ditetapkan sebagai kontrak dan bukti repository hanya laporan Programmer yang belum diverifikasi independen (`server.js#L2400-L2416, L2467-L2470`, `publish_pipeline.js#L316-L410`; status bukti implementasi: inspeksi kode lokal Programmer / audit independen pending [NOT VERIFIED — PRIMARY SOURCE EVIDENCE NOT AVAILABLE], pengujian runtime belum dilakukan, terpisah dari transaksi B-04); jika upload gagal dan dipilih Lewati: tahap upload ditandai gagal/dilewati, lanjut ke anggota berikutnya, berkas sumber dan hasil `.nx` tetap dipertahankan; status forging dan status upload dibedakan secara granular per anggota | `[TEST-PLANNED — SPEC READY]` | Keputusan PO §2.4 (Studio Failure Handling: Ulangi & Lewati; Spesifikasi Idempotensi Session Siap; Terpisah dari B-04) |
| **AC-32** | NC-13 | White Paper Universal Viewer; PO §2.5; AA §16.11/§16.15 | Player advances after current viewer emits definitive completion | Normalized VIEWER_COMPLETED, stale/duplicate rejection, resource release and fresh JIT specified; platform/payload source feasibility and parity tests remain required | `[TEST-PLANNED — EXECUTION BLOCKED BY VIEWER SOURCE FEASIBILITY / TESTS]` | AA lifecycle contract specified; source evidence and platform tests pending |
| **AC-33** | NC-14 | White Paper v5.6 §Verify Desktop; Keputusan PO §2.6, §2.7; §5.3 | Pengguna membuka Album pada NX Verify Desktop; membership authenticity must pass the PO-approved fail-closed verifier before file is processed/labeled as an Album member | Jika autentisitas membership terbukti, Verify memproses anggota pertama dan menampilkan hasil verifikasi individual; jika belum terbukti, file dari manifest tidak diproses/dilabeli sebagai anggota Album; file yang diberikan independen hanya dapat diverifikasi sebagai standalone PE-01; pengguna menekan tombol "Next" secara manual untuk beralih ke anggota berikutnya; setiap anggota diverifikasi sendiri-sendiri tanpa status agregat keseluruhan Album (Option B APPROVED); fitur Full Verify Desktop existing (Batch Verification, Export Report, manual Registry Refresh) tetap utuh dan tersedia; Verify tidak memberikan playback authorization | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER / SIGNER LIFECYCLE]` | Keputusan PO §2.6 & §2.7 (Verify Desktop Manual Next & No Aggregate Status) |
| **AC-34** | NC-14 | White Paper v5.6 §Verify Mobile Lite; PO §2.6/§2.7; §5.3 | NX Verify Mobile opens an Album; membership authenticity must pass before files are processed/labeled as Album members | If authenticated, Verify processes one member per step; otherwise manifest files are not processed as Album members. Independently supplied files remain standalone PE-01. Manual Next only; no aggregate Album status; Verify-Lite excludes Desktop batch verification, export, manual Registry refresh and payload rendering | `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER / SIGNER LIFECYCLE]` | PO §2.6/§2.7 (Verify Mobile Lite Manual Next & Lite Isolation)
---


Matriks berikut mendokumentasikan keterlacakan dua arah (*Forward & Reverse Traceability*) dengan struktur tabel markdown valid dan rujukan dependensi yang realistis tanpa klaim semu:

| ID NC | ID AC Penguji | Sumber Otoritatif | Bukti Pendukung / Lokasi Kode | Status Kesiapan AC | Status Blocker / Keputusan |
|:---:|:---:|:---|:---|:---:|:---:|
| **NC-01** | AC-01, AC-02, AC-28, AC-30, AC-31 | White Paper v5.6 §Manifest/Studio; RFC 8259; PO decisions; AA §16.2/§16.12 | §5.1; §16.2; §16.12 | AC-01/02 `[TEST-PLANNED — EXECUTION BLOCKED BY COMPLETE SCHEMA / ENVELOPE]`; AC-28 `[TEST-PLANNED — SOURCE FEASIBILITY BLOCKED]`; AC-30/31 `[TEST-PLANNED — SPEC READY]` | Strict unknown-field rejection approved; ordered members[] and payload_type/audio field contract specified. Remaining NC-01 gaps: complete machine-validatable nested schema/version rules, exact ZIP Manifest entry name/location, and parser/validator implementation. NC-06 persistence is separately evidence-blocked |
| **NC-02** | AC-03 | IETF RFC 8032; RFC 8785; AA §16.4 | §6.2; signed-content contract | `[CONTRACT SPECIFIED BY AA; IMPLEMENTATION / TESTS POST-AUTHORIZATION]` | Exact signed field set, JCS byte domain, embedded Ed25519 signature envelope, verifier flow and cross-language vectors specified §16.4 |
| **NC-03** | AC-05, AC-06 | White Paper v5.6 §Parsers; IETF RFC 8785 | RFC 8785 Test Vectors TV-01..TV-08 | AC-05 `[BLOCKED B-01]`; AC-06 `[BLOCKED B-02]` | B-01, B-02 (Strict Parser & JCS - Implementation Modules Pending) |
| **NC-04** | AC-07, AC-08 | Roadmap v4.8 §5.5; White Paper v5.6 §19.6; PO CONF-01; AA §16.5 | Roadmap organization identity invariants; §16.5/§16.15 | AC-07 `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER IMPLEMENTATION]`; AC-08 `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 LIFECYCLE / VERIFIER IMPLEMENTATION]` | Subject classes and fail-closed membership policy approved; per-Album issuer authority and carrier/verifier semantics specified by PO/AA; implementation and source integration remain post-authorization |
| **NC-05** | AC-09, AC-10 | White Paper v5.6 §Genesis; AA §16.12; AUDIT-NEW-10 | §6.9; §16.9/§16.12; E-01 | AC-09 `[TEST-PLANNED — SPEC READY]`; AC-10 `[TEST-PLANNED — EXECUTION BLOCKED BY GENESIS ERROR TAXONOMY / IMPLEMENTATION]` | Audio digest field/path and byte-domain specified by AA; Genesis error taxonomy remains separate residual |
| **NC-06** | AC-04, AC-11, AC-12, AC-28, AC-29, AC-31 | White Paper v5.6 §Container, §Studio; Keputusan PO §2.3, §2.4; `container.go` | `internal/container/container.go#L110`; §5.1, §5.4, §5.5; E-02 | AC-04, AC-11, AC-12, AC-31 `[TEST-PLANNED — SPEC READY]`; AC-28, AC-29 `[TEST-PLANNED — EXECUTION BLOCKED PENDING ALBUM IDENTITY/RELOAD]` | Baseline Frozen (PE-01); Keputusan PO APPROVED (Failure Handling Retry/Skip, hasil `.nx` yang sama tanpa re-forging, larangan listing duplikat; mekanisme idempotensi teknis unresolved; gap identitas & reload terbuka) |
| **NC-07** | AC-13 | PKWARE APPNOTE; RFC 1951; B-07 benchmark methodology | §6.7 Batas Keamanan Ekstraksi Arsip ZIP Wrapper | AC-13 `[TEST-PLANNED — SPECIFICATION DEPENDS ON B-07 BENCHMARK / ARCHITECTURE RATIFICATION]` | B-07 (benchmark envelope empat payload, threat model, adversarial tests, dan capacity evidence belum selesai); AC-02 belongs to NC-01 universal manifest contract, not B-07. |
| **NC-08** | AC-14, AC-15 | PO commercial decisions; AA §16.8/§16.13/§16.15 | `marketplace/server.js` reported; source/DDL proof required | `[AA CONTRACT SPECIFIED — SOURCE-BACKED ZERO-DDL FEASIBILITY BLOCKED]` | Checkout/member execution state, idempotency, receipts, reconciliation and recovery specified; durable store and actual acquisition mapping must be proven under §16.15 |
| **NC-09** | AC-16 | White Paper v5.6 §Marketplace; AA §16.3/§16.15 | §6.9; E-03; §15.9.5 | `[CHILD HASH CONTRACT SPECIFIED — EXISTING STORAGE MAPPING BLOCKED]` | Child .nx byte-domain specified; acquired_package_sha256 remains wrapper-domain where source evidence says so; Zero-DDL child hash persistence proof required |
| **NC-10** | AC-17 | `schema.postgres.sql#L63-L115` | `marketplace/db/schema.postgres.sql#L63`; E-03 | `[TEST-PLANNED — SPEC READY]` | Laporan Programmer tentang DDL statis (belum diverifikasi independen) (Independen B-04; Runtime Live DB `NOT VERIFIED`)|
| **NC-11** | AC-18, AC-19 | White Paper v5.6 §Registry | White Paper v5.6 §Offline Fallback | `[TEST-PLANNED — SPEC READY]` | Tidak ada |
| **NC-12** | AC-20, AC-21 | POSIX.1-2017; White Paper v5.6 §Safe-Open | `sdk/typescript/src/fs_safe.ts#L30-L55`; E-07 | AC-20 `[TEST-PLANNED — EXECUTION BLOCKED BY B-06]`; AC-21 `[TEST-PLANNED — EXECUTION BLOCKED BY B-06]` | B-06 (Batas Safe-Open Filesystem Desktop Terbuka; Residual Gap TOCTOU POSIX) |
| **NC-13** | AC-22, AC-23, AC-24, AC-32 | White Paper v5.6 §JIT/Universal Viewer; PO §2.5; AA §16.1/§16.11/§16.15 | §5.2; E-05; §16.15 | AC-22 `[TEST-PLANNED — JIT / B-09 INTEGRATION BLOCKED]`; AC-23/24 `[TEST-PLANNED — SPEC READY]`; AC-32 `[TEST-PLANNED — VIEWER SOURCE FEASIBILITY BLOCKED]` | Stage 8a permission and Auto-Next event semantics specified; B-09 integration and definitive per-platform/payload completion source remain to be evidenced |
| **NC-14** | AC-25, AC-33, AC-34 | White Paper v5.6 §Verify; Keputusan PO §2.6, §2.7 (CONF-02 Pilihan B APPROVED) | §5.3 Tiga Lapisan Status Verify | AC-25 `[TEST-PLANNED — SPEC READY]`; AC-33/AC-34 `[TEST-PLANNED — EXECUTION BLOCKED BY B-09 AUTHORITY CARRIER / VERIFIER / SIGNER LIFECYCLE]` | Keputusan PO CONF-02 / NC-14 Pilihan B APPROVED (Tanpa Status Agregat Album; Kategori Diagnostik Internal Tunduk pada 4 Status Kanonikal; Verify Desktop & Mobile Lite Terpisah) |
| **NC-15** | AC-26 | Error Taxonomy Spec; NC-15 | §6.15 Taksonomi 20 Kode Error Kanonikal | `[TEST-PLANNED — BLOCKED BY PROPOSED SPEC]` | Usulan Spesifikasi Teknis NC-15 (Pending Pembekuan Arsitektur) |
| **NC-16** | AC-27 | AA §16.13; DDL/source evidence §16.15 | §16.13 | `[FORMULA SPECIFIED BY AA — RECEIPT / DDL COMPATIBILITY BLOCKED]` | member_execution_key and operation idempotency JCS preimages specified; no acquisition_id replacement or new DDL; actual durable receipt mapping remains B-04 evidence dependency |

---

## 10. STATUS KEPUTUSAN PRODUCT OWNER DAN RESIDUAL AUTHORITY

### 10.1 CONF-01 Disahkan — Identitas dan Lifecycle Album Signer sebagai Gap Teknis (NC-04, B-09, AUDIT-TRUTH-02)
Kebijakan produk CONF-01 telah disahkan PO: manifest dengan signer `UNKNOWN` atau signature invalid tidak mengautentikasi membership Album. Tidak ada PO decision blocker yang tersisa untuk kebijakan ini. Desain identity binding, authority, trust store, lifecycle, rotation, revocation, freshness, dan verifier merupakan pekerjaan teknis B-09/NC-04; PSV-R10/R10A telah ditutup pada tingkat bukti yang dilaporkan di §15.11.3. **CONF-01 bukan pilihan kebijakan playback global.**

1. **Evaluasi Kebutuhan Entitas Album Signer**:
    - Album Signer hanya mengautentikasi deklarasi manifest dan daftar anggota; identitas/lifecycle signer serta mekanisme Registry yang sah tetap merupakan kontrak teknis B-09/NC-04, bukan keputusan PO yang masih tertunda.
   - Album Signer **DILARANG** menggantikan Creator signature, Genesis proof, Registry trust, asset trust, active license, atau otorisasi playback masing-masing member `.nx`.
    - Dasar identitas, private-key custody, pendaftaran public key ke Registry, identity binding, key rotation, revocation, dan freshness belum ditetapkan sebagai kontrak teknis (**`OPEN — ARCHITECTURE / IMPLEMENTATION GAP B-09`**); jangan menciptakan endpoint/record/field baru tanpa dasar dan otorisasi.

2. **Batas Keputusan CONF-01 untuk Signer `UNKNOWN`**:
    - Kebijakan CONF-01 telah diputuskan: manifest signer `UNKNOWN` tidak dapat mengautentikasi membership Album. Tidak ada keputusan PO yang masih diperlukan untuk pilihan tersebut; desain identity/lifecycle signer tetap terbuka sebagai pekerjaan teknis B-09/NC-04.
   - Otorisasi playback tetap dilakukan secara JIT dan independen untuk setiap member berdasarkan kontrak PE-01, Creator signature, Genesis ownership, Registry evidence, dan active license yang berlaku.
   - Programmer **DILARANG** memilih opsi yang memblokir atau mengizinkan seluruh playback Album atas dasar status Album Signer.
   - Sesuai keputusan PO CONF-01, membership dari manifest dengan signer `UNKNOWN` tidak boleh dianggap autentik; kebijakan fail-closed telah diputuskan, sedangkan implementasi identity/lifecycle signer tetap terbuka. Namun status tersebut juga **TIDAK BOLEH** otomatis mengubah status member menjadi `INVALID` atau membatalkan trust member.

3. **Preservasi Prinsip White Paper v5.6**:
   - Status `UNKNOWN / INCOMPLETE` **BUKAN `INVALID`**.
   - Integritas kontainer dan tanda tangan Creator setiap member tetap independen dari status signer manifest.
   - Tidak boleh menciptakan Registry endpoint, record sintetis, revocation list, key lifecycle, atau mekanisme fallback yang belum memiliki dasar kontrak.

> **Status Tata Kelola:** Kebijakan CONF-01 (Album Membership Authenticity Fail-Closed) telah disahkan PO. Tidak ada PO decision blocker untuk kebijakan signer UNKNOWN; identity binding, authority, trust store, dan lifecycle signer tetap merupakan gap teknis B-09/NC-04. Residual PSV telah ditutup pada §15.11.3; tidak ada PSV ulang kecuali ada pertanyaan source-level baru yang spesifik dan material. CONF-01 bukan pilihan global playback.

### 10.2 Pembekuan Parameter Kuota Ekstraksi ZIP & Rekonsiliasi Celah Pengujian (B-07, NC-07, REQ-B03-04..06)
1. **Rasio Dekompresi ZIP Bomb (REQ-B03-04):** PSV-R07 telah diselesaikan pada scope source review yang dicatat di §15.9.7/§15.11.3; tidak perlu meminta Programmer mengulang pemeriksaan parser/extractor atau pencarian enforcement yang sama. Bukti yang tersedia membedakan batas container `.nx` dari kuota wrapper ZIP dan tidak membuktikan bahwa kuota wrapper telah ditegakkan. Architecture Authority menetapkan compressed/expanded per-entry dan kumulatif, expansion ratio, jumlah physical entries, kapasitas jumlah member teknis, ukuran `.nx` individual, serta CPU/time/memory/resource hard caps berdasarkan **benchmark envelope empat jenis payload (Music, Video, Document, Image)**, threat model, dan kapasitas sistem. Benchmark harus mengukur distribusi ukuran payload dan wrapper, compressed/expanded bytes, rasio kompresi, waktu ekstraksi, CPU, memory/resource consumption, serta perilaku pada kondisi batas. Rasio 10:1 dan 100:1 tetap kandidat, bukan nilai normatif. Hard cap per lapisan baru ditetapkan setelah hasil benchmark dan pengujian adversarial tersedia.
2. **Batas Ukuran Wrapper dan Payload Individual (REQ-B03-05):** Gunakan hasil PSV-R07 yang telah dicatat; tidak perlu PSV ulang atas source scope yang sama. Bukti 2 GiB yang tersedia berkaitan dengan batas payload kontainer `.nx` di Go, bukan bukti kuota expanded wrapper ZIP. Architecture Authority menetapkan batas compressed wrapper, expanded cumulative wrapper, dan payload individual `.nx` berdasarkan benchmark envelope empat jenis payload, threat model, serta kapasitas sistem; semua harus diukur dan diuji secara terpisah. Hard cap per lapisan ditetapkan setelah benchmark dan pengujian adversarial, bukan sebelum evidence tersebut tersedia. Jangan menyatakan batas yang tidak ditemukan pada source sebagai implemented.
3. **Panduan UX 50 Member vs Kuota Teknis ZIP (REQ-B03-06):** PSV-R07 telah memeriksa scope source terkait; tidak perlu pengulangan. Keputusan PO telah ditetapkan: 50 member hanya UX guidance, bukan hard product limit; Album dengan jumlah member di atas 50 tidak boleh ditolak semata-mata karena melewati angka tersebut. Pisahkan panduan UI dari jumlah entry fisik ZIP. Nilai 200 physical entries, batas member teknis aktual, kuota lainnya, dan enforcement resource merupakan keputusan Architecture Authority berdasarkan threat model, benchmark, dan kapasitas sistem.
4. **Metode penetapan B-07 (PO APPROVED):** gunakan benchmark envelope yang mencakup empat jenis payload Nexa—Music, Video, Document, dan Image. Ukur compressed/expanded size (per-entry dan kumulatif), compression ratio, physical ZIP entries, jumlah member, ukuran `.nx` individual, CPU, waktu ekstraksi, memori, dan resource consumption pada kondisi normal, batas, serta adversarial. Architecture Authority menetapkan hard cap per lapisan hanya setelah threat model, hasil benchmark, pengujian adversarial, dan kapasitas sistem dianalisis. Nilai usulan tetap `PROPOSED / NOT NORMATIVE` sampai proses itu selesai. Angka 50 tetap UX guidance saja; bukan batas validasi/penolakan.



**Metode benchmark B-07 — PO APPROVED:** Architecture Authority wajib menggunakan benchmark envelope empat jenis payload Nexa (Music, Video, Document, Image). Benchmark mencakup ukuran dan distribusi payload/wrapper, compressed bytes, expanded bytes per-entry dan kumulatif, compression ratio, physical ZIP entry count, jumlah `.nx` members, ukuran individual `.nx`, waktu ekstraksi, CPU, memori, dan resource consumption. Pengujian meliputi workload representatif, kondisi batas, serta adversarial ZIP bomb, entry flooding, path traversal, duplicate/case-fold collision, symlink/special files, dan resource exhaustion. Hasil benchmark dan threat model menjadi dasar penetapan hard cap terpisah per lapisan, enforcement point, error behavior, margin keselamatan, serta acceptance/adversarial test criteria. Tidak ada angka usulan yang menjadi normatif sebelum keputusan teknis tersebut terdokumentasi.

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

### 10.3.1 Keputusan PO — 50 Album Members sebagai UX Guidance (REQ-B03-06 — RESOLVED)

1. Product Owner menetapkan bahwa angka **50 Album members hanya merupakan UX guidance**, bukan hard product limit, bukan batas validasi manifest, dan bukan dasar penolakan Album.
2. Album dengan lebih dari 50 member tetap dapat diterima sepanjang memenuhi seluruh batas teknis yang berlaku; angka 50 sendiri tidak boleh memicu `REJECT` atau `ERR_*`.
3. Architecture Authority menetapkan batas teknis jumlah member dan seluruh kuota ekstraksi ZIP berdasarkan threat model, benchmark, serta kapasitas sistem. Penetapan harus membedakan compressed size, expanded per-entry/kumulatif, physical ZIP entries, jumlah member, ukuran `.nx` individual, CPU, waktu, dan resource limits.
4. Setiap batas teknis harus memiliki unit, enforcement point, perilaku fail-closed, rationale, benchmark evidence, dan acceptance/adversarial tests. Angka usulan yang belum ditetapkan tetap `PROPOSED / NOT NORMATIVE`.
5. Keputusan ini tidak mengesahkan angka 200 physical entries, `maxItems: 199`, atau nilai kuota lain sebagai batas final; semuanya tetap tunduk pada penetapan teknis Architecture Authority.

### 10.4 Status Keputusan AUDIT-NEW-10 — Authority dan Delegation Telah Diputuskan

**Keputusan PO AUDIT-NEW-10: APPROVED / RESOLVED pada tingkat semantik produk.** genesisPubKey adalah Genesis Creator/originator dan menandatangani Genesis Ownership Certificate; containerSigKey adalah Container Packager/Packaging Engine dan menandatangani integritas binary container .nx; ownCertPubKey adalah current holder/buyer/collector sebagai subjek hak kepemilikan/lisensi saat ini. Ketiganya adalah peran berbeda dan tidak diwajibkan identik.

ownCertPubKey dapat berbeda dari genesisPubKey apabila rantai transfer kepemilikan sah menghubungkan keduanya. Third-party packaging dengan containerSigKey != genesisPubKey wajib memiliki delegation/authorization evidence yang dapat diverifikasi. Tanpa bukti tersebut, packaging dinyatakan UNTRUSTED / UNAUTHORIZED PACKAGING, sekalipun signature matematis valid. Self-packaging dengan containerSigKey == genesisPubKey memiliki otoritas inheren dan tidak memerlukan delegation tambahan. Signature kontainer membuktikan integritas matematis, bukan dengan sendirinya hak cipta atau otoritas packaging.

Keputusan PO telah menetapkan Genesis Creator sebagai satu-satunya ROOT / INITIAL AUTHORITY untuk menerbitkan delegation `CONTAINER_PACKAGING`, dengan satu tingkat subdelegation (hierarki maksimum L0–L2) sesuai Option A. Immutability mandat, syarat parent permission, terminal L2, larangan L3, explicit revocation, dan Dual-Horizon Time Rule juga telah diputuskan serta dirinci pada §13.12.11. Tidak ada lagi pertanyaan normatif PO yang tertunda mengenai issuer authority atau subdelegation. Sisa pekerjaan adalah kontrak teknis, verifier, canonical payload/JCS, test vectors lintas TypeScript/Go, lifecycle evidence, trusted-time/recorded_at, freshness, dan implementasi/pengujian; ini bukan PSV ulang atas keputusan yang telah disahkan.

Lifecycle revocation, freshness, dan offline disposition harus mengikuti keputusan Dual-Horizon Time Rule serta batas offline yang telah disahkan pada §13.12.11. Detail clock, receipt evidence, freshness, reason codes, dan cross-language test vectors tetap pekerjaan teknis; perubahan perilaku produk hanya dieskalasikan bila desain menemukan konflik nyata dengan keputusan yang telah disahkan.

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
- **G-01 (Fact-Based Plan Verification)**: `CONDITIONALLY MET — DOCUMENT REVIEW ONLY` (Plan memuat laporan Programmer tentang inspeksi lokal pada Evidence Ledger; AA belum memverifikasi repositori/bukti primer secara independen. Status ini bukan klaim inspeksi source oleh AA).
- **G-02 (Empirical Evidence Verification)**: `CONDITIONALLY MET — BASED ON PROGRAMMER-REPORTED STATIC INSPECTION ONLY` (Klaim inspeksi kode statis merupakan evidence yang diserahkan Programmer; AA menilai konsistensi dan batas buktinya tanpa mengakses source; pengujian fisik mobile tetap `NOT VERIFIED`).
- **G-03 (Repository Evidence Ledger Provenance)**: `CONDITIONALLY MET — EVIDENCE PROVENANCE NOT INDEPENDENTLY VERIFIED` (Evidence Ledger §4.4 memuat path, baris, dan raw snippets yang dilaporkan berasal dari kode lokal; AA tidak mengakses repository source `whisnu/nexa` dan tidak mengklaim verifikasi source independen. E-07, database live, dan runtime mobile tetap tunduk pada batas bukti masing-masing).
- **G-04 (Preservation Gate Synchronization)**: `CONDITIONALLY MET` (Diselaraskan dengan evaluasi konservatif D-01 s.d. D-07 pada §12.1; kesimpulan preservasi berstatus PARTIAL; pengujian runtime fisik berstatus NOT VERIFIED).
- **G-05 (Readiness Conclusion Cross-Check)**: `CONDITIONALLY MET` (Rekapitulasi aktif setelah rekonsiliasi AC-27: 12 Spec Ready + 22 Execution Blocked + 0 PO Decision Required = 34 AC. AC-01 menunggu universal schema/parser; AC-07 telah mendapat keputusan PO mengenai per-Album Membership Authority; implementasi dan pengujian tetap pascaotorisasi. AC-27 dipindahkan ke Execution Blocked karena formula child ID, encoding/domain separation, dan provenance DDL belum ditutup. Gap AC-22, AC-28, AC-29, AC-32 serta parameter/test gaps lain tetap dicatat; angka agregat harus konsisten dengan §2.1, §8, §9, dan §13.1).
- **G-06 (Normative Contract & Acceptance Consistency)**: `CONDITIONALLY MET` (16 NC dan 34 AC terpetakan dua arah; blocker teknis B-01, B-02, B-06, B-08 dan gap spesifikasi B-07 tetap dicatat; AUDIT-NEW-10 telah direkonsiliasi pada tingkat keputusan produk dan target architecture di §13.12.11, sementara implementation/test evidence belum diklaim selesai).
- **G-07 (Governance Lock & Single File Output)**: `MET` (Pengecualian prasyarat administratif corrective revision count untuk mandat koreksi AUDIT-NEW-01..10 telah disahkan secara resmi oleh Product Owner melalui PO Governance Override; riwayat revisi historis tidak diubah atau direkayasa; tidak ada klaim REV4 atau cycle baru; satu berkas kanonikal dipertahankan tanpa artefak tambahan; implementasi kode PE-02 tetap NOT AUTHORIZED).
- **G-08 (Zero Implementation Authorization)**: `MET` (Implementasi kode PE-02 tetap secara sah `NOT AUTHORIZED`).
- **G-09 (Zero Mutation & Clean Repo State)**: `CONDITIONALLY MET WITH DISCLOSURE` (Nol mutasi kode tracked; keberadaan 2 berkas dokumen untracked di `docs/` dicatat transparan; inspeksi kebersihan repositori dibatasi pada tingkat direktori root dan tidak diklaim sebagai jaminan kebersihan rekursif).
- **G-10 (Adversarial Plan Audit & Contradiction Filter)**: `NOT PASSED — REQUIRES TARGETED CORRECTIONS / OPEN MATERIAL GAPS ACKNOWLEDGED` (Kebijakan CONF-01 dan CONF-02 telah disahkan PO; CONF-03 direklasifikasi sebagai kontrak teknis B-04 yang masih terbuka, bukan konflik keputusan PO. G-10 tetap belum lulus karena B-04, B-05, B-06, B-07, B-08, B-09, gap spesifikasi, serta konsistensi lintas-register masih harus dituntaskan).

---

### 12.3 Evaluasi Gate Kualitas Plan (Gate A) vs Kesiapan Implementasi (Gate B)
Dokumen ini memisahkan secara tegas antara evaluasi kualitas dokumen rencana (*Gate A*) dan kesiapan pelaksanaan implementasi (*Gate B*):

**Definisi normatif Gate B — implementation readiness, bukan implementation completion atau bukti keberhasilan implementasi:** Gate B menilai kelengkapan dan konsistensi desain yang akan dikerjakan: kontrak normatif, keputusan PO/AA yang diperlukan sebelum coding, work package, dependency ownership, acceptance criteria, test design, platform/lifecycle coverage, failure/recovery boundaries, serta strategi fail-closed. Gate B TIDAK BOLEH mensyaratkan source code PE-02 telah selesai, runtime integration telah tersedia, benchmark hasil implementasi telah lulus, atau post-implementation tests telah dijalankan. Semua itu merupakan acceptance/evidence gate setelah otorisasi. Source evidence existing yang sudah diserahkan Programmer harus diintegrasikan dan diaudit dari artefak yang tersedia; tidak boleh meminta PSV yang sama diulang. Gap yang telah dibuktikan menjadi pekerjaan implementasi eksplisit, bukan syarat agar gap tersebut sudah hilang sebelum coding diizinkan. Gate B hanya boleh tetap BLOCKED oleh keputusan arsitektur/produk atau detail desain yang benar-benar wajib ditetapkan sebelum implementasi dan belum dapat dirumuskan secara aman; bukan oleh pekerjaan yang secara logis baru dapat dilakukan setelah otorisasi. Gate A PASS dan Gate B PASS tetap diperlukan, lalu PO memberikan otorisasi implementasi terpisah.


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
| 2. B-08 — signed-content / signature construction | Kontrak AA §16.4 menetapkan Signature-Stripped JCS; signature tetap sebagai embedded field/envelope dalam manifest JSON yang sama dan dikecualikan dari signed JCS bytes. Detached signature file dan outer cryptographic envelope tidak dipilih. Implementasi engine dan test execution setelah otorisasi. |
| 3. B-04 — Marketplace / Zero-DDL | Kontrak transaksi/recovery AA §16.8 telah ditetapkan. Residual Gate B: buktikan existing persistent storage dan mapping source yang memenuhi Zero-DDL (durability, lookup, immutability, concurrency, recovery). Tidak ada asumsi 2PC. Implementasi/tests setelah otorisasi |
| 4. B-05 — child hash contract | Byte-domain full-file `.nx`, producer/consumer, wrapper-hash separation, dan test vectors ditetapkan AA §16.3. Residual: bukti mapping ke storage/acquisition existing tanpa DDL |
| 5. B-06 — filesystem / POSIX TOCTOU | Safe-Open contract, descriptor-relative staging, no-follow, post-open validation, atomic promotion, cleanup, threat model, dan adversarial test plan ditetapkan AA §16.6. Platform implementation/test execution setelah otorisasi |
| 6. B-09 — signer/membership | Programmer evidence report diterima: Organization Identity primitives PRESENT (Programmer-reported); Individual Creator lifecycle PARTIAL; Album capability, authority carrier, Album-specific federated authority resolution, dan production verifier wiring NOT FOUND. Ketiadaan capability merupakan expected PE-02 implementation gap, bukan kekurangan White Paper/Roadmap. PO telah menetapkan per-Album Membership Authority; AA mengunci carrier/API/verifier contract dan WP-04/WP-05 pada §16.16.4A. Gate B tidak menuntut implementasi atau post-authorization test telah selesai sebelum otorisasi. |
| 7. B-07 / NC-07 — ZIP quota & extraction security | Benchmark protocol empat payload, workload, metrik, repeatability, boundary/adversarial suite, dan evidence format ditetapkan AA §16.14. Numeric caps per dimensi tetap BLOCKED sampai benchmark deployment-representative menghasilkan capacity envelope; ZIP extractor implementation/tests setelah otorisasi |
| 8. NC-01 / AC-01 — universal manifest schema | Manifest envelope, ordered members, payload discriminator, dan audio field contract telah ditetapkan AA §16.2/§16.12. Complete JSON Schema, manifest file name/location, schema-version release, dan signer schema placement masih harus direkonsiliasi sebelum Gate B PASS; parser implementation setelah otorisasi |
| 9. NC-05 / AC-09/10 — audio hash & Genesis taxonomy | AC-09 SPEC READY: members[].audio_payload_sha256, payload discriminator, exact encrypted audio byte-domain, 64-lowercase-hex encoding ditetapkan AA §16.12. AC-10 Genesis error taxonomy dan source mapping tetap residual; tidak mengubah PE-01 error semantics |
| 10. NC-06 / AC-28/29 — Album identity/persistence/reload | Tetapkan Album ID, member relation, persistence, reload/reconstruction, integrity, dan recovery tanpa DDL sebelum Gate B PASS |
| 11. NC-13 / AC-22/32 — JIT Stage 8a & Auto-Next | Stage 8a permission/dependency/side-effect closed by PO/AA (§16.1). Stage 8b requires 7b + 7c + matching digest; 8c only current member after 8b. AC-32 residual: source feasibility and platform/payload completion event tests under §16.11/§16.15; no artificial timeout |
| 12. NC-15 / AC-26 — error taxonomy | Dimensi error, unknown-vs-invalid, stage/object/retryability mapping, evidence reference, dan user disposition ditetapkan AA §16.9. Final stable code registry wajib diselaraskan lintas seluruh AC/NC dan UI/API contract sebelum Gate A PASS |
| 13. Otorisasi resmi pelaksanaan implementasi        | TIDAK DIBERIKAN (NOT AUTHORIZED)             |
+----------------------------------------------------+----------------------------------------------+
| STATUS AKHIR GATE B                                | BLOCKED — READINESS / PRE-CODING CONTRACTS ONLY; NOT BLOCKED BY MISSING IMPLEMENTATION OR POST-AUTHORIZATION TESTS |
+----------------------------------------------------+----------------------------------------------+
```

---

## 13. READINESS GATE DAN BATAS OTORISASI

### 13.1 Evaluasi Kesiapan (Readiness Conclusion)
Berdasarkan isi dokumen, laporan Programmer, dan batas bukti yang tersedia bagi AA, kesiapan sistem dirinci ke dalam 8 kategori kesiapan. Klasifikasi di bawah ini adalah status readiness, bukan pengganti urutan PSV: seluruh fakta implementasi yang menjadi dependency blocker source-dependent tetap harus diperiksa Programmer terlebih dahulu sesuai §7.1 dan §15.3.
1. **Laporan inspeksi repositori Programmer (`REPORTED BY PROGRAMMER — NOT INDEPENDENTLY VERIFIED`):** Programmer telah menyerahkan `PE-02_SOURCE_EVIDENCE_AND_GAP_IDENTIFICATION_REPORT.md` untuk `whisnu/nexa:main` commit `fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956`; laporan tersebut kini terintegrasi pada §16.18. Klaim source tetap berstatus Programmer-reported; AA memeriksa konsistensi evidence dan PLAN tanpa mengakses source. Ini bukan alasan meminta Programmer mengulang PSV terhadap commit dan scope yang sama.
2. **Hal yang Berstatus Spesifikasi Konseptual (`SPECIFIED — PENDING IMPL`):** Schema universal kini memiliki canonical manifest envelope, ordered members, payload_type discriminator, dan audio digest field/path pada §16.2/§16.12; schema file envelope/name/location, complete JSON Schema/version constraints, signer evidence schema placement, serta persistence mapping masih perlu rekonsiliasi. Batas 199 track tetap non-normative. JCS engine, Safe-Open implementation, error registry cross-layer, dan existing ID/receipt integration tetap pending.
3. **Inventaris dan Klasifikasi Kesiapan Seluruh Acceptance Criteria (Total Tepat 34 AC) (DEFECT-01):**
   Seluruh 34 AC terpetakan secara lengkap dan eksklusif berdasarkan register otoritatif §8 (setiap AC berada tepat di satu kelompok utama tanpa penghitungan ganda):
     - *Kelompok 1: 12 AC Spesifikasi Siap Uji (`[TEST-PLANNED — SPECIFICATION READY]`)*: AC-04, AC-09, AC-11, AC-12, AC-17, AC-18, AC-19, AC-23, AC-24, AC-25, AC-30, AC-31.
     - *Kelompok 2: 22 AC Rencana Uji Terblokir Eksekusi (`[TEST-PLANNED — EXECUTION BLOCKED]`)*:
     - *Sub-Kategori 2a: Modul Implementasi Belum Tersedia (`[IMPLEMENTATION MODULE PENDING]` - 2 AC)*: AC-05 (B-01: Strict JSON Parser belum dikoding), AC-06 (B-02: RFC 8785 JCS Serializer belum dikoding).
       - *Sub-Kategori 2b: Terblokir Gap Arsitektur/Implementasi/Evidence (20 AC)*: AC-01 (NC-01: complete universal schema/manifest envelope), AC-02 (NC-01: manifest filename/location and schema release), AC-03 (B-08: implementation/cross-language verifier), AC-07/08 (B-09: existing identity/capability/revocation evidence integration), AC-10 (NC-05: Genesis error taxonomy), AC-13 (B-07: benchmark and numeric capacity limits), AC-14/15 (B-04: transaction/storage/idempotency proof), AC-16 (B-05: existing child-hash storage mapping), AC-20/21 (B-06: Safe-Open implementation/adversarial tests), AC-22 (NC-13: JIT integration), AC-26 (NC-15: stable error registry cross-register), AC-27 (NC-16: receipt/DDL compatibility evidence), AC-28/29 (NC-06: persistence/reload proof), AC-32 (NC-13: viewer source feasibility), AC-33/34 (NC-14: verifier/lifecycle integration).
   - *Kelompok 3: 0 AC Menunggu Keputusan Resmi Product Owner (`[PO DECISION REQUIRED]`)*: Tidak ada PO decision item aktif pada kelompok ini.
    *(Rekonsiliasi agregat aktif: 12 + 22 + 0 = 34 AC. AC-09 berpindah dari Execution Blocked ke Specification Ready setelah field/path dan byte-domain ditetapkan AA §16.12. Tidak ada AC yang menunggu keputusan PO.)*
4. **Hal yang Belum Diverifikasi (`NOT VERIFIED — EVIDENCE NOT AVAILABLE`):** Pengujian fisik runtime mobile iOS/Android dan Usage Service cluster.
5. **Rangkuman Ketergantungan Blocker Teknis & Arsitektur:** AA telah menetapkan Stage 8a contract, B-03/B-04 transaction design/B-05 child hash byte-domain/B-06 Safe-Open/B-08 signature/JCS/B-09 signer semantics, NC-05 audio field/path, NC-15 taxonomy dimensions, dan NC-16 member_execution_key formula. Residual readiness utama: source-backed Zero-DDL storage/receipt B-04/B-05, measured ZIP capacity limits B-07, existing Identity/authority integration B-09, complete schema/envelope/versioning NC-01, persistence/reload NC-06, stable error registry NC-15, JIT and viewer source feasibility NC-13. PSV R-02 s.d. R-10 telah ditutup; tidak ada pengulangan PSV. Gate A memerlukan cross-register reconciliation dan independent re-audit.
6. **Rangkuman Ketergantungan Keputusan Otoritatif PO:** Tidak ada PO decision blocker aktif untuk CONF-01, issuer authority B-09, atau pemilihan Model B-04. Model per-Album Membership Authority telah disahkan PO dan dikunci pada §16.16.4A. CONF-02 Pilihan B telah disahkan; CONF-03 merupakan residual kontrak/storage feasibility B-04, bukan pemilihan model produk. Residual PSV R-02 s.d. R-10 beserta R-09A/R-09A-1/R-10A telah dinyatakan CLOSED pada §15.11.3; tidak ada PSV ulang menyeluruh. Keputusan PO/Architecture Authority berikutnya hanya diminta bila muncul pertanyaan normatif baru yang benar-benar belum ditetapkan. **Klarifikasi B-09:** kedua kelas Identity Subject—Individual Creator dan Organization—telah disetujui PO pada 2026-11-10. Tidak ada lagi pertanyaan PO mengenai kelayakan kelas subject atau issuer authority. Per-Album Membership Authority, exact album binding, dedicated purpose, signed Authority Evidence Carrier, Dual-Horizon revocation, fail-closed membership, dan PE-01 isolation telah ditetapkan PO/AA pada §16.5/§16.16.4A.
7. **Kualifikasi Kelulusan Gate:** Gate A berstatus **`NOT PASSED — PRODUCT TRUTH RECONCILIATION APPLIED; SUBSTANTIVE BLOCKERS REMAIN; INDEPENDENT RE-AUDIT REQUIRED`**; Gate B berstatus **`BLOCKED`**.
8. **Status Otorisasi Implementasi PE-02:** **`NOT AUTHORIZED`** (Dilarang keras memulai implementasi kode atau migrasi database).


### 13.1.1 Rekonsiliasi Keputusan PO Terbaru — Status Aktif yang Menggantikan Snapshot Historis

Bagian ini adalah status aktif setelah keputusan PO yang telah disahkan; snapshot readiness lama dan catatan audit historis tidak dihapus, tetapi tidak boleh digunakan sebagai status keputusan terkini bila bertentangan dengan bagian ini.

1. **AC-01 / NC-01 — Unknown Fields:** PO telah menyetujui kebijakan strict: unknown fields wajib ditolak fail-closed. AC-01 tidak lagi menunggu keputusan PO. AC-01 tetap belum siap dieksekusi end-to-end karena universal multi-payload schema dan implementasi parser/validator masih menjadi dependency.
2. **AC-07 / NC-04 / CONF-01 — Membership Authenticity:** PO telah menyetujui Album Membership Authenticity Fail-Closed. Manifest dengan signer `UNKNOWN` atau signature manifest invalid tidak dapat mengautentikasi membership Album. Ini bukan global playback gate; file `.nx` yang dipilih secara independen tetap mengikuti PE-01 standalone. Kebijakan fail-closed AC-07 dan model per-Album Membership Authority telah disahkan PO. Authority carrier, trust lifecycle, dan verifier contract ditetapkan AA pada §16.5/§16.16.4A; implementasi/pengujian pascaotorisasi.
3. **CONF-03 / B-04:** CONF-03 tidak lagi diperlakukan sebagai konflik yang menunggu pemilihan model normatif. Model B, SSP/Largest Remainder, `bundle_checkout_id`, dan Immutable Checkout Manifest SSOT telah disahkan. B-04 tetap OPEN/BLOCKED karena kontrak transaksi/recovery telah ditetapkan AA pada §16.8/§16.8.1, tetapi Zero-DDL durable storage feasibility, member-to-acquisition receipt mapping, dan external operation-status interfaces masih memerlukan bukti/kompatibilitas.
4. **Agregat aktif 34 AC:** 12 `TEST-PLANNED — SPECIFICATION READY` + 22 `TEST-PLANNED — EXECUTION BLOCKED` + 0 `PO DECISION REQUIRED` = 34. AC-09 berpindah ke Specification Ready setelah field/path dan byte-domain ditetapkan AA §16.12. AC-01 tetap execution-blocked oleh schema/parser; AC-07 telah mendapat keputusan PO dan execution-blocked hanya oleh implementasi authority carrier/verifier pascaotorisasi. Setiap perubahan status harus tercermin pada register individual §8, NC register §6, blocker register §7, dan ringkasan §2.1.
5. **Gate:** Gate A tetap `NOT PASSED` sampai kontrak dan traceability seluruh AC/NC, konflik internal, bukti, dan expected result direkonsiliasi serta lulus independent re-audit oleh AA. Gate B tetap `BLOCKED` oleh kesiapan teknis yang belum terpenuhi. Tidak ada perubahan otorisasi implementasi.
6. **PSV boundary:** Register residual PSV dinyatakan CLOSED pada §15.11.3. Tidak ada permintaan PSV ulang untuk B-04/B-05/B-06/B-08/B-09 atau workstream R-02 s.d. R-10 yang sama. Hanya fakta baru yang spesifik dan material dapat memicu PSV targeted baru.

### 13.2 Disposisi Kesiapan Dokumen Resmi
Status kesiapan resmi dokumen ditetapkan sebagai:

**`NOT READY — PRODUCT-TRUTH BOUNDARY AND ACTIVE REGISTER / CROSS-SECTION SEMANTIC CONSISTENCY REQUIRE INDEPENDENT RE-AUDIT; IMPLEMENTATION BLOCKED`**

---


## 13.3 REKONSILIASI AUDIT TERARAH — FINDING-01 s.d. FINDING-06 (BASELINE AUDIT 2026-11-08)
**CATATAN SNAPSHOT HISTORIS — 2026-11-08:** Temuan di bawah merekam status pada tanggal audit tersebut, sebelum keputusan PO dan rekonsiliasi teknis pada percakapan 2026-11-09/10. Bagian ini dipertahankan sebagai audit trail dan tidak boleh dipakai sebagai status aktif bila bertentangan dengan §13.1.1, §10.3–§10.4, §13.12.11, atau koreksi terbaru. AC-01 unknown-field policy, CONF-01 membership policy, dan AUDIT-NEW-10 issuer/subdelegation telah diputuskan setelah snapshot ini.


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
- **Status:** `DECISION RESOLVED — TECHNICAL CONTRACT COMPLETION REQUIRED`.
- **Snapshot historis:** pada saat finding ini ditulis, signature-stripped JCS dan detached `album_manifest.sig` masih proposal. Keputusan PO/Architecture Authority yang lebih baru telah memilih Signature-Stripped JCS; detached signature file tidak dipilih.
- Kontrak harus menetapkan canonical payload, field yang dikecualikan bila ada, urutan canonicalization/signing, lokasi/representasi signature, dan verifikasi. Sampai itu ditetapkan, AC-03 tetap blocked dan schema tidak boleh mewajibkan `album_signer_signature`.
- Pertahankan empat jenis signature yang terpisah. Tidak ada signature Album yang menggantikan signature Creator/Container/Registry/Genesis.



**PO / Architecture Authority Decision — Signature-Stripped JCS (APPROVED):** The manifest signature field `album_signer_signature` is excluded before RFC 8785 JCS canonicalization. The canonical UTF-8 bytes of the remaining signed-content object are the Ed25519 signing and verification input. Signature remains represented in the same manifest; detached signature file and outer cryptographic envelope are not selected. This decision resolves the construction-model choice and circular dependency only; exact signed field set, canonical byte-domain details, serializer conformance, verifier contract, and negative/adversarial tests remain B-08 work. Signer identity and lifecycle remain B-09 work.

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
- White Paper v5.6 mendefinisikan baseline ekosistem, batas authority, container/manifest, Creator/Genesis ownership, Registry, JIT Player, Verify, dan Studio. ZIP wrapper Album kini disahkan melalui keputusan PO PE-02 sebagai transport/packaging envelope; White Paper tetap tidak menetapkan spesifikasi normatif untuk Album Membership Manifest, Album Signer, identitas Album multi-member, atau lifecycle signer Album.
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
**CATATAN SNAPSHOT HISTORIS:** Status AC-07/CONF-01 dan Stage 8a yang dicatat dalam audit tanggal 2026-11-08 merupakan snapshot saat itu. Untuk status aktif, gunakan §13.1.1 dan keputusan PO terbaru; jangan menghidupkan kembali PO decision blocker yang sudah diselesaikan. Batas Stage 8a tetap tunduk pada keputusan PO dan kontrak JIT terbaru.


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
3. Izin produk Stage 8a telah selesai. Sisa AC-22 adalah kontrak teknis payload hash/byte-domain dan pemisahan diagnostik dari authorization; CONF-01 bukan gerbang playback global.
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
4. Stage 8a diagnostic/background permission telah disahkan PO pada 2026-11-10; Stage 8b/8c dan JIT current-member boundary tetap tidak berubah.
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
**CATATAN SNAPSHOT HISTORIS:** Bagian ini mencatat status pada 2026-11-08. Pernyataan bahwa CONF-01/AC-01 masih unresolved dan agregat 12/20/2 telah superseded oleh keputusan PO berikutnya; status aktif adalah 11 Spec Ready + 23 Execution Blocked + 0 PO Decision Required sebagaimana §13.1.1.


**Ruang lingkup:** Koreksi terarah sesuai mandat handover Product Truth Reconciliation. Perubahan hanya pada file kanonikal ini; tidak membuka corrective cycle baru dan tidak memberikan otorisasi implementasi.

1. **PT-01/PT-02 — Packaging dan Manifest:** ZIP wrapper telah disahkan PO hanya sebagai transport/packaging envelope Album. Nama/lokasi manifest, schema JSON, nama array, field path, versi manifest, timestamp, metadata tambahan, dan field payload tetap proposal/unresolved. Semantik title/artwork PO dipertahankan tanpa mengesahkan JSON path. Keputusan ZIP entry semantics dan filename tetap berlaku dalam batas yang telah disahkan.
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
**CATATAN SNAPSHOT HISTORIS:** Hasil audit tanggal 2026-11-08 dipertahankan sebagai audit trail. Status CONF-01/AC-01 dan agregat readiness di bagian ini bukan status aktif; lihat §13.1.1.


**Ruang lingkup:** Koreksi terarah atas tiga temuan konsistensi baru dari audit plan. ID berikut menggunakan prefiks `AUDIT-PLAN` dan **berbeda dari FINDING-01 sampai FINDING-03 historis yang telah CLOSED**. Koreksi hanya menyentuh traceability status dan kualifikasi bukti; tidak mengubah kontrak produk, keputusan PO, atau blocker substantif.

1. **AUDIT-PLAN-01 — AC-20 / NC-12:** Status AC-20 pada traceability §9 diselaraskan menjadi `TEST-PLANNED — EXECUTION BLOCKED BY B-06`, konsisten dengan AC Register §8 dan klasifikasi Execution Blocked §13.1. AC-21 tetap Execution Blocked oleh B-06. Tidak ada perubahan pada mitigasi Safe-Open atau penerimaan residual risk.
2. **AUDIT-PLAN-02 — AC-25 / NC-14:** Traceability §9 kini memisahkan AC-25 `TEST-PLANNED — SPEC READY` dari AC-33/AC-34 `TEST-PLANNED — EXECUTION BLOCKED BY UNRESOLVED MEMBERSHIP AUTHENTICITY / CONF-01`. Keputusan PO CONF-02 Pilihan B tetap disahkan; CONF-01/B-09 tidak dipindahkan atau ditutup.
3. **AUDIT-PLAN-03 — Evidence Ledger / Gate A:** §12.3 kini menyatakan bahwa Evidence Ledger terdokumentasi dalam plan secara bersyarat, sementara bukti sumber primer belum diverifikasi independen. Redaksi ini tidak mengubah status G-01 sampai G-03 dan tidak mengklaim audit independen atas repository `whisnu/nexa`.

**Verifikasi pascakoreksi:** File kanonikal pada `whisnu/plan:main` telah di-fetch ulang setelah commit. Ketiga redaksi koreksi ditemukan pada §9 dan §12.3. Jumlah AC tetap 34; agregat tetap 12 Spec Ready + 20 Execution Blocked + 2 PO Decision Required.

**Disposisi:** Ketiga temuan konsistensi dokumen ini dikoreksi pada artefak kanonikal yang sama. Gate A tetap `NOT PASSED`; Gate B tetap `BLOCKED`; PE-02 Implementation tetap `NOT AUTHORIZED`; Sprint 16 dan PE-01 tetap `CLOSED / FROZEN`; Sprint 17 tetap `NOT STARTED`. Koreksi ini bukan persetujuan Gate A, bukan penutupan blocker substantif, dan bukan otorisasi implementasi.


## 13.11 DECISION REGISTER PE-02 DAN REKONSILIASI TEMUAN NC-06 / NC-13 — 2026-11-08
**CATATAN SNAPSHOT / BASIS KOREKSI:** Bagian ini disusun pada 2026-11-08. Status keputusan PO di dalamnya harus dibaca bersama rekonsiliasi terbaru §13.1.1, §10.3–§10.4, dan §13.12.11. CONF-01, AC-01, serta AUDIT-NEW-10 issuer/subdelegation tidak lagi menunggu keputusan PO. PSV residual R-02 s.d. R-10 telah ditutup sebagaimana §15.11.3; jangan meminta PSV ulang atas fakta yang sama.


**Tujuan dan batas:** Register ini mengonsolidasikan residual desain teknis/arsitektur/data/keamanan yang masih diperlukan setelah keputusan PO terbaru. Keputusan yang telah disahkan pada §10.3–§10.4 dan §13.12.11 mengikat dan tidak diajukan ulang. Pencantuman item teknis di register ini bukan persetujuan atas implementasi atau bukti bahwa mekanismenya sudah tersedia.

**Prinsip pengikat yang wajib dipertahankan saat keputusan dibuat:**
1. Pisahkan Identity, Ownership Evidence, Registry Trust, Asset Trust, dan Licensing Authority. Ownership Evidence tidak otomatis menjadi Licensing Authority; identitas organisasi tidak otomatis membuktikan kepemilikan aset atau otoritas lisensi.
2. Pertahankan model multi-registry/federated trust dan prinsip **No Single Root of Trust**. Jangan menciptakan otoritas global tunggal atau mempromosikan Creator self-signed evidence menjadi Registry Verified.
3. Pertahankan trust semantics White Paper v5.6: **UNKNOWN / INCOMPLETE** bukan **INVALID**; kegagalan integritas/signature/hash dan authoritative revocation tetap hard-block sesuai kontrak yang berlaku. Keputusan tentang autentisitas membership Album tidak boleh diam-diam mengubah trust atau playback policy member .nx standalone.
4. Pertahankan kontrak standalone .nx, Genesis Ownership Evidence, Registry/sidecar, Licensing Authority, Player memory/streaming boundary, dan baseline PE-01/Sprint 16. Tidak ada keputusan PE-02 yang boleh membuka atau mengubah baseline frozen.
5. White Paper v5.6 dan Roadmap v4.8 tidak menetapkan Album ZIP wrapper, Album Manifest schema, Album Signer, maupun signer lifecycle. ZIP wrapper sebagai transport/packaging envelope kini disahkan secara terpisah melalui keputusan PO PE-02; schema Album Membership Manifest, Album Signer, dan signer lifecycle tetap belum ditetapkan. Model konstruksi Signature-Stripped JCS telah diputuskan PO/Architecture Authority; detail schema/signed-content dan signer lifecycle tetap harus ditetapkan secara tertulis oleh otoritas yang tepat.

### 13.11.1 Baseline Rekomendasi Desain Teknis — Bukan Daftar Delegasi kepada PO

Bagian ini menggantikan pola sebelumnya yang menyerahkan hampir seluruh masalah teknis sebagai pertanyaan kepada PO. Analisis dan rancangan awal merupakan tanggung jawab penyusun plan. Tabel memisahkan ketentuan normatif yang telah disahkan PO (misalnya TD-01/TD-02/TD-04/TD-11) dari rekomendasi mekanisme teknis yang masih harus ditetapkan Architecture Authority. Pencantuman rekomendasi teknis tidak menjadikannya keputusan PO, bukti implementasi, atau otorisasi coding.

| ID | Area / blocker | Rekomendasi desain yang harus menjadi baseline evaluasi | Batas dan status yang tetap berlaku |
|:---:|:---|:---|:---|
| TD-01 | Membership authenticity — B-09 / CONF-01 / AC-07 / AC-33/34 | Terapkan keputusan PO CONF-01: manifest dengan signer UNKNOWN atau signature invalid tidak mengautentikasi membership Album. File `.nx` yang diberikan secara independen tetap diverifikasi sebagai standalone PE-01. | Kebijakan fail-closed telah APPROVED; bukan INVALID untuk member standalone, bukan global playback gate, dan bukan otorisasi Registry baru. PSV-R10/R10A CLOSED; identity binding, authority, trust store, lifecycle, verifier, dan tests tetap technical gap B-09. |
| TD-02 | Manifest schema — NC-01 / AC-01 | Terapkan keputusan PO AC-01: unknown fields pada schema version aktif ditolak fail-closed. Parser juga menolak duplicate keys, malformed Unicode, tipe salah, required field hilang, dan versi tidak didukung sesuai kontrak parser. | Kebijakan unknown-field reject telah APPROVED. Jangan mengklaim schema universal selesai atau mengunci `additionalProperties:false` pada objek yang belum didefinisikan; nama array, JSON path, payload schema, dan field audio tetap unresolved. Extension/versioning hanya boleh mengikuti kontrak eksplisit yang kelak ditetapkan, bukan diasumsikan. |
| TD-03 | Signature construction — B-08 / NC-02 / AC-03 | Terapkan model PO-approved **Signature-Stripped JCS**: keluarkan `album_signer_signature` dari objek manifest, serialisasi signed content menggunakan RFC 8785 JCS, lalu gunakan byte UTF-8 hasil canonicalization sebagai input Ed25519. | Model konstruksi telah diputuskan; exact signed field set, canonical byte-domain details, key/signature binding, serializer behavior, dan negative/adversarial tests tetap technical work sebelum AC-03 siap. Detached file dan outer envelope bukan pilihan. |
| TD-04 | Pemisahan trust — NC-04 / NC-05 / AC-07/08/09/10 | Pertahankan domain terpisah: Album declaration/membership authenticity; container packaging integrity/signature; Genesis ownership evidence; Registry trust; active licensing; playback authorization. Tiga key roles AUDIT-NEW-10 (`genesisPubKey`, `containerSigKey`, `ownCertPubKey`) berbeda dan tidak diwajibkan identik; binding/authority mengikuti §13.12.11. | Jangan menyamakan Album Signer, Container Packager, Genesis Creator, current holder, Registry Authority, atau Licensing Authority. 3-Way Identity Binding bukan lagi unresolved PO decision; implementation/verifier evidence tetap terbuka. |
| TD-05 | Verify membership — NC-14 / AC-25 / AC-33/34 | Jalankan dua pemeriksaan independen: (a) verifikasi member .nx sesuai PE-01; (b) autentikasi relasi member-ke-Album. Laporkan hasil member sesuai status kanonikal Nexa dan membership sebagai hasil terpisah. Jika membership belum autentik, jangan proses atau label file dari manifest sebagai Album member. | CONF-02 Option B tetap final: tidak ada aggregate Album trust status. Verify tidak memberikan playback authorization. File yang dipilih independen tetap dapat diverifikasi sebagai standalone. |
| TD-06 | Album identity/persistence/reload — NC-06 / AC-28/29 | Modelkan Album identity, member identity, dan membership relation sebagai konsep berbeda. Album ID tidak boleh bergantung hanya pada nama, urutan, atau hash member pertama. Simpan metadata dan relasi tanpa memodifikasi bytes .nx; pada reload, rekonstruksi membership lalu verifikasi ulang bukti yang diperlukan. | Bentuk storage, ID formula, tabel/sidecar, dan API belum dipilih. Gunakan mekanisme persistence Nexa yang sudah ada bila terbukti memadai; jangan membuat DDL/API baru atau mengklaim dukungan sebelum pemeriksaan repository. |
| TD-07 | Player JIT / Stage 8a / Auto-Next — NC-13 / AC-22/32 | Otorisasi hanya untuk current member. Urutan kausal member aktif: validasi container/integrity, Genesis/ownership, active license sesuai PE-01, lalu operasi payload yang memang dipersyaratkan tipe payload. Background work hanya boleh non-authorizing; tidak boleh mendaftarkan playback buffer atau mewariskan authorization. Auto-Next menggunakan completion signal dari lifecycle viewer untuk tipe payload terkait, bukan satu event universal. | Stage 8a tidak boleh melewati Genesis atau active license. Tidak ada timeout/duration buatan untuk dokumen/gambar. Adapter dan completion signal harus dibuktikan pada source per platform; bila tidak tersedia, AC-32 tetap blocked dan Programmer wajib STOP AND CLARIFY. |
| TD-08 | Audio hash — NC-05 / AC-09 | Definisikan setiap digest dengan byte-domain eksplisit: container .nx, payload audio hasil ekstraksi, atau source file adalah objek berbeda. Digest member/container tidak dapat menggantikan digest audio; package hash juga bukan member hash. | Jangan memilih audio_sha256 atau notasi draft tracks[].sha256, parent array, alias, fallback, atau JSON path sampai domain dan sumber normatif terbukti. AC-09 tetap blocked. |
| TD-09 | ZIP security — NC-07 / B-03 / B-07 / AC-02/13 | Terapkan streaming extraction dengan hard cap byte terkompresi, byte hasil ekstraksi per-entry dan kumulatif, jumlah entry fisik, jumlah member, ukuran .nx individual, serta batas waktu/CPU. Tolak path traversal, duplicate/case-fold collision, symlink, special file, metadata ambigu, dan entry yang tidak sesuai bijeksi. Hitung batas saat streaming, bukan hanya dari Central Directory. | Nilai 500 MB compressed, 4 GB expanded, 200 physical entries, batas member teknis, 2 GiB per `.nx`, dan rasio 10:1/100:1 tetap proposal sampai benchmark envelope empat payload, threat model, pengujian adversarial, kapasitas sistem, dan keputusan Architecture Authority. Angka 50 Album members adalah UX guidance saja, bukan hard cap. Pisahkan batas wrapper, panduan UI/member, dan batas container PE-01. |
| TD-10 | Safe-Open / TOCTOU — NC-12 / B-06 / AC-20/21 | Ekstraksi ke private staging directory dengan permission terbatas; gunakan operasi relatif terhadap directory handle/descriptor dan validasi file descriptor setelah open; jangan mengandalkan realpath/lstat lalu open path sebagai satu-satunya kontrol. Implementasi harus platform-specific dan diuji terhadap symlink, replacement, rename, dan race. | O_NOFOLLOW pada final component saja tidak membuktikan containment terhadap seluruh ancestor race. Linux openat2/equivalent hanya kandidat bila runtime mendukung; Windows/Android memerlukan analisis sendiri. Residual risk tetap harus dinyatakan, bukan diklaim hilang. |
| TD-11 | Marketplace settlement — NC-08 / B-04 / CONF-03 / AC-14/15 | Sebagai konsekuensi normatif §§6.8.3–6.8.8, gunakan durable execution state/receipt per-member yang terpisah dari Immutable Checkout Manifest untuk mencatat execution reality: acquisition, entitlement, License Daemon result, retry/recovery, terminal evidence, refund, dan exception resolution. Seluruh operasi harus idempotent dan dapat direkonsiliasi; side effect eksternal tidak dianggap rollback oleh SQL. | Prinsip pencatatan durable per-member dan pemisahan Commercial Intent vs Execution Reality telah ditetapkan oleh keputusan PO; tidak memerlukan pertanyaan/approval PO baru. Pilihan storage, mapping, schema, persistence, atomicity, recovery, dan Zero-DDL proof tetap desain teknis B-04; jika tidak ada mekanisme existing yang memenuhi, B-04 tetap blocked. |
| TD-12 | acquired_package_sha256 — NC-09 / B-05 / AC-16 | Pertahankan pemisahan package hash, member .nx hash, dan payload hash. Jangan menggunakan satu field sebagai substitusi objek hash yang lain. Definisikan producer, consumer, waktu komputasi, byte-domain, parent/child semantics, dan persistence sebelum field dipakai. | Makna field dan DDL belum diverifikasi independen. Jangan mengasumsikan bahwa field adalah hash ZIP, hash child .nx, atau hash asset. |
| TD-13 | Error taxonomy — NC-15 / AC-10/26 | Susun taxonomy berdasarkan layer dan kondisi yang benar-benar dapat dibedakan: malformed input, cryptographic failure, trust unknown/revoked, filesystem failure, quota failure, transaction/reconciliation failure. Error harus stabil dan tidak membocorkan detail sensitif. | Jangan menetapkan 20 kode sebagai normatif hanya karena daftar telah ditulis. Setiap kode harus punya trigger, layer, user-visible disposition, retryability, dan AC; Genesis error taxonomy tetap blocked sampai kontrak dibuktikan. |
| TD-14 | Batas penerapan dan baseline | Seluruh rancangan Album berada di luar perubahan perilaku standalone .nx; tidak ada perubahan Sprint 16/PE-01, shared Player/Core, renderer, memory boundary, trust model, atau database tanpa bukti kebutuhan dan otorisasi terpisah. | Tidak ada implementasi, migrasi, atau perubahan source code yang diotorisasi oleh rekonsiliasi ini. |

### Keputusan/otorisasi yang benar-benar tersisa

Tidak ada lagi PO decision blocker untuk AC-01, CONF-01, AUDIT-NEW-10 issuer authority/subdelegation, Model B, SSP/Largest Remainder, `bundle_checkout_id`, Immutable Checkout Manifest, partial fulfillment, refund obligation, automatic refund, atau Mandatory Exception Resolution. Keputusan tersebut telah disahkan dan harus diterapkan tanpa diajukan ulang.

**Keputusan PO REQ-B03-06 telah diselesaikan:** 50 Album members hanya UX guidance, bukan hard product limit. Status 11 Spec Ready + 23 Execution Blocked + 0 PO Decision Required pada §13.1.1 hanya menghitung status 34 AC; keputusan REQ-B03-06 dicatat terpisah karena berada di luar register AC. Tidak ada lagi keputusan PO yang terbuka terkait angka 50.

Sisa pekerjaan dan kewenangannya:
1. **Architecture Authority:** menyelesaikan kontrak teknis B-04/NC-08, B-05/NC-09, B-06/NC-12, B-07/NC-07, B-08/NC-02, B-09/NC-04, NC-01 schema universal, NC-05 audio hash/Genesis taxonomy, NC-06 Album identity/persistence/reload, dan NC-13 JIT/Auto-Next berdasarkan keputusan PO serta bukti yang sudah tersedia.
2. **Programmer:** tidak mengulang PSV-R02–R10/R09A/R09A-1/R10A yang telah ditutup. PSV baru hanya untuk pertanyaan source-level faktual yang spesifik dan material; setelah itu setiap temuan wajib diklasifikasikan PSV vs non-PSV. Defect dokumen/non-PSV dikoreksi langsung pada PLAN kanonikal, bukan dikirim kembali kepada Programmer.
3. **Lead Security / Architecture Authority:** menetapkan mitigasi B-06 dan evaluasi residual risk berdasarkan desain serta adversarial tests lintas platform; source PSV yang sama tidak diulang.
4. **Product Owner:** REQ-B03-06 telah diputuskan: 50 Album members adalah UX guidance, bukan hard product limit. Architecture Authority menetapkan batas teknis aktual berdasarkan threat model, benchmark, dan kapasitas sistem. Keputusan produk baru hanya diminta bila desain teknis memerlukan perubahan terhadap perilaku produk yang telah disahkan atau menyentuh baseline frozen; PO tidak diminta merancang detail implementasi teknis.

### 13.11.2 Prasyarat bukti primer — bukan keputusan desain

PSV atas repository sumber `whisnu/nexa` merupakan tanggung jawab Programmer, tetapi **PSV-R02 sampai PSV-R10 beserta sub-PSV yang dicatat pada §15.11.3 telah diselesaikan dalam scope yang dilaporkan**. Programmer tidak diminta mengulang pemeriksaan source yang sama, mengirim ZIP, atau melakukan clone penuh. PSV baru hanya boleh diminta jika Architecture Authority mengidentifikasi pertanyaan source-level yang spesifik, material, dan belum tercakup bukti terdahulu; handoff wajib menyebut pertanyaan, file/scope yang relevan, alasan mengapa bukti lama tidak cukup, serta bentuk evidence yang diperlukan. Bila suatu temuan hanya defect/inkonsistensi dokumen atau dapat diselesaikan dari keputusan PO dan PLAN yang tersedia, itu bukan PSV dan harus dikoreksi langsung oleh penyusun PLAN. Jika akses atau bukti tidak tersedia, klaim tetap `NOT VERIFIED`; jangan mengganti kekosongan bukti dengan inferensi.

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

### 13.12.2 Arsitektur membership berdasarkan keputusan PO CONF-01

1. Album adalah grouping dari .nx independen; tidak ada container .nx baru dan tidak ada trust/ownership bersama yang menggantikan bukti per-member. Ini diturunkan dari keputusan PO pada §10.3.
2. **Album Membership Manifest adalah deklarasi membership Album yang terpisah dari Immutable Checkout Manifest Marketplace** (keputusan PO pada §5.1). Manifest tersebut hanya dapat membuktikan membership setelah signature/provenance yang mengikat deklarasi dan referensi member dapat diverifikasi menurut kebijakan CONF-01/B-09. ZIP entry, nama file, urutan, kesamaan hash, dan keberadaan `.nx` tidak membuktikan membership. Persetujuan PO atas keberadaan/fungsi deklarasi membership ini tidak menetapkan nama/lokasi file, schema JSON, member array/path, signed-field set, atau mekanisme signature.
3. Sesuai CONF-01 yang telah disahkan PO, manifest dengan signer `UNKNOWN` atau signature manifest invalid tidak mengautentikasi membership Album. File yang hanya diperoleh dari deklarasi membership yang tidak autentik tidak boleh diproses/dilabeli sebagai anggota Album. File `.nx` yang disediakan/dipilih secara independen tetap dapat diverifikasi sebagai standalone PE-01.
4. Disposisi di atas tidak mengubah member menjadi INVALID, tidak mengubah arti UNKNOWN / INCOMPLETE, tidak memblokir playback global berdasarkan Album Signer, dan tidak menghalangi file .nx yang dipilih secara independen untuk diverifikasi sebagai standalone PE-01.
5. Jangan memperkenalkan Album Signer sebagai root of trust global atau menyamakannya dengan Creator, Genesis Creator, Registry Authority, atau Licensing Authority. Jika Album Signer tidak mempunyai enrollment/identity binding/lifecycle yang dapat dibuktikan, membership belum dapat dinyatakan autentik.
6. Tidak perlu menciptakan Album Membership Proof signature kedua yang terpisah dari manifest signature sebagai desain awal. Rekomendasi paling sederhana adalah manifest signature—jika mekanisme signer kelak sah—mengikat deklarasi membership dan member references secara keseluruhan. Bukti signature terpisah hanya dipertimbangkan jika ada kebutuhan produk dan arsitektur yang terbukti.

### 13.12.3 Manifest, parser, canonicalization, dan signature

1. Rekomendasi schema adalah versioned closed schema: setiap versi mempunyai allowlist, requiredness, tipe, batas, dan aturan extension yang eksplisit. Versi yang tidak didukung ditolak; jangan mencoba menafsirkan dengan schema versi lain.
2. Strict parser menolak duplicate JSON keys setelah decoding escape, malformed Unicode, invalid encoding, invalid number/string forms, dan struktur yang tidak sesuai. Parser harus bekerja pada byte input sebelum normalisasi yang dapat menyamarkan ambiguitas.
3. Keputusan PO AC-01 menetapkan unknown fields wajib ditolak fail-closed. Ketentuan ini tidak mengesahkan schema universal atau field/path yang belum ditetapkan. Extension hanya dapat diterima bila suatu kontrak schema/version/namespace eksplisit kelak disahkan; jangan menganggap extension sudah tersedia.
4. **Signature construction yang telah disetujui:** keluarkan field signature dari objek sebelum canonicalization; canonicalize signed content menggunakan RFC 8785 JCS; simpan signature sebagai field pada manifest yang sama, tetapi jangan masukkan field signature ke signed content. Detached signature file dan outer cryptographic envelope bukan model yang dipilih. Exact signed field set, field contract, canonical byte-domain, dan verifier behavior tetap harus ditetapkan konsisten sebelum AC-03 siap.
5. **RFC 8785 JCS dan Ed25519 merupakan bagian dari model konstruksi Signature-Stripped JCS yang telah disetujui PO/Architecture Authority** (lihat §6.2). Persetujuan model tersebut tidak menetapkan identitas Album Signer, trust root, enrollment, key custody, rotation, revocation, freshness, atau Registry API.
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
3. Nilai 500 MB compressed, 4 GB expanded, 200 physical entries, panduan UX 50 Album members, batas teknis member yang kelak ditetapkan, 2 GiB individual .nx, dan compression ratio 10:1/100:1 tidak boleh dicampur. Angka 50 hanya panduan UI/UX dan tidak boleh digunakan sebagai batas manifest yang menolak Album; 200 physical entries menghitung entri arsip termasuk direktori dan manifest. 2 GiB adalah batas payload kontainer individual, bukan batas wrapper.
4. Rekomendasi security adalah hard cap absolut per layer dan streaming enforcement; compression ratio hanya kontrol tambahan, bukan satu-satunya ZIP-bomb defense. Pilihan angka final harus didukung threat model dan benchmark payload nyata. B-07 tetap terbuka sampai angka dan coverage AC ditetapkan.
5. Safe-Open harus memverifikasi file descriptor setelah open dan memastikan operasi berada di bawah staging directory yang dikendalikan. O_NOFOLLOW hanya pada komponen akhir tidak cukup untuk membuktikan semua ancestor containment. Evaluasi platform-specific primitive (misalnya descriptor-relative open atau primitive OS yang ekuivalen) wajib dilakukan; jangan mengklaim TOCTOU hilang absolut.
6. Staging harus private, tidak dapat ditulis pihak tak tepercaya, dan dibersihkan secara terkendali. Race test harus mencakup symlink substitution, file replacement, ancestor rename, path traversal, serta concurrent extraction/open. B-06 tetap terbuka sampai implementasi/test dan keputusan residual risk selesai.

### 13.12.8 Blocker disposition setelah rekonsiliasi

| Blocker | Hasil rekonsiliasi desain | Apa yang masih benar-benar menghalangi penutupan |
|---|---|---|
| B-01 | Parser contract diperjelas: byte-level strict parser, duplicate-key rejection setelah escape decoding, schema validation terpisah, dan unknown-field rejection sesuai keputusan PO. | Spesifikasi/negative test design AC-01/AC-05 harus siap sebelum Gate B; implementasi parser dan test execution merupakan pekerjaan pasca-otorisasi, bukan prasyarat source PSV tambahan. |
| B-02 | RFC 8785 JCS menjadi serializer canonical untuk signed content setelah exact field set dan signature-stripping rule B-08 ditetapkan; JCS tidak mengkanonisasi signature field itu sendiri. | Exact signed field set/canonical byte-domain B-08 dan test vectors harus ditetapkan sebelum Gate B; implementasi serializer TypeScript dan runtime parity test merupakan pekerjaan pasca-otorisasi. |
| B-03 | Layered streaming ZIP security dan file-type policy dikonsolidasikan. | Implementasi extractor dan coverage semua invariant belum tersedia; B-07 memblokir parameter final. |
| B-04 | Commercial Bundle Model B dan seluruh kebijakan PO §6.8.1–§6.8.8 tetap normatif. Tidak ada klaim distributed ACID/2PC atau compensation eksternal. | Architecture Authority harus menyelesaikan desain teknis durable Manifest persistence/lookup/integrity, per-member execution state/receipt, mapping member–acquisition–entitlement–payment, idempotency/replay, commit boundary, daemon reconciliation/deduplication, settlement, refund provider capability/reconciliation, exception workflow, Zero-DDL feasibility, serta acceptance/adversarial tests. PSV-R05 tetap CLOSED; targeted PSV hanya jika muncul pertanyaan source-level material baru. |
| B-05 | Package/member/payload hash adalah objek berbeda; wrapper ZIP hash existing tidak boleh disamakan dengan child `.nx` member hash atau audio payload hash. | Architecture Authority menetapkan byte-domain tepat untuk child `.nx`, producer/consumer, mapping per-member ke acquisition/entitlement, consistency rules, dan Zero-DDL persistence. PSV-R06 tetap CLOSED; jangan meminta PSV ulang atas fakta yang sudah diperiksa. Bila DDL existing tidak dapat menampung relasi yang dibutuhkan, catat konflik Zero-DDL sebagai blocker normatif/arsitektural, bukan membuat schema baru. |
| B-06 | PSV-R08 telah memetakan call paths Desktop, Android, dan iOS; adversarial TOCTOU tests dan runtime mobile fisik belum tersedia/NOT RUN. O_NOFOLLOW pada komponen akhir saja tidak membuktikan seluruh ancestor containment. | Architecture Authority menetapkan mitigasi platform-specific, staging/descriptor containment, threat model, residual-risk statement, serta adversarial test plan/expected results sebelum Gate B. PSV-R08 tetap CLOSED; source re-review tidak diulang. Implementasi dan eksekusi adversarial/runtime tests dilakukan setelah otorisasi; evaluasi residual risk dilakukan berdasarkan hasilnya. |
| B-07 | Kandidat numerik sebelumnya bukan hard cap normatif; batas 2 GiB pada PE-01 adalah batas payload kontainer individual dan tetap berada pada domain PE-01, bukan ZIP wrapper. | Architecture Authority menyelesaikan benchmark envelope Music, Video, Document, dan Image; threat model; adversarial tests; metrik resource/kapasitas; lalu menetapkan hard caps archive-level: compressed bytes, expanded per-entry/cumulative bytes, physical entries, member count, compression-ratio defense, CPU/time/memory. Benchmark wajib memperhitungkan batas PE-01 individual `.nx` sebagai constraint kompatibilitas, tetapi tidak mengubah atau menetapkannya ulang. Tidak ada angka hard cap ZIP yang diratifikasi sebelum evidence lengkap. PSV-R07 tetap CLOSED. |
| B-08 | Signature-Stripped JCS telah disahkan: keluarkan `album_signer_signature`, canonicalize signed content dengan RFC 8785 JCS, dan gunakan UTF-8 canonical bytes sebagai input Ed25519. | Architecture Authority melengkapi exact signed field set, schema/version field contract, canonical byte-domain, serializer conformance, verifier behavior, dan negative/adversarial test specification. PSV-R09/R09A/R09A-1 tetap CLOSED; tidak perlu mengulang source review yang sama. |
| B-09 | Album Signer Architecture Model B dan CONF-01 membership fail-closed telah disahkan; PSV-R10/R10A tetap CLOSED. | Architecture Authority menyelesaikan concrete subject/key binding, authority evidence, Federated Trust resolution/conflict, custody, activation/validity, rotation/recovery/revocation/freshness, membership verifier, dan negative tests dengan mengadaptasi primitive Identity/Federated Trust existing. Kedua kelas subject—Individual Creator dan Organization—telah disetujui PO; tidak ada eskalasi PO lanjutan untuk subject-class selection. Tidak ada PSV ulang tanpa pertanyaan source-level material baru. |

### 13.12.9 Bukti repository yang wajib diperoleh sebelum finalisasi implementability

Daftar berikut adalah cakupan minimum bukti primer yang relevan untuk PE-02. Sebagian besar source scope telah ditelusuri dalam PSV-01 s.d. PSV-09 / PSV-R02 s.d. PSV-R10 dan statusnya direkonsiliasi pada §15.9–§15.11; daftar ini **bukan mandat mengulang PSV yang telah CLOSED**. Pemeriksaan tambahan hanya dibuka untuk pertanyaan source-level baru yang material. Pemeriksaan harus terarah, bukan full clone atau ZIP. Minimum evidence set:
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
Closed-schema invariant AC-01 tetap berlaku: unknown fields pada schema version aktif ditolak. Delegation evidence masuk melalui schema version baru atau extension namespace/version yang eksplisit dan di-allowlist, bukan field ad hoc pada schema lama. Setiap versi menetapkan required/optional fields, tipe, batas ukuran, canonicalization, signature scope, compatibility/migration, dan unsupported-version disposition. Consumer yang belum mendukung versi baru harus menolak/menyatakan unsupported; tidak boleh mengabaikan delegation lalu menganggap third-party package self-packaged. Parser/schema validator dan test vectors harus konsisten di SDK TypeScript, Go, Player, Verify. Representasi fisik delegation dan Tier-1 designation evidence mengikuti keputusan PO Opsi A: kedua objek bukti lengkap di-embed di dalam Album Manifest; external sidecar/reference tidak memenuhi kontrak offline. Nama field, schema version, signature preimage/scope, dan detail serialization tetap harus ditetapkan eksplisit di PLAN sebelum Gate B PASS, tanpa menganggap implementasi existing.

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

**Kesimpulan AUDIT-NEW-10:** keputusan produk tiga peran, Genesis Creator sebagai ROOT / INITIAL AUTHORITY, satu tingkat subdelegation (L0–L2), immutability delegation, explicit revocation, dan Dual-Horizon Time Rule telah disahkan serta direkonsiliasi pada §13.12.11. Tidak ada pertanyaan normatif issuer authority atau subdelegation yang tersisa. Gap verifier, schema, canonicalization, trusted-time, freshness, evidence, cross-language tests, dan implementasi tetap merupakan pekerjaan teknis.
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
9. **Status Blocker dan keputusan pasca-PSV**: B-01, B-02, B-03, dan B-06 tetap `OPEN / BLOCKED`; B-04 tetap `OPEN / BLOCKED` karena fakta transaksi yang dilaporkan belum mengesahkan pola transaksi Album; B-05 hanya memiliki bukti semantik field database yang dilaporkan dan belum menutup kontrak end-to-end/child mapping; B-07 tetap `OPEN / BLOCKED` sampai parameter teknis ditetapkan Architecture Authority; B-08 tetap `OPEN / BLOCKED` untuk exact signed-content field set, canonical byte-domain, verifier contract, dan negative/adversarial test specification; model Signature-Stripped JCS telah disahkan PO; B-09 tetap `OPEN / BLOCKED` sampai bukti signer/membership lengkap dan keputusan normatif residual diterbitkan. Integrasi PSV pada §15.9 adalah laporan Programmer dan belum boleh disebut verifikasi independen selesai. DEC-03 dihapus karena keputusan PO Auto-Next yang telah ada tidak memerlukan ratifikasi ulang; DEC-04 bukan keputusan untuk menerima proposal mitigasi yang belum diuji.
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
| R-09 — Parser/JCS/cryptography | PSV-R09/R09A/R09A-1 telah menutup source review verifier/JCS yang dicakup. Jangan mengulang pemeriksaan yang sama. Untuk kontrak B-08, finalisasi exact signed field set, canonical byte-domain, RFC 8785 conformance, Ed25519 input, key role binding, dan test vectors berdasarkan model Signature-Stripped JCS yang telah diputuskan. | Nama library atau pemanggilan serializer saja tidak membuktikan kesesuaian RFC 8785 maupun signature scope. |
| R-10 — Album Signer/membership authenticity | Periksa identity binding, enrollment, authority, key custody, rotation, revocation, freshness, manifest verification, dan dependency Registry bila memang ada. | Jangan mengasumsikan Album Signer sudah mempunyai lifecycle atau authority yang belum dibuktikan. |
| B-04 / NC-08 / CONF-03 | Commit-pinned DDL/schema for the existing durable store; source call paths that create/read/update checkout, per-member acquisition and entitlement records; transaction boundaries; idempotency inputs; daemon request/result lookup; recovery/reconciliation worker; backup/retention guarantees or authoritative operational contract | Semua relasi checkout→member→actual acquisition/entitlement dapat disimpan dan ditemukan deterministik, durable, concurrency-safe, append-only/overwrite-protected, recoverable, tanpa DDL baru; external unknown result dapat direkonsiliasi sebelum resend | Jika bukti tidak ada, mandatory implementation work package: implementasi durable receipt/mapping/idempotency/reconciliation memakai existing Zero-DDL-compatible store. Jika tidak ada store existing yang mampu memenuhi invariants, tetap BLOCKED dan eskalasi konflik kelayakan Zero-DDL kepada PO; dilarang mengarang DDL | Periksa workflow aktual Studio/Marketplace, schema, transaksi, dan side effect layanan eksternal. | Lakukan PSV terlebih dahulu. Source evidence tidak menggantikan keputusan normatif Zero-DDL/arsitektur yang mungkin tetap diperlukan setelah PSV. |
| B-05 / NC-09 | Commit-pinned DDL and producer/consumer call paths for acquired_package_sha256, spool/package hash, and any existing per-member evidence object | Semantics of existing wrapper hash remain intact; child .nx hash can be persisted/retrieved via existing Zero-DDL mechanism and mapped to immutable member/acquisition identity | Jika mapping child hash tidak ada, mandatory implementation work package untuk persist/retrieve child member hash melalui existing Zero-DDL-compatible mechanism; jangan mengubah atau mengalias acquired_package_sha256 yang tetap wrapper-domain. Jika tidak feasible tanpa DDL, tetap BLOCKED dan laporkan incompatibility, bukan mengubah semantik hash | Periksa schema/DDL aktual, producer-consumer mapping, persistence, byte-domain, dan seluruh penggunaan hash terkait. | Lakukan PSV terlebih dahulu; jangan mengubah status blocker menjadi siap hanya karena nama kolom ditemukan. |
| B-06 / NC-12 | Periksa source filesystem dan test keamanan per platform. | Lakukan PSV terlebih dahulu; mitigasi desain tertulis tidak sama dengan implementasi dan test yang lulus. |
| B-08 | Finalisasi exact signed-content field set, Signature-Stripped JCS byte-domain, serialization, verifier contract, dan negative/adversarial test design. | Model sudah diputuskan; gunakan PSV-R09/R09A/R09A-1 yang telah ditutup. PSV tambahan hanya jika muncul fakta source-level baru yang material dan belum dicakup. |
| B-09 / NC-04 / CONF-01 | Existing Identity subject/key binding verifier for Individual Creator and Organization; organization Genesis-root Subject ID and recovery-lineage resolution; current active-key-at-time resolution; concrete capability/scope issuance and authority evidence including issuer, subject, key, purpose/scope, validity, revocation, and federation provenance; caller-to-verifier integration call path; source/tests proving that Album Signer capability is distinct from CONTAINER_PACKAGING | Both approved subject classes can be resolved; signer key is bound to the exact Subject ID; ALBUM_MEMBERSHIP_SIGNING is explicitly issued/authorized, temporally valid and revocable; federated provenance/conflict is resolved fail-closed; caller uses the authoritative verifier; standalone PE-01 remains independent | If all predicates exist, cite exact source and tests. If any predicate is absent, report NOT FOUND with searched scope and make the missing capability/evidence/lifecycle/verifier work mandatory PE-02 implementation under §16.16; B-09 remains BLOCKED pending implementation and evidence. No new trust root, endpoint, credential type, or schema may be invented during evidence collection | Existing Identity subject/key binding verifier for Individual Creator and Organization; organization Genesis-root Subject ID and recovery-lineage resolution; current active-key-at-time resolution; concrete capability/scope issuance and authority evidence including issuer, subject, key, purpose/scope, validity, revocation, and federation provenance; caller-to-verifier integration call path; source/tests proving that Album Signer capability is distinct from CONTAINER_PACKAGING | Both approved subject classes can be resolved; signer key is bound to the exact Subject ID; ALBUM_MEMBERSHIP_SIGNING is explicitly issued/authorized, temporally valid and revocable; federated provenance/conflict is resolved fail-closed; caller uses the authoritative verifier; standalone PE-01 remains independent | If all predicates exist, cite exact source and tests. If any predicate is absent, report NOT FOUND with searched scope and make the missing capability/evidence/lifecycle/verifier work mandatory PE-02 implementation under §16.16; B-09 remains BLOCKED pending implementation and evidence. No new trust root, endpoint, credential type, or schema may be invented during evidence collection |

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
- **Status Parameter Kuota:** Kandidat 500 MB compressed, 4 GB cumulative expanded, 200 physical entries, dan rasio 10:1/100:1 bukan hard cap normatif. Batas 2 GiB pada `container.go:L106` adalah batas payload kontainer `.nx` individual, bukan dekompresi wrapper ZIP. Semua hard cap wrapper menunggu benchmark/threat model/kapasitas B-07. Catatan angka lama di atas merupakan proposal historis, bukan spesifikasi aktif.
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
| **B-01** (Strict JSON Parser) | `OPEN / IMPLEMENTATION PENDING` | PSV-08 telah membuktikan parser V8 `JSON.parse` tidak memenuhi duplicate-key rejection. | Modul strict byte-level parser TypeScript belum ada; spesifikasi/negative test vectors harus siap sebelum Gate B, sedangkan implementasi dan eksekusi test dilakukan setelah otorisasi. | Programmer membangun parser sesuai kontrak AC-01/AC-05 setelah PE-02 Implementation AUTHORIZED; tidak perlu PSV ulang atas fakta parser yang telah diperiksa. |
| **B-02** (RFC 8785 JCS) | `OPEN / IMPLEMENTATION PENDING` | PSV-08 telah membuktikan Go JCS generik tersedia/lulus test, sedangkan TypeScript SDK hanya memiliki template canonicalization spesifik. | Serializer JCS generik TypeScript belum ada; spesifikasi dan cross-language vectors harus siap sebelum Gate B, implementasi serta test execution setelah otorisasi. | Programmer membangun serializer TypeScript sesuai AC-06 setelah PE-02 Implementation AUTHORIZED; tidak perlu PSV ulang atas fakta yang telah diperiksa. |
| **B-03** (ZIP Extractor Aman) | `OPEN / BLOCKED — IMPLEMENTATION MODULE ABSENT; B-07 PARAMETERS OPEN` | PSV-06/R07 telah menunjukkan parser/extractor ZIP Album tidak ditemukan pada scope pemeriksaan. | Streaming ZIP extractor aman dan adversarial tests belum ada; spesifikasi ekstraksi/kuota bergantung pada keputusan teknis B-07. | Tidak perlu PSV ulang untuk ketiadaan modul yang telah diperiksa. Architecture Authority menetapkan kuota/threat model dan test design sebelum Gate B; Programmer mengimplementasikan setelah otorisasi. |
| **B-04** (Marketplace Transaction / Zero-DDL) | `OPEN / BLOCKED — PO PRODUCT POLICIES APPROVED; TECHNICAL TRANSACTION / STORAGE / RECOVERY CONTRACT OPEN` | PSV-04/PSV-R05 telah ditutup pada tingkat pembuktian sumber yang dilaporkan: transaksi SQL lokal dan side effect HTTP eksternal tanpa 2PC/compensation otomatis telah ditelusuri; orkestrasi Album multi-member belum ada pada scope yang diperiksa. | Manifest persistence/lookup/integrity, durable per-member execution state/receipt, member-to-acquisition mapping, payment-order relation, idempotency scopes, commit boundary, daemon status reconciliation/deduplication, settlement, automatic refund provider capability/reconciliation, exception workflow, dan Zero-DDL proof belum ditetapkan/diimplementasikan. | Model B, SSP/Largest Remainder, `bundle_checkout_id`, Immutable Checkout Manifest, partial fulfillment, objective terminal criteria, refund obligation, automatic refund, dan Mandatory Exception Resolution telah disahkan PO (§6.8.1–§6.8.8). Architecture Authority menyelesaikan desain teknis; targeted PSV baru hanya bila muncul pertanyaan source-level faktual baru yang material. |
| **B-05** (`acquired_package_sha256`) | `PSV-R06 CLOSED — STATIC SOURCE REPORTED BY PROGRAMMER; CHILD-MEMBER CONTRACT OPEN` | Bukti yang dilaporkan pada PSV-05 menunjukkan DDL statis, producer/consumer, dan byte-domain hash existing sebagai seluruh wrapper ZIP delivery package. Auditor tidak mengklaim verifikasi source independen atau live DB. | Target child `.nx` member hash, producer/consumer per-member, mapping ke acquisition/entitlement, dan Zero-DDL persistence belum ditetapkan. | Tidak perlu PSV ulang untuk fakta yang telah dicakup PSV-R06; Architecture Authority menetapkan target child contract tanpa menyamakan wrapper hash dengan child hash. |
| **B-06** (Safe-Open / TOCTOU) | `OPEN / BLOCKED — DESKTOP & MOBILE CALL PATHS VERIFIED; ADVERSARIAL TOCTOU TESTS NOT AVAILABLE` | PSV-07 membuktikan seluruh jalur Desktop, Android (`NexaCoreModule.kt:L56-L92` via SAF PFD detach & JNI), dan iOS (`NexaCoreModule.mm:L289-L352` via Security-Scoped URL & POSIX `open`) menggunakan open standar tanpa mitigasi `O_NOFOLLOW` atau `fstat`. Unit test `containerOpening.test.ts` lulus 3/3 (`VERIFIED BY PROGRAMMER — TEST`). | Modul uji adversarial symlink/TOCTOU tidak tersedia di repo (`NOT AVAILABLE / NOT RUN`). Uji runtime mobile fisik tidak dijalankan (`NOT RUN`). | Opsi mitigasi Safe-Open tetap proposal arsitektur sampai Architecture Authority mengevaluasi desain setelah pengujian adversarial dirancang. |
| **B-07** (Batas Kuota ZIP) | `OPEN / BLOCKED — ARCHITECTURE AUTHORITY DECISION REQUIRED` | PSV-06 membuktikan batas 2 GiB ada pada payload kontainer tunggal di Go (`container.go:L106`), bukan kuota wrapper ZIP. | Batas kuota wrapper belum ditegakkan di kode. | Architecture Authority menetapkan parameter teknis normatif kuota ZIP berdasarkan threat model dan benchmark (angka 500MB/2GiB/200/100:1 adalah usulan). |
| **B-08** (Signature-Stripped JCS) | `OPEN / BLOCKED — MODEL APPROVED; EXACT SIGNED-CONTENT / VERIFIER CONTRACT OPEN; PSV-R09 CLOSED` | PSV-R09/R09A/R09A-1 telah menelusuri source verifier, JCS yang tersedia, dan cakupan test. Direct-positive verifier test evidence tersedia; direct-negative manifest-verifier test tidak ditemukan pada scope pemeriksaan yang dicatat di §15.9.8. | Exact signed field set, canonical byte-domain, serializer conformance, verifier behavior, dan negative/adversarial test design belum ditetapkan. | Model Signature-Stripped JCS telah dipilih PO/Architecture Authority. Tidak perlu mengulang PSV yang sama. Architecture Authority melengkapi kontrak dan test specification sebelum Gate B; implementasi/verifikasi sesudah otorisasi. |
| **B-09** (Album Signer Trust) | `OPEN / BLOCKED — CONF-01 POLICY APPROVED; PSV-R10/R10A CLOSED; TECHNICAL IDENTITY / LIFECYCLE GAP OPEN` | PSV-R10/R10A membuktikan batas playback standalone `.nx` Desktop/Android/iOS terpisah dari Album membership; entitas Album Signer dan verifier membership tidak ditemukan pada scope pemeriksaan yang dilaporkan. | Identity binding, authority registration, trust store, lifecycle, freshness, membership verifier, dan tests belum tersedia/ditetapkan. | Tidak ada PO ratification atau PSV ulang yang diperlukan untuk CONF-01; Architecture Authority menyelesaikan desain teknis B-09/NC-04. |

---

#### Daftar Penetapan Residual yang Memerlukan Otoritas Formal
1. **DEC-01 (Architecture Authority — Parameter Teknis B-07):** Menetapkan batas kuota ZIP wrapper dan batas resource per-layer berdasarkan benchmark envelope empat kelas payload, threat model, adversarial tests, dan capacity evidence. Kandidat 500 MB / 4 GB / 200 entries / 10:1 atau 100:1 bukan nilai normatif. Batas 2 GiB hanya merupakan batas payload kontainer individual PE-01 yang terpisah.
2. **CONF-01 — RESOLVED:** kebijakan membership fail-closed telah disahkan PO. Tidak ada residual decision formal. Implementasi teknis B-09/NC-04 tetap terbuka sesuai AC-07/AC-08/AC-33/AC-34.
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

### 15.11 Review Architecture Authority atas Hasil Eksekusi Programmer — Disposisi PSV dan DGR

#### 15.11.1 Batas pemeriksaan dan provenance
1. AA memeriksa PLAN kanonikal, struktur bukti yang diserahkan Programmer, konsistensi internal, ketepatan klasifikasi, keterlacakan klaim, dan kecukupan evidence terhadap kontrak. AA tidak mengakses repository source.
2. Akses ke repository sumber `whisnu/nexa` merupakan kewenangan dan lingkungan kerja **Programmer-only**. AA tidak memiliki akses dan tidak akan mengakses repository source. Keterbatasan tersebut bukan defect, bukan blocker proyek, bukan kekurangan bukti Programmer, dan tidak boleh dijadikan item PSV atau handoff.
3. Karena bukti repository berasal dari hasil inspeksi Programmer, setiap klaim source/schema/test/runtime harus dinilai berdasarkan materi primer yang disertakan Programmer (path, commit, line range, raw snippet, command, exit code, output, dan runtime evidence yang relevan). Status `VERIFIED` pada §15.9 berarti subklaim tersebut diverifikasi dalam pemeriksaan Programmer sesuai bukti yang dicantumkan; status itu tidak boleh diperluas melampaui ruang lingkup bukti atau dianggap sebagai verifikasi runtime jika hanya ada inspeksi statis.
4. AA tidak boleh menurunkan status bukti hanya karena tidak mengakses repository source. AA tetap wajib mengidentifikasi kontradiksi internal, klaim yang melampaui bukti yang diserahkan, test yang gagal/tidak dijalankan, serta runtime/platform yang belum dibuktikan.
5. Tidak ada perubahan source code, schema, database, konfigurasi runtime, atau Product Truth. Tidak ada Gate yang dinaikkan dan tidak ada otorisasi implementasi yang diberikan.

#### 15.11.2 Koreksi DGR yang dilakukan langsung pada PLAN kanonikal
| ID | Temuan dokumen | Disposisi |
|---|---|---|
| DGR-PSV-02 | Subklaim PSV-01 tentang batas otorisasi Stage 8a berisi kondisi hipotetis tetapi diberi status VERIFIED. | Dikoreksi menjadi NOT VERIFIED — CONDITIONAL RISK ONLY; caller Stage 8a tidak terbukti ada. |
| DGR-PSV-03 | Disposisi B-04 berpotensi mengangkat polling idempoten menjadi bagian kontrak yang harus ditetapkan, padahal masih proposal. | Dikoreksi agar Architecture Authority mengevaluasi kontrak; polling idempoten tetap proposal dan bukan keputusan normatif. |
| DGR-PSV-04 | Pada audit sebelumnya, kutipan E-03 tidak menampilkan definisi lengkap tabel entitlements sehingga keberadaan field B-05 belum dapat diterima. | PSV-05 terbaru melaporkan DDL utuh kedua tabel pada commit yang sama. Ledger E-03 diselaraskan dengan §15.9.5; keberadaan field pada DDL statis dicatat sebagai VERIFIED BY PROGRAMMER, bukan verifikasi live DB atau verifikasi independen AA. Byte-domain parent hash dan child contract tetap dipisahkan. |

Koreksi DGR-PSV-02 s.d. DGR-PSV-04 merupakan koreksi dokumentasi/provenance yang tidak memerlukan PSV tambahan. Karena telah diterapkan langsung pada PLAN kanonikal, item tersebut **tidak boleh dimasukkan kembali** sebagai pekerjaan Programmer. Keterbatasan akses langsung AA ke repository `whisnu/nexa` bukan defect dan bukan pekerjaan Programmer.

#### 15.11.3 Register PSV residual — wajib bukti primer lanjutan

Hasil pemeriksaan pada §15.9 menunjukkan seluruh workstream R-02 s.d. R-10 telah ditelusuri. Tidak semua workstream memerlukan PSV tambahan. Jika bukti source/search yang diserahkan sudah cukup menunjukkan komponen atau test belum ada, kekurangannya diklasifikasikan sebagai gap implementasi/test atau keputusan normatif, bukan alasan mengulang pencarian yang sama.

| ID | Disposisi hasil pemeriksaan | Alasan dan batas klaim |
|---|---|---|
| PSV-R02 | **PSV CLOSED — NORMATIVE DECISION OPEN** | Caller Stage 8a tidak ditemukan pada scope pencarian; test Player FAILED karena binary CLI tidak tersedia; test/runtime Stage 8a NOT AVAILABLE/NOT RUN. Bukti cukup untuk klaim ketiadaan saat ini. Tidak ada PSV tambahan untuk mengulang pencarian. Izin diagnostik Stage 8a kemudian disahkan PO pada 2026-11-10; status lama ini merupakan snapshot historis. |
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


## 16. ARCHITECTURE AUTHORITY — PE-02 TECHNICAL CONTRACT DETERMINATIONS (2026-11-10)

Bagian ini adalah keputusan teknis Architecture Authority untuk mengisi kontrak PE-02. Bagian ini tidak mengubah keputusan PO, White Paper/Roadmap, Zero-DDL, PE-01, Sprint 16, dan tidak memberikan otorisasi implementasi. Kontrak Nexa yang sudah ada tetap menjadi fondasi; ketentuan Album adalah ekstensi yang tidak membentuk trust root atau container .nx baru.

### 16.1 Stage 8a — keputusan PO selesai; kontrak teknis AA

Keputusan PO 2026-11-10: passive background inspection / diagnostic digest diperbolehkan. Izin ini tidak memberi playback authorization, tidak mengizinkan dekripsi atau buffer registration, tidak melewati Genesis, active-license, atau trust checks, dan tidak mengubah status otorisasi secara implisit. Persetujuan produk bukan otorisasi implementasi.

Kontrak AA:
1. Stage 8a adalah operasi read-only untuk menghitung SHA-256 atas byte-domain payload audio mentah terenkripsi yang dideklarasikan oleh kontrak payload. Tidak ada dekripsi.
2. Stage 8a boleh dijalankan untuk current member maupun queued/next member sebagai pre-verification diagnostik. Hasil queued member hanya diagnostic evidence yang terikat pada identitas member/file, digest, byte length, dan provenance pembacaan. Hasil itu bukan entitlement, authorization token, trust assertion, atau playback status.
3. Genesis 7b dan active license 7c bukan prasyarat untuk komputasi digest diagnostik pasif. Ini bukan bypass: hasil 8a tidak dapat digunakan untuk Stage 8b tanpa validasi 7b dan 7c yang sah.
4. Stage 8b wajib mensyaratkan integritas container PE-01 (7a), Genesis/ownership validation (7b), active license (7c), dan digest 8a yang cocok. Kegagalan atau status unknown/unavailable pada prasyarat wajib menghentikan dekripsi secara fail-closed.
5. Stage 8c hanya boleh mendaftarkan buffer hasil dekripsi 8b untuk current member. Background pre-verification tidak boleh membuat playback session, menambahkan authorized track, atau menghasilkan otorisasi yang dapat dipakai ulang.
6. Digest cocok tidak memperbaiki signature, Genesis, ownership, Registry, Album membership, atau license yang invalid/unknown. Stage 8a tidak mengubah trust, ownership, entitlement, atau playback state.
7. Jika manifest membership belum authenticated, hasil diagnostik atas file dari arsip tidak boleh dilabeli sebagai hasil verifikasi anggota Album. File yang dipilih/disediakan independen tetap dapat diperiksa sebagai standalone PE-01.
8. Negative tests: queued digest tanpa authorization side effect; Genesis invalid tetap memblokir 8b; license absent/expired/revoked memblokir 8b; digest mismatch memblokir 8b; tidak ada decrypt/buffer/session untuk queued member; current member tetap menjalani JIT penuh; hasil diagnostik tidak menjadi authorization setelah perubahan license/Genesis/trust.

Status: Stage 8a product permission CLOSED — PO APPROVED; dependency/order and side-effect contract SPECIFIED BY AA; implementation and test execution POST-AUTHORIZATION.

### 16.2 NC-01 / NC-06 — canonical Album Membership Manifest and identity

1. Album adalah logical collection dengan identitas stabil, bukan container .nx baru. ZIP hanya transport envelope; setiap child .nx tetap independen.
2. Canonical Album Manifest adalah satu JSON object closed-schema dengan top-level fields tepat: schema_version, album_id, origin_declaration, authority_subject_id, authority_evidence, signer, members, dan signature. origin_declaration adalah structured Tier-1 Authority Designation beserta complete embedded evidence closure sebagaimana §16.16.4A/§16.16.4B; authority_subject_id wajib exact-match dengan origin_declaration.designated_authority_subject_id; authority_evidence adalah structured Tier-2 Authority Evidence Carrier. Ketiganya bukan URI, sidecar, detached file, atau network reference. Signature adalah embedded outer Album Signer signature-envelope dalam objek Manifest yang sama dan dikecualikan hanya dari outer signed JCS payload. Detached signature file dan outer cryptographic envelope tidak dipilih.
3. signer memuat Album Signer subject identity dan key reference. members adalah ordered array. Setiap member memuat member_id immutable, file_name, member_sha256, member_size_bytes, dan payload_type. Untuk MUSIC_AUDIO, member wajib memuat audio_payload_sha256; field tersebut tidak berlaku untuk tiga payload class lain (lihat §16.12). Exact nested schemas, proof object types, signature scopes, and validation order are normative in §16.16.4A/§16.16.4B.
4. member_sha256 adalah SHA-256 seluruh byte fisik child .nx final. Ia berbeda dari ZIP wrapper hash dan payload-internal hash. Producer menghitung setelah child .nx final ditutup; consumer menghitung ulang atas file hasil extraction.
5. Nama file adalah flat basename sesuai keputusan PO AUDIT-NEW-06/07: case dipertahankan dan uniqueness memakai deterministic ASCII case-fold. ZIP directory entries diperbolehkan; symlink/special entries ditolak. Himpunan regular .nx entries harus bijektif dengan deklarasi members: tidak boleh ada missing, undeclared, duplicate, atau ambiguous member.
6. Urutan playback mengikuti urutan deklarasi members, bukan urutan ZIP directory entry. album_id/member_id tidak sama dengan acquisition_id, payment_order_id, bundle_checkout_id, asset_id, atau certID. ID tidak diturunkan dari urutan UI, ZIP order, timestamp, signer key, atau filename saja.
7. Manifest, signature, Album ID, ordered member declarations, dan evidence references harus persisten dan dapat direkonstruksi. Jika storage existing tidak membuktikan durability, immutability, deterministic lookup, dan recovery, persistence tetap blocked; tidak boleh menambah DDL.
8. AC-01: unknown fields ditolak. Extension hanya melalui schema version/namespace eksplisit dan allowlist. Unsupported version ditolak, bukan diparse sebagian.

### 16.3 B-05 — child .nx hash contract

1. Child hash adalah SHA-256 atas exact complete byte sequence file .nx individual setelah final packaging, mencakup header, manifest, payload, dan signature trailer sesuai file fisik yang didistribusikan.
2. Producer menghitung hash dari file final yang sama dengan file yang dikirim/disimpan; consumer menghitung ulang dari file hasil extraction sebelum member dinyatakan cocok dengan deklarasi.
3. ZIP wrapper SHA-256 hanya membuktikan wrapper delivery package dan tidak dapat menggantikan hash individual child .nx.
4. acquired_package_sha256 yang evidence-nya menyatakan wrapper ZIP tetap wrapper-domain sampai source evidence dan kontrak eksplisit membuktikan lain. Jangan mengubah semantik field existing atau menambah DDL. Jika field existing tidak dapat menampung child hash tanpa konflik, child hash berada dalam manifest/evidence object durable yang sesuai Zero-DDL.
5. Test vectors: child identik; mutasi satu byte pada header/manifest/payload/trailer; wrapper re-compression dengan child tetap; child replacement dalam wrapper yang sama; dan mismatch member-to-acquisition mapping.

Status: target byte-domain SPECIFIED BY AA; existing field/storage mapping harus dibuktikan dalam B-04 tanpa DDL.

### 16.4 B-08 — signed-content, JCS, and Ed25519 verifier

1. Signature-Stripped JCS berarti signature envelope tidak termasuk bytes yang ditandatangani; seluruh semantic manifest content tetap termasuk.
2. Outer Album Manifest signed payload adalah RFC 8785 JCS UTF-8 bytes dari canonical Manifest object setelah hanya top-level property signature dihilangkan. Tidak ada field lain yang boleh dihilangkan, dinormalisasi diam-diam, atau diurutkan secara custom di luar RFC 8785.
3. Outer signed field set mencakup seluruh remaining top-level fields: schema_version, album_id, origin_declaration (termasuk seluruh evidence_closure dan signature internalnya), authority_subject_id, authority_evidence (termasuk delegation/identity/revocation evidence dan signature internalnya), signer, dan seluruh ordered members[] termasuk member ID, filename, child SHA-256, dan byte length. Dengan demikian seluruh Tier-1/Tier-2 proof material, signer identity, membership, order, filename, dan child integrity binding terikat oleh outer Album Signer signature.
4. Signature envelope memakai Ed25519 dan key reference yang harus identik dengan key reference pada signed signer object. Envelope tidak dapat mengganti signer/key tanpa membuat signature gagal.
5. Verifier: strict-parse JSON (duplicate keys ditolak); validate closed schema/version; reconstruct Signature-Stripped JCS; verify outer Ed25519 signature; independently verify Tier-1 Origin Declaration and its complete embedded evidence closure; resolve and verify Tier-2 Membership Authority delegation, signer identity/key and lifecycle through B-09; then validate archive/member bijection and child hashes. Verification of inner proof signatures uses each existing credential/proof type's own normative signature-preimage contract; this clause does not silently replace an existing Genesis/Identity credential signature format with a new generic format. Kegagalan signature Manifest bukan kegagalan integritas standalone PE-01 member.
6. Cross-language vectors wajib mencakup Unicode/escaping, integer boundaries, object-key ordering, absent/null, array order, duplicate keys, unknown fields, altered signer/key reference, altered member order/name/hash/size, malformed signature, wrong key, dan envelope mutation.
7. B-01 strict parser dan B-02 JCS serializer adalah implementation tasks post-authorization; spesifikasi byte-domain dan test vectors ditetapkan di sini.

Status: B-08 SPECIFIED BY AA; engine implementation and test execution post-authorization.

### 16.5 B-09 / NC-04 — Album Signer identity, authority, lifecycle

1. Subject classes yang disetujui PO adalah Individual Creator dan Organization. Kelayakan subject tidak otomatis memberikan Album Membership Signing Authority.
2. Subject identity diselesaikan melalui Nexa Identity yang existing. Untuk Organization, Subject ID adalah urn:nexa:id: + lowercase SHA-256 hex dari Genesis Root Public Key dan immutable sepanjang rotasi, recovery, dan delegasi. Genesis Root Key tidak pernah direassign; Current Root ditentukan per timestamp melalui verified recovery lineage 2-Step (recovery_key_digest match + Ed25519 signature atas JCS payload), self-recovery ke key identik dilarang, dan competing recovery branch menjadi conflict. Tepat satu Active Level-1 key berlaku per Subject ID pada timestamp tertentu dengan monotonic sequence. Delegasi maksimum Root → Active → Delegated, wajib scope-subsetting, tanpa sub-delegasi Level 2; revocation memerlukan Level-0 Current Root atau delegation chain dengan SCOPE_REVOCATION. Tidak dibuat Album-specific root identity.
3. Signing key harus terikat secara terverifikasi pada Subject ID melalui existing identity/key-resolution authority. Key possession atau signature validity saja tidak membuktikan subject binding maupun authority.
4. Album Membership Signing Authority adalah capability eksplisit untuk purpose/scope ALBUM_MEMBERSHIP_SIGNING. Capability tidak boleh disimpulkan dari Creator/Organization status, asset ownership, CONTAINER_PACKAGING delegation, Registry operator status, atau valid signature saja.
5. Federated Trust resolution mempertahankan registry/federation provenance. Tidak ada hidden global authority atau hardcoded ecosystem root. Conflict, unknown issuer, unavailable federation, stale evidence, key mismatch, unsupported scope, expired/revoked authority, dan incomplete lineage tidak menghasilkan authenticated membership.
6. Lifecycle mencakup registration/binding, activation, validity, rotation, recovery, revocation, dan historical verification. Verifier membedakan signature validity saat penandatanganan dari current authority/revocation saat evaluasi. Untuk offline mode, A1 Complete Evidence Closure menyediakan seluruh proof material penerbitan dan lineage yang diperlukan untuk memverifikasi issuance-time authority tanpa network fetch; verifier tetap wajib menyatakan freshness limitation atas status pencabutan terkini jika tidak tersedia snapshot/status authoritative yang cukup baru.
7. CONF-01: signer unknown/invalid/incompletely identity-bound, authority evidence absent/invalid, atau manifest signature invalid menghasilkan Album Membership NOT AUTHENTICATED. Ini tidak membatalkan standalone .nx integrity/status dan bukan global playback gate PE-01.
8. Album Signer authority terpisah dari CONTAINER_PACKAGING delegation; tidak ada fallback antar-purpose.
9. Per-Album Membership Authority: untuk setiap Album, satu Nexa Identity Subject (Individual Creator atau Organization) harus secara eksplisit ditetapkan sebagai Membership Authority untuk exact `album_id`; status Creator/Organization, ownership, Registry operator status, key possession, atau valid signature saja tidak memberikan authority.
10. Manifest binding: canonical manifest wajib memuat `authority_subject_id` dan `authority_evidence`; carrier ditandatangani key yang terbukti berwenang untuk subject tersebut dan mengikat exact `album_id`, `ALBUM_MEMBERSHIP_SIGNING`, `signer_subject_id`, `signer_public_key`/key reference, `not_before`, `not_after`, issuer/key lineage, dan revocation evidence. Kedua field termasuk semantic content Signature-Stripped JCS §16.4.
11. Exact scope/purpose: verifier menolak wildcard, scope kosong/omitted, mismatch `album_id`, signer/key mismatch, atau purpose selain tepat `ALBUM_MEMBERSHIP_SIGNING`; `CONTAINER_PACKAGING`, `asset:publish`, `identity:manage`, dan generic scope bukan fallback.
12. Lifecycle: validity memakai trusted time. `revoked_at` mengatur horizon internal setelah verifiable notice diterima; authoritative `recorded_at` pada Registry/Event Store/Revocation List mengatur public-verifier cut-off. Public verifier tidak menerapkan revocation retroaktif dari `revoked_at` saja sebelum `recorded_at`. Offline verifier menggunakan snapshot resmi terakhir dan wajib mengungkap freshness limitation. Terapkan Dual-Horizon Time Rule §13.12.11.A.3 klausul 4a.1 pada per-Album authority, tanpa mengimpor purpose/delegation `CONTAINER_PACKAGING`.
13. Fail-closed/PE-01 isolation: authority/carrier invalid atau absent, expired, effectively revoked, scope/purpose/subject/key mismatch, invalid manifest signature, atau required freshness failure menghasilkan membership `UNAUTHENTICATED`/`INVALID`; tidak mengubah integrity/trust/standalone verification child `.nx` dan bukan global playback gate.
14. Negative tests: unknown subject; key tidak terikat; valid key tanpa membership-signing capability; wrong purpose/scope; federation conflict; stale/unavailable trust; expired/revoked/rotated key; invalid recovery lineage; signer-envelope mismatch; dan standalone .nx valid ketika Album membership gagal.

Status: **PER-ALBUM MEMBERSHIP AUTHORITY APPROVED BY PO; SEMANTIC CONTRACT SPECIFIED BY AA.** Existing Nexa Identity and Federated Trust are reused. Source-specific integration is an implementation/evidence matter, not an unresolved PO decision. Canonical carrier and manifest predicates are fixed by §16.16.4A; WP-04/WP-05 implementation and tests are post-authorization.

### 16.6 B-03 / B-06 — secure ZIP extraction and Safe-Open

1. ZIP diproses melalui bounded staged extraction, tidak langsung ke direktori final/user-visible.
2. Central directory dan local headers harus konsisten. Reject malformed offsets, unsupported/encrypted entries, multi-disk archive, symlink/special mode, duplicate normalized names, traversal, absolute path, drive/UNC prefix, NUL/control characters, file-directory collision, dan compression method yang tidak didukung.
3. Hanya regular file dan directory entry diterima. Directory entry hanya struktural. Case filename dipertahankan; uniqueness mengikuti ASCII case-fold PO decision.
4. Gunakan private staging root dengan restrictive permissions, no-follow creation, exclusive create, streaming byte counters per-entry dan cumulative, entry counter, ratio monitoring, cancellation, dan cleanup. Jangan mempercayai declared uncompressed size saja.
5. Pembuatan file harus relatif terhadap staging-root directory handle yang sudah terbuka (openat/equivalent), no-follow, exclusive, dan descriptor validation pasca-open. Resolve setiap path component tanpa mengikuti symlink.
6. POSIX: fstat descriptor (regular-file type, ukuran, device/inode bila relevan); jangan validasi pathname lalu membuka ulang berdasarkan nama. Platform non-POSIX memakai handle-based no-follow/reparse-point protection yang ekuivalen dan harus menyatakan jaminan race-nya secara eksplisit.
7. Setelah extraction, flush/close, hitung child hashes, validasi manifest-to-file bijection, lalu promote staging secara atomik hanya setelah seluruh pemeriksaan lulus. Pada kegagalan, cleanup descriptor-relative; tidak boleh meninggalkan output parsial yang dipercaya.
8. Threat model/test mencakup concurrent rename/symlink substitution, traversal, case collision, decompression bomb, oversized/sparse entry, disk exhaustion, malformed headers, TOCTOU, cleanup race, dan concurrent extraction.

Status: B-03/B-06 design SPECIFIED BY AA. B-03 hard resource limits mengikuti B-07. Platform adversarial/runtime test execution post-authorization.

### 16.7 B-07 — benchmark-gated ZIP resource policy

1. Tidak ada angka proposal 500 MB compressed, 4 GB expanded, 200 entries, 10:1 atau 100:1 yang normatif sebelum benchmark. 50 members tetap UX guidance, bukan hard limit.
2. Benchmark mencakup Music, Video, Document, Image; ukuran small/median/large; incompressible/highly compressible; mixed workloads; malformed/adversarial archives.
3. Ukur peak RSS, CPU, wall-clock extraction, bytes read/written, temporary disk peak, file descriptors, cancellation latency, throughput, dan concurrent jobs. Catat hardware/OS/runtime/storage profile dan repeatability.
4. Turunkan batas terpisah untuk wrapper bytes, expanded cumulative bytes, per-entry bytes, entry count, path/name length, compression ratio, path depth, concurrency, dan staging disk budget. Selaraskan dengan kapasitas deployment dan PE-01 independent 2 GiB per-container limit.
5. Adversarial tests harus membuktikan enforcement saat streaming; boundary limit−1/limit/limit+1; ratio bombs; declared-size mismatch; integer overflow; disk full; cancellation; cleanup; concurrency.
6. Sebelum benchmark, runtime wajib memakai bounded deployment configuration yang konservatif dan gagal tertutup bila konfigurasi aman tidak tersedia. Tidak boleh mengarang universal numeric hard cap.

Status: methodology SPECIFIED BY AA; numeric hard caps BENCHMARK PENDING.

### 16.8 B-04 / NC-08 — transaction, immutable checkout manifest, recovery

1. Immutable Checkout Manifest adalah SSOT Commercial Intent: checkout composition, buyer/currency, member list, SSP snapshot, dan price allocation. Immutable setelah issuance.
2. Setiap member memiliki durable execution record/receipt keyed by bundle_checkout_id + immutable member identity + operation identity. Record append-only membuktikan state transition/evidence; tidak mengubah checkout manifest.
3. bundle_checkout_id, payment_order_id, acquisition_id, Album ID, dan member ID tetap identifier berbeda. Mapping harus eksplisit dan persisten; dilarang inferensi dari row order, timestamp, buyer equality, atau playlist order.
4. State per-member minimum: NOT_STARTED → ACQUISITION_PENDING → ACQUISITION_CONFIRMED → ENTITLEMENT_PENDING → ENTITLEMENT_CONFIRMED → FULFILLED. Failure/uncertainty memakai RETRYABLE, UNRESOLVED, UNKNOWN_EXTERNAL_RESULT, atau PERMANENTLY_UNFULFILLABLE sesuai bukti dan kriteria §6.8.6. Kewajiban penyelesaian/refund setelah status terminal dicatat terpisah dengan REFUND_DUE → REFUND_PENDING → REFUND_COMPLETED, atau REFUND_UNRESOLVED / EXCEPTION_REQUIRED. Status tidak boleh melompati bukti atau dipromosikan hanya karena timeout.
5. Setiap side effect memakai idempotency key stabil dari checkout identity, member identity, operation type, dan operation version. Timeout tidak membuat key baru. License Daemon unknown result wajib status lookup/reconciliation sebelum resend.
6. Transaksi PostgreSQL hanya atomik untuk local records. Tidak ada asumsi distributed 2PC atau rollback side effect eksternal. Persist intent sebelum external call; catat receipt setelah; reconcile ambiguous result; compensation hanya jika external system terbukti menyediakan operasi compensation.
7. Aggregate checkout status diturunkan dari seluruh member execution records. FULLY_FULFILLED mensyaratkan acquisition dan entitlement evidence semua member. Partial fulfillment mempertahankan member sukses. Refund dan Mandatory Exception Resolution mengikuti kebijakan PO.
8. Zero-DDL absolut. Storage adapter harus memakai mekanisme existing yang membuktikan durability, deterministic lookup, immutability/overwrite protection, concurrency, retention, backup/recovery, dan reconciliation. Tidak boleh memakai temporary file/cache volatil sebagai authority. Jika source evidence tidak mengidentifikasi durable store existing yang patuh, B-04 tetap blocked pada source-backed feasibility, bukan pada kekosongan desain.
9. Tests: duplicate callbacks/fulfillment, timeout sebelum/sesudah external commit, crash pada setiap boundary, partial success, retry, unknown daemon result, refund idempotency, manifest/projection divergence, corrupted/missing receipt, restart recovery, dan concurrent workers.

Status: transaction/recovery contract SPECIFIED BY AA; existing Zero-DDL durable storage dan source-backed mapping masih harus dibuktikan.


#### 16.8.1 Normative per-member execution and settlement contract

1. **Unit of execution:** Each member is an independent acquisition/entitlement execution unit. There is no all-N atomic transaction and no rollback of already fulfilled members because another member fails. The immutable Checkout Manifest remains the sole authority for the declared checkout composition and member allocation.
2. **Durable intent before side effect:** Before invoking License Daemon or a payment/refund provider, persist the member operation intent and its stable operation identity. Commit the local durable intent before the external request. Do not hold a PostgreSQL transaction open across an external HTTP side effect.
3. **Stable idempotency:** Reuse the exact member_execution_key and operation-specific idempotency key from §16.13 for every retry, callback replay, restart, and reconciliation. The key is not regenerated after timeout. A repeated request with the same key must return or resolve the same logical operation; it must not create a second acquisition, entitlement, license grant, or refund.
4. **External outcome protocol:** Each external side-effect integration used for License Daemon grant or refund must expose an authoritative way to resolve an operation by its stable idempotency identity, either a status lookup or an equivalent signed/authoritative receipt query. Outcomes are classified as CONFIRMED_SUCCESS, CONFIRMED_FAILURE, PENDING, or UNKNOWN. UNKNOWN and PENDING are not failure and prohibit blind resend, permanent-failure classification, or refund triggering. If an external system cannot provide authoritative status, the operation remains UNRESOLVED and enters controlled exception/reconciliation; no success or failure is fabricated.
5. **Local transaction boundary:** A local PostgreSQL transaction may atomically write only the local records included in that transaction. It cannot reverse a committed external effect. The per-member workflow persists intent, performs the external operation with the stable key, then persists the verified result/receipt. A crash between external success and local receipt is recovered by querying the external operation identity, not by issuing a new operation.
6. **Permanent failure:** PERMANENTLY_UNFULFILLABLE is permitted only after the objective criteria in §6.8.6 are satisfied, required recovery attempts have reached their defined terminal boundary, and all relevant external outcomes have been reconciled. Timeout, transport failure, pending provider response, missing receipt, or operator preference alone can never establish this state.
7. **Refund obligation:** Once PERMANENTLY_UNFULFILLABLE is validly established, create the per-member REFUND_DUE obligation automatically. The system must initiate the refund workflow without routine per-case operator approval, as required by §6.8.7. REFUND_COMPLETED requires authoritative evidence of actual settlement; request submission or an HTTP success response alone is insufficient.
8. **Refund provider limitation:** If the provider cannot execute the required partial refund, the obligation remains active and must enter the lawful manual/alternative resolution path defined by §6.8.5. Store credit, voucher, replacement member, or other non-cash resolution requires the buyer's explicit recorded consent. No provider capability may be assumed.
9. **Mandatory exception resolution:** A refund held by a limit, security control, anomaly, provider failure, or unavailable automatic route must create a durable exception case under §6.8.8. The case has a responsible owner/role, reason, evidence references, status history, escalation path, and remains open until the obligation is actually resolved. Operators cannot erase the obligation or close the case without proof.
10. **Aggregate status:** Checkout status is a derived view over the immutable manifest and all per-member durable execution/settlement evidence. FULLY_FULFILLED requires every declared member to have confirmed acquisition and entitlement plus the required external result. A partial or unresolved member cannot be silently counted as fulfilled.
11. **Concurrency:** Concurrent workers must acquire/claim a member operation using an atomic uniqueness/conditional-write primitive in the selected existing durable store. Duplicate claims must converge on the same operation identity. Last-write-wins overwrite is prohibited for authoritative receipts and terminal evidence.
12. **Zero-DDL storage acceptance:** The Immutable Checkout Manifest and per-member execution/settlement evidence must use an existing persistent Storage Engine/object-storage capability only if Programmer source evidence demonstrates deterministic lookup, durable write/read after restart, create-if-absent or equivalent immutability, concurrency control, integrity/authenticity, retention, backup/recovery, and reconciliation access. The PO previously identified Storage Engine / storage_object_id as a candidate, not as a verified capability. No path naming convention, object metadata behavior, atomicity, or retention guarantee is assumed. If no existing mechanism meets these conditions, B-04 remains blocked and no PostgreSQL DDL or volatile cache workaround is permitted.
13. **No invented compensation:** License Daemon grant, payment capture, and refund are separate external effects. Compensation is used only when the relevant external system explicitly supports it and its outcome can be authoritatively reconciled. Otherwise use the approved member-level recovery/refund/exception policy; do not describe local SQL rollback as compensation.

#### 16.8.2 B-04 evidence boundary and remaining dependency

The Programmer evidence report has already established the bounded Marketplace/PostgreSQL findings at commit fc08a5c7ac6aa1b0e4bcf64dc2cce066f149e1956. No repeat of that search is requested. The report did not establish the Storage Engine candidate's object persistence/conditional-write guarantees or the external License Daemon/payment-provider operation-status contracts. Any further Programmer evidence request must therefore be restricted to those exact unexamined interfaces and their existing API/source contracts; it must not repeat the already completed Marketplace DDL/acquisition/entitlement search.

B-04 is **architecture-contract specified** by §16.8 and this subsection. The remaining source-evidence question is whether the existing Storage Engine satisfies the stated Zero-DDL durable-record requirements. External status/refund integrations must implement the protocol above where existing provider capabilities do not already satisfy it. These are not requests for the missing PE-02 implementation to be completed before authorization. They are bounded feasibility checks for the one non-negotiable Zero-DDL storage constraint and interface compatibility.

### 16.9 NC-05 / NC-15 / NC-16 — payload hash, error taxonomy, identifiers

1. Pisahkan tiga hash domain: ZIP wrapper hash; complete child .nx hash (member_sha256); payload-internal hash Stage 8a. Ketiganya tidak saling menggantikan.
2. Stage 8a audio digest adalah SHA-256 atas exact encrypted audio bitstream byte sequence dari payload region PE-01 sebelum dekripsi. Ini bukan full .nx hash dan bukan wrapper hash. Canonical field/path dan discriminator payload ditetapkan AA pada §16.12; audio_sha256 dan notasi draf tracks[].sha256 bukan alias dan bukan field normatif.
3. Error taxonomy mempertahankan dimensi terpisah: container format/signature, payload digest, Genesis certificate, ownership chain, packaging authorization, Registry trust, license entitlement, Album membership, filesystem containment, resource quota, transaction/recovery. UNKNOWN/UNAVAILABLE bukan INVALID.
4. Setiap reason code machine-readable dan versioned; UI text localized terpisah. Setiap error memetakan originating stage, affected object, retryability, user action, evidence reference, serta apakah memblokir membership, standalone verification, atau playback.
5. NC-16 memakai deterministic member_execution_key sebagai logical correlation/idempotency identity, bukan sebagai pengganti acquisition_id. Preimage JCS domain-separated, input, dan output ditetapkan pada §16.13. acquisition_id existing tetap authoritative dan dapat server-generated; durable execution receipt memetakan pasangan checkout/member ke acquisition ID aktual.
6. member_execution_key berukuran tetap 64 karakter lowercase hexadecimal SHA-256; tidak mengubah tipe/ukuran kolom existing karena merupakan logical key untuk idempotency/correlation dan bukan mandat penambahan kolom. Pemetaan receipt ke acquisition ID existing tetap harus dibuktikan terhadap DDL/source. Collision/duplicate-key anomaly ditangani detect-and-fail, tidak pernah overwrite.

### 16.10 AA disposition and remaining feasibility

| Item | AA disposition | Residual dependency |
|---|---|---|
| Stage 8a permission/order | CLOSED — PO DECISION + AA CONTRACT | Implementation/tests after authorization |
| B-01 strict parser | Specification defined; implementation task | Code/tests after authorization |
| B-02 JCS engine | Specification defined; implementation task | Code/vectors after authorization |
| B-03 ZIP extraction | SPECIFIED BY AA | B-07 resource limits; implementation later |
| B-04 transaction/recovery | SPECIFIED BY AA | Existing Zero-DDL durable store and source-backed mapping |
| B-05 child hash | SPECIFIED BY AA | Existing field/storage mapping proof |
| B-06 Safe-Open | SPECIFIED BY AA | Platform implementation/adversarial tests later |
| B-07 ZIP quotas | Benchmark protocol specified by AA | Measured four-class benchmark/capacity evidence; numeric limits remain blocked |
| B-08 signature/JCS | SPECIFIED BY AA | Implementation and cross-language tests later |
| B-09 Album Signer | Existing Organization Identity and Federated Trust primitives are protected foundations; Album-specific capability issuance/evidence and verifier integration are not specified in WP/Roadmap | Programmer source evidence must prove whether the existing authority model can issue, bind, resolve, and revoke ALBUM_MEMBERSHIP_SIGNING for both approved subject classes. If any predicate is absent, §16.16 mandates implementation within PE-02 after separate PO authorization |
| NC-01/NC-06 | Target schema/identity contract specified | Source-backed persistence feasibility |
| NC-05/NC-15/NC-16 | AA semantic contract specified; canonical audio field and member execution key specified in §16.12–§16.13 | Source evidence for payload-byte extraction and existing receipt/acquisition mapping; implementation tests post-authorization |

Keputusan dan kontrak AA di atas menggantikan status lama yang menyebut Stage 8a background diagnostic permission, Genesis/active-license prerequisite untuk digest computation, atau desain teknis B-03/B-04/B-05/B-06/B-08/B-09 masih menunggu keputusan PO. §16.12–§16.15 melengkapi keputusan AA untuk hash audio, identifier correlation, benchmark protocol, dan source-evidence acceptance. Snapshot audit historis dipertahankan sebagai histori, bukan status aktif.

Gate A tetap memerlukan rekonsiliasi seluruh cross-register dan independent re-audit. Gate B menilai implementation readiness, bukan menunggu kode PE-02 atau post-authorization runtime tests selesai. Seluruh keputusan AA ini tidak memberikan otorisasi implementasi; otorisasi tetap keputusan PO terpisah setelah Gate A dan Gate B PASS.


### 16.11 NC-13 / AC-32 — viewer lifecycle completion and Auto-Next

PO product decision: Album playback/viewing proceeds member-by-member and advances automatically after the current viewer reports completion. This AA contract defines the completion signal without introducing an arbitrary timer or treating an unrelated UI event as completion.

1. Every payload viewer must expose one normalized lifecycle event: VIEWER_COMPLETED(member_id, viewer_instance_id, completion_reason, evidence). The event is accepted only from the active viewer instance for the current member; stale, duplicate, background, or prior-instance events are ignored idempotently.
2. Audio completion is the native playback engine's definitive end-of-stream event (not pause, stop, seek, buffer underrun, or component unmount).
3. Video completion is the native video engine's definitive ended/end-of-stream event (not timeupdate, reaching a percentage threshold, pause, seek, or unmount).
4. Document completion is emitted only when the document viewer reaches its terminal document position and the viewer explicitly completes its lifecycle through its defined completion action. Merely opening a document, rendering the first page, reaching an arbitrary dwell time, or backgrounding the app is not completion.
5. Image completion has no intrinsic time-based event. It is emitted only by the image viewer's explicit completion/advance action. No dwell-time heuristic or automatic timeout may be invented.
6. On VIEWER_COMPLETED, Player releases the current member's playback/viewer resources and authorization, then performs a fresh independent JIT authorization for the next member. The next member's Stage 8a diagnostic result may be reused only as a diagnostic cache if its identity, byte hash, and freshness still match; it never supplies Genesis/license/trust authorization.
7. Auto-Next must not run if the current viewer reports failure, user cancellation, app backgrounding, resource interruption, or an ambiguous completion state. Those cases preserve the existing user-directed failure handling; they do not silently skip.
8. There is at most one accepted completion event per viewer instance. A replayed or duplicated event cannot advance two members. Member index advances only after the next member is selected and its own JIT authorization succeeds; failure of the next member is handled per existing retry/skip policy and does not alter completed member evidence.
9. Platform parity tests cover Audio/Video/Document/Image on Desktop and Mobile, including natural completion, manual stop, pause, seek, app background/resume, viewer recreation, duplicate/stale completion event, current-member authorization release, next-member authorization failure, and no timer-triggered advance.

Status: product behavior approved; normalized completion event and platform-specific completion source specified by AA. If a target viewer cannot provide the required completion event, that platform/payload combination remains NOT READY; do not synthesize a timer or infer completion from UI visibility.

### 16.12 NC-05 / AC-09 — canonical audio payload digest field

Architecture Authority menetapkan field manifest kanonikal berikut untuk menghilangkan konflik dua notasi draf tanpa mengubah byte-domain PE-01:

1. Setiap objek members[] memiliki discriminator payload_type dengan nilai tertutup: MUSIC_AUDIO, VIDEO, DOCUMENT, atau IMAGE. Nilai ini mengklasifikasikan payload member; ia tidak mengubah struktur atau status standalone child .nx.
2. Untuk payload_type = MUSIC_AUDIO, field wajib adalah audio_payload_sha256 pada path members[].audio_payload_sha256. Nilai berupa 64 karakter lowercase hexadecimal SHA-256.
3. Field audio_payload_sha256 mengikat exact encrypted audio bitstream byte sequence yang menjadi input Stage 8a, dibaca dari payload region child PE-01 sebelum dekripsi. Field ini bukan hash seluruh child .nx, bukan ZIP wrapper hash, bukan Genesis certificate hash, dan bukan hash atas plaintext hasil dekripsi.
4. Untuk VIDEO, DOCUMENT, dan IMAGE, audio_payload_sha256 tidak berlaku dan tidak boleh diwajibkan. Hash/verification domain khusus payload non-audio tetap mengikuti kontrak masing-masing dan tidak diciptakan oleh keputusan ini. Universal child integrity tetap member_sha256.
5. audio_sha256 dan notasi draf tracks[].sha256 dinyatakan superseded sebagai kandidat draf, bukan alias, bukan fallback, dan bukan compatibility alternative. Parser canonical schema menolak keduanya sebagai unknown fields kecuali suatu versi schema eksplisit kelak mendefinisikannya; tidak ada silent migration.
6. Perubahan ini harus tercermin pada canonical schema revision melalui schema_version. Verifier hanya menerima schema version yang didukung secara eksplisit; tidak boleh menebak versi atau mem-parsing sebagian.
7. Stage 8a tetap read-only dan pasif sebagaimana §16.1. Field yang cocok hanya memenuhi digest comparison; ia tidak memberikan Genesis, ownership, trust, license, Album membership, atau playback authorization.

Disposisi: kontrak semantik hash, payload discriminator, field name/path, cardinality (satu digest untuk setiap member audio), dan encoding ditetapkan oleh AA. AC-09 dapat berstatus SPEC READY. Bukti source bahwa payload extractor menghasilkan tepat byte sequence tersebut, serta producer/consumer field mapping, adalah implementation/source-evidence verification; bukan alasan untuk mengulang PSV yang sudah ditutup dan bukan izin implementasi.

### 16.13 NC-16 / AC-16 / AC-27 — deterministic member execution identity

1. member_execution_key adalah logical, deterministic correlation identity untuk satu member dalam satu bundle_checkout_id. Ia bukan acquisition_id, payment_order_id, entitlement_id, Album ID, atau member ID.
2. Canonical preimage adalah RFC 8785 JCS UTF-8 dari object dengan tepat empat property berikut: domain, version, bundle_checkout_id, dan member_id. Nilai domain tetap urn:nexa:pe02:member-execution-key; version adalah integer 1; dua identifier lainnya adalah exact canonical identifiers yang diterbitkan oleh sistem asalnya. Tidak ada trim, case-fold, Unicode normalization, coercion, atau timestamp insertion.
3. Key dihitung sebagai SHA-256 atas canonical preimage dan direpresentasikan sebagai 64 karakter lowercase hexadecimal tanpa prefix. Implementasi harus menggunakan JCS yang sama dengan kontrak §16.4.
4. Untuk setiap operasi, idempotency key adalah SHA-256 atas JCS object dengan property tepat: domain = urn:nexa:pe02:member-operation, version = integer 1, member_execution_key, operation_type, dan operation_version. operation_type dan operation_version adalah identifier stabil dari kontrak operasi; retry untuk operasi yang sama wajib menghasilkan key identik.
5. Formula tersebut tidak mengubah, menggantikan, atau memprediksi nilai acquisition_id yang diterbitkan existing system. Receipt durable harus menyimpan/menghubungkan bundle_checkout_id, member_id, operation identity, member_execution_key, dan acquisition_id aktual beserta evidence hasil operasi.
6. Tidak ada kolom baru, tabel baru, atau perubahan DDL yang disahkan oleh formula ini. Implementasi wajib menggunakan durable store/receipt mechanism yang sudah ada dan membuktikan uniqueness, concurrency safety, deterministic lookup, dan recovery. Bila existing storage tidak dapat menyimpan relasi ini, B-04/NC-08 tetap BLOCKED; dilarang membuat schema baru untuk menutup gap.
7. Duplicate key atau collision anomaly harus menghentikan operasi dan memunculkan exception/evidence; dilarang overwrite atau menggabungkan dua member. SHA-256 collision resistance bukan bukti bahwa database uniqueness constraint sudah tersedia.

Disposisi: rumus dan byte encoding NC-16 ditetapkan AA. AC-16/AC-27 tidak boleh diklaim implementation-ready sebelum source/DDL membuktikan bahwa receipt dan relasi aktual dapat dipersistenkan sesuai Zero-DDL.

### 16.14 B-07 — reproducible benchmark and capacity-evidence protocol

1. Benchmark harus dijalankan pada deployment-representative environment, dengan hardware/CPU, RAM, OS/kernel, filesystem, storage medium, runtime/library versions, configured concurrency, dan free-space baseline dicatat. Hasil dari laptop/developer workstation tidak boleh langsung menjadi deployment cap.
2. Dataset dipisahkan untuk Music/Audio, Video, Document, dan Image. Tiap kelas memuat small, median, large, highly-compressible, low-compressibility/incompressible, dan mixed-member workloads. Dataset harus mencatat source, byte sizes, compression method/ratio, entry count, dan apakah data sintetis atau representatif; tidak boleh memakai data privat tanpa otorisasi.
3. Setiap skenario diulang sekurang-kurangnya 5 kali pada kondisi yang sama. Laporkan seluruh raw observations, median, P95 bila jumlah sampel memadai, maksimum teramati, variance, serta kegagalan/cancellation. Jangan mengubah hasil pengukuran menjadi angka universal tanpa capacity margin dan deployment envelope.
4. Ukur wall-clock extraction, CPU time/utilization, peak RSS, peak temporary disk, bytes read/written, open file descriptors, throughput, cancellation latency, cleanup duration, dan concurrent-job interference. Pisahkan parsing, extraction, hashing, validation, dan promotion bila instrumentation memungkinkan.
5. Boundary suite menguji setiap kandidat limit pada N−1, N, N+1; compressed/expanded size, per-entry/cumulative bytes, entry count, path/name length, path depth, compression ratio, concurrency, dan staging disk. Tambahkan integer overflow, declared-size mismatch, malformed central/local headers, decompression bomb, disk-full, cancellation race, cleanup race, duplicate names, dan symlink/special entry.
6. Capacity policy diturunkan per dimensi, bukan satu angka gabungan. Setiap cap harus disertai measured safe envelope, resource headroom, alasan margin, konfigurasi deployment, dan fail-closed behavior ketika konfigurasi tidak tersedia. Hard cap tidak boleh melampaui batas resource yang dapat dipertanggungjawabkan dari evidence.
7. Hasil benchmark wajib berupa raw machine-readable records plus ringkasan environment, dataset manifest, command/test invocation, exit code, dan artifact hashes. Programmer wajib menyediakan artefak yang memungkinkan PO dan AA menilai serta meminta reproduksi terarah; AA tidak mengakses source code atau menjalankan inspeksi source.
8. Batas PE-01 individual container 2 GiB tetap invariant terpisah. Batas itu bukan izin menetapkan wrapper/expanded Album ZIP cap 2 GiB atau angka lainnya.
9. Sebelum evidence benchmark tersedia, tidak ada hard numeric cap universal yang ditetapkan AA. Runtime tidak boleh menerima archive tanpa bounded configuration yang disediakan deployment; ketiadaan konfigurasi aman harus fail-closed. Nilai sementara hanya boleh menjadi deployment configuration yang terdokumentasi dan terukur, bukan normative product limit.

Acceptance evidence: dataset manifest; environment manifest; raw run outputs; per-metric results; boundary/adversarial test logs; proposed per-dimension caps with capacity rationale; independent reproducibility record. Tanpa paket evidence tersebut B-07 tetap BLOCKED.

### 16.15 Source-evidence closure criteria — B-04, B-05, B-09, NC-06, AC-32

Bagian ini menetapkan tepat bukti yang harus ditunjukkan; bukan mandat untuk mengulang PSV dan bukan klaim bahwa bukti tersebut telah tersedia.

| Residual | Required primary evidence | Pass condition | Failure disposition |
|---|---|---|---|
| B-04 / NC-08 / CONF-03 | Commit-pinned DDL/schema for the existing durable store; source call paths that create/read/update checkout, per-member acquisition and entitlement records; transaction boundaries; idempotency inputs; daemon request/result lookup; recovery/reconciliation worker; backup/retention guarantees or authoritative operational contract | Semua relasi checkout→member→actual acquisition/entitlement dapat disimpan dan ditemukan deterministik, durable, concurrency-safe, append-only/overwrite-protected, recoverable, tanpa DDL baru; external unknown result dapat direkonsiliasi sebelum resend | Jika bukti tidak ada, mandatory implementation work package: implementasi durable receipt/mapping/idempotency/reconciliation memakai existing Zero-DDL-compatible store. Jika tidak ada store existing yang mampu memenuhi invariants, tetap BLOCKED dan eskalasi konflik kelayakan Zero-DDL kepada PO; dilarang mengarang DDL |
| B-05 / NC-09 | Commit-pinned DDL and producer/consumer call paths for acquired_package_sha256, spool/package hash, and any existing per-member evidence object | Semantics of existing wrapper hash remain intact; child .nx hash can be persisted/retrieved via existing Zero-DDL mechanism and mapped to immutable member/acquisition identity | Jika mapping child hash tidak ada, mandatory implementation work package untuk persist/retrieve child member hash melalui existing Zero-DDL-compatible mechanism; jangan mengubah atau mengalias acquired_package_sha256 yang tetap wrapper-domain. Jika tidak feasible tanpa DDL, tetap BLOCKED dan laporkan incompatibility, bukan mengubah semantik hash |
| B-09 / NC-04 / CONF-01 | Existing Identity subject/key binding verifier for Individual Creator and Organization; organization Genesis-root Subject ID and recovery-lineage resolution; current active-key-at-time resolution; concrete capability/scope issuance and authority evidence including issuer, subject, key, purpose/scope, validity, revocation, and federation provenance; caller-to-verifier integration call path; source/tests proving that Album Signer capability is distinct from CONTAINER_PACKAGING | Both approved subject classes can be resolved; signer key is bound to the exact Subject ID; ALBUM_MEMBERSHIP_SIGNING is explicitly issued/authorized, temporally valid and revocable; federated provenance/conflict is resolved fail-closed; caller uses the authoritative verifier; standalone PE-01 remains independent | If all predicates exist, cite exact source and tests. If any predicate is absent, report NOT FOUND with searched scope and make the missing capability/evidence/lifecycle/verifier work mandatory PE-02 implementation under §16.16; B-09 remains BLOCKED pending implementation and evidence. No new trust root, endpoint, credential type, or schema may be invented during evidence collection |
| NC-06 / AC-28 / AC-29 | Existing Studio persistence/publication and Marketplace/Storage association, reload, lookup, and recovery source paths; DDL and tests for multi-member association | Same Album identity and ordered member relation survive process restart, reload, retry, partial publication, and recovery under Zero-DDL; member bytes/hash and PE-01 contracts remain independent | Jika association/persistence/reload belum tersedia, mandatory implementation work package untuk relasi Album/member dan recovery melalui existing Zero-DDL-compatible persistence. Jika tidak ada mekanisme existing yang mampu, tetap BLOCKED dan eskalasi konflik Zero-DDL; katalog individual bukan bukti asosiasi Album |
| AC-32 / NC-13 | Viewer source per platform/payload showing definitive completion signal, viewer-instance identity, event de-duplication, authorization release and next-member JIT path | Every supported platform/payload pair emits one definitive completion event and passes parity tests; no timeout heuristic or stale event advances playback | Jika source event tidak tersedia, mandatory implementation work package untuk completion signal/event wiring per platform/payload, lifecycle identity, deduplication, resource release, and next-member JIT. Tidak boleh mengganti dengan timeout; pair belum siap sampai implementasi dan tests terbukti |

Evidence format: each claim must identify repository, branch, commit SHA, exact path and line range, source excerpt, relevant DDL/migration, exact test command, exit code, and raw test output. A source absence claim must state the searched scope and exact search terms/command. Static source existence is not runtime proof; a test file is not a passing test; a Programmer-reported result remains Programmer-submitted evidence until AA reviews its internal consistency and PO accepts the evidence disposition.

Role boundary: no new PSV is requested for already-closed search scopes. This is a bounded source-evidence handoff, not a request to repeat PSV-R10/R10A. Programmer must report positive evidence and explicit NOT FOUND results for every predicate in §16.15. A NOT FOUND result is not a terminal disposition: it activates the mandatory PE-02 implementation work package in §16.16; it must not be left as an unspecified future investigation. AA evaluates architectural compatibility and the submitted evidence without accessing source code; PO decides product matters and authorization. No code/DDL changes are authorized by this evidence handoff.



### 16.16 B-09 — all-version Product Truth audit and mandatory Album Signer capability implementation

#### 16.16.1 Audit of all inventoried White Paper and Roadmap versions

The Library inventory and the historical archive `WPdanRM.zip` were inspected. The archive contains the following version history:

- White Paper: v1, v3, v5, v5.1, v5.2, v5.3, v5.4, v5.5; current standalone Library document v5.6.
- Development Roadmap: v1, v1.0, v2.0, v3.1, v4.0, v4.1, v4.2, v4.3, v4.4, v4.5, v4.6, v4.7; current standalone Library document v4.8.
- Supporting identity/revocation documents in the archive: `registry_api_v0.3.md`, `revocation_v0.3.md`, their patch files, and `Korelasi-Whitepaper+RoadmapDev.md`.

The historical progression is:

1. White Paper v1/v3 and early Roadmap versions define container Creator/issuer/certificate and Registry revocation foundations. They do not define Organization Identity or Album Signer capability.
2. Roadmap v2.0 introduces Sprint 14 — Organization Identity as an objective; Roadmap v3.1/v4.0/v4.1 keep it planned. These versions do not specify Album membership signing authority.
3. Roadmap v4.3 and White Paper v5/v5.1 establish the architectural separation of Organization Identity from Organization Trust, Asset Ownership, and Licensing Authority, while Sprint 14 is still planned or being prepared.
4. Roadmap v4.4 onward records Sprint 14 as CLOSED and independently verified. White Paper v5.2 onward records the closed Organization Identity baseline and its invariants.
5. White Paper v5.3/v5.4/v5.5/v5.6 and Roadmap v4.5/v4.6/v4.7/v4.8 preserve the Organization Identity baseline. The current detailed invariants include immutable Organization Subject ID derived from Genesis Root Public Key, immutable Genesis Root Key, timestamp-resolved Current Root, 2-Step recovery with digest match and Ed25519/JCS proof, one active Level-1 signing key per Subject at a timestamp with monotonic sequence, bounded Root → Active → Delegated authority with scope-subsetting and no Level-2 subdelegation, and revocation by Current Root or explicit `SCOPE_REVOCATION` delegation.
6. The documents also preserve separation between Organization Identity, Organization Trust, Asset Ownership, and Licensing Authority; Sprint 15 consumes the authoritative Sprint 14 production path and publisher-key provenance without creator-key fallback.

**Finding and correct interpretation:** Album Handling is a new PE-02 capability. Its absence from pre-existing White Paper/Roadmap versions is expected and is not a Product Truth defect, missing baseline requirement, or reason to modify those documents. White Paper/Roadmap remain authoritative for the existing Organization Identity and Federated Trust foundations and their boundaries. The implementation evidence report (§16.18) records that the Album-specific capability, authority carrier, Album-specific federated authority resolution, and production Album Manifest verifier wiring were not found in the examined source scope. These are new PE-02 implementation requirements to be designed and implemented by reusing the existing identity/trust foundations, without a new trust root or global authority. Generic delegation scope-subsetting and `SCOPE_REVOCATION` do not prove that the specific Album capability has been issued or can be resolved.

Supporting legacy Registry documents `registry_api_v0.3.md` and `revocation_v0.3.md` were also included in the archive review. Their issuer/signature/revocation contract concerns existing `.nxcert` certificate issuance and revocation; it does not define an Organization Subject capability or Album membership signing authority. Those mechanisms must not be repurposed by inference as proof of `ALBUM_MEMBERSHIP_SIGNING`.

Any older PE-02 proposal that uses a local `trusted_signers.json`, interactive user consent, a hardcoded signer key, or a local trust list is not an authoritative substitute for this B-09 contract. Such data may not grant Album Membership Signing Authority, establish issuer provenance, or override Federated Trust. If retained for a separately approved non-authoritative cache/presentation purpose, it cannot change the membership authentication result.

This finding does not require a new organization identity, a new trust root, a global authority, or a new Registry model. It requires the Album-specific signing capability to be expressed through the existing Nexa identity/authority/federation model. The capability is not inherited from Creator/Organization eligibility, ownership, `CONTAINER_PACKAGING`, Registry operator status, or possession of a valid Ed25519 key.

#### 16.16.2 Mandatory source-evidence decision

The Programmer has completed the bounded source inspection and submitted the commit-pinned evidence report integrated in §16.18. The predicates below are the evidence-review and implementation-acceptance checklist; they are not a request to repeat PSV. For each predicate, use the submitted report's PRESENT / PARTIAL / NOT FOUND disposition and the cited source/test evidence. Any genuinely material ambiguity must be isolated to the exact claim and must not trigger a repeat of the same search scope:

1. Individual Creator subject resolution and exact key-to-subject binding.
2. Organization Subject ID resolution from Genesis Root Public Key, Current Root lineage, and timestamp-correct Active Level-1 key.
3. A concrete existing authority/scope mechanism that can explicitly issue or delegate the exact purpose `ALBUM_MEMBERSHIP_SIGNING` to a key bound to the subject.
4. Issuer authorization to grant that capability, including the authoritative issuer identity and its own trust provenance; no self-asserted capability.
5. Evidence representation and verification of subject ID, key reference, purpose/scope, issuer, validity interval, issuance time, and revocation/lifecycle state.
6. Delegation enforcement: scope-subsetting, bounded depth, no unauthorized subdelegation, and separation from `CONTAINER_PACKAGING`.
7. Federated Trust resolution across Registry authorities, including issuer discovery/provenance, conflict, unknown/unavailable issuer, stale evidence, and fail-closed behavior.
8. Rotation, recovery, revocation, historical-at-signing verification, current-at-evaluation verification, and offline freshness limitations.
9. Actual caller-to-verifier production path from Album Manifest verification to authoritative identity/authority resolution. A library or helper that is not wired into the production verifier is insufficient.
10. Negative and positive tests for both approved subject classes, including valid identity without Album capability, wrong scope, wrong subject/key, revoked/expired/rotated key, invalid recovery lineage, unknown/conflicting issuer, stale offline evidence, and a valid standalone PE-01 member when Album membership fails.

The submitted evidence is commit-pinned to repository whisnu/nexa, branch main, commit fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956. Its evidence format includes source paths/line ranges, excerpts, caller paths, DDL where relevant, search commands/scopes, and two existing identity test runs with exit code 0. The report's evidence is Programmer-submitted; AA reviews the report and its consistency with this canonical plan but does not independently inspect source code. A test result proves only the tested baseline and not untested Album behavior. A new targeted clarification is permissible only for a specific material inconsistency or unexamined dependency, not as repeated broad PSV.

#### 16.16.3 Mandatory implementation work package when evidence is absent

For every predicate in §16.16.2 that Programmer cannot prove, the missing capability is a **mandatory PE-02 implementation requirement**, not a deferred question and not a reason to close B-09 as merely "evidence pending". The implementation work package must include the missing items below as applicable:

1. Implement the PO-approved per-Album Membership Authority: an explicitly designated existing Nexa Identity Subject for exact `album_id` authorizes a separate Album Signer subject/key for purpose `ALBUM_MEMBERSHIP_SIGNING`, using §16.16.4A. Reuse existing Subject ID and key lifecycle; do not create an Album-specific identity root.
2. Implement canonical manifest fields `authority_subject_id` and `authority_evidence` with exact carrier predicates in §16.16.4A. Reuse an existing compatible credential/evidence mechanism where possible; transport/API/storage integration must preserve these semantics. No unilateral field renaming, scope broadening, or alternate purpose is permitted.
3. Enforce issuer authorization and delegation rules, including scope-subsetting, bounded Root → Active → Delegated chain, no Level-2 subdelegation, explicit revocation authority, and separation from `CONTAINER_PACKAGING`.
4. Implement authoritative federated resolution and provenance handling for the capability; unknown, conflicting, unavailable, stale, expired, revoked, mismatched, or incomplete evidence must never authenticate Album membership.
5. Wire Album Manifest verification to the authoritative subject/key/capability/lifecycle verifier. A disconnected helper, static allowlist, hardcoded key, local-only trust root, creator-key fallback, or caller-supplied authority claim does not satisfy this requirement.
6. Implement lifecycle and temporal semantics: activation, validity, rotation, recovery, revocation, historical signature-time evaluation, current evaluation, and explicit offline freshness limitations.
7. Add cross-language/production-path tests and adversarial negative tests for Individual Creator and Organization; prove that missing capability cannot false-pass and that failure of Album membership does not invalidate standalone PE-01 member integrity/status or create a global playback gate.
8. Add non-regression tests for existing Sprint 10–15 Identity/Federated Trust semantics, Organization Identity immutable Subject ID and key lineage, Registry Identity ≠ Registry Trust, and PE-01 standalone behavior.

The normative carrier fields and semantic predicates are fixed in §16.16.4A. Programmer may identify the compatible existing source integration point and implement the approved contract after authorization; Programmer may not redesign the authority model or alter canonical field/purpose/scope semantics.

#### 16.16.4A PO-approved per-Album Membership Authority and Authority Designation — normative contract

**PO decision: APPROVED.** Authority is a three-tier proof chain. The subject named by `authority_subject_id` is not trusted merely because it appears in the Manifest: an independently verifiable Authority Designation MUST first establish that the subject is entitled to act as Membership Authority for the exact `album_id`. This Membership Authority may then authorize a separate Album Signer subject/key. This is per-Album authority, not global or ambient authority.

**Tier 1 — Authority Designation (who is entitled to appoint the Membership Authority).**

1. For every exact `album_id`, the verifier MUST obtain an explicit Authority Designation Evidence anchor that binds `album_id` to exactly one `designated_authority_subject_id`. The value MUST exact-match the Manifest's `authority_subject_id`. Missing, empty, wildcard, ambiguous, disputed, or mismatched designation is not valid evidence.
2. Authority Designation MUST originate from a Creator, Publisher, or Organization whose authority to issue/manage that Album is itself verifiable through existing Nexa Identity and Nexa ownership/rights evidence. The evidence MUST establish authority over the Album as a whole; possession, authorship, ownership, or publication of one or more individual child `.nx` members, Creator/Organization status alone, Registry operator status, key possession, or a valid signature alone MUST NOT be inferred as sufficient. No member-level ownership fallback is permitted.
3. The designation evidence MUST be cryptographically bound to its issuer, issuer subject/key, exact `album_id`, designated authority subject, and its applicable validity/status/revocation information. The issuer's identity, key binding, and rights/authority basis MUST be independently verifiable through existing Nexa Identity/Federated Trust and ownership/rights foundations. A Registry operator may attest publication/record provenance under Registry Trust, but Registry operation alone does not create copyright, ownership, or publisher authority.
4. **Online/Federated mode:** the verifier MUST resolve an official Album registration/Registry record or Federated Registry/Event Store record that records the exact pair `(album_id, designated_authority_subject_id)` and preserves/verifies the underlying authorized designation. Registry/Event Store attestation establishes the provenance and status/timing of the published record; it MUST NOT replace verification of the designating Creator/Publisher/Organization's authority basis. The record and its issuer/registry trust chain MUST be verifiable through existing Nexa federation/Registry trust; no new global trust root is created.
5. **Offline/Standalone mode — PO-approved A1 Complete Evidence Closure:** the complete signed Album Genesis Origin Declaration and all cryptographic proof material required to verify its issuer identity, Genesis-root provenance, key succession/recovery lineage, timestamp-correct active signing key, Album-wide rights/authority basis, and designation of designated_authority_subject_id MUST be embedded as structured objects within the canonical Album Manifest's origin_declaration. This includes the complete signed Genesis Root Certificate/identity credential, every required signed key-lineage/recovery proof in the relevant chain, signed Album-wide rights/authority evidence objects, the signed designation assertion, and issuance-time revocation/status evidence needed to evaluate the chain at issuance. It MUST NOT be represented solely by a URI, external file path, ZIP sidecar, or network reference. The offline verifier MUST validate Tier-1 issuance-time authority from the single Manifest payload without external evidence-file access or network connectivity. Embedded certificates/public keys are proof material, not self-authenticating trust anchors: validation MUST terminate at a trust anchor already provisioned and trusted by the verifier under the existing Nexa trust model. The Manifest MUST NOT introduce, nominate, or bootstrap a new trust root. Offline acceptance MUST disclose the evidence snapshot/freshness boundary and MUST NOT claim current non-revocation when no sufficiently current authoritative revocation/status evidence is available. Complete Tier-2 signer identity/key lineage and delegation proof needed to validate the Album Signer chain MUST likewise be embedded in authority_evidence; no external proof retrieval is required for basic offline verification.
6. The online Registry/Federated record and the embedded offline Origin Declaration are evidence-delivery/verification modes for the same designation fact, not independent competing grants of authority. In offline/standalone mode, Tier-1 evidence MUST be self-contained in the Manifest; an external reference cannot satisfy the requirement. Where online authoritative status is available, it MUST be reconciled with the embedded declaration for the applicable version/validity period. Conflicting designated subjects, rights basis, invalid signatures, unresolved issuer/key lineage, or unresolved status/version ordering MUST fail closed as `UNAUTHENTICATED / REJECTED`; verifier MUST NOT select whichever source is more permissive. A newer authoritative Registry/Event Store status or revocation record is processed under the existing Dual-Horizon rule in clause 12 below. Embedded evidence cannot override a known later authoritative revocation or unresolved conflict.
7. The designation lifecycle MUST preserve provenance and distinguish initial designation, authorized change/replacement, expiry, revocation, and dispute. Any replacement MUST itself be supported by a newly verifiable designation from an issuer with authority to make that change; a Registry update alone cannot manufacture that authority. A disputed or superseded designation MUST NOT authenticate a new Album membership declaration unless the applicable authority/status can be resolved deterministically.

**Tier 2 — Capability Delegation (which Album Signer is appointed).**

8. Canonical Album Manifest MUST contain authority_subject_id, the complete embedded Tier-1 origin_declaration including its A1 Complete Evidence Closure, and the complete embedded Tier-2 authority_evidence including proof material needed to verify Membership Authority and Album Signer key lineage offline. These are structured evidence objects in the Manifest payload, not external file references. The Origin Declaration MUST carry its own independently verifiable issuer signature over its defined canonical signed content; the Authority Evidence Carrier MUST carry its own independently verifiable Membership Authority signature and delegation predicates. The Album Signer's outer Manifest signature MUST cover the complete semantic content of both embedded evidence objects, together with ordered members and all other signed fields, under the Signature-Stripped JCS contract in §16.4. The inner signatures and outer Manifest signature have distinct scopes and MUST NOT be conflated.
9. The carrier MUST bind exact `album_id`, purpose exactly `ALBUM_MEMBERSHIP_SIGNING`, `signer_subject_id`, exact `signer_public_key` or unambiguous key reference, `not_before`, and `not_after`; it MUST include verifiable issuer/key lineage and revocation evidence/reference. The issuer MUST be the Membership Authority established by a valid Tier-1 designation for that exact Album. No wildcard, omitted/empty scope, or implicit inheritance is allowed.
10. Verifier MUST exact-match the designation's `designated_authority_subject_id`, Manifest `authority_subject_id`, carrier issuer subject, canonical `album_id`, signer subject/key, purpose, and validity window. Any mismatch is rejected. Purpose MUST be exactly `ALBUM_MEMBERSHIP_SIGNING`; `CONTAINER_PACKAGING`, `asset:publish`, `identity:manage`, generic scope, or broader capability is never equivalent and never a fallback.
11. Eligible Membership Authority subject classes are existing Nexa Identity Individual Creator and Organization subjects, but only when Tier-1 Authority Designation is valid. No new identity root, Album-specific root, hardcoded ecosystem root, or hidden global authority is introduced. Album Signer remains a separate subject/key bounded by `(album_id, purpose=ALBUM_MEMBERSHIP_SIGNING, signer_subject_id, signer_key, validity_window)`. Separation of duties is supported: an authority subject may authorize an automated CI/CD bot, Studio packaging agent, or separate Album Signer without transferring Genesis Root Key or Active Level-1 Key custody. No subdelegation is granted by this decision.

**Temporal, revocation, failure, and PE-01 isolation rules.**

12. `not_before`/`not_after` and designation validity use trusted-time policy. Revocation follows PO-approved Dual-Horizon Time Rule §13.12.11.A.3 clause 4a.1: signed `revoked_at` is the internal revocation time and governs the internal relationship when verifiable notice is received; authoritative Registry/Event Store/Revocation List `recorded_at` is the public-verifier cut-off. Public verification MUST NOT retroactively apply revocation from `revoked_at` alone before `recorded_at`. Offline verification uses the latest official snapshot/evidence and MUST disclose freshness limits; stale/unavailable evidence MUST NOT silently yield authenticated membership where freshness is required.
13. Missing/invalid designation anchor, unproven Album-wide issuer rights, missing/invalid authority carrier, invalid issuer authority, scope/purpose/subject/key mismatch, expiry, effective public revocation, unresolved dispute/conflict, invalid Album Signer signature, or required-but-stale/unavailable evidence yields Album Membership `UNAUTHENTICATED / REJECTED` or `INVALID` according to the reason code. Fail-closed applies to the Album membership declaration only. It MUST NOT invalidate, downgrade, or mutate the independent signature, Genesis/ownership, Registry trust, asset trust, integrity, or standalone verification result of any child `.nx`; it MUST NOT create a global playback gate. PE-01 per-member JIT authorization remains authoritative.
14. Work packages: WP-04 MUST implement/resolve the Tier-1 designation evidence and Tier-2 capability issuance, identity/key binding, embedded Origin Declaration, embedded Authority Evidence Carrier, federated/Registry provenance and conflict resolution, lifecycle/revocation, production verifier, and adversarial negative tests. WP-05 MUST integrate the complete embedded Tier-1 and Tier-2 evidence objects, authority_subject_id, and ordered member declarations into Album creation, persistence, reload/reconstruction and recovery within Zero-DDL. The Manifest payload is the single persisted/reconstructed cryptographic evidence unit; offline verification MUST NOT require sidecar storage, URI dereferencing, external document retrieval, or multi-key blob references for designation/delegation evidence. Any serialized schema, signature scope, API/persistence detail required to make these predicates implementable MUST be specified in this PLAN before Gate B PASS; Programmer may identify compatible existing integration points but may not redesign the approved authority model. Both work packages remain post-authorization implementation/test work, after Gate A PASS, Gate B PASS, and separate explicit PO authorization.

This resolves the PO-approved principle that a Membership Authority must be explicitly designated for the exact Album and the PO-approved Opsi A (Embedded Evidence) decision. It does not claim that Registry publication, Origin Declaration issuance, embedded evidence serialization, or verifier implementation already exists; it does not independently prove any particular rights-holder's authority; and it does not authorize coding.



#### 16.16.4B A1 Complete Evidence Closure — canonical evidence structure and offline verifier contract

**PO decision: A1 APPROVED. AA disposition: NORMATIVE ARCHITECTURE CONTRACT.** This section implements the PO decision in the canonical Manifest, JCS, evidence, and verifier contracts. It does not assert that these structures or verifiers already exist in source code.

**1. Canonical Manifest object shape**

The canonical top-level object is exactly the field set defined in §16.2: schema_version, album_id, origin_declaration, authority_subject_id, authority_evidence, signer, members, and signature. origin_declaration is the complete Tier-1 signed declaration and A1 evidence closure. authority_subject_id must equal origin_declaration.designated_authority_subject_id. authority_evidence is the complete Tier-2 signed Authority Evidence Carrier and its embedded signer/issuer proof material. No external URI, detached evidence file, ZIP sidecar, or network locator may substitute for any required proof object. Unknown fields are rejected.

**2. Tier-1 Origin Declaration structure**

origin_declaration is one structured, closed-schema object with these required logical fields: schema_version; album_id; designated_authority_subject_id; issuer_subject_id; issuer_key_ref; authority_scope; issued_at; not_before; not_after; evidence_closure; signature.

The declaration signature is Ed25519 over RFC 8785 JCS UTF-8 of the complete Origin Declaration object after removing only its own signature property. All other fields, including every evidence object and proof signature within evidence_closure, are covered by this declaration signature. No field may be omitted from the preimage by an implementation-specific rule.

**3. Required Tier-1 evidence_closure contents**

evidence_closure is closed-schema and MUST embed, in full, each proof category required for issuance-time verification. A reference that requires an external fetch is not a substitute:

1. genesis_identity_credential: complete signed Genesis Root Certificate/identity credential for the declaring issuer, including public-key material and issuer/subject binding required by the existing Nexa Genesis/Identity format.
2. key_lineage_proofs: ordered complete signed proof objects establishing the issuer's key lineage from Genesis Root through every applicable succession, rotation, and recovery transition to the signing key. For Organization subjects, include existing 2-Step recovery predicates, recovery-key digest match, signed JCS payload, monotonic sequence, and competing-branch/conflict evidence required by the existing Organization Identity contract.
3. active_signing_key_proof: complete evidence that issuer_key_ref was the single valid Active Level-1 key for the issuer Subject ID at issued_at under existing timestamp-resolution and lifecycle rules.
4. album_rights_basis: complete signed Ownership Evidence and/or publisher-origin authority evidence establishing the issuer's authority over the Album as a whole and supporting exact album_id. It MUST preserve the White Paper boundary Ownership Evidence ≠ Licensing Authority: commercial license authority, buyer entitlement, or a license grant alone cannot substitute for Album-wide origin/rights authority. Member-level Creator signatures, ownership of individual members, Registry operator status, or a bare assertion are insufficient.
5. federation_provenance: complete signed Registry Authority evidence and/or Federated Trust attestations/proof objects needed to establish provenance and authority of participating issuer/registry assertions. For offline membership authentication, this MUST include valid Registry Authority evidence sufficient under the existing Nexa trust model; Creator self-signed ownership evidence alone MUST NOT be promoted to Registry Verified. The evidence must terminate at an existing locally trusted Registry/Nexa anchor and be verifiable without network access. This does not make a Registry operator the rights-holder and does not replace the underlying Album-wide rights basis.
6. issuance_status_evidence: complete available authoritative status/revocation evidence and snapshot metadata needed to evaluate identity, key, issuer authority, and designation status at issuance, including authoritative source identity, sequence/version or equivalent ordering, and recorded-time information under the Dual-Horizon rule.

The Origin Declaration signature authenticates the assembled declaration and exact evidence closure as one declaration. It does not replace independent verification of native signatures and authority semantics of embedded Genesis, key-lineage, rights, and federation proof objects. Each embedded credential/proof MUST be validated according to its own existing Nexa normative format and signature-preimage rules. This clause does not invent a new Genesis certificate format or rewrite existing credential signatures.

**4. Tier-2 Authority Evidence Carrier closure**

authority_evidence MUST embed the complete identity/key-lineage proof material needed to verify the designated Membership Authority's subject and signing key at carrier issuance; the carrier issuer's authorization to grant exact ALBUM_MEMBERSHIP_SIGNING for exact album_id; the Album Signer subject/key binding and timestamp-correct active key; all required delegation lineage and validity predicates; and available issuance-time revocation/status evidence. A proof reference requiring a remote Registry, external document store, sidecar, or URL is insufficient for A1. Existing native signed proof objects are embedded without changing their native signature semantics. The carrier signature is Ed25519 over RFC 8785 JCS UTF-8 of the complete Authority Evidence Carrier object after removing only its own signature property. The carrier is a PE-02 Album-specific signed evidence object; embedded native Identity/Genesis/delegation proof objects retain their own existing signature-preimage formats. The outer Manifest signature covers the entire carrier including its inner signature and proof objects.

**5. Trust anchor and offline trust boundary**

A1 is complete evidence closure, not self-rooted trust. The verifier MUST use the existing Nexa trust model and locally provisioned trust-anchor material/configuration already accepted by that verifier. An embedded Genesis Root Certificate, issuer key, Registry attestation, or any other Manifest-supplied key MUST NOT be promoted to a trust anchor solely because it is present, self-signed, or linked by internally consistent signatures. The embedded chain must terminate at an independently trusted existing Nexa anchor. No Album-specific root, hidden global authority, hardcoded ecosystem root, or Manifest-selected trust anchor is permitted.

Basic offline verification MUST NOT perform network fetches and MUST NOT require external evidence-file access. If the verifier lacks the necessary pre-provisioned existing trust anchor, required embedded proof is missing/invalid, or a proof chain cannot be resolved deterministically, the result is NOT AUTHENTICATED.

**6. Signature layering and byte-domain**

There are three distinct signature layers: (a) Tier-1 Origin Declaration issuer signature over the full Origin Declaration excluding only its own signature property, using JCS as specified above; (b) Tier-2 Authority Evidence Carrier Ed25519 signature over RFC 8785 JCS UTF-8 of the full carrier excluding only its own signature property; and (c) Tier-3 outer Album Manifest signature over the full canonical Manifest excluding only the top-level signature property, using RFC 8785 JCS UTF-8 as specified in §16.4. Inner signature envelopes remain included in their containing signed objects. No signature signs itself. The outer signature binds the exact Tier-1/Tier-2 evidence closure, inner proof signatures, and ordered members.

**7. Offline verification sequence and result semantics**

The verifier MUST: (1) strict-parse the Manifest and reject duplicate keys, malformed encoding, unsupported schema, unknown fields, invalid types, and prohibited null/empty values; (2) validate closed schemas and exact cross-field bindings for album_id, authority_subject_id, designated authority, carrier issuer, signer subject/key, purpose, and validity; (3) validate the embedded Genesis/Identity chain against the existing locally provisioned Nexa trust anchor; (4) validate all key-lineage/recovery proofs, monotonic sequence, timestamp-correct active key, and absence of unresolved competing branches; (5) validate native signatures/scopes in album_rights_basis and federation_provenance and establish Album-wide authority; (6) validate Tier-1 Origin Declaration signature and designation binding; (7) validate Tier-2 carrier signature, Membership Authority authorization, exact ALBUM_MEMBERSHIP_SIGNING purpose, Album ID, signer subject/key, delegation lineage, validity, and embedded signer key proof; (8) validate outer Manifest signature over Signature-Stripped JCS; (9) validate ZIP/Manifest bijection, child .nx sizes, and member_sha256 values; and (10) evaluate available revocation/status evidence under the PO-approved Dual-Horizon rule and report freshness separately from issuance-time proof validity.

When all cryptographic and authority predicates pass using the embedded closure and existing local trust anchor, the verifier may report the PO-approved indicator: AUTHENTICATED (OFFLINE EVIDENCE — VERIFIED AGAINST EMBEDDED CLOSURE). The result MUST separately expose the status/freshness boundary, including latest embedded snapshot timestamp/source and whether current authoritative revocation status is unavailable, stale, or freshly confirmed. The indicator MUST NOT be represented as proof of current non-revocation where no sufficiently current authoritative status is available. A later known authoritative revocation or unresolved conflict MUST be applied under Dual-Horizon and cannot be overridden by embedded issuance evidence. This indicator is an Album Membership issuance-evidence result only; it MUST NOT be conflated with the child .nx canonical Registry Trust status or standalone PE-01 result. Membership authentication and revocation freshness MUST be separate result dimensions (at minimum: membership_evidence_status and revocation_freshness_status). A stale/unknown freshness state MUST remain visible and MUST NOT be silently promoted to current TRUSTED / Registry Verified status under the existing White Paper trust semantics.

**8. Evidence-size and resource policy**

The PO's 5–10 KB estimate is a planning estimate only, not a normative size guarantee, quota, or acceptance threshold. Actual serialized size and verifier resource cost depend on key rotation/recovery depth, certificate chain, rights evidence, federation provenance, and revocation snapshots and must be measured in B-07. No proof may be truncated or externalized to meet an assumed size estimate. Any resource cap must be evidence-based, explicit, and fail-closed.

**9. Compatibility and change control**

This contract reuses existing Nexa Genesis, Identity, Organization Identity, ownership/rights, Federated Trust, Registry, and Dual-Horizon semantics. It does not create a new trust root or alter PE-01 standalone .nx trust. If a required proof type has no stable serializable representation or its native signature semantics cannot be verified offline, that is an explicit architecture compatibility defect to be resolved by AA before Gate B PASS. Programmer may provide bounded source evidence about the existing representation but may not invent a substitute format. Schema evolution requires an explicit supported schema_version; silent omission, externalization, or permissive parsing is prohibited.

**10. A1 source-evidence disposition — no-repeat boundary**

The A1 evidence package and supplements are the bounded source-evidence submission available for this planning cycle. AA will not request a repeat or expanded Programmer investigation. The evidence establishes only the primitives and call paths expressly documented in A1; it does not establish a complete serialized native proof schema and offline verifier call path for every category below. Items not established by that submission remain `NOT VERIFIED — A1 EVIDENCE DOES NOT ESTABLISH THE REQUIRED SERIALIZED REPRESENTATION / VERIFIER PATH`. AA must not upgrade them to PRESENT, infer a schema from conceptual descriptions, or fabricate native source semantics:

1. Genesis Root Certificate / Creator Genesis identity credential: exact serialized form, signed fields/preimage, issuer/subject/public-key binding, verification function, and trusted-anchor termination.
2. Organization and Individual Creator key-lineage evidence: exact recovery/succession assertion shape, signed payload/preimage, recovery-key digest input, sequence/previous-key linkage, active-key-at-timestamp resolution, and conflict detection.
3. Album-wide Ownership Evidence / publisher-origin authority: exact native evidence object(s), issuer and subject binding, asset/Album scope semantics, historical owner-at-time resolution, and verification path. Explicitly distinguish Ownership Evidence from Licensing Authority; do not use a license grant as a substitute for Album-wide rights authority.
4. Registry Authority / Federated Trust proof: exact signed attestation or Registry evidence object, registry identity versus registry trust binding, federation provenance, locally provisioned trust-anchor lookup, and offline verification path. Include the Registry-authenticated evidence required by the existing OFFLINE TRUSTED contract.
5. Revocation Proof / status snapshot: exact signed proof structure, authority binding, recorded-time/sequence/version fields, Dual-Horizon interpretation, and offline freshness evaluation.
6. Tier-2 Membership Authority / Album Signer identity and delegation: exact reusable native credential/delegation object(s), purpose/scope binding, signer key binding, validity, issuer lineage, and revocation proof.

For each category, preserve only the evidence state supported by A1 (PRESENT / PARTIAL / NOT FOUND / NOT VERIFIED) and its declared repository, branch, commit, directories and excerpts. No new Programmer handoff is issued by this reconciliation. The six categories remain an AA architecture-compatibility ledger: Genesis identity credential and trust-anchor termination; Individual Creator and Organization key-lineage serialization; Album-wide rights-basis object and verifier; Registry Authority/Federated Trust proof and offline trust-anchor path; signed revocation/status snapshot and Dual-Horizon evaluation; and Tier-2 capability/delegation native object and verifier. A category not concretely established by A1 remains NOT VERIFIED. Gate B MUST NOT PASS while an indispensable offline proof representation, native signature semantics, or trust-anchor verification path remains unresolved. This is a planning gate, not a request to repeat PSV and not authorization to change code/schema/configuration/runtime. AA owns architecture decisions; PO approval is required only if resolution changes product policy or frozen invariants.

**10. Acceptance evidence after implementation authorization**

Post-authorization acceptance must include canonical schema fixtures; positive/negative proof-chain vectors; Genesis/root/key-lineage/recovery fixtures; valid/invalid Album-wide rights-basis fixtures; federation provenance/conflict fixtures; carrier/delegation fixtures; online/offline parity vectors; no-network offline tests; missing-anchor and wrong-anchor rejection; stale/newer revocation handling under Dual-Horizon; tamper tests for every nested proof/signature layer; cross-language JCS/Ed25519 vectors; and PE-01 non-regression evidence. These are implementation/test deliverables, not claims of present source support and not prerequisites requiring code to exist before Gate B.

**Gate effect:** A1 resolves the PO policy choice and evidence-closure architecture. It does not close B-09 implementation, B-07 benchmark, or WP-04/WP-05. It does not authorize implementation.

#### 16.16.4 Status and gate effect

- B-09 remains an OPEN implementation workstream because the Programmer evidence report identifies absent Album-specific capability/carrier/federated resolution/production verifier wiring. The PO-approved per-Album Membership Authority, canonical Manifest binding, A1 evidence closure, carrier predicates, exact scope/purpose, Dual-Horizon lifecycle, fail-closed behavior, and PE-01 isolation are specified in §16.5/§16.16.4A/§16.16.4B. Implementation and tests are post-authorization; they are not preconditions to Gate B merely because the code does not yet exist.
- AC-07, AC-08, AC-33, and AC-34 may remain IMPLEMENTATION / POST-AUTHORIZATION TEST PENDING; their pending code/tests do not block Gate B if expected behavior, negative/adversarial coverage, and acceptance evidence are fully specified.
- B-09 remains an OPEN implementation workstream because the Programmer evidence report identifies absent Album-specific capability/carrier/federated resolution/production verifier wiring. It is not required to be implemented and independently runtime-verified before Gate B or PE-02 authorization; that would create a circular gate. Before authorization, AA must complete the minimum implementable contract and work package in this canonical PLAN, including any serialized carrier/API/persistence decision that cannot safely be deferred to implementation.
- The source-evidence handoff itself is evidence gathering only. It does not authorize code, schema, database, endpoint, configuration, or runtime changes.
- Implementation can begin only after Gate A PASS, Gate B PASS, and a separate explicit PO implementation authorization. Plan approval or this handoff is not implementation authorization.
- Sprint 16 and PE-01 remain CLOSED/FROZEN; Sprint 17 remains NOT STARTED.


### 16.17 Mandatory disposition when required evidence is NOT FOUND

1. The Programmer's evidence handoff is evidence-only. It does not authorize implementation. However, a `NOT FOUND` result is not permission to leave a required capability as an indefinite research item: the corresponding implementation or benchmark work package is mandatory in this canonical PLAN.
2. **B-04 / NC-08:** if the existing source does not prove a Zero-DDL-compatible durable receipt, mapping, idempotency and reconciliation path, plan implementation using an existing compatible durable store. If no such store exists, B-04 remains BLOCKED and the incompatibility with the approved Zero-DDL invariant must be escalated for an explicit PO decision. Do not silently introduce DDL.
3. **B-05 / NC-09:** if child `.nx` hash persistence/mapping is absent, plan implementation through an existing Zero-DDL-compatible mechanism. Preserve `acquired_package_sha256` as wrapper hash; never repurpose it as child hash. If Zero-DDL compatibility is impossible, remain BLOCKED and report the exact incompatibility.
4. **B-07 / NC-07:** if benchmark evidence is absent, plan and execute the reproducible four-payload-class benchmark in §16.14. No hard numeric quota is approved until raw measurements, capacity rationale and reproducibility evidence exist.
5. **B-09 / NC-04:** if any subject/key/capability/issuer/federation/lifecycle/verifier predicate is absent, mandatory implementation scope is defined in §16.16. Do not treat generic Organization Identity or delegation as proof of Album membership signing capability.
12. **NC-06 / AC-28 / AC-29:** if Album identity, ordered member association, persistence, reload or recovery is absent, plan implementation through the existing Zero-DDL-compatible storage/publication architecture. If no compatible mechanism exists, remain BLOCKED and escalate the exact Zero-DDL conflict; do not invent tables or infer association from catalog metadata.
7. **AC-32 / NC-13:** if a definitive viewer completion signal is absent for a supported platform/payload pair, plan implementation of the viewer lifecycle event and its production wiring, event identity/deduplication, resource release and fresh next-member JIT. No timeout or UI-visibility heuristic may substitute for completion.
8. A source claim marked NOT FOUND must identify repository, branch, commit SHA, searched directories, exact search terms/commands, and command exit codes. A claim marked PRESENT must include exact source path/line ranges, raw excerpts, caller/callee chain, DDL/evidence shape where relevant, exact test command, exit code, and raw output.
9. For every NOT FOUND result, the returned handoff must explicitly list the affected requirement, the absent implementation predicate, the corresponding mandatory plan work package above, dependencies, and objective acceptance evidence. Programmer must not silently omit a missing predicate from the return.
10. All implementation work remains gated: Gate A PASS → Gate B PASS → separate explicit PO authorization. This mandatory planning disposition does not authorize code, schema, database, endpoint, configuration, or runtime changes. Sprint 16/PE-01 remain frozen; Sprint 17 remains NOT STARTED.


### 16.18 Integration of Programmer Source Evidence & Mandatory Work Packages

This section integrates the temporary Programmer report PE-02_SOURCE_EVIDENCE_AND_GAP_IDENTIFICATION_REPORT.md into this canonical PLAN. The temporary report is an evidence-delivery artifact only; this PLAN remains the sole retained canonical implementation plan. Product Owner may delete the temporary report after confirming this integration is complete. No second plan or permanent evidence report is created by this section.

**Evidence baseline received:** repository whisnu/nexa, branch main, HEAD and origin/main commit fc08a5c7ac6aa1b0e4bcf64dc264666f149e1956; report timestamp 2026-11-10T16:26:00+07:00; canonical plan baseline blob reported as 5dcb5ff0261aea9ae434d02af451ca4d4cde5a62. The report states the inspection was read-only and no tracked source, schema, migration, configuration, or runtime files were modified. These are Programmer-submitted source-evidence claims; they are not represented here as independent AA verification or runtime proof.

#### 16.18.1 Consolidated evidence disposition

| Requirement | Programmer-reported source finding | Canonical disposition |
|---|---|---|
| B-04 / NC-08 / CONF-03 | Existing PostgreSQL acquisitions/entitlements are 1:1; local SQL transaction and row lock exist; no durable multi-member checkout receipt/mapping, idempotency key, daemon status lookup/reconciliation worker, or per-member refund implementation found in examined scope. External License Daemon side effect can outlive local rollback. | OPEN / BLOCKED. Mandatory WP-01. Preserve approved Model B, independent member acquisitions/entitlements, immutable Checkout Manifest SSOT, partial fulfillment/member-level recovery, and Zero-DDL. WP-01 must NOT require all N members to commit atomically as one all-or-nothing transaction; it must implement the approved per-member durable execution/receipt and recovery semantics. No claim of 2PC or compensation unless implemented and proven. Any storage mechanism must be selected/validated against existing source before coding; no DDL invention. |
| B-05 / NC-09 | acquired_package_sha256 is reported to hash the complete delivery wrapper ZIP; child .nx hash persistence and mapping to member/acquisition/entitlement were not found. | OPEN / BLOCKED. Mandatory WP-02. Preserve wrapper hash semantics and implement distinct member_sha256 persistence/retrieval/mapping through a Zero-DDL-compatible mechanism. |
| B-07 / NC-07 | Four-payload benchmark dataset/environment manifests, raw repeated measurements, boundary/adversarial suite, and reproducibility evidence were not found. | OPEN / BLOCKED FOR CAPACITY ACCEPTANCE. Mandatory WP-03 under §16.14. No universal numeric ZIP cap is inferred. Runtime must fail closed when safe bounded deployment configuration is absent. Benchmark and capacity acceptance are post-authorization work unless separately performed as non-mutating measurement; they are not a precondition that PE-02 code already exist. |
| B-09 / NC-04 / CONF-01 | Organization Subject ID, root recovery, lineage and Active Level-1 key resolution are reported present with passing existing identity/audit test suites. Individual Creator subject/lifecycle is partial. Explicit ALBUM_MEMBERSHIP_SIGNING, Album authority evidence carrier, Album-specific federated authority resolution, lifecycle for this capability, production Album Manifest verifier wiring, and Album-specific positive/negative tests were not found. | OPEN / IMPLEMENTATION WORKSTREAM SPECIFIED. Mandatory WP-04 under §16.16.4A/§16.16.3; WP-05 integrates authority fields into Album creation/persistence. This is an expected new PE-02 capability, not a missing White Paper/Roadmap baseline requirement. Reuse existing identity foundations; implementation and test execution follow authorization. |
| NC-06 / AC-28 / AC-29 | No Studio multi-member Album identity/ordered association/collective persistence/reload/recovery found; current reported Studio forge/publish path handles one asset at a time; Marketplace catalog records are individual-asset oriented. | OPEN / BLOCKED. Mandatory WP-05. Define Album identity and ordered member association, persistence, reload and recovery within Zero-DDL and existing publication/storage constraints. Do not infer association from catalog ordering or timestamps. |
| AC-32 / NC-13 | Desktop audio has a local ended listener that rotates GUI library assets, but no canonical member/viewer event identity; Desktop video/document/image and all Mobile payload completion signals absent; no dedupe, authorization release or next-member JIT wiring found. | OPEN / BLOCKED. Mandatory WP-06. Preserve PO-approved Auto-Next; implement normalized VIEWER_COMPLETED, per-instance dedupe, resource/authorization release, and fresh next-member JIT. Do not replace with timer, UI visibility, or manual Next. |

#### 16.18.2 Evidence quality and audit boundary

1. The report provides repository/branch/commit baseline, DDL/source paths and line ranges, search commands, selected source excerpts, and two existing Organization Identity test-suite invocations with exit code 0. It is accepted as the Programmer's evidence submission for the bounded scope in §16.15; Programmer is not instructed to repeat the same PSV against the same commit/scope.
2. The reported test passes establish only the reported existing Organization Identity baseline tests. They do not establish Album Signer capability, Album Manifest verifier integration, Mobile Player completion, benchmark capacity, B-04 durable recovery, or runtime deployment behavior.
3. The report's NOT FOUND IN EXAMINED SCOPE results are bounded to its declared repository, commit, directories, and search commands. They must not be generalized to unexamined repositories, branches, deployment environments, or runtime services.
4. AA review of this report is a review of Programmer-submitted evidence and its consistency with the canonical plan, not a claim of independent source inspection and not a request for a new broad PSV. If a cited source excerpt or path is materially ambiguous, AA identifies only that exact discrepancy and the minimum clarification needed; do not restart closed searches.
5. Programmer's proposed WP-01 wording in the temporary report is not adopted where it conflicts with approved partial fulfillment/member-level recovery. The canonical WP-01 disposition in this PLAN controls.

#### 16.18.3 Gate effect and single-artifact rule

1. This evidence integration does not close B-04, B-05, B-07, B-09, NC-06, or AC-32; it converts their previously unstructured evidence gaps into explicit, commit-pinned implementation/benchmark work packages.
2. Gate A evaluates whether this canonical PLAN consistently incorporates the evidence, PO decisions, AA contracts, NC/AC/blocker registers, dependencies, and acceptance criteria. Gate A does not require implementation to be complete.
3. Gate B evaluates whether the work packages are sufficiently specified and executable after authorization. It does not require the missing capabilities, runtime wiring, benchmark outputs, or post-implementation tests to exist before authorization. Any architecture decision that is genuinely indispensable before coding must be completed by AA in this PLAN, not delegated as an unbounded research task to Programmer.
4. Sequence remains: Gate A PASS → Gate B PASS → separate explicit PO authorization. Gate B may not be held BLOCKED merely because the implementation gaps it is intended to authorize remain unimplemented. Conversely, neither Gate A nor Gate B PASS alone authorizes implementation.
5. Only PE-02_HANDLING_ALBUM_IMPLEMENTATION_PLAN.md is the canonical retained plan. The temporary source-evidence report may be deleted by PO after review; no one may require it as a second permanent plan artifact.
6. Sprint 16 and PE-01 remain CLOSED/FROZEN; Sprint 17 remains NOT STARTED; no implementation is authorized by this integration.

### 16.19 Architecture Baseline — Existing Capability, Required New Capability, and Normative Decisions

**Purpose and phase boundary**

Bagian ini mengonsolidasikan hasil A1 dan keputusan arsitektur AA sebagai Architecture Baseline untuk perencanaan implementasi Album Handling. Album Handling belum tersedia sebagai kemampuan produk yang selesai; kemampuan tersebut adalah target yang akan dirancang, dibangun, diuji, dan diintegrasikan melalui PE-02 setelah otorisasi implementasi yang terpisah.

PE-02 pada status saat ini berada dalam **PLANNING**, bukan IMPLEMENTATION. Karena itu:
- A1 adalah *architecture-enabling evidence assessment*: memahami fondasi Nexa yang benar-benar dilaporkan tersedia, membatasi klaim existing capability, dan mengidentifikasi gap yang harus direncanakan.
- A1 bukan audit yang mensyaratkan Album Manifest, Album Signer, Album Membership Authority, Album persistence, atau Album verifier sudah ada.
- Ketiadaan fitur Album-spesifik merupakan *required new capability* jika memang ditetapkan dalam kontrak PE-02; hal itu bukan otomatis kegagalan desain atau alasan mengulang source investigation.
- Source evidence digunakan secara proporsional untuk mencegah desain bergantung pada asumsi yang salah. Klaim source tetap dibatasi pada repository, revision, direktori, dan pencarian yang dinyatakan oleh Programmer.
- Penetapan kontrak arsitektur adalah tanggung jawab AA sesuai hierarki otoritas §1.2/§3.1. Programmer tidak diberi kewenangan untuk mengisi gap dengan desain sepihak.

Bagian ini tidak mengubah keputusan PO, kontrak PE-01, Sprint 16 frozen baseline, Zero-DDL, maupun status otorisasi. Bagian ini juga tidak menyatakan bahwa kemampuan baru telah diimplementasikan.

#### 16.19.1 Existing Capability — fondasi Nexa yang dilaporkan tersedia

Klasifikasi berikut adalah kondisi existing berdasarkan evidence Programmer yang telah diintegrasikan pada §16.18 dan batas assessment A1. Ini bukan klaim bahwa AA telah melakukan independent source/runtime verification atas seluruh repository.

| Area | Existing capability / evidence yang dilaporkan | Batas yang wajib dipertahankan |
|---|---|---|
| Identity Subject | Organization Subject ID, Genesis-root identity, root recovery/lineage, dan Active Level-1 key resolution dilaporkan tersedia. | Individual Creator subject/lifecycle hanya PARTIAL pada evidence yang diserahkan; jangan mengklaim end-to-end Individual Creator flow telah terbukti. |
| Identity cryptography | Identity assertion menggunakan JCS/Ed25519 pada mekanisme yang diperiksa. | Setiap proof type tetap mengikuti native signed payload/preimage-nya sendiri; jangan menganggap semua objek Nexa memakai satu preimage generik. |
| Organization tests | Existing identity/audit test invocations dilaporkan PASS pada scope yang diserahkan. | Test primitive/subject-agnostic tidak boleh dilabeli Organization-specific. Test tersebut tidak membuktikan Album capability. |
| Registry identity | RegistryIdentity memiliki signed canonical fields sebagaimana source mapping A1; signing dan verification memakai canonicalization yang sama. | `SupportedFeatures` tidak termasuk preimage yang ditunjukkan; keberhasilan IdentitySignature tidak mengautentikasi field tersebut secara kriptografis. |
| CRL/revocation | Source excerpt menunjukkan CRL signature preimage mencakup `registry_id` dan `updated_at`. Konfigurasi memuat `ISSUER_PRIVATE_KEY_HEX` dan `ISSUER_PUBLIC_KEY_HEX`. | `RevokedKeys` tidak tercakup dalam preimage yang ditampilkan. Pasangan kriptografis, pemilik/otoritas key, distribusi trust, dan verifier eksternal tidak boleh dianggap terbukti apabila evidence tidak menunjukkannya. |
| Registry/federation resolution | Registry identity/federation primitives dan evaluator online dilaporkan tersedia dalam scope pemeriksaan. | Registry identity bukan dengan sendirinya Registry trust proof. Online classification bukan bukti freshness; offline self-contained proof/verifier tidak boleh diasumsikan tersedia. |
| Ownership evidence | OwnershipCertificate dengan scope asset-level/scalar `asset_id` dilaporkan ada dalam source scope yang diperiksa. | Album-wide rights/ownership authority tidak boleh diinferensikan dari ownership satu member. Status negatif hanya bounded ke examined scope. |
| Delegation | Generic delegation/key-lineage primitives dilaporkan tersedia, termasuk batas hierarki yang telah diperiksa. | Generic delegation tidak otomatis memberikan purpose `ALBUM_MEMBERSHIP_SIGNING`, exact `album_id` scope, atau Album Signer authority. |
| Existing member .nx / PE-01 | Member `.nx` tetap memiliki integrity, Genesis/ownership, Registry, license, dan playback trust lifecycle masing-masing sesuai baseline PE-01. | Album wrapper/Manifest tidak menggantikan atau mengubah standalone member trust. |
| Existing storage/transaction | PostgreSQL acquisition/entitlement dan local transaction/row-lock primitives dilaporkan tersedia. | Belum terbukti sebagai durable multi-member checkout receipt, immutable mapping, idempotency/reconciliation, atau member-level recovery yang disyaratkan B-04. |
| Existing client lifecycle | Desktop audio local ended listener dilaporkan ada. | Belum membuktikan normalized viewer-completion event, event identity/deduplication, resource release, dan next-member JIT untuk semua platform/payload. |

**Evidence qualification:** istilah PRESENT/PARTIAL/NOT FOUND dalam tabel di atas adalah klasifikasi terhadap evidence yang diserahkan dan examined scope, bukan pernyataan universal mengenai seluruh repository, semua branch, semua deployment, atau seluruh runtime.

#### 16.19.2 Required New Capability — kemampuan PE-02 yang harus dirancang dan dibangun

Kemampuan berikut merupakan target pembangunan Album Handling. Keberadaannya tidak dipersyaratkan pada source Nexa sebelum perencanaan selesai.

| Work package | Required new capability | Normative baseline / dependency | Planning disposition |
|---|---|---|---|
| WP-01 — Commercial bundle execution and recovery | Durable per-member execution receipt, immutable correlation/mapping, idempotency, status reconciliation, partial fulfillment, member-level recovery/refund. | §16.8, §16.8.1, approved Model B, immutable Checkout Manifest SSOT, independent member acquisitions, `bundle_checkout_id` independent identity, Zero-DDL. | Contract specified; Zero-DDL storage feasibility and external operation-status integration remain open dependencies. |
| WP-02 — Child member integrity mapping | Persist/retrieve exact child `.nx` `member_sha256` and map it to the correct Album member/acquisition/entitlement without changing wrapper-hash semantics. | §16.2–§16.3, B-05/NC-09, existing `acquired_package_sha256` remains wrapper-domain unless separately proven. | Byte-domain contract specified; existing durable field/storage mapping remains to be resolved without DDL. |
| WP-03 — ZIP capacity and resource acceptance | Reproducible four-payload-class benchmark, adversarial/boundary tests, measured resource envelope, and deployment-safe bounded limits. | §16.6–§16.7 and §16.14; no universal numeric cap inferred before measurements. | Benchmark protocol specified; measured capacity and production numeric limits remain pending. |
| WP-04 — Membership authority and verifier | Per-Album authority designation, exact capability/purpose, signed Tier-2 carrier, Album Signer lifecycle, federated resolution, embedded proof verification, and production Manifest verifier integration. | §16.5 and §16.16.4A/§16.16.4B; existing Identity subject/key foundations; no new trust root. | Normative semantic contract specified; Album-specific implementation and tests are post-authorization. |
| WP-05 — Album creation, identity, persistence and publication | Stable Album identity, ordered member association, Forge New and Select Existing flows, collective persistence/reload/recovery, Manifest/evidence generation and publication integration. | §5.4, §16.2, NC-01/NC-06, Zero-DDL, existing Studio/storage/publication constraints. | Product/manifest semantics specified; concrete compatible persistence/publication integration remains a planning dependency to resolve without inventing DDL. |
| WP-06 — Viewer completion and Auto-Next | Normalized `VIEWER_COMPLETED` event, per-instance identity/deduplication, release of current member resources/authorization, and fresh JIT authorization for the next member. | §5.2, §16.11, NC-13/AC-32; PO-approved sequential Auto-Next behavior. | Lifecycle contract specified; platform/payload event wiring and acceptance coverage are post-authorization implementation work. |

No work package above authorizes source, schema, migration, endpoint, configuration, or runtime changes. Implementation and implementation test execution remain post-authorization.

#### 16.19.3 Normative Architecture Decisions — decisions already established

The following decisions are the active architecture baseline and must not be reopened or weakened by implementation convenience:

1. **Album product model:** Album is a logical collection of independent canonical `.nx` members. ZIP is only the transport/packaging envelope; no `album.nx` or new .nx container is created.
2. **Canonical Manifest:** one closed-schema JSON Manifest with the exact top-level field set and ordered `members[]` defined in §16.2 and the detailed Tier-1/Tier-2 evidence structure in §16.16.4A/§16.16.4B. Unknown fields, duplicate JSON keys, unsupported schema versions, and invalid bindings fail closed.
3. **Three distinct authority/signature tiers:** Tier-1 Origin Declaration proves who may designate Album Membership Authority for the exact Album; Tier-2 Authority Evidence Carrier proves that the designated Membership Authority authorizes a separate Album Signer for exact `album_id` and exact `ALBUM_MEMBERSHIP_SIGNING` purpose; Tier-3 Album Signer signs the complete canonical Manifest. Inner native proof signatures retain their own native preimage semantics.
4. **Per-Album Membership Authority:** an explicitly designated existing Nexa Identity Subject (Individual Creator or Organization) is bound to exact `album_id`. Subject class, Creator status, ownership of one member, Registry operator status, key possession, generic delegation, or valid signature alone is insufficient.
5. **Embedded Evidence / A1 Complete Evidence Closure:** complete Tier-1 origin/rights/identity/key-lineage proof material and complete Tier-2 signer/delegation proof material are embedded as structured objects in the Manifest. External URI, sidecar, detached file, or network fetch cannot substitute for proof required for basic offline verification.
6. **No self-rooting:** embedded certificates and keys are proof material, not trust anchors. Verification must terminate at an existing independently provisioned Nexa trust anchor. No Album-specific root, hidden global authority, hardcoded ecosystem root, or Manifest-selected trust anchor.
7. **Cryptographic binding:** outer Manifest signature is Ed25519 over RFC 8785 JCS UTF-8 of the complete Manifest after removing only the top-level `signature` property. It binds the complete Tier-1 and Tier-2 evidence objects, their inner signatures, signer, and ordered members.
8. **Ownership and licensing separation:** Album-wide rights/ownership authority is not inferred from member ownership or license entitlement. Licensing Authority remains a separate decision domain and active license remains mandatory for playback authorization.
9. **Dual-Horizon revocation:** internal `revoked_at` and public authoritative `recorded_at` retain their approved distinct semantics. Offline issuance-time evidence does not prove current non-revocation; freshness remains a separate visible result dimension.
10. **Offline status truth:** the approved indicator `AUTHENTICATED (OFFLINE EVIDENCE — VERIFIED AGAINST EMBEDDED CLOSURE)` describes successful verification of embedded issuance evidence against an existing local trust anchor. It must not be represented as current Registry freshness or current non-revocation.
11. **Stage 8a/8b/8c:** Stage 8a is passive read-only digest diagnostics and may inspect queued/next member without authorization side effects. Stage 8b requires PE-01 integrity, Genesis/ownership, active license, and matching digest. Stage 8c can register decrypted buffer only for the current member.
12. **Player and Verify isolation:** Player authorization remains current-member JIT only; pre-verification of a queued member cannot authorize playback. Verify's result is not playback authorization. Preserve the PO-approved Verify behavior in §5.3/§10.3. Do not introduce Album aggregate status if PO-approved Option B excludes it.
13. **Member integrity:** `member_sha256` is the SHA-256 of the exact final child `.nx` bytes; wrapper ZIP hash and payload-internal digest remain separate byte domains.
14. **ZIP/filesystem safety:** bounded staged extraction, strict ZIP validation, path traversal/symlink/special-file rejection, descriptor-relative no-follow Safe-Open, atomic promotion, and cleanup are mandatory. Numeric resource limits remain benchmark-derived.
15. **Marketplace semantics:** preserve independent member acquisitions/entitlements, approved Model B, immutable Checkout Manifest SSOT, partial fulfillment/member-level recovery, automatic refund policy after objectively terminal unfulfillable state, and distinct `bundle_checkout_id`, `payment_order_id`, `acquisition_id`, Album ID, and member ID.
16. **Zero-DDL and frozen baselines:** no new DDL or schema migration may be assumed. Sprint 16 and PE-01 remain frozen; no regression of standalone member behavior.

These are architecture/product constraints, not claims that the implementation exists.

#### 16.19.4 Architecture closure ledger — what is decided and what remains to be resolved in planning

| Area | Decision/contract status | Remaining planning closure before Gate A/B evaluation |
|---|---|---|
| Album logical model, ZIP envelope, member order | DECIDED / SPECIFIED | Cross-section traceability and AC/NC consistency only. |
| Manifest top-level field set, signature envelope, strict parsing, JCS signed set | DECIDED / SPECIFIED | Ensure every schema/path/field reference in earlier sections and AC register matches §16.2/§16.4/§16.16.4B. Do not invent new fields or alternate envelopes. |
| Tier-1/Tier-2/Tier-3 authority and embedded evidence closure | PO APPROVED / AA CONTRACT SPECIFIED | Ensure no contradiction with earlier evidence-ledger or source-mapping language. Exact native proof object compatibility must be treated as bounded implementation integration evidence; if a proof cannot be serialized/verified under its native semantics, AA must resolve that specific compatibility defect before Gate B PASS. |
| Existing trust anchors and offline verifier | PRINCIPLE DECIDED | Existing trust-anchor provisioning/verification compatibility must be represented accurately. Embedded keys cannot bootstrap trust. Current freshness remains separate. |
| Organization/Individual subject and Album capability | PRODUCT SUBJECT CLASSES APPROVED; ALBUM CAPABILITY SPECIFIED | Individual Creator existing lifecycle is partial; reuse/complete required integration in WP-04. Do not claim current end-to-end support. |
| CRL/revocation key chain | EXISTING EVIDENCE PARTIAL | Preserve NOT VERIFIED elements for key-pair relationship, authority, distribution, and verifier where evidence is insufficient. This is not permission to weaken the Dual-Horizon contract. |
| B-04 durable transaction/recovery | PRODUCT MODEL AND AA SEMANTICS DECIDED | Resolve exact Zero-DDL durable store/mapping and external License Daemon status/reconciliation interface. If no compatible mechanism exists, retain BLOCKED and escalate the precise Zero-DDL incompatibility; no silent DDL. |
| B-05 child hash storage | BYTE-DOMAIN DECIDED | Resolve exact Zero-DDL persistence and retrieval mapping. Wrapper hash cannot be repurposed. |
| B-07 ZIP numeric capacity | BENCHMARK METHOD DECIDED | Numeric limits require reproducible measurements and capacity rationale; do not invent values. |
| NC-06 Album persistence/Studio | PRODUCT FLOW AND IDENTITY REQUIREMENT SPECIFIED | Resolve concrete existing compatible storage/publication mapping and recovery behavior within Zero-DDL. |
| NC-13 viewer lifecycle | EVENT CONTRACT SPECIFIED | Platform/payload completion source, event identity, deduplication, resource release, and integration acceptance evidence belong to WP-06. |
| NC-15/NC-16 error and identifier consistency | NC-15 semantic dimensions specified but 20-code registry remains PROPOSED (§16.9/§6.15); NC-16 formula specified (§16.13) | Reconcile stable code registry, triggers, provenance and cross-register mappings; preserve B-04 receipt dependency for NC-16. |
| AC/NC/B/Work Package traceability | NOT YET GLOBALLY CLOSED | Perform AA-owned cross-section consistency pass; do not delegate another broad repository investigation. |

A planning dependency may remain OPEN/BLOCKED without implying the feature must already exist. It must, however, have a bounded decision, named work package, dependency, and objective acceptance evidence. Where the unresolved matter is an indispensable architecture choice (not a post-authorization implementation detail), AA must resolve it in this canonical PLAN before declaring the applicable gate passed.

#### 16.19.5 Required planning sequence and gate interpretation

The remaining sequence is:

1. **A1 evidence assessment:** sufficient for architecture planning when existing capabilities and evidence limitations are accurately bounded. The five A1 supplement documents are supporting assessment artifacts; they do not replace this canonical PLAN.
2. **Architecture Baseline:** this section classifies existing foundations, required new capabilities, and normative decisions.
3. **AA-owned contract/traceability reconciliation:** reconcile all active Manifest, NC, blocker, AC, WP, dependency, and gate statements in this single canonical PLAN. Resolve any indispensable pre-authorization architecture decision here.
4. **Gate A evaluation:** assess product truth, canonical plan consistency, complete contract definitions, PO decision traceability, and absence of material contradiction. Gate A does not require Album Handling code to exist.
5. **Gate B evaluation:** assess whether work packages are bounded, dependencies explicit, Zero-DDL/compatibility constraints understood, and post-authorization implementation/test acceptance criteria executable. Gate B does not require the new capabilities, runtime wiring, measured post-authorization benchmark deliverables, or implementation tests to exist merely because they are future work. It may remain BLOCKED only for a concrete unresolved prerequisite to safe execution, not because the implementation has not yet happened.
6. **Separate PO implementation authorization:** only after Gate A PASS and Gate B PASS may the PO decide whether to authorize implementation. Neither gate result itself grants authorization.

No additional broad Programmer investigation is required merely to prove Album Handling exists. Any future source request must be tied to a specific, material compatibility question that cannot be resolved from the bounded A1 evidence and existing plan. The default next work is AA-owned planning and contract reconciliation.

### 16.20 Canonical cross-section and traceability reconciliation — AA disposition

Bagian ini adalah active reconciliation overlay untuk PLAN kanonis. Historical audit records tidak dihapus. Jika snapshot historis atau redaksi lama bertentangan, active status pada §13.1.1, §16.18, §16.19 dan §16.20 mengendalikan. Tidak ada perubahan kode, schema, endpoint, konfigurasi atau runtime yang diotorisasi.

##### 16.20.1 Authoritative cross-register mapping

Matriks berikut adalah pemetaan aktif dua arah. Setiap AC harus dapat ditelusuri ke NC primer dan blocker/dependency yang relevan; setiap NC harus menunjuk kembali ke AC penguji. Satu AC boleh menguji lebih dari satu NC bila batas kontraknya memang beririsan, tetapi tidak boleh menggabungkan domain hash, authority, atau lifecycle yang berbeda.

| Architecture area | NC | Blocker / dependency | AC | Work package / acceptance boundary |
|---|---|---|---|---|
| Manifest schema, ZIP Manifest entry and member binding | NC-01 | AA schema/entry completion; B-03 only for ZIP structural requirements; B-01/B-02 are parser/JCS implementation under NC-03 | AC-01, AC-02, AC-28, AC-30, AC-31 | WP-05 creation/persistence. AC-01/02 remain blocked by complete nested schema/version and ZIP Manifest entry name/location. AC-02 structural ZIP tests are distinct from numeric resource-capacity tests in AC-13. |
| Strict JSON parser and JCS serializer modules | NC-03 | B-01 strict parser; B-02 RFC 8785 serializer | AC-05, AC-06 | Post-authorization implementation modules and their duplicate-key/Unicode and RFC 8785 conformance vectors. These are not NC-01 schema blockers and must not be mapped to NC-01 as their primary contract. |
| Signature and verifier | NC-02 | B-08 | AC-03 | Signature contract §16.4; engine and cross-language/adversarial vectors post-authorization. |
| Identity, authority and signer lifecycle | NC-04 | B-09 | AC-07, AC-08 | WP-04 capability/evidence/verifier; WP-05 Manifest integration. No PO decision pending. A1 gaps remain NOT VERIFIED; no new Programmer handoff. |
| Genesis and payload digest | NC-05 | Genesis error-taxonomy residual (A-05 / NC-15 mapping where applicable) | AC-09, AC-10 | §16.12 fixes the audio digest field/path and byte-domain. AC-10's Genesis/packaging error distinction remains blocked on final deterministic error mapping and implementation. |
| Member integrity and Album persistence | NC-06 | B-05 only for child-hash persistence where applicable; NC-06 persistence/reload feasibility | AC-04, AC-11, AC-12, AC-28, AC-29, AC-31 | WP-02 child integrity; WP-05 Album identity/order/Studio persistence/reload. Preserve PE-01 frozen member behavior. |
| Child .nx hash persistence | NC-09 | B-05 | AC-16 | WP-02 / existing Zero-DDL field and receipt mapping. member_sha256 is the exact child .nx byte-domain; acquired_package_sha256 is not repurposed from its evidenced wrapper domain. |
| ZIP extraction and capacity | NC-07 | B-03 extraction security design; B-07 benchmark and numeric capacity ratification | AC-02 (structural ZIP requirements only), AC-13 (resource/capacity requirements) | WP-03. AC-02 validates entry type, archive integrity, naming and manifest/archive bijection; AC-13 validates only ratified resource limits after benchmark. B-07 numeric limits remain unratified. |
| Filesystem Safe-Open | NC-12 | B-06 | AC-20, AC-21 | Descriptor-relative no-follow, post-open validation, containment and platform-specific adversarial acceptance. Implementation/tests are post-authorization; residual risk remains explicit. |
| Commercial bundle execution and durable receipt | NC-08 | B-04 | AC-14, AC-15 | WP-01 per-member durable receipt, mapping, idempotency, daemon reconciliation and recovery. No DDL or assumed 2PC. |
| Commercial identifier / idempotency derivation | NC-16 | B-04 receipt mapping; formula specified in §16.13 | AC-27 | WP-01. member_execution_key and operation key are correlation/idempotency keys, not replacements for acquisition_id; durable mapping remains B-04. |
| Zero-DDL schema compliance | NC-10 | Static DDL source evidence; live DB remains NOT VERIFIED | AC-17 | Existing schema compliance test boundary only. Do not claim live database state from static DDL evidence. |
| Registry online/offline fallback | NC-11 | Existing Registry contract; online/offline verifier integration as separately scoped | AC-18, AC-19 | Online authoritative verification; offline fallback only on transport failure; HTTP 5xx/bad signature fail closed. |
| JIT and viewer lifecycle | NC-13 | B-09 only for membership/JIT integration; viewer completion source belongs WP-06 | AC-22, AC-23, AC-24, AC-32 | Stage 8a/8b/8c §16.1; viewer lifecycle §16.11; WP-06 normalized event, deduplication, resource release and fresh next-member JIT. |
| Verify behavior | NC-14 | B-09 | AC-25, AC-33, AC-34 | CONF-02 Option B: no aggregate Album status. AC-25 spec-ready; AC-33/34 membership authentication and per-member processing remain blocked on B-09. Verify result is not playback authorization. |
| Error taxonomy and stable reason-code registry | NC-15 | AA/PO contract decision CLOSED; no new B identifier | AC-26, AC-10 Genesis signature case, and other mapped error-producing ACs | §6.15 and §16.21.6 specify 20 active emitted reason codes (including PO-approved `ERR_GENESIS_SIGNATURE_INVALID`); replay label deprecated. Implementation and tests remain post-authorization. |

**Reverse-coverage check:** AC-01..AC-34 all appear at least once in the matrix above. Shared mappings are intentional: AC-02 spans NC-01 manifest/archive binding and NC-07 ZIP structural validation; AC-28/31 span NC-01 and NC-06; AC-16 is NC-09 (not NC-06); AC-27 is NC-16 with B-04 receipt dependency; AC-22 is NC-13 with B-09 only for membership/JIT integration. NC-01..NC-16 each have an explicit row.
##### 16.20.2 Active status reconciliation

1. **Acceptance Criteria:** 34 total; 12 specification-ready (AC-04, AC-09, AC-11, AC-12, AC-17, AC-18, AC-19, AC-23, AC-24, AC-25, AC-30, AC-31); 22 execution-blocked (AC-01, AC-02, AC-03, AC-05, AC-06, AC-07, AC-08, AC-10, AC-13, AC-14, AC-15, AC-16, AC-20, AC-21, AC-22, AC-26, AC-27, AC-28, AC-29, AC-32, AC-33, AC-34); 0 PO decision required.
2. **Register completeness:** NC-01..NC-16 are each represented in §16.20.1; B-01..B-09 are mapped to their owning NC and AC dependencies there. AC-01..AC-34 are all covered in the reverse-coverage check. Shared AC mappings are deliberate and do not change the single primary contract/dependency recorded in §8.
3. **PO decision status:** CONF-01 membership authenticity/per-Album authority policy, CONF-02 Verify no-aggregate Option B, and Model B/CONF-03 commercial model are decided. B-04 feasibility is technical/storage compatibility, not an unresolved choice of commercial model.
4. **NC-01:** exact top-level Manifest fields and initial version primitive are specified; ZIP entry is fixed as root `manifest.json`. Native nested proof object compatibility/schema remains bounded by §16.21.4, §16.16.4B, and the A1 NOT VERIFIED ledger.
5. **NC-02/B-08:** exact outer signed-content field set and Signature-Stripped JCS contract are specified in §16.4. Historical §6.2/audit snapshots that say exact signed-content remains undecided are superseded. Implementation and cross-language tests remain post-authorization.
6. **NC-04/B-09:** PO authority policy and AA semantic carrier/offline closure contracts are specified. Album-specific implementation is absent at this planning stage. Individual Creator lifecycle and native proof serialization/verifier compatibility are not upgraded beyond A1 evidence. No PO issuer-authority decision remains open.
7. **NC-06 versus NC-08:** NC-06 is Album identity/member ordering/Studio persistence/reload; NC-08 is Marketplace commercial checkout/member receipt/idempotency/reconciliation. Their identifiers and receipts are not interchangeable. WP-05 owns Album persistence; WP-01 owns commercial execution receipts.
8. **NC-07/B-07:** security design and benchmark method are specified; numeric capacity limits are not ratified. Benchmark output is a future acceptance deliverable and does not mean Album implementation already exists.
9. **NC-13/AC-32:** Stage 8a/8b/8c authorization boundaries are specified; viewer completion integration remains WP-06. No timer or UI-visibility heuristic is permitted.
10. **NC-14:** CONF-02 Option B is active. Verify must not create an aggregate Album trust status. Membership authentication is a prerequisite for labeling files as Album members, not a global playback gate.
11. **NC-15:** deterministic reason-code semantics and the 20-code active registry are specified by §6.15/§16.21.6; the Genesis code is PO-approved and replay label deprecated. Source implementation is not claimed. The contract residual is closed; implementation/tests remain post-authorization.
12. **NC-16:** JCS formulas are specified in §16.13; durable receipt mapping is a B-04 dependency. Do not imply the formula creates a database constraint or replaces an existing acquisition identifier.
##### 16.20.3 Gate disposition after reconciliation

- **Gate A:** NC-15's deterministic taxonomy and Genesis reason-code contract residuals are CLOSED by PO approval and active-register reconciliation (§6.15, §16.20.1–§16.20.2, §16.21.6). Gate A is READY FOR AA RE-EVALUATION after a final active-section consistency pass; this is not itself a PASS. Native-proof source compatibility remains bounded by A1 and is separately a Gate B prerequisite. Manifest ZIP entry/version decision is closed by §16.21.1.
- **Gate B remains BLOCKED** only on the two indispensable pre-coding predicates in §16.21.7: Zero-DDL durable storage feasibility (B-04/B-05/NC-06) and native proof/signature/trust-anchor compatibility (B-09). Album-specific implementation, benchmark measurements, parser/extractor code, viewer adapters, and post-authorization tests are not pre-coding blockers.
- **No Programmer re-investigation is authorized or requested.** A1 evidence limitations remain explicitly NOT VERIFIED. AA must not invent missing native source formats. If an indispensable compatibility predicate cannot be resolved from submitted evidence and authoritative documents, Gate B stays blocked pending AA/PO-level resolution; this does not reopen the completed Programmer correction handoff.
- Sequence remains Gate A PASS → Gate B PASS → separate explicit PO implementation authorization. Sprint 16 and PE-01 remain CLOSED/FROZEN; Sprint 17 remains NOT STARTED.


## 16.21 AA residual architecture closure — active decisions and bounded non-closures

This section is the active AA disposition of the remaining planning residuals identified in §16.19.4 and §16.20. It distinguishes decisions AA can make from source-compatibility facts that cannot be inferred or fabricated. It does not authorize source, DDL, configuration, or runtime changes.

### 16.21.1 NC-01 — canonical ZIP Manifest entry and initial schema version

AA closes the previously unspecified ZIP Manifest entry placement and initial schema-version primitive:

1. The ZIP wrapper MUST contain exactly one Manifest regular-file entry at the archive root named exactly `manifest.json` (ASCII lowercase). No alternate filename, nested location, extension, sidecar, detached Manifest, or discovery-by-content fallback is permitted.
2. The Manifest entry is excluded from the declared child `.nx` member set. Directory entries remain permitted under the PO decision; they are structural only and are not members. The set of regular child `.nx` entries MUST be bijective with `members[]`. Any other undeclared regular file fails with `ERR_ZIP_ENTRY_MISMATCH`; a case-fold collision involving the reserved `manifest.json` entry fails at ZIP-reader layer with `ERR_ZIP_INVALID`.
3. The initial canonical Manifest schema version is integer `1` (`schema_version: 1`). Missing, non-integer, zero, negative, or unsupported values fail with `ERR_MANIFEST_MALFORMED`. No permissive parsing or automatic migration is allowed. A future schema requires a separately specified and explicitly supported version.
4. Manifest bytes MUST be valid UTF-8 JSON without a byte-order mark. Duplicate keys are rejected by B-01 before schema evaluation. Canonical signing bytes remain RFC 8785 UTF-8 after strict parsing and removal of only the top-level `signature` property under §16.4.
5. This decision fixes ZIP entry name/location and the version primitive; it does NOT claim every nested native evidence object schema is independently machine-validatable today. The closed logical field sets in §16.2 and §16.16.4A/§16.16.4B remain controlling. Native Genesis/Identity/rights/federation/revocation/delegation serialization and signature semantics remain bounded by the A1 compatibility ledger. A category marked NOT VERIFIED cannot be replaced by an invented JSON shape.

**Disposition:** NC-01 entry placement and initial version primitive are AA-DECIDED. The remaining residual is exact native evidence object compatibility/schema validation where A1 did not establish the existing representation. AC-01/AC-02 remain execution-blocked until indispensable nested-schema predicates are resolved and the parser/validator is implemented after authorization.

### 16.21.2 B-04 / B-05 / NC-06 / NC-09 — Zero-DDL storage feasibility boundary

1. The architecture contract is closed: WP-01/WP-02/WP-05 MUST use an existing durable storage capability and MUST NOT add DDL, migration, new table/column, or repurpose `acquired_package_sha256`. The immutable Checkout Manifest, per-member execution/settlement evidence, Album identity/ordered member association, and child `member_sha256` are distinct logical records/values with explicit identity mapping.
2. `acquired_package_sha256` retains its evidenced/reported wrapper-package byte-domain. It MUST NOT be treated as child `.nx` hash. Child `member_sha256` is SHA-256 of exact final child `.nx` bytes. No inference from field names, row order, timestamps, filenames, or catalog order is permitted.
3. A storage mechanism is acceptable only if implementation demonstrates durable write/read after restart, deterministic lookup, create-if-absent or equivalent immutability, concurrency-safe conditional mutation, integrity/authenticity, retention, backup/recovery, and reconciliation access. Volatile cache, temporary file, last-write-wins object overwrite, or an unverified Storage Engine candidate is not an authoritative receipt.
4. AA cannot certify source-specific feasibility without verifiable source/DDL evidence. Existing A1/PSV reports are accepted as bounded Programmer submissions but do not establish the missing Zero-DDL store predicates to independent source-audit certainty. No repeat PSV or broad Programmer investigation is requested here.
5. If already-submitted evidence does not establish a compatible existing store, the work package remains BLOCKED at that exact storage-feasibility predicate. No fallback DDL, semantic reuse of wrapper hash, or volatile persistence workaround is authorized. If the only feasible solution violates Zero-DDL, that incompatibility must return to PO; AA cannot waive it.

**Disposition:** B-04/B-05/NC-06/NC-09 architecture semantics are DECIDED; source-backed Zero-DDL feasibility is NOT VERIFIED / BLOCKED. This is a genuine Gate B prerequisite because safe implementation cannot be bounded without knowing whether mandatory persistence invariants are achievable under the frozen Zero-DDL constraint.

### 16.21.3 B-07 / NC-07 — benchmark and capacity boundary

1. No proposed numeric value (500 MB, 4 GB, 200 entries, 10:1, 100:1, or earlier candidate) is normative. The 50-member value remains UX guidance only.
2. The benchmark protocol in §16.7/§16.14 is complete as a method. Numeric caps are deployment-envelope decisions based on reproducible measurements, not a precondition that Album code already exists.
3. Before a measured deployment profile is ratified, the extractor MUST require an explicit bounded deployment configuration for every enforced resource dimension and fail closed when a required bound is absent. It MUST stream and enforce counters during extraction; declared ZIP sizes alone are insufficient.
4. Four-payload benchmark and adversarial measurements are WP-03 acceptance deliverables after implementation authorization (or may be performed earlier only as non-mutating measurement with an explicitly available representative environment). Their absence does not by itself block Gate B.

**Disposition:** B-07 method DECIDED; measured numeric capacity profile remains POST-AUTHORIZATION ACCEPTANCE / NOT YET MEASURED. No numeric cap is invented.

### 16.21.4 B-09 / NC-04 — native proof compatibility boundary

1. The PO-approved Tier-1/Tier-2/Tier-3 authority model, field binding, embedded-evidence requirement, signature-layer separation, offline trust-anchor termination, and Dual-Horizon freshness semantics are fixed by §16.5 and §16.16.4A/§16.16.4B.
2. The A1 compatibility ledger remains authoritative for evidence state. The six categories are not promoted from PARTIAL/NOT FOUND/NOT VERIFIED to PRESENT merely because the target logical carrier is specified.
3. No generic JCS wrapper may replace native Genesis, Identity, Ownership, Registry, revocation, or delegation signature preimages. Inner evidence must be serialized and verified under its own existing native contract, then embedded in the PE-02 carrier; outer carrier and Manifest signatures do not cure an invalid native proof.
4. Where an indispensable native proof representation, issuer/key lineage, trust-anchor termination, or verifier semantics remain NOT VERIFIED, Gate B remains BLOCKED. No additional Programmer investigation is requested; no missing representation is to be guessed. Resolution is limited to the exact compatibility predicate and must not create a new trust root or weaken offline verification.

**Disposition:** Product and semantic architecture DECIDED; native compatibility closure remains NOT VERIFIED / BLOCKED at the indispensable predicates listed in §16.16.4B. B-09 implementation itself remains a post-authorization workstream and is not a blocker merely because Album-specific code does not yet exist.

### 16.21.5 NC-13 / AC-32 — viewer lifecycle boundary

The normalized `VIEWER_COMPLETED` semantics, per-viewer identity, deduplication, authorization/resource release, and fresh next-member JIT are specified in §16.11. Platform/payload event adapters and parity tests are implementation acceptance under WP-06. Missing future adapter code is not a pre-coding architecture blocker. A platform/payload pair that cannot provide a definitive completion event remains NOT READY; no timer, duration, visibility heuristic, or manual-next substitution is permitted.

**Disposition:** AA architecture contract DECIDED; WP-06 source adapters and tests are POST-AUTHORIZATION implementation acceptance. AC-32 remains execution-blocked until implemented and tested, but its absence does not independently block Gate B.

### 16.21.6 NC-15 / AC-10 / AC-26 — deterministic error semantics and bounded Genesis residual

AA closes the deterministic semantics of the existing error proposals wherever this can be done without changing PE-01 or inventing native proof behavior. The table in §6.15 remains a proposal register until the single Genesis code-contract decision below is made. The following dispositions govern future implementation; they do not claim that any Album error producer already exists in source.

| Existing proposal | Deterministic trigger / producer boundary | Machine disposition and retry rule | Affected object and product impact | AC / evidence boundary |
|---|---|---|---|---|
| `ERR_MANIFEST_MISSING` | ZIP/package validator has completed archive enumeration and the one required root `manifest.json` entry is absent. | Reject package; no automatic retry. Corrected/repacked input may be resubmitted. | Package membership declaration unavailable; do not infer Album membership or invalidate independently supplied standalone members. | AC-01/02; root entry contract §16.21.1. |
| `ERR_MANIFEST_MALFORMED` | Strict Manifest parser detects invalid UTF-8/JSON, BOM, invalid top-level/schema types, unsupported schema_version, or a malformed field/value after duplicate-key handling. | Reject Manifest; no parser fallback or auto-migration. Retry only with corrected input. | Manifest/package membership rejected; standalone verification of independently supplied members remains separate. | AC-01; strict parser is post-authorization implementation. |
| `ERR_MANIFEST_DUPLICATE_KEY` | Strict JSON parser detects duplicate object keys, including duplicates that become equal after JSON escape decoding. | Stop parsing and reject; non-retryable for the same bytes. | Manifest rejected; no last-key-wins interpretation. | AC-05 / B-01. |
| `ERR_MANIFEST_SIGNATURE_INVALID` | Tier-3 verifier has the required signer key and trust context, but Ed25519 verification of the outer Signature-Stripped JCS Manifest payload fails. | Reject Manifest membership declaration; do not fall back to unsigned interpretation. Non-retryable unless the signed bytes/signature are corrected. | Album membership declaration is unauthenticated; this does not by itself mark child .nx standalone PE-01 signatures invalid. | AC-03 / B-08. |
| `ERR_ALBUM_SIGNER_UNKNOWN` | Membership trust resolver cannot establish the Album Signer identity/key/trust state from the available evidence and applicable local trust configuration; this is UNKNOWN, not a positive untrusted/revoked determination. | Fail closed for membership authentication. Retry only after relevant trust/evidence becomes available or is refreshed; do not convert UNKNOWN to INVALID. | Manifest cannot authenticate membership; no global playback block and no standalone member INVALID result. | AC-07; B-09/A1 signer and trust path remain compatibility-gated. |
| `ERR_ALBUM_SIGNER_UNTRUSTED` | Trust evaluation positively establishes that the Album Signer is untrusted/revoked under an authoritative applicable status. Mere absence/unavailability is insufficient. | Reject membership authentication; retry only after an authoritative status change and fresh evaluation. | Membership declaration rejected; do not automatically mark child member standalone trust INVALID or prohibit independent standalone verification. | AC-08; revocation/federation native proof remains A1-bounded. |
| `ERR_CONTAINER_SIGNATURE_INVALID` | Existing PE-01 container verifier positively fails the individual .nx container signature. Producer remains the PE-01 verifier. | Preserve the exact frozen PE-01 fail-closed behavior; no Album-specific remapping or changed observable result is authorized. | The individual .nx member fails its PE-01 integrity/authenticity check; playback of that member is denied. | AC-04; frozen PE-01 source/runtime contract is not modified by this plan. |
| `ERR_CONTAINER_HASH_MISMATCH` | Stage 8a compares SHA-256 of the exact encrypted audio payload byte sequence with the canonical Manifest audio digest for a MUSIC_AUDIO member and the values differ. | Fail closed for that payload; no fallback to wrapper or complete-.nx hash. Retry only with a corrected, consistently signed package. | Affected member payload integrity fails; no playback/decryption authorization. | AC-09; §16.12 byte-domain. |
| `ERR_ZIP_INVALID` | ZIP reader rejects corrupt/truncated ZIP structure, invalid central directory, unsupported/special entry type, traversal, or reserved-name case-fold collision. | Abort package read/extraction; no fallback parser. Retry only with a corrected archive. | Package rejected before membership is trusted; standalone member checks remain independent. | AC-02/13; ZIP-reader producer is a PE-02 implementation target, not proven by the existing .nx container error. |
| `ERR_ZIP_QUOTA_EXCEEDED` | Streaming extractor crosses any explicitly configured and ratified hard resource cap. Each enforced dimension must have a configured value; missing required configuration fails closed and must not be silently treated as unlimited. | Abort and clean staged extraction. Retry may occur only with a package within the configured envelope or after an authorized deployment-envelope change. | Package extraction rejected; does not mean the child .nx itself is malformed. | AC-13 / B-07; numeric caps remain unratified and post-authorization benchmark-derived. |
| `ERR_ZIP_BOMB_DETECTED` | ZIP reader/extractor detects a defined structural bomb predicate, including nonzero expanded size with zero compressed size, or a ratio predicate only after its threshold is explicitly ratified. | Abort extraction and clean staging. No quarantine action is implied unless a separate security handling contract defines it. | Package rejected as unsafe to extract. | AC-13 / B-07; unratified ratio threshold cannot be used as an active trigger. |
| `ERR_ZIP_ENTRY_MISMATCH` | Packaging validator finds that regular child .nx entries are not in bijection with Manifest members, or finds an undeclared regular file. Root `manifest.json` is excluded; structural directory entries are not members. | Reject package; no auto-discovery or repair. | Album membership/package structure rejected; standalone member verification remains independent. | AC-02/13; §16.21.1. |
| `ERR_FILESYSTEM_CONTAINMENT_VIOLATION` | Safe-Open detects traversal, prohibited symlink/special file, descriptor/path identity mismatch, or another defined containment violation. | Close acquired descriptors, abort access, clean staging, and fail closed. No automatic retry against the same path/object. | Access to the affected extracted member is denied; do not claim all POSIX ancestor-rename races are eliminated absent platform-specific proof. | AC-20/21 / B-06; implementation and adversarial acceptance remain post-authorization. |
| `ERR_PLAYBACK_UNAUTHORIZED` | JIT authorizer positively determines that the current member has no valid active playback entitlement/license after the authoritative license evaluation completes. | Deny playback. Retry only after entitlement/license state changes and a fresh JIT evaluation. PENDING/UNKNOWN is not this terminal result. | Current member playback denied; does not invalidate Album membership or standalone cryptographic verification. | AC-22; Stage 8b requires all §16.1 predicates. |
| `ERR_MARKETPLACE_REPLAY_DETECTED` | The same idempotency/correlation identity and same immutable request tuple is presented again. This is a replay/retry, not a business failure. | **Do not emit this value as an error.** Return/reconcile the original operation's authoritative state and receipt idempotently. If the same key is presented with a different immutable tuple, handle as an identifier/correlation conflict, not as a successful replay. | Existing checkout/member operation is returned; no duplicate acquisition, charge, fulfillment, or receipt is created. | AC-15 / B-04 / CONF-03. Existing table entry is retained as a deprecated proposal label only, not a terminal error code. |
| `ERR_ID_COLLISION` | Identity/receipt layer finds the same derived logical key associated with a different immutable source tuple. Same key + same tuple is an idempotent match, not a collision. | Fail closed, preserve the existing record, do not overwrite, and raise an integrity/operator diagnostic. No retry with the same conflicting tuple/key. This does not assert SHA-256 is collision-free or that a DB uniqueness constraint exists. | Conflicting logical identity/receipt mapping is rejected; no acquisition or member mapping is silently reassigned. | AC-27 / NC-16 / B-04; durable mapping feasibility remains separate. |
| `ERR_TRANSACTION_FAILED` | Local database transaction definitively fails before local commit. | Roll back the local transaction. Retry only through the idempotent operation/reconciliation path. This does not claim rollback/compensation of an already committed external License Daemon effect. | Local checkout/member receipt mutation is not committed; external outcome may still require reconciliation. | AC-14 / B-04 / CONF-03. |
| `ERR_REGISTRY_UNREACHABLE` | Registry transport cannot be reached and no acceptable cached proof/status is available under the existing online/offline fallback contract. | Return unavailable/fail-closed for the requested trust decision; retryable after transport recovery. Do not label the asset INVALID solely because transport is unavailable. | Requested Registry trust result is UNKNOWN/UNAVAILABLE; membership or verification cannot be promoted to trusted. | AC-18/19; NC-11. |
| `ERR_REGISTRY_SIGNATURE_INVALID` | Registry response/attestation is received but its applicable native signature or binding validation positively fails. | Reject the response; non-retryable for identical signed bytes. Do not downgrade to offline trust merely because the online signature is bad. | Registry assertion is untrusted; affected trust decision fails closed. | AC-18/19; native Registry proof compatibility remains A1-bounded. |
| `ERR_LICENSE_DAEMON_COMMUNICATION` | License Daemon call has a definitive transport/protocol failure whose outcome is known not to have committed, after status/reconciliation rules have been applied. | Use only for confirmed communication failure. If request outcome may have committed or cannot be determined, return/retain PENDING or UNKNOWN and reconcile by the existing operation identity; do not report terminal failure, duplicate the request, or assume external rollback. | Checkout/member execution remains pending reconciliation where outcome is ambiguous; local transaction and external daemon effects remain distinct. | AC-14 / B-04 / CONF-03. |

**Cross-cutting rules:**

1. A reason code is emitted only by its named producer layer and only for its exact trigger. A caller must not relabel a downstream failure as its own layer's error.
2. UNKNOWN, UNAVAILABLE, PENDING, and CONFIRMED INVALID/FAILED are distinct machine outcomes. Network absence, missing evidence, or an unresolved external operation is not proof of invalidity or terminal failure.
3. Every emitted error response must carry the affected object identity, originating stage/layer, retryability, safe user/operator disposition, evidence/provenance reference, and the relevant AC mapping. Localized UI prose is not the machine contract.
4. Membership authentication, standalone PE-01 verification, and playback authorization are separate impact domains. An Album membership error must not silently invalidate a standalone member; a standalone PE-01 failure must retain its frozen behavior; a license error must not rewrite cryptographic trust.
5. `ERR_MARKETPLACE_REPLAY_DETECTED` is removed from the set of emitted error outcomes and retained only as a deprecated historical label for idempotent replay. This does not create a replacement error code.

**PO decision — APPROVED.** PO explicitly approved `ERR_GENESIS_SIGNATURE_INVALID` for the Genesis Certificate verification boundary only (E-01). It MUST NOT be mapped to `ERR_CONTAINER_SIGNATURE_INVALID`, `ERR_MANIFEST_SIGNATURE_INVALID`, or `ERR_REGISTRY_SIGNATURE_INVALID`. This is a normative reason-code decision; it does not assert that the code already exists in source.

**PE-01 isolation — immutable.** PE-01 remains CLOSED / FROZEN. Its observable failure behavior remains exactly fail-closed: `canPlay: false`, `is_valid: false`, `status: INVALID`. The new Genesis reason code does not authorize changes to PE-01 callers, SDK behavior, or ecosystem interfaces. The code is exposed only at the Genesis Certificate verification boundary defined by E-01. Any implementation must preserve this boundary and behavior.

**Disposition:** NC-15 semantic taxonomy residual is CLOSED at plan/contract level; AC-10 Genesis taxonomy residual is CLOSED at plan/contract level; AC-26 taxonomy specification residual is CLOSED at plan/contract level. §6.15 records 20 active emitted reason codes (19 retained from the original proposal plus the approved Genesis code); `ERR_MARKETPLACE_REPLAY_DETECTED` remains a deprecated historical label and MUST NOT be emitted as an error. These closures do not claim source implementation, runtime test completion, or Gate A PASS.
 
### 16.21.7 Active gate consequence

- **Gate A:** the NC-15/AC-26 and Genesis portion of AC-10 contract decision residual is CLOSED by PO approval recorded in §16.21.6 and reflected in §6.15. Gate A is READY FOR AA RE-EVALUATION after active-section consistency verification; this closure alone is not a Gate A PASS. Manifest ZIP entry/version decision is closed by §16.21.1.
- **Gate B:** remains BLOCKED on two indispensable pre-coding predicates: (a) B-04/B-05/NC-06 Zero-DDL durable storage feasibility; and (b) B-09 native proof compatibility, specifically serialized native proof representations, native signature/preimage verification, key/issuer lineage, and independent local trust-anchor termination. A1 is sufficient to define the evidence-closure architecture, but is NOT sufficient to prove these existing native compatibility predicates. Album-specific implementation, B-07 measured caps, parser/extractor code, viewer adapters, and post-authorization tests are not pre-coding blockers.
- **A1 compatibility assessment:** six categories remain bounded by the submitted evidence: Genesis credential/trust-anchor termination (PARTIAL); Organization/Individual key-lineage serialization and timestamp-correct resolution (PARTIAL / NOT VERIFIED elements); Album-wide rights-basis object and verifier (PARTIAL / NOT FOUND in examined scope); Registry/Federated Trust proof and offline anchor path (PARTIAL; no pinned verifier trust anchor demonstrated); signed revocation/status snapshot and Dual-Horizon offline evaluation (PARTIAL / NOT FOUND); Tier-2 membership capability/delegation native object and verifier (NOT FOUND in examined scope). These findings do not establish universal absence from the repository; they establish that the A1 submission does not prove the complete native representation/verifier path required by §16.16.4B.
- **Programmer:** no new investigation, repeated PSV, broad search, or test-suite rerun is requested. No unsupported native format or verifier behavior may be inferred.
- **Authorization:** PE-02 implementation remains NOT AUTHORIZED. Gate A PASS and Gate B PASS, followed by separate explicit PO authorization, are all still required.

#### 16.19.6 Governance status — unchanged

- Current phase: **PLANNING PE-02 Album Handling**.
- Album Handling: **NOT YET IMPLEMENTED — TARGET CAPABILITY TO BE BUILT**.
- Sprint 16: **CLOSED / FINAL ACCEPTED / FROZEN**.
- PE-01: **CLOSED / FROZEN**.
- Sprint 17: **NOT STARTED**.
- Gate A: **NOT PASSED** pending AA-owned plan consistency/independent re-audit.
- Gate B: **BLOCKED** pending concrete pre-authorization readiness closure; not because Album implementation is absent.
- PE-02 implementation: **NOT AUTHORIZED**.
- No source code, schema, migration, endpoint, configuration, or runtime change is authorized by this Architecture Baseline.

**AA disposition:** Architecture Baseline established as the planning classification and consolidation layer. The next AA task is the canonical PLAN cross-section/traceability reconciliation, followed by gate evaluation. Programmer's A1 documentation correction handoff is not reopened by this section.

