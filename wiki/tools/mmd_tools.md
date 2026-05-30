---
title: mmd_tools (Blender 插件)
type: tool
status: stable
sources:
  - 种子内容/通用领域知识
  - https://github.com/MMD-Blender/blender_mmd_tools
  - https://extensions.blender.org/add-ons/mmd-tools/
  - https://mmd-blender.fandom.com/wiki/MMD_UuuNyaa_Tools
updated: 2026-05-30
---

# mmd_tools — Blender 的 MMD 核心插件

让 Blender 能**导入/导出 PMX/PMD 模型与 VMD 动作**的关键插件,是 Blender×MMD 工作流的中枢。

## 版本与 Blender 兼容性 (核实于 2026-05-30)

| 版本线 | 适用 Blender | 安装方式 | 状态 |
|---|---|---|---|
| **v4.x**(当前) | **Blender 4.2 LTS ~ 5.1**(推荐 4.2+) | 官方 [extensions.blender.org](https://extensions.blender.org/add-ons/mmd-tools/),Edit → Preferences → Get Extensions 内直接装并自动更新 | 活跃维护 |
| **v2.x**(旧) | **Blender 3.6** | 手动下 zip(v2.10.3)→ Install from Disk | 不再维护 |

- 仓库现位于 **MMD-Blender 组织**(`github.com/MMD-Blender/blender_mmd_tools`),**fork 自 powroupi/blender_mmd_tools**,由 UuuNyaa 等接手维护。(来源: GitHub MMD-Blender;extensions.blender.org)
- 当前最新约 **v4.5.11**(2026-05-13);extensions 页明确写「推荐 Blender 4.2+ 搭配最新 mmd_tools,Blender 3.6 支持已停止维护」。(来源: extensions.blender.org,核实于 2026-05-30)
- **选版规则**:Blender ≥ 4.2 → 走 Extensions 装 v4.x;仍在 3.6 → 用 v2.10.3 旧 zip;更早的 Blender 已不支持。
- 另有配套增强插件 **MMD UuuNyaa Tools**(`blender_mmd_uuunyaa_tools`),用于场景/材质/物理辅助,需 Blender 4.2+ 与 mmd_tools v4.2.1+。(来源: mmd-blender.fandom MMD_UuuNyaa_Tools)

> 版本会变:升级 Blender 前先确认 mmd_tools 对应版本;涉及版本号的结论以 extensions.blender.org 当前页为准。

## 能做什么
- 导入 `.pmx` / `.pmd` 模型、`.vmd` 动作 / 表情 / 相机、`.vpd` 姿势。
- 导出 `.pmx`(建模成果)、`.vmd`。
- 维护 MMD 专属数据:**MMD Bone Tools / Material / Morph / Rigid Body / Joint / Display(显示枠)** 面板。
- 在 Blender 内预览物理、播放动作。

## 关键概念:Model 根空物体
导入后会得到一个 **MMD Model 空物体(Empty)** 作为根,下面挂 Armature + Mesh。所有 MMD 元数据挂在这套层级上——**不要随意打散层级**,否则导出会丢信息。

## 与各概念的对应
| 面板 | 对应概念 |
|---|---|
| Bone Tools | [[骨骼-bones]](IK、付与)·[[准标准骨骼-semi-standard-bones]] |
| Material | [[材质-materials]](Toon/Sphere/edge) |
| Morph Tools | [[表情-morphs]] |
| Rigid Body / Joint | [[物理-physics]] |

## 注意
- **版本兼容性敏感**:见上方版本表;版本号相关结论务必标注来源与日期。
- 维护谱系:**powroupi 原版 → MMD-Blender 组织 v2.x(Blender 3.6)→ v4.x(Blender 4.2+)**;以你实际安装版本的文档为准。
- 常与 [[cats-blender-plugin]] 配合做模型清理;v4 已把不少清理功能内置,MMD 用途下对 Cats 的依赖减少。

完整导出路线见 [[blender-to-pmx-导出流程]]。

> 提示:升级 Blender 前,在 Edit → Preferences → Get Extensions 核对本机 mmd_tools 版本与上表对应关系。
