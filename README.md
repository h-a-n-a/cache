# Cache

Design and planning for caching in [Rolldown](https://github.com/rolldown/rolldown):
a persistent cache on disk, a cache shared across git worktrees, and incremental
builds that redo only the work whose cache key changed. The code itself lands in
Rolldown.

## Layout

| Path                             | What it holds                                                                     |
| -------------------------------- | --------------------------------------------------------------------------------- |
| [`goals.md`](goals.md)           | The end result of caching in Rolldown, and what is out of scope. Read this first. |
| [`principles.md`](principles.md) | Rules that every design follows.                                                  |
| [`design-docs/`](design-docs/)   | One record per feature or decision: what and why.                                 |
| [`milestones.md`](milestones.md) | The order of work, the features in each milestone, and their status.              |

## Adding a design doc

1. Copy [`design-docs/0000-template.md`](design-docs/0000-template.md) to
   `design-docs/NNNN-short-name.md`, using the next free number.
2. Add the feature to its milestone in [`milestones.md`](milestones.md) and
   link the new doc.
