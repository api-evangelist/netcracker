---
name: netcracker-publish-api-version
description: Publish a new version of an API package to a Qubership APIHUB instance and confirm it landed, using the APIHUB Registry API.
api: openapi/netcracker-qubership-apihub-registry-openapi.yml
generated: '2026-07-25'
method: generated
operations:
  - getPackages
  - getPackagesId
  - postPackages
  - postPackagesIdPublish
  - getPackagesIdPublishIdStatus
  - getPackagesIdVersionsV3
  - getPackagesIdVersionsIdV4
  - patchPackagesIdVersionsIdV2
  - getVersionProblems
---

# Publish an API version to APIHUB

APIHUB is **self-hosted**. Every call goes to the operator's own instance
(`https://{apihub-host}`), never to a Netcracker-run domain.

## Authenticate

Pick one scheme from `authentication/netcracker-authentication.yml`:

- automation / CI → `api-key: <package API key>` header, or `X-Personal-Access-Token: <PAT>`
- browser session → the `apihub-access-token` cookie
- bearer JWT is also accepted (`Authorization: Bearer …`)

A `401` with `code: APIHUB-4101` (`Authentication required`) means the credential is missing or
expired. A privileges error means the credential is valid but not entitled to that package —
**stop, do not retry, do not try a different package to work around it.**

## Steps

1. **Find or create the package.** `getPackages` lists packages (`page` from 0, `limit` max
   100, `textFilter` for a name search); `getPackagesId` fetches one by `packageId`. If it does
   not exist, `postPackages` creates it — a package needs `parentId` (its group/workspace),
   `kind`, `name` and `alias`.
2. **Check the version does not already exist.** `getPackagesIdVersionsV3` lists versions;
   note that version strings are package-specific (`2026.2`, `1.4.0`, `v1` are all valid).
3. **Publish.** `postPackagesIdPublish` uploads the sources and starts an asynchronous build.
   It returns a `publishId` — the response is an accepted job, not a finished publication.
4. **Poll.** `getPackagesIdPublishIdStatus` with that `publishId` until the build completes.
   This is the standard APIHUB async shape (see `conventions/netcracker-conventions.yml`);
   there are no webhooks to wait on.
5. **Verify.** `getPackagesIdVersionsIdV4` returns the published version content;
   `getVersionProblems` reports what the build flagged.
6. **Promote when ready.** `patchPackagesIdVersionsIdV2` moves a version from `draft` to
   `release`.

## Rules that will bite you

- **Release/draft chain.** Publishing a `release` version whose `previousVersion` is still a
  `draft` fails with `400` code `8600`; the message names the offending version and package in
  `params`. Promote the previous version first, or publish this one as a draft.
- **No general idempotency key.** Only the AI-chat send accepts `clientMessageId`. Re-posting a
  publish creates new work — poll the `publishId` you already have instead of re-submitting.
- **Deletes are reference-checked.** Deleting a version or package that a dashboard references
  fails with `409` code `8500`; the message lists the referencing dashboard versions.
- Full error contract: `errors/netcracker-problem-types.yml`.
