---
title: Krkn-Hub All Scenarios Variables
description: >
date: 2017-01-05
weight: 1
---
These variables are to be used for the top level configuration template that are shared by all the scenarios in Krkn-hub.

Each section below corresponds to a section in the [Krkn config reference](../krkn/config.md). Set variables on the host running the container:

```bash
export <parameter_name>=<value>
```

---

## Kraken

Signal and status publishing settings. See [Kraken config](../krkn/config.md#kraken) for full details.

Parameter | Description | Default
--- | --- | ---
`KRKN_KUBE_CONFIG` | Path to the kubeconfig file for cluster access | _required_
`PUBLISH_KRAKEN_STATUS` | Publish kraken status to the signal address | True
`SIGNAL_ADDRESS` | Address to publish kraken status to | 0.0.0.0
`PORT` | Port to publish kraken status to | 8081
`SIGNAL_STATE` | Waits for the RUN signal when set to PAUSE before running the scenarios, refer [docs](../krkn/signal.md) for more details | RUN

---

## Cerberus

Cluster health monitoring integration. See [Cerberus config](../krkn/config.md#cerberus) for full details.

{{< param-table scenario="globals" source="krkn-hub" group="cerberus" >}}

---

## Performance Monitoring

Prometheus metrics collection and alert evaluation. See [Performance Monitoring config](../krkn/config.md#performance-monitoring) for full details.

Parameter | Description | Default
--- | --- | ---
`PROMETHEUS_URL` | URL to Prometheus instance; auto-detected on OpenShift, required for Kubernetes | _blank_
`PROMETHEUS_TOKEN` | Bearer token for Prometheus authentication; auto-detected on OpenShift, required for Kubernetes | _blank_
`UUID` | UUID for the run; auto-generated if not set | _blank_
`CAPTURE_METRICS` | Captures metrics as specified in the profile from in-cluster prometheus. Default metrics captures are listed [here](https://github.com/krkn-chaos/krkn/blob/master/config/metrics-aggregated.yaml) | False
`METRICS_PATH` | Path to the metrics profile to use when CAPTURE_METRICS is set | config/metrics-aggregated.yaml
`ENABLE_ALERTS` | Evaluates expressions from in-cluster prometheus and exits 0 or 1 based on the severity set. [Default profile](https://github.com/krkn-chaos/krkn/blob/master/config/alerts.yaml). | False
`ALERTS_PATH` | Path to the alerts file to use when ENABLE_ALERTS is set | config/alerts
`CHECK_CRITICAL_ALERTS` | When enabled will check prometheus for critical alerts firing post chaos | False

---

## Resiliency Score

Resiliency scoring configuration. See [Resiliency Score config](../krkn/config.md#resiliency-score) for full details.

Parameter | Description | Default
--- | --- | ---
`RESILIENCY_RUN_MODE` | Resiliency scoring mode: `standalone` embeds score in telemetry, `detailed` prints JSON report to stdout, `disabled` turns off scoring | standalone
`RESILIENCY_FILE` | Path to a YAML file containing SLO definitions; defaults to the alerts profile or `config/alerts.yaml` | config/alerts.yaml

---

## Elastic

Elasticsearch storage for telemetry and metrics. See [Elastic config](../krkn/config.md#elastic) for full details.

Parameter | Description | Default
--- | --- | ---
`ENABLE_ES` | Enable Elasticsearch integration | False
`ES_VERIFY_CERTS` | Verify SSL certificates when connecting to Elasticsearch | True
`ES_SERVER` | URL of the Elasticsearch instance | _blank_
`ES_PORT` | Port of the Elasticsearch instance | _blank_
`ES_USERNAME` | Username for Elasticsearch authentication | _blank_
`ES_PASSWORD` | Password for Elasticsearch authentication | _blank_
`ES_METRICS_INDEX` | Elasticsearch index for metrics data | _blank_
`ES_ALERTS_INDEX` | Elasticsearch index for alerts data | _blank_
`ES_TELEMETRY_INDEX` | Elasticsearch index for telemetry data | _blank_
`ES_RUN_TAG` | Tag to identify the run in Elasticsearch | _blank_

---

## Tunings

Execution timing and iteration controls. See [Tunings config](../krkn/config.md#tunings) for full details.

{{< param-table scenario="globals" source="krkn-hub" group="general" >}}

---

## Telemetry

Run data collection and upload settings. See [Telemetry config](../krkn/config.md#telemetry) for full details.

{{< param-table scenario="globals" source="krkn-hub" group="telemetry" >}}

{{% alert title="Note" %}} For setting the `TELEMETRY_ARCHIVE_SIZE`, the lower the value the higher the number of archive files produced and uploaded (processed by `TELEMETRY_BACKUP_THREADS` simultaneously). For unstable or slow connections, keep this value low and increase `TELEMETRY_BACKUP_THREADS` so that on upload failure only the failed chunk is retried. {{% /alert %}}

---

## Health Checks

Application endpoint monitoring during chaos. See [Health Checks config](../krkn/config.md#health-checks) for full details.

{{< param-table scenario="globals" source="krkn-hub" group="health_check" >}}

---

## Virt Checks

KubeVirt VMI SSH connection monitoring during chaos. See [Virt Checks config](../krkn/config.md#virt-checks) for full details.

{{< param-table scenario="globals" source="krkn-hub" group="kubevirt" >}}
