---
name: user-story-jira
description: Use this skill to turn a feature idea, request, or note into one or more user stories with Given/When/Then acceptance criteria, and create them directly as Jira issues when a Jira/Atlassian connection is available (falling back to a JIRA-ready text ticket otherwise). Trigger whenever the user asks to "write a user story", "create a user story", "make acceptance criteria", "create a JIRA ticket/story", "file this in Jira", or gives a feature and wants it turned into a ticket. Each story is capped at 3-5 acceptance criteria — if more are needed, the skill splits the work into additional linked stories rather than overloading one ticket. Do not use this skill for full requirements documents, system/functional requirements, or architecture — use a system-requirements skill for that instead.
---

# User Story & Acceptance Criteria (JIRA-Ready)

Converts a feature idea, request, or note into one or more user stories, each with clear Given/When/Then acceptance criteria, formatted as a ticket ready to paste into JIRA.

## Core Rule: 3–5 Acceptance Criteria Per Story

This is the defining constraint of the skill:

- Every story gets **3 to 5** acceptance criteria. Not fewer (too thin to be testable), not more (the story is too big).
- If, while writing acceptance criteria, you find yourself needing a 6th, **stop**. That's a signal the story covers more than one unit of value. Split it:
  1. Identify which criteria belong to a distinct sub-behavior (e.g., "resending a verification email" inside an "account creation" story).
  2. Carve those into a **new story** with its own title, own 3–5 ACs, and a noted dependency/link back to the original (e.g., "Relates to US-001").
  3. Re-check the original story's remaining ACs still stand on their own at 3–5.
- Never pad a story with filler criteria just to hit 3. If a story genuinely only supports 1–2 meaningful criteria, say so and note it's a small/simple story rather than inventing extra ones.

## Workflow

0. **Check for a Jira connection.** Look for connected Atlassian/Jira MCP tools (e.g. `createJiraIssue`, `getJiraIssue`, `discover`, `executeWrite`, or any available tool whose name/description indicates Jira issue creation — tool names can vary by connector). If none are connected, search the MCP registry for an Atlassian/Jira connector and offer it to the user via the connector picker — never call a Jira-writing tool without the user's explicit go-ahead to connect. If the user declines or none is available, say plainly what you checked for and found (e.g. "no Jira/Atlassian tool is available in this session") before falling back to producing the JIRA Ticket Template below as text — don't silently assume no connection exists without naming what was checked.

1. **Understand the input.** Before assuming no feature was given, check the conversation for an attached or referenced document (PRD, spec, notes file, etc.) and read its actual content — don't draft a generic placeholder story if a real document is present but unread. Once you have the real input, identify the actor/persona, the action, and the benefit/value. If any of these is missing or unclear even after checking attachments, do not invent it — mark it as an **Assumption** (a reasonable default you're proceeding with) or an **Open Question** (something that needs a stakeholder decision) directly under the relevant story.
2. **Decide if this is one story or several.** If the request describes multiple distinct pieces of value (e.g., "let users sign up and reset their password"), write separate stories rather than merging them.
3. **Draft the story** in standard form:
   ```
   As a [persona],
   I want to [action],
   so that [benefit].
   ```
4. **Write 3–5 acceptance criteria** in Given/When/Then form, applying the Core Rule above. Cover the happy path plus the most relevant validation/failure/edge cases — don't force in edge cases that don't realistically apply.
5. **Format as a JIRA ticket** (template below) for every story produced.
6. **Quality check before presenting:**
   - Is the persona specific (not just "user") where the input allows it?
   - Does the story communicate Who / What / Why?
   - Is each AC observable and testable — could QA write a test from it directly?
   - Is the story small enough to implement and verify independently (INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable)?
   - Did I invent any business rule, field, or behavior not implied by the input? If so, relabel it as an Assumption.

## Creating Issues Directly in Jira (when connected)

When a Jira/Atlassian MCP connection is available, create the issue(s) instead of just printing text:

1. **Confirm the target before writing anything.** Ask for (or look up, if the tools allow browsing projects) the Jira **project key**, and confirm the issue type name if it isn't simply "Story" in that project.
2. **Show the draft first.** Present each story using the Ticket Content below and get the user's confirmation before creating it in Jira — don't silently file tickets from a first draft.
3. **Create the issue** (e.g. via `createJiraIssue` or the equivalent write tool) using:
   - Project = the confirmed project key
   - Issue type = Story (or the confirmed equivalent)
   - Summary = the "As a / I want / so that" line
   - Description = the full story text plus the Acceptance Criteria as a numbered list
   - Labels, if any were identified
4. **Link split stories.** If a story was split per the Core Rule, create the new issue and then link it to the original (e.g. "relates to" / "split from") using the tool's issue-linking capability, rather than only noting the link in text.
5. **Report back** the created issue key(s) and a link to each, instead of re-printing the full ticket text once it's filed.
6. Never create, edit, or delete a Jira issue without the user's explicit confirmation of that specific story's content first.

## Ticket Content (used for the Jira description, or as the fallback template)

```markdown
### [US-001] <Short, action-oriented title>

**Issue Type:** Story
**Summary:** As a [persona], I want to [action], so that [benefit].
**Labels:** [relevant tags, e.g. auth, onboarding — omit if none obvious]

**Description**
As a [persona],
I want to [action],
so that [benefit].

**Acceptance Criteria**
1. Given [context], when [action], then [outcome].
2. Given [context], when [action], then [outcome].
3. Given [context], when [action], then [outcome].
(3-5 total — never more; split into a new story if needed)

**Dependencies:** [e.g., "Requires US-000 — Login"; omit if none]
**Linked Stories:** [only if this was split off from or spawned another story]
**Assumptions:** [only if any were made; omit section if none]
**Open Questions:** [only if any materially affect scope; omit section if none]
```

When a request produces multiple stories, work through them as a numbered sequence (US-001, US-002, ...). If not connected to Jira, present each in its own ticket block as text and cross-reference dependencies/splits using the Dependencies/Linked Stories fields. If connected, use these fields to populate the created issues and their links as described above.

## What NOT to do

- Don't write functional/non-functional requirements documents, business-rule catalogs, or system-level specs — that's a separate skill.
- Don't invent personas, business rules, fields, or integrations not implied by the input; label anything uncertain as an Assumption or Open Question instead.
- Don't let a single story creep past 5 acceptance criteria — split instead.
- Don't pad with meaningless acceptance criteria to reach 3.
- Don't create, edit, or delete anything in Jira without first showing the user the story content and getting confirmation.
- Don't pick a Jira project or issue type on the user's behalf — confirm it.
