```bash
krknctl run node-network-filter [--<parameter> <value>]
```

Can also set any global variable listed [here](../../all-scenario-env-krknctl.md)

### Node Network Filter Parameters

krknctl marks `--ingress` and `--egress` as required flags (you should pass both). **Values:** at least one of `--ingress` or `--egress` must be `true`; both may be `true` to filter incoming and outgoing traffic.

| Argument          | Type    | Description                                                                 | Required | Default Value                       |
| :---------------- | :------ | :-------------------------------------------------------------------------- | :------- | :---------------------------------- |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Total duration of the chaos experiment in seconds. | int | `60` |
| NODE_SELECTOR | Node label selector for targeting nodes. | string | `` |
| NODE_NAME | Specific node name to target. | string | `` |
| NAMESPACE | Kubernetes namespace to apply chaos. | string | `default` |
| INSTANCE_COUNT | Number of instances to target. | int | `1` |
| EXECUTION | Execution mode or strategy. | string | `` |
| INGRESS | Ingress traffic filter. | string | `` |
| EGRESS | Egress traffic filter. | string | `` |
| INTERFACES | Network interfaces to filter. | string | `` |
| PORTS | Port numbers to filter. | string | `` |
| PROTOCOLS | Protocol(s) to filter, e.g., tcp,udp. | string | `tcp` |
| TAINTS | Node taints to apply. | string | `` |
| SERVICE_ACCOUNT | Service account to target pods. | string | `` |
<!-- AUTO:END id="params" -->

### Parameter Format Details

**Node Selection:**
- `--node-selector`: Label selector in format `key=value` (e.g., `node-role.kubernetes.io/worker=`)
- `--node-name`: Specific node name (e.g., `ip-10-0-1-100.ec2.internal`)
- Specify either `--node-selector` OR `--node-name`, not both
- When using `--node-selector`, use `--instance-count` to limit the number of selected nodes

**Port Format:**
- Single port: `8080`
- Multiple ports: `8080,8081,8082` (comma-separated, no spaces)

**Protocol Format:**
- Valid values: `tcp`, `udp`, `tcp,udp`, or `udp,tcp`
- Default: `tcp`

**Interface Format:**
- Applies to **egress** (outgoing) filtering, matching the scenario image metadata
- Single interface: `eth0`
- Multiple interfaces: `eth0,eth1,eth2` (comma-separated, no spaces)
- May be left empty when not needed for your egress rules

**Taints Format:**
- Comma-separated Kubernetes **taints**; the workload gets matching tolerations
- Examples: `node-role.kubernetes.io/master:NoSchedule` or `key=value:NoSchedule` when the taint includes a value

### Usage Notes

- **Node targeting:** This scenario targets nodes (not pods) and creates iptables rules on the target node(s) to filter network traffic
- **Ingress/Egress:** Pass both flags; at least one must be `true`. Both may be `true` to filter incoming and outgoing traffic
- **Execution modes:**
  - `parallel`: Applies network filtering to all selected nodes simultaneously
  - `serial`: Applies network filtering to nodes one at a time

### Example Commands

**Basic egress filtering (block outgoing traffic):**
```bash
krknctl run node-network-filter \
  --node-selector node-role.kubernetes.io/worker= \
  --instance-count 1 \
  --ingress false \
  --egress true \
  --ports 8080 \
  --protocols tcp \
  --chaos-duration 120
```

**Ingress + egress filtering (block both incoming and outgoing):**
```bash
krknctl run node-network-filter \
  --node-name ip-10-0-1-100.ec2.internal \
  --ingress true \
  --egress true \
  --ports 9090,9091 \
  --protocols tcp,udp \
  --interfaces eth0 \
  --chaos-duration 300
```

**Multi-port filtering with parallel execution:**
```bash
krknctl run node-network-filter \
  --node-selector kubernetes.io/os=linux \
  --instance-count 3 \
  --execution parallel \
  --ingress false \
  --egress true \
  --ports 6379,6380,6381 \
  --protocols tcp \
  --chaos-duration 180
```