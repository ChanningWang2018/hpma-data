# hpma-data/spellbook

数据集目录（本仓已归档冻结；继任仓
[hpma-bits/hpma-spellbook](https://github.com/hpma-bits/hpma-spellbook)）。

## 内容

- `cards.json` — 魔咒书卡牌数据：141 条，zh/en 双语，含分级数值与图路径
- `echoes.json` — 回响数据集：184 条 / 46 角色 / 270 词缀，与 cards 域分立
- `manifest.json` — 版本与覆盖率清单（`datasets` 注册表 + `coverage`）
- `images/`、`images_webp/`、`frames/` — 卡面图与品质边框
- `echo_images/`、`echo_images_webp/` — 回响图标
- `schema/` — JSON Schema（cards / manifest / echoes）
- `checksums.txt` — sha256 清单，`sha256sum -c checksums.txt` 校验
- `check.html` — 内置参考消费者，随发布 zip 附带（按 `manifest.json` 的
  `datasets` 注册表加载数据并渲染，双数据集核对页）

## 版本轴

Release / tag 版本 = `spellbook-v{schema_version}.{data_version}.0`
（当前 `spellbook-v8.20261005.0`）：

- `schema_version` — 数据结构版本；消费端需改代码时 +1
- `data_version` — 内容刷新版本（YYYYMMDD）

历史版本见本仓 [Releases](../../releases)；后续更新在继任仓按
`cards-v{S}.{D}.0` / `echoes-v{S}.{D}.0` 双轴发布。

## 许可

仅供个人学习研究，请勿商用；如有权利方异议，请联系删除。
见 [../LICENSE-NOTES.md](../LICENSE-NOTES.md)。
