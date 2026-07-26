---
name: netcracker-discover-api-operations
description: Find the right API operation across an organization's catalog in Qubership APIHUB — over MCP when the agent is wired to an instance, or over REST — and fetch its specification.
api: openapi/netcracker-qubership-apihub-registry-openapi.yml
generated: '2026-07-25'
method: generated
operations:
  - postSearchV4
  - getPackages
  - getPackagesIdVersionsV3
  - getPackagesIdVersionsIdApiTypeOperations
  - getPackagesIdVersionsIdApiTypeOperationsId
  - getPackagesIdVersionsIdDocuments
  - getPackagesIdVersionsIdDocumentsSlugV2
  - getPackagesIdVersionsIdFilesSlugRaw
  - getPackagesIdVersionsIdApiTypeTags
---

# Discover API operations in an APIHUB catalog

## Two front doors, one index

| Surface | Use it when |
|---|---|
| MCP (`apihub-mcp`, `https://{apihub-host}/api/v1/mcp/`) | An agent is connected to the instance. Tools: `search_api_operations`, `get_api_operation_specification`, `get_api_operation_diff`, `get_document`. |
| REST | Scripts, CI, or anything that needs the operations in `mcp/netcracker-tool-crosswalk.yml`. |

The crosswalk is exact: `search_api_operations` → `postSearchV4`,
`get_api_operation_specification` → `getPackagesIdVersionsIdApiTypeOperationsId`,
`get_document` → `getPackagesIdVersionsIdDocumentsSlugV2`, `get_api_operation_diff` →
`getPackagesIdVersionsApiTypeOperationsIdChanges`.

## Search that actually finds things

`postSearchV4` takes a `searchLevel` path parameter — `operations`, `packages`, `documents`,
`ddl`, `mcp`. Search is **lexical full text**, not semantic, not fuzzy, not substring. The
vendor's own agent instructions are worth following verbatim:

- always pass `apiType` (`rest`, `graphql`, `asyncapi`) when searching operations;
- open with `limit: 100`, `page: 0`, then page;
- simplify the query — "create customer" often finds nothing where "customer" finds everything;
- `-word` excludes a term, `"quoted phrase"` forces an exact phrase;
- for REST also try the HTTP method, a distinctive path segment, or the title;
  for AsyncAPI try the channel address, message name or payload field;
  for GraphQL try the operation type and input/output type names;
- group results by `packageId` when you display them.

**Version trap.** When `release` is omitted the search uses the nearest completed calendar
quarter (e.g. `2026.2`), *not* the newest version that exists. Many packages use semver or
never published that quarter. If a query returns nothing, list the package's real versions
(`getPackagesIdVersionsV3`, or the `mcp://api-packages-list` MCP resource) and retry with an
explicit `release`.

## Then fetch

1. `getPackagesIdVersionsIdApiTypeOperations` — browse the operation index of one version;
   `getPackagesIdVersionsIdApiTypeTags` gives the tag facets.
2. `getPackagesIdVersionsIdApiTypeOperationsId` — the operation-level contract (parameters,
   schemas, security). Only pull this once the user has chosen an operation.
3. `getPackagesIdVersionsIdDocumentsSlugV2` / `getPackagesIdVersionsIdFilesSlugRaw` — the full
   source specification, addressed by the `documentId` slug the search returned. Never invent a
   slug.

## Authorization

Results are filtered by the caller's entitlements. A response that begins
`Failed to check user privileges`, or says the user lacks privileges/access, is an
authorization failure: **stop for that package**, report it, and continue only with the
packages the caller can see. That is different from an empty result, which is worth retrying
with different terms or an explicit `release`.
