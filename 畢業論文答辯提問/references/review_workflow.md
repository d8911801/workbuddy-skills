# Detailed Review Workflow

This file stores the detailed operating checklist for thesis-defense question preparation.

## Scope

Use this workflow when the user wants defense questions for a thesis in Word or PDF format and does not need written review comments yet.

## Paper-by-Paper Procedure

1. Read the paper from the Word or PDF file.
2. Extract the title, abstract, chapter structure, conclusion, and references.
3. Identify the real thesis task:
   - text study
   - figure study
   - reception history
   - teaching application
   - comparative study
   - mixed structure
4. Locate the most vulnerable academic points.
5. Sample modern scholarship to verify possible AI-heavy drafting.
6. Produce the final 3-part briefing:
   - basic understanding
   - main problems
   - exactly 3 defense questions

When writing `main problems`, include a practical close-reading pointer for each major issue so the user knows exactly what to inspect without rereading the whole thesis.

If the input is PDF:

- extract text in the cleanest way available
- verify whether chapter titles and references remain legible
- if extraction is noisy, avoid false precision and lean on structure rather than line-level wording

## What Counts as a High-Value Oral-Defense Question

Prefer questions that test whether the student truly understands their own paper.

Strong questions usually require the student to:

- explain why a chapter exists
- justify a key interpretive move
- connect a cited scholar to a specific paragraph
- distinguish summary from argument
- defend the use of a modern concept on ancient material
- explain why a teaching chapter belongs in a thesis rather than as an appendix or extension

Weak questions are those that can be answered by repeating broad slogans or summary statements from the abstract.

## Orientation Brief Requirements

Before listing problems or questions, give the user a short but usable understanding of the paper.

This section should answer:

- What is the paper trying to do?
- How does it try to do it?
- What materials does it mainly use?
- What modern scholarship or theory does it rely on?
- Is the paper's real focus consistent with its title?

The goal is to let the user understand the logic of the questioning. The user should be able to ask the later questions without sounding detached from the paper itself.

## Close-Reading Pointer Rule

For each major problem, identify the smallest useful reading target for the user:

- a specific chapter
- a subsection
- a transition between chapters
- a table or classification chart
- the literature-review paragraph where a key scholar is cited
- the paragraph where a key concept is defined or first asserted

Keep the pointer concrete and preparation-oriented. The user should be able to skim that spot and immediately understand why the problem matters.

## AI Verification Checklist

For each sampled modern reference, try to confirm:

- author
- title
- publication or institution
- year / issue when easy to verify
- abstract or summary page when available

Then compare the sampled source with the thesis:

- Is the source really used, or only name-dropped?
- Does the thesis describe the source accurately?
- Can the thesis body show where the source matters?
- Does the student's literature review sound more confident than the evidence supports?

## Escalation Signals

Treat the following as strong warning signs:

- multiple sampled references cannot be verified
- journal name or issue information is repeatedly inaccurate
- the thesis cites a scholar but the body never meaningfully uses that scholar's point
- the abstract of a sampled article does not match the thesis's description of it
- the literature review looks fuller than the body can sustain

## Default Question Families

### AI verification

Ask the student to explain one designated modern source in terms of exact source data, abstract/core view, body placement, and argumentative necessity.

Do not leave the designated source unspecified. For each thesis, recommend at least one concrete modern source that the user should point to on site, and ideally one backup source.

Pick sources that are most diagnostic:

- central to the thesis claim
- weakly digested in the body
- suspicious in title / source formatting / usage
- difficult to improvise convincingly without real reading

## Batch / Child-Agent Notes

When many theses are processed in one run:

- assign only one thesis per child agent
- let child agents generate draft briefings only
- keep final question sharpening and source designation in the main agent
- maintain a running master record so context loss does not erase prior judgments

### Title and structure

Ask why later chapters belong to the thesis question and whether the paper would become more focused if one appended chapter were removed.

### Core argument

Ask the student to show which textual details support a central concept such as subjectivity, moral judgment, gendered writing, political function, or narrative value.

### Theory control

Ask how the student avoids projecting modern theory directly onto premodern material.

### Material adequacy

Ask whether the evidence base is sufficient to support a large conclusion, especially when the paper generalizes from one character or one episode.
