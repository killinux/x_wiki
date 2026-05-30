---
title: XPS / XNALara 模型格式
type: concept
status: stable
sources: [种子内容/通用领域知识]
updated: 2026-05-30
---

# XPS / XNALara 模型格式

XNALara（后继 XPS = XNALara POSING Studio）是一款基于 XNA 框架的模型查看/摆 pose 工具,广泛用于游戏模型的 rip & pose 社区。

## 文件格式

| 扩展名 | 说明 |
|---|---|
| `.xps` | 二进制格式,XPS 原生,较新 |
| `.mesh` / `.mesh.ascii` | 旧版 XNALara 格式(二进制 / 文本) |
| `.ascii` | 纯文本,结构与 `.mesh.ascii` 相同,方便手动编辑 |

三种格式存储的信息本质相同,只是编码不同。

## 数据结构概览

一个 XPS 模型包含:

1. **骨骼(Bones)** — 名称 + 父级索引 + 位置。无旋转限制、无 IK 信息。
2. **网格(Meshes)** — 每个 mesh 对应一个渲染组(render group),含:
   - 顶点:位置、法线、UV(可多层)、骨骼索引 + 权重(最多 4 骨)
   - 三角面索引
3. **材质/贴图** — 每个 mesh 绑定一组贴图文件名(diffuse、lightmap、bumpmap、specular、环境等),由 render group 编号决定如何使用。

## 与 PMX 的关键差异

| 维度 | XPS | PMX |
|---|---|---|
| 骨骼命名 | 英文,来自游戏原始数据,无统一规范 | 日文标准名(センター、上半身等) |
| IK / 付与 | 无 | 有,MMD 动作依赖 IK 链 |
| 表情(Morph) | 无 | 有,顶点/骨骼/材质/UV 变形 |
| 物理(刚体/关节) | 无 | 有,头发/裙子等布料模拟 |
| 材质系统 | 基于 render group 编号,支持法线/specular | Toon 渲染 + Sphere(SPH/SPA)+ 描边 |
| 显示枠 | 无 | 有,用于 MMD 界面中的骨骼分组 |

> **核心结论**:XPS 只有「静态模型 + 骨骼 + 权重 + 贴图」,转为 MMD 需要**大量补全**:骨骼重命名/重建 IK、添加表情、添加物理、材质适配。见 [[xps-to-mmd-流程]]。

## 相关页面

- [[xps-tools-blender]] — Blender 导入 XPS 的插件
- [[xps-骨骼映射]] — 骨骼名对照与映射
- [[xps-材质差异]] — 材质系统差异与转换
- [[pmx-format]] — PMX 格式对比
