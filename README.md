# Numou Tenancy

Tenant lifecycle, tenant membership, tenant settings, provisioning and tenant-context capability.

## Repository status

**Status:** Source transferred; independent build verification pending shared Maven package availability.

The first source transfer is staged from `andalus-ai/numu/tenancy` into this repository. It contains the source files under that root, including domain, SPI, application, in-memory adapter and domain tests. The root POM and capability BOM are repository-local Maven aggregators.

- Source repository: https://github.com/andalus-ai/numu
- Source root: `tenancy/`
- Source commit: `25dd5a99ff95b6d32ab59c864731528819da027f`
- Destination reactor: root `pom.xml`
- Capability BOM: `numou-tenancy-bom`

This is a staged extraction, not yet an independently verified release. The source monorepo remains authoritative until the acceptance criteria below pass.

## Maven dependency model

This repository uses:

- Parent: `tech.kayys.numou:numou-parent:0.1.0-SNAPSHOT`
- Platform BOM: `tech.kayys.numou:numou-bom:0.1.0-SNAPSHOT`
- Repository-local BOM: `tech.kayys.numou:numou-tenancy-bom:0.1.0-SNAPSHOT`
- Package source: GitHub Packages at `https://maven.pkg.github.com/andalus-ai/numu`
- Java: 21

The parent and platform BOM are maintained in the source monorepo under `core/framework/parent` and `core/framework/bom`. The monorepo contains a manual publication workflow:

[Publish Shared Maven Parent and Platform Artifacts](https://github.com/andalus-ai/numu/blob/main/.github/workflows/publish-shared-foundation.yml)

The workflow must be run successfully against the intended source revision before this repository's build can be considered independently reproducible. The documentation PR that introduced the capability matrix is not the publication PR and does not publish Maven artifacts.

## Build prerequisites

1. Run the manual **Publish Shared Maven Parent and Platform Artifacts** workflow in `andalus-ai/numu`.
2. Verify that `numou-parent`, `numou-bom`, and the Foundation artifacts referenced by this reactor are available at the declared version.
3. Ensure this repository has read access to the source repository's GitHub Packages artifacts. For private packages, configure a token with package read permission.
4. Ensure Maven credentials are supplied through environment variables; never commit credentials.

The repository-local `.mvn/settings.xml` reads credentials from environment variables. No credentials belong in source control.

Run:

```bash
mvn -B -ntp verify
```

The CI workflow is intentionally manual-only until shared artifacts are published and package access is verified. After a clean build succeeds, enable pull-request and push triggers in a separate reviewed change.

## Ownership

Tenancy owns:

- tenant lifecycle and hierarchy;
- tenant membership and invitations;
- tenant settings, locale and timezone;
- tenant provisioning workflow and provisioner ports;
- tenant-context contracts and tenant lifecycle events.

Identity owns canonical person and organization subjects. Security owns authentication and authorization policy. Tenant membership is not an automatic role grant.

Organization membership and tenant membership are different relationships. A person may belong to an organization without belonging to every tenant associated with that organization, and a tenant membership must not silently grant business permissions.

## Extraction acceptance checklist

- [x] Source root transferred into this repository.
- [x] Repository-local root POM and capability BOM created.
- [x] Source provenance recorded.
- [ ] Shared parent and platform BOM are confirmed published at the expected version.
- [ ] Clean `mvn -B -ntp verify` succeeds using only remote artifacts.
- [ ] CI is enabled for pull requests and pushes after the clean build succeeds.
- [ ] Tenant isolation and membership authorization integration tests pass.
- [ ] Monorepo consumers are migrated to published Tenancy contracts.
- [ ] Source monorepo copy is retired only after consumer migration and rollback verification.

See the source monorepo's `docs/architecture/DOMAIN-CAPABILITY-MATRIX.md` for the normative ecosystem ownership contract.
