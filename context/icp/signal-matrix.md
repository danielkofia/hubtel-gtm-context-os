# Hubtel signal matrix (work in progress)

Method: `knowledge-base/playbooks/signal-matrix-framework.md` and `workflow-anatomy.md`. Inputs: `context/icp/icp.md`, `context/icp/personas.md`, `context/docs/research/*`. Tags: [co] company.md, [cu] customers.md, [cp] competitors.md, [mk] market.md, [sg] signals.md, [vo] voice.md. Anything not in those files is marked INFERRED, or WEB when I checked it on the web on 2026-11-16 outside the research files. This is a draft for validation with Hubtel sales, not a final deliverable.

## Read this first
- One product line to the buyer: payments collection and payouts for Ghanaian organisations, with the same platform doing mobile money, cards, USSD, POS and APIs [co][cu]. So Matrix 1 changes the angle per cell, not the product.
- Ghana has a weak digital footprint for B2B signals. INFERRED from the framework's Colombia and Argentina notes, which say government registries and physical-world signals beat LinkedIn-style signals. The research has no Ghana data volumes (Not found).
- Persona titles and buyer quotes are Not found [co][cu]. Angles below are hypotheses for sales to validate.
- No named prospect companies. The case-study customers are anonymous [cu], so I left "company examples" as "Requires research with these filters" rather than guess.

## Matrix 1: segments by personas (angle per cell)
Rows are the five ICP segments, ranked by proof [icp.md]. Columns are the personas [personas.md]. Each cell is the angle: the line of reasoning to lead with.

| Segment (proof) | Champion (runs collections, payouts or integration) | Economic buyer (approves spend) | Influencer (compliance, risk, procurement) |
|---|---|---|---|
| **1. Utilities and power distributors** (power distributor case: "less than 22% of its revenue potential" to "GHS 51 billion through a single platform" [cu]) | One platform for every pay-in channel, so collections stop leaking between channels. Source claim: single platform [cu] | Revenue captured against potential. Use the "less than 22%" case only as Hubtel's own claim, customer unnamed [cu] | Where merchant funds sit under BoG Notice 43 (2026-11-06) [mk]. Hubtel's own set-up and compliance response: Not found [sg], so do not assert it. Get Hubtel's answer first |
| **2. Insurers** (insurance case: "office-hours selling" to "84% more policies per agent" [cu]) | Let agents sell and customers pay outside office hours using mobile money and USSD. INFERRED link from "office-hours selling" to channels | Policies per agent, using the 84% as Hubtel's claim [cu] | Funds handling and licence status, from Notice 43 and the Zeepay revocation [mk]. Hubtel's answer Not found |
| **3. Betting and gaming** (gaming case: "built its entire Ghana payment operation on Hubtel", GHS 162B [cu]) | USSD deposits for users without smartphones, and payout APIs (Send Money API, SMS and Notification API) [cu, from search summary, body not read] | Transaction value and growth, e.g. "785% growth in transaction value from 2021 to 2025" [cu, search summary, unverified] | Licence and funds rules. A BoG directive on crypto and FX wallets shows regulator attention on payment providers [mk] |
| **4. Transport and school-fee collectors** (Akwantuo Express, Aura-Rich Consult [cu]) | Recurring collection by Direct Debit API, or Receive & Send Money API for school payments [cu] | Revenue leakage "cut to zero" and "80% of transactions" through the API, per search summary [cu, unverified] | Not found. No influencer evidence for this segment |
| **5. POS merchants** (Golden Crystal Experience, Rabito Clinic [cu]) | Hubtel POS for customer service at the counter [cu]. Detail Not found | Fee. Do not lead with a number yet: Hubtel's own page says 1.95%, one POS case study says "competitive 1% transaction fee" [co][cu] | Not found |

Priority flags (INFERRED from [icp.md] grades): High = 1, 2, 3 (grade A proof). Medium = 4. Low for outbound = 5 (many small merchants, per-account value not in research).

## Matrix 2: signals by segment
Scored on four tests, 0 to 3 each, total out of 12. R = clear buying reason. V = enough volume. D = data you can get. S = natural story. All scores are my judgement (INFERRED). Volume in Ghana is Not found for every signal, so V is a guess.

Tool key: **Clay** actions come from the framework and were not tested in this workspace. **treg** calls were tested: LinkedIn jobs (`harvestapi.linkedin.search.jobs`, $0.001, worked, 0 results for Hubtel), LinkedIn company profile (`fetchinio.linkedin.company.profile`, $0.0015, worked), LinkedIn company posts and X posts (`scrapecreators`, $0.00188, worked) [sg]. **crawl4ai** and **agent-browser** are in `tools/` and untested. **n8n** schedules and diffs.

| # | Type | Signal | Mother intent (catalog) | Data source | Tool to detect | Segments | R | V | D | S | Total | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| U1 | Universal | Hiring for collections, revenue assurance, payments, digital channels or mobile money roles | Hiring specific roles | LinkedIn Jobs (WEB: treg tool verified, Ghana volume Not found); Indeed or local boards INFERRED | treg `harvestapi.linkedin.search.jobs`, Clay Find Jobs, n8n weekly | 1, 2, 3, 4, 5 | 2 | 1 | 2 | 3 | 8 | Planned, test volume first |
| U2 | Universal | New CFO, head of digital, head of IT or payments lead in last 90 days | New leadership | LinkedIn people data; titles for this buyer Not found [personas.md] | Clay Find People with start-date filter, treg LinkedIn profile tools | 1, 2, 3 | 2 | 1 | 2 | 2 | 7 | Use as secondary enrichment, not a trigger |
| U3 | Universal | Headcount growth over 20 to 25% | Hypergrowth (headcount) | LinkedIn company profile. Hubtel's own profile shows 557 against 722 on payroll [co], so LinkedIn undercounts | treg `fetchinio.linkedin.company.profile` monthly snapshots, n8n diff | 3, 4 | 1 | 2 | 2 | 1 | 6 | Weak, compound only |
| N1 | Niche | Business still uses or lists a provider hit by regulation (Zeepay, licence revoked July 2026) [mk] | Competitor customers or website content mentions | Prospect websites and web search for the provider name. WEB: exact source varies | treg `treg.google.serp.organic`, crawl4ai | 2, 3, 4 (INFERRED: Zeepay serves remittance and e-money, fit unclear) | 2 | 1 | 2 | 3 | 8 | Decaying, one-time list |
| N2 | Niche | BoG notice on payment providers (Notice 43 on merchant funds, 2026-11-06; Nos. 41 and 42) [mk] | Regulatory changes | bog.gov.gh notice pages [mk]. Hubtel set-up Not found | crawl4ai or agent-browser watch, n8n diff, alert | 1, 2, 3, 4, 5 | 2 | 3 | 3 | 2 | 10 | Message overlay, not a filter. Cuts both ways: buyers may question every PSP, Hubtel included |
| N3 | Niche | Public pressure on revenue collection at a distributor (WEB: IMF 2026 paper reports ECG declared GH¢10.4B against validated collections of GH¢15.5B; PURC probed prepaid credit depletion, Feb 2026. Not in research) | Regulatory changes or content mentions | News, PURC, IMF paper. WEB | treg web search, n8n | 1 | 3 | 0 | 2 | 3 | 8 | Account list, not a workflow: a handful of distributors |
| N4 | Niche | New or renewing gaming licence (WEB: Gaming Commission licensed-operators page per third-party sites; licences annual, e.g. valid 1/1/2026 to 31/12/2026; counts conflict 15 to 35) | Licensing events | gamingcommission.gov.gh licensed operators (WEB, not opened by me) | crawl4ai or agent-browser, n8n diff monthly | 3 | 3 | 1 | 2 | 3 | 9 | Planned. INFERRED: new licensee needs Ghana payment rails |
| N5 | Niche | Public tender for a collection platform, payment gateway, revenue collection or fee system | Public procurement (framework niche list) | GHANEPS and PPA tender notices (WEB: ghaneps.gov.gh, ppa.gov.gh; entities must advertise on PPA site; supplier registration needed) | crawl4ai or agent-browser, n8n daily diff, Clay HTTP | 1, 4 (INFERRED: public utilities, public schools and state bodies) | 3 | 1 | 2 | 3 | 9 | Planned. Check access limits first. CEO says government clients paying upfront is "an open debate" [cu], so expect slow payers |
| N6 | Niche | Public statement of manual or limited-hours collection ("office-hours", queues, leakage) | Website content mentions | Company news and LinkedIn posts. Framework warns this needs manual research | treg web search, LinkedIn post tools | 1, 2, 4 | 3 | 0 | 1 | 3 | 7 | Partial. Use for personalisation, not to build lists |
| N7 | Niche | Insurer on the NIC good-standing list (WEB: latest list found 2020, 130 entities incl. 17 life and 27 non-life; check nicgh.org) | ICP filter, not a timing signal | nicgh.org | crawl4ai, Clay HTTP | 2 | 0 | 2 | 2 | 1 | 5 | Account universe only. Pair with U1 or U2 |

### Killed or blocked (documented so we do not retry them)
| Signal | Why |
|---|---|
| Fundraising | Hubtel itself shows one unattributed round and is described as self-funded [co]. INFERRED same for most Ghanaian mid-market. Framework says useless without a VC ecosystem |
| BuiltWith technographics | Cannot see backend payment tools. Framework: compound only |
| LinkedIn content engagement | Framework: low volume where buyers do not post. Hubtel's own X account is quiet (last original post 2026-03-05) [sg] |
| Website visitor deanonymisation (RB2B) | Catalog says US companies with 20k+ visitors only |
| Lookalike of customers | Blocked. Customers are anonymous [cu]. Unblocks if Hubtel shares a customer list |
| Competitor customers via technographics | Folded into N1 for web mentions. BuiltWith cannot see this |

### Compounding view
- Universal, build once: U1, U2, U3. Same Clay and treg build for all five segments; only keywords and angle change per Matrix 1.
- Niche, one build each: N2 (BoG), N4 (gaming licence), N5 (tenders), N7 (NIC list).
- Segments 1 and 4 share one niche build (N5). Segments 2 and 3 each need their own registry.

## Build first
1. **U1 Hiring signal.** Build once, cover all five segments, cost is tiny ($0.001 per treg search, tested). Risk: Ghana volume unknown. Run a 2-week volume test before committing the workflow.
2. **N5 Public tenders.** The only signal where the prospect announces a buying process. Fits segments 1 and 4 (utility and schools). Check portal access and tender categories before building.
3. **N4 Gaming licence events.** Segment 3 has the strongest Hubtel proof (GHS 162B) [cu] and a small registry with annual dates, so it is a bounded, repeatable list. Volume is low but each win is large.
4. **N2 BoG notices as an overlay.** Not a list. Monitor the notices and route every message through it. It is the most timely hook, and it cuts both ways. Do not use it until Hubtel confirms its own funds-segregation position (Not found [sg]).
5. **U2 New leadership as a secondary enrichment** on U1 and N4 hits. Persona titles must be confirmed first [personas.md].

Not in the first five: N3 (too few accounts for a workflow, use as an ABM list for segment 1), N1 (decaying), N6 (manual), N7 (static list), U3 (weak).

## Matrix 3: workflow tracker (planned)
| W # | Status | Workflow name | Mother intent | Segments | Persona | Channel | Clay or treg link | Total leads |
|---|---|---|---|---|---|---|---|---|
| 1 | Planned | Hiring collections and payments roles | Hiring specific roles | 1 to 5 | Champion | Email, LinkedIn | | |
| 2 | Planned | Public tenders for collection platforms | Public procurement | 1, 4 | Champion, influencer | Email | | |
| 3 | Planned | New gaming licence | Licensing events | 3 | Economic buyer | Email, LinkedIn | | |
| 4 | Planned | BoG notice overlay | Regulatory changes | 1 to 5 | Influencer | Message layer | | |
| 5 | Planned | New leader on a signal hit | New leadership | 1, 2, 3 | Economic buyer | LinkedIn | | |

## Open questions (before building)
1. Which signal volumes hold in Ghana? Run counts for U1, N4, N5 first. Not found anywhere in the research.
2. What are the buyer titles in each segment? [personas.md]
3. Can Hubtel state its Notice 43 position, so N2 can be used safely? [sg]
4. Does GHANEPS allow automated reading? WEB check needed on terms and login.
5. Which of the five segments does Hubtel's sales team already close? No win/loss data [icp.md].
6. Can Hubtel name the three anonymous case-study customers, or share its customer list to unblock lookalikes? [cu]
