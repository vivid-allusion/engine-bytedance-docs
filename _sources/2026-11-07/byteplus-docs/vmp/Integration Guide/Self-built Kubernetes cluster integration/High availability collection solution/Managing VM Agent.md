---
title: "Managing VM Agent"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Managing-the-VM-Agent"
---

After the VM Agent collector is installed, you can use the deployment script to uninstall the collector and vm\-operator. This topic describes how to uninstall the VM Agent collector and vm\-operator.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you uninstall VM Agent and vm\-operator, first delete VM Agent, and then delete vm\-operator after ensuring the corresponding workload no longer exists.</div>


<span id=".5Y246L29IFZNIEFnZW50"></span>
## Uninstall VM Agent


1. Download the script in your local environment. For more details, refer to [Obtaining the script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to uninstall the VM Agent collector:


```bash
./install.sh uninstall \
--agent vmagent \
--region cn-beijing
```


<span id=".5Y246L29IHZtLW9wZXJhdG9y"></span>
## Uninstall vm\-operator


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to uninstall vm\-operator:


```bash
./install.sh uninstall-operator \
--region cn-beijing \
--namespace volcano-metrics
```


<span id=".5L2_55So5biu5Yqp"></span>
## Use the \-\-help parameter

<span id=".5Y246L29IFZNIEFnZW50IOS9v-eUqOW4ruWKqQ=="></span>
### Use the \-\-help parameter when uninstalling VM Agent

You can view all the predefined fields and their meanings in the script by using the `--help` parameter.

```bash
./install.sh uninstall --help
```


The following section describes the meanings and examples of different fields in the script.

```shell
./install.sh uninstall --help
uninstall agent and system metrics exporter

Usage: install.sh uninstall [flag...]

Flag:
  {{flag}} {{current val if exist}}
  --agent vmagent
  --region cn-beijing
  --exec-script-env local
  --namespace volcano-metrics
  --vmpagent-name vmagent
```



|Parameters |Description |
|---|---|
|\-\-agent |Select the collector to uninstall. The value is fixed as **vmagent**. |
|\-\-region |The region of the VMP workspace, such as cn\-beijing. |
|\-\-exec\-script\-env |The script execution environment, including:<br><br><br>* **local**: the local environment. It indicates that you execute the script in your local environment.<br><br>* **public\-cloud\-vpc**: the VPC. It indicates that you execute the script in the VPC. |
|\-\-namespace |The namespace of Grafana. If you do not specify this parameter, the collector will be deployed in the `volcano-metrics` namespace by default. |
|\-\-vmpagent\-name |The name of the collector. |


<span id=".5Y246L29IHZtLW9wZXJhdG9yIOS9v-eUqOW4ruWKqQ=="></span>
### Use the \-\-help parameter when uninstalling vm\-operator

You can view all the predefined fields and their meanings in the script by using the `--help` parameter.

```bash
./install.sh uninstall-operator --help
```


The following section describes the meanings and examples of different fields in the script.

```Bash
./install.sh uninstall-operator --help
uninstall operator

Usage: install.sh uninstall-operator [flag...]

Flag:
  {{flag}} {{current val if exist}}
  --region cn-beijing
  --exec-script-env local
  --namespace volcano-metrics
```



|Parameters |Description |
|---|---|
|\-\-region |The region of the VMP workspace, such as cn\-beijing. |
|\-\-exec\-script\-env |The script execution environment, including:<br><br><br>* **local**: the local environment. It indicates that you execute the script in your local environment.<br><br>* **public\-cloud\-vpc**: the VPC. It indicates that you execute the script in the VPC. |
|\-\-namespace |The namespace of the collector. If you do not specify this parameter, the collector will be deployed in the `volcano-metrics` namespace by default. |
