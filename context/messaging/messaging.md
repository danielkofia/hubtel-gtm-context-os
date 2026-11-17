# Hubtel messaging (draft for approval)

Built from `context/icp/icp.md`, `personas.md`, `signal-matrix.md` and the research in `context/docs/research/`. Source tags: [co] company.md, [cu] customers.md, [cp] competitors.md, [mk] market.md, [sg] signals.md, [vo] voice.md, [icp] icp.md, [per] personas.md, [sm] signal-matrix.md, [pb] knowledge-base/playbooks/copy-bans.yaml and signal-matrix-framework.md. INFERRED = my synthesis, not stated in the research. Customer metrics are Hubtel's own, self-reported, customers unnamed [cu]. Nothing here is approved for sending until Hubtel signs off the claims (see Open questions).

## Core message
**Hubtel removes what blocks payments in Ghana, so you collect more of what you are owed.**
- Anchor: Hubtel's own line, "When nothing blocks payments, growth happens." [vo][co]
- Why this shape: all three flagship cases are about collecting more through more channels and hours [cu][icp]. INFERRED synthesis.
- Sender register: plain, Ghana-rooted, benefit first [vo].

## Pillars
| # | Pillar | Message (draft copy line) | Proof point | Source | Status |
|---|---|---|---|---|---|
| 1 | Every channel, one platform | "Your customers pay the way they already pay: MTN MoMo, Telecel Cash, AT Money, card, bank, POS, USSD or an invoice link. You run it from one place." | Hubtel's channel list. Power distributor went from "less than 22% of its revenue potential" to "GHS 51 billion through a single platform" (Hubtel case, customer unnamed, 2026-06-24) | [co][cu] | Ready, claims need Hubtel sign-off |
| 2 | Collect when customers are ready | "Take payment when the customer is ready, not only when your office is open." | Insurer: "office-hours selling" to "84% more policies per agent" (2026-06-26). Power distributor above. Akwantuo Express: 80% of transactions through the API and revenue leakage cut to zero (search summary, body not read) | [cu] | Ready for insurer and utility proof. Hold Akwantuo figures until verified |
| 3 | Built in Ghana, at scale | "Twenty years in Ghana. About 8,000 businesses. The CEO puts Hubtel at about 12% of Ghana's fintech transaction volume." | "20+ years" (founded 2005); "7,979+" and "over 8,000" businesses; 722 staff (April 2025); CEO: "just about 12% of the volume of transactions"; gaming case GHS 162B | [co][vo][cu] | Ready as self-reported. Number conflicts: 7,979+ vs 8,000+ vs 15,000 [co]. Use "about 8,000" |
| 4 | Pay out and collect by API | "Collect by direct debit, pay out through the Send Money API, confirm by SMS. Your team integrates once." | Direct Debit API (Akwantuo), Receive & Send Money API (Aura-Rich), Send Money, SMS and Notification APIs and USSD deposits (gaming case) | [cu] | Ready for champion. API docs not read (developer site returned 403) [cu] |
| 5 | Licensed and accountable | Not drafted. | Bank of Ghana approval as a payment service provider in 2022 (Wikipedia). Hubtel's position on BoG Notice 43 (merchant funds segregation): Not found | [co][mk][sg] | ON HOLD. Do not send until Hubtel confirms its funds set-up and licence evidence |
| 6 | Upfront, simple pricing | Not drafted. | Hubtel page text: "Simple transparent transaction fee of 1.95% per transaction value." Third parties say 1% to 3%. CEO: "When we serve small businesses, we charge upfront." | [co][cp][vo] | ON HOLD. Fee table did not load, figures conflict |

## Angle per persona
Persona titles are Not found [per]. Angles are hypotheses for sales to validate.

| Persona | Lead pillar | Angle | Lead proof | Do not say | Source |
|---|---|---|---|---|---|
| Champion (runs collections, payouts, integration) | 1 then 4 | "One platform for every pay-in channel, with APIs for payouts and confirmations." Talk about channels, reconciliation and integration work | Channel list; Direct Debit and Send Money APIs [cu] | Fee numbers; unverified API features | [per][cu][co] |
| Economic buyer (approves spend) | 2 then 3 | "More of your revenue collected, through the channels customers use, from a provider with 20 years in Ghana." Talk about revenue captured and leakage | Insurer 84%; utility "less than 22%" to "GHS 51 billion"; scale claims [cu][co] | "Cheapest"; a fee number; named customers | [per][cu][co] |
| Influencer (compliance, risk, procurement) | 5, on hold | Hold. Once Hubtel confirms: "Here is where merchant funds sit and how we meet Notice 43." Until then lead with pillar 3 track record only | Not found: Hubtel compliance response [sg] | Any claim of compliance with Notice 43 or fund safety | [per][mk][sg] |

Segment emphasis (from [sm] Matrix 1): utilities lead with pillar 1 and the "single platform" case; insurers lead with pillar 2; gaming leads with pillar 4 (USSD deposits, payout APIs); transport and school-fee collectors lead with direct debit (pillar 4); POS merchants hold until fee is confirmed.

## Words to use (Hubtel's own)
| Word or phrase | Where Hubtel says it | Source |
|---|---|---|
| "When nothing blocks payments, growth happens." | Homepage headline | [co][vo] |
| "useful", "Useful Everyday" | Homepage; "Africa's most useful company"; "Ghana's most useful app" | [vo] |
| "scale-ready businesses in Ghana" | Homepage audience line | [co][vo] |
| "Clarity", "Control", "Growth" | Product names on homepage | [co][vo] |
| "single platform", "single service" | Power distributor case title; Stanford profile | [cu][vo] |
| "connecting businesses to communities" | "20+ years of connecting businesses to communities" | [co][vo] |
| "Switch to Hubtel" | Homepage nav | [co] |
| "ownership, integrity, and continuous improvement" | Careers page, culture | [vo] |
| "revenue potential", "office-hours selling", "revenue leakage" | Case-study language for the buyer's problem | [cu] |
| "woven into the story of Ghana" | CEO, Oct 2025 | [vo] |

## Words and angles to avoid
### Words
| Avoid | Why | Source |
|---|---|---|
| "cheap", "cheapest", "lowest fee", "best price" | Hubtel's homepage says it is not for businesses wanting "the cheapest fee" (exact wording needs a manual check). Global ban on "cheap" | [co][pb] |
| "unlock", "solutions", "seamless", "empower", "streamline", "comprehensive" | Hubtel itself uses "Unlock Growth" in its page title, but the global copy-ban list forbids these words. Use "grow", "collect", "run" instead | [vo][pb] |
| "free", "guaranteed" | Global ban. Also unsupported: no free tier or guarantee in the research | [pb] |
| "pan-African", "across Africa", "cross-border" | Hubtel markets Ghana only. Expansion is an ambition, not a capability. One source says it lacks cross-border, unverified | [co][cp] |
| "number one fintech", "Africa's most useful company" as fact | CEO opinion and a stated goal, not verified | [vo] |
| Exclamation marks and em dashes | Global ban and the repo rule. Hubtel's own X post uses an exclamation mark; do not copy it | [pb][sg] |

### Angles
| Avoid | Why | Source |
|---|---|---|
| Price-first or fee-comparison angle | Conflicting fees (1.95%, 1%, 2.5% plus fixed, up to 3%); comparison sites are commercial; Hubtel positions as not cheapest | [co][cp] |
| Quoting any fee number | Fee table did not load; no approved figure | [co] |
| Naming case-study customers (e.g. SportyBet, ECG) | Hubtel did not name them; the links are INFERRED only | [cu] |
| Using the 785%, 80% and GHS 23.65 billion figures | From search summaries of case studies, bodies not read | [cu] |
| Saying funds are segregated, safe or Notice 43 compliant | Hubtel's position is Not found, and the notice cuts both ways | [mk][sg] |
| Fear angle about regulators, or naming Zeepay | Zeepay fit unclear; negative framing about a named company is a risk. INFERRED | [mk][sm] |
| Diagnosing the buyer ("your collections are failing") | Playbook guardrail: guess their situation, not their problems | [pb] |
| Mixing consumer super-app lines (food, rides, stores) into B2B copy | Dilutes the collections story. INFERRED | [co][icp] |
| Government-payer angle | CEO calls whether governments should pay upfront "an open debate" | [cu] |
| Defensive CEO lines ("heavily misunderstood by the public") | Reads as a problem, not a benefit. INFERRED | [vo] |

## Open questions (to approve before use)
1. Which customer claims can Hubtel approve for outbound, and may any customer be named? [cu]
2. What is the real fee and does it vary by channel? [co][cp]
3. What is Hubtel's Notice 43 position and licence evidence? [sg]
4. Can Hubtel share the case-study bodies so the 80%, 785% and USSD claims can be verified? [cu]
5. Who is the sender and what is the CTA? No sender or sales process in the research.
6. Which buyer words appear on real calls? Buyer quotes are Not found [cu].
