
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
| ACTION | The chaos action to perform (e.g., kill, label, etc.) | string | `` |
| LABEL_SELECTOR | Kubernetes label selector to target worker nodes | string | `node-role.kubernetes.io/worker` |
| EXCLUDE_LABEL | Optional label to exclude from the target set | string | `` |
| NODE_NAME | Specific node name to target | string | `` |
| INSTANCE_COUNT | Number of instances to affect | int | `1` |
| RUNS | Number of times to repeat the chaos experiment | int | `1` |
| CLOUD_TYPE | Cloud provider type (e.g., aws, azure, gcp) | string | `aws` |
| TIMEOUT | Maximum seconds to wait for the experiment before aborting | int | `180` |
| DURATION | Length of the experiment in seconds | int | `120` |
| PARALLEL | Whether to run experiments in parallel across multiple nodes | bool | `False` |
| VERIFY_SESSION | Whether to verify the chaos session is active | bool | `False` |
| SKIP_OPENSHIFT_CHECKS | Whether to skip OpenShift-specific validations | bool | `False` |
| KUBE_CHECK | Whether to perform Kubernetes API checks before execution | bool | `True` |
| DISABLE_SSL_VERIFICATION | Whether to disable SSL certificate verification for API calls | bool | `False` |
| BMC_USER | Username for BMC (Baseboard Management Controller) access | string | `` |
| BMC_PASSWORD | Password for BMC access | string | `` |
| BMC_ADDR | IP address or hostname of the BMC | string | `` |
| DISKS | Disk identifiers to target for I/O chaos | string | `` |
| VSPHERE_IP | vSphere IP address for VM hardware interactions | string | `` |
| VSPHERE_USERNAME | vSphere username for authentication | string | `` |
| VSPHERE_PASSWORD | vSphere password for authentication | string | `` |
| AWS_ACCESS_KEY_ID | AWS access key ID for authentication | string | `` |
| AWS_SECRET_ACCESS_KEY | AWS secret access key for authentication | string | `` |
| AWS_DEFAULT_REGION | Default AWS region for operations | string | `` |
| IBMC_URL | IBM Cloud URL endpoint | string | `` |
| IBMC_POWER_URL | IBM Cloud Power URL | string | `` |
| IBMC_POWER_CRN | IBM Cloud Power CRN identifier | string | `` |
| IBMC_APIKEY | IBM Cloud API key | string | `` |
| AZURE_TENANT_ID | Azure AD tenant ID | string | `` |
| AZURE_CLIENT_SECRET | Azure client secret | string | `` |
| AZURE_CLIENT_ID | Azure client ID | string | `` |
| AZURE_SUBSCRIPTION_ID | Azure subscription ID | string | `` |
| GOOGLE_APPLICATION_CREDENTIALS | Path to Google service account credentials JSON | string | `` |

**NOTE** In case of using custom metrics profile or alerts profile when
`CAPTURE_METRICS` or `ENABLE_ALERTS` is enabled, mount the metrics profile from
the host using podman/docker under `/home/krkn/kraken/config/metrics-aggregated.yaml`.
