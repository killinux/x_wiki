---
title: XPS → MMD 骨骼映射
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-30
---

# XPS → MMD 骨骼映射

XPS 模型的骨骼名来自游戏原始数据,没有统一规范;MMD 则要求一套**固定的日文标准骨骼名**才能正确加载动作(.vmd)。转换的核心工作之一就是骨骼映射。

## MMD 标准骨骼(必须存在)

以下骨骼是加载通用 VMD 动作的最低要求:

| 日文名 | 英文 | 说明 |
|---|---|---|
| 全ての親 | master / root | 根骨骼,控制整体移动 |
| センター | center | 重心,VMD 大量使用 |
| グルーブ | groove | 可选,部分动作使用 |
| 上半身 | upper body | 上半身旋转 |
| 上半身2 | upper body 2 | 胸部区域 |
| 下半身 | lower body | 臀部/腰 |
| 首 | neck | 颈部 |
| 頭 | head | 头部 |
| 左肩 / 右肩 | shoulder L/R | 肩 |
| 左腕 / 右腕 | arm L/R | 上臂 |
| 左ひじ / 右ひじ | elbow L/R | 肘(前臂) |
| 左手首 / 右手首 | wrist L/R | 手腕 |
| 左足 / 右足 | leg L/R | 大腿 |
| 左ひざ / 右ひざ | knee L/R | 膝(小腿) |
| 左足首 / 右足首 | ankle L/R | 脚踝 |
| 左つま先 / 右つま先 | toe L/R | 脚尖 |
| 左目 / 右目 | eye L/R | 眼球(可选) |

还需要 IK 骨骼:左足ＩＫ / 右足ＩＫ、左つま先ＩＫ / 右つま先ＩＫ。

## XPS 常见骨骼名对照

XPS 模型因来源游戏不同,骨骼命名差异很大。常见模式:

| XPS 常见名 | 对应 MMD 骨骼 | 备注 |
|---|---|---|
| `root` / `root ground` | 全ての親 | |
| `pelvis` / `hip` / `hips` | 下半身 / センター | 需判断是重心还是臀部 |
| `spine` / `spine1` | 上半身 | 有时 spine 链有 3-4 节,需合并 |
| `spine2` / `chest` | 上半身2 | |
| `neck` | 首 | |
| `head` | 頭 | |
| `clavicle_L` / `shoulder_L` | 左肩 | clavicle = 锁骨 ≈ MMD 的肩 |
| `upperarm_L` / `arm_L` | 左腕 | 注意:MMD 的「腕」= 上臂 |
| `forearm_L` / `lowerarm_L` | 左ひじ | |
| `hand_L` | 左手首 | |
| `thigh_L` / `upperleg_L` | 左足 | |
| `calf_L` / `lowerleg_L` / `shin_L` | 左ひざ | |
| `foot_L` | 左足首 | |
| `toe_L` / `toes_L` | 左つま先 | |

> **注意**:这张表只是常见模式,实际模型可能完全不同。务必逐个检查。

## 映射方式

1. **Cats 插件自动映射** — [[cats-blender-plugin]] 的 Fix Model 功能能识别常见命名并自动重命名为 MMD 标准名,是最快的方式。但不保证 100% 正确,需要人工检查。
2. **手动重命名** — 在 Blender 的 Armature 编辑模式下逐个改名。适合 Cats 无法识别的情况。
3. **骨骼约束/重绑定** — 有些 XPS 模型骨骼结构差异太大(如缺少 center、spine 分段不同),需要新建 MMD 骨骼并转移权重,见 [[权重-weights]]。

## XPS 没有但 MMD 需要的骨骼

转换时通常需要**手动添加**:
- **全ての親**(root)— 很多 XPS 模型没有全局根骨
- **センター / グルーブ** — 重心骨,XPS 没有对应概念
- **IK 骨骼** — 左足ＩＫ、右足ＩＫ、つま先ＩＫ,XPS 完全没有 IK
- **目ボーン** — 眼球骨骼,XPS 有时有有时没有
- **指骨** — XPS 有时有完整手指骨骼,有时没有;MMD 动作常用到手指

## 相关页面

- [[骨骼-bones]] — MMD 骨骼体系详解
- [[xps-format]] — XPS 格式概览
- [[cats-blender-plugin]] — 自动修复/重命名工具
- [[xps-to-mmd-流程]] — 完整转换流程
