---
title: "Creating StatefulSets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet"
---

A StatefulSet in Kubernetes is a workload that preserves data or state. For example, a MySQL StatefulSet saves the data that is written to it. You can create a StatefulSet in a cluster by using an image. This topic describes how to create a StatefulSet.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A container image has been created. You can directly use an image from a third\-party container registry, or upload an image to the Container Registry (CR) service. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

<span id=".6YCa6L-H5o6n5Yi25Y-w5Yib5bu6"></span>
## Use the console


1. Go to the StatefulSet page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the cluster for which you need to create a StatefulSet.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **StatefulSet**.

2. On the StatefulSet page, click **Create StatefulSet**.

3. Configure the StatefulSet. For parameter details, see [Workload configurations](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

4. Click **Confirm** in the lower\-right corner of the page.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5Yib5bu6"></span>
## Use kubectl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create the YAML file of the workload. The following example is a file named `statefulset-demo.yaml`:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: statefulset-demo     # The headless service name.
     labels:
       app: demo
   spec:
     ports:
     - port: 80                 # The port number for communication between pods.
       name: web                # The port name for communication between pods.
     clusterIP: None            # For a headless service, it needs to be None.
     selector:
       app: demo    # Select pods with the key:value label.
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: statefulset-demo # The StatefulSet name.
     namespace: default # The namespace where the StatefulSet is located.
   spec:
     replicas: 2 # The number of StatefulSet replicas.
     serviceName: statefulset-demo # The headless service name.
     selector:
       matchLabels:
         app: demo
     template:
       metadata:
         labels:
           app: demo
       spec:
         containers:
         - name: nginx # The container name.
           image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
           ports:
           - containerPort: 80 # The exposed port number of the container.
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
   kubectl apply -f statefulset-demo.yaml
   ```
   


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

You can click **Workload** \> **StatefulSet** to check the status of the workload. You can click the button in the Actions column to manage the created StatefulSets. For more operations, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).
