# LaTeX Agent `SKILL`（arXiv ML/AI 综述论文）

[English](README.md) · 简体中文

> [!NOTE]
> 本仓库实现了一个 `.codex` `SKILL`：一个端到端、以 issue 驱动的工作流，用于生成面向 arXiv.org 的 **ML/AI 综述论文 IEEEtran 双栏 LaTeX 项目**，并包含**已验证的 BibTeX 引用**。
> 通过 `.claude` → `.codex` 提供实验性的 Claude Code 支持。

## 这里有什么

- **端到端工作流**：issue-driven 论文写作（生成 plan → 用户确认 → 生成 issues CSV → 按 issue 写作 → rhythm refinement（节奏润色） → QA/编译）。
- **主要 `SKILL`**：`arxiv-paper-writer` 位于 `.codex/skills/arxiv-paper-writer/SKILL.md`。
- **辅助脚本**：脚手架、规划、校验、编译位于 `.codex/skills/arxiv-paper-writer/scripts/`。
- **示例输出**：`example/` 中的一篇生成论文（包括 `example/main.pdf`）。

> [!NOTE]
> 该工作流受“issue-driven development”启发，参考项目 [`appautomaton/agent-designer`](https://github.com/appautomaton/agent-designer)。

## 快速开始（两条 prompt → 可编译的示例论文）

本仓库的 `example/v0-single-SKILL` 论文通过 **两条用户 prompt** 激活 `arxiv-paper-writer` `SKILL` 生成。

### Prompt 1（开始论文）

```text
write a review article for arxiv that is about SOTA generative image models
```

在第一条 prompt 之后，agent 会：
- 做一次初步文献检索，
- 搭建章节框架，
- 提供几个候选标题供你选择，
- 并生成 `plan/<timestamp>-<slug>.md`，其中包含澄清问题与草案计划。

> [!TIP]
> 打开生成的 `plan/` markdown 文件并回答澄清问题，以便引导范围、标题与覆盖内容。

### Prompt 2（授权 agent 决策并继续）

```text
I will let you choose the best title and with the topics and inclusion of material that you see the best fit
```

在这个示例里，第二条 prompt 刻意写得比较模糊（并且忽略了 plan 中的问题）。agent 仍会尽力做出选择，并生成一个可以编译成 PDF 的完整 LaTeX 项目。

> [!NOTE]
> 结果见 `example/main.tex`、`example/ref.bib` 和 `example/main.pdf`。

## 环境说明

> [!IMPORTANT]
> 需要已安装并可用的 LaTeX 环境（例如 `pdflatex` + `bibtex`，或 `latexmk`）。

- 已在 macOS 上使用 GPT-5.2（Extra High）测试通过。
