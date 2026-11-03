# Course guidelines → where it lives in this repository

Source: *Project Guidelines: IoT and V2X System Design* (B. Soret, Sept. 2026), Track A. Update the **Status** column every week.

## Deliverables
| Requirement | Where | Status |
|---|---|---|
| Written report, 8-12 pages, technical design document: architecture + reasoning, implementation only where it supports a claim, every metric tied to a decision | `report/` (create at week 12) | pending |
| Individual-contribution statement | `CONTRIBUTIONS.md` | pending |
| Code repository with README reproducible by an outsider | `README.md`, `docker-compose.yml` | in progress |
| Dependency file | `requirements.txt` | proposed |
| Clear commit history reflecting real contributions | PR workflow in `CONTRIBUTING.md` | in progress |
| Live demo and individual oral questioning | all members must explain any part | pending |

## The six components (each must be defined and identifiable)
| Component | Guideline text (short) | Folder | Status |
|---|---|---|---|
| Data source | generate or replay sensor readings at a realistic rate | `src/datasource/` | pending |
| Communication layer | lightweight IoT protocol; **measure its overhead** and discuss | `infra/`, `experiments/` | pending |
| Edge layer | receive, filter, route; **keeps working with no cloud connectivity** | `src/edge/` | pending |
| Edge AI | lightweight on-device inference within a bounded latency budget | `src/edge_ai/`, `ml/` | pending |
| Cloud layer | stores history, dashboard | `src/cloud/`, `infra/grafana/` | pending |
| Cloud AI | **periodic retraining** and **push updated weights back to the edge** | `src/cloud_ai/` | pending |

## Required justifications
| Justification | Where |
|---|---|
| Edge vs cloud split in terms of **latency, bandwidth, privacy and energy** | `docs/05-edge-cloud-split.md` |
| Protocol choice, message format | `docs/decisions/`, `docs/04-message-contract.md` |
| ML evaluated under realistic constraints (latency, connectivity, compute budget) | `experiments/` |
| Quantitative results related to theoretical models | `experiments/`, report |

## Design steps from the guidelines
| # | Step | Status |
|---|---|---|
| 1 | Requirements analysis | in progress (`docs/01-requirements.md`) |
| 2 | Provision environment, Git, README, docker-compose | in progress |
| 3 | Data generation / replay, validate message format | pending |
| 4 | Communication layer; capture traffic (Wireshark / MQTT Explorer) to measure overhead, latency, bandwidth | pending |
| 5 | Edge layer | pending |
| 6 | Edge AI: train offline, export, run with the edge disconnected from the cloud | pending |
| 7 | Cloud layer: storage + dashboard | pending |
| 8 | Cloud AI: retraining job + push weights to the edge | pending |
| 9 | Integration and explicit edge/cloud split | pending |
| 10 | Evaluation and documentation | pending |

## Timeline in the guidelines
Week 1 groups and topic · Week 3 timeline + requirements started · Weeks 4-13 design, implementation, validation · Week 14 report and repo clean-up, rehearse demo · Week 15 oral exam.
**Check the real calendar dates with the instructor** and write them in `docs/planning.md`.
