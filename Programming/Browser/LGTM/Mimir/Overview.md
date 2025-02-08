# Overview of Mimir from the LGTM Stack

## Introduction

Mimir is the scalable, highly available, and multi-tenant time-series database component of the **LGTM stack** (Loki, Grafana, Tempo, and Mimir). It is designed to store and query Prometheus metrics efficiently, making it an ideal choice for observability and monitoring at scale.

## Key Features

- **Highly Scalable**: Mimir can handle millions of active time-series with horizontal scalability.
- **Multi-Tenancy**: Supports multiple users with isolated metric storage and queries.
- **Long-Term Storage**: Integrates with object storage (S3, GCS, Azure Blob) to persist time-series data.
- **Efficient Querying**: Optimized for PromQL queries with query caching and parallel execution.
- **Compaction & Retention**: Provides automatic compaction and retention policies to manage storage costs.
- **High Availability**: Supports replication and sharding to ensure minimal downtime.

## Architecture

Mimir follows a **modular microservices architecture**, similar to Cortex, and consists of several components:

- **Distributor**: Handles incoming metric data and distributes it to the appropriate ingesters.
- **Ingester**: Temporarily stores recent time-series data before persisting to long-term storage.
- **Querier**: Processes PromQL queries efficiently using caching and parallel execution.
- **Store-Gateway**: Optimizes long-term storage access and reduces load on object storage.
- **Compactor**: Runs periodic compaction jobs to optimize storage efficiency.
- **Ruler**: Evaluates and manages alerting and recording rules.
- **Frontend**: Handles query execution and caching for improved performance.

## Deployment Options

Mimir can be deployed in various environments:

- **Kubernetes**: Official Helm charts are available for seamless Kubernetes deployment.
- **Docker**: Supports containerized deployment using Docker Compose or standalone instances.
- **Bare Metal/VMs**: Can be deployed directly on virtual machines or physical hardware.

## Integration with LGTM Stack

Mimir integrates with other components of the LGTM stack:

- **Loki**: For centralized log aggregation alongside metrics.
- **Grafana**: Provides a rich UI for visualizing Mimir's stored metrics.
- **Tempo**: Enables distributed tracing to correlate logs, metrics, and traces.

## Use Cases

- **Kubernetes Monitoring**: Collects and stores Prometheus metrics for Kubernetes clusters.
- **Infrastructure Monitoring**: Tracks system performance across distributed infrastructure.
- **Application Performance Monitoring (APM)**: Stores time-series data for debugging and optimization.
- **IoT & Edge Monitoring**: Suitable for large-scale telemetry and time-series storage.

## Conclusion

Mimir is a powerful and scalable alternative to vanilla Prometheus, providing long-term metric storage, multi-tenancy, and high availability. It is a core component of the LGTM stack, making it an essential tool for modern observability solutions.