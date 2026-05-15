
#### Run

```bash
krknctl run node-network-filter [--param=value ...]
```

Run `krknctl describe node-network-filter` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Total duration of chaos in seconds | int | `60` |
| NODE_SELECTOR | Node selector to target specific nodes | string | `` |
| NODE_NAME | Specific node name to target | string | `` |
| NAMESPACE | Kubernetes namespace to target | string | `default` |
| INSTANCE_COUNT | Number of instances to affect | int | `1` |
| EXECUTION | Execution mode or strategy | string | `` |
| INGRESS | Ingress filter criteria | string | `` |
| EGRESS | Egress filter criteria | string | `` |
| INTERFACES | Network interfaces to target | string | `` |
| PORTS | Ports to filter | string | `` |
| PROTOCOLS | Network protocols to filter | string | `tcp` |
| TAINTS | Taints to apply | string | `` |
| SERVICE_ACCOUNT | Service account to target | string | `` |
<!-- AUTO:END id="params" -->
