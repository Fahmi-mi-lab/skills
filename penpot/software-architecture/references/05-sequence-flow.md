# Sequence / Flow Diagram for Critical Processes

## When to use which
- **Sequence diagram (UML)** — for showing interactions between components/services over time (who calls whom, in what order). Good for flows like "OAuth login flow", "payment flow".
- **Flowchart** — for showing business logic/decision flow (not inter-service interaction). Good for "invoice approval flow", "input validation flow".

Pick at most 2-3 of the most critical/complex processes to diagram — not every process needs one; focus on the ones that carry the most risk or get asked about most often.

## Sequence diagram notation
- **Participant/Actor** — a box at the top, representing a user, service, or external system.
- **Lifeline** — a vertical dashed line descending from each participant.
- **Message (sync)** — a solid arrow with a filled arrowhead, from caller to callee.
- **Message (async)** — an arrow with an open arrowhead/plain line, indicating no immediate wait for a response.
- **Return/response** — a dashed arrow back to the caller.
- **Activation bar** — a thin vertical box on the lifeline, marking when a participant is actively processing.
- Time flows from top to bottom.

## Flowchart notation
- **Oval** — start/end
- **Rectangle** — process/action
- **Diamond** — decision point, with Yes/No (or specific condition) labels on each outgoing branch
- **Arrow** — flow direction

## Representation in Penpot
One frame per critical process, named `05-Flow-[Process-Name]` (e.g. `05-Flow-OAuth-Login`). Use reusable components for lifelines, activation bars, and decision shapes — don't redraw them for every new process.

## Polish checklist
- [ ] Message order reads clearly top-to-bottom without ambiguity
- [ ] Sync vs async messages use visually distinct arrow styles
- [ ] Every decision point in a flowchart has a label on each branch (Yes/No, or a specific condition)
- [ ] Only genuinely critical processes are diagrammed (not every process needs one)
