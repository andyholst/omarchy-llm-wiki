# Omarchy LLM Wiki

Knowledge base for Omarchy Linux on MacBook Air 5,2 — kernel development, hardware support, power management.

Built following [Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) pattern: interlinked markdown files, immutable raw sources, agent-curated synthesis.

## Structure

```
wiki/
├── SCHEMA.md           # Conventions, tag taxonomy, structure rules
├── index.md            # Sectioned content catalog with one-line summaries
├── log.md              # Chronological action log (append-only)
├── raw/                # Layer 1: Immutable source material
│   ├── articles/       # Web articles, clippings
│   ├── papers/         # PDFs, arxiv papers
│   ├── transcripts/    # Meeting notes, interviews
│   └── assets/         # Images, diagrams
├── entities/           # Layer 2: Entity pages (people, orgs, products, models)
├── concepts/           # Layer 2: Concept/topic pages
├── comparisons/        # Layer 2: Side-by-side analyses
└── queries/            # Layer 2: Filed query results worth keeping
```

## Usage

All pages are markdown with YAML frontmatter and `[[wikilinks]]`. Open in Obsidian, VS Code, or any editor.

## Karpathy Practice Compliance

- **Three-layer architecture**: Raw sources (immutable), wiki pages (agent-curated), schema (conventions)
- **Frontmatter on every page**: title, created, updated, type, tags, sources, confidence
- **Wikilinks everywhere**: minimum 2 outbound links per page, explicit Relationships sections
- **Provenance markers**: used on pages synthesizing 3+ sources
- **Tag taxonomy**: defined in SCHEMA.md, enforced on all pages
- **Page thresholds**: create only when entity appears in 2+ sources or is central to one
- **Update policy**: contradictions noted with dates, marked in frontmatter
- **Scaling rules**: index sections split at 50+, log rotates at 500+, topic-map at 200+

## Status

- **Pages:** 5 (3 entities, 2 concepts)
- **Sources ingested:** 0 (raw/ is empty)
- **Last updated:** 2026-09-10
- **Repository:** https://github.com/andyholst/omarchy-llm-wiki
