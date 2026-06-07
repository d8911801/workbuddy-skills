---
name: academic-manuscript-collaboration-workflow
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
- Separate internal working notes from reader-facing prose. Do not put process language into formal manuscript text.
- When unsure whether a note is resolved, keep it visible and mark the handling status rather than silently deleting it.
- Use subagents for separable research tasks such as source lookup, bibliography checks, original-text extraction, and technical workflow validation. The main agent must review and integrate their outputs.

## Word Review Drafts

For Word files, use the Documents skill or an equivalent Word-verifiable workflow.

Hard rules:

1. Do not overwrite source review files or master manuscripts. Save a new file.
2. If starting a new revision round, accept the user's prior body-text revisions only when requested or clearly appropriate.
3. Preserve all user comments unless the user explicitly asks to remove them.
4. AI changes should appear as tracked revisions when editing a reviewed draft.
5. If responding to comments, use real Word comment replies under the original user comments.
6. Comment replies must be authored by the current agent identity, normally `Codex`, not by the user.
7. Verify in Word that top-level user comments, reply counts, reply authors, and tracked revisions are correct before delivery.

Read [word_review_workflow.md](references/word_review_workflow.md) before editing a Word review draft with tracked changes or comments.

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
