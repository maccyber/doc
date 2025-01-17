# Alerts

If your application is [serving metrics](./metrics.md), you can create alerts to notify your team when something happens. The team is notified in the Slack channel specified in `Console` `https://console.nav.cloud.nais.io`

You can define alerts by using Kubernetes resources (`PrometheusRule`), as well as directly in Grafana (GUI based).

You will have a separate alertmanager for each environment available at `https://alertmanager.<environment>.nav.cloud.nais.io/`

## Kubernetes resources

We use native [Prometheus alert rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/), and let [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) handle the notifications.

You can define alerts by creating a `PrometheusRule` resource in your teams namespace.

```yaml
---
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: my-alert
spec:
  groups:
  - name: my-alert
    rules:
    - alert: InstanceDown
      expr: count(up) == 0
      for: 5m
      annotations:
        consequence: Application is unavailable
        action: "`kubectl describe pod <podname>` -> `kubectl logs <podname>`"
        summary: |-
          This is a multi-line summary with
          linebreaks and everything. Here you can give a more detailed
          summary of what this alert is about
      labels:
        namespace: <team namespace> # required
        severity: critical
```

Apply this resource to your teams namespace by creating a file containing the content above with your own values and running `kubectl apply -f <path to file>`

This file should be added to your application repository, alongside `nais.yaml` and be deployed by your CI/CD pipeline using the nais deploy action.

You can see the alerts in the Alertmanager at `https://alertmanager.<environment>.nav.cloud.nais.io/` and the defined rules in Prometheus at `https://prometheus.<environment>.nav.cloud.nais.io/rules`


### Deployment

To automatically deploy your alerts to the cluster, you can use the nais deploy action. This action will deploy the alerts to the cluster when you change the `alerts.yaml` file in your repository.

```yaml
name: Deploy alerts to NAIS
on:
  push:
    branches:
      - main
    paths:
      - 'alerts.yaml'
      - '.github/workflows/alerts.yaml'
jobs:
  apply-alerts:
    name: Apply alerts to cluster
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: deploy to dev
        uses: nais/deploy/actions/deploy@v1
        env:
          APIKEY: ${{ secrets.NAIS_DEPLOY_APIKEY }}
          CLUSTER: dev
          RESOURCE: /path/to/alerts.yaml
      - name: deploy to prod
        uses: nais/deploy/actions/deploy@v1
        env:
          APIKEY: ${{ secrets.NAIS_DEPLOY_APIKEY }}
          CLUSTER: prod
          RESOURCE: /path/to/alerts.yaml
```

## How to write a good alert

### Writing the `expr`

In order to minimize the feedback loop we suggest experimenting on the Prometheus server to find the right metric for your alert and the notification threshold.
The Prometheus server can be found in each cluster, at `https://prometheus.{env}.nav.cloud.nais.io` (e.g. https://prometheus.dev.nav.cloud.nais.io).

You can also visit the Alertmanager at `https://alertmanager.{env}.nav.cloud.nais.io` (e.g. https://alertmanager.dev.nav.cloud.nais.io) to see which alerts are triggered now (you can also silence already triggered alerts).

### `for`

How long time the `expr` must evaluate to `true` before firing.

When the `expr` first evaluates to `true` the alert will be in `pending` state for the duration specified.

Example values: `30s`, `5m`, `1h`.

### Severity

This will affect what color the notification gets. Possible values are `critical` (red), `warning` (yellow) and `notice` (green).

### Consequence

Optionally describe ahead of time to the one receiving the alert what happens in the world when this alert fires.

### Action

Optionally describe ahead of time to the one receiving the alert what is the best course of action to resolve this issue.

### Summary

Optional longer description of the alert
