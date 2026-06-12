## Slide 1: Controls Applications and User Interfaces

Charge questions addressed: CQ7 (readiness framing)

Slide overview:
Title slide and session context for the applications/operator-interface scope.

Slide 1:
- **Application Layer & Operator Interfaces**
- **Kunal Shroff**
- **Software Technical Lead**
- **EIC Accelerator Controls Global Software, Networking & Computing PDR**
- **June 15-17, 2026**

Notes:
1. Frame this talk as application-layer architecture maturity for this review phase.
2. Emphasize user workflows, maintainability, and phased readiness.

Speaking notes:
This talk focuses on the application layer and operator interfaces for EIC controls. The goal is to show that the architecture, tooling model, and delivery approach are mature enough for this design phase. I will focus on operator workflows, technical integration boundaries, and readiness signals rather than claiming final deployment closure.

Detailed talking points:
- Position this talk as the user-facing half of the controls strategy: architecture decisions are only successful if operators and commissioning teams can execute consistently under load. State clearly that this is phase maturity evidence tied to delivery readiness, not a claim that every interface is production-final.
- Resource grounding: MOCR002 positions Phoebus as the successor to the Eclipse RCP era with a modular Java/JavaFX architecture designed for sustainable long-term operations.
## Slide 2: About Me - Kunal Shroff

Charge questions addressed: N/A (speaker context)

Slide overview:
Establish technical ownership and relevant experience behind the presented architecture.

Slide 2:
- **Controls Software Technical Lead for the Electron-Ion Collider (EIC) at Brookhaven National Laboratory**
- **Leads architecture and deployment strategy for controls software and operational services**
- **17 years of control systems software experience at large scientific facilities**
- **Technical lead of the EPICS Phoebus Collaboration**
- **Education: M.S. Electrical & Computer Engineering, Stony Brook University**
- **Technical focus: Controls Architecture, EPICS/Phoebus, Distributed Systems, DevOps/CI/CD/Infrastructure Automation**

Notes:
1. Keep this concise and connect background to architecture accountability.

Speaking notes:
I am responsible for controls software architecture and deployment strategy for EIC, and I also serve as technical lead for the EPICS Phoebus Collaboration. That combination lets me connect local EIC requirements with proven community practice and roadmap realities. The rest of this deck reflects that integration of project needs and collaboration-backed implementation patterns.

Detailed talking points:
- Use this slide to establish accountability: architecture ownership plus direct upstream collaboration participation means decisions are based on both EIC constraints and real deployment experience at other labs. This supports credibility when discussing migration, extensibility, and long-lifecycle maintenance.
- Resource grounding: The collaboration paper and ROD context support presenting technical ownership as a bridge between local EIC needs and multi-facility operational experience.
## Slide 3: Charge Questions

Charge questions addressed: CQ1-CQ7

Slide overview:
Define the review criteria that this presentation maps to.

Slide 3:
- **CQ1: Are the system requirements sufficiently defined, understood, and documented for this phase of the design?**
- **CQ2: Do the designs meet the requirements?**
- **CQ3: Are the interfaces sufficiently defined, understood and documented for this phase of the design?**
- **CQ4: Are the design analysis, simulations, drawings and specifications, and work plans, sufficient for this phase of the design?**
- **CQ5: Have technical risks been identified and are mitigation plans adequate for this phase of the design?**
- **CQ6: Are plans to address ES&H and Quality sufficient for this phase of the design?**
- **CQ7: Is the overall design maturity sufficient to proceed with the final design phase?**

Notes:
1. Use this as the anchor map for the rest of the talk.

Speaking notes:
These are the criteria used by the review panel, and each section in this presentation ties back to one or more of them. The emphasis is phase-appropriate design maturity with evidence and clear boundaries. I will call out requirement anchors, interface definitions, and risk mitigations as we move through the technical slides.

Detailed talking points:
- Briefly map your sections to CQ themes: requirements traceability (CQ1), functional fit and interfaces (CQ2/CQ3), implementation sufficiency (CQ4), risk handling (CQ5), and readiness (CQ7). Keep this under one minute and transition to evidence slides.
- Resource grounding: The ROD framework maps decisions, risks, and alternatives so CQ responses can reference explicit decision rationale rather than informal preference.
## Slide 4: Outline

Charge questions addressed: CQ7 (overall maturity roadmap)

Slide overview:
Roadmap for the applications and user-interface narrative.

Slide 4:
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
1. Sequence moves from scope and requirements to capabilities, architecture, and risk/readiness.

Speaking notes:
The flow starts with scope and requirements, then moves through the core operator toolkit and applications, and closes on architecture sustainability and risk posture. This order is intentional so the review can evaluate both user-facing functionality and the underlying maintainability model. The summary then ties back to readiness for final design progression.

Detailed talking points:
- Explain that the flow is intentional: start with requirement authority, then operator workflow tools, then architecture internals and risk posture. This helps the panel see that usability and maintainability are treated as coupled design objectives.
- Resource grounding: MOCR002 frames the same sequence used here: integrated toolkit experience first, then framework internals, then service and collaboration sustainment.
## Slide 5: Scope

Charge questions addressed: CQ1

Slide overview:
Define what is in scope for this applications/UI review.

Slide 5:
- **User-facing tools for control system operation**
- **Focus on applications used to monitor, operate, diagnose, and document large-scale control systems**
- **Phoebus as the primary application environment**
- **Integrated toolkit: displays, alarms, archiving, logging, PV tools, save/restore workflows**
- **Client libraries beyond Phoebus for other environments/languages**
- **Integration with analysis and engineering workflows (Python notebooks, MATLAB applications, scripts, custom tools)**
- **Common goal: flexible, connected interfaces aligned to task-specific user needs**

Notes:
1. Keep this slide practical and user-workflow focused.

Speaking notes:
Scope here is the application layer used day to day by operators and engineers. Phoebus is the primary environment, but we also include client-library access for analysis and engineering use cases outside the desktop toolkit. The design target is consistent workflow continuity across tools while preserving flexibility for different user contexts.

Detailed talking points:
- Call out the dual audience: control-room operators and engineering/physics users. Emphasize that Phoebus desktop is primary for integrated operations, while client-library access enables analysis workflows in Python and MATLAB without breaking control-system governance.
- Resource grounding: The Phoebus ROD explicitly defines operator workflows across displays, alarms, trends, logbook, and restore as the standardized operational scope.
## Slide 6: Requirements

Charge questions addressed: CQ1

Slide overview:
State the requirements sources that anchor this deck.

Slide 6:
- **Initial versions of Performance Requirements Documents (PRDs)**
- **High Level Applications [EIC-SEG-RSI-158]**
- **Networking & Computing [EIC-SEG-RSI-XXX]**

Notes:
1. Treat `EIC-SEG-RSI-158` as authoritative for controls software requirement claims.
2. Keep unverified performance statements explicitly labeled as assumptions.

References:
- Requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)

Speaking notes:
This slide anchors the talk in current requirements documentation. For application-layer requirements and performance expectations, `EIC-SEG-RSI-158` is the governing source. Where metrics are still being finalized or validated in integration environments, we treat statements as assumptions rather than as closed requirements evidence.

Detailed talking points:
- Anchor all requirement/performance language to `EIC-SEG-RSI-158`. Mention that this deck touches OPI, alarm, archive, save/restore, logbook, and HLA requirement families; demonstration-level closure remains a planned verification activity, not assumed complete.
- Resource grounding: RSI-158 table families cover OPI, ALRM, ARCH, DIR, SR, LOGBK, GW, and HLA capability domains referenced throughout this deck.
## Slide 7: Control System Architecture

Charge questions addressed: CQ1-CQ5

Slide overview:
Place application tooling in the full controls stack.

Slide 7:
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **[EIC-ROD-069]**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Keep boundaries clear: apps consume services; services integrate with control protocols.

References:
- EPICS baseline decision: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)
- Phoebus tools/services decision: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

Speaking notes:
This layered view shows where application responsibilities begin and end. Operator tools are intentionally separated from protocol and storage details through service interfaces, which supports maintainability and scaling. The architecture aligns with the EPICS and Phoebus decision records and keeps integration boundaries explicit.

Detailed talking points:
- Reinforce interface boundaries: operator applications consume middle-layer service contracts; services interface with EPICS/PVA and compatibility paths. This separation lowers coupling and supports phased evolution of storage and service implementations.
- Resource grounding: The EPICS ROD and Phoebus ROD jointly define boundaries: EPICS/PVA at controls layer and Phoebus/services at operator and middle layers.
## Slide 8: Phoebus

Charge questions addressed: CQ1-CQ5

Slide overview:
Describe Phoebus as the integrated operator toolkit and framework.

Slide 8:
- **Rich client toolkit for control system applications**
- **Unified desktop environment for operators, engineers, and developers**
- **Integrated framework combining displays, alarms, archiving, logging, PV tools, and save/restore**
- **Cross-application context sharing (PV names, values, timestamps, alarm states, archive sources, displays, logbook entries)**
- **Consistent/extensible UX with shared UI patterns and well-defined interfaces**
- **Scalable and collaborative platform supporting modern Java LTS, containerization, CI/CD workflows**

Notes:
1. Emphasize workflow continuity and operational efficiency rather than tooling catalog alone.

Speaking notes:
Phoebus is not just a set of separate applications; it is an integrated environment designed for continuous operational workflows. Operators can move from alarm response to trend analysis to display control to documentation without re-entering context. That reduces response latency and lowers training/support overhead while preserving extensibility.

Detailed talking points:
- Use concrete workflow continuity from the Phoebus ecosystem: alarm investigation -> data browser trend -> display interaction -> logbook entry with carried context. Tie this directly to OPI integration requirements such as `F-EIC-CTRL-SW-OPI.7` and operational efficiency goals.
- Resource grounding: MOCR002 details context propagation via selection and adapter services, including PVs, timestamps, alarm state, archive source, and display context.
## Slide 9: Display Builder

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Introduce Display Builder and its two operating modes.

Slide 9:
- **Display Builder**
- **editor**
- **runtime**

Notes:
1. Use this as transition from toolkit overview to concrete application behavior.

Speaking notes:
Display Builder is the core HMI authoring and execution path. The editor supports screen development and maintenance, while runtime is what operations uses in live control scenarios. The next two slides separate those concerns.

Detailed talking points:
- Frame Display Builder as the operational front door, with editor and runtime intentionally separated so teams can iterate displays without destabilizing operations. Keep transition crisp to the two follow-on slides.
- Resource grounding: MOCR002 treats Display Builder as a cornerstone application with shared runtime conventions to keep operator behavior consistent across systems.
## Slide 10: Display Builder - Editor

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Detail authoring features and maintainability properties.

Slide 10:
- **WYSIWYG editor**
- **Large pallet of widgets**
- **Control system aware**
- **Advanced customization through properties and scripting**
- **Reusable widgets/groups/screens**
- **Simple file format**

Notes:
1. Tie editor capabilities to faster iteration and reduced maintenance burden.

Speaking notes:
The editor is designed for practical maintainability: visual authoring, reusable components, and a simple format that is easy to version and review. Control-system awareness and scriptable behavior allow domain-specific displays without forking platform internals. This supports both rapid commissioning iteration and long-term support.

Detailed talking points:
- Highlight maintainability primitives: reusable widgets, parameterization, and simple file format support version control and review workflows (`F-EIC-CTRL-SW-OPI.3`). This is where you connect screen engineering discipline to lower long-term support burden.
- Resource grounding: MOCR002 notes reusable widgets, customization support, and XML `.bob` portability as practical maintainability features for site evolution.
## Slide 11: Display Builder - Runtime

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Show live operational behavior at runtime.

Slide 11:
- **Live process data with metadata, alarm awareness, units, and precision**

Notes:
1. Keep this anchored to daily operator usage and situational awareness.

Speaking notes:
Runtime is where display design translates directly into operator decisions. Metadata, units, precision, and alarm state are presented in context so users can act quickly and accurately. This closes the loop between engineering display design and operational effectiveness.

Detailed talking points:
- Tie runtime behavior to operator performance expectations: live values, metadata consistency, alarm awareness, and connection state are essential for decision quality (`F-EIC-CTRL-SW-OPI.5`, `F-EIC-CTRL-SW-OPI.6`). Mention that update-rate and latency goals are verified by demonstration requirements (`P-EIC-CTRL-SW-OPI.*`).
- Resource grounding: OPI requirement families emphasize metadata consistency, connection status clarity, and integrated control-service workflows in runtime views.
## Slide 12: Web Runtime and Remote Operations

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Extend display workflows to web-based consumption.

Slide 12:
- **Support remote operations by bringing OPI screens to the web**
- **`.bob` files converted to web runtime OPIs**

Notes:
1. Position web runtime as complement to desktop operations.

Speaking notes:
Web runtime extends screen access to environments where a full desktop deployment is not ideal. The key point is continuity: the same authored content can serve both rich operator desktops and lighter remote interfaces. This improves coverage without fragmenting display authoring workflows.

Detailed talking points:
- Explain web runtime as an access extension, not a replacement for desktop operations. The same `.bob` artifacts support consistent behavior across clients, reducing divergence risk and helping distributed operations and stakeholder visibility.
- Resource grounding: MOCR002 states that `.bob` artifacts are usable in web runtime, enabling one display artifact path across desktop and web deployments.
## Slide 13: Screen Creation

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Placeholder slide for screen creation workflow framing.

Slide 13:
- **Screen creation**

Notes:
1. Use this slide to connect authoring standards with operational consistency.

Speaking notes:
This section reinforces that screen creation is not only a UI activity but also an operational quality control point. Consistent naming, widget conventions, and review practices improve maintainability and reduce operator confusion. It is part of engineering discipline, not just presentation aesthetics.

Detailed talking points:
- Use this as a process slide: screen creation standards, naming conventions, and review expectations are quality controls that prevent fragmented user experience. Keep it short and transition to data workflows.
- Resource grounding: Product and preference layering in MOCR002 supports site standards for screen conventions without hard-forking application code.
## Slide 14: Data Browser

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Historical/live data analysis capabilities for operations and diagnostics.

Slide 14:
- **Presents live and historical data in one plotting environment**
- **Cross-channel correlation for diagnosis and post-mortem analysis**
- **Data export and inspection**
- **Optimized retrieval**
- **Workflow continuity with display, alarm, and logbook tools**
- **Supports multiple archive providers**

Notes:
1. Emphasize post-event analysis and troubleshooting value.

Speaking notes:
Data Browser supports both real-time context and retrospective analysis in a single workflow. Cross-channel correlation and multi-provider archive support are critical for diagnosing complex behaviors and validating corrective actions. Integration with other tools keeps operators in a continuous workflow rather than disconnected utilities.

Detailed talking points:
- Emphasize diagnostic loop closure: live+historical overlays, multi-provider archive access, and export paths enable post-event analysis and operational tuning. Tie to archive service requirements such as structured data support and time-range query performance (`F-EIC-CTRL-SW-ARCH.*`, `P-EIC-CTRL-SW-ARCH.*`).
- Resource grounding: MOCR002 describes multi-provider trending, including Archiver Appliance and RDB/Timescale-backed providers, for unified live-historical analysis.
## Slide 15: Alarm Applications

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Alarm-system goals and management focus.

Slide 15:
- **Goals**
- **Support operator response quality and reduce troubleshooting latency**
- **Support configuration and management of Alarm Server behavior (hierarchy, limits, annunciation rules)**

Notes:
1. Keep message centered on response quality and lifecycle tuning.

Speaking notes:
Alarm applications are about operational response quality, not just alarm display count. The architecture supports both immediate action and long-term alarm quality management through controlled configuration. That combination improves reliability during commissioning and operations.

Detailed talking points:
- Position alarm goals around human factors: low-noise, high-signal alarm environments improve response quality. Mention alignment with central scalable alarm requirements and notification/logging integration (`F-EIC-CTRL-SW-ALRM.1`, `.2`, `.3`).
- Resource grounding: The Phoebus ROD defines alarm services as real-time response plus retrospective tuning via history and configuration control.
## Slide 16: Alarm Applications (Client Views)

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Alarm client modes for monitoring, triage, and post-mortem.

Slide 16:
- **Alarm clients include:**
- **Tree: organized hierarchical view**
- **Table: fast detection of new/pending/acknowledged alarms with severity/timestamp context**
- **Panel**
- **Annunciator**
- **Alarm history: supports post-mortem review and alarm-quality tuning**

Notes:
1. Mention that different views support different operator tasks and cognitive load.

Speaking notes:
Different alarm views serve different operational tasks: hierarchy for structure, tables for triage speed, annunciation for immediate attention, and history for quality improvement. This model supports both real-time response and process refinement. It is designed to reduce missed conditions and improve signal-to-noise over time.

Detailed talking points:
- Explain why multiple alarm client views exist: hierarchy for structure, table for rapid triage, annunciation for immediacy, and history for improvement cycles. Connect to alarm UI/config/history requirements (`F-EIC-CTRL-SW-ALRM.5`) and performance targets (`P-EIC-CTRL-SW-ALRM.*`).
- Resource grounding: MOCR002 alarm stack includes active monitoring, history logging, and configuration logging to support both immediate action and tuning cycles.
## Slide 17: Save and Restore

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Repeatable machine-state workflows via configurations and snapshots.

Slide 17:
- **Save & Restore**
- **Organized representation of configurations and snapshots**
- **Interface to live, archived, and snapshot data**
- **Integration with logbook**

Notes:
1. Tie this to reproducibility and safer recovery operations.

Speaking notes:
Save and Restore supports reproducible operations by capturing known-good machine states and restoring them in a controlled way. Integration with live and archived context helps users validate restoration outcomes, and logbook integration improves traceability. This is a key risk-reduction capability for commissioning and routine operations.

Detailed talking points:
- State that save/restore is a controlled reproducibility mechanism, not a convenience button. Configuration snapshots plus restore workflows are critical for repeatable commissioning states and safer rollback paths (`EIC-CTRL-SW-SR` requirement family).
- Resource grounding: The Phoebus ROD calls save/restore a controlled reproducibility and recovery mechanism, including versioned snapshots and role-aware usage patterns.
## Slide 18: Logbook

Charge questions addressed: CQ1, CQ2, CQ4

Slide overview:
Structured operational documentation with automatic context capture.

Slide 18:
- **Enable users to create and retrieve log entries documenting EIC operations, observations, and events**
- **Phoebus clients: automatic context capture from active application state**
- **Web clients: easy access for quick entry and review**

Notes:
1. Emphasize traceability and knowledge retention.

Speaking notes:
The logbook is a core operations record, not an optional note-taking tool. Automatic context capture reduces manual entry burden while increasing data quality and traceability. Combined desktop and web clients support both deep control-room workflows and broader access across teams.

Detailed talking points:
- Logbook integration is about operational memory and traceability. Automatic context capture reduces manual errors and supports correlation across alarms, displays, and restoration actions (`EIC-CTRL-SW-LOGBK` requirement family).
- Resource grounding: MOCR002 Olog design captures structured entries plus searchable metadata and supports integrated, web, and mobile client access patterns.
## Slide 19: Applications Portfolio

Charge questions addressed: CQ2, CQ4

Slide overview:
PV discovery and diagnostics tooling complementing primary operator apps.

Slide 19:
- **Channel Finder clients: fast PV search with metadata (IOC host, record type, tags)**
- **PV Utilities:**
- **Probe: detailed PV introspection**
- **PV Table: monitor/save groups of PVs**
- **PV Tree: visualize EPICS record linkages**

Notes:
1. Position these as productivity multipliers for both operations and engineering.

Speaking notes:
The broader applications portfolio improves usability and diagnostics beyond primary control screens. Channel discovery and PV introspection tools reduce troubleshooting time and improve consistency across teams. These utilities are especially valuable in commissioning when rapid investigation is frequent.

Detailed talking points:
- Channel discovery and PV utilities reduce diagnosis time during both commissioning and operations. Metadata-driven navigation scales better than flat PV-space browsing and supports both operations and HLA tool development.
- Resource grounding: MOCR002 describes ChannelFinder as metadata-driven discovery over flat EPICS namespaces, enabling hierarchical or functional navigation views.
## Slide 20: Commissioning Tools

Charge questions addressed: CQ1, CQ2, CQ4, CQ7

Slide overview:
Commissioning scope and infrastructure-first strategy.

Slide 20:
- **Tuning and scans: model-assisted scans, optimization loops, scripted recovery/tuning workflows (HLA.1, HLA.2)**
- **Beam diagnostics and optics correction: orbit, tune, trajectory, response-matrix workflows**
- **Model-based commissioning: online model integration to reduce machine time/risk (HLA.4)**
- **Commissioning tools infrastructure as the near-term focus**
- **Python and Java client libraries in development for controls-system and middle-layer service access**

Notes:
1. Make clear that requirements for individual commissioning tools are still being refined.
2. Focus on enabling framework and delivery path.

References:
- Requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)
- Commissioning references: [presentations/raw/commissioning-tools/tuzzplm3.pdf](raw/commissioning-tools/tuzzplm3.pdf)
- Commissioning references: [presentations/raw/commissioning-tools/tucpr07.pdf](raw/commissioning-tools/tucpr07.pdf)

Speaking notes:
Commissioning applications are being developed with an infrastructure-first strategy so teams can deliver tools consistently on shared foundations. The near-term focus is client libraries, workflow integration, and model-assisted capability paths aligned to HLA requirements. This approach reduces duplication and supports faster, lower-risk commissioning tool rollout.

Detailed talking points:
- Present commissioning as infrastructure-first by design: common Python/Java client libraries reduce duplicated integration work and speed tool rollout. Tie explicitly to `F-EIC-CTRL-SW-HLA.1` through `.4` for API availability, packaging, PV Access interface, and model-tool interfaces.
- Resource grounding: RSI-158 HLA requirements (`F-EIC-CTRL-SW-HLA.1` to `.4`) align with API availability, packaging consistency, PV Access interface, and model integration.
## Slide 21: Phoebus Architecture

Charge questions addressed: CQ2, CQ4, CQ5

Slide overview:
Core technical architecture and runtime model.

Slide 21:
- **Modular framework built on Java + JavaFX (no Eclipse RCP)**
- **Core modules: PV access, VTypes, adapters, logging, jobs**
- **Core-UI modules: docking, menus, selection services**
- **Applications: operator-facing tools (Display Builder, Data Browser, etc.)**
- **Jobs/scheduling: run tasks off UI thread**
- **Connection management: pooled reusable PV and REST clients**
- **VTypes: protocol-agnostic canonical model, immutable and safe to share**
- **Formula functions: efficient thread-safe data processing pipelines**

Notes:
1. Link architecture choices to responsiveness, extensibility, and maintenance risk reduction.

Speaking notes:
Phoebus architecture is modular by design, separating shared core capabilities from application-specific logic. Threading, connection pooling, and immutable value models are chosen for responsiveness and reliability under operational load. This foundation supports long lifecycle maintenance while preserving room for incremental extension.

Detailed talking points:
- Use architecture internals to justify sustainability: core/core-UI separation, connection reuse, off-UI-thread jobs, and immutable value models are practical decisions for responsiveness and reliability at scale. Keep this technical but concise.
- Resource grounding: MOCR002 core modules include CorePV, VTypes, scheduler, configuration, logging, and security primitives used across apps and services.
## Slide 22: Phoebus Architecture - Extensibility

Charge questions addressed: CQ2, CQ4, CQ5

Slide overview:
SPI-based extension points for protocols, services, apps, and UI.

Slide 22:
- **Extensible via Java SPI (Service Provider Interface)**
- **New data sources and protocols (CA, PVA, MQTT, Tango, ...)**
- **Clients for middle-layer services (Olog, elog, ...)**
- **New applications**
- **UI extensions (menus, toolbars, context menus)**

Notes:
1. Present extensibility as targeted adaptation without core destabilization.

Speaking notes:
Extensibility through SPI enables controlled adaptation for site needs while keeping core platform behavior stable. This is important for long-term evolution as protocols, services, and workflows change. It also reduces fork pressure and helps maintain compatibility across collaboration partners.

Detailed talking points:
- SPI extensibility is the control point that enables site adaptation without core forking. Mention that protocol, service-client, application, and UI extension hooks allow controlled local customization while preserving upstream compatibility.
- Resource grounding: MOCR002 SPI examples show protocol adapters, service clients, and UI extensions can be added with loose coupling and curated product control.
## Slide 23: Phoebus Architecture - EIC Product

Charge questions addressed: CQ2, CQ4, CQ5

Slide overview:
Site-specific EIC product composition.

Slide 23:
- **EIC Phoebus product includes site-specific:**
- **Applications**
- **Datasources**
- **Configurations**
- **Branding**
- **Adapters**
- **Addresses needs of a particular organization or workflow**

Notes:
1. Clarify distinction between shared upstream platform and EIC product profile.

Speaking notes:
The EIC product model packages site-specific needs on top of shared architecture. This lets us tailor workflows and integrations without losing alignment with upstream collaboration. It is a practical balance between local requirements and long-term maintainability.

Detailed talking points:
- Clarify productization: EIC package composition selects approved apps, data sources, configs, and adapters from a shared platform. This is how local workflow needs are met without abandoning collaboration-driven maintenance.
- Resource grounding: MOCR002 product model supports site-specific composition (applications, adapters, branding, preferences) while preserving upstream architecture contracts.
## Slide 24: Phoebus Collaboration

Charge questions addressed: CQ2, CQ5

Slide overview:
Collaboration scale and activity as maintainability evidence.

Slide 24:
- **International collaboration of dozens of research facilities**
- **Phoebus activity indicators: ~300 PRs, ~100 issues**

Notes:
1. Use collaboration activity as evidence for ecosystem sustainability and support depth.

Speaking notes:
Active collaboration is a core risk mitigation for long-lifecycle software. Broad participation, steady PR flow, and issue handling indicate sustained maintenance capacity and faster response to changes. For EIC, this reduces single-site dependency risk and improves future adaptability.

Detailed talking points:
- Use collaboration activity as lifecycle evidence, not vanity metrics. Broad contributor base and active issue/PR flow indicate resilience against single-team dependency and better long-term change response.
- Resource grounding: MOCR002 reports contributors from dozens of facilities and sustained activity as evidence of maintainability and reduced single-site dependency.
## Slide 25: Risks

Charge questions addressed: CQ5

Slide overview:
State primary risk and concrete mitigations.

Slide 25:
- **Risk RT-6-007-001**
- **Mitigation: modular/extensible framework enables targeted upgrades with minimized disruption**
- **Mitigation: multi-lab collaboration spreads maintenance risk and improves response speed to technology changes**

Notes:
1. Keep mitigation statements concrete and architecture-linked.

Speaking notes:
The key risk is technology evolution over the project lifecycle. Our mitigation strategy is architectural modularity plus active collaboration, which together reduce upgrade impact and improve response capacity. This risk posture is intentional and aligned with long-term operations support goals.

Detailed talking points:
- Keep risk discussion focused and brief: main concern is technology evolution across long lifecycles. Mitigation is architectural modularity plus distributed collaboration ownership, enabling targeted upgrades rather than disruptive rewrites.
- Resource grounding: Phoebus ROD risk table highlights over-customization and service sprawl mitigated by baseline product policy, ownership, version pinning, and readiness checks.
## Slide 26: Summary

Charge questions addressed: CQ7 (overall readiness)

Slide overview:
Close with the applications/UI readiness argument.

Slide 26:
- **Phoebus is the primary EIC application environment for operator workflows**
- **Display Builder, Web Runtime, and Data Browser provide path from screen creation to remote operations and post-event analysis**
- **Alarm, Save/Restore, and Logbook workflows improve response quality, repeatability, and traceability**
- **PV utilities strengthen usability through discovery, metadata context, and diagnostics**
- **Modular Java/JavaFX + SPI architecture supports long-term maintainability and site-specific composition**
- **Active collaboration and risk mitigations support final-design progression**

Notes:
1. End with readiness statement grounded in requirements traceability and risk mitigation.

Speaking notes:
In summary, the applications/UI architecture provides an integrated operator environment with clear workflow continuity, maintainable technical foundations, and explicit risk controls. The approach aligns with requirement authority and supports phased implementation during design progression. This establishes confidence for moving forward toward final design.

## CQ Traceability Matrix

| Slide(s) | Primary CQ(s) | Evidence / Basis |
|---|---|---|
| 1, 4, 26 | CQ7 | Deck framing and readiness summary |
| 3 | CQ1-CQ7 | Charge question statements |
| 5-6 | CQ1 | Scope and PRD requirement anchors (`EIC-SEG-RSI-158`) |
| 7-8 | CQ1-CQ5 | Layered architecture and integration boundaries |
| 9-18 | CQ1, CQ2, CQ4 | Operator applications and workflow capabilities |
| 20 | CQ1, CQ2, CQ4, CQ7 | Commissioning strategy and HLA alignment |
| 21-23 | CQ2, CQ4, CQ5 | Phoebus architecture, extensibility, EIC productization |
| 24-25 | CQ2, CQ5 | Collaboration evidence and risk mitigation |

## Optional Short Cues (30-45 seconds per slide)

- 1-2: Session context and architecture ownership.
- 3-4: CQ map and deck roadmap.
- 5-8: Scope, requirements, and integrated toolkit framing.
- 9-13: Display workflows from authoring to runtime and web delivery.
- 14-18: Data, alarms, save/restore, and logbook operations cycle.
- 19-20: Utility portfolio and commissioning enablement strategy.
- 21-23: Architecture internals, extensibility, and EIC-specific product model.
- 24-25: Collaboration sustainability and risk posture.
- 26: Final readiness summary tied to CQ progression.

## 30-Minute Delivery Plan (Presenter Timing)

| Segment | Slides | Target Time |
|---|---|---|
| Opening and framing | 1-4 | 3 min |
| Scope and requirements anchor | 5-7 | 3 min |
| Phoebus toolkit and display workflows | 8-13 | 8 min |
| Data, alarm, restore, and logbook workflows | 14-18 | 7 min |
| Utility and commissioning tooling | 19-20 | 3 min |
| Architecture, extensibility, and collaboration | 21-24 | 4 min |
| Risk and close | 25-26 | 2 min |

Detailed talking points:
- Close on readiness with three points: integrated operator workflow, requirement-aligned capabilities, and maintainable architecture with active ecosystem support. End by inviting panel questions on verification sequencing and deployment priorities.

## Panel Q&A One-Page (Quick Reference)

- **Why Phoebus as primary toolkit?** Integrated workflow continuity, modular architecture, and broad collaboration support reduce long-term cost and integration friction.
- **How are requirements covered?** `EIC-SEG-RSI-158` requirement families are mapped across OPI, alarm, archiving, save/restore, logbook, and HLA interfaces; demonstration-heavy items remain on the verification plan.
- **How do desktop and web tools coexist?** Desktop remains primary operator environment; web runtime and web clients extend access and visibility without changing service boundaries.
- **How is scalability handled?** Service-oriented deployment enables independent scaling of alarm, archive, and logging workloads, with shared data models and consistent APIs.
- **How is quality controlled?** Versioned artifacts, review workflows, reusable components, and standardized interfaces reduce drift and improve reproducibility.
- **What is still maturing?** Some commissioning tool requirements and subsystem-specific performance closure are still being finalized and validated in phased integration.
- **How are migration and compatibility managed?** Application/service layers stay protocol-aware through EPICS/PVA-first interfaces and compatibility patterns already defined in architecture decisions.
- **What should panel remember?** The application stack is designed to deliver usable operations now while remaining maintainable for multi-decade evolution.
- Resource grounding: The combined ROD position is stable: EPICS/PVA-first controls foundation with Phoebus/services as the standard operator and middle-layer platform.

