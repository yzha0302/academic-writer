# Phase 1: Initialization — Full Prompts

Execute these prompts as written. They have been tested across 90+ projects.

---

## Step 2 Prompt — Knowledge Base Construction

Send this prompt to yourself and execute it faithfully:

> 你是一名严谨的资料入库专员。请对目录下的所有文件进行全量深度读取。
> 规则如下：
>
> 1. **全类型覆盖**：PDF/Word/PPT/Code/Image 等所有文件均不放过。**特别注意**：涉及 PDF/PPT 中的关键图表/图片，必须调用 AI Vision 能力进行语义描述，不可忽略。
> 2. **区别处理**：
>    - **普通资料**（如课件、参考书、无关范文）：进行要点提炼与缩减优化 (Summarize & Optimize)，仅保留核心知识点，避免冗余。
>    - **核心三要素**（1. 作业要求、2. 用户个性化需求）：必须**原封不动、逐字摘录** (Verbatim Extraction)。
>    - **评分标准 (Rubric)**：执行 **"两步法"**：
>      1. **Raw Extraction**: 先原文摘录最高分档 (Distinction/High Distinction) 的所有描述。
>      2. **Optimization**: 将其转化为可执行的 **"Self-Audit Checklist"** (包含 Knowledge, Logic, Theory, Limitations, Delivery 五大维度)，置入 Project Bible。
> 3. **输出目标**：构建一份 `04_写作工作区/00_project_bible.md` (编号00-基础库)，将上述"核心三要素"置顶整合。
> 4. **基准原则 (Baseline Principle)**：**优先查阅 Project Bible**。若发现 Bible 内容不够详细（如具体数据或图表细节），**必须**回溯原始文件（PDF/PPT）进行查证，确保信息准确度。

### Execution Details

1. **Binary File Handling**: `.docx` and `.pptx` files are ZIP archives. If the Read tool can't display them, extract text programmatically (e.g., Python `zipfile` → read `word/document.xml` or parse HTML exports). Never skip a file because it's binary.

2. **Tiered Reading**:
   - **Tier 1 (Verbatim)**: Full extraction of Requirements & Client Notes
   - **Tier 1.5 (Rubric Optimization)**: Extract highest grade band → rewrite as Quality Barrier Checklist (Is it specific? Is it critical? etc.)
   - **Tier 2 (Summary)**: Quick scan of Lecture Notes → extract Key Concepts
   - **Visual Processing**: For PDF/PPT figures and tables, describe them semantically

2. **Build `04_写作工作区/00_project_bible.md`**:
   - `# CORE PILLARS` — verbatim requirements, rubric checklist, client notes
   - `# KNOWLEDGE BASE` — summarized course content

3. **Anchor Rule**: All subsequent steps must include: "Prioritize `00_project_bible.md`. If details are missing, verify with original PDFs."

### Why This Matters

A single unified context file prevents token loss across conversation turns. Without it, the AI "forgets" requirements mid-conversation and starts hallucinating or missing rubric criteria. This step alone prevents 70% of quality issues.
