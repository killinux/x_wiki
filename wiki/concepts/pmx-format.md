---
title: PMX 模型格式
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# PMX 模型格式 (PMX / Polygon Model eXtended)

MMD 当前的**标准模型格式**,由 PMD 演进而来。一个 `.pmx` 文件打包了模型的全部数据。

## 与 PMD 的关系
- **PMD**:旧格式,字段固定、对编码与扩展支持差。
- **PMX**:现行标准(常见 2.0 / 2.1),支持 UTF 文本、更灵活的材质、更多变形类型与骨骼标志。新建模型应优先用 PMX。

## 一个 PMX 文件里有什么
- 顶点(位置、法线、UV、附加 UV)与 **变形类型** → 见 [[权重-weights]]
- 面 / 材质(贴图、Toon、Sphere 标志)→ 见 [[材质-materials]]
- 骨骼(层级、IK、轴限制)→ 见 [[骨骼-bones]]
- 变形 / 表情(顶点、骨骼、材质、UV、组)→ 见 [[表情-morphs]]
- 刚体 + 关节(物理)→ 见 [[物理-physics]]
- 显示枠(显示框,把骨骼/表情分组方便操作)

## 配套格式
- `.vmd` — 动作 / 表情 / 相机数据(motion)。建模阶段不产出,但绑定好坏直接影响 VMD 复用效果。
- `.vpd` — 单帧姿势数据。

## 在 Blender 里
Blender 不原生支持 PMX,需要 [[mmd_tools]] 插件来导入/导出。完整路线见 [[blender-to-pmx-导出流程]]。

> 待补充:PMX 2.0 与 2.1 的具体差异(2.1 的部分特性 MMD 本体支持有限)——请 ingest 权威来源后校正。
