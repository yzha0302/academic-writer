# Phase 6: Delivery — Full Instructions

---

## Step 9 — De-AI Processing

### AI Pre-Processing

1. Copy `09_final_submission_v3.md` to `10_final_submission_human_verified.md`
2. **De-bold only**: Remove `**text**` formatting from body paragraphs → plain `text`
3. **Strictly preserve**: Headings (`#`), links (`[]()`), lists (`-`), image references (`![]`)
4. Do NOT flatten to plain text — the markdown structure must survive

### Human Manual Process 🔴

The user will:
1. Extract body text from file `10`
2. Run through external humanizer tool (e.g., TwainGPT)
3. Paste processed text back into file `10`
4. Confirm completion

Wait for the user to confirm before proceeding to Step 10.

---

## Step 10 — Final Formatting & Delivery

### Sub-step 10.1: Extract Format Requirements

Read `01_作业要求与评分标准/` folder for specific formatting instructions:
- Font (default: Times New Roman)
- Size (default: 11pt)
- Spacing (default: 1.5)
- Reference style (check `00_project_bible.md`; default: APA 7th)
- Any special requirements (cover page, TOC, page numbers, etc.)

### Sub-step 10.2: User Format Choice 🔴

Ask the user which delivery format:

| Option | Format | Output File |
|--------|--------|-------------|
| 1 | DOCX (for Turnitin) | `11_final_submission.docx` |
| 2 | HTML (for PDF export) | `11_final_submission_landscape.html` |
| 3 | PDF (direct) | `11_final_submission.pdf` |

Default settings (if `00_project_bible.md` has no specific format requirements): Times New Roman, 11pt, 1.5 spacing, APA 7th, clickable links. **Always check bible first — project requirements override these defaults.**

### Sub-step 10.3: Generate & Verify

1. Generate the file per the format specs in `references/formatting.md`
2. Run through the verification checklist in `references/quality-gates.md`
3. Report results to user

### Common Pitfalls (avoid these)

| Problem | Fix |
|---------|-----|
| Font size inconsistent | Use `font-size: 11pt !important` on all content elements |
| Residual italics | Set `em, h3 { font-style: normal !important; }` in CSS |
| Residual asterisks `*` | Run regex cleanup after markdown conversion |
| Cover page too plain | Use project charts or generate AI cover image |
| Wrong reference format | Double-check against `00_project_bible.md` — use specified format, not default |
| References missing URLs | URL 覆盖率 < 70%: 书籍→出版社/Amazon，期刊→DOI，歌曲→YouTube/Spotify |
| HTML page overflow | Use `min-height: 210mm; height: auto;` not fixed height |
