---
title: "Creating CronJobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob"
---

A CronJob is a one\-off task that runs at a specified time or a task that runs periodically. It corresponds to the CronJob in Kubernetes. You can create a CronJob in a cluster by using an image.

## Prerequisites

A container image has been created. You can directly use an image from a third\-party container registry, or upload an image to the Container Registry (CR) service. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

## Creating DaemonSets on the console

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. Click **Workload** \> **CronJob** in the left navigation bar. On the page that appears, click **Create CronJob**.

4. Configure CronJob information. For parameter details, see [Workload configurations](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

5. Click **Confirm** in the lower\-right corner of the page.

## Creating CronJobs by using kubectl

> **tip**

> Before you start creating a CronJob by using kubectl, make sure that the following conditions are met:

* > The kubectl tool has been installed on your on\-premises computer. For details, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

* > The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

1. Create the YAML file of the workload. The code of the `cronjob-demo.yaml` sample file is as follows:

   ```yaml
   apiVersion: batch/v1beta1
   kind: CronJob
   metadata:
     name: cronjob-demo # The CronJob name.
     namespace: default # The namespace to which the CronJob belongs.
   spec:
     schedule: "*/1 * * * *" # The execution time of the CronJob.
     jobTemplate:
       spec:
         template:
           spec:
             containers:
             - name: hello # The name of the container in the CronJob.
               image: busybox # The container image.
               command: # The command executed in the container.
               - /bin/sh
               - -c
               - date; echo Hello from the Kubernetes cluster
               resources:
                 requests:  # Specify CPU and memory requests for the container.
                   cpu: "500m"      
                   memory: "1024Mi"
                 limits:  # The resource quotas, such as the CPU limit, memory limit, and number of RDMA cards.
                   cpu: "1"      
                   memory: "2Gi"
                   vke.volcengine.com/rdma: 2
             restartPolicy: OnFailure # The restart policy when the Job fails in the container. Valid values: Never and OnFailure.
   ```

2. Run the following command to create the workload.

   ```bash
   kubectl apply -f cronjob-demo.yaml
   ```

## Operation result

After you create the CronJob, you can view the status of the workload on the **Workload** \> **CronJob** page. You can click the button in the Actions column to manage the created CronJob. For more operations, see [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments).
