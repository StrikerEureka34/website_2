
#### Run

```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true \
  -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:node-cpu-hog
$ podman logs -f <container_name>
$ podman inspect <container_name> --format "{{.State.ExitCode}}"
```

```bash
$ docker run $(./get_docker_params.sh) --name=<container_name> --net=host \
  --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:node-cpu-hog
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
| TOTAL_CHAOS_DURATION | Total duration of the chaos experiment in seconds. | int | `60` |
| NODE_CPU_CORE | Number of CPU cores per node to target with the hog. | int | `` |
| NODE_CPU_PERCENTAGE | Percentage of CPU usage to hog on each node. | int | `50` |
| NAMESPACE | Kubernetes namespace where the chaos pod is launched. | string | `default` |
| NODE_SELECTOR | Node label selector to target specific nodes. | string | `` |
| NUMBER_OF_NODES | Number of nodes to involve in the experiment. | int | `` |
| TAINTS | Taints to tolerate for the chaos pod. | string | `` |
<!-- AUTO:END id="params" -->

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
