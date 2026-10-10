---
name: loa-snapshot-builder
version: 2
description: Builds a ready-to-send LOA Snapshot Block and formatted email for the assigned Loan Officer Assistant from an ILC file, 1003, or raw intake notes. Output is always the LOA Snapshot Block first, then the email to the LOA. Subject line always follows borrower naming convention. The LOA never receives guesses. Unknown fields are marked TBD or Needs Verification.
---

# Skill: loa-snapshot-builder

**Supersedes:** `clare-snapshot-builder_CURRENT_2026-05-08.md` (Google Drive, archive as SUPERSEDED) and the earlier `Scenario_Engine_Clare_Snapshot_Instruction_Block_CURRENT_2026-04-09.md` reference. Generalized 2026-10-10 so it works for any assigned LOA.

## Assigned LOA

- LOA Name: [LOA Name]
- LOA Email: [LOA Email]

Rules:
- Replace [LOA Name] and [LOA Email] with the LOA assigned to this file.
- If Scott names an LOA in the request, use that name.
- If no LOA is named and none is on file, write "LOA (Unassigned)" and ask Scott who receives it before generating the email.
- Never default to a past LOA by name.

## Purpose

Produce a complete LOA Snapshot Block and the formatted email to the assigned LOA in one shot, from any combination of ILC file, 1003, or raw intake notes.

This skill is the final handoff layer between Scott's intake and the LOA's desk.

Claude drafts. Scott approves. Scott sends.

## When to Activate

Activate this skill when Scott says:

- "build LOA snapshot"
- "LOA snapshot"
- "send to LOA" or "send to [LOA Name]"
- "LOA handoff" or "[LOA Name] handoff"
- "build the LOA block"
- "file is ready for the LOA" or "file is ready for [LOA Name]"
- "snapshot for [LOA Name]"
- "prep LOA email" or "prep [LOA Name] email"
- "notes for the LOA" or "notes for [LOA Name]"
- Any legacy trigger that uses "Clare" (treat as LOA)

Also activate after any ILC session when Scott says "Dual Output" or "notes for Notion and the LOA."

## Required Inputs

Use whatever Scott provides. Accept any combination of:

- ILC working file
- 1003 (Uniform Residential Loan Application)
- Raw intake notes
- Prior session context

If inputs are incomplete, proceed with a partial snapshot. Mark every unknown field TBD, Unknown, or Needs Verification. Never guess.

## Truth Hierarchy

Apply to every field:

- [Confirmed]: Explicitly captured in ILC, 1003, or source document
- [Borrower Stated]: Claimed by borrower, not independently verified
- [Advisor Inference]: Professional interpretation of available facts
- [Needs Verification]: Unverified, approximate, missing, or incomplete

Do not present inference as fact. Do not bury uncertainty.

## Subject Line Rule

Always follow borrower email naming convention:

Last Name | Loan # | What the email is about

Example: Smith | Loan #1002000000 | New File | Conventional Purchase | Walnut Creek CA

If Loan # is unknown, ask Scott before generating the subject line.

## Output Order

Always produce both blocks in this exact order:

1. LOA SNAPSHOT BLOCK
2. EMAIL TO LOA

Do not merge the blocks. Do not stop after the first block.

---

## LOA SNAPSHOT BLOCK: TEMPLATE

Titled exactly: LOA SNAPSHOT BLOCK

Keep it short, tactical, and operational. No narrative. No guessing.

```
LOA SNAPSHOT BLOCK
Prepared For: [LOA Name]

SUBJECT PROPERTY / DEAL SETUP

- Subject Property:
- County:
- Price / Value:
- Loan Amount:
- LTV / CLTV:
- Occupancy:
- Refi Purpose:
- R/T or C/O:
- C/O Amount:
- Property Type:
- Impounds:
- FTHB:
- Loan Program:
- Term / Product:

PRICING SNAPSHOT

- Investor / Jumbo:
- Rate:
- Credit:
- Pricing Date:
- Pricing:
- Cost:

QUESTIONS / UNDERWRITING FLAGS

- Current Rate (Refi):
- Active Employment:
- Leave Date:
- Return Date:
- Other REOs:
- Co-signed REOs:
- If yes, full address + occupancy status + Sch E if rented:
- 2nd / HELOC:
- P/O or Sub?:

SCOTT NOTES

- Strategic note 1:
- Strategic note 2:
- Strategic note 3:

MISSING ITEMS FOR LOA

- Missing item 1:
- Missing item 2:
- Missing item 3:

ESCALATION REQUIRED: YES or NO
```

If YES, state the reason in one sentence below the escalation line.

---

## EMAIL TO LOA: RULES

Generate the email immediately after the LOA Snapshot Block.

To: [LOA Name] ([LOA Email])

Subject line: Last Name | Loan # | What the email is about

Greeting: "Hi [LOA Name],"

Format: Mirror the LOA Snapshot Block exactly. Use the same section headers and field labels. No narrative paragraphs. No jargon. Operational and scannable.

Close with:
- HubSpot Deal ID (if known)
- HubSpot Contact ID(s) (if known)
- Loan # (always)
- "I'll send the 1003 separately." (if 1003 is not attached)

Signature: Scott

---

## Execution Rules

- Never fill a field with a guess. TBD or Needs Verification always beats a wrong answer.
- If Loan # is missing, ask Scott before writing the subject line.
- If the LOA is unassigned, ask Scott before writing the email.
- If ESCALATION REQUIRED is YES, state the reason clearly.
- Every field must have an entry. Never leave a field blank.
- Apply truth hierarchy tags where uncertainty exists.
- Output is paste-ready. No additional editing required.

## What Claude May Do

- Build the LOA Snapshot Block from any available input
- Generate the email to the assigned LOA
- Flag missing items
- Flag complexity markers
- Flag escalation triggers
- Apply truth hierarchy tags

## What Claude May Not Do

- Send the email
- Update CRM
- Update Notion
- Guess at unknown fields
- Guess which LOA receives the file
- Present inference as confirmed fact
- Skip the email block if only the snapshot was requested (both always generate together unless Scott explicitly says snapshot only)

## Final Rule

The LOA's desk runs clean or it does not run. Every field has an answer. Every unknown is labeled. Every escalation is flagged.
