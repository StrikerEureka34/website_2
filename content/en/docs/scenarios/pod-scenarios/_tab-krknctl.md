
#### Run

```bash
krknctl run pod-scenarios [--param=value ...]
```

Run `krknctl describe pod-scenarios` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| NAMESPACE | Namespace to target for chaos. | string | `openshift-*` |
| NODE_NAMES | Comma-separated list of node names to target. | string | `` |
| NODE_LABEL_SELECTOR | Label selector for nodes. | string | `` |
| POD_LABEL | Label selector for pods. | string | `` |
| EXCLUDE_LABEL | Label selector to exclude resources. | string | `` |
| NAME_PATTERN | Regex pattern for resource names. | string | `.*` |
| DISRUPTION_COUNT | Number of resources to disrupt. | int | `1` |
| KILL_TIMEOUT | Timeout in seconds for killing pods. | int | `180` |
| EXPECTED_RECOVERY_TIME | Expected recovery time in seconds. | int | `120` |
<!-- AUTO:END id="params" -->
