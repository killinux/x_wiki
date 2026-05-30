---
title: MMD 兼容/替代软件(MMM / nanoem)
type: tool
status: stable
sources:
  - https://dic.nicovideo.jp/a/mikumikumoving
  - https://sites.google.com/site/mikumikumoving/
  - https://nanoem.readthedocs.io/
  - https://3d-modely.com/blog/animation/nanoem/
updated: 2026-05-30
---

# MMD 兼容/替代软件(MMM / nanoem)

MMD 本体([[mmd本体-使用]])只有 Windows、且功能偏基础。社区有几款**兼容 PMX/VMD** 的替代软件,各有所长。模型仍按 [[pmx-format|PMX]] 制作,这些软件读同样的模型/动作。

## MikuMikuMoving(MMM)
- 作者 **Mogg**(Face And Lips 的作者),Windows。功能与 MMD 对等,且**做动作更强**。
- 兼容:可直接用 MMD 的**模型/pose/动作**;但**读不了 MMD 的工程文件 `.pmm`**。
- 亮点(来源: niconico 大百科 MikuMikuMoving;官方 sites):
  - **骨骼多层 layer**:不改骨架就能把一根骨的运动拆成多层管理。
  - **可变帧率**:不限 30fps,可做 60fps 高帧或 8/12fps 的「赛璐珞」风。
  - MP3 音频、便捷 lip-sync、**无需 MME 即可加字幕**。

## nanoem
- 作者 **hkrn**,**跨平台**(主打 **macOS**,也有其它平台)。Mac 用户的 MMD 方案。
- 兼容:读写 MMD 的**模型与 VMD 动作**;另有自有 **NMD** 扩展动作格式(NMD **不能**被 MMD/其它兼容软件读)。
- 当前版本约 v34.x(以 readthedocs 文档为准)。
(来源: nanoem readthedocs;モデログ nanoem)

## 选用
- 只是放模型跳现成舞 → MMD 本体即可([[mmd本体-使用]])。
- 想**自己 K 动作**、要高帧率/分层/字幕 → MMM。
- 在 **Mac** 上 → nanoem。

## 相关页面
- [[mmd本体-使用]] — MMD 本体
- [[pmx-format]] · [[vmd-动作格式]] · [[vpd-姿势格式]]
- [[mme-特效]]
