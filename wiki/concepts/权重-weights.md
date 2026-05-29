---
title: 权重 / ウェイト / weights & 变形类型
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# 权重与变形类型 (ウェイト / weights)

权重决定每个顶点受哪些骨骼、各占多少,直接决定关节处变形是否自然。

## PMX 顶点变形类型
- **BDEF1**:1 根骨骼,权重 100%(刚性部分,如骨头)。
- **BDEF2**:2 根骨骼线性混合(最常见)。
- **BDEF4**:4 根骨骼混合(复杂区域)。
- **SDEF**:球面变形,改善**手腕/肩等扭转处**的塌陷,效果比 BDEF2 自然(MMD 特有,需正确设置)。
- (PMX 2.1 还有 QDEF,本体支持有限)

## 刷权重要点
- 关节处(肘、膝、腕)做平滑过渡,避免「塌陷/撕裂」。
- 旋转测试:摆 pose 检查变形,而非只看静态。
- 物理骨(头发/裙)末端通常 BDEF1 绑到对应末端骨,再交给 [[物理-physics]]。

## 在 Blender 中
- 用 **Vertex Groups + Weight Paint**;每个 Vertex Group 名要对应骨骼名(见 [[骨骼-bones]])。
- [[mmd_tools]] 导出时把权重转为 PMX 的 BDEF/SDEF。Blender 没有 SDEF 概念,SDEF 通常需在 [[pmxeditor]] 中转换/设置。
- [[cats-blender-plugin]] 有权重相关辅助(如合并骨骼并转移权重)。

参见 [[pmx-format]]、[[blender-to-pmx-导出流程]]。

> 待补充:Blender 权重 → PMX SDEF 的具体转换流程——ingest 后补全。
