# AGENTS Guide

## Repository Purpose
- This repository is a documentation workspace for EIC controls decisions and communication artifacts, not an application codebase.
- Core artifacts include RODs in `rod/`, supporting evidence in `supporting-docs/`, and slide material in `presentations/`.
- Use task-specific user instructions first, then reuse patterns from existing files in the relevant folder.

## Big Picture Architecture
- `rod/EIC-ROD-EPICS-Control-System.md` defines the controls baseline: EPICS 7 with **pvAccess (PVA) first** for new systems.
- Legacy ADO systems are transitional and exposed through `AdoEpicsBridge` (p4p-based ADO-to-EPICS bridge, primary for FEC) and `AdoPvaSrv` (server-side pvAccess ADO implementation); CA is compatibility-only.
- `rod/EIC-ROD-Phoebus-Tools-and-Services.md` defines the operator/middle layer: Phoebus tools + microservices (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, PVA Gateway).
- `rod/EIC-ROD-GitHub-Platform.md` defines delivery/governance: GitHub as SCM, PR review, branch protections, CODEOWNERS, reusable Actions, tagged releases.

## How To Work In This Repo
- Treat edits as documentation authoring (decision records, supporting docs, and presentations), not software feature work.
- Before drafting, ingest relevant materials from `rod/examples/`, `presentations/examples/`, and `rod/raw_resources/`.
- For RODs, follow the established section order in existing `rod/*.md` files unless the user requests a different format.
- For presentations, model structure and level of detail on `presentations/examples/` and align claims with referenced evidence.
- Keep statements evidence-backed and auditable; explicitly label assumptions.
- Cross-link related decisions when relevant (example: Phoebus ROD references the EPICS ROD).
- Preserve alternatives at the end in concise table form when writing RODs.

## Project-Specific Conventions
- Tone is neutral, factual, and review-ready for engineering + management audiences.
- Mandatory concepts to separate clearly: `decision`, `alternative`, `risk`, `assumption`, `evidence`.
- Preferred ROD structure is stable: Title -> Statement of Decision -> Purpose/Background -> Scope/Impact -> Risks -> References -> Alternatives.
- Scope and impact are explicit bullets; risks are usually a `Risk | Severity | Mitigation` table.
- References are concrete URLs/papers and should map to claims made in the text.

## Developer Workflows (Docs-Focused)
- There are currently no discoverable build/test/lint manifests in this repo (no `package.json`, `pyproject.toml`, `Makefile`, etc.).
- Validation is editorial/traceability based: section completeness, claim-to-reference alignment, and consistency with nearby examples.
- For ROD drafting, use `rod/Record of Decision Template.docx` and examples in `rod/examples/` as formatting precedents.
- For presentations, use `presentations/examples/` as precedent for slide flow, technical depth, and audience-ready phrasing.

## Source Priority
- Use this order when drafting content: user request -> examples/raw materials in the target domain (`rod/examples/`, `presentations/examples/`, `rod/raw_resources/`) -> existing artifact in target folder -> related RODs/supporting docs -> explicitly labeled assumptions.

## Foundational Requirements Authority
- **EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.docx** is the authoritative source for all controls system requirements.
- All presentation claims about requirements, performance, and scope must be traceable to this document.
- Ingest this document early when preparing any presentation content.

## Integration Boundaries To Respect
- EPICS ROD: system-control protocol and migration boundary (PVA default, CA compatibility, AdoEpicsBridge / AdoPvaSrv only for legacy ADO systems).
- Phoebus ROD: operator UX and middle-layer service boundary on top of EPICS.
- GitHub Platform ROD: repo governance, CI/CD, release evidence, and collaboration boundary.
- Keep new decision text aligned with these boundaries unless the task is explicitly to supersede them.

