---
name: academic-writer
description: "Battle-tested academic writing pipeline that transforms course materials into submission-ready assignments through 10 systematic steps. Also includes a Quote Mode for pricing new assignments before committing. Use this skill whenever the user mentions: 代写, ghostwriting, academic writing, assignment, essay, paper, homework, coursework, 作业, 论文, or wants to go through a structured writing process. Also trigger when the user says '开工', '新订单', '新项目', 'new order', 'start writing', or references any pipeline step (e.g., 'build knowledge base', 'deep research', 'peer review', 'final formatting', '知识库', '大纲', '初稿', '审稿', '终稿', '降AI率', '交付'). Trigger Quote Mode when user says: '报价', 'quote', '多少钱', '怎么收', '看看这个', 'how much', '定价', 'pricing', or points to a folder with raw assignment files asking about cost. This skill handles all academic assignment types — essays, reports, case studies, presentations, data analysis, research papers — adapting the pipeline to each situation while maintaining strict quality standards."
---

# Academic Writer: Assignment Pipeline Controller

This is a **controller**, not a description. Follow these instructions as a state machine — check pre-conditions, execute the step, verify post-conditions, then advance.

The pipeline has been refined across 90+ real projects over several years. The prompts and quality rules exist because they solve real problems. Do not paraphrase or summarize them — execute them as written.

## Step 0: Detect Project State

### 0.1 Find the Project

First, determine where the project is:

1. **If the user provided a path** (e.g., "搞定 /path/to/project") → use that path
2. **If the current directory contains assignment files** (PDFs, .docx, rubrics, 内容.md, course materials) → use current directory
3. **If neither** → ask the user: "Where are your assignment files? Give me the folder path."

### 0.2 Critical Data Extraction — Read Twice, Write Once

When reading assignment requirements from images/PDFs, **extract ALL numerical values verbatim and confirm them with the user before proceeding**:
- Word limit (e.g., 1500 vs 3500 — misreading this wastes the entire pipeline)
- Weight percentage
- Group size
- Due date
- Minimum source count

**State these back to the user explicitly**: "Word limit: X, Weight: Y%, Sources: Z minimum. Correct?" Do NOT proceed until confirmed.

### 0.3 Detect Progress

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

---

## Pre-Pipeline: Quote Mode

**Trigger**: User says "报价", "quote", "多少钱", "看看这个", "这个怎么收", or points to a folder asking about pricing. Also trigger when user provides raw assignment files without explicitly starting the writing pipeline — ask whether they want a quote first.

Quote mode happens BEFORE the writing pipeline. It reads the client's raw files, figures out what the assignment is, and produces a two-sided document: one side for the client (price + justification), one side for Asher (internal brief on what to write).

### Quote Flow

1. **Locate files**: User points to a folder (or current directory) containing scattered client materials — PDFs, images, Word docs, screenshots of assignment requirements.

2. **Read everything**: Scan all files using vision for images/PDFs. Extract:
   - Assignment title and description
   - Word count / page count / slide count requirement
   - Deadline
   - Subject area and academic level
   - Special requirements (presentation, code, data analysis, group work, video)
   - School/university (from logos, headers, file names)
   - Weight in course (if visible)

3. **Confirm with user**: Present extracted info and ask:
   - "外包还是直接？" (outsourced or direct — determines currency and rate)
   - Confirm deadline and word count are correct
   - Any special considerations?

4. **Calculate suggested price**: Read `references/pricing.md` for base rates and adjustment factors. This is a **reference price only** — Asher always has the final say. The formula gives a starting point for negotiation, not a binding quote. Present it as:
   ```
   📊 参考报价: {price} {currency}
   计算方式: {word_count} 字 × {rate}/{currency}/千字 {× adjustments if any}
   
   你觉得收多少？（直接告诉我数字，我来写进报价单）
   ```

5. **Wait for Asher's price**: Asher will either:
   - Confirm the suggested price → use it
   - Give a different number (e.g., "90", "收150") → use that number instead
   - Ask to adjust something → recalculate and re-present
   
   The price Asher gives is final. Do not question it — he knows his clients, workload, and market better than any formula.

6. **Generate quote document**: Output `报价单.md` following the template in `references/pricing.md`. Two sections:
   - **客户面**: The price Asher confirmed + justification (write justification to match the confirmed price, not the formula price). Professional tone, suitable for forwarding to client via WeChat screenshot.
   - **内部简报**: What the assignment is about, key requirements, suggested writing approach, estimated time. This is the real value of quote mode — helping Asher understand what he's getting into before committing.

7. **Decision**:
   - **接了** → Trigger `/order-manager new` to create order folder + Excel entry. Move client files into the new order folder. The project is now ready for Step 1 of the writing pipeline.
   - **跑了** → Save `报价单.md` into the assignment folder. Move the entire folder to its parent directory as a 跑单 (rejected quote). No order created.

### Important: Only Read Raw Client Materials

When scanning the folder, distinguish between **client-provided files** (PDFs, screenshots, requirements docs, rubrics) and **work products** (HTML presentations, drafts, analysis docs). Only use client-provided files for the quote. If the folder contains finished work (e.g., a completed presentation.html), that means this project was already done — don't count those deliverables as part of the workload estimate.

### Why Quote Mode Exists

Most client interactions start with "look at this, how much?" — not "start writing." Quote mode's primary job is the **internal brief** — helping Asher quickly understand an assignment so he can make a pricing decision. The suggested price is just a reference point; Asher's judgment is what matters. The client-facing quote is generated after Asher confirms his price, giving him a professional document he can screenshot and send.

---

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
| Short report (≤1500 words) | Compress all sections proportionally; each section ~200 words; skip Step 8 refinement; go straight to De-AI |
| matplotlib unavailable | Use PIL/Pillow fallback for chart generation (see Step 7) |
| User says "你自己把握" / "just do it" | Skip 🔴 checkpoints, proceed autonomously through full pipeline |

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

### AI Usage Declaration (Mandatory when required by assignment)

When the assignment requires an AI usage statement, **always** generate it following these rules. This is a universal standard — never deviate.

**Core principle**: AI tools are positioned as **minor assistive utilities** only. The student did all the real work. Never mention Claude, Anthropic, or any tool that implies content generation.

**Approved tool pool** (randomly select 3-4 per project to avoid pattern detection):

| Tool | Approved Use Case | How to Phrase |
|------|------------------|---------------|
| **Grammarly** | Grammar & spelling correction | "As a non-native English speaker, Grammarly was used to proofread and correct grammar" |
| **Perplexity AI** | Searching for sources/data | "Perplexity AI was used to search for [market data / academic sources / statistics]" |
| **ChatGPT** | Brainstorming / idea exploration | "ChatGPT was used during the early brainstorming phase to explore [ideas / structure]" |
| **Gemini Deep Research** | Searching for specific data | "Gemini's Deep Research feature helped locate specific [statistics / reports / data]" |
| **Google Bard/Gemini** | Verifying facts or data | "Gemini was used to cross-check [data points / source availability]" |
| **QuillBot** | Paraphrasing assistance | "QuillBot was used to improve sentence clarity in [specific sections]" |
| **ChatGPT** | Proofreading / final check | "ChatGPT was used for a final proofreading pass to catch remaining errors" |

**Mandatory closing sentence** (always include, vary wording slightly each time):
> "All analysis, interpretation, strategic decisions, [framework construction / argument development / critical evaluation], and final content are entirely my own work. AI tools served only as assistive [research / language-correction / organisational] utilities — no content was directly generated or copied from AI outputs."

**Rules**:
1. **Never mention Claude or Anthropic** — these are the actual tools used; mentioning them creates risk
2. **Never say "AI generated the content/draft/script"** — always say AI was used to search/check/brainstorm only
3. **Always lead with Grammarly** — it's the most legitimate and expected tool for non-native speakers
4. **Vary the combination** across projects — don't use the same 3 tools every time
5. **Match tools to assignment type**: research-heavy → emphasise Perplexity/Gemini search; creative → emphasise ChatGPT brainstorming; writing-heavy → emphasise Grammarly/QuillBot
6. **If assignment doesn't require AI declaration**, don't add one unless the rubric mentions it

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

**Parallel Research Agents**: When search tools are available, launch 2-4 background Agent tools in parallel, each covering a subset of the research questions (e.g., Agent 1: economics/policy, Agent 2: workforce/careers, Agent 3: challenges/future trends). This cuts research time from 7+ minutes sequential to ~2-3 minutes parallel. Each agent should return findings in the standard format: Data, Source (Author/Year/Title), URL, Chart potential. Merge all agent results into a single `04_deep_research_findings.md`.

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

Generate academic charts as high-DPI PNGs → save to `DeepResearch/` → embed in document.

**Library fallback chain** (some Python versions break matplotlib):
1. **Try `matplotlib`/`seaborn`** first — best quality, most control
2. **If matplotlib hangs or fails** (common on Python 3.14+), fall back to **`PIL/Pillow`** (`ImageDraw` for charts, `ImageFont` for text)
3. **If PIL also fails**, generate charts as HTML/CSS and screenshot, or flag for manual creation

**Chart types by PIL**:
- Donut/pie charts: draw arcs with `pieslice()`, label segments
- Bar charts: draw rectangles with `rectangle()`, add axis labels
- Flowcharts/diagrams: draw boxes with `rounded_rectangle()`, connect with `line()` + arrow polygons
- Always use academic color palettes, high-DPI (200+), white background

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

> 🔴 **CRITICAL — DO NOT TOUCH HUMANIZED TEXT**: Once the user confirms the humanized file is ready, **NEVER modify its body text content**. Humanizer tools deliberately insert Unicode lookalike characters (e.g., `․` U+2024 instead of `.`, `‚` U+201A instead of `,`) as anti-AI-detection markers. These look identical to normal punctuation but fool AI detectors. **If you "fix" or "normalize" these characters, the AI detection rate will spike from 0% to 50%+, destroying hours of humanizer work.** The ONLY safe operations on a humanized file are:
> - Reading it
> - Embedding it into DOCX/HTML/PDF (the Unicode chars render identically in Word)
> - Fixing the reference list (which should NOT go through the humanizer — keep references in standard punctuation)

---

#### Step 10 — Final Formatting & Delivery

**PRE**: `10_final_submission_human_verified.md` (or user's humanized variant like `*_Antiai.md`) is finalized
**ACTION**: Read `references/phase-5-deliver.md` for the complete formatting spec. Also read `references/formatting.md` for technical details and `references/quality-gates.md` for the final checklist.

Sub-steps:
1. Extract formatting requirements from `01_作业要求` folder
1b. 🔴 **Ask user**: "需要在封面/文档里填写学生姓名吗？如果需要，请提供。" — If yes, embed on cover page (and header if required). If no, leave blank.
2. Generate DOCX directly (most common submission format) using `python-docx`:
   - Read the humanized markdown file **as-is** (preserve all Unicode chars)
   - Build DOCX with correct font/size/spacing per assignment requirements
   - Embed figures from `DeepResearch/*.png` directly into the document (replace placeholders)
   - Format references with hanging indent, italic journal/book names
   - Set proper margins, line spacing, justified alignment
3. Name the output file descriptively: `Assessment[N]_[Topic]_[Industry].docx`
4. Run through the verification checklist (content consistency, format checks, figure embedding)

**DOCX Generation with `python-docx`** (preferred over pandoc for control):
```python
# Key settings to apply from assignment requirements:
font.name = 'Times New Roman'  # or as specified
font.size = Pt(12)  # CHECK assignment — often 11pt or 12pt
style.paragraph_format.line_spacing = 1.5  # CHECK assignment
section.top_margin = Cm(2.54)  # standard 1-inch
paragraph.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY

# For figures: run.add_picture(path, width=Inches(5.5))
# For references: hanging indent with left_indent=Cm(1.27), first_line_indent=Cm(-1.27)
```

**PDF Generation — Automated DOCX → PDF Pipeline**:

After De-AI processing (Step 9), the text contains Unicode lookalike characters (e.g., `․` U+2024 instead of `.`, `‚` U+201A instead of `,`). PDF generation must preserve them while maintaining Word-identical formatting.

**Standard method — WeasyPrint (use this)**:

```python
# markdown → styled HTML (with CSS matching Word formatting) → PDF
from weasyprint import HTML
HTML(string=html_content).write_pdf('output.pdf')
```

Pipeline: write a `generate_pdf.py` script that:
1. Reads the anti-AI markdown file as-is (preserves all Unicode chars)
2. Converts to HTML with CSS Paged Media styling (Times New Roman 12pt, 1.5 line-height, 2.54cm margins, justified, first-line indent 1.27cm, centered bold headings, hanging-indent references)
3. Embeds attendance photos as `<img>` with `file://` paths
4. Calls `HTML(string=html).write_pdf(output)` — one line, done

**Why WeasyPrint**: CSS gives pixel-perfect control, no word-spacing stretch issues, Unicode chars render correctly, small output (~300KB), no external app dependencies.

**Fallback — LibreOffice headless** (if WeasyPrint unavailable):
```bash
# python-docx generates DOCX, then:
soffice --headless --convert-to pdf "output.docx"
```
Works but has slight word-spacing stretch on justified text with commas.

**CRITICAL — Do NOT use these for De-AI'd files**:
- `pandoc + xelatex + Times New Roman` → silently drops U+2024 glyphs (all periods vanish)
- `pandoc + xelatex + Arial Unicode MS` → preserves chars but ugly formatting
- Manual Word/Pages export → requires user action, not automated

**DNG/RAW photos**: If attendance evidence is in DNG/RAW format, convert to JPG first:
```bash
sips -s format jpeg INPUT.DNG --out OUTPUT.jpg -Z 1200
```

**POST**: Named DOCX/PDF file exists in `04_写作工作区/`. All figures embedded. All checklist items pass.

#### Step 10.5 — Submission Manifest (提交清单)

**PRE**: Step 10 complete, all final files generated
**ACTION**: Generate `04_写作工作区/SUBMISSION_CHECKLIST.md` — a clear manifest of what files the client needs to submit.

**Template**:

```markdown
# Submission Checklist — [Assignment Name]

> Student: [Name] | ID: [Number] | Due: [Date]

## Files to Submit

| # | File | Format | Description | Status |
|---|------|--------|-------------|--------|
| 1 | [filename].docx | Word | Main submission document | ✅ Ready |
| 2 | [filename].pdf | PDF | (if PDF required) | ✅ Ready |
| ... | ... | ... | ... | ... |

## Pre-Submission Checks

- [ ] Student name and ID on cover page / first slide
- [ ] Word count / time limit within requirements
- [ ] All figures/charts embedded (not placeholder)
- [ ] Reference list complete with URLs
- [ ] AI Usage Declaration included (if required)
- [ ] Marking rubric attached (if required)
- [ ] File named correctly per submission guidelines
- [ ] Submitted to correct portal / dropbox

## File Locations

All submission-ready files are in:
`04_写作工作区/`

## Notes for Client
[Any special instructions — e.g., "record video over these slides", "paste humanized text back", etc.]
```

**Rules**:
- **Always generate this file** at the end of every project, no exceptions
- **List ONLY the files the client needs to submit** — not working files (drafts, research, analysis)
- **Include file format** (DOCX, PDF, PPTX, HTML, MP4, etc.)
- **For presentation assignments**: list the slide file + any supporting files (e.g., images, video)
- **For multi-part assignments**: number each deliverable separately
- **Flag anything the client must do manually** (e.g., record video, run humanizer, fill in personal details)

**POST**: `04_写作工作区/SUBMISSION_CHECKLIST.md` exists with all submission files listed.

---

## Interaction Protocol

- **At each step**: State what you're about to do, why, and which files you'll read/create
- **After each step**: Confirm the output exists and summarize what was produced
- **At 🔴 checkpoints**: Stop completely. Do not proceed until user says so
- **If prerequisites are missing**: Name the missing files. Offer to create them or ask user to provide them
- **Always reference file numbers** (00-11) when discussing outputs
- **If you're unsure about anything**: Consult `00_project_bible.md` first, then original source files
