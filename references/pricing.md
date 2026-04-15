# Pricing Reference

> Read this file when Quote Mode is triggered. Contains base rates, adjustment factors, and output templates.

## Base Rates

| Type | Rate | Currency | When |
|------|------|----------|------|
| 直接单 (Direct) | 200 | AUD | Asher does it himself (with AI) |
| 外包单 (Outsourced) | 300 | CNY | Subcontracted to others |

**Unit**: per 1000 words (or equivalent — see Special Format Conversion below).

## Word Count Estimation

The quote depends on accurately estimating the deliverable size. Extract from assignment files:

| Source | How to Find |
|--------|------------|
| Explicit word limit | "1500 words", "2000-word essay" in requirements |
| Page count | "5 pages" → ~1250 words (250 words/page, double-spaced) |
| Slide count | "10 slides + speaker notes" → see Special Format below |
| No limit stated | Estimate from rubric weight + academic norms for the level |

If ambiguous, estimate conservatively (round up to nearest 500).

## Special Format Conversion

Not everything is a plain essay. Convert to word-equivalent for pricing:

| Format | Conversion | Rationale |
|--------|-----------|-----------|
| Essay / Report | 1:1 | Direct word count |
| Presentation (slides + script) | slides × 200 words | ~200 words script per slide |
| Presentation (slides only, no script) | slides × 100 words | Design + bullet points |
| Data analysis + report | word count × 1.3 | Extra effort for data processing |
| Code + report | word count × 1.5 | Coding time |
| Annotated bibliography | entries × 200 words | Per-entry analysis |
| Reflective journal / blog | 1:1 | Usually simpler writing |
| Exam / quiz | questions × 150 words | Per-question estimate |

## Adjustment Factors

Since the work is AI-assisted, adjustments are modest. Apply cumulatively (multiply, don't add):

| Factor | Condition | Multiplier | Rationale |
|--------|-----------|-----------|-----------|
| **Urgency** | < 24 hours | × 1.3 | Rush job |
| | < 48 hours | × 1.2 | Tight turnaround |
| | < 3 days | × 1.1 | Slightly rushed |
| | ≥ 3 days | × 1.0 | Normal |
| **Subject** | STEM / Law / Medical | × 1.15 | Specialist knowledge, stricter accuracy |
| | Business / Humanities | × 1.0 | Standard |
| | General / Intro level | × 0.95 | Lower complexity |
| **Level** | Postgraduate / Honours | × 1.1 | Higher academic bar |
| | Undergraduate | × 1.0 | Standard |
| **Special Req** | Turnitin report required | × 1.0 | Standard (AI handles) |
| | Video recording needed | × 1.1 | Extra deliverable |
| | Group coordination | × 1.1 | Communication overhead |

**Minimum order**: 100 AUD or 200 CNY (below this it's not worth the setup time).

## Rounding

Final price: round to nearest $10 (AUD) or ¥50 (CNY). Clean numbers look more professional.

## Step 1: Internal Brief (Show First)

Before asking about price, present the **internal brief** so Asher can understand the assignment. This is the primary value of quote mode.

```
📋 作业概要
━━━━━━━━━━━━━━━━━━━━━━━━━
项目: {assignment title}
类型: {essay / presentation / report / ...}
科目: {subject area}
学校: {school, if identified}
权重: {weight}%
截止: {deadline}
预估字数: {N} 字
━━━━━━━━━━━━━━━━━━━━━━━━━

{1-2 sentences: what this assignment is about, what the student needs to do}

写作路子:
• {bullet 1}
• {bullet 2}
• {bullet 3}
```

## Step 2: Suggested Price (Reference Only)

After the brief, show a reference price. Make it clear this is a suggestion:

```
📊 参考报价: {calculated_price} {currency}
计算方式: {word_count} 字 × {rate}/{currency}/千字 {× adjustments}

你觉得收多少？
```

Wait for Asher's response. He might say "90", "收150", "就这样", or "太高了"。Whatever number he gives, use that.

## Step 3: Generate Quote Document

Only after Asher confirms a price, generate `报价单.md`:

```markdown
# 报价单

> 日期: {today}
> 项目: {assignment title}
> 客户: {client name, if known}

---

## 报价

| 项目 | 数值 |
|------|------|
| 作业类型 | {essay / presentation / report / ...} |
| 预估字数 | {N} 字 |
| **报价** | **{asher_confirmed_price} {currency}** |

## 说明

{2-3 sentences justifying the CONFIRMED price — not the formula price. Adapt the reasoning to match whatever number Asher chose. If Asher's price is lower than the formula, emphasize efficiency; if higher, emphasize complexity. Written in a tone suitable for forwarding to client via WeChat screenshot.}

---

## 📋 内部简报 (Asher Only)

### 这个作业写什么

{1 paragraph summary: topic, key requirements, what the student needs to demonstrate}

### 关键要求

- 字数: {word limit}
- 截止: {deadline}
- 格式: {citation format, special formatting}
- 权重: {weight in course}
- 特殊: {any unusual requirements — group work, video, specific tools}

### 写作路子

{Brief strategy: what approach to take, which frameworks/theories to use, what to emphasize for high marks. 3-5 bullet points.}

### 预估工时

{Rough time estimate for Asher — e.g. "~2小时，含研究+写作+排版"}
```

## Decision Flow After Quote

```
Asher reviews final 报价单
  ├── "接了" / "OK" / "做"
  │   → Trigger order-manager: create order folder + Excel entry
  │   → Move files into new order folder
  │   → Ready for academic-writer Step 1
  │
  └── "不做" / "跑了" / "算了"
      → Save 报价单.md to the assignment folder
      → Move the entire folder to parent directory (as 跑单)
      → No order created
```
