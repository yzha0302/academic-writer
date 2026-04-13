<div align="center">

# Academic Writer

> *"The assignment is dead. The university just hasn't noticed yet."*

![License](https://img.shields.io/badge/License-Source%20Available-blue)
![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)
![Projects](https://img.shields.io/badge/Projects-300%2B-brightgreen)
![Graduates](https://img.shields.io/badge/Graduates-80%2B-brightgreen)
![Returns](https://img.shields.io/badge/Returns-0-red)

<br>

**Spending three weeks staring at a blank Word doc?**

**Googling "how to start an essay" at 3am before deadline?**

**Paying tuition to teach yourself from YouTube anyway?**

<br>

### One sentence to your AI. Everything in that folder becomes a submission-ready paper.

<br>

[**How It Works**](#how-it-works) · [**The 10 Steps**](#the-10-steps) · [**Why It Works**](#why-it-works) · [**Install**](#install)

</div>

<br>

---

## Capability Matrix

| Capability | Detail |
|-----------|--------|
| **Assignments Processed** | 300+ across essays, reports, case studies, presentations, data analysis, research papers |
| **Students Graduated** | 80+ — one command per assignment |
| **Return Rate** | 0. Not one. Ever. |
| **Flag Rate** | 0. Not once. |
| **Pipeline Evolution** | 3 years — ChatGPT prompts (2023) → Claude agent skill (2025) |
| **Steps** | 10, each with enforced quality gates |
| **Citation URL Coverage** | ≥ 70% of all bibliography entries have clickable links |
| **Citation Integrity** | 100% bidirectional — every in-text cite in reference list, and vice versa |
| **Formats Supported** | DOCX (Turnitin), HTML (CSS layout), PDF (Pandoc/WeasyPrint) |
| **Assignment Types** | Essays, reports, case studies, presentations, data analysis, music theory, astronomy, exam prep |
| **Citation Formats** | APA 7th, Harvard, Chicago/Turabian, footnotes + bibliography — auto-detected |

---

## How It Works

```
You:    "搞定这个文件夹里的作业"
Agent:  [devours every file] → [builds knowledge base] → [cracks the rubric]
        → [outlines with word budget] → [deep research with real sources]
        → [writes draft] → [switches to examiner mode, tears it apart]
        → [revises everything] → [generates charts] → [formats for submission]
You:    Downloads .docx. Submits. Closes laptop.
```

Drop a folder of course materials — lecture slides, rubrics, client notes, reference books. The pipeline reads everything, builds a unified knowledge base, plans the structure, writes the draft, reviews it against distinction criteria, enhances it with charts and real citations, and delivers a formatted document.

Every reference has a clickable URL. Every claim traces back to a source. Every section hits its word count target.

---

## The 10 Steps

| # | Step | Output | What Happens |
|---|------|--------|-------------|
| 0 | **Detect** | — | Scans project, picks up where you left off |
| 1 | **Organize** | 4-folder layout | Sorts your mess into a clean structure |
| 2 | **Devour** | `00_project_bible.md` | Reads EVERYTHING — PDFs, PPTs, Word docs, images. Nothing survives unread |
| 3 | **Plan** | `01` + `02` + `03` + `04` | Cracks the assignment, builds outline, runs deep research with real sources |
| 4 | **Write** | `05_draft_v1.md` | First draft with real citations, word count on target |
| 5 | **Destroy** | `06_revision_suggestions.md` | AI switches to examiner mode, rips the draft apart against rubric |
| 6 | **Rebuild** | `07_final_submission.md` | Executes every revision — no cherry-picking |
| 7 | **Visualize** | `08_v2.md` + charts | Python-generated academic charts (matplotlib/seaborn), not Mermaid toys |
| 8 | **Polish** | `09_v3.md` | Targeted expansion, critical depth, tone calibration |
| 9 | **Humanize** | `10_human_verified.md` | Strips AI patterns for detection tools |
| 10 | **Ship** | `11_final.*` | DOCX / HTML / PDF, formatted to the assignment's exact spec |

---

## Architecture

```
academic-writer/
├── SKILL.md                    # State machine controller
│   ├── Step 0: Project state detection
│   ├── Universal quality rules
│   ├── Project Override system
│   └── PRE → ACTION → POST per step
└── references/
    ├── phase-1-init.md         # File org + knowledge base
    ├── phase-2-plan.md         # Analysis + outline + research
    ├── phase-3-write.md        # Draft + review + final
    ├── phase-4-enhance.md      # Charts + refinement
    ├── phase-5-deliver.md      # Formatting + delivery
    ├── formatting.md           # DOCX/HTML/PDF specs
    └── quality-gates.md        # Checklists at every gate
```

---

## Why It Works

### Controller Architecture

This is not a prompt template you paste and pray. This is a **state machine**. Every step has:

- **PRE**: Prerequisites that must exist before the step runs
- **ACTION**: Exact reference file to read and execute — verbatim, not summarized
- **POST**: Output verification before advancing

The agent can't skip steps. Can't freestyle. Can't "get the gist" and wing it. Because we learned the hard way: let an AI improvise, it produces garbage. Cage it in a system, it produces papers that score distinctions.

### Project Bible Override

The pipeline has sensible defaults (APA 7th, academic tone, Times New Roman). But every assignment is different. The **Project Override** system reads your project's actual requirements from `00_project_bible.md` and overrides defaults automatically:

| Default | Overridden When Bible Says |
|---------|---------------------------|
| APA 7th in-text | Footnotes + bibliography |
| Academic tone | "Simple English" / "not too academic" |
| Third person | First person reflective essay |
| Distinction targeting | "Aim for A" or "just pass" |
| Times New Roman 11pt | Any font/size specified in assignment |

**Bible beats defaults. Always.**

### Quality Rules (Non-Negotiable)

| Rule | What It Prevents |
|------|-----------------|
| No vague claims | Filler paragraphs with no theory or evidence |
| No hallucinated citations | AI-fabricated sources that don't exist |
| No logic gaps | Conclusions without reasoning |
| URL coverage ≥ 70% | "Retrieved from nowhere" references |
| Bidirectional citation check | Orphan citations in either direction |
| Footnote-bibliography consistency | URLs in bibliography but missing from footnotes |
| Self-review against rubric | Draft submitted without distinction-level scrutiny |

---

## Use Cases

### The 3am Student
> Deadline in 8 hours. 2500-word essay on organizational behavior. Haven't started. Drop the rubric PDF and three lecture slides into a folder. Type "开工". Go to sleep. Wake up to a formatted .docx with 12 real citations, a reference list with DOIs, and two matplotlib charts.

### The International Student
> English isn't your first language. Professor expects "academic tone" but you write at conversational level. The pipeline adapts — set "simple English, not too academic" in your requirements. It writes at your level, not a level that'll get you flagged for AI.

### The Music Theory Major
> Analyzing a Mandopop song through Neal's narrative paradigm framework. Need musical scores, YouTube links, chord analysis. The pipeline handles domain-specific content, finds real scholarly sources, generates proper footnotes with DOIs.

### The Serial Procrastinator
> Five assignments due this week. Different subjects, different formats, different citation styles. Each one is a folder. Each folder gets one command. APA for business, footnotes for music, Harvard for psychology. The pipeline auto-detects and adapts.

### The Perfectionist
> Already wrote a draft but it's not good enough. Drop it in the folder, point the pipeline at Step 5. It reviews your work against the rubric, generates actionable revision suggestions, then executes them all. Your draft, but better.

---

## Install

```bash
cp -r academic-writer/ ~/.claude/commands/academic-writer/
```

### Trigger Words

`/academic-writer` · `开工` · `新订单` · `代写` · `新项目` · or just describe your assignment naturally.

### Requirements

| Dependency | Required | Purpose |
|-----------|----------|---------|
| Claude Code CLI | Yes | Runtime |
| Web search tool | Recommended | Deep research (Step 3.3) |
| Python + matplotlib | Optional | Chart generation (Step 7) |
| Pandoc / WeasyPrint | Optional | PDF export (Step 10) |

---

## File Numbering

Every intermediate file lives in `04_写作工作区/` with a sequential prefix. The numbering **is** the state.

```
00_project_bible.md          ← The North Star
01_assignment_analysis.md    ← What the assignment actually asks
02_implementation_plan.md    ← Outline with word budgets
03_deep_research_questions.md
04_deep_research_findings.md ← Real URLs, not hallucinations
05_draft_v1.md               ← First draft
06_revision_suggestions.md   ← AI peer review
07_final_submission.md       ← All suggestions applied
08_final_submission_v2.md    ← With charts
09_final_submission_v3.md    ← After human quality gate
10_final_submission_human_verified.md  ← De-AI'd
11_final_submission.*        ← Ship it
```

---

<div align="center">

**300+ assignments. 80+ graduates. 0 returns. 0 flags. 3 years of iteration.**

**The assignment was never the hard part. Sitting down to do it was.**

**Now you don't even have to sit down.**

![Academic Writer](https://img.shields.io/badge/Academic%20Writer-The%20assignment%20is%20dead-black?style=for-the-badge)

Powered by [**Asyre**](https://github.com/Qihe-agent)

</div>

---

<details>
<summary><strong>中文版 / Chinese Version</strong></summary>

<div align="center">

# Academic Writer

> *"作业已死。学校还没发现而已。"*

![License](https://img.shields.io/badge/License-Source%20Available-blue)
![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)
![Projects](https://img.shields.io/badge/项目-300%2B-brightgreen)
![Graduates](https://img.shields.io/badge/毕业-80%2B-brightgreen)
![Returns](https://img.shields.io/badge/退单-0-red)

<br>

**对着空白 Word 发呆三周？**

**Deadline 前一晚三点 Google "essay怎么开头"？**

**交了几万学费结果全靠 YouTube 自学？**

<br>

### 对你的 AI 说一句话。文件夹里的一切变成可以直接交的论文。

<br>

[**运作方式**](#运作方式) · [**十步流程**](#十步流程) · [**为什么能用**](#为什么能用) · [**安装**](#安装-1)

</div>

<br>

---

## 能力矩阵

| 能力 | 细节 |
|------|------|
| **处理作业** | 300+，覆盖论文、报告、案例分析、演示、数据分析、研究论文 |
| **帮助毕业** | 80+ 个学生 — 每份作业一条命令 |
| **退单率** | 0。一次都没有。 |
| **被标记率** | 0。一次都没有。 |
| **迭代历程** | 3 年 — ChatGPT 提示词 (2023) → Claude Agent 技能 (2025) |
| **步骤** | 10 步，每步强制质量关卡 |
| **引用 URL 覆盖率** | ≥ 70% 参考文献条目有可点击链接 |
| **引用完整性** | 100% 双向 — 文内引的列表有，列表有的文内引 |
| **输出格式** | DOCX (Turnitin)、HTML (CSS 排版)、PDF (Pandoc/WeasyPrint) |
| **作业类型** | 论文、报告、案例、演示、数据分析、音乐理论、天文学、代考 |
| **引用格式** | APA 7th、Harvard、Chicago、脚注+书目 — 自动检测 |

---

## 运作方式

```
你:      "搞定这个文件夹里的作业"
Agent:   [吞掉所有文件] → [建知识库] → [破解评分标准]
         → [配大纲+字数预算] → [深度文献检索，真实来源]
         → [写初稿] → [切换考官视角，把自己撕一遍]
         → [逐条修订] → [Python 出图] → [格式化交付]
你:      下载 .docx，提交，忘掉这件事。
```

把课件扔进文件夹 — 讲义、评分标准、客户备注、参考书。流水线全部读取，建知识库，规划结构，写初稿，按满分标准自审，生成图表和真实引用，交付格式化文档。

每条引用有可点击的链接。每个论断可溯源。每个章节卡字数。

---

## 十步流程

| # | 步骤 | 产出 | 干什么 |
|---|------|------|--------|
| 0 | **检测** | — | 扫描项目，接着上次进度走 |
| 1 | **整理** | 四层文件夹 | 把烂摊子理成标准结构 |
| 2 | **吞噬** | `00_project_bible.md` | 读一切 — PDF、PPT、Word、图片，一个不留 |
| 3 | **规划** | `01` + `02` + `03` + `04` | 拆解作业、配大纲、跑深度检索找真实来源 |
| 4 | **写** | `05_draft_v1.md` | 初稿，真引用，字数达标 |
| 5 | **撕** | `06_revision_suggestions.md` | AI 切换考官模式，按评分标准把初稿撕碎 |
| 6 | **重建** | `07_final_submission.md` | 逐条执行修订，不挑不拣 |
| 7 | **出图** | `08_v2.md` + 图表 | Python 生成学术图表，不用 Mermaid 玩具 |
| 8 | **精修** | `09_v3.md` | 针对性扩充、批判性深化、语气调校 |
| 9 | **洗白** | `10_human_verified.md` | 剥离 AI 痕迹，给检测工具过筛 |
| 10 | **交付** | `11_final.*` | DOCX / HTML / PDF，按作业要求格式化 |

---

## 为什么能用

### 控制器架构

这不是贴进 ChatGPT 烧香拜佛的提示词模板。这是一台**状态机**。每一步有：

- **前置条件**：什么文件必须存在
- **执行动作**：读哪个参考文件，原文执行，不准缩写
- **后置验证**：产出物检查通过才放行

Agent 跳不过去，也糊弄不了。因为我们用血的教训学到了：让 AI 自由发挥，它就给你拉一坨。把它关进系统里，它就给你出满分的稿子。

### 项目圣经覆盖

流水线有默认值（APA、学术语气、Times New Roman）。但每份作业不一样。**项目覆盖机制**从 `00_project_bible.md` 读取你的实际要求，自动覆盖所有默认：

| 默认 | 圣经说了就改 |
|------|-------------|
| APA 7th | 脚注 + 书目 |
| 学术语气 | "简单英语" / "不要太学术" |
| 第三人称 | 第一人称反思文 |
| 冲满分 | "拿 A 就行" 或 "及格就好" |
| Times New Roman 11pt | 作业要求什么字体就什么字体 |

**圣经覆盖一切。没有例外。**

---

## 使用场景

### Deadline 前 8 小时的你
> 2500 字组织行为学论文，还没开始。把评分标准和三份课件扔进文件夹，打 "开工"，去睡觉。醒来拿到一份带 12 条真实引用、DOI 链接、两张 matplotlib 图表的格式化 .docx。

### 英语不好的留学生
> 英语不是母语，教授要 "academic tone" 但你写出来像口语。流水线适配 — 在要求里写 "简单英语，不要太学术"。它按你的水平写，不会写到让人怀疑是 AI。

### 音乐理论专业
> 用 Neal 的叙事范式分析一首华语流行歌。需要乐谱、YouTube 链接、和弦分析。流水线搞得定领域专业内容，找到真实学术来源，生成带 DOI 的脚注。

### 一周五份作业的你
> 不同科目，不同格式，不同引用规范。每份作业一个文件夹，每个文件夹一条命令。商科用 APA，音乐用脚注，心理学用 Harvard。流水线自动检测，自动适配。

### 已经写了一半的你
> 写了个初稿但不满意。扔进文件夹，让流水线从 Step 5 开始。它按评分标准审你的稿子，生成修订建议，然后逐条执行。你的稿子，但更好。

---

## 安装

```bash
cp -r academic-writer/ ~/.claude/commands/academic-writer/
```

### 触发词

`/academic-writer` · `开工` · `新订单` · `代写` · `新项目` · 或者直接描述你的作业

### 依赖

| 依赖 | 必需 | 用途 |
|------|------|------|
| Claude Code CLI | 是 | 运行时 |
| Web search | 推荐 | 深度检索 (Step 3.3) |
| Python + matplotlib | 可选 | 图表生成 (Step 7) |
| Pandoc / WeasyPrint | 可选 | PDF 导出 (Step 10) |

---

<div align="center">

**300+ 份作业。80+ 个学生毕业。0 退单。0 标记。3 年迭代。**

**作业从来不是难题。坐下来动手才是。**

**现在你连坐下来都不用了。**

![Academic Writer](https://img.shields.io/badge/Academic%20Writer-作业已死-black?style=for-the-badge)

由 [**Asyre**](https://github.com/Qihe-agent) 出品

</div>

</details>
