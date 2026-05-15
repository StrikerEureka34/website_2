
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
| NAMESPACE | Target namespace pattern for pods, supports wildcard matching. | string | `openshift-*` |
| POD_LABEL | Label selector for target pods, optional. | string | `` |
| EXCLUDE_LABEL | Label selector to exclude certain pods from the scenario. | string | `` |
| NAME_PATTERN | Regex pattern for pod names to target in the scenario. | string | `.*` |
| DISRUPTION_COUNT | Number of pods to disrupt in this scenario. | int | `1` |
| KILL_TIMEOUT | Maximum time (seconds) to wait for a pod to be killed. | int | `180` |
| EXPECTED_RECOVERY_TIME | Estimated time (seconds) for disrupted pods to recover. | int | `120` |
| NODE_LABEL_SELECTOR | Node label selector to target nodes for chaos injection. | string | `` |
| NODE_NAMES | Explicit list of node names to target for chaos injection. | string | `` |
<!-- AUTO:END id="params" -->

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
