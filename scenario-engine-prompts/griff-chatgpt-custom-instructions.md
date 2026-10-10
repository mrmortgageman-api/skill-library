# GRIFF — CHATGPT CUSTOM GPT INSTRUCTIONS

Status: **SUPERSEDED — 2026-10-10**

## Superseded notice

The old Scenario Engine Custom GPT is retired from active use (confirmed by Scott, 2026-10-10). It is replaced by the **Scenario Engine plugin** (ChatGPT Plugin Creator), version 0.32.1 at retirement, running shared kernel v7.0.1.

- Plugin: https://chatgpt.com/plugins/plugin_62b84a9dcc788191a72ab20a98996c85
- Shared kernel and knowledge source: `mrmortgageman-api/skill-library` → `scenario-engine-prompts/` (this folder)
- Plugin adapter: lives inside the Plugin Creator package at `skills/instructions/SKILL.md`, with scoped TCA/handoff reference files and `lookup/source-lock.json`. No separate GitHub repo exists for the adapter.

All future Scenario Engine updates go into this folder first, then the plugin syncs from it. Do not paste anything from this file into a Custom GPT.

This is retirement from active workflows, not deletion. The original stub text is preserved below as history.

---

## Historical record (pre-2026-10-10 stub, preserved verbatim)

Status: **NOT YET RECONCILED**

### Why this file is a stub

Drive holds several dated copies of Griff's instructions (v6.2 from 2026-01-11, v6.4.1 from 2026-02-06, plus supporting playbooks). The 2026-08-20 reconciliation only verified and fixed the Claude Project prompt — it did not verify which of the Griff copies, if any, matches what's actually pasted into the ChatGPT Custom GPT builder right now. Given what we just found on the Claude side, assuming the newest-dated Drive copy is current would risk repeating the exact same mistake.

### What needs to happen before this file is filled in

1. Open the Griff Custom GPT in ChatGPT and copy its actual live instructions field.
2. Paste that here, verbatim, as the first commit to this file.
3. From that point forward, this file becomes canonical the same way the Claude Project file is — edit here first, then paste into ChatGPT.

Until step 1 happens, treat every Griff-related document in Drive as unverified.
