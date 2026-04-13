# Phase 2: Planning — Full Prompts

Execute these prompts as written. They have been tested across 90+ projects.

---

## Step 3.1 Prompt — Assignment Analysis (Prompt A)

> 你是一名专业的作业分析师，目标是在每一项作业中达到满分水平。你需要以专业分析师的身份，提供符合学术标准、质量最高、可直接用于写作与提交的分析与指导。
> **具体分析要求**:
>
> 1. **始终保持逻辑清晰、结构严谨**：观点—论据—推导—结论完整闭环，层次分明，不跳步、不含糊。
> 2. **引用准确且可核查**：所有关键论断需有可靠依据，引用格式与标注方式严格符合学术规范。
> 3. **严格遵循标准与限制**：包括题目范围、写作要求、格式规范、字数要求、评分标准（Rubric）等，不得偏离。
> 4. **逐步指导完成作业**：按"理解任务 → 拆解要求 → 制定结构 → 逐段写作要点 → 校对与对标评分标准"的顺序，一步一步推进。
> 5. **对标满分标准**：在每一部分完成后，明确说明其如何满足评分点，并指出可进一步加分的优化方向。
>
> **质量阻断机制 (Quality Barrier) - 必须严格执行**:
>
> - **拒绝泛泛而谈**: 任何没有具体课程理论 (Courseware Theory) 支撑的观点均为废话。
> - **拒绝幻觉引用**: 不得编造 Academic Reference，必须使用资料库中的真实文献。
> - **拒绝模棱两可**: 如"可能"、"大概"等不确定的表述，必须精准对标 Rubric。
> - **拒绝逻辑跳跃**: 防止仅有结论而无推导过程的"AI 式"回答。
>
> 请基于 `00_project_bible.md` (优先) 和原始课件 (保底)，输出一份包含上述'分析要求'与'低质量预警'的深度作业分析报告。

### Execution Details

1. **Theory Mapping**: Map `00_project_bible.md` core theories to specific assignment questions. No theory = no paragraph.
2. **Logic Chain Preview**: For each argument: `Claim → Evidence → Reasoning → Conclusion`
3. **Negative Scan**: Identify and flag vague statements (e.g., "we need innovation...") → force replacement with specific theory (e.g., "According to Schumpeter's innovation theory...")
4. **Citation Tracing**: Every citation must trace to `00_project_bible.md` or a specific PDF page
5. **Rubric Decomposition**: Convert Distinction descriptors to checkpoints, identify gaps

### Output File

`04_写作工作区/01_assignment_analysis.md` containing:
- 任务拆解 (Task Decomposition)
- 结构规划 (Structure Planning)
- 段落级写作指引 (Paragraph-level Writing Guide)
- 满分自查表 (Distinction Self-Audit Table)

---

## Step 3.2 Prompt — Outline Configuration (Prompt B)

> 请以专业人士的身份，协助我整理一份结构清晰、符合高分标准的作业大纲。具体要求如下：
>
> - 按照严密的逻辑顺序拆解作业的各项要求，明确每一部分在整体中的位置与功能。
> - 对每一部分分别列出写作要点、核心内容，以及在写作中体现高分标准的方式。
> - 清晰标注各部分的字数分配，便于后续按比例展开写作。
> - 在需要选题的情况下，从多个可选主题中进行取舍。
> - 结合你目前掌握的信息 (`00_project_bible.md`)，包括但不限于作业内容要求、评分标准及相关参考工具，选择一个资料获取最便捷、且最有利于取得高分的主题。
> - 基于所选主题，重新构建一份完整、全新的作业大纲。

### Execution Details

1. **Topic Selection**: Based on available courseware and rubric, recommend the safest high-scoring topic
2. **Outline Construction**: Word count budget + detailed paragraph plan + theory citation points

### Output File

`04_写作工作区/02_implementation_plan.md`

---

## Step 3.3 Prompts — Deep Research (Prompt C + D)

### Phase 1: Question Generation (Prompt C)

> 请你以专业学者的身份，根据既定的作业大纲 (`02_implementation_plan.md`)，设计一组具有高学术价值、可用于深度文献检索的问题。
> **具体要求**:
>
> - **针对性**: 针对大纲每一部分生成 2–5 个高质量研究问题。
> - **证据导向**: 问题应指向实证研究、理论模型、统计数据或权威观点。
> - **可检索性**: 问题需具备明确的关键词，利于 Deep Research 工具 (Perplexity/Gemini) 抓取。
> - **产出要求**:
>   1. 请先创建文件夹 `04_写作工作区/DeepResearch`。
>   2. 生成 `04_写作工作区/DeepResearch/03_deep_research_questions.md`，列出这些问题。
>   3. (后续步骤) 我们会将检索到的带链接的文献证据填入 `04_写作工作区/DeepResearch/04_deep_research_findings.md`。

### Phase 2: Research Execution (Prompt D)

> 现在，请启动深度研究模式 (Deep Research Mode)。
> **输入**: 读取 `04_写作工作区/DeepResearch/03_deep_research_questions.md` 中的所有问题。
> **执行**: 针对每个问题进行广度与深度搜索，寻找高信度的学术证据（数据、案例、理论）。
> **输出**: 将结果填入 `04_写作工作区/DeepResearch/04_deep_research_findings.md`。
> **关键约束 (CRITICAL)**:
>
> 1. **权威数据源**: 必须优先使用 .edu, .gov, 或知名期刊/智库来源。每一条数据都必须有**明确出处**。
> 2. **引用格式准备**: 为每一条 Findings 预备完整的引用信息 (Author, Year, Title, Source)，并在末尾附带**可点击的原始 URL/DOI**。具体格式参照 `00_project_bible.md` 中指定的引用规范（APA 7th / Harvard / footnotes / 其他）。
> 3. **可视化数据**: 特别关注适合制作图表的数据。明确标注"此数据适合制作 Figure X"。
> 4. **No Dead Links**: 严禁由 AI 臆造链接，必须确保链接真实可访问。
> 5. **URL 覆盖率 ≥ 70%**: 至少 70% 的 findings 条目必须附带可点击的链接。书籍用出版社/Amazon/Google Books 链接，期刊用 DOI，歌曲/录音用 YouTube/Spotify 链接。生成完毕后统计覆盖率，不达标则补搜。

### Execution Modes

- **Mode A (AI Auto)**: If search tools (WebSearch, Exa, etc.) are available, use them. Aggregate results into `04_deep_research_findings.md`. This is the default when tools exist.
- **Mode B (User Manual)**: If no search tools are available, generate the questions file and tell the user: "Please search these questions externally and paste findings into `04_deep_research_findings.md`."

### Output Files

- `04_写作工作区/DeepResearch/03_deep_research_questions.md`
- `04_写作工作区/DeepResearch/04_deep_research_findings.md`
