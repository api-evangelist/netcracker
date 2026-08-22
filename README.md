# Netcracker (netcracker)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Netcracker Technology is a Waltham, Massachusetts-based BSS/OSS and digital business software vendor and a wholly owned subsidiary of NEC Corporation. It sells cloud BSS, digital commerce and monetization, convergent charging, service and network orchestration, and API management and integration software to communications service providers worldwide — it is a supplier to carriers rather than a carrier itself, sitting one layer behind the operator in the telecom value chain.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/netcracker/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/netcracker/refs/heads/main/apis.yml)

## The honest API posture

Netcracker publishes **no developer portal**. `developer.netcracker.com`, `developers.netcracker.com`, `docs.netcracker.com`, `api.netcracker.com`, `opengateway.netcracker.com` and `portal.netcracker.com` do not resolve. `/developer`, `/developers`, `/api`, `/openapi.json`, `/swagger.json`, `/api-docs` and `/graphql` on `www.netcracker.com` all return 404. The only API-related page on the corporate site is a product marketing page selling an API management platform to carriers — a company that sells an API exposure platform while exposing none of its own.

Its commercial telecom APIs — the TM Forum Open APIs its BSS/OSS products implement — reach integrators only through a customer or partner engagement.

The one genuinely public, self-serve surface is **Qubership**, Netcracker's open-source cloud platform at [github.com/Netcracker](https://github.com/Netcracker) (verified org, 287 public repositories) and [netcracker.github.io](https://netcracker.github.io/). Four real OpenAPI/Swagger definitions were harvested verbatim from it. They describe platform-engineering components — an API registry, messaging, DBaaS — not telecom network or BSS APIs.

## CAMARA posture

**Named in marketing, implemented nowhere.** The API Management product page lists CAMARA among the standards Netcracker aligns with, and says CSPs can monetize "plug and play developer APIs, such as those from CAMARA." No CAMARA API is specified, implemented or callable anywhere in Netcracker's public surface. The string "camara" appears zero times in the site sitemap, no CAMARA API name appears anywhere, and a GitHub search for "netcracker" across `org:camaraproject` returns zero results. A press release is not an implementation, and here there is not even a press release.

**GSMA Open Gateway:** no evidence of participation. Netcracker is a vendor, not an operator. **Aduna:** no mention found.

## TM Forum

Netcracker holds real, published TM Forum credentials — and discloses none of the specs behind them:

- **TM Forum Platinum Badge for Open API** and **ODA Compliance at "Ready for ODA" Level 6** (product page)
- **Ready for ODA status for its BSS/OSS portfolio** (2023-12-13) — "one of the first vendors to be certified as Ready for ODA by TM Forum"
- **2019 TM Forum Excellence Award for Open API adoption** — for "adopting the broadest range of TM Forum Open APIs" and "contributing multiple conformance toolkits to the Open API program"

No TMF API numbers, conformance certificates or specifications are published where a developer could read them.

## Tags

- Telecommunications
- United States
- BSS
- OSS
- Network Vendor
- API Management
- TM Forum
- Open API
- CAMARA
- Standards
- Orchestration
- Monetization
- Open Source

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### Qubership APIHUB Registry API

The external, public-facing API contract for APIHUB — Netcracker's open-source API registry and developer portal product. OpenAPI 3.0.3, version 2026.1, 111 documented paths.

- **Human URL:** [https://netcracker.github.io/apihub/](https://netcracker.github.io/apihub/)
- **Base URL:** `https://{apihub}.qubership.org` (self-hosted template — `qubership.org` does not resolve publicly)

#### Properties

- [OpenAPI](openapi/netcracker-qubership-apihub-registry-openapi.yml)
- [Documentation](https://netcracker.github.io/apihub/)
- [API Reference](https://github.com/Netcracker/qubership-apihub-backend/blob/develop/docs/api/APIHUB_API.yaml)
- [Source Code](https://github.com/Netcracker/qubership-apihub-backend)

### Qubership APIHUB System Administrators API

The external administration API contract for APIHUB — package transitions, system operations, role and administrator management. OpenAPI 3.0.3, version 2026.1, 18 documented paths.

- **Human URL:** [https://netcracker.github.io/apihub/](https://netcracker.github.io/apihub/)

#### Properties

- [OpenAPI](openapi/netcracker-qubership-apihub-admin-openapi.yml)
- [Documentation](https://netcracker.github.io/apihub/)
- [API Reference](https://github.com/Netcracker/qubership-apihub-backend/blob/develop/docs/api/Admin%20API.yaml)
- [Source Code](https://github.com/Netcracker/qubership-apihub-backend)

### Qubership MaaS (Messaging as a Service) API

REST API for Qubership MaaS, which provisions and manages Kafka topics and RabbitMQ virtual hosts for microservices on the Qubership platform. Swagger 2.0, 35 documented paths, HTTP Basic auth.

- **Human URL:** [https://github.com/Netcracker/qubership-maas](https://github.com/Netcracker/qubership-maas)

#### Properties

- [OpenAPI](openapi/netcracker-qubership-maas-swagger.yml)
- [Documentation](https://github.com/Netcracker/qubership-maas)
- [API Reference](https://github.com/Netcracker/qubership-maas/blob/main/maas/maas-service/docs/swagger.yaml)

### Qubership DBaaS Aggregator API

REST API for Qubership DBaaS, an aggregator that routes managed-database requests to the right adapter and tracks every database in a cloud project. OpenAPI 3.1.0, version 6.13.2, 73 documented paths, Bearer JWT auth.

- **Human URL:** [https://github.com/Netcracker/qubership-dbaas](https://github.com/Netcracker/qubership-dbaas)

#### Properties

- [OpenAPI](openapi/netcracker-qubership-dbaas-openapi.json)
- [Documentation](https://github.com/Netcracker/qubership-dbaas)
- [API Reference](https://github.com/Netcracker/qubership-dbaas/blob/main/docs/OpenAPI.json)

## Common Properties

- [Website](https://www.netcracker.com/)
- [Documentation](https://netcracker.github.io/)
- [GitHub Organization](https://github.com/Netcracker)
- [LinkedIn](https://www.linkedin.com/company/netcracker-technology)
- [Blog](https://www.netcracker.com/blog)
- [Press Releases](https://www.netcracker.com/news/press-releases)
- [Product Page](https://www.netcracker.com/portfolio/products/netcracker-api-management-integration)
- [Portfolio](https://www.netcracker.com/portfolio)

## Maintainers

- Kin Lane — kin@apievangelist.com
