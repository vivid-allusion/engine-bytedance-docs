---
title: "Use RayHistoryServer to view historical jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_RayHistoryServer_to_view_historical_jobs"
---

Currently, the Ray community does not provide a solution for viewing historical jobs. To address this user pain point, the EMR team has developed the RayHistoryServer component, making it easier for users to view historical jobs. The following describes in detail how to enable and use RayHistoryServer in EMR on VKE.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Currently, RayHistoryServer only supports viewing jobs that have already finished running. For jobs that are still running, you can use the native UI provided by the Ray community to view their status.</div>


* <div data-tips="true" data-tips-type="warning">It is strongly recommended that customers enable RayHistoryServer, especially in scenarios where Ray is used in the RayJob mode. After enabling RayHistoryServer, you can efficiently analyze the reasons for RayJob failures.</div>



<span id="fa7d4c86"></span>
## Enable RayHistoryServer

As shown in the figure above, when selecting the Ray service, it is recommended to enable RayHistoryServer at the same time (by default, it only occupies 1 CU of resources). You also need to provide a TOS address (used to store Ray historical job metadata and log information) and the corresponding AK/SK (AK/SK can be configured to have read and write permissions only for the above TOS).

On the history page, you can find the corresponding cluster entry using the EMR cluster ID and RayCluster name, then click to view the details of historical jobs.

<span id="4935ddde"></span>
## RayHistoryServer\-related configuration

Currently, RayHistoryServer only supports the above configurations. Besides cpu/memory resource configuration, the configuration users are most likely to use is retained_days, which is used to set the validity period for saving historical jobs. The default is 15, meaning the information of historical jobs from the last 15 days will be saved.

<span id="f1b5eeff"></span>
## Excluding special jobs from history recording

After enabling history recording, users may need to exclude certain special jobs from being recorded in RayHistoryServer. This can be achieved by configuring the annotation in the yaml file, as shown below:

```YAML
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  annotations:
    #The following configuration is used to configure certain special jobs not to be recorded by RayHistoryServer
    ray.io/enable-ray-history-server: false 
  labels:
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: kuberay
    helm.sh/chart: ray-cluster-1.0.0
  name: raycluster
spec:
  enableInTreeAutoscaling: false
  headGroupSpec:
    rayStartParams:
    ....
```
