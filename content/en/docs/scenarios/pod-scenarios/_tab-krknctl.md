
#### Run

```bash
krknctl run pod-scenarios [--param=value ...]
```

Run `krknctl describe pod-scenarios` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| NAMESPACE | Target namespace for pods, defaults to openshift-* | string | `openshift-*` |
| NODE_NAMES | Comma-separated list of node names to target, optional | string | `` |
| NODE_LABEL_SELECTOR | Label selector to filter nodes, optional | string | `` |
| POD_LABEL | Label to select pods for disruption, optional | string | `` |
| EXCLUDE_LABEL | Label to exclude pods from being targeted, optional | string | `` |
| NAME_PATTERN | Regex pattern for pod name matching, defaults to any pod | string | `.*` |
| DISRUPTION_COUNT | Number of pods to disrupt simultaneously, defaults to 1 | int | `1` |
| KILL_TIMEOUT | Maximum time in seconds to wait before killing a pod, defaults to 180 | int | `180` |
| EXPECTED_RECOVERY_TIME | Estimated time in seconds for a disrupted pod to recover, defaults to 120 | int | `120` |
<!-- AUTO:END id="params" -->
