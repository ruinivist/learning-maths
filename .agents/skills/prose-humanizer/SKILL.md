---
name: prose-humanizer
description: Write and edit this repository's maths notes, explanations, documentation, and comments using plain prose and humanizer guidance. Use for writing and LaTeX edits while preserving mathematical meaning.
---

# Prose and humanizer

## Maths notes

- Write maths with short explanations. Define terms and symbols before using them; avoid long paragraphs.
- Preserve mathematical meaning, assumptions, quantifiers, notation, and proof steps. Keep necessary technical terms.
- Use dollar-based KaTeX: `$...$` inline and `$$...$$` for display maths.
- Keep each equation together. Do not split at every equals sign or add line breaks without a mathematical reason.
- Preserve the author's useful examples, intuition, and voice. Do not add anecdotes, opinions, or invented facts to make text sound human.

## Plain prose

- Use familiar words and simple verbs: "use," "help," and "is" rather than "leverage," "facilitate," and "serves as."
- Prefer active voice when it reads naturally. Remove filler, needless adverbs, and repeated explanations.
- Use American English in prose; preserve identifiers, quotations, and established mathematical terminology.
- Expand unfamiliar acronyms. Keep common ones and defined mathematical abbreviations.
- Avoid corporate language, inflated claims, and calling a task "easy," "simple," or "obvious."
- Write notes and documentation so they stand alone. Leave out chat history, review discussions, and accounts of how the text was written.

## Humanizer pass

- State the concrete claim. Remove grand claims about significance, promotional language, and shallow phrases such as "highlighting its importance."
- Replace staged openings, rhetorical questions, slogans, and "not X, but Y" formulas with direct statements. Preserve contrasts that express a necessary mathematical distinction.
- Remove chatbot greetings, praise, offers to continue, and generic closing summaries from notes.
- Avoid forced groups of three, repeated sentence templates, synonym cycling, and dramatic fragments. Keep terminology consistent.
- Keep uncertainty that affects the claim. Remove stacked hedges; never replace an unknown with a plausible guess or invent a citation.
- Treat these as editing cues, not proof that text was AI-written. Leave effective prose, quotations, and deliberate stylistic choices alone.

## Formatting and review

- Use sentence case for headings and keep their hierarchy shallow.
- Use lists for parallel items or steps. Avoid decorative bold labels, emojis, and unnecessary headings.
- Use backticks for filenames, commands, and code identifiers; use maths delimiters for mathematical symbols.
- Keep prose paragraphs on one source line. Avoid excessive dashes and exclamation marks.
- Before finishing, check that the edit preserves the maths and removes repetition without losing information. Return the edited text without draft rewrites or an editing report unless requested.
- For commits, follow the repository convention: lowercase conventional commits, at most eight words. Add a body only when the reason needs explanation.
