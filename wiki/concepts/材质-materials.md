---
title: 材质 / 材質 / materials
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# 材质 (材質 / materials)

MMD 材质偏卡通渲染(NPR),与 Blender 的 PBR 思路不同,导出时要做映射。

## PMX 材质的关键要素
- **基础贴图(Texture)**:漫反射贴图。
- **Toon 贴图**:卡通明暗的渐变图(toon01.bmp…toon10.bmp 为共享 toon,或自带 toon)。控制阴影色阶。
- **Sphere 贴图(球面贴图)**,按混合模式分:
  - `SPH`(.sph)— **相乘**,常用于高光/金属感。
  - `SPA`(.spa)— **相加**,常用于发光/反光叠加。
  - `subTexture` — 作为附加 UV 的子贴图。
- **绘制标志**:双面显示、地面阴影、自身阴影、边缘(轮廓线)等。
- **边缘(エッジ / edge)**:轮廓线颜色与粗细 —— MMD 卡通描边。

## 与 Blender 的映射
- Blender 用节点材质(Principled BSDF / Toon 等);[[mmd_tools]] 会维护一份 **MMD Material** 数据,导出 PMX 时以它为准。
- 贴图路径在导出后常需修正(相对路径、编码)。
- Toon / Sphere 在 Blender 视口里不一定所见即所得,**以 MMD 本体或 [[pmxeditor]] 预览为准**。

## 常见坑
- 贴图丢失 / 路径乱码:见 [[troubleshooting]]。
- 透明排序:半透明材质的绘制顺序问题。
- 描边过粗/穿插:edge 参数。

参见 [[pmx-format]]、[[权重-weights]]、[[blender-to-pmx-导出流程]]。

## XPS 材质 → MMD 材质

XPS 使用 render group 编号控制材质行为(支持法线贴图、specular 等现代特性),与 MMD 的 Toon 渲染差异较大。转换时:
- Diffuse 贴图直接沿用
- 法线贴图、specular 贴图需丢弃(标准 MMD 不支持)或烘焙进 diffuse
- 需手动设置 Toon 编号、Sphere 贴图、描边参数

详见 [[xps-材质差异]]。

> 待补充:mmd_tools 材质面板各字段 ↔ PMX 字段的精确对应——ingest 插件文档后补全。
