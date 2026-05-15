
#### Run

```bash
krknctl run node-network-filter [--param=value ...]
```

Run `krknctl describe node-network-filter` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Length of the chaos experiment in seconds. | int | `60` |
| NODE_SELECTOR | Node label selector for targeting nodes. | string | `` |
| NODE_NAME | Specific node name to target. | string | `` |
| NAMESPACE | Kubernetes namespace to apply chaos resources. | string | `default` |
| INSTANCE_COUNT | Number of instances to inject chaos into. | int | `1` |
| EXECUTION | Execution mode or strategy for the scenario. | string | `` |
| INGRESS | Ingress traffic filter criteria. | string | `` |
| EGRESS | Egress traffic filter criteria. | string | `` |
| INTERFACES | Network interfaces to affect. | string | `` |
| PORTS | Port numbers to target in the scenario. | string | `` |
| PROTOCOLS | Network protocols to filter (e.g., tcp). | string | `tcp` |
| TAINTS | Node taint configuration to apply. | string | `` |
| SERVICE_ACCOUNT | Kubernetes service account used for chaos actions. | string | `` |
<!-- AUTO:END id="params" -->
