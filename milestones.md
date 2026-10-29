# Milestones

Each feature links to its design doc and to the rolldown PRs that implement it.
Mark a feature `(in progress)` while work is open, and check it when all its
PRs have merged.

## M1: Persistent and shared scan cache

**Goal:** Preserve Rolldown's existing scan-stage incremental capability while
making its cache persistent and reusable across worktrees of the same project.

**Done when:**

- Restarting Rolldown reuses valid cached scan results to reduce repeated work
  and build time.
- Building in another worktree of the same project reuses valid cached scan
  results without invalidating the entire cache because the root path differs.
- After a local source change, rebuilding updates only the affected cache data
  without rewriting the entire disk cache.
- Multiple worktrees of the same project can build in parallel with correct
  results. Cache data is saved correctly in each worktree's project-local cache
  directory and the shared project-global cache directory.
- Damaged cache data, interrupted writes, and incompatible cache versions do not
  cause incorrect results, panics, or cache-related build failures.
- Representative rebuild and restart scenarios complete faster with persistent
  caching than without it, including cache validation, restoration, and write costs.

**Deliverables:**

- [ ] **Persistent cache storage and incremental writes.** Define and implement
  the project-global and project-local directory layouts, stored data, and
  incremental write model. Cover parallel worktree builds, interrupted writes,
  damaged data, and cache version compatibility.
- [ ] **Working-directory-agnostic serialization and deserialization.** Save and
  restore scan cache data across different working directories. Handle
  path-dependent data and restore the state needed to continue incremental
  builds, including side-effect records that must survive process restarts.
  Select which scan data to persist based on correctness and overall performance
  benefit; persisting the full scan state or AST is not required.
- [ ] **Scan dependency tracking, invalidation, and side effects.** Define the
  inputs that affect scan results and track them to validate cached results after
  restarts and across worktrees, including changes made while Rolldown was
  stopped. Define how required side effects are tracked and handled when cached
  computations are reused or invalidated. Preserve the existing scan-stage
  incremental scope without adding incremental computation in other stages.

## Template

```markdown
## M<N>: Milestone name

**Goal:** what users get when this milestone ships.

**Done when:**

- An observable behavior that shows the milestone meets its goal.

**Deliverables:**

- [ ] Feature name. Design: [0001](design-docs/0001-feature-name.md). PRs: rolldown/rolldown#0000
```
