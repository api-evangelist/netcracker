# gRPC / Protobuf — Netcracker

`netcracker-qubership-control-plane-bus.proto` was saved **verbatim** from
<https://github.com/Netcracker/qubership-core-control-plane/blob/main/control-plane/event/bus/bus.proto>
(HTTP 200, fetched 2026-07-25).

It is the only first-party service-bearing `.proto` published in the Netcracker GitHub
organization: the `EventBus` service used by the Qubership Core control plane to stream
configuration change events between control-plane replicas (`Subscribe(Topic) returns
(stream Event)`, `GetLastSnapshot(Empty) returns (Event)`).

Scope caveats, recorded honestly:

- It belongs to the **internal event bus** of a self-hosted platform component, not to any of
  the four APIs catalogued in `apis.yml`, and there is no public gRPC endpoint to call.
- gRPC is advertised as a *supported format* on the Netcracker API Management and Integration
  product page; no gRPC contract for any commercial Netcracker product is published.
- The remaining `.proto` files in the org (`qubership-testing-platform-*`) are Kafka message
  schemas, not services.
