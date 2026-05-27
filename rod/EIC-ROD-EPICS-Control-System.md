## Title
Adopt EPICS (Experimental Physics and Industrial Control System) as the standard control system framework for the Electron-Ion Collider.

## Statement of Decision
EIC will use EPICS as its standard control system framework for all new and upgraded subsystems, covering:

- Input/Output Controllers (IOCs) for device-level hardware interfacing,
- **pvAccess (PVA) as the primary network protocol** for all new EIC controls communication, with legacy compatibility to ADO via bridge layers,
- High-level operator and application tooling in the EPICS ecosystem (including Phoebus),
- Standard EPICS middle-layer service patterns (archiving, alarms, save/restore, logging),
- Integration of legacy ADO-based subsystems through AdoPvaSrv (pvAccess ADO server) and AdoEpicsBridge (p4p-based ADO-to-EPICS bridge, primary for FEC) during the transition period.

This decision establishes EPICS with pvAccess as the primary protocol as the controls architecture foundation for the EIC. All new IOCs, services, and client applications shall be built and configured to use PVA by default.

## Description / Purpose

### What This Decision Establishes and Accomplishes
This decision establishes EPICS as the controls framework standard for EIC.

It accomplishes the following:

- Establishes a unified, distributed controls architecture scaled to the full complexity and channel count of the EIC accelerator complex.
- Aligns EIC with the same framework used by the world's major particle physics and photon science facilities, enabling direct reuse of device support libraries, drivers, and operational tools.
- Standardizes new controls communication on pvAccess (PVA), enabling structured data transport, efficient subscriptions, and modern service interfaces.
- Positions EIC to benefit from active, ongoing EPICS development, including EPICS 7 structured data (pvAccess), IPv6 networking, and TLS-secured communications.
- Reduces long-term total cost of ownership by reusing open-source modules, avoiding proprietary lock-in, and sharing development work with the broader collaboration.

### Background
The EIC accelerator complex will comprise a large number of heterogeneous subsystems — magnets, RF systems, beam diagnostics, vacuum, cryogenics, machine protection, and experiment instrumentation — each requiring real-time monitoring and control. The controls system must be scalable to millions of Process Variables (PVs), distributed across hundreds of IOC nodes, and available continuously during machine operations.

BNL's existing controls infrastructure for the RHIC facility is based on the ADO (Accelerator Device Objects) framework, a BNL-developed in-house system. ADO has served RHIC operations well but does not provide the same standardized EPICS 7 module ecosystem and PVA-first architecture targeted for EIC-scale expansion.

The EIC Project requires a controls framework that can be maintained and extended over a multi-decade operational lifetime and can directly reuse the large catalog of existing EPICS device support modules and services. EPICS meets these criteria. The choice of EPICS has been confirmed at the national level: the ICALEPCS 2023 paper by Lange et al. explicitly cites BNL's selection of EPICS for the EIC project as one of the major new adoptions of EPICS 7.

The ePIC detector collaboration has indicated EPICS as its controls-system direction. Aligning accelerator and detector controls on the same EPICS/PVA technical stack enables straightforward slow-controls data exchange through PVA gateway patterns between network domains, while preserving security boundaries. This alignment also supports common standards for PV naming, timing interfaces, alarms, and archival metadata, and reduces integration cost and schedule risk by reusing shared tools, designs, and operational experience.

### Core Technical Strengths of EPICS

#### Distributed Architecture and Scalability
EPICS is built around a fully distributed, client-server architecture in which each Input/Output Controller (IOC) operates independently, hosting a local Process Database of PVs and serving data to any client on the network. There is no central broker and no single point of failure. This design scales linearly: adding subsystems means deploying additional IOCs, not re-architecting the system.

**pvAccess (PVA)** is the primary network protocol for all new EIC communication. It is the EPICS 7 next-generation protocol and supersedes Channel Access for all new development. PVA provides:

- Transport of structured data types (scalars, arrays, images, tables) with self-describing metadata, enabling generic clients to display and process data without custom coding,
- Efficient delta-update subscriptions: only changed fields within a structure are transmitted over the network, significantly reducing bandwidth compared to CA,
- Full support for IPv6 (in the PVXS C++ and core-pva Java libraries) and a roadmap for TLS-secured connections using X.509 certificates.

**Channel Access (CA)** remains available on every EPICS 7 IOC and is retained by EIC exclusively as a compatibility and bridging layer. No new EIC subsystem shall be designed or commissioned with CA as its primary client protocol.

Both protocols run simultaneously on every EPICS 7 IOC. A PVA client and a CA client can access the same PV on the same IOC transparently, which is what makes the phased ADO migration feasible without a flag-day cutover.

#### EPICS 7: Structured Data and Modern Capabilities
EPICS 7, first released in December 2017, represents the merger of the proven EPICS V3 codebase with the new EPICS V4 (pvAccess/pvData) extensions. Its key capabilities include:

- **Normative Types:** Standard structured data types (NTScalar, NTArray, NTNDArray for images, NTTable for tabular data) that allow generic clients to display, archive, and process data without custom coding. This is directly analogous to the role of standard DBR types in EPICS V3, preserving the "configure rather than code" philosophy.
- **Efficient bandwidth use:** PVA subscriptions transmit only the changed elements of a structure, reducing network load substantially for high-frequency or large-structure updates compared to CA.
- **High-performance data acquisition:** The NTNDArray type supports multi-dimensional arrays with compression metadata, used in production at Diamond Light Source and NSLS-II for areaDetector image streams at 10 Gbps link utilisation rates.
- **Middle-layer services via RPC:** Services such as physics lattice retrieval, relational database interfaces, beam model queries, and complex transactional writes (demonstrated at ITER for 74 FPGA-based controllers) are implemented cleanly as EPICS 7 PVA services.
- **IPv6 and TLS roadmap:** IPv6 support is implemented in the PVXS (C++) and core-pva (Java) libraries. TLS-based secure connections using X.509 certificates and ACF-based access control are in active development, addressing long-term network security requirements.
- **Next-generation client libraries:** The PVXS (C++) and core-pva (Java) libraries replace the initial EPICS V4 implementations with language-idiomatic, fully documented APIs. The P4P Python binding provides convenient scripting access. CS-Studio/Phoebus uses core-pva as its default PVA client.

#### Open-Source Ecosystem: Device Support, Drivers, and Tools
A critical operational advantage of EPICS is the breadth of its open-source module catalog, directly usable by EIC without development investment:

- **Device support and hardware drivers:** Hundreds of community-maintained modules cover VME, PCI, PCIe, and Ethernet-based hardware including PLCs (Allen-Bradley, Siemens, Beckhoff), motion controllers, power supplies, digitizers, timing systems, and cryogenic instrumentation. The EPICS module repository (https://epics.anl.gov/modules) and the EPICS Tech-Talk community provide active maintenance.
- **areaDetector:** A widely deployed framework for detector and camera integration supporting dozens of camera vendors and providing PVA-native image transport. Used in production at x-ray beamlines, neutron facilities, and now planned for EIC detector instrumentation.
- **Operations tooling and services:** EPICS provides mature open-source building blocks for operator interfaces, archiving, alarms, PV metadata management, and save/restore workflows. These capabilities are in scope at a framework level for this decision; detailed tool/service architecture is defined in a separate Phoebus/tools-services ROD.

#### International Collaboration
EPICS is maintained through an open multi-laboratory collaboration, which is technically important for EIC because core components and widely used modules are continuously tested and improved across many production environments.

For EIC, this translates into lower technical risk through shared maintenance of EPICS Base, PVA libraries, and common modules, plus direct reuse of deployment patterns from existing EPICS 7 facilities.

Representative EPICS facilities include SNS, NSLS-II, APS/APS-U, LCLS-II HE, MEC-U, ESS, ITER, FRIB, RAON, Diamond Light Source, Gemini Observatory, and Fermilab PIP-II. The EIC EPICS adoption is explicitly noted in Lange et al. (ICALEPCS 2023).

### ADO Coexistence and Parallel Operation During Transition
The existing BNL ADO control system infrastructure will remain operational for RHIC and for legacy CAD subsystems during the EIC construction and commissioning phase. The bridging strategy is designed so that EPICS and ADO can exchange data without requiring an immediate full migration, while all new EIC development proceeds on PVA-first EPICS from day one.

The primary bridging mechanisms are:

- **AdoEpicsBridge / AdoPvaSrv:** ADO is a BNL-proprietary control system with its own wire protocol; it cannot be bridged to EPICS using EPICS-internal gateways. Integration requires a dedicated ADO-to-EPICS adapter layer. BNL has developed the AdoEpicsBridge (a p4p-based bridge, primary for FEC) and AdoPvaSrv (the pvAccess ADO server, server-side implementation) for this purpose: these components connect to ADO on one side using the native ADO protocol, and publish the corresponding data as EPICS PVs (accessible over PVA or CA) on the other side. This is the only supported mechanism for exposing ADO-managed devices to EPICS clients during the coexistence period. It is not intended as a permanent integration layer; each ADO subsystem migrated to a native EPICS IOC retires its AdoEpicsBridge / AdoPvaSrv entry.
- **PVA Gateway:** Based on P4P (the Python PVXS binding), the EPICS 7 PVA Gateway is the preferred gateway for new EIC inter-network connections *within the EPICS domain*. It bridges pvAccess traffic across network boundaries and has demonstrated major performance improvements over CA gateways under mixed load conditions — particularly for concurrent connections handling a mix of scalar and multi-megabyte array data — as reported from ESS commissioning in 2023 (Lange et al., ICALEPCS 2023). The PVA Gateway can also bridge IPv4 to IPv6 network segments, aligning with the US government IPv6 transition mandate.
- **CA Gateway:** The EPICS CA Gateway is an EPICS-internal proxy server that bridges Channel Access traffic across network boundaries *between EPICS CA clients and EPICS IOCs*. It has no capability to interface with ADO. For EIC its role is limited to supporting CA-speaking EPICS client tools that need to reach IOCs on isolated network segments; it is not used for ADO integration.
- **Phased IOC migration:** New subsystems are commissioned directly on EPICS IOCs with PVA as the primary protocol. Existing ADO subsystems are migrated subsystem by subsystem during scheduled maintenance periods, following a priority order based on operational criticality and subsystem lifecycle stage. As each subsystem migrates, its AdoEpicsBridge / AdoPvaSrv entry is retired.

The coexistence topology therefore has a clear directionality: all new traffic is PVA, legacy ADO devices are exposed to EPICS clients through the dedicated AdoEpicsBridge / AdoPvaSrv layer, and those entries shrink over time as native EPICS IOC migration progresses.

### Scope and Expected Impact

**Scope:**
- All new EIC controls subsystems, including but not limited to: magnets, RF, beam diagnostics, vacuum, cryogenics, timing, and machine protection interfaces.
- All IOC software, device support modules, and hardware driver integration for EIC subsystems.
- Operator interface displays, archiver configuration, and alarm management for EIC operations.
- CI/CD and configuration management for EPICS IOC software (in conjunction with the GitHub Platform ROD).
- The ADO-EPICS gateway layer during the defined coexistence period.

**Expected impact:**
- Uniform controls architecture across EIC subsystems, enabling cross-subsystem integration and shared operational tooling.
- Alignment with ePIC detector controls on EPICS/PVA, enabling lower-friction accelerator-detector slow-controls interoperability and shared standards for data, timing, and alarms.
- Reduced controls engineering risk through direct reuse of mature EPICS modules, drivers, and tested integration patterns.
- Improved long-term maintainability through open-source governance, avoiding proprietary framework lock-in.
- Operational continuity during the transition period through the CA/PVA gateway bridging strategy.

## Risks and Mitigations

| Risk | Severity | Mitigation |
|------|----------|------------|
| ADO-to-EPICS bridge complexity increases during simultaneous operations | Medium | Define AdoEpicsBridge bridge topology and PV naming conventions early; isolate ADO traffic on dedicated network segments; validate bridge performance under expected channel counts before commissioning. Note: the CA Gateway cannot bridge ADO — only the dedicated ADO2EPICS bridge / pvAccess ADO server can interface with the ADO protocol. |
| Inconsistent PVA/CA protocol usage across teams during transition | Medium | Establish site-wide PVA-default configuration across EPICS clients and services from initial deployment; enforce PVA-first convention in IOC build templates and code review policy. |
| Initial EPICS 7/PVA onboarding gap for ADO-centric teams | Medium | Provide IOC template baselines, protocol-specific coding standards, and staged subsystem migration rehearsals before operations deployment. |
| EPICS 7 PVA protocol maturity on specific hardware targets (VMEbus, RTEMS) | Low–Medium | RTEMS 6 support is now under active development by the EPICS Collaboration with APS, Gemini, and Diamond participation; mitigated by using Linux-based IOC hardware for new EIC subsystems where feasible. |
| Version and lifecycle management across a large IOC fleet | Medium | Establish EPICS base version pinning, module dependency manifests, and automated IOC build/test pipelines via GitHub Actions (per the GitHub Platform ROD). |
| Upstream EPICS module/version drift across long EIC lifecycle | Medium | Pin EPICS base and module versions per release train, run compatibility tests in CI, and schedule controlled upgrade windows with regression validation. |

## References

EPICS Framework and Architecture:
- EPICS Controls Collaboration. About EPICS. https://epics-controls.org/about-epics/
- EPICS Controls Collaboration. EPICS Module Repository. https://epics.anl.gov/modules/
- EPICS Controls Collaboration. epics-base on GitHub. https://github.com/epics-base/epics-base

Conference Papers (Attached Raw Resources):
- R. Lange et al., "Five Years of EPICS 7 – Status Update and Roadmap," *Proc. ICALEPCS 2023*, Cape Town, South Africa, TH1BCO01. doi:10.18429/JACoW-ICALEPCS2023-TH1BCO01. *(Explicitly confirms BNL EPICS selection for EIC; co-authored by K. Shroff, BNL.)*
- L. R. Dalesio et al., "EPICS 7 Provides Major Enhancements to the EPICS Toolkit," *Proc. ICALEPCS 2017*, Barcelona, Spain, MOBPL01. doi:10.18429/JACoW-ICALEPCS2017-MOBPL01. *(Documents EPICS 7 initial release, structured data capabilities, and early facility deployments.)*

Facility Adoption:
- SNS (Spallation Neutron Source, ORNL): EPICS operational since facility commissioning (~2006), EPICS 7 upgrade in progress.
- NSLS-II (Brookhaven National Laboratory): Full EPICS 7 deployment, areaDetector, Directory Service, MASAR in production; over 1 million PVs.
- APS-U (Advanced Photon Source Upgrade, ANL): EPICS 7 selected for the upgrade project.
- LCLS-II HE and MEC-U (SLAC): EPICS 7 in use; middle-layer services for physics applications.
- ESS (European Spallation Source, Sweden): Full facility deployment on EPICS 7, pvAccess as default protocol since 2023 commissioning.
- ITER (France): EPICS 7 for Magnetics Diagnostics system; 74 FPGA controllers managed via PVA RPC.
- Fermilab PIP-II: EPICS selected as the control system framework for the flagship accelerator project.
- FRIB (Facility for Rare Isotope Beams, MSU): EPICS 7 deployment.

High-Level Application Tools:
- CS-Studio / Phoebus. https://github.com/ControlSystemStudio/phoebus
- EPICS Archiver Appliance. https://slacmshankar.github.io/epicsarchiver_docs/
- areaDetector. https://areadetector.github.io/areaDetector/

Gateway and Bridging:
- EPICS CA Gateway. https://epics.anl.gov/extensions/gateway/index.php
- P4P (Python PVA Gateway based on PVXS). https://mdavidsaver.github.io/p4p/

Contextual Reference:
- Matthias Clausen, L. Dalesio, "EPICS – Experimental Physics and Industrial Control System," *ICFA Beam Dynamics Newsletter* 47, pp. 56–66, Dec. 2008.

## Alternatives

The following alternatives were evaluated and are provided for the record.

| Alternative | Summary | Reason Not Selected |
|-------------|---------|---------------------|
| **Continue and extend ADO** | Maintain BNL's existing ADO framework as the EIC control system. | ADO is not aligned with EIC's target architecture for standardized EPICS 7 modules and PVA-first structured data transport. Extending ADO would require substantial BNL-specific development and integration effort. |
| **TANGO Controls** | Adopt TANGO, the European open-source controls framework used at ESRF, ELETTRA, and others. | TANGO is a viable framework but would require larger adaptation effort for existing BNL EPICS-aligned tooling, drivers, and migration plans. EPICS provides stronger continuity with current BNL controls direction for EIC. |
| **Custom or commercial SCADA framework** | Develop a custom framework or adopt an industrial SCADA platform (e.g., WinCC OA, LabVIEW NI). | Neither path provides the physics-specific device support, community governance, or long-term sustainability of EPICS. Commercial platforms introduce vendor lock-in and licensing risk over multi-decade operational lifetimes. |
