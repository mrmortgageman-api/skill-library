---
name: open-decisions-manager
version: 1
description: Surfaces open decisions from OPEN_DECISIONS.md that have aged without resolution. Prevents drift by flagging stale items and prompting Scott for a decision. Claude may not resolve or close decisions without Scott approval.
agents: [claude_cowork]
trigger_phrases:
  - "check open decisions"
  - "what's still open"
  - "any aged decisions"
  - "open decisions report"
---

# Skill: open-decisions-manager

## Purpose
Surface open decisions that have aged without resolution. Prevent drift by prompting Scott for a decision before items become invisible blockers.

## When to Activate
Activate at the start of any governance session, when Scott says "check open decisions," or when cowork-session-closer flags open items.

## Age Thresholds
**URGENT** — Open 7+ days with no update. Surfaces first.
**AGING** — Open 3–6 days. Surfaces second.
**CURRENT** — Open 0–2 days. Surfaces last for awareness only.

## Output: Open Decisions Report

**OPEN DECISIONS REPORT — [DATE]**

**URGENT (7+ days):**
[Item | Opened | Owner | Last Status]
If none: NONE

**AGING (3–6 days):**
[Item | Opened | Owner | Last Status]
If none: NONE

**CURRENT (0–2 days):**
[Item | Opened | Owner | Last Status]
If none: NONE

**Recommended Resolution Queue:**
[List URGENT items in priority order with one-sentence recommended next action each.]

**Items Claude Can Prepare for Scott's Review:**
[Any items where Claude can stage a draft, comparison, or summary to make Scott's decision faster. List only — do not act without approval.]

## Guardrails
- Claude may surface, summarize, and recommend only.
- Claude may not mark any decision as resolved, closed, or deferred without Scott explicitly confirming.
- If OPEN_DECISIONS.md is inaccessible in the current session, state: "OPEN_DECISIONS.md not available. Manual check required."
- Never carry an URGENT item forward without surfacing it to Scott first.
