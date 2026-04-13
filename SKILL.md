---
name: academic-writer
description: "Battle-tested academic writing pipeline that transforms course materials into submission-ready assignments through 10 systematic steps. Use this skill whenever the user mentions: 代写, ghostwriting, academic writing, assignment, essay, paper, homework, coursework, 作业, 论文, or wants to go through a structured writing process. Also trigger when the user says '开工', '新订单', '新项目', 'new order', 'start writing', or references any pipeline step (e.g., 'build knowledge base', 'deep research', 'peer review', 'final formatting', '知识库', '大纲', '初稿', '审稿', '终稿', '降AI率', '交付'). This skill handles all academic assignment types — essays, reports, case studies, presentations, data analysis, research papers — adapting the pipeline to each situation while maintaining strict quality standards."
---

# Academic Writer: Assignment Pipeline Controller

This is a **controller**, not a description. Follow these instructions as a state machine — check pre-conditions, execute the step, verify post-conditions, then advance.

The pipeline has been refined across 90+ real projects over several years. The prompts and quality rules exist because they solve real problems. Do not paraphrase or summarize them — execute them as written.

## Step 0: Detect Project State

### 0.1 Find the Project

First, determine where the project is:

1. **If the user provided a path** (e.g., "搞定 /path/to/project") → use that path
2. **If the current directory contains assignment files** (PDFs, .docx, rubrics, 内容.md) → use current directory
3. **If neither** → scan for active projects in the known work area:
   ```bash
   ls ~/Desktop/工作区/代写/业务/外包代写/*/处理区域/
   ```
   List the project folders found and ask the user: "Found these active projects — which one?" If the work area doesn't exist, ask the user for the project path.

### 0.2 Detect Progress

Once you have the project directory, scan it to determine where we are:

```
IF no standard folder structure exists     → Start at Step 1
IF folders exist but no 00_project_bible   → Start at Step 2
IF 00_project_bible exists but no outline  → Start at Step 3
IF outline exists but no draft             → Start at Step 4
IF draft exists but no review              → Start at Step 5
IF review exists but no final              → Start at Step 6
IF final v1 exists but no charts           → Start at Step 7
IF final v2 exists but needs refinement    → Step 8
IF final v3 exists but not de-AI'd         → Step 9
IF human-verified exists                   → Step 10
```

Tell the user: "I've scanned the project. You're at **Step N** — [brief reason]. Ready to proceed?" Wait for confirmation before executing.

If the user names a specific step, verify its prerequisites exist. If they don't, say which files are missing and offer to backfill.

## Adapting to the Situation

Not every project needs all 10 steps. Read the assignment type and adapt:

| Situation | Adaptation |
|-----------|------------|
| Short essay (<1000 words) | Skip Step 3.3 (deep research) and Step 7 (Python charts) |
| Presentation / PPT | Replace Steps 4-6 with slide content generation; Step 10 outputs slides |
| Data analysis assignment | Add a data processing sub-step before Step 4 |
| Exam prep (代考) | Focus on Steps 1-3 (organize + analyze); skip writing pipeline |
| Client provides partial draft | Start at Step 5 (review) with their draft as input |
| No rubric available | Step 2 derives a Self-Audit Checklist from stated requirements instead of rubric |
| Non-APA citation format | Detect format from project bible (footnotes, Harvard, Chicago, etc.) and override all APA references in prompts |
| No images/charts needed | Step 7 copies v1 final to v2 unchanged; skip Python visualization |

The pipeline is the backbone. Adapt it — don't abandon it.

---

## Universal Quality Rules

These rules apply to EVERY step from Step 2 onward. Violating any of these makes the output unacceptable.

### The Quality Barrier (质量阻断)

- **Reject vague claims**: Any statement without a specific theory, model, or evidence from the course materials is filler. Replace it with a concrete reference.
- **Reject hallucinated citations**: Every citation must trace back to `00_project_bible.md` or the original source files. If you can't find the source, don't cite it.
- **Reject ambiguity**: Words like "可能", "大概", "perhaps", "might" are banned in analytical sections. Be precise and anchor to the rubric.
- **Reject logic gaps**: Every argument must follow: `Claim → Evidence → Reasoning → Conclusion`. No jumping from claim to conclusion.

### The Baseline Principle

`00_project_bible.md` is the North Star. Every decision, every paragraph, every citation should be traceable back to it. If the bible is missing detail, go back to the original PDFs — never guess.

### Project Override — Bible Beats Defaults

The prompts in the reference files contain default assumptions (e.g., "academic tone", "APA 7th", "Distinction targeting"). **When `00_project_bible.md` specifies something different, the bible wins.** After completing Step 2, scan the bible for project-specific overrides and carry them through every subsequent step:

| Default in Prompts | Override If Bible Says |
|--------------------|-----------------------|
| 学术语气 (academic tone) | "简单英语" / "not too academic" → use simple, natural language |
| APA 7th in-text | "footnotes + bibliography" / "Harvard" / "Chicago" → use that format |
| 第三人称 (third person) | "first person allowed" / reflective essay → adapt person accordingly |
| Distinction/HD targeting | Specific grade target (e.g., "aim for A") → calibrate depth accordingly |
| Times New Roman 11pt | Any font/size/spacing specified in assignment → use that |
| English | Assignment in another language → write in that language |

This table is not exhaustive. The principle is: **read the bible, check for conflicts with prompt defaults, adapt.** If unsure, ask the user.

### Citation Integrity

- **Detect the required format from `00_project_bible.md`** before writing anything. Common formats: APA 7th (default), Harvard, Chicago/Turabian, footnotes + bibliography. If the project bible or assignment requirements specify a format, use that — do not default to APA.
- **Bidirectional check**: Every citation in the text must appear in the reference list/bibliography. Every reference list entry must be cited in-text. No orphans.
- **URL coverage ≥ 70%**: At least 70% of bibliography/reference list entries must include a clickable URL, DOI, or direct link. Books → use publisher URL, Amazon, or Google Books link. Journal articles → use DOI. Songs/recordings → use YouTube, Spotify, or Apple Music link. "No URL available" is not acceptable for most sources — search for one. Run a count after generating the reference list: if URL coverage < 70%, go back and find missing links before proceeding.

---

## The Pipeline

### Phase 1: Initialization

#### Step 1 — File Architecture

**PRE**: Raw project directory with scattered files
**ACTION**: Scan all files, create standard structure, move files into place:

```
项目根目录/
├── 01_作业要求与评分标准/
│   └── 范例/
├── 02_课件资料/
├── 03_客户额外需求/
└── 04_写作工作区/
    └── DeepResearch/
```

**POST**: All files sorted into folders. Original files stay in root as backup (copy, don't move — safer). Confirm structure with user.

**WHY**: AI needs clean file paths for accurate context. Messy files cause hallucinations and missed requirements.

---

#### Step 2 — Knowledge Base Construction

**PRE**: Standard folder structure from Step 1
**ACTION**: Read `references/phase-1-init.md` § "Step 2 Prompt" and execute it exactly.

The core logic (do not skip any of these):
1. **Full coverage**: Read ALL files — PDF, Word, PPT, images. Use vision for figures/tables.
2. **Tiered processing**:
   - **Tier 1 (Verbatim)**: Assignment requirements + client notes → extract word-for-word
   - **Tier 1.5 (Rubric → Checklist)**: Extract highest grade band → convert to Self-Audit Checklist with 5 dimensions: Knowledge, Logic, Theory, Limitations, Delivery
   - **Tier 2 (Summary)**: Course materials → key concepts only
3. **Output**: `04_写作工作区/00_project_bible.md` with `# CORE PILLARS` (verbatim) + `# KNOWLEDGE BASE` (summarized)

**POST**: `00_project_bible.md` exists. Verify it contains: (1) verbatim requirements, (2) rubric checklist, (3) knowledge base. If any section is empty, go back and re-read the source files.

**WHY**: A unified context file prevents token loss across conversation turns and keeps the AI anchored to real requirements.

---

### Phase 2: Planning

#### Step 3.1 — Assignment Analysis

**PRE**: `00_project_bible.md` exists
**ACTION**: Read `references/phase-2-plan.md` § "Step 3.1 Prompt" and execute it.

You are a professional assignment analyst targeting top marks. Produce:
- Theory mapping (bible theories → assignment questions)
- Logic chains per argument: Claim → Evidence → Reasoning → Conclusion
- Quality barrier enforcement (scan for vague/hallucinated content)
- Distinction-targeting gap analysis

**POST**: `04_写作工作区/01_assignment_analysis.md` exists and contains: 任务拆解 + 结构规划 + 段落级写作指引 + 满分自查表

---

#### Step 3.2 — Outline Configuration

**PRE**: `01_assignment_analysis.md` exists
**ACTION**: Read `references/phase-2-plan.md` § "Step 3.2 Prompt" and execute it.

Build a structured outline with:
- Logical decomposition of all requirements
- Writing points + word count allocation per section
- Topic selection (if applicable) based on material availability and scoring potential

**POST**: `04_写作工作区/02_implementation_plan.md` exists with clear section-by-section breakdown and word counts.

---

#### Step 3.3 — Deep Research

**PRE**: `02_implementation_plan.md` exists
**ACTION**: Read `references/phase-2-plan.md` § "Step 3.3 Prompts" and execute both phases:

**Phase 1 — Question Generation**: Generate 2-5 research questions per outline section.
→ Output: `04_写作工作区/DeepResearch/03_deep_research_questions.md`

**Phase 2 — Research Execution**: AI search or user-provided findings. All findings must include Reference Links / DOIs from authoritative sources (.edu, .gov, major journals).
→ Output: `04_写作工作区/DeepResearch/04_deep_research_findings.md`

**POST**: Both files exist. Findings contain real, verifiable URLs (no fabricated links).

> 🔴 **CHECKPOINT**: Stop here. User must review the outline and research, then confirm "LGTM" before writing begins.

---

### Phase 3: Writing

#### Step 4 — Academic Draft

**PRE**: `02_implementation_plan.md` + `DeepResearch/04_deep_research_findings.md` exist. User has confirmed "LGTM" on the outline.
**ACTION**: Read `references/phase-3-write.md` § "Step 4 Prompt" and execute it.

Key non-negotiables:
- Every major paragraph must contain relevant citations
- APA 7th in-text + reference list with bidirectional consistency
- Check `DeepResearch/` for existing images before using placeholders
- Follow the outline's word count allocation strictly

**POST**: `04_写作工作区/05_draft_v1.md` exists. Run a self-check: (1) citation count matches paragraph count, (2) word count within 10% of outline allocation, (3) no unsupported claims.

---

### Phase 4: Review & Iteration

#### Step 5 — Deep Review

**PRE**: `05_draft_v1.md` exists
**ACTION**: Read `references/phase-3-write.md` § "Step 5 Prompt" and execute it.

Switch to "thesis review mentor" role. Compare draft against Distinction criteria. Produce actionable revision instructions (imperative verbs only — "Add...", "Replace...", "Strengthen...").

**POST**: `04_写作工作区/06_revision_suggestions.md` exists with numbered, actionable items.

---

#### Step 6 — Final Draft

**PRE**: `05_draft_v1.md` + `06_revision_suggestions.md` exist
**ACTION**: Read `references/phase-3-write.md` § "Step 6 Prompt" and execute it.

Execute every suggestion. Verify:
- All suggestions addressed
- Reference list has no dead links
- Section headings match original assignment questions verbatim

**POST**: `04_写作工作区/07_final_submission.md` exists. Every item in `06_revision_suggestions.md` is addressed.

---

### Phase 5: Enhancement

#### Step 7 — Python Visualization

**PRE**: `07_final_submission.md` exists
**ACTION**: Read `references/phase-4-enhance.md` § "Step 7 Prompt" and execute it.

Generate academic charts with Python (`matplotlib`/`seaborn`), NOT Mermaid. Create script → generate high-DPI PNGs → save to `DeepResearch/` → embed in document.

**POST**: `04_写作工作区/08_final_submission_v2.md` exists with embedded chart references. PNG files exist in `DeepResearch/`.

> **SKIP CONDITION**: If the assignment doesn't benefit from charts (e.g., pure reflective essay), copy `07` to `08` and proceed.

---

#### 🔴 Human Quality Gate (between Step 7 and Step 8)

Before Step 8, diagnose the current state against `00_project_bible.md`:

| Scenario | Diagnosis | Trigger |
|----------|-----------|---------|
| A: Word count < target | 字数不足 | "Holistic Expansion" |
| B: Description > analysis | 深度不够 | "Critical Injection" |
| C: Tone too AI / too casual | 风格问题 | "Academic Tone Shift" |

Report the diagnosis to the user. Wait for their input on which refinements to apply.

---

#### Step 8 — Targeted Refinement

**PRE**: `08_final_submission_v2.md` exists + human quality gate diagnosis
**ACTION**: Read `references/phase-4-enhance.md` § "Step 8 Prompt" and execute the variant matching the diagnosis.

**CRITICAL RULE — Additive Only**:
- ✅ Micro-edits (sentence-level polish)
- ✅ Expansion (reflective overlay, new supporting paragraphs)
- ❌ Macro-rewrites (never delete whole paragraphs or rewrite core arguments)

**POST**: `04_写作工作区/09_final_submission_v3.md` exists. Core structure from v2 is preserved.

---

### Phase 6: Delivery

#### Step 9 — De-AI Processing

**PRE**: `09_final_submission_v3.md` exists
**ACTION**:
1. Copy v3 to `10_final_submission_human_verified.md`
2. Remove bold formatting from paragraphs only (`**text**` → `text`)
3. Preserve: headings (`#`), links (`[]()`), lists (`-`), image references (`![]`)

**POST**: `04_写作工作区/10_final_submission_human_verified.md` exists with bold removed from body text.

> 🔴 **MANUAL**: User extracts text → runs through external humanizer tool → pastes back. Wait for user to confirm this is done.

---

#### Step 10 — Final Formatting & Delivery

**PRE**: `10_final_submission_human_verified.md` is finalized by user
**ACTION**: Read `references/phase-5-deliver.md` for the complete formatting spec. Also read `references/formatting.md` for technical details and `references/quality-gates.md` for the final checklist.

Sub-steps:
1. Extract formatting requirements from `01_作业要求` folder
2. Ask user which format: DOCX / HTML / PDF
3. Generate the final file per technical specs
4. Run through the verification checklist (content consistency, format checks, link tests)

**POST**: `04_写作工作区/11_final_submission.*` exists in the chosen format. All checklist items pass.

---

## Interaction Protocol

- **At each step**: State what you're about to do, why, and which files you'll read/create
- **After each step**: Confirm the output exists and summarize what was produced
- **At 🔴 checkpoints**: Stop completely. Do not proceed until user says so
- **If prerequisites are missing**: Name the missing files. Offer to create them or ask user to provide them
- **Always reference file numbers** (00-11) when discussing outputs
- **If you're unsure about anything**: Consult `00_project_bible.md` first, then original source files
