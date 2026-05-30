---
title: UV / 贴图打包(XPS→MMD)
type: concept
status: stable
sources:
  - 种子内容/通用领域知识
  - 实测 ~/Reika18_Children.pmx → [[标准骨架范本-reika]]
updated: 2026-05-30
---

# UV / 贴图打包(XPS→MMD)

XPS rip 模型通常**一个部件一个 mesh、各自一张贴图**(范本实测:32 材质 / 34 贴图)。转 MMD 时要处理 UV 与贴图的组织,既影响外观也影响性能与分发。

## XPS 模型的 UV 现状

- **每 mesh 独立 UV**:XPS 的每个 render group(→ Blender 里一个 mesh)有自己的 UV,占满 0–1 空间。导入后 UV 通常**完好可用**(diffuse 直接显示对)。
- **多层 UV**:XPS 顶点可带多层 UV(范本有附加 UV ×1)。MMD 主要用第 1 层;附加 UV 仅在 UV morph / 特定材质用,见 [[pmx-format]]。
- 结论:**一般不需要重新展 UV**,diffuse 能正确贴上就别动。

## 何时要动 UV

| 情况 | 处理 |
|---|---|
| 合并 mesh 但**各自贴图不同** | UV 不变,但要么保留多材质,要么做 UV 重排 + 贴图合并(图集) |
| 想减少材质/贴图数(性能、分发) | 把多张小贴图打包成**图集(atlas)**,同步重排 UV |
| 贴图有重叠 UV(镜像件) | 镜像部件常共用 UV;合并时注意别破坏 |
| 加 SPH/SPA 球面贴图 | 球面贴图用**屏幕/球面映射**,不吃模型 UV,无需改 UV |

## 合并 mesh 与材质槽

- Blender 里 `Ctrl+J` 合并对象后,各原 mesh 的材质变成**多个材质槽**,UV 各自保留 → **外观不变**(推荐的安全做法)。
- 只有当你想把多材质**并成一个**时,才需要真正重排 UV + 合并贴图。
- [[cats-blender-plugin]] 的 Join Meshes / Atlas 功能可半自动做图集打包(VRChat 流程常用);MMD 用途下**非必需**——MMD 对材质数量不像 VRChat 那么敏感。

## 贴图打包(atlas)取舍

- **好处**:材质/Draw call 更少、分发文件更整齐。
- **代价**:重排 UV 有风险(接缝、精度损失);MMD 里多材质本身不是大问题。
- 建议:**MMD 模型一般不必强行做图集**;除非材质数量极多影响加载。优先保证 diffuse 正确、材质有序。

## 贴图文件管理(实测痛点)

范本贴图名暴露了 XPS 来源的典型问题(见 [[材质-materials]] 实测):

- **子目录前缀**:部分贴图路径带 `textures\...`(Windows 反斜杠)。导出 PMX 后要确认路径对、最好**拍平到 PMX 同目录**并改相对路径。
- **特殊字符 / 空格**:XPS 贴图名常含空格、`_AO`、大小写混杂(`Tifa Head D_AO.jpg`),跨系统易丢失。必要时**重命名为简单 ASCII**。
- **冗余贴图**:`_N`(法线)、`_AO`、`_s`(specular)MMD 用不到,**删掉引用**减小体积。
- **格式**:jpg/png 都行;MMD 也支持 bmp/tga/dds。透明用带 alpha 的 png。

> 导出时勾 mmd_tools 的 **Copy Textures**,把用到的贴图复制到导出目录,避免绝对路径。见 [[xps-to-mmd-流程]] ⑨ 与 [[导出前qa清单]]。

## 相关页面
- [[材质-materials]] · [[xps-材质差异]] — 贴图与材质实测
- [[pmx-format]] — 附加 UV / UV morph 的格式
- [[cats-blender-plugin]] — Join/Atlas 工具
- [[xps-to-mmd-流程]] · [[导出前qa清单]]
