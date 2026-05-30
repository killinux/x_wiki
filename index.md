---
title: 内容地图
type: index
updated: 2026-05-30
---

# Blender × MMD 建模知识库 — 内容地图

<!-- updated 2026-05-30: 校正 mmd_tools/Cats 版本兼容性;新增准标准骨骼页 -->


> 维护说明见 [CLAUDE.md](CLAUDE.md);用法见 [README.md](README.md);摄入记录见 [log.md](log.md)。
> status: `stub` 占位 · `draft` 种子内容待校正 · `stable` 已用可靠来源核实。

## 概念 (concepts)

### MMD / PMX
- [[pmx-format]] — PMX 模型格式总览 · *draft*
- [[骨骼-bones]] — 骨骼命名、IK、付与 · *draft*
- [[准标准骨骼-semi-standard-bones]] — 准标准骨清单 + 实测付与系数 · *stable*

### 参考范本 (reference)
- [[标准骨架范本-reika]] — 一具完整 PMX 的实测骨架/IK/付与/物理(263 骨) · *stable*
- [[表情-morphs]] — 表情/变形(顶点/骨骼/材质/UV/组) · *draft*
- [[物理-physics]] — 刚体与关节 · *draft*
- [[材质-materials]] — Toon / Sphere(SPH/SPA)/ 描边 · *draft*
- [[toon-贴图对照]] — 共有 toon01–10 各编号特征与选用 · *draft*
- [[权重-weights]] — 权重与 BDEF/SDEF · *draft*

### XPS / XNALara
- [[xps-format]] — XPS 模型格式与数据结构 · *draft*
- [[xps-骨骼映射]] — XPS → MMD 骨骼名对照与映射策略 · *draft*
- [[xps-材质差异]] — XPS → MMD 材质体系差异与转换 · *draft*
- [[坐标系-朝向-pose]] — 轴向/朝向/A-T pose/骨骼roll(扭曲散架根因) · *draft*

## 工具 (tools)
- [[mmd_tools]] — Blender 的 MMD 核心插件(导入/导出);v4.x=Blender 4.2+,旧 v2.x=Blender 3.6 · *draft*
- [[xps-tools-blender]] — XPS/XNALara 导入 Blender 插件 · *draft*
- [[cats-blender-plugin]] — 模型清理优化;原版 4.0 后停更,新版用 Team Neoneko/Tuxedo 分支 · *draft*
- [[pmxeditor]] — PMX 精修工具;含准标准ボーン追加プラグイン · *draft*

## 流程 (workflows)
- [[xps-to-mmd-流程]] — **XPS → Blender → MMD 端到端转换** · *draft*
- [[blender-mmd-绑定改造]] — Blender 端建 IK/付与/显示枠/英文名 · *draft*
- [[blender-to-pmx-导出流程]] — 从建模到 MMD 可用的端到端路线 · *draft*

## 排查 (troubleshooting)
- [[xps-转换常见问题]] — XPS → MMD 转换常见报错与解决 · *draft*
- [[导出前qa清单]] — 导出 PMX 前逐项自检 · *draft*
- [[troubleshooting/README|问题排查索引]] · *stub*

---

## 现状与下一步
- 现有内容为**种子页面**(基于通用领域知识),用来固化页面约定与交叉引用结构。
- 它们都标了「待补充」点。请用你的可靠资料 `ingest` 来校正版本敏感信息(尤其 Blender / mmd_tools 版本兼容性)和具体操作步骤。
- 建议优先补:① 你用的 Blender + mmd_tools 版本;② 半标准骨架清单;③ 你常踩的坑(进 troubleshooting)。
