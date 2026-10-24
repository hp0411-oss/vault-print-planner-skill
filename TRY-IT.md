# Try VAULT Print Planner v0.1.0

English | [简体中文](#简体中文)

## Plan your USSA VAULT build before you print

I built this local planner while figuring out which parts to print for my own modular storage. It brings configuration, illustrative assembly previews, source-file lists, initial plate-fit checks, hardware notes and print progress into one place. It exports a P1S 3MF project for Bambu Studio; you still inspect, slice and send the print yourself.

- Free and open source. English and Chinese interface.
- Run locally with Python 3.11+ and Bambu Studio. No Codex or ChatGPT subscription required for the website.
- Optional Codex skill for assisted use.
- **Purchase the VAULT models separately. No paid models are included.** Unofficial; not affiliated with USSA Design or Bambu Lab.
- macOS installation/export smoke-tested. Windows and Linux instructions are available but have not been tested on those systems. Assembly previews are illustrative, not engineering validation.

[Download v0.1.0](https://github.com/hp0411-oss/vault-print-planner-skill/releases/tag/v0.1.0) · [Setup instructions](README.md#start-here-installation-and-first-use) · [Report a problem](https://github.com/hp0411-oss/vault-print-planner-skill/issues/new/choose)

Built on [marcelfarres/vault-configurator](https://github.com/marcelfarres/vault-configurator), under AGPL-3.0. This version adds the bilingual planner workflow, accessory-only selection, task recovery and print-progress records.

## Looking for the first 3–5 testers

Do you already own the matching VAULT model archive? Please try this short workflow:

1. Follow the README from a fresh download. Tell us your OS, Python version, Studio version, printer and nozzle.
2. Configure one small build or an accessory for a body you own.
3. Run the checks. Can you identify every required file and hardware item?
4. Save the task, export 3MF and open it in Studio. Check part count, printer/nozzle and layout. **A physical print is optional.**
5. Report where you got stuck and one improvement you would most like to see. Windows/Linux installation feedback is particularly welcome.

Please do not attach purchased STLs, 3MFs containing paid models, access codes or unredacted personal paths. Share a cropped error screenshot or minimal text instead. Feedback is public; use the issue templates.

## 简体中文

### 在打印前，规划好你的 USSA VAULT 组合

我在规划自己的组合收纳箱时做了这个本地工具。它把选型、示意组装预览、源文件清单、初步打印板适配检查、五金说明和打印进度放在一起，并可导出 P1S 的 3MF 项目到 Bambu Studio。导出以后，仍需自己检查、切片和发送打印。

- 免费开源，中英文界面；本地运行，需要 Python 3.11+ 和 Bambu Studio。
- 网页不需要 Codex 或 ChatGPT 订阅；也提供可选的 Codex Skill。
- **VAULT 模型需要自行购买，项目不包含付费模型。** 非 USSA Design 或 Bambu Lab 官方产品。
- 已验证 macOS 安装和导出基础流程；Windows/Linux 尚待实际测试。组装预览只是示意，不是工程验证。

[下载 v0.1.0](https://github.com/hp0411-oss/vault-print-planner-skill/releases/tag/v0.1.0) · [中文安装说明](README.zh-CN.md) · [反馈问题](https://github.com/hp0411-oss/vault-print-planner-skill/issues/new/choose)

基于 [marcelfarres/vault-configurator](https://github.com/marcelfarres/vault-configurator)，遵循 AGPL-3.0；本版本增加中英文规划流程、单独配件选择、任务恢复和打印进度记录。

### 招募首批 3～5 位试用者

如果你已经购买了对应的 VAULT 模型，欢迎从全新下载开始尝试：安装 → 选一个小组合或单独配件 → 检查文件和五金清单 → 保存任务 → 导出 3MF → 在 Studio 中核对。无需实际打印，也能提供有用反馈。

请告诉我们系统、Python / Studio 版本、打印机和喷嘴，以及卡住的步骤和最希望改进的一点。尤其欢迎 Windows/Linux 用户。

反馈是公开的。请勿上传付费 STL、包含模型的 3MF、设备访问码或未遮盖的私人路径。
