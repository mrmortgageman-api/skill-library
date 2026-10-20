---
name: myhomereport
version: 1
description: Runs MyHomeReport, Scott's monthly closed-database homeowner newsletter. Use to build a monthly send (Market Pulse, 4 segment Coach's Notes, Homeowner Tip), enroll a client after a Post-Closing Consultation, or handle a Strike Rate hit. Claude drafts and stages only. Scott approves every send and every client call.
agents: [claude_chat, claude_cowork]
trigger_phrases:
  - "build this month's MyHomeReport"
  - "MyHomeReport for [month]"
  - "draft the coach notes"
  - "draft the homeowner tip"
  - "enroll [client] in MyHomeReport"
  - "strike rate hit"
  - "strike rate check"
---

# Skill: myhomereport

## Purpose
MyHomeReport is a monthly newsletter for Scott's closed database. It is offered live on the Post-Closing Consultation call as a free, ongoing touchpoint.

It runs on tools Scott already owns: HubSpot, Notion, Mailchimp, FRED, and FHFA public data. Zero new vendor cost. Scott chose to own this system instead of buying MyHomeIQ, Homebot, or MBS Highway Value Alert. Do not suggest switching back to a vendor.

Treat it as revenue-adjacent infrastructure. It is tracked on the ACTIVE_PROJECT_BOARD in Notion under System: SignalStrike B2C.

## When to Activate
- Scott asks to build, draft, or QA a monthly send.
- Scott asks for coach notes or a homeowner tip.
- Scott finishes a Post-Closing Consultation and wants the client enrolled.
- A Strike Rate task fires, or Scott asks for a strike rate check.

## The Product (one email per contact per month)
1. **Market Pulse.** FHFA zip-level home price appreciation for the contact's zip, plus a Zillow link to their area. Shared across segments, filled by merge fields.
2. **Coach's Note.** Short note written in Scott's voice. One version per segment.
3. **Homeowner Tip.** Seasonal, non-mortgage, a little fun. One version for everyone.

**Single CTA in every email: call or text Scott directly.** No landing page. No form. No rates.

## Segments (HubSpot `segment_tag`)
| Segment | Rule | Coach's Note angle |
|---|---|---|
| Bay Area High Value | Bay Area, home value over $1.2M | Equity strategy, protecting wealth, jumbo context |
| Bay Area Mid | Bay Area, $600K to $1.2M | Equity growth, move-up thinking, smart use of equity |
| Inland/Suburban | Home value under $600K | Building equity, payment confidence, simple wins |
| Out of Area | Property outside Scott's core markets | Local-market humility, national trends, stay in touch |

Edge rules:
- Exactly $1.2M goes to Bay Area Mid. Exactly $600K goes to Bay Area Mid.
- Missing `segment_tag`: do not guess. List the contact in the QA report as "Needs segment."

## Mode 1: Monthly Send Build

### Step 1. Market Pulse data
- Pull the latest FHFA HPI release. FHFA zip data is annual and county/metro data is quarterly. Always label the period the number covers. Never present it as this month's value.
- If the engine is running, use `fhfa.ts` output. If not, pull the public FHFA data and note "manual pull" in the QA report.
- Use FRED only for context Scott asks for. Never print a mortgage rate in the email.
- Zillow link goes in as a merge field. Never quote a Zillow estimate as the client's home value.

### Step 2. Draft four Coach's Notes
- 60 to 90 words each.
- Structure: Hook (1 line, how they feel) / Insight (2 to 3 sentences) / Action (call or text Scott).
- Tie the note to something real this month: a season, a data point, a common homeowner question.
- Never promise a value, a rate, a savings amount, or a timeline.

### Step 3. Draft one Homeowner Tip
- 40 to 70 words. Seasonal. Non-mortgage. A little fun.
- Good topics: gutters before rain, smoke detector batteries, HVAC filters, holiday lights safety, garden timing, property tax deadlines (date only, no tax advice).
- Scott's dogs Leo and Smoosh may appear in a tip when it fits naturally.

### Step 4. Assemble and QA
Run the QA checklist below on every block. Fix before presenting.

### Step 5. Stage, do not send
- If the Mailchimp connector is available, save the campaign as a **draft only**.
- Never send, schedule, or publish without Scott typing approval in chat.
- Write the coach notes and tip into the Notion Coach Notes and Tip Calendar databases when they exist. If they do not exist yet, say so in the QA report.

## Mode 2: Client Enrollment (after the Post-Closing Consultation)
Collect from Scott:
- Client name and HubSpot contact
- Property zip and home value (for segment)
- Agreed strike rate (the target mortgage rate the client and Scott set together)

Then stage these HubSpot updates for Scott's approval:
- `segment_tag` = segment from the table above
- `strike_rate` = agreed target rate
- `strike_rate_status` = Active
- `strike_rate_set_date` = date of the consultation
- Add the contact to the MyHomeReport Mailchimp audience

Deliver as one cut-and-paste block tagged "FOR: Scott". Do not write to HubSpot until Scott approves.

## Mode 3: Strike Rate Hit
When the live market rate reaches a client's `strike_rate`:
- HubSpot creates a **HIGH priority task to Scott**. That is the only automated action.
- **No automated client email. Ever.** Scott makes this call personally.
- Claude may prepare a call-prep card: client name, loan details on file, strike rate, set date, current rate, and one opening line in Scott's voice.
- After the call, Scott decides the new `strike_rate_status`. Claude does not change it on its own.

## Voice Rules (every client-facing word)
- Scott's voice: MrMortgageMan. Calm, direct, coach energy. Zero hype.
- A B-average high school senior gets it instantly.
- Short sentences, active voice, every sentence under 20 words.
- Specific numbers over vague claims.
- No em dashes. Use periods or commas.
- Banned: hopefully, maybe, no problem, best rate, fingers crossed, crushing it, killing it, game-changer, revolutionary, act now, limited time, don't miss out, delve, robust, moreover, furthermore, in today's market, I hope this message finds you well.
- Sign-off: "Mortgage Made Simple." then "Scott"

Approved phrases Scott uses:
- "Smart strategy beats perfect timing."
- "You've got equity sitting there."
- "Numbers tell a story. My job is to translate it."
- "Let's slow this down and make it simple."

## QA Checklist (run before presenting anything)
- [ ] Exactly one CTA: call or text Scott
- [ ] No rates anywhere in the email
- [ ] No promised value, savings, or timeline
- [ ] FHFA period labeled correctly
- [ ] Every sentence under 20 words
- [ ] Zero em dashes, zero banned words
- [ ] Coach notes 60 to 90 words, tip 40 to 70 words
- [ ] Footer company name and NMLS number confirmed current before every send
- [ ] Equal Housing language present in footer
- [ ] Contacts missing `segment_tag` listed

## Output Format
Deliver as one complete, self-contained cut-and-paste block with a one-line recipient tag (for example "FOR: Scott"). No partial updates.

Monthly build output:

**MYHOMEREPORT: [MONTH YEAR]**
- Market Pulse data period: [period]
- Coach's Note: Bay Area High Value
- Coach's Note: Bay Area Mid
- Coach's Note: Inland/Suburban
- Coach's Note: Out of Area
- Homeowner Tip
- QA report (pass/fail per item, plus open flags)
- **One next step** for Scott. Never a menu of options.

## Guardrails
- Draft and stage only. No sends, no schedules, no HubSpot writes without Scott's approval in chat.
- No automated client contact on a strike rate hit.
- No API keys, passwords, or tokens in chat or in this repo. Keys live in the password manager or the local `.env.local` on the mini-PC.
- No client names, loan numbers, or client data committed to GitHub.
- Flag any revenue-connected item that is not tracked in HubSpot.

## Reference Locations
- Engine code: MyHomeReport-B2C folder on Scott's mini-PC (`calculate.ts`, `fred.ts`, `fhfa.ts`, `hubspot.ts`, `notion.ts`, `zillow.ts`, `mailchimp.ts`, monthly runner, Mailchimp click webhook)
- Notion: "MyHomeReport-B2C Homeowner Intelligence Newsletter" and "MyHomeReport Engine Build Session 2026-05-07"
- Framework: Post-Closing Consultation Framework (Google Doc)
- HubSpot contact fields: `strike_rate`, `strike_rate_status`, `strike_rate_set_date`, `segment_tag` (live)

## Known Gaps (as of 2026-07-20 audit)
Until these close, run Mode 1 as a manual build and stage in Mailchimp by hand.
- No `package.json`, dependencies, or git repo for the engine code
- `.env.local` keys blank
- Notion Coach Notes and Tip Calendar databases not created
- No Mailchimp email template
- No monthly cron scheduled
- Client enrollment workflow not yet documented outside this skill
