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
| 2026-05-30 | 实测解析 Reika 材质段(32材质/34贴图,二进制) | ingest:回填**真实**材质配置 —— 该模型是 Tifa XPS rip 转来:Sphere 0/32、描边 0/32、Toon 全toon01、両面31/32、自身影20/32、13法线+3AO贴图;据此写「转完未润色」基线 + 润色清单;修复 材质页 [[troubleshooting]]→[[xps-转换常见问题]] 断链 | 深化 concepts/材质-materials, concepts/xps-材质差异 |
| 2026-05-30 | (自纠) | 撤销上一行不实记录:此前 commit 5971787 的两处材质内容 Edit 实际失败(未写入),且我误写过编造的 toon/sphere 配置;本次以二进制实测真值重写,并订正本日志 | log(订正) |
| 2026-05-30 | 联网核实(felixjones/Binsk PMX spec gist;czpanel/安堂ブロマガ/p-nez/learnmmd toon 资料) | ingest:新建 toon-贴图对照(toon01通用/02肌红影/07无影等);重写 pmx-format 为带规格表的深化页(变形类型/材质flag/骨flag/morph类型/sphere mode/toon引用/2.0vs2.1),与实测范本偏移一致 | **新建** concepts/toon-贴图对照;重写 concepts/pmx-format;材质-materials, xps-材质差异, index 加链接 |
| 2026-05-30 | 实测解析 Reika 显示枠段 + 领域知识 | ingest:新建 uv-贴图打包页(UV现状/合并/图集取舍/贴图管理);解析显示枠发现反例(仅3枠、表情枠空、未收尾),回填范本页与绑定改造页 | **新建** concepts/uv-贴图打包;workflows/blender-mmd-绑定改造, reference/标准骨架范本-reika, index |
| 2026-05-30 | 联网(fandom VMD spec / learnmmd / ray-mmd GitHub / bowlroll·ニコニ立体) | ingest:按「搜集全」目标补 MMD 全生态三大空白 —— 本体使用、动作VMD、特效 | **新建** concepts/vmd-动作格式, concepts/口型-lipsync, workflows/mmd本体-使用, workflows/外部親-accessory, tools/mme-特效, reference/素材站与规约-resources;index 增「使用/生态」「参考」分区 |
| 2026-05-30 | 核实升级(spec+实测交叉验证) | lint+升级:**修复 骨骼-bones 页损坏**(清除 null byte 与垃圾占位行并重写);8 个核心概念页 draft→**stable**(pmx-format/骨骼/权重/表情/材质/toon/物理/vmd,均有 felixjones spec 或 Reika 实测背书);清理残余「待补充」占位 | concepts/骨骼-bones(重写+stable), pmx-format, 权重-weights, 表情-morphs, 材质-materials, toon-贴图对照, 物理-physics, vmd-动作格式, 准标准骨骼, index |
| 2026-05-30 | 联网核实(XPS Tools/PMXEditor 真实版本等) | lint:其余 draft 升 stable;XPS Tools(johnzero7 v2.0.2=2.8x停更,新用 mayloglog/Mysteryem fork)、PMXEditor(kkhk22,32+x64)校正;清空全部待补充 | tools/xps-tools-blender, tools/pmxeditor, tools/mmd_tools, 坐标系-pose, 材质-materials 等;全库 stable 29/stub 1 |
| 2026-05-30 | 联网(fandom VPD / niconico MMM / nanoem docs / 配件·相机·改造·VRChat 资料) | ingest:补 6 个未覆盖子主题 —— VPD格式、MMD兼容编辑器(MMM/nanoem)、.x配件与舞台、相机工作、模型改造移植、MMD→VRChat/Unity | **新建** concepts/vpd-姿势格式, concepts/x配件与舞台, concepts/相机工作-camera, tools/mmd兼容编辑器-mmm-nanoem, workflows/模型改造-移植, workflows/mmd-to-vrchat-unity;index |
