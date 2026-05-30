---
title: PMXEditor / PMXエディタ
type: tool
status: stable
sources:
  - https://kkhk22.seesaa.net/category/14045227-1.html  # 官方分发(極北P/kkhk22)
  - https://w.atwiki.jp/vpvpwiki/pages/394.html
  - https://tktk.hateblo.jp/entry/2023/10/05/145115
  - 通用领域知识
updated: 2026-05-30
---

# PMXEditor / PMXエディタ

MMD 生态里编辑 `.pmx` 的专用工具(Windows)。常用于 Blender 导出后的**精修**:
- 权重微调、SDEF 设置(见 [[权重-weights]])
- 物理刚体/关节细调(见 [[物理-physics]])
- 显示枠(显示框)整理、材质顺序、贴图路径修正
- TransformView 摆 pose 验证变形

与 Blender 的分工:Blender 建模 + 绑骨 + 物理大框架 → PMXEditor 收尾精修。完整路线见 [[blender-to-pmx-导出流程]]。

## 版本与获取 (核实于 2026-05-30)

| 项目 | 内容 |
|---|---|
| 作者/分发 | **極北P(kkhk22)**;原 PMD Editor 出自同作者一脉 |
| 官方分发处 | kkhk22 的 Seesaa 博客「とある工房」(同意利用规约后下 zip) |
| 位数 | zip 内含 **`PmxEditor.exe`(32位)** 与 **`PmxEditor_x64.exe`(64位)**;大模型(高顶点/材质)用 x64 版更稳 |
| 依赖 | 需 **.NET Framework** + **Visual C++ 运行库** |
| 语言 | 日文为主,需自行找英文化/汉化补丁 |

(来源: kkhk22 Seesaa「ダウンロード」;vpvpwiki)

## 关键插件:準標準ボーン追加プラグイン

PMXEditor 有社区插件 **準標準ボーン追加プラグイン**(准标准骨添加),在标准骨架上半自动补齐准标准骨:全ての親 / グルーブ / 腰 / 上半身2 / 肩P・肩C / 腕捩 / 手捩 / 親指0 / 操作中心 / 足IK親 / 足先EX / ダミー 等,并自动设好父子与付与关系。这是从 Blender 导出 PMX 后补准标准骨的标准做法。详见 [[准标准骨骼-semi-standard-bones]]。

> 插件一般解压到 PMXEditor 的 `_plugin/User` 目录,在「編集 → プラグイン」菜单调用。(来源: tktk MMD ブログ;MMD swamp)

## 常用精修操作
- **SDEF 设置**:Blender 导出的是 BDEF,腕/肩扭转塌陷处可在此转 SDEF(见 [[权重-weights]])。
- **材质顺序/透明**:调绘制顺序解决半透明穿透(见 [[材质-materials]])。
- **显示枠**:把骨/表情归类到 Root/表情/IK/体/指 等枠(见 [[blender-mmd-绑定改造]])。
- **贴图路径**:改为相对路径,配合模型同目录贴图。

## 相关页面
- [[pmx-format]] · [[准标准骨骼-semi-standard-bones]]
- [[物理-physics]] · [[权重-weights]] · [[材质-materials]]
- [[blender-to-pmx-导出流程]] · [[blender-mmd-绑定改造]]
