---
title: PMXEditor
type: tool
status: draft
sources:
  - 种子内容/通用领域知识
  - https://sites.google.com/view/mmd-swamp/
  - https://tktk.hateblo.jp/entry/2023/10/05/145115
updated: 2026-05-30
---

# PMXEditor

MMD 生态里编辑 `.pmx` 的专用工具(Windows)。常用于 Blender 导出后的**精修**:
- 权重微调、SDEF 设置(见 [[权重-weights]])
- 物理刚体/关节细调(见 [[物理-physics]])
- 显示枠(显示框)整理、材质顺序、贴图路径修正
- TransformView 摆 pose 验证变形

与 Blender 的分工:Blender 建模 + 绑骨 + 物理大框架 → PMXEditor 收尾精修。完整路线见 [[blender-to-pmx-导出流程]]。

## 关键插件:準標準ボーン追加プラグイン

PMXEditor 生态有一个广泛使用的社区插件 **準標準ボーン追加プラグイン**(准标准骨添加),能在已有标准骨架上**半自动补齐准标准骨**:全ての親 / グルーブ / 腰 / 上半身2 / 肩P・肩C / 腕捩 / 手捩 / 親指0 / 操作中心 / 足IK親 / 足先EX / 手持ちアクセサリ(ダミー)等,并自动设好父子与付与关系。这是从 Blender 导出 PMX 后补准标准骨的标准做法。(来源: MMD swamp;tktk MMD ブログ 2023-10-05)

详见 [[准标准骨骼-semi-standard-bones]]。

> 待补充:PMXEditor 版本、获取方式(本体多为日文社区分发)、与 64 位 (x64) 版本差异;插件具体安装路径。

## 相关页面
- [[pmx-format]]
- [[准标准骨骼-semi-standard-bones]]
- [[物理-physics]]
- [[权重-weights]]
- [[blender-to-pmx-导出流程]]
