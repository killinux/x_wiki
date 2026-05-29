# LLM Wiki Schema — Blender × MMD 建模知识库

这是一个按 Andrej Karpathy「LLM Wiki」模式构建的个人知识库,领域聚焦 **用 Blender 为 MMD(MikuMikuDance)做建模 / 改模 / 绑定 / 物理 / 导出**。

你(Claude)是这个 wiki 的**维护者**。你的工作不是每次都重读原始资料,而是把资料「编译」进结构化的 markdown 页面,并长期保持它的一致性。

---

## 三层架构

1. **Raw sources(`sources/`)** — 不可变。我收集的原始资料:教程链接、论坛帖、视频笔记、官方文档、踩坑记录。你只读不改。
2. **The wiki(`wiki/`)** — 你维护的产物。摘要页、概念页、工具页、流程页、问题排查页,互相用 `[[wiki 链接]]` 交叉引用。
3. **The schema(本文件)** — 约定与工作流。

---

## 目录约定

```
sources/                 # 原始资料(我投喂,你只读)
wiki/
  concepts/              # 概念:格式、骨骼、表情、物理、材质、权重…
  tools/                 # 工具/插件:mmd_tools、Cats、PMXEditor…
  workflows/             # 端到端流程:建模→UV→绑定→物理→导出
  troubleshooting/       # 报错与症状 → 原因 → 解法
index.md                 # wiki 首页 / 内容地图
log.md                   # 摄入日志(每次 ingest 追加一行)
```

## 页面约定

- 文件名:`kebab-case` 或中文短名,概念页可中英混排(如 `骨骼-bones.md`)。
- 每个 wiki 页面顶部带 frontmatter:
  ```yaml
  ---
  title: 页面标题
  type: concept | tool | workflow | troubleshooting | entity
  status: stub | draft | stable
  sources: [来源文件名或URL, ...]   # 该页知识的出处
  updated: YYYY-MM-DD
  ---
  ```
- 交叉引用用 `[[文件名不带扩展名]]`,例如 `[[pmx-format]]`、`[[mmd_tools]]`。链接到尚不存在的页面也可以——这是「待写」的标记。
- 每个结论尽量可溯源:重要论断后用 `(来源: …)` 标注。
- 术语**中日英对照**:MMD 大量使用日文术语,页面里保留日文原名 + 中文 + 英文,例如 `センター / 中心骨 / center`。

---

## 工作流(我会用这些动词指挥你)

### `ingest`(摄入)
我丢进一份新资料(放进 `sources/` 或直接粘贴)。你:
1. 通读资料。
2. 判断它触及哪些已有页面,更新它们;不存在的就新建。
3. 抽取人物/工具/概念作为实体页并交叉引用。
4. 在 `log.md` 追加一行:日期、来源、改动了哪些页面。
> 一份资料牵动 5–15 个页面是正常的。

### `query`(查询)
我提一个问题。你**只基于 wiki 内容**回答(不够就说明缺口)。如果答案有价值,把它整理成新页面回填,并在 `log.md` 记一笔。

### `lint`(体检)
我说 lint 时,你扫描整个 wiki,报告:
- 矛盾的论断
- 过时 / 可能失效的信息(如插件版本、Blender 版本兼容性)
- 孤立页面(没有任何页面链接它)
- 缺失的交叉引用 / 待写的 `[[链接]]`
- frontmatter 缺失或 status 长期停在 stub 的页面

### `map`(地图)
更新 `index.md`,反映当前所有页面的结构与状态。

---

## 领域注意事项(避免常见错误)

- **格式**:PMX 是当前标准(PMX 2.0/2.1),PMD 是旧格式。优先围绕 PMX 组织知识。
- **版本敏感**:Blender 与 `mmd_tools` 的兼容性随版本变化大,涉及版本号的论断**必须**标注来源与日期。
- **不要编造数值**:骨骼名、变形类型(BDEF1/2/4、SDEF)、物理参数等若资料未给出,标为「待补充」,不要臆造。
- **保留日文原名**:MMD 生态以日文为主,骨骼名/材质标志(SPH/SPA/Toon)等保留原文。
