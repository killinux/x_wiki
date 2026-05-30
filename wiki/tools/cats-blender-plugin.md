---
title: Cats Blender Plugin
type: tool
status: stub
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# Cats Blender Plugin

辅助清理/优化模型的 Blender 插件,常见于 MMD / VRChat 改模流程。典型用途:模型修复、合并骨骼并转移权重、合并材质、生成/简化等。

与 [[mmd_tools]] 配合:Cats 做清理优化,mmd_tools 做 MMD 数据与导出。

## 在 XPS → MMD 流程中的作用

Cats 在 XPS 转换流程中非常有用:
- **Fix Model** — 自动识别 XPS 骨骼名并重命名为 MMD 标准日文名(不保证 100% 正确,需人工检查)
- **Join Meshes** — 合并过于碎片化的 mesh(XPS 模型常见)
- **合并骨骼 + 转移权重** — 简化多余骨骼(如游戏模型的辅助骨)
- **支持 XPS 导入** — 内部集成或调用 [[xps-tools-blender]]

详见 [[xps-to-mmd-流程]] 的骨骼处理步骤。

> stub:本页待 `ingest` 校正——确认当前维护状态、对应 Blender 版本、与 MMD(而非仅 VRChat)流程的具体配合点。
