---
name: netcracker-review-api-changes
description: Find and classify what changed between two versions of an API in Qubership APIHUB — breaking vs safe — and export the result for a release review.
api: openapi/netcracker-qubership-apihub-registry-openapi.yml
generated: '2026-07-25'
method: generated
operations:
  - postCompare
  - getPackageIdVersionChangesSummary
  - getPackagesIdVersionsIdApiTypeChangesV4
  - getPackagesIdVersionsApiTypeOperationsIdChanges
  - getPackagesIdVersionsApiTypeOperationsIdChangesSummary
  - getPackageIdVersionIdChangesExportV3
  - getPackageIdVersionDeprecatedSummaryV3
  - getPackagesIdVersionsIdApiTypeDeprecations
---

# Review API changes between two versions

Change classification is APIHUB's core job: it tells you whether a version is **backward
compatible**, not just what text moved.

## Steps

1. **Kick off the comparison.** `postCompare` starts the asynchronous changelog calculation
   between two package versions. Like every long job in APIHUB it returns a handle you poll —
   do not assume the changelog is ready on return.
2. **Read the summary.** `getPackageIdVersionChangesSummary` gives the version-level roll-up
   (counts by severity). This is the number you put in a release note.
3. **List changed operations.** `getPackagesIdVersionsIdApiTypeChangesV4` returns changed
   operations for one `apiType` (`rest`, `graphql`, `asyncapi`). Page with `page`/`limit`.
4. **Drill into one operation.** `getPackagesIdVersionsApiTypeOperationsIdChanges` is the
   single-operation changelog; `…ChangesSummary` is its severity roll-up.
5. **Check deprecations separately.** `getPackageIdVersionDeprecatedSummaryV3` and
   `getPackagesIdVersionsIdApiTypeDeprecations` are how APIHUB communicates deprecation —
   there is no `Sunset` or `Deprecation` HTTP header anywhere in the platform
   (`lifecycle/netcracker-lifecycle.yml`).
6. **Export for humans.** `getPackageIdVersionIdChangesExportV3` produces the xlsx used in
   release/architecture review.

## Local alternative (no instance required)

If the two specs are files on your machine, use the first-party CLI/MCP tool instead —
same classification engine, no APIHUB deployment needed:

```bash
apihub-api-diff previous.yaml current.yaml --format md --fail-on breaking
```

`--fail-on breaking` exits 2, which makes it a CI gate. The same binary runs as a local MCP
server (`apihub-api-diff mcp`) exposing one tool, `apihub_api_diff`
(`previousPath`, `currentPath`, `format`, `includeValues`, `title`) — see
`mcp/netcracker-mcp.yml` and `cli/netcracker-cli.yml`.

## Interpreting results

- Severity/action/scope come from the APIHUB api-processor, the same engine the Portal and the
  quality gates use; `md` output is the format the vendor recommends for LLM summarisation,
  `json` when you need counts or to chain further logic.
- A version cannot be moved back to `draft` if a released version names it as its
  `previousVersion` (`400`, code `8600`).
