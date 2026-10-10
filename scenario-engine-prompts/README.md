# Scenario Engine — Source of Truth

**This folder is the canonical source for the Scenario Engine.** Not Notion. Not Google Drive. Not whatever is currently pasted into the Claude Project settings screen or loaded in the Scenario Engine plugin. If any of those ever disagree with what's here, this folder wins — copy it over the live version, don't edit the live version in place and forget to sync back.

## Why this exists

Before 2026-08-20, the same governing text lived in three places — the live Claude Project prompt, a Google Drive doc, and a Notion page — with no mechanical link between them. They drifted. This folder fixes that by being the one place edits actually happen; every other copy is a pointer or a manual paste target.

## Structure — kernel + knowledge docs

As of 2026-08-20 this moved from one flat prompt file to a **lean kernel + knowledge docs** architecture, matching how Claude Projects and ChatGPT plugins actually work: a short instructions field that references a set of documents the model retrieves on demand, rather than one giant wall of text trying to hold everything.

```
scenario-engine-prompts/
  kernel/
    scenario-engine-kernel.md      ← paste this into the Claude Project custom instructions field
  knowledge/
    complexity-marker-reference.md  ← the 8-marker taxonomy; STRATEGY LOCK gate counts against this
    credit-intelligence-playbook.md ← 12-section credit diagnostic
    heloc-analysis-module.md
    multi-property-portfolio-module.md
    investment-property-income-module.md
    three-move-wealth-strategy-module.md
    dti-stress-test-module.md
    output-templates.md             ← B2C Notion Handoff Block + LOA Snapshot Block rules
    loa-snapshot-builder.md         ← LOA Snapshot field structure + email to the assigned LOA
    calculator-router.md            ← calculator selection logic, no math itself
    tca-master-schema.md            ← authoritative TCA export JSON schema
    operational-identity.md         ← contact info, assigned LOA, IDs, naming conventions
    voice-and-language.md           ← full voice detail (kernel carries the compressed version)
  griff-chatgpt-custom-instructions.md ← SUPERSEDED 2026-10-10 (Custom GPT retired); kept as history
```

**The test for what belongs in the kernel vs. a knowledge doc:** if getting it wrong produces invalid math, an unauthorized conclusion, wrong classification, or a broken export, it's kernel. If it's reference material, a playbook, a schema, or a module that a trigger phrase pulls in, it's a knowledge doc.

**Knowledge Override Rule (stated in the kernel, repeated here for emphasis):** a knowledge doc can extend behavior, never weaken a kernel hard gate, unless the kernel names the exception itself.

### Authority / Routing Index

Quick lookup for "which file governs X" — for humans auditing this system and as a map for what to retrieve.

```
Hard gates / exceptions        → kernel
Complexity definition          → complexity-marker-reference
Calculator selection           → calculator-router
Module math subordination      → kernel (Module Math Subordination Rule)
TCA payload contract           → tca-master-schema
Credit diagnosis               → credit-intelligence-playbook
HELOC analysis                 → heloc-analysis-module
Rental income protocol         → investment-property-income-module
Portfolio analysis             → multi-property-portfolio-module
DTI forward capacity           → dti-stress-test-module
Three-move strategy            → three-move-wealth-strategy-module
B2C + LOA structure            → output-templates
LOA Snapshot fields + email    → loa-snapshot-builder
Voice                          → voice-and-language
IDs / naming / assigned LOA    → operational-identity
```

## How each platform uses this

**Claude Project (claude.ai):** `kernel/scenario-engine-kernel.md` gets pasted into the Project's custom instructions field. Every file under `knowledge/` gets uploaded into the Project's actual knowledge base (via Project docs) so the model can retrieve them when a trigger fires — the same content, not summaries of it.

**Griff / Scenario Engine plugin (ChatGPT Plugin Creator):** As of 2026-10-10 Griff runs the Scenario Engine as a plugin, not a Custom GPT. Plugin: https://chatgpt.com/plugins/plugin_62b84a9dcc788191a72ab20a98996c85 (version 0.32.1 at the switch, shared kernel v7.0.1). The plugin syncs the shared kernel and every `knowledge/*.md` file from this folder; Griff verifies the match against `main` after each change. The plugin's own adapter lives inside the Plugin Creator package at `skills/instructions/SKILL.md`, with scoped TCA/handoff reference files and `lookup/source-lock.json`. No separate GitHub repo exists for that adapter. The old Custom GPT is retired; `griff-chatgpt-custom-instructions.md` is kept as history only.

## Versioning

No more manual `CURRENT_YYYY-MM-DD` / `SUPERSEDED_YYYY-MM-DD` renaming inside this folder — git history is the version history. `git log -- scenario-engine-prompts/` shows every change with a timestamp and message. `git diff` between two commits shows exactly what changed.

For milestone releases, this gets tagged with semantic versioning (`scenario-engine-v7.0.0`, etc.) — major = architecture change, minor = new module or doc, patch = a fix. The August 20, 2026 kernel+knowledge-docs rebuild is `v7.0.0`. The October 10, 2026 LOA generalization (Clare references replaced with an assigned-LOA slot, `loa-snapshot-builder.md` added) is `v7.0.1`, the version currently in the kernel file's header. Path to v7.0.0: RC1 went through Griff's first architecture review, which passed the core design but found a real STRATEGY LOCK/Escape Protocol contradiction, a module math-authority gap, and a kernel conversation-starter bug — all fixed in RC2. RC2 then went through Griff's adversarial gate-test suite, pulled live from GitHub: 12 of 14 controls passed outright. Two surgical gaps remained — the TCA Export Decision could still offer export after a Manual Math Exception run, and there was no deterministic firing order when multiple terminal gates were true at once. Both fixed in RC3. RC3 then passed the full gate suite 14/14, live from GitHub `main`, and Griff signed off on tagging `v7.0.0` on 2026-08-20. **The git tag itself still needs to be created by hand** — no tool in this environment can create a GitHub tag or release; see the note in Scott's session for the exact command / UI steps.

## Update workflow

1. Edit the relevant file(s) under `kernel/` or `knowledge/` in this repo.
2. Commit with a clear message describing what changed and why.
3. If the kernel file changed, copy its full text into the Claude Project custom instructions field — this has to be done by hand; there's no API for the Project instructions field.
4. If a knowledge doc changed, re-upload it to the Claude Project's knowledge base, replacing the old version, not adding a duplicate.
5. Notify Griff (via Bo2bot) so the Scenario Engine plugin syncs from `main` and confirms the match.
6. Notion and Drive pointer pages don't need updating for routine edits — they point at this repo, not at a copy of the text.

## Known open items

- **Credit Intelligence structure decision:** two different 12-section credit diagnostic structures existed — one embedded in the old flat kernel, one in the Drive-sourced Playbook doc. The Playbook structure was adopted as canonical (see the reconciliation note at the top of `knowledge/credit-intelligence-playbook.md`) without a prior explicit sign-off from Scott. Flag it if that's wrong — it's a one-file revert.
- **Calculator naming reconciliation:** BUYDOWN_COMPARISON and WEALTH_ACCELERATOR, previously listed as separate pending calculators in the kernel, were folded into PURCHASE_PAYMENT_STANDARD_CALCULATOR per the newer Calculator Router doc. See the reconciliation note at the top of `knowledge/calculator-router.md`.
- **Assigned LOA details (2026-10-10):** `operational-identity.md` now holds an assigned-LOA slot. Name, NMLS, email, and phone stay as placeholders until Scott confirms the assignment.
- **TCA scenario count vs. label doctrine (2026-10-10):** the kernel and `tca-master-schema.md` still require exactly four scenarios. The label-doctrine work in `nextjs-boilerplate` PR #1 accepts 1 to 4 scenarios and an optional `featured` field. Do not change the export contract until that PR is merged, deployed, and Scott approves the switch.

## Resolved during this rebuild

- **TCA schema vs. the live tool:** the first version of `knowledge/tca-master-schema.md` matched a Drive doc, not the actually-deployed `nextjs-boilerplate/app/tca-mvp.jsx` (live at the Vercel URL Scott uses). Scott caught this by asking directly. Confirmed against the deployed code and rewritten to match it exactly — see the "Why this doc changed" note at the top of that file. The Drive doc's richer schema is a Phase 2 target, not today's export format, until `tca-mvp.jsx` is rebuilt against it and redeployed.
- **Griff platform (2026-10-10):** the Custom GPT track was retired and replaced by the Scenario Engine plugin. The open item to reconcile the Custom GPT's live instructions is closed.
