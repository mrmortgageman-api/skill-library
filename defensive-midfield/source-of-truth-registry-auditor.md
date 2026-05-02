---
name: source-of-truth-registry-auditor
version: 1
description: Before Claude acts on any file, doc, prompt, or system idea, this skill classifies it against the known source-of-truth registry. Output is a classification card only. Claude may not promote, rename, move, delete, or mark anything as superseded without explicit Scott approval.
agents: [claude_cowork]
trigger_phrases:
  - "Check if this is canonical"
  - "Can we promote this?"
  - "Is this still current?"
  - "Compare this against the registry"
  - "Should we use this?"
  - "Is this the right version?"
---

# Skill: source-of-truth-registry-auditor

## Purpose
Classify a candidate document, file, or action before Claude acts on it.
This skill produces a classification card. It does not act on the classification.

## When to Activate
Activate this skill whenever:
- A document, prompt, or file is proposed for use, promotion, or reference
- Claude is asked whether something is current or canonical
- A version discrepancy is detected between two docs serving the same purpose
- Claude encounters a doc without a CURRENT date marker or explicit status
- Any doc dated earlier than the recognized authority for its system area is referenced

## Authority Hierarchy (read in this order)
1. **Notion** — strategic truth. If Notion has a CURRENT-dated record or an explicit registry entry, that governs.
2. **Google Drive** — supporting docs. Drive files are canonical only if explicitly registered in Notion.
3. **Claude context window / session notes** — temporary only. Never canonical. Always verify against Notion and Drive.

## Classification Card Output

Produce this card for every audit. All fields required.

---

**SOURCE-OF-TRUTH AUDIT**

**Candidate Item:**
[File name, doc title, or described action]

**Claimed Purpose:**
[What this item is supposed to do or govern]

**Current Authority Check:**
[What Notion or Drive currently shows as the recognized authority for this system area. State the file name, date, and location. If unknown, state: NOT FOUND — needs manual check.]

**Registry Match:**
[Does this candidate appear in the known registry? YES / NO / PARTIAL]
[If PARTIAL, describe what matches and what differs.]

**Conflicting or Older Docs:**
[List any other files serving the same purpose with older dates or lower version numbers. If none found, state: NONE DETECTED.]

**Status:**
[ ] CANONICAL — This is the recognized current authority. Safe to use.
[ ] SUPERSEDED — A newer authority exists. Do not use without Scott review.
[ ] REFERENCE ONLY — Useful context but not governing. May be cited, not acted on.
[ ] NEEDS REVIEW — Authority unclear. Cannot confirm without manual check.
[ ] PROPOSED ONLY — Has not been approved or registered. Treat as staged draft.

**Recommended Next Action:**
[One clear sentence.]

**Approval Required?**
[ ] YES — Scott must confirm before Claude takes any action based on this item.
[ ] NO — Classification only. No action proposed.

---

## Guardrails (Non-Negotiable)

Claude may:
- Produce the classification card
- Recommend a next action
- Flag a conflict or discrepancy

Claude may NOT (without explicit Scott approval):
- Promote a doc from PROPOSED to CANONICAL
- Mark any doc as SUPERSEDED
- Rename, move, delete, or overwrite any file
- Act on a NEEDS REVIEW item
- Treat a session note or prompt as a registry authority

## Ambiguity Rule
If registry data is incomplete or unavailable in the current session, default status is NEEDS REVIEW. State clearly: "Registry data unavailable in this session. Manual check required before any action."

## Version Conflict Rule
If two docs exist for the same purpose and dates differ, the newer CURRENT-dated doc governs — unless Notion explicitly records otherwise. Flag both to Scott. Do not self-resolve version conflicts.
