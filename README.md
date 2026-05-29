# Blender × MMD 建模知识库

一个基于 [Andrej Karpathy 的 LLM Wiki 模式](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 的个人知识库,聚焦 **用 Blender 为 MMD(MikuMikuDance)建模、改模、绑定、物理、导出**。

## 怎么用

这个仓库的设计是配合 Claude Code 使用的。常用指令(在本目录里对 Claude 说):

- **投喂资料**:把教程链接 / 笔记 / 文档放进 `sources/`,然后说「`ingest sources/xxx`」。也可以直接粘贴内容说「ingest 这个」。
- **提问**:「`query` 头发物理怎么设刚体和关节?」——Claude 只基于 wiki 回答,缺口会说明。
- **体检**:「`lint`」——找矛盾、过时信息、孤立页面、待写链接。
- **更新地图**:「`map`」——刷新 [index.md](index.md)。

工作约定与领域注意事项见 [CLAUDE.md](CLAUDE.md)(给 Claude 看的 schema)。

## 结构

| 目录 | 内容 |
|---|---|
| `sources/` | 你投喂的原始资料(只读) |
| `wiki/concepts/` | 概念:格式、骨骼、表情、物理、材质、权重 |
| `wiki/tools/` | 工具与插件 |
| `wiki/workflows/` | 端到端流程 |
| `wiki/troubleshooting/` | 报错与排查 |
| `index.md` | 内容地图 |
| `log.md` | 摄入日志 |

> 现有页面是**种子内容**,基于通用领域知识写成,用来演示页面约定。请用你自己的可靠资料 `ingest` 来校正和扩充。
