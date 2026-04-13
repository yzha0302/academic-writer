# Phase 3-4: Writing & Review — Full Prompts

Execute these prompts as written. They have been tested across 90+ projects.

---

## Step 4 Prompt — Academic Draft (Prompt E)

> 你是一个专业的学者，擅长创作符合要求的学术文献。接下来我需要你根据我们 Deep Research 得到的资料 (`04_写作工作区/DeepResearch/04_deep_research_findings.md`) 以及作业大纲 (`04_写作工作区/02_implementation_plan.md`)，生成一份初稿。
>
> **核心要求**:
>
> 1. **合理引用 (Evidence-Based)**: 确保每个主要段落中包含相关的文献引用，信息必须与段落内容紧密相关。
> 2. **引用格式 (Citation Format)**:
>    - **检查 `00_project_bible.md` 中指定的引用格式**。如果指定了 footnotes、Harvard、Chicago 等格式，使用该格式。如未指定，默认 APA 7th。
>    - **Reference List / Bibliography**: 必须包含完整信息 (Author, Year, Title, Source, URL)。
>    - **Consistency Check**: **双向核对**——文中引用的必须在列表/书目中，列表有的必须文中引用，严禁"孤儿引用"。
> 3. **图表植入 (Visual Integration)**:
>    - 检查 `04_写作工作区/DeepResearch/` 目录下是否有现成的图表 (e.g., .png)。
>    - 如果有，**直接在文中插入** (Markdown: `![Caption](../DeepResearch/image.png)`)，替代纯文本占位符。
>    - 如果没有，才保留 `(Insert Figure X Here)` 标记。
> 4. **内容与语气**:
>    - **语气**: 检查 `00_project_bible.md` 的要求。如指定"简单英语"或"不要太学术"，使用自然、清晰的语言；如无特殊要求，默认柔和自信的学术语气 (Confident yet Measured)。
>    - 结构上遵循正常的文章段落 (Paragraphs)。
>    - 严格执行大纲的字数分配，不能少于标准要求。
> 5. **分步输出**: 如果单个对话框无法全部输出，请先提供部分内容，并在后续对话框中自动补完。
>
> **产出目标**: 生成 `04_写作工作区/05_draft_v1.md`。

### Pre-Flight Checks (Do These Before Writing)

1. **Asset Check**: Scan `DeepResearch/` folder for existing images (.png, .jpg). List what's available.
2. **Word Budget**: Reconfirm the outline's word count allocation. Write it down.
3. **Citation Pool**: Review `04_deep_research_findings.md` — know what citations you have before you start writing.

### During Writing

- Generate content section by section, matching the outline order
- After each section, count words and compare against budget
- Run citation bidirectional check: every (Author, Year) in text → must be in reference list, and vice versa

### After Writing — URL Coverage Check

Every bibliography/reference list entry should have a clickable link. The target is **≥ 70% URL coverage**. For each entry without a URL, search for one:

| Source Type | Where to Find URL |
|-------------|------------------|
| Journal article | DOI link (https://doi.org/...) or journal website |
| Book | Publisher website, Amazon, or Google Books |
| Song/recording | YouTube, Spotify, Apple Music, or official MV link |
| Website/report | Direct URL |
| Conference paper | Conference proceedings URL or ResearchGate |

Count: `entries_with_URL / total_entries ≥ 0.70`. If below 70%, search for the missing links before finalizing. A reference without a URL when one exists is incomplete work.

**Footnote-Bibliography consistency**: When using footnotes + bibliography format, the first full citation of each source in the footnotes must include the same URL as the bibliography entry. Subsequent short-form citations (e.g., "Neal, 'Narrative Paradigms,' 42") do not need URLs. Never have a URL in the bibliography but not in the corresponding first footnote — they must match.

### Output File

`04_写作工作区/05_draft_v1.md`

---

## Step 5 Prompt — Deep Review (Prompt F)

> 你是一个专业的论文评论导师，擅长在每一项作业中拿到满分。你需要仔细阅读初稿 (`05_draft_v1.md`)，并根据高分标准 (`00_project_bible.md`) 和具体的作业要求（Rubric），提供优化文章的具体指示。
>
> **输入**: `05_draft_v1.md`, `00_project_bible.md`
> **执行**: 对照 Distinction 标准，寻找当前草稿的弱点（如论证不够深、引用格式小错误、语气不够学术）。
> **输出**: 生成 `04_写作工作区/06_revision_suggestions.md`。
> **关键要求**: 只针对内容和质量提出"可执行的指令" (Use imperative verbs), 确保每条指令都能直接帮助提高文章质量。

### What Good Revision Suggestions Look Like

Each suggestion must be:
- **Actionable**: Uses imperative verbs — "Add...", "Replace...", "Strengthen...", "Delete..."
- **Specific**: Points to exact section/paragraph, not "improve the analysis"
- **Rubric-anchored**: Explains which rubric criterion this addresses

### Output File

`04_写作工作区/06_revision_suggestions.md`

---

## Step 6 Prompt — Final Draft (Prompt G)

> 你是一个专业人士，接下来我需要根据优化建议 (`06_revision_suggestions.md`) 和初稿 (`05_draft_v1.md`) 完成终稿。
> **执行**:
>
> 1. **执行建议**: 逐条落实修订建议中的内容。
> 2. **Strict Formatting**: 确保 Reference List 无死链，In-text citation 完美对应。
> 3. **Verbatim Headers**: 确保小标题严格使用作业原题 (e.g., 'Question 1: ...')。
>
> **输出**: 生成 `04_写作工作区/07_final_submission.md`。

### Verification

After generating the final draft:
1. Check off each item in `06_revision_suggestions.md` — was it addressed?
2. Run citation bidirectional check one more time
3. Verify section headings match the original assignment questions exactly

### Output File

`04_写作工作区/07_final_submission.md`
