---
title: PMX 模型格式
type: concept
status: stable
sources:
  - 种子内容/通用领域知识
  - https://gist.github.com/felixjones/f8a06bd48f9da9a4539f  # PMX 2.0/2.1 spec
  - https://gist.github.com/Binsk/3bfd792e2dd4aa9cd6bb45dd05c0727e  # PMX 2.1 spec
  - 实测 ~/Reika18_Children.pmx → [[标准骨架范本-reika]]
updated: 2026-05-30
---

# PMX 模型格式 (PMX / Polygon Model eXtended)

MMD 当前的**标准模型格式**,由 PMD 演进而来。一个 `.pmx` 文件打包了模型的全部数据。

## 与 PMD 的关系
- **PMD**:旧格式,字段固定、对编码与扩展支持差。
- **PMX**:现行标准(常见 2.0 / 2.1),支持 UTF 文本、更灵活的材质、更多变形类型与骨骼标志。新建模型应优先用 PMX。

## 文件结构(顶层顺序)

PMX 按固定顺序排列各段(解析时必须顺序读过去):

```
Header(签名 "PMX " + 版本float + Globals)
→ 顶点 → 面 → 贴图 → 材质 → 骨骼 → 表情(morph)
→ 显示枠 → 刚体 → 关节 →(2.1: SoftBody)
```

### Globals(头部全局参数,8 字节)
决定后续怎么解析,关键两个:
- **文本编码**:0 = UTF-16LE,1 = UTF-8。
- **索引宽度**(各 1/2/4 字节):顶点 / 贴图 / 材质 / 骨骼 / 表情 / 刚体。骨数多时骨索引会是 2 或 4 字节。
- 还有「附加 UV 数量」。
(来源: felixjones PMX spec;实测范本为 UTF-16LE、骨索引 2 字节、附加 UV ×1)

## 变形类型(顶点权重)
PMX 顶点的蒙皮方式(详见 [[权重-weights]]):

| 值 | 类型 | 说明 |
|---|---|---|
| 0 | BDEF1 | 单骨,权重 1.0 |
| 1 | BDEF2 | 双骨线性混合 |
| 2 | BDEF4 | 四骨混合 |
| 3 | SDEF | 球面变形,改善扭转处塌陷 |
| 4 | QDEF | 双四元数(PMX 2.1 新增) |
(来源: felixjones PMX spec)

## 材质字段(与渲染相关)
- 颜色:diffuse(RGBA)/ specular(RGB)+ 光泽度 / ambient(RGB)。
- 贴图索引 / **Sphere 索引 + sphere mode** / **toon 引用**。
- **绘制标志位**(material flag):

| 位 | 含义 |
|---|---|
| bit0 (0x01) | 无背面剔除(=**両面描画**) |
| bit1 (0x02) | 地面阴影 |
| bit2 (0x04) | 产生阴影(draw to shadow map) |
| bit3 (0x08) | 接收自身阴影 |
| bit4 (0x10) | **描边(エッジ)** |
| bit5 (0x20) | 顶点色(2.1) |
| bit6/7 | 点/线绘制(2.1) |

- **Sphere mode**:0=无,1=**SPH(乘算)**,2=**SPA(加算)**,3=附加 UV 子贴图。
- **Toon 引用**:0=用贴图索引指定(个别 toon);1=用共享 toon(一个字节 0–9 对应 toon01–10)。见 [[toon-贴图对照]]。
(来源: felixjones PMX spec;实测见 [[材质-materials]])

## 骨骼标志位(bone flag)
控制每根骨行为,转换/补骨时关键:

| 位 | 含义 |
|---|---|
| bit0 (0x0001) | 连接点用骨索引(否则用坐标偏移) |
| bit1 (0x0002) | 可旋转 |
| bit2 (0x0004) | 可移动 |
| bit3 (0x0008) | 可见 |
| bit4 (0x0010) | 可操作(enabled) |
| bit5 (0x0020) | **IK** |
| bit8 (0x0100) | **回転付与**(继承旋转) |
| bit9 (0x0200) | **移動付与**(继承平移) |
| bit10 (0x0400) | 固定轴 |
| bit11 (0x0800) | 局部轴 |
| bit12 (0x1000) | 物理后变形 |
| bit13 (0x2000) | 外部父变形 |
(来源: felixjones PMX spec;付与/IK 实测见 [[标准骨架范本-reika]])

## 表情(morph)类型

| 值 | 类型 | 值 | 类型 |
|---|---|---|---|
| 0 | 组(group) | 6 | UV ext3 |
| 1 | 顶点(vertex) | 7 | UV ext4 |
| 2 | 骨骼(bone) | 8 | 材质(material) |
| 3 | UV | 9 | flip(2.1) |
| 4 | UV ext1 | 10 | impulse(2.1) |
| 5 | UV ext2 | | |
(来源: felixjones PMX spec。详见 [[表情-morphs]];范本实测 19 个全为 bone 型)

## PMX 2.0 vs 2.1
- **2.1 新增**:QDEF(变形)、flip / impulse(morph)、材质顶点色与点/线绘制、SoftBody(软体)。
- **关键提醒**:**MMD 本体只完整支持 2.0**;2.1 的特性多数 MMD 本体不识别,仅部分第三方(如 MMM、某些加载器)支持。**做通用模型应坚持 PMX 2.0 范围内的特性**。(来源: felixjones/Binsk spec 对比;社区共识)

## 其它段
- **显示枠(表示枠)**:把骨骼/表情分组,供 MMD 界面操作;不进枠的骨在 MMD 里点不到。见 [[blender-mmd-绑定改造]]。
- **刚体 + 关节**:物理,见 [[物理-physics]]。

## 配套格式
- `.vmd` — 动作 / 表情 / 相机数据(motion)。
- `.vpd` — 单帧姿势数据。

## 在 Blender 里
Blender 不原生支持 PMX,需要 [[mmd_tools]] 插件来导入/导出。完整路线见 [[blender-to-pmx-导出流程]]。

## 相关页面
- [[标准骨架范本-reika]] — 一具 PMX 的实测各段
- [[权重-weights]] · [[材质-materials]] · [[骨骼-bones]] · [[表情-morphs]] · [[物理-physics]]
- [[toon-贴图对照]] · [[mmd_tools]]
