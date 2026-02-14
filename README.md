# mathtrail-solution-validator
Validation engine that checks student solutions using symbolic computation and rule-based logic.

## Mission & Responsibilities
- Accept solution submissions (student answer + task reference)
- Validate solutions (exact match, symbolic equivalence, step-by-step)
- Return detailed feedback (correct/incorrect, hints, partial credit)
- Publish results for Profile and Mentor to consume

## Tech Stack
- **Language**: Go or Python (TBD — Python preferred for sympy)
- **Math Engine**: SymPy (symbolic), custom rule engine
- **Events**: Dapr pub/sub over Kafka

## API & Communication (Dapr)
- **Inbound**: REST API (POST /validate), Dapr invocation from UI
- **Outbound**: Dapr invoke → mathtrail-task (get solution reference)
- **Publishes**: `task.attempt.completed` (result for Profile + Mentor)

## Data Persistence
- **None** — stateless validator.

## Secrets
- None required

## Infrastructure
Standard `infra/` layout:
- `infra/helm/` — Helm chart + environment overlays (dev, on-prem, cloud)
- `infra/terraform/` — Environment scaffolds (stateless — no DB)
- `infra/ansible/` — On-prem node preparation

## Roadmap
1. Implement exact-match validator for numerical answers
2. Add symbolic equivalence checking (SymPy or equivalent)
3. Build feedback generator (partial credit, hint selection)
