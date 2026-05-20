# Record of Decision: GitHub Platform for EIC Controls, Configuration, and CI/CD

## Title
Adopt GitHub and Git-based source code management as the primary platform for EIC controls code, configuration resources, CI/CD, and release management workflows.

## Statement of Decision
EIC will use GitHub as the primary platform for:
- Git-based source code management for controls code and configuration resources,
- CI/CD workflow automation,
- release creation and release management,
- collaborative development across internal and external contributors.

This decision establishes Git-based repository workflows and GitHub-native automation as a foundation of the EIC infrastructure-as-code approach.

## Description / Purpose

### What This Decision Establishes and Accomplishes
This decision establishes Git as the common version-control model and GitHub as the EIC standard platform for controls code, configuration resources, and CI/CD workflows.

It sets a single collaboration and governance model for repositories used by EIC teams and collaborators, and it accomplishes the following:
- Establishes GitHub as the shared system of record for controls source code and configuration resources.
- Standardizes change management through pull requests, branch protections, and CODEOWNERS-based ownership.
- Enables consistent CI/CD automation with reusable workflows.
- Establishes a consistent release management pattern using tags, releases, and release evidence.
- Improves traceability by linking code changes, reviews, workflow runs, and build evidence in one platform.
- Supports both private/internal repositories and selective public collaboration.

### Background
EIC controls and infrastructure work depends on software, configuration, and operational logic that change continuously during design, integration, and operations.

Without a single Git-based source-control model and shared collaboration platform, teams face increased risk of:
- inconsistent change records across code and configuration assets,
- reduced traceability from requirement to implementation and deployment,
- uneven review quality and governance across repositories,
- slower integration due to manual handoffs and tool fragmentation,
- higher operational risk when rollback and reproducibility are not standardized.

This decision addresses those gaps by defining a common approach for version control, collaboration, and delivery automation.

### Git-Based Source Code Management
Git is the source code management foundation for this decision. SCM is the practice of maintaining versioned, traceable history of code and related configuration changes, and Git provides the core mechanism for doing this reliably.

For EIC, Git-based SCM is required to:
- maintain an immutable commit history that shows what changed, when, and by whom,
- support branch-based development so teams can work in parallel with controlled integration,
- enable pull request review workflows before changes are merged,
- provide reproducibility through tags and commit references for releases and operations,
- support rapid rollback to known-good revisions when regressions are introduced,
- establish auditable configuration control for controls and infrastructure resources.

### Continuous Integration and Continuous Delivery (CI/CD)
CI/CD means using automated workflows to continuously integrate changes (build, validate, test) and continuously deliver or deploy approved changes.

For EIC, CI/CD is needed to:
- detect issues earlier through automated checks,
- enforce consistent quality and policy gates before merge and deployment,
- reduce manual and error-prone release steps,
- accelerate reliable delivery of controls software and configuration updates,
- provide repeatable evidence of validation and delivery outcomes.

### Release Management
Release management is the process of creating, approving, publishing, and tracking production-ready versions of software and configuration changes.

For EIC, GitHub-based release management should use the following pattern:
- create a version tag from an approved baseline commit,
- generate a GitHub Release linked to that tag with release notes,
- attach validated build artifacts and relevant deployment metadata,
- record links to workflow runs, checks, and evidence used for release approval,
- use release status and notes to communicate what changed and what is deployed.

This approach ensures each release is traceable to a specific Git revision and validation history, which improves auditability, rollback readiness, and operational confidence.

### Scope and Expected Impact
Scope:
- Controls application source code.
- Infrastructure and configuration resources used by EIC systems.
- CI/CD workflows that validate, test, and deploy those resources.
- Release workflows and release records for versioned delivery.

Expected impact:
- Higher consistency in engineering practices across teams.
- Faster and more reliable collaboration across internal and external contributors.
- Stronger baseline security posture for software delivery and operations.

### References and Evidence
Platform and governance:
- GitHub Docs. Understanding GitHub Actions. https://docs.github.com/en/actions/get-started/understand-github-actions
- GitHub Docs. Reuse workflows. https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows
- GitHub Docs. About protected branches. https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
- GitHub Docs. About code owners. https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
- GitHub Docs. About organizations. https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/about-organizations
- GitHub Docs. About Projects. https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects
- GitHub Docs. About releases. https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases

Security and supply chain:
- GitHub Docs. OpenID Connect. https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect
- GitHub Docs. Secure use reference. https://docs.github.com/en/actions/reference/security/secure-use
- GitHub Docs. Artifact attestations for build provenance. https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations
- NIST. SP 800-218 Secure Software Development Framework (SSDF). https://csrc.nist.gov/pubs/sp/800/218/final
- SLSA. Supply-chain Levels for Software Artifacts. https://slsa.dev/
- OpenSSF Scorecard. https://securityscorecards.dev/

IaC alignment and operations:
- Terraform Registry. GitHub Provider (integrations/github). https://registry.terraform.io/providers/integrations/github/latest/docs
- GitHub Docs. GitHub's plans. https://docs.github.com/en/get-started/learning-about-github/githubs-plans

Contextual reference:
- DORA Research Program. https://dora.dev/research/

## Alternatives

| Alternative | Summary | Reason Not Selected |
|-------------|---------|---------------------|
| **Self-hosted GitLab (on-premises)** | Run GitLab on local infrastructure for source control, CI/CD, and release workflows, including hosting GitLab Runner instances for CI/CD execution. | Technically viable, but transfers full platform operations responsibility to EIC: infrastructure provisioning, upgrades, backups, runner fleet management, monitoring, incident response, and security patching. Maintaining a production-grade GitLab instance with CI/CD runners is estimated at 0.33–0.5 FTE of dedicated platform operations effort on an ongoing basis, representing a sustained staffing cost not required under a managed hosted model. |
| **Self-hosted GitHub Enterprise Server (on-premises)** | Run GitHub Enterprise Server locally to keep GitHub workflows while hosting internally. | Preserves GitHub semantics but still requires local platform operations and capacity planning; added infrastructure and service ownership cost is not preferred for current EIC delivery timelines. |
| **Mixed platform model (multiple SCM/CI tools by team)** | Allow teams to choose different hosting and CI/CD platforms. | Creates inconsistent governance, fragmented automation patterns, and weaker traceability across controls repositories, increasing integration and support complexity. |
