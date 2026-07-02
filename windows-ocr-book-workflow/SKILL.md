---
name: Windows書籍OCR工作流
description: Use for Windows-native OCR, split, verify, and archive work on Chinese PDF books when the goal is reliable completion with a local controller, actual folder checks, and resumable one-book or batch processing.
---

# Windows OCR Book Workflow

## Purpose

Use this skill for long-running PDF book workflows on Windows where Codex must actually finish the line: inspect the real state, avoid rerunning completed books, OCR when needed, keep split outputs readable, and archive results into clean `浣滆€咃細鏇稿悕` folders.

## Default stance

- Prefer a local controller and local scripts.
- Do not use conversational Hermes dispatch as the main production path.
- Treat progress JSON as a hint only; the real source of truth is the live folder state.
- Do not assume a launched OCR command will finish by itself. Patrol it.

## First inspection

Before restarting anything, inspect in this order:

1. Whether OCR, batch, or controller processes are still running and still making progress.
2. Whether the source root already has `浣滆€咃細鏇稿悕` folders.
3. Whether root-level OCR artifacts already exist for a book.
4. Whether split PDFs already exist and are readable.
5. Only then read progress files such as `state/shangbo-ocr-progress.json`.

If a book folder already exists, do not blindly rerun that book.

## Choose the right mode

### Mode A: Standard whole-book OCR package

Use when the deliverable really needs:

- original PDF
- searchable `(OCR).pdf`
- copyable UTF-8 `.txt`
- `.report.json`
- `.report.md`
- archived `浣滆€咃細鏇稿悕` folder

Flow:

1. `scripts/run-windows-ocr.ps1`
2. `scripts/verify-windows-ocr.ps1`
3. `scripts/organize-ocr-book.ps1`

### Mode B: Split-oriented workflow

Use when OCR is only a means to make the book readable and splittable for later agent work.

Rules:

- If split PDFs already exist and can yield text on spot checks, treat the book as completed enough.
- If split PDFs exist but have no usable text layer, OCR still needs to be added.
- For books that still need OCR plus splitting, prefer **whole-book OCR first, then split from the OCR PDF**. This is usually faster and more stable than OCRing each split file one by one.

### Mode C: Resume batch safely

Use batch control only when many books remain and the environment is already stable.

- Prefer `scripts/resume-shangbo-ocr-all.ps1`.
- Keep a separate completed list so the controller can skip finished books.
- If the controller becomes unreliable, fall back to one-book loops instead of defending the batch script.

## Verification rules

For the full OCR package, use `scripts/verify-windows-ocr.ps1`.

Minimum pass signal:

- page counts match
- sampled pages are non-empty
- `.txt` is UTF-8
- report page count matches
- `ready_for_organize = true`

For split-oriented work, verify readability directly on representative split PDFs. A quick PyMuPDF text extraction check is enough if the project goal is readability rather than the five-file package.

## Archive rules

- Final folder name should normally be `浣滆€咃細鏇稿悕`.
- Keep the complete book PDF inside the book folder, not loose in the root.
- After whole-book OCR finishes, move the whole-book package into the author folder so the root stays clean.
- If root-level complete-book PDFs are already safely archived inside folders, they may be moved out of the root or to recycle bin, but only after confirming the folder copy exists.

## Reference copy rules

- After chapter splitting is finished, copy each usable chapter PDF into the matching `參考文獻\\依篇目分類\\{篇目資料夾}` folder when its chapter title matches an 上博楚簡篇名.
- Treat this as a duplicate-copy step, not a move; keep the source chapter PDF in the book folder.
- If a chapter name cannot be aligned to an 上博楚簡篇名, leave it in place for later review instead of forcing a match.
- A book is not fully wrapped until the chapter PDFs have both been archived in the book folder and duplicated into the reference classification tree when applicable.

## Patrol rules

Never fire and forget. During long OCR runs, keep checking:

- is the process still alive
- has file size or modified time changed
- did new artifacts land
- did verify finish
- did organize finish

If a book fails, record exactly which book and which step failed.

## Project-specific notes

For the current Shangbo / early Chinese thought workflow, also read:

- `references/shangbo-ocr-notes.md`
