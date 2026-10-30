# Documentation consistency

- Before writing any statement into a document, compare it with the relevant
  goals, principles, milestones, and design docs. This includes statements
  supplied by the user.
- If a statement conflicts with existing documentation, tell the user before
  writing it. Point to the conflicting passages, explain the difference, and
  propose the changes needed to resolve it. Do not silently choose one version
  or leave both as current guidance. Resolve the conflict with the user first.
- Once the decision is clear, update all affected documents and references
  together. Do not leave contradictory statements in separate documents.
- Follow the design status definitions in README.md. A proposal
  may explicitly replace an accepted design; do not present both as accepted.

# Keeping designs current

- Base designs on current code, agreed goals, and milestone scope. Distinguish
  implemented behavior, planned changes, and open questions.
- When changing an accepted design, explain what changes and why. Update all
  affected docs together, including changes discovered during implementation.
- Update existing docs across milestones. Create a new doc only for a distinct
  feature or decision; reference shared contracts instead of copying them.
- Merge or delete docs that have been replaced, preserving useful content and
  updating links. Keep one consistent design; Git history preserves old designs.
