---
title: "Using the script"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Script-use-guide"
---

The deployment script is used to deploy collectors, Grafana, and the kube\-state\-metrics add\-on in self\-built Kubernetes clusters. This topic describes the basic usage of the deployment script.

<span id=".5Z-65pys5L2_55So5pa55rOV"></span>
## Basic usage

After you obtain the deployment script, you can use the script in the following format:

```bash
./install.sh ${command} ${flag}
```


For example, you can run the following command to install the VM Agent collector and the corresponding exporter:

```bash
./install.sh --agent vmagent --region cn-beijing --remote-write-url http://write.prometheus-cn-beijing.ivolces.com/workspaces/b762e1a3-37***/api/v1/write --basic-auth-username username-demo --basic-auth-password password-demo
```


You can also use the following format for better clarity:

```bash
./install.sh \
--agent vmagent \
--region cn-beijing \
--remote-write-url http://write.prometheus-cn-beijing.ivolces.com/workspaces/b762e1a3-37***/api/v1/write  \
--basic-auth-username username-demo \
--basic-auth-password password-demo
```


The `${command}` field consists of the following commands:


|Command |Description |
|---|---|
|install |Deploy the collector and the corresponding exporter. When you deploy the VM Agent collector, vm\-operator is also deployed automatically.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">install is the default value. If you do not specify the <code>${command}</code> field, the install command will be run by default.</div><br> |
|uninstall |Uninstall the collector and the corresponding exporter. |
|uninstall\-operator |Uninstall vm\-operator. |
|scale |Scale out the VM Agent collector and the kube\-state\-metrics add\-on. |
|install\-grafana |Deploy Grafana. |
|uninstall\-grafana |Uninstall Grafana. |
|fetchall |Download the native Kubernetes configurations of all resources. You can modify the configurations and then deploy the resources. |
|clear |Delete all local native Kubernetes resource configurations. |


<span id=".5LiL6L296LWE5rqQ6YWN572u5riF5Y2V"></span>
## Download resource configurations

You can run the `fetchall` command to download the native Kubernetes configurations of all resources.

```Bash
./install.sh fetchall \
--exec-script-env local \ # (Optional) The script execution environment. local: local environment; public-cloud-vpc: VPC environment.
--region cn-beijing # The region of the cluster where the add-on is deployed.
```


<span id=".5riF55CG6LWE5rqQ6YWN572u5riF5Y2V"></span>
## Clear configurations

You can run the `clear` command to clear the local resource configurations.

```Bash
./install.sh clear
```


<span id=".5L2_55So5biu5Yqp"></span>
## Use the \-\-help parameter

You can view all the predefined fields and their meanings in the installation script by using the `--help` parameter.

```Bash
./install.sh --help
```
