# Data Model / ERD (Entity Relationship Diagram)

## What this covers
The structure of the system's core data: what entities exist, what attributes each entity has, and how entities relate to each other.

## ERD components
- **Entity** — a core object/concept (e.g. User, Order, Product). Drawn as a box with the entity name as the header and a list of attributes below it.
- **Attribute** — a property of an entity (e.g. User has id, email, created_at). Explicitly mark **Primary Key (PK)** and **Foreign Key (FK)** in the attribute list.
- **Relationship & cardinality** — how entities connect, shown with a connecting line and crow's foot notation for cardinality:
  - One-to-One (1:1)
  - One-to-Many (1:N) — most common, e.g. one User has many Orders
  - Many-to-Many (N:N) — usually needs a junction table, e.g. Order ↔ Product via OrderItem

## Key standards to keep in mind
- Normalize to at least 3NF for transactional data (avoid unnecessary duplication), unless there's a deliberate reason to denormalize for performance (which should then be documented in the related ADR).
- Keep table/entity naming consistent (singular or plural — pick one convention and stick with it, don't mix).
- Mark nullable vs not-null columns when it matters for understanding business constraints.

## Representation in Penpot
Frame `04-Data-Model-ERD`. Use one reusable "entity box" component from the library (header + attribute list), laid out with consistent grid spacing. Relationship lines use the same connector style throughout, with crow's foot notation at the line ends to indicate cardinality. PK/FK are marked with a distinct text style (e.g. bold/different color) from regular attributes.

## Polish checklist
- [ ] All PKs and FKs are clearly marked visually (not plain text identical to other attributes)
- [ ] Every relationship's cardinality is drawn with correct notation, not a meaningless plain line
- [ ] Junction tables for N:N relationships are shown as their own entity, not hidden
- [ ] Entity naming is consistent (singular/plural not mixed)
