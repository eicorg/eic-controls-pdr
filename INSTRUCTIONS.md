# PDR AI Agent Instructions (Common)

## Purpose
Use this guidance for all AI-assisted tasks in this PDR workspace.
`ROD` means **Record of Decision**. Agents should produce clear, auditable, and technically grounded decision artifacts.

## Scope
Apply these instructions when:
- Drafting or updating a Record of Decision.
- Summarizing decision evidence from technical documents.
- Acknowledging alternatives and recommending a preferred option.
- Preparing review-ready decision text for project records.

## Source Material Priority
When building a response, prioritize sources in this order:
1. Task-specific user instructions.
2. Existing ROD template: `rod/Record of Decision Template.docx`.
3. Existing examples in `rod/examples/`.
4. Supporting references in `supporting-docs/`.
5. Explicitly stated assumptions (clearly labeled as assumptions).

## Required Working Style
- Be factual, concise, and neutral.
- Separate facts from assumptions.
- Do not invent data, requirements, or approvals.
- If evidence is missing, call it out and continue with a bounded draft.
- Keep wording review-ready (suitable for engineering and management stakeholders).

## Standard ROD Workflow
For each ROD task, follow this sequence:
1. Clarify the decision statement: what is being decided.
2. Describe what the decision establishes for the project.
3. Describe what the decision accomplishes (outcomes and value).
4. Define scope and expected impact.
5. Capture key risks and mitigations.
6. Record traceability: list source docs and evidence used.
7. Add concise alternatives at the end.

## Output Structure (Default)
Unless the user requests a different format, generate output with these sections:
- Title
- Statement of Decision
- Description / Purpose
- What This Decision Establishes and Accomplishes
- Background
- Git-Based Source Code Management
- Continuous Integration and Continuous Delivery (CI/CD)
- Scope and Expected Impact
- Risks and Mitigations (optional, include when requested or relevant)
- References and Evidence
- Alternatives (Concise, at end)

Only include `Implementation / Next Actions` or `Open Issues / Assumptions` when explicitly requested by the user.

## Quality Gate Checklist
Before finalizing, verify:
- Decision is unambiguous and testable.
- Decision description is focused on what the decision is and what it accomplishes.
- Alternatives are concise and placed at the end.
- Risks and mitigations are stated.
- References are listed and relevant.
- No contradiction between decision statement and outcomes.

## Formatting Rules
- Prefer plain Markdown.
- Use short paragraphs and clear headings.
- Use tables for side-by-side alternative comparisons when helpful.
- Use consistent terms: `decision`, `alternative`, `criterion`, `risk`, `assumption`.

## Safety and Integrity
- Do not claim approvals that did not occur.
- Do not represent assumptions as confirmed facts.
- Flag uncertainty clearly and propose how to resolve it.

## Reuse Pattern for New Tasks
When starting a new task, agents should begin with:
- Decision objective (1-2 lines)
- Inputs reviewed (bulleted list)
- Draft output using the standard structure above
- Gaps/questions only if needed for finalization
