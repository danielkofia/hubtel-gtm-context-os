# Workflow spec: Licensed gaming operators in Ghana

**Status:** STRUCTURE-APPROVED 2026-11-19 · copy pending

Combines campaign-strategy ideas 1 (new gaming licence wave) and 4 (licensed gaming operators list), plus an always-on hiring overlay. Labels: Tested = we ran it. INFERRED = my reading, not evidence. To-detect = a read we must build and test. Not found = no data. Persona titles are INFERRED and need a people search to confirm. Nothing here is copy.

## 1. Mother intent [ENGINE]
**Operators that hold a current Gaming Commission licence for online betting or gaming in Ghana, and so must run deposits and payouts in Ghana every day.**

- Catalog match: not in the Mother Intent Catalog. Closest is "Niche-specific play". Flagged as a new intent: licensing events (a brand appearing on, or staying on, the regulator's register).
- Signal-led, not vertical-led: the trigger is the register entry, not "betting companies".
- Two ways in: **New** (brand first seen on the register since the last snapshot) and **Listed** (brand already on the register). Same list, different timing.

## 2. Inclusion and exclusion [ICP]
### Include
| Element | Rule | Evidence |
|---|---|---|
| Geography | Ghana. Licensed by the Gaming Commission | Register, Tested 2026-11-16 |
| Industry | Segment 3, betting and gaming | icp.md (grade A proof, anonymous gaming case) |
| Licence | Brand has at least one register row of type Sports Betting, Online Sports Betting, Online Casino, Remote Interactive Games, or Online & Land-Based Sports Betting. **47 named brands** in the 2026-11-16 snapshot | `gaming-licensed-operators.csv` |
| Licence validity | Row end date is today or later. All 47 run 1 Jan to 31 Dec 2026 | Tested |
| Size | Not found. "Scale-ready" has no number in `icp.md`. No size filter in v1 | icp.md open question 1 |
| Trigger | Brand listed on the register (S1). New brand = not in any earlier snapshot (S2) | see section 4 |
| Recipient | One person per company per cycle, in this order: Head of Payments, Finance Manager or CFO, Country Manager. All INFERRED titles, confirm with a people search | personas.md (titles Not found) |

### Exclude
| Who | Why | How it is read |
|---|---|---|
| Existing Hubtel customers | Do not cold-email a customer. Hubtel's gaming case is anonymous, so we cannot name it | **To-detect:** regex "hubtel" in text or image alt text on the brand's deposit page (G1). Risk: many deposit pages sit behind a login or JavaScript, so a miss is possible. Hubtel sales reviews the list before any send |
| Active Hubtel pipeline | Avoid double outreach | Not found. Ask Hubtel for a list |
| 21 named brands with only Casino (land-based), Bingo, Scratch Card or Route licences | Cash or non-online payment. INFERRED | Register type |
| 3 rows with a blank trade name | Cannot name the account. Hold until resolved | Register |
| Brand whose licence has ended (CONSUL GAMES, ended 31/01/2026, type Route) | Not current | Register end date |
| Look-alike or affiliate sites | Wrong domain, such as the 1xbet clone sites seen in the test | Domain must be the one that names the brand as licence holder or appears in its own app listing |
| Second brand of an already-contacted company | One conversation per company | Legal company match (S4) |

## 3. Sources [ENGINE]
| # | Data needed | Source | Tool | Cost | Status |
|---|---|---|---|---|---|
| A | Licensed operators (trigger) | gamingcommission.gov.gh/licensed-operators | `treg.web.extract` (site certificate expired, so no normal fetch) | $0.00025 per read | Tested 2026-11-16. 88 rows, 47 brands |
| B | Monthly change | Diff of snapshot A against the previous one | n8n or a script | Free | To-build |
| C | Domain for each brand | Google search on the brand name plus "Ghana betting company official website" | `anyapi.google.serp.organic` | $0.0005 per call | Tested on 10 brands 2026-11-19: 8 clear, 1 probable, 1 uncertain |
| D | Legal company | Footer or terms page of the domain from C | `treg.web.extract` or crawl4ai | About $0.00025 per page (INFERRED) | To-detect, untested |
| E | Existing Hubtel customer check | Deposit and payments page of the domain from C | same as D | same | To-detect, untested. Login walls likely |
| F | Company LinkedIn page | Search by legal company or brand | `fetchinio.linkedin.company.profile` ($0.0015) after a lookup | $0.0015 per profile | Profile call Tested. Name-to-page lookup untested |
| G | Hiring overlay | LinkedIn jobs by company | `harvestapi.linkedin.search.jobs` | about $0.0005 per search | Tested in the hiring sample: titles returned, description text not returned |
| H | People | LinkedIn people search by company and title | Clay Find People or treg LinkedIn tools | Not found | Untested for Ghana |
| I | Email | Clay email waterfall | Clay | Not found | Not chosen, untested for Ghana |

## 4. Signals table [ENGINE]
Every read is a boolean, a count or a regex. Roles: trigger fires the send, router picks the narrative, context-clause is one line of colour and never routes.

| # | Signal | Role | How it is read | Output |
|---|---|---|---|---|
| S1 | On the register | trigger | Brand name matches at least one register row of an included licence type with end date today or later | true or false |
| S2 | New to the register | router | Brand name is in snapshot A now and in no earlier snapshot. Compare names after upper-casing and trimming. Renewal in January 2027 is not new, because the name is already in the history | `new` or `listed` |
| S3 | Hiring for payments or finance roles | router | Count of open LinkedIn postings at the operator's company page, posted in the last 30 days, whose **title** matches regex `payment\|collections?\|treasury\|reconciliation\|mobile money\|digital channels?\|finance manager\|head of finance\|fintech\|billing`. Only titles are read, because description text is not returned (Tested). Weekly refresh | cluster: `0` = not hiring, `1+` = hiring |
| S4 | Legal company name found | context-clause | Regex on footer and terms text: a name ending in `Ltd`, `Limited`, `Company` or `Inc`, within 120 characters of `operated by`, `owned by`, `licensed to` or `a company registered` | text or empty. Used for de-duplication, never for routing |
| S5 | Product mix | context-clause | Count of the operator's included licence types: 1 = one product, 2+ = several (sports betting and casino) | cluster: `one`, `several` |

**Count cluster for S3:** `0` means no open payments or finance posting found. `1+` means at least one. Two clusters only. A higher count is not routed, because the tested volume is thin (13 postings in Ghana in the 30-day sample, 5 in Ghana, 0 in an ICP segment).

### Gates (checked before a person is contacted; not signals, never routed)
| # | Gate | How it is read | If false |
|---|---|---|---|
| G1 | Not an existing Hubtel customer | regex `hubtel` absent from deposit page text and alt text (source E) | Hold. Hubtel sales confirms |
| G2 | Domain resolved to the brand's own site | Result from source C, top result on the brand's own domain, not an affiliate | Hold for manual check |
| G3 | One company only | S4 name not already contacted in this cycle | Skip the duplicate brand |
| G4 | Buyer found | A person at the company whose title matches `head of payments\|payments (lead\|manager)\|finance manager\|chief financial officer\|\bcfo\b\|country manager\|general manager` | Hold. Not sendable |
| G5 | Email verified | Verifier result valid | Hold |

### Open points for you
1. **S3 is a router on thin data.** I expect most accounts to land in `0`. I kept it as a router, as your instructor advised and because it costs about $0.0005 per account per search. If you prefer, I can downgrade it to a context-clause, which removes one axis from section 5.
2. **G1 may miss existing customers** if deposit pages sit behind a login. A short 10-brand test would show how often. Until then Hubtel sales reviews the list.
3. **S2 depends on how fast the register updates.** Not found.
4. **Titles in G4 are INFERRED.** Hubtel has not confirmed who buys at an operator.

## 5. Routing matrix with angles [ENGINE]
Two axes, both named in section 4. Axis 1 is S2, with 2 values: `new` or `listed`. Axis 2 is S3, with 2 values: `0` or `1+` open payments or finance postings in the last 30 days. Stacked: 2 x 2 = **4 cells**. S4 and S5 are context-clauses and do not route. The recipient fallback order (section 2) is not an axis.

Inference rule used: each row says what the company is probably DOING, not how it feels. Angles are meaning, not copy. Nothing here is a Hubtel claim: no number, no customer, no compliance statement. Pillar references are to `messaging.md`. Pillar 4 (APIs, USSD, payouts) leads for gaming.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns |
|---|---|---|---|
| **A: New, not hiring** | S2 = `new` and S3 = `0` | The brand has just appeared on the Gaming Commission register. INFERRED: it is preparing to take Ghanaian players, or has just started. It is not hiring for payments or finance, so INFERRED the work is being handled by an existing team or an outside provider. We do not know which, so we do not assume it has no provider. | **Ghana pay-in and payout rails for a new licence.** Anchor on the one fact we have: they are newly on the register. Speak about the local channels Ghanaian players use (mobile money, USSD for players without smartphones) and about payouts (pillar 4). The ask is a question about who is handling Ghana payments. No assumption that they are unprepared |
| **B: New, hiring** | S2 = `new` and S3 = `1+` | Newly on the register and posting a payments or finance role. INFERRED: the Ghana operation is being built in-house now and the role will own part of it. `{{role_title}}` exists in this cell. | **The integration work the open role will own.** Anchor on the role and the new licence together. Speak to the person who would work with Hubtel's pay-in, payout and confirmation APIs (pillar 4) as input for whoever fills the role. Hedge that the role may cover something else |
| **C: Listed, not hiring (HELD, approved 2026-11-19: stays in the table, does not send)** | S2 = `listed` and S3 = `0` | Already licensed in an earlier snapshot and showing no payments or finance posting. INFERRED: payments are running with the team and provider they have. Nothing visible has changed. This is the weakest cell: no timing signal. | **A second look at channels and payouts for a running licensed operator.** Anchor on the licence types they hold (S5: one product or several) and the register fact. Speak about USSD for players without smartphones and payout through APIs (pillar 4). A single low-pressure question about who owns payments. No claim that something is wrong |
| **D: Listed, hiring** | S2 = `listed` and S3 = `1+` | Established licence holder posting a payments or finance role. INFERRED: a change is under way in how payments are run, though we cannot tell whether it is growth, replacement or backfill. `{{role_title}}` exists in this cell. | **Payments work an incoming hire inherits.** Anchor on the open role. Speak to the integration and reconciliation work that role will start from, and to payout and confirmation APIs (pillar 4). Hedge that the role may be a backfill |

### Branch coverage
- `{{role_title}}`, `{{job_post_url}}` exist only in B and D. A and C never mention a role.
- `{{licence_summary}}` (derived from S5) exists in all four cells.
- `{{legal_company}}` (S4) may be empty in any cell. No angle depends on it. When empty the greeting uses the brand name only.
- `{{first_seen_date}}` exists only in A and B.
- A and C survive without any hiring data. B and D survive without any first-seen data except the new-licence anchor in B, which uses S2 only.

### Niche-native test
- A and B could not be sent by any PSP unchanged: they name a licensing event on the Gaming Commission register.
- D is native to a hiring event at a licensed operator.
- **C is the one that fails.** Any PSP could send "licensed operator, who owns payments?". The only sharpening I can offer is the licence type from S5. If you want, C can be dropped from v1, so that only A, B and D send, and C operators wait until they show a hiring post or a licence change.

### Cell volumes (INFERRED, not tested)
- A: 0 to 3 a month, plus a possible January 2027 batch of new brand names. B: 0 to 1. C: about 40 of the 47. D: 0 to 3. Hiring volume is thin in the test (0 ICP postings in 13).

### Open points for you
1. Decided 2026-11-19: cell C is HELD. It stays in the table and `Ready to Contact?` is false for it until a hiring post or a licence change moves the account to another cell.
2. B and D depend on the hiring regex catching Ghanaian job titles on LinkedIn. Not tested on these 47 accounts.
3. Angles use pillar 4 only. Pillars 5 and 6 are on hold, and no claim is approved in `facts.md`.

## 6. Variables contract [ENGINE]
Copy may use only these variables, in double braces. Anything not listed cannot be said. Names follow `{{snake_case}}`. Match the sequencer's syntax at export.

| Variable | Source field | Exists in branches | Note |
|---|---|---|---|
| `{{first_name}}` | People search, first name of the recipient (gate G4) | A, B, D | Cleaned to first name only |
| `{{company_name}}` | Register `operator_trade_name`, title-cased (S1) | A, B, D | The brand name as the register prints it |
| `{{legal_company}}` | S4 footer or terms regex | A, B, D, but may be empty | If empty, copy uses `{{company_name}}` only. No angle depends on it |
| `{{licence_summary}}` | Register `licence_type` values for the brand, mapped to one plain phrase: sports betting, online casino, remote games, or "sports betting and casino" when several (S5) | A, B, D | Taken from the register, so true by construction |
| `{{first_seen_date}}` | Date of the first snapshot that contains the brand (S2) | A, B | Month and year only. Not the licence issue date, which the register does not publish |
| `{{role_title}}` | Title of the matching open posting (S3) | B, D only | If more than one posting matches, the most recently posted one |
| `{{job_post_url}}` | URL of that posting (S3) | B, D only | Reference only, not shown unless copy needs it |
| `{{sender_name}}` | `facts.md` sender identity | A, B, D | **Not found.** Hubtel has not named a sender. Placeholder until it does |
| `{{sender_title}}` | `facts.md` sender identity | A, B, D | **Not found** |
| `{{approved_claim_n}}` | `facts.md` approved claims table | none yet | **No claim is approved.** No branch may use a number, customer or compliance statement until Hubtel fills the "Approved by" cell |

Held cell C has no variables mapped, because it does not send.

Rules for this contract:
- Data-must-exist: if the field is empty, the line that uses it is dropped. It is never filled from memory.
- No variable carries a fee, a Notice 43 position, a case-study figure or a customer name. Those are banned in `facts.md` until approved.
- `{{role_title}}` is never used in A. It does not exist there.

## 7. Cadence and channel [ENGINE]
| Item | Setting | Basis |
|---|---|---|
| Register snapshot | Monthly. One read per month through `treg.web.extract` | Register is annual and slow, INFERRED. How fast it updates is Not found. Extra read in the first week of January 2027 for the renewal wave |
| Diff (S2) | Monthly, same run as the snapshot | n8n or script, free |
| Hiring check (S3) | Weekly, per account in the list | Job postings are high velocity (workflow-anatomy.md). About $0.0005 per account |
| Domain, legal company, deposit-page check (G1, G2, S4) | Once per new brand, re-checked every 6 months | PROPOSAL |
| People and email | Once per account when it enters a sendable cell, re-verified before each send | PROPOSAL |
| Sendable cells | A, B and D. C is held | Approved 2026-11-19 |
| Channel | Email first. LinkedIn second | Playbook: 3 to 4 email steps over about 14 days; LinkedIn is an empty connection request plus at most two DMs |
| Sequence shape | Email 1, then a LinkedIn connection request, then emails 2 and 3, then one LinkedIn DM. About 14 days | PROPOSAL, from the playbook. Copy not written |
| Volume cap | Under 10 new accounts a week | The list is only 47 brands. Small batches let us read replies |
| Suppression | 90 days after a sequence ends. Re-entry only when the cell changes to one with a new signal (for example D after a hiring post) | PROPOSAL |
| De-duplication | By `{{legal_company}}` (S4). One recipient per company per cycle | Section 2 |
| Review gates | (1) Hubtel sales reviews the list for existing customers (G1) and active pipeline. (2) A human approves each first email. Nothing is sent without your approval | CLAUDE.md rule: ask before sending |

### What this means for the first run
- All 47 brands are `listed` on the first run, because the 2026-11-16 snapshot is the baseline and no earlier one exists. With C held, only cell D can send, and only when a hiring post is found (0 to 3, INFERRED; the hiring sample found 0 in an ICP segment).
- Cells A and B start only when a new brand name appears in a later snapshot. The first realistic chance is the January 2027 renewal.
- So v1 will send very little until then. I think that is the honest result of holding C. The decision to reopen C, or to add a second signal to cells A to D, is yours.

### Blocked before any send
1. `facts.md` has no approved claim and no sender. `/campaign-copy` will refuse to run its gate until one is approved.
2. Sequencer and LinkedIn tool are not chosen.
3. The email waterfall for Ghana has not been tested.
4. Buyer titles in G4 are INFERRED.
