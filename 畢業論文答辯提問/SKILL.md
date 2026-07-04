---
name: 畢業論文答辯提問
description: 用於閱讀單篇畢業論文或學位論文，整理基本理解、主要問題與三道現場答辯提問；其中至少一題用來核實學生是否真正讀過並使用其所引現代研究成果。
---

# 畢業論文答辯提問

Prepare defense questions, not written review comments, unless the user explicitly asks for comments.

Read one thesis at a time unless the user explicitly asks for batch handling.

For Word files, follow the document-reading workflow first so the paper is understood from the body text, chapter structure, abstract, and references rather than from the filename or user summary alone.

If the user later asks to write the generated issues or questions back into the thesis as Word comments, use actual Word comment objects in the original file rather than a separate note file whenever possible.

When adding Word comments:

- preserve all existing teacher or user comments unless the user explicitly asks to replace them
- if some files were already manually reviewed and the user says not to touch them, skip them completely
- match the visible comment-author name already used by the user in that document set
- never leave newly added comments under `Codex`; rewrite or recreate them so the displayed author is the user's own name
- after insertion, verify that the comment author shown in Word is the user's name rather than the agent name

For PDF theses, extract the text as faithfully as possible and then apply the same review standard. If PDF extraction quality is visibly noisy, still produce a best-effort briefing, but do not pretend to have line-level certainty; rely more on chapter headings, reference lists, and repeated structural signals.

## Core Output

For each thesis, produce a 3-part briefing in this order:

1. `Basic understanding of the paper`
2. `Main problems`
3. `Three oral-defense questions`

The third part must contain exactly 3 questions:

1. One `AI verification` question.
2. Two additional questions chosen from the paper's weakest or most revealing content issues.

Do not default to the same two non-AI question types every time. Choose the three questions that best test whether the paper truly reaches thesis standards.

Keep the questions ready for live oral use. They should be direct, specific, and hard to evade.

## Working Standard

Judge the paper by whether its content reaches the expected threshold for a graduation thesis. This includes, but is not limited to:

- whether the title matches the actual content
- whether the research question is clear
- whether the chapter structure is coherent
- whether the argument genuinely develops rather than merely piles up material
- whether textual interpretation is accurate
- whether historical or scholarly claims are trustworthy
- whether modern theory is used carefully rather than mechanically projected backward
- whether teaching-application or modern-value sections drift too far away from the main research task
- whether the paper has basic academic value beyond generic summary

Writing-level issues may also matter when they affect thesis quality, especially:

- missing or weak introduction
- missing or weak conclusion
- missing transition logic between chapters
- abrupt shifts in topic or method

Ignore document-format trivia such as fonts, line spacing, or page layout unless the user explicitly asks for those.

## Required Workflow

### 1. Read the thesis

- Extract the full text.
- Identify the title, abstract, chapter headings, conclusion, and reference list.
- Build a quick internal map of what the paper claims to study and what it actually does.

If handling a PDF:

- extract text page by page when possible
- check whether headings, references, and chapter boundaries remain legible
- if extraction is noisy, avoid overclaiming fine-grained textual certainty

### 2. Diagnose the paper's most important issues

Focus on the issues that are best exposed through oral defense questioning.

Prefer high-yield weaknesses such as:

- mismatch between title and body
- blurred research object
- chapter arrangement that does not serve the thesis question
- conclusions that outrun the evidence
- theoretical labels that are asserted but not demonstrated
- classroom-application chapters that feel appended rather than organically derived
- overconfident claims based on thin textual evidence

### 3. Perform AI-use verification

This step is mandatory for every paper.

Check the reference list and the literature-review section for signs that the student may have heavily relied on AI or search-tool stitching.

Look first for internal warning signs:

- smooth but generic literature review language
- many cited modern scholars but weak linkage to the body
- vague phrases like `some scholars believe` without precise use
- references that feel suspiciously convenient or unusually generic
- arguments that cite modern scholarship but never show how that scholarship is used

Before turning the diagnosis into questions, prepare a short orienting brief so the user understands the paper's basic shape. This brief is not a full review comment. It should give the user enough command of the paper to understand why the later questions matter.

When listing the main problems, also tell the user which chapter, section, or part of the paper is most worth close reading for each problem. The user should not have to read the whole thesis carefully. Point them toward the smallest set of places that will let them understand and ask the questions confidently.

The orienting brief should usually include:

- what the paper is mainly trying to argue
- how the argument is organized chapter by chapter
- what primary materials or corpora it relies on
- what modern scholarship or theoretical tools it relies on
- where the paper's center of gravity actually lies

Then verify a small sample of modern scholarship on the web.

## Web Verification Rules

Verify 2 to 4 modern references, not the whole bibliography.

Prioritize:

- references heavily used in the literature review
- references that support key claims
- references with suspicious titles or source formatting
- recent articles, theses, or low-visibility publications

For each sampled item, check:

1. whether the author really wrote it
2. whether the title is accurate
3. whether the source is accurate
4. when an abstract is available, whether the thesis's understanding of that work broadly matches the abstract

Use CNKI first when available through the user's authenticated browser session.

If CNKI is unavailable, blocked, or incomplete, use reliable fallbacks such as:

- Wanfang
- CQVIP / Qikan pages
- journal or publisher pages
- university thesis repositories
- public institutional pages that can confirm thesis authorship or degree records

Treat web verification as evidence gathering, not as a hunt for certainty. A reference that cannot be found is not automatically fake. But if multiple sampled items have title/source mismatches or the paper's description does not match the abstract, treat that as a serious warning sign.

Do not claim the student definitely used AI unless the evidence is unusually strong. Prefer formulations such as:

- the literature use appears insufficiently verified
- the paper may rely heavily on AI or stitched search results
- this should be tested in the oral defense

### 4. Turn the diagnosis into the final 3-part briefing

One question must be the AI-verification question.

Design it so that even if students get the question 15 minutes in advance, they still cannot easily survive by quickly searching titles on their phones.

The best pattern is to force them to connect four layers at once:

- source identity
- source content
- source location in the thesis
- argumentative function

Use this default AI-question template:

`Please answer using one modern scholarly source cited in your thesis, which I will designate on site. Explain its exact title, author, and database or publication source; summarize its abstract or core argument; state where in your thesis you actually used it; and explain what part of your argument would weaken if this source were removed.`

Do not stop at the generic template. For each paper, identify at least one specific modern source that the user should preferably designate on site, and when possible give one backup option.

Choose the recommended source strategically. Prefer:

- a source central to the paper's main argument
- a source cited in the literature review but weakly integrated into the body
- a source whose title, source data, or usage looks unstable
- a source that would be hard for the student to bluff about in 15 minutes

When presenting the AI-verification question in the final answer, also add a short note such as:

- `Recommended source to designate on site: ...`
- `Backup source: ...`

This recommendation should help the user know exactly which cited work to ask about during the defense.

Then choose two more questions from the paper's most revealing content problems. Common families:

- title/content fit
- chapter-logic coherence
- key-concept justification
- evidence-to-conclusion chain
- theory projection risk
- research-value clarification

## Final Response Structure

### 1. Basic understanding of the paper

Write a compact orientation for the user so they can see the paper's logic before asking questions.

Include, as relevant:

- the paper's main claim or argumentative direction
- the chapter path the student uses to reach that claim
- the main primary materials
- the main secondary materials, theories, or research frames
- whether the paper is mainly doing textual analysis, historical reconstruction, theoretical relabeling, teaching extension, or some mixture

Do not let this section become a long summary. Its job is to help the user understand the later questions and not appear uninformed at the defense.

### 2. Main problems

State the most important weaknesses clearly and concretely.

Prefer the 2 to 4 issues that most affect whether the paper reaches thesis standards. These may involve:

- structural mismatch
- blurred research problem
- weak evidence chain
- overextension of theory
- unreliable or thin source use
- appended teaching/application chapters
- suspicious literature handling

After each major problem, add a short `Suggested close-reading spot` note. This should point to the most useful chapter, section, table, literature-review paragraph, or case-analysis segment for the user to inspect before the defense.

These close-reading pointers should be practical, for example:

- `read the literature review and the first paragraph where that scholar is cited`
- `read Chapter 3, section 2, where the key concept is first defined`
- `read the transition from Chapter 3 to Chapter 4`
- `read the table that claims to classify commentators, then the paragraph immediately below it`

The goal is to reduce the user's preparation burden while increasing confidence and precision in live questioning.

### 3. Three oral-defense questions

List exactly 3 questions.

At least one must be the AI-verification question.

Each question should be understandable on its own and should visibly connect back to the problems identified above.

## Batch / Multi-Agent Mode

When the user is processing many theses in one session, keep the single-paper quality bar intact and scale only the operations.

Rules:

- each child agent should handle only one thesis at a time
- child agents should produce initial drafts only, not final deliverables
- the main agent must perform final QA, sharpen the questions, and normalize the AI-verification source recommendation
- if cost matters, child agents may use a cheaper model and moderate reasoning, but the main agent must preserve the final quality bar
- do not let multiple child agents work on the same thesis unless the user explicitly wants internal parallel decomposition

In batch mode, maintain a master summary record containing:

- thesis title
- basic understanding
- main problems
- suggested close-reading spots
- the three final questions
- the recommended on-site AI-verification source and backup source

If the user asks for a final field-use report, generate a clean consolidated document from that master record.

If batch work later expands from question generation to direct Word commenting, keep the same safeguards in every child-agent handoff:

- child agents may draft comment text or anchor positions
- the main agent must ensure the final comments are inserted into Word with the user's author name
- do not let different child agents leave mixed visible author names in the same batch

## Output Rules

Default to the 3-part structure above, even when the user only asks for questions later in the workflow. The orientation and problem sections should stay concise but should still be present.

When helpful, label the 3 questions briefly:

- `AI verification question`
- `structure question`
- `core argument question`

If the user is processing multiple theses, keep an internal running record of:

- thesis title
- the short orientation
- the main problems
- the 3 final questions
- which question is the AI-verification question

When all theses are done, use that record to assemble the final on-site questioning document.

## References

For the detailed operating checklist, use [references/review_workflow.md](./references/review_workflow.md).
