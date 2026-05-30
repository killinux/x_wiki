---
title: XPS → MMD 材质差异与转换
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-30
---

# XPS → MMD 材质差异与转换

XPS 和 MMD 的材质/渲染体系差异很大。XPS 偏向现代 PBR 风格,MMD 使用独特的 Toon 渲染。转换时需要理解两者差异并做取舍。

## XPS 材质体系

XPS 使用 **Render Group** 编号来定义材质如何渲染。每个 mesh 关联一组贴图,render group 编号决定这些贴图的用途:

| 贴图槽位 | 常见用途 |
|---|---|
| 第1张 | Diffuse(漫反射/主贴图) |
| 第2张 | Lightmap / AO(光照图/环境遮蔽) |
| 第3张 | Bump / Normal map(法线贴图) |
| 第4张 | Specular / Mask(高光/遮罩) |
| 第5张+ | 环境贴图、Emission 等 |

不同 render group 编号对应不同的 shader 行为(透明、双面、发光等)。

## MMD 材质体系

MMD/PMX 的材质系统(详见 [[材质-materials]]):

- **Diffuse + Ambient + Specular** — 基本颜色参数
- **Toon 贴图** — 10 张预设 toon 纹理(toon01.bmp ~ toon10.bmp)控制明暗过渡
- **Sphere 贴图(SPH/SPA)** — 球形环境映射,用于金属感/光泽
- **描边(Edge)** — 轮廓线,可调颜色和粗细
- **透明度** — Alpha 通道

## 转换对照

| XPS 侧 | MMD 侧 | 转换策略 |
|---|---|---|
| Diffuse 贴图 | Tex(纹理贴图) | **直接使用**,通常无需修改 |
| Normal map | — | **丢弃**或烘焙进 diffuse。MMD 标准不支持法线贴图(部分 MME 效果文件可以,但不通用) |
| Specular map | Sphere(SPH) | 可尝试转为球形环境贴图,但效果差异大;多数情况**不转** |
| Lightmap / AO | — | **丢弃**或手动烘焙进 diffuse |
| 透明材质 | Alpha 通道 | 需要在 PMX 中正确设置透明标志与绘制顺序 |
| 双面渲染 | 双面标志 | 在 PMX 材质中勾选「両面描画」 |

## 实际操作要点

1. **最重要的是 Diffuse** — 只要 Diffuse 贴图正确,MMD 里看起来就不会太差。
2. **Toon 选择** — 根据角色风格选择合适的 Toon 贴图编号。皮肤常用 toon02,衣服用 toon01 或 toon03。待补充:各 toon 效果对照。
3. **SPH/SPA 的使用** — 可选。给头发加 SPA 能增加光泽感,金属/皮革部件加 SPH 增加质感,但需要自己制作或找合适的球形贴图。
4. **描边** — 一般全部材质开启描边(边缘线),透明部件(睫毛、头发边缘)可关闭或减细。
5. **贴图路径** — XPS 的贴图路径可能含中文/日文/特殊字符,导入 Blender 后需检查路径是否正确,导出 PMX 时确保贴图在模型同目录下。

## 进阶:通过 MME 保留更多细节

如果目标用户使用支持 MikuMikuEffect(MME)的环境,可以:
- 编写自定义 effect 文件(.fx)支持法线贴图
- 使用 Ray-MMD 等高级渲染方案,支持 PBR 流程

但这超出了标准 PMX 的范围,不是所有 MMD 用户都能使用。

## 相关页面

- [[材质-materials]] — MMD 材质系统详解
- [[xps-format]] — XPS 格式与 render group
- [[xps-to-mmd-流程]] — 完整转换流程
