
#### Run

```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true \
  -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:pod-scenarios
$ podman logs -f <container_name>
$ podman inspect <container_name> --format "{{.State.ExitCode}}"
```

```bash
$ docker run $(./get_docker_params.sh) --name=<container_name> --net=host \
  --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:pod-scenarios
$ docker logs -f <container_name>
$ docker inspect <container_name> --format "{{.State.ExitCode}}"
```

**TIP**: Because the container runs with a non-root user, ensure the kube config
is globally readable before mounting it in the container.

#### Supported parameters

The following environment variables can be set on the host running the container
to tweak the scenario/faults being injected:

See list of variables that apply to all scenarios [here](/docs/scenarios/all-scenario-env.md)
that can be used/set in addition to these scenario specific variables

| Parameter | Description | Type | Default |
| --------- | ----------- | ---- | ------- |
<!-- AUTO:START id="params" -->
| NAMESPACE | Namespace to target with wildcard support. | string | `openshift-.*` |
| POD_LABEL | Label selector for pods to target. | string | `` |
| EXCLUDE_LABEL | Label to exclude from selection. | string | `` |
| NAME_PATTERN | Regex pattern for pod name matching. | string | `.*` |
| DISRUPTION_COUNT | Number of pods to disrupt in each iteration. | int | `1` |
| KILL_TIMEOUT | Maximum time in seconds to wait before force killing a pod. | int | `180` |
| EXPECTED_RECOVERY_TIME | Expected time in seconds for the system to recover after disruption. | int | `120` |
| NODE_LABEL_SELECTOR | Label selector for nodes to target. | string | `` |
| NODE_NAMES | Comma-separated list of node names to target. | string | `` |
<!-- AUTO:END id="params" -->

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
