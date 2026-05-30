# 摄入日志 (Ingest Log)

每次 `ingest` / 回填 `query` 后追加一行:`日期 | 来源 | 动作 | 受影响页面`。

| 日期 | 来源 | 动作 | 受影响页面 |
|---|---|---|---|
| 2026-05-29 | (初始化) | 搭建骨架 + 写入种子页面 | index, concepts/*, tools/mmd_tools, workflows/blender-to-pmx |
| 2026-05-30 | 通用领域知识 | 新建 XPS→MMD 转换知识页面(种子) | concepts/xps-format, concepts/xps-骨骼映射, concepts/xps-材质差异, tools/xps-tools-blender, workflows/xps-to-mmd-流程, troubleshooting/xps-转换常见问题 |
| 2026-05-30 | (扩展) | 现有页面补充 XPS 转换相关内容 | concepts/骨骼-bones, concepts/权重-weights, concepts/材质-materials, tools/cats-blender-plugin, index |
| 2026-05-30 | 联网核实(MMD-Blender GitHub / extensions.blender.org / teamneoneko+feilen GitHub / vpvpwiki 394 / MMD swamp / tktk blog) | ingest:新建准标准骨页;校正 mmd_tools 版本(v4.x/Blender 4.2+,旧 v2.x/Blender 3.6,仓库迁 MMD-Blender 组织)与 Cats 现状(原版 4.0 后停更,新版用 Team Neoneko/Tuxedo);补 PMXEditor 准标准ボーン插件 | **新建** concepts/准标准骨骼-semi-standard-bones;tools/mmd_tools, tools/cats-blender-plugin, tools/pmxeditor, concepts/骨骼-bones, index |
| 2026-05-30 | 实测解析 ~/Reika18_Children.pmx(PMX 2.0, 二进制解析) | ingest:新建标准骨架范本页(263骨/19骨骼morph/48刚体/29关节实测);用实测付与系数(肩C -1.0、腕捩 0.25/0.5/0.75、足D 1.0)与 IK 链补全准标准骨页并升 stable;记录两处反常发现(全角 親指０/ＩＫ;表情全为骨骼morph) | **新建** reference/标准骨架范本-reika;concepts/准标准骨骼-semi-standard-bones(→stable), index |
| 2026-05-30 | 缺口补全(领域知识 + Reika 实测物理参数) | ingest:补 XPS→MMD 方向的零覆盖知识 —— 新建 坐标系/朝向/roll、Blender端绑定改造、导出前QA清单;深化 物理(从零搭建+实测参数 衰减~0.95/回弹0)、权重(SDEF断层/4骨上限/控制骨不刷权重)、表情(从零做+Shape Key日文命名) | **新建** concepts/坐标系-朝向-pose, workflows/blender-mmd-绑定改造, troubleshooting/导出前qa清单;深化 物理-physics, 权重-weights, 表情-morphs, index |
| 2026-05-30 | 实测解析 Reika 材质段(32材质/34贴图) | ingest:回填材质实测配置 —— 自定义toon(skin/eye/hair)、SPH给肤发+SPA给眼、32全両面+自身阴影+27描边、_s/_n命名痕迹;并修正 xps-材质差异 的重复段与 材质-materials 底部垃圾行 | 深化 concepts/材质-materials, concepts/xps-材质差异(去重) |
