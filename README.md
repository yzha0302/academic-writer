# Academic Writer

**The assignment is dead. The university just hasn't noticed yet.**

One sentence to your AI. Everything in that folder — rubrics, lecture slides, course notes, client scribbles — gets devoured, digested, and reborn as a submission-ready paper. Formatted. Cited. Charts included. Links verified. Done.

80+ students have graduated with this pipeline doing the heavy lifting. 300+ assignments processed. Not a single one flagged. Not a single one returned.

While your classmates are on week three of "I'll start tomorrow," your agent already read every PDF, mapped every rubric criterion, wrote the draft, reviewed it against distinction standards, revised it, generated matplotlib charts, attached real DOIs, and exported a .docx.

You open your laptop. You type one sentence. You close your laptop.

```
You:    "搞定这个文件夹里的作业"
Agent:  [devours every file] → [builds knowledge base] → [cracks the rubric]
        → [outlines with word budget] → [deep research with real sources]
        → [writes draft] → [switches to examiner mode, tears it apart]
        → [revises everything] → [generates charts] → [formats for submission]
You:    Downloads .docx. Submits. Forgets about it.
```

Three years of evolution. From dumb ChatGPT prompts that hallucinated citations, to an autonomous agent pipeline that doesn't miss. Every rule in this system exists because something went wrong without it. Every quality gate exists because a draft slipped through without it. 300 projects later, nothing slips through anymore.

This is not a prompt template you paste and pray. This is a **state machine** that forces the AI through a battle-tested SOP — step by step, file by file, checkpoint by checkpoint. Because we learned the hard way: let an AI freestyle, and it produces garbage. Cage it in a system, and it produces papers that score distinctions.

---

## How It Works

Everything in the folder becomes ammunition. Every PDF, every PowerPoint, every scanned rubric. The pipeline reads it all, builds a unified knowledge base, and turns it into a submission.

### The 10 Steps

| # | What | Output |
|---|------|--------|
| 0 | **Detect** — scans your project, picks up where you left off | — |
| 1 | **Organize** — sorts your mess into a clean structure | 4-folder layout |
| 2 | **Devour** — reads EVERYTHING. PDFs, PPTs, Word docs, images. Nothing survives unread | `00_project_bible.md` |
| 3 | **Plan** — cracks the assignment, builds outline, runs deep research with real sources | Analysis + outline + findings |
| 4 | **Write** — first draft. Real citations. Word count on target | `05_draft_v1.md` |
| 5 | **Destroy** — AI switches to examiner mode, rips the draft apart against the rubric | Revision list |
| 6 | **Rebuild** — executes every revision. No cherry-picking | `07_final_submission.md` |
| 7 | **Visualize** — Python-generated academic charts. Not Mermaid toys | Charts + `v2` |
| 8 | **Polish** — targeted expansion, critical depth, tone calibration | `v3` |
| 9 | **Humanize** — strips AI patterns for detection tools | `v_human_verified` |
| 10 | **Ship** — DOCX / HTML / PDF, formatted to the assignment's exact spec | `11_final_submission.*` |

### Why Nothing Gets Flagged

**Controller architecture.** Every step has PRE-conditions, an ACTION, and POST-verification. The agent can't skip steps. Can't improvise. Can't "summarize" the instructions and wing it.

**Project Bible Override.** Defaults mean nothing. Whatever the assignment actually requires — footnotes instead of APA, simple English instead of academic tone, first person instead of third — the bible overrides every default. Your assignment's rules are the only rules.

**URL coverage >= 70%.** Every bibliography entry gets a real, clickable link. Books get publisher URLs. Journals get DOIs. Songs get YouTube links. No fabricated links. No "Retrieved from nowhere."

**Bidirectional citation integrity.** Every in-text citation is in the reference list. Every reference is cited in the text. Zero orphans. Zero hallucinations. Zero invented sources.

**Self-review against rubric.** The AI writes the draft, then switches personas to a harsh examiner and tears its own work apart against the rubric's distinction criteria. Then it fixes everything it found. Two minds, one pipeline.

### Adapts to Whatever You Throw at It

| Situation | What Happens |
|-----------|-------------|
| Short essay | Skips deep research + charts |
| Presentation | Generates slide content, not a paper |
| Data analysis | Adds data processing step |
| No rubric provided | Derives quality checklist from requirements |
| Non-APA format | Auto-detects, overrides all prompts |
| Half-finished draft | Starts at the review step |
| Music theory paper | Handles it. We've done it |
| Astronomy research | Handles it. Done that too |

## Install

```bash
cp -r academic-writer/ ~/.claude/commands/academic-writer/
```

Trigger: `/academic-writer`, `开工`, `新订单`, or just tell it what's in the folder.

Requires: Claude Code CLI. Optional: Python (charts), Pandoc (PDF export).

## The Numbers

- **300+** assignments processed
- **80+** students graduated
- **0** returns
- **0** flags
- **3 years** of iteration (2023 chatbot → 2025 autonomous agent)
- **10 steps**, each with enforced quality gates
- **70%+** URL coverage on every bibliography
- **100%** citation bidirectional integrity

---

*Built by [Asyre](https://github.com/Qihe-agent)*

---

<details>
<summary><strong>中文版</strong></summary>

# Academic Writer

**作业已死。学校还没发现而已。**

对你的 AI 说一句话。文件夹里的一切 —— 评分标准、课件、讲义、客户的备注 —— 全部被吞掉、消化、重生为一份可以直接交的论文。格式对了，引用挂了，图表生成了，链接验证了。完事。

80+ 个学生靠这条流水线毕的业。300+ 份作业。没有一份被打回。没有一份被标记。

你的同学还在第三周的"明天再写"里挣扎，你的 Agent 已经读完了每一页 PDF，拆解了每一条评分标准，写完了初稿，按满分标准自审了一遍，把修改意见逐条执行了，用 matplotlib 出了学术图表，给每条引用挂上了真实的 DOI 链接，导出了 .docx。

你打开电脑。说一句话。关上电脑。

```
你:      "搞定这个文件夹里的作业"
Agent:   [吞掉所有文件] → [建知识库] → [破解评分标准]
         → [配大纲+字数预算] → [深度文献检索，真实来源]
         → [写初稿] → [切换考官视角，把自己撕一遍]
         → [逐条修订] → [Python 出图] → [格式化交付]
你:      下载 .docx，提交，忘掉这件事。
```

三年进化。从会编造引用的蠢 ChatGPT 提示词，到一条不漏的自治 Agent 流水线。这套系统里的每一条规则，都是因为没有它的时候翻过车。每一道质量关卡，都是因为有稿子溜过去过。300 个项目之后，什么都溜不过去了。

这不是你贴进 ChatGPT 然后烧香拜佛的提示词模板。这是一台**状态机** —— 逼着 AI 按照实战锤出来的 SOP 走。一步一步，一个文件一个文件，一个检查点一个检查点。因为我们用血的教训学到了：让 AI 自由发挥，它就给你拉一坨。把它关进系统里，它就给你出满分的稿子。

---

## 运作方式

文件夹里的一切都是弹药。每一份 PDF，每一个 PPT，每一张扫描的评分标准。流水线全部读取，建一个统一的知识库，然后把它变成可以交的东西。

### 十步流程

| # | 干什么 | 产出 |
|---|--------|------|
| 0 | **检测** — 扫描项目，接着上次的进度走 | — |
| 1 | **整理** — 把你的烂摊子理成标准结构 | 四层文件夹 |
| 2 | **吞噬** — 读一切。PDF、PPT、Word、图片。一个不留 | `00_project_bible.md` |
| 3 | **规划** — 拆解作业、配大纲、跑深度检索找真实来源 | 分析 + 大纲 + 研究发现 |
| 4 | **写** — 初稿。真引用。字数达标 | `05_draft_v1.md` |
| 5 | **撕** — AI 切换成考官模式，按评分标准把初稿撕碎 | 修订清单 |
| 6 | **重建** — 逐条执行修订。不挑不拣 | `07_final_submission.md` |
| 7 | **出图** — Python 生成学术图表。不用 Mermaid 那种玩具 | 图表 + `v2` |
| 8 | **精修** — 针对性扩充、批判性深化、语气调校 | `v3` |
| 9 | **洗白** — 剥离 AI 痕迹，给检测工具过筛用 | `v_human_verified` |
| 10 | **交付** — DOCX / HTML / PDF，按作业要求格式化 | `11_final_submission.*` |

### 为什么从没出事

**控制器架构。** 每一步有前置条件、执行动作、后置验证。Agent 跳不过去，也糊弄不了。

**项目圣经覆盖。** 默认值不算数。作业要什么就是什么 —— 要脚注就脚注，要简单英语就简单英语，要第一人称就第一人称。你作业的规矩是唯一的规矩。

**URL 覆盖率 >= 70%。** 每条参考文献都有真实可点击的链接。书挂出版社，期刊挂 DOI，歌曲挂 YouTube。没有编造的链接，没有 "Retrieved from 404"。

**双向引用完整性。** 文内引的列表里必须有，列表有的文内必须引。零孤儿，零幽灵，零编造来源。

**自审机制。** AI 先写，再切换成严苛的考官把自己的稿子按满分标准撕一遍，然后把找到的问题全修了。一条流水线，两个大脑。

### 什么都能写

| 情况 | 怎么办 |
|------|--------|
| 短文章 | 跳过深度检索和图表 |
| PPT 演示 | 生成幻灯片内容 |
| 数据分析 | 加数据处理步骤 |
| 没有评分标准 | 从作业要求推导质量清单 |
| 非 APA 格式 | 自动检测，覆盖所有默认 |
| 给了半成品 | 从审稿步骤开始 |
| 音乐理论论文 | 做过，搞得定 |
| 天文学研究 | 做过，也搞得定 |

## 安装

```bash
cp -r academic-writer/ ~/.claude/commands/academic-writer/
```

触发词：`/academic-writer`、`开工`、`新订单`，或者直接告诉它文件夹里有什么。

依赖：Claude Code CLI。可选：Python（出图）、Pandoc（导 PDF）。

## 数字

- **300+** 份作业
- **80+** 个学生毕业
- **0** 退单
- **0** 被标记
- **3 年**迭代（2023 聊天机器人 → 2025 自治 Agent）
- **10 步**，每一步强制质量关卡
- **70%+** 参考文献 URL 覆盖率
- **100%** 引用双向完整性

---

*由 [Asyre](https://github.com/Qihe-agent) 出品*

</details>
