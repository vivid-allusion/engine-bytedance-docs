---
title: "Initializing applications by using init containers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_Init_Containers_to_initialize_an_application"
---

Init containers are a set of specialized containers, which can be executed before application containers in pods start. Init containers can contain utilities or installation scripts not present in an application container during installation. This topic describes the basic usage of the init container.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Init containers can be used in various Kubernetes workloads, such as Deployments, DaemonSets, and Jobs, and are commonly used to perform initialization operations before the main container starts. Init containers are very similar to regular containers in terms of properties and behavior, except for the following two aspects:


* Init containers always run to completion.

* A pod can contain one or more init containers, but each init container must complete successfully before the next one starts. If an init container of a pod fails to be started, the kubelet repeatedly restarts the init container until it succeeds. However, if the pod has a restartPolicy of `Never`, and an init container fails during the startup of the pod, Kubernetes treats the overall pod as failed. To specify an init container for a pod, add the `initContainers` field, which is an array of container\-type objects, residing at the same level and adjacent to the `containers` array for the main container. For more details, see the [Kubernetes official documentation](https://kubernetes.io/zh-cn/docs/concepts/workloads/pods/init-containers/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you create a Deployment by using the kubectl command line interface, make sure that the following preparations are made:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool is installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster is connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting clusters</a>. This topic uses a Deployment as an example to describe how to configure Init containers.</div>


1. Create the YAML file of the workload. The code of the sample file `deployment-demo.yaml` is as follows:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment 
   spec:
     replicas: 1 
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         labels:
           app: nginx
       spec:
         initContainers: # Configure Init containers
         - name: getresource
           image: cr-cn-beijing.volces.com/tw/nginx:1.0 # Init container image address and tag
           command: ['sh', '-c', 'echo This is initContainers information! && sleep 30']
         containers:
         - name: nginx
           image: cr-cn-beijing.volces.com/tw/nginx:1.0 # Main container image address and tag
           ports:
           - containerPort: 80
   ```
   

2. Run the following command to create the workload.

   ```bash
   kubectl apply -f deployment-demo.yaml
   ```
   


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

<span id=".5p-l55yLLWluaXQt5a655Zmo5L-h5oGv"></span>
### View the init container information

After you configure the init container, you can view the status of the init container in the console.


1. Go to the Deployment page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the cluster for which you need to create a Deployment.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. On the Deployment page, click the name of the target workload to go to the workload details page.

3. Click the **List of instances** tab, and click the  **+ ** icon before the instance name to view the status of the Init container.


<span id=".5p-l55yLLWluaXQt5a655Zmo5pel5b-X"></span>
### Viewing init container logs


1. On the Deployment page, click the name of the target workload to go to the workload details page.

2. Click the **Log** tab, and select the corresponding init container from the **Pod/Container** drop\-down list to view the log of the init container.
