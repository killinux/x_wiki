---
title: VPD 姿势格式 / Vocaloid Pose Data
type: concept
status: stable
sources:
  - https://mikumikudance.fandom.com/wiki/MMD:Vocaloid_Pose_Data
  - https://noname0310.github.io/babylon-mmd/docs/reference/understanding-mmd-behaviour/introduction-to-vmd-and-vpd/
  - https://learnmmd.com/http:/learnmmd.com/vpd-pose-files-help-you-demo-new-mmd-models/
updated: 2026-05-30
---

# VPD 姿势格式(Vocaloid Pose Data)

`.vpd` 是 MMD 的**单帧姿势**数据:加载后把模型骨骼摆成某个固定姿势。与 [[vmd-动作格式|VMD]] 的区别——VMD 是多帧动画,VPD 只是**一个静止 pose**。

## 用途
- **展示新模型**:摆个好看的招牌 pose 截图。
- **绑定/改模时验证**:套一个标准 pose 检查变形、穿模(类似 PMXEditor 的 TransformView)。
- **存储姿势库**:把常用手势/站姿存成 vpd 复用。

## 格式特征
- **文本格式**(不像 VMD/PMX 是二进制),可用文本编辑器查看。
- 头部声明骨骼条目数 + 目标模型名;随后每个骨骼一段:**骨骼名 + 位置(3 值)+ 旋转(四元数 4 值)**。
- 只存「骨骼名 + 状态」,和 VMD 一样**按骨骼名匹配**(见 [[骨骼-bones]];全角半角需一致)。
- 较新约定也能存表情(morph)状态。
(来源: fandom Vocaloid_Pose_Data;babylon-mmd VMD/VPD)

## 与 Blender
- [[mmd_tools]] 支持导入/导出 VPD,把 pose 套到 Blender 骨骼上。
- 也可在 [[pmxeditor]] 里加载 vpd 摆 pose 检查。

## 相关页面
- [[vmd-动作格式]] — 多帧动作(对比)
- [[骨骼-bones]] · [[mmd_tools]] · [[pmxeditor]]
