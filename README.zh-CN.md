# VAULT 打印规划器 — Bambu Studio / P1S 3D 打印工具与 Codex Skill

[English](README.md) | 中文

**为 USSA VAULT 模块化收纳箱和抽屉规划 3D 打印，并导出 Bambu Studio 3MF 工程。** 这是非官方的本地打印规划器，也可以作为 Codex skill 使用。支持抽屉与翻盖箱选型、Gridfinity 底板和锁等配件补打、三维预览、STL 零件清单、P1S 初步排板、五金清单与打印进度记录。

**[下载 v0.1.0 最新版](https://github.com/hp0411-oss/vault-print-planner-skill/releases/tag/v0.1.0)** · [English guide](README.md)

**不附带模型文件**：请自行购买，并使用本地模型目录。本工具不是 USSA Design 或 Bambu Lab 官方产品。

下载仓库中的 `vault-print-planner-skill.zip` 并解压，以下路径以解压后的文件夹为准。

页面右上角可以切换中文 / English，当前选型会保留。自己填写的任务名称、备注和原始模型文件名不会被翻译。原厂说明书图片保留原文。

中英文 VAULT 模块化收纳打印规划工具与 Codex skill：选组合、单独补配件、查看简化 3D 装配、保存/恢复打印任务、记录已打印数量及整体组合进度，并导出 Bambu Studio 3MF 工程。

当前规划流程针对 P1S、0.4/0.6 mm 喷嘴、PLA/PETG。不会自动发送打印。必须使用自己合法取得的 VAULT 模型和说明书；仓库不附带模型；说明书的使用方式见下文。

## 从这里开始：安装与第一次使用

**只用网页工具不需要 Codex，也不需要 ChatGPT 订阅。** skill 是可选的助手使用方式。这是需要本地启动的 Python 程序，不是在线托管网页，也还不是双击安装的软件。

### 1. 准备软件和已购买的模型

- 安装 **Python 3.11 或更新版本**。Windows 安装时勾选添加到 PATH。macOS/Linux 用 `python3 --version`、Windows 用 `py --version` 检查版本。
- 安装并打开一次 Bambu Studio，完成设置向导，启用 **P1S、实际使用的 0.4 或 0.6 mm 喷嘴，以及 PLA/PETG 耗材预设**。工具读取本机预设；仅做规划和导出时不需要连接打印机。
- 自行购买 VAULT 模型并完整解压。模型根目录应直接包含 `01. DRAWERS`、`02. SUSTAINERS`、`03. MODIFICATIONS`，不要选择 ZIP 或外层 Downloads 文件夹。本版使用 `261020_VAULT_USSA` 文件结构测试。对应 PDF 说明书放在模型根目录，供工具提取帮助图；没有说明书也能启动主体功能。
- [下载完整工具包](https://github.com/hp0411-oss/vault-print-planner-skill/raw/refs/heads/main/vault-print-planner-skill.zip)并解压。进入包含 `requirements.txt` 和 `skills/` 的 `vault-print-planner-skill` 文件夹。如果用了 GitHub 的 **Code → Download ZIP**，还需要再解压里面的 `vault-print-planner-skill.zip`。

### 2. 安装依赖并自检

将下面示例路径换成自己的实际路径，路径有空格时保留引号。`--archive` 指向**购买的模型文件夹**，不是工具文件夹。

macOS / Linux 终端：

```sh
cd "/实际路径/vault-print-planner-skill"
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python skills/vault-print-planner/scripts/launch.py --archive "/实际路径/261020_VAULT_USSA" --check
```

Windows PowerShell：

```powershell
cd "C:\实际路径\vault-print-planner-skill"
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe skills/vault-print-planner/scripts/launch.py --archive "C:\实际路径\261020_VAULT_USSA" --check
```

依赖、本地 STL、P1S 的 PLA/PETG 预设应显示 **OK**。如果用 0.6 mm 喷嘴，在自检命令末尾加 `--nozzle 0.6`，网页中也要选择 0.6 mm。自检检查安装环境，不代表所有模型组合或打印路径都已验证。

### 3. 启动网页

macOS / Linux：

```sh
.venv/bin/python skills/vault-print-planner/scripts/launch.py --archive "/实际路径/261020_VAULT_USSA" --port 8766
```

Windows PowerShell：

```powershell
.\.venv\Scripts\python.exe skills/vault-print-planner/scripts/launch.py --archive "C:\实际路径\261020_VAULT_USSA" --port 8766
```

保持终端运行，在 Chrome 等浏览器打开 **http://127.0.0.1:8766/planner.html**。不要双击 HTML 文件。这个地址只用于运行服务的电脑，不是分享给别人的在线网站。首次启动需要索引模型、提取本地帮助图；右上角可切换中文 / English。

### 4. 生成第一个打印工程

1. 选择整组组合或“只打印配件”，再选尺寸、模块高度、内部配置、顶盖、耗材和喷嘴。
2. 点击“检查配件和排板”，核对缺文件/尺寸警告、源文件、整文件打印数量、支撑和五金。先解决阻止导出的错误。
3. 点击“保存待打印任务”，在待打印任务中点“生成 P1S 3MF”，等到“工程就绪 · 待切片”。
4. macOS 可以点“在 Bambu Studio 打开”。也可以到 `skills/vault-print-planner/assets/app/output/job-任务编号/` 找到 `.3mf`，在 Studio 中**作为项目打开**。Windows/Linux 需用这种手动方式，自动打开按钮目前只适用于 macOS。
5. 核对 P1S、喷嘴、实际耗材、打印板、AMS 槽位、支撑和首层留量；逐盘切片后自行发送。工具不会自动启动打印。
6. 实物完成后到“总体规划与打印进度”填写完成套数。只完成部分打印板时先写备注，生成工程不等于打印完成。

### 重启、更新与常见问题

- 在服务终端按 **Ctrl+C** 停止。下次进入同一个工具目录，只需重跑启动命令，不必每次重新创建虚拟环境。
- 任务保存在 `skills/vault-print-planner/assets/app/print-jobs/`，进度在 `print-progress.json`，工程在 `output/`。更换或升级工具目录前先备份；不同解压副本的记录是分开的。
- **找不到 Python / 版本过低：**安装 Python 3.11+ 后重开终端。**找不到 requirements.txt：**先进入正确的工具目录。
- **缺少 Python 包：**用启动时同一个 `.venv` Python 重跑 pip 安装。安装依赖需要联网，平常本地规划使用离线模式。
- **找不到 01. DRAWERS / STL：**选择完整解压后的模型根目录；云盘占位文件要先下载到本机。
- **Profile check failed：**完成 Studio 向导并启用 P1S、喷嘴及 PLA/PETG 预设。自检会显示搜索的预设目录；便携版、Flatpak 或特殊安装路径尚未验证。
- **端口占用：**改用 `--port 8767`，浏览器也改为 `http://127.0.0.1:8767/planner.html`。**无法连接：**检查终端是否仍在运行，以及输出的网址和报错。
- **帮助图片缺失：**将匹配的原版 PDF 放到模型根目录后重启。**零件放不下/缺文件：**核对尺寸和模型版本，不要为塞进打印板而缩放装配零件。
- 服务仅用于本机，没有远程登录认证，不要暴露到公网。

**验证记录（2026-10-23）：**从公开 GitHub 重新下载 ZIP，解压到全新目录，在 macOS 的新 Python 3.13 虚拟环境中安装，使用本地已购买的模型及现有 Studio 预设测试。选型、配件、保存、3MF 导出及归档结构、进度记录、删除恢复和英文网页通过；增强后的自检在有预设时通过，在无预设时正确提示。Windows/Linux 命令已提供，但**尚未在对应系统实测**。这次没有进行实物打印或最终切片路径验证。

## 界面预览

以下为使用示例组合拍摄的真实界面，不包含个人打印记录。三维组合是用于理解功能的简化示意，不是可打印模型，也不是经过验证的装配仿真。模型仍需自行购买并在本地使用。

**中文界面：选型与组合预览**

![中文界面、语言切换与简化三维组合预览](interface-zh-CN.jpg)

**英文界面：选型与打开内部预览**

![英文界面与简化三维内部预览](interface-en.jpg)

## 展开选项与查看打印清单

点击层设置上方的 **“展开全部选项”**，可以同时看到模块类型、高度、抽屉分配、内部配置和锁的选项；点击 **“收起选项”** 恢复紧凑的下拉框。可选内容会随尺寸变化。1F / 2F / 4F 表示高度等级，不是抽屉个数；图中示例是 2F 外壳里放两个 1F 抽屉。

![展开模块类型、高度、抽屉分配和内部配置选项](options-expanded.jpg)

选好组合、耗材和喷嘴后，点击 **“检查配件和排板”**，向下查看：

| 检查内容 | 可以看到什么 |
| --- | --- |
| 完整打印零件清单 | 对应 STL 文件、数量、尺寸、缩略图、支撑标记和源文件说明。数量按完整文件计算，一个文件可能已包含一对零件。 |
| 耗材与喷嘴 | 整个任务选择 PLA / PETG 和 0.4 / 0.6 mm 喷嘴；目前不会自动为每个零件推荐不同材料，实际耗材型号需在 Studio 中核对。 |
| 是否适合打印机 | 针对当前支持的 P1S 做初步几何排板，提示缺失文件或放不下的零件；不代表适配所有打印机，也不代表最终打印路径已经验证。 |
| 分盘与五金 | 每盘对应的文件，以及需要另买的螺丝等五金名称和数量；清单随选型变化。 |
| 相关说明 | 尺寸命名、堆叠与装配参考、源文件说明、支撑标记及开打前检查提醒；说明书从本地文件读取。 |

**检查示例：** S3、2F 外壳、两个 1F 抽屉、网格顶盖，选择 PETG 和 0.4 mm 喷嘴，得到 14 类零件、27 个整文件打印实例、初步 3 盘。此处用于展示功能，不是所有组合通用的清单，也不是已经验证可直接开打的工程。

![耗材和喷嘴选择，以及初步零件与排板检查结果](print-check.jpg)

![对应打印文件、数量、尺寸及支撑提示](parts-list.jpg)

示例列出 **M4 × 14 mm 螺栓 8 颗**。购买前仍需按对应说明书核对头型、长度和装配要求，不能只凭简写清单选商品。逐盘在 Bambu Studio 切片后，检查实际起始线、brim、支撑、首层和警告。

![需要另购的五金数量及展开的逐盘文件清单](hardware-plates.jpg)

## 模型购买、本地部署与说明书

**本工具不提供、不上传、不分发 VAULT 模型文件。每位使用者需要自行向设计师或授权渠道购买模型，并遵守模型许可。** 将购买的文件下载、解压到自己的电脑，启动时通过 `--archive` 指向该本地文件夹。本工具的 AGPL 开源许可不包含 VAULT 模型的使用或分发权。

模型及含模型几何数据的文件都应保留在本地，包括 STL、STEP、3MF、转换后的网格、打印工程和模型压缩包，不得上传到本仓库或放进发布安装包。规划器读取本地模型进行预览、配件选择和工程生成，不需要把模型上传到 GitHub。

说明书可以用于选型、打印和装配参考，需要时读取使用者本地的说明书。如果权利人允许转载，也可以将说明书作为参考资源附带；使用本地说明书和公开转载说明书是两回事。目前安装包尚未附带第三方说明书。

## 安装 skill

建议先按上方步骤跑通独立网页。skill 文件夹也自带 `requirements.txt`；如果只安装该文件夹，请在其中创建虚拟环境并安装依赖，再运行 `scripts/launch.py`。

把 `skills/vault-print-planner` 整个文件夹复制到 `~/.codex/skills/`（或自己的 `$CODEX_HOME/skills/`），重新开始会话后使用 `$vault-print-planner`。

例如：“用 $vault-print-planner 选一组 M5 抽屉，另外补两套底板，并检查打印板前缘挤出线。”

## 打印边界

导出的 3MF 是待检查的工程，不是已经验证可开打的指令。当前打包版补充了保守的前缘和板边留量；仍需检查实际起始 G-code、brim、支撑、材料预设及 AMS 对应关系。大件可能需要手动排板或分盘，不自动缩放。简化装配图不是精确装配仿真。

原本一次打印中，小配件与前缘预挤出线重叠，因此 skill 明确要求把“几何放得下”和“实际首层路径无冲突”分开核对。已保存的历史工程不会自动套用新的留量。

## 常见问题

**这是模型下载，还是打印规划工具？** 这是针对已购买 VAULT 模型的规划工具，不分发 STL 模型库。它把选型对应到本地文件，并生成可编辑工程。

**可以用于拓竹 P1S 和 Bambu Studio 吗？** 支持 P1S、0.4 / 0.6 mm 喷嘴及 PLA / PETG 的初步规划。导出 3MF 后需要在 Bambu Studio 检查和切片；它不是切片器，也不会自动发送打印。

**必须使用 Codex 吗？** 独立网页不需要 Codex 或 ChatGPT 订阅。需要助手协助规划时再安装可选 skill。

**可以只补打 Gridfinity 底板或锁吗？** 可以使用“只打印配件”，按箱体尺寸选择兼容文件，不必重新打印整个抽屉。它不是通用 Gridfinity 模型生成器。

**Windows 和 Linux 可以用吗？** 已提供操作命令，但目前仅在 macOS 做过完整安装流程测试，请先阅读验证范围和限制。

## 来源与许可

应用基于 [marcelfarres/vault-configurator](https://github.com/marcelfarres/vault-configurator) 的下载版本修改，遵循 [GNU AGPL v3](LICENSE)。本仓库增加中文规划入口、配件模式、删除恢复、完成记录、组合预览、skill 说明及保守 P1S 留边。无原仓库 Git 历史，不能声称它是正式 GitHub fork 或某个已核实 commit。

Three.js 保留其 `vendor/three/LICENSE`。VAULT 模型、说明书及品牌属于 USSA Design，不在本仓库授权范围内。本工具非 USSA Design 或 Bambu Lab 官方产品。设计师的耗材统计未附带，空数据文件仅用于启动；最终重量/时间以切片器为准。

打印记录、输出工程、缓存、原始模型和个人路径仅保存在本地，并由 .gitignore 排除。
