# GitHub 文献管理规范（供 Codex 使用）

本文档用于指导 Codex 在 GitHub 仓库中辅助管理论文、阅读笔记、BibTeX、复现实验与索引文件。  
当用户要求“整理文献”“新增论文”“生成阅读笔记”“更新索引”“维护 bibliography”“创建 issue/PR”时，请优先遵循本文档。

---

## 1. 仓库目标

本仓库用于长期管理学术文献，目标包括：

1. 系统化保存论文元数据、阅读笔记、主题分类与复现记录。
2. 让每篇论文都有可追踪的状态：待读、在读、已读、已讨论、复现中、已复现。
3. 支持按研究方向、年份、方法、数据集、任务类型检索论文。
4. 将 Zotero / BibTeX 文献库与 GitHub 笔记、代码、实验结果连接起来。
5. 支持个人或课题组通过 Issue、Project、Pull Request 进行协作。

---

## 2. Codex 的工作原则

Codex 在修改仓库时应遵循以下原则：

1. **不要破坏已有结构**：新增内容前先检查现有目录、README、模板、索引文件。
2. **优先补全索引**：新增论文笔记后，必须同步更新相关 `README.md`、主题索引或总索引。
3. **一篇论文一个笔记文件**：除非用户明确要求合并综述，否则每篇论文对应一个 Markdown 笔记。
4. **元数据优先准确**：标题、作者、年份、会议/期刊、链接、BibTeX key 不确定时标注 `TODO`，不要编造。
5. **PDF 谨慎处理**：不要主动把受版权保护的 PDF 加入公开仓库；如需管理 PDF，建议只在私有仓库或 Git LFS 中处理。
6. **保持可 diff**：每次改动应小而清晰，方便 Pull Request 审查。
7. **不要无故重命名已有文件**：除非用户要求或现有命名明显不符合规范。
8. **所有自动生成内容必须可人工编辑**：不要生成难以维护的大段机器格式。

---

## 3. 推荐目录结构

```text
papers/
├── README.md                         # 总索引
├── CODEX_LITERATURE_MANAGEMENT.md    # 本规范
├── library.bib                       # BibTeX 文献库，可由 Zotero / Better BibTeX 导出
├── .gitattributes                    # Git LFS 配置，可用于 PDF
├── .gitignore
│
├── topics/                           # 按研究主题组织
│   ├── llm/
│   │   ├── README.md
│   │   └── papers/
│   ├── rag/
│   │   ├── README.md
│   │   └── papers/
│   ├── agent/
│   │   ├── README.md
│   │   └── papers/
│   ├── multimodal/
│   │   ├── README.md
│   │   └── papers/
│   └── evaluation/
│       ├── README.md
│       └── papers/
│
├── notes/
│   ├── paper-template.md             # 单篇论文笔记模板
│   ├── survey-template.md            # 综述笔记模板
│   └── weekly-reading-log.md         # 每周阅读记录
│
├── bib/
│   ├── README.md
│   ├── by-topic/
│   └── by-year/
│
├── pdfs/                             # 可选；公开仓库不建议存放版权 PDF
│   └── README.md
│
├── code/                             # 论文复现、实验脚本
│   ├── README.md
│   └── reproductions/
│
├── slides/                           # 组会或汇报材料
│   └── README.md
│
└── scripts/                          # 自动化脚本
    ├── validate_metadata.py
    ├── generate_index.py
    └── check_bibtex.py
```

如果现有仓库结构不同，Codex 不应强制重构；应在现有结构上最小化修改。

---

## 4. 文件命名规范

### 4.1 论文笔记文件名

推荐格式：

```text
YYYY-short-title.md
```

示例：

```text
2017-attention-is-all-you-need.md
2020-retrieval-augmented-generation.md
2023-react-synergizing-reasoning-and-acting.md
```

命名规则：

1. 全部小写。
2. 空格替换为连字符 `-`。
3. 删除冒号、问号、引号等特殊字符。
4. 标题过长时保留 5–8 个关键词。
5. 同年同名冲突时追加作者姓氏或会议名。

---

## 5. 单篇论文笔记模板

当用户要求新增论文笔记时，Codex 应使用以下模板。

```markdown
# Paper Title

## Metadata

- **Year**:
- **Authors**:
- **Venue**:
- **Paper Link**:
- **Code Link**:
- **Project Page**:
- **BibTeX Key**:
- **Tags**:
- **Status**: to-read
- **Added Date**:
- **Last Updated**:

## One-line Summary

TODO: 用一句话说明这篇论文解决的问题和核心贡献。

## Problem

这篇论文试图解决什么问题？

## Motivation

为什么这个问题重要？已有方法有什么不足？

## Method

简要说明方法结构、关键模块、训练或推理流程。

## Contributions

1. TODO
2. TODO
3. TODO

## Experiments

### Datasets

- TODO

### Baselines

- TODO

### Metrics

- TODO

### Main Results

- TODO

## Strengths

- TODO

## Limitations

- TODO

## Reproducibility Notes

- 是否有代码：
- 是否有数据：
- 复现难点：
- 环境依赖：
- 预计复现成本：

## Relation to My Work

这篇论文和当前研究、项目或代码仓库有什么关系？

## Follow-up Papers

- [ ] TODO

## Reading Notes

### Key Ideas

- TODO

### Important Details

- TODO

### Questions

- TODO

## Citation

```bibtex
TODO
```
```

---

## 6. 综述类笔记模板

当用户要求“整理某一方向论文”“做 literature review”“总结一个主题”时，使用此模板。

```markdown
# Survey: Topic Name

## Scope

本综述覆盖的研究问题、方法类别和时间范围。

## Key Questions

1. 这个方向解决什么核心问题？
2. 主流方法有哪些？
3. 主要数据集和评价指标是什么？
4. 当前瓶颈是什么？
5. 哪些论文值得优先阅读？

## Paper Map

| Paper | Year | Venue | Category | Status | Note |
|---|---:|---|---|---|---|
| TODO | TODO | TODO | TODO | TODO | TODO |

## Taxonomy

### Category 1

- TODO

### Category 2

- TODO

### Category 3

- TODO

## Timeline

| Year | Development |
|---:|---|
| TODO | TODO |

## Datasets and Benchmarks

| Dataset / Benchmark | Task | Used By | Notes |
|---|---|---|---|
| TODO | TODO | TODO | TODO |

## Open Problems

- TODO

## Recommended Reading Order

1. TODO
2. TODO
3. TODO
```

---

## 7. README 总索引规范

仓库根目录 `README.md` 应至少包含：

```markdown
# Literature Repository

## Research Topics

- [LLM](topics/llm/README.md)
- [RAG](topics/rag/README.md)
- [Agent](topics/agent/README.md)
- [Multimodal](topics/multimodal/README.md)
- [Evaluation](topics/evaluation/README.md)

## Priority Reading List

| Priority | Paper | Year | Topic | Status | Note |
|---:|---|---:|---|---|---|
| 1 | TODO | TODO | TODO | to-read | TODO |

## Recently Added

| Paper | Year | Topic | Added Date | Note |
|---|---:|---|---|---|
| TODO | TODO | TODO | TODO | TODO |

## Status Legend

- `to-read`: 待读
- `reading`: 在读
- `read`: 已读
- `discussed`: 已讨论
- `reproducing`: 复现中
- `reproduced`: 已复现
- `archived`: 暂不关注
```

当新增论文时，Codex 应更新：

1. 根目录 `README.md` 的 `Recently Added` 或 `Priority Reading List`。
2. 对应主题目录的 `README.md`。
3. 必要时更新 `library.bib`。
4. 如果有复现实验，更新 `code/README.md` 或相关复现目录。

---

## 8. 主题索引规范

每个 `topics/<topic>/README.md` 推荐包含：

```markdown
# Topic Name

## Overview

本主题关注的问题、典型方法和应用场景。

## Core Papers

| Paper | Year | Venue | Status | Note |
|---|---:|---|---|---|
| TODO | TODO | TODO | TODO | TODO |

## Reading Order

1. TODO
2. TODO
3. TODO

## Method Taxonomy

- TODO

## Open Problems

- TODO
```

---

## 9. BibTeX 管理规范

### 9.1 BibTeX key 格式

推荐格式：

```text
authorYYYYkeyword
```

示例：

```text
vaswani2017attention
lewis2020retrieval
yao2023react
```

规则：

1. 使用第一作者姓氏。
2. 加年份。
3. 加标题关键词。
4. 不使用空格和特殊符号。
5. 与 `library.bib` 保持一致。

### 9.2 新增 BibTeX 时

Codex 应检查：

1. 是否已有相同标题或相同 DOI/arXiv ID。
2. BibTeX key 是否冲突。
3. 年份、作者、venue 是否完整。
4. 是否需要在论文笔记的 `Citation` 部分同步。

如果信息不确定，使用：

```bibtex
note = {TODO: metadata needs verification}
```

不要编造 DOI、页码、会议名或出版社信息。

---

## 10. Issue 管理规范

### 10.1 新增待读论文 Issue

标题格式：

```text
[Paper] Paper Title
```

Issue 内容模板：

```markdown
## Paper

- Title:
- Year:
- Link:
- Topic:
- Priority:
- Suggested by:

## Why Read This?

TODO

## Tasks

- [ ] Add BibTeX entry
- [ ] Create paper note
- [ ] Read paper
- [ ] Summarize method
- [ ] Summarize experiments
- [ ] Update topic README
- [ ] Discuss in reading group
- [ ] Decide whether to reproduce

## Status

to-read
```

### 10.2 复现类 Issue

标题格式：

```text
[Reproduce] Paper Title
```

内容模板：

```markdown
## Goal

复现这篇论文的哪个结果、模块或实验？

## Paper

- Note:
- Code:
- Dataset:

## Tasks

- [ ] Check official code
- [ ] Set up environment
- [ ] Prepare dataset
- [ ] Run baseline
- [ ] Run target method
- [ ] Compare metrics
- [ ] Document results
- [ ] Update paper note

## Expected Output

- 复现实验脚本
- 实验日志
- 结果表格
- README 说明
```

---

## 11. Pull Request 规范

Codex 创建或修改 PR 时，描述应包含：

```markdown
## Summary

- 新增/修改了哪些论文笔记
- 更新了哪些索引
- 是否修改了 BibTeX
- 是否涉及复现实验代码

## Checklist

- [ ] 文件命名符合规范
- [ ] 元数据完整或已标记 TODO
- [ ] 主题 README 已更新
- [ ] 根 README 已更新
- [ ] BibTeX key 无冲突
- [ ] 未向公开仓库加入受版权保护的 PDF
```

---

## 12. 标签规范

推荐 GitHub Labels：

```text
paper
reading
survey
bibtex
reproduction
code
dataset
high-priority
low-priority
llm
rag
agent
multimodal
evaluation
to-read
reading
read
discussed
reproducing
reproduced
archived
```

Codex 创建 Issue 或整理任务时，应优先复用这些标签。

---

## 13. Project 看板规范

推荐列：

```text
Backlog
To Read
Reading
Discussed
Reproducing
Done
Archived
```

状态流转：

```text
Backlog → To Read → Reading → Discussed → Done
                         ↘ Reproducing → Done
```

---

## 14. 自动化脚本建议

Codex 可以在 `scripts/` 下辅助创建脚本，但应保持简单、可读。

### 14.1 `generate_index.py`

用途：

1. 扫描 `topics/**/papers/*.md`。
2. 读取每篇论文的 Metadata。
3. 自动生成主题 README 中的论文表格。
4. 自动生成根 README 中的 Recently Added 列表。

### 14.2 `validate_metadata.py`

用途：

1. 检查每篇论文是否包含必要字段。
2. 检查状态值是否合法。
3. 检查 BibTeX key 是否缺失。
4. 检查文件名是否符合规范。

### 14.3 `check_bibtex.py`

用途：

1. 检查 `library.bib` 是否存在重复 key。
2. 检查常见字段是否缺失。
3. 检查笔记中的 BibTeX key 是否能在 `library.bib` 中找到。

---

## 15. 状态字段规范

允许的状态值：

```text
to-read
reading
read
discussed
reproducing
reproduced
archived
```

不要新增同义状态，例如：

```text
todo
done
finished
completed
pending
```

除非用户明确要求扩展状态体系。

---

## 16. 标签字段规范

论文笔记中的 Tags 推荐使用简短小写词：

```text
llm
rag
agent
multimodal
evaluation
alignment
reasoning
retrieval
benchmark
dataset
survey
reproduction
```

不要混用大小写，例如同时出现 `LLM`、`llm`、`LargeLanguageModel`。

---

## 17. 新增论文的标准流程

当用户要求“添加这篇论文”时，Codex 应按以下顺序操作：

1. 识别论文标题、链接、年份、作者、venue、代码地址。
2. 判断所属主题目录。
3. 创建论文笔记文件：
   ```text
   topics/<topic>/papers/YYYY-short-title.md
   ```
4. 填写 Metadata。
5. 添加 One-line Summary；不确定则写 TODO。
6. 添加或更新 `library.bib`。
7. 更新主题 `README.md`。
8. 更新根目录 `README.md`。
9. 如有复现需求，创建 `code/reproductions/<paper-key>/README.md`。
10. 总结本次改动。

---

## 18. 整理一个主题的标准流程

当用户要求“整理 RAG 方向论文”或“帮我梳理某主题文献”时，Codex 应：

1. 搜索现有相关论文笔记。
2. 归并重复论文。
3. 按年份、方法类别、任务或数据集建立 taxonomy。
4. 更新 `topics/<topic>/README.md`。
5. 必要时新增 `topics/<topic>/survey.md`。
6. 输出推荐阅读顺序。
7. 标出缺失信息和 TODO。

---

## 19. 复现实验管理规范

每个复现实验目录推荐结构：

```text
code/reproductions/<bibtex-key>/
├── README.md
├── environment.yml
├── requirements.txt
├── scripts/
├── configs/
├── results/
└── logs/
```

`README.md` 模板：

```markdown
# Reproduction: Paper Title

## Goal

## Paper

- Note:
- Code:
- Dataset:

## Environment

## Commands

## Results

| Setting | Metric | Paper Result | Reproduced Result | Difference |
|---|---:|---:|---:|---:|
| TODO | TODO | TODO | TODO | TODO |

## Notes

## Problems

## Next Steps
```

---

## 20. PDF 管理规范

1. 公开仓库：不要上传受版权保护的 PDF。
2. 私有仓库：可以在 `pdfs/` 中存放，但建议使用 Git LFS。
3. 开放获取论文：可以保存链接，是否保存 PDF 由用户决定。
4. 每篇笔记中优先保存：
   - Paper Link
   - arXiv Link
   - DOI
   - Project Page
   - Code Link

推荐 `.gitattributes`：

```text
*.pdf filter=lfs diff=lfs merge=lfs -text
```

---

## 21. Codex 回答用户时的格式

完成仓库修改后，Codex 应用简洁中文说明：

```markdown
已完成：

- 新增论文笔记：`...`
- 更新主题索引：`...`
- 更新总索引：`...`
- 更新 BibTeX：`...`

仍需确认：

- TODO: venue
- TODO: official code link
```

如果有不确定信息，必须明确列出，不要隐藏。

---

## 22. 不应做的事情

Codex 不应：

1. 在没有来源的情况下编造论文元数据。
2. 把所有论文混进一个巨大的 Markdown 文件。
3. 未经用户要求大规模重构目录。
4. 未经确认删除论文笔记、BibTeX 条目或复现实验。
5. 在公开仓库提交受版权保护的 PDF。
6. 用不稳定、不可读的自动生成格式替代人工可维护笔记。
7. 在同一 PR 中混合大量无关改动。

---

## 23. 推荐初始化任务

如果仓库是空的，Codex 可以建议或创建：

```text
README.md
CODEX_LITERATURE_MANAGEMENT.md
notes/paper-template.md
notes/survey-template.md
topics/llm/README.md
topics/rag/README.md
topics/agent/README.md
topics/multimodal/README.md
topics/evaluation/README.md
library.bib
.gitattributes
.gitignore
```

初始 `.gitignore` 可包含：

```text
.DS_Store
__pycache__/
*.pyc
.env
.venv/
.ipynb_checkpoints/
```

---

## 24. 推荐给用户的工作流

用户可以用以下方式让 Codex 协助管理文献：

```text
请按照 CODEX_LITERATURE_MANAGEMENT.md，把这篇论文加入 RAG 主题，并更新 README 和 library.bib。
```

```text
请检查 topics/llm 下所有论文笔记的 metadata 是否完整，并列出缺失项。
```

```text
请把 topics/rag 的论文按方法类别重新整理索引，不要移动原文件。
```

```text
请为 @vaswani2017attention 创建复现实验目录，并写一个 README 模板。
```

```text
请根据现有笔记生成一份 agent 方向的 survey.md。
```

---

## 25. 最小维护标准

每次新增论文至少完成：

1. 一个论文笔记文件。
2. 一个 BibTeX key。
3. 一个主题归类。
4. 一个状态字段。
5. 主题 README 更新。
6. 根 README 更新。

如果无法完成，必须在修改总结中列出原因和 TODO。
