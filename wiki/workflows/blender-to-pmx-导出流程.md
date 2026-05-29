---
title: Blender → PMX 端到端流程
type: workflow
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# Blender → PMX 建模导出流程

一个从零做 / 改一个 MMD 模型到可在 MMD 本体使用的典型路线。具体面板操作以 [[mmd_tools]] 实际版本为准。

## 1. 准备
- 安装对应 Blender 版本的 [[mmd_tools]];可选 [[cats-blender-plugin]]。
- 若是改模:先用 mmd_tools 导入已有 `.pmx`,保留其 MMD Model 根层级。

## 2. 建模 / 改模
- 几何体、拓扑(变形处布线要利于弯曲)。
- UV 展开。

## 3. 材质与贴图
- 设贴图、Toon、Sphere(SPH/SPA)、边缘描边。
- 细节见 [[材质-materials]]。

## 4. 骨骼
- 建 / 对齐 Armature,**骨骼名对齐 MMD 半标准日文名**(见 [[骨骼-bones]])。
- 配置 IK、付与。

## 5. 权重
- Weight Paint;Vertex Group 名 = 骨骼名。
- 摆 pose 测试变形;扭转处考虑 SDEF。详见 [[权重-weights]]。

## 6. 表情
- 用 Shape Keys 做顶点 morph,按 眉/目/口/その他 归类。
- 对口型五元音 `あいうえお` 做齐。详见 [[表情-morphs]]。

## 7. 物理
- 刚体 + 关节(头发、裙摆、饰品)。
- 设非碰撞组防穿模。详见 [[物理-physics]]。

## 8. 导出 PMX
- 用 mmd_tools 导出 `.pmx`。
- 检查贴图路径 / 编码。

## 9. 精修与验证(PMXEditor)
- 在 [[pmxeditor]] 里修权重(SDEF)、物理细调、显示枠整理。
- **在 MMD 本体里加载标准动作 + 标准 pose 验证**:对口型、穿模、关节变形、物理甩动。

## 验收检查点
- [ ] 骨骼名匹配,标准 VMD 能驱动
- [ ] 权重在极限 pose 下不塌陷
- [ ] 五元音 + 眨眼 morph 正常
- [ ] 物理不爆炸、不穿模
- [ ] 材质 Toon/Sphere/描边在 MMD 本体里正确

> 待补充:每步的具体面板按钮与快捷键——ingest 你跟的教程后逐步细化。
