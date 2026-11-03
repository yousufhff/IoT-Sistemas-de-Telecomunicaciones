# Message contract

The agreement between components. Change it only through a PR and bump the version.

## Transport
Protocol, broker, QoS per message type, topic naming (e.g. `wildfire/v1/<side>/<id>/<kind>`).

## Minimum fields (every message)
| Field | Meaning | Used for |
|---|---|---|
| `v` | contract version | evolve the format without breaking others |
| `id` | node or edge identifier | origin of data and alarms |
| `ts` | time of the measurement | ordering, detection delay |
| `tx` | send time | end-to-end latency (needs synchronised clocks) |
| `seq` | per-sender counter | packet-loss detection |
| `kind` | periodic / event / emergency | routing and decisions |
| measurements | variables of `docs/01-requirements.md` | detection |

## Message types
| Type | Direction | Trigger | QoS | Example payload | Size |
|---|---|---|---|---|---|
| | | | | | |

## Versioning rules
- Adding an optional field: compatible.
- Removing/renaming a field or changing a unit: new version.

## Format decision
JSON vs compact binary: see `docs/decisions/`.
