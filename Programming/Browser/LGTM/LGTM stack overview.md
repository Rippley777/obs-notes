The **LGTM stack** is a monitoring and observability stack that consists of the following open-source tools:

1. **Loki** (by Grafana) - A log aggregation system similar to Elasticsearch but optimized for storing and querying logs efficiently. It is designed to work well with **Promtail**, **Fluentd**, and other log shippers.
    
2. **Grafana** - A powerful visualization and monitoring tool that allows you to create dashboards and alerts based on metrics, logs, and traces from various data sources, including **Loki**, **Prometheus**, and **Tempo**.
    
3. **Tempo** (by Grafana) - A distributed tracing system that helps track requests as they move through different services in a microservices architecture. It supports tracing formats like **Jaeger** and **Zipkin**.
    
4. **Mimir** (by Grafana) - A scalable and highly available time-series database designed as a long-term storage solution for **Prometheus** metrics.
    

### How They Work Together:

- **Loki** collects and stores logs.
- **Mimir** stores and processes time-series metrics.
- **Tempo** captures traces to help debug request flows across services.
- **Grafana** provides a unified interface to visualize logs, metrics, and traces in a single dashboard.

This stack is commonly used for cloud-native observability, replacing older ELK (Elasticsearch, Logstash, Kibana) or Prometheus + Alertmanager setups.