---
title: MME / MikuMikuEffect 与特效(Ray-MMD 等)
type: tool
status: draft
sources:
  - https://learnmmd.com/
  - https://github.com/ray-cast/ray-mmd
updated: 2026-05-30
---

# MME / MikuMikuEffect 与特效

**MMEffect(MME)** 是给 MMD 加 shader 特效的插件,用 `.fx`(HLSL effect)文件实现辉光、景深、PBR 渲染等。它是「让画面好看」的关键一层,但**不属于模型数据**——是场景/渲染时的东西。

## 安装 MME
- 把 MMEffect 文件(`d3d9.dll` 等)放到 `MikuMikuDance.exe` 同目录。
- 启动后右上角出现 **MMEffect** 按钮。
- 在 MME 面板把 `.fx` 指派给材质/模型。

## 常见特效

| 特效 | 作用 |
|---|---|
| **AutoLuminous** | 让自发光材质发光/泛光(霓虹、眼睛高光) |
| **Ray-MMD** | 完整 PBR / 延迟渲染,真实感大幅提升;GitHub 免费、吃显卡 |
| PowerDOF | 景深 |
| diffusion / o_Bloom | 柔光辉光 |
| ikBokeh / SvSSAO | 散景 / 环境光遮蔽 |
(来源: learnmmd;ray-cast/ray-mmd)

## 与模型/材质的关系(重要)
- 特效**不写进 PMX**:标准 PMX 不携带 effect 数据。你分发模型时,对方需自己有同样的特效才能复现画面。
- **Ray-MMD 需要材质配好贴图**:它能利用法线/specular 等 PBR 贴图——这一点对 [[xps-材质差异|XPS 转换]]有意义:XPS 自带的 `_N`(法线)/`_s`(specular)在标准 MMD 里没用,但**在 Ray-MMD 下能派上用场**。所以如果目标是 Ray-MMD 渲染,转换时**别急着删法线贴图**。
- 这是标准 PMX Toon 渲染([[材质-materials]])之外的「进阶渲染路线」。

## 与 Blender 的关系
- 特效是 MMD 本体侧的事,和 Blender 建模不直接相关。
- 但若你在 Blender 端就想要 PBR 外观,也可考虑直接在 Blender 渲染(不进 MMD),取舍见各自工作流。

## 相关页面
- [[mmd本体-使用]] — 在哪里加载特效
- [[材质-materials]] · [[xps-材质差异]] — 标准 Toon vs PBR 贴图
- [[toon-贴图对照]] — 标准渲染的 toon
