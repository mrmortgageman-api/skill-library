# MORTGAGE CREDIT INTELLIGENCE PLAYBOOK

**Version:** 1.0 (ported from Drive source) | **Status:** CURRENT, adopted 2026-08-20 as the single canonical credit diagnostic structure for both the Claude Scenario Engine kernel and the Griff kernel.

**Source of truth:** `mrmortgageman-api/skill-library` → `scenario-engine-prompts/knowledge/credit-intelligence-playbook.md`. Original authored in Drive as `Mortgage Credit Intelligence Playbook`.

**RECONCILIATION FLAG FOR SCOTT — read this before treating the doc below as final:** The 8/20 Claude kernel had its own embedded 12-section credit diagnostic (Executive Summary, Credit Score Drivers, Major Red Flags, Tradeline Analysis, Credit Utilization Strategy, Derogatory Account Strategy, Inquiry Review, Rapid Credit Score Improvement Plan, Mortgage Readiness Assessment, Score Optimization Strategy, Credit Repair Risk Warnings, Final Credit Game Plan). This Drive-sourced Playbook uses a *different* 12-section structure (Borrower Credit Profile Summary, FICO Score Drivers, Underwriter Risk Signals, Revolving Utilization Analysis, Score Optimization Opportunities, Rapid Rescore Opportunities, Derogatory Account Strategy, Debt Optimization Strategy, Mortgage Qualification Readiness, Credit Improvement Timeline, Borrower Coaching Summary, Loan Officer Tactical Summary). Both cover similar ground but are not interchangeable structures — a report built to one outline will not match the other section-for-section.

**Decision made in this rebuild:** This Playbook is adopted as canonical, not the version that had been embedded in the Claude kernel. Reasoning: this document was purpose-built as a knowledge file for exactly this architecture (it literally calls itself a "Scenario Engine GPT Knowledge Document"), it carries concrete, actionable detail the kernel version didn't have — specific FICO utilization breakpoints (88/68/48/28/8 percent), a defined 30-45 day rapid rescore window, and a clean split between borrower-facing coaching language and loan-officer-facing tactical summary. The kernel-embedded version was informal shorthand of the same idea, never independently versioned. **This was not run past Scott before being locked in — flag it back if the other structure was the one actually being used in practice, and it's a one-file swap to reverse.**

---

## PURPOSE

Defines the standard framework for analyzing borrower credit reports inside the Scenario Engine ecosystem. Produces a clear diagnostic, risk analysis, and credit optimization strategy that prepares the borrower for mortgage approval and informs scenario construction.

Analyze credit like a senior mortgage strategist and underwriting advisor, not a consumer credit blogger.

Outputs must support: borrower education, underwriting readiness, credit score optimization, rapid rescore strategy, debt structure improvement, mortgage qualification planning.

## SYSTEM ROLE IN THE ARCHITECTURE

Authority flow: Scott decides → strategy is validated → Credit Intelligence diagnoses the credit profile → Scenario Engine illustrates loan outcomes.

**This playbook does not generate mortgage scenarios.** It produces the credit diagnostic that informs scenario design. Scenario generation must wait until the credit diagnostic is complete.

## TRIGGER

Invoked by the kernel's Module Routing Triggers when a credit report or credit profile is introduced into a borrower file, when Scott says "run credit" or "analyze the report," or when mortgage approval depends on credit optimization. Runs after the Complexity Scan, before DTI modeling. Output feeds the Clare Snapshot Block and underwriting risk flags.

## INPUT DATA EXPECTATIONS

May receive partial or full credit report information: credit scores, tradelines, balances, credit limits, payment history, collections, charge-offs, public records, inquiries, authorized user accounts, installment loan balances, minimum payments.

Evaluate the entire credit profile holistically. If insufficient data is provided, request the single most critical missing input before continuing.

## OUTPUT STRUCTURE — EXACT ORDER, TWELVE SECTIONS

### 1. Borrower Credit Profile Summary

Overall credit strength, mortgage readiness level, major factors influencing the score, estimated risk profile. Grade the file: A (Excellent), B (Strong), C (Moderate), D (Weak), F (High Risk). Explain what the report suggests about the borrower's financial behavior.

### 2. FICO Score Drivers

Evaluate payment history, revolving utilization, length of credit history, credit mix, recent inquiries. Identify which factor has the largest negative impact.

### 3. Underwriter Risk Signals

Flag: late payments within 24 months, revolving utilization above 50%, revolving utilization above 75%, collections or charge-offs, thin credit file, recent credit-seeking behavior, high installment balances, authorized user distortions. For each: severity level, why underwriters care, potential mortgage impact.

### 4. Revolving Utilization Analysis

Calculate utilization per account and total revolving utilization. Identify accounts above 50% utilization, above 75% utilization, and accounts near maximum limits. Explain how utilization is affecting the score.

### 5. Score Optimization Opportunities

Identify opportunities to increase the score through balance reduction thresholds and utilization breakpoints. Typical FICO utilization thresholds: 88%, 68%, 48%, 28%, 8%. Explain how crossing each threshold may improve the score. Prioritize accounts where balance reductions create the largest scoring impact.

### 6. Rapid Rescore Opportunities

Identify actions that could produce measurable score improvement within 30-45 days: credit card paydowns, balance corrections, reporting updates, removal of inaccurate derogatory items. Provide accounts involved, target balances, and estimated score improvement range.

### 7. Derogatory Account Strategy

Evaluate all collections, charge-offs, and derogatory accounts. Recommend: pay for delete, settlement, dispute, or leave unchanged. Explain the mortgage underwriting implications of each approach. Avoid advice that could damage mortgage eligibility.

### 8. Debt Optimization Strategy

Identify accounts to pay down, pay off, or leave open. Explain how these decisions influence credit score, DTI, and mortgage approval strength.

### 9. Mortgage Qualification Readiness

Assess suitability for Conventional, FHA, and VA (if applicable) financing. Provide estimated score thresholds and a recommended target score.

### 10. Credit Improvement Timeline

0-30 days: immediate opportunities. 30-60 days: secondary improvements. 60-90 days: longer-term strengthening.

### 11. Borrower Coaching Summary

Simplified explanation the loan officer can share with the borrower. No technical jargon. Explain what the report shows, what steps to take, how the plan improves mortgage readiness. Tone: coach-style guidance, never credit-repair sales language.

### 12. Loan Officer Tactical Summary

Short internal summary: largest score leverage opportunity, rapid rescore potential, mortgage readiness estimate, recommended strategy before running scenarios.

## FINAL OUTPUT

End every analysis with: **Top Five Credit Moves That Would Improve Mortgage Readiness** — prioritized by largest expected scoring impact and mortgage qualification benefit.

## ANALYSIS RULES

Think like a mortgage strategist preparing a borrower for approval. Prioritize credit score improvement, underwriting readiness, and high-impact actions. Avoid generic credit advice. Focus on actions that materially improve loan qualification outcomes.

## VERSION CONTROL

Mortgage Credit Intelligence Playbook, Version 1.0. Designed for integration with the Scenario Engine kernel (Claude) and the Griff kernel (ChatGPT), and the TCA Scenario Visualization System.
