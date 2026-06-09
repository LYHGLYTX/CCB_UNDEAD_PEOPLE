# CCB_UNDEAD_PEOPLE 贴图包

基于 [I-am-Erk/CDDA-Tilesets](https://github.com/I-am-Erk/CDDA-Tilesets) 的 **Chibi_Ultica** 贴图,用于 CCB (Cataclysm: Cleanwater Bomb)。

Q 版（chibi）风格：角色与怪物使用 Q 版小人造型，世界环境沿用 Ultica 风格。

## 关于 id 与显示名

游戏内 `tileset.txt`：

```
NAME: UNDEAD_PEOPLE        # 贴图 id —— 模组通过它匹配兼容贴图
VIEW: CCB_UNDEAD_PEOPLE    # 游戏选项菜单内显示的名字
```

`NAME` 沿用 **`UNDEAD_PEOPLE`**，因为这个 id 被各类模组（mod_tileset 的 `compatibility`）适配得最广泛，能让最多模组的专属贴图正确加载。`VIEW` 设为 `CCB_UNDEAD_PEOPLE`，在游戏里与其它贴图包区分开。

## 来源

本仓库是 **Chibi_Ultica 的独立自包含版本**。上游 Chibi_Ultica 自身几乎不存散图，而是通过 symlink 复用同仓库其它贴图包的素材。本仓库已将这些 symlink **全部实体化**为真实文件，无需上游其它包即可独立 compose：

| 来源贴图包 | 提供内容 |
|---|---|
| **MShockXotto+** | 角色与怪物的 Q 版（Chibi*）精灵 |
| **UltimateCataclysm** | 地形、家具、物品、filler 等世界精灵 |
| **Dungeon Crawl: Stone Soup** | `dcss` 精灵表（CC0） |

## 署名

| 贡献者 | 角色 |
|---|---|
| I-am-Erk | CDDA-Tilesets 仓库维护者，Chibi_Ultica 贴图包作者 |
| MShock777 | MShockXotto+ 原版作者（角色/怪物精灵来源） |
| Ultica 团队 | UltimateCataclysm 贴图包作者（世界精灵来源） |
| Crawl 团队 | Dungeon Crawl: Stone Soup（dcss 精灵，CC0） |

本贴图包基于 **CC-BY-SA 3.0** 协议分发，与上游 CDDA-Tilesets 保持一致。

## 目录结构

```
pngs_*/                # 各尺寸散图（已实体化，无 symlink）
tile_info.json         # compose 配置（精灵表尺寸、偏移、exclude 规则）
layering.json          # 图层叠加规则
tileset.txt            # 贴图包元信息（NAME/VIEW）
fallback.png           # ASCII 回退图
tools/gfx_tools/
  compose.py           # 官方 compose 工具（搬运自 CDDA，仅打包本贴图用）
  list_tileset_ids.py  # 列出贴图包内全部 ID
```

> 注意：`tile_info.json` 与 `pngs_Chibi*` 里的 `Chibi*` 是**精灵表文件名**，是 compose 的内部素材引用，玩家不可见，请勿改动。游戏内身份只由 `tileset.txt` 的 `NAME`/`VIEW` 决定。

## 本地 compose

需要 Python3 + pyvips（或 Pillow 回退）：

```bash
pip install pyvips
python3 tools/gfx_tools/compose.py --use-all --feedback CONCISE . gfx/UNDEAD_PEOPLE
```

产物在 `gfx/UNDEAD_PEOPLE/`：`tile_config.json` + 各精灵表 PNG。

## 自动构建

推送到 `master` 或手动触发 `workflow_dispatch` 时，CI 会自动 compose 并发布一个包含成品贴图的 Release ZIP。

## 在 CCB 中使用

CCB 的 CI 构建流程会从本仓库的最新 Release 下载成品贴图，供玩家在游戏内选用。
