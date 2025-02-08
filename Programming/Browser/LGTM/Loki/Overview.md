# Overview of Loki from the LGTM Stack

Loki is a horizontally scalable, multi-tenant log aggregation system inspired by Prometheus. It is part of the LGTM stack (Loki, Grafana, Tempo, and Mimir), which is designed for observability by handling logs, metrics, and traces efficiently.

## Key Features
- **Index-Free Design**: Unlike Elasticsearch-based solutions, Loki does not index logs, making it highly efficient and cost-effective.
- **Scalability**: Supports horizontal scaling and multi-tenancy.
- **Integration with Grafana**: Works seamlessly with Grafana for visualization and querying.
- **LogQL**: Uses a PromQL-inspired query language for flexible log searching.
- **Storage Backends**: Supports various object storage solutions like S3, GCS, and Azure Blob Storage.
- **Native Kubernetes Support**: Designed to collect logs from Kubernetes clusters efficiently.

## Loki Architecture
Loki consists of several components:
1. **Distributor**: Accepts log entries and forwards them to ingesters.
2. **Ingester**: Buffers log entries in memory before persisting them to storage.
3. **Querier**: Handles queries and retrieves logs from storage.
4. **Query Frontend** (Optional): Improves query performance with caching and parallelization.
5. **Compactor**: Manages and optimizes stored logs to reduce storage costs.
6. **Index Gateway** (Optional): Handles metadata indexing for large-scale deployments.

## Deployment Options
- **Standalone**: Runs all components in a single instance for lightweight deployments.
- **Microservices Mode**: Deploys components separately for high availability and scalability.
- **Helm Chart for Kubernetes**: Deploys Loki in Kubernetes using Helm.

## LogQL - Loki's Query Language
Loki provides LogQL, a query language similar to PromQL, with two main types of queries:
- **Log Stream Queries**: `{"{app="nginx"}