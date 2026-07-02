---
name: 千問純文字轉Word
description: Prepare a fixed SOP for cloud Qwen manuscript polishing, then turn Qwen's pure-text Markdown output into independent Word drafts or tracked-revision Word files with real footnotes. Use when the user asks to standardize Qwen revision output, keep `[^N]` footnotes, or convert an original text plus a Qwen-polished pure-text draft into a reviewable `.docx`.
---

# Qwen Manuscript To Word

Use this skill for the specific workflow where cloud Qwen does the polishing, but the agent handles Word production locally afterward.

The core split is:

1. Qwen only revises prose and returns pure text.
2. The agent locally generates the Word file, footnotes, and tracked revisions.

## Select The Stage

1. **Before Qwen revision**
   - Read [references/qwen-revision-sop.md](references/qwen-revision-sop.md).
   - Give that paste-ready memo to the user.
   - Do not ask Qwen to emit `<ins>/<del>`.
2. **After Qwen revision**
   - Treat the returned pure-text Markdown as approved content.
   - Do not re-discuss, re-polish, shorten, or expand the argument unless the user separately asks.

## Hard Boundaries

- Preserve the supplied title, prose, quotations, punctuation, source wording, and bibliography.
- Preserve all `[^N]` footnote markers in the body and all `[^N]: ...` note definitions at the end.
- Do not silently repair missing sources, duplicate footnote labels, or non-contiguous numbering.
- Do not overwrite any source or master manuscript.
- Create one independent Word file per section unless the user explicitly asks for another packaging.
- When tracked revisions are requested for this Qwen workflow, default to **pure-text diff first**, not hand-authored `<ins>/<del>`.
- Only fall back to manual `<ins>/<del>` when the local diff result is visibly too coarse and a few local spans need tighter control.
- This skill is for **independent section-level Word output**. If the user needs to preserve the original Word file's comments, tables, or layout, coordinate with `academic-manuscript-collaboration-workflow` and use the document-aware route instead of rebuilding the file here.

## Required Markdown

Accept this structure:

```markdown
### 5. 「天命與禮論」：兩周之際天命信仰的動搖與重構

正文……[^25]

> 獨立引文……[^26]

[^25]: 腳注內容。
[^26]: （原稿此處腳注空缺，待補）
```

Require:

- headings beginning with `###` when section headings are present;
- blank lines between paragraphs;
- block quotations beginning with `>`;
- body references as `[^N]`;
- note definitions as `[^N]: note text`;
- no emoji, no process commentary, no `<ins>/<del>` in the Qwen output by default.

## Convert

### Route A: Pure-text Qwen draft -> independent DOCX without tracked revisions

Use this when the user only wants a clean Word file.

1. Save the supplied Markdown as UTF-8 `.md`.
2. Run the local AI Revision Merger:

```powershell
cd C:\Users\d8911801\WorkBuddy\2026-06-15-14-48-44\ai_revision_merger
python main.py --cli -m "C:\path\input.md" --output "C:\path\output.docx"
```

### Route B: Original text + Qwen pure-text revision -> tracked-revision DOCX

Use this when the user wants a reviewable tracked file for the section, but the source revision came back from Qwen as pure text.

1. Save the original section text as UTF-8 `orig.txt`.
   - Keep the body text.
   - Footnote definitions may remain at the end; the local diff script now strips trailing note-definition blocks before paragraph alignment.
2. Save the Qwen-polished pure-text draft as UTF-8 `polished.txt`.
   - Keep `[^N]` markers in place.
   - Keep `[^N]: ...` note definitions at the end.
3. Run the local diff step:

```powershell
python C:\Users\d8911801\.workbuddy\skills\md2docx\scripts\diff_to_tracked.py "C:\path\orig.txt" "C:\path\polished.txt" -o "C:\path\tracked.md"
```

4. Convert the generated tracked Markdown into Word tracked revisions:

```powershell
python C:\Users\d8911801\.workbuddy\skills\md2docx\scripts\convert_tracked.py "C:\path\tracked.md" --output "C:\path\tracked.docx" --author "Codex" --del-author "Codex"
```

5. Use this route only for independent Qwen section drafts. If the task instead requires preserving an existing Word file's review state or doing Word Compare directly against an original `.docx`, switch to `academic-manuscript-collaboration-workflow`.

## Validate

After conversion:

1. Confirm the CLI reports success and record the final output path.
2. Open the output read-only in Microsoft Word and confirm:
   - the file opens;
   - footnote count is correct;
   - no raw `[^N]` marker remains in body text;
   - tracked revisions are visible when Route B was used.
3. If Route B was used, inspect the revision granularity:
   - unchanged text should remain plain body text;
   - revisions should normally be word-, phrase-, or clause-level;
   - note-definition blocks should not appear as spurious deleted paragraphs.
4. Use the Documents skill only when page-level layout QA is still needed.
5. Remove temporary build files after QA. Deliver only the intended `.docx`.

## Output Defaults

- Default to the user's chosen output directory.
- If none is given for this project, use:

```text
C:\Users\d8911801\Desktop\千問潤稿獨立Word寫作
```

- Save as a new filename and never overwrite the original source file.

## Report

Report only:

- the final file link;
- whether tracked revisions were generated;
- the footnote readback status;
- any unresolved issue as `pending-confirmation`.

Do not reopen prose discussion during the conversion stage.
