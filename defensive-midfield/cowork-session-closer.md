---
name: cowork-session-closer
version: 1
description: Closes every Claude Cowork session cleanly. Generates a session summary card and determines whether a Notion mirror is required.
agents: [claude_cowork]
trigger_phrases:
  - "close the session"
  - "wrap up"
  - "session done"
  - "end of session"
---

# Skill: cowork-session-closer

## Purpose
Close every Claude Cowork session with a clean, consistent summary card. Prevent the "where were we?" tax at the start of the next session.

## When to Activate
Activate when Scott says "close the session," "wrap up," "session done," or at the natural end of any Cowork working session.

## Output: Session Close Card

**SESSION CLOSE — [DATE]**

**Session Type:**
[Governance / Build / Review / Execution / Mixed]

**Files Touched:**
[List each file modified, created, or staged. State location: Notion / Drive / PENDING_REVIEW.]

**Decisions Made:**
[List confirmed decisions only. If none, state: NONE THIS SESSION.]

**Open Decisions Added:**
[Any new items that need Scott's decision. Add to OPEN_DECISIONS.md.]

**Batons Issued:**
[Who owns what next. Claude / Scott / Griff / Other.]

**Next First Move:**
[One sentence. The single most important action to take at the start of the next session.]

**Notion Mirror Required?**
YES if any of these apply:
- Governance decision made
- System architecture changed
- Canonical file created or updated
- Council decision recorded
- New workflow approved
- Integration changed

NO if session was execution-only with no system-level changes.

**Session Status:**
[ ] CLEAN CLOSE — all items logged, no loose ends
[ ] OPEN ITEMS REMAIN — list them

## Guardrails
- Claude may not mark a session closed if PENDING_REVIEW items exist without flagging them.
- If Notion Mirror is YES, generate the session log entry before closing.
- Do not summarize decisions that were only discussed but not confirmed.
