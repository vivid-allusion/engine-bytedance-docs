---
title: "Deploying VM Agent"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Deploying-the-VM-Agent"
---

To use a high\-availability collection solution, you need to first deploy the VM Agent collector in the target cluster. This topic describes the basic concepts, deployment procedure, and parameter configuration of the VM Agent collector in detail.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">VM Agent is a native version of VictoriaMetrics and does not support AK/SK authentication of .</div>


* <div data-tips="true" data-tips-type="warning">If you use a VKE cluster, we recommend using the <strong>add\-on management</strong> feature in clusters to install collectors and add\-ons. For more details, see <a href="https://docs.byteplus.com/en/docs/vmp/cluster-monitoring">VKE integration</a>.</div>



<span id=".5qaC6L-w"></span>
## Overview

<span id=".6auY5Y-v55So5oCn6K-05piO"></span>
### High availability description

The VM Agent collector comes with an operator, which achieves sharding and data collection for the collector and the kube\-state\-metrics add\-on, achieving high performance and availability.

<span id=".57uE5Lu26K-05piO"></span>
### Agent description

When you install the VM Agent collector in the cluster, the vm\-operator, kube\-state\-metrics, and node\-exporter add\-ons are also installed. The following table describes the name, type, and feature of each agent.


|Agent Name |Workload Type |Namespace |Description |
|---|---|---|---|
|vmagent |StatefulSet |volcano\-metrics |Collects metrics exposed by kubelet, kubelet\-cadvisor, kube\-state\-metrics, and node\-exporter in the cluster. |
|vm\-operator |Deployment |volcano\-metrics |The controlling agent of VM Agent. |
|kube\-state\-metrics |StatefulSet |volcano\-metrics |Provides the metric data of Kubernetes resources. |
|node\-exporter |DaemonSet |volcano\-metrics |Provides the metric data of node resources. |


VM Agent serves as a data collection agent of Vital Managed Service for Prometheus (VMP). It scrapes monitoring data of monitoring targets and sends the data to VMP for storage. By default, the monitoring data includes the data of node\-exporter, kubelet metrics/cadvisor, kubelet metrics, kube\-state\-metrics, and the agent itself.

<span id=".6buY6K6k6KeE5qC8"></span>
### Default specifications

The following table shows the default instance specifications of the add\-ons related to the VM Agent collector.


|<div style="text-align: center"><br><strong>Agent Name</strong></div><br> |<div style="text-align: center"><br><strong>Default CPU Request</strong></div><br> |<div style="text-align: center"><br><strong>Default Memory Request</strong></div><br> |<div style="text-align: center"><br><strong>Default CPU Upper Limit</strong></div><br> |<div style="text-align: center"><br><strong>Default Memory Upper Limit</strong></div><br> |
|---|---|---|---|---|
|<div style="text-align: center"><br>vmagent</div><br> |<div style="text-align: center"><br>2 core</div><br> |<div style="text-align: center"><br>2 GiB</div><br> |<div style="text-align: center"><br>4 core</div><br> |<div style="text-align: center"><br>4 GiB</div><br> |
|<div style="text-align: center"><br>kube\-state\-metrics</div><br> |<div style="text-align: center"><br>0.2 Core</div><br> |<div style="text-align: center"><br>512 MiB</div><br> |<div style="text-align: center"><br>0.8 core</div><br> |<div style="text-align: center"><br>2 GiB</div><br> |
|<div style="text-align: center"><br>node\-exporter</div><br> |<div style="text-align: center"><br>0.05 core</div><br> |<div style="text-align: center"><br>128 MiB</div><br> |<div style="text-align: center"><br>0.1 core</div><br> |<div style="text-align: center"><br>256 MiB</div><br> |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A self\-managed Kubernetes cluster is created,  a virtual private cloud (VPC) is connected to an Internet data center (IDC) through methods such as .

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* When you use the script to install VM Agent, you need to use wget, echo, curl, and sed in your local environment (Linux/Mac). Ensure that these command\-line tools are installed on your system.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The VM Agent collector cannot be used together with the prometheus\-agent add\-on in the VKE cluster. Before you deploy the VM Agent collector, make sure that the prometheus\-agent add\-on is not installed in your cluster. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/cluster-monitoring">VKE integration</a>.</div>


<span id=".6YOo572y5a6e5L6L77yI6buY6K6k6YWN572u77yJ"></span>
## Deploy the instance (default configuration)

You can use the deployment script to quickly deploy the VM Agent collector. You can perform the following steps to deploy the default configurations:


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to deploy the VM Agent collector:


```bash
./install.sh \
--agent vmagent \ # The collector type.
--region cn-beijing \ # The region of the VMP workspace.
--remote-write-url http://write.prometheus-cn-beijing.ivolces.com/workspaces/b762e1a3-37***/api/v1/write \ # The Remote Write URL of the VMP workspace, with the api/v1/write suffix added.
--namespace volcano-metrics \ # The namespace of the collector.
--basic-auth-username username-demo \ # The username for authentication in Basic Auth mode of the VMP workspace.
--basic-auth-password password-demo  # The password for authentication in Basic Auth mode of the VMP workspace.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Modify the <code>region</code>, <code>remote-write-url</code>, <code>namespace</code>, <code>basic-auth-username</code>, and <code>basic-auth-password</code> parameters in the preceding configuration based on your business requirements.</div>


<span id=".6YOo572y5a6e5L6L77yI6Ieq5a6a5LmJ6YWN572u77yJ"></span>
## Deploy the instance (custom configuration)

If the default specification of the collector cannot meet your business requirements, you can use predefined parameters in the deployment script to modify the instance configuration (such as the CPU and memory capacity of the collector) before deployment. Procedure:


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to modify parameters and deploy the VM Agent collector:


```bash
./install.sh \
--region cn-beijing \ # The region of the VMP workspace.
--remote-write-url http://write.prometheus-cn-beijing.ivolces.com/workspaces/b762e1a3-37***/api/v1/write \ # The URL of the VMP workspace, with the api/v1/write suffix added.
--basic-auth-username username-demo \ # The username for authentication in Basic Auth mode of the VMP workspace.
--basic-auth-password password-demo \ # The password for authentication in Basic Auth mode of the VMP workspace.
--agent vmagent \ # The collector type.
--namespace volcano-metrics \ # The namespace of the collector.
--agent-scrape-interval 15s \ # The data collection interval for the collector.
--vmagent-replicas 1 \ # The number of replicas for the VM Agent collector.
--vmagent-shards 2 \ # The number of shards for the VM Agent collector.
--vmagent-resources-requests-cpu 100m \ # The CPU request value for the VM Agent collector.
--vmagent-resources-requests-memory 200Mi \ # The memory request value for the VM Agent collector.
--vmagent-resources-limits-cpu 100m \ # The CPU upper limit for the VM Agent collector.
--vmagent-resources-limits-memory 200Mi \ # The memory upper limit for the VM Agent collector.
--kube-state-metrics-shards 2 \ # The number of shards for the kube-state-metrics agent.
--kube-state-metrics-resources-requests-cpu 50m \ # The CPU request value for kube-state-metrics.
--kube-state-metrics-resources-requests-memory 100Mi \ # The memory request value for kube-state-metrics.
--kube-state-metrics-resources-limits-cpu 50m \ # The CPU upper limit for kube-state-metrics.
--kube-state-metrics-resources-limits-memory 100Mi # The memory upper limit for kube-state-metrics.
```


<span id=".6YOo572y5a6e5L6L77yI6Ieq5a6a5LmJ5Y-C5pWw77yJ"></span>
## Deploy the instance (custom parameters)

If the predefined parameters in the deployment script cannot meet your business requirements, you can perform the following steps to specify custom parameters:


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following commands to specify your custom parameters and generate the install.yaml configuration file:


```bash
./install.sh \
--region cn-beijing \
--remote-write-url http://write.prometheus-cn-beijing.ivolces.com/workspaces/b762e1a3-37***/api/v1/write \
--basic-auth-username username-demo \
--basic-auth-password password-demo \
--agent vmagent \
--rendering-only > install.yaml
```



4. Open the install.yaml file, specify relevant parameters, and save the file.


```bash
vim install.yaml
```



5. Run the following command to deploy the related agents:


```bash
kubectl apply -f install.yaml
```


<span id=".5qOA5p-l57uT5p6c"></span>
## Check the result

After VM Agent is deployed, log in to the cluster and you can view the workloads of vm\-operator in the list of Deployments. In the list of StatefulSets, you can view the workloads of VM Agent and kube\-state\-metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To ensure that the collector can collect data as expected, you need to make sure that the collector runs as expected and the metrics API or the exporter of the collection target is functioning correctly. You must complete the related configuration and deployment, and ensure they are configured correctly.</div>


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After you deploy the collector, in addition to the default collection rules, you can also use ServiceMonitor or PodMonitor to configure collection rules for custom targets. For more details, refer to [Service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery).

<span id=".5L2_55So5biu5Yqp"></span>
## Use the \-\-help parameter

You can view all the predefined fields and their meanings in the installation script by using the `--help` parameter.

```bash
./install.sh install --help
```


The following section describes the meanings and examples of different fields in the installation script.

```bash
./install.sh install --help
install agent and system metrics exporter. if it is VM Agent, vmoperator will also be installed

Usage: install.sh install [flag...]

Flag:
  {{flag}} {{current val if exist}}
  --agent vmagent
  --remote-write-url http://write.prometheus-cn-beijing.com/workspace/b762e1a3-37***/api/v1/write
  --basic-auth-username username-demo
  --basic-auth-password password-demo
  --access-key TDOSNQG***
  --secret-key YvT3ing***
  --region cn-beijing
  --exec-script-env local
  --rendering-only
  --namespace volcano-metrics
  --topology-key-zone topology.kubernetes.io/zone
  --topology-key-node kubernetes.io/hostname
  --storage-class 
  --kube-state-metrics-shards 1
  --kube-state-metrics-resources-requests-cpu 100m
  --kube-state-metrics-resources-requests-memory 250Mi
  --kube-state-metrics-resources-limits-cpu 500m
  --kube-state-metrics-resources-limits-memory 1Gi
  --agent-scrape-interval 15s
  --vmpagent-name vmpagent
  --vmpagent-replicas 1
  --vmpagent-pvc-capacity
  --vmpagent-resources-requests-cpu 500m
  --vmpagent-resources-requests-memory 1Gi
  --vmpagent-resources-limits-cpu 2
  --vmpagent-resources-limits-memory 4Gi
  --vmagent-replicas 1
  --vmagent-shards 2
  --vmagent-pvc-capacity
  --vmagent-resources-requests-cpu 200m
  --vmagent-resources-requests-memory 400Mi
  --vmagent-resources-limits-cpu 1
  --vmagent-resources-limits-memory 2Gi
  --disable-cadvisor
  --cadvisor-only
  --disable-install-node-exporter
```



|Parameters |Description |
|---|---|
|\-\-agent |Select the collector to deploy. The value is fixed as **vmagent**. |
|\-\-remote\-write\-url |The remote write URL of the VMP workspace. For details, see [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). |
|\-\-basic\-auth\-username |The username for authentication in Basic Auth mode of the VMP workspace. |
|\-\-basic\-auth\-password |The password for authentication in Basic Auth mode of the VMP workspace. |
|\-\-region |The region of the collector cluster, such as cn\-beijing. For more details, refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones). |
|\-\-exec\-script\-env |The script execution environment, including:<br><br><br>* **local**: the local environment. It indicates that you execute the script in your local environment.<br><br>* **public\-cloud\-vpc**: the VPC. It indicates that you execute the script in the VPC. |
|\-\-rendering\-only |You can only view the installation list of add\-ons, such as VM Agent and vm\-operator, and do not install the add\-ons. |
|\-\-namespace |The namespace of the collector. If you do not specify this parameter, the collector will be deployed in the `volcano-metrics` namespace by default. |
|\-\-storage\-class |The PersistentVolumeClaim (PVC) storage type. |
|\-\-kube\-state\-metrics\-shards |The number of shards for the kube\-state\-metrics agent. |
|\-\-kube\-state\-metrics\-resources\-requests\-cpu |The CPU request of kube\-state\-metrics. The value must be an integer. Unit: m. For example, 100m indicates a CPU request of 100 millicores. |
|\-\-kube\-state\-metrics\-resources\-requests\-memory |The memory request of kube\-state\-metrics. The value must be an integer. Unit: Mi. For example, 200Mi indicates a memory request of 200 MB. |
|\-\-kube\-state\-metrics\-resources\-limits\-cpu |The CPU upper limit of kube\-state\-metrics. The value must be an integer. Unit: m. For example, 100m indicates a maximum value of 100 millicores. |
|\-\-kube\-state\-metrics\-resources\-limits\-memory |The memory upper limit of the kube\-state\-metrics collector. The value must be an integer. Unit: Mi. For example, 200Mi indicates a maximum value of 200 MB. |
|\-\-agent\-scrape\-interval |The data collection interval of the collector. The value must be an integer in seconds. Example: 15 seconds. |
|\-\-vmpagent\-name |The name of the VMP Agent collector. |
|\-\-vmpagent\-replicas |The number of replicas for the VMP Agent collector. |
|\-\-vmpagent\-pvc\-capacity |The storage capacity of the VMP Agent collector. |
|\-\-vmpagent\-resources\-requests\-cpu |The CPU request of the VMP Agent collector. The value must be an integer. Unit: m. For example, 100m indicates a CPU request of 100 millicores. |
|\-\-vmpagent\-resources\-requests\-memory |The memory request of the VMP Agent collector. The value must be an integer. Unit: Mi. For example, 200Mi indicates a memory request of 200 MB. |
|\-\-vmpagent\-resources\-limits\-cpu |The CPU upper limit of the VMP Agent collector. The value must be an integer. Unit: m. For example, 100m indicates a maximum value of 100 millicores. |
|\-\-vmpagent\-resources\-limits\-memory |The memory upper limit of the VMP Agent collector. The value must be an integer. Unit: Mi. For example, 200Mi indicates a maximum value of 200 MB. |
|\-\-vmagent\-replicas |The number of replicas for the VM Agent collector. |
|\-\-vmagent\-shards |The number of shards for the VM Agent collector. |
|\-\-vmagent\-pvc\-capacity |The storage capacity of the VM Agent collector. |
|\-\-vmagent\-resources\-requests\-cpu |The CPU request of the VM Agent collector. The value must be an integer. Unit: m. For example, 100m indicates a CPU request of 100 millicores. |
|\-\-vmagent\-resources\-requests\-memory |The memory request of the VM Agent collector. The value must be an integer. Unit: Mi. For example, 200Mi indicates a memory request of 200 MB. |
|\-\-vmagent\-resources\-limits\-cpu |The CPU upper limit of the VM Agent collector. The value must be an integer. Unit: m. For example, 100m indicates a maximum value of 100 millicores. |
|\-\-vmagent\-resources\-limits\-memory |The memory upper limit of the VM Agent collector. The value must be an integer. Unit: Mi. For example, 200Mi indicates a maximum value of 200 MB. |
|\-\-disable\-cadvisor |Disables the rule that allows VMP Agent to collect the metrics of cAdvisor. |
|\-\-cadvisor\-only |Only enables the rule that allows VMP Agent to collect the metrics of cAdvisor. |
|\-\-disable\-install\-node\-exporter |Disables the rule that allows VMP Agent to collect the metrics of node\-exporter. |
