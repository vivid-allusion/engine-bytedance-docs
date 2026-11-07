---
title: "Scaling out agents"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Scaling-up-components"
---

As your business develops, the initial number of agent shards that you deployed may not support the increasing volume of business data. The typical issues include the saturation of cluster resources for related agents and the abnormal operational status of containers. In this case, you need to scale out the agents. This topic describes how to scale out agents.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you need to scale out agents, it is recommended to first increase the number of shards for agents such as the VM Agent collector according to the description in this topic. If you need to increase the number of replicas for agents, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Deploying-the-VM-Agent">Deploying VM Agent</a>.</div>


<span id=".Vk0gQWdlbnQg6YeH6ZuG5Zmo5omp5a65"></span>
## Scaling out VM Agent collectors

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">During scale\-out, the rolling update of all VM Agent collectors is performed. If the update takes too long, breakpoints may occur in the monitoring data.</div>


* <div data-tips="true" data-tips-type="warning">When you scale out the VM Agent collector and the kube\-state\-metrics agent, it is recommended to specify the number of shards for the kube\-state\-metrics agent as an integer multiple of the number of shards for the VM Agent collector to ensure load balancing. For example, maintain a 1:1 or 2:1 ratio of <strong>the number of shards for the kube\-state\-metrics agent to the number of shards for the VM Agent collector</strong>.</div>



You can quickly scale out the VM Agent collector by using the deployment script. Procedure:


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to scale out the VM Agent collector:


```bash
./install.sh scale \
--namespace volcano-metrics \# The namespace where the collector is located.
--workload vmagent \ # The name of the agent to be scaled-out. In this example, the name is VM Agent.
--shards 3 # The number of shards after scale-out. You can adjust the value based on your business requirements.
```


<span id=".a3ViZS1zdGF0ZS1tZXRyaWNzIOe7hOS7tuaJqeWuuQ=="></span>
## Scaling out kube\-state\-metrics agents

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">During the scale\-out, the existing replicas of the kube\-state\-metrics agent will be sharded again before the new replicas are ready. Therefore, if the update takes too long, breakpoints may occur in the monitoring data. We recommend performing this operation during off\-peak data periods.</div>


* <div data-tips="true" data-tips-type="warning">When you scale out the VM Agent collector and the kube\-state\-metrics agent, it is recommended to specify the number of shards for the kube\-state\-metrics agent as an integer multiple of the number of shards for the VM Agent collector to ensure load balancing. For example, maintain a 1:1 or 2:1 ratio of <strong>the number of shards for the kube\-state\-metrics agent to the number of shards for the VM Agent collector</strong>.</div>



You can quickly scale out the kube\-state\-metrics agent by using the deployment script. Procedure:


1. Download the script in your local environment. For more details, refer to [Obtaining a script](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the Kubernetes cluster.

3. Run the following command to scale out the kube\-state\-metrics agent:


```bash
./install.sh scale \
--namespace volcano-metrics \# The namespace where the add-on is located.
--workload kube-state-metrics \ # The name of the agent to be scaled-out. In this example, the name is kube-state-metrics.
--shards 3 # The number of shards after scale-out. You can adjust the value based on your business requirements.
```


<span id=".5L2_55So5biu5Yqp"></span>
## Use the \-\-help parameter

You can view all the predefined fields and their meanings in the installation script by using the `--help` parameter.

```bash
./install.sh scale --help
```


The following section describes the meanings and examples of different fields in the installation script.

```Plain Text
./install.sh scale --help
scale set a new shards for a workload (vmagent or kube-state-metrics)

Usage: install.sh scale [flag...]

Examples:
  * scale shards of vmagent under the volcano-metrics namespace to 3
      ./install.sh scale --workload vmagent --shards 3
  * scale shards of kube-state-metrics under the monitoring namespace to 3
      ./install.sh scale --workload kube-state-metrics --shards 3 --namespace monitoring

Flag:
  {{flag}} {{current val if exist}}
  --workload vmagent
  --shards 3
  --namespace volcano-metrics
```



|Parameters |Description |
|---|---|
|\-\-workload |Select the agent to scale out. Available options include vmagent and kube\-state\-metrics. |
|\-\-shards |Specify the number of shards after scale\-out. |
|\-\-namespace |Select the namespace of the agent. |
