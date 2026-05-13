
#### Run

```bash
$ podman run --name=<container_name> --net=host --pull=always --env-host=true \
  -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d quay.io/krkn-chaos/krkn-hub:node-scenarios
$ podman logs -f <container_name>
$ podman inspect <container_name> --format "{{.State.ExitCode}}"
```

```bash
$ docker run $(./get_docker_params.sh) --name=<container_name> --net=host \
  --pull=always -v <path-to-kube-config>:/home/krkn/.kube/config:Z \
  -d quay.io/krkn-chaos/krkn-hub:node-scenarios
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
| ACTION | Specifies the chaos action to perform on nodes, such as kill, drain, or reboot. | string | `` |
| LABEL_SELECTOR | Selects nodes by label to target for the experiment. | string | `` |
| EXCLUDE_LABEL | Excludes nodes with a specific label from the experiment. | string | `` |
| NODE_NAME | Names the specific node(s) to target for the chaos action. | string | `` |
| INSTANCE_COUNT | Number of nodes to involve in the chaos scenario. | int | `1` |
| RUNS | How many times to repeat the chaos experiment. | int | `1` |
| CLOUD_TYPE | Identifies the cloud provider, e.g., aws, azure, gcp. | string | `aws` |
| TIMEOUT | Maximum seconds to wait for the experiment to complete. | int | `180` |
| DURATION | Length of time the experiment runs before stopping. | int | `120` |
| PARALLEL | If true, runs experiments on multiple nodes concurrently. | bool | `False` |
| VERIFY_SESSION | If true, verifies the session after the experiment. | bool | `False` |
| SKIP_OPENSHIFT_CHECKS | If true, skips OpenShift-specific pre-checks. | bool | `False` |
| KUBE_CHECK | If true, performs additional Kubernetes health checks. | bool | `True` |
| DISABLE_SSL_VERIFICATION | If true, disables SSL verification for remote connections. | bool | `False` |
| BMC_USER | Username for accessing BMC console. | string | `` |
| BMC_PASSWORD | Password for accessing BMC console. | string | `` |
| BMC_ADDR | IP address or hostname of the BMC device. | string | `` |
| DISKS | Disk identifiers to target during the experiment. | string | `` |
| VSPHERE_IP | vSphere IP address for connecting to the virtual environment. | string | `` |
| VSPHERE_USERNAME | Username for vSphere authentication. | string | `` |
| VSPHERE_PASSWORD | Password for vSphere authentication. | string | `` |
| AWS_ACCESS_KEY_ID | AWS access key identifier used for API calls. | string | `` |
| AWS_SECRET_ACCESS_KEY | AWS secret access key used for API calls. | string | `` |
| AWS_DEFAULT_REGION | Default AWS region for API operations. | string | `` |
| IBMC_URL | IBM Cloud URL for accessing services. | string | `` |
| IBMC_POWER_URL | Power endpoint URL for IBM Cloud. | string | `` |
| IBMC_POWER_CRN | IBM Cloud Power CRN identifier. | string | `` |
| IBMC_APIKEY | API key for IBM Cloud authentication. | string | `` |
| AZURE_TENANT_ID | Azure AD tenant ID for authentication. | string | `` |
| AZURE_CLIENT_SECRET | Azure client secret used for authentication. | string | `` |
| AZURE_CLIENT_ID | Azure client ID for authentication. | string | `` |
| AZURE_SUBSCRIPTION_ID | Azure subscription ID for resource targeting. | string | `` |
| GOOGLE_APPLICATION_CREDENTIALS | Path to Google service account JSON credentials. | string | `` |

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
