---
title: XPS Tools for Blender (导入插件)
type: tool
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-30
---

# XPS Tools for Blender

在 Blender 中导入 XPS/XNALara 模型的插件。是「XPS → Blender → MMD」流程的第一步。

## 基本信息

| 项目 | 内容 |
|---|---|
| 名称 | XPS Tools / XNALara Import-Export |
| 作者 | johnzero7 |
| 仓库 | GitHub: johnzero7/XNALaraMesh(待确认最新 fork） |
| 支持格式 | `.xps`、`.mesh`、`.mesh.ascii`、`.ascii` |
| Blender 版本 | 待补充:各版本兼容性 |

> **版本敏感**:Blender 2.8x → 3.x → 4.x API 变动大,需确认使用的 fork 版本是否兼容当前 Blender。

## 安装

1. 从 GitHub 下载 zip(或 clone)
2. Blender → Edit → Preferences → Add-ons → Install → 选 zip
3. 启用 `Import-Export: XNALara/XPS`
4. 在 File → Import 中出现 `XNALara/XPS` 选项

## 导入选项

导入时的关键选项(待补充具体面板截图/说明):

- **Import Armature** — 是否导入骨骼。转 MMD 必须开启。
- **Bone length** — 骨骼显示长度,不影响功能。
- **Connect bones** — 是否自动连接父子骨骼。
- **Auto IK** — 自动添加 IK?待确认。
- **Import textures** — 贴图导入。确保贴图文件在模型同目录下。

## 导入后的常见状态

成功导入后,Blender 场景中会有:
- 一个 **Armature** 对象(骨架),骨骼名为英文(来自 XPS 原始数据)
- 若干 **Mesh** 对象,每个对应 XPS 的一个 render group
- 材质节点中引用了贴图文件

### 需要注意的问题

1. **缩放** — XPS 模型经常尺寸偏大或偏小(游戏引擎单位不同),需要在导入后统一缩放。建议: Apply Scale 后再进行后续操作。
2. **骨骼方向** — XPS 骨骼可能和 Blender 的轴向约定不同,导致 pose 模式下旋转方向不直觉。
3. **贴图路径** — 如果贴图文件名含特殊字符或路径过长,可能加载失败。手动在 Shader Editor 中修正。
4. **法线方向** — 部分 mesh 法线可能翻转,需要在 Blender 中 Recalculate Normals。

## 替代方案

- 有些社区 fork 针对 Blender 4.x 做了适配,待补充具体链接。
- [[cats-blender-plugin]] 也支持导入 XPS(内部调用 XPS Tools 或自带转换逻辑),且提供后续的自动清理功能。

## 相关页面

- [[xps-format]] — XPS 格式详解
- [[xps-to-mmd-流程]] — 导入后的完整转换流程
- [[cats-blender-plugin]] — 自动清理工具
- [[mmd_tools]] — MMD 导出插件
