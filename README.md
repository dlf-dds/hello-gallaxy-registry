# hello-gallaxy

A collection of nine example repositories demonstrating different IaC tools, runtime architectures, and application patterns -- all integrated with the [ironskillet](https://github.com/dlf-dds/ironskillet-infra) compliance system.

Each repo is a self-contained, deployable service that follows ironskillet's tagging and registration conventions. Together they cover Terraform, CloudFormation, Pulumi, Ansible, serverless, containers, and edge-portable patterns.

## Repos

| Repo | IaC | Runtime | Description |
| ---- | --- | ------- | ----------- |
| [spin-min](https://github.com/dlf-dds/spin-min) | Terraform | EC2 + Flask + wasmtime | Mandelbrot fractal explorer (Wasm compute) |
| [spin-full](https://github.com/dlf-dds/spin-full) | Terraform | EC2 + Flask + wasmtime | Wasm benchmark lab (4 kernels) |
| [juno](https://github.com/dlf-dds/juno) | Terraform | EC2 + Flask + SQLite + wasmtime | Notebook with Wasm text processing |
| [magic-8ball](https://github.com/dlf-dds/magic-8ball) | Terraform | API Gateway + Lambda | Magic 8-Ball oracle API |
| [dad-jokes](https://github.com/dlf-dds/dad-jokes) | CloudFormation | API Gateway + Lambda | Daily dad joke service |
| [color-palette](https://github.com/dlf-dds/color-palette) | Pulumi | API Gateway + Lambda | Random color palette generator |
| [mesh-dash](https://github.com/dlf-dds/mesh-dash) | Terraform + Ansible | EC2 + Node.js + React + PgSQL | Network mesh monitoring dashboard |
| [field-report](https://github.com/dlf-dds/field-report) | Terraform + Ansible | EC2 + FastAPI + PgSQL | Field incident reporting API |
| [asset-ledger](https://github.com/dlf-dds/asset-ledger) | Terraform + Ansible | EC2 + .NET 8 + Vue.js + PgSQL | Asset tracking with audit log |

## Architecture Groups

### Edge-Native Wasm (spin-min, spin-full, juno)

ARM64 EC2 instances running Flask + wasmtime. Hand-written WAT modules handle compute workloads. Can run fully disconnected on a Raspberry Pi.

### Serverless APIs (magic-8ball, dad-jokes, color-palette)

API Gateway + Lambda + DynamoDB. Three different IaC tools (Terraform, CloudFormation, Pulumi) deploying the same serverless pattern.

### Edge-Portable Services (mesh-dash, field-report, asset-ledger)

Terraform creates AWS infrastructure; Ansible configures the host. The same playbook deploys to EC2 or bare-metal ARM64 devices. PostgreSQL 16 on each instance. Three different languages (Node.js, Python, C#).

## Compliance Integration

Every repo integrates with the ironskillet compliance system through:

1. **Tagging** -- 5 required tags on all resources (Project, Environment, ManagedBy, Repository, Lifecycle) via the [compliance-tags](https://github.com/dlf-dds/ironskillet-infra/tree/main/modules/aws/compliance-tags) module
2. **Registration** -- SSM parameter at `/{project}/{environment}/iac-registry/{repo-slug}` via the [iac-registry](https://github.com/dlf-dds/ironskillet-infra/tree/main/modules/aws/iac-registry) module

The compliance scanner automatically discovers registered repos, reads their IaC state, and verifies all resources are tagged and managed.

## Using a Repo as a Template

1. Fork any repo as a starting point
2. Update `backend.tf` (or equivalent) with a new state key
3. Set `service_name` and `repository_url` to your values
4. Replace the application code

See the [Multi-Repo Compliance Guide](https://github.com/dlf-dds/ironskillet-infra/blob/main/docs/guides/MULTI-REPO-COMPLIANCE.md) for detailed onboarding instructions.

## Future

This registry will eventually become an automated live index that discovers hello-gallaxy repos dynamically. For now it's a manually maintained reference.

---

*Note: These repos are planned to be renamed with a `hello-gallaxy-` prefix (e.g., `hello-gallaxy-spin-min`) to make the collection more discoverable. Links above use current names and will auto-redirect after the rename.*
