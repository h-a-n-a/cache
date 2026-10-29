# Milestones

Each feature links to its design doc and to the rolldown PRs that implement it.
Mark a feature `(in progress)` while work is open, and check it when all its
PRs have merged.

M1 and M2 can be developed in parallel with shared design work. Complete M1's
performance evaluation early so its findings can guide M2. M2's acceptance
requires the persistence and restoration capability delivered by M1.

## M1: Persistent scan cache

**Goal:** Make Rolldown's existing scan cache reusable after restarting in the
same worktree, while preserving its module-level incremental behavior. This
milestone does not introduce independently cached resolve, load, or transform
steps, or incremental computation in later build stages.

**Done when:**

- Restarting Rolldown in the same worktree reuses valid cached scan results.
- Changes made while Rolldown was stopped are handled correctly without manual
  cache cleanup.
- After a local source change, rebuilding updates only the affected cache data
  without rewriting the entire disk cache.
- Damaged cache data, interrupted writes, and incompatible cache versions do not
  cause incorrect results, panics, or cache-related build failures.
- Representative restart scenarios complete faster with persistent caching than
  without it. Comparisons use the same inputs and a new process in both cases,
  including validation, reading, deserialization, required recomputation, and
  write costs. Rebuild measurements also account for cache maintenance costs.

**Deliverables:**

- [ ] **Persistent cache storage and incremental writes.** Define and implement
  the cache layout, stored data, and incremental write model for the original
  worktree. Cover interrupted writes, damaged data, and version compatibility.
  Coordinate the storage design with M2's sharing requirements.
- [ ] **Serialization and deserialization.** Save and restore the scan data and
  side-effect records needed to continue incremental builds. Select what to
  persist based on correctness and measured overall performance; persisting the
  full scan state or AST is not required.
- [ ] **Scan dependency tracking, invalidation, and side effects.** Define and
  track the inputs needed to validate cached results after restarts, including
  changes made while Rolldown was stopped. Handle required side effects when
  cached computations are reused or invalidated, within the existing scan-stage
  incremental scope.

## M2: Shared scan cache

**Goal:** Reuse valid scan results across working directories, worktrees, and
machines on the same platform for the same project, building on M1's persistent
cache.

**Done when:**

- Moving a project or building in another worktree reuses valid scan results
  without invalidating the entire cache because the root path differs.
- Multiple worktrees of the same project can build in parallel with correct
  results. Cache data is saved correctly in each worktree's project-local cache
  directory and the shared project-global cache directory.
- A project's cache can be uploaded and restored on another machine on the same
  platform, including in CI, and valid entries are reused.
- Representative shared-cache scenarios reduce build time compared with builds
  without a reusable cache, including validation, restoration, and write costs.
- Shared cache use preserves M1's incremental write and safety guarantees.

**Deliverables:**

- [ ] **Project-local and project-global storage.** Define and implement what is
  stored in each directory and how concurrent worktree builds safely share and
  update cache data.
- [ ] **Working-directory-agnostic restoration and validation.** Handle
  path-dependent data and input differences across worktrees and project moves,
  preserving reuse where results remain valid.
- [ ] **Same-platform cache transfer.** Support saving and restoring the project's
  cache across compatible machines, including through external CI cache tools.
  Use M1's measurements to guide storage and restoration choices.

## M3: Incremental reuse in link and generate

**Goal:** Reduce rebuild time by reusing unaffected work in the link and generate
stages, with persistent and shared caching as in M1 and M2. Use their
implementation and performance measurements to select the scope; full incremental execution of both
stages is not required.

**Done when:**

- Selected representative rebuild scenarios complete faster than M2, including
  the cost of validating and maintaining the new caches.
- Builds using the new reuse paths produce the same output and required behavior
  as builds without caching, including after changes that affect multiple modules.
- Changes outside the supported reuse scope still produce correct builds by
  running the required computations.
- New cache entries support the same persistence and sharing capabilities as
  M1 and M2: reuse after restarts and across working directories and worktrees,
  incremental writes, safe parallel worktree builds, and safe handling of damaged
  data, interrupted writes, and incompatible versions.

**Deliverables:**

- [ ] **Baseline and research.** Measure link and generate costs after M1 and M2 and
  investigate approaches to incremental reuse. Identify repeated work and the
  opportunities most likely to improve overall rebuild performance.
- [ ] **Reuse boundaries and validation.** Design candidate computation and cache
  boundaries, including dependencies, invalidation, and required side effects.
  Use targeted experiments to select a scope with demonstrated benefits before
  committing to production implementation.
- [ ] **Incremental implementation and verification.** Implement the selected
  reuse paths with the persistence, incremental write, sharing, and safety
  capabilities from M1 and M2. Verify correctness and overall performance against
  M2, including
  cache restoration and write costs.
  Document supported scenarios and limits. Further subdivision of scan caching
  remains a separate candidate rather than a required part of this milestone.

## Template

```markdown
## M<N>: Milestone name

**Goal:** what users get when this milestone ships.

**Done when:**

- An observable behavior that shows the milestone meets its goal.

**Deliverables:**

- [ ] Feature name. Design: [0001](design-docs/0001-feature-name.md). PRs: rolldown/rolldown#0000
```
