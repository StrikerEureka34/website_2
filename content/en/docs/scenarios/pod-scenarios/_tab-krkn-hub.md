
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
| NAMESPACE | Target namespace for chaos injection; default matches openshift-*. | string | `openshift-.*` |
| POD_LABEL | Label used to select pods for disruption; default is empty. | string | `` |
| EXCLUDE_LABEL | Label to exclude selected pods; default is empty. | string | `` |
| NAME_PATTERN | Pattern to match pod names; default matches any name. | string | `.*` |
| DISRUPTION_COUNT | Number of pod disruptions to cause; default is 1. | int | `1` |
| KILL_TIMEOUT | Timeout in seconds for killing a pod; default is 180. | int | `180` |
| EXPECTED_RECOVERY_TIME | Expected time in seconds for pods to recover; default is 120. | int | `120` |
| NODE_LABEL_SELECTOR | Node label selector to target nodes; default is empty. | string | `` |
| NODE_NAMES | Specific node names to target; default is empty. | string | `` |
<!-- AUTO:END id="params" -->

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
