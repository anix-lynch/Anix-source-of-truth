# 🔷 Azure — Microsoft Azure

## Stack
- **Microsoft Fabric + OneLake** — lakehouse, end-to-end on the free trial via CLI/API
- **dbt-fabric** — dbt adapter targeting Fabric warehouse
- **TMDL** — Tabular Model Definition Language (semantic models as code)
- **Power BI — Direct Lake** — reports straight off OneLake delta tables
- **DAX** — measures via the executeQueries API
- **Azure AD** — auth / tenant
- **Azure Cosmos DB** — NoSQL

## What it demonstrates
- Full Fabric lakehouse (deltalake → OneLake ingest → semantic model → Power BI report) driven entirely by CLI/API
- Semantic modeling as code (TMDL) + DAX, not click-ops
- The Microsoft analytics stack as a peer to the GCP/AWS pipelines (3-cloud portability)

> Repo: [healthcare-da](https://github.com/anix-lynch/healthcare-da) (Fabric)
