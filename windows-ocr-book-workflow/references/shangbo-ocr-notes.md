# Shangbo OCR Notes

## Repo and source roots

- Repo: `C:\Users\d8911801\Documents\多 Agent工作流\codex-multi-agent-workflow`
- Source root: `C:\Users\d8911801\WPSDrive\646045039_2\WPS云盘\電子書（gp22）\6.出土文獻\思想學術\書籍`

## Useful scripts

- `scripts/run-windows-ocr.ps1`
- `scripts/verify-windows-ocr.ps1`
- `scripts/organize-ocr-book.ps1`
- `scripts/run-shangbo-ocr-batch.ps1`
- `scripts/run-all-shangbo-ocr.ps1`
- `scripts/resume-shangbo-ocr-all.ps1`

## State files

- `state/shangbo-ocr-batches.json`
- `state/shangbo-ocr-progress.json`
- `state/shangbo-ocr-master-progress.json`
- `state/shangbo-ocr-completed.json`

## Lessons from the June 2026 rollout

1. The main problem was not Paddle GPU support. GPU OCR worked.
2. The unstable part was the handoff chain: long batch control, weak patrol, and incomplete cleanup.
3. Do not trust progress JSON alone. Always compare it with the actual root folder, author folders, and running processes.
4. A visible `作者：書名` folder often means the book is already complete enough and should be skipped.
5. Some older books were already split by an earlier workflow. Split files can count as done if they are readable.
6. If split files exist but have no readable text layer, OCR is still needed.
7. For split recovery, whole-book OCR first and then splitting from the OCR PDF is more efficient than OCRing split files one by one.
8. WPS cloud sync can make moves look inconsistent for a moment. Confirm both destination presence and root cleanup.
9. When only a few books remain, one-book loops are often faster and safer than repairing the full controller.

## Current naming convention

- Standard archive folder: `作者：書名`
- Standard OCR PDF suffix: `(OCR)`

