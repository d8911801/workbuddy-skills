---
name: 學術書稿協作工作流
description: Use for academic manuscript collaboration, especially Word review drafts, tracked revisions, comment digestion, source-based rewriting, and protecting the user's edits across scholarly writing projects.
---

# Academic Manuscript Collaboration Workflow

Use this skill when working with the user on academic books, articles, research notes, review drafts, or Word manuscripts. It is topic-neutral: do not import project-specific arguments, chapter theses, or source judgments unless the current task provides them.

## Start Every Task

1. State the current scope in one sentence: project, chapter/section/subsection, or document unit.
2. Treat the newest manuscript file named by the user as the source of truth.
3. Do not expand to other chapters, files, or topics unless needed for a narrow cross-reference.
4. If the user is asking for discussion, digest first and wait for confirmation before drafting.
5. If the user asks for a direct paste-in paragraph, answer in the chat and do not edit files.

## Collaboration Defaults

- Preserve the user's intellectual decisions. If the user has already edited a passage, prefer additive revision: insert before, append after, or make local phrase edits.
- Avoid deleting the user's revised paragraph and rewriting it wholesale unless the user explicitly asks for a rewrite.
- When the user has already reviewed a passage, revise at the word, phrase, or sentence level unless the user explicitly asks for a full rewrite; do not replace the whole paragraph just to add evidence or polish language.
- When preparing Markdown for tracked revisions, preserve unchanged wording outside `<ins>` and `<del>` tags. Do not wrap an entire reviewed paragraph in one delete and one insert if the real change is only local.
- For tracked-revision drafts, default to the smallest visible change set that accurately reflects the revision. If a sentence can be fixed by replacing one clause, do not delete and reinsert the whole sentence.
- If a full-sentence or full-paragraph replacement is truly unavoidable, say so explicitly in the delivery note and explain why narrower edits would be misleading or impractical.
- When discussing a location in a manuscript, identify it by searchable opening words or a quoted phrase, not by paragraph numbers alone.
- When preparing a pure-text digest or施工清單 for Word comments, quote the user's original comment text first, then give the handling plan or status. Do not list only comment numbers, otherwise the user may lose the context while reviewing.
- When a Word revision round handles the user's comments, add a real Word reply under each handled original comment, authored as `Codex`, briefly stating how it was handled or why it remains pending. Do not rely only on the final chat message or a separate施工清單 as the handling record.
- Before generating a new Word artifact, if the user is still in the discussion, comparison, or placement-confirmation stage, prefer creating a small side-reading reference file inside the current local working folder so the user can open it from the sidebar while reviewing.
- For those discussion-stage side-reading files, default to a plain-text `.txt` reference file saved under the exact local sub-workspace the user is actively using for that unit, not a higher-level workspace root or the manuscript root.
- In the current Shangbo Chapter 3 `情論` workflow, the default side-reading target folder is `C:\Users\d8911801\Desktop\3.第三章 道德思想：性情、工夫論與君子觀工作區\性心情論\情論`.
- The key requirement is local-folder visibility inside the user's actual working subfolder, not Markdown specifically. A `.txt` side-reading file placed in that active local sub-workspace is preferred over a broader desktop root, manuscript root, or other external path because the latter may fail to appear where the user expects and may force a second window.
- Unless the user explicitly asks for a summary or analysis sheet, that side-reading `.txt` should mirror the user's manuscript content itself rather than the agent's generated commentary. Default to exporting the relevant passage, section, or full current local unit from the manuscript with visible paragraph numbering or other direct anchors.
- For discussion-stage side-reading text, do not add extra outer numbering such as `1. 2. 3.` when the user mainly needs to track the manuscript by line or paragraph position. Let the manuscript text carry the discussion, and use paragraph numbers or line positions as the primary anchors.
- For long manuscripts, handle one local unit at a time. Do not launch a full-document polish while content is still being drafted or stitched; defer whole-document unification until the user asks for that pass.
- Separate internal working notes from reader-facing prose. Do not put process language into formal manuscript text.
- Treat dated patch labels and workflow markers such as `【YYYY-MM-DD補強｜主題】`, `【待補】`, `TODO`, revision-round labels, and agent-facing instructions as non-reader-facing material. Before delivering a revised manuscript, scan the full visible body text and remove them after confirming that the associated prose has been integrated.
- Removing a marker is not enough when it separates duplicate drafting layers. Compare the paragraphs on both sides, merge or delete repetition as needed, and verify that the argument remains continuous after the marker is gone.
- If a marker represents an unresolved scholarly or structural issue, do not silently erase it. Convert it to a real Word comment or report it as `pending-confirmation`. User comments are review records and are never included in this marker-cleanup rule.
- When unsure whether a note is resolved, keep it visible and mark the handling status rather than silently deleting it.
- When relocating existing manuscript passages inside a Word file, first check whether the source range contains footnotes, endnotes, comment anchors, or tracked-review anchors.
- Hard rule: if such anchors are present, never relocate the passage by rewriting paragraph text, `Range.Text`, Markdown-only reconstruction, or any other plain-text move. Move the original Word range itself, such as via Word-native cut/paste or `Range.FormattedText`, so the anchors travel with the passage.
- For passages with notes or review anchors, the safe sequence is: move the original anchored range first; verify that the destination still contains the expected footnote/endnote/comment counts; only then perform local wording edits or compare generation.
- Use subagents for separable research tasks such as source lookup, bibliography checks, original-text extraction, and technical workflow validation. The main agent must review and integrate their outputs.

## Word Review Drafts

For Word files, keep two routes distinct. When the task must preserve an existing Word file's layout, comments, tables, or review state, prefer the local AI Revision Merger at `C:\Users\d8911801\WorkBuddy\2026-06-15-14-48-44\ai_revision_merger\` for Markdown to DOCX, `[^N]` to real Word footnotes, `<ins>/<del>` to native tracked revisions, or old/new DOCX compare. When the source revision comes back from cloud Qwen as pure-text Markdown and the deliverable is an independent section-level tracked draft, the local `md2docx` route at `C:\Users\d8911801\.workbuddy\skills\md2docx\scripts\diff_to_tracked.py` plus `convert_tracked.py` is a valid lower-token alternative. Use the Documents skill or another Word-verifiable workflow only for tasks those generators do not cover, such as comment replies, review-state inspection, or layout QA.

On this machine, do not use LibreOffice / `soffice` as the default render or verification path for Word review work. The standing verification route is: Word COM or the Word object model opens the file, Word exports PDF, Poppler `pdftoppm` converts selected or all pages to PNG for visual QA, and comments / footnotes / tracked revisions are checked through Word's object model or OOXML structure rather than through LibreOffice rendering.

Default tracked-revision strategy:

1. When both an old version and a revised clean version are available and the task is tied to an existing reviewed Word file, prefer `old/new compare` first. This is the default because it usually costs fewer tokens and preserves a more natural revision history.
2. While preparing the revised clean version for compare, keep paragraph order, sentence order, and unchanged wording as stable as reasonably possible so Word Compare can stay granular.
3. If the revision source is cloud Qwen pure text and the output is an independent section draft, prefer `orig.txt` + `polished.txt` -> `diff_to_tracked.py` -> `convert_tracked.py` before asking Qwen to emit `<ins>/<del>`.
4. Use `<ins>/<del>` only as a fallback when compare output is too coarse, when a few local changes need tighter control, or when compare misreads structural edits.

Hard rules:

1. Do not overwrite source review files or master manuscripts. Save a new file.
2. If starting a new revision round, accept the user's prior body-text revisions only when requested or clearly appropriate.
3. Preserve all user comments unless the user explicitly asks to remove them.
4. AI changes should appear as tracked revisions when editing a reviewed draft. If those edits are first prepared in Markdown, generate the working `.docx` through the document-aware route that matches the scenario: AI Revision Merger for compare/preserve-format work, or the local `md2docx` diff-plus-convert route for cloud-Qwen pure-text section drafts.
5. If responding to comments, use real Word comment replies under the original user comments.
6. Comment replies must be authored by the current agent identity, normally `Codex`, not by the user.
7. Reply to each user comment under that specific original comment; do not put replies for multiple comments under one unrelated comment.
8. Verify in Word that top-level user comments, reply counts, reply authors, and tracked revisions are correct before delivery.
9. Run a final body-text search for internal working markers and confirm that none remain unless the user explicitly asked to retain them.
10. When the user has already reviewed one tracked-revision round and wants a further pass, prefer this sequence unless they ask otherwise: create a copy, accept the user's existing body-text revisions in that copy, then add only the new agent revisions for the current round. Deliver the new tracked file against that accepted copy so the visible redlines show only the latest pass.
11. If the user needs to inspect paragraph numbering, move plans, or local placement before Word generation, first provide a side-reading file inside the exact local sub-workspace currently in use for that unit. By default this should be a plain-text `.txt` file with visible paragraph numbering or other direct anchors, and it should usually contain the user's manuscript text itself rather than an agent-written digest. In the current Shangbo Chapter 3 `情論` workflow, use `C:\Users\d8911801\Desktop\3.第三章 道德思想：性情、工夫論與君子觀工作區\性心情論\情論` unless the user later names a different active sub-workspace. Treat that reference file as a discussion aid, not as the final manuscript artifact.
12. For visual QA on this machine, default to Word export rather than LibreOffice: export the working `.docx` to PDF from Word, convert the PDF to PNG with Poppler `pdftoppm`, and inspect those images. For comments, footnotes, reply authors, and tracked revisions, treat Word's object model and OOXML structure as the source of truth; do not use PDF rendering as the primary verification method for those features.

Read [word_review_workflow.md](references/word_review_workflow.md) before editing a Word review draft with tracked changes or comments. Follow its generator commands whenever the revision source starts as Markdown or a comparison draft.

## Scholarly Writing

General rules:

1. Quote or cite source material before analyzing it when the argument depends on wording.
2. Do not silently omit key words from original-text evidence.
3. Keep material layers distinct: primary text, later transmitted text, commentary, modern scholarship, and the user's own prior work.
4. Avoid anachronistic modernization. Modern analytic concepts may be used only as analytic frames, not as unmarked claims about the source material itself.
5. Avoid equating different periods, textual layers, genres, or attributed voices without qualification.
6. If variants or uncertain readings matter, flag them and let the user decide the preferred form.
7. Present research history by first stating a scholar's contribution, then explaining how the current draft uses, extends, or differs from it.

Read [research_writing_rules.md](references/research_writing_rules.md) when drafting or revising scholarly prose.

## Delivery

Before final delivery, report only what matters:

- output file path, if a file was created;
- whether the source file was preserved;
- whether tracked revisions/comments/replies were verified;
- any unresolved issue that still needs user judgment.

If an error occurs, acknowledge the missed requirement directly, correct the artifact, and verify the correction against the user's actual standard.
