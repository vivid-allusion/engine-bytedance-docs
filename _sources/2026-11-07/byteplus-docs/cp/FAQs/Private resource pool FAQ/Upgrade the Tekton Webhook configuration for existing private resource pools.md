---
title: "Upgrade the Tekton Webhook configuration for existing private resource pools"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Upgrade_the_Tekton_Webhook_configuration_for_existing_private_resource_pools"
---

For private resource pools created before June 8, 2022, 20:00:00, it is recommended that you upgrade the Tekton Webhook configuration by following the steps below to improve the response speed when pipelines run multiple concurrent tasks.

You need to connect to the cluster using kubectl, adjust the CPU and memory limits in the `resource.limit` section under the deployment webhook to 2C4G, adjust the hpa targetAverageUtilization to 60%, and adjust the maxReplicas to 5. Specific operations are as follows:


1. Run the following command to enter edit mode, locate the limits parameter under `deployment tekton-pipelines/tekton-pipelines-webhook`, set the CPU to `"2"` and memory to `4Gi`, then save and exit.


```shell
kubectl -n cp-system edit deploy tekton-pipelines-webhook

//  After entering the edit mode, please find and modify the following parameters.
    deployment tekton-pipelines/tekton-pipelines-webhook
    limits:
        cpu: "2" 
        memory: 4Gi
```



2. Execute the following command to set hpa targetAverageUtilization to `60%` and maxReplicas to`5`.


```shell
kubectl -n cp-system patch hpa tekton-pipelines-webhook -p '{"spec":{"maxReplicas":5,"targetCPUUtilizationPercentage":60}}' --type=merge             

// After executing the command, you can check whether the modifications are correct by comparing them against the following results.
hpa tekton-pipelines/tekton-pipelines-webhook
   maxReplicas: 5
   minReplicas: 1
   scaleTargetRef:
     apiVersion: apps/v1
     kind: Deployment
     name: tekton-pipelines-webhook
   targetCPUUtilizationPercentage: 60
```
