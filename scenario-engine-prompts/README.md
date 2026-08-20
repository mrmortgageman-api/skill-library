# Scenario Engine Prompts — Canonical Source

## Source-of-truth rule

The files in this folder are the single canonical copy of the Scenario Engine's governing system prompts. If what's live in the Claude Project or the Griff Custom GPT ever disagrees with what's committed here, **this repo wins** — copy the committed version into the platform, don't edit the platform and forget to commit back here.

Notion and Google Drive no longer hold full copies of these prompts. Both hold a short pointer back to this folder. If you ever find a full copy of a prompt sitting in Notion or Drive again, that's drift — replace it with a pointer.

## Why this exists

On 2026-08-20, Scott found that the Claude Project's live system prompt, a Drive doc dated 2026-06-03, and a Notion doc dated 2026-03-10 had all drifted apart independently. Reconciling them took a full investigation across three platforms. This folder exists so that never has to happen again — `git log` and `git diff` answer "is this current?" in seconds instead of hours.

## Files

- `claude-project-system-prompt.md` — governs the Claude Project ("Scenario Engine | MrMortgageMan"). Current as of 2026-08-20.
- `griff-chatgpt-custom-instructions.md` — governs the Griff Custom GPT (ChatGPT). **Not yet populated with a verified current copy** — see that file for why.

## Workflow when you update a prompt

1. Edit the file in this repo. Commit with a message that says what changed and why.
2. Copy the full committed file content.
3. Paste it into the platform's instructions field (Claude Project settings, or the Griff Custom GPT builder). Neither platform has an API for this field, so this step stays manual.
4. Don't edit the platform directly and skip step 1 — that's exactly how the 2026-08-20 drift happened.

## Version history

Git commit history on this folder is the version history. No more manual `CURRENT_YYYY-MM-DD` / `SUPERSEDED_YYYY-MM-DD` renaming — `git log --follow scenario-engine-prompts/claude-project-system-prompt.md` shows every change.
