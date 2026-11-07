---
title: "Upgrade solution for Apmplus Operator certificate expiration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Repair_and_upgrade_plan_for_expired_Apmplus_Operator_certificates"
---

The Apmplus Operator certificate expired on 2025\-02\-07, which will cause newly created business pods to fail to collect observability data. This topic describes how to upgrade the Apmplus Operator for existing clusters.

<span id="a9b56c30"></span>
## Background

Apmplus Operator can be used for Java pods within VKE clusters to enable automatic injection of observability instrumentation capabilities. When creating pods with specific annotations, the Operator can inject the "javaagent" into them.

Currently, the Apmplus Operator certificate expired on 2025\-02\-07, affecting the automatic injection capability. As a direct result, newly created business pods cannot have the "javaagent" automatically injected, and thus cannot collect observability data for the service.

<span id="7db4fe03"></span>
## Prerequisites

You have already downloaded and installed the latest version of the kubectl tool locally from the official Kubernetes website. For detailed installation instructions, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

<span id="a9f38a88"></span>
## Procedure

For existing clusters that use Apmplus Operator, you can see the following steps to perform the upgrade.

<span id="0aeae057"></span>
### Step 1: Check the deployment status of the apmplus\-operator add\-on

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the current cluster does not have the apmplus\-operator add\-on deployed, it will not be affected by this certificate expiration, and the following upgrade steps are not required.</div>


You can determine whether the apmplus\-operator add\-on is deployed in the current cluster by checking whether the `apmplus-operator-controller-manager` add\-on is deployed in the `apmplus` namespace.


1. Log in to the cluster via kubectl and execute the following command to get the list of cluster namespaces, then check whether a namespace named `apmplus` exists.


```Bash
kubectl get namespace
```



2. Execute the following command to check whether the `apmplus-operator-controller-manager` add\-on is deployed in the `apmplus` namespace.


```Bash
kubectl -n apmplus get po
```


Example result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/167aa79c08e74fa2ad98284446d84a8a~tplv-goo7wpa0wc-image.image) </span>

<span id="4eed00a9"></span>
### Step 2: Obtain the App Key required for APMPlus


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Click **Click to enter service list** to go to the Service management page.

3. In the left navigation pane, select **Integration hub**, specify the workspace, and obtain the App Key from the service integration information.


<span id="d91a6344"></span>
### Step 3: Deploy Apmplus Operator resources

Execute the following command to deploy Apmplus Operator resources in the cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an error occurs when executing the kubectl apply command, it may be caused by dependency issues when deploying resources via YAML files, such as CRD and CR not being handled properly. Repeating the command usually resolves the issue.</div>



* If you deploy via the public network, execute the following command:


```Bash
kubectl apply -f "https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-operator.yaml?appkey={appkey}&network=public"
```



* If you deploy via the private network, execute the following command:


```Bash
kubectl apply -f "http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-operator.yaml?appkey={appkey}&network=private"
```


The above commands contain two variables that need to be replaced with actual values:


|Variable |Description |
|---|---|
|region |The region information of the cluster. Enter the corresponding RegionID based on the actual cluster region, for example, `cn-beijing`, `cn-shanghai`. |
|appkey |The appkey obtained in Step 2. |
