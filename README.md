# Numou Tenancy

Tenant lifecycle, tenant membership, tenant settings, provisioning and tenant-context capability.

## Repository status

**Status:** Source transferred — build pending shared artifacts

The first source transfer is staged from `andalus-ai/numu/tenancy` into this repository. The transfer contains all 75 source files under that root, including domain, SPI, application, adapter and domain tests. The monorepo root POM and legacy BOM were replaced with repository-local Maven aggregators.

- Source repository: https://github.com/andalus-ai/numu
- Source root: `tenancy/`
- Source commit: `25dd5a99ff95b6d32ab59c864731528819da027f`
- Destination reactor: root `pom.xml`
- Capability BOM: `numou-tenancy-bom`

## Build prerequisites

This repository consumes the shared Maven parent and platform BOM from GitHub Packages in `andalus-ai/numu`. The shared parent/Foundation publication PR is tracked in [numu PR #1988](https://github.com/andalus-ai/numu/pull/1988).

Before running the build:

1. Merge the shared-parent/platform-artifact PR.
2. Run the manual **Publish Shared Maven Parent and Platform Artifacts** workflow in `andalus-ai/numu`.
3. Ensure the shared packages are public or grant this repository package read access.
4. Provide `GITHUB_ACTOR` and `GITHUB_TOKEN` for private package access.

The repository-local `.mvn/settings.xml` reads credentials from environment variables; no credentials are committed.

Run:

```bash
mvn -B -ntp verify
```

The CI workflow is manual-only until shared artifacts are published and package access is configured. It must then be enabled for pull requests and pushes.

## Ownership

Tenancy owns tenant lifecycle, tenant membership, tenant settings, tenant provisioning and tenant-context contracts. Identity owns canonical person/organization subjects; Security owns authentication and authorization policy. Tenant membership is not an automatic role grant.

See the source monorepo's `docs/architecture/DOMAIN-CAPABILITY-MATRIX.md` for the normative ecosystem boundary.
