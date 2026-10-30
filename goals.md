# Goals

The end result of caching in Rolldown. Each milestone in
[milestones.md](milestones.md) moves toward one or more of these goals.

## Goals

1. **Reduce repeated computation.** Reuse valid computation results whenever
   their inputs match, including results from JavaScript plugins, so cache hits
   avoid repeated work on both the Rust and JavaScript sides.
   Check: verify reuse for matching inputs, including between build and dev,
   and confirm that cache hits skip the corresponding JavaScript plugin
   computations. Verify recomputation when relevant inputs change and no valid
   result is cached.

2. **Preserve reuse across runs and working directories.** Support reuse across
   process restarts, worktrees, project moves, and machines on the same platform.
   Check: verify reuse in each scenario, including CI cache upload and download.
   Moving a project must not invalidate the entire cache; work affected by the
   path change may run again.

3. **Keep results correct automatically.** Handle input changes without requiring
   users to clear the cache.
   Check: compare cached and clean builds after edits, branch changes, worktree
   changes, and changes made while Rolldown was stopped; verify matching output
   and required behavior without manual cache cleanup.

4. **Recover from unusable caches.** Missing, damaged, or incompatible caches may
   slow down a build, but must not cause a panic or prevent an otherwise valid build.
   Check: remove, corrupt, or provide incompatible cache data; verify that the
   build completes with correct results by recomputing the required work.

## Non-goals

- **Cross-platform cache reuse.** Reuse is limited to the same platform.
- **Cross-project cache reuse.** Reuse is limited to the same project.
