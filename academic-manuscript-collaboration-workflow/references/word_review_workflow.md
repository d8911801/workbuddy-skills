# Word Review Workflow

Use this reference for `.docx` review drafts, tracked revisions, and comment handling.

When tracked revisions or footnotes must be generated from Markdown or from an old/new draft comparison tied to an existing Word file, prefer the local AI Revision Merger:

```text
C:\Users\d8911801\WorkBuddy\2026-06-15-14-48-44\ai_revision_merger\
```

Use these CLI patterns before any comment-reply pass:

```powershell
cd C:\Users\d8911801\WorkBuddy\2026-06-15-14-48-44\ai_revision_merger
python main.py --cli -m "C:\path\revised.md" --output "C:\path\output.docx"
python main.py --cli -m "C:\path\revised_with_insdel.md" --output "C:\path\tracked_revision.docx"
python main.py --cli -o "C:\path\old.docx" -m "C:\path\revised.md"
```

For cloud-Qwen pure-text revision workflows that only need an independent section-level tracked draft, a lighter local alternative is:

```powershell
python C:\Users\d8911801\.workbuddy\skills\md2docx\scripts\diff_to_tracked.py "C:\path\orig.txt" "C:\path\polished.txt" -o "C:\path\tracked.md"
python C:\Users\d8911801\.workbuddy\skills\md2docx\scripts\convert_tracked.py "C:\path\tracked.md" --output "C:\path\tracked.docx" --author "Codex" --del-author "Codex"
```

Use that `md2docx` route only when:

1. Qwen returns pure-text Markdown rather than `<ins>/<del>`;
2. the output is an independent review draft rather than a format-preserving continuation of the original Word file;
3. local paragraph/word-level diff quality matters more than preserving the original Word layout or comments.

## Verification route on this machine

Do not use LibreOffice / `soffice` as the default render path for this workflow on this computer. The stable verification route is:

1. Open the `.docx` through Word's object model.
2. Export PDF from Word, normally via `ExportAsFixedFormat`.
3. Convert the PDF to PNG with Poppler `pdftoppm` for visual QA.
4. Verify comments, footnotes, reply authors, and tracked revisions through Word's object model or OOXML structure, not through PDF rendering.

Rationale:

- Word export matches the user's actual reading environment more closely than LibreOffice.
- Poppler page images are sufficient for layout review once the PDF comes from Word.
- Comments and review metadata are structural features; PDF output is only secondary evidence for them.

## Preferred Strategy

For tracked revisions, prefer this order by default:

1. If the task is anchored to an existing reviewed Word file, prepare one clean revised draft that preserves unchanged wording and keeps paragraph structure stable.
2. Run `old.docx` versus revised Markdown or DOCX through Word Compare.
3. Inspect the result.
4. If the task instead comes from a cloud-Qwen pure-text section draft, prepare `orig.txt` and `polished.txt`, run `diff_to_tracked.py`, then convert with `convert_tracked.py`.
5. Only if the chosen route still gives revisions that are too coarse, repair the affected locations with narrower local markup and regenerate.

This is the default because compare usually uses fewer tokens than hand-marking every change and often produces a cleaner revision history when the structure is stable.

## Safe Revision Sequence

1. Copy the source `.docx` to a working file, or generate that working file first through the local AI Revision Merger if the revision source is Markdown or a comparison draft. If the source instead is a cloud-Qwen pure-text section draft, prepare the tracked Markdown locally through `diff_to_tracked.py` before converting to Word.
2. If requested, accept only the user's previous body-text revisions.
3. If the user has already completed one review round and now wants a second tracked-revision pass on top of that reviewed draft, prefer this sequence unless they ask otherwise:
   - create a new copy of the reviewed draft;
   - accept the existing body-text tracked revisions in that copy;
   - keep user comments;
   - add only the new agent revisions for the current round;
   - if using compare, compare the accepted copy against the new clean revision so the resulting redlines show only the current pass.
4. Keep user comments.
5. Turn on tracked revisions for the agent's body-text edits.
6. Prefer additive changes over paragraph replacement:
   - insert a transition before a paragraph;
   - append a sentence at the end;
   - add a new paragraph after;
   - make narrow phrase-level fixes.
7. If a paragraph has already been reviewed by the user, keep the user's wording as the base and make only the smallest local edit that handles the issue.
8. If the tracked-revision source starts as Markdown with `<ins>` and `<del>`, mark only the changed words, clauses, or sentences. Keep all unchanged text outside revision tags.
9. Do not simulate tracked changes by wrapping a whole reviewed paragraph in one `<del>` block and then pasting the new paragraph in one `<ins>` block unless the user explicitly requested a wholesale rewrite.
10. When relocating an existing passage that contains footnotes, endnotes, comment anchors, or tracked-review anchors, move the original Word range itself. Use Word-native cut/paste or `Range.FormattedText`; do not relocate it by rewriting `Range.Text`, paragraph text, or any other plain-text reconstruction.
11. After such a move, verify at the destination that the expected note/comment counts are still present before doing any wording edits. If the passage still needs rewriting, move first, verify second, edit third.
12. When discussing changes with the user, refer to passages by searchable opening words or exact quoted anchors rather than paragraph numbers.
13. Save as a new output file.
14. Add comment replies after body revision, or re-check them if added earlier.

## Comment Handling Requirements

User comments are not disposable task markers. They are part of the review record.

Required behavior:

- Preserve every user top-level comment.
- Do not delete a comment just because it was handled.
- Do not replace the user's comment text with an agent note.
- Do not create a separate floating comment as a substitute for a reply.
- Use real Word replies under the original comment.
- Reply to each comment at its own location; never collect answers to several comments under one comment.
- Reply text should be concise:
  - `已修改／修改情況：...`
  - `已補入：...`
  - `暫未改動：原因是...`

## Author Identity

The reply author must be the agent identity, normally `Codex`.

Verification must check Word's model, not only raw XML text:

- top-level comments remain authored by the user;
- each top-level user comment has the expected reply count;
- each reply author is `Codex`;
- tracked revisions still exist after comment handling.

If Word writes replies under the user's name, fix reply authors before delivery and re-open the file in Word to verify.

## Anti-Patterns

Do not:

- use XML-only pseudo-replies that Word does not display as replies;
- append agent handling text inside the user's comment body;
- remove comments after "resolving" them;
- silently drop comments whose anchors were replaced;
- replace the user's edited paragraph with an entirely new paragraph when a local addition would work.
- emit paragraph-wide delete/insert markup when the actual revision is only a few phrases or one sentence.
- relocate a note-bearing passage by copying only its visible text and leaving its footnote/endnote/comment anchors behind.

## Final Checks

Before delivery, inspect:

1. Word opens the file.
2. Source file was not overwritten.
3. Top-level user comment count matches the source review file.
4. Reply count matches intended handled comments.
5. Reply author is the agent identity.
6. Tracked revisions are visible and not accidentally accepted.
7. If any passage was moved, the destination still shows the expected footnote/endnote/comment anchors.
8. No hidden Word or conversion process is left running.

PDF or image rendering is useful but secondary. On this machine, use Word export plus Poppler PNG review as the default visual-QA path, and use Word object-model or OOXML checks for comments, footnotes, and tracked revisions.
