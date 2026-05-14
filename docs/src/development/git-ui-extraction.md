---
title: Extracting the Git UI
description: "How to extract Zed's Git UI into an independent app."
---

# Extracting the Git UI

Zed's Git workflow UI is centered in the `git_ui` crate and is similar in scope to a GitHub Desktop-style experience (commit, stage/unstage, diff review, fetch/pull/push, branch/stash flows).

## Primary module to extract first

- `/home/runner/work/zed/zed/crates/git_ui`

## Key files for commit and review workflows

- `/home/runner/work/zed/zed/crates/git_ui/src/git_panel.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/project_diff.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/file_diff_view.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/text_diff_view.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/multi_diff_view.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/commit_view.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/commit_modal.rs`
- `/home/runner/work/zed/zed/crates/git_ui/src/git_ui.rs`

## Backend layers it depends on

- `/home/runner/work/zed/zed/crates/git/src/git.rs`
- `/home/runner/work/zed/zed/crates/project/src/git_store.rs`

## Practical extraction sequence

1. Create a new Rust + GPUI app as the host shell.
2. Bring in `git_ui` first, then only the minimum dependencies it needs (`git`, selected `project`, `workspace`, `editor`, and `ui` integrations).
3. Replace `Workspace`/`Project`-specific integration points with your app services and data models.
4. Keep the existing diff and commit UI components, and rewire actions (`stage`, `unstage`, `commit`, `fetch`, `pull`, `push`) to your own service layer.

## Integration points to rewire early

From `git_ui` initialization and registration:

- `/home/runner/work/zed/zed/crates/git_ui/src/git_ui.rs`

From panel behavior and action handlers:

- `/home/runner/work/zed/zed/crates/git_ui/src/git_panel.rs`

In app startup where `git_ui::init(cx)` is called:

- `/home/runner/work/zed/zed/crates/zed/src/main.rs`
- `/home/runner/work/zed/zed/crates/zed/src/zed.rs`

## Expected effort and risk

This extraction is feasible, but not plug-and-play. The main complexity is coupling to Zed-specific `workspace`, `project`, and editor action wiring.
