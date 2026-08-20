# Scenario Engine — Source of Truth

**This folder is the canonical source for the Scenario Engine.** Not Notion. Not Google Drive. Not whatever is currently pasted into the Claude Project or ChatGPT Custom GPT settings screens. If any of those ever disagree with what's here, this folder wins — copy it over the live version, don't edit the live version in place and forget to sync back.

## Why this exists

Before 2026-08-20, the same governing text lived in three places — the live Claude Project prompt, a Google Drive doc, and a Notion page — with no mechanical link between them. They drifted. This folder fixes that by being the one place edits actually happen; every other copy is a pointer or a manual paste target.

## Structure — kernel + knowledge docs

As of 2026-08-20 this moved from one flat prompt file to a **lean kernel + knowledge docs** architecture, matching how Claude Projects and ChatGPT Custom GPTs actually work: a short instructions field that references a set of documents the model retrieves on demand, rather than one giant wall of text trying to hold everything.

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
    output-templates.md             ← B2C Notion Handoff Block + Clare Snapshot Block rules
    calculator-router.md            ← calculator selection logic, no math itself
    tca-master-schema.md            ← authoritative TCA export JSON schema
    operational-identity.md         ← contact info, IDs, naming conventions
    voice-and-language.md           ← full voice detail (kernel carries the compressed version)
```

**The test for what belongs in the kernel vs. a knowledge doc:** if getting it wrong produces invalid math, an unauthorized conclusion, wrong classification, or a broken export, it's kernel. If it's reference material, a playbook, a schema, or a module that a trigger phrase pulls in, it's a knowledge doc.

**Knowledge Override Rule (stated in the kernel, repeated here for emphasis):** a knowledge doc can extend behavior, never weaken a kernel hard gate, unless the kernel names the exception itself.

## How each platform uses this

**Claude Project (claude.ai):** `kernel/scenario-engine-kernel.md` gets pasted into the Project's custom instructions field. Every file under `knowledge/` gets uploaded into the Project's actual knowledge base (via Project docs) so the model can retrieve them when a trigger fires — the same content, not summaries of it.

**Griff / ChatGPT Custom GPT:** same pattern, different upload mechanism. A Griff-specific kernel (see `griff-chatgpt-custom-instructions.md`) goes in the GPT's instructions field; the same `knowledge/*.md` files get uploaded as Knowledge files in the GPT builder. Griff's kernel is a separate file because the ChatGPT instructions field has its own formatting quirks and Griff's file was, historically, a slightly different lineage (v6.6 track) — but it should reference the same knowledge docs, not a forked copy of them.

## Versioning

No more manual `CURRENT_YYYY-MM-DD` / `SUPERSEDED_YYYY-MM-DD` renaming inside this folder — git history is the version history. `git log -- scenario-engine-prompts/` shows every change with a timestamp and message. `git diff` between two commits shows exactly what changed.

For milestone releases, this gets tagged with semantic versioning (`scenario-engine-v7.0.0`, etc.) — major = architecture change, minor = new module or doc, patch = a fix. The August 20, 2026 kernel+knowledge-docs rebuild is the intended v7.0.0, pending Scott's sign-off after a live test run; it's marked `v7.0.0-rc1` in the kernel file's header until then.

## Update workflow

1. Edit the relevant file(s) under `kernel/` or `knowledge/` in this repo.
2. Commit with a clear message describing what changed and why.
3. If the kernel file changed, copy its full text into the Claude Project custom instructions field (and Griff's GPT instructions field, if that kernel also changed) — this has to be done by hand; there's no API for either platform's instructions field.
4. If a knowledge doc changed, re-upload it to the Claude Project's knowledge base and to the GPT's Knowledge files — replacing the old version, not adding a duplicate.
5. Notion and Drive pointer pages don't need updating for routine edits — they point at this repo, not at a copy of the text.

## Known open items (as of 2026-08-20 rebuild)

- **Credit Intelligence structure decision:** two different 12-section credit diagnostic structures existed — one embedded in the old flat kernel, one in the Drive-sourced Playbook doc. The Playbook structure was adopted as canonical (see the reconciliation note at the top of `knowledge/credit-intelligence-playbook.md`) without a prior explicit sign-off from Scott. Flag it if that's wrong — it's a one-file revert.
- **Calculator naming reconciliation:** BUYDOWN_COMPARISON and WEALTH_ACCELERATOR, previously listed as separate pending calculators in the kernel, were folded into PURCHASE_PAYMENT_STANDARD_CALCULATOR per the newer Calculator Router doc. See the reconciliation note at the top of `knowledge/calculator-router.md`.
