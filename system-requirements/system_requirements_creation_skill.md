---
name: system-requirements-creation
description: To transform raw product ideas, feature requests, architectural notes, or PRDs into clear, structured functional system requirements, non-functional requirements, and explicit business or validation rules. This process focuses purely on technical definitions, structural backend rules, and engineering constraints behind the scenes.
---

# Technical Product & System Requirements Creation Skill

This skill converts raw product descriptions, feature notes, and high-level PRDs into structured system requirements. Acting as a Technical Requirements Analyst and Systems Architect, it focuses purely on functional system rules, structural backend logic, and engineering constraints, eliminating downstream testing documentation.

The core function of this skill is to systematically break down a concept into explicit system requirements, non-functional constraints, and technical validation parameters. It isolates what the architecture must execute behind the scenes to support product features.

## Core Workflow

Always follow this route:

```
INPUT
  ↓
1. UNDERSTAND
  ↓
2. DEFINE SYSTEM REQUIREMENTS
  ↓
3. DEFINE BUSINESS & VALIDATION RULES
  ↓
FINAL OUTPUT
```

Do not skip important stages, but do not generate unnecessary documentation.

## 1. Understand the Input

First determine what the user is providing (Product idea, Feature, Architectural notes, etc.). Identify only the technical information that is relevant:
- Product/context, Systems impacted, Data entities, Performance targets, Security baselines, Dependencies, Scope.

Do not invent missing information. If something important is unclear, mark it as **Open Question** or **Assumption** instead of presenting it as fact.

## 2. System Requirements Breakdown

Separate structural requirements into explicit system rules and behaviors:

### Functional System Requirements
What the system backend, database, APIs, or logic must execute behind the scenes.
> SYS-FR-001: The system must hash user passwords using bcrypt before saving to the database.

### Non-Functional System Requirements
System performance, security, and scalability constraints.
- Performance, Security, Accessibility, Reliability, Usability, Scalability, Privacy.

### Business & Validation Rules
- Identify backend calculation rules that control how the system behaves ("Only verified accounts can trigger an API transfer").
- Identify validation bounds (Required payload fields, data types, valid/invalid value limits, string formats, system thresholds).

## 3. Scope Control & Edge Cases

Separate:
- **In Scope:** Technical infrastructure and data logic required for the immediate version.
- **Out of Scope:** Future architectural scaling or unrelated backend optimization.
- **Realistic Edge Cases:** Focus on technical anomalies (e.g., database timeouts, API failures, rate limiting, race conditions).

## 4. Assumptions & Open Questions
- **Assumptions:** Things inferred because the system or architecture requirement is incomplete.
- **Open Questions:** Things that need a stakeholder, architect, or engineering lead decision before implementation.

## 5. Requirement IDs

Use simple IDs when producing structured requirements:

| Prefix | Meaning |
|--------|---------|
| SYS-FR-001 | Functional System Requirement |
| SYS-NFR-001 | Non-Functional System Requirement |
| BR-001 | Business Rule / Validation Rule |

## 6. Standard Output Layout

For a normal system breakdown, use this structure to ensure precise technical readability:

```markdown
# Technical Requirements: [Feature Name]

## 1. Technical Context & Scope
Brief explanation of the technical context, microservices, databases, or systems impacted by this requirement set.

## 2. System Requirements
### Functional

| ID | System Requirement Definition | Priority |
|----|-------------------------------|----------|
| SYS-FR-001 | The system must... | Must Have |

### Non-Functional
- SYS-NFR-001: ...

### Business Rules & Validation Bounds
- BR-001: ...

## 3. Technical Assumptions & Open Questions
- **Assumptions:** ...
- **Open Questions:** ...
```

## 7. Anti-Hallucination & Golden Rule
Never invent systems or engineering details outside the prompt bounds. The absolute purpose of this skill is to transform a raw product idea strictly into **Functional System Requirements, Non-Functional Constraints, and Business/Validation Rules.** All testing/QA verification frameworks and user-facing frontend paths (User Stories) are completely removed from this lifecycle.