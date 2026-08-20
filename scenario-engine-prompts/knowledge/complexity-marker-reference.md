# COMPLEXITY MARKER REFERENCE GUIDE

**Version:** 1.2 (ported unchanged from Drive source) | **Original Release:** February 14, 2026 | **Status:** Governance-Aligned | **This doc owns:** the complete complexity marker taxonomy, trigger language, and validation checklist for both the Claude Scenario Engine kernel and the Griff (ChatGPT) kernel. The kernel's STRATEGY LOCK GATE is mechanical — it counts markers from this list and enforces the gate. This document defines what counts as a marker and why.

**Source of truth:** `mrmortgageman-api/skill-library` → `scenario-engine-prompts/knowledge/complexity-marker-reference.md`. Original authored in Drive as `Complexity_marker_reference_guide_v_1.2`.

**Reconciliation note (2026-08-20):** This 8-marker taxonomy replaces the informal 12-item complexity marker list that had been living directly inside the Claude kernel (self-employed income, multiple properties, co-signed obligations, active HELOC, DTI near 43%, non-QM/jumbo, asset depletion, renovation/construction, recent credit event, non-warrantable condo, bridge loan, foreign national). That 12-item list was never versioned or governed — it was informal shorthand. This document is the actual governed taxonomy and is now the single source both AI tracks reference. Several items from the old informal list (HELOC, DTI proximity, renovation loans, non-warrantable condos) are still real risk factors — they are handled by their own dedicated modules (`heloc-analysis-module.md`, `dti-stress-test-module.md`) or by the Safety Posture section of the kernel, which triggers independent of marker-count math. They do not need to also be complexity markers to get attention; the Safety Posture rules catch them directly.

---

## PURPOSE

Provides definitive definitions, examples, and governance context for complexity markers that trigger mandatory validation before the Scenario Engine produces any client-facing scenarios.

This guide exists to:

- Prevent over-commitment by AI
- Preserve Scott's decision authority
- Enforce enforcement-layer gates consistently

## DECISION AUTHORITY STACK (MANDATORY)

Scott decides → validation happens → Scenario Engine illustrates → AI never commits.

Validation does not equal approval. Scenario Engine output is illustrative only unless Scott explicitly authorizes execution.

## SAFETY OVERLAY (GLOBAL)

These enforcement gates override scenario generation when triggered. They are enforced mechanically by the kernel; this document defines the conditions.

**Gate — Strategy Lock Enforcement (Absolute Hard Stop):** If two or more complexity markers below are present and STRATEGY LOCK is missing, output ONLY: `STRATEGY LOCK REQUIRED — SCENARIO GENERATION BLOCKED`. No exploratory guidance. No A/B/C. Stop.

**Gate — Profile Completeness (Hard Stop):** Before any classification, confirm credit is visible, monthly income is established, total monthly liabilities are known, target price is known, and housing payment is known. If any is missing, output ONLY: `INSUFFICIENT DATA FOR CLASSIFICATION`, list the missing fields, ask ONE clarifying question explaining why it changes the math, then stop.

**Hard Brake Language (allowed):** "If we don't slow this down, we risk bad advice."

**Scenario Kill Switch (allowed when optionality creates confusion):** Single-path clarity is permitted when Scott requests it explicitly or when optionality creates analysis paralysis. This does not override the two gates above.

---

## SECTION 1: COMPLEXITY MARKER DEFINITIONS

Each marker below represents a strategic variable requiring validation before scenarios are shown to a client.

### MARKER 1: 1031 EXCHANGE

**Trigger words:** Exchange, 1031, Accommodator, 45-day clock, Like-kind

**Why it's complex:** IRS timelines are non-negotiable. Funds are controlled by a third-party accommodator. Occupancy classification carries risk. Underwriters resist deadline pressure.

**Must validate:** Fund availability timing. Property classification strategy. Reserve treatment. Timeline feasibility.

### MARKER 2: SELF-EMPLOYED INCOME (1099 / K-1)

**Trigger words:** 1099, Contractor, Business owner, Schedule C, Partnership

**Why it's complex:** Two-year averaging creates volatility. Down-year documentation carries risk. Underwriters are skeptical of projections.

**Must validate:** Income calculation method. Down-year narrative strategy. Whether the income is required or optional to qualify.

### MARKER 3: MULTI-UNIT PROPERTY (2-4 UNITS / ADU)

**Trigger words:** Duplex, Triplex, Quad, Mixed-use, ADU

**Why it's complex:** Occupancy classification impacts pricing. Reserve requirements are elevated. Rental income documentation draws scrutiny.

**Must validate:** Owner-occupied vs. investment treatment. Rental income offset limits. Reserve overlays.

**Legal gating note:** SB 326 / SB 721 disclosures surface only when property type is explicitly stated.

### MARKER 4: CREDIT ISSUES

**Trigger words:** Collections, Medical, Late payments, Charge-off, Bankruptcy

**Why it's complex:** Investor overlays vary. Disputes can halt underwriting. Recent lates trigger manual scrutiny.

**Must validate:** Payoff vs. document strategy. Score re-aging risk. Timeline impact.

### MARKER 5: DECISION-MAKER CONFLICT

**Trigger words:** Disagree, Tension, One spouse prefers

**Why it's complex:** Decision paralysis risk. Emotional amplification under stress. Agent confidence erosion.

**Must validate:** Root cause of conflict. Path A vs. Path B consequences. Communication strategy.

### MARKER 6: LOW CREDIT SCORE (<680)

**Trigger:** Any borrower under 680.

**Why it's complex:** LLPAs increase cost. Manual underwriting becomes more likely. Compensating factors are required.

**Must validate:** Score trend. Inquiry risk. Backup strategy.

### MARKER 7: NON-OCCUPANT CO-BORROWER / LARGE GIFT FUNDS

**Trigger words:** Non-occupant co-borrower, Gift funds >25%

**Why it's complex:** Source and seasoning documentation is required. Occupancy intent draws scrutiny. DTI inclusion rules apply.

**Must validate:** Gift sourcing. Donor documentation. Occupancy narrative.

### MARKER 8: TIGHT TIMELINE / TIME COMPRESSION

**Trigger words:** <30 days, Non-contingent, 1031 clock

**Why it's complex:** Approval gates compress. Error tolerance drops. Emotional pressure increases.

**Must validate:** Feasibility vs. risk. Required documentation timeline. Whether the Scenario Kill Switch is appropriate here.

---

## SECTION 2: STRATEGIC PRE-FLIGHT CHECKLIST (6 GATES)

- Complexity markers identified
- Authority stack acknowledged
- Safety overlay considered
- Timeline realism validated
- Emotional load assessed
- STRATEGY LOCK required if 2+ markers

## SECTION 3: STRATEGY LOCK REQUIREMENT

If two or more markers are present, Scenario Engine output is blocked until a STRATEGY LOCK is provided by Scott.

## SECTION 4: COMMON BYPASS TRAPS (explicitly prohibited assumptions)

- "Score is high so we're fine"
- "It's owner-occupied so it's easy"
- "We can figure it out later"

## SECTION 5: EDUCATIONAL FLAGS LIBRARY

Used to educate the borrower without committing to a path when safety protocols are active. Educational Flags do not override the Strategy Lock or Profile Completeness gates.

## SECTION 6: INTEGRATION WORKFLOW SUMMARY

Markers detected → Validation → Scott's decision → Scenario illustration.

## SECTION 7: RELATED PLAYBOOK CROSS-REFERENCE

- 1031 Exchange → speed/timeline narrative considerations
- Decision-Maker Conflict → follow-up cadence considerations
- Tight Timeline → complexity qualification considerations

---

## CHANGELOG

**v1.2 (Feb 14, 2026):** Updated governance alignment to current enforcement gates. Clarified that Educational Flags do not override the Strategy Lock or Profile Completeness gates. Kept existing marker definitions intact.

**v1.1 (Feb 6, 2026):** Prior governance alignment pass.

**2026-08-20:** Adopted as the single canonical complexity marker taxonomy for both the Claude Scenario Engine kernel and the Griff kernel, replacing the informal 12-item list that had been embedded directly in the Claude kernel. See Reconciliation Note above.
