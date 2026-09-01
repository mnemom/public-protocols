# mnemom/public-protocols

Consolidated monorepo for Mnemom's public, npm/PyPI-published agent-trust protocol
packages. Created by **MNE-6778** by merging three previously separate repositories
into one, **with full git history preserved** (`git subtree`). Package names and
release configuration are unchanged — consumers are unaffected; only the git path moved.

## Packages

| Directory | Published package(s) | Language | Source repo (pre-consolidation) |
|-----------|----------------------|----------|----------------------------------|
| [`aip/`](./aip) | npm [`@mnemom/agent-integrity-protocol`](https://www.npmjs.com/package/@mnemom/agent-integrity-protocol) · PyPI `agent-integrity-proto` | TypeScript + Python | `mnemom/aip` |
| [`aap/`](./aap) | npm [`@mnemom/agent-alignment-protocol`](https://www.npmjs.com/package/@mnemom/agent-alignment-protocol) · PyPI `agent-alignment-protocol` | TypeScript + Python | `mnemom/aap` |
| [`aip-otel-exporter/`](./aip-otel-exporter) | npm [`@mnemom/aip-otel-exporter`](https://www.npmjs.com/package/@mnemom/aip-otel-exporter) · PyPI `aip-otel-exporter` | TypeScript + Python | `mnemom/aip-otel-exporter` |

Each sub-project remains **self-contained**: it keeps its own `package.json` /
`pyproject.toml`, lockfiles, and build tooling, and builds independently from its own
directory (no root workspace is required).

## Building

```bash
# TypeScript packages (self-contained, npm)
cd aip/packages/typescript   && npm ci && npm run build
cd aap/typescript            && npm ci && npm run build
cd aip-otel-exporter         && npm ci && npm run build   # npm workspace

# Python packages
cd aip/packages/python                  && python -m build
cd aap                                  && python -m build
cd aip-otel-exporter/packages/python    && python -m build
```

## Releases

Release automation is consolidated at the repo root:

- `release-please-config.json` + `.release-please-manifest.json` — one manifest-mode
  config covering all release-please-managed packages under their new paths. TypeScript
  packages now carry a **component in their release tag** (e.g.
  `agent-integrity-protocol-v1.3.0`) so the two npm packages no longer collide on a bare
  `v<version>` tag in the shared repo.
- `.github/workflows/` — security rail (CodeQL, OpenSSF Scorecard, Dependabot
  auto-merge), per-package CI, per-package publish, and the consolidated release-please
  workflow.

Publishing to npm/PyPI is **human-gated** and not yet enabled on this repo — see the
consolidation PR for the exact remaining steps (Trusted Publisher reconfiguration for the
new repo path, org release-App install, branch protection).
