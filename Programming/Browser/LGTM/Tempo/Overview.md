# Tempo Overview (LGTM Stack)

## What is Tempo?

Tempo is an open-source distributed tracing backend, designed for high-scale, cost-effective trace storage and querying. It is part of the **LGTM stack** (Loki, Grafana, Tempo, Mimir), which provides a full suite for observability.

## Key Features

- **Scalable and Cost-Effective**: Uses object storage (S3, GCS, Azure Blob) for trace storage, reducing costs.
- **No Indexing**: Unlike traditional tracing backends, Tempo does not require indexing, simplifying operations and improving scalability.
- **Compatible with Major Tracing Protocols**: Supports Jaeger, Zipkin, OpenTelemetry, and other tracing formats.
- **Seamless Integration with Grafana**: Enables tracing visualization and correlation with logs and metrics in Grafana.
- **Multi-Tenant Support**: Built-in support for multi-tenancy with authentication mechanisms.

## How Tempo Works

1. **Trace Collection**: Receives traces from OpenTelemetry, Jaeger, Zipkin, or other sources.
2. **Trace Storage**: Stores traces in backends like S3, GCS, or Azure Blob without requiring an index.
3. **Trace Retrieval**: Uses a trace ID-based lookup for efficient querying.
4. **Visualization & Correlation**: Integrates with Grafana for tracing visualization and correlating with logs (Loki) and metrics (Mimir).

## Deployment Options

- **Standalone**: Runs as a single binary for small-scale deployments.
- **Distributed**: Can be deployed as a microservices architecture for large-scale environments.
- **Kubernetes Native**: Supports deployment on Kubernetes with Helm charts and operator support.

## Integrating Tempo with LGTM Stack

1. **Loki (Logs)** - Enables linking logs with traces for deeper observability.
2. **Grafana (Visualization)** - Provides a UI for exploring traces and correlating with logs/metrics.
3. **Mimir (Metrics)** - Stores and queries metrics to complement tracing.

## Use Cases

- **Microservices Debugging**: Track requests across multiple services to diagnose issues.
- **Performance Monitoring**: Identify bottlenecks in distributed systems.
- **Incident Response**: Quickly pinpoint root causes by correlating traces with logs and metrics.
- **Cost-Effective Tracing**: Reduce costs by leveraging object storage instead of high-maintenance databases.

## Getting Started

- **Install via Helm** (Kubernetes):
    
    ```sh
    helm repo add grafana https://grafana.github.io/helm-charts
    helm install tempo grafana/tempo
    ```
    
- **Run via Docker**:
    
    ```sh
    docker run -p 3200:3200 grafana/tempo:latest
    ```
    
- **Configure Tracing Clients**: Send traces using OpenTelemetry, Jaeger, or Zipkin.

## Conclusion

Tempo is a powerful, scalable tracing backend that seamlessly integrates with the LGTM stack. Its focus on cost-effective storage and deep Grafana integration makes it an ideal choice for modern observability solutions.