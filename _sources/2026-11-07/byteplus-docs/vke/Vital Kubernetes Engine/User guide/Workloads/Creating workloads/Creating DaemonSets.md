---
title: "Creating DaemonSets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet"
---

A DaemonSet ensures that exactly one pod runs on each eligible node in a cluster. DaemonSets are suitable for system\-level applications, such as log collection and resource monitoring. DaemonSets can effectively ensure the availability of basic services in clusters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A container image has been created. You can directly use an image from a third\-party container registry, or upload an image to the Container Registry (CR) service. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

<span id=".6YCa6L-H5o6n5Yi25Y-w5Yib5bu6"></span>
## Creating DaemonSets on the console


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click **Workload** \> **DaemonSet**. On the page that appears, click **Create DaemonSet**, and then configure the DaemonSet.

4. Configure DaemonSet information. For parameter details, see [Workload configurations](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

5. Click **Confirm** in the lower\-right corner of the page.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5Yib5bu6"></span>
## Creating DaemonSets by using kubectl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start creating a DaemonSet by using kubectl, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create the YAML file of the workload. The code of the sample file `daemonset-demo.yaml` is as follows:

   ```yaml
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
     name: daemonset-demo # The name of the DaemonSet.
     namespace: default # The namespace of the DaemonSet.
   spec:
     selector:
       matchLabels:
         app: demo
     template:
       metadata:
         labels:
           app: demo
       spec:
         containers:
         - name: nginx # The name of the container.
           image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
           ports:
           - containerPort: 80 # The exposed port of the container.
           resources:
             requests:  # The container CPU and memory requests.
               cpu: "500m"      
               memory: "1024Mi"
             limits:  # The resource quotas, such as the CPU limit, memory limit, and number of RDMA cards.
               cpu: "1"      
               memory: "2Gi"
               vke.volcengine.com/rdma: 2
   ```
   

2. Run the following command to create the workload.

   ```bash
   kubectl apply -f daemonset-demo.yaml
   ```
   


<span id=".5pON5L2c57uT5p6c"></span>
## Results

After you create the DaemonSet, you can view the status of the workload on the **Workload** \> **DaemonSet** page. You can click the button in the Actions column to manage the created DaemonSet. For more operations, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).
