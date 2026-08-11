---
name: organize-learning
description: Consolidate questions and answers from accessible learning conversations into one existing Notion handbook, organized by a stable knowledge map with a chronological learning index. Use when the user asks to organize today's learning, consolidate a specified date or date range, update a learning handbook, deduplicate study notes, or invokes $organize-learning. Do not use for generic Notion editing, unrelated conversation summaries, or creating a new workspace without explicit permission.
---

# Organize Learning

Turn scattered learning conversations into one structured, searchable handbook without duplicating content.

## Resolve the Target

1. Determine the target date or date range. Default to today in the user's time zone.
2. Identify the existing destination handbook from the request, current context, or a connected Notion search.
3. If more than one plausible destination exists, ask the user to choose.
4. If no destination exists, ask for a page URL or explicit permission to create one.
5. Treat invocation as authorization to read relevant source conversations and update only the selected handbook.

## Collect Source Material

1. Discover conversations or tasks active in the requested period.
2. Select only material that is clearly part of the user's learning scope.
3. Read the actual question-and-answer turns when available; do not rely only on titles or summaries.
4. Exclude status messages, navigation chatter, repeated prompts, private unrelated content, and unsupported inference.
5. If another platform is inaccessible, request an export or pasted content instead of pretending to have read it.

## Build the Knowledge Map

Read `references/classification-guide.md` when the handbook lacks a stable taxonomy or a new topic does not fit.

- Reuse the handbook's existing top-level categories whenever possible.
- Place each question in exactly one primary category.
- Represent cross-category relationships through prerequisites and related concepts, not duplicated answers.
- Create a new category only when no existing category fits and multiple related questions justify a durable branch.

## Create or Update Entries

Use one collapsed entry per question:

```markdown
<details>
<summary>Original question, with only minor clarity edits</summary>
	**Date**: YYYY-MM-DD  **Keywords**: keyword 1, keyword 2
	### Short answer
	Answer the question directly.
	### Full explanation
	Preserve enough context, reasoning, comparisons, steps, examples, and risks that the learner does not need to reopen the source conversation.
	**Prerequisites**: ...  **Related / next**: ...
</details>
```

- Preserve the learner's intent and terminology.
- Write for the learner's demonstrated level.
- Treat paraphrases with the same learning goal as one question.
- Update an equivalent existing entry instead of adding another.
- Keep the strongest existing explanation and merge only useful new information.
- For time-sensitive facts, verify with primary sources when possible and add `Last verified: YYYY-MM-DD`.
- If verification is unavailable, label the claim as potentially outdated.

## Maintain the Chronological Index

Keep one entry per date containing:

- topics studied;
- a concise synthesis of the day's learning;
- exact titles of questions added or updated;
- unresolved questions;
- the next practical learning step.

Do not repeat full answers in the chronological index. Update an existing date rather than adding a duplicate date section.

## Edit Safely

- Fetch the destination before editing and preserve its structure.
- Prefer targeted insertions or exact search-and-replace updates.
- Never replace an entire page when that could remove child pages or databases.
- Never create another page, database, or handbook unless explicitly requested.
- Never change sharing permissions or publish content externally.
- Never store API keys, passwords, tokens, identity documents, financial data, or sensitive personal information.

## Verify

Fetch the handbook after editing and confirm:

- every saved question includes its answer;
- every question appears in one primary category;
- no meaningful duplicate was added;
- the chronological index matches the updated entries;
- unresolved questions and next steps are explicit;
- only the selected destination was changed.

Report the number of sources read, questions added, questions updated, duplicates skipped, and unresolved items. If no relevant learning material exists, make no change and say so.
