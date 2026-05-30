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
- [[pmx-format]] — PMX 模型格式总览(含规格表) · *stable*
- [[骨骼-bones]] — 骨骼命名、IK、付与 · *stable*
- [[准标准骨骼-semi-standard-bones]] — 准标准骨清单 + 实测付与系数 · *stable*
- [[权重-weights]] — 权重与 BDEF/SDEF · *stable*
- [[表情-morphs]] — 表情/变形(顶点/骨骼/材质/UV/组) · *stable*
- [[口型-lipsync]] — 对口型(元音 morph) · *stable*
- [[材质-materials]] — Toon / Sphere(SPH/SPA)/ 描边 · *stable*
- [[toon-贴图对照]] — 共有 toon01–10 各编号特征与选用 · *stable*
- [[物理-physics]] — 刚体与关节 · *stable*
- [[vmd-动作格式]] — VMD 动作/表情/相机数据格式 · *stable*
- [[vpd-姿势格式]] — VPD 单帧姿势数据 · *stable*
- [[相机工作-camera]] — 相机帧/补间曲线/镜头 · *stable*
- [[x配件与舞台]] — .x 配件 / 舞台格式 · *stable*

### XPS / XNALara
- [[xps-format]] — XPS 模型格式与数据结构 · *stable*
- [[xps-骨骼映射]] — XPS → MMD 骨骼名对照与映射策略 · *stable*
- [[xps-材质差异]] — XPS → MMD 材质体系差异与转换 · *stable*
- [[uv-贴图打包]] — UV 处理、mesh/材质合并、贴图图集与管理 · *stable*
- [[坐标系-朝向-pose]] — 轴向/朝向/A-T pose/骨骼roll(扭曲散架根因) · *stable*

## 工具 (tools)
- [[mmd_tools]] — Blender 的 MMD 核心插件(导入/导出);v4.x=Blender 4.2+,旧 v2.x=Blender 3.6 · *stable*
- [[xps-tools-blender]] — XPS/XNALara 导入 Blender 插件 · *stable*
- [[cats-blender-plugin]] — 模型清理优化;原版 4.0 后停更,新版用 Team Neoneko/Tuxedo 分支 · *stable*
- [[pmxeditor]] — PMX 精修工具;含准标准ボーン追加プラグイン · *stable*
- [[mme-特效]] — MikuMikuEffect / Ray-MMD 等渲染特效 · *stable*
- [[mmd兼容编辑器-mmm-nanoem]] — MMM(动作强)/ nanoem(Mac) · *stable*

## 流程 (workflows)
- [[xps-to-mmd-流程]] — **XPS → Blender → MMD 端到端转换** · *stable*
- [[blender-mmd-绑定改造]] — Blender 端建 IK/付与/显示枠/英文名 · *stable*
- [[blender-to-pmx-导出流程]] — 从建模到 MMD 可用的端到端路线 · *stable*
- [[模型改造-移植]] — 体型改变/换衣换发/部件移植 · *stable*
- [[mmd-to-vrchat-unity]] — PMX → VRChat/Unity 移植 · *stable*

## 使用 / 生态 (usage)
- [[mmd本体-使用]] — MikuMikuDance.exe 加载模型/动作/物理/出片 · *stable*
- [[外部親-accessory]] — 外部親与配件(拿道具/戴饰品) · *stable*
- [[mme-特效]] — 见上「工具」:MikuMikuEffect / Ray-MMD
- [[素材站与规约-resources]] — 模型/动作来源站点与使用规约 · *stable*

## 参考 (reference)
- [[标准骨架范本-reika]] — 一具完整 PMX 的实测骨架/IK/付与/物理/显示枠(263 骨) · *stable*

## 排查 (troubleshooting)
- [[xps-转换常见问题]] — XPS → MMD 转换常见报错与解决 · *stable*
- [[导出前qa清单]] — 导出 PMX 前逐项自检 · *stable*
- [[troubleshooting/README|问题排查索引]] · *stub*

---

## 现状与下一步
- 覆盖范围已从「XPS→MMD 转换/建模线」扩展到 **MMD 全生态**:格式(PMX/VMD/XPS)、骨骼/权重/材质/表情/物理/UV、工具链、本体使用、动作/口型、特效、素材规约。
- 多数页为 `draft`(领域知识 + 部分二进制实测);[[标准骨架范本-reika]] 与准标准骨页已 `stable`。
- 下一步:把高频 draft 页逐个核实到 stable;有新素材(VMD/MME 工程等)可继续 `ingest` 出实测真值。
