# MrMortgageMan Skill Library

Claude AI operator skill files for the MrMortgageMan AI system.

Skills are `.md` files loaded into Claude Cowork sessions to govern how Claude classifies, closes, triages, and manages the system.

## Defensive Midfield (Operator Skills)

| Skill | Version | Purpose |
|-------|---------|--------|
| source-of-truth-registry-auditor | v1 | Classifies any doc or action against known authority before Claude acts |
| cowork-session-closer | v1 | Closes every Cowork session cleanly with a summary card |
| archive-triage-decay-rater | v1 | Applies Decay Risk ratings to archive files before promotion or deletion |
| open-decisions-manager | v1 | Surfaces aged open decisions from OPEN_DECISIONS.md |

## B2C Systems (SignalStrike B2C)

| Skill | Version | Purpose |
|-------|---------|--------|
| myhomereport | v1 | Builds the monthly MyHomeReport send, enrolls clients after the Post-Closing Consultation, and handles Strike Rate hits. Draft and stage only. |

## AI ACT Identities (Cross-Platform, Version Control Only)

Notion is the live source of truth for every identity's boot brief. These files are version-controlled mirrors of the platform-side configuration (ChatGPT Project instructions, etc.) — GitHub does not execute them. Update the file here whenever the live platform configuration changes.

| Identity | Platform | Live Brief (Notion) | Status |
|-------|---------|---------|--------|
| Griff | ChatGPT (Project) | GRIFF_ACT_BRIEF_CURRENT | Live-tested and operational, 2026-07-04 |
| Hank | Perplexity | HANK_ACT_BOOT_PROMPT_CURRENT | Certified, live-invocation layer not yet built |
| Claude | Cowork (Skill) | CLAUDE_ACT_BRIEF_CURRENT | Skill drafted, pending install by Scott |
| Sloan | Cowork (Skill) | SLOAN_ACT_BRIEF_CURRENT | Skill drafted, pending install by Scott |

## Usage

Load a skill into a Claude session by referencing the raw file URL or pasting the contents into the session context.

For ACT identities, always fetch the live Notion brief first — files in `act-identities/` are historical mirrors for version control, not the operating source.

---
*Built by Scott W Thompson | MrMortgageMan | Applied Intelligence Systems*
*Mortgage Made Simple.*
