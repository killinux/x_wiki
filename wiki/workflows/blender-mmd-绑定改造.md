---
title: Blender 端 MMD 绑定改造(建 IK / 付与 / 显示枠 / 英文名)
type: workflow
status: draft
sources:
  - 种子内容/通用领域知识
  - 实测对照 [[标准骨架范本-reika]]
updated: 2026-05-30
---

# Blender 端 MMD 绑定改造

骨骼**改完名只是第一步**。要让模型「吃得下」VMD 动作,还要在 Blender 端用 [[mmd_tools]] 把 IK、付与、显示枠、英文名等 MMD 专属数据补上。这页接在 [[xps-to-mmd-流程]] ③ 之后。

> 前提:模型已是 MMD Model 层级(Empty→Armature→Mesh),骨名已对齐 [[xps-骨骼映射]],坐标/朝向/roll 已按 [[坐标系-朝向-pose]] 处理干净。

## 1. 转成 mmd_tools 可管理的模型

- 若模型不是 mmd_tools 导入的,用 **MMD Tools → Convert Model**(把普通 Armature 转为 MMD model),之后 Bone/Material/Morph/Rigid/Joint 面板才生效。

## 2. 建 IK(足/つま先)

参照范本实测(见 [[标准骨架范本-reika]]):

| IK 骨 | target | chain | 链长 |
|---|---|---|---|
| 左足ＩＫ/右足ＩＫ | 足首 | [ひざ, 足] | 2 |
| 左つま先ＩＫ/右つま先ＩＫ | つま先 | [足首] | 1 |

- 新建 IK 骨置于脚跟/脚尖位置,parent 接 `足IK親`(足IK親 接 全ての親)。
- 在 mmd_tools 的 **Bone 面板**给 IK 骨设 IK target 与链、loop 次数、单步角度限制。
- ⚠️ MMD 的 IK ≠ Blender 的 IK 约束;**用 mmd_tools 的 MMD-IK 设置**,导出才正确。
- 膝盖要给一个**轻微前弯**作为 IK 解算朝向,否则会反折。

## 3. 设付与(回転/移動付与)

补准标准扭转骨/D 骨/肩 时设置付与(系数取自范本实测):

| 子骨 | 付与源 | 系数 |
|---|---|---|
| 肩C | 肩P | −1.0 |
| 腕捩1/2/3 | 腕捩 | 0.25 / 0.5 / 0.75 |
| 手捩1/2/3 | 手捩 | 0.25 / 0.5 / 0.75 |
| 足D/ひざD/足首D | 足/ひざ/足首 | 1.0 |

- 在 mmd_tools Bone 面板勾 **Additional Transform**,选源骨与影响系数,选回転/移動。
- 详见 [[准标准骨骼-semi-standard-bones]];完整补准标准骨常在 [[pmxeditor]] 用插件做更快。

## 4. 排显示枠(表示枠)

显示枠是 MMD 界面里的骨/表情分组。mmd_tools 的 **Display 面板**编辑。常见分组:

- Root(全ての親・センター)/ 表情(全 morph)/ ＩＫ / 体(上)/ 体(下)/ 指 / 物理 / その他
- 两个**特殊枠**(Root、表情)是固定存在的;MMD 的表情滑块就读「表情」枠里的 morph。
- 不进显示枠的骨在 MMD 里**点不到**(但仍受动作驱动)。

> ⚠️ **实测反例(范本 [[标准骨架范本-reika]])**:这具模型有 263 骨、19 表情,但显示枠**几乎没整理**——只有 3 个枠,「表情」枠**是空的**(19 个 morph 一个都没归入 → 在 MMD 里表情滑块全调不出来!),Root 枠放的是「操作中心」而非全ての親/センター。这就是「XPS 转完未收尾」的典型残缺:**模型能动,但 morph 用不了、骨点不到**。所以这一步**不能省**:至少要把所有 morph 放进「表情」枠、把常用骨按上面分组排好。

## 5. 补骨骼英文名

- mmd_tools 每根骨有「日文名 + 英文名」两栏。VMD 按**日文名**匹配,但英文名利于跨语言编辑、部分工具识别。
- XPS 导入的英文骨名可保留到英文栏,日文栏填 MMD 标准名。

## 6. 自检 → 导出

- Pose 模式逐一旋转 IK / 扭转骨,确认无麻花、无反折(roll 问题见 [[坐标系-朝向-pose]])。
- 导出 PMX 见 [[blender-to-pmx-导出流程]] / [[xps-to-mmd-流程]] ⑨,再进 [[pmxeditor]] 精修。

## 相关页面
- [[xps-to-mmd-流程]] — 总流程(本页是 ③ 的展开)
- [[标准骨架范本-reika]] — IK 链 / 付与系数 / 层级 实测来源
- [[准标准骨骼-semi-standard-bones]] · [[骨骼-bones]]
- [[mmd_tools]] · [[pmxeditor]] · [[坐标系-朝向-pose]]
