
```bash
krknctl run node-scenarios [--<parameter> <value>]
```

Can also set any global variable listed [here](../all-scenario-env-krknctl.md)


Scenario specific parameters:  (be sure to scroll to right)
| Parameter      | Description    | Type      | Required |  Default | Possible Values | 
| ----------------------- | ----------------------    | ------------------  | :------: | ------------------------------------ | :----------------:  | 
<!-- AUTO:START id="params" -->
| ACTION | User-defined action to perform. | string | `` |
| LABEL_SELECTOR | Kubernetes label selector for worker nodes. | string | `node-role.kubernetes.io/worker` |
| EXCLUDE_LABEL | Label to exclude from the target set. | string | `` |
| NODE_NAME | Specific node name to target. | string | `` |
| INSTANCE_COUNT | Number of instances to target. | int | `1` |
| RUNS | Number of times to run the scenario. | int | `1` |
| KUBE_CHECK | Enable Kubernetes health check after actions. | bool | `True` |
| PARALLEL | Run the scenario in parallel mode. | bool | `False` |
| CLOUD_TYPE | Cloud provider type being used. | string | `aws` |
| TIMEOUT | Timeout duration in seconds before aborting. | int | `180` |
| DURATION | Duration of the chaos injection in seconds. | int | `120` |
| VSPHERE_IP | vSphere IP address for connection. | string | `` |
| VSPHERE_USERNAME | vSphere username for authentication. | string | `` |
| VSPHERE_PASSWORD | vSphere password for authentication. | string | `` |
| AWS_ACCESS_KEY_ID | AWS access key identifier. | string | `` |
| AWS_SECRET_ACCESS_KEY | AWS secret access key. | string | `` |
| AWS_DEFAULT_REGION | Default AWS region for operations. | string | `` |
| BMC_USER | BMC user name for IPMI connection. | string | `` |
| BMC_PASSWORD | BMC password for IPMI connection. | string | `` |
| BMC_ADDR | BMC address for IPMI connection. | string | `` |
| DISABLE_SSL_VERIFICATION | Disable SSL verification for TLS connections. | bool | `False` |
| AZURE_TENANT_ID | Azure tenant identifier. | string | `` |
| AZURE_CLIENT_SECRET | Azure client secret for authentication. | string | `` |
| AZURE_CLIENT_ID | Azure client ID for authentication. | string | `` |
| AZURE_SUBSCRIPTION_ID | Azure subscription identifier. | string | `` |
| GOOGLE_APPLICATION_CREDENTIALS | Path to Google service account credentials file. | string | `` |
<!-- AUTO:END id="params" -->
`--action` | action performed on the node, visit https://github.com/krkn-chaos/krkn/blob/main/docs/node_scenarios.md for more infos | enum | Yes |  | node_start_scenario,node_stop_scenario,node_stop_start_scenario,node_termination_scenario,node_reboot_scenario,stop_kubelet_scenario,stop_start_kubelet_scenario,restart_kubelet_scenario,node_crash_scenario,stop_start_helper_node_scenario | 
`--label-selector` | Node label to target | string | No | node-role.kubernetes.io/worker | 
`--exclude-label` | excludes nodes marked by this label from chaos | string | No |
`--node-name` | Node name to inject faults in case of targeting a specific node; Can set multiple node names separated by a comma | string | No | 
`--instance-count` | Targeted instance count matching the label selector | number | No | 1 | 
`--runs` | Iterations to perform action on a single node | number | No | 1 | 
`--cloud-type` | Cloud platform on top of which cluster is running, supported platforms - aws, azure, gcp, vmware, ibmcloud, bm | enum | No | aws | 
`--kube-check` | Connecting to the kubernetes api to check the node status, set to False for SNO | enum | No | true | 
`--timeout` | Duration to wait for completion of node scenario injection | number | No | 180| 
`--duration` | Duration to wait for completion of node scenario injection | number | No | 120 | 
`--vsphere-ip` | vSphere IP address | string | No | 
`--vsphere-username` | vSphere IP address | string (secret)| No | 
`--vsphere-password` | vSphere password | string (secret)| No | 
`--aws-access-key-id` | AWS Access Key Id | string (secret)| No | 
`--aws-secret-access-key` | AWS Secret Access Key | string (secret)| No | 
`--aws-default-region` | AWS default region | string | No | 
`--bmc-user` | Only needed for Baremetal ( bm ) - IPMI/bmc username | string(secret) | No | 
`--bmc-password` | Only needed for Baremetal ( bm ) - IPMI/bmc password | string(secret) | No | 
`--bmc-address` | Only needed for Baremetal ( bm ) - IPMI/bmc address | string | No | 
`--ibmc-address` | IBM Cloud URL | string | No | 
`--ibmc-api-key` | IBM Cloud API Key | string (secret)| No | 
`--ibmc-power-address` | IBM Power Cloud URL | string | No | 
`--ibmc-cnr` | IBM Cloud Power Workspace CNR | string | No | 
`--disable-ssl-verification` | Disable SSL verification, to avoid certificate errors | enum | Yes | false |
`--azure-tenant` | Azure Tenant | string | No | 
`--azure-client-secret` | Azure Client Secret | string(secret) | No | 
`--azure-client-id` | Azure Client ID | string(secret) | No | 
`--azure-subscription-id` | Azure Subscription ID | string (secret)| No | 
`--gcp-application-credentials` | GCP application credentials file location | file | No | 

NOTE: The secret string types will be masked when scenario is ran

#### Parameter Dependencies

- **`--node-name` vs `--label-selector`:** When `--node-name` is set, `--label-selector` is ignored. The scenario targets the named node(s) directly.
- **`--instance-count`:** Only applies when using `--label-selector`. It limits how many of the matched nodes are targeted.
- **Cloud credentials:** The `--vsphere-*`, `--aws-*`, `--bmc-*`, `--ibmc-*`, `--azure-*`, and `--gcp-*` parameters are only required for their respective `--cloud-type` value. For example, `--aws-access-key-id` is only needed when `--cloud-type` is `aws`.

To see all available scenario options 
```bash
krknctl run node-scenarios --help
```