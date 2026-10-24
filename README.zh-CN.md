# VAULT Print Planner Skill

[English](README.md) | 中文

下载仓库中的 `vault-print-planner-skill.zip` 并解压，以下路径以解压后的文件夹为准。

页面右上角可以切换中文 / English，当前选型会保留。自己填写的任务名称、备注和原始模型文件名不会被翻译。原厂说明书图片保留原文。

中英文 VAULT 模块化收纳打印规划工具与 Codex skill：选组合、单独补配件、查看简化 3D 装配、保存/恢复打印任务、记录已打印数量及整体组合进度，并导出 Bambu Studio 3MF 工程。

当前规划流程针对 P1S、0.4/0.6 mm 喷嘴、PLA/PETG。不会自动发送打印。必须使用自己合法取得的 VAULT 模型和说明书；仓库不附带模型；说明书的使用方式见下文。

## 模型购买、本地部署与说明书

**本工具不提供、不上传、不分发 VAULT 模型文件。每位使用者需要自行向设计师或授权渠道购买模型，并遵守模型许可。** 将购买的文件下载、解压到自己的电脑，启动时通过 `--archive` 指向该本地文件夹。本工具的 AGPL 开源许可不包含 VAULT 模型的使用或分发权。

模型及含模型几何数据的文件都应保留在本地，包括 STL、STEP、3MF、转换后的网格、打印工程和模型压缩包，不得上传到本仓库或放进发布安装包。规划器读取本地模型进行预览、配件选择和工程生成，不需要把模型上传到 GitHub。

说明书可以用于选型、打印和装配参考，需要时读取使用者本地的说明书。如果权利人允许转载，也可以将说明书作为参考资源附带；使用本地说明书和公开转载说明书是两回事。目前安装包尚未附带第三方说明书。

## 安装 skill

把 `skills/vault-print-planner` 整个文件夹复制到 `~/.codex/skills/`（或自己的 `$CODEX_HOME/skills/`），重新开始会话后使用 `$vault-print-planner`。

例如：“用 $vault-print-planner 选一组 M5 抽屉，另外补两套底板，并检查打印板前缘挤出线。”

## 单独运行网页

需要 Python 3.11+ 和已安装的 Bambu Studio 预设。

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python skills/vault-print-planner/scripts/launch.py --archive '/path/to/VAULT' --port 8766
```

用 Chrome 或其他浏览器打开 http://127.0.0.1:8766/planner.html 。Windows 可改用 `.venv\Scripts\python.exe`；自动“打开 Bambu Studio”按钮目前仅适配 macOS。

## 打印边界

导出的 3MF 是待检查的工程，不是已经验证可开打的指令。当前打包版补充了保守的前缘和板边留量；仍需检查实际起始 G-code、brim、支撑、材料预设及 AMS 对应关系。大件可能需要手动排板或分盘，不自动缩放。简化装配图不是精确装配仿真。

原本一次打印中，小配件与前缘预挤出线重叠，因此 skill 明确要求把“几何放得下”和“实际首层路径无冲突”分开核对。已保存的历史工程不会自动套用新的留量。

## 来源与许可

应用基于 [marcelfarres/vault-configurator](https://github.com/marcelfarres/vault-configurator) 的下载版本修改，遵循 [GNU AGPL v3](LICENSE)。本仓库增加中文规划入口、配件模式、删除恢复、完成记录、组合预览、skill 说明及保守 P1S 留边。无原仓库 Git 历史，不能声称它是正式 GitHub fork 或某个已核实 commit。

Three.js 保留其 `vendor/three/LICENSE`。VAULT 模型、说明书及品牌属于 USSA Design，不在本仓库授权范围内。本工具非 USSA Design 或 Bambu Lab 官方产品。设计师的耗材统计未附带，空数据文件仅用于启动；最终重量/时间以切片器为准。

打印记录、输出工程、缓存、原始模型和个人路径仅保存在本地，并由 .gitignore 排除。
