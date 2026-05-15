
#### Run

```bash
krknctl run node-interface-down [--param=value ...]
```

Run `krknctl describe node-interface-down` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Total length of chaos experiment in seconds. | integer | `60` |
| NODE_SELECTOR | Label selector for target nodes. | string | `` |
| NODE_NAME | Specific node name to target. | string | `` |
| NAMESPACE | Kubernetes namespace to apply chaos. | string | `default` |
| INSTANCE_COUNT | Number of instances to affect. | integer | `1` |
| EXECUTION | Execution mode, e.g., parallel or serial. | string | `parallel` |
| INTERFACES | Network interfaces to bring down. | string | `` |
| RECOVERY_TIME | Time in seconds before recovery. | integer | `0` |
| SERVICE_ACCOUNT | Service account used for injection. | string | `` |
| TAINTS | Node taints to apply during chaos. | string | `` |
<!-- AUTO:END id="params" -->
