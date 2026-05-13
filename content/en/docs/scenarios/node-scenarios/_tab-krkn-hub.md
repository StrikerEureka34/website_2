
#### Run

```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true \
  -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:node-scenarios
$ podman logs -f <container_name>
$ podman inspect <container_name> --format "{{.State.ExitCode}}"
```

```bash
$ docker run $(./get_docker_params.sh) --name=<container_name> --net=host \
  --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d containers.krkn-chaos.dev/krkn-chaos/krkn-hub:node-scenarios
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
| ACTION | The action to perform (e.g., inject, fault). | string | `` |
| LABEL_SELECTOR | Label selector used to identify target nodes. | string | `node-role.kubernetes.io/worker` |
| EXCLUDE_LABEL | Additional label to exclude from selection. | string | `` |
| NODE_NAME | Specific node name to target. | string | `` |
| INSTANCE_COUNT | Number of instances to generate. | int | `1` |
| RUNS | Number of times to repeat the scenario. | int | `1` |
| CLOUD_TYPE | The cloud provider type (e.g., aws). | string | `aws` |
| TIMEOUT | Timeout in seconds for operations. | int | `180` |
| DURATION | Duration in seconds for which to run the scenario. | int | `120` |
| PARALLEL | Whether to run operations in parallel. | bool | `False` |
| VERIFY_SESSION | Whether to verify session connectivity. | bool | `False` |
| SKIP_OPENSHIFT_CHECKS | Whether to skip OpenShift health checks. | bool | `False` |
| KUBE_CHECK | Whether to perform Kubernetes health checks. | bool | `True` |
| DISABLE_SSL_VERIFICATION | Whether to skip SSL verification. | bool | `False` |
| BMC_USER | BMC username for remote management. | string | `` |
| BMC_PASSWORD | BMC password. | string | `` |
| BMC_ADDR | BMC address. | string | `` |
| DISKS | Disk configuration details. | string | `` |
| VSPHERE_IP | vSphere IP address. | string | `` |
| VSPHERE_USERNAME | vSphere username. | string | `` |
| VSPHERE_PASSWORD | vSphere password. | string | `` |
| AWS_ACCESS_KEY_ID | AWS access key ID. | string | `` |
| AWS_SECRET_ACCESS_KEY | AWS secret access key. | string | `` |
| AWS_DEFAULT_REGION | AWS region. | string | `` |
| IBMC_URL | IBM Cloud URL. | string | `` |
| IBMC_POWER_URL | IBM Cloud Power URL. | string | `` |
| IBMC_POWER_CRN | IBM Cloud Power CRN. | string | `` |
| IBMC_APIKEY | IBM Cloud API key. | string | `` |
| AZURE_TENANT_ID | Azure tenant ID. | string | `` |
| AZURE_CLIENT_SECRET | Azure client secret. | string | `` |
| AZURE_CLIENT_ID | Azure client ID. | string | `` |
| AZURE_SUBSCRIPTION_ID | Azure subscription ID. | string | `` |
| GOOGLE_APPLICATION_CREDENTIALS | Path to Google application credentials file. | string | `` |

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
