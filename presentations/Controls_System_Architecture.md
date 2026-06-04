## Slide 1: Controls System Architecture

Charge questions addressed: CQ7 (design maturity readiness framing)

Slide overview:
Establish the review context, scope intent, and expected outcome of the presentation for the committee.

Slide 1:
- **Controls System Architecture**
- **Kunal Shroff**
- **Software Technical Lead**
- **Accelerator Controls Global Software, Networking & Computing PDR**
- **June 15-17, 2026**

Notes:
1. This talk addresses architecture maturity for the current review phase, not full final-design closure.
2. The core narrative is EPICS/PVA baseline, ADO coexistence strategy, and integrated operator and middle-layer tooling.
3. The presentation includes technical rationale, requirements alignment highlights, and implementation-readiness signals.

Detailed references appear in the technical slides where they are used.

## Slide 2: Charge Questions

Charge questions addressed: CQ1-CQ7 (definition and scope of all charge questions)

Slide overview:
Frame the review criteria and clarify which questions are addressed in this presentation phase versus later phases.

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
Presentation roadmap across architecture, EPICS/ADO strategy, networking, services, tooling, and path forward.

Slide 3:
- **Scope**
- **Architecture**
- **EPICS**
- **ADO, dual-system coexistence, tradeoffs, and decision matrix**
- **Network architecture, subnet strategy, and buildout plan**
- **EPICS IOC continuity and pvAccess protocol value**
- **Middle-layer services**
- **Phoebus toolkit**
- **CI/CD governance, automation stack, QA/QC gates, and domain pipelines**
- **Path Forward**
- **Summary**

Notes:
1. The outline is intentionally sequenced from strategic framing to technical architecture, then execution readiness.

## Slide 4: Scope

Charge questions addressed: CQ1-7

Slide overview:
What this presentation covers at the architecture level.

Slide 4:
- **Controls system architecture baseline (EPICS 7, PVA-first)**
- **Coexistence strategy for EPICS and legacy ADO systems**
- **Middle-layer services and operator tools**
- **Network and infrastructure architecture**
- **CI/CD and governance model**

## Slide 5: Requirements

Charge questions addressed: CQ1,2,7

Slide overview:
Reference the PRD sources that anchor requirements for this review phase.

Slide 5:
- **Initial versions of the Performance Requirements Documents (PRDs)**
- **High Level Applications [EIC-SEG-RSI-158]**
- **Networking & Computing [EIC-SEG-RSI-XXX]**

Notes:
1. This is the anchor diagram for the rest of the talk; later slides zoom into each layer.
2. The key message is architectural coherence: multiple subsystems, one operational experience.
3. Coexistence is intentional in this phase, with transition path toward EPICS-first operations.

References:
- Thin talk ecosystem visual source: [presentations/examples/thin_MOCR002_talk.pptx](examples/thin_MOCR002_talk.pptx)
- Ecosystem text basis: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 6: Control System Architecture

Charge questions addressed: CQ1

Slide overview:
Show the three-layer controls architecture: operator/apps, middle-layer services, and control system.

Slide 6:
- **Control System Architecture**
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Keep this as a concise executive primer for the platform context before the Phoebus overview.
2. Use Slide 7 for technical depth and Slide 8 for protocol-specific details.

References:
- EPICS overview: https://epics-controls.org/about-epics/
- EPICS modules and support resources: https://epics-controls.org/resources-and-support/modules/
- EPICS decision baseline: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)

## Slide 7: Control System Architecture (Layered View)

Charge questions addressed: CQ1,2,3,4,5

Slide overview:
Reinforce the layered architecture view used to frame subsequent EPICS, ADO, and service slides.

Slide 7:
- **Control System Architecture**
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:

additional material
- **Performance and scale support:**
	- **Faster behavior can be configured with non-standard scan rates or `I/O Intr` event-driven processing when device support and platform timing allow**
	- **Requirement traceability: alarm threshold evaluation >=10 Hz (`P-EIC-CTRL-SW-ALRM.3`) and OPI update support up to 30 Hz (`P-EIC-CTRL-SW-OPI.3`) via demonstration**


References:
- EPICS decision baseline: [rod/EIC-ROD-EPICS-Control-System.md](../rod/EIC-ROD-EPICS-Control-System.md)
- EPICS 7 enhancements paper (extracted): [rod/raw_resources/_extracted/mobpl01.txt](../rod/raw_resources/_extracted/mobpl01.txt)
- EPICS 7 five-year status paper (extracted): [rod/raw_resources/_extracted/th1bco01.txt](../rod/raw_resources/_extracted/th1bco01.txt)

## Slide 8: EPICS Control System

Charge questions addressed: CQ1,2

Slide overview:
Introduce EPICS platform fundamentals, scalability, and ecosystem maturity.

Slide 8:
- **EPICS Control System**
- **What EPICS is: Open-source control system toolkit used across accelerator and large experimental facilities**
- **Distributed architecture: independent IOCs which embed controls logic and provide an interface to hardware**
- **Core communication model: client/server plus publish-subscribe behavior for scalable monitoring and control**
- **Scalability: modular deployment, incremental expansion**
- **Technology ecosystem: large EPICS ecosystem of community-maintained modules, device support, drivers, and operations tools**
- **Longevity: active multi-lab collaboration over decades**

Notes:
1. Keep this slide focused on protocol capability and migration path, not broader system architecture.
2. Tie claims to the EPICS 7 roadmap paper and treat TLS as planned work rather than a completed capability.

References:
- EPICS 7 five-year status paper (extracted): [rod/raw_resources/_extracted/th1bco01.txt](../rod/raw_resources/_extracted/th1bco01.txt)
- EPICS 7 enhancements paper (extracted): [rod/raw_resources/_extracted/mobpl01.txt](../rod/raw_resources/_extracted/mobpl01.txt)

## Slide 9: EPICS for EIC (Functional and Reliability Support)

Charge questions addressed: CQ1,2,3,4

Slide overview:
Detail EPICS functional fit and reliability/operations support for EIC.

Slide 9:
- **EPICS for EIC**
- **Functional support:**
	- **Distributed IOC model supports heterogeneous subsystems and interfaces**
	- **PVA protocol path supports structured data exchange and service integration for new EIC systems**
	- **Normative Types (`NTScalar`, `NTArray`, `NTNDArray`, `NTTable`) plus modern libraries (PVXS C++, core-pva Java, p4p Python) enable generic clients and service-oriented integration**
- **Reliability and operations support:**
	- **Distributed IOC and service architecture reduces single-point concentration risk when deployed with redundancy**
	- **Delta subscription updates reduce unnecessary network traffic for rich structures, improving operational efficiency under sustained load**
	- **Mature operations tooling ecosystem (`areaDetector`, archiver, alarms, save/restore, metadata tooling) supports production workflows and maintainability**

Notes:
1. Keep this slide balanced: acknowledge ADO strengths while clearly framing why transition is required.
2. The next slides detail how dual-system coexistence is implemented and governed.

## Slide 10: EPICS for EIC (Performance and Collaboration)

Charge questions addressed: CQ1,2,3,4

Slide overview:
Cover EPICS performance/scale support and international collaboration reuse.

Slide 10:
- **EPICS for EIC**
- **Performance and scale support:**
	- **EPICS IOC record processing supports standard periodic scan classes (10, 5, 2, 1, 0.5, 0.2, 0.1 seconds), up to 10 Hz in default periodic mode**
	- **Architecture supports staged growth through horizontal scaling of IOCs, services, and client workloads**
- **International collaboration support:**
	- **EPICS maintains a large global ecosystem of modules, device support, drivers, and tools across Base, IOC modules, and extensions**
	- **Community maintenance and distributed expertise across major labs reduce single-site dependency risk**
	- **Deployment patterns from EPICS 7 facilities (including ESS, NSLS-II, ITER, APS-U, PIP-II) are directly reusable for EIC**

Notes:
1. This slide serves as the architectural map for dual-system operations.
2. Emphasize that coexistence is engineered, not accidental, and includes explicit integration contracts.
3. The user experience target is protocol-transparent operations even while backend systems differ.

## Slide 11: pvAccess Protocol for EIC

Charge questions addressed: CQ1,2,3,4

Slide overview:
Describe pvAccess capabilities for structured data, subscriptions, RPC workflows, and supported client libraries.

Slide 11:
- **pvAccess Protocol for EIC**
- **pvAccess is EPICS's next-generation control protocol.**
- **What pvAccess provides:**
	- **Transports structured data types (scalars, arrays, tables, images) with metadata**
	- **Efficient subscriptions transfer only changed fields, reducing network load**
	- **Supports RPC-style interactions for service-oriented control workflows**
	- **Supports high-bandwidth data acquisition, imaging, and large structured payloads such as `NTNDArray`**
	- **Supported via multiple client libraries (`PVXS`, `core-pva`, `P4P`), IPv6 support, and planned TLS-secured connections**

Notes:
1. No single strategy is best everywhere; deployment can combine approaches by subsystem and risk profile.
2. The recommendation should prioritize operator transparency and measured performance under real load.

## Slide 12: ADO Control System

Charge questions addressed: CQ3,4,5

Slide overview:
Summarize ADO architecture, operational maturity, and active-use continuity during EIC construction.

Slide 12:
- **ADO Control System**
- **What ADO is:**
	- **RHIC controls were built in the early 1990s as a network-based distributed, client-server architecture**
	- **High-level services cover operator interfaces, sequencing, alarms, archiving, and logbook workflows; low-level control runs through VME/ADO on VxWorks**
	- **This architecture has supported RHIC for about 25 years with staged upgrades (including FPGA-based LLRF), demonstrating operational maturity**
- **Current status (still in use):**
	- **ADO-based hadron injection controls, including BLIP-related operations, remain active during EIC construction**
	- **Existing device integrations and operating experience remain valuable for near-term reliability and commissioning continuity**

Notes:
1. Keep this slide at architecture level; detailed firewall rules and VLAN assignments belong in implementation design packages.
2. Emphasize that network segmentation is an enabler for reliability, security, and operational scalability.
3. Highlight that distributed placement choices should be validated with mixed-mode load testing.

## Slide 13: Dual System Architecture Diagram (Need and Plan)

Charge questions addressed: CQ3,4,5

Slide overview:
Explain why near-term dual-system coexistence is required and how migration is staged.

Slide 13:
- **Dual System Architecture Diagram**
- **EIC plan and dual-system need:**
	- **EIC performance goals (about two orders of magnitude luminosity increase vs RHIC) require modernized controls platforms**
	- **Software strategy prioritizes long-term maintainability for a 30+ year lifecycle and broader talent/community support**
	- **Therefore, the near-term architecture is intentionally dual-system: legacy ADO paths continue where needed while new systems are delivered on EPICS/PVA and migrated in phases**

Notes:
1. This slide is intentionally a placeholder for deeper network design content.
2. Expand once network architecture decisions are finalized.


## Slide 14: Dual System Architecture Diagram (Strategy 1: AdoPvaSrv)

Charge questions addressed: CQ3,4,5

Slide overview:
Present Strategy 1 (AdoPvaSrv): distributed pvAccess exposure directly from ADO Managers.

Slide 14:
- **Dual System Architecture Diagram**
- **Strategy 1: AdoPvaSrv**
	- **AdoPvaSrv runs on each ADO Manager allowing it to speak pvAccess**
	- **Fully distributed with no central broker or gateway infrastructure required**
	- **Horizontally scalable**
	- **Can be rolled out iteratively**

Notes:
1. Keep the framing architecture-focused: services complement IOCs rather than replacing real-time device control.
2. Emphasize that this is the standard operator-facing and middle-layer integration layer on top of EPICS.
3. Highlight service ownership, version pinning, and readiness checks as maintainability controls.

References:
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)
- Phoebus ecosystem paper (extracted): [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 15: Dual System Architecture Diagram (Strategy 2: AdoEpicsBridge)

Charge questions addressed: CQ3,4,5

Slide overview:
Present Strategy 2 (AdoEpicsBridge): p4p bridge exposing ADO devices as EPICS PVs.

Slide 15:
- **Dual System Architecture Diagram**
- **Strategy 2: AdoEpicsBridge**
	- **A p4p-based bridge that exposes ADO devices as EPICS PVs over pvAccess**
	- **Requires no changes to existing ADO infrastructure — ADO devices and managers remain untouched**
	- **Seamlessly merges the two control systems from the EPICS side by exposing ADO devices as EPICS PVs**
	- **Primarily used for FEC; p4p-based bridge between ADO and EPICS (pvAccess)**
	- **Requires a cluster of AdoEpicsBridge instances with a load balancer — additional infrastructure investment, but achievable and well-understood**

Notes:
1. Descriptions are sourced from the Phoebus ROD and ecosystem papers.
2. Each service has a focused, well-defined role and can be scaled independently.
3. These services work together to enable the consistent operator workflows shown in Slide 16.

## Slide 16: Dual System Architecture Diagram (Strategy 3: Ado Datasource)

Charge questions addressed: CQ3,4,5

Slide overview:
Present Strategy 3 (Ado Datasource): tool/service-layer ADO client integration.

Slide 16:
- **Dual System Architecture Diagram**
- **Strategy 3: Ado Datasource**
	- **ADO protocol client in core-pv**
	- **Requires no changes to existing ADO infrastructure — ADO devices and managers remain untouched**
	- **Seamlessly merges the two control systems at the tools and services layer**
	- **No central broker or gateway infrastructure required**

Notes:
1. This is the strategic rationale: efficiency, consistency, and sustainability drive the Phoebus investment.
2. Transition to the next slides to show concrete implementations (applications, architecture, web tools).

References:
- Phoebus ecosystem paper: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 17: Network Architecture and Subnet Strategy

Charge questions addressed: CQ1,2

Slide overview:
Define network goals, subnet segmentation, and coexistence deployment implications.

Slide 17:
- **Network Architecture and Subnet Strategy**
- **Network architecture goals:**
	- **Scalable connectivity for distributed and clustered components**
	- **Clear segmentation across controls, instrumentation, and data services**
- **Subnet model:**
	- **Controls subnet: IOC, ADO Manager, gateway, and command/control traffic**
	- **Instrumentation subnet: device-facing acquisition and timing-sensitive interfaces**
	- **Data/services subnet:**
- **Integration and security:**
	- **Controlled cross-subnet access through gateways and service endpoints**
	- **Monitoring and observability at subnet and service boundaries**
- **Coexistence deployment implications:**
	- **ADO server and bridge clusters placed for low-latency access to legacy domains**
	- **EPICS/PVA services scaled horizontally on service networks**
	- **Operator tools consume unified interfaces without direct dependency on backend protocol location**

Notes:
1. These applications are tightly integrated; context (PV names, values, alarms, archive sources) flows seamlessly between tools.
2. Operators move fluidly from alarm investigation -> historical trends -> device displays -> logbook without re-entry.
3. Emphasize the consistent, unified user experience across all workflows.

References:
- Phoebus applications and ecosystem integration: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 18: Network Architecture and Subnet Strategy (Diagram Continuation)

Charge questions addressed: CQ1,2

Slide overview:
Continuation slide for subnet strategy and topology context.

Slide 18:
- **Network Architecture and Subnet Strategy**

Notes:
1. This architecture is why Phoebus can evolve sustainably: extensions plug in via SPI, and applications stay focused on business logic.
2. Core libraries are shared across desktop applications and middle-layer services, ensuring consistent data models and reduced duplication.
3. The modular design supports containerized deployment and modern CI/CD practices.

References:
- Phoebus framework architecture and SPI: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)

## Slide 19: Middle-Layer Services (Layered Context)

Charge questions addressed: CQ1,2,3

Slide overview:
Place middle-layer services in the full controls stack between operator tools and EPICS.

Slide 19:
- **Middle-Layer Services**
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Keep the contrast clear: desktop for rich operations, web for easy access and flexible consumption.
2. Use concrete examples (`pvws`, `dbwr`, Olog web, `etraveller`, component database, `pvinfo`) instead of generic web tooling claims.

References:
- Phoebus ecosystem paper (Olog web, multi-platform access): [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)
- pvinfo project: https://github.com/ChannelFinder/pvinfo

## Slide 20: Middle-Layer Services (Service Model Benefits)

Charge questions addressed: CQ1,2,3

Slide overview:
Describe architectural benefits of modular, API-driven middle-layer services.

Slide 20:
- **Middle-Layer Services**
- **Modular services: each service has a focused, well-defined role and can evolve independently**
- **Flexible interfaces: support command-response and publish-subscribe patterns via standard service APIs**
- **Data abstraction: tools interact with services, not storage internals, preserving user workflow while backends evolve**
- **Optimized data handling: purpose-built stores per domain (time-series, alarms, snapshots, metadata)**
- **Interoperable by design: consistent service contracts across tools and client environments**
- **Scalable and maintainable: deploy and scale services independently based on facility demand**


Notes:
- **CI/CD purpose for controls architecture:**
	- **Standardize delivery workflows across infrastructure, controls software, and operations tooling**
	- **Reduce integration risk through automated validation and repeatable deployment steps**
	- **Improve traceability from design change to deployed system state**
- **Industry-aligned workflow model:**
	- **Git-based change control with pull request approvals and protected branches**
	- **Pipeline-first validation before integration and release**
	- **Infrastructure as code as the default operating model for environment setup and updates**
- **GitHub as source control platform:**
	- **Full history and traceability of architecture, code, configuration, and operations assets**
	- **Structured collaboration via pull requests, reviews, and issue tracking**
	- **Branch protection and CODEOWNERS enforce controlled change paths**
- **GitHub Actions for CI/CD orchestration:**
	- **Automated build, test, packaging, and deployment workflows**
	- **Reusable workflows reduce duplication and enforce common standards**
	- **Environment-aware pipelines for development, test, and production readiness**
- **Ansible and AWX for operational automation:**
	- **Ansible playbooks define desired state for systems and services**
	- **AWX provides managed execution, scheduling, credential handling, and run visibility**
	- **Consistent, repeatable rollouts across multiple environments**
- **Infrastructure as code principles:**
	- **Version-controlled infrastructure definitions and configuration policies**
	- **Reviewable, auditable changes to platform and service topology**
	- **Drift reduction through repeatable automation runs**
2. Emphasize that CI/CD is part of architecture maturity, not only software process.
3. Focus on the end-to-end toolchain, not isolated tools.

References:
- GitHub platform decision record: [rod/EIC-ROD-GitHub-Platform.md](../rod/EIC-ROD-GitHub-Platform.md)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 21: Middle-Layer Services (Service Roles)

Charge questions addressed: CQ1,2,3

Slide overview:
Detail responsibilities of Archiver, Alarm, ChannelFinder, NameOps, Olog, Save/Restore, and PVA Gateway.

Slide 21:
- **Middle-Layer Services**
- **Archiver:** EPICS Archiver Appliance stores time-series PV data at configurable rates and provides fast historical queries. Supports post-event analysis and correlation with live values in Data Browser.
- **Alarm:** Monitors, filters, and aggregates alarms in real-time, notifies operators, maintains alarm history, and supports configuration rollback. Enables both immediate response and retrospective tuning of alarm quality.
- **ChannelFinder:** Directory service for PV catalogs, tags, and properties.
- **NameOps:** Generate and validate EIC device and PV names.
- **Olog (Online Logbook):** Structured operator and operations logging with automatic context capture (PV names, alarm states, timestamps).
- **Save/Restore:** Captures, stores, and restores PV snapshots that reproduce known good states. Supports repeatable operations and controlled recovery from incident or configuration changes.
- **PVA Gateway:** Enables EPICS-domain inter-network connectivity with controlled PV exposure across network boundaries. Supports scalable client access patterns without overwhelming IOC resources.

Notes:
1. Unit tests catch individual component issues early; integration tests catch interaction failures before operations.
2. Tie quality outcomes directly to reduced commissioning and operations risk.
3. Reproducible environments are what make the test pipeline trustworthy at scale.

## Slide 22: Phoebus Operator Toolkit (Layered Context)

Charge questions addressed: CQ1,2,3

Slide overview:
Show Phoebus toolkit placement above middle-layer services and EPICS control system.

Slide 22:
- **Phoebus Operator Toolkit**
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Keep domain boundaries explicit to clarify ownership and pipeline responsibility.
2. Use this slide as the operational view of how CI/CD supports the full controls stack.

## Slide 23: Phoebus Operator Toolkit (Strategic Benefits)

Charge questions addressed: CQ1,2,3

Slide overview:
Summarize integrated-toolkit advantages for operator workflows, extensibility, and maintainability.

Slide 23:
- **Phoebus Operator Toolkit**
- **Integrated set of tools across displays, alarms, trends, logbook, and save/restore**
- **Operators navigate seamlessly between tools**
- **Context sharing reduces operator burden and improves efficiency**
- **Single integrated desktop environment reduces training overhead and support burden**
- **Extensible and Modular architecture**
	- **SPI-based extensibility allow sites to add tools and protocols without disrupting core stability**
	- **Shared data models, resources, etc allows for simplified and efficient applications**
- **Large, active collaboration strengthens maintainability and support**

Notes:
1. This summary slide ties back to the charge questions and affirms readiness progression.
2. Keep the tone factual and evidence-grounded; avoid overstating maturity beyond the scope of this phase.

## Slide 24: Phoebus Operator Toolkit - Applications

Charge questions addressed: CQ1,2,3

Slide overview:
User-facing applications within Phoebus that form a cohesive operator environment.

Slide 24:
- **Phoebus Operator Toolkit**
- **Display Builder:** OPI/HMI editor and runtime with alarm awareness, units, and precision. Supports legacy display migration (EDM, MEDM, BOY auto-conversion) and web-based runtime execution.
- **Data Browser:** Trending across multiple archive providers (Archiver Appliance, RDB, TimescaleDB). Enables correlation analysis with live PV values in unified plotting environment.
- **Alarm UI:** Real-time alarm monitoring with high-level overviews, alarm tables, hierarchical trees, and voice annunciator. Ensures critical conditions are surfaced and managed efficiently.
- **Olog (Logbook UI):** Structured operator logging with automatic PV/alarm/timestamp context capture. Integrated within Phoebus for seamless workflow documentation.
- **PV Utilities:** Probe for detailed introspection, PV Table for monitoring and save/restore groups, PV Tree for record linkages. Support diagnostics and day-to-day operations.
- **ChannelFinder Client:** Fast, case-insensitive PV discovery with metadata search (IOC host, record type, status). Hierarchical views improve navigability of flat EPICS namespace.
- **Save/Restore UI:** Snapshot capture, versioning, and restoration with merge/scale capabilities. Enables reproducible operations and rapid recovery from configuration changes.

Notes:
1. These applications are tightly integrated; context (PV names, values, alarms, archive sources) flows seamlessly between tools.
2. Operators move fluidly from alarm investigation -> historical trends -> device displays -> logbook without re-entry.

References:
- Phoebus applications and ecosystem integration: [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 25: Web Tools

Charge questions addressed: CQ1,2,3

Slide overview:
Why web applications are needed alongside Phoebus desktop, and which web tools EIC will use.

Slide 25:
- **Web Tools**
- **Why web applications are needed:**
	- **Phoebus desktop remains the rich operator environment for integrated control-room workflows**
	- **Web tools complement desktop with easier access, flexible deployment, and lightweight views for broader users**
- **EIC web tools:**
	- **`pvws` and `dbwr`: WebSocket-based toolkit for displaying controls information on web pages and archive-oriented views**
	- **Web clients for Olog, `etraveller`, and component database workflows**
	- **`pvinfo`: web/CLI PV metadata and connection-status lookup**

Notes:
1. Keep the contrast clear: desktop for rich operations, web for easy access and flexible consumption.
2. Use concrete examples instead of generic web tooling claims.

References:
- Phoebus ecosystem paper (Olog web, multi-platform access): [rod/raw_resources/_extracted/MOCR002.txt](../rod/raw_resources/_extracted/MOCR002.txt)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)
- pvinfo project: https://github.com/ChannelFinder/pvinfo

## Slide 26: QA/QC

Charge questions addressed: CQ1,2,6

Slide overview:
How QA/QC is embedded into code review, unit tests, and integration tests before changes reach operations.

Slide 26:
- **QA/QC**
- **How QA/QC is embedded into code review, unit tests, and integration tests before changes reach operations.**
- **QA/QC control points:**
	- **Code review gates:** pull request templates, review checklists, and mandatory approvals enforce design and safety expectations before any change is merged.
	- **Unit tests:** per-component build validation, syntax checks, and schema conformance gates run automatically on each change before merge — catching individual component regressions early.
	- **Integration tests:** post-merge deployment into a controlled test environment validates that components interact correctly — IOC + gateway + service stack behavior tested together before promotion.
	- **Promotion gates:** release to operations only after both unit and integration test suites pass, with artifact traceability linking each deployed version to its validated test record.
- **Dev/test environment enablement:**
	- **Rapid environment setup from versioned automation definitions**
	- **Reproducible test conditions across team members and subsystems**
	- **Faster defect isolation and higher confidence before production rollout**

Notes:
1. Unit tests catch individual component issues early; integration tests catch interaction failures before operations.
2. Tie quality outcomes directly to reduced commissioning and operations risk.
3. Reproducible environments are what make the test pipeline trustworthy at scale.

## Slide 27: CI/CD and Automation Stack

Charge questions addressed: CQ1,2,6

Slide overview:
End-to-end delivery backbone: governance in GitHub, CI/CD orchestration in Actions, and repeatable operations via Ansible/AWX and infrastructure as code.

Slide 27:
- **CI/CD and Automation Stack**
- **CI/CD purpose for controls architecture:** Standardize delivery workflows across infrastructure, controls software, and operations tooling; reduce integration risk through automated validation and repeatable deployment steps; improve traceability from design change to deployed system state.
- **Change control (GitHub):** Structured collaboration through pull requests, reviews, and issue tracking; branch protection and CODEOWNERS enforce controlled change paths; full history and traceability across architecture, code, configuration, and operations assets.
- **Orchestration (GitHub Actions):** Automated build, test, packaging, and deployment workflows; reusable workflows reduce duplication and enforce common standards; environment-aware pipelines support development, test, and production readiness.
- **Operational automation (Ansible/AWX + IaC):** Ansible playbooks define desired state, AWX provides managed execution and visibility, and infrastructure-as-code keeps environment setup and updates version-controlled, reviewable, auditable, and repeatable.

Notes:
1. Emphasize that CI/CD is part of architecture maturity, not only software process.
2. Focus on the end-to-end toolchain, not isolated tools.

References:
- GitHub platform decision record: [rod/EIC-ROD-GitHub-Platform.md](../rod/EIC-ROD-GitHub-Platform.md)
- Phoebus tools and services decision record: [rod/EIC-ROD-Phoebus-Tools-and-Services.md](../rod/EIC-ROD-Phoebus-Tools-and-Services.md)

## Slide 28: CI/CD Pipelines

Charge questions addressed: CQ1,2,6

Slide overview:
CI/CD pipeline scope by domain: infrastructure, IOCs, services, tools, and resources.

Slide 28:
- **CI/CD Pipelines**
- **CI/CD and automated deploy pipelines eliminate manual, error-prone delivery steps — replacing them with repeatable, auditable workflows that enforce quality gates from code change to production system.**
- **Infrastructure pipelines:**
	- **VM provisioning and base image configuration**
	- **Network and policy artifacts (including firewall and routing policy updates)**
- **IOC and controls application pipelines:**
	- **Build, package, and deploy IOC software and associated configuration**
- **Phoebus Tools and Service pipelines:**
	- **Deploy and update archiver, alarm, databases, and HTTP service components**
	- **Phoebus product packaging and distribution updates**
- **Resource pipelines:**
	- **OPI screens, preferences, and configuration management artifacts**

Notes:
1. Keep domain boundaries explicit to clarify ownership and pipeline responsibility.
2. Use this slide as the operational view of how CI/CD supports the full controls stack.

## Slide 29: Summary

Charge questions addressed: CQ7 (overall design maturity and readiness for final design phase)

Slide overview:
Recap key decisions and messages, affirm readiness to proceed.

Slide 29:
- **EPICS 7 with pvAccess-first architecture is the controls baseline for new EIC systems**
- **Legacy ADO systems remain part of the near-term plan, with defined coexistence paths through AdoPvaSrv, AdoEpicsBridge, and Ado Datasource**
- **Network architecture provides the structure for scalable and maintainable operations**
- **Middle-layer services and Phoebus tooling provide the operator and integration framework for the controls stack**
- **The controls stack is designed to support long-term operability, collaboration, and phased migration during EIC construction**
- **QA/QC gates and CI/CD automation provide the delivery and governance framework needed for final design progression**

Notes:
1. This summary slide ties back to all charge questions and affirms readiness for final design phase progression.
