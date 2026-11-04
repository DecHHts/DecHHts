# Hi, I'm HE YUXUAN 👋

集成电路方向本科生，主攻**数字 IC 设计与全流程实现**（RTL → 综合 → 布局布线 → 签核）。
课余用 AI 工具把一些小想法做成 App 和插件。喜欢旅行，梦想走遍世界。

📫 christopherhyx@outlook.com

---

## 🔬 数字集成电路 · 主要方向

### [function_gen](https://github.com/DecHHts/SCUT_BEng_IC_Program)：从一行公式做到一张通过签核的版图

$$y = \frac{a \cdot b \cdot \cos(2\pi c / 4096)}{(a + d) \cdot 4096}$$

课程设计。在 0.18 µm 工艺、200 MHz 下实现上式，完整走通 RTL 到 GDSII 的数字流程，并通过 DRC / LVS 和三个工艺角的时序签核。

| | |
| --- | --- |
| **架构** | 乘法、余弦查表、除数准备三路并行流水；12 级恢复余数除法与"乘余弦"合并在同一段流水里，省掉一个独立乘法器；累加用进位保留形式。总延迟 18 拍 |
| **结果** | 102 376 组向量全部通过，最大误差 1.891 LSB（要求 ±4）；6377 个单元 / 1251 个触发器；三个工艺角无时序违例；LVS `CORRECT`，天线 0 违例 |
| **工具** | VCS / Verdi · Design Compiler · Formality · IC Compiler II · Calibre · PrimeTime |

做的过程中自己定位并解决的问题：

- **DRC 报几万处闩锁违例**：读规则原文发现这套库的单元不自带阱接触，需在布局前按间隔插入专门的接触单元
- **天线检查两个工具结论不一致**：把 Calibre 规则换算成 ICC2 设置；输入端口线网没有泄放路径，逐个加保护二极管
- **LVS 几十个器件对不上**：综合在同一模块里生成了 `N12` 和 `n12`，Verilog 区分大小写而 SPICE 不区分
- **ICC2 与 PrimeTime 对端口路径差半纳秒**：根因在输入延迟约束与时钟树后端口参考时钟延迟的处理差异
- **寄生参数三个工艺角用了同一份文件**：从三份 SPEF 大小完全一样发现脚本按文件名挑错了文件

仓库分两个分支：`main` 是**题目版**（题目、流程骨架、验收 testbench，可以当练习做），`solution` 是参考实现。
含网表、时序报告和签核结果的完整工作目录因涉及工艺库受限数据，放在私有仓库，可应要求展示。

### [Crypto-MCU](https://github.com/DecHHts/Crypto-MCU)：进行中

2026 年 9 月开始的密码学 MCU 项目，目前搭好了 RTL / 综合 / 后端 / 签核的目录与流程骨架。

---

## 🤖 [VibeCoding](https://github.com/DecHHts/VibeCoding) · AI 协作作品

> 以下项目由我提出想法、定义需求、拆分里程碑并测试验收，**代码主要由 AI（Claude）生成**。
> 它们展示的是产品想法和用 AI 把想法落地的能力，不代表我在这些语言上的编程功底。

| 项目 | 一句话 | 平台 |
| --- | --- | --- |
| [Notchi · 刘海仔](https://github.com/DecHHts/VibeCoding/tree/main/Notchi) | 住在 MacBook 刘海里的小宠物：眼睛跟着鼠标转，悬停展开成迷你游戏机 | macOS · SwiftUI / SpriteKit |
| [世遗漫游](https://github.com/DecHHts/VibeCoding/tree/main/WorldHeritage) | 基于 UNESCO 世界遗产名录的旅行 App：热力图、国家地图、目的地转盘、端侧 AI 推荐 | iOS · SwiftUI / MapKit |
| [region-undo](https://github.com/DecHHts/VibeCoding/tree/main/region-undo) | 选中一段代码按 `Ctrl+Z`，只撤回选区内的修改；支持 VSCode、JetBrains、Vim/Neovim、Sublime | 编辑器插件 |
| [HealthLab 体检记](https://github.com/DecHHts/VibeCoding/tree/main/HealthLab) | 拍照识别医院化验单，按项目记录历次结果和趋势，数据只存本地 | iOS · Vision / SwiftData |

---

## 🛠 个人配置

- [dotfiles](https://github.com/DecHHts/DecHHts/tree/main/dotfiles)：我的 macOS 终端与编辑器配置（zsh、Starship、Neovim、Ghostty），用 GNU Stow 管理
