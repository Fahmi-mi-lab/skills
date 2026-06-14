# zed-skills

Kumpulan skill untuk [Zed Editor](https://zed.dev) — siap pakai untuk workflow coding sehari-hari.

## Skills

### Planning

| Skill | Deskripsi |
|-------|-----------|
| [`prd`](./prd/SKILL.md) | Generate PRD lengkap — architecture, tech stack, user flow, data model, dan API design |
| [`gen-context`](./gen-context/SKILL.md) | Generate context files boilerplate dari PRD yang sudah selesai, adaptif berdasarkan tipe project |

### Coding

| Skill | Deskripsi |
|-------|-----------|
| [`review-code`](./review-code/SKILL.md) | Review kode untuk bug, security, performance, dan best practices |
| [`gen-test`](./gen-test/SKILL.md) | Generate unit/integration test dari fungsi atau modul yang dipilih |
| [`gen-docs`](./gen-docs/SKILL.md) | Generate JSDoc, docstring, atau Rustdoc untuk kode yang dipilih |
| [`explain-code`](./explain-code/SKILL.md) | Jelaskan kode yang kompleks dalam bahasa yang mudah dipahami |
| [`fix-code`](./fix-code/SKILL.md) | Diagnosa dan perbaiki bug atau error pada kode |
| [`gen-commit`](./gen-commit/SKILL.md) | Generate conventional commit message dari perubahan kode |

## Cara Install

### Import via URL (recommended)

1. Di Zed, buka **Skill Creator** (`Cmd/Ctrl + Shift + P` → "New Skill")
2. Copy raw URL dari file SKILL.md yang diinginkan, contoh:
   ```
   https://raw.githubusercontent.com/Fahmi-mi-lab/zed-skills/refs/heads/main/review-code/SKILL.md
   ```
3. Paste ke field **"Import from URL"**
4. Zed otomatis mengisi form — klik Save

### Manual

Copy isi file `SKILL.md` langsung ke field **Skill Content** di Skill Creator.

## Workflow yang Disarankan

```
Ide / requirement
      ↓
    prd             ← buat perencanaan lengkap
      ↓
 gen-context        ← generate context files di folder context/
      ↓
  Mulai coding      ← gunakan context/ sebagai referensi AI
      ↓
 review-code        ← cek sebelum lanjut
      ↓
  gen-test          ← tambah test coverage
      ↓
  gen-docs          ← dokumentasi fungsi baru
      ↓
 gen-commit         ← commit message yang rapi
```

## Bahasa yang Didukung

Semua skill mendeteksi bahasa secara otomatis dari kode yang dipilih:

- JavaScript / TypeScript
- Python
- Rust
- Go
- PHP dan bahasa lainnya
