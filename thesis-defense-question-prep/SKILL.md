---
name: 論文答辯提問準備
description: Prepare live oral-defense questions for graduation theses in Word or PDF format. Use when the user provides a thesis docx or pdf and wants on-site questioning rather than written review comments, especially for Chinese literature, classical-text, or teaching-oriented theses. Produce exactly three defense questions, including one AI-verification question.
---

# Thesis Defense Question Prep

Prepare defense questions, not written review comments, unless the user explicitly asks for comments. Read one thesis at a time unless batch handling is explicitly requested.

## Core Output
For each thesis, produce a 3-part briefing:
1. Basic understanding of the paper
2. Main problems
3. Three oral-defense questions

The third part must contain exactly 3 questions. One must be an AI-verification question; two additional questions should target the weakest or most revealing content issues.

## Working Standard
Judge whether the paper reaches graduation-thesis standards: title/content fit, clear research question, coherent chapters, real argument development, accurate textual interpretation, trustworthy historical/scholarly claims, careful theory use, and whether teaching/application sections drift away from the main task.

## Required Workflow
1. Read the thesis from Word or PDF. Extract title, abstract, chapter headings, conclusion, and references.
2. Diagnose the most important issues that are best exposed through oral defense questioning.
3. Verify 2 to 4 modern references when possible, prioritizing suspicious or central sources. Do not claim definite AI use unless evidence is unusually strong; frame it as a defense-verification point.
4. Produce the final 3-part briefing. Add practical close-reading pointers in the problems section.

## AI Question Pattern
Ask the student to explain one designated modern scholarly source cited in the thesis: exact title, author, database/publication source, abstract/core argument, where it is used in the thesis, and what part of the argument would weaken if removed. Recommend at least one specific source to designate on site and one backup when possible.

## Batch Mode
Each child agent handles only one thesis at a time. Child agents draft only; the main agent performs final QA, sharpens questions, and normalizes the AI-verification source recommendation.

## References
For detailed checklist, use `references/review_workflow.md`.
