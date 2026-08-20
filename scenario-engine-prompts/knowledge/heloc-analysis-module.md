# HELOC ANALYSIS MODULE

**Status:** CURRENT. Ported unchanged from the 2026-06-03 module set, restored into the 2026-08-20 kernel rebuild.

**Trigger:** HELOC detected on application, mentioned in intake, or flagged as down payment source. Runs inside the Complexity Scan when the HELOC marker is flagged. Required before DTI modeling when a HELOC is present.

**Calculator authority:** This module defines what to capture and what to model — it is not itself a calculation authority. Paydown timelines, cash-out-refi trigger rates, blended-rate comparisons, and DTI impact figures below must run through the calculator the Router selects, per `calculator-router.md` and the kernel's Module Math Subordination Rule. If no calculator covers the specific comparison being asked for, that's a missing-calculator condition — Escape Protocol, not a workaround.

## Capture and Confirm

- HELOC balance (current drawn amount)
- HELOC credit limit (total available)
- HELOC rate (fixed or variable — if variable, confirm index and margin)
- HELOC position (first lien or subordinate)
- HELOC payment structure (interest-only or fully amortizing)
- HELOC monthly payment at current balance
- Lender name and account status
- Purpose of HELOC funds (down payment, renovation, debt payoff, other)
- Subordination status (will the lender subordinate to the new first mortgage if applicable)

## When HELOC Is Used as Down Payment Source — Model All Three Paths

**Path 1 — Carry as-is:** Show monthly carrying cost at current rate. Model paydown timeline at current cash flow.

**Path 2 — Refinance HELOC to new product:** Rate-neutral but may offer flexibility. Flag if NAF has an applicable product.

**Path 3 — Future cash-out refi on collateral property:** Model the trigger rate that makes blending mathematically worthwhile. Do not recommend without a clear mathematical win.

## Output Requirements

- Full monthly payment picture including HELOC drag alongside the new loan payment
- HELOC paydown timeline at current income
- Rate trigger point for cash-out refi to make sense
- Impact on DTI before and after this transaction

## Strategic Constraint

Never recommend touching a sub-5% first mortgage to pay off a HELOC unless the blended rate math is unambiguous. Model the numbers. Let the math speak.
