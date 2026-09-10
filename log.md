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

## [2026-09-10] update | Full Karpathy LLM Wiki alignment
- SCHEMA.md: added Storage tag category, expanded tag taxonomy, added scaling rules for index
- index.md: rewrote with richer one-line summaries, proper section structure, total pages counter
- README.md: added Karpathy pattern reference, repository link, clearer usage section
- entities/macbook-air-5-2.md: expanded hardware specs, added Software Status and Hardware Notes sections, 4 cross-refs
- entities/bq20z451-battery.md: minor cleanup, 3 cross-refs
- entities/applesmc-driver.md: expanded dependencies, added patch status (not upstream), 4 cross-refs
- concepts/luks-btrfs-boot.md: expanded pitfalls, added recovery section, 4 cross-refs
- concepts/kernel-module-install.md: expanded common mistakes table, added Version Matching section, 4 cross-refs
- All pages now have minimum 2 outbound wikilinks (verified: 3-4 each)
- All tags verified against SCHEMA.md taxonomy (no rogue tags)
- No new pages created — focused on content quality of existing pages
