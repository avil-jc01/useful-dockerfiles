# prometheus-stack

Prometheus-stack is a Compose project containing a Prometheus server,
Grafana frontend, and Blackbox Exporter service. Its purpose is to
track uptime and TLS certificate metrics for a configurable set of
endpoints.

## Prometheus Server

The Prometheus server stores the metrics and performs the scraping.

Files:
 - etc/prometheus_config.yml.example: Prometheus configuration (see link TODO).

Ports:
 - 9091:9090 - frontend and querying port

## Grafana Frontend

The Grafana frontend allows the metrics to be viewed on a dashboard.

Files:
 - etc/grafana_datasource_config.yml: Grafana datasource configuration
 - etc/grafana_dashboard_config.yml: Grafana dashboard provider configuration
 - dashboards/blackbox_exporter_targets.json: dashboard for Blackbox Exporter targets

Ports:
 - 3001:3000 - Grafana web UI port

## Blackbox Exporter

The Blackbox Exporter allows Prometheus to provide uptime and a few
other metrics for endpoints that do not expose a Prometheus
native-format `/metrics` or similar. Prometheus is configured to
scrape it (and not the desired endpoint) using the `/probe` URI,
passing in the metrics target and other parameters.

Files:
 - etc/blackbox_config.yml: Blackbox Exporter configuration

Ports:
 - 9115:9115 - Blackbox Exporter http & web UI port