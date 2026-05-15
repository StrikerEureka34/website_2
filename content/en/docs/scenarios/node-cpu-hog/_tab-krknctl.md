
#### Run

```bash
krknctl run node-cpu-hog [--param=value ...]
```

Run `krknctl describe node-cpu-hog` to see all available flags with their current defaults.

#### Supported parameters

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Duration of the chaos experiment in seconds. | int | `60` |
| NODE_CPU_CORE | Number of CPU cores to target on each node. | string | `` |
| NODE_CPU_PERCENTAGE | Percentage of CPU usage to overload. | int | `50` |
| NAMESPACE | Kubernetes namespace where the pod will be launched. | string | `default` |
| NODE_SELECTOR | Node label selector to target specific nodes. | string | `` |
| TAINTS | Node taint toleration list for pod scheduling. | string | `[]` |
| NUMBER_OF_NODES | Number of nodes to involve in the chaos scenario. | int | `0` |
<!-- AUTO:END id="params" -->
