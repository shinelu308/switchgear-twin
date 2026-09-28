# 开关柜三维参考模型

这是以用户提供的爆炸分解图为主参考制作的中等精度展示资产，适合后续进行部件选择、状态展示和数字孪生数据绑定。不是实物测绘、制造图纸或经过校验的电气设计。

## 文件

- `switchgear_master.blend`：Blender 主工程，包含模型、材质、灯光、相机与爆炸动画。
- `switchgear_digital_twin.glb`：实时展示用资产，包含部件层级、材质、自定义属性及展开动画；不包含摄影棚背景。
- `switchgear_exploded.png`：爆炸状态渲染。
- `switchgear_assembled_cutaway.png`：装配状态剖视渲染，隐藏前门、右侧板及顶盖，方便查看内部。
- `component_manifest.json`：稳定部件 ID、类别、爆炸位移和预留数据绑定字段。
- `build_switchgear.py`：可重新生成资产的 Blender Python 脚本。
- `optimize_glb.py`：将部件内网格合并并导出统一展开动画，保留主工程的独立可编辑零件。

## 打开和操作

使用 Blender 5.2 或兼容版本打开主工程。工程默认显示爆炸状态：

- 时间轴第 1 帧：完整装配状态。
- 第 24–90 帧：由装配状态展开。
- 第 90 帧：爆炸状态。
- 在 Outliner 中展开 `ASSET | Switchgear`，按 `SG-` 前缀查找部件组。
- `STUDIO | Excluded from GLB` 为相机、灯光和地面。

展开动画仅用于结构展示，不能作为真实拆装顺序或无碰撞装配路径。柜门本版随部件整体分离，尚未提供独立绕铰链开门动画。

## 尺寸与准确性

建模单位为米。采用 0.8 × 1.0 × 2.2 m 的柜体外形作为假设值，来源于另一张参考图，尚未确认对应同一设备。内部部件尺寸、板厚、线缆路径、连接端子、背面和安装关系均包含推定。

模型突出骨架、板件、主断路器、母排、线缆和端子排。小型孔位部分用表面凹槽视觉表示，没有逐孔布尔切穿；紧固件复用，仪表文字为示意。本版没有复制厂商商标，断路器是参考形态而非认证型号。电气导通关系、绝缘距离、设备额定值均未验证。

## 数字孪生接入

各部件父节点包含 `component_id`、`label`、`category`、`geometry_status` 和 `sensor_binding`。GLB 开启自定义属性导出，可由支持 glTF extras 的应用读取。

以 `component_manifest.json` 中的 ID 作为业务映射键，不要依赖子网格名称或节点数组序号。传感器地址尚为空，需根据实际设备点表接入。导出后的 glTF 按格式惯例采用 Y 轴向上，Blender 工程为 Z 轴向上。

实时平台需验证透明度、阴影、动画、拾取以及多柜场景的性能。本版为单柜展示资产，暂未制作多级 LOD，也未完成实际业务平台集成。

主工程保留细分零件；实时 GLB 按 17 个语义部件组合网格，便于以部件为单位选取。紧固件和单个端子在实时版本中不再是独立可选节点。如需单独选取，应从主工程另行导出。

## 重新生成

在 PowerShell 中运行：

```powershell
& 'E:\Program Files\Blender Foundation\Blender 5.2\blender.exe' --background --factory-startup --python 'E:\codex\2026-09-28\bang\outputs\build_switchgear.py'
```

将重新写入同目录中的生成模型、清单和渲染文件。修改前请先备份已有人工编辑版本。
