---
name: 畢業論文格式審查
description: 用於審查中文本科畢業論文格式，尤其是漢江師範學院及相近院校的格式要求。重點檢查段落、字體、目錄、表格、引文、標點、參考文獻等可見版面問題，並優先吸收既有 Word 批註中的教師審查習慣。除非教師批註明確要求，否則不做內容觀點審查。
---

# 畢業論文格式審查

Review one thesis at a time.

## Workflow

1. Read the current paper first.
2. If the document contains teacher comments, extract them before reviewing.
3. Apply the saved review principles from `references/principles.md`.
4. Use a paper-visual standard:
   visible layout, paragraphing, typography, TOC appearance, table titles, quotation shapes, punctuation shape, reference display.
5. Do not over-focus on computer-internal style settings when the printed result looks acceptable.
6. If the user asked for a re-review, separate:
   issues already mentioned by the teacher,
   newly found issues.
7. If the user asks for issues to be written back into the Word file as comments, use actual Word/WPS comment objects in the source document.
8. When writing back Word comments:
   preserve all existing teacher comments unless the user explicitly asks to replace them;
   keep already reviewed files untouched when the user says they are done;
   use the user's own visible comment-author name from the document set;
   never leave newly added comments under `Codex`;
   verify after saving that the displayed comment author is the user's name.

## Output Rules

Produce two outputs unless the user requests otherwise:

1. Student-facing report:
   each issue should include location, clear explanation, and a concrete fix example.
2. Teacher short-phrase version:
   one short comment per issue for Word/WPS marginal notes.

If the teacher short-phrase version is inserted directly into Word/WPS, keep the comments short, location-specific, and consistent with the user's established marginal-note style.

## Location Rules

Do not use TSV line numbers or internal audit coordinates as the main locator.

Prefer:

- chapter / section
- nearby heading
- a short sentence snippet
- reference item number

## Reference Rules

When reporting reference issues:

1. Always state the item number.
2. Follow the template and saved teacher conventions.
3. Do not force mechanical punctuation unification across the whole list.

## Scope Guardrails

1. Review formatting first, not argument quality.
2. However, if the teacher's established comments repeatedly treat an item as required for formal submission, keep checking it.
3. Prefer concise, actionable reports over exhaustive technical diagnostics.

Read `references/principles.md` before producing the final review.
