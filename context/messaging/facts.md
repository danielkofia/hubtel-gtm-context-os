# Hubtel: Authorized Copy Facts (DRAFT, nothing approved yet)

> The only source of names, numbers and claims for prospect-facing copy (`/campaign-copy` FACTS GATE). Anything not listed here renders as `{{placeholder}}`, never from memory.
>
> Status: every claim below is a CANDIDATE taken from public sources in `context/docs/research/`. No Hubtel person has approved any of them. Until the "Approved by / date" cell is filled, treat the claim as NOT usable in sent copy. Retire or update a claim the same day its status changes.

**Last updated:** 2026-11-16 by Claude (draft). Approver: pending, Hubtel to name one.

Source tags: [co] company.md, [cu] customers.md, [cp] competitors.md, [mk] market.md, [sg] signals.md, [vo] voice.md, all in `context/docs/research/`. Other: [msg] `context/messaging/messaging.md`, [pb] `knowledge-base/playbooks/copy-bans.yaml`.

---

## Sender identity
| Field | Value |
|---|---|
| Sender name(s) | {{sender_name}}. Not found: no sender or sales owner in the research |
| Title | {{sender_title}}. Not found |
| Signature format | {{signature}}. Not found |
| Sender persona notes | Not found. Hubtel's public voice is plain and Ghana-rooted [vo] |

## What we do (locked value prop)
Candidate variants, from [msg]. The lead-in is verbatim Hubtel; confirm with Hubtel before use.
- **Variant A:** "Hubtel helps businesses in Ghana collect payments on every channel their customers use, from one platform." Basis: channels list and "single platform" [co][cu].
- **Variant B:** "When nothing blocks payments, growth happens." Hubtel's own homepage headline [co][vo]. Use verbatim only.

Product one-liner (context, not copy): Hubtel is a Ghana-based payments and digital commerce company, founded 2005 as SMSGH, offering payment collection, payouts and APIs, POS, bulk SMS and a consumer app [co]. Source for B2B packaging: Not found.

## Approved claims and numbers
No claim is approved. Candidates, with exact phrasing to use if approved:

| Claim | Candidate phrasing | Source | Approved by / date |
|---|---|---|---|
| Experience | "20+ years in Ghana" | hubtel.com homepage: "20+ years of connecting businesses to communities" [co][vo] | Pending |
| Scale (businesses) | "about 8,000 businesses" | Homepage "7,979+"; April 2025 release "over 8,000" [co]. 15,000 appears only in a weak source, never use | Pending |
| Scale (volume share) | "the CEO puts Hubtel at about 12% of Ghana's fintech transaction volume" | CEO, MyJoyOnline 2025-10-04: "just about 12% of the volume of transactions" [co][vo] | Pending. Attribute to the CEO, never state as a fact |
| Customer result: insurer | "a leading insurance company went from office-hours selling to 84% more policies per agent" | Hubtel case study, 2026-06-26 [cu] | Pending. Customer unnamed |
| Customer result: utility | "Ghana's largest power distributor went from collecting less than 22% of its revenue potential to processing GHS 51 billion through a single platform" | Hubtel case study, 2026-06-24 [cu] | Pending. Customer unnamed |
| Customer result: gaming | "a Pan-African gaming and entertainment company built its entire Ghana payment operation on Hubtel" | Hubtel case study, 2026-06-25 [cu] | Pending. Do not quote GHS 162B until the body is checked |
| Channels | "MTN MoMo, Telecel Cash, AT Money, bank, card, POS, USSD and invoice link" | Homepage [co]. USSD from case study [cu] | Pending |
| Licence | "licensed by the Bank of Ghana" | Wikipedia: approval in 2022 as a payment services provider [co]. BoG register entry not found | NOT USABLE. Needs licence evidence |

**Formatting rules for proof**
- Write company names as Hubtel writes them: "Hubtel", "MTN MoMo", "Telecel Cash", "AT Money".
- Use "GHS" for cedi amounts. Write amounts as "GHS 51 billion".
- Counts from public pages are prefixed "about" or "over", never exact.
- Attribute CEO statements to the CEO. Attribute case-study results to Hubtel's own case study.
- No em dashes, no exclamation marks, no ellipsis characters [pb].

## Numbers to keep fuzzy (never quote as hard numbers)
- Team size: 722 [co], about 700 [co], LinkedIn 557 [co]. Say nothing.
- Annual revenue: CEO "over $110 million" [co]. Internal only.
- Merchants and users: use "about 8,000 businesses" only. Do not use "4M+ annual users" or "12 million customers", which mix consumers and merchants.
- Fee: 1.95% [co] vs 1%, 2.5% plus fixed, up to 3% [cp]. Quote no fee.
- Case-study figures not yet verified: 785% growth, GHS 23.65 billion Send Money, 80% of transactions, GHS 162B [cu].
- Funding: not discussed in copy. Source conflict [co].

## Authorized social-proof names
None authorised. Hubtel's three flagship customers are unnamed [cu]. These named customers exist in Hubtel case studies but are not approved for outbound:

| Name | What it would prove | Caveat |
|---|---|---|
| Akwantuo Express | Direct Debit API for student transport [cu] | Body not read; numbers unverified |
| Aura-Rich Consult and Technologies | Receive & Send Money API for school payments [cu] | No metrics found |
| Golden Crystal Experience | Hubtel POS [cu] | Details not retrieved |
| Rabito Clinic | Hubtel POS [cu] | Details not retrieved |

Everyone else, including logos on the Hubtel website (GhQR, Mastercard, Visa, GhIPSS, Affinity [co]) and partners (AWS, Visa, Payworks [cu]), stays out of copy until added here with approval. Do not name SportyBet or ECG: unconfirmed [cu].

## Proof caveats
- The three case studies are Hubtel-published and self-reported. They prove outcomes for one utility, one insurer and one gaming firm, not results for every segment [cu].
- The insurer case proves selling beyond office hours for an insurer. Do not imply the same lift for utilities or schools.
- The utility case describes collections at a very large distributor. Do not imply smaller utilities get the same scale.
- The CEO's 12% is a statement in a media interview, not an audited figure [vo].

## Banned
### Banned angles
- Price or fee-first framing, and any fee comparison [co][cp].
- Quoting any fee number until Hubtel approves one.
- Claiming funds are segregated, safe or compliant with BoG Notice 43. Hubtel's position is Not found [mk][sg].
- Fear framing about regulators, or naming Zeepay [mk].
- Naming unnamed case-study customers or guessing who they are [cu].
- Cross-border, pan-African or multi-country capability claims [co][cp].
- A government-payer angle. The CEO calls government clients paying upfront "an open debate" [cu].
- Mixing consumer app lines (food, stores, rides) into B2B copy [co].
- Diagnosing the prospect's team or process as failing [pb].
- Guarantees or promised percentage lifts for the prospect.

### Banned words and phrasing (company-specific)
The global list is `knowledge-base/playbooks/copy-bans.yaml`. Add for Hubtel:
- "cheapest", "lowest fee", "best price": Hubtel says it is not for those who want "the cheapest fee" [co].
- "unlock": Hubtel uses "Unlock Growth" in its own title, but the global ban applies. Say "grow" or "collect" [vo][pb].
- "number one", "Africa's most useful company" stated as fact: aspiration or opinion [vo].
- "pan-African" about Hubtel itself (it may describe a customer, only as the case study does) [co][cu].

### Never in copy, under any circumstance
- Hubtel's revenue, headcount or funding [co].
- The unverified metrics listed under "Numbers to keep fuzzy".
- Anything from a non-public source or from this file's INFERRED notes in `messaging.md`.

## Voice notes
- Register: plain, direct, benefit first, Ghana-rooted. Short declarative lines [vo].
- Brand word: "useful" ("Useful Everyday") [vo].
- Hedges about the prospect: "my guess is", "could be off". Never state their problem as fact [pb].
- House phrases proven in live copy: Not found. No live Hubtel outbound exists in the research.
- Subjects: lowercase, 8 words or fewer, no exclamation marks, no brackets [pb].

## CTA ladder
- **Primary:** Not found. Hubtel's own nav offers "Switch to Hubtel" and "Developer APIs" [co]. Decide the first ask with Hubtel sales.
- **Secondary:** Not found.
- Never: "book a call", "schedule 15 minutes", calendar links in email 1 [pb].

## Internal only (never in prospect copy)
- Hubtel revenue, headcount, funding and the BoG Notice 43 discussion [co][mk].
- Competitor fee numbers from comparison blogs [cp].
- Everything in this file marked Pending, Not found or INFERRED.
- Unverified case-study figures, and the signal matrix scores [cu].
