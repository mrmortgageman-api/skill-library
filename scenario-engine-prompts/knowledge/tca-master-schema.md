# TCA MASTER JSON SCHEMA

**Status:** CURRENT — updated 2026-10-13 for kernel v7.1.0 (1-4 scenarios, outcome labels, optional `featured`), matching the tool as deployed 2026-10-10 (nextjs-boilerplate PR #1). Originally rewritten 2026-08-20 to match the actual deployed tool, replacing an earlier version of this doc that matched a Drive-sourced schema spec instead. See "Why this doc changed" below before touching anything downstream of it.

**Source of truth for this version:** the live code at `mrmortgageman-api/nextjs-boilerplate` → `app/tca-mvp.jsx`, deployed at `https://mrmortgageman-tca.vercel.app/tca-mvp` (production as of 2026-10-10; the older `nextjs-boilerplate-one-pearl-61.vercel.app` URL is historical). That tool's own header comment pins it to `MMM_TCA_JSON_MASTER_SCHEMA_CURRENT_2026-03-22`, and its README (`TCA_MVP_README.md`) says "MVP Locked: Yes | Ready for Client Use: Yes" as of June 17-18, 2026. **When this doc and the deployed code disagree, re-check the code — the code is what actually runs when Scott pastes JSON into the tool. This doc is a description of that code, not the other way around.**

---

## WHY THIS DOC CHANGED (read this once)

The first version of this file, written earlier in this same rebuild, was ported from a Drive doc called `MMM_TCA_Master_Schema` that explicitly says "when Griff, the schema, or the tool conflict — this document wins." That Drive doc describes a richer schema: `taxMonthly`/`insuranceMonthly`/`taxAnnual`/`hazardAnnual`, dollar `downPayment`, per-scenario `purchasePrice`/`downPayment` overrides, `buydownType`.

Scott asked directly whether the export would work against the current live tool. It would not have. The deployed `tca-mvp.jsx` uses a different, older, simpler schema (`monthlyTax`/`monthlyInsurance`/`hoaMonthly`, `downPaymentPct`, a single top-level `loanAmount` used for every scenario, no `taxAnnual`/`hazardAnnual` fields at all, plus several Coach-View-only fields the Drive doc never mentions: `dti`, `creditScore`, `incomeDocsComplete`, `employmentTenure`).

This doc now describes what's actually live. The richer Drive-doc schema may be where the tool is headed in a future phase, but exporting to it today would fail the tool's own validation gate or silently produce wrong numbers. Treat the Drive doc as a Phase 2 design note, not the current export target, until someone actually rebuilds `tca-mvp.jsx` against it and redeploys.

---

## TOP-LEVEL FIELDS

| Field | Type | Required | Notes |
|---|---|---|---|
| mode | string | Yes | "purchase" or "refi". Defaults to "purchase" if omitted, but include it explicitly. |
| borrowerName | string | No | Displayed in the header if present. |
| coBorrowerName | string | No | Display only. |
| analysisDate | string | Yes | Validation fails without it. Use YYYY-MM-DD. |
| loanType | string | Yes | Validation fails without it. Not restricted to a fixed list in code, but use "Conventional", "FHA", "VA", or "Jumbo" for consistency. |
| loanAmount | number | Yes (effectively) | **This is the field the payment math actually uses — for both purchase and refi.** It is not derived from purchasePrice minus downPayment; the code just reads `data.loanAmount` directly. If this is missing, every scenario's P&I computes as if the loan amount were 0. |
| currentLoanAmount | number | Yes for refi | Required by the validation gate for refi mode, but **not** read by the payment computation — the computation still uses top-level `loanAmount`. Set both `currentLoanAmount` and `loanAmount` to the same value for refi exports so validation passes and the math is right. This is a known quirk in the MVP, not something to "fix" by omitting one of the two fields. |
| purchasePrice | number | No (purchase mode) | Used only to compute PMI via LTV = loanAmount / purchasePrice. Omit for refi. |
| downPaymentPct | number | No | Whole-number percent (20, not 0.20). Used only for a Coach View "20% Down / no PMI" green flag — does not feed the PMI math itself (that comes from the loanAmount/purchasePrice LTV). There is no dollar-amount downPayment field in this schema; if you have a dollar figure, convert to a percent for this field. |
| monthlyTax | number | No | Added into PITI. Defaults to 0 if omitted — do not omit if tax is known. |
| monthlyInsurance | number | No | Added into PITI. Defaults to 0 if omitted. |
| hoaMonthly | number | No | Added into PITI. Defaults to 0 if omitted. |
| propertyAddress | string | No | Display only; triggers a yellow "Property TBD" flag in Coach View if omitted. |
| dti | number | No | Decimal (0.38 for 38%). Triggers a red flag above 0.43. |
| creditScore | number | No | Triggers a red flag below 620. |
| incomeDocsComplete | boolean | No | `false` triggers a red flag. |
| employmentTenure | number | No | Years. Triggers a green flag above 5. |

There are no `taxAnnual` or `hazardAnnual` fields in the live schema — do not compute or include them, the tool doesn't read them.

## SCENARIOS ARRAY

1 to 4 objects. One per strategy Scott approved. Each label at most once. Validation fails on zero, more than four, an unknown label, or a duplicate.

| Canonical order | Purchase label | Refi label | Why sentence shown under the label (fixed in the tool) |
|---|---|---|---|
| 1 | Today's Rate | Keep Current | Purchase: "Your baseline, priced at today's market rate with no added cost." Refi: "The loan you have today. No new closing costs." |
| 2 | Fastest Payoff | Fastest Payoff | "Pays off years sooner and saves the most in total interest." |
| 3 | Best Monthly Value | Best Monthly Value | "The strongest trade between upfront cost and monthly savings." |
| 4 | Maximum Savings | Maximum Savings | "Biggest upfront investment for the lowest possible payment and long-term interest." |

Export in canonical order. The tool also re-sorts into this order before validating.

**Retired labels (do not use in new exports):** Current Loan, Conservative, Balanced, Wealth Accelerator. The tool still maps them forward (Current Loan to Today's Rate, Conservative to Fastest Payoff, Balanced to Best Monthly Value, Wealth Accelerator to Maximum Savings) so old exports keep working. Refi has no legacy mapping for "Keep Current"; it is already canonical.

**Optional top-level `featured` (string):** the label of the scenario to feature. Include it only when Scott names one. If omitted, the tool features Best Monthly Value when it is present and enabled, otherwise nothing.

Per-scenario fields:

| Field | Type | Required | Notes |
|---|---|---|---|
| label | string | Yes | One of the mode's canonical labels above. |
| rate | number | Yes | Decimal, 0 to 1 (0.065 for 6.5%). Validation fails outside that range. |
| term | number | Yes | Integer, 5 to 40. Validation fails outside that range or on a non-integer. |
| points | number | No | Displayed on the Scenarios tab. **Does not affect the payment math in this MVP** — the calculator has no points-to-rate or points-to-cost logic yet. Include it for display accuracy, but don't expect it to change P&I. |
| enabled | boolean | No | If `false`, that scenario is skipped when building the visualization. With 1-4 scenarios allowed, drop a slot you don't need instead of sending a disabled placeholder. |
| loanAmount | number | No | **Currently ignored.** The computation always uses the top-level `loanAmount` for every scenario, not a per-scenario override. Don't rely on this field to model different loan amounts across scenarios — the live tool can't do that yet. If you need per-scenario price/loan-amount comparisons, that's a Phase 2 gap, not something the current export can express; say so in Internal Output rather than putting a value here that will be silently ignored. |
| isARM | boolean | No | Coach View only — combines with `paymentShock` below. |
| paymentShock | number | No | Dollar amount. Coach View shows a yellow flag if `isARM` is true and this exceeds 200. |
| buydownType | — | — | Not read anywhere in the live code. Omit — including it does nothing and isn't validated either way. |

## FULL EXAMPLES (values match what the live validator and calculator actually expect)

Every example keeps its labels' promises (see the label-outcome check in the kernel's Export Mode): Fastest Payoff has the shortest term and least total interest, Best Monthly Value and Maximum Savings are 30-year, and Maximum Savings has the lowest payment and the most points. Passing the validator is not enough. A block can validate and still mislabel a strategy.

**Purchase:**

```json
{
  "mode": "purchase",
  "borrowerName": "John Smith",
  "coBorrowerName": "Jane Smith",
  "purchasePrice": 850000,
  "downPaymentPct": 20,
  "loanAmount": 680000,
  "monthlyTax": 583,
  "monthlyInsurance": 150,
  "hoaMonthly": 350,
  "analysisDate": "2026-10-13",
  "loanType": "Conventional",
  "creditScore": 750,
  "employmentTenure": 14,
  "incomeDocsComplete": true,
  "propertyAddress": "123 Oak St, San Ramon CA 94583",
  "dti": 0.38,
  "featured": "Best Monthly Value",
  "scenarios": [
    { "label": "Today's Rate", "rate": 0.06625, "term": 30, "points": 0, "enabled": true },
    { "label": "Fastest Payoff", "rate": 0.06, "term": 15, "points": 0, "enabled": true },
    { "label": "Best Monthly Value", "rate": 0.06375, "term": 30, "points": 0.5, "enabled": true },
    { "label": "Maximum Savings", "rate": 0.06125, "term": 30, "points": 1.5, "enabled": true }
  ]
}
```

**Refi** (note `currentLoanAmount` and `loanAmount` both set — see the quirk noted above; Keep Current is the existing loan with 27 years left):

```json
{
  "mode": "refi",
  "borrowerName": "John Smith",
  "currentLoanAmount": 450000,
  "loanAmount": 450000,
  "analysisDate": "2026-10-13",
  "loanType": "Conventional",
  "monthlyTax": 700,
  "monthlyInsurance": 150,
  "scenarios": [
    { "label": "Keep Current", "rate": 0.0725, "term": 27, "points": 0, "enabled": true },
    { "label": "Fastest Payoff", "rate": 0.0575, "term": 15, "points": 0, "enabled": true },
    { "label": "Best Monthly Value", "rate": 0.0625, "term": 30, "points": 0.5, "enabled": true },
    { "label": "Maximum Savings", "rate": 0.06, "term": 30, "points": 1.25, "enabled": true }
  ]
}
```

**Two-scenario example** (only the strategies Scott approved, no placeholders):

```json
{
  "mode": "purchase",
  "borrowerName": "John Smith",
  "purchasePrice": 850000,
  "downPaymentPct": 20,
  "loanAmount": 680000,
  "monthlyTax": 583,
  "monthlyInsurance": 150,
  "analysisDate": "2026-10-13",
  "loanType": "Conventional",
  "scenarios": [
    { "label": "Today's Rate", "rate": 0.06625, "term": 30, "points": 0, "enabled": true },
    { "label": "Best Monthly Value", "rate": 0.06125, "term": 30, "points": 0.5, "enabled": true }
  ]
}
```

## VALIDATION GATE (exact logic, ported from `normalizeTCA()` and `validateTCA()` in `tca-mvp.jsx`, deployed 2026-10-10)

Before validating, the tool maps retired labels forward and sorts scenarios into canonical order. The tool will not render anything until this passes. It shows the raw error message inline.

1. `mode` must be "purchase" or "refi", else: `Invalid mode: {mode}`
2. `scenarios` must be an array of 1 to 4, else: `Scenarios error: expected 1 to 4, got {n}`
3. For each scenario: it must be an object; its label (after legacy mapping) must be one of the mode's canonical labels, else `Scenario label error: "{label}" is not a valid {mode} label...`; no label may repeat, else `Scenario label error: duplicate "{label}"...`; `rate` must be a number between 0 and 1, else `Scenario {n} rate error`; `term` must be an integer between 5 and 40, else `Scenario {n} term error`
4. `analysisDate` must be present, else `Missing analysisDate`
5. `loanType` must be present, else `Missing loanType`
6. If `mode` is "refi", `currentLoanAmount` must be present, else `Refi mode requires currentLoanAmount`

`featured` is not validated. An unknown or disabled `featured` label falls back to Best Monthly Value.

## KNOWN LIMITATIONS OF THE LIVE MVP (from its own README — don't design an export around fixing these, they're not this schema's job)

- Points don't affect payment math yet.
- Per-scenario loan amount / price overrides aren't read — all scenarios share the one top-level `loanAmount`.
- Buydown structures (1-0, 2-1, 3-2-1) aren't modeled — the `buydownType` idea from the Drive doc isn't implemented here.
- Coach View flags are simple threshold checks, not auto-generated from a full underwriting picture.
- No HubSpot, Gmail, Drive, or Notion integration — those are stubbed for Phase 2.

MrMortgageMan™ | NMLS #1864494 | New American Funding | Internal Use Only
