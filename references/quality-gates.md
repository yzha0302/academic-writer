# Ghostwriter: 质量检查清单 (Quality Gates)

Read this file at checkpoints and before final delivery.

---

## 人工质检局 — 差异化诊断 (Step 7 → Step 8 之间)

在最终交付前，进行"差异化诊断"，确保交付物符合该具体订单的特殊要求。

### 诊断流程

1. **提取与核对**: 将 Draft 内容对照 `00_project_bible.md` 的硬性指标（字数 / 图表 / 理论要求）
2. **场景分支**:

| Scenario | 现状 | 触发动作 |
|----------|------|----------|
| **A: 字数不足** | 当前字数少于目标 | → "Holistic Expansion" (Step 8, Prompt I - Expansion) |
| **B: 深度不够** | 描述多于分析，Rubric 要求 HD | → "Critical Injection" (Step 8, Prompt I - Critique) |
| **C: 风格问题** | 语气太像 AI / 太口语 | → "Academic Tone Shift" (Step 8, Prompt I - Tone) |

3. 根据诊断结果，向 AI 发送针对性的 Step 8 指令

---

## Step 9: 降 AI 率处理流程

### AI 预处理
1. 将 `09_final_submission_v3.md` 复制为 `10_final_submission_human_verified.md`
2. **仅去除**段落中的加粗格式 (`**text**` → `text`)
3. **严格保留**: 标题 (`#`)、链接 (`[]()`)、列表 (`-`)、图片引用 (`![]`)

### 人工操作 🔴
1. 从 `10` 文件中复制纯文本段落
2. 放入外部降 AI 软件处理
3. 将处理干净的文本粘贴回 `10`
4. 最后恢复格式

---

## Step 10.6: 内容一致性验证

**源文件 (Single Source of Truth)**: `04_写作工作区/10_final_submission_human_verified.md`

### 验证清单

- [ ] **标题一致**: 最终文档标题与源文件 H1 标题完全一致
- [ ] **章节完整**: 所有 H2/H3 章节都已正确渲染，无遗漏
- [ ] **图片完整**: 所有 `![Image](path)` 都已正确显示，无 broken image
- [ ] **引用完整**: References 部分与源文件一致，无丢失/重复
- [ ] **内容无篡改**: 正文内容未被意外修改 (可用 diff 工具对比)
- [ ] **格式转换无损**: Markdown 格式正确转换为 HTML/Word 格式

### 验证方法
1. 打开源文件 `10_final_submission_human_verified.md` 和最终交付物
2. 逐章节对比内容
3. 若发现差异，以 `10` 为准修正

---

## Step 10.7: 最终交付检查清单

### 格式检查

- [ ] **字体一致性**: 正文全部为 Times New Roman 11pt
- [ ] **无斜体残留**: 除期刊名外，正文无斜体
- [ ] **无星号残留**: 搜索 `*` 字符，应无结果
- [ ] **链接可点击**: 测试至少 3 个参考文献链接
- [ ] **URL 覆盖率 ≥ 70%**: 统计 bibliography 中有 URL 的条目 / 总条目，必须 ≥ 70%。不达标则补搜（书籍→出版社/Amazon/Google Books，期刊→DOI，歌曲→YouTube/Spotify）
- [ ] **分页正确**: 每个主要章节在新页开始
- [ ] **封面完整**: 包含课程代码、标题、年份

### 内容检查

- [ ] **内容与源文件一致**: 与 `10_final_submission_human_verified.md` 对比无差异
- [ ] **参考文献格式**: APA 7th / Harvard 格式无误
- [ ] **图表完整**: 所有图表正常显示
- [ ] **字数达标**: 达到或超过目标字数
- [ ] **引用双向一致**: 文内引用 ↔ Reference List 完美对应
- [ ] **URL 覆盖率 ≥ 70%**: 有链接条目 / 总条目 ≥ 0.70
