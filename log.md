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

## [2026-09-10] update | Karpathy practice alignment pass
- SCHEMA.md: added Scaling Rules section (index section 50+ entries, 200+ total, log rotation 500+)
- index.md: added scaling rule comment, verified alphabetical ordering in sections
- entities/macbook-air-5-2.md: added Relationships section with 4 cross-refs, fixed See Also to match
- entities/bq20z451-battery.md: added Relationships section with 3 cross-refs
- entities/applesmc-driver.md: added Relationships section with 4 cross-refs, fixed macair→macbook-air wikilink
- concepts/kernel-module-install.md: added Relationships section with 4 cross-refs
- concepts/luks-btrfs-boot.md: added Relationships section with 4 cross-refs
- All pages now have explicit Relationships sections for stronger interlinking
- Verified all wikilinks resolve to existing pages (no broken links)
- All frontmatter validated against SCHEMA.md requirements

## [2026-09-11] ingest | WiFi test results + charge threshold kernel build
- Created raw source: raw/articles/wifi-bcm43224-test-results.md (physical WiFi test)
- Created raw source: raw/articles/kernel-applesmc-charge-threshold.md (custom kernel build)
- Created source-summary pages: sources/wifi-bcm43224-test-results.md, sources/kernel-applesmc-charge-threshold.md
- Created 3 new entities: bcm43224-wifi, broadcom-wl-dkms, linux-applesmc-kernel
- Created 3 new concepts: wifi-driver-comparison, custom-kernel-build-arch, charge-threshold-control
- Updated entities/macbook-air-5-2.md: added WiFi details, 4 new relationships, source + updated date
- Updated entities/applesmc-driver.md: added build method details, 3 new relationships, source + updated date
- Updated entities/bq20z451-battery.md: added charge threshold details, 2 new relationships, source + updated date
- Updated concepts/kernel-module-install.md: 2 new relationships, source + updated date
- Updated concepts/luks-btrfs-boot.md: 2 new relationships, source + updated date
- Updated index.md: added 6 new pages + 2 sources, total pages 5→12, updated date
- All new pages have minimum 2 outbound wikilinks
- All tags verified against SCHEMA.md taxonomy
