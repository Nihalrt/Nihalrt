# Project guide

Start with the three projects below for backend, applied AI, and testable service design. Each repository documents its implemented behavior and current limits. These are personal prototypes and learning projects; they are not production deployments or performance guarantees.

## Core projects

### [Switchboard](https://github.com/Nihalrt/switchboard)

**Question:** How can a rollout stay predictable while failures are investigated?

- A Go relay hashes each device/flag pair into a stable bucket and reads rollout percentages from Redis.
- FastAPI manages flags in PostgreSQL and updates the rollout cache.
- Python agents compare completed outcomes and inspect possible cross-flag interactions.
- Tests use SQLite, mocked Gemini responses, and a fake cache for isolated checks.

**Read first:** [hashing](https://github.com/Nihalrt/switchboard/blob/main/relay/internal/routing/hash.go), [request handler](https://github.com/Nihalrt/switchboard/blob/main/relay/cmd/relay/main.go), [Agent 1](https://github.com/Nihalrt/switchboard/blob/main/agents/Agent1.py), [Agent 2](https://github.com/Nihalrt/switchboard/blob/main/agents/Agent2.py).

**Boundary:** Simulated routing outcomes; statistical findings are exploratory. Live ingestion, authentication, and atomic database/cache updates remain future work.

### [Lucent](https://github.com/Nihalrt/agent-notes)

**Question:** How can typed and handwritten notes become useful, retrievable information?

- Expo and React Native share the web/mobile interface.
- Vector strokes are validated and rendered in memory for Gemini transcription.
- FastAPI creates summaries, tasks, tags, and embeddings; PostgreSQL preserves the note and drawing.
- Related-note lookup uses cosine distance against stored embeddings.

**Read first:** [backend processing](https://github.com/Nihalrt/agent-notes/blob/main/backend/api.py), [drawing canvas](https://github.com/Nihalrt/agent-notes/blob/main/frontend/src/components/HandwritingCanvas.js), [API regressions](https://github.com/Nihalrt/agent-notes/blob/main/backend/tests/test_api.py).

**Try it:** [web demo](https://nihalrt.github.io/agent-notes/), using sample notes. Authentication, per-user ownership, and rate limits are not yet implemented; native store releases are separate from the web deployment.

### [Real-time fraud detection](https://github.com/Nihalrt/Realtime-Fraud-Detection-With-MLOps)

**Question:** How can transaction scoring and alert persistence share a consistent model contract?

- Python builds time, amount, location, and user-history features.
- Supervised and unsupervised training save preprocessing, feature order, and threshold/calibration artifacts.
- Spark micro-batches read Kafka transactions and publish suspicious transactions as alerts.
- The PostgreSQL sink commits a batch before acknowledging Kafka offsets, and upserts by transaction ID to support replay.

**Read first:** [feature engineering](https://github.com/Nihalrt/Realtime-Fraud-Detection-With-MLOps/blob/main/models/train_model.py), [stream scoring](https://github.com/Nihalrt/Realtime-Fraud-Detection-With-MLOps/blob/main/spark-streaming/main.py), [alert sink](https://github.com/Nihalrt/Realtime-Fraud-Detection-With-MLOps/blob/main/services/alert_sink/main.py).

**Boundary:** Features are batch-local, and the Pub/Sub generator is a separate ingestion path without an included Kafka bridge. Unit tests do not establish fraud-detection accuracy or end-to-end throughput.

## More engineering work

| Repository | What to inspect | Scope |
| --- | --- | --- |
| [Low-Level Traceroute Analyzer](https://github.com/Nihalrt/Low-Level-Traceroute-Analyzer) | Raw PCAP parsing, IPv4/UDP/ICMP headers, RTT aggregation, fragmentation | Networking learning project with supplied capture fixtures |
| [Hierarchical 3D Renderer](https://github.com/Nihalrt/Hierarchical-3D-Renderer) | Hierarchical transforms, texture mapping, WebGL shaders, camera controls | CSC 305 graphics coursework |
| [Inventory Management](https://github.com/Nihalrt/inventory-management) | Next.js/Redux dashboard, Express routes, Prisma schema and PostgreSQL | Full-stack dashboard; deployment availability is separate from source |
| [FILE-SYSTEMS](https://github.com/Nihalrt/FILE-SYSTEMS) | FAT-style disk structures and file read/write utilities in C | Educational filesystem exercises |
| [Radical Sequencing](https://github.com/Nihalrt/Radical-Sequencing) | Mutex/condition-variable and semaphore implementations | Thread-synchronization exercises in C |
| [Responsive Queues](https://github.com/Nihalrt/Responsive-Queues) | Multi-level feedback queues and starvation prevention | Scheduling simulation in C |

## Research and learning

My UVic research work investigated speculative decoding for LLM inference. Employer and research experience is summarized on my [profile](README.md); private work is not represented as public source code.

Older applications, notebooks, and interview-practice repositories record my learning over time. Forks retain their upstream authorship and are not presented here as projects I built from scratch. [Browse all public repositories](https://github.com/Nihalrt?tab=repositories).
