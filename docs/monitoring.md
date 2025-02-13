# Data Warehouse Monitoring
We will use Prometheus to collect metrics from the different services and we will use grafana for displaying the metrics.

## Dagster
For monitoring Dagster pipelines, we will first install `dagster-prometheus`

`pip install dagster-prometheus`

Then we will add prometheus to the `workspace.yaml` file

```
resources:
  prometheus:
    config:
      push_gateway_url: 'http://localhost:9091/'
```

Add the scrape job on `prometheus.yml`

```
  - job_name: prometheus
    honor_timestamps: true
    scrape_interval: 15s
    scrape_timeout: 10s
    metrics_path: /metrics
    scheme: http
    static_configs:
    - targets:
      - localhost:9090

```

## Minio
We will add a test json file for the minio dashboard. We also need to add the scrape job on `prometheus.yml` so that it can collect the metrics

```
- job_name: minio-job
  metrics_path: /minio/prometheus/metrics
  scheme: http
  static_configs:
      - targets: ['minio:9000']
```