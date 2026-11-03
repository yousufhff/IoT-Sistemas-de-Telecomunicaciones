# Architecture

```mermaid
flowchart LR
  subgraph Laptop A
    DS[Data source] --> BR[(MQTT broker)]
    BR --> ED[Edge service]
    ED --> EAI[Edge AI model]
  end
  subgraph Laptop B
    CL[Cloud ingest] --> DB[(Time-series DB)]
    DB --> DASH[Dashboard]
    DB --> CAI[Cloud AI retraining]
  end
  ED -- alarms + summaries --> CL
  CAI -. model update .-> ED
```
_(Adjust to the real deployment: which component runs on which machine, ports, network.)_

## Components
For each of the six components: responsibility, inputs/outputs, technology, resource limits, owner. Link to its `src/<component>/README.md`.

## Deployment
Machines, containers, resource limits, ports, network assumptions.

## Failure behaviour
What happens if the cloud is unreachable, the broker restarts, or a node goes silent.
