# Glossary

Terms used in cache discussions and designs. These definitions do not decide
storage layout, record placement, or user-facing options.

| Term | Meaning |
| --- | --- |
| **Worktree** | An independent working directory of a project, with its own source files and configuration. No worktree is the baseline for another. |
| **Local cache** | Project-local cache storage associated with one worktree. Use **local** as the short name. |
| **Global cache** | Project-global cache storage available to worktrees of the same project. Use **global**, not **shared**, as the short name. It does not mean a cache across unrelated projects. |

Reuse limits are defined in [goals.md](goals.md). Open questions about local
and global storage are recorded in [scratchpad.md](scratchpad.md).
