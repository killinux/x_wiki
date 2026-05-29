---
title: mmd_tools (Blender 插件)
type: tool
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# mmd_tools — Blender 的 MMD 核心插件

让 Blender 能**导入/导出 PMX/PMD 模型与 VMD 动作**的关键插件,是 Blender×MMD 工作流的中枢。

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
| Bone Tools | [[骨骼-bones]](IK、付与) |
| Material | [[材质-materials]](Toon/Sphere/edge) |
| Morph Tools | [[表情-morphs]] |
| Rigid Body / Joint | [[物理-physics]] |

## 注意
- **版本兼容性敏感**:不同 Blender 版本要装对应版本的 mmd_tools;版本号相关结论务必标注来源与日期。
- 维护版本历史上有多个(原 powroupi 版、后续社区/UuuNyaa 维护版),功能与安装方式可能不同——以你实际安装的版本文档为准。
- 常与 [[cats-blender-plugin]] 配合做模型清理。

完整导出路线见 [[blender-to-pmx-导出流程]]。

> 待补充:你实际使用的 mmd_tools 版本、安装方式、对应 Blender 版本——ingest 后填入。
