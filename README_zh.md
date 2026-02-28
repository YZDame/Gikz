# Gikz

[![npm version](https://img.shields.io/npm/v/gikz)](https://www.npmjs.com/package/gikz)
[![license](https://img.shields.io/npm/l/gikz)](LICENSE)
[![node](https://img.shields.io/node/v/gikz)](https://nodejs.org)
[![downloads](https://img.shields.io/npm/dm/gikz)](https://www.npmjs.com/package/gikz)

**[English](README.md)**

**将 GeoGebra 导出的 TikZ 代码清洗为简洁、可读的 LaTeX 代码。**

一个零依赖的 Node.js CLI 工具，将 GeoGebra 冗长的 TikZ 输出转为干净、手写风格的代码，直接用于 `.tex` 文件。同时支持从 `.ggb` 和 `.xml` 文件直接转换。

> 衍生自 [GGB-Tikz-Code-Filter](https://github.com/By990920/GGB-Tikz-Code-Filter)，作者 [By990920](https://github.com/By990920)。基于 GPL-2.0 协议。

## 功能特性

- 去除冗余样式（`line width`、颜色定义、`scriptsize` 包裹等）
- 坐标四舍五入至 3 位小数（可关闭）
- 用命名标签替换原始坐标（`(A)`、`(B)` …）
- 根据点的几何位置智能放置标签
- 转换线型（`dash pattern=...` → `dashed`）
- 支持：点、线段、圆、椭圆、圆弧、扇形、角度标记、函数图像、贝塞尔曲线、文本标签
- **直接从 `.ggb`（GeoGebra 工程文件）和 `.xml` 文件转换**
- 输出为 `tikzpicture` 片段或完整的 `standalone` 文档
- 批量处理 & 标准输入/输出管道

## 安装

```bash
# 全局安装（推荐）
npm install -g gikz

# 或直接运行
npx gikz export.txt

# 或 clone 后使用
git clone https://github.com/YZDame/gikz.git
cd gikz
node gikz.js export.txt
```

## 支持的输入格式

| 格式 | 说明 |
|---|---|
| `.txt` / `.tex` | GeoGebra TikZ 导出文件（清洗模式） |
| `.ggb` | GeoGebra 工程文件（直接转换） |
| `.xml` | GeoGebra XML 文件（直接转换） |

## 使用方法

```bash
# 清洗 TikZ 导出文件
gikz export.txt

# 直接转换 GeoGebra 工程文件
gikz figure.ggb

# 转换 GeoGebra XML 文件
gikz geogebra.xml

# 输出 standalone 文档 — 可直接用 pdflatex 编译
gikz -s export.txt

# 写入文件
gikz -s -o clean.tex figure.ggb

# 批量处理 — 多个文件输出到目录
gikz fig1.ggb fig2.txt fig3.xml -o output/

# 管道输入
cat export.txt | gikz -s > clean.tex

# 不输出点和标签
gikz --no-points --no-labels export.txt

# 保留原始坐标精度
gikz --no-round export.txt
```

## 选项

| 参数 | 说明 |
|---|---|
| `-s`, `--standalone` | 输出完整的 `standalone` LaTeX 文档 |
| `-t`, `--tikzonly` | 仅输出 `tikzpicture` 片段（默认） |
| `--no-points` | 不输出点标记（`\draw[fill=black]...`） |
| `--no-labels` | 不输出点标签（`\node...`） |
| `--no-round` | 保留原始坐标精度 |
| `-o`, `--output <path>` | 写入文件（批量时为目录） |
| `-h`, `--help` | 显示帮助 |

## 示例

**输入**（GeoGebra 导出）：
```latex
\draw [line width=2pt,color=rvwvcq] (-2.75,2.1)-- (-4.89,-2.06);
\draw [fill=rvwvcq] (-2.75,2.1) circle (2.5pt);
\draw[color=rvwvcq] (-2.6468416958718426,2.3645220512615386) node {$A$};
```

**输出**（Gikz）：
```latex
\coordinate (A) at (-2.75,2.1);
\draw (A) -- (B);
\draw[fill=black] (A) circle (1pt);
\node [above] at (A) {$A$};
```

## AI 编程助手集成

Gikz 包含 AI 编程助手的技能文件：

| 助手 | 文件 | 用法 |
|---|---|---|
| Claude Code | `CLAUDE.md` | 在工作区中自动检测 |
| OpenAI Codex | `AGENTS.md` | 在工作区中自动检测 |

这些文件让 AI 助手学会如何在你的项目中调用 Gikz 来清洗 TikZ 代码。

## 环境要求

- Node.js ≥ 14

无其他依赖。

## 许可证

GPL-2.0 — 见 [LICENSE](LICENSE)。

衍生自 [GGB-Tikz-Code-Filter](https://github.com/By990920/GGB-Tikz-Code-Filter)，作者 [By990920](https://github.com/By990920)。
