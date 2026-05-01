# Swagger Petstore - OpenAPI 3.0

> One repo, one service, one Postman workspace.

This repo manages the **Swagger Petstore - OpenAPI 3.0** API lifecycle using the
[`postman-cs` GitHub Action suite](https://github.com/postman-cs/postman-api-onboarding-action).

## Quick Start

### 1. Configure secrets

| Secret | How to get it |
|--------|---------------|
| `POSTMAN_API_KEY` | Postman > Settings > API Keys > Generate |
| `POSTMAN_ACCESS_TOKEN` | `postman login` then extract from `~/.postman/postmanrc` |
| `GH_FALLBACK_TOKEN` | GitHub PAT with `actions:write` + `contents:write` |

### 2. Push to main

Any change to `specs/` or `api-manifest.json` triggers the onboarding pipeline:

```bash
git push origin main
```

### 3. What happens automatically

1. **Governance** (on PR) -- Spectral lint, manifest validation, spec structure check
2. **Onboard** (on merge) -- uploads spec to Spec Hub, generates collections, creates workspace
3. **CI Tests** (auto-generated) -- smoke + contract tests via Postman CLI
4. **Promote** (after tests pass) -- adds workspace to the Private API Network

## Spec

- [`specs/petstore-api-1.0.27.yaml`](specs/petstore-api-1.0.27.yaml)

## Workflows

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `onboard-apis.yml` | Push to main | Onboard to Postman v12 API Catalog |
| `api-governance.yml` | Pull request | Spectral lint + manifest validation |
| `promote-to-private-network.yml` | After onboard/CI succeeds | Promote to Private API Network |
| `postman-ci-*.yml` | Auto-generated | Smoke + contract tests |
