# Hubtel GTM Context OS

## Company
Hubtel is a Ghana-based payments and digital commerce company, founded 2005 as SMSGH, serving about 8,000 businesses with 722 staff (self-reported; sources in `context/docs/research/company.md`).

## How this folder works
- `context/icp/`: `icp.md` (five-layer ICP and non-fits) and `personas.md` (champion, economic buyer, influencer). Read before targeting, list building or personalizing.
- `context/positioning/`: positioning, value props, competitive angles. Read before writing any pitch or campaign.
- `context/messaging/`: approved messaging, tone and proof points. Read before drafting any copy.
- `context/brand-kit/`: logos, colors, fonts, voice rules. Read before producing anything visual or branded.
- `context/docs/research/`: raw company and market research with sources. Read when you need a fact, then cite it.
- `knowledge-base/playbooks/`: repeatable how-to processes. Read before running a recurring task.
- `knowledge-base/learnings/`: what worked and what did not. Read before planning or repeating a campaign.
- `meetings/`: notes and transcripts from calls. Read when you need decisions or customer language.
- `output/campaigns/`: finished and in-progress campaign assets. Read to reuse or avoid duplicating work.
- `output/outbound/`: cold email, LinkedIn DMs and call scripts. Read before writing or reusing outbound copy.
- `output/socials/`: social posts and calendars. Read before drafting or scheduling posts.
- `output/paid-ads/`: ad copy, creative briefs and targeting. Read before building or revising paid campaigns.
- `tools/`: scripts and integrations. Read before building anything new, to see what exists.
- `weekly-priorities/`: one file per ISO week (YYYY-Www.md). Read first every session.
- `work-log/`: one file per ISO week, same name as the priorities file. Read to see recent changes, and write to it after every change.
- `.claude/skills/`: reusable skills for this workspace. Read when a task matches a skill.

## Rules
- Cite a source for every company fact.
- Never invent numbers. If a figure is unknown, say so.
- No em dashes in any copy.
- Ask before sending or publishing anything.
- Log every change in this week's work log.

## Tools
GTM stack: Clay (enrichment and list building), HubSpot (CRM), n8n (automation).
Helpers in `tools/`: `rex/` (drive Clay from Claude, unofficial), `agent-browser/` (browser automation), `crawl4ai/` (site crawling to Markdown). Read each README before use.

## Skills (`.claude/skills/`)
- `signal-matrix`: build ICP and signal matrices. `campaign-strategy`: generate campaign ideas.
- `build-workflow-spec`: turn a play into a workflow spec. `campaign-copy`: write cold email and LinkedIn copy from an approved spec.
- `campaign-contract`: write the Clay build sheet. `campaign-qa`: QA a table or campaign against its spec.
- `clay-build-plan`: step-by-step Clay build guide. `build-clay`: build or repair a Clay outbound workbook.
- `design-clay-table-json`: write Clay table JSON. `import-clay-table`: import it into Clay. `save-clay-schema`: save a table to the registry. `export-tables`: export Clay tables to CSV.
- `prompt-builder`: build per-row AI prompts. `calculate-costs` and `workspace-cost-audit`: report Clay and AI spend.
- `inbox-placement-test`: test cold email inbox placement. `miro-gtm-flowchart`: draw GTM flows in Miro.
- `agent-browser`: automate browsers. `crawl4ai`: crawl sites into Markdown.
