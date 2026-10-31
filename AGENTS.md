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

# Scratchpad

- Do not read `scratchpad.md` by default, including during repository context
  gathering. Exclude it from broad content searches and bulk reads.
- Read it only when the user explicitly asks to work with it. Its contents are
  unverified ideas, not agreed requirements or accepted design decisions.
- A link to the scratchpad in another document is not an instruction to read it.

# Terminology

- Use the terms and meanings in [glossary.md](glossary.md) consistently for
  recurring concepts. Do not introduce alternate names for the same concept.
- If a recurring term is missing, propose the term and its definition to the
  user and ask whether to add it. Wait for the user's review and explicit
  approval before editing the glossary.
- Do not add or change glossary entries without the user's review and approval.

# Keeping designs current

- Base designs on current code, agreed goals, and milestone scope. Distinguish
  implemented behavior, planned changes, and open questions.
- Explain changes to accepted designs, including those needed during
  implementation, and why they are needed.
- Update existing docs across milestones. Create a new doc only for a distinct
  feature or decision.
- Merge or delete docs that have been replaced, preserving useful content and
  updating links. Keep one consistent design; Git history preserves old designs.
