## Title
Adopt the Phoebus tools and services technology stack as the primary operator and middle-layer platform for EIC controls operations.

## Statement of Decision
EIC will use the Phoebus tools and services technology stack as the preferred and primary controls platform for all new EIC controls deployments, including:

- Display Builder for operator displays (OPI/HMI) and runtime execution,
- Data Browser for historical trending and correlation with live values,
- Alarm UI for alarm response workflows,
- Logbook integration via Olog clients,
- Save and Restore client tooling for state snapshot and recovery workflows,
- PV utilities and discovery workflows (Probe, PV Table, PV Tree, ChannelFinder clients).

EIC will also adopt the same Phoebus tools and services technology stack for controls operations workflows and controls data persistence, including:

- Archiver services,
- Alarm services,
- PVA Gateway,
- Olog,
- ChannelFinder,
- Save and Restore.

This decision establishes the Phoebus tools and services technology stack as the standard operator-facing and middle-layer integration layer on top of the EPICS controls architecture.

## Description / Purpose

### What This Decision Establishes and Accomplishes
This decision establishes the Phoebus tools and services technology stack as the standard modular platform for EIC operations. Phoebus is a suite of applications for monitoring and operating control systems, sharing context to enable seamless workflows across displays, alarms, history, and logging. The middle-layer services are microservices providing archiving, alarm management, and logging—complementary functions that keep IOCs focused on hardware interfacing and real-time control, while enabling client applications to focus on visualization and operational tooling.

It accomplishes the following:

- Standardizes operator workflows across alarms, history, displays, and logging in one integrated stack.
- Enables seamless workflows through context sharing (PV names, values, alarms, timestamps, archive sources).
- Aligns EIC with an actively developed EPICS-compatible stack supported across multiple facilities.
- Provides modular, independently scalable services for archiving, alarms, logging, metadata, and restore workflows.
- Supports long-term maintainability through open-source governance and versioned interfaces.

### Background
EIC operations require a coherent operator environment that spans real-time control, alarm response, post-event analysis, and configuration recovery. Running these functions through disconnected tools increases operator burden, slows diagnosis, and raises integration risk.

Phoebus addresses this by enabling seamless workflows where operators move directly between alarm investigation, historical trends, displays, and logbook documentation while preserving context—exactly aligned with EIC operational requirements.

### Phoebus Tools
The suite of Phoebus applications provides consistent, integrated operator functionality:

- **Display Builder**: OPI/HMI creation and execution with alarm-aware widgets.
- **Data Browser**: historical trending across multiple archive sources.
- **Alarm UI**: active alarm handling and acknowledgement workflow.
- **Logbook clients**: operator documentation with automatic context capture.
- **Save and Restore tool**: snapshot capture and restore workflows.
- **PV utilities**: Probe, PV Table, PV Tree for diagnostics and exploration.

Context propagation between applications (selection services) reduces manual re-entry and enables seamless workflows.

### Phoebus Middle-Layer Services
The following middle-layer services are in scope as the baseline EIC operations set within the Phoebus tools and services technology stack.

Core architectural benefits of these services are:

- **Modular:** Each service has a focused, well-defined role, making the system easier to understand and extend.
- **Flexible interfaces (HTTP, message bus,... ):** Services support both command-response and publish-subscribe models via standard REST and Kafka.
- **Data abstraction:** Client tools interact with services, not storage, enabling backend evolution without changing the user experience.
- **Optimized data handling:** Purpose-built data stores for each service domain (time-series, snapshot, etc.), improving performance and organization.
- **Interoperable by design:** Works with diverse controls clients, enabling reuse and collaboration.
- **Scalable and maintainable:** Services deploy, scale, and run independently based on facility needs.

#### Archiver Services
EIC will use EPICS Archiver Appliance services for time-series persistence and retrieval. EPICS Archiver Appliance is the default for EIC-scale deployments because it supports high channel counts, high event rates, and fine-grained per-channel configuration options. Subsystems are also expected to use Archiver Appliance, with separate instances permitted where isolation, lifecycle, or performance needs justify them.

#### Alarm Services
EIC will deploy an alarm service stack supporting:

- alarm evaluation and notification,
- alarm history logging,
- configuration history and rollback.

This enables both real-time response and retrospective tuning of alarm quality.
 
#### PVA Gateway Services
EIC will use PVA Gateway services for EPICS-domain inter-network connectivity, controlled PV exposure across network boundaries, and scalable client access patterns for PVA operations.
 
#### Olog (Online Logbook)
EIC will use Olog for structured operator and operations logging. Phoebus integration ensures alarm and PV context are automatically captured in log entries.

#### ChannelFinder
EIC will use ChannelFinder as the metadata and discovery service for PV catalogs, tags, and properties, supporting operator search and application-level data discovery.

#### Save and Restore
EIC will use save-and-restore services to capture, version, and restore PV snapshots that reproduce a known state or defined set of states for repeatable operations and controlled recovery.

### Integration with EPICS/PVA and Service Architecture
This decision is aligned with the EPICS controls ROD and its PVA-first direction:

- The Phoebus tools and services technology stack is deployed against EPICS IOC and middle-layer interfaces in the EPICS domain.
- PVA is the default client/protocol path for new workflows; CA may remain for compatibility where required.
- Services are deployed using modular microservice patterns, enabling independent scaling and fault isolation.
- Service implementation details (topology, HA profiles, backup/restore policies, and SLOs) are managed in project implementation specifications.

## Scope and Expected Impact

**Scope:**
- Phoebus tools and services technology stack applications used for EIC controls operations.
- Middle-layer services for archiving, alarms, logbook, metadata/discovery, and save/restore.
- Integration patterns between operator tools, EPICS IOCs, and service APIs.
- Deployment and lifecycle conventions for the services in production and commissioning environments.

**Expected impact:**
- Faster and more consistent operator workflows across alarm, trend, display, and logging tasks.
- Improved reliability through standardized alarm handling, historical access, and reproducible restore workflows.
- Lower integration and maintenance cost by using one shared open-source stack.
- Better scalability and resilience through independently deployable services.

## Risks and Mitigations

| Risk | Severity | Mitigation |
|------|----------|------------|
| Over-customization of Phoebus products across teams causes inconsistent UX and support burden | Medium | Define a site baseline product and controlled extension policy; require review for non-standard plugins/apps. |
| Service sprawl and uneven operational maturity across microservices | Medium | Establish service ownership, version pinning, SLOs, and production readiness checklists before deployment. |
| Alarm noise and poor configuration quality reduce operator effectiveness | Medium | Enforce alarm philosophy guidelines, periodic alarm KPI review, and use alarm history analytics for tuning. |
| Archiver sizing/performance mismatch during ramp-up | Medium | Perform staged load tests, define retention tiers, and choose implementation profile (Appliance vs alternate) based on validated channel counts. |
| Incomplete PV metadata degrades search/discovery value in ChannelFinder | Medium | Adopt naming/property standards and CI checks for mandatory metadata fields. |
| Save-and-restore misuse could apply unsafe states | Medium | Use role-based authorization, snapshot approval workflows for critical systems, and subsystem interlock constraints. |

## References and Evidence

Primary source reviewed:
- K. Shroff et al., "Phoebus: An Open Ecosystem for Control System Applications and Services." Published paper: https://indico.jacow.org/event/86/contributions/10103/

Phoebus tools and services technology stack references:
- Phoebus project site: http://www.phoebus.org
- Control System Studio / Phoebus repository: https://github.com/ControlSystemStudio/phoebus
- EPICS controls collaboration: https://epics-controls.org/

Service references:
- EPICS Archiver Appliance repository: https://github.com/archiver-appliance/epicsarchiverap
- ChannelFinder project: https://github.com/ChannelFinder
- Phoebus Olog repository: https://github.com/Olog/phoebus-olog
- Phoebus services: https://github.com/ControlSystemStudio/phoebus/tree/master/services

Related EIC decision context:
- `rod/EIC-ROD-EPICS-Control-System.md`

## Alternatives

| Alternative | Summary | Reason Not Selected |
|-------------|---------|---------------------|
| Build custom in-house operator toolkit and bespoke services | Develop EIC-specific applications and middleware from scratch | High schedule/cost risk and reduced reuse of established EPICS/Phoebus components. |
| Adopt a mixed, non-standard toolset per subsystem | Allow each subsystem to choose independent UI and services | Leads to inconsistent operator workflows, duplicated integration effort, and larger operations/support burden. |
