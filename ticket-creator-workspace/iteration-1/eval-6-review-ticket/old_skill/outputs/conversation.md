# Ticket Review Conversation — Old Skill (Baseline)

## User Request

"Review this ticket for me:

Title: Fix notifications

Body:
## Description
The notifications thing is broken. It should work properly.

## Acceptance Criteria
- [ ] Fix the bug
- [ ] Test everything works

## Additional Information
This is high priority."

---

## Skill Preflight

- `gh` is installed (version 2.92.0) — preflight passed.

---

## Ticket Type Identification

- **Type:** Bug (broken behavior, "notifications... broken")
- No Sentry link or ID provided — Sentry integration skipped.

---

## Review (per "Improving Existing Tickets" workflow)

### Blockers

1. **No description of what "notifications thing" refers to** — Push notifications? In-app? Email? SMS? A specific screen? The ticket doesn't say. A developer has no starting point.
2. **Acceptance criteria are meaningless** — "Fix the bug" and "Test everything works" are not verifiable. "Fix" and "works" are undefined. No QA engineer could confirm completion.
3. **No steps to reproduce** — Without knowing the current broken behavior, nobody can verify the fix.
4. **No actual vs. expected behavior** — What is happening now? What should happen instead?

### Improvements

1. **Title "Fix notifications"** — "Fix" describes the activity, not the outcome. A better title would describe what observable change the fix produces.
2. **"The notifications thing is broken"** — Extremely vague. Needs specifics: what doesn't work under what conditions?
3. **"It should work properly"** — "Properly" is a weasel word. What specifically should happen?
4. **"Test everything works"** — "Everything" is unbounded. Which scenarios should be tested? Success/failure/edge cases?

### Suggestions

- Add reproduction steps.
- Specify environment (device, OS, app version).
- Link to related files or modules if known.
- Add screenshots, logs, or Sentry links if available.

### Improved Draft (using `bug` template)

```markdown
## Description
Notifications are not functioning as expected. The specific behavior, affected notification type (push/in-app/email), and symptoms require clarification from the reporter.

## Steps to Reproduce
1. [Placeholder — unknown; reporter did not provide steps]
2.
3.

## Actual Behavior
[Placeholder — reporter stated "broken" but did not describe the current behavior]

## Expected Behavior
[Placeholder — reporter stated "should work properly" but did not define correct behavior]

## Additional Information
- Environment: [Not specified]
- Priority: High
- Related Files: [Not identified]
- Workaround: [Unknown]
- Sentry ticket: [None provided]
```

This ticket cannot be worked on as-is. The blockers above need to be resolved first. Would you like me to ask the clarifying questions to fill in the gaps, or would you like to update the ticket with the missing details yourself?
