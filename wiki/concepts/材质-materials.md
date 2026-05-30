---
title: 材质 / 材質 / materials
type: concept
status: stable
sources:
  - 通用领域知识
  - https://gist.github.com/felixjones/f8a06bd48f9da9a4539f  # 材质 flag / sphere mode / toon
  - 实测 [[标准骨架范本-reika]]
updated: 2026-05-30
---

# 材质 (材質 / materials)

MMD 材质偏卡通渲染(NPR),与 Blender 的 PBR 思路不同,导出时要做映射。

## PMX 材质的关键要素
- **基础贴图(Texture)**:漫反射贴图。
- **Toon 贴图**:卡通明暗的渐变图(toon01.bmp…toon10.bmp 为共享 toon,或自带 toon)。控制阴影色阶。各编号特征见 [[toon-贴图对照]]。
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
- 贴图丢失 / 路径乱码:见 [[xps-转换常见问题]]。
- 透明排序:半透明材质的绘制顺序问题。
- 描边过粗/穿插:edge 参数。

参见 [[pmx-format]]、[[权重-weights]]、[[blender-to-pmx-导出流程]]。

## XPS 材质 → MMD 材质

XPS 使用 render group 编号控制材质行为(支持法线贴图、specular 等现代特性),与 MMD 的 Toon 渲染差异较大。转换时:
- Diffuse 贴图直接沿用
- 法线贴图、specular 贴图需丢弃(标准 MMD 不支持)或烘焙进 diffuse
- 需手动设置 Toon 编号、Sphere 贴图、描边参数

详见 [[xps-材质差异]]。

## 实测:一具「XPS 转过来的」模型材质长什么样(范本 [[标准骨架范本-reika]])

解析范本(32 材质 / 34 贴图)——它本身就是**从 XPS rip 转来的**(贴图名是 `Suit_1-02_Base_Color.jpg`、`Legs_D.jpg`、`Arms_N.jpg`、`Tifa_Hair_D.png`、`*_AO.jpg`、`*_Normal_OpenGL.jpg`),正好示范「**转完但没做 MMD 化润色**」的真实状态:

| 维度 | 实测值 | 说明 |
|---|---|---|
| Sphere(SPH/SPA) | **0 / 32(全无)** | 完全没用球面贴图 |
| Toon | **32 / 32 全用共享 toon01** | 没分肤质/发质,统一最朴素的 toon |
| 描边(エッジ) | **0 / 32(全关)** | ⚠️ 一个都没开描边 |
| 両面描画 | 31 / 32 | XPS rip 常见(原模型多双面) |
| 自身阴影 | 20 / 32 | |
| 半透明(diffuse α<1) | 0 | 透明靠贴图 alpha,不靠材质 α |
| 贴图 | 34 张,29 jpg/5 png,**13 张法线 `_N`/`_Normal`、3 张 `_AO`** | 法线/AO 是 XPS/PBR 残留,MMD 用不到 |

> **这正是一个反面教材 + 真实基线**:它能在 MMD 里显示(diffuse 对、両面开),但**没描边、没 sphere、toon 全 01** —— 看起来「平」、缺 MMD 那种卡通味。要让它更像 MMD 模型,典型润色就是:**给材质开描边、皮肤/头发挑合适 toon(或 SPH)、删掉用不到的 `_N`/`_AO` 贴图引用**。
>
> 也说明:[[mmd_tools]] / [[xps-tools-blender]] 自动转过来的材质**只保证「能显示」,不保证「像 MMD」**,卡通化是手工活。

## XPS→MMD 材质润色清单(从上面归纳)
- [ ] 给主要材质**开描边**(エッジ),透明件(眼/睫)再单独关
- [ ] Toon:皮肤换 toon02、脸按需 toon07(无影)、衣服/头发 toon01,或上自定义 toon(见 [[toon-贴图对照]])
- [ ] 按需给皮肤/头发加 SPH、眼睛加 SPA
- [ ] 清掉 `_N`(法线)、`_AO`、`_s`(specular)等 MMD 不吃的贴图引用
- [ ] 确认两面需求(XPS 默认全両面,实心部件可关以省面/避免内壁穿透)

> PMX 材质各字段(diffuse/specular/ambient、sphere mode 0–3、toon 引用、绘制标志位 両面/描边/阴影)的二进制定义见 [[pmx-format]] 的「材质字段」一节;mmd_tools 面板里对应的就是这些字段(面板用语随插件版本略有差异,以本机版本为准)。
