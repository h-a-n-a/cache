# Documentation consistency

- Keep a single source of truth for each rule or design contract. Define it
  once and reference it elsewhere, both within a document and across documents.
- Before writing a statement, including one supplied by the user, check it
  against the relevant goals, principles, milestones, and design docs.
- If it conflicts, alert the user before writing it. Cite the conflicting
  passages and propose a correction. Resolve the conflict with the user;
  do not silently choose a version or leave contradictory guidance.
- After agreement, update all affected docs and references together.
- Follow the status definitions in README.md. A proposal may explicitly replace
  an accepted design; do not present both as accepted.

# Keeping designs current

- Base designs on current code, agreed goals, and milestone scope. Distinguish
  implemented behavior, planned changes, and open questions.
- Explain changes to accepted designs, including those needed during
  implementation, and why they are needed.
- Update existing docs across milestones. Create a new doc only for a distinct
  feature or decision.
- Merge or delete docs that have been replaced, preserving useful content and
  updating links. Keep one consistent design; Git history preserves old designs.
