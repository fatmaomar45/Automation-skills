# Product Requirements & Feature Breakdown Skill

Converts raw product ideas, feature requests, and PRDs into structured,
testable engineering specifications: functional/non-functional requirements,
business rules, capabilities, user stories, and Given/When/Then acceptance
criteria. Refuses to invent missing details — gaps are flagged as
**Assumptions** or **Open Questions** instead.

See `SKILL.md` for the full workflow.

## What this skill does well

- Enforces the Understand → Requirements → Capabilities → Stories →
  Acceptance Criteria → Validate pipeline, so features aren't turned into a
  single oversized story.
- Keeps functional and non-functional requirements separate, and only adds
  NFRs when relevant.
- Strict anti-hallucination rule: unclear items are always labeled
  Assumption / Open Question rather than presented as fact.
- Adapts depth to feature complexity instead of always producing a maximal
  document.
- Consistent ID scheme (FR/NFR/BR/CAP/US/AC/EC) for traceability.

## How it compares to similar skills

A handful of public Claude skills solve the same problem (feature →
user stories → acceptance criteria). Comparing against them surfaced some
patterns they use that this skill currently doesn't:

| Capability | This skill | Seen in other skills |
|---|---|---|
| Reference files split out of the main body (EARS syntax, interview questions, spec templates, worked examples loaded on demand) | No — everything lives in one SKILL.md | `feature-forge` |
| Structured elicitation step before drafting (explicit interview/question phase) | Partial — flags gaps as Open Questions, but doesn't actively interview first | `feature-forge` |
| Defined file-output convention (e.g. auto-save to `stories-[feature-name].md`) | No — output format is defined, but no save step | `user-stories` (claude-code-pm-skills) |
| Programmatic validation of the generated doc (a script, not just an LLM self-check) | No — Section 12 is an internal checklist only | PRD Generator (`prd-generator`) |
| Blank reusable templates for a single story / single AC | No | Several (`ba-zone-user-story-ac-writer`, `prd-generator`) |
| EARS format offered as an alternative to Given/When/Then for functional requirements | No — Given/When/Then only | `feature-forge` |
| Named operating modes (write new / refine existing / add AC only) selectable up front | Implicit via Section 15, not an explicit mode selector | `ba-zone-user-story-ac-writer` |
| Explicit story-splitting technique for oversized stories | Only "do not split unnecessarily" — no splitting method | `user-stories`, `Product-Manager-Skills/user-story` |

## Possible enhancements

Not implemented yet — listed here so they're easy to pick up later:

1. Break `SKILL.md` into a slim workflow file plus a `references/` folder
   (e.g. `ears-syntax.md`, `interview-questions.md`, `examples.md`) so the
   always-loaded body stays short.
2. Add an explicit elicitation pass that asks clarifying questions before
   drafting, rather than only flagging gaps after the fact.
3. Define a save convention, e.g. write output to
   `requirements-[feature-name].md`.
4. Add a lightweight validation script (field presence, ID formatting,
   Given/When/Then structure) to backstop the internal quality check.
5. Ship blank `templates/user-story-template.md` and
   `templates/ac-template.md` for standalone reuse.
6. Offer EARS phrasing as an option for functional requirements alongside
   Given/When/Then acceptance criteria.
7. Turn Section 15 ("Different Requests") into explicit selectable modes.
8. Add a concrete story-splitting technique (e.g. by workflow step, business
   rule, or CRUD operation) for oversized stories.

## Sources consulted

- `feature-forge` — github.com/jeffallan/claude-skills
- `user-stories` — github.com/Mehdibargach/claude-code-pm-skills
- `ba-zone-user-story-ac-writer` — github.com/blaoman/ba-zone-user-story-ac-writer
- `prd-generator` — github.com/jamesrochabrun/skills
- `user-story-templates` — github.com/slgoodrich/agents
- `user-story` — github.com/deanpeters/Product-Manager-Skills
