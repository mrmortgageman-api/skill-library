# TCA MASTER JSON SCHEMA

**Status:** CURRENT, single source of truth for the TCA DATA BLOCK. Adopted 2026-08-20 as the schema the kernel's Export Mode must comply with, replacing the malformed single-scenario example that had been embedded directly in the Claude kernel.

**Source of truth:** `mrmortgageman-api/skill-library` → `scenario-engine-prompts/knowledge/tca-master-schema.md`. Original authored in Drive as `MMM_TCA_Master_Schema`. This document is the single source of truth for the JSON schema connecting Griff/Scenario Engine, the TCA visualization tool, and the React scenario engine. **When Griff, the kernel, or the tool conflict on a field-level question, this document wins.** (The kernel still governs whether export is allowed to happen at all — Scenario Lock, calculator authority, and approval gates all sit upstream of this schema.)

---

## TOP-LEVEL FIELDS — BOTH MODES

Always output `mode`, `borrowerName`, `loanType`, and `analysisDate`. No exceptions.

| Field | Type | Required | Notes |
|---|---|---|---|
| mode | string | Yes | "purchase" or "refi" — controls which UI and calculations render |
| borrowerName | string | Yes | First and last name of primary borrower |
| coBorrowerName | string | No | Include only if co-borrower exists. Omit entirely if none — never output empty string |
| propertyAddress | string | No | Full street address if known. Omit if not available |
| loanType | string | Yes | "Conventional", "FHA", "VA", or "Jumbo" |
| analysisDate | string | Yes | Today's date, ISO format: YYYY-MM-DD |
| analysisHorizon | number | Yes | Years for horizon calculations. Default 10 |
| taxMonthly | number | Yes | Monthly property tax. Default 700 if unknown |
| insuranceMonthly | number | Yes | Monthly hazard insurance. Default 150 if unknown |
| taxAnnual | number | Yes | taxMonthly × 12. Always compute — never omit |
| hazardAnnual | number | Yes | insuranceMonthly × 12. Always compute — never omit |
| hoaMonthly | number | No | Monthly HOA if applicable. Omit if none |

## PURCHASE MODE FIELDS

Shared top-level price — all scenarios inherit unless overridden:

| Field | Type | Required | Notes |
|---|---|---|---|
| purchasePrice | number | Yes | Shared default purchase price |
| downPayment | number | Yes | Shared default down payment in dollars |

Per-scenario price override — add inside a scenario object only when that scenario uses a different price point; omit from all others:

| Field | Type | Required | Notes |
|---|---|---|---|
| purchasePrice | number | No | Override shared price for this scenario only |
| downPayment | number | No | Override shared down payment for this scenario only |

Rule: if a scenario omits `purchasePrice`/`downPayment`, the tool uses the shared top-level values. Only populate per-scenario price fields when the scenario genuinely uses a different price point (e.g. comparing two program/price combinations).

## REFI MODE FIELDS

Required in addition to top-level fields, only when mode = "refi":

| Field | Type | Required | Notes |
|---|---|---|---|
| currentLoanAmount | number | Yes | Remaining principal balance on the current loan |
| currentRate | number | Yes | Current rate as decimal. Example: 0.0699 for 6.99% |
| currentTermMonths | number | Yes | Original loan term in months. Example: 360 for 30-year |
| currentMonthsIn | number | Yes | Months already paid on the current loan |
| propertyValue | number | Yes | Current estimated property value |
| currentExtraMonthly | number | No | Extra principal paid monthly on current loan. Default 0 |

## SCENARIOS ARRAY — BOTH MODES

Always output exactly four scenario objects, in this fixed order. No exceptions. Use the placeholder structure for any slot that was not generated.

| Slot | Label | Purpose |
|---|---|---|
| 1 | Current Loan (purchase) / Keep Current (refi) | Baseline. The status quo. Always enabled. |
| 2 | Conservative | Lower-risk option — modest rate improvement or shorter term |
| 3 | Balanced | Middle path — rate and payment optimization |
| 4 | Wealth Accelerator | Maximum savings or equity acceleration strategy |

Scenario object fields:

| Field | Type | Required | Notes |
|---|---|---|---|
| label | string | Yes | Must match the fixed labels exactly |
| rate | number | Yes | Decimal. Example: 0.065 for 6.500% |
| term | number | Yes | Loan term in years. Typically 30 or 15 |
| points | number | Yes | Discount points paid. Default 0 |
| enabled | boolean | Yes | true if active, false for empty placeholder slots |
| loanAmount | number | No | Refi mode only: new loan amount for this scenario |
| purchasePrice | number | No | Purchase override only (see above) |
| downPayment | number | No | Purchase override only (see above) |
| buydownType | string | No | "1-0", "2-1", or "3-2-1" — include only if the scenario uses a buydown |

Empty placeholder structure:

```json
{ "label": "Conservative", "rate": 0, "term": 30, "points": 0, "enabled": false }
```

## FULL EXAMPLES

**Purchase — shared price:**

```json
{
  "mode": "purchase",
  "borrowerName": "Alberto Cruz",
  "coBorrowerName": "Maria Cruz",
  "propertyAddress": "1234 Elm Street, San Jose, CA 95101",
  "loanType": "Jumbo",
  "analysisDate": "2026-08-20",
  "analysisHorizon": 10,
  "purchasePrice": 775000,
  "downPayment": 38750,
  "taxMonthly": 807.29,
  "insuranceMonthly": 125,
  "taxAnnual": 9687.48,
  "hazardAnnual": 1500,
  "scenarios": [
    { "label": "Current Loan", "rate": 0.065, "term": 30, "points": 0, "enabled": true },
    { "label": "Conservative", "rate": 0.0625, "term": 30, "points": 0, "enabled": true },
    { "label": "Balanced", "rate": 0.060, "term": 30, "points": 0.5, "enabled": true },
    { "label": "Wealth Accelerator", "rate": 0.0575, "term": 30, "points": 1, "enabled": true }
  ]
}
```

**Purchase — with per-scenario price override:**

```json
{
  "mode": "purchase",
  "borrowerName": "James Reyes",
  "loanType": "Conventional",
  "analysisDate": "2026-08-20",
  "analysisHorizon": 10,
  "purchasePrice": 650000,
  "downPayment": 130000,
  "taxMonthly": 700,
  "insuranceMonthly": 150,
  "taxAnnual": 8400,
  "hazardAnnual": 1800,
  "scenarios": [
    { "label": "Current Loan", "rate": 0.0699, "term": 30, "points": 0, "enabled": true },
    { "label": "Conservative", "rate": 0.0699, "term": 30, "points": 0, "enabled": true },
    { "label": "Balanced", "purchasePrice": 675000, "downPayment": 135000, "rate": 0.0699, "term": 30, "points": 0, "enabled": true },
    { "label": "Wealth Accelerator", "purchasePrice": 700000, "downPayment": 140000, "rate": 0.0699, "term": 30, "points": 0, "enabled": true }
  ]
}
```

**Refi — full example:**

```json
{
  "mode": "refi",
  "borrowerName": "David Park",
  "coBorrowerName": "Susan Park",
  "propertyAddress": "4500 Oak Avenue, Fremont, CA 94538",
  "loanType": "Conventional",
  "analysisDate": "2026-08-20",
  "analysisHorizon": 10,
  "currentLoanAmount": 480000,
  "currentRate": 0.075,
  "currentTermMonths": 360,
  "currentMonthsIn": 24,
  "propertyValue": 620000,
  "taxMonthly": 700,
  "insuranceMonthly": 150,
  "taxAnnual": 8400,
  "hazardAnnual": 1800,
  "scenarios": [
    { "label": "Keep Current", "rate": 0.075, "loanAmount": 480000, "term": 30, "points": 0, "enabled": true },
    { "label": "Conservative", "rate": 0.0675, "loanAmount": 480000, "term": 30, "points": 0, "enabled": true },
    { "label": "Balanced", "rate": 0.065, "loanAmount": 480000, "term": 30, "points": 0.5, "enabled": true },
    { "label": "Wealth Accelerator", "rate": 0.0625, "loanAmount": 480000, "term": 15, "points": 1, "enabled": true }
  ]
}
```

## TCA DATA BLOCK — EXPORT FORMAT

After CLIENT OUTPUT and INTERNAL OUTPUT sections, append:

```
=== TCA DATA BLOCK ===
{ ...full JSON object per this schema... }
```

Rules: Output VALID JSON only, zero commentary inside the JSON. Numbers must be numeric types, never strings. Rates as decimals — 0.065, not 6.5. Do not round; full decimal precision. `analysisDate` = today, YYYY-MM-DD. `analysisHorizon` defaults to 10 unless the client specifies otherwise. This block is for machine consumption only — never reference it in client-facing narrative.

After the TCA DATA BLOCK is produced, stop output. Do not continue the conversation.

## HARD RULES & COMMON ERRORS

| Rule | Why it matters |
|---|---|
| HARD STOP — always exactly 4 scenario objects | Tool breaks if array length isn't 4 |
| HARD STOP — rates as decimals (0.065, never 6.5 or "6.500%") | Calculator math fails with percentage format |
| HARD STOP — `mode` field always present | Tool can't route to the correct UI without it |
| HARD STOP — `taxAnnual` and `hazardAnnual` always computed and included | Chart and amortization fail without these |
| REQUIRED — `analysisDate` = today, YYYY-MM-DD | Header display and audit trail |
| REQUIRED — `loanType` must be one of the 4 valid values | Header badge renders from this field |
| REQUIRED — omit `coBorrowerName` entirely if no co-borrower | An empty string renders a blank name on the output |
| BEST PRACTICE — use per-scenario price only when price actually differs | Unnecessary overrides create confusion |
| BEST PRACTICE — don't round rates | Rounding changes payment calculations |

MrMortgageMan™ | NMLS #1864494 | New American Funding | Internal Use Only
