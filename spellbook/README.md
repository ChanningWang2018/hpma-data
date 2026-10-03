# hpma-data/spellbook

Standalone dataset of spellbook cards from *Harry Potter: Magic Awakening*
(HPMA): **141 cards**, bilingual (zh/en), including card art.

Produced by the [HPMA-Research](https://github.com/ChanningWang2018)
extraction toolchain (`export_spellbook_web_bundle.py` →
`package_spellbook_bundle.py`); this directory is the published data-package
layer for consumers.

## Current version

**v5.20261004.0** — version semantics (shared contract between producer, data
package and consumers):

- `schema_version` (currently `1`) — data *structure* version; bumped when
  fields change in a way that requires consumer code updates.
- `data_version` (currently `1`) — *content* refresh counter starting at 1;
  bumped when a game update adds or changes cards, structure unchanged.
- Release / npm version = `{schema_version}.{data_version}.0` — the npm minor
  always equals the data generation. Current: **v5.20261004.0**
  (schema 5, data 20261004); a game hot update bumping data to 2 becomes v1.2.0.
- Git tags: `spellbook-v{version}` (e.g. `spellbook-v1.1.0`).

## Files

- `cards.json` — card records: id/type/rarity/cost/img/spell_word/tags +
  `i18n{zh,en}` name/desc/quote + per-level `levels` stats
- `manifest.json` — versions, generated_at, coverage, source notes
- `images/{id}.png` — card art, 375x500 transparent PNG
- `schema/` — JSON Schema files for validating `cards.json` / `manifest.json`
- `checksums.txt` — sha256 list; verify with `sha256sum -c checksums.txt`

## Consuming

1. **npm package** — `hpma-spellbook-data`, versioned as above.
2. **git submodule** — pin this repo at a `spellbook-vX.Y.Z` tag; the dataset
   root is the `spellbook/` directory.
3. **CI download** — fetch `hpma-spellbook-data-{ver}.zip` from the producer's
   GitHub Release (tag `spellbook-v{ver}`) and verify against the `.sha256`
   file; the zip extracts to a `spellbook/` directory.

A reference consumer lives at `E:\Scripts\hpma-cards-consumer` (npm /
submodule / CI-download wiring, schema validation in CI, configurable image
base URL).

## Update flow

Game hot update → rerun the HPMA-Research export →
`package_spellbook_bundle.py` → `publish_spellbook_bundle.py` (push + GitHub
Release + npm) → bump consumers.

## License

Game-derived data, **not** open-source — see
[../LICENSE-NOTES.md](../LICENSE-NOTES.md).
