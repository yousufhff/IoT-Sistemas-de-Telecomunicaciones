# ADR-0001: Messaging protocol between components

- Status: proposed
- Date: 2026-11-03
- Deciders: team (to confirm)

## Context
Components publish periodic readings, events and alarms. The edge must keep working without cloud connectivity, and we must measure protocol overhead (guideline step 4).

## Options considered
| Option | Pros | Cons |
|---|---|---|
| MQTT (Mosquitto) | Lightweight, publish/subscribe decouples components, QoS levels, standard in IoT | Needs a broker |
| CoAP | Very light, UDP, request/response, good for constrained devices | Less tooling, no native pub/sub |
| HTTP | Universal | Heavier, request/response only |

## Decision
_(to be agreed)_

## Consequences
_(overhead measured in E6; QoS per message type in `docs/04-message-contract.md`)_
