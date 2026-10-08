[README.md](https://github.com/user-attachments/files/33188978/README.md)
# -
适用于文科生写作获取相关史实
# wenke-factbase 文科写作事实素材库

> 给中文写作者的事实素材库：**每条素材都带出处**，按写作主题检索，随取随用。
> A citation-first factbase for Chinese essay writing — every fact carries a verifiable source. Local-first, zero dependencies, agent-skill ready.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![Dependencies: none](https://img.shields.io/badge/Dependencies-0-brightgreen.svg)

写文章最怕两件事：**没有论据**，和**论据不可靠**。

factbase 把「背过的名句、学过的史实、读到的数据」整理成一个带出处的可检索素材库：

- 📚 **48 条种子素材**，六大门类：历史 / 文学 / 哲学 / 科技 / 文化 / 当代
- 🔍 **按写作主题检索** —— 要写「坚持」，直接查「坚持」，12 条素材立刻到手
- 🧾 **每条必带出处** —— 「据《史记·商君列传》」，而不是「有句话说得好」
- ✍️ **附引用示例** —— 示范这条素材怎么织进文章
- 🧩 **配套 Agent 技能** —— Claude Code / ZCode 等写作助手会先查库再动笔
- ⚙️ **零依赖** —— 纯 Python 标准库 + SQLite，离线可用，数据全在本地

## 快速开始

```bash
git clone https://github.com/<your-name>/wenke-factbase.git
cd wenke-factbase
python kb.py init        # 建库并载入 48 条种子素材
```

> 若系统 `python` 不可用（如 Windows 的 Microsoft Store 别名），请使用完整解释器路径，或 `uv run python kb.py ...`。

日常三条命令：

```bash
# 1. 按主题找素材（写作前：“我要写‘坚持’，有什么可用？”）
python kb.py theme 坚持

# 2. 按关键词搜（多个词，空格分隔，需全部命中）
python kb.py search 司马迁 逆境

# 3. 看看库里都有什么
python kb.py stats
```

## 素材长什么样

每条素材包含六个字段：

| 字段 | 说明 |
|---|---|
| `category` | 类别：历史 / 文学 / 哲学 / 科技 / 文化 / 当代 |
| `fact` | 一句话说清的事实陈述 |
| `source` | 出处：书名篇名、传记或官方数据（引用时的底气） |
| `era` | 年代 |
| `themes` | 适用主题标签，如：坚持、家国、匠心 |
| `citation` | 引用示例：示范怎么把这条素材写进文章 |

真实检索输出（`python kb.py theme 家国` 节选）：

```
──────────────────────────────────────────────
[4] 【历史】 南宋（1278年被俘，1283年就义）
  事实:南宋末年，文天祥兵败被俘，过零丁洋时写下“人生自古谁无死，留取丹心照汗青”，
       拒绝元朝劝降，1283年从容就义。
  出处:《文山先生全集·过零丁洋》《宋史·文天祥传》
  适用主题:家国,气节,信念,牺牲
  引用示例:写“家国情怀”：七百多年前那句“留取丹心照汗青”，是中国人气节最滚烫的注脚。
──────────────────────────────────────────────
[7] 【历史】 明末清初（1662年）
  事实:1662年，郑成功率军驱逐荷兰殖民者，收复台湾，台湾重回祖国版图。
  出处:《清史稿·郑成功传》；连横《台湾通史》
  适用主题:家国,勇气
  引用示例:写“家国领土”：1662年，郑成功收复台湾——历史反复印证：国土一寸不可弃。
──────────────────────────────────────────────
共 13 条。
```

## 全部命令

| 命令 | 作用 |
|---|---|
| `init [--force]` | 建库 / 载入种子素材（`--force` 清空重建） |
| `search 词1 词2 [-c 类别] [-t 主题] [-n 数量]` | 关键词检索 |
| `theme 标签 [-n 数量]` | 按主题标签检索 |
| `themes` | 列出所有主题标签及数量 |
| `show ID` | 查看某条素材完整信息 |
| `random [-c 类别]` | 随机抽一条（找灵感） |
| `add -c -f -s [-e] [-t] [-u]` | 新增一条素材 |
| `import 文件.json/.csv` | 批量导入 |
| `export 文件.json` | 导出全部（备份用） |
| `validate [文件]` | 校验素材文件格式（贡献者自检） |
| `stats` | 库统计 |

## 写作工作流

1. **动笔前**：`kb.py theme 主题词` / `kb.py search 关键词`，挑 2–3 条最贴切的素材
2. **写作中**：引用必带出处——「据《史记·商君列传》记载⋯⋯」比「有句话说得好」有分量
3. **写完**：核对引文与库中原文一致；数字类事实注明数据年份
4. **读到好素材**：随手入库，库会越用越厚

## 把新素材入库

```bash
python kb.py add -c 历史 -f "事实陈述" -s "出处" -e "年代" -t "主题1,主题2" -u "引用示例"
```

入库三原则：

1. **出处真实可查** —— 不写「网上看到」
2. **不确定的数字宁缺毋滥** —— 或注明「待核实」
3. **主题标签复用现有体系** —— 先 `kb.py themes` 看看已有哪些标签

## 配套 Agent 技能

仓库根目录的 `SKILL.md` 是配套的 Agent 技能文件，适用于 ZCode / Claude Code 等支持 SKILL.md 标准的写作助手：

- **ZCode**：复制到 `~/.zcode/skills/wenke-factbase/`
- **Claude Code**：复制到 `~/.claude/skills/wenke-factbase/`（或项目内 `.claude/skills/`）

技能生效后，写作请求会自动触发「先查库、引用带出处、写完核对」的流程。

## 设计原则：为什么不是 RAG / 知识图谱？

事实性素材要的是**准确与可追溯**，不是语义相似度：

- 一条素材能不能用，取决于**出处**和**写作主题**，不取决于向量距离
- 六字段结构天然适合人工校对与协作贡献；embedding chunk 做不到「必带出处」
- 本地、离线、零依赖：断网能用，数据属于你（`facts.db` 默认不进版本库）

## Roadmap

- [ ] 素材扩展到 500+（每门类 80+）
- [ ] `kb.py pack`：按教科书单元打包主题素材包
- [ ] 导出 Markdown 卡片 / Anki 背诵卡组
- [ ] 与 Zotero MCP 联动（规范论文参考文献场景）

## 贡献

欢迎 PR 补充素材，收录标准与提交流程见 [CONTRIBUTING.md](CONTRIBUTING.md)。
特别欢迎**出处辨析类素材**（纠正常见误引，如「天下兴亡，匹夫有责」实为梁启超概括）——这是本库的特色。

## License

[MIT](LICENSE)
