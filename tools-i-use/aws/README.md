# 🟧 AWS — Amazon Web Services

## Stack
- **Amazon Bedrock** — managed LLM / RAG (multi-model)
- **S3 + DynamoDB** — object store + NoSQL feature/lookup store (openFDA dataset)
- **boto3** — Python SDK automation
- **3-cloud reconcile** — same dataset landed & cross-checked across GCP / AWS / Azure to prove portability

## What it demonstrates
- RAG on a managed cloud LLM service (Bedrock) vs self-hosted Vertex/Gemini — same retrieval contract, different provider
- NoSQL feature store pattern (DynamoDB) alongside the BigQuery warehouse
- Provider-agnostic data engineering: one pipeline, three clouds, reconciled outputs

> Repos: [mocktailverse-bedrock](https://github.com/anix-lynch/mocktailverse-bedrock) · [healthcare-de-AWS](https://github.com/anix-lynch/healthcare-de-AWS) · [realtime-fraud-detection](https://github.com/anix-lynch/realtime-fraud-detection)
