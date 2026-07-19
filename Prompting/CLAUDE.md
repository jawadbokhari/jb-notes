# Prompting Project

## Purpose
A learning + practice workspace for prompt engineering with Claude (and LLMs generally). Source material (books, articles, courses) gets read here, distilled into techniques and reusable templates, and — once polished — published into the public jb-notes site.

## How this folder relates to `content/`
This repo is a Quartz site. Only files under `content/` get published. This `Prompting/` folder (repo root, sibling to `content/`) is a **staging area**:

- `Prompting/` — working notes, source extractions, drafts, template library (not published)
- `content/prompting/` — polished, finished notes ready for the public site (create as topics mature)

Workflow: read source → extract into `sources/` → distill into `techniques/` and `templates/` → once a note is solid, move/adapt it into `content/prompting/` with the same frontmatter conventions as the rest of the vault (see `content/ai-fundamentals/*.md` for style reference: `---\ntitle: X\n---`, terse notes, tables, Obsidian wikilinks `[[slug|Label]]`).

## Structure
- `sources/` — condensed extractions from books/courses/articles, one file per source, with chapter/section references so claims are traceable back to origin
- `techniques/` — technique-level notes (one concept per file), split into foundational vs. advanced
- `templates/` — ready-to-copy prompt templates, grouped by use case

## Conventions
- Keep notes terse and scannable (bullets, tables) — match the existing vault's style, not the source book's prose.
- Every technique/template note should cite its source (book + chapter) so provenance isn't lost.
- When multiple sources cover the same technique, merge into one note and list all sources rather than duplicating.

## Sources logged so far
- *Mastering Claude AI* (Ryan Dickey, Apress) — epub in `~/Downloads/01_Learning & Development/`. Extracted: Ch.4 "The Art of Prompting", Ch.10 "Advanced Prompting Strategies", Appendix A (Quick Reference), Appendix C (Templates & Frameworks). See `sources/mastering-claude-ai.md`.
