# ADR-0002: Message format

- Status: proposed
- Date: 2026-11-03

## Context
We do not simulate LoRa for now, so payload size does not limit the link. We still want a format that is easy to debug and to version.

## Options considered
| Option | Pros | Cons |
|---|---|---|
| JSON | Readable, flexible, easy to debug | More bytes |
| Compact binary | Smallest | Hard to read and evolve |

## Decision
_(proposal: JSON everywhere; state that a real LoRa link would need a compact binary format)_

## Consequences
Overhead measured in E6.
