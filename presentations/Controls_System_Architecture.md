## Slide 1: Controls System Architecture

Charge questions addressed: CQ7 (readiness framing)

Slide overview:
Title, speaker, and review context for architecture maturity.

Slide 1:
- **Controls System Architecture**
- **Kunal Shroff**
- **Software Technical Lead**
- **EIC Accelerator Controls Global Software, Networking & Computing PDR**
- **June 15-17, 2026**

Notes:
1. This talk is architecture maturity for this phase, not final implementation closure.
2. The core thread is EPICS/PVA baseline, managed ADO coexistence, and delivery governance.

Speaking notes:
This presentation focuses on controls architecture maturity for the current review phase. The objective is to show that our baseline decisions, integration boundaries, and delivery model are sufficient to proceed toward final design. I will cover the technical stack, coexistence strategy, and how we execute with QA/QC and CI/CD controls.

Detailed talking points:
- Set expectations that this is an architecture readiness briefing. The argument is that protocol baseline, coexistence strategy, and delivery governance are sufficiently defined to proceed with final design workstreams.
- Resource grounding: EPICS ROD sets EPICS with PVA-first as the controls foundation; this slide frames how that decision translates into review-phase readiness.
## Slide 2: About Me - Kunal Shroff

Charge questions addressed: N/A (speaker context)

Slide overview:
Establish role, relevant experience, and technical scope ownership.

Slide 2:
- **Controls Software Technical Lead for EIC at BNL**
- **Leads architecture and deployment strategy for controls software and operational services**
- **17 years of controls software experience**
- **Technical lead of the EPICS Phoebus Collaboration**
- **Education: M.S. Electrical and Computer Engineering, Stony Brook University**
- **Technical focus: controls architecture, EPICS/Phoebus, distributed systems, DevOps/CI/CD/automation**

Notes:
1. Keep this brief and tie credibility to platform decisions and delivery execution.
2. Transition by stating the deck focuses on architecture decisions and implementation readiness.

Speaking notes:
I serve as EIC Controls Software Technical Lead at BNL, responsible for architecture and deployment strategy for controls software and operations services. I also lead the EPICS Phoebus Collaboration, which gives us direct access to community roadmap and implementation practice. My background is in controls architecture, distributed systems, and automation-driven delivery.

Detailed talking points:
- Use this slide quickly to establish technical accountability and upstream collaboration context. That helps when answering why specific technology choices are practical over a multi-decade lifecycle.
- Resource grounding: Technical leadership across EIC and Phoebus collaboration supports alignment between local design constraints and upstream implementation realities.
## Slide 3: Charge Questions

Charge questions addressed: CQ1-CQ7

Slide overview:
Set review criteria used throughout this deck.

Slide 3:
- **CQ1: Are requirements sufficiently defined and documented for this phase?**
- **CQ2: Do designs meet the requirements?**
- **CQ3: Are interfaces sufficiently defined?**
- **CQ4: Are design analysis and plans sufficient for this phase?**
- **CQ5: Have technical risks and mitigations been identified?**
- **CQ6: Are ES&H and Quality plans sufficient?**
- **CQ7: Is maturity sufficient to proceed to final design?**

Notes:
1. Call out that each technical section maps back to these questions.

Speaking notes:
These are the review questions guiding the presentation, from requirements and interfaces through risk, quality, and readiness. Each section of the talk maps explicitly to one or more charge questions. The key point is that we are showing phase-appropriate maturity, not claiming complete final-design closure.

Detailed talking points:
- Map CQ coverage to the talk structure so the panel sees traceability from requirements through implementation planning. Keep this tight and transition to scope.
- Resource grounding: CQ mapping is backed by explicit decision records and requirement families, enabling auditable response paths during panel questioning.
## Slide 4: Outline

Charge questions addressed: CQ7

Slide overview:
Roadmap from architecture baseline to execution and readiness.

Slide 4:
- **Scope**
- **Architecture**
- **EPICS**
- **ADO coexistence, tradeoffs, decision matrix**
- **Network architecture and subnet strategy**
- **EPICS IOC continuity and pvAccess value**
- **Middle-layer services**
- **Phoebus toolkit**
- **CI/CD governance, automation stack, QA/QC, pipelines**
- **Path forward and summary**

Notes:
1. Signal that the sequence moves from technical baseline to delivery confidence.

Speaking notes:
The flow is intentional: scope and requirements first, then architecture and technology choices, then coexistence and networking, then services and operator tooling, and finally delivery governance. This structure supports a clear argument from technical baseline to execution confidence.

Detailed talking points:
- Present the sequence as deliberate: define scope, justify architecture, show coexistence and networking, then prove delivery controls. This shows maturity is treated as both technical and operational.
- Resource grounding: The architecture narrative mirrors decision boundaries in EPICS, Phoebus, and GitHub platform RODs to avoid scope overlap or ambiguity.
## Slide 5: Scope

Charge questions addressed: CQ1-CQ7

Slide overview:
Define architecture topics in scope for this review phase.

Slide 5:
- **Controls system baseline (EPICS 7, PVA-first)**
- **EPICS + legacy ADO coexistence strategy**
- **Middle-layer services and operator tooling**
- **Network and infrastructure architecture**
- **CI/CD and governance model**

Notes:
1. Clarify this is architecture scope, with subsystem implementation details handled in domain reviews.

Speaking notes:
This review covers controls baseline architecture, EPICS and ADO coexistence, middle-layer services, operator tooling, network boundaries, and governance pipeline. Detailed subsystem implementation specifics remain in domain reviews. The focus here is integrated architecture and readiness.

Detailed talking points:
- Clarify scope boundaries: this deck defines architecture contracts and integration direction; subsystem-level implementation details remain in domain design packages. This avoids over-claiming closure at this review stage.
- Resource grounding: Scope reflects three decision planes: protocol/migration boundary, operator-service boundary, and delivery-governance boundary.
## Slide 6: Requirements

Charge questions addressed: CQ1, CQ3

Slide overview:
Anchor claims to current PRD sources.

Slide 6:
- **Initial versions of Performance Requirements Documents (PRDs)**
- **High Level Applications [EIC-SEG-RSI-158]**
- **Networking and Computing [EIC-SEG-RSI-124]**

Notes:
1. Use `EIC-SEG-RSI-158` as the authority for application and operational requirements.
2. Treat unverified performance values as assumptions unless explicitly cited.

References:
- Requirements authority: [supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt](../supporting-docs/EIC-SEG-RSI-158-Control.Software-Performance.Requirements.Document.txt)

Speaking notes:
Requirements are anchored in current PRDs, with application and operations requirements based on `EIC-SEG-RSI-158` and networking/computing references including `EIC-SEG-RSI-124`. For this talk, claims are either tied to those sources or identified as assumptions where data is still being finalized.

Detailed talking points:
- Anchor requirement and performance statements to `EIC-SEG-RSI-158` and companion PRDs. Mention that demonstration-level targets are on the verification path, while architecture decisions are already fixed enough for downstream planning.
- Resource grounding: RSI-158 remains authority for capability/performance requirements while RODs establish architecture and governance decisions for implementation.
## Slide 7: Control System Architecture (Reference View)

Charge questions addressed: CQ1-CQ5

Slide overview:
Three-layer stack with cross-links to relevant ROD and companion talks.

Slide 7:
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA, ADO compatibility)**
- **References shown on slide: [EIC-ROD-069], [Talk-12-Shroff], [Talk-11-Nemesure], [EIC-ROD-056]**

Notes:
1. Explain this is the integration view used across talks, not a new architecture.
2. Assumption: slide reference tags map to final PDR reference list in the deck.

Speaking notes:
This is the three-layer integration model used across the controls talks: operator/applications, middle-layer services, and controls protocol layer. The references on this slide align this talk with related RODs and companion presentations. The message is architectural consistency across workstreams.

Detailed talking points:
- Reinforce the three-layer model as the stable integration contract across talks. Operator tools, middle-layer services, and control protocols each have distinct ownership and scaling behavior.
- Resource grounding: Layering aligns with ROD text: tools above services above controls protocols, with explicit coexistence mechanisms for ADO transition.
## Slide 8: Control System Architecture (Operational View)

Charge questions addressed: CQ1-CQ5

Slide overview:
Same layered model with final wording for EPICS PVA-first and CA compatibility.

Slide 8:
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Use this slide to reinforce that PVA-first does not remove CA compatibility needs.

Speaking notes:
This repeats the layered view with finalized wording: EPICS 7 with PVA-first and CA compatibility. The point is that modern default and compatibility support coexist in a deliberate operating model. It gives us forward path without disconnecting legacy workflows.

Detailed talking points:
- Use this operational wording slide to emphasize PVA-first with CA compatibility, not CA parity. New workflows default to PVA; compatibility is retained where transition support is required.
- Resource grounding: EPICS ROD states CA remains compatibility-only while new development defaults to PVA, which is the key operational distinction on this slide.
## Slide 9: EPICS Control System

Charge questions addressed: CQ1, CQ2

Slide overview:
EPICS fundamentals, scalability, and ecosystem maturity.

Slide 9:
- **Open-source control system toolkit for accelerators and large experiments**
- **Distributed IOC model with hardware-facing control logic**
- **Client/server and publish-subscribe communication model**
- **Scalable modular deployment**
- **Large ecosystem of modules, drivers, and tools**
- **Long-term active multi-lab collaboration**

Notes:
1. Keep this as baseline capability, then specialize for EIC on the next slides.

Speaking notes:
EPICS provides a proven distributed IOC model, modular scaling, and a mature ecosystem of tools and drivers. Its long-term multi-lab collaboration reduces lifecycle risk and improves supportability. This slide establishes EPICS as a stable platform choice before EIC-specific mapping.

Detailed talking points:
- Present EPICS as the distributed controls foundation: independent IOCs, modular scaling, large module ecosystem, and long-lived multi-lab operations history. Keep this as platform baseline before EIC-specific fit.
- Resource grounding: EPICS ROD emphasizes distributed IOC architecture, ecosystem reuse, and long-lived multi-lab operations as primary risk-reduction factors.
## Slide 10: EPICS for EIC (Functional + Reliability)

Charge questions addressed: CQ1-CQ4

Slide overview:
Map EPICS capabilities to EIC functional and operations needs.

Slide 10:
- **Functional support: distributed IOC model for heterogeneous subsystems**
- **PVA path for structured data exchange and service integration**
- **Normative Types (`NTScalar`, `NTArray`, `NTNDArray`, `NTTable`) and libraries (`PVXS`, `core-pva`, `p4p`)**
- **Reliability support via distributed IOC/service deployment with redundancy options**
- **Delta subscriptions reduce network load for structured updates**
- **Mature operations tooling ecosystem supports maintainability**

Notes:
1. Emphasize fit-for-purpose architecture rather than protocol preference alone.

Speaking notes:
For EIC, EPICS supports heterogeneous subsystem integration through distributed IOCs and structured PVA exchanges. Normative Types and client libraries let us build generic, service-oriented tooling across C++, Java, and Python. Reliability comes from distributed deployment and reduced data movement via delta subscriptions.

Detailed talking points:
- Tie EPICS fit to EIC needs: structured-data integration via normative types and language libraries, distributed deployment for reliability, and tooling ecosystem support for operational maintainability.
- Resource grounding: EPICS ROD details normative types and modern libraries (`PVXS`, `core-pva`, `p4p`) as the structured-data interoperability baseline.
## Slide 11: EPICS for EIC (Performance + Collaboration)

Charge questions addressed: CQ1-CQ4

Slide overview:
Performance scaling model and collaboration reuse argument.

Slide 11:
- **Periodic scan support up to 10 Hz in default periodic mode**
- **Horizontal scaling across IOCs, services, and clients**
- **Global EPICS ecosystem for modules, drivers, and extensions**
- **Distributed expertise reduces single-site dependency risk**
- **Reusable deployment patterns from ESS, NSLS-II, ITER, APS-U, PIP-II**

Notes:
1. For any requirement claim above these baseline values, cite `EIC-SEG-RSI-158` or mark as assumption.

Speaking notes:
Baseline periodic scan behavior supports up to 10 Hz in standard periodic mode, while architecture scales horizontally across IOCs and services. We also benefit from deployment patterns already exercised at major facilities, which lowers adoption risk. Any higher-performance claims should remain explicitly traceable to requirement documents or test evidence.

Detailed talking points:
- Explain performance and collaboration together: baseline periodic scan behavior and horizontal scaling model, backed by deployment patterns reused from major facilities. Distinguish demonstrated architecture capability from site-specific performance closure still under test plans.
- Resource grounding: EPICS ROD cites reuse of EPICS 7 deployment patterns from major facilities as practical evidence for scale-out planning.
## Slide 12: pvAccess Protocol for EIC

Charge questions addressed: CQ1-CQ4

Slide overview:
Protocol-level capabilities needed for modern services and rich data.

Slide 12:
- **Structured data transport with metadata (scalars, arrays, tables, images)**
- **Efficient subscriptions transfer changed fields**
- **RPC-style workflow support**
- **High-bandwidth support for payloads such as `NTNDArray`**
- **Library support: `PVXS`, `core-pva`, `p4p`; IPv6 support; planned TLS-secured connections**

Notes:
1. Present TLS status as planned/roadmap unless validated as deployed for this scope.

Speaking notes:
pvAccess is the protocol foundation for structured, metadata-rich exchange and service-oriented workflows. It supports efficient subscriptions and large payloads such as imaging and `NTNDArray`, which are important for modern operations and diagnostics. TLS is framed as planned capability unless explicitly demonstrated in deployed scope.

Detailed talking points:
- Describe pvAccess as the protocol enabling structured transport, efficient delta subscriptions, and RPC-style service interactions. Keep TLS language roadmap-oriented unless deployment evidence is explicitly available for this phase.
- Resource grounding: EPICS ROD describes PVA structured transport, delta subscriptions, IPv6 support, and TLS roadmap as protocol-level modernization drivers.
## Slide 13: ADO Control System

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Legacy system continuity and operational maturity basis.

Slide 13:
- **RHIC ADO origins in early 1990s distributed client/server architecture**
- **High-level services: operator interfaces, sequencing, alarms, archiving, logbook**
- **Low-level control via VME/ADO on VxWorks**
- **~25 years of operations with staged upgrades (including FPGA-based LLRF)**
- **Active use for hadron injection controls, including BLIP-related operations**

Notes:
1. Frame ADO as valuable operational asset during migration, not a competing future baseline.

Speaking notes:
ADO has decades of operational history and remains active for hadron injection and related workflows during construction. The purpose of this slide is continuity, not replacement of EPICS baseline. We retain operational value while migration proceeds in controlled phases.

Detailed talking points:
- Frame ADO as an active operational asset during transition. The message is continuity plus staged migration, not replacement rhetoric.
- Resource grounding: EPICS ROD explicitly treats ADO as a coexistence-era operational system while migration proceeds subsystem by subsystem.
## Slide 14: Dual System Architecture (Need and Plan)

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Why dual-system architecture is deliberate in this phase.

Slide 14:
- **EIC luminosity goals require controls modernization**
- **Software strategy prioritizes maintainability over 30+ year lifecycle**
- **Near-term model: legacy ADO continuity plus EPICS/PVA delivery and phased migration**
- **Slide references [Talk-8/10-Kabir] for supporting context**

Notes:
1. Assumption: this diagram matches the network/migration narrative used in the Kabir talk.

Speaking notes:
The dual-system plan is intentional: EIC performance goals and lifecycle expectations require modernization, while existing operations must remain stable. The near-term architecture therefore supports ADO continuity and EPICS/PVA growth in parallel. Migration is phased rather than disruptive.

Detailed talking points:
- Use this as strategic justification for dual-system operations: modernization requirements and lifecycle maintainability must be balanced against ongoing mission operations. The coexistence period is intentionally engineered.
- Resource grounding: ROD migration language defines coexistence as directional: new traffic PVA-first, legacy ADO exposure through approved bridge patterns.
## Slide 15: Dual System Architecture (Strategy 1: AdoPvaSrv)

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Distributed per-manager pvAccess exposure.

Slide 15:
- **AdoPvaSrv on each ADO Manager**
- **No central broker/gateway requirement**
- **Horizontal scaling model**
- **Supports iterative rollout**

Notes:
1. Position as low-central-infrastructure path with distributed ownership.

Speaking notes:
AdoPvaSrv exposes pvAccess at each ADO manager and avoids centralized broker infrastructure. It is distributed and can be rolled out incrementally. This strategy favors local ownership and simpler central dependencies.

Detailed talking points:
- Strategy 1 (`AdoPvaSrv`) is the distributed per-manager path with lower central infrastructure dependency. Highlight incremental rollout practicality and local ownership model.
- Resource grounding: Strategy 1 aligns with server-side ADO-to-PVA exposure (`AdoPvaSrv`) and favors distributed rollout without central broker dependency.
## Slide 16: Dual System Architecture (Strategy 2: AdoEpicsBridge)

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Bridge-based EPICS-side integration for ADO devices.

Slide 16:
- **p4p bridge exposing ADO devices as EPICS PVs over PVA**
- **No required changes to existing ADO devices/managers**
- **Primarily used for FEC**
- **Requires bridge cluster plus load balancer**
- **Higher infrastructure investment, but achievable model**

Notes:
1. Use this slide to discuss tradeoff: infrastructure cost versus protocol transparency for clients.

Speaking notes:
AdoEpicsBridge provides EPICS-side unification by exposing ADO devices as EPICS PVs, without changing existing ADO devices and managers. It is effective for FEC use cases but needs bridge clusters and load balancing. The tradeoff is higher infrastructure footprint for cleaner client-facing protocol abstraction.

Detailed talking points:
- Strategy 2 (`AdoEpicsBridge`) provides EPICS-facing unification without modifying legacy ADO endpoints, but requires clustered bridge infrastructure. This is the tradeoff slide: cleaner client abstraction versus additional infrastructure overhead.
- Resource grounding: EPICS ROD names p4p-based ADO bridge as primary for FEC, with infrastructure planning required for clustered deployment models.
## Slide 17: Dual System Architecture (Strategy 3: Ado Datasource)

Charge questions addressed: CQ3, CQ4, CQ5

Slide overview:
Tool/service-layer ADO access via core libraries.

Slide 17:
- **ADO protocol client in `core-pv`**
- **No changes to ADO devices/managers**
- **Integration at tools and services layer**
- **No central broker/gateway requirement**

Notes:
1. Highlight fit when teams want application-layer integration with minimal infrastructure.

Speaking notes:
Ado Datasource integrates at tool and service layer through `core-pv` ADO client support. It also preserves existing ADO infrastructure and avoids centralized broker components. This is often the lower-infrastructure path where application-layer integration is sufficient.

Detailed talking points:
- Strategy 3 (`Ado Datasource`) moves integration into tools/services through `core-pv`, with minimal central infrastructure. Position it as fit-for-use where application-layer integration is the priority.
- Resource grounding: Application-layer datasource strategy aligns with Phoebus/CorePV extension philosophy for controlled protocol abstraction in tools/services.
## Slide 18: Network Architecture and Subnet Strategy (Part 1)

Charge questions addressed: CQ1, CQ2

Slide overview:
Network goals and first part of subnet model.

Slide 18:
- **Scalable connectivity for distributed and clustered components**
- **Segmentation across controls, instrumentation, and data services**
- **Controls subnet: IOC, ADO Manager, gateway, command/control traffic**
- **Instrumentation subnet: acquisition and timing-sensitive interfaces**
- **Slide references [Talk-6/7-Kulmatycski]**

Speaking notes:
We are aware of the challanges the size (both geographic and # of devices) of the eic controls system will pose to the network. The controls network as a private, structured stub network for EIC controls. It provides scalable connectivity for distributed components while segmenting controls traffic from instrumentation and data services. The controls subnet hosts IOCs, ADO managers, gateways, and command/control traffic, while instrumentation subnets handle acquisition and timing-sensitive interfaces.
Full implementation details are owned by the network architecture talk.

## Slide 19: Network Architecture and Subnet Strategy (Part 2)

Charge questions addressed: CQ1, CQ2

Slide overview:
Security boundaries and coexistence placement implications.

Slide 19:
- **Controlled cross-subnet access through gateways and service endpoints**
- **Monitoring and observability at subnet and service boundaries**
- **ADO server/bridge cluster placement for low-latency legacy access**
- **EPICS/PVA services scaled on service networks**
- **Operator tools consume unified interfaces independent of backend protocol location**

Speaking notes:
We keep the controls fabric separate from the campus network, and any externally managed services cross only through a controlled gateway/firewall boundary. Monitoring and observability are focused at subnet and service boundaries to maintain visibility without overexposing internal traffic. ADO server/bridge clusters are placed for low-latency access to legacy systems, while EPICS/PVA services scale on the service network.The message here is that the facility will have a dedicated controls network, independent of the campus network and anchored at Bldg 1003a. We are not starting from scratch: the design builds on RHIC/CAD experience, with BNL ITD as the engineering partner under an MOU/SLA.

## Slide 20: Middle-Layer Services (Layered Context)

Charge questions addressed: CQ1, CQ2, CQ3

Slide overview:
Service layer placement in the full controls stack.

Slide 20:
- **Operator and application layer (Phoebus, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**
Speaking notes:
- This is the same layered model as before, but now we are zooming in on the middle-layer services. The point is to show how these services sit between the control system protocols and the operator-facing tools, providing critical functionality and abstraction that supports maintainability and scalability.


## Slide 21: Middle-Layer Services (Service Model Benefits)

Charge questions addressed: CQ1, CQ2, CQ3

Slide overview:
Why the service-oriented model is maintainable and scalable.

Slide 21:
- **Modular focused services**
- **Flexible command-response and publish-subscribe interfaces**
- **Data abstraction between tools and storage internals**
- **Purpose-built stores by domain (time-series, alarms, snapshots, metadata)**
- **Consistent service contracts across client environments**
- **Independent deployment and scaling by demand**

Speaking notes:
The service model improves maintainability through modular roles and consistent APIs. It enables backend evolution without breaking operator workflows and supports scaling by service demand. Interoperability is designed into contracts rather than added later.

Detailed talking points:
- Use service-model benefits to justify maintainability: modular ownership, consistent APIs, and independent scaling reduce coupling and support phased evolution. Mention that service contracts are as important as protocol choices.
- Resource grounding: MOCR002 service model highlights modularity, independent scaling, and fault isolation as reasons to avoid monolithic middleware.

## Slide 22: Middle-Layer Services (Service Roles)

Charge questions addressed: CQ1, CQ2, CQ3

Slide overview:
Specific responsibilities of core services.

Slide 22:
- **Archiver: time-series storage and fast historical query support**
- **Alarm: real-time monitoring, notification, history, configuration rollback**
- **ChannelFinder: PV catalog, tags, properties**
- **NameOps: EIC naming generation and validation**
- **Olog: structured operational logging with context capture**
- **Save/Restore: known-good state snapshots and recovery workflows**
- **PVA Gateway: controlled cross-network PV exposure**

Notes:
1. Tie each service role to operator workflow outcomes (faster diagnosis, safer recovery, traceability).

Speaking notes:
This slide defines concrete responsibilities for Archiver, Alarm, ChannelFinder, NameOps, Olog, Save/Restore, and PVA Gateway. Each service maps to a specific operational outcome: visibility, response quality, discoverability, traceability, repeatability, and controlled access. Together they provide the operational fabric for the stack.

Detailed talking points:
- Define service roles in operational terms: archiver for post-event evidence, alarm stack for response quality, channel metadata for discoverability, logbook for traceability, save/restore for reproducibility, gateway for controlled exposure.
- Resource grounding: Service roles in the Phoebus ROD map directly to operational outcomes: time-series evidence, alarm response, metadata discovery, traceable logging, reproducible restore, and controlled exposure.
## Slide 23: Phoebus Operator Toolkit (Layered Context)

Charge questions addressed: CQ1, CQ2, CQ3

Slide overview:
Placement of operator toolkit above services and controls layer.

Slide 23:
- **Operator and application layer (Phoebus tools, web tools, HLAs)**
- **Middle-layer services (Archiver, Alarm, Olog, ChannelFinder, Save/Restore, Gateway)**
- **Control system layer (EPICS 7 with PVA-first, CA compatibility)**

Notes:
1. Use this to transition from architecture stack to operator experience.

Speaking notes:
Phoebus sits in the operator/application layer above services and controls protocols. The point is to show clear boundaries while preserving end-to-end workflow continuity. This sets up the next slides on operator outcomes.


## Slide 24: Phoebus Operator Toolkit (Strategic Benefits)

Charge questions addressed: CQ1, CQ2, CQ3, CQ5

Slide overview:
Integrated workflow, extensibility, and maintainability value proposition.

Slide 24:
- **Integrated tools across displays, alarms, trends, logbook, save/restore**
- **Seamless navigation and context sharing across tools**
- **Reduced training and support burden with unified desktop**
- **SPI extensibility for adding tools/protocols without destabilizing core**
- **Shared data models/resources for efficiency**
- **Active collaboration improves long-term supportability**

Notes:
1. Keep benefits tied to operations outcomes and lifecycle sustainability.

Speaking notes:
Phoebus provides integrated navigation across displays, alarms, trends, logging, and recovery workflows. Shared context and common UI patterns reduce training burden and speed troubleshooting. SPI extensibility and active collaboration support long-term sustainability.

Detailed talking points:
- Highlight integrated workflows and shared context as the main productivity gain. Extensibility via SPI and active collaboration are the lifecycle sustainability mechanisms.
- Resource grounding: SPI-based extensibility plus active collaboration is the sustainability mechanism identified in MOCR002 and the Phoebus ROD.
## Slide 25: Phoebus Operator Toolkit (Applications)

Charge questions addressed: CQ1, CQ3, CQ7

Slide overview:
Application-level capabilities delivered in the operator environment.

Slide 25:
- **Display Builder: OPI/HMI editor/runtime with alarm awareness and migration support**
- **Data Browser: multi-provider trending and live/historical correlation**
- **Alarm UI: real-time alarm views and annunciation**
- **Olog UI: structured logbook with automatic operational context**
- **PV Utilities: Probe, PV Table, PV Tree diagnostics**
- **ChannelFinder Client: metadata-enriched PV discovery**
- **Save/Restore UI: snapshot versioning and restoration workflows**

Notes:
1. Emphasize seamless operator flow across these applications.

Speaking notes:
These are the concrete user-facing applications: Display Builder, Data Browser, Alarm UI, Olog UI, PV utilities, ChannelFinder client, and Save/Restore UI. The central message is workflow continuity with context carried across tools. That directly improves operator effectiveness and incident response.

Detailed talking points:
- Treat this as concrete tool capability coverage rather than a feature list. Emphasize how the applications work together during real operations and troubleshooting flows.
- Resource grounding: MOCR002 application set and Phoebus ROD decision scope align on Display Builder, Data Browser, Alarm UI, Olog, PV utilities, and Save/Restore.
## Slide 26: Web Tools

Charge questions addressed: CQ1, CQ3, CQ7

Slide overview:
Why web tools complement (not replace) desktop operations.

Slide 26:
- **Phoebus desktop remains primary rich operator environment**
- **Web tools provide easier access and lightweight deployment paths**
- **`pvws` and `dbwr` for web display and archive-oriented views**
- **Web clients for Olog, `etraveller`, and component database workflows**
- **`pvinfo` for web/CLI metadata and connection status lookup**

Notes:
1. Keep role split explicit: desktop for integrated control-room workflows, web for reach and flexibility.

Speaking notes:
Web tools complement, not replace, the desktop operator environment. They expand access for lightweight views, remote use, and broader stakeholder interaction through tools such as `pvws`, `dbwr`, Olog web clients, and `pvinfo`. This is a coverage and usability extension of the same architecture.

## Slide 27: QA/QC

Charge questions addressed: CQ1, CQ6, CQ7

Slide overview:
Quality controls from change proposal to release promotion.

Slide 27:
- **Code review gates with templates, checklists, mandatory approvals**
- **Unit tests for per-component validation and conformance**
- **Integration tests for IOC + gateway + services interactions**
- **Promotion gates require passing test suites with traceable artifacts**
- **Versioned automation enables reproducible dev/test environments**

Speaking notes:
these slides should show how quality and delivery controls turn architecture into reliable operations.
We need QA/QC to start at code review and continue through unit testing, integration testing, and release promotion so that every change is validated before it reaches production. The key idea is reproducibility: versioned automation gives us traceable artifacts and repeatable dev/test environments, which is what lets us trust the release path rather than relying on ad hoc acceptance.

- QA/QC is part of architecture execution control: review gates, unit/integration validation, and promotion rules reduce commissioning and operations risk. This is implementation discipline, not optional process overhead.


## Slide 28: CI/CD and Automation Stack

Charge questions addressed: CQ1, CQ6, CQ7

Slide overview:
Governance and execution stack for repeatable controls delivery.

Slide 28:
- **Purpose: standardize delivery, reduce integration risk, improve traceability**
- **GitHub change control: PR reviews, branch protection, CODEOWNERS, history**
- **GitHub Actions orchestration: build/test/package/deploy, reusable workflows**
- **Ansible/AWX + IaC: desired-state automation, managed execution, auditable updates**

Notes:
1. Tie directly to `EIC-ROD-GitHub-Platform` governance commitments.

References:
- GitHub platform decision record: [rod/EIC-ROD-GitHub-Platform.md](../rod/EIC-ROD-GitHub-Platform.md)

Speaking notes:
This slide is the governance layer that makes QA/QC operational. GitHub provides the change-control discipline through pull requests, branch protection, CODEOWNERS, and history, while GitHub Actions provides the orchestration for build, test, package, and deploy workflows.
Ansible/AWX and Infrastructure as Code give us the ability to automate desired-state configuration and deployment with managed execution and auditable change history. Together, this stack standardizes delivery, reduces integration risk, and improves traceability.

## Slide 29: CI/CD Pipelines

Charge questions addressed: CQ1, CQ6, CQ7

Slide overview:
Pipeline domains for infrastructure, controls software, services, and configuration assets.

Slide 29:
- **Infrastructure: VM provisioning, base images, network/policy artifacts**
- **IOC/controls applications: build, package, deploy software and configuration**
- **Phoebus tools/services: archiver/alarm/database/HTTP deployments and product packaging**
- **Resource pipelines: OPI screens, preferences, configuration management artifacts**

Notes:
1. Emphasize that automation replaces manual, error-prone release steps with auditable gates.

Speaking notes:
Pipeline domains cover infrastructure, IOC and controls software, Phoebus services/products, and configuration resources like OPI artifacts. The purpose is eliminating manual, error-prone release steps in favor of quality-gated automation. This supports consistency at scale across controls domains.

Detailed talking points:
- Use pipeline domains to demonstrate system-level completeness: infrastructure, IOC software, services/products, and operational resources. Automation replaces manual drift with quality-gated releases.
- Resource grounding: Domain pipelines (infrastructure, IOC, services, resources) map to architecture ownership boundaries and reduce manual-release variability.
## Slide 30: Summary

Charge questions addressed: CQ7

Slide overview:
Close with baseline decisions and readiness message.

Slide 30:
- **EPICS 7 with pvAccess-first is the baseline for new EIC systems**
- **Legacy ADO remains in near-term plan with defined coexistence paths**
- **Network architecture supports scalable, maintainable operations**
- **Middle-layer services plus Phoebus provide operator and integration framework**
- **Architecture supports long-term operability and phased migration during construction**
- **QA/QC and CI/CD governance support progression to final design**

Notes:
1. Close by reaffirming progression readiness while noting implementation remains phased.

## Talking Notes Appendix (Condensed Script)

Use these one-line transitions when rehearsing:

- **1 -> 2:** Introduce architecture scope, then establish speaker ownership and relevant experience.
- **2 -> 3:** Move from speaker context to review criteria.
- **3 -> 6:** Set scope and requirements authority before technical detail.
- **7 -> 13:** Walk architecture baseline first, then EPICS and ADO capability framing.
- **14 -> 17:** Explain dual-system need, then evaluate coexistence strategies.
- **18 -> 22:** Transition from network boundaries to service-layer implementation.
- **23 -> 26:** Move from architecture placement to operator-facing toolkit and web access.
- **27 -> 29:** Show quality and delivery controls that convert architecture into reliable operations.
- **29 -> 30:** End with readiness message tied to charge questions.

Speaking notes:
The baseline is EPICS 7 with PVA-first for new systems, with controlled coexistence paths for legacy ADO. Network and service architecture provide scalable operations, and Phoebus provides operator-facing integration. QA/QC and CI/CD governance provide the execution confidence needed to proceed toward final design.
## CQ Traceability Matrix

| Slide(s) | Primary CQ(s) | Evidence / Basis |
|---|---|---|
| 1, 4, 30 | CQ7 | Deck framing and readiness summary |
| 3 | CQ1-CQ7 | Charge question statements |
| 5-6 | CQ1, CQ3 | PRDs, `EIC-SEG-RSI-158`, `EIC-SEG-RSI-124` |
| 7-8 | CQ1-CQ5 | Layered architecture and integration references |
| 9-12 | CQ1-CQ4 | EPICS/PVA capabilities and ecosystem basis |
| 13-17 | CQ3-CQ5 | ADO continuity and coexistence strategies |
| 18-19 | CQ1-CQ2 | Network/subnet architecture and boundary controls |
| 20-22 | CQ1-CQ3 | Middle-layer service model and service roles |
| 23-26 | CQ1, CQ2, CQ3, CQ5, CQ7 | Operator toolkit architecture and workflow support |
| 27-29 | CQ1, CQ6, CQ7 | QA/QC gates, CI/CD governance, domain pipelines |

## Optional Short Cues (30-45 seconds per slide)

- 1: Maturity scope and desired review outcome.
- 2: Why I am accountable for this architecture.
- 3: CQ map for the rest of the deck.
- 4-6: Scope and requirement anchors.
- 7-12: EPICS/PVA technical baseline and fit.
- 13-17: ADO continuity plus three coexistence patterns.
- 18-19: Network segmentation and integration boundaries.
- 20-22: Service architecture and operational roles.
- 23-26: Operator workflows across desktop and web.
- 27-29: Quality and delivery controls.
- 30: Readiness statement and transition to Q&A.

## 30-Minute Delivery Plan (Presenter Timing)

| Segment | Slides | Target Time |
|---|---|---|
| Opening, CQ framing, scope | 1-6 | 5 min |
| Architecture and EPICS/PVA baseline | 7-12 | 8 min |
| ADO coexistence strategies | 13-17 | 6 min |
| Network and service architecture | 18-22 | 5 min |
| Phoebus/operator layer | 23-26 | 3 min |
| QA/QC, CI/CD, and close | 27-30 | 3 min |

Detailed talking points:
- Close with a concise readiness claim: architecture baseline is set, coexistence strategy is explicit, network/service/operator layers are aligned, and delivery governance is in place for next-phase execution.

## Panel Q&A One-Page (Quick Reference)

- **Why EPICS/PVA-first?** Structured data, scalable distributed IOC model, and strong ecosystem reuse align with EIC lifecycle and integration needs.
- **Why not immediate ADO cutover?** Operational continuity requires staged coexistence; bridge and datasource strategies provide controlled migration without flag-day risk.
- **How are protocol boundaries managed?** PVA is default for new workflows; CA remains compatibility-only where needed during transition.
- **How does this map to requirements?** `EIC-SEG-RSI-158` families are reflected across OPI, alarm, archiver, directory, save/restore, logbook, gateway, and HLA integration flows.
- **What gives confidence in execution?** QA/QC gates plus CI/CD and IaC practices provide traceable, repeatable delivery from change proposal through deployment.
- **Where are the biggest remaining uncertainties?** Subsystem-specific performance closure and phased migration sequencing remain active verification topics, not architectural blockers.
- **How do services improve operations?** They decouple user workflows from storage/protocol internals, allowing independent scaling, better fault isolation, and stable operator UX.
- **What should panel remember?** The architecture is designed for phased delivery now and maintainable evolution over long facility lifetime.
- Resource grounding: Combined decisions are coherent: EPICS/PVA-first baseline, managed ADO coexistence, standardized services/tooling, and governed delivery model.

