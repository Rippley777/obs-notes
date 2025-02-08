Grafana is a **browser-based** observability platform and visualization tool. It runs as a web application, typically served from a backend that can be hosted on a server, a container, or even locally. You interact with it entirely through a web UI.

### **What is Grafana?**

- **Web-based dashboarding tool**: You access it via a browser (e.g., `http://localhost:3000` by default).
- **Data visualization & alerting**: It connects to various **data sources** (Prometheus, Loki, MySQL, PostgreSQL, InfluxDB, etc.) and allows you to create **interactive dashboards**.
- **Multi-source support**: Unlike Prometheus (metrics) or Loki (logs), Grafana is **not** a data storage system. Instead, it queries data from external sources and visualizes it.
- **Observability hub**: In an **LGTM stack**, it ties together:
    - **Logs (Loki)**
    - **Metrics (Mimir)**
    - **Traces (Tempo)**

---

### **How It Works**

1. **You install Grafana** (runs as a server process, default port `3000`).
2. **You configure data sources** (Loki, Prometheus, Tempo, etc.).
3. **You create dashboards** using its UI, querying and visualizing logs, metrics, and traces.
4. **You set up alerts** based on queries (e.g., if CPU usage spikes above 80%, send a Slack alert).

