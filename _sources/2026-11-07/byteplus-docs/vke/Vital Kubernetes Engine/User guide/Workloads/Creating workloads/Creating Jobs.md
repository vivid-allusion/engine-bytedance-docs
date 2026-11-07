---
title: "Creating Jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-Job"
---

A Job refers to a one\-off task that runs after deployment and stops upon successful execution. It corresponds to the Job in Kubernetes. You can create a Job in a cluster by using an image.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A container image has been created. You can directly use an image from a third\-party container registry, or upload an image to the Container Registry (CR) service. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

<span id=".6YCa6L-H5o6n5Yi25Y-w5Yib5bu6"></span>
## Use the console


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click **Workload** \> **Job** in the left navigation bar. On the page that appears, click **Create Job**.

4. Configure the Job based on the on\-screen prompts. For parameter details, see [Workload configurations](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

5. Click **Confirm** in the lower\-right corner of the page.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5Yib5bu6"></span>
## Use kubectl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start creating a Job by using kubectl, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create the YAML file of the workload. The code of the `job-demo.yaml` sample file is as follows:

   ```yaml
   apiVersion: batch/v1
   kind: Job
   metadata:
     name: job-demo # The Job name.
     namespace: default # The namespace to which the Job belongs.
   spec:
     template:
       spec:
         containers:
         - name: pi # The container name.
           image: perl # The container image.
           command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"] # The command executed in the container.
           resources:
             requests:  # Specify CPU and memory requests for the container.
               cpu: "500m"      
               memory: "1024Mi"
             limits:  # Specify resource quotas, such as the CPU limit, memory limit, and number of RDMA cards.
               cpu: "1"      
               memory: "2Gi"
               vke.volcengine.com/rdma: 2
         restartPolicy: Never # The restart policy when the Job fails in the container. Valid values: Never and OnFailure.
     backoffLimit: 4 # The number of retries after the Job fails in the container.
   ```
   

2. Run the following command to create the workload.

   ```bash
   kubectl apply -f job-demo.yaml
   ```
   


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After the Job is created, you can view the status of the workload on the **Workload** \> **Job** page. You can click the button in the Actions column to manage the created Job. For more operations, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).
