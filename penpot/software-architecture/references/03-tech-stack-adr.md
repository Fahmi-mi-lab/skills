# Tech Stack & Architecture Decision Record (ADR)

## Why ADRs matter
A technology choice made without a written reason gets questioned again and again later ("why did we pick X back then?"). An ADR documents a significant decision along with its context and trade-offs, once.

## Standard ADR format (one per major decision)
One ADR per significant decision (not for minor things). Write separate ADRs for decisions like: database choice, architecture style (monolith vs microservices), cloud provider, message broker, and similar.

Structure:
- **Title** — short decision name, e.g. "ADR-003: Choosing PostgreSQL as the primary database"
- **Status** — Proposed / Accepted / Deprecated / Superseded
- **Context** — what problem or constraint is driving this decision
- **Decision** — what was decided
- **Alternatives considered** — other options that were weighed and why they weren't chosen
- **Consequences** — positive and negative consequences of this decision (trade-offs must be stated honestly, not just the upsides)

## Tech stack table by layer
Organize by layer — don't just list technology names without reasons:

| Layer | Choice | Short reason |
|-------|--------|----------------|
| Frontend | ... | ... |
| Backend/API | ... | ... |
| Database | ... | ... |
| Caching | ... | ... |
| Message Queue | ... | ... |
| Infra/Hosting | ... | ... |
| CI/CD | ... | ... |
| Monitoring | ... | ... |

Every reason should trace back to a requirement/constraint from stage 1 (e.g. "chosen for strong consistency needed in financial transactions", not "because it's popular").

## Representation in Penpot
Frame `03-Tech-Stack-ADR`: the stack table at the top, an ADR summary (one card per decision) below or in a separate frame if there are many ADRs. A stack diagram (technology icons arranged by layer) can complement the table as a visual aid, not replace it.

## Polish checklist
- [ ] Every tech stack row has a reason tracing back to a requirement, not a generic opinion
- [ ] Every ADR lists at least one rejected alternative with a reason
- [ ] Trade-offs/consequences are stated honestly (not only the upsides)
