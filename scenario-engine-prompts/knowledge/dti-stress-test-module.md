# DTI STRESS TEST MODULE

**Status:** CURRENT. Ported unchanged from the 2026-06-03 module set, restored into the 2026-08-20 kernel rebuild.

**Trigger:** Scott asks "does this deal max them out," "what is their DTI after this closes," "can they buy again after this," or any forward-looking borrowing capacity question. Also triggers automatically when the Three-Move Wealth Strategy Frame is active. Runs after income analysis and before or alongside scenario modeling.

**Calculator authority:** This module defines what to capture and how to report it — it is not itself a calculation authority. Every ratio, headroom figure, and forward-capacity number below must run through the calculator the Router selects (`DTI_3_PROPERTY_STANDARD_CALCULATOR`, per `calculator-router.md`) before being reported. See the kernel's Module Math Subordination Rule. If that calculator is unavailable, this is a missing-calculator condition — Escape Protocol, not a workaround.

## Produce Three DTI Snapshots

**Snapshot 1 — Current DTI (Pre-Transaction):** All current monthly debt obligations from the 1003, all confirmed qualifying income, front-end ratio (housing only), back-end ratio (all obligations), available DTI headroom to the 43% threshold.

**Snapshot 2 — Post-Close DTI (After This Transaction):** Add the new loan payment to the obligation stack. Add HELOC payment if drawn for down payment. Apply qualifying rental income from the subject property (if documented). Recalculate front-end and back-end ratios. State remaining DTI headroom.

**Snapshot 3 — Forward Capacity (Move 2 Readiness):** Estimate the maximum new loan payment available within the 43% DTI ceiling. Translate to an approximate purchase price range at current rates. Flag income events that would expand capacity (rental income seasoning, pay increase, HELOC paydown). State a timeline estimate for Move 2 based on current trajectory.

## Flag Immediately If

- Post-close DTI exceeds 43%
- Rental income is required to stay under the threshold
- Move 2 capacity is zero or negative at current income levels

## Assumption Discipline

State every assumption used. Tag every number with its confidence level. Never present a DTI number as confirmed when it is based on unverified income.
