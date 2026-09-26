# High-Level Architecture — C4 Model

## What C4 Model is
An industry-standard way of describing software architecture at multiple levels of abstraction, from most abstract to most detailed, so different audiences (non-technical stakeholders vs engineers) can read the level that fits them.

Levels (build at least Level 1 & 2; Level 3 optional depending on complexity; Level 4/Code is rarely drawn manually):
1. **Context** — the system as a single box, surrounded by users/personas and external systems it interacts with. The most zoomed-out level.
2. **Container** — break the system into independently deployable units: web app, mobile app, API service, database, message queue. This is the level most commonly used for architecture discussions.
3. **Component** — break one container into internal modules/components (e.g. inside an API service there's an Auth Module, a Payment Module). Build this if the container is complex enough to warrant it.
4. **Code** — class diagrams, usually generated from code rather than drawn manually.

## Standard notation
- **Person** — drawn as a person/stick-figure icon, representing a human user/actor.
- **Software System (in scope)** — a solid box with a primary color.
- **External System** — a box with a dashed border or a different (usually grey) color, marking it as outside the team's control.
- **Container** (at level 2) — a box labeled with its technology, e.g. "API Service [Node.js]".
- **Database** — usually a cylinder icon, not a plain box, so it's instantly recognizable.
- **Relationship/arrow** — a one-directional arrow with a short label explaining what flows (e.g. "sends HTTP request", "reads/writes data"), never a bare unlabeled arrow.

## Color convention (fill in per project tokens; common pattern shown below)
- Person → neutral color (grey/black outline)
- The system being designed → primary/brand color
- External/third-party system → secondary/muted color
- Database/storage → a color distinct from regular containers (e.g. an accent color), so it stands out at a glance

## Layout
Context diagram: person/user on the left or top, the system in the center, external systems on the right/bottom. Container diagram: flow left→right or top→bottom, consistent with the direction chosen for the whole document.

## Representation in Penpot
Two separate frames: `02a-Context-Diagram` and `02b-Container-Diagram` (add `02c-Component-Diagram` if needed). Use library components for the person icon, database cylinder, and container box — don't redraw them each time.

## Polish checklist
- [ ] Every arrow has a label describing the interaction, not just a line
- [ ] External systems are visually distinct from core systems (different color/border)
- [ ] Databases use a cylinder shape, not a plain box
- [ ] Flow direction is consistent across every diagram in the document
