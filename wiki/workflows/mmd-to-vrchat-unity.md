---
title: MMD → VRChat / Unity 移植
type: workflow
status: stable
sources:
  - https://steamcommunity.com/app/438100/discussions/1/2595630410188916283/
  - https://learnmmd.com/
  - https://github.com/absolute-quantum/cats-blender-plugin
updated: 2026-05-30
---

# MMD(PMX) → VRChat / Unity 移植

把 PMX 模型做成 VRChat 头像或 Unity 用资产,是 MMD 模型的另一大去向。与 [[xps-to-mmd-流程|XPS→MMD]] 方向相反,但用到同一批 Blender 工具。

> ⚠️ **规约**:PMX 模型用于 VRChat/再分发前必须确认原作允许(见 [[素材站与规约-resources]])。

## 总流程
```
PMX → Blender(mmd_tools 导入 + Cats 整理)→ 导出 FBX → Unity(+VRCSDK)→ 上传
```

## 1. 导入 Blender
- 用 [[mmd_tools]] 导入 PMX(保留骨/权重/morph)。
- 用 [[cats-blender-plugin]] 整理:Fix Model、**骨骼名转英文**(Unity Humanoid 需要英文骨名,与 MMD 的日文名相反)。

## 2. 优化(VRChat 有性能预算)
- **减面**:VRChat 头像建议 ≤ 约 2 万面(Cats/Tuxedo 的 Decimate;见 [[cats-blender-plugin]])。
- 合并材质/做图集(见 [[uv-贴图打包]]),减少 material 数。
- 设置 **visemes(口型)**:从 MMD 的 `あいうえお` morph 映射到 VRChat 的 viseme(见 [[口型-lipsync]])。
- 眼追(eye tracking)骨/blendshape。

## 3. 导出 FBX → Unity
- Blender 导出 **FBX**,导入 Unity。
- Rig 设为 **Humanoid**(映射骨骼)。
- 贴图/材质重连(Unity 用自己的 shader,如 lilToon/Poiyomi 还原卡通感)。

## 4. VRChat
- 装 **VRCSDK**,配 Avatar Descriptor、viseme、眼追、碰撞/动骨(PhysBones 替代 MMD 物理)。
- 上传。

## 关键差异(MMD vs VRChat)
| 项 | MMD | VRChat/Unity |
|---|---|---|
| 骨名 | 日文 | 英文(Humanoid) |
| 物理 | 刚体+关节(Bullet) | PhysBones |
| 表情 | morph(日文名) | blendshape + viseme |
| 渲染 | Toon/MME | lilToon/Poiyomi 等 |
| 面数 | 宽松 | 严格预算 |

> 即:MMD 的物理、Toon、日文骨名在 VRChat 都要**换体系**;morph 可复用但要映射 viseme。

## 相关页面
- [[mmd_tools]] · [[cats-blender-plugin]] — 导入/整理
- [[口型-lipsync]] — viseme 来源
- [[uv-贴图打包]] · [[物理-physics]] · [[素材站与规约-resources]]
