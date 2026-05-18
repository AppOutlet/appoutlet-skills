# Eval: bug-notifications-mark-all-read (Iteration 1, with skill)

## Skill Loaded
Loaded `ticket-creator` skill.

## Preflight
- `gh --version`: ✓ gh version 2.92.0 installed
- `gh auth status`: ✓ Logged in as `MessiasLima`

## Duplicate Check
Ran `gh issue list --state all --limit 50 --search "mark all as read notification badge"` and `gh issue list --state all --limit 10` in `/Users/messias/Workspace/skills`. No existing issues found in this repository. No duplicates detected.

## Codebase Investigation

Searched for:
- `**/*.kt` — No files found
- `**/*notification*` — No files found
- `**/*.gradle*` — No files found
- Grep for `NotificationsViewModel|NotificationsOrchestrator|NotificationRepository` — Only matched in eval metadata files, not in application source code
- `git ls-files` — Confirms repo contains only SKILL.md, README, AGENTS.md, and template/eval JSON files

**Finding:** This repository (`appoutlet-skills`) is a **skills repository** for agent skills used with OpenCode. Per its AGENTS.md: "Each subdirectory under `skills/` is a self-contained agent skill — not application source code. There is no build, test suite, CI, or runtime environment."

No Android/Kotlin application code or notification-related implementation exists in this repository. A codebase investigation in the actual app repository (where `NotificationsViewModel`, `NotificationsOrchestrator`, `NotificationRepository`, etc. live) would be needed to identify the root cause. Common causes for this type of bug:
1. The badge count is cached in a local data store and only refreshed at app startup.
2. "Mark all as read" marks notifications read on the backend but does not update the local badge counter.
3. The `NotificationsViewModel`/`NotificationsOrchestrator` emits a new count, but the badge observer is no longer active after navigating to the notifications screen.
4. The unread count flow does not re-trigger after the mutation completes.

## Draft Presented

### Proposed Title
Unread notification badge persists after "Mark all as read" until app restart

### Proposed Body

```markdown
## Description

After tapping "Mark all as read" on the notifications screen, the unread badge count on the app icon or navigation element does not update to reflect the new read state. The badge only corrects itself after the user kills and restarts the app. This suggests a stale local badge cache that is not invalidated when notifications are marked as read.

This issue was observed in the app's notifications screen. A codebase investigation in the current repository found no application source code (this is a skills configuration repository). The root cause likely lives in the app repository and involves the synchronization between the "Mark all as read" action and the persisted/provided unread badge count.

## Steps to Reproduce

1. Launch the app and ensure there is at least one unread notification.
2. Note the unread badge count shown on the app icon or navigation element.
3. Navigate to the notifications screen.
4. Tap the "Mark all as read" button.
5. Return to the previous screen or background the app.
6. Observe the unread badge count — it still shows the previous count.

## Actual Behavior

The unread badge count remains unchanged after tapping "Mark all as read". The badge only updates after the user force-closes and reopens the app.

## Expected Behavior

Tapping "Mark all as read" immediately sets the unread badge count to zero (or the correct remaining count), reflecting the updated read state without requiring an app restart.

## Additional Information

- **Environment:** All platforms where the notifications feature is available
- **Priority:** Medium — functional issue that degrades UX but does not crash the app
- **Related Files:** `NotificationsViewModel`, `NotificationsOrchestrator`, `NotificationRepository`, `DefaultNotificationRepository` (in the app repository)
- **Workaround:** Force-close and reopen the app to refresh the badge count
- **Sentry ticket:** N/A
```

## Self-Review

1. **Title alone tells the story:** "Unread notification badge persists after 'Mark all as read' until app restart" — outcome-oriented, no ambiguity.
2. **Description for new readers:** Explains the symptom, the stale-cache hypothesis, and notes that investigation happened in a skills-only repo. The "why" is clear.
3. **Acceptance criteria (Steps + Expected):** Verifiable by a QA engineer: tap "Mark all as read", check badge, no restart needed.
4. **Weasel words checked:** No "properly", "correctly", "as expected" used without definition.
5. **Hidden scope:** None detected — this is a single-concern ticket about badge sync. No backend, multi-platform, or migration dependencies flagged outside the bug.

**Draft ready for user approval.**
