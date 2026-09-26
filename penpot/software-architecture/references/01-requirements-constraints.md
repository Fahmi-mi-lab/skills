# Requirements & Constraints

## What this covers
The foundation for every architectural decision that follows. If this stage is skipped or rushed, every later stage (tech stack, ERD, deployment) risks heading in the wrong direction.

## Functional Requirements (FR)
What the system MUST be able to do, from a user/business point of view.
- Format: "User can [action] in order to [goal]" — similar to a user story.
- Example: "User can upload an invoice and the system automatically extracts the amount and date."

## Non-Functional Requirements (NFR)
Qualities of the system, not features. Industry-standard categories — go through each one, don't skip any without thinking about it:
- **Performance** — latency/throughput targets (e.g. p95 < 200ms)
- **Scalability** — current vs projected user/request volume over the next year
- **Availability** — uptime target (e.g. 99.9%), downtime tolerance
- **Security** — auth requirements, data encryption, compliance needs (GDPR, PCI-DSS, etc. if relevant)
- **Maintainability** — team expectations (team size, who maintains this long-term)
- **Cost** — infra budget ceiling per month
- **Portability** — does it need to be multi-cloud or vendor-lock-in-free

## Constraints
Non-negotiable limits: mandated technology (company policy), available team (skillset), deadlines, budget, regulations.

## How to ask the user (don't invent)
If the user hasn't specified, ask at minimum: expected user scale, any existing tech stack/cloud preference, any specific compliance/regulatory requirements, timeline and team size. If the user genuinely doesn't know yet, record it as an explicit assumption — don't silently assume it.

## Representation in Penpot
Frame `01-Requirements-Constraints`, as two side-by-side tables (FR | NFR) plus a small list for Constraints. No need for a free-form diagram here — table clarity matters more than visual complexity.

## Polish checklist
- [ ] Every FR is written from the user's point of view, not the system's
- [ ] All NFR categories above have been considered (can be "N/A" if truly irrelevant, but must be stated explicitly)
- [ ] Assumptions made because the user didn't answer are clearly flagged as assumptions
