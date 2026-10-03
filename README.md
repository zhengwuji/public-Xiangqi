# TCHESS（个人维护版）

TCHESS 是一款支持 uci 和 ucci 协议引擎的跨平台象棋界面程序。

本仓库基于 [sojourners/public-Xiangqi](https://github.com/sojourners/public-Xiangqi) V1.9 维护，合入了社区 PR 改进，并配置了 **GitHub Actions 自动构建**：每次推送代码（README.md 修改除外）都会自动编译 Windows EXE 并发布到 [Releases](https://github.com/zhengwuji/public-Xiangqi/releases)，Release 说明自动写入中文更新内容。

# 功能

+ 加载引擎（uci / ucci 协议）
+ 对弈（人机 / 引擎互殴：**红黑双方可选不同引擎对战**）
+ 分析（multipv 多主变显示）
+ 棋谱（pgn / xqf / cbr / txq 读写、管理、分支、变招）
+ 连线（识别其他程序窗口 / 图片中的棋盘，支持深色棋盘）
+ 开局库（云端 / 本地 xqb / bh / pf）

# 中文更新内容

## 2026-10-04 自定义构建（基于上游 V1.9）

1. 合入 [PR #77](https://github.com/sojourners/public-Xiangqi/pull/77)：**红黑方可选不同引擎对战**，各自独立设置线程数、哈希大小；工具栏红/黑按钮位置对调；分析模式固定使用红方引擎；
2. 合入 [PR #76](https://github.com/sojourners/public-Xiangqi/pull/76)：**深色棋盘识别修复**（相位 / DPI / 多棋盘分组 / 残局补棋 / 引擎路径回退），新增 VinYolo5 识别模型（yolo5-vin.onnx）；
3. 新增 GitHub Actions 自动构建：推送代码 → 自动编译 EXE → 自动发布 Release（附中文更新说明）；
4. 建议（非自动）配套更新引擎：Pikafish 2026-09-06，见下方"引擎下载"。

## 上游 V1.9（2026.08.01）

1. 支持复制粘贴文本棋谱
2. 支持读取 xqf、cbr 棋谱
3. 修复 pgn 棋谱读取问题
4. 棋谱列显示注释标记
5. 支持拖拽修改变招列表顺序
6. 支持主题及箭头颜色配置
7. 增加搜索固定节点数配置

## 上游历史版本（摘要）

- **V1.8**（2026.03.01）：棋谱管理 / 打开 / 保存 / 编辑 / 浏览 / 分支；multipv 多主变着法显示；引擎兼容性、中文棋谱翻译、将军判定修复；开局库加载查询优化
- **V1.7**（2026.01.16）：变招功能；xqb 格式开局库；置顶弹窗修复
- **V1.6**（2024.10.20）：窗口置顶；连线算法优化；Windows 后台模式；升级 yolov11 模型
- **V1.5 及更早**：编辑局面、图片解析导入导出、自适应棋盘等

# 使用说明

## 下载运行

1. 到 [Releases](https://github.com/zhengwuji/public-Xiangqi/releases) 下载 `TChess-Windows.zip`；
2. 解压后运行 `TChess.exe`（自带 Java 运行时，无需安装 JDK）。

## 引擎下载（重要）

Release 包**不含象棋引擎**，需要自行下载并放入 `model` 目录：

+ **Pikafish（魚皮，最强开源引擎）**：https://github.com/official-pikafish/Pikafish/releases ，下载最新版压缩包，把 `Pikafish-Windows-x86-64-universal.exe`（新版权威通用版，自动适配 CPU）和 `pikafish.nnue` 放入 `model` 目录，nnue 需放在程序根目录或 model 目录；
+ 其他 uci/ucci 引擎（象眼 ElephantEye 等）同样放入任意目录即可。

## 添加引擎

菜单"引擎" → 引擎管理 → 添加：填写名称、选择引擎 exe 路径、选择协议（uci 或 ucci）。

## 红黑双引擎对战（本版新功能）

1. 至少添加一个引擎后，界面右上"红方引擎 / 黑方引擎"两个下拉框分别选择引擎，各自设置线程数与哈希（MB）；
2. 两边选**不同引擎** + 工具栏"自动走棋"= 引擎自动对打，用于评测引擎强弱；
3. 两边选**同一引擎**、设置不同线程 / 哈希 / 时间 = 对比配置对棋力的影响；
4. 人机对弈时只有行棋方的引擎参与思考；"分析"（B 按钮）固定使用红方引擎，建议把红方设为最强配置。

## 连线（识别其他窗口 / 图片）

菜单"连线" → 选择识别方式 → 把目标框住即可自动识别棋盘。识别不了深色棋盘时，使用本版新增的 VinYolo5 模型（连线设置中切换）。

## 更多说明

详细使用文档见 [MANUAL.md](MANUAL.md)。

# 本地编译

+ JDK 21、Maven 3.9+
+ `mvn package` 生成 jar；或直接推送代码，由 Actions 自动构建 EXE
+ 仅本地快速验证编译：`javac --release 21 -cp <已有fat jar> $(find src -name "*.java" ! -name "module-info.java")`

# 交流反馈

上游原作 Q群：1094058444（上游作者 sojourners）

# 声明

本项目基于 [GPLv3](LICENSE) 协议开源，你可以自由下载、使用、复制修改，但需遵守开源协议内容，禁止未经授权用于商业用途！
