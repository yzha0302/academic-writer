# Ghostwriter: 交付格式规范 (Formatting Specifications)

Read this file at Step 10 when preparing the final delivery document.

---

## 交付格式选项

| 格式 | 描述 | 输出文件 |
|------|------|----------|
| **DOCX** | 标准 Word 文档，适用于 Turnitin 提交 | `11_final_submission.docx` |
| **HTML** | 精美 CSS 排版的网页文档，适用于 PDF 导出 | `11_final_submission_landscape.html` |
| **PDF** | 直接生成的 PDF 文件 (通过 Pandoc/WeasyPrint) | `11_final_submission.pdf` |

**Default Settings** (若 `00_project_bible.md` 无特殊要求): `Times New Roman`, `11pt`, `1.5 Spacing`, `APA 7th Referencing`, `Active Links: Yes`。**但必须先检查 project bible 和作业要求中的格式规定——如有指定，以指定为准。**

---

## DOCX 文档规范

| 要素 | 强制标准 |
|------|----------|
| **字体** | `Times New Roman`, `11pt` (正文), `14pt` (标题) |
| **对齐** | `Justified` (两端对齐) |
| **行距** | `1.5` |
| **封面页** | 必须包含: 学校名称、课程代码、标题、日期 (无学号/字数，除非用户要求) |
| **目录** | 自动生成 Table of Contents (TOC) |
| **页码** | 每页底部居中显示页码 |
| **分页** | 确保各章节独立分页 |
| **参考文献** | APA 7th 格式，期刊/书名斜体 |
| **链接** | 所有 URL 必须为**可点击超链接** |

---

## HTML 文档规范

| 要素 | 强制标准 |
|------|----------|
| **布局** | A4 Landscape (297mm x 210mm) 或 Portrait，分页式 "Sheet View" |
| **字体** | `Times New Roman` for ALL body text (`p`, `li`, `em`, `a`) — 必须使用 `!important` 强制覆盖 |
| **字号** | 统一 `11pt` — 禁止不同元素使用不同字号 |
| **斜体** | 默认关闭 (`font-style: normal`)，除非用户特别要求 |
| **封面设计** | AI 可自由设计，但必须包含: 课程代码、标题、年份/学期 |
| **封面图片** | 优先使用项目内已有资源，或生成 AI 图片 |
| **配色** | 由 AI 根据项目主题决定 |
| **参考文献** | 正确使用 `<em>` 标签包裹期刊名 |
| **链接** | 所有 URL 必须为可点击链接，带 `target="_blank"` |

---

## PDF 文档规范

- 与 DOCX 要求一致
- 生成方式: 使用 `pandoc` 或 `weasyprint` 从 HTML 转换
- 或: 指导用户在浏览器中打开 HTML 后使用 `打印 -> 另存为 PDF`

---

## 常见问题与防御措施

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 字体大小不统一 | 部分文本未被 `<p>` 包裹 | `font-size: 11pt !important` 强制所有 `.content-wrapper *` |
| 残留斜体 | `<em>` 默认渲染为斜体 | `em, h3 { font-style: normal !important; }` |
| 残留星号 `*` | Markdown 未被正确解析 | 使用 Regex 清理: `html.replace('*', '')` |
| 封面缺少图片 | 只有文字，视觉不足 | 使用项目内图表或 AI 生成封面图 |
| 参考文献格式错误 | 格式混用 | 严格遵循选定的格式模板 |
| 页面过高 (HTML) | 固定高度被内容溢出 | 使用 `min-height: 210mm; height: auto;` |

---

## 参考文献格式模板

### Harvard 格式

```
# 期刊文章
Author, A.A. and Author, B.B. (Year) 'Article title', Journal Name, Volume(Issue), pp. X-X. doi: 10.xxxx/xxxxx. Available at: https://full-url (Accessed: Day Month Year).

# 书籍
Author, A.A. (Year) Book Title. Place: Publisher. Available at: https://full-url (Accessed: Day Month Year).

# 网页/报告
Organisation Name (Year) Report Title. Available at: https://full-url (Accessed: Day Month Year).
```

### APA 7th 格式

```
# 期刊文章
Author, A. A., & Author, B. B. (Year). Article title. Journal Name, Volume(Issue), Page-Page. https://doi.org/xxxxx

# 书籍
Author, A. A. (Year). Book title (Edition if applicable). Publisher. https://full-url-to-book

# 网页/报告
Organisation Name. (Year). Report title. https://full-url-to-source

# 带检索日期的网页 (动态内容)
Organisation Name. (Year, Month Day). Page title. Site Name. Retrieved Month Day, Year, from https://full-url
```

**URL 来源优先级** (从高到低):
1. DOI 链接 (学术期刊首选)
2. 出版社官网链接
3. Amazon/图书零售商链接 (书籍)
4. 可信数据库链接

**格式选择**: 以 `00_project_bible.md` 中指定的格式为准。如未指定，默认 APA 7th。常见替代：Harvard、Chicago/Turabian、footnotes + bibliography。

**关键**: Bibliography/Reference List 的 URL 覆盖率必须 ≥ 70%。每条引用都应尽力附带可点击链接（DOI、出版社链接、Amazon、YouTube 等）。无链接的引用视为不完整——在提交前必须搜索补全。
