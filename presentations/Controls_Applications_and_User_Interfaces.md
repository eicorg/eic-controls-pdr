## Slide 1: Controls Applications and User Interfaces

Charge questions addressed: CQ7 (design maturity readiness framing)

Slide overview:
Establish review context for applications and user interfaces, using the thin MOCR002 talk flow adapted for EIC PDR.

Slide 1:
- **Title: Controls Applications and User Interfaces**
- **Subtitle: EIC Controls PDR Applications and Operator Workflow Review**
- **Presenter block: team, date, review body**
- **Purpose statement:**
	Present the baseline operator toolkit, integrated user workflows, and implementation readiness for controls applications.

Notes:
1. This outline is adapted from the thin MOCR002 talk and the extracted MOCR002 paper text, with PDR framing added for review traceability.
2. The emphasis is applications, operator workflows, and the user-visible service model; deeper service detail is pushed to appendix slides.
3. This phase demonstrates architecture maturity and workflow coherence, not final verification closure.

Detailed references appear in technical slides where they are used.

## Slide 2: Charge Questions

Charge questions addressed: CQ1-CQ7 (definition and scope of all charge questions)

Slide overview:
Frame review criteria and what this applications/UI talk addresses in the current phase.

Slide 2:
- **CQ1: Are the system requirements sufficiently defined, understood, and documented for this phase of the design?**
- **CQ2: Do the designs meet the requirements?**
- **CQ3: Are the interfaces sufficiently defined, understood and documented for this phase of the design?**
- **CQ4: Are the design analysis, simulations, drawings and specifications, and work plans, sufficient for this phase of the design?**
- **CQ5: Have technical risks been identified and are mitigation plans adequate for this phase of the design?**
- **CQ6: Are plans to address ES&H and Quality sufficient for this phase of the design?**
- **CQ7: Is the overall design maturity sufficient to proceed with the final design phase?**

## Slide 3: Outline of the Talk

Charge questions addressed: CQ7 (overall maturity roadmap)

Slide overview:

Slide 3:
- **Scope**
- **Phoebus in the EPICS controls ecosystem**
- **Application workflow: Display Builder, web runtime, Data Browser, Alarm UI**
- **Applications portfolio: Logbook, Save & Restore, ChannelFinder, PV utilities**
- **Middle-layer services and service/application stack**
- **Architecture fundamentals and under-the-hood behavior**
- **Extensibility (SPI) and site-specific product model for EIC**
- **Collaboration, contribution model, and useful links**
- **Open questions and appendix service details (only if requested)**

Notes:
1. Main body focuses on applications and user interfaces.
2. Service-depth slides are intentionally placed at the end as appendix material.

## Slide 4: Scope

Charge questions addressed: CQ1, CQ3, CQ4, CQ7

Slide overview:
Define what is in and out of scope for this presentation, and where the source talk has been condensed.

Slide 4:
- **In scope:**
	- **Operator-facing applications and user workflow integration**
	- **Phoebus middle-layer services only at the level needed to explain UI behavior and operator workflows**
	- **Desktop and web runtime usage patterns**
	- **Architecture decisions that directly impact UI/application behavior**
	- **Requirements traceability for operator interface capabilities**
- **Out of scope for main narrative:**
	- **Detailed service deployment and operations internals (appendix)**
	- **Full performance verification closure**
	- **Final implementation sizing and operational readiness evidence**

## Slide 5: Phoebus in the EPICS Controls Ecosystem

Charge questions addressed: CQ1, CQ3, CQ7

Slide overview:
Introduce Phoebus using the MOCR002 paper's three-part definition and ecosystem diagram, establishing its role as the operator application and service platform layer for EIC.
Slide 5:
- **Primary visual: presentations/examples/images/MOCR002_f1.png**
- **Phoebus is simultaneously three things:**
- **An operator-facing toolkit: Display Builder, Data Browser, Alarm UI, Logbook, Save/Restore, ChannelFinder client, PV utilities**
- **A group of middle-layer microservices: Archiver Appliance, Alarm Server/Logger, Olog, ChannelFinder, Save/Restore service, PVA Gateway**
- **A framework for building site-specific tools and services via Java SPI extensibility**
- **Successor to Control System Studio (CS-Studio): replaces Eclipse RCP with a modular Java and JavaFX architecture — no platform lock-in, cleaner modularity, and modern toolchain support**
- **Selection and Adapter services propagate context automatically: PV names, values, timestamps, alarm states, archive sources, log entries, and screen locations flow between applications without manual re-entry**
- **Integrated workflows span the full operator day: alarm detection → trend investigation → display navigation → logbook capture, all within one environment**
- **Broad multi-lab adoption across the EPICS community (ORNL, BNL, ESS, DESY, FNAL, and others) with active collaboration via monthly meetings, GitHub issues/PRs, and shared codeathon activity**
- **One coherent user experience for EIC across commissioning, operations, and post-mortem analysis workflows**
Notes:
1. Use the MOCR002 three-part definition verbatim as an anchor: toolkit / services / framework. This matches the source talk structure exactly.
2. Emphasize that the Selection and Adapter framework is what makes Phoebus more than a collection of tools — it is an integrated environment.
3. Tie multi-lab adoption claim to the collaboration statistics cited in Slide 15.
4. The ecosystem diagram (MOCR002_f1) visually shows applications, services, and the shared core/core-UI foundation — reference it directly on the slide.
References:
- Phoebus ecosystem paper (primary source): [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 6: Display Builder Strategy

Charge questions addressed: CQ2, CQ3, CQ4

Slide overview:
How Display Builder supports reusable synoptic UI development and runtime use, using the source talk’s editor/runtime split.

Slide 6:
- **Display Builder editor and runtime**
- **Reusable widgets and parameterized displays**
- **Live process data with metadata, alarm awareness, units, and precision**
- **Version-controlled `.bob` screen assets for consistent operations**
- **Advanced customization through properties and scripting**
- **Auto-conversion from legacy EDM, MEDM, and BOY displays with minimal adjustments**
- **Supports OPI requirement intent for reusable controls, navigation, and service integration**

Notes:
1. Keep this practical and operator-centric.
2. Emphasize maintainability and repeatability over tool branding.

References:
- Requirements authority (OPI scope): [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)

## Slide 7: Web Runtime and Remote Operations

Charge questions addressed: CQ3, CQ4, CQ6

Slide overview:
Show how web access complements desktop operations and supports remote access, matching the source deck’s web-runtime slides.

Slide 7:
- **Phoebus on the web**
- **`.bob` files converted to web runtime OPIs**
- **Converted screens with improved generation workflow for maintainability**
- **Help support remote operations by bringing OPI screens to the web**
- **Remote visibility and role-appropriate access outside main control consoles**
- **Same display assets reused across desktop and web contexts**
- **Reduced duplication in UI maintenance**
- **Web runtime is complementary to the desktop toolkit, not a replacement**
- **Converted-screen tooling stays source-driven so one screen asset serves both runtimes**
- **`phoebusgen` / `autogen` cited as examples, not a committed toolchain**

Notes:
1. Position web tools as complementary, not replacement for operator desktops.
2. Keep security boundary details at architecture level in this talk.

## Slide 8: Data Browser Workflow

Charge questions addressed: CQ2, CQ3, CQ5

Slide overview:
Trend and history access as a core operator diagnostic capability, with the source deck’s emphasis on archive backends and unified plotting.

Slide 8:
- **Data Browser for PV history access**
- **Fast shift from live alarm/event to historical trend context**
- **Cross-channel correlation for diagnosis and post-mortem analysis**
- **Workflow continuity with display, alarm, and logbook tools**
- **Supports multiple archive providers through SPI-based integration, including EPICS Archiver Appliance and RDB / TimescaleDB-backed stores**
- **Presents live and historical data in one plotting environment**

Notes:
1. Connect this slide to operational risk reduction and troubleshooting speed.
2. Keep performance claims qualitative unless a verified metric is cited.

## Slide 9: Alarm UI Workflow

Charge questions addressed: CQ2, CQ3, CQ5

Slide overview:
Show alarm monitoring and response workflow as a first-class operator function before the broader applications portfolio.

Slide 9:
- **Alarm UI with hierarchical alarm trees, active alarm tables, and annunciator behavior**
- **Alarm clients include tree, table, panel, and alarm history views**
- **Fast detection of new, pending, and acknowledged alarms with severity and timestamp context**
- **Direct transition from alarm context to Data Browser, displays, and logbook actions**
- **Alarm history supports post-mortem review and alarm-quality tuning**
- **Supports operator response quality and reduces troubleshooting latency during commissioning and operations**

Notes:
1. Keep this operator-UI focused; service internals remain in appendix slides.
2. Align terminology with thin talk wording: alarm tree/table/panel/history and annunciator.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 10: Applications Portfolio (User Workflow View)

Charge questions addressed: CQ2, CQ3, CQ4

Slide overview:
Consolidated application view matching the source deck’s application slide content and terminology.

Slide 10:
- **Logbook:**
	- **Integrated operator logging with context capture**
	- **Backend-agnostic model (Olog/elog and site-specific variants)**
- **Save and Restore:**
	- **Snapshot and restore groups of PVs**
	- **Supports scaling and merging snapshots where needed**
- **ChannelFinder clients:**
	- **Fast PV search with metadata (IOC host, record type, tags)**
	- **Search is case-insensitive in the source talk’s wording**
- **PV utilities:**
	- **Probe, PV Table, PV Tree for operations and diagnostics**

Notes:
1. Keep this slide close to the source talk language.
2. Use this as the "what operators use daily" summary slide.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem details: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 11: Application Stack Diagram

Charge questions addressed: CQ3, CQ4, CQ7

Slide overview:
Visualize applications and shared platform foundation, aligning with the source deck’s application/service stack diagram.

Slide 11:
- **Primary visual: `presentations/examples/images/MOCR002_f2.png`**
- **Diagram highlights:**
	- **Phoebus applications tier over common core/core-UI**
	- **Middle-layer services sit alongside the applications tier in the broader ecosystem**
	- **Shared data/value model and integration patterns**
	- **Consistent UX behavior enabled by shared framework components**
	- **Optional callout: map each application box to the workflow step from Slide 10**

Notes:
1. Keep explanation concise and visual-first.
2. Reinforce why shared foundation reduces long-term support cost.

## Slide 12: Architecture Fundamentals for UI Behavior

Charge questions addressed: CQ1, CQ4, CQ7

Slide overview:
Summarize the architecture points from the thin talk that matter directly to user-facing behavior, while keeping the source’s service model in view.

Slide 12:
- **Java and JavaFX modular framework (no Eclipse RCP dependency)**
- **Core modules for PV access, VTypes, adapters, jobs, logging, and configuration**
- **Core-UI modules for docking, menus, selection services, and toolbars**
- **Job scheduling and processing off the UI thread for responsiveness**
- **Connection management with pooled/reused PV and REST clients**
- **VTypes as immutable values not tied to protocol memory layout**
- **Formula-function pipelines for thread-safe data processing**
- **Product as an assembled distribution of common modules, applications, and service clients**
- **Modular microservices extending EPICS with scalability, resilience, and maintainability**
- **Spring Boot baseline for many services, with specialized implementations where needed**
- **CI/CD, containerization, and observability in the deployment model**
- **Responsive interfaces, stable data semantics, and predictable cross-application integration**

Notes:
1. Keep this focused on user-visible outcomes rather than implementation detail.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)

## Slide 13: Extensibility and SPI Model

Charge questions addressed: CQ4, CQ7

Slide overview:
Explain how SPI supports controlled evolution of tools and integrations, using the source deck’s application, data-source, and UI extension examples.

Slide 13:
- **Extensible via Java SPI**
- **New data sources/protocols (CA, PVA, MQTT, Tango), service clients, applications, file handlers, and UI extensions**
- **Site-specific adaptation without forking core platform**
- **Lower integration friction for future subsystem and workflow needs**
- **Cleaner long-term maintainability path**
- **New functionality added through well-defined contracts instead of ad hoc coupling**

Notes:
1. Keep this as architecture governance and evolution argument.
2. Mention protocol examples only as capability, not committed deployment scope.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- SPI architecture basis: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 14: Site-Specific Product Strategy for EIC

Charge questions addressed: CQ4, CQ7

Slide overview:
Apply the thin-talk product model to EIC delivery planning.

Slide 14:
- **Assemble site-specific products from a common framework**
- **Include site adapters, data sources, configuration, and branding**
- **Curated distribution per environment role (operations, development, commissioning)**
- **Common baseline with controlled extensions by subsystem need**
- **Consistent release and support posture across teams**
- **Site-specific products assembled from shared framework pieces rather than forks**
- **Product composition, default preferences, icons, and menus treated as configuration inputs**

Notes:
1. Keep this practical for delivery planning discussions.
2. Tie back to governance and configuration control practices.

## Slide 15: Collaboration and Contribution Model

Charge questions addressed: CQ6, CQ7

Slide overview:
Show the sustainability model based on active multi-site collaboration, as presented in the source deck’s collaboration slides.

Slide 15:
- **Multi-site collaboration across labs and facilities**
- **Contribution through GitHub issues/PRs and recurring meetings**
- **Collaboration scale signal: sustained PR and issue activity in source talk**
- **Thin talk cites roughly 300 PRs and 100 issues in Phoebus, with related activity in ChannelFinder and Phoebus-Olog**
- **Access to broader expertise and shared maintenance burden**
- **Better resilience against single-site knowledge concentration**
- **Clear pathway for EIC contributions upstream where appropriate**
- **Monthly collaboration cadence targets the second Wednesday**
- **Participation via issues, PRs, and codeathon/documentathon activity**

Notes:
1. Keep this concise and evidence-oriented.
2. Focus on sustainability and supportability outcomes.

## Slide 16: Readiness, Risks, and Open Questions

Charge questions addressed: CQ5, CQ7

Slide overview:
Summarize what is ready now and what remains before final-design closure, while preserving the source deck’s concluding discussion posture.

Slide 16:
- **Application workflow model is coherent and source-backed**
- **Core application set, middle-layer service model, and architecture direction are defined**
- **Desktop and web usage patterns are established**
- **Complete formal performance characterization under representative load**
- **Finalize subsystem rollout priorities and acceptance evidence**
- **Close unresolved interface and operational ownership items**
- **Validate web-runtime and service assumptions against EIC-specific rollout plans**
- **Are boundaries of the application scope acceptable for this phase?**
- **Which workflows need deeper review before final design?**
- **Which source talk elements stay in the main body versus appendix for the final slide deck?**

Notes:
1. Keep this balanced: clear progress plus explicit open items.
2. The source deck closes with a questions slide; this PDR version keeps the same discussion intent while adding readiness framing.

## Slide 17: References

Charge questions addressed: CQ1, CQ4

Slide overview:
Consolidated references for all claims used in this presentation, including the source deck and extracted paper text.

Slide 17:
- **Primary source talk: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)**
- **Phoebus ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)**
- **Controls software requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)**
- **EPICS controls baseline decision: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)**
- **Phoebus tools/services decision: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)**
- **GitHub governance context: [rod/EIC-ROD-GitHub-Platform.md](../rod/EIC-ROD-GitHub-Platform.md)**

Notes:
1. Keep all technical statements traceable to these references.

## Appendix Slide A1: Alarm and Discovery Services (Optional)

Charge questions addressed: CQ3, CQ5

Slide overview:
Optional detail slide for the alarm and discovery backend capabilities that the source deck keeps for service-depth discussion.

Slide A1:
- **Alarm Server, Alarm Logger, Alarm Configuration Manager roles**
- **ChannelFinder metadata/discovery role**
- **Relationship to operator workflow and response quality**

## Appendix Slide A2: Persistence and Logging Services (Optional)

Charge questions addressed: CQ3, CQ4

Slide overview:
Optional detail slide for save/restore, logbook, and archive internals.

Slide A2:
- **Save/Restore persistence and API model**
- **Olog backend options and client access paths**
- **Archiver backend choices and deployment notes**
- **Relationship to operator workflow and response quality**

## Appendix Slide A3: VTypes: Type Definitions (Optional)

Charge questions addressed: CQ4

Slide overview:
Optional detail slide for the source deck’s VTypes discussion.

Slide A3:
- **Java interfaces for values**
- **Not tied to protocol or implementation (database, EPICS protocol, file, etc.)**
- **Not tied to memory representation; can be read from the network buffer or lazily calculated**
- **Immutable and safe to read/share**

## Appendix Slide A4: Formula Functions and Threading (Optional)

Charge questions addressed: CQ4

Slide overview:
Optional detail slide for the source deck’s formula pipeline and threading model.

Slide A4:
- **Efficient way to support data processing**
- **No scripts and rules**
- **Data processing happening off the UI thread**
- **Thread-safe access to data**
- **Connection management supporting shared access patterns**

Notes:
1. Include these only if the review panel asks for service-level depth in this session.

## Appendix Slide A5: Collaboration Links (Optional)

Charge questions addressed: CQ4

Slide overview:
Optional practical links from the source talk for participation and support.

Slide A5:
- **Phoebus portal: http://phoebus.org**
- **ControlSystemStudio GitHub org: https://github.com/ControlSystemStudio**
- **ChannelFinder project: http://channelfinder.github.io/**
- **Olog project: https://github.com/Olog**
- **Phoebus services path: https://github.com/ControlSystemStudio/phoebus/tree/master/services**

Notes:
1. Keep this appendix slide optional unless contribution/process questions come up live.
