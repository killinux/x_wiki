---
title: XPS Tools for Blender (导入插件)
type: tool
status: stable
sources:
  - https://github.com/johnzero7/XNALaraMesh
  - https://github.com/johnzero7/XNALaraMesh/releases/tag/v2.0.2
  - https://github.com/mayloglog/XNALaraMesh-blender4.4
  - https://github.com/Mysteryem/XNALaraMesh
  - https://extensions.blender.org/add-ons/io-xnalara/
updated: 2026-05-30
---

# XPS Tools for Blender

在 Blender 中导入 XPS/XNALara 模型的插件。是「XPS → Blender → MMD」流程的第一步。

## 基本信息

| 项目 | 内容 |
|---|---|
| 名称 | XPS Tools / XNALara Import-Export(`Import-Export: XNALara/XPS`) |
| 作者 | johnzero7 |
| 仓库 | GitHub: **johnzero7/XNALaraMesh**(原仓) |
| 支持格式 | `.xps`、`.mesh`、`.mesh.ascii`、`.ascii`、姿势文件 |

## 版本与 Blender 兼容性 (核实于 2026-05-30)

| 版本 / 分支 | 适用 Blender | 说明 |
|---|---|---|
| **v2.0.2**(johnzero7,2020) | **2.80 ~ 2.83** | 原作最后发布;v2.0.0 起仅支持 2.80+ |
| v1.8.7(johnzero7) | 2.79 | 旧 Blender 专用 |
| **mayloglog/XNALaraMesh-blender4.4** | **4.4 / 5.0** | 社区 fork,v2.1.0→4.4、v2.2.0→5.0 |
| Mysteryem/XNALaraMesh | 较新 Blender | 另一活跃 fork |
| extensions.blender.org 的 io-xnalara | 见该页 | 上架 Blender 官方扩展站的版本 |

> ⚠️ **原作已约 5 年未更新**(截至 2025):johnzero7 原仓 v2.0.2 装在新 Blender(3.x/4.x/5.x)上**会报错或不可用**。新 Blender 请用 **mayloglog / Mysteryem 的 fork** 或官方扩展站版本。(来源: johnzero7/XNALaraMesh releases;mayloglog fork README)

## 安装

1. 从对应仓库下载 zip(按你的 Blender 版本选 fork)
2. Blender → Edit → Preferences → Add-ons → Install → 选 zip
3. 启用 `Import-Export: XNALara/XPS`
4. 在 File → Import 中出现 `XNALara/XPS` 选项
5. Blender 4.2+ 也可经 Edit → Preferences → Get Extensions 装上架版本

## 导入选项

导入时的关键选项:

- **Import Armature** — 是否导入骨骼。转 MMD 必须开启。
- **Bone length** — 骨骼显示长度,不影响功能。
- **Connect bones** — 是否自动连接父子骨骼(影响 roll/层级观感,见 [[坐标系-朝向-pose]])。
- **Import textures** — 贴图导入。确保贴图文件在模型同目录下。

## 导入后的常见状态

成功导入后,Blender 场景中会有:
- 一个 **Armature** 对象(骨架),骨骼名为英文(来自 XPS 原始数据)
- 若干 **Mesh** 对象,每个对应 XPS 的一个 render group
- 材质节点中引用了贴图文件

### 需要注意的问题

1. **缩放** — XPS 模型经常尺寸偏大或偏小(游戏引擎单位不同),需在导入后统一缩放,Apply Scale 后再继续。
2. **骨骼方向 / roll** — XPS 骨骼轴向与 Blender 约定不同,pose 模式旋转方向不直觉;见 [[坐标系-朝向-pose]]。
3. **贴图路径** — 含特殊字符或路径过长可能加载失败,手动在 Shader Editor 修正;见 [[uv-贴图打包]]。
4. **法线方向** — 部分 mesh 法线可能翻转,Recalculate Normals。

## 替代方案

- 新 Blender 用 **mayloglog / Mysteryem fork**(见上版本表)。
- [[cats-blender-plugin]] 也涉及 XPS 导入/清理流程。

## 相关页面

- [[xps-format]] — XPS 格式详解
- [[xps-to-mmd-流程]] — 导入后的完整转换流程
- [[cats-blender-plugin]] — 清理工具
- [[坐标系-朝向-pose]] · [[uv-贴图打包]] · [[mmd_tools]]
