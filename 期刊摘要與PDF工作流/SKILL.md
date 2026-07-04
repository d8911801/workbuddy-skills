---
name: 期刊摘要與PDF工作流
description: 用於處理年度期刊論文 Excel 清單，補齊正式摘要、來源網址、公開 PDF、年度 manifest 與交付報告。適合中文研究工作流，且不直接覆寫原始 Excel。
---

# 期刊摘要與PDF工作流

Use this skill for repetitive journal-article spreadsheet work where the user has yearly Excel files and wants a controlled workflow for abstract capture, PDF/source supplementation, or final handoff packaging.

## Pick The Mode First

Choose one mode before touching files.

### Mode A: Abstract Fill

Use when the user wants missing abstracts filled back into Excel.

Do:
- Work from a copied Excel, never the original.
- Use only formal abstract fields explicitly labeled `摘要` / `中文摘要` / `提要`.
- Copy the abstract verbatim.
- Record the exact source URL.
- Mark ambiguous matches as `待人工確認`.

Do not:
- Rewrite, shorten, normalize, or paraphrase abstracts.
- Treat正文首段 as abstract.
- Continue into the next batch unless asked.

### Mode B: PDF / Source Supplement

Use when the user mainly wants materials for human checking.

Do:
- Keep the original abstract column untouched.
- Add source URLs, PDF URLs, local PDF paths, source type, and retrieval status.
- Download only public, lawful PDFs.
- Save PDFs in a dedicated handoff folder.

Do not:
- Judge whether the abstract is complete unless the user explicitly asks.
- Save HTML pages as fake PDFs.

### Mode C: Final Audit / Handoff

Use when the user wants a final cleanup pass.

Do:
- Check status totals.
- Check whether manifests, reports, and yearly output files exist.
- Check whether PDFs listed in manifests actually exist.
- Identify orphan PDFs, broken PDFs, and items needing manual review.
- Produce a concise handoff report for an assistant.

## Shared Rules

Apply these rules in every mode.

### File Handling

- Always copy the source Excel before editing.
- Prefer one year per run, then stop.
- Keep outputs in a dedicated workspace with stable subfolders.
- Do not delete, rename, or move source files unless the user explicitly asks.

Recommended subfolders:
- `Excel_*`
- `PDF原文_給助理` or `原文PDF`
- `來源證據`
- `工作報告`

### Source Priority

Search in this order unless the user overrides it:

1. Original journal / school / institution official PDF
2. National Central Library journal pages
3. TCI
4. Airiti / CEPS / Huayi
5. Other public lawful sources

Treat Yuandan / 月旦 as auxiliary only. If it looks like正文首段 instead of a formal abstract, do not adopt it as the abstract.

### PDF Rules

- Download only public, lawful PDFs.
- Validate that the file is a real PDF after download.
- If the source requires login, captcha, or payment, do not force through it. Record `需登入/付費`.
- If a PDF cannot be downloaded, still record the best available source page URL for manual review.

### Match Rules

Check author, title, journal, year, issue, and pages together.

Use these status patterns unless the user already has a fixed schema:
- `已完成`
- `未找到`
- `待人工確認`

Use these bibliographic match patterns unless the user already has a fixed schema:
- `書目吻合`
- `有書目但無摘要`
- `查無可靠來源`
- `疑似同名待確認`

## Minimal Yearly Workflow

When the user gives a yearly file:

1. Identify the mode.
2. Create or confirm the workspace and subfolders.
3. Copy the year’s Excel into the output subfolder.
4. Add only the columns needed for the chosen mode.
5. Process that year only.
6. Generate:
   - updated Excel copy
   - yearly manifest
   - yearly short report
7. Open the updated Excel when requested.
8. Stop instead of rolling into the next year.

## Suggested Columns

Use only the columns needed for the current task.

### For Abstract Fill

- 摘要
- 摘要來源網址
- 核對結果
- 狀態
- 備註

### For PDF / Source Supplement

- 原文PDF來源網址
- 原文PDF本地路徑
- 核對用來源網址
- 來源類型
- PDF取得狀態
- 書目核對結果
- 備註

## Reporting Pattern

Keep the end-of-run report short and operational.

Include:
- year handled
- total rows
- downloaded PDFs
- no public PDF
- login/paywalled items
- ambiguous items
- failed downloads
- output Excel path
- manifest path
- report path
- handoff PDF folder path

## Guardrails For Long Runs

If the task spans many years or many rows:

- Run year by year.
- Prefer a fresh window for the next year when context starts to bloat.
- Preserve intermediate files after each year.
- Do not silently change schemas halfway through the series.

## Example Triggers

This skill is appropriate for prompts like:

- “幫我補抓這批期刊論文的摘要並回填 Excel。”
- “只補 PDF 和來源網址，給助理人工校對。”
- “把 2010-2019 這批每年各做一份 PDF manifest。”
- “檢查交付包裡哪些 PDF 是孤兒檔案。”
