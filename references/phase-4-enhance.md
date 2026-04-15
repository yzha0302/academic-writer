# Phase 5: Enhancement — Full Prompts

Execute these prompts as written. They have been tested across 90+ projects.

---

## Step 7 Prompt — Python Visualization (Prompt H)

> 我不推荐用 Mermaid 画图。我希望用 **Python** 直接生成图片，然后插入文中。
> **执行**:
>
> 1. **编写脚本**: 创建 `generate_conceptual_charts.py`，使用 `matplotlib` / `seaborn`。
> 2. **生成图表**: 针对相关理论框架生成高 DPI 学术图表 (.png)。
> 3. **保存路径**: `04_写作工作区/DeepResearch/`。
> 4. **植入文档**: 使用 `![Caption](DeepResearch/xxx.png)` 语法替换原 Mermaid 代码。
>
> **输出**: 更新文档为 `04_写作工作区/08_final_submission_v2.md`。

### Chart Style Requirements

- High DPI (200+) for print quality
- Academic color palette (avoid garish colors)
- Clear axis labels, titles, and legends
- Consistent font sizes across all charts
- Save as PNG with white background

### Library Fallback Chain

matplotlib may hang or crash on newer Python versions (3.14+). Use this fallback:

1. **matplotlib/seaborn** — try first, set `matplotlib.use('Agg')`, test with a simple plot before committing
2. **PIL/Pillow** — reliable fallback, available on most systems:
   - `ImageDraw.pieslice()` for donut/pie charts
   - `ImageDraw.rounded_rectangle()` + `ImageDraw.line()` for flowcharts/diagrams
   - `ImageDraw.rectangle()` for bar charts
   - `ImageFont.truetype('/System/Library/Fonts/Helvetica.ttc', size)` for macOS fonts
   - Always test with timeout: if matplotlib doesn't return within 15 seconds, kill and switch to PIL
3. **HTML/CSS screenshot** — last resort, generate as styled HTML and screenshot via browser tool

### When to Skip

If the assignment is a pure reflective essay or doesn't benefit from visual aids, simply copy `07_final_submission.md` to `08_final_submission_v2.md` and proceed.

---

## Step 8 Prompt — Targeted Refinement (Prompt I)

This step is driven by the Human Quality Gate diagnosis. Choose the matching variant:

### Variant A: Expansion (字数不足)

> 字数要求是 **[Target]字**。请在**保持核心观点不变**的前提下，进行'反思性叠加' (Reflective Overlay)。
> 策略：请基于此段落的现有内容，**智能判断**最合适的扩充角度（例如：增加批判性反思、深入挖掘理论背景、补充实证案例、或强化逻辑推导）。请选择最能提升文章深度和学术价值的方向进行扩充，而不受限于特定模式。

### Variant B: Critical Injection (深度不够)

> 请加强批判性分析。在每个论点后增加 'However, ...' 的反思段落，包含反面论证 (Counter-arguments) 和理论局限性分析。

### Variant C: Tone Fix (风格问题)

> 请将全文重写为严谨的第三人称学术口吻，移除所有情绪化形容词。

### The Red Line — Additive Only

No matter which variant:
- ✅ **Micro-edits**: Sentence-level trimming, polishing, removing redundant words
- ✅ **Expansion**: Reflective overlay, new supporting paragraphs, deeper analysis
- ❌ **Macro-rewrites**: Never delete whole paragraphs. Never rewrite core arguments. The v2 structure and reasoning must be preserved.

Breaking this rule destroys hours of accumulated quality. Small, targeted improvements compound better than rewrites.

### Output File

`04_写作工作区/09_final_submission_v3.md`
