# Shaunak Blackburn

Data operations engineer and full-stack product builder. I turn messy, rule-heavy operational work into pipelines and web apps that other people can actually run.

Most of my day job is automotive consumer research: survey data operations, VIN enrichment, open-end coding, and QA pipelines that have to be right the first time. On my own time I ship production web apps — Next.js, TypeScript, Supabase, Postgres.

- **Location:** San Diego, CA (open to remote)
- **Currently:** Data & automation work at an automotive consumer-research firm
- **Open to:** Data engineering, analytics engineering, research/survey data operations, full-stack product roles

---

## What I build

### Automotive data enrichment pipeline
A production Python pipeline that takes raw multi-source vehicle buyer files and turns them into validated, coded, mailable deliverables.

- NHTSA VIN decoding with explicit reject-code handling (error codes route to rejection instead of quietly passing)
- Cell-code and 21-digit UCC assignment from a 15,000+ pattern master lookup table
- Column normalization across several different data providers with conflicting schemas
- Deduplication against historical send files, geography filtering, and panelization
- A `needs-review` report as a deliberate handoff surface: ambiguous vehicle patterns are held for research rather than force-coded into the nearest available code

Reached 99.87%+ coding accuracy across a production batch set. Separated batch processing, deduplication, and final formatting into independent stages so a formatting failure never looks like a pipeline failure.

**Python · pandas · NHTSA vPIC API · Tkinter GUIs · YAML-driven config**

### SPSS derived-field reconstruction
Rebuilt a recurring SPSS augmentation step so it can run without an SPSS license: read `.sav` files with `pyreadstat`, recover the real mapping rules by cross-tabbing source against published output across two survey waves, and encode confirmed transformations in a declarative YAML spec that round-trips while preserving column order, value labels, and SPSS metadata.

The interesting part was refusing to guess. Arithmetic brand inference matched only 2.3% of codes, so the mappings were recovered from observed data instead. Sentinel values (995–999) are preserved as valid non-vehicle states, because nulling them would corrupt analysis bases.

**Python · pyreadstat · pandas · YAML specs**

### AutoApp — vehicle ownership assistant
A Next.js 16 + Supabase web app for vehicle owners: a garage with VIN-decoded vehicles, service records with multi-file attachments, fuel logs, photo galleries, maintenance reminders, NHTSA recall lookup, and a document glovebox.

- AI receipt OCR that parses images and multi-page PDFs into service-record fields, with server-side PDF rasterization
- Token-gated public share links that expose a redacted ownership history for resale, with revoke and expiry
- Tiered access with Stripe scaffolding and scan limits
- Delete safety scaled to how hard a record is to reconstruct: 30-day trash plus undo for vehicles and service history, hard delete for easily recreated entries

**Next.js · TypeScript · Supabase (Auth, Postgres, Storage) · Vercel · Stripe**

### EchoMe — family legacy platform
A TypeScript web app for preserving family memories, live at `app.echome.family`. Folder-first architecture where every upload path flows through a person's folder, with AI features progressively disclosed only after enough material exists and the user explicitly opts in.

- Postgres-backed session store (moved off in-memory sessions so deploys stop logging people out)
- Correct deletion cascades across dependent letter and resend tables
- Whisper transcription, Sharp image processing, Cloudflare R2 object storage
- Navigation redesigned before visual polish: predictable back behavior down the Dashboard → Folder → memory tree

**TypeScript · Drizzle ORM · Supabase/Postgres · Railway · Cloudflare R2 · Whisper**

### Recipe Vault — private family recipe app
A Next.js/Supabase/Vercel app for a real family recipe collection of 200+ recipes, with a household privacy model built on Postgres row-level security and magic-link auth.

- Import pipeline that ingests recipes from URLs (JSON-LD first, HTML heuristics as fallback), DOCX files via `mammoth`, and text PDFs via `pdfjs-dist`, splitting multi-recipe documents into individual candidates
- Review-before-save flow: imports land as candidates for correction and batch save instead of silently creating records
- Source images are downloaded into Supabase Storage at save time so recipes don't break when a source CDN disappears
- Structured nutrition fields (protein, sodium, potassium, phosphorus) for kidney-diet cooking, extracted during import
- Taxonomy tooling — rename, merge, delete, and unused-tag cleanup — so a growing collection doesn't accumulate duplicate labels

**Next.js · TypeScript · Supabase (RLS, Storage) · Vercel · mammoth · pdfjs-dist**

### Internal tools dashboard
A browser-hosted dashboard that gives coworkers access to operational Python GUIs without distributing production source or private configuration. Frontend on AWS Amplify, processing and credentials stay server-side behind an API, with employee-readable docs kept in a separate repository from production code.

**AWS Amplify · Python APIs · role-based access · audit logging**

### Company website rebuild
Delivered a standalone Next.js site with a CMS-backed content layer, deployed on Vercel, replacing a legacy platform — including the respondent-facing paths that real survey participants land on.

**Next.js · TypeScript · headless CMS · Vercel**

---

## How I work

- Data quality is a design decision, not a cleanup step. Uncertain rows get held for review, not approximated.
- Pipeline stages stay separable so failures stay diagnosable.
- Navigation and predictability before visual polish.
- Rules belong in declarative config that a human can audit, not buried in code.

## Stack

**Languages:** Python, TypeScript, SQL
**Data:** pandas, pyreadstat, Postgres, SPSS `.sav`, Qualtrics exports, NHTSA vPIC
**Web:** Next.js, React, Tailwind, Supabase, Drizzle ORM
**Infra:** Vercel, Railway, AWS Amplify, Cloudflare R2, Stripe, GitHub Actions

---

Several repositories here are private because they contain client or family data. Happy to walk through architecture, code, or a live demo on request.
