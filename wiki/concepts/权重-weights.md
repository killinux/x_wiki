---
title: 权重 / ウェイト / weights & 变形类型
type: concept
status: draft
sources: [种子内容/通用领域知识]
updated: 2026-05-29
---

# 权重与变形类型 (ウェイト / weights)

权重决定每个顶点受哪些骨骼、各占多少,直接决定关节处变形是否自然。

## PMX 顶点变形类型
- **BDEF1**:1 根骨骼,权重 100%(刚性部分,如骨头)。
- **BDEF2**:2 根骨骼线性混合(最常见)。
- **BDEF4**:4 根骨骼混合(复杂区域)。
- **SDEF**:球面变形,改善**手腕/肩等扭转处**的塌陷,效果比 BDEF2 自然(MMD 特有,需正确设置)。
- (PMX 2.1 还有 QDEF,本体支持有限)

## 刷权重要点
- 关节处(肘、膝、腕)做平滑过渡,避免「塌陷/撕裂」。
- 旋转测试:摆 pose 检查变形,而非只看静态。
- 物理骨(头发/裙)末端通常 BDEF1 绑到对应末端骨,再交给 [[物理-physics]]。

## 在 Blender 中
- 用 **Vertex Groups + Weight Paint**;每个 Vertex Group 名要对应骨骼名(见 [[骨骼-bones]])。
- [[mmd_tools]] 导出时把权重转为 PMX 的 BDEF/SDEF。Blender 没有 SDEF 概念,SDEF 通常需在 [[pmxeditor]] 中转换/设置。
- [[cats-blender-plugin]] 有权重相关辅助(如合并骨骼并转移权重)。

参见 [[pmx-format]]、[[blender-to-pmx-导出流程]]。

## XPS 权重转换注意事项

XPS 模型支持最多 4 骨权重(类似 BDEF4),导入 Blender 后权重数据通常保留完好。但转换过程中需注意:
- **骨骼重命名后**,对应的 Vertex Group 名也必须同步修改,否则权重失效。Cats 的 Fix Model 会自动处理;手动改名时要逐个同步。
- **新增骨骼**(center、IK 等)是纯控制骨,通常不需要权重。
- **合并 mesh 时**确保各 mesh 的 Vertex Group 名称指向同一骨骼,否则权重会冲突。
- XPS 权重来自游戏引擎,质量通常不错,但某些关节(肩、腕)可能需要手动平滑。

详见 [[xps-骨骼映射]]、[[xps-to-mmd-流程]]。

## Blender 权重 → PMX SDEF / 多骨的断层

这是 Blender↔MMD 的已知不对等点:

- **Blender 没有 SDEF 概念**。从 Blender 导出的权重都是 BDEF 系。要 SDEF(改善腕/肩扭转塌陷),需在 [[pmxeditor]] 里把目标顶点的 BDEF2 **转为 SDEF**(PMXEditor 有批量转换/SDEF 自动设置功能)。
- **每顶点超过 4 骨**:Blender 顶点可绑任意多骨,但 PMX 最多 4 骨(BDEF4/QDEF)。导出时 [[mmd_tools]] 会**裁剪到权重最大的 4 根并重新归一化**——若关键骨权重很小会被丢。导出前用 **Weight Tools → Limit Total = 4** 自己先清理,结果更可控。
- **控制骨不刷权重**:IK 骨(足ＩＫ/つま先ＩＫ)、付与父骨(肩P、足IK親)、グルーブ/センター 等是**纯控制骨,顶点组应为空**;给它们刷权重反而导致动作时部位乱飞。参见 [[标准骨架范本-reika]] 的骨清单(那些骨都不承载蒙皮)。
- **D 系足骨承载形变**:足D/ひざD/足首D 才是实际蒙皮的骨(由付与跟随可见足骨,系数 1.0),做 D 系绑定时把腿部权重转到 D 骨。见 [[准标准骨骼-semi-standard-bones]]。

> 实务:先在 Blender 把 BDEF 权重刷干净、Limit Total=4、控制骨清空,导出后再到 PMXEditor 补 SDEF。
