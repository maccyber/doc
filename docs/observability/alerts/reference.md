# NAIS Alert reference

<!--
  This documentation was automatically generated by the liberator pipeline.
  See https://github.com/nais/liberator/actions for details.

  DO NOT MAKE MANUAL CHANGES TO THIS FILE, THEY WILL BE OVERWRITTEN!
-->

This document describes all possible configuration values in the `Alert` spec, commonly known as the `alert.yaml` file.

## alerts
Type: `array`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].action
What human actions are needed to resolve or investigate this alert.

Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].alert
The name of the alert.

Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].description
Simple description of the triggered alert.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].documentation
URL for documentation for this alert.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].expr
Prometheus expression that triggers an alert. Explore expressions in the [Prometheus](https://docs.nais.io/observability/alerts/#writing-the-expr)-interface

Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].for
Duration before the alert should trigger.

Type: `string`<br />
Required: `true`<br />
Pattern: `^\d+[smhdwy]$`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].severity
Alert level for Slack messages.

Type: `string`<br />
Required: `false`<br />
Default value: `danger`<br />
Pattern: `^$|good|warning|danger|#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

### alerts[].sla
Time before a human should resolve the alert.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      alerts:
        - action: kubectl describe pod {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for events, og `kubectl logs {{ $labels.kubernetes_pod_name }} -n {{ $labels.kubernetes_namespace }}` for logger
          alert: applikasjon nede
          description: App {{ $labels.app }} er nede i namespace {{ $labels.kubernetes_namespace }}
          documentation: https://doc.nais.io/observability/alerts/
          expr: kube_deployment_status_replicas_available{deployment="<appname>"} > 0
          for: 2m
          severity: danger
          sla: Mellom 8 og 16
    ```

## inhibitRules
A list of inhibit rules. An inhibition rule mutes an alert (target) matching a set of matchers when an alert (source) exists that matches another set of matchers. Both target and source alerts must have the same label values for the label names in the labels list.

Relevant information:

* [https://prometheus.io/docs/alerting/latest/configuration/#inhibit_rule](https://prometheus.io/docs/alerting/latest/configuration/#inhibit_rule)

Type: `array`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

### inhibitRules[].labels
Labels that must have an equal value in the source and target alert for the inhibition to take effect.

Type: `array`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

### inhibitRules[].sources
Matchers for which one or more alerts have to exist for the inhibition to take effect. These are key/value pairs.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

### inhibitRules[].sourcesRegex
Regex matchers for which one or more alerts have to exist for the inhibition to take effect. These are key/value pairs, where the value can be a regex.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

### inhibitRules[].targets
Matchers that have to be fulfilled in the alerts to be muted. These are key/value pairs.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

### inhibitRules[].targetsRegex
Regex matchers that have to be fulfilled in the alerts to be muted. These are key/value pairs, where the value can be a regex.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      inhibitRules:
        - labels:
            - label
            - name
          sources:
            key: value
          sourcesRegex:
            key: value(.)?
          targets:
            key: value
          targetsRegex:
            key: value(.)+
    ```

## receivers
A list of notification recievers. You can use one or more of: e-mail, slack, sms. There needs to be at least one receiver.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        email:
          to: myteam@nav.no
        slack:
          channel: '#alert-channel'
          icon_emoji: ':chart_with_upwards_trend:'
          icon_url: http://lorempixel.com/48/48
          prependText: Oh noes!
          send_resolved: true
          username: Alertmanager
        sms:
          recipients: "12345678"
          send_resolved: false
        webhook:
          http_config:
            proxy_url: webproxy.nav
            tls_config:
              insecure_skip_verify: true
          max_alerts: 0
          send_resolved: true
          url: https://the.feature.now
    ```

### receivers.email
Alerts via e-mails

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        email:
          to: myteam@nav.no
    ```

#### receivers.email.send_resolved
Whether or not to notify about resolved alerts.

Type: `boolean`<br />
Required: `false`<br />
Default value: `false`<br />

#### receivers.email.to
Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        email:
          to: myteam@nav.no
    ```

### receivers.slack
Slack notifications are sent via Slack webhooks.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          channel: '#alert-channel'
          icon_emoji: ':chart_with_upwards_trend:'
          icon_url: http://lorempixel.com/48/48
          prependText: Oh noes!
          send_resolved: true
          username: Alertmanager
    ```

#### receivers.slack.channel
The channel or user to send notifications to. Can be specified with and without `#`.

Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          channel: '#alert-channel'
    ```

#### receivers.slack.icon_emoji
Emoji to use as the icon for this message

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          icon_emoji: ':chart_with_upwards_trend:'
    ```

#### receivers.slack.icon_url
URL to an image to use as the icon for this message

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          icon_url: http://lorempixel.com/48/48
    ```

#### receivers.slack.prependText
Text to prepend every Slack message with severity `danger`.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          prependText: Oh noes!
    ```

#### receivers.slack.send_resolved
Whether or not to notify about resolved alerts.

Type: `boolean`<br />
Required: `false`<br />
Default value: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          send_resolved: true
    ```

#### receivers.slack.username
Set your bot's user name.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        slack:
          username: Alertmanager
    ```

### receivers.sms
Alerts via SMS

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        sms:
          recipients: "12345678"
          send_resolved: false
    ```

#### receivers.sms.recipients
Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        sms:
          recipients: "12345678"
    ```

#### receivers.sms.send_resolved
Whether or not to notify about resolved alerts.

Type: `boolean`<br />
Required: `false`<br />
Default value: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        sms:
          send_resolved: false
    ```

### receivers.webhook
Alerts via custom web application

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          http_config:
            proxy_url: webproxy.nav
            tls_config:
              insecure_skip_verify: true
          max_alerts: 0
          send_resolved: true
          url: https://the.feature.now
    ```

#### receivers.webhook.http_config
A http_config allows configuring the HTTP client that the receiver uses to communicate with HTTP-based API services.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          http_config:
            proxy_url: webproxy.nav
            tls_config:
              insecure_skip_verify: true
    ```

##### receivers.webhook.http_config.proxy_url
Optional proxy URL.

Type: `string`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          http_config:
            proxy_url: webproxy.nav
    ```

##### receivers.webhook.http_config.tls_config
Configures the TLS settings.

Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          http_config:
            tls_config:
              insecure_skip_verify: true
    ```

###### receivers.webhook.http_config.tls_config.insecure_skip_verify
Disable validation of the server certificate.

Type: `boolean`<br />
Required: `false`<br />
Default value: `false`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          http_config:
            tls_config:
              insecure_skip_verify: true
    ```

#### receivers.webhook.max_alerts
The maximum number of alerts to include in a single webhook message. Alerts above this threshold are truncated. When leaving this at its default value of 0, all alerts are included.

Type: `integer`<br />
Required: `true`<br />
Default value: `0`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          max_alerts: 0
    ```

#### receivers.webhook.send_resolved
Whether or not to notify about resolved alerts.

Type: `boolean`<br />
Required: `false`<br />
Default value: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          send_resolved: true
    ```

#### receivers.webhook.url
The endpoint to send HTTP POST requests to.

Type: `string`<br />
Required: `true`<br />

??? example
    ``` yaml
    spec:
      receivers:
        webhook:
          url: https://the.feature.now
    ```

## route
Type: `object`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      route:
        group_by:
          - label
          - name
        groupInterval: 5m
        groupWait: 30s
        repeatInterval: 3h
    ```

### route.groupInterval
How long to wait before sending a notification about new alerts that are added to a group of alerts for which an initial notification has already been sent.

Type: `string`<br />
Required: `false`<br />
Default value: `5m`<br />
Pattern: `((([0-9]+)y)?(([0-9]+)w)?(([0-9]+)d)?(([0-9]+)h)?(([0-9]+)m)?(([0-9]+)s)?(([0-9]+)ms)?|0)`<br />

??? example
    ``` yaml
    spec:
      route:
        groupInterval: 5m
    ```

### route.groupWait
How long to initially wait to send a notification for a group of alerts. Allows to wait for an inhibiting alert to arrive or collect more initial alerts for the same group.

Type: `string`<br />
Required: `false`<br />
Default value: `10s`<br />
Pattern: `((([0-9]+)y)?(([0-9]+)w)?(([0-9]+)d)?(([0-9]+)h)?(([0-9]+)m)?(([0-9]+)s)?(([0-9]+)ms)?|0)`<br />

??? example
    ``` yaml
    spec:
      route:
        groupWait: 30s
    ```

### route.group_by
The labels by which incoming alerts are grouped together.

Type: `array`<br />
Required: `false`<br />

??? example
    ``` yaml
    spec:
      route:
        group_by:
          - label
          - name
    ```

### route.repeatInterval
How long to wait before sending a notification again if it has already been sent successfully for an alert.

Type: `string`<br />
Required: `false`<br />
Default value: `1h`<br />
Pattern: `((([0-9]+)y)?(([0-9]+)w)?(([0-9]+)d)?(([0-9]+)h)?(([0-9]+)m)?(([0-9]+)s)?(([0-9]+)ms)?|0)`<br />

??? example
    ``` yaml
    spec:
      route:
        repeatInterval: 3h
    ```

