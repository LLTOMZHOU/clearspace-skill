---
name: clearspace-skill
description: Audit macOS storage, explain cleanup opportunities, and perform explicitly approved cleanup. Use for disk-space reviews or cleanup planning, with an optional local review interface.
---

# Clearspace

Help the user decide what is worth cleaning and why. Start with a read-only audit, prioritize useful opportunities, and keep inspection, content analysis, and cleanup execution distinct. Malware detection and removal are out of scope.

## Audit and explain

Use the user's requested scope and available context. Begin with targeted measurements rather than an unrestricted filesystem traversal. Use installed, read-only filesystem and owning-tool inventories; report inaccessible, skipped, or timed-out locations as unknown, not empty. Do not expand permissions or hydrate cloud placeholders to complete a scan.

Inspect metadata by default. Size, folder names, modification time, missing last-use information, and a lack of tracked Git changes do not establish that data is disposable. Preserve sources, unique outputs, credentials, app databases, active runtimes, and recovery state.

Group findings by the decision the user needs to make:

| Review path | Evidence and boundary |
| --- | --- |
| Caches and generated environments | Identify the owner, regeneration method, active jobs, offline needs, and rebuild cost. Shared package stores require native inventory/prune estimates. Project dependencies may contain local edits. |
| Worktrees | Check owning task/session, branch and HEAD, tracked/untracked/ignored state, locks, unique commits, and remote-ref freshness. Preserve unknown ownership and unique work. Pruning dangling Git records does not remove existing checkouts. |
| Temporary folders | Identify the creating job, completion/activity signals, and whether useful outputs exist elsewhere. A temporary name or old timestamp is only a clue. |
| Apps | Separate bundle size, usage evidence, vendor uninstall flow, and related user data. Missing usage is unknown; uninstalling does not cancel subscriptions. |
| Large or old files | Review purpose, provenance, backups, and replacement cost. Downloaded installers, compressed sources, and extracted payloads need distinct decisions. Old media and datasets may still be valuable. |
| Duplicates and versions | Distinguish exact copies, similar media, and related document versions. Identical bytes can have different contextual roles or references; do not choose a keeper from filenames or recency alone. |

Include models, Docker/VM storage, media libraries, toolchains, app-retention data, or backups when relevant. Distinguish downloadable models from custom checkpoints; distinguish VM build cache/images from volumes and writable state. Use the owning application's manager for managed media, backups, and snapshots instead of deleting library internals.

For exact-copy verification, explain and bound local file-byte hashing. Exclude cloud placeholders, credential stores, and managed-library internals; account for hardlinks and files changing during the scan. Semantic reading, OCR, image similarity, and version ranking require a separate, explicit folder/type/processing scope. Confirm the provider before any remote content analysis. Ranking is not deletion approval.

Keep four measurements separate:

- Measured storage: byte basis, timestamp, source, and coverage.
- Review candidates: selected, non-overlapping findings, not promised recovery.
- Estimated reclaimable space: an owning-tool preview or an explicitly labeled estimate; unknown when unsupported.
- Observed capacity change: consistent before/after capacity measurements after an approved action.

Allocated sizes are not unique physical consumption on APFS. Shared blobs, clones, sparse VM disks, and snapshots prevent naive summation. Same-volume Trash or quarantine retains occupied storage until data is actually released.

Present a brief summary of the biggest useful opportunities, with reasons, confidence, and the next decision. Link mentioned objects to local evidence or drilldowns when the presentation supports it. Prefer a short prioritized review over a catalog of everything large.

## Optional local review UI

When the user wants a UI, generate it from the actual private snapshot. Start with standalone HTML; use harness-supported interactivity when available. Offer a temporary loopback server only when live refresh or native actions justify one and the user opts in.

Use a quiet desktop overview: a brief navigable summary, a proportional tree/treemap when useful, and details on demand. Avoid a default search bar, permanent inspector, or dense dashboard. The map shows storage distribution, not removal eligibility. Keep coverage and provenance inspectable.

Folder references may navigate the saved audit. Native reveal/open actions need a real supported bridge; do not present inert controls as working. Show selected objects, sizes, byte bases, and reasons in the review. Avoid summing overlapping selections.

A review export identifies the matching snapshot and selected objects and retains these semantics:

```json
{
  "intent": "review_only",
  "requires_execution_time_revalidation": true,
  "approved_for_deletion": false
}
```

Exporting a plan or preparing a content-analysis request does not launch an agent, authorize content reading, or approve cleanup. State the actual next step.

## Approved cleanup

Before destructive cleanup, present the concrete selected objects, supported action, impact, replacement cost, and recovery option. Require explicit approval for that proposal and follow the host's action-time confirmation rules. A general audit/cleanup request is not blanket approval for every finding.

Revalidate scope, identity, symlinks, ownership, activity, freshness, and recovery assumptions immediately before execution. If the scope or consequences changed, return to review. Prefer owning-tool operations, verify their installed behavior, and avoid broad recursive removal commands. Use recoverable actions where appropriate without promising that they free space immediately.

Report completed, skipped, and failed actions separately. Verify downstream results and capacity evidence; do not equate a successful command with a particular recovery amount. An app uninstall, local cloud eviction, permanent deletion, and subscription cancellation are different actions.

## Private runtime data

Keep scan results, reports, paths, filenames, hashes, screenshots, logs, and generated HTML in a private local output directory outside public repositories and their Git worktrees. Treat even metadata and disk layout as personal data. Use offline/local assets and avoid telemetry or third-party UI resources that expose scan data.

Never add real user artifacts, machine details, conversation excerpts, or study history to this skill's source or Git history. Public documentation and fixtures must be generic or wholly synthetic. Do not publish or transmit a private snapshot merely to make a report or UI easier to share.
