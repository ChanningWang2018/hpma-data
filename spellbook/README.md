# hpma-data/spellbook

Standalone dataset of spellbook cards from *Harry Potter: Magic Awakening*
(HPMA): **141 cards**, bilingual (zh/en), including card art.

Produced by the [HPMA-Research](https://github.com/ChanningWang2018)
extraction toolchain (`export_spellbook_web_bundle.py` →
`package_spellbook_bundle.py`); this directory is the published data-package
layer for consumers.

## Current version

**v7.20261005.0** — version semantics (shared contract between producer, data
package and consumers):

- `schema_version` — data *structure* version; bumped when fields change in a
  way that requires consumer code updates (currently `6`).
- `data_version` — *content* refresh stamp (YYYYMMDD since 2026-10-01);
  bumped when a game update adds or changes cards, structure unchanged
  (currently `20261004`).
- Release version = `{schema_version}.{data_version}.0`. Current:
  **v7.20261005.0** (schema 7, data 20261005); a game hot update
  re-publishes as `v6.{new YYYYMMDD}.0`, a structure change as
  `v7.{date}.0`.
- Git tags: `spellbook-v{version}` (e.g. `spellbook-v6.20261004.0`).

## Files

- `cards.json` — card records: id/type/rarity/cost/img/spell_word/tags +
  `i18n{zh,en}` name/desc/quote + per-level `levels` stats (v6: rows mirror
  the game `attr_val_list` 1:1 with `attr_name`; face-stats set in top-level
  `face_attrs`, hover picks in `levels.battle_show`)
- `manifest.json` — versions, generated_at, coverage, source notes
- `images/{id}.png` — card art, 375x500 transparent PNG
- `images_webp/{id}.webp` — card art WebP copies (same names/resolution, q82;
  2026-10-04 onwards — prefer these, fall back to PNG when absent)
- `frames/frame_{rarity}.png` — straight quality-frame overlays (v5 onwards)
- `schema/` — JSON Schema files for validating `cards.json` / `manifest.json`
- `checksums.txt` — sha256 list; verify with `sha256sum -c checksums.txt`

## Consuming

1. **git submodule** — pin this repo at a `spellbook-vX.Y.Z` tag; the dataset
   root is the `spellbook/` directory.
2. **CI download** — fetch `hpma-spellbook-data-{ver}.zip` from the producer's
   GitHub Release (tag `spellbook-v{ver}`) and verify against the `.sha256`
   file; the zip extracts to a `spellbook/` directory.

An npm package (`hpma-spellbook-data`) is planned but **not yet published** —
do not depend on it; this README will link the package once the channel
ships.

A reference consumer lives at `E:\Scripts\hpma-cards-consumer` (submodule /
CI-download wiring, schema validation in CI, configurable image base URL).

## Update flow

Game hot update → rerun the HPMA-Research export →
`package_spellbook_bundle.py` → `publish_spellbook_bundle.py` (push + GitHub
Release; npm not yet enabled) → bump consumers.

## License

Game-derived data, **not** open-source — see
[../LICENSE-NOTES.md](../LICENSE-NOTES.md).
