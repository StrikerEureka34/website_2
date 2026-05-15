
#### Run

```bash
krknctl run pod-scenarios [--param=value ...]
```

Run `krknctl describe pod-scenarios` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| NAMESPACE | Namespace to target for chaos actions. | string | `openshift-*` |
| NODE_NAMES | Specific node names to target (comma-separated list), if empty matches all nodes. | string | `` |
| NODE_LABEL_SELECTOR | Node label selector to identify nodes for chaos injection. | string | `` |
| POD_LABEL | Pod label selector to identify pods for chaos injection. | string | `` |
| EXCLUDE_LABEL | Label to exclude from chaos actions. | string | `` |
| NAME_PATTERN | Regex pattern to match resource names for chaos injection. | string | `.*` |
| DISRUPTION_COUNT | Number of resources to disrupt in each iteration. | int | `1` |
| KILL_TIMEOUT | Maximum time in seconds to wait before killing a target. | int | `180` |
| EXPECTED_RECOVERY_TIME | Estimated time in seconds for the disrupted resource to recover. | int | `120` |
<!-- AUTO:END id="params" -->
