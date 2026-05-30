---
title: Toon 贴图对照 / 共有トゥーン toon01–10
type: concept
status: draft
sources:
  - https://czpanel.com/lecture/mmd/pmxe/toonmap/
  - https://ch.nicovideo.jp/andou0409natu/blomaga/ar1239837
  - https://p-nez.net/toontips
  - https://learnmmd.com/http:/learnmmd.com/category/mme-effects-tutorials/toon-shader/
updated: 2026-05-30
---

# Toon 贴图对照(共有トゥーン toon01–10)

MMD 的卡通明暗靠 **Toon 贴图**:一张「上亮下暗」的渐变图,按受光角度查表上色。MMD 自带 **toon01.bmp ~ toon10.bmp** 共 10 张「共享 toon(共有トゥーン)」。

> ⚠️ **保留名**:`toon01.bmp`~`toon10.bmp` 是 MMD 保留文件名。即使你在模型目录放同名文件,**MMD 也会忽略你的、用它自带的**。要自定义 toon 必须用别的文件名。(来源: learnmmd Toon Shader)

## toon01–10 各编号特征

> 各来源描述基本一致,但**没有官方逐张色值表**;下表是社区共识,作为「选哪张」的参考,**最终以 MMD/PMXEditor 实际预览为准**。

| 编号 | 特征 | 常用于 |
|---|---|---|
| **toon01** | 一般阴影,上白下黑、明暗分界清晰 | 头发、眉、睫、眼、衣服(通用) |
| **toon02** | **皮肤标准**,阴影偏**红**(暖色) | 皮肤、脸、身体(最常用肤色 toon) |
| toon03 | 比 01 更**深**的阴影 | 想要重阴影的部件 |
| toon04 | 上半不再纯白,偏**淡黄** | 风格化 |
| toon05 | 偏粉、用**渐变**而非硬分界(肤色备选) | 深一点肤色 / 柔和过渡 |
| toon06 | 偏黄/金 | 风格化 |
| **toon07** | 接近**纯白 = 几乎无影** | 脸(想让脸不出硬阴影时)、平涂部件 |
| toon08–10 | 偏黄、缺上半白色;08–10 趋于**空白/极淡** | 几乎不出影 / 特殊用途 |

> 关键三张速记:**toon01 通用影、toon02 皮肤(红影)、toon07 无影(白)**。(来源: 安堂ブロマガ ar1239837;czpanel toonmap;p-nez toontips)

## 渐变方向(做自定义 toon 时)
- toon 图是**纵向渐变**:**上=亮、下=暗**。
- 还有两个关键区域:**左边缘**用于「关自身阴影」时按光照角度上色;**右下角**用于「开自身阴影」时乘以阴影深度。(来源: learnmmd Toon Shader)

## 实用建议
- 新手最简:**皮肤 toon02,其余 toon01**,即可得到像样的 MMD 卡通感。
- 脸部硬阴影难看 → 脸单独换 **toon07**(无影)或自定义柔和 toon。
- 想统一风格 → 把 toon 当作「整个场景的特性」,全模型尽量用一致的 toon,而非每材质各搞一张。(来源: learnmmd)
- 自定义肤质/发质 toon → 用**非保留名**(如 `skin_toon.png`),在材质里指定为「个别 toon」。

## 与转换的关系
- XPS 转过来的模型**没有 toon 概念**,默认可能全挂 toon01(平、缺味道,见 [[材质-materials]] 的 Reika 实测:32/32 全 toon01)。
- MMD 化润色时按上表给皮肤换 toon02、脸按需 toon07。见 [[xps-材质差异]] 的润色清单。

## 相关页面
- [[材质-materials]] — Toon 在 PMX 材质里的字段
- [[xps-材质差异]] — XPS→MMD 材质润色
- [[pmx-format]] — toon 引用的二进制表示(共享 vs 个别)
- [[pmxeditor]] — 设置 toon 的工具
