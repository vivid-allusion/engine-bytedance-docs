---
title: "Gang scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Gang-scheduling"
---

Vital Kubernetes Engine (VKE) has extended the capabilities of the native kube\-scheduler and now supports Gang scheduling.  This article describes how to trigger and use Gang scheduling.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

Gang scheduling is a scheduling policy in concurrent systems that schedules multiple related processes to run simultaneously on different processors. This prevents the blockage of all related processes due to anomalies in some processes.

The primary principle of Gang scheduling is to ensure that all related processes can start simultaneously and that no abnormal processes are allowed, that is, All\-or\-Nothing. All\-or\-Nothing means that either all processes are started and the batch task runs successfully or if there are any abnormal processes, none of the processes can be started and the batch task fails.

VKE introduces the PodGroup CustomResourceDefinition (CRD) resource to implement Gang scheduling. A PodGroup in VKE consists of a set of related pods that need to be started for batch tasks to match the All\-or\-Nothing principle. To use Gang scheduling in VKE, create a PodGroup with a custom name, specify minimum replicas required for batch tasks to run as expected, and specify a timeout. Then, associate it with your workload by using instance labels.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The scheduler\-plugin add\-on has been installed, and the **Gang scheduling** capability has been enabled. For specific operations, see [scheduler-plugin](https://docs.byteplus.com/en/docs/vke/scheduler-plugin-add-on).

<span id=".5L2_55So5pa55rOV"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXBvZGdyb3VwLWNyZC3otYTmupA="></span>
### Step 1: Create a PodGroup CRD


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane of the VKE console, click **Cluster**.

3. In the cluster list, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**.

5. On the **Resource Explorer** page, click **Create with Yaml** to create a PodGroup CRD resource.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Select <strong>Custom</strong> from the <strong>Type</strong> drop\-down list.   </div>
   

   
   <Tabs>
   <Tab zoneid="jxwY5iYrNb" title="Kubernetes v1.26 and earlier">
   <TabTitle>Kubernetes v1.26 and earlier</TabTitle>
   
   ```YAML
   apiVersion: scheduling.sigs.k8s.io/v1alpha1
   kind: PodGroup
   metadata:
     name: demo-podgroup # The name of the PodGroup.
     namespace: default # The namespace of the PodGroup.
   spec:
     scheduleTimeoutSeconds: 10 # Timeout for waiting for the PodGroup to reach the minimum number of replicas.
     minMember: 4 # The minimum number of replicas required for this PodGroup.
   ```
   
   
   
   </Tab>
   <Tab zoneid="ohFaQhT4Dw" title=" Kubernetes v1.28 and later">
   <TabTitle> Kubernetes v1.28 and later</TabTitle>
   
   ```YAML
   apiVersion: scheduling.x-k8s.io/v1alpha1
   kind: PodGroup
   metadata:
     name: demo-podgroup # The name of the PodGroup.
     namespace: default # The namespace of the PodGroup.
   spec:
     scheduleTimeoutSeconds: 10 # Timeout for waiting for the PodGroup to reach the minimum number of replicas.
     minMember: 4 # The minimum number of replicas required for this PodGroup.
   ```
   
   
   
   </Tab>
   </Tabs>
   

6. Click **Confirm**.

   In the CRD category of the Resource Explorer, view the created PodGroup CRD resource. Click **podgroup** to enter the details page, where you can view the name of the PodGroup.


<span id=".5q2l6aqk5LqM77ya5bel5L2c6LSf6L295Lit5L2_55SoLWdhbmct6LCD5bqm"></span>
### Step 2: Use Gang scheduling on workloads

The following content uses a Deployment as an example.

<span id="jppyzyeR"></span>
#### Use the console


1. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. On the **Deployment** page, create a Deployment or update an existing Deployment. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment) and [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).

   In the **Advanced settings** step, go to the **Instance configuration** section to add an **instance label**.

   * For clusters running Kubernetes v1.26 or earlier, set the label key to `pod-group.scheduling.sigs.k8s.io` and the value to `<PodGroup name>`.

   * For clusters running Kubernetes v1.28 or later, set the label key to `scheduling.x-k8s.io/pod-group` and the value to `<PodGroup name>`.


<span id="IrNXD6mq"></span>
#### Use YAML

The following sample code shows how to configure Gang scheduling by using YAML:


<Tabs>
<Tab zoneid="rPAxcwO64z" title="Kubernetes v1.26 and earlier">
<TabTitle>Kubernetes v1.26 and earlier</TabTitle>

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: worker  # The name of the Deployment.
  namespace: default  # The namespace of the Deployment.
spec:
  replicas: 4  #  The number of replicas for the Deployment. It must be consistent with the minMember of the PodGroup.
  selector:
    matchLabels:
      app: worker
  template:
    metadata:
      labels:
        app: worker
        pod-group.scheduling.sigs.k8s.io: demo-podgroup  # The critical label. It is associated with the created PodGroup.
    spec:
      containers:
      - name: worker
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        resources:
          requests:
            cpu: "2"    # The CPU size requested by a single Pod
```



</Tab>
<Tab zoneid="TboYA6fyay" title=" Kubernetes v1.28 and later">
<TabTitle> Kubernetes v1.28 and later</TabTitle>

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: worker  # The name of the Deployment.
  namespace: default  # The namespace of the Deployment.
spec:
  replicas: 4  #  The number of replicas for the Deployment. It must be consistent with the minMember of the PodGroup.
  selector:
    matchLabels:
      app: worker
  template:
    metadata:
      labels:
        app: worker
        scheduling.x-k8s.io/pod-group: demo-podgroup  # The critical label. It is associated with the created PodGroup.
    spec:
      containers:
      - name: worker
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        resources:
          requests:
            cpu: "2"    # The CPU size requested by a single Pod.
```



</Tab>
</Tabs>


<span id="GfePHzh4"></span>
## Validating results


* If the node resources in the cluster satisfy the resource requests of all Pods in the Deployment, all Pods in the workload will start as expected and enter the **Running** state. You can view the startup status of the Pod on the **List of instances** tab of the workload details page.


If the node resources in the cluster can only satisfy the resource requests of some Pods in the Deployment (for example, only requests of 3 out of 4 Pods can be satisfied), all Pods in the workload will remain in the **Pending** state.
