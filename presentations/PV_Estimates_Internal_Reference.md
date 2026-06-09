# PV Estimates - Internal Reference

## Planning statement
- EIC planning estimate: approximately **~20 million PVs**.
- ESS comparison is used as an **order-of-magnitude benchmark** (approaching ~10M-class scale).
- EIC architecture assumption: EPICS distributed IOC and service model allows horizontal scaling to this PV class when governance and operations are enforced.
- **Execution dependency:** Achieving 20M-class operations depends on disciplined standards for PV naming, IOC app structure, and CI/CD-controlled deployment.
- "EPICS distributed architecture, plus disciplined naming/IOC standards and CI/CD operations, is the basis for scaling to this range."

## Baseline context from current ADO inventory (Sep 8, 2025 snapshot)
- `All_operational`: 33,538,899 total parameters (3,227,327 set; 30,311,572 measured)
- `All_development`: 32,189,604
- `All_standby`: 3,849,380
- `All_retired`: 3,921,038
- Notes:
  - These are ADO parameter counts, not direct one-to-one EPICS PV counts.
  - These count are for RHIC and the injector complex, thus represent a larger scale than the initial EIC deployment.

## Archive sizing (planning estimate)
- Planning assumption: archive **25-33%** of total PVs.
- At ~20M PV total, archived PV range is approximately:
  - **5.0M PVs** (25%)
  - **6.6M PVs** (33%)
- Preferred strategy: hybrid model
  - shared horizontally scaled archiver services for broad coverage
  - dedicated archivers for high-rate or subsystem-isolated workloads

## Requirement references
- Requirements authority requires archive scalability to millions of control points:
  - `F-EIC-CTRL-SW-ARCH.2`: archive service shall scale to millions of control points with tiered/expandable storage.
  - `P-EIC-CTRL-SW-ARCH.1`: sustained write throughput target of 1-2M control point updates/second under nominal load.
- Requirements authority also requires horizontally scalable alarm service:
  - `F-EIC-CTRL-SW-ALRM.1`: robust, reliable, horizontally scalable central alarm management.
- EPICS ROD states distributed IOC architecture and horizontal growth model for subsystem scaling.

## Risks and mitigations
- Risk: ADO-to-PV mapping overestimates active operational PVs.
  - Mitigation: subsystem-by-subsystem reconciliation with deduplication and lifecycle filtering.
- Risk: Archive ingest/storage is undersized if high-rate channels are over-included.
  - Mitigation: define archive classes (fast/medium/slow/event) and enforce policy with deadbands/sampling modes.
- Risk: Inconsistent naming and IOC packaging causes integration overhead at scale.
  - Mitigation: enforce naming conventions, IOC templates, review gates, and CI/CD promotion pipelines.
