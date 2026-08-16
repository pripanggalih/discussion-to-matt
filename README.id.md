# discussion-to-matt

[![license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![skills](https://img.shields.io/badge/skills-1-informational)](#yang-ditulisnya)

> **[English →](README.md)**

Satu skill: lapisan yang diasumsikan [mattpocock/skills](https://github.com/mattpocock/skills) tapi tidak pernah dibuatnya.

Skill engineering Matt sangat baik per fitur. `/to-spec` mengubah percakapan jadi spec, `/to-tickets` memotongnya jadi tracer bullet, `/implement` membangunnya, `/code-review` memeriksanya. Semuanya dimulai di udara: stack dianggap sudah dipilih, entity dianggap sudah punya nama, seam dianggap sudah ada, dan "selesai" dianggap sudah berarti sesuatu yang spesifik di repo ini. Tidak ada satu pun di set itu yang menetapkannya.

`discussion-to-matt` menetapkannya sekali, lalu menyerahkan tiap fitur ke pipeline dalam keadaan sudah berpijak.

## Yang ditulisnya

```
PRODUCT.md                              masalah, cakupan v1, non-goal, ukuran keberhasilan  (root, berbagi dengan impeccable)
docs/foundation/
├── ARCHITECTURE.md                     stack + versi, struktur, NFR, scaffold-atau-extend
├── CONVENTIONS.md                      reuse inventory, layout, testing, definition of done
├── DATA-MODEL.md                       entity dan relasinya                (hanya kalau ada data)
├── SEAMS.md                            registri seam                       (hanya setelah ada seam)
├── ROADMAP.md                          fitur terurut — satu-satunya tempat progress dan depth hidup
└── run-sheets/NN-<slug>.md             satu per baris roadmap, siap paste
```

Glosarium dan ADR **tidak** ditulis di sini — `/domain-modeling` yang menulisnya inline saat interogasi berlangsung, dan salinan akan menyimpang begitu satu sisi diperbarui sendirian. `DESIGN.md` milik [impeccable](https://github.com/pbakaus/impeccable).

## Alurnya

```
ide bebas  (atau repo warisan)
  → /discussion-to-matt      interogasi, tulis foundation, urutkan roadmap,
                             tulis satu run sheet per baris
  → per baris roadmap, dari atas ke bawah, satu sesi baru tiap baris:
      paste briefing block ke /grill-with-docs
      /impeccable shape      (khusus UI)
      /to-spec  →  /to-tickets  →  /implement
      /impeccable critique · audit · polish   (khusus UI)
  → baris berikutnya
```

## Bedanya dengan menulis dokumen sendiri

**Interogasinya punya lantai.** Ia berhenti saat tiap tema punya jawaban yang bisa dikutip ulang **dan** tiap section dari tiap format yang berlaku bisa diisi tanpa menebak — bukan saat pertanyaannya habis. Kehabisan pertanyaan tidak sama dengan punya jawaban.

**Detail ditulis belakangan, dengan sengaja.** Tiap run sheet lahir sebagai brief. Hanya baris yang akan dibangun yang dipromosikan jadi detailed, terhadap kode yang sudah ada saat itu. Run sheet yang ditulis hari ini untuk baris 07 menggambarkan kode yang baru ada enam sesi lagi, dan `/to-spec` akan membacanya sebagai fakta.

**Promosi itu kerja agent, bukan kerjamu.** Ia menyala saat kau paste briefing block ke sesi berikutnya — tidak ada dokumen untuk dirawat, tidak ada checkbox untuk dicentang manual. Kau menjawab pertanyaan di chat; agent yang menulis semua file.

**Satu fakta, satu rumah.** Tiap file punya charter, dan self-review-nya mengecek placeholder dengan `grep` sungguhan, melacak tiap kapabilitas sampai ke anchor run sheet yang benar-benar ada, lalu ditutup dengan membaca ulang run sheet 01 sebagai agent yang tidak menyaksikan percakapannya.

## Pasang

Dengan CLI [vercel-labs `skills`](https://www.skills.sh):

```bash
npx skills add pripanggalih/discussion-to-matt
```

Skill ini adalah foundation *untuk* set milik Matt — pasang itu juga, dan jalankan setup-nya sekali per repo:

```bash
npx skills add mattpocock/skills
/setup-matt-pocock-skills
```

Untuk proyek yang punya antarmuka, tambah [impeccable](https://github.com/pbakaus/impeccable):

```bash
npx impeccable install
```

Kalau setup belum dijalankan, `/discussion-to-matt` menjalankannya untukmu, bukan berhenti.

## Pakai

```
/discussion-to-matt
```

Jalankan di **awal** pembangunan, ia memegang seluruh percakapan desainnya. Jalankan di **akhir** sebuah percakapan, ia membuka dari apa yang sudah diputuskan di situ, mengonfirmasinya tema per tema, lalu menginterogasi celahnya saja. Jalankan lagi nanti, ia melanjutkan: checkbox yang sudah ada tetap, file yang menyimpang ditambal, roadmap diperpanjang dan tidak pernah ditulis ulang.

Greenfield, brownfield, atau lanjutan — ia menentukan modenya sendiri dan menyebutkannya sebelum bertanya apa pun.

## Yang tidak dilakukannya

- Tidak menulis kode, spec, ticket, atau plan. Semua itu punya pemilik di hilir, dan versi kedua yang ditulis di sini adalah versi yang akan mereka bantah.
- Tidak menulis acceptance criteria dan contract di run sheet, dengan alasan yang sama.
- Tidak ada session hook. Tiap command di run sheet adalah command yang kau ketik.

## Lisensi & atribusi

MIT ([`LICENSE`](LICENSE)). Skill ini berdiri di atas kerja yang bukan miliknya — atribusi jujurnya di [`NOTICE.md`](NOTICE.md).
