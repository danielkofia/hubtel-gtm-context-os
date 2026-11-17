# Hubtel ICP

Built only from `context/docs/research/`. Tags: [co] company.md, [cu] customers.md, [cp] competitors.md, [mk] market.md, [sg] signals.md, [vo] voice.md. INFERRED = my reading, not stated in the research. Evidence grades: A = Hubtel-published customer proof, B = Hubtel or credible third-party statement, C = inference only. Nothing here is a validated conversion pattern. The research has no win/loss, pipeline or customer-size data [cu].

## Who we mean
Hubtel is the seller. The buyer is a Ghana-based organisation that collects money from many payers, or pays out to many recipients, and does it through manual, office-hours or leaky processes today. That is the pattern in all three flagship case studies [cu]. Hubtel also serves micro-merchants [cu], but they are not the outbound target (see Not a fit).

## Segments to test first
Ranked by strength of proof. Case-study customers are anonymous, so each row is a hypothesis about lookalikes, not a proven conversion pattern.

| # | Segment | Pain Hubtel has publicly solved | Proof | Grade | Where to find them (INFERRED) |
|---|---|---|---|---|---|
| 1 | Utilities and power distributors | Collected "less than 22% of its revenue potential"; now "GHS 51 billion through a single platform" | Power distributor case, 2026-06-24 [cu] | A | Other utilities and distribution firms in Ghana |
| 2 | Insurers | "office-hours selling" to "84% more policies per agent" | Insurance case, 2026-06-26 [cu] | A | Insurers with agent sales forces |
| 3 | Betting and gaming operators | "built its entire Ghana payment operation on Hubtel", GHS 162B flow; USSD deposits for users without smartphones | Gaming case, 2026-06-25 [cu] | A | Pan-African operators entering or running in Ghana |
| 4 | Transport and school-fee collectors | Akwantuo Express: Direct Debit API, per search summary 80% of transactions through Hubtel, revenue leakage cut to zero; Aura-Rich Consult: school payments | Named case studies [cu] | B (bodies not read) | Student transport, schools, education operators |
| 5 | In-person merchants on POS | Golden Crystal Experience, Rabito Clinic POS cases | Named cases, details not retrieved [cu] | B | Clinics, hospitality, events |

## Layers
### 1. Firmographic
| Attribute | Rule | Evidence |
|---|---|---|
| Country | Must be Ghana. Hubtel markets 8+ Ghanaian cities only | [co] |
| Industry | The five segments above. Banks, telecoms, retailers are named by Hubtel but have no case proof in the research | [co][cu] |
| Size | Not found. Hubtel says "scale-ready" without a number [co]. Needed before list building. Proxy to test: organisations with high-volume repeat payers (policies, bills, tickets, fees) | Gap |

### 2. Technographic
Generic "uses mobile money" is not a filter in Ghana, so it is not a criterion here.
| Criterion | Why it separates fits from non-fits | Evidence | Grade |
|---|---|---|---|
| Runs high-volume repeat collections or payouts that touch finance or reconciliation | Every Hubtel case is about volume and leakage, not one-off checkout | [cu] | A |
| Needs API or USSD rather than a payment link | APIs used: Direct Debit, Receive & Send Money, Send Money, SMS and Notification; USSD for non-smartphone users | [cu] | A |
| Current provider is a bank rail or manual process | Power and insurer cases start from manual collection. Competing PSP use: Not found | [cu][cp] | B |
| Needs bill-pay reach across channels | Hubtel lists MTN MoMo, Telecel Cash, AT Money, bank, card, POS. ExpressPay competes directly on utility bill pay [co][cp] | [co][cp] | B |

### 3. Intent signals
Honest read: none of these is a prospect-level trigger yet. All are market-level, and prospect-level triggers (hiring, funding, new leaders, expansion at a named prospect) are Not found [sg].
| Signal | How we would detect it (INFERRED) | Direction | Grade |
|---|---|---|---|
| Public mention of manual collection, queues, office-hours service, or missing revenue | Company news, annual reports, service pages | Strong. Same pain as the three cases | A |
| Prospect uses a PSP hit by regulation, e.g. Zeepay (licence revoked July 2026, four months old) [mk] | Customer lists, merchant pages | Medium, decaying | B |
| BoG Notice 43 (2026-11-06) on merchant funds [mk] | Ask in discovery where the buyer's PSP holds funds | Two-sided. It may push buyers to scrutinise PSPs, including Hubtel. No deadline found | C |
| E-VAT expansion to medium enterprises, 2026-11-01 (reported, unconfirmed) [mk] | Company size and VAT status | Weak until confirmed | C |
| Cross-border digital VAT withheld by payment providers [mk] | n/a | Rarely relevant to Hubtel's ICP. Dropped from targeting | C |

### 4. Persona
Titles are not in the research. See `personas.md`; its titles are open questions.

### 5. Engagement readiness
What the research actually supports is thin.
| Factor | Evidence | Grade |
|---|---|---|
| Hubtel has a published offer for switching and an API path | "Switch to Hubtel", "Developer APIs" in nav [co] | B |
| Existing merchants have Relationship Managers | Terms update [co] | B |
| Proof is anonymous | Case studies name no customer [cu]. Expect a "who is this?" objection | B |
| Sales cycle, procurement path, pilot terms, pricing for large accounts | Not found. Hubtel's 1.95% fee and third-party figures of 1% to 3% conflict [co][cp] | Gap |

## Qualify in, then score
- Must have: Ghana; recurring high-volume collections or payouts; a manual, limited-hours or leaky current process.
- Boosters (each adds fit): API or USSD need; sits in segments 1 to 3; public pain statement; uses a provider under regulatory pressure.
- Disqualifiers: see below.

## Not a fit, and why
| Who | Why | Evidence |
|---|---|---|
| Businesses outside Ghana or needing multi-country collection | Hubtel markets only Ghana; Flutterwave is the stronger multi-country option. Lack of cross-border capability is from one unverified source | [co][cp] |
| Buyers who choose on lowest fee | Homepage says Hubtel is not for those wanting "the cheapest fee" (exact wording needs a manual check) | [co] |
| Micro and informal merchants | Hubtel serves them [cu], but INFERRED low value for outbound, since no sales motion or economics for them are in the research | [cu] |
| Businesses in activity Hubtel's terms restrict | Terms allow blocking settlement or terminating "without liability to Hubtel". The Restrictions list itself: Not found | [co][sg] |
| Foreign-currency crypto wallet activity | BoG told PSPs to stop supporting it without authorisation | [mk] |

## Open questions (in order of impact on pipeline)
1. What size is "scale-ready"? Customer headcount, revenue or monthly volume. Not found [cu].
2. Who are the three anonymous case-study customers, and can Hubtel name them? [cu]
3. Which segment closes fastest and at what contract value? No win/loss data.
4. What do real quotes and reviews say? Customer quotes and Trustpilot: Not found [cu].
5. What is the real fee, and how does it vary by channel? [co][cp]
6. Does Notice 43 help or hurt Hubtel's pitch, and is there a deadline? [mk]
7. Which PSP do each segment's prospects use today? [cp]
