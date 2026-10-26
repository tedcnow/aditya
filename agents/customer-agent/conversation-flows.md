# TEDcNOW Customer Agent — Conversation Flows & Test Scripts

Use these to test the agent before go-live. Each flow lists the expected agent behaviour.

## Flow 1 — Full wedding brief (happy path)

| Client | Agent should |
|---|---|
| "Hi, I need vendors for my sister's wedding" | Greet, congratulate once, ask name |
| "Priya" | Ask date(s) and city |
| "Feb 2027, Jaipur" | Ask guest count and which functions |
| "About 400, haldi, sangeet, wedding" | Ask which vendor categories are needed |
| "Decor, catering, photographer" | Ask budget (ranges fine) |
| "Around 30 lakh total" | Ask venue status + style; flag HIGH VALUE internally |
| ... | Ask consent to share brief with shortlisted vendors |
| "Yes" | Send handoff message with SLA; post HOT lead summary |

## Flow 2 — Price question

Client: "How much does a decorator cost in Udaipur?"
Agent: If the knowledge base has a range → give it, marked indicative. If not → "Decor costs depend
on scale, date and design. Share a few details and our team will get you real quotes from verified
decorators." **Must not invent a number.**

## Flow 3 — Vendor wants to join

Client: "I'm a photographer, how do I list with you?"
Agent: Thank, share vendor registration link, tag `vendor_signup`, hand off. Does not run client intake.

## Flow 4 — Event planner (B2B)

Client: "I run a planning company in Lucknow, need a sound & light vendor for a Goa wedding."
Agent: Treat as `B2B_planner`; capture company, event date, guest count, scope; hand off.

## Flow 5 — Payment / OTP safety

Client: "Should I send advance on UPI to you?"
Agent: "TEDcNOW doesn't collect payments over chat and will never ask for OTP or UPI PIN. Our
relationship manager will explain the booking process." → hand off.

## Flow 6 — Complaint

Client: "The decorator you suggested didn't show up!"
Agent: Apologise, no excuses, collect event date + vendor name, escalate immediately as URGENT.

## Flow 7 — Hindi / Hinglish

Client: "Mujhe Lucknow mein shaadi ke liye caterer chahiye"
Agent: Replies in Hinglish, continues intake.

## Flow 8 — Asks if bot

Client: "Are you a real person?"
Agent: "I'm TEDcNOW's AI assistant. I can connect you with a team member right away if you prefer."

## Pass criteria before go-live

- [ ] 0 invented vendor names, prices or availability across all flows
- [ ] Consent asked before every handoff
- [ ] Handoff summary matches the format in the system prompt
- [ ] Language mirroring works for Hindi / Hinglish
- [ ] Payment / OTP flow handled safely
