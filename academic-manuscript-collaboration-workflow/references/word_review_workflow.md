# Word Review Workflow

Use this reference for `.docx` review drafts, tracked revisions, and comment handling.

## Safe Revision Sequence

1. Copy the source `.docx` to a working file.
2. If requested, accept only the user's previous body-text revisions.
3. Keep user comments.
4. Turn on tracked revisions for the agent's body-text edits.
5. Prefer additive changes over paragraph replacement:
   - insert a transition before a paragraph;
   - append a sentence at the end;
   - add a new paragraph after;
   - make narrow phrase-level fixes.
6. Save as a new output file.
7. Add comment replies after body revision, or re-check them if added earlier.

## Comment Handling Requirements

User comments are not disposable task markers. They are part of the review record.

Required behavior:

- Preserve every user top-level comment.
- Do not delete a comment just because it was handled.
- Do not replace the user's comment text with an agent note.
- Do not create a separate floating comment as a substitute for a reply.
- Use real Word replies under the original comment.
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

## Final Checks

Before delivery, inspect:

1. Word opens the file.
2. Source file was not overwritten.
3. Top-level user comment count matches the source review file.
4. Reply count matches intended handled comments.
5. Reply author is the agent identity.
6. Tracked revisions are visible and not accidentally accepted.
7. No hidden Word or conversion process is left running.

PDF or image rendering is useful but secondary. If LibreOffice fails, use Word export or Word object-model checks instead of assuming the document is invalid.
