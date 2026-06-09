## Slide 1: Controls Applications and User Interfaces

Charge questions addressed: CQ7 (design maturity readiness framing)

Slide overview:
Establish the speaker, session context, and scope for application-layer and operator-interface content.

Slide 1:
- **Application Layer & Operator Interfaces**
- **Kunal Shroff**
- **Software Technical Lead**
- **Accelerator Controls Global Software, Networking & Computing PDR**
- **June 15-17, 2026**

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

## Slide 3: Outline

Charge questions addressed: CQ7 (overall maturity roadmap)

Slide overview:
Presentation roadmap for scope, requirements, applications, architecture, risks, and path forward.

Slide 3:
- **Scope**
- **Requirements**
- **Phoebus**
- **Phoebus applications**
- **Display Builder**
- **Databrowser**
- **Alarm Applications**
- **Logging**
- **Phoebus Architecture**
- **Risks**
- **Path Forward**
- **Summary**

Notes:
1. Main body focuses on applications and user interfaces.
2. Service-depth slides are intentionally placed at the end as appendix material.

## Slide 4: Scope

Charge questions addressed: CQ1, CQ3, CQ4, CQ7

Slide overview:
Define what is in and out of scope for this presentation, and where the source talk has been condensed.

Slide 4:
- **User-facing tools for control system operation**
- **Focus on applications used to monitor, operate, diagnose, and document large-scale control systems**
- **Phoebus as the primary application environment**
- **Cover the integrated Phoebus toolkit, including displays, alarms, archiving, logging, PV tools, and save/restore workflows**
- **Client libraries beyond Phoebus**
- **Include libraries that bring control system access into other environments and languages**
- **Integration with analysis and engineering workflows**
- **Discuss use from Python notebooks, MATLAB applications, scripts, and custom tools**
- **Common goal**
- **Provide flexible, connected interfaces for users to interact with the control system in the environment that best fits their task**

## Slide 5: Requirements

Charge questions addressed: CQ1, CQ3, CQ7

Slide overview:
Reference the PRD sources that anchor requirements for this presentation phase.
Slide 5:
- **Initial versions of the Performance Requirements Documents (PRDs)**
- **High Level Applications [EIC-SEG-RSI-158]**
- **Networking & Computing [EIC-SEG-RSI-XXX]**
Notes:
1. Use the MOCR002 three-part definition verbatim as an anchor: toolkit / services / framework. This matches the source talk structure exactly.
2. Emphasize that the Selection and Adapter framework is what makes Phoebus more than a collection of tools — it is an integrated environment.
3. Tie multi-lab adoption claim to the collaboration statistics cited in Slide 15.
4. The ecosystem diagram (MOCR002_f1) visually shows applications, services, and the shared core/core-UI foundation — reference it directly on the slide.
References:
- Phoebus ecosystem paper (primary source): [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 6: Control System Architecture

Charge questions addressed: CQ2, CQ3, CQ4

Slide overview:
Show the three-layer controls architecture context: operator/applications, middle-layer services, and control system.

Slide 6:
- **Control System Architecture**
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Keep this practical and operator-centric.
2. Emphasize maintainability and repeatability over tool branding.

References:
- Requirements authority (OPI scope): [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)

## Slide 7: Phoebus

Charge questions addressed: CQ3, CQ4, CQ6

Slide overview:
Describe Phoebus as the integrated operator toolkit and application framework.

Slide 7:
- **Phoebus**
- **Rich client toolkit for control system applications**
- **A collection of tools for monitoring, operating, and troubleshooting large-scale control systems**
- **Provides a unified desktop environment for operators, engineers, and developers**
- **Integrated application framework**
- **Combines displays, alarms, archiving, logging, PV tools, and save/restore workflows**
- **Enables applications to share data and operational context automatically**
- **Seamless cross-application workflows**
- **PV names, values, timestamps, alarm states, archive sources, displays, and logbook entries can move from one tool to another**
- **Operators can move naturally from alarm investigation, to historical data, to device displays, to logbook documentation**
- **Consistent and extensible user experience**
- **Shared UI patterns, menus, selections, and context handling reduce operator effort**
- **Applications interoperate through well-defined interfaces without tight coupling**
- **Scalable, sustainable, and collaborative platform**
- **Supports modern Java LTS releases, containerized deployment, CI/CD workflows, and microservice-based infrastructure**
- **Developed collaboratively by facilities worldwide as an open ecosystem for control system tools**

Notes:
1. Position web tools as complementary, not replacement for operator desktops.
2. Keep security boundary details at architecture level in this talk.

## Slide 8: Display Builder

Charge questions addressed: CQ2, CQ3, CQ5

Slide overview:
Introduce Display Builder at a high level (editor and runtime views).

Slide 8:
- **Display Builder**
- **editor**
- **runtime**

Notes:
1. Connect this slide to operational risk reduction and troubleshooting speed.
2. Keep performance claims qualitative unless a verified metric is cited.

## Slide 9: Display Builder - Editor

Charge questions addressed: CQ2, CQ3, CQ5

Slide overview:
Detail Display Builder editor capabilities and screen authoring features.

Slide 9:
- **Display Builder - editor**
- **WYSIWYG editor**
- **Large Pallet of widgets**
- **Control System Aware**
- **Advanced customization through properties and scripting**
- **Resuable widgets/groups/screens**
- **Simple file format**

Notes:
1. Keep this operator-UI focused; service internals remain in appendix slides.
2. Align terminology with thin talk wording: alarm tree/table/panel/history and annunciator.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 10: Display Builder - Runtime

Charge questions addressed: CQ2, CQ3, CQ4

Slide overview:
Show runtime behavior for live process data with metadata and alarm awareness.

Slide 10:
- **Display Builder - runtime**
- **Live process data with metadata, alarm awareness, units, and precision**

Notes:
1. Keep this slide close to the source talk language.
2. Use this as the "what operators use daily" summary slide.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem details: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 11: Web Runtime and Remote Operations

Charge questions addressed: CQ3, CQ4, CQ7

Slide overview:
Show how OPI screens are brought to web runtime to support remote operations.

Slide 11:
- **Web Runtime and Remote Operations**
- **Help support remote operations by bringing OPI screens to the web**
- **.bob files converted to web runtime OPI's**

Notes:
1. Keep this visual-first and use it as the transition into architecture internals.
2. Focus on how the diagram explains operator workflow continuity and supportability.

## Slide 12: Screen Creation

Charge questions addressed: CQ1, CQ4, CQ7

Slide overview:
Placeholder slide for screen creation examples/workflow.

Slide 12:
- **Screen creation**

Notes:
1. Keep this centered on user-visible behavior rather than service deployment internals.
2. Use Slide 11 diagram callouts to anchor each architecture point.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem paper extract: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 13: Data Browser

Charge questions addressed: CQ4, CQ7

Slide overview:
Present Data Browser capabilities for live/historical plotting and correlation analysis.

Slide 13:
- **Data Browser**
- **Presents live and historical data in one plotting environment**
- **Cross-channel correlation for diagnosis and post-mortem analysis**
- **Data export and inspection**
- **Optimized retrieval**
- **Workflow continuity with display, alarm, and logbook tools**
- **Supports multiple archive providers**

Notes:
1. Keep this as architecture governance and evolution argument.
2. Mention protocol examples only as capability, not committed deployment scope.

References:
- Thin talk source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- SPI architecture basis: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 14: Alarm Applications

Charge questions addressed: CQ4, CQ7

Slide overview:
State alarm application goals for response quality and alarm-server configuration management.

Slide 14:
- **Alarm Applications**
- **Goals**
- **Support operator response quality and reduces troubleshooting latency during commissioning and operations**
- **support configuration and management of Alarm Server behavior (alarm hierarchy, limits, and annunciation rules)**

Notes:
1. Keep this practical for delivery planning discussions.
2. Tie back to governance and configuration control practices.

## Slide 15: Alarm Applications (Client Views)

Charge questions addressed: CQ6, CQ7

Slide overview:
Describe alarm client views (tree, table, panel, annunciator, history) used in operations.

Slide 15:
- **Alarm Applications**
- **Alarm clients include**
- **Tree**
- **Organized hierarchical view of alarms**
- **Table**
- **Fast detection of new, pending, and acknowledged alarms with severity and timestamp context**
- **Panel**
- **Annunciator**
- **Alarm history**
- **supports post-mortem review and alarm-quality tuning**

Notes:
1. Keep this concise and evidence-oriented.
2. Focus on sustainability and supportability outcomes.

## Slide 16: Save and Restore

Charge questions addressed: CQ5, CQ7

Slide overview:
Present Save & Restore workflows for configurations, snapshots, and logbook integration.

Slide 16:
- **Save and Restore**
- **Save & Restore**
- **Organized representation of Configurations and Snapshots**
- **Interface to live, archived, and snapshot data**
- **Integration with logbook**

Notes:
1. Keep this balanced: clear progress plus explicit open items.
2. The source deck closes with a questions slide; this PDR version keeps the same discussion intent while adding readiness framing.

## Slide 17: Logbook

Charge questions addressed: CQ1, CQ4

Slide overview:
Present logbook usage for documenting operations with automatic context capture and web access.

Slide 17:
- **Logbook**
- **Enable users to create and retrieve log entries which document EIC operations, observations, and events.**
- **Phoebus clients**
- **Automatic context capture: Log entries are pre-populated from the active application state.**
- **Web clients**
- **Easy access for quick entry and review**

Notes:
1. Keep all technical statements traceable to these references.

## Slide 18: Applications Portfolio

Slide overview:
Summarize Channel Finder and PV utilities used for search, introspection, and linkage diagnostics.

Slide 18:
- **Channel Finder Clients - fast PV search enriched with metadata (IOC host, record type, tags)**
- **PV Utilities**
	- **Probe: detailed PV introspection**
	- **PV Table: monitor/save groups of PVs**
	- **PV Tree: visualize EPICS record linkages**

## Slide 19: Commissioning tools

Charge questions addressed: CQ1, CQ3, CQ4, CQ7

Slide overview:
Describe commissioning application scope and current delivery strategy: infrastructure-first, with tool requirements still being collected and shared client libraries being developed.

Slide 19:
- **Commissioning tools**
- **Commissioning tools infrastructure**
	- **Requirements for individual commissioning tools are still being collected and refined**
	- **Primary near-term focus is infrastructure/framework needed to build and integrate these tools**
	- **Python and Java client libraries are in development for controls-system and middle-layer service access**
- **Automated Tuning and Scans**
	- **Model-assisted scans, optimization loops, and scripted recovery/tuning workflows (HLA.1, HLA.2)**
- **Beam Diagnostics and Optics Correction**
	- **Orbit, tune, trajectory, and optics correction using BPM and response-matrix methods**
- **RF and Timing Commissioning**
	- **Phase alignment, timing synchronization, LLRF validation, and injection timing tools (HLA.3)**
- **Configuration and State Control**
	- **Save/Restore snapshots, versioned settings, and controlled rollback during machine studies**
- **Operational Traceability**
	- **Electronic logbooks, alarm/event correlation, and archiver-backed post-mortem analysis**
- **Model-Based Commissioning**
	- **Online model integration (virtual accelerator / digital twin style) to reduce machine time and risk (HLA.4)**

Notes:
1. Keep this slide physics-commissioning focused and exclude installation workflow tooling.
2. Be explicit that requirements capture is in progress; this slide shows direction and enabling framework.
3. Emphasize shared Python/Java client libraries as the foundation for faster tool delivery.
4. All workflows align with EPICS/PVA and EIC-SEG-RSI-158 HLA requirements (Table 4-2).

References:
- HLA requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)
- EPICS software framework moves from controls to physics (paper): [presentations/raw/commissioning-tools/tuzzplm3.pdf](raw/commissioning-tools/tuzzplm3.pdf)
- EPICS software framework moves from controls to physics (talk): [presentations/raw/commissioning-tools/tuzzplm3_talk.pdf](raw/commissioning-tools/tuzzplm3_talk.pdf)
- High-level physics controls applications for FRIB (phantasy): [presentations/raw/commissioning-tools/tucpr07.pdf](raw/commissioning-tools/tucpr07.pdf)
- EPICS decision baseline: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)

## Slide 20: Phoebus Architecture

Slide overview:
Describe core Phoebus architecture modules, runtime behavior, and data model foundations.

Slide 20:
- **Modular framework - built on Java + JavaFX (no Eclipse RCP)**
- **Core modules: PV access, VTypes, adapters, logging, jobs**
- **Core-UI modules: docking, menus, selection services**
- **Applications: operator-facing tools (Display Builder, Data Browser, etc.)**
- **Jobs & scheduling - run tasks off the UI thread for responsiveness**
- **Connection management - pooled, reusable PV and REST clients**
- **VTypes - canonical value model**
	- **Protocol-agnostic, not tied to memory layout**
	- **Immutable and safe to share**
- **Formula functions - efficient, thread-safe data processing pipelines**

## Slide 21: Phoebus Architecture - Extensibility

Slide overview:
Describe Java SPI-based extensibility for protocols, service clients, applications, and UI extensions.

Slide 21:
- **Extensible via Java SPI (Service Provider Interface)**
- **New data sources & protocols (CA, PVA, MQTT, Tango, ...)**
- **Clients for middle-layer services (Olog, elog, ...)**
- **New applications**
- **UI extensions (menus, toolbars, context menus)**

## Slide 22: Phoebus Architecture - eic product

Slide overview:
Define site-specific EIC product composition: applications, datasources, configurations, branding, and adapters.

Slide 22:
- **EIC phoebus product includes site specific**
- **Applications**
- **Datasources**
- **Configurations**
- **Branding**
- **Adapters**
- **Address the needs of a particular organization or workflow.**

## Slide 23: Phoebus Collaboration

Slide overview:
Show collaboration scale and activity across facilities maintaining the Phoebus ecosystem.

Slide 23:
- **An international collaboration of dozens of research facilites**
- **Phoebus**
- **~300 PR's**
- **~100 Issue**

## Slide 24: Risks

Slide overview:
Capture key technology-evolution risk and mitigation strategy.

Slide 24:
- **Risk RT-6-007-001**
- **Mitigation: modular, extensible framework enables targeted upgrades with minimized disruption**
- **Mitigation: multi-lab collaboration spreads maintenance risk and improves response speed to technology changes**

## Slide 25: Path forward

Slide overview:
State the forward plan from the applications/UI architecture perspective.

Slide 25:
- **Path forward**

## Slide 26: Summary

Slide overview:
Close the talk with a concise summary slide.

Slide 26:
- **Phoebus is the primary application environment for EIC operator workflows, with integrated tools for control, diagnostics, and documentation**
- **Display Builder, Web Runtime, and Data Browser provide a practical path from screen creation to remote operations and post-event analysis**
- **Alarm, Save/Restore, and Logbook workflows improve operational response quality, repeatability, and traceability**
- **ChannelFinder and PV utilities strengthen day-to-day usability through fast discovery, metadata context, and diagnostics support**
- **A modular Java/JavaFX architecture with SPI extensibility supports long-term maintainability and site-specific product composition**
- **Active multi-lab collaboration and targeted risk mitigations position the applications stack for final-design progression**

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


