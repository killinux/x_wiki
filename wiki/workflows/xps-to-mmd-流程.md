---
title: XPS → Blender → MMD 端到端转换流程
type: workflow
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-30
---

# XPS → Blender → MMD 端到端转换流程

将 XPS/XNALara 游戏 rip 模型转换为 MMD(PMX)可用模型的完整流程。

> **前提**:安装好 [[xps-tools-blender]]、[[cats-blender-plugin]]（可选但强烈推荐）、[[mmd_tools]]。

---

## 流程总览

```
XPS 模型文件(.xps/.mesh)
  │
  ▼ ① 导入 Blender
  │
  ▼ ② 初步清理(缩放、法线、合并)
  │
  ▼ ③ 骨骼处理(重命名、补缺、建 IK)
  │
  ▼ ④ 权重检查与修复
  │
  ▼ ⑤ 材质适配(Toon/Sphere/描边)
  │
  ▼ ⑥ 添加表情(Morph)
  │
  ▼ ⑦ 添加物理(刚体 + 关节)
  │
  ▼ ⑧ 设置显示枠
  │
  ▼ ⑨ 导出 PMX
  │
  ▼ ⑩ PMXEditor 精修 + 测试
```

---

## ① 导入 XPS

1. File → Import → XNALara/XPS
2. 选择 `.xps` 或 `.mesh` 文件
3. 确保勾选 Import Armature
4. 导入后检查:模型是否完整、贴图是否加载

详见 [[xps-tools-blender]]。

## ② 初步清理

### 缩放
- XPS 模型通常尺寸不对。MMD 标准身高约 20 个 Blender 单位(1 单位 ≈ 8cm)。
- 缩放后 **Ctrl+A → Apply Scale**,否则后续物理和导出会出问题。

### 法线
- Edit Mode → Mesh → Normals → Recalculate Outside
- 检查有无翻转的面(Viewport Overlays → Face Orientation,蓝色=正面,红色=反面)

### 网格合并(可选)
- 如果 mesh 过于碎片化(XPS 经常每个部件一个 mesh),可根据材质分组合并。
- Cats 插件的 Join Meshes 功能可以快速处理。
- **注意**:合并前确保各 mesh 的 UV 和权重正确。

### 清理顶点
- 移除重叠顶点:Edit Mode → Merge by Distance(阈值 0.0001 左右)
- 删除松散顶点/边

## ③ 骨骼处理

这是工作量最大的一步。详见 [[xps-骨骼映射]]。

### 方案 A:使用 Cats 自动修复
1. 选中 Armature
2. Cats 面板 → Fix Model
3. Cats 会尝试自动识别并重命名骨骼为 MMD 标准名
4. **必须人工检查**:打开骨骼列表,确认关键骨骼是否正确映射

### 方案 B:手动处理
1. 进入 Armature Edit Mode
2. 逐个重命名骨骼(参照 [[xps-骨骼映射]] 的对照表)
3. 添加缺失骨骼:
   - 全ての親(root)
   - センター(center)
   - グルーブ(groove,可选)
4. 调整骨骼层级(parent 关系)

### 建立 IK
- 使用 mmd_tools 或手动添加:
  - 左足ＩＫ / 右足ＩＫ — 控制脚的位置
  - 左つま先ＩＫ / 右つま先ＩＫ — 控制脚尖
- IK 链长度:足ＩＫ 通常链长 2(膝→踝)

### 手指骨骼
- 如果 XPS 模型有手指骨骼,重命名为 MMD 标准名(左親指0/1/2 等)
- 如果没有手指骨骼,需要手动添加并刷权重,或者放弃手指动作

## ④ 权重检查与修复

详见 [[权重-weights]]。

- 检查每个骨骼的权重涂抹是否合理(Weight Paint 模式)
- XPS 权重通常质量不错(来自游戏引擎),但合并/添加骨骼后可能需要修正
- 确保新添加的骨骼(center、IK 等)有正确的权重(或者不需要权重——IK 骨是纯控制骨)
- 检查对称性:如果需要,可以 Mirror Weights

## ⑤ 材质适配

详见 [[xps-材质差异]]。

1. 确保 Diffuse 贴图正确加载
2. 在 mmd_tools 的材质面板中设置:
   - Toon 贴图编号
   - Sphere 贴图(可选)
   - 描边开关与粗细
   - 透明度(Alpha)
3. 丢弃 XPS 的法线贴图、specular 贴图(标准 MMD 不支持)
4. 调整材质绘制顺序(透明材质放后面)

## ⑥ 添加表情(Morph)

XPS 模型通常**没有表情数据**,需要手动制作或放弃。

常见的基本表情:
- 眨眼(まばたき)— 顶点 morph,闭合上眼皮
- 笑眼(笑い)
- 口型(あ、い、う、え、お)— A/I/U/E/O

制作方式:
1. Blender Shape Keys — 在 Basis 基础上雕刻变形
2. 导出时 mmd_tools 会将 Shape Keys 转为 PMX 的顶点 morph

> 如果只是做静态展示或简单动作,可以暂时跳过表情。

## ⑦ 添加物理

详见 [[物理-physics]]。

XPS 模型没有物理数据,需要手动添加刚体(rigid body)和关节(joint):

- **头发** — 多段刚体链 + 关节,实现飘动效果
- **裙子/衣摆** — 类似头发,但通常需要更多段
- **胸部** — 可选,2 个刚体 + 关节
- **饰品(丝带、耳环等)** — 按需添加

> 物理是最耗时的部分之一。初期可以先跳过,后续用 PMXEditor 精调。

## ⑧ 设置显示枠

显示枠(表示枠)是 MMD 界面中骨骼的分组显示。使用 mmd_tools 的面板设置:

- Root — 全ての親、センター
- 表情 — 所有 morph
- IK — 足 IK、つま先 IK
- 体(上) — 上半身、首、頭、肩、腕、ひじ、手首
- 体(下) — 下半身、足、ひざ、足首
- 指 — 手指骨骼
- その他 — 其余骨骼

## ⑨ 导出 PMX

1. File → Export → MikuMikuDance Model (.pmx)（mmd_tools 提供）
2. 导出选项:
   - Scale:确认比例正确
   - Copy textures:建议开启,将贴图复制到导出目录
3. 检查导出文件大小是否合理

详见 [[blender-to-pmx-导出流程]]。

## ⑩ PMXEditor 精修 + 测试

详见 [[pmxeditor]]。

1. 用 PMXEditor 打开导出的 PMX
2. TransformView 摆 pose 检查:
   - 骨骼变形是否正常
   - 权重有无穿模
   - IK 是否工作
3. 在 MMD 中加载一个标准动作(.vmd)测试:
   - 动作是否正确映射到各骨骼
   - 物理是否自然
   - 有无严重穿模

## 时间预估

| 步骤 | 简单模型 | 复杂模型 |
|---|---|---|
| 导入+清理 | 15 min | 30 min |
| 骨骼处理 | 30 min | 2-4 h |
| 权重修复 | 15 min | 1-2 h |
| 材质适配 | 15 min | 30 min |
| 表情 | 跳过 | 2-4 h |
| 物理 | 跳过 | 4-8 h |
| 显示枠+导出 | 15 min | 30 min |
| 精修+测试 | 30 min | 1-2 h |
| **合计** | **~2 h** | **~12-20 h** |

## 相关页面

- [[xps-format]] — XPS 格式
- [[xps-tools-blender]] — XPS 导入插件
- [[xps-骨骼映射]] — 骨骼名对照
- [[xps-材质差异]] — 材质转换
- [[xps-转换常见问题]] — 常见报错与解决
- [[blender-to-pmx-导出流程]] — Blender 导出 PMX 的通用流程
- [[cats-blender-plugin]] — 自动清理工具
- [[mmd_tools]] — MMD 核心插件
