# hasura-otel-logs-metrics-exporter

This repository contains a demo where it shows how logs are exported from OpenTelemetry exporter in Hasura to OTEL collector and then build visualizations on top of that in Grafana via Loki

### Pre-requisites

- docker and docker-compose (to be installed on your machine)
- Familiarity with Loki, Prometheus and Grafana

### Get started

There is hasura folder containing metadata and migrations. It will use cli-migrations image so migrations will be automatically applied upon startup of hasura graphql-engine.

All the env variables are stored in `dotenv`. Please create a `.env` file by cloning the contents of `dotenv` file.

We have six services in docker-compose.yaml

- postgres
- grafana
- loki
- otel collector
- hasura
- prometheus

After setting up `.env`, please run

```
docker compose up
```

It'll take some time (1-2 mins) to apply migrations on Hasura project, and then after you can start by firing some queries on API explorer to see logs and metrics in action.

### Grafana dashboards

The grafana dashboards are present in `grafana` directory. After docker container is up and running without any service showing error, you can look up on `http://localhost:3000` . Upon opening, you'll be required to input username and password which can be found inside your env file.

After login, you'll find dashboards related to hasura. Some are showing logs and logs related visualizations, while some show metrics of Hasura engine.

### The flow of logs and metrics

The logs and metrics are exported by OTEL exporter in hasura, they'll be collected by OTEL collector. After OTEL collector processes, it'll export to desired targets. For logs, it would be Loki and for metrics, it would be prometheus.

### Useful links

- [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)
- [Loki (2.8.x)](https://grafana.com/docs/loki/v2.8.x/)
- [Prometheus](https://prometheus.io/)
