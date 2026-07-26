---
name: netcracker-provision-messaging
description: Provision and inspect Kafka topics and RabbitMQ virtual hosts for a namespace through the Qubership MaaS API.
api: openapi/netcracker-qubership-maas-swagger.yml
generated: '2026-07-25'
method: generated
operations:
  - GetOrCreateTopicV2
  - GetTopicByClassifierV2
  - SearchTopicsV2
  - DeleteTopic
  - GetOrCreateVHost
  - GetVHostAndConfigByClassifier
  - DeleteVHost
  - ApplyConfigV2
  - GetAllKafkaInstances
  - GetAllRabbitInstances
  - GetTenantsByNamespace
  - GetReport
---

# Provision messaging with Qubership MaaS

MaaS gives a microservice its Kafka topics and RabbitMQ vhosts without the service knowing
which broker it landed on. Everything is **self-hosted**: the base URL is your own MaaS
deployment.

## Authenticate

HTTP **Basic** only — MaaS declares no other scheme
(`authentication/netcracker-authentication.yml`). Accounts are role-scoped and the roles are
visible in the operation summaries themselves: *Agent Role* for day-to-day provisioning,
*Manager Role* for instance registration and account management. Use an agent account for
anything in this skill except the instance-registration operations.

## The classifier is the key

MaaS addresses a topic or vhost by a **classifier** (a namespace + name + tenant tuple), not by
a broker-specific identifier. Get-or-create is the intended entry point — it is safe to call
repeatedly and returns the existing resource if it is already provisioned.

## Kafka

1. `GetOrCreateTopicV2` (`POST /api/v2/kafka/topic`) — provision or return the topic for a
   classifier.
2. `GetTopicByClassifierV2` — look one up without creating it.
3. `SearchTopicsV2` — find topics across a namespace.
4. `DeleteTopic` — remove one (agent role).
5. `GetReport` (`/api/v2/kafka/discrepancy-report/{namespace}`) — reconcile what MaaS believes
   exists against the broker; `SyncTopicToKafka` / `SyncAllTopicsToKafka` repair drift.

Prefer the **v2** operations: `GetOrCreateTopicV1`, `GetTopicByClassifierV1` and `SearchTopicsV1`
are the older `/api/v1` surface kept alongside them.

## RabbitMQ

1. `GetOrCreateVHost` (`POST /api/v1/rabbit/vhost`) — provision or return the vhost.
2. `GetVHostAndConfigByClassifier` — fetch the vhost plus its declared entities.
3. `ValidateRabbitConfigs` — check the declarative configuration before applying it.
4. `RecoverNamespace` (`/api/v2/rabbit/recovery/{namespace}`) — rebuild a namespace's entities.
5. `DeleteVHost` — remove one.

## Declarative configuration

`ApplyConfigV2` (`POST /api/v2/config`) applies a whole namespace's messaging configuration in
one call — the pattern the platform's own deployments use. `GetTenantsByNamespace` and
`SyncTenants` keep multi-tenant topics aligned.

## Notes

- No rate-limit headers, no webhooks, no idempotency-key header — get-or-create *is* the
  idempotent path (`conventions/netcracker-conventions.yml`).
- Client libraries exist and are first-party: Go
  (`go get github.com/netcracker/qubership-core-lib-go-maas-client/v3`) and Java
  (`com.netcracker.cloud.maas.client`, GitHub Packages) — see `packages/netcracker-packages.yml`.
