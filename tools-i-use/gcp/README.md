# ☁️ GCP — Google Cloud Platform

What's actually built, deployed, and running — not "I've heard of it."

## Architecture

```
Batch ingestion
  load_bigquery.py  ──►  BigQuery WRITE_TRUNCATE  ──►  raw_healthcare_data (49,986 rows)
                                                            │
                                                    dbt transforms
                                                            │
                                              fact_encounters_optimized
                                              (DAY-partitioned · clustered)

Streaming — Path A (Pub/Sub push)
  publish_event.py  ──►  Pub/Sub topic        ──►  Cloud Run FastAPI  ──►  MERGE  ──►  raw_ingest_clean
                         encounter-events            /pubsub/push            │
                                                   (validate + quarantine)  STG table

Streaming — Path B (direct BQ subscription)
  vitals-stream  ──►  BigQuery direct subscription  ──►  streaming_vitals
                      (no Cloud Run, BQ handles delivery)

Operational layer
  Cloud Scheduler: freshness watchdog  ──►  HTTP ping every 6h  ──►  Cloud Run watchdog
  Artifact Registry: Docker images per service
  Cloud Build: CI image builds
  Cloud Logging + Monitoring: wired to all services
```

## Services — Live
- 7 Cloud Run services deployed with live HTTPS URLs (scale-to-zero, $0 idle)
- 2 Pub/Sub topics (encounter-events + vitals-stream), both ACTIVE
- Cloud Scheduler freshness watchdog, every 6h, ENABLED
- Artifact Registry + Cloud Build: Docker CI pipeline

## Warehouse — BigQuery
- 4 datasets: analytics · governed · secure · openfda_gold
- 35+ tables: partitioned facts · materialized views · Feast feature tables
- dbt-bigquery adapter: full project (models · tests · sources · seeds)
- Great Expectations quality gate: 0 violations in agent-facing corpus
- Dataplex + Dataform: governance + SQL workflow layer

## AI Layer
- Vertex AI + Gemini (Flash): grounded RAG, production
- BM25 + Feast feature store for retrieval

## Google Maps Platform
- Full API suite + SA key: Places · Geocoding · Routes · Directions · Distance Matrix · Static Maps · Street View · Elevation · Maps Embed
- Same project also runs: Vertex AI · Gemini · Vision AI · Text-to-Speech · Translate · Discovery Engine
- Infra: Cloud Functions · Firestore · Cloud SQL · Secret Manager · Eventarc · Workflows · Cloud Run · Pub/Sub

## Workspace Automation (GAM)
- Zero-browser Gmail / Drive / Calendar / Admin SDK automation across 2 domains
- Powers a JD pipeline: Gemini → Sheet → Gmail draft → send, no browser

## Interview one-liners
- **Streaming pipeline?** → Pub/Sub push subscription into Cloud Run FastAPI, record-level validation + quarantine, idempotent MERGE into BigQuery. Two paths: push-to-Cloud-Run and direct BQ subscription.
- **BigQuery in production?** → ~50k rows, 4 datasets, partitioned + clustered, dbt transforms, Great Expectations gates.
- **Cloud Run experience?** → 7 services, scale-to-zero, Pub/Sub push + Cloud Scheduler watchdog.
- **Google Maps APIs?** → Full suite on a dedicated project, SA key active, can demo any of them.
- **Workspace automation?** → GAM across 2 domains, zero-browser, built a zero-touch JD → email-draft pipeline.

> Repos: [healthcare-ai-data-engineer](https://github.com/anix-lynch/healthcare-ai-data-engineer) · [healthcare-signal-platform](https://github.com/anix-lynch/healthcare-signal-platform) · [healthcare-genai-engineer](https://github.com/anix-lynch/healthcare-genai-engineer)
