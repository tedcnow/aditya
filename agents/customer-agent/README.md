# TEDcNOW Customer Agent ("Triveni")

An AI client concierge that takes event briefs from couples, families, corporates and planners,
qualifies them, and hands them to a TEDcNOW relationship manager (RM), who matches them with verified
vendors across India.

| File | Purpose |
|---|---|
| `system-prompt.md` | The agent's instructions: persona, intake, guardrails, handoff |
| `knowledge-base.md` | The only facts the agent may use. Every **[CONFIRM]** item must be confirmed before launch |
| `lead-schema.json` | Lead fields for the CRM, including booked value and commission tracking |
| `conversation-flows.md` | 8 test scripts and go-live pass criteria |

## Execution plan

**Objective:** capture and qualify client leads 24×7 and get every qualified lead to an RM within the SLA.

| Phase | Actions | Owner | Timeline |
|---|---|---|---|
| 1. Confirm facts | Fill every [CONFIRM] in the knowledge base: active cities, verification steps, client fee, SLA, WhatsApp number | Aditya | Week 1 |
| 2. Pick the channel | WhatsApp Business (primary for Indian clients), website chat on tedcnow.com, voice (optional) | Aditya | Week 1 |
| 3. Build & connect | Load the prompt and knowledge base into the platform; send handoffs to a Google Sheet or CRM plus an RM WhatsApp group | Claude + Aditya | Week 1–2 |
| 4. Test | Run all 8 flows in `conversation-flows.md`; fix failures | Aditya + 1 RM | Week 2 |
| 5. Soft launch | Turn it on for Instagram / website traffic only; a human reviews every chat | RM | Weeks 3–4 |
| 6. Scale | Add campaigns, click-to-WhatsApp ads, planner referrals | Marketing | Month 2+ |

## KPIs

| KPI | Target to set after soft launch |
|---|---|
| Chats → complete brief | % |
| Complete brief → qualified (HOT/WARM) | % |
| Lead handoff → first RM contact | within the SLA |
| Qualified lead → booking | % |
| Booked value per lead (₹) | ₹ |
| Commission earned (₹), from booked value × agreed % | ₹ |
| Hallucination incidents (invented vendor, price or claim) | 0 |

## Revenue logic (worked example, not a forecast)

Commission = booked vendor value × commission % (5% per the current model, subject to each vendor agreement).
Example: one booking with ₹10,00,000 of vendor value through TEDcNOW → ₹50,000 commission.
Real conversion and ticket sizes will come from soft-launch data, so none are assumed here.

## Risks and mitigations

| Risk | Mitigation |
|---|---|
| The agent promises vendors or coverage TEDcNOW doesn't have | Hard rules in the prompt; the knowledge base lists only confirmed active cities |
| Leads go cold after handoff | RM SLA, a WhatsApp group alert, and a daily review of unassigned leads |
| Vendors bypass TEDcNOW after an introduction (commission leakage) | Commission terms in the vendor agreement; log every intro with lead_id and date |
| Data privacy (DPDP Act 2023) | Consent captured in chat; privacy policy on the website; deletion on request |
| WhatsApp policy / template rejection | Use the official WhatsApp Business API, opt-in, approved templates for outbound messages |
