# OUTPUT TEMPLATES — B2C NOTION HANDOFF BLOCK & CLARE SNAPSHOT BLOCK

**Status:** CURRENT. Ported unchanged from the live kernel, moved to a knowledge doc 2026-08-20 so the kernel's Dual Output Mode section can stay a one-line trigger.

**Trigger:** Applied whenever the kernel's Dual Output Mode fires — Scott asks for both blocks, notes for Notion and Clare, or operational handoff after an ILC.

**Open question, flagged rather than guessed at:** Griff's RC1 review noted this extraction may be less specific than "the fuller B2C handoff governance you've been using" — in particular, explicit `Strategic Lane Recommendation` subfields and named `Execution Baton` owner roles that a fuller canonical version apparently defines. This file is a verbatim port of the Section Rules that existed in the reconciled 2026-08-20 Claude kernel text — nothing was compressed during extraction. If a more detailed canonical version exists elsewhere (a Drive doc, a Griff-side knowledge file), it hasn't surfaced in this rebuild's research and needs to be supplied — pasted, uploaded, or pointed to — before this file can be reconciled against it. Not fabricating subfields or owner names here; that would be worse than the current honest general-description state.

---

## B2C NOTION HANDOFF BLOCK — RULES

### Truth Hierarchy

Apply to all information:

- **[Confirmed]** — Explicitly captured in ILC or source material
- **[Borrower Stated]** — Claimed by borrower, not independently verified
- **[Advisor Inference]** — Professional interpretation of available facts
- **[Needs Verification]** — Unverified, approximate, missing, or incomplete

Do not present inference as fact. Do not bury uncertainty. Use confidence tags in brackets.

### File Entry Status Gate

Every B2C Notion Handoff Block must begin with one of: `READY FOR NOTION`, `PARTIAL ENTRY ONLY`, `HOLD FOR MORE DATA`.

Immediately below status include: `Reason: [one concise sentence]`

### Output Order — use exactly, every time

File Entry Status, Raw Intake Facts, Strategy Interpretation, Missing / Unverified, Scenario Timeline, Advisory Notes, Current Blockers, Decision Points, Strategic Lane Recommendation, Communication Log, Execution Baton, Educational Flags.

Do not leave sections blank. If a section has nothing, write: "None identified at this stage."

### Section Rules

**Raw Intake Facts** — facts only, no interpretation, no recommendations. Include: Borrower Name(s), Referral Source, Referral Partner Role, Transaction Type, Occupancy, Target Property/Area, Price Range, Down Payment/Equity, Income Structure, Employment/Business Type, Assets, Liabilities, Credit Notes, Timeline, Primary Goal, Primary Concern, Co-Borrower, Current Housing Status.

**Strategy Interpretation** — what the facts suggest. Core opportunity, main constraint, likely advisory lane, income complexity, asset strategy angle.

**Missing/Unverified** — explicit list. Do not bury in narrative.

**Scenario Timeline** — what has been modeled, what is proposed, what is pending Scott approval.

**Advisory Notes** — strategic observations. Scott's framing points for the client conversation.

**Current Blockers** — active hard stops only. Not general concerns.

**Decision Points** — open decisions requiring Scott or borrower action.

**Strategic Lane Recommendation** — single recommended path with reasoning.

**Communication Log** — chronological log of contacts and conversations.

**Execution Baton** — clear next action, owner, and deadline.

**Educational Flags** — concepts the borrower needs explained before next step.

---

## CLARE SNAPSHOT BLOCK — REQUIRED TEMPLATE

Output this block second. Titled exactly: `CLARE SNAPSHOT BLOCK`

Keep it short, tactical, and operational. No narrative. No guessing. If a field is unknown, write `TBD`, `Unknown`, or `Needs Verification`.

```
CLARE SNAPSHOT BLOCK

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

MISSING ITEMS FOR CLARE
- Missing item 1:
- Missing item 2:
- Missing item 3:

ESCALATION REQUIRED: YES or NO
```
