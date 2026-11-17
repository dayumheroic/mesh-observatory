# Extraction validation

Date: 2026-11-17. Source: commit 4f412518d3bbf478b76aa4c2661d4a19db423dde of the research branch documented in PROVENANCE.md.

## Checks completed

- Python unittest discovery for tools/deco_bridge: passed.
- Node tests for the mesh client and cloud contracts/associations/floorplan/RF/sensing modules: 36 passed, zero failed.
- Synthetic collector replay: passed; output retains synthetic state and unavailable CSI/human-presence/pose capabilities.
- npm ci --ignore-scripts: completed using the extracted lockfile.
- Cloud UI and Worker bundle: built successfully.
- Wrangler type generation and TypeScript check: passed after adding explicit declarations for private secret binding names. No secret values were introduced.

The type declarations and tsconfig inclusion fix a clean-checkout issue: generated types know the Durable Object binding but cannot infer undeclared deployment secrets. This changes type information only, not runtime authority.

Wrangler logging was redirected into the checkout because the environment does not permit writing its default user-preferences log directory.

## Scope

These checks exercise synthetic inputs and local test services. They do not connect to the mesh, invoke live Mac radio collection, install a LaunchAgent, deploy a Worker, establish sensor accuracy or certify security. Historical hardware results are summarized separately in the root README.

Targeted source review and pattern scans found no private capture files, literal live credentials or actual deployed endpoint in the selected export. This is not a guarantee that every possible vulnerability or sensitive string has been detected.
