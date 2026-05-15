
#### Run

```bash
krknctl run pod-scenarios [--param=value ...]
```

Run `krknctl describe pod-scenarios` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| NAMESPACE | Namespace to target for chaos injection | string | `openshift-*` |
| NODE_NAMES | Specific node names to target, leave empty to affect all nodes | string | `` |
| NODE_LABEL_SELECTOR | Label selector to filter nodes for targeting | string | `` |
| POD_LABEL | Label selector to filter pods for targeting | string | `` |
| EXCLUDE_LABEL | Label to exclude from targeting | string | `` |
| NAME_PATTERN | Regex pattern to match pod or node names | string | `.*` |
| DISRUPTION_COUNT | Number of resources to disrupt in each iteration | int | `1` |
| KILL_TIMEOUT | Maximum time in seconds to wait before killing a resource | int | `180` |
| EXPECTED_RECOVERY_TIME | Estimated time in seconds for the system to recover after disruption | int | `120` |
<!-- AUTO:END id="params" -->
