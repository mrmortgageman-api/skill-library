# CALCULATOR ROUTER KNOWLEDGE LAYER

**Version:** 2026-03-29 (ported from Drive source, newest confirmed version) | **Status:** CURRENT | **Layer:** Knowledge file. Not kernel. Not API. Logic only.

**Source of truth:** `mrmortgageman-api/skill-library` → `scenario-engine-prompts/knowledge/calculator-router.md`. Original authored in Drive as `CALCULATOR_ROUTER_KNOWLEDGE_LAYER_CURRENT_2026-03-29`.

**Reconciliation note (2026-08-20):** The Claude kernel had previously listed BUYDOWN_COMPARISON and WEALTH_ACCELERATOR as separate, not-yet-validated calculators. This router — the newer, more authoritative source — shows Runs 1 through 4 (Payment Comfort, Price Sensitivity, Rate Buydown Comparison, Wealth Accelerator) all routing to the single PURCHASE_PAYMENT_STANDARD_CALCULATOR. The kernel has been updated to match this router. If BUYDOWN_COMPARISON and WEALTH_ACCELERATOR were meant to be genuinely separate, not-yet-built calculators rather than scenario objectives handled by the existing purchase calculator, flag it and this gets reverted — as written today, this router is the more specific and more recent source, so it wins.

**Naming note:** The kernel's Manual Math Exception refers to this calculator as `REFI_BREAK_EVEN_STANDARD` for brevity. In the repository, it is `REFINANCE_BREAK_EVEN_STANDARD_CALCULATOR_CURRENT_2026-03-12`. Same calculator, same exception — treat the names as synonymous.

---

## 1. Purpose

The Calculator Router selects the authoritative calculator before any scenario math runs. It does not perform math — it routes to the math authority.

No calculator confirmed = no scenario generation. No exceptions **except** the kernel's bounded Manual Math Exception for refinance break-even in Exploratory Modeling Mode (see kernel Enforcement Layer — that exception lives in the kernel, not here, because it's a hard-gate carve-out and this is a knowledge doc that cannot grant one on its own).

## 2. Router Map

### Purchase Scenarios

| Run | Scenario Objective | Calculator |
|---|---|---|
| Run 1 | Payment Comfort Test | PURCHASE_PAYMENT_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Run 2 | Price Sensitivity | PURCHASE_PAYMENT_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Run 3 | Rate Buydown Comparison | PURCHASE_PAYMENT_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Run 4 | Wealth Accelerator | PURCHASE_PAYMENT_STANDARD_CALCULATOR_CURRENT_2026-03-12 |

### Refinance Scenarios

| Run | Scenario Objective | Calculator |
|---|---|---|
| Run 5 | Refinance Break-Even | REFINANCE_BREAK_EVEN_STANDARD_CALCULATOR_CURRENT_2026-03-12 |

### Qualification Routing

| Trigger | Calculator |
|---|---|
| Borrower income type = W2 | INCOME_W2_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Income type = asset depletion AND program = Jumbo | ASSET_DEPLETION_JUMBO_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Income type = asset depletion AND program = Portfolio | ASSET_DEPLETION_PORTFOLIO_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Loan program = NonQM OR income type = NonQM | NONQM_INCOME_STANDARD_CALCULATOR_CURRENT_2026-03-12 |
| Borrower owns 2+ financed properties OR objective = DTI review | DTI_3_PROPERTY_STANDARD_CALCULATOR_CURRENT_2026-03-12 |

## 3. Selection Logic

Execute in order: (1) match run type to router map, (2) confirm transaction type (purchase or refinance), (3) confirm required input set is present or assumed under Exploratory Modeling Mode, (4) confirm the calculator exists in the Calculator Repository, (5) if no authoritative match resolves cleanly, enter Escape Protocol.

## 4. Repository Rule

The Calculator Repository is the only valid math source. Resolve every routing decision against it. Do not assume calculator availability — confirm it.

## 5. Conflict Rule

If multiple calculators appear to match a scenario, do not choose heuristically. Enter Escape Protocol. Require manual validation before proceeding.

## 6. Missing Calculator Rule

No confirmed calculator = no scenario classification. Exploratory Modeling Mode is permitted while resolution is pending. Scenario generation is not — except the kernel's bounded refinance exception.

## 7. Priority Order

When qualification and scenario math are both required: (1) transaction-critical scenario calculator (Purchase Payment or Refi Break-Even), (2) income qualification calculator (W2, Asset Depletion, Non-QM), (3) DTI qualification calculator. If qualification must be established before scenario math, run the qualification calculator first.

## 8. Sequencing

**Purchase file:** Validate income (if needed) → Validate DTI (if needed) → Run Purchase Payment Calculator → Scenario generation proceeds.

**Refinance file:** Confirm objective → Run Refi Break-Even Calculator → Scenario generation proceeds.

**Asset Depletion file:** Confirm program type → Run Jumbo or Portfolio calculator → Use qualifying income result downstream.

## 9. Exploratory Modeling Mode

Assumptions are allowed. Calculator authority is not bypassed. If a validated calculator can run on declared assumptions, use it. If inputs are too incomplete to route responsibly, enter Escape Protocol.

## 10. Escape Protocol Triggers

Pause and surface the gap if: no validated calculator exists for the scenario type; the required calculator is known but unavailable; borrower classification is too ambiguous to route; two calculators conflict with no rule to resolve it; required inputs cannot be reasonably assumed; or the scenario math falls outside current repository scope.

When triggered: pause scenario generation, surface the missing gate, ask one clarifying question. Do not generate mortgage math.

## 11. Output Handshake

Scenario generation may proceed only after router selection is complete and the calculator is confirmed in the repository.

**TCA export is permitted only after calculator-backed scenario execution is complete.** This is consistent with the kernel's Manual Math Exception, which explicitly excludes exploratory refi break-even math from ever reaching TCA export.

## 12. Explicit Exclusions

No API calls. No direct Google Sheets execution. No live spreadsheet integration. Logic and routing layer only.
