
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
| ACTION | User-defined action to perform | string | `` |
| LABEL_SELECTOR | Label selector used to identify target nodes | string | `node-role.kubernetes.io/worker` |
| EXCLUDE_LABEL | Optional label to exclude from selection | string | `` |
| NODE_NAME | Specific node name to target | string | `` |
| INSTANCE_COUNT | Number of instances to trigger | int | `1` |
| RUNS | Number of times to repeat the scenario | int | `1` |
| CLOUD_TYPE | Cloud provider type | string | `aws` |
| TIMEOUT | Timeout value in seconds before aborting | int | `180` |
| DURATION | Duration of the scenario in seconds | int | `120` |
| PARALLEL | Enable parallel execution | bool | `false` |
| VERIFY_SESSION | Verify the session after execution | bool | `false` |
| SKIP_OPENSHIFT_CHECKS | Skip OpenShift-specific checks | bool | `false` |
| KUBE_CHECK | Perform Kubernetes health checks | bool | `true` |
| DISABLE_SSL_VERIFICATION | Disable SSL verification for connections | bool | `false` |
| BMC_USER | BMC username for hardware access | string | `` |
| BMC_PASSWORD | BMC password for hardware access | string | `` |
| BMC_ADDR | BMC address to connect to | string | `` |
| DISKS | Disk specifications for VMs | string | `` |
| VSPHERE_IP | vSphere IP address for integration | string | `` |
| VSPHERE_USERNAME | vSphere username for integration | string | `` |
| VSPHERE_PASSWORD | vSphere password for integration | string | `` |
| AWS_ACCESS_KEY_ID | AWS access key ID | string | `` |
| AWS_SECRET_ACCESS_KEY | AWS secret access key | string | `` |
| AWS_DEFAULT_REGION | Default AWS region | string | `` |
| IBMC_URL | IBM Cloud URL for integration | string | `` |
| IBMC_POWER_URL | IBM Cloud Power URL for integration | string | `` |
| IBMC_POWER_CRN | IBM Cloud Power CRN for integration | string | `` |
| IBMC_APIKEY | IBM Cloud API key for integration | string | `` |
| AZURE_TENANT_ID | Azure tenant ID for integration | string | `` |
| AZURE_CLIENT_SECRET | Azure client secret for integration | string | `` |
| AZURE_CLIENT_ID | Azure client ID for integration | string | `` |
| AZURE_SUBSCRIPTION_ID | Azure subscription ID for integration | string | `` |
| GOOGLE_APPLICATION_CREDENTIALS | Google application credentials file path | string | `` |

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
