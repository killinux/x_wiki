---
title: VMD 动作格式 / Vocaloid Motion Data
type: concept
status: draft
sources:
  - https://mikumikudance.fandom.com/wiki/VMD_file_format
  - VMD format gist(社区规格)
updated: 2026-05-30
---

# VMD 动作格式(Vocaloid Motion Data)

`.vmd` 是 MMD 的**动作/表情/相机/光照**数据格式。建模阶段不产出 VMD,但模型绑定的好坏直接决定「能不能吃下别人的 VMD」——所以理解它很重要。见 [[骨骼-bones]]、[[表情-morphs]]。

## 核心特征:按名字匹配

VMD **只存名字 + 帧 + 数值**,不存骨骼层级。播放时按**骨骼名/表情名**找模型里的同名对象套用。

> 这就是为什么 [[xps-骨骼映射]] 必须把骨改成 MMD 标准日文名、且**全角半角要一致**(见 [[标准骨架范本-reika]] 的 `親指０`/`ＩＫ` 坑)——名字对不上,这条轨道就被忽略。

## 文件结构(社区规格)

| 段 | 内容 |
|---|---|
| 头部 | 30 字节签名 `Vocaloid Motion Data 0002` + 模型名(20 字节,旧版 10) |
| 骨骼帧 | 4 字节计数 + 每帧 **111 字节** |
| 表情帧 | 4 字节计数 + 每帧 **23 字节** |
| 相机帧 | 4 字节计数 + 每帧 **61 字节** |
| 光照 / 自阴影 / IK 开关 | 新版本追加 |

### 骨骼帧(111 字节)
- 15 字节 骨骼名(**Shift-JIS** 编码——注意不是 UTF)
- 4 字节 帧号(uint32)
- 12 字节 位置(3×float)
- 16 字节 旋转(**四元数** 4×float,X/Y/Z/W)
- 64 字节 插值参数(贝塞尔曲线控制点)

### 表情帧(23 字节)
- 15 字节 表情名(Shift-JIS)+ 4 字节 帧号 + 4 字节 权重(float 0.0–1.0)

### 相机帧(61 字节)
- 帧号 + 距离 + 位置(3f)+ 旋转(欧拉 3f)+ 插值(24)+ 视角 + 透视开关
(来源: fandom VMD_file_format;社区 gist。字段细节以规格原文为准。)

## 与 Blender 的关系
- [[mmd_tools]] 能**导入 VMD** 到 Blender(套到骨骼/Shape Key 上),也能**导出 VMD**。
- 编码是 Shift-JIS:Blender 端处理日文骨名时注意编码,避免乱码导致轨道丢失。

## 相关页面
- [[骨骼-bones]] · [[xps-骨骼映射]] — 名字匹配
- [[表情-morphs]] · [[口型-lipsync]] — 表情轨道
- [[mmd本体-使用]] — 在 MMD 里加载 VMD
- [[pmx-format]] — 模型侧格式
