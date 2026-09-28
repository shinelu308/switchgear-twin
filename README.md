# 开关柜三维参考模型 · 在线展示

交互式查看由 Blender 参数化生成的开关柜数字孪生资产（SG-01）。

**在线访问**：https://shinelu308.github.io/switchgear-twin/

## 页面能力

- Three.js（r160）本地化加载：拖拽旋转 / 滚轮缩放 / 右键平移 / 自动旋转
- 装配 ⇄ 爆炸切换：页面按 `component_manifest.json` 的 `exploded_offset_m` 实时驱动各部件 mesh 位移（不依赖 GLB 内置动画）
- 17 个语义部件清单（稳定 ID / 类别 / 爆炸位移）
- 数字孪生接入说明（glTF extras 数据绑定字段）

## 目录结构

```
index.html                           展示页（Three.js 加载 + 部件清单）
assets/vendor/                       本地化 Three.js 核心与 addons（去 CDN，国内访问稳定）
assets/switchgear_digital_twin.glb   展示资产（7.2MB，17 网格 / 34 节点）
assets/component_manifest.json       部件清单（component_id / 类别 / 爆炸位移 / sensor_binding）
assets/validation_report.json        资产校验报告
img/assembled_cutaway.png            装配剖视渲染
img/exploded.png                     爆炸状态渲染
docs/USAGE.md                        模型使用与再生成说明
```

## 数字孪生接入要点

- 部件父节点携带 `component_id` / `label` / `category` / `geometry_status` / `sensor_binding`（glTF extras），以 `component_manifest.json` 的 ID 作为业务映射键。
- 建模单位米，包络 0.8 × 1.0 × 2.2 m；glTF 按 Y 轴向上导出。
- 传感器地址待实际设备点表接入；展开动画仅用于结构展示。

## 来源与免责

模型由 Blender 5.2 参数化脚本生成，以爆炸分解图为主参考制作，属于中等精度展示资产——
不是实物测绘、制造图纸或经过校验的电气设计；电气导通关系、绝缘距离、设备额定值均未验证。
