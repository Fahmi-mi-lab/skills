# Deployment & Infrastructure Diagram

## What this covers
Shows how the containers/services from the C4 Container diagram are actually run physically/on the cloud: which machine/server, which region, how traffic enters, and how components connect at the network level.

## Standard elements
- **Node** — an infrastructure unit (server, container, VM, managed service), drawn as a 3D-style box or a labeled box indicating its node type.
- **Deployed artifact** — the software running inside a node (e.g. "API Service v1.2" running inside an "ECS Task" node).
- **Network boundary** — a large box wrapping several nodes, marking a VPC, subnet, or region/availability zone. Usually drawn with a dashed border and a label in the corner.
- **Load Balancer** — typically a dedicated icon, placed in front of a set of identical nodes (indicating horizontal scaling).
- **CDN** — drawn at the front (closest to the user) if the system serves static content.
- **Cloud provider icons** — if using provider-specific icons (AWS/GCP/Azure), use one official icon set consistently — don't mix icon styles from different providers in one diagram.

## Must-show details
- Region/availability zone boundaries (to indicate redundancy)
- Direction of incoming traffic (from the internet → load balancer → service)
- Which components are horizontally scaled (usually shown as several identical node instances, or one node with an "xN" notation)

## Representation in Penpot
Frame `06-Deployment-Infrastructure`. Network boundaries are drawn as large frames/groups with dashed borders; nodes inside use reusable components by type (compute, database, load balancer, etc.) from the library. Keep one consistent icon style/provider throughout the diagram.

## Polish checklist
- [ ] Region/VPC/AZ boundaries are clearly visible, not all nodes mixed together without boundaries
- [ ] Load balancers/scaling points are shown explicitly for components that scale
- [ ] Node icons/style are consistent, from one provider, not mixed
- [ ] Traffic direction from user into the system is clearly readable
