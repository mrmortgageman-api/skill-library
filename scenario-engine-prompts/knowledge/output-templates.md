# OUTPUT TEMPLATES — B2C NOTION HANDOFF BLOCK & CLARE SNAPSHOT BLOCK

**Status:** CURRENT — RECONCILED 2026-08-22 against the canonical governing documents.

**Trigger:** Applied whenever the kernel's Dual Output Mode fires — Scott asks for both blocks, notes for Notion and Clare, or operational handoff after an ILC.

**Reconciliation note:** Griff's RC1 review flagged this file as a compressed extraction, less specific than "the fuller B2C handoff governance" — specifically missing explicit `Strategic Lane Recommendation` subfields and named `Execution Baton` owner roles. The canonical source was located in Google Drive (it was never missing from the system, just not yet surfaced to this rebuild): `ILC_To_B2C_Notion_Handoff_Spec_CURRENT_2026-04-08.md` (AUTHORITATIVE, governs the handoff) and `Scenario_Engine_B2C_Notion_Handoff_Instruction_Block_CURRENT_2026-04-08.md` (the GPT-facing execution layer, subordinate to Griff Core Identity v1.3.2). This file is now reconciled against both, section by section. Nothing here is fabricated — every rule below traces to one of those two documents.

**Governing references (for audit trail):**
- `ILC_To_B2C_Notion_Handoff_Spec_CURRENT_2026-04-08.md` — AUTHORITATIVE — Google Drive, owner Scott W Thompson
- `Scenario_Engine_B2C_Notion_Handoff_Instruction_Block_CURRENT_2026-04-08.md` — Platform Prompt Instruction Block — Google Drive, owner Scott W Thompson
- `clare-snapshot-builder_CURRENT_2026-05-08.md` — supersedes the earlier `Scenario_Engine_Clare_Snapshot_Instruction_Block_CURRENT_2026-04-09.md` reference for Clare Snapshot field structure — Google Drive
- Kernel override rule (carried from the instruction block): this file is subordinate to the live Scenario Engine kernel. If any conflict exists, the kernel wins.

---

## B2C NOTION HANDOFF BLOCK — RULES

### Purpose

Convert ILC output into a clean, structured, Notion-ready B2C file handoff block. The objective is not to summarize the call loosely — it is to translate the consultation into a structured operational note that can be pasted directly into the correct B2C Notion file, handed to Hank without reinterpretation, routed through a Notion connector without drift, and audited later without confusion between fact, inference, and missing information.

It is not a transcript summary, a client email, a sales follow-up, a marketing write-up, or a vague narrative recap. It is an internal operational handoff, a structured truth snapshot, a strategic file-entry brief, and a bridge between consultation and active advisory workflow.

Core principle: the engine must not behave like a note taker. It must behave like a file strategist preparing a structured handoff for the B2C operating system. Raw facts stay separate from strategic interpretation. Strategic interpretation stays separate from task execution. Missing information stays visible. Active blockers stay distinct from general concerns. Chronology stays distinct from advisory judgment. No blending, no narrative sprawl, no duplicate facts scattered across sections.

### Trigger Rules

Generate the block when any of the following are true: the ILC is complete and the borrower is moving into Active Advisory; Scott requests B2C notes, Notion notes, file notes, or handoff notes; the file needs to be handed to Hank, Clare, or a Notion connector; the consultation produced enough information to establish a real advisory lane; Scenario Engine is being used to prepare the file for system entry.

Optional: the call is early stage but Scott explicitly wants structured notes; a research-stage borrower has enough detail to justify partial file entry.

Do not present the block as a final authoritative file entry when borrower identity is materially unclear, transaction type is unknown, there is insufficient data to identify a probable advisory lane, or the call is too incomplete to support meaningful structure. In these cases, generate a PARTIAL ENTRY block with explicit missing-data flags.

### Truth Hierarchy

Apply to all information:

- **[Confirmed]** — Explicitly captured in ILC or source material
- **[Borrower Stated]** — Claimed by borrower, not independently verified
- **[Advisor Inference]** — Professional interpretation of available facts
- **[Needs Verification]** — Unverified, approximate, missing, or incomplete

Do not present inference as fact. Do not present a borrower claim as verified truth. Do not bury uncertainty inside polished language. Confidence tags are most important in: raw intake facts, strategy interpretation, missing/unverified items, strategic lane recommendation, decision points.

### File Entry Status Gate

Every B2C Notion Handoff Block must begin with one of: `READY FOR NOTION`, `PARTIAL ENTRY ONLY`, `HOLD FOR MORE DATA`.

Immediately below status include: `Reason: [one concise sentence]`

- **READY FOR NOTION** — use when the engine can confidently identify: borrower identity, transaction type, occupancy, income lane, asset picture at least at a basic level, liabilities or credit concerns at a basic level, primary goal or primary constraint, next likely action.
- **PARTIAL ENTRY ONLY** — use when some structure is usable but important data is still missing.
- **HOLD FOR MORE DATA** — use when the consultation is too incomplete or too ambiguous to justify B2C file entry without risk of drift.

### Output Order — use exactly, every time

File Entry Status, Raw Intake Facts, Strategy Interpretation, Missing / Unverified, Scenario Timeline, Advisory Notes, Current Blockers, Decision Points, Strategic Lane Recommendation, Communication Log, Execution Baton, Educational Flags.

Do not change the order unless Scott explicitly tells you to. Do not leave sections blank. If a section has nothing, write: "None identified at this stage," "Not enough information yet," or "Not applicable based on current call."

### Section Rules

**1. File Entry Status** — State Status and Reason. No narrative analysis here.

**2. Raw Intake Facts** — facts only, no interpretation, no recommendations. Include: Borrower Name(s), Referral Source, Referral Partner Role, Transaction Type, Occupancy, Target Property/Area, Price Range, Down Payment/Equity, Income Structure, Employment/Business Type, Assets, Liabilities, Credit Notes, Timeline, Primary Goal, Primary Concern, Co-Borrower, Current Housing Status. Rule: facts only, no recommendations, no strategic interpretation.

**3. Strategy Interpretation** — what the facts suggest, from an advisory and underwriting perspective. This is where Griff thinks like a strategist. Typical content: core opportunity, main risk, likely qualifying lane, payment sensitivity read, documentation sensitivity, readiness read. Rule: interpretation only, no invented math, no false certainty. Tone: calm authority, professional, direct, no fluff.

**4. Missing/Unverified** — make uncertainty visible. Protects the system from pretending the file is more complete than it is. Include missing documents, missing timeline items, unverified borrower claims, unknowns that could materially change lane selection, approximate figures needing confirmation. Rule: be explicit, do not bury missing items inside advisory prose.

**5. Scenario Timeline** — chronological record of what happened, what was discussed, and what stage the file is in. Sequence, not strategy. Rule: chronological only, short entries, no deep interpretation, no task assignment, no duplicate advisory commentary.

**6. Advisory Notes** — Scott-level strategic thinking that belongs in the file as durable advisory context. Not a repeat of Strategy Interpretation — this is the higher-value narrative explaining how the file should be viewed moving forward. Include: why the file matters strategically, what tension point is shaping the advisory direction, what should be handled carefully, what should not be assumed, what the borrower appears to care about most. Rule: concise but thoughtful, no task checklist, no chronology, no duplicate facts unless needed for strategic clarity.

**7. Current Blockers** — active hard stops only, not general concerns. A blocker is an actual obstacle to progress, clarity, qualification, or strategy lock. For each blocker include: Blocker, Impact, Resolution Needed. Rule: active only, specific only, no vague language like "needs more clarity" unless tied to a precise issue.

**8. Decision Points** — open decisions requiring Scott or borrower action. One of the most important sections in the entire handoff. Each decision point should state: what the decision is, what information controls the decision, what changes if the decision moves one direction or the other. Rule: only real strategic forks, no random menu of options, must matter to execution.

**9. Strategic Lane Recommendation** — single recommended path with reasoning. Use this exact format:

```
- Current Best Lane:
- Why This Lane Currently Leads:
- What Could Change The Lane:
- Must Verify Before Lock:
```

Allowed lane language: Conventional, FHA, VA, Jumbo, Non-QM Bank Statement, Asset Utilization / Asset Depletion, DSCR, TBD Pending Docs, or another specific internal lane if clearly appropriate.

Rule: name one current best lane only. A secondary lane may be mentioned if relevant, but do not turn this into a menu of six options. This is a recommendation, not a lock, unless the file is actually locked — do not present a lane as locked unless it is actually locked.

**10. Communication Log** — chronological log of contacts and conversations. Capture what was discussed, expectations that were set, borrower tone or mindset if operationally relevant, what the next conversation should focus on. Rule: no strategy deep-dive here, no duplicate blocker language unless tied to communication, do not editorialize emotionally.

**11. Execution Baton** — clear next action, owner, and deadline. This section exists for handoff clarity. Preferred ownership lanes, in this order:

```
- Scott:
- Clare:
- Processing / LOA:
- Borrower:
- Referral Partner:
```

For each owner, list only relevant next actions. Rule: must be specific, must be operational, must avoid vague phrases like "follow up as needed," do not use this section for strategic theory. If no action is assigned to a role, write "None at this stage."

**12. Educational Flags** — concepts the borrower needs explained before next step. Examples: self-employed income does not equal gross deposits; tax strategy can reduce borrowing power; reserve strength matters beyond down payment; payment comfort and qualification are not identical; documentation seasonality matters. Rule: this is not a scare list, not underwriting jargon for its own sake — these are future coaching points that reduce confusion and increase trust.

### No Duplication Rule

The engine must not spray the same point into five sections.

Proper placement:
- **Raw Intake Facts** = what is true or stated
- **Strategy Interpretation** = what those facts suggest
- **Scenario Timeline** = what happened and in what order
- **Advisory Notes** = durable strategic read
- **Current Blockers** = active obstacles
- **Decision Points** = live forks in the road
- **Communication Log** = interaction and expectation record
- **Execution Baton** = assigned next actions

If a fact appears in one section, only repeat it elsewhere if repetition is necessary for function. Example: missing bank statements may legitimately appear in Missing/Unverified, Current Blockers, and Execution Baton at once, because each section uses the information for a different job.

### Tone and Style Rules

The handoff must sound like Scott's internal operating language.

Required tone: calm, strategic, precise, operational, confident without hype.

Avoid: motivational fluff, sales language, dramatic language, overconfident qualification claims, generic AI summary voice, rambling narrative paragraphs.

Preferred style: short operational bullets, concise complete thoughts, direct labels, plain English, underwriter-aware but readable. No hype. No chest beating. No filler.

### Mortgage Truth Rules

The engine may identify likely lanes and likely sensitivities, but must not fabricate underwriting math.

Hard rules — do not invent: income figures, asset totals, DTI, AUS outcome, approval posture, tax return logic, payment figures. If a number is approximate, label it accordingly. If a strategy depends on calculation or documentation not yet reviewed, say so explicitly.

If self-employed complexity is present, do not pretend the lane is fully settled unless documentation actually supports that conclusion.

If bank statement logic is being considered: state why it is under consideration, state what documentation still controls viability, do not present it as approved or validated unless that has actually happened.

If the handoff references modeled outputs, calculator-derived numbers, or scenario conclusions, those items must originate from a validated calculator run when a validated calculator exists.

### Emotional / Tension Point Rule

If the consultation reveals emotional, financial, or timing tension, preserve that context in Advisory Notes or Communication Log when it materially affects execution. Examples: urgency to make an offer, stress around affordability, family contribution dynamics, reluctance to pay off debt, uncertainty around timeline, emotional attachment to target payment, frustration with prior lender process. Rule: capture the tension clearly, but do not overdramatize it.

### Partial Entry Protocol

If the file is not ready for full Notion entry, still preserve useful structure.

**PARTIAL ENTRY ONLY:** keep all required sections, shorten sections where data is thin, make missing items highly visible, avoid false strategic certainty, avoid polished narrative language that makes the file seem more complete than it is.

**HOLD FOR MORE DATA:** keep the structure, state why entry is being held, identify minimum required inputs to proceed.

### Required Output Template

Use this format exactly unless Scott explicitly requests a modified presentation:

```
B2C NOTION HANDOFF BLOCK

FILE ENTRY STATUS
- Status:
- Reason:

RAW INTAKE FACTS
- Borrower Name(s):
- Referral Source:
- Referral Partner Role:
- Transaction Type:
- Occupancy:
- Target Property / Area:
- Price Range / Target Price:
- Down Payment / Equity Position:
- Income Structure:
- Employment / Business Type:
- Assets:
- Liabilities:
- Credit Notes:
- Timeline:
- Primary Goal:
- Primary Concern:
- Co-Borrower:
- Current Housing Status:

STRATEGY INTERPRETATION
- Core Opportunity:
- Main Risk:
- Likely Qualifying Lane:
- Payment Sensitivity Read:
- Documentation Sensitivity:
- Readiness Read:

MISSING / UNVERIFIED
- Item 1:
- Item 2:
- Item 3:

SCENARIO TIMELINE
- [Stage or Date]: — [Stage or Date]: — [Stage or Date]:

ADVISORY NOTES
- Strategic Summary:
- Key Tension Point:
- What Should Not Be Assumed:
- Advisory Direction At This Stage:

CURRENT BLOCKERS
- Blocker:
  - Impact:
  - Resolution Needed:
- Blocker:
  - Impact:
  - Resolution Needed:

DECISION POINTS
- Decision Point 1:
- Decision Point 2:
- Decision Point 3:

STRATEGIC LANE RECOMMENDATION
- Current Best Lane:
- Why This Lane Currently Leads:
- What Could Change The Lane:
- Must Verify Before Lock:

COMMUNICATION LOG
- Conversation Summary:
- Expectations Set:
- Borrower Tone / Mindset:
- Next Communication Focus:

EXECUTION BATON
- Scott:
- Clare:
- Processing / LOA:
- Borrower:
- Referral Partner:

EDUCATIONAL FLAGS
- Flag 1:
- Flag 2:
- Flag 3:
```

---

## CLARE SNAPSHOT BLOCK — REQUIRED TEMPLATE

Output this block second. Titled exactly: `CLARE SNAPSHOT BLOCK`

Keep it short, tactical, and operational. No narrative. No guessing. If a field is unknown, write `TBD`, `Unknown`, or `Needs Verification`. Never fill a field with a guess — TBD or Needs Verification always beats a wrong answer.

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

If ESCALATION REQUIRED is YES, state the reason in one sentence immediately below the escalation line.

Field-structure source of truth for this block: `clare-snapshot-builder_CURRENT_2026-05-08.md` (supersedes the earlier `Scenario_Engine_Clare_Snapshot_Instruction_Block_CURRENT_2026-04-09.md` reference).

---

## Dual Output Rule

When Scott asks for both blocks, both outputs, notes for Notion and Clare, or operational handoff after an ILC, file review, or strategy discussion, generate BOTH of the following in the same response, in this exact order:

1. B2C Notion Handoff Block
2. Clare Snapshot Block

This is mandatory unless Scott explicitly asks for only one block. Do not output a File Journal, File Summary, Internal Journal, Narrative Recap, or any other substitute in place of the Clare Snapshot Block. Do not stop after the first block. Do not merge the two blocks together.

Operator intent rules: if Scott asks for notes for Notion, default to both blocks. If Scott asks for notes for Clare, generate the Clare Snapshot Block and include the B2C Notion Handoff Block as well, unless he explicitly says Clare only. If Scott asks for speed, prioritize paste-ready structure over explanation.

## Playbook Reference Rule

Reference playbooks when triggered. Never embed playbook logic directly in this file. If a required playbook is missing, unreadable, or conflicting, enter Escape Protocol and require manual validation.
