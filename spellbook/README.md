# hpma-data/spellbook

Standalone dataset from *Harry Potter: Magic Awakening* (HPMA): **141
spellbook cards** plus — since v7 — a fully separate **echoes** dataset
(184 echoes / 46 characters / 270 affixes / growth & economy tables),
bilingual (zh/en), including artwork.

Produced by the [HPMA-Research](https://github.com/ChanningWang2018)
extraction toolchain (`export_spellbook_web_bundle.py` →
`package_spellbook_bundle.py`); this directory is the published data-package
layer for consumers.

## Current version

**v7.20261005.0** — version semantics (shared contract between producer, data
package and consumers):

- `schema_version` — data *structure* version; bumped when fields change in a
  way that requires consumer code updates (see the header of the bundled
  `schema/*.schema.json` files for the per-version changelog).
- `data_version` — *content* refresh stamp (YYYYMMDD since 2026-10-01);
  bumped when a game update adds or changes content, structure unchanged.
- Release version = `{schema_version}.{data_version}.0`. Current:
  **v7.20261005.0** (schema 7, data 20261005); a game hot update
  re-publishes as `v7.{new YYYYMMDD}.0`, a structure change as
  `v{S+1}.{date}.0`.
- Git tags: `spellbook-v{version}` (e.g. `spellbook-v7.20261005.0`).

One version axis covers all datasets in this directory: the `datasets`
registry in `manifest.json` lists what ships (id / file / count), and
`cards.json` / `echoes.json` always carry the same `schema_version` +
`data_version` pair as the manifest.

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
- `echoes.json` — echo dataset (v7 onwards), fully disjoint from the cards
  domain: `characters` (46) / `echoes` (184) / `attribute_groups` /
  `affixes` (270) / `growth` / `economy` / `card_echo_scores`; echo IDs and
  card IDs are independent spaces — never infer a record's type from its
  numeric ID, use the `datasets` registry instead
- `echo_images/` + `echo_images_webp/` — echo icons (named per source file;
  icons missing from the game install are `null` and listed in
  `manifest.coverage.echoes.missing_icons`)
- `schema/` — JSON Schema files for validating `cards.json` /
  `manifest.json` / `echoes.json`
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

The producer repo ships a **reference consumer** built in: the bundle's
`check.html` (per-record manual verification page) loads data the way a
consumer should — via the `manifest.json` `datasets` registry — and renders
both datasets; it doubles as a living usage example of this contract.

## Update flow

Game hot update → rerun the HPMA-Research export →
`package_spellbook_bundle.py` → `publish_spellbook_bundle.py` (push + GitHub
Release; npm not yet enabled) → bump consumers.

## License

Game-derived data, **not** open-source — see
[../LICENSE-NOTES.md](../LICENSE-NOTES.md).
