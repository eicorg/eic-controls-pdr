## Slide 1: Controls Applications and User Interfaces

Charge questions addressed: CQ8 (design maturity readiness framing)

Slide overview:
Establish review context for applications and user interfaces, using the thin MOCR002 talk flow adapted for EIC PDR.

Slide 1:
- Title: Controls Applications and User Interfaces
- Subtitle: EIC Controls PDR Applications and Operator Workflow Review
- Presenter block: team, date, review body
- Purpose statement:
	Present the baseline operator toolkit, integrated user workflows, and implementation readiness for controls applications.

Notes:
1. This talk follows the thin MOCR002 sequence as the primary source, cleaned up for PDR traceability.
2. The emphasis is applications and operator experience; detailed service internals are moved to appendix slides.
3. This phase demonstrates architecture maturity and workflow coherence, not final verification closure.

Detailed references appear in technical slides where they are used.

## Slide 2: Charge Questions

Charge questions addressed: CQ1-CQ8 (definition and scope of all charge questions)

Slide overview:
Frame review criteria and what this applications/UI talk addresses in the current phase.

Slide 2:
- CQ1: Have committee recommendations from the Preliminary Design Review been addressed adequately?
- CQ2: Are the system requirements sufficiently defined, understood, and documented for this phase of the design?
- CQ3: Do the designs meet the requirements? (scope for later phase)
- CQ4: Are the interfaces sufficiently defined, understood, and documented for this phase of the design?
- CQ5: Are the analysis, simulations, drawings, specifications, and work plans sufficient for this phase of the design?
- CQ6: Are the plans to address ES&H and quality sufficient for this phase of the design?
- CQ7: Have technical risks been identified and are mitigation plans adequate for this phase of the design? (scope for later phase)
- CQ8: Is the overall design maturity sufficient to proceed with the final design phase?

## Slide 3: Outline of the Talk

Charge questions addressed: CQ8 (overall maturity roadmap)

Slide overview:
Roadmap aligned to the thin MOCR002 talk with EIC-specific framing.

Slide 3:
- Scope and review framing
- Phoebus position in the EPICS controls ecosystem
- Application-focused workflow (Display Builder, Data Browser, Alarm, Logbook, Save/Restore)
- Web and remote operations access
- Architecture foundation and extensibility (SPI)
- Site-specific product model for EIC
- Collaboration and contribution model
- Open questions and appendix service details (only if requested)

Notes:
1. Main body focuses on applications and user interfaces.
2. Service-depth slides are intentionally placed at the end as appendix material.

## Slide 4: Scope

Charge questions addressed: CQ2, CQ4, CQ5, CQ8

Slide overview:
Define what is in and out of scope for this presentation.

Slide 4:
- In scope:
	- Operator-facing applications and user workflow integration
	- Desktop and web runtime usage patterns
	- Architecture decisions that directly impact UI/application behavior
	- Requirements traceability for operator interface capabilities
- Out of scope for main narrative:
	- Detailed service deployment and operations internals (appendix)
	- Full performance verification closure

## Slide 5: Phoebus in the EPICS Controls Ecosystem

Charge questions addressed: CQ2, CQ4, CQ8

Slide overview:
Position Phoebus as operator toolkit, service ecosystem, and framework.

Slide 5:
- Primary visual: `presentations/examples/images/MOCR002_f1.png`
- Core message from thin talk:
	- Phoebus is an operator-facing toolkit for integrated workflows
	- Phoebus is a group of middle-layer microservices
	- Phoebus is a framework for building tools and services
- EIC implication:
	- One coherent user experience across commissioning and operations domains

Notes:
1. Keep wording close to thin MOCR002 talk for familiarity.
2. Tie every claim to EIC architecture boundaries and requirements document language.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 6: CS-Studio and Phoebus Coexistence Context

Charge questions addressed: CQ1, CQ4

Slide overview:
Clarify near-term coexistence and migration posture for user tools.

Slide 6:
- Thin talk message adapted:
	- CS-Studio and Phoebus coexist in real facility operations
	- Common EPICS services support both toolchains during transition
- EIC framing:
	- Preserve operational continuity while standardizing on modern tooling
	- Keep user workflow stable while backend services evolve

Notes:
1. Keep this as transition context, not a deep migration plan slide.
2. Use this bridge slide before diving into specific applications.

## Slide 7: Display Builder Strategy

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
How Display Builder supports reusable synoptic UI development and runtime use.

Slide 7:
- Thin talk anchors:
	- Display Builder editor
	- Display Builder runtime
- EIC operator-interface fit:
	- Reusable widgets and parameterized displays
	- Live process data with metadata and clear status behavior
	- Version-controlled screen assets for consistent operations
	- Supports OPI requirement intent for reusable controls, navigation, and service integration

Notes:
1. Keep this practical and operator-centric.
2. Emphasize maintainability and repeatability over tool branding.

References:
- Requirements authority (OPI scope): [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)

## Slide 8: Web Runtime and Remote Operations

Charge questions addressed: CQ4, CQ5, CQ6

Slide overview:
Show how web access complements desktop operations.

Slide 8:
- Thin talk anchors:
	- Phoebus on the web
	- .bob files converted to web runtime OPIs
	- Converted screens with improved generation workflow for maintainability
- EIC framing:
	- Remote visibility and role-appropriate access outside main control consoles
	- Same display assets reused across desktop and web contexts
	- Reduced duplication in UI maintenance

Notes:
1. Position web tools as complementary, not replacement for operator desktops.
2. Keep security boundary details at architecture level in this talk.

## Slide 9: Data Browser Workflow

Charge questions addressed: CQ3, CQ4, CQ7

Slide overview:
Trend and history access as a core operator diagnostic capability.

Slide 9:
- Thin talk anchor:
	- Data Browser for PV history access
- EIC operations value:
	- Fast shift from live alarm/event to historical trend context
	- Cross-channel correlation for diagnosis and post-mortem analysis
	- Workflow continuity with display, alarm, and logbook tools

Notes:
1. Connect this slide to operational risk reduction and troubleshooting speed.
2. Keep performance claims qualitative unless a verified metric is cited.

## Slide 10: Applications Portfolio (User Workflow View)

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Consolidated application view matching thin MOCR002 application slide content.

Slide 10:
- Alarm UI:
	- Hierarchical alarm trees, active alarm tables, annunciation
	- Alarm awareness integrated into related workflows
- Logbook:
	- Integrated operator logging with context capture
	- Backend-agnostic model (Olog/elog and site-specific variants)
- Save and Restore:
	- Snapshot and restore groups of PVs
	- Supports scaling and merging snapshots where needed
- ChannelFinder clients:
	- Fast PV search with metadata (IOC host, record type, tags)
- PV utilities:
	- Probe, PV Table, PV Tree for operations and diagnostics

Source alignment note:
- This slide intentionally mirrors the thin MOCR002 applications slide content and naming.

Notes:
1. Keep this slide close to the source talk language.
2. Use this as the "what operators use daily" summary slide.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem details: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 11: Application Stack Diagram

Charge questions addressed: CQ4, CQ5, CQ8

Slide overview:
Visualize applications and shared platform foundation.

Slide 11:
- Primary visual: `presentations/examples/images/MOCR002_f2.png`
- Diagram highlights:
	- Phoebus applications tier over common core/core-UI
	- Shared data/value model and integration patterns
	- Consistent UX behavior enabled by shared framework components
	- Optional callout: map each application box to corresponding workflow step from Slide 10

Notes:
1. Keep explanation concise and visual-first.
2. Reinforce why shared foundation reduces long-term support cost.

## Slide 12: Architecture Fundamentals for UI Behavior

Charge questions addressed: CQ2, CQ5, CQ8

Slide overview:
Summarize architecture points from thin talk that matter directly to user-facing behavior.

Slide 12:
- Thin talk architecture anchors:
	- Java and JavaFX modular framework (no Eclipse RCP dependency)
	- Core modules for PV access, VTypes, adapters, jobs, logging
	- Core-UI modules for docking, menus, selection services
	- Job scheduling and processing off the UI thread for responsiveness
	- Connection management with pooled/reused PV and REST clients
	- VTypes as immutable values not tied to protocol memory layout
	- Formula-function pipelines for thread-safe data processing
- UI impact:
	- Responsive interfaces through background job handling
	- Stable data semantics through shared value model
	- Predictable integration across applications

Notes:
1. Keep this focused on user-visible outcomes rather than implementation detail.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)

## Slide 13: Extensibility and SPI Model

Charge questions addressed: CQ5, CQ8

Slide overview:
Explain how SPI supports controlled evolution of tools and integrations.

Slide 13:
- Thin talk anchors:
	- Extensible via Java SPI
	- New data sources/protocols (CA, PVA, MQTT, Tango), service clients, applications, UI extensions
- EIC implications:
	- Site-specific adaptation without forking core platform
	- Lower integration friction for future subsystem and workflow needs
	- Cleaner long-term maintainability path

Notes:
1. Keep this as architecture governance and evolution argument.
2. Mention protocol examples only as capability, not committed deployment scope.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- SPI architecture basis: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 14: Site-Specific Product Strategy for EIC

Charge questions addressed: CQ1, CQ5, CQ8

Slide overview:
Apply thin-talk product model to EIC delivery planning.

Slide 14:
- Thin talk anchors:
	- Assemble site-specific products from common framework
	- Include site adapters, data sources, configuration, branding
- EIC-specific interpretation:
	- Curated distribution per environment role (operations, development, commissioning)
	- Common baseline with controlled extensions by subsystem need
	- Consistent release and support posture across teams

Notes:
1. Keep this practical for delivery planning discussions.
2. Tie back to governance and configuration control practices.

## Slide 15: Collaboration and Contribution Model

Charge questions addressed: CQ1, CQ6, CQ8

Slide overview:
Show sustainability model based on active multi-site collaboration.

Slide 15:
- Thin talk anchors:
	- Multi-site collaboration across labs and facilities
	- Contribution through GitHub issues/PRs and recurring meetings
	- Collaboration scale signal: sustained PR and issue activity in source talk
- EIC relevance:
	- Access to broader expertise and shared maintenance burden
	- Better resilience against single-site knowledge concentration
	- Clear pathway for EIC contributions upstream where appropriate

Optional speaker notes from thin talk:
1. Monthly collaboration cadence targets the second Wednesday.
2. Encourage participation via issues, PRs, and codeathon/documentathon activity.

Notes:
1. Keep this concise and evidence-oriented.
2. Focus on sustainability and supportability outcomes.

## Slide 16: Readiness, Risks, and Open Questions

Charge questions addressed: CQ7, CQ8

Slide overview:
Summarize what is ready now and what remains before final-design closure.

Slide 16:
- Readiness indicators:
	- Application workflow model is coherent and source-backed
	- Core application set and architecture direction are defined
	- Desktop and web usage patterns are established
- Remaining work:
	- Complete formal performance characterization under representative load
	- Finalize subsystem rollout priorities and acceptance evidence
	- Close any unresolved interface and operational ownership items
- Discussion prompts:
	- Are boundaries of the application scope acceptable for this phase?
	- Which workflows need deeper review before final design?

Notes:
1. Keep this balanced: clear progress plus explicit open items.

## Slide 17: References

Charge questions addressed: CQ2, CQ5

Slide overview:
Consolidated references for all claims used in this presentation.

Slide 17:
- Primary source talk: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Phoebus ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Controls software requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)
- EPICS controls baseline decision: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)
- Phoebus tools/services decision: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

Notes:
1. Keep all technical statements traceable to these references.

## Appendix Slide A1: Service Context Overview (Optional)

Charge questions addressed: CQ2, CQ5

Slide overview:
Optional service context slide moved out of main narrative per presentation focus.

Slide A1:
- EPICS services used by applications:
	- Archiver, ChannelFinder, Save/Restore, Olog, Alarm
- Why in appendix:
	- Main talk stays application and UI focused
	- Service deployment details are available for deep-dive discussion

## Appendix Slide A2: Alarm and Discovery Services (Optional)

Charge questions addressed: CQ4, CQ7

Slide overview:
Optional detail slide for alarm/discovery backend capabilities.

Slide A2:
- Alarm Server, Alarm Logger, Alarm Configuration Manager roles
- ChannelFinder metadata/discovery role
- Relationship to operator workflow and response quality

## Appendix Slide A3: Persistence and Logging Services (Optional)

Charge questions addressed: CQ4, CQ5

Slide overview:
Optional detail slide for save/restore, logbook, and archive internals.

Slide A3:
- Save/Restore persistence and API model
- Olog backend options and client access paths
- Archiver backend choices and deployment notes
- Optional visual: `presentations/examples/images/MOCR002_f3.png` (logbook SPI pattern)

Notes:
1. Include these only if the review panel asks for service-level depth in this session.

## Appendix Slide A4: Thin MOCR002 Crosswalk (Build Guide)

Charge questions addressed: CQ5

Slide overview:
Fast mapping from this outline to the source thin talk for slide construction.

Slide A4:
- Outline Slide 5  -> thin Slide 3/4 (ecosystem and CS-Studio/Phoebus context)
- Outline Slide 7  -> thin Slide 5 (Display Builder)
- Outline Slide 8  -> thin Slide 7/8 (web runtime and converted screens)
- Outline Slide 9  -> thin Slide 9 (Data Browser)
- Outline Slide 10 -> thin Slide 10 (applications portfolio)
- Outline Slide 11 -> thin Slide 16/17 + MOCR002_f2 (architecture/app stack framing)
- Outline Slide 12 -> thin Slide 16/17/29/30 (core architecture, VTypes, formula/jobs)
- Outline Slide 13 -> thin Slide 18 (SPI extensibility)
- Outline Slide 14 -> thin Slide 19 (site-specific products)
- Outline Slide 15 -> thin Slide 2/21/22/23/24 (collaboration and contribution)

Notes:
1. Use this crosswalk when drafting final PPT slides to preserve the source talk feel.
2. Keep service-heavy thin slides (11-15, 26-28) in appendix unless requested live.

## Appendix Slide A5: Collaboration Links (Optional)

Charge questions addressed: CQ5

Slide overview:
Optional practical links from the source talk for participation and support.

Slide A5:
- Phoebus portal: http://phoebus.org
- ControlSystemStudio GitHub org: https://github.com/ControlSystemStudio
- ChannelFinder project: http://channelfinder.github.io/
- Olog project: https://github.com/Olog
- Phoebus services path: https://github.com/ControlSystemStudio/phoebus/tree/master/services

Notes:
1. Keep this appendix slide optional unless contribution/process questions come up live.
