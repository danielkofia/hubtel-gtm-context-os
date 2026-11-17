# Hubtel outbound GTM system (design draft)

Written for: Hubtel's go-to-market owner and whoever builds the workflows. Built from `context/icp/icp.md`, `personas.md`, `signal-matrix.md`, plus `context/messaging/`, `context/positioning/` and `context/docs/research/`. Method: `knowledge-base/playbooks/workflow-anatomy.md`, `signal-matrix-framework.md`, `copy-iron-laws.md`, `linkedin-dm-frameworks.md`.

Tags: [icp] icp.md, [per] personas.md, [sm] signal-matrix.md, [msg] messaging.md, [fx] facts.md, [pos] positioning.md, [res] research files, [pb] playbooks. PROPOSAL = a number or rule I am suggesting, not found in the research. INFERRED = my reading. This is a draft to validate with Hubtel sales. Nothing here has run yet.

## Assumptions and facts that shape the design
- **Stack:** Clay, HubSpot and n8n are the GTM tools named for this project (the bracketed example in the brief; confirm). The sequencer and LinkedIn automation tool are NOT chosen. Playbooks name Smartlead, Instantly, Lemlist and HeyReach as examples only [pb]. Decision needed (Open question 1).
- **treg** (tested this project): LinkedIn jobs $0.001, LinkedIn company profile $0.0015, LinkedIn and X posts $0.00188 [res signals.md]. Catalog also lists routed email find (`treg.people.email.find`), email verify (`treg.people.email.verify`), people search (`treg.people.search`). Ghana coverage of these is untested. Hard cap per call: `X-Treg-Route-Max-Cost`.
- **Ghana data is thin.** Framework says weak-footprint markets need registry and physical-world signals, not LinkedIn-style signals [pb][sm]. Volumes are Not found.
- **No claim is approved** in `facts.md`. Copy cannot be sent until Hubtel approves claims [fx].
- **Repo rules** (`CLAUDE.md`): cite sources, no invented numbers, no em dashes, ask before sending or publishing, log every change.
- **Human in the loop:** every first send and every reply is approved by a person until Hubtel says otherwise. This follows the "ask before sending" rule.

## The system in one view
```
[1 Context OS] -> [2 Signals] -> [3 Find companies] -> [4 Enrich] -> [5 ICP fit]
      ^                                                                  |
      |                                                                  v
[12 Weekly loop] <- [11 CRM] <- [10 Replies] <- [9 Sequence] <- [8 Emails] <- [7 People] <- [6 Route by segment]
```
Steps 3 to 11 are shared by every workflow. Only the signal (step 2) and the angle (step 6) change per workflow. That is the composable design [sm].

Five workflows planned [sm Matrix 3]: W1 hiring, W2 public tenders, W3 new gaming licence, W4 BoG notice overlay, W5 new leader on a signal hit.

---

## Step 1. The Context OS
**What happens:** This repo is the single source of truth. Every step reads from it and writes learnings back to it.

| Folder | Read by | Used for |
|---|---|---|
| `context/icp/` | Steps 2, 5, 6, 7 | Segments, fit rules, personas, signals |
| `context/messaging/facts.md` | Steps 9, 10 | The only allowed claims and bans |
| `context/messaging/messaging.md`, `positioning/` | Steps 6, 9 | Pillars, angles, words |
| `context/docs/research/` | Steps 4, 6 | Source facts |
| `knowledge-base/playbooks/` | Steps 9, 10 | Copy rules, DM rules |
| `knowledge-base/learnings/` | Step 12 | What worked |
| `weekly-priorities/`, `work-log/` | Step 12 | Plan and change log |

**Tool:** Claude Code in this repo, with the skills in `.claude/skills/` (signal-matrix, campaign-strategy, build-workflow-spec, campaign-copy, campaign-qa, build-clay and others).

| Decision | Answer | Leads to |
|---|---|---|
| Is a claim in `facts.md` approved? | Yes | Usable in copy (step 9) |
| | No (Pending) | Copy uses `{{placeholder}}`, or the claim is left out |
| Does a new fact conflict with a stored one? | Yes | Keep both with sources, flag in `Open questions`, do not pick silently |
| Is a workflow's signal in `signal-matrix.md`? | No | Add it there first (scored on the four tests), then build |

---

## Step 2. Buying signals (always on)
**What happens:** Monitors run on a schedule and write each hit (signal, company, date, source URL) to a Clay table. Signal-led: the signal comes first, the ICP filter second [pb signal-matrix-framework].

| Workflow | Signal | Detection | Tool | Cadence (PROPOSAL, from the framework's velocity table) |
|---|---|---|---|---|
| W1 | Hiring collections, revenue assurance, payments, digital channel roles | LinkedIn jobs search per keyword | treg `harvestapi.linkedin.search.jobs`, Clay Find Jobs | Weekly |
| W2 | Tender for collection platform, gateway, revenue collection | GHANEPS and PPA notices | crawl4ai or agent-browser, n8n diff | Daily |
| W3 | New or renewed gaming licence | Gaming Commission licensed-operators page | crawl4ai or agent-browser, n8n diff | Monthly |
| W4 | BoG notice on payment providers | bog.gov.gh notices page | crawl4ai, n8n diff, alert to a human | Weekly |
| W5 | New CFO, digital or payments lead in 90 days | LinkedIn people data | Clay Find People, treg | Monthly |

**Tool for scheduling and storing hits:** n8n runs the monitors, posts hits to Clay.

| Decision | Answer | Leads to |
|---|---|---|
| Did the monitor return anything this run? | Yes | Step 3 |
| | No, three runs in a row | Flag the signal in step 12. Possible dead source or low volume. Do not keep it silently |
| Is the source page unchanged or blocked (403, login)? | Yes | Mark the source BLOCKED in `signal-matrix.md`, ask Hubtel for access or another source |
| Is the hit market-level (BoG notice) rather than company-level? | Yes | Do not build a list. Update the overlay used in step 6 and notify the owner |
| Is the signal older than its freshness window? | Yes (PROPOSAL: tender closed, licence expired, job older than 30 days) | Drop it |

Volume per signal is Not found for Ghana. Run a 2-week count first [sm].

---

## Step 3. Finding companies
**What happens:** Each signal hit becomes a company record. Signal-led means the company exists in the table because the signal fired. Separately, a static account universe supports ABM: NIC insurer list, Gaming Commission operators, utility distributors [sm][WEB].

**Tool:** Clay (company table, dedupe by domain), treg `treg.web.search` and `fetchinio.linkedin.company.profile` to resolve name to domain and LinkedIn page.

| Decision | Answer | Leads to |
|---|---|---|
| Can the signal be resolved to one domain? | Yes | Step 4 |
| | No | Park in "unresolved". A human resolves or drops it weekly |
| Already in HubSpot as company, customer or open deal? | Customer | Drop from outbound, notify the owner |
| | Open deal or recent contact | Suppress. Add the new signal as a note on the deal |
| | No | Step 4 |
| Is the company a competitor PSP, a Hubtel partner or a regulator? | Yes | Drop. Examples: AWS, Visa, GhIPSS, BoG [res customers.md] |
| Is it an account-universe company without a signal? | Yes | Keep in the ABM list. Outreach waits for a signal |

---

## Step 4. Enrichment
**What happens:** Add the fields the fit check and routing need. Two to four secondary enrichments only, so volume survives [pb workflow-anatomy].

| Field | Source | Tool |
|---|---|---|
| Country, city, HQ | LinkedIn profile | treg `fetchinio.linkedin.company.profile` |
| Industry, headcount band | LinkedIn profile (undercounts: Hubtel shows 557 on LinkedIn vs 722 on payroll [res company.md]) | same |
| Segment guess (utility, insurer, gaming, transport or school, POS) | Industry plus website text | Clay AI column over crawl4ai page text |
| Pain statement (office hours, queues, leakage, manual collection) | Website, news, LinkedIn posts | treg web search, `scrapecreators` posts; partial per framework |
| Current provider or payment page evidence | Website checkout or payment page | crawl4ai, treg `treg.google.serp.organic` |
| Hiring pattern (other open payment roles) | LinkedIn jobs | treg |

| Decision | Answer | Leads to |
|---|---|---|
| Is a required field missing after one pass (country, industry, domain)? | Yes | One retry with a second source. Still missing: mark `fit = unknown`, send to human review |
| Did enrichment cost exceed the per-company cap? | Yes (PROPOSAL: set cap after first week's costs) | Stop paid calls, finish with free fields |
| Are two sources in conflict (headcount, country)? | Yes | Keep the source with a date, store both, flag |
| Is a field INFERRED rather than found? | Yes | Store with `inferred = true`. Never feed it into a claim in copy |

---

## Step 5. ICP fit check
**What happens:** Score against `icp.md` rules.
- Must have: Ghana; recurring high-volume collections or payouts; manual, limited-hours or leaky process [icp].
- Boosters: API or USSD need, segment 1 to 3, public pain statement, provider under regulatory pressure [icp].
- Disqualifiers: outside Ghana or multi-country, lowest-fee buyer, micro or informal merchant, restricted activity, foreign-currency crypto wallets [icp].

**Tool:** Clay formula column for must-haves and disqualifiers, Clay AI column for pain and segment judgement, with the reason stored. A human reviews borderline cases.

| Decision | Answer | Leads to |
|---|---|---|
| Any disqualifier true? | Yes | `fit = no`. Log reason. Never contacted |
| All must-haves true? | Yes | Fit. Count boosters |
| | Unknown | `fit = unknown`, human review (step 4 rule) |
| | No | `fit = no` |
| Boosters count | 2 or more (PROPOSAL, tune after first results) | Tier A: first in the queue |
| | 0 to 1 | Tier B: queued after Tier A, lighter sequence |
| Customer size known? | No (Not found [icp]) | Do not filter by size. Add size to Open questions. Review after first 50 accounts |

---

## Step 6. Routing by segment
**What happens:** Pick the narrative route from segment, persona and signal. Same data, different angle. Uses Matrix 1 in `signal-matrix.md` and pillars in `messaging.md`.

| Segment | Lead pillar | Source |
|---|---|---|
| 1 Utilities | Every channel, one platform | [msg][sm] |
| 2 Insurers | Collect when customers are ready | [msg][sm] |
| 3 Gaming | Pay out and collect by API (USSD deposits) | [msg][sm] |
| 4 Transport, schools | Direct debit by API | [msg][sm] |
| 5 POS merchants | Hold until fee is approved | [msg][fx] |

**Tool:** Clay routing column, then `/build-workflow-spec` to record each route.

| Decision | Answer | Leads to |
|---|---|---|
| Which segment? | 1 to 4 | Matching route above |
| | 5 | Parked until the fee is approved (Open question 4) |
| | Unclear | Human review |
| Does a BoG notice overlay apply (W4)? | Hubtel has approved its Notice 43 position | Add the overlay line in the copy |
| | Not approved (today's state [fx]) | No overlay. Do not mention funds safety |
| Does the segment have an approved proof point in `facts.md`? | Yes | Use it |
| | No | Use a generic route without a customer result, or hold the segment |
| Secondary signal also present (e.g. new leader on a hiring hit)? | Yes | Use the stacked route (two signals, one line each) |
| | No | Single-signal route |

---

## Step 7. Finding people
**What happens:** Find the champion first, then the economic buyer. Influencer is not contacted in outbound unless a route calls for it (Notice 43 content is on hold). Persona titles are Not found [per], so role keywords are hypotheses to test.

| Persona | Title keywords to test (INFERRED) | Tool |
|---|---|---|
| Champion | head of digital, head of IT, payments, finance operations, revenue assurance | treg `treg.people.search`, Apollo through Clay, LinkedIn |
| Economic buyer | CEO, managing director, CFO, finance head | same |
| Influencer | compliance, risk, procurement, internal audit | same, only on request |

| Decision | Answer | Leads to |
|---|---|---|
| Is the champion found and current (LinkedIn role matches the company)? | Yes | Step 8 |
| | No | Try the economic buyer |
| | Neither | Park, retry next month, note in step 12 |
| Contacts per account | 1 champion plus 1 economic buyer (PROPOSAL) | Two separate sequences. Never email both on the same day with the same copy |
| Does a contact appear in HubSpot (existing relationship)? | Yes | Route to the owner for a personal note, not the sequence |
| Is the person a Hubtel partner or ex-employee? | Yes | Drop |

---

## Step 8. Finding and verifying emails
**What happens:** Find, then verify, then decide. A found email is not a confirmed one [treg skill]. Never re-run a paid find on the same person.

**Tool:** treg `treg.people.email.find` with `X-Treg-Route-Verify: true`, capped with `X-Treg-Route-Max-Cost`. Separate verify call only for results the first pass flags. Cost reference: verify tools list at $0.00018 to $0.0009 per success. Coverage in Ghana is untested, so test on a 20-person sample before scaling.

| Decision | Answer | Leads to |
|---|---|---|
| Verification verdict | valid | Send queue |
| | accept_all (catch-all) | Risky. Send only to Tier A, in small batches, watch bounces. Otherwise use LinkedIn first |
| | invalid or not found | No email. LinkedIn only, or drop |
| Is the domain a free mail provider? | Yes | LinkedIn only |
| Did the find cost exceed the cap? | Yes | Skip the person, do not retry on another paid tool for the same person |
| Bounce rate on first batch higher than the pause line? | Yes (PROPOSAL: set the line before launch, e.g. with the sender) | Pause the workflow, re-verify the list, check domain and inbox health with `/inbox-placement-test` |

Phone and WhatsApp finders exist in treg, but no phone or WhatsApp step is in the playbooks. Not included (Open question 6).

---

## Step 9. The sequence (email and LinkedIn)
**What happens:** Generate copy with `/campaign-copy` from the approved route, then `/campaign-qa` against the spec. A person approves the first batch before it sends.

| Channel | Structure (from playbooks [pb]) |
|---|---|
| Email | 3 to 4 steps over about 14 days. Aim for 60 words, ceiling 120. Step 1 earns a reply, step 2 earns the meeting. Each follow-up adds new value, shorter than the one before. Lowercase subject, 8 words or fewer |
| LinkedIn | Empty connection request. DM 1 one sentence, 1 to 2 days after accept. DM 2 two to three sentences, 3 to 5 days later. No third DM. 20 to 30 requests per day per account at most |
| Timing | Email on day 0, LinkedIn connection request on day 1 to 2 |

**Tools:** Sequencer (not chosen), LinkedIn automation (not chosen), Clay for variables, `/campaign-copy` and `/campaign-qa` for copy and checks.

| Decision | Answer | Leads to |
|---|---|---|
| Does every claim in the copy exist in `facts.md` as approved? | Yes | Proceed |
| | No | Facts gate fails. Render `{{placeholder}}` or remove the line. Do not send |
| Does copy pass the ban list (`copy-bans.yaml` and Hubtel bans in `facts.md`)? | No | Rewrite. Do not ship |
| Has a person approved the batch? | No | Hold. Approval is required before any send |
| Does the contact have an email? | Yes | Email first, LinkedIn staggered |
| | No | LinkedIn only |
| Contact replied, bounced, unsubscribed or asked to stop? | Yes | Stop the sequence for that person at once (step 10) |
| Same company already in sequence from another workflow? | Yes | Suppress the new one. Merge signals into one message |
| Copy fingerprinted by inbox providers? | Placement drops | Refresh copy lines and subjects every 4 to 6 weeks [pb] |

---

## Step 10. Reply handling
**What happens:** n8n pulls replies from the sequencer inbox, classifies them, and Claude drafts a response. A person approves every outgoing reply. The reply is logged to HubSpot.

| Class | What it looks like | Action |
|---|---|---|
| Interested | Wants a call or details | Draft reply with one clear next step. Notify the sales owner. Create deal (step 11) |
| Question | Asks about fees, funds, compliance, customers | Answer only from `facts.md`. If not approved, hand to Hubtel sales. Never improvise a fee or compliance claim |
| Not now | Later, busy | Snooze with a date. Re-enter only on a new signal |
| Wrong person | Refers a colleague | Add the referred person at step 7 with a note |
| Not interested | Clear no | Close, suppress, log reason |
| Unsubscribe or hostile | Stop, remove | Stop all channels at once. Add to suppression |
| Out of office, auto-reply | | Wait. Do not count as a reply |
| Unclear | | Human reads it |

| Decision | Answer | Leads to |
|---|---|---|
| Is the reply about price or compliance? | Yes | Human answer only, using approved facts |
| Is it a referral? | Yes | Step 7 for the new person, thank the referrer |
| Reply within the working window? | No | Queue for next morning (PROPOSAL: response target set with Hubtel sales) |

---

## Step 11. The CRM (HubSpot)
**What happens:** HubSpot holds companies, contacts, deals and the outcome of every workflow. Clay writes company and contact records; the sequencer or n8n logs replies; sales owns deals.

| Object | Key fields |
|---|---|
| Company | Domain, segment, tier, fit status, source workflow (W1 to W5), signal text and date, signal source URL |
| Contact | Persona, role, email status (valid, accept_all), channel history |
| Deal | Source workflow, route used, reply class, stage, closed reason |
| Note | Message sent (route and version), reply text |

| Decision | Answer | Leads to |
|---|---|---|
| Interested reply logged? | Yes | Create deal, owner assigned by segment |
| Deal moves | Meeting held | Stage update, sales takes over |
| | Won | Tag customer. Suppress from all outbound. Ask Hubtel whether the case can be used in `facts.md` |
| | Lost | Record loss reason (required). Feeds step 12 |
| Does a record already exist (same domain)? | Yes | Update, never duplicate |
| Is a field missing at stage change? | Yes | Block the stage move until filled. This keeps data clean |

---

## Step 12. Weekly feedback loop into the Context OS
**What happens:** Once a week, a person and Claude review last week's funnel and update the repo. The output lands in `weekly-priorities/<ISO week>.md` and `work-log/<ISO week>.md`.

**Review table (per workflow, per route):** signals found, companies fit, people found, emails valid, sent, replies by class, meetings, deals, closed won or lost with reasons. Counts only; no benchmark is claimed because none exists in the research.

| Question | If yes | If no |
|---|---|---|
| Did a signal fire fewer times than expected for 3 weeks? | Revise or kill it in `signal-matrix.md` with the reason | Keep |
| Did a route get replies but no meetings? | Edit that route's copy in `messaging.md`; note in `knowledge-base/learnings/` | Keep |
| Did a segment give zero replies after a fair sample? | Lower its priority in `icp.md`; question the ICP rule | Keep |
| Did any reply raise a new objection or word? | Add to `personas.md` and `messaging.md` (buyer words are Not found today) | Keep |
| Did Hubtel approve or retire a claim? | Update `facts.md` the same day | Keep |
| Did a won or lost deal teach a size, industry or title pattern? | Fill the size rule and titles in `icp.md` and `personas.md` | Keep |
| Did bounces or placement drop? | Rebuild lists and refresh copy (step 8, 9) | Keep |

**Writes back to:**
| File | What changes |
|---|---|
| `context/icp/icp.md`, `personas.md` | Size rule, titles, objections, non-fits |
| `context/icp/signal-matrix.md` | Scores, kills, new signals |
| `context/messaging/messaging.md`, `facts.md` | Words, angles, approved claims |
| `knowledge-base/learnings/` | What worked and what did not |
| `weekly-priorities/`, `work-log/` | Next week's plan and what changed |

---

## Check against the four pillars
| Pillar | How this design meets it | Where it is weak |
|---|---|---|
| **Clean data** | One source of truth (Context OS). Facts gate: no unapproved claim reaches copy. Dedupe by domain in step 3. HubSpot blocks stage changes with missing fields. Every field carries a source and an `inferred` flag | Customer size, buyer titles and fees are Not found, so some rules are hypotheses. LinkedIn undercounts Ghana headcount. Case-study customers are anonymous |
| **Always-on signals** | Monitors in step 2 run on a schedule through n8n and write dated hits. Dead signals are flagged after three empty runs | Signal volume in Ghana is unknown. Only three sources are tested (LinkedIn jobs, profiles, posts). Registers and tender portals are unopened, access unconfirmed. BoG notice is a market-level hook, not a prospect list |
| **Composable workflows** | Steps 3 to 11 are shared. A new workflow only adds a signal (step 2) and a route (step 6). Five workflows come from three universal signals and four niche builds [sm] | The sequencer and LinkedIn tool are not chosen, so steps 9 and 10 cannot be built yet. Clay actions were not tested here |
| **Tight feedback loops** | Weekly review writes to ICP, signal matrix, messaging and facts. Deal closed reasons are required in HubSpot. Reply classes map to specific files | No win/loss history exists, so early weeks have little data. Reply classification quality is untested. Small volume may make weekly signals noisy; then extend to fortnightly (PROPOSAL) |

## Build order (PROPOSAL)
1. **Week 1:** Hubtel approves claims and names an approver. Choose the sequencer and LinkedIn tool. Test treg email find on 20 Ghanaian contacts.
2. **Week 2:** Build W1 (hiring) end to end on a small batch in Clay and n8n, with the volume test running for W2 and W3 sources.
3. **Week 3:** Pilot send to Tier A only, human approval on every send, HubSpot logging live.
4. **Week 4:** First weekly review. Keep, fix or kill each signal. Add W2 and W3 if their sources work.
5. **After that:** W5 as an enrichment. W4 overlay only when Hubtel confirms its Notice 43 position.

## Risks
- Claims are unapproved, so no copy can go out yet [fx].
- Ghana data and tool coverage are untested; first results may show most signals are too thin.
- Email accept-all rates in Ghana are unknown.
- Public repo: do not put contact lists, replies, or CRM exports here. `.gitignore` already excludes CSV and XLSX.

## Open questions
1. Which sequencer and LinkedIn automation tool, and who owns the inboxes and sender names? Not found.
2. Who at Hubtel approves claims, and how fast?
3. Which signals produce enough volume in Ghana? Counts needed first.
4. What is the real fee, so segment 5 and the pricing pillar can be released?
5. What is Hubtel's Notice 43 position, so the W4 overlay can be used?
6. Should WhatsApp or phone be a channel? Not in the playbooks. Hubtel's own X post uses a WhatsApp number for rider recruitment [res signals.md], which suggests the channel matters locally. INFERRED.
7. What do sales do after a meeting is booked, and what counts as a qualified opportunity? Not found.
8. Are Clay, HubSpot and n8n the actual stack? The list came from a bracketed example in the brief.
