
#### Run

```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true -v <path-to-kube-config>:/home/krkn/.kube/config:Z -d quay.io/krkn-chaos/krkn-hub:node-network-filter
$ podman logs -f <container_name or container_id> # Streams Kraken logs
$ podman inspect <container-name or container-id> --format "{{.State.ExitCode}}" # Outputs exit code which can considered as pass/fail for the scenario
```

```bash
$ docker run $(./get_docker_params.sh) --name=<container_name> --net=host --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z -d quay.io/krkn-chaos/krkn-hub:node-network-filter
OR 
$ docker run -e <VARIABLE>=<value> --net=host --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z -d quay.io/krkn-chaos/krkn-hub:node-network-filter
$ docker logs -f <container_name or container_id> # Streams Kraken logs
$ docker inspect <container-name or container-id> --format "{{.State.ExitCode}}" # Outputs exit code which can considered as pass/fail for the scenario
```

**TIP**: Because the container runs with a non-root user, ensure the kube config is globally readable before mounting it in the container. You can achieve this with the following commands:
```bash
kubectl config view --flatten > ~/kubeconfig && chmod 444 ~/kubeconfig && docker run $(./get_docker_params.sh) --name=<container_name> --net=host --pull=always -v ~kubeconfig:/home/krkn/.kube/config:Z -d quay.io/krkn-chaos/krkn-hub:<scenario>
```


#### Supported parameters

The following environment variables can be set on the host running the container to tweak the scenario/faults being injected:

ex.) 
`export <parameter_name>=<value>`


See list of variables that apply to all scenarios [here](/docs/scenarios/all-scenario-env.md) that can be used/set in addition to these scenario specific variables

|  Parameter                    | Description                                                           | Type | Default
|-------------------------------| -----------------------------------------------------------------     | ---- | ------------------------------------ |
<!-- AUTO:START id="params" -->
| TOTAL_CHAOS_DURATION | Total duration of the chaos experiment in seconds. | int | `60` |
| NODE_SELECTOR | Label selector to target nodes for the experiment. | string | `` |
| NAMESPACE | Kubernetes namespace where the experiment is applied. | string | `default` |
| INSTANCE_COUNT | Number of instances to inject chaos into. | int | `1` |
| EXECUTION | Execution mode of the experiment (e.g., parallel or sequential). | string | `parallel` |
| INGRESS | Whether to block inbound traffic during the experiment. | bool | `false` |
| EGRESS | Whether to block outbound traffic during the experiment. | bool | `false` |
| INTERFACES | Network interfaces to target for chaos injection. | string | `` |
| PORTS | Ports to target for chaos injection. | string | `` |
| PROTOCOLS | Network protocols to target for chaos injection. | string | `tcp` |
| NODE_NAME | Specific node name to target for the experiment. | string | `` |
| TAINTS | Node taint to apply during the experiment. | string | `` |
| SERVICE_ACCOUNT | Service account to use for executing the experiment. | string | `` |
<!-- AUTO:END id="params" -->


**NOTE** In case of using custom metrics profile or alerts profile when `CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from the host on which the container is run using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml` and `/home/krkn/kraken/config/alerts`. For example:
```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true -v <path-to-custom-metrics-profile>:/home/krkn/kraken/config/metrics-aggregated.yaml -v <path-to-custom-alerts-profile>:/home/krkn/kraken/config/alerts -v <path-to-kube-config>:/home/krkn/.kube/config:Z -d quay.io/krkn-chaos/krkn-hub:node-network-filter
```