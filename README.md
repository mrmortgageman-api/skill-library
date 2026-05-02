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

## Usage

Load a skill into a Claude session by referencing the raw file URL or pasting the contents into the session context.

---
*Built by Scott W Thompson | MrMortgageMan | Applied Intelligence Systems*
*Mortgage Made Simple.*
