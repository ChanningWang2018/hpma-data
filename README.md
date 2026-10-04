# hpma-data

Data packages  from * Potter: * (HPMA, PC client)
by the [](https://github.com/) 
toolchain. One directory per dataset; each dataset is self-contained
(documentation, data, images, JSON Schemas, checksums) and versioned
independently.

## Datasets

| Directory | Contents | Current version |
|---|---|---|
| [`spellbook/`](spellbook/) | In-game spellbook (魔咒书): 141 duel cards, zh/en text, level stats, card art, quality frames | v6.20261004.0 (schema 6, data 20261004) |

## Consuming

Per-dataset instructions in each directory's README. In short:

1. **git submodule** — pin this repo at a `spellbook-vX.Y.Z` tag.
2. **CI download** — fetch `hpma-spellbook-data-{ver}.zip` from the matching
   GitHub Release and verify the `.sha256` file.

npm (`hpma-spellbook-data`) is planned but **not yet published** — this
README will link the package once the npm channel ships.

## License

 data, **not** open-source — see
[LICENSE-NOTES.md](LICENSE-NOTES.md).
