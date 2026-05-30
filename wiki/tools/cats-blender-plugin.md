---
title: Cats Blender Plugin
type: tool
status: stable
sources:
  - 种子内容/通用领域知识
  - https://github.com/absolute-quantum/cats-blender-plugin
  - https://github.com/teamneoneko/Cats-Blender-Plugin-Unofficial-
  - https://github.com/feilen/tuxedo-blender-plugin
updated: 2026-05-30
---

# Cats Blender Plugin

辅助清理/优化模型的 Blender 插件,常见于 MMD / VRChat 改模流程。典型用途:模型修复、合并骨骼并转移权重、合并材质、生成/简化等。

与 [[mmd_tools]] 配合:Cats 做清理优化,mmd_tools 做 MMD 数据与导出。

## 维护现状与分支 (核实于 2026-05-30)

原版 Cats 在 **Blender 4.0 之后基本停更**,新版 Blender 上要改用社区分支:

| 版本 | 仓库 | Blender 兼容 | 状态 |
|---|---|---|---|
| 原版 Cats | absolute-quantum / cats-blender-plugin | 偏旧(~3.x) | Blender 4.0 后停滞 |
| **Cats Unofficial**(Team Neoneko) | teamneoneko/Cats-Blender-Plugin-Unofficial-(站点 catsblenderplugin.xyz) | 早期 4.1 系列;**最新版要求 Blender 5.0+**,不向下兼容 4.x | 社区续作,活跃 |
| **Tuxedo**(feilen) | feilen/tuxedo-blender-plugin | 跟进到 4.2/4.3/4.5/5.0(v0.4.2-alpha,2026-01) | Cats 减面/烘焙的替代,偏 VRChat 优化与 PBR 烘焙 |

> 选用建议(来源: 三处 GitHub 仓库 / r/blender 讨论,核实 2026-05-30):
> - Blender 4.1 左右 → **Cats Unofficial** 的 4.1 系列发布。
> - Blender 5.0+ → **Cats Unofficial** 最新版。
> - 需要减面 / PBR 烘焙(法线等)→ **Tuxedo**。
> - 注意:原版 Cats 在 Blender 4.1 起移除了减面(Decimation)与全身追踪修复等功能。

> 对 MMD 用途,[[mmd_tools]] v4 已把不少骨骼/材质清理功能内置,很多 MMD 改模流程已可少依赖 Cats。

## 在 XPS → MMD 流程中的作用

Cats 在 XPS 转换流程中非常有用:
- **Fix Model** — 自动识别 XPS 骨骼名并重命名为 MMD 标准日文名(不保证 100% 正确,需人工检查)
- **Join Meshes** — 合并过于碎片化的 mesh(XPS 模型常见)
- **合并骨骼 + 转移权重** — 简化多余骨骼(如游戏模型的辅助骨)
- **支持 XPS 导入** — 内部集成或调用 [[xps-tools-blender]]

详见 [[xps-to-mmd-流程]] 的骨骼处理步骤。

## 注意
- 版本与 Blender 兼容性敏感:见上表,版本号结论以各 GitHub 仓库当前页为准。
- 与 [[mmd_tools]] 装在同一 Blender 中协同使用。
- Cats 自动重命名按其内置规则映射,对**准标准骨**不一定补齐;完整准标准骨见 [[准标准骨骼-semi-standard-bones]],通常仍需在 [[pmxeditor]] 里用「準標準ボーン追加プラグイン」补。
