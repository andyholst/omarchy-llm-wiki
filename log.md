# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to log-YYYY.md, start fresh.

## [2026-09-10] create | Wiki initialized
- Domain: Omarchy Linux, kernel development, hardware support
- Structure created with SCHEMA.md, index.md, log.md
- Directories: raw/articles, raw/papers, raw/transcripts, raw/assets, entities, concepts, comparisons, queries
- Initial pages: 5 (macbook-air-5-2, bq20z451-battery, applesmc-driver, luks-btrfs-boot, kernel-module-install)
- Configured WIKI_PATH in ~/.bashrc and ~/.hermes/.env

## [2026-09-10] update | Wiki lint and cleanup
- Fixed SCHEMA.md: added `intel`/`broadcom` to tag taxonomy, fixed frontmatter indentation
- Fixed index.md: corrected page count from 7 → 5
- Fixed README.md: updated to reflect actual wiki structure
- All 5 entity/concept pages verified: frontmatter valid, wikilinks present, cross-references intact
- raw/ directory is empty — no sources ingested yet; sources:[] on all pages is expected
