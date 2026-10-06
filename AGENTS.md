# Public-source boundary

This repository contains reusable skill source only. Never commit or publish real scan results, disk layouts, absolute user paths, filenames from private files, screenshots, logs, hashes, credentials, account details, conversation excerpts, or local study artifacts. Runtime outputs must live outside this repository and its Git worktrees. Public examples must be wholly synthetic.

The publication allowlist is in .gitignore. Stage explicit source paths and review the full diff before committing. Do not force-add ignored runtime artifacts. Changes to the allowlist must preserve the private-output boundary.

Use a neutral project author and a non-personal noreply email for commits; do not inherit a personal name, email, signing identity, or co-author trailer. Before publishing, inspect commit metadata and every reachable tree/blob, including earlier revisions. Removing a sensitive file from the latest tree does not remove it from history.

If private data enters local Git history, stop before any push and reconstruct clean history from verified source. If it was published, stop further publication and report the exposure; deleting the current file is insufficient.
